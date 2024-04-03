### [l-01] Lack of KYC and Sanction List Verification in `_approve` Function for spender.

**Description:** 
The `_approve` function is used to setting the allowance of a spender over the owner's tokens. Call by the public functions like `approve` and `increaseAllowance` functions to set the allowance of spender. But there is no check in `_approve` function if the spender address is in KYC whitelist and not sanctioned too cause if the spender address is not KYC'd and in sanction list than the spender can not make any transaction even though the `allowances[_owner][_spender]` mapping for the spender show's the allowance to be non zero.

**Impact:**
The non KYC'd or sanctioned address will have the allowance for rOUSG token. 

**Proof of Concept:**
1. Using the public `approve` and `increaseAllowance` function the rOUSG token holder can give the allowance of rOUSG to the non KYC'd or sanctioned address.
2. Even though if spender try to execute the `transferFrom` function it will failed cause of the check in `transfer` function.
3. So it is better to not give the allowance of rOUSG token to non KYC'd or sanctioned address at first place.
4. For that `_approve` function should check the `_getKYCStatus` for the spender.

5. approve() function: 
```javascript
  function approve(address _spender, uint256 _amount) public returns (bool) {
    _approve(msg.sender, _spender, _amount); //approving spender on behalf of owner
    return true;
  }
```

6. increaseAllowance() function:
```javascript
  function increaseAllowance(
    address _spender, //spender address
    uint256 _addedValue //value to increase allowance
  ) public returns (bool) {
    _approve(
      msg.sender,
      _spender,
      allowances[msg.sender][_spender] + _addedValue 
    );
    return true;
  }
```
7. _approve() function:
```javascript
function _approve(
    address _owner,
    address _spender,
    uint256 _amount
  ) internal whenNotPaused {
    require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");
    require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");

    allowances[_owner][_spender] = _amount; 
    emit Approval(_owner, _spender, _amount);
  }
```

**Recommended Mitigation:**  
The recommended mitigation is to add `_getKYCStatus` check for the spender.
Coded mitigation:
```diff
function _approve(
    address _owner,
    address _spender,
    uint256 _amount
  ) internal whenNotPaused {
    require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");
    require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");
+   require(_getKYCStatus(_spender), "rOUSG: '_spender' address not KYC'd");

    allowances[_owner][_spender] = _amount; 
    emit Approval(_owner, _spender, _amount);
  }
```

### [l-02] Incorrect reference to USDC instead of rOUSG.

**Description:** 
The `ousgInstantManager` constructor performs a check for decimal compatibility between OUSG and rOUSG tokens but incorrectly refers to USDC instead of rOUSG in the checks.

**Impact:**
Can lead to confusion for the developer who will deploy and initialize the `ousgInstantManager` contract.

**Proof of Concept:**
```javascript
constructor(
    address defaultAdmin,
    address _usdc,
    address _usdcReciever,
    address _feeReceiver,
    address _ousgOracle,
    address _ousg,
    address _rousg,
    address _buidl,
    address _buidlRedeemer,
    RateLimiterConfig memory rateLimiterConfig
  ) 
    InstantMintTimeBasedRateLimiter( 
      rateLimiterConfig.mintLimitDuration,
      rateLimiterConfig.redeemLimitDuration,
      rateLimiterConfig.mintLimit,
      rateLimiterConfig.redeemLimit
    )
  {
    require(
      address(_usdc) != address(0),
      "OUSGInstantManager: USDC cannot be 0x0"
    );
    require(
      address(_usdcReciever) != address(0),
      "OUSGInstantManager: USDC Receiver cannot be 0x0"
    );
    require(
      address(_feeReceiver) != address(0),
      "OUSGInstantManager: feeReceiver cannot be 0x0"
    );
    require(
      address(_ousgOracle) != address(0),
      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
    );
    require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
    require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
    require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
    require(
      address(_buidlRedeemer) != address(0),
      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    );
    require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
@>     "OUSGInstantManager: OUSG decimals must be equal to USDC decimals" //@audit-info 
    );
    require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(), 
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    );
    usdc = IERC20(_usdc); 
    usdcReceiver = _usdcReciever;
    feeReceiver = _feeReceiver;
    oracle = IRWAOracle(_ousgOracle);
    ousg = IRWALike(_ousg);
    rousg = ROUSG(_rousg);
    buidl = IERC20(_buidl);
    buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
    decimalsMultiplier = 
      10 **
        (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals()); //10*1e12
    require(
      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
    );

    _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
    _grantRole(CONFIGURER_ROLE, defaultAdmin);
    _grantRole(PAUSER_ROLE, defaultAdmin);
  }
```

