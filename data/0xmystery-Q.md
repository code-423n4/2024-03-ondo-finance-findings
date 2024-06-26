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
Note: The same shall also apply to `redeem()` that's governed by `_checkAndUpdateInstantRedemptionLimit()`.

## [L-03] Oracle reliability that is optimistically Chainlink dependent
`getOUSGPrice()` with `price` fed by [Chainlink](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/rwaOracles/RWAOracleExternalComparisonCheck.sol#L25-L32) is frequently called in ousgInstantManager.sol and rOUSG.sol. The system would be crippled if Chainlink failed to feed correct prices due to uncontrolled situations e.g. staleness, outside min/max answers, new integrations needed to accommodate decimals changes initiated by Chainlink etc.    

To mitigate the risks associated with relying on a single oracle, such as Chainlink, for price feeds in smart contracts, several strategies can be employed. These include multi-oracle aggregation, which leverages data from multiple sources to derive a more reliable price point; fallback oracles such as Uniswap TWAP, which serve as backups in case the primary oracle fails; oracle heartbeat checks to ensure regular data updates; circuit breakers to halt operations under abnormal data conditions; governance intervention for manual fixes; decentralized oracle networks for broader data aggregation; and cross-referencing with on-chain data for additional validation. Implementing a combination of these methods can significantly enhance the robustness and security of smart contracts, especially in decentralized finance (DeFi) applications, by reducing the dependency on a single data source and mitigating the risks of data manipulation or failure.

## [L-04] Helper view functions for current rate limit quota
Consider introducing view functions in ousgInstantManager.sol on remaining rate limits where possible so that investors may check whether or not their [mints](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L290)/[redeems](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L406) are going to be permissible.

Here're the suggested functions:

```solidity
function checkInstantMintLimit(uint256 amount) public view returns (bool permissible) {
    permissible = (amount <= instantMintLimit - currentInstantMintAmount);
``` 
```solidity
function checkInstantRedemptionLimit(uint256 amount) public view returns (bool permissible) {
    permissible = (amount <= instantRedemptionLimit - currentInstantRedemptionAmount);
``` 
## [L-05] Possibly overinflated `MINIMUM_OUSG_PRICE`
The oracle contracts are out of scope, but I am noticing `MINIMUM_OUSG_PRICE` might be inflated by two decimals:

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L63

```solidity
  uint256 public constant MINIMUM_OUSG_PRICE = 105e18;
```
The [RWADynamicOracle](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/rwaOracles/RWADynamicOracle.sol) contract's price calculation, as defined by its `derivePrice` function, uses a compound interest formula that factors in the elapsed time since a range's start, the daily interest rate, and the previous range's closing price. The function employs fixed-point arithmetic for operations, crucial due to Solidity's lack of native floating-point support. The final price is thus influenced by the set daily interest rate, the duration of the elapsed time, and the starting price point for each range. Given these dynamics, it's possible for the contract to output prices exceeding `1.05e18`, especially with higher interest rates or over longer periods. However, reaching or surpassing `105e18` would likely indicate unusually high rates or extended compounding periods, possibly pointing to misconfiguration or an aggressive financial model. The actual price outcomes will ultimately hinge on the specific interest rates and range durations set within the contract, emphasizing the need for careful review and alignment with the intended economic behaviors and use cases.

The sponsor probably meant 1.05e18. Otherwise, OUSD and the shares associated with rOUSG will all be diminished/shifted by two decimals. Setting the `MINIMUM_OUSG_PRICE` to `105e18` instead of the intended `1.05e18` may not pose a direct security vulnerability but can significantly impact the contract's functionality and economics. Such a high threshold could inadvertently block minting and redemption processes such as those integrated via a router, skew the token's economic mechanisms and exchange rates, disrupt interactions with other DeFi contracts, and degrade user experience due to unrealistic operational conditions. Correcting this error post-deployment, especially on immutable platforms like Ethereum, would be challenging and costly, necessitating a potential contract migration and updates across dependent systems. This underscores the importance of rigorous review and testing of smart contract parameters to avoid such impactful errors.

## [L-06] Modifier for `getOUSGPrice()`
`_mint()` having the following code logic,

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L306-L307

```solidity
    // Calculate the mint amount based on mint fees and usdc quantity
    uint256 ousgPrice = getOUSGPrice();
```
as well as `_redeem()` having similar code logic below,

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L399

```solidity
    uint256 ousgPrice = getOUSGPrice();
```
should be prepended with `getOUSGPrice()` as modifier for better visibility, cleaner code logic, and earlier revert when need be. 

## [L-07] Helper view functions for previewing conversions between OUSG and USDC
Consider introducing view functions in ousgInstantManager.sol for previewing conversions between OUSG and USDC where possible so that investors may better manage their [mints](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L290)/[redeems](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L406) with the anticipated [ousgAmountOut](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L237)/[usdcAmountOut](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L342) just as it has been introduced in rOUSG.sol:

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L185-L203

```solidity
  /**
   * @return the amount of tokens in existence.
   */
  function totalSupply() public view returns (uint256) {
    return
      (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
  }

  /**
   * @return the amount of tokens owned by the `_account`.
   *
   * @dev Balances are dynamic and equal the `_account`'s OUSG shares multiplied
   *      by the price of OUSG
   */
  function balanceOf(address _account) public view returns (uint256) {
    return
      (_sharesOf(_account) * getOUSGPrice()) /
      (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
  } 
```
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
## [NC-02] Private function with embedded modifier reduces contract size
Consider having the logic of a modifier embedded through a private function to reduce contract size if need be. A `private` visibility that is more efficient on function calls than the `internal` visibility is adopted because the modifier will only be making this call inside the contract.

For instance, the modifier below may be refactored as follows:

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L756-L759

```diff
+    function _whenMintNotPaused() private view {
+        require(!mintPaused, "OUSGInstantManager: Mint paused");
+    }

     modifier whenMintNotPaused() {
-        require(!mintPaused, "OUSGInstantManager: Mint paused");
+        _whenMintNotPaused();
     _;
     }
```
## [NC-03] Activate the Optimizer
Before deploying your contract, activate the optimizer when compiling using “solc --optimize --bin sourceFile.sol”. By default, the optimizer will optimize the contract assuming it is called 200 times across its lifetime. If you want the initial contract deployment to be cheaper and the later function executions to be more expensive, set it to “ --optimize-runs=1”. Conversely, if you expect many transactions and do not care for higher deployment cost and output size, set “--optimize-runs” to a high number.

```
module.exports = {
solidity: {
version: "0.8.16",
settings: {
optimizer: {
  enabled: true,
  runs: 1000,
},
},
},
};
```
Please visit the following site for further information:

https://docs.soliditylang.org/en/v0.5.4/using-the-compiler.html#using-the-commandline-compiler

Here's one example of instance on opcode comparison that delineates the gas saving mechanism:

```
for !=0 before optimization
PUSH1 0x00
DUP2
EQ
ISZERO
PUSH1 [cont offset]
JUMPI

after optimization
DUP1
PUSH1 [revert offset]
JUMPI
```
Disclaimer: There have been several bugs with security implications related to optimizations. For this reason, Solidity compiler optimizations are disabled by default, and it is unclear how many contracts in the wild actually use them. Therefore, it is unclear how well they are being tested and exercised. High-severity security issues due to optimization bugs have occurred in the past . A high-severity bug in the emscripten -generated solc-js compiler used by Truffle and Remix persisted until late 2018. The fix for this bug was not reported in the Solidity CHANGELOG. Another high-severity optimization bug resulting in incorrect bit shift results was patched in Solidity 0.5.6. Please measure the gas savings from optimizations, and carefully weigh them against the possibility of an optimization-related bug. Also, monitor the development and adoption of Solidity compiler optimizations to assess their maturity.   