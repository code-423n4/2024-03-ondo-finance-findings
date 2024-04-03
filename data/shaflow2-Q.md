# [L-1] When buidlAmountToRedeem is greater than minBUIDLRedeemAmount, the function may not catch the error correctly
## Details
In the _redeemBUIDL function of the OUSGInstantManager contract, the balance of BUIDL within the contract is checked to be greater than minBUIDLRedeemAmount. If the validation passes, the redemption operation is carried out.
```solidity
    require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
    uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
    buidlRedeemer.redeem(buidlAmountToRedeem);
```
However, when usdcAmountToRedeem >= minBUIDLRedeemAmount and usdcAmountToRedeem > buidl.balanceOf(address(this)),
```solidity
    if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
      // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
      // to cover the full amount
      _redeemBUIDL(usdcAmountToRedeem);
    }
```
The amount of BUIDL to be redeemed will be usdcAmountToRedeem, but there isn't enough BUIDL in the contract. However, the caller won't receive an error message like "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance." The error message received will depend on the redemption implementation. For instance, if redemption doesn't roll back but rather redeems the existing BUIDL in the contract, then the message received will be "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1".
## suggestion
Compare the number of buidlAmountToRedeem when checking the BUIDL in the contract
```solidity
    require(
      buidl.balanceOf(address(this)) >= buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
```




# [L-2] The event trigger parameters are incorrect and there are unnecessary calculations
## Details
In the burn function of rOUSG, the parameters when the Transfer event is triggered are incorrect and there are unnecessary calculations.
```solidity
  function burn(
    address _account,
    uint256 _amount
  ) external onlyRole(BURNER_ROLE) {
    uint256 ousgSharesAmount = getSharesByROUSG(_amount);
    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
      revert UnwrapTooSmall();

    _burnShares(_account, ousgSharesAmount);

    ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
    emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount)); 
    emit TransferShares(_account, address(0), ousgSharesAmount);
  }
```
First, we can understand that the Transfer event is used to track the flow of rOUSG’s token balance. TransferShares is used to track the flow of rOUSG shares, which can be reflected in functions such as warp, unwarp, and transfer.
In the burn function, the token balance flow of rOUSG is _account -> address(0), while the token balance triggered by the event flows to address(0) -> msg.sender which is wrong.
And the input in the burn function is the destruction balance of rOUSG. We use it to calculate the current corresponding share ousgSharesAmount, and when the event is triggered, we use ousgSharesAmount to reversely calculate the destruction balance of rOUSG. This is unnecessary repeated calculation. .
## suggestion
Use correct token balance flow and remove unnecessary calculations
```solidity
-  emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount)); 
+  emit Transfer(_account, address(0), _amount); 
```


# [NC-1] Upgradeable inheritance contract is not initialized by calling
## Details
The ROUSG contract inherits ContextUpgradeable, PausableUpgradeable, AccessControlEnumerableUpgradeable, but their initialization functions __init(bool callChain), __Pausable_init(), __AccessControl_init() are not called in the initialize function.
Although this will not affect the functionality of the system, I think it is a bad habit.
## suggestion
```solidity
   function initialize(
     address _kycRegistry,
     uint256 requirementGroup,
     address _ousg,
     address guardian,
     address _oracle
   ) public virtual initializer {
     __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
+    __init(false);
+    __Pausable_init();
+    __AccessControl_init();
   }
```