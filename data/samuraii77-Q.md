1. Message for the revert is incorrect. The require checks whether the `OUSG` and `ROUSG` decimals are equal however the revert message implies that is it comparing the `OUSG` decimals with the `USDC` decimals. Furthermore, `OUSG` decimals are supposed to be 18 and `USDC` decimals are 6 making what the revert message implies, impossible.
```solidity
 require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    );
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L186-L189

2. The require statement below is redundant as `usdcAmountOut` can never be zero.
```solidity
uint256 usdcFees = _getInstantRedemptionFees(usdcAmountToRedeem);
    usdcAmountOut = usdcAmountToRedeem - usdcFees;
    require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    );
```

The only way `usdcAmountOut` can be 0 is if `usdcFees` is equal to the `usdcAmountToRedeem`. This is how `usdcFees` is computed:
```solidity
function _getInstantRedemptionFees(
    uint256 usdcAmount
  ) internal view returns (uint256) {
    return (usdcAmount * redeemFee) / FEE_GRANULARITY;
  }
```
The value of `FEE_GRANULARITY` is 10,000. The maximum value of `redeemFee` is 199. That means that `usdcFee` will always be with a value lower than the `usdcAmountToRedeem` as you are multiplying with a smaller value than you are dividing with resulting in the return value always being smaller.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L415-L420