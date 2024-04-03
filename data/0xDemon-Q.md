## [L-1] Incorrect error messages

Incorrect error messages may lead to errors in taking the next steps to correct the problem

```solidity
    require( 
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    ); //@audit-issue LOW it should be : OUSG decimals must be equal to ROUSG decimals
```

*Github : [186 - 189](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L186-L189)*