## [L-01] False checks of fee values in ```setMintFee``` and ```setRedeemFee``` functions.
Both the functions check the storage variables(which is already set) instead of the arguments;

**setMintFee** - https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L557C2-L557C76

**setRedeemFee** - https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L570C4-L570C80

which is no use since it can still be set to more than 200 and gives false protection to users. 
And if set to more than 200(accidentally or intentionally) i.e. more than 2% it can never be changed back because the check will revert and users will keep paying fees which is more than the capped percentage they were promised. 

Replace both the lines with:

```diff
-       require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
+       require(_mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");

-       require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
+       require(_redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
```


## [L-02] ```_redeemBUIDL``` always checks for ```minBUIDLRedeemAmount``` instead of the argument.

Inside the [```_redeemBUILD```]("https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L459C4-L462C7") internal function there is a require statement to make sure that the contract has enough BUILD tokens to redeem before actuall redeeming. 
```javascript
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
If we look at the ```_redeem``` function in the case when ```usdcAmountToRedeem >= minBUIDLRedeemAmount``` the ```_redeemBUIDL``` function is called with ```_redeemBUIDL(usdcAmountToRedeem);``` and not ``` _redeemBUIDL(minBUIDLRedeemAmount);```.

Suppose when;
 * usdcAmountToRedeem = 1,000,000e6 and the contract has just 500,000e6 BUILD tokens, 
 * then 1,000,000e6 > 250_000e6(minBUIDLRedeemAmount) so ```_redeemBUIDL``` will be called with ```_redeemBUIDL(usdcAmountToRedeem);``` i.e. with 1,000,000e6.
 * balance check will pass inside ```_redeemBUIDL``` function because it checks minBUIDLRedeemAmount(250_000e6) instead of the amount to redeem i.e. 1,000,000e6. 
 Now the contract thinks it has enough BUILD tokens and will call redeem.

However the redeem will still fail and most likely revert because the contract doesn't have enough to redeem. Although there is no loss in funds for the user or the contract, the function could return false error messages when it is suppose to return "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance".

Change the require statement in the ```_redeemBUILD``` to:
```diff
      require(
-           buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
            "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
         );

       require(
+            buidl.balanceOf(address(this)) >= buidlAmountToRedeem,
             "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
         );
```

## [L-03] 
Investors can frontrun price oracle update and escape from loss in case of OUSG price drop.

Note: The known issues section mention about how the users could [frontrun](https://code4rena.com/audits/2024-03-ondo-finance#top:~:text=Price/Rebasing%20Arbitrage,global%20rate%20limits.) when they see a price increase and sell it right after to make a profit but does not mention this one where a user could escape loss incase of price drops.

This is possible because the price update is done on-chain using this [oracle](https://etherscan.deth.net/address/0x0502c5ae08E7CD64fe1AEDA7D6e229413eCC6abe) contract. For this oracle consider sending price update transactions only through [flashbots](https://docs.flashbots.net/flashbots-protect/overview).

## [N-01] 
In an extreme case where [OUSG price](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L481C5-L484C7) drops below 105 investors have no way to redeem and their investments will be permanently locked. Consider adding a functionality where investors accept loss and can redeem if they don't what to wait for the price to go back up.

## [N-02] 
It is mentioned in the documentation that minimum investment is 100k usdc but users could be investing slightly lesser than 100k usdc because the [check](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L286C5-L289C7) is done before deducting fees, so after the fee is deducted the actual amount invested could be less than 100k usdc.
The [redeem](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L402C5-L420C7) function also has this logic.

## [N-03] 
One of the mentioned behaviours in scope for BUILD(i.e. [**Revert on transfer to the zero address**](https://code4rena.com/audits/2024-03-ondo-finance#top:~:text=Revert%20on%20transfer%20to%20the%20zero%20address)) is present but doesn't really have any impact because ```ousgInstantManager``` contract never transfer BUILD tokens to the 0 address. 

## [N-04] 
The ```buildRedeemer``` contract used to redeem BUILD tokens is unknown and there is a possibility that it might have unknown integration issues.
All the redeem calls were done by only one address i.e. 0x1e695A689CF29c8fE0AF6848A957e3f84B61Fe69 the [holder no. 4](https://etherscan.io/token/tokenholderchart/0x7712c34205737192402172409a8f7ccef8aa2aec#:~:text=4,0x1e695A68...84B61Fe69).
And the amounts redeemed were only 25000000(25 BUILD). While the code has ```minBUIDLRedeemAmount = 250_000e6;``` which is much more then the amounts redeemed by holder4. Since the buildRedeemer is not verified we really don't know how much it would allow to redeem or it might even have a limit.
For example, when I tested it with the holder4's address it reverts with **[FAIL. Reason: revert: Settlement: exceeds allowed amount]**. And after playing with the timestamp using foundry reverts with another error message: **[FAIL. Reason: revert: Under lock-up]**(which is likely because of the lock-period BUILD implements).
It would be best to wait for the source code to get verified re-check the code and deploy out contracts.

