# [L-1] Missing check
## Details
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L437
```
When the user calls the unwrap() function, there is no check on the contract's OUSG balance during the transfer of OUSG.

When the transaction is rolled back due to insufficient contract balance, there is no error message.
## suggestion
Check the contract ousg balance before transferring ousg. If the balance is insufficient, an error message will be returned.

# [L-2] Missing check
## Details
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L426
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L458
```
In the redeemBUIDL function of the OUSGInstantManager contract, it is checked whether the balance of buidl in the contract is greater than minBUIDLRedeemAmount. If it passes the verification, the redemption operation will be performed.

But when usdcAmountToRedeem >= minBUIDLRedeemAmount and usdcAmountToRedeem > buidl.balanceOf(address(this)) in the contract, the transaction will be rolled back because there is not enough BUIDL, but no error message will be returned.

## suggestion
Check the number of BUIDLs in the contract and return an error message if it is insufficient.
```solidity
    require(
      buidl.balanceOf(address(this)) >= buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
```

# [NC-1] Missing comments
## Details
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L794
```
The function multiexcall() lacks a @notice comment explaining its functionality.

# [NC-2] Missing annotations
## Details
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L378
```
The getOUSGPrice() function lacks a @return annotation.



### Time spent:
11 hours