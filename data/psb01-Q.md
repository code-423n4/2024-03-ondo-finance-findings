### [L-01] Appoval of buidl token more than the balance of contract given to buidlRedeemer will result in unexpected behaviour.

### Details

Inside ousgInstantManager.sol, In function [_redeem](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L426-L429) while redeeming usdc amount when
 `usdcAmountToRedeem >= minBUIDLRedeemAmount` 
[_redeemBUIDL(usdcAmountToRedeem)](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458-L470) is called which before giving approval of amount equivalent to usdcAmountToRedeem 
in this line `buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount` 
check only that whether buidl balance in this contract >= minBUIDLRedeemAmount (250_000e6).

suppose usdcAmountToRedeem = 400_000e6
and buidl.balanceOf(address(this) = 300_000e6
as As in this case 'buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount' so this check 
`require(`
 `buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,`
 `"OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"`
 `);` will pass
and `buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);` 
will approve buidl more than the balance of contract to the buidlRedeemer which while redeeming inside buidlRedeemer will result in unexpected behaviour.

### Recommendation:

`require(`
      `buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount &&`
      `buidl.balanceOf(address(this)) >= buidlAmountToRedeem,`
      `"OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"`
    `);`

### [N-01] Incorrect comment in rOUSG contract

here In https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L38 instead of `*   ousgPrice = 100.505` It should be `*   ousgPrice = 1.05`