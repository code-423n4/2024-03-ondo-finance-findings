### Report 1:
#### Loss of fund from Precision Loss when Scaling Down Token Conversion
 
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704
```solidity
  function _getRedemptionAmount(
    uint256 ousgAmountBurned,
    uint256 price
  ) internal view returns (uint256 usdcOwed) {
    uint256 amountE36 = ousgAmountBurned * price;
>>>    usdcOwed = _scaleDown(amountE36 / 1e18);
  }
```