**Recommended Mitigation:** 
The recommended mitigation is to rewrite the error comment and change the USDC with rOUSG.
Add this:
"OUSGInstantManager: OUSG decimals must be equal to rOUSG decimals"

### [l-03] Strict Equivalence Check in `ousgInstantManager::_redeemBUIDL` function.

**Description:** 
The `ousgInstantManager::_redeemBUIDL` function is having a strict equivalence check when verifying the balance of USDC tokens in the contract after redeeming BUIDL tokens. The equality check (==) ensures that the USDC balance is exactly equal to the previous balance plus the redeemed BUIDL amount. However, a less strict check, such as greater than or equal to (>=), would be more appropriate if there any potential rounding or minor difference between the expected and actual balance occur.

**Impact:** 
The minor difference in token balances could lead to transaction revert, potentially stopping the intended functionality of the contract, If the USDC balance of contract is more than expected.

**Proof of Concept:**
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
@>     usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem, //@audit-info strick == check should be >=
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
  }
 ``` 

**Recommended Mitigation:** 
The recommended mitigation is to use greater than or equal (>=) instead of (==) equality check which will also work as intended and it will even execute the tx even if the USDC balance of contract is more than expected.
Coded recommendation:
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
-     usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem, 
+     usdc.balanceOf(address(this)) >= usdcBalanceBefore + buidlAmountToRedeem, 
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
  }
 ```

### [l-04] The `multiexcall` function can revert if contract can't accept ETH.

**Description:** 
As the readme of contest sates "The permissioned multicall function on OUSGInstantManager will only be used to transfer non-ERC20 assets out of the contract if the assets are accidentally deposited." If any one of the arbitrary contract does not accepts the ether than it will revert the whole `multiexcall` function transaction. 

**Proof of Concept:**
1. As the contest readme quotes `multiexcall` function is used to transfer non-ERC20 assets out of the contract is the asset are accidentally deposited.
2. The `multiexcall` function is transferring eth to the multiple addresses.
3. If any of the arbitrary address can't accepts eth than the whole tx will revert.

**Impact:** 
The transferring of eth to multiple addresses will revert.

**Recommended Mitigation:** 
The recommended mitigation is that the admin needs to  remove th address from the array which is causing revert. 

### [NC-01] Missing calls to base initializers in `rOUSG` contract

**Description:** 
The `rOUSG` contract is using OpenZeppelin's upgradeable contracts, such as ContextUpgradeable, PausableUpgradeable, and AccessControlEnumerableUpgradeable, but it not calling the init functions for these contracts in its own initializer `__rOUSG_init` function.

**Proof of Concept:**
The `PausableUpgradeable` contract have `__Pausable_init()` function which is used to Initializes the contract in unpaused state. but the `rOUSG::__rOUSG_init` is not calling it.

```
  /**
   * @dev Initializes the contract in unpaused state.
   */
  function __Pausable_init() internal onlyInitializing {
    __Pausable_init_unchained();
  }

  function __Pausable_init_unchained() internal onlyInitializing {
    _paused = false;
  }
```

**Recommended Mitigation:** 
Ensure that the initializer `__rOUSG_init` function of the contract `rOUSG` calls the init functions of all inherited upgradeable contracts.

### [NC-02] Missing handling of return bool in `transfer` and `transferFrom` functions.

