# Ondo Finance QA report by Timenov

## Summary

| |Issue|Instances|
|-|:-|:-:|
| I-01 | Minimun redeem to high. | 1 |
| I-02 | Unnecessary decimals validation. | 5 |
| I-03 | Admin role not used. | 1 |
| L-01 | Wrong validation of token balance. | 1 |

### [I-01] Minimun redeem to high.
In `ousgInstantManager` the state variable `minBUIDLRedeemAmount` is used to determine what is the minimum amount of BUIDL that must be redeemed in a single redemption. On deployment is set to `250_000e6`. Considering that `USDC:BUIDL` must be `1:1` this means that the minimum redeem is 250 000 dollars, which may be too much for some of the users.

### [I-02] Unnecessary decimals validation.
In `ousgInstantManager` the constructor has checks if the decimals of `ousg` and `rousg` are equal and so for the `usdc` and `buidl`. Then in `_mint` and `_redeem` there are validation on the decimals of the `usdc` and `buidl`, which is unnecessary. Also in the constructor when calculation the `decimalsMultiplier =
      10 **
        (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());`, the decimals can be hardcoded or stored in a variable instead of making another calls to get their value.
        
### [I-03] Admin role not used.
In `rOUSGFactory` a `DEFAULT_ADMIN_ROLE` is set to `bytes32(0)` and never used anywhere. Consider making a use of it or remove it.

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSGFactory.sol#L38

### [L-01] Wrong validation of token balance.
In `ousgInstantManager::_redeemBUIDL()` is used to redeem `BUIDL` tokens. This function is internal and is called in 2 places - first with `usdcAmountToRedeem`, second with `minBUIDLRedeemAmount` as parameters. 

The functions is as follows:

```solidity
  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
    uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
    buidlRedeemer.redeem(buidlAmountToRedeem);
    require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
  }
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L460

The `require` statement will validate if the contract has more than the `minBUIDLRedeemAmount`. However if the `buidlAmountToRedeem` is bigger than `buidl.balanceOf(address(this))` the check will pass and eventually revert later on with a different error message, which could confuse users.

Use `buidlAmountToRedeem` to validate balance instead of `minBUIDLRedeemAmount`.

```diff
  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    require(
-      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
+      buidl.balanceOf(address(this)) >= buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
    uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
    buidlRedeemer.redeem(buidlAmountToRedeem);
    require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
  }
```


