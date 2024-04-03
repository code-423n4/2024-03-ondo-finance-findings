### [L-1] Malicious admin can steal fees from users by abusing the `ousgInstantManager::setFeeReceiver` function and tokens by abusing `ousgInstantManager::retrieveTokens`.

**Description:** Since the admin has the authority to set or change the `feeReceiver` address in `ousgInstantManager::setFeeReceiver` function, he can simply add his own address as a parameter and receive all the fees paid by users of the protocol.

Admin can steal tokens from the protcol by using the `ousgInstantManager::retrieveTokens` function the same way.


**Recommended Mitigation:** Restrict the admin by setting his own address in these two functions: 

```diff
/**
   * @notice Admin function to set the fee receiver address

   * @param _feeReceiver The address to receive the mint and redemption fees
   */
  function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
-    require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
+    require(_feeReceiver != address(0) && msg.sender != _feeReceiver, "FeeReceiver cannot be 0x0");
    emit FeeReceiverSet(feeReceiver, _feeReceiver);
    feeReceiver = _feeReceiver;
  }
```

Or remove the fee receiver function and set the address in the constructor.

```diff
function retrieveTokens(
    address token,
    address to,
    uint256 amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
+   if (to == msg.sender || to == address(0)) revert(); 
    IERC20(token).transfer(to, amount);
  }
```

And consequently update the message error.

### [L-2] Use safe wrapper functions of OZ's `SafeERC20` library for transfer functions.

 https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L824
 https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L451-L455
 https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L317-L319
 

### [L-3] Too strong admin privilege in the protocol.

**Description:** Malicious admin can harm the protocol in many ways if he wishes due to the roles assigned to him upon deployment: 

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L211-L213

He can also use the protocol's services and set the fee to 0 when he is minting or redeeming, he can harm the users by pausing the mint and redeem functions and many more. Although his role can be revoked this doesn't restrict his actions.

**Recommended Mitigation:** There are several recommendations:

1. Consider using a multisig wallet between the owner and the admin 
2. Can implement a timelock mechanism, so there is a delay in case of malicious actions

This would make the protocol more secure and less centralized.

### [L-4] Missing slippage control checks in `ousgInstantManager::mint`, `ousgInstantManager::mintRebasingOUSG`, `ousgInstantManager::redeem` and `ousgInstantManager::redeemRebasingOUSG` functions.

**Description:** The minting and redemption functions _mint and _redeem respectively, calculate token quantities based on the current token price fetched from the oracle. However, they do not incorporate checks to ensure that the executed transactions remain within an acceptable slippage tolerance, which could expose users to risks associated with price fluctuations of the OUSG token since it's determined by an oracle: 

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L479

Although is has minimum ousg token price parameter check, this still doesn't prevent users receiving fewer tokens than expected or paying more than anticipated during transactions due to sudden price changes.

**Recommended Mitigation:** Add `uint256 minExpectedAmount` parameters and the required checks in the functions mentioned above. However this may require user calculating the acceptable slippage tolerance amount off-chain.

### [I-1] Missing calls to base initializers in `rOSUG.sol`.

**Description:** The `rOUSG::__rOUSG_init_unchained` function is missing calls to initializer functions of the base contracts:

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L128

- ContextUpgradeable
- PausableUpgradeable
- AccessControlEnumerableUpgradeable

### [I-2] Use named imports for better clarity.