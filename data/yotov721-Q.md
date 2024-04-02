[L-1] A bit of ousg tokens are lost during unwrapping
This is in the known issue category, but it can be easily fixed by burning only the amount being transfered, by subtracting the leftover.
```diff
 function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
    require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
    uint256 ousgSharesAmount = getSharesByROUSG(_rOUSGAmount);

    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER) revert UnwrapTooSmall();

-    _burnShares(msg.sender, ousgSharesAmount);
+    _burnShares(msg.sender, ousgSharesAmount - ousgSharesAmount % OUSG_TO_ROUSG_SHARES_MULTIPLIER);

    ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
...
```

[NC-1] Unused variable in `ROUSGFactory`
The `DEFAULT_ADMIN_ROLE` constant in `ROUSGFactory` is never used. It could be removed - this would also save a bit of gas.