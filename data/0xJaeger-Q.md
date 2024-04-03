**[L-1] rOUSG:initialize `PausableUpgradable` not initialized.**
-

When initializing the `rOUSG` the PausableUpgradeable's `__Pausable_init` is not called.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128
```solidity
  function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
    __KYCRegistryClientInitializable_init(_kycRegistry, _requirementGroup);
    ousg = IERC20(_ousg);
    oracle = IRWAOracle(_oracle);
    _grantRole(DEFAULT_ADMIN_ROLE, guardian);
    _grantRole(PAUSER_ROLE, guardian);
    _grantRole(BURNER_ROLE, guardian);
    _grantRole(CONFIGURER_ROLE, guardian);
  }
```
If your contract inherits from PausableUpgradeable, you can still use the functions provided, even if you don't call Pausable_init() in your initialize function. However, it's important to understand that while you can technically use the functions provided by PausableUpgradeable without explicitly initializing the pausable functionality, the behavior might not be as expected. The pausable functionality won't be properly set up, so the contract might not behave as intended when you attempt to pause or unpause it, as it may not have initialized the storage slots properly.

Please modify like below:
```diff
  function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
    __KYCRegistryClientInitializable_init(_kycRegistry, _requirementGroup);
+   __Pausable_init()
    ousg = IERC20(_ousg);
    oracle = IRWAOracle(_oracle);
    _grantRole(DEFAULT_ADMIN_ROLE, guardian);
    _grantRole(PAUSER_ROLE, guardian);
    _grantRole(BURNER_ROLE, guardian);
    _grantRole(CONFIGURER_ROLE, guardian);
  }
```


**[NC-1] Require statement not necessary for checking if contract has sufficient allowance.**
-
There is no need for a require statement to check if there are sufficient allowances for the contract, as it will revert during transfer if there is insufficient allowance.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L299

```diff
  function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {
    // rest of function
-   require(
-     usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
-     "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
-   );
    // rest of function
}

```


**[NC-2] Missing @return natspec for rOUSG::getOUSGPrice()**
-
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378-L380
```diff
+   /**
+   * @notice Returns the current price of OUSG in USDC with 18 decimals of precision
+   */
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
  }
```

**[NC-3] Code readeability improvements for `rOUSG::_transferShares`, `rOUSG::_mintShares`, `rOUSG::_burnShares`**
-
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529
```diff
function _mintShares(
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
    require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");

    _beforeTokenTransfer(address(0), _recipient, _sharesAmount);

    totalShares += _sharesAmount;

-   shares[_recipient] = shares[_recipient] + _sharesAmount;
+   shares[_recipient] += _sharesAmount;

    return totalShares;
  }
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L501
```diff
function _transferShares(
    address _sender,
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused {
    require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");
    require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");

    _beforeTokenTransfer(_sender, _recipient, _sharesAmount);

    uint256 currentSenderShares = shares[_sender];
    require(
      _sharesAmount <= currentSenderShares,
      "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
    );

    shares[_sender] = currentSenderShares - _sharesAmount;
-    shares[_recipient] = shares[_recipient] + _sharesAmount;
+    shares[_recipient] += _sharesAmount;
  }
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554
```diff
 function _burnShares(
    address _account,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
    require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS");

    _beforeTokenTransfer(_account, address(0), _sharesAmount);

    uint256 accountShares = shares[_account];
    require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE");

    totalShares -= _sharesAmount;

-    shares[_account] = accountShares - _sharesAmount;   
+    shares[_account] -= _sharesAmount;

    return totalShares;
  }
```

**[NC-4] Fix math in rOUSG natspec**
-
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L28-L53
```diff
 * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
 * controlled by the protocol. To calculate each account's balance, we do
 *
 *   shares[account] * ousgPrice
 *
 * For example, assume that we have:
 *
 *   ousgPrice = 100.505
 *   sharesOf(user1) -> 100
 *   sharesOf(user2) -> 400
 *
 * Therefore:
 *  
- *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
+ *   balanceOf(user1) -> (_sharesOf(_account) * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
+ *
+ *   (100e18 * 10000 * 100.505) / (1e18 * 10000) = 10050
+ *     
+ *   balanceOf(user1) -> 10050 rOUSG which corresponds to 100 shares
- *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
+ *   balanceOf(user2) -> 40202 rOUSG which corresponds to 400 shares 
 *
```


**[NC-5] Improve readability in `ousgInstantManager::getOUSGPrice()` notice**
-
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L472-L478
```diff
  /**
-   * @notice Returns the current price of OUSG in USDC
+   * @notice Returns the current price of OUSG in USDC with 18 decimal precision
   *
   * @dev Sanity check: this function will revert if the price is unexpectedly low
   *
-   * @return price The current price of OUSG in USDC 
+   * @return price The current price of OUSG in USDC with 18 decimal precision
   */
```

**[NC-6] Wrong link in `ousgInstantManager::increaseAllowance()` notice**
-
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L472-L478
```diff
  /**
     * @notice Atomically increases the allowance granted to `_spender` by the caller by `_addedValue`.
     *
     * This is an alternative to `approve` that can be used as a mitigation for
     * problems described in:
-    * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42
+    * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/release-v4.7/contracts/token/ERC20/IERC20.sol#L57
     * Emits an `Approval` event indicating the updated allowance.
     *
     * Requirements:
     *
     * - `_spender` cannot be the the zero address.
     * - the contract must not be paused.
     */
```