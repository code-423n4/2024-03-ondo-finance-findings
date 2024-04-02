## missing check
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L437
```
When the user calls the unwrap() function, there is no check on the contract's OUSG balance during the transfer of OUSG.

When the transaction is rolled back due to insufficient contract balance, there is no error message.

## Missing comments
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L794
```
The function multiexcall() lacks a @notice comment explaining its functionality.





### Time spent:
10 hours