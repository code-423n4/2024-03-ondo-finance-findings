# [L-01] Missing 0 address check for `defaultAdmin`
In the constructor of `ousgInstantManager.sol` `defaultAdmin` is used as input but never checked for 0 value. There is also no setter so the owner won't be able to grant the roles after deployment if he enters an incorrect address.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L145

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L211-L213

## Recommendations
Add a zero address check and a setter function that the owner of the contract can use to grant the admin roles to a desired address

# [L-02] Wrong error message returned
In the constructor of `ousgInstantManager` when `_ousg` and `_rousg` have different decimals the function reverts with this error message:
>"OUSGInstantManager: OUSG decimals must be equal to USDC decimals"

This error message is incorrect and should rather say:
>"OUSGInstantManager: OUSG decimals must be equal to rOUSG decimals"

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L186-L189

# [L-03] Check prevents user from withdrawing as much as they want
Let's say a malicious user has somehow managed to convert all BUIDL amount the `ousgInstantManager` holds to USDC or at least get it below 250k (for example using flash loans if fees are set to 0).

After that when a user wants to withdraw more than 250k USDC it will enter the following if statement (keep in mind `minBUIDLRedeemAmount` = 250k):
```
    if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
      // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
      // to cover the full amount
      _redeemBUIDL(usdcAmountToRedeem);
```
`_redeemBUIDL()` has the following check:
```
require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
```
This check will see that there is less than 250k BUIDL in the contract and revert even if there is for example 1 million USDC in the contract that can be used for the user to withdraw.

This means that if for example he has OUSG tokens equal to 500k USDC he can't redeem them at once because of this check. Instead he has to do 3 transactions below 250k which is not practical.

## Recommendations
Perhaps make a check to see if the contract has enough USDC to give to the user instead of trying to convert BUIDL tokens for more USDC.

# [L-04] Wrong check in `_redeemBUIDL()`
The `_redeemBUIDL()` function has the following check:
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L460
```
  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount, 
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
```
The require statement should actually check if the BUIDL balance is bigger than the requested `buidlAmountToRedeem` which can be larger than `minBUIDLRedeemAmount`.

## Recommendations
Change the check from above to this:
```
    require(
      buidl.balanceOf(address(this)) >= buidlAmountToRedeem, 
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
```

# [L-05] Wrong checks in minimum deposit/redeem setters

The function `setMinimumDepositAmount()` has the following check:
```
require(
      _minimumDepositAmount >= FEE_GRANULARITY,
      "setMinimumDepositAmount: Amount too small"
    );
```
However this check is not correct because `_minimumDepositAmount` and `FEE_GRANULARITY` are not the same decimals (`_minimumDepositAmount` is 6  decimal and `FEE_GRANULARITY = 10_000`). This means that it allows the admin to set a value for `_minimumDepositAmount` to for example 50_000 which isn't an appropriate value.

The same error is made in the `setMinimumRedemptionAmount()` function.
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602-L605

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L584-L587

## Recommendations
Change the require statement to check for a 6 decimal value instead of 10_000