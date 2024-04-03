### Report 1:
#### Loss of fund from Precision Loss when Scaling Down Token Conversion
 As can be noted in the code provided from the ousgInstantManager contract, it shows how amount is scaled down based on token conversion from higher decimal to lower decimal, the problem is that the amount lost from solidity precision during division operation as noted from the pointer is not accounted for by the protocol and would be completely lost. Protocol should make provision for an additional state variable to monitor the accumulation of this lost value
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