**Description:** 
The `rOUSG.sol` and `ousgInstantManager.sol`contract does not handle the boolean return from the transfer and transferFrom functions as recommended by the ERC-20 standard. The ERC-20 standard specifies that *Callers MUST handle false from returns (bool success). Callers MUST NOT assume that false is never returned!*
As EIP20 Quotes:
NOTES:
1. The following specifications use syntax from Solidity 0.4.17 (or above)
2. @> *Callers MUST handle false from returns (bool success). Callers MUST NOT assume that false is never returned!*

**Impact:** 
Not handling the bool return value from transfer and transferFrom functions lead to a lack of proper error handling,

**Proof of Concept:**
The unwrap function of `rOUSG` contract calling the `transfer` function to return the OUSG token back to msg.sender but missing handling the return bool.

```javascript
function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
    require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
    uint256 ousgSharesAmount = getSharesByROUSG(_rOUSGAmount); 
    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER) 
      revert UnwrapTooSmall();
    _burnShares(msg.sender, ousgSharesAmount); 
@>    ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER 
    );
    emit Transfer(msg.sender, address(0), _rOUSGAmount);
    emit TransferShares(msg.sender, address(0), ousgSharesAmount);
  }
```

**Recommended Mitigation:** 
The recommended mitigation is to handle the return bool value where ever the `transfer` and `transferFrom` function is called in the `rOUSG` and `ousgInstantManager` contract because it is better engineering/error handling practices.
Coded mitigation:
```diff
function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
    require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
    uint256 ousgSharesAmount = getSharesByROUSG(_rOUSGAmount); 
    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER) 
      revert UnwrapTooSmall();
    _burnShares(msg.sender, ousgSharesAmount); 
+   bool success = ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER //KYC check is implicit
    );
+   require(success, "rOUSG: Failed to transfer!");
    emit Transfer(msg.sender, address(0), _rOUSGAmount);
    emit TransferShares(msg.sender, address(0), ousgSharesAmount);
  }
```

### [NC-03] Not including MINIMUM_OUSG_PRICE in `getOUSGPrice()` check.

**Description:** 
The `getOUSGPrice` function checks a requirement to ensure that the price of OUSG in USDC is above a MINIMUM_OUSG_PRICE which is 105e18. But it does not include the MINIMUM_OUSG_PRICE in check, It will be better to include the MINIMUM_OUSG_PRICE in check cause for majority of time the price of OUSG was below 105e18 it is only 16 feb when the OUSG price cross the MINIMUM_OUSG_PRICE mark.

**Impact:**
Overly strict check do not understand the market price of OUSG.

**Proof of Concept:**
```javascript
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData(); //the pirce of OUSG in USDC
    require(
@>     price > MINIMUM_OUSG_PRICE, //MINIMUM_OUSG_PRICE = 105e18 
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

**Recommended Mitigation:** 
The recommended mitigation is to include MINIMUM_OUSG_PRICE in `getOUSGPrice()` function check.
Coded recommendation:
```diff
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData(); //the pirce of OUSG in USDC
    require(
-      price > MINIMUM_OUSG_PRICE, 
+      price >= MINIMUM_OUSG_PRICE, 
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

### [NC-04] 200 is a magic number in `ousgInstantManager` contract.

**Description:** 
The `setMintFee` and `setRedeemFee` functions are used for configuration of the minting fee and redeem fee. But these both function use 200 as the max fee and it is magic number, cause it is hard-coded numeric constants and lack explanation. So it is better to initialize a constant variable MAX_FEE with 200 and than use it in functions rather than direct 200.

**Impact:** 
The magic numbers in the code reduces code readability, so it is better to not uses them.

**Proof of Concept:**
1. `setMintfee` function:
```javascript
 function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) { //@audit-info 200 is magic number 
@>   require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high"); 
    emit MintFeeSet(mintFee, _mintFee);
    mintFee = _mintFee;
  }
```
2. `setRedeemFee` function:
```javascript
 function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {//@audit-info 200 is magic number 
@>  require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
    emit RedeemFeeSet(redeemFee, _redeemFee);
    redeemFee = _redeemFee;
  }
```
**Recommended Mitigation:** 
The recommended mitigation is to initialize a constant variable MAX_FEE with 200 and than use it.
Coded Recommendation:
```diff
+ uint256 public constant MAX_FEE = 200;
```




