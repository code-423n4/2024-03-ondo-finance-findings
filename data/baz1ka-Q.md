## [N-01] No need to type cast `exCallData.target`.

## Relevant GitHub Links

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L126

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L805

## Summary

No need to typecast `exCallData.target` to address type as it already has address type

## Recommended Mitigation Steps

Remove redundant type casting.

```diff
@@ -802,7 +808,7 @@ contract OUSGInstantManager is
   {
     results = new bytes[](exCallData.length);
     for (uint256 i = 0; i < exCallData.length; ++i) {
-      (bool success, bytes memory ret) = address(exCallData[i].target).call{
+      (bool success, bytes memory ret) = exCallData[i].target.call{
         value: exCallData[i].value
       }(exCallData[i].data);
       require(success, "Call Failed");
```

```diff
@@ -123,7 +123,7 @@ contract ROUSGFactory is IMulticall {
   ) external payable override onlyGuardian returns (bytes[] memory results) {
     results = new bytes[](exCallData.length);
     for (uint256 i = 0; i < exCallData.length; ++i) {
-      (bool success, bytes memory ret) = address(exCallData[i].target).call{
+      (bool success, bytes memory ret) = exCallData[i].target.call{
         value: exCallData[i].value
       }(exCallData[i].data);
       require(success, "Call Failed");
```

## [N-02] Use existing function to calculate `rOUSG.totalSupply()` and `rOUSG.balanceOf()`.

## Relevant GitHub Links

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L188-L191

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L199-L203

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L373-L376

## Summary

`rOUSG` contract already has function that calculates amount of rOUSG per share, so it's better to use already declared function to improve code readability.

## Recommended Mitigation Steps

```diff
@@ -186,8 +186,7 @@ contract ROUSG is
    * @return the amount of tokens in existence.
    */
   function totalSupply() public view returns (uint256) {
-    return
-      (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
+    return getROUSGByShares(totalShares);
   }

   /**
@@ -197,9 +196,7 @@ contract ROUSG is
    *      by the price of OUSG
    */
   function balanceOf(address _account) public view returns (uint256) {
-    return
-      (_sharesOf(_account) * getOUSGPrice()) /
-      (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
+    return getROUSGByShares(_sharesOf(_account));
   }
```

## [N-03] Create function which checks if there are enough tokens to unwrap in `rOUSG`.

## Relevant GitHub Links

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L434-L435

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L629-L630

## Summary

`rOUSG.unwrap()` and `rOUSG.burn()` both have condition that checks whether enough rOUSG was provided to unwrap. This condition can be moved into function to improve code readability.

## Recommended Mitigation Steps

```diff
@@ -431,9 +430,10 @@ contract ROUSG is
   function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
     require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
     uint256 ousgSharesAmount = getSharesByROUSG(_rOUSGAmount);
-    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
-      revert UnwrapTooSmall();
+
+    _checkEnoughOusgSharedProvided(ousgSharesAmount);
     _burnShares(msg.sender, ousgSharesAmount);
+
     ousg.transfer(
       msg.sender,
       ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER

@@ -626,9 +629,8 @@ contract ROUSG is
     uint256 _amount
   ) external onlyRole(BURNER_ROLE) {
     uint256 ousgSharesAmount = getSharesByROUSG(_amount);
-    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
-      revert UnwrapTooSmall();

+    _checkEnoughOusgSharedProvided(ousgSharesAmount);
     _burnShares(_account, ousgSharesAmount);

     ousg.transfer(

@@ -658,4 +660,9 @@ contract ROUSG is
   ) external override onlyRole(CONFIGURER_ROLE) {
     _setKYCRequirementGroup(group);
   }
+
+  function _checkEnoughOusgSharedProvided(uint256 _ousgSharesAmount) internal {
+    if (_ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
+      revert UnwrapTooSmall();
+  }
 }
```
