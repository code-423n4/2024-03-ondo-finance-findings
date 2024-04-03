# QA Report

## Low Risk Issues

| Count | Explanation |
|:--:|:-------|
| [L-01] | `TransparentUpgradeableProxy` clashing selector calls may not be delegated |  
| [L-02] | Potential DoS in redeem functionality in case USDC enables Fees on transfer |  
| [L-03] | Lack of Enforced Timelock on Fee Updates |  
| [L-04] | Risk of Funds Getting Stuck due to Minimum Redemption Amount Update |  
| [L-05] | Precision loss from minting and redeeming rOUSG can be reduced |
| [L-06] | Some functions can be vulnerable to Slippage |   

| Total Low Risk Issues | 6 |
|:--:|:--:|

### [L-01] TransparentUpgradeableProxy clashing selector calls may not be delegated

## Description

* In the `rOUSGFactory` contract, the `deployRebasingOUSG` function utilizes the `TransparentUpgradeableProxy` pattern to deploy the `rOUSGProxy` contract. 

```solidity

@->    rOUSGProxy = new TokenProxy(address(rOUSGImplementation), address(rOUSGProxyAdmin), "");

```

* However, the `TransparentUpgradeableProxy` contract imported from the `external/openzeppelin` directory is based on an outdated version (4.4.1) of the OpenZeppelin library ([Link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/external/openzeppelin/contracts/proxy/TransparentUpgradeableProxy.sol#L2)).

* There is a known Vulnerability in this version of `TransparentUpgradableProxy` pattern which you can see [here](https://github.com/OpenZeppelin/openzeppelin-contracts/security/advisories/GHSA-mx2q-35m2-x2rh).

Impact of this vulnerability as stated officially:

> A function in the implementation contract may be inaccessible if its selector clashes with one of the proxy's own selectors. Specifically, if the clashing function has a different signature with incompatible ABI encoding, the proxy could revert while attempting to decode the arguments from calldata.

## Recommended Mitigation

Use latest Version of Openzeppelin Library to mitigate this risk.

### [L-02] Potential DoS in redeem functionality in case USDC enables Fees on transfer

* The `_redeemBUIDL` function in the contract `OUSGInstantManager` helps the redemption of BUIDL tokens.

* Within `_redeemBUIDL`, a require statement (marked with @->) verifies the balance of USDC tokens after redemption to ensure a 1:1 ratio with BUIDL tokens redeemed.

```solidity

    function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
      require(buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,"OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance");
      uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
      buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
      buidlRedeemer.redeem(buidlAmountToRedeem);
@->   require(usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem, "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1");
    }

```

* Currently, USDC does not impose fees on token transfers. However, there is a possibility of enabling such fees in the future.

* If USDC introduces fees on transfers, the require statement validating the balance of USDC tokens post-redemption against the pre-redemption balance will always fail.

* Consequently, any attempt to redeem BUIDL tokens would result in a reverting transaction, leading to DoS Scenario.

### [L-03] Lack of Enforced Timelock on Fee Updates

* The `OUSGInstantManager` contract contains functions such as `setMintFee` and `setRedeemFee`, which enable the adjustment of fees associated with minting and redeeming operations.

```solidity

    function setMintFee(
        uint256 _mintFee
      ) external override onlyRole(CONFIGURER_ROLE) {
        require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
        emit MintFeeSet(mintFee, _mintFee);
        mintFee = _mintFee;
      }

```

* These fee adjustment functions do not currently incorporate a timelock mechanism, allowing privileged roles to update fees instantly without prior notice to users.

* The absence of a timelock mechanism means that fee updates can take effect immediately upon execution of the corresponding function by a privileged role.

* Users who initiate minting or redemption transactions during or shortly after a fee update may experience discrepancies in the expected fee structure, leading to confusion and potentially financial loss.

### [L-04] Risk of Funds Getting Stuck due to Minimum Redemption Amount Update

**Consider the following Scenario:**

* The contract currently sets the `setMinimumRedemptionAmount` to `50_000e6`.

* For instance, consider Alice, who has deposited `120,000 USDC` to mint `X` OUSG tokens.

* Alice then initiates a redemption of `60,000 USDC` worth of OUSG, assuming she can redeem `60,000 USDC` more anytime given the current `setMinimumRedemptionAmount` of `50_000e6`.

* At some time in future, `CONFIGURE_ROLE` decides to increase this minimum redemption amount to `75_000e6` which is completely normal behavour on his behalf.

* However, now as the `setMinimumRedemptionAmount` is updated to `75_000e6`, Alice's funds will get stuck as she cannot redeem her amount, falling below the new minimum redemption threshold.

**Recommended Mitigation:**

Use a Timelock for this call which allows users enough time to make necessary changes to their portfolio.

### [L-05] Precision loss from minting and redeeming rOUSG can be reduced

* In the `OUSGInstantManager` contract, the `mintRebasingOUSG` function helps minting of `rOUSG` tokens in exchange for `USDC`.

* However, the current implementation may result in precision loss due to rounding when transferring `rOUSG` tokens to the user (As Acknowledged in Readme as well).

* In `mintRebasingOUSG` function, ROUSG Amount is calculated from `shares` and then that amount is transferred using `transfer` function. This can result in loss of dust amount in the contract because of rounding.

```solidity

    function mintRebasingOUSG(uint256 usdcAmountIn) external
      override
      nonReentrant
      whenMintNotPaused
      returns (uint256 rousgAmountOut)
    {
      uint256 ousgAmountOut = _mint(usdcAmountIn, address(this));
      ousg.approve(address(rousg), ousgAmountOut);
      rousg.wrap(ousgAmountOut);
      rousgAmountOut = rousg.getROUSGByShares(ousgAmountOut * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
@->   rousg.transfer(msg.sender, rousgAmountOut);
      emit InstantMintRebasingOUSG(msg.sender, usdcAmountIn, ousgAmountOut, rousgAmountOut);
    }

```

* By using `rousg.transferShares` function instead of `rousg.transfer` function, this issue can be easily mitigated.

### [L-06] Some functions can be vulnerable to Slippage

* Given the possibility of rebasing prices based on updates from the Oracle, certain functions within the contract may be vulnerable to slippage or lack of deadline enforcement.

* Whether it's `transfer`, `transferShares` or even `approve` function, Not having slippage or deadline can lead to issues.

Issue Detail:

1. Consider a scenario where User A intends to transfer a specific amount of rOUSG tokens to User B, resulting in a certain number of shares being transferred.
2. If the Oracle price updates between transaction initiation and execution, the actual number of shares transferred may differ from the intended amount, leading to unexpected outcomes for the users involved.
3. Even if functions such as transferShares are used, users may still unknowingly send more or less rOUSG tokens than intended due to price fluctuations.

For such Scenario, Having a Slippage control and Deadline helps protecting user from unexpected Issues.