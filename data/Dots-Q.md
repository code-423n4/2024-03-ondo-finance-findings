## [L-1] Its possible for the CONFIGURER_ROLE to set minimumRedemptionAmount incorrectly.

If the CONFIGURER_ROLE uses `setMinimumRedemptionAmount` to set `minimumRedemptionAmount` he could forget the decimals which would lead to precision loss in the `_getRedemptionAmount` function.

```
function setMinimumRedemptionAmount(
    uint256 _minimumRedemptionAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(
      _minimumRedemptionAmount >= FEE_GRANULARITY, // 50000e6 >= 10000
      "setMinimumRedemptionAmount: Amount too small"
    );
    emit MinimumRedemptionAmountSet(
      minimumRedemptionAmount,
      _minimumRedemptionAmount
    );
    minimumRedemptionAmount = _minimumRedemptionAmount;
  }
```
```
function _getRedemptionAmount(
    uint256 ousgAmountBurned,
    uint256 price
  ) internal view returns (uint256 usdcOwed) {
    uint256 amountE36 = ousgAmountBurned * price;
    usdcOwed = _scaleDown(amountE36 / 1e18);
  }
```
## Recommendations
Add a decimal check in `setMinimumRedemptionAmount`


## [L-2] Its possible for the CONFIGURER_ROLE to set minimumDepositAmount incorrectly.

If the CONFIGURER_ROLE uses `setMinimumDepositAmount` to set `minimumDepositAmount` he could forget the decimals which would lead to precision loss in the `_getMintAmount` function.

```
function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(
      _minimumDepositAmount >= FEE_GRANULARITY,
      "setMinimumDepositAmount: Amount too small"
    ); //@audit missing check for e6

    emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
    minimumDepositAmount = _minimumDepositAmount;
  }
```
```
function _getMintAmount(
    uint256 usdcAmountIn,
    uint256 price
  ) internal view returns (uint256 ousgAmountOut) {
    uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;
    ousgAmountOut = amountE36 / price;
  }
```
## Recommendations
Add a decimal check in `setMinimumDepositAmount`