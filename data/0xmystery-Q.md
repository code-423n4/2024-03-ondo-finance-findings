## [L-01] Front-running attacks in rOUSG allowance management
Decreasing an ERC20 token allowance via the `approve` function can unwittingly expose transactions to front-running attacks, where malicious actors exploit the delay between transaction submission and confirmation to their advantage. In such scenarios, a spender could detect a pending decrease in their allowance and quickly utilize the existing higher allowance before the approve transaction is confirmed, often by submitting their transaction with a higher gas fee for priority processing. 

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L251-L254

```solidity
  function approve(address _spender, uint256 _amount) public returns (bool) {
    _approve(msg.sender, _spender, _amount);
    return true;
  }
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L472-L482

```solidity
  function _approve(
    address _owner,
    address _spender,
    uint256 _amount
  ) internal whenNotPaused {
    require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");
    require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");

    allowances[_owner][_spender] = _amount;
    emit Approval(_owner, _spender, _amount);
  }
```

This vulnerability underscores the importance of using the `increaseAllowance` and `decreaseAllowance` functions, as recommended by the ERC20 standard and secure implementations like OpenZeppelin. These methods offer a more secure approach to adjusting allowances by basing changes on the current allowance level, thereby reducing the susceptibility to front-running and enhancing the overall security of token transactions. 

As such, users should be reminded to proceed with cautions when handling spenders' allowances.  

## [L-02] Enhancing flexibility in the OUSGInstantManager's rate limiter
The OUSGInstantManager contract employs a simple yet effective rate limiting mechanism through its `_checkAndUpdateInstantMintLimit` function, setting a cap on the total amount mintable within defined durations to manage liquidity and mitigate potential abuses.

Here's a hypothetical situation:

1. `minimumDepositAmount` has been assigned 100_000e6, i.e. 100_000 USDC.
2. `instantMintLimit` is set to 1 million USDC and `resetInstantMintDuration` is set to 1 day. 
3. If investors doing eight 100k USDC deposits with the 9th depositor doing 100k + 1 USDC, the 10th depositor will not be able to deposit till `block.timestamp >= lastResetInstantRedemptionTime + resetInstantRedemptionDuration`.
4. This rigid system hinders transactions marginally above the limit, as observed with a hypothetical 10th depositor being unable to transact due to a minor excess.

Consider introducing an appropriate `CUSHION` e.g. 100 USDC or a tiny fraction of `instantRedemptionLimit` or `minimumDepositAmount` to circumvent the aforementioned exploit:  

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/InstantMintTimeBasedRateLimiter.sol#L131-L134

```diff
    require(
-      amount <= instantRedemptionLimit - currentInstantRedemptionAmount,
+      amount <= instantRedemptionLimit - currentInstantRedemptionAmount + CUSHION,
      "RateLimit: Redemption exceeds rate limit"
    );
```
## [L-03] Oracle reliability that is optimistically Chainlink dependent
`getOUSGPrice()` with `price` fed by [Chainlink](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/rwaOracles/RWAOracleExternalComparisonCheck.sol#L25-L32) is frequently called in ousgInstantManager.sol and rOUSG.sol. The system would be crippled if Chainlink failed to feed correct prices due to uncontrolled situations e.g. staleness, outside min/max answers, new integrations needed to accommodate decimals changes initiated by Chainlink etc.    

To mitigate the risks associated with relying on a single oracle, such as Chainlink, for price feeds in smart contracts, several strategies can be employed. These include multi-oracle aggregation, which leverages data from multiple sources to derive a more reliable price point; fallback oracles such as Uniswap TWAP, which serve as backups in case the primary oracle fails; oracle heartbeat checks to ensure regular data updates; circuit breakers to halt operations under abnormal data conditions; governance intervention for manual fixes; decentralized oracle networks for broader data aggregation; and cross-referencing with on-chain data for additional validation. Implementing a combination of these methods can significantly enhance the robustness and security of smart contracts, especially in decentralized finance (DeFi) applications, by reducing the dependency on a single data source and mitigating the risks of data manipulation or failure.

## [NC-01] Erroneous require message
Consider having the following code line refactored to accurately portray the supposed message:   

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L186-L189

```diff
    require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
-      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
+      "OUSGInstantManager: OUSG decimals must be equal to rOUSG decimals"
    );
```