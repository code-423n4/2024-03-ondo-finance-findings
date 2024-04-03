# QA Report for Ondo Finance

## QA-1 : Magic Number `200` is used at `ousgInstantmanager::setMintFee` as Max Mint Fee

### Proof of Concept:
The `ousgInstantmanager::setMintFee` function uses a magic number (`200`) as the maximum allowed value for the mint fee. Magic numbers are hardcoded values that lack context and can make the code less readable and maintainable.

Take a look at: https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L557
```solidity
function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high"); //@audit - magic number
    emit MintFeeSet(mintFee, _mintFee);
    mintFee = _mintFee;
  }
  ```
### Impact
Using magic numbers can make the code harder to understand and maintain. It reduces the readability of the code, as the meaning and purpose of the number may not be immediately clear to developers. If the maximum allowed mint fee needs to be changed in the future, it would require modifying the hardcoded value directly in the contract, which can be error-prone and may lead to inconsistencies if the value is used in multiple places.

### Recommended Mitigation Steps
To improve code readability and maintainability, it is recommended to replace the magic number with a named constant that clearly conveys its purpose. This makes the code more self-explanatory and allows for easier modification if needed.
```diff
function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
-    require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high"); //@audit - magic number
+    require(mintFee < MAX_MINT_FEE,  "OUSGInstantManager::setMintFee: Fee too high");
    emit MintFeeSet(mintFee, _mintFee);
    mintFee = _mintFee;
  }
  ```
 By introducing a named constant `MAX_MINT_FEE`, the code becomes more readable, and the purpose of the value becomes clear.


## QA-2 : Incorrect variable comparison in `OUSGInstantManager::setMinimumDepositAmount` function

### Proof of Concept
The `OUSGInstantManager::setMinimumDepositAmount` function compares the `_minimumDepositAmount` parameter with the `FEE_GRANULARITY` constant to ensure that the minimum deposit amount is not too small. However, according to the developer's confirmation, the comparison should be made with the value `100_100e6` instead.

Take a look at: https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L585
```solidity
function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(
      _minimumDepositAmount >= FEE_GRANULARITY, //@audit - this check is incorrect, there should be >= 100_000e6
      "setMinimumDepositAmount: Amount too small"
    );

    emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
    minimumDepositAmount = _minimumDepositAmount;
  }
  ```
In the code above, the `_minimumDepositAmount` parameter is compared with `FEE_GRANULARITY`, which is not the intended comparison I think. The comparison should be made with the value `100_000e6`.

### Impact
Using the incorrect variable for comparison in the `setMinimumDepositAmount` function can lead to unintended behavior and allow setting a minimum deposit amount that is smaller than the intended value.

### Recommended Mitigation Steps
Update the `setMinimumDepositAmount` function to compare the `_minimumDepositAmount` parameter with the correct value of `100_100e6`:
```solidity
function setMinimumDepositAmount(uint256 _minimumDepositAmount) external override onlyRole(CONFIGURER_ROLE) {
    require(
        _minimumDepositAmount >= 100_100e6,
        "setMinimumDepositAmount: Amount too small"
    );

    emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
    minimumDepositAmount = _minimumDepositAmount;
}
```
By updating the comparison to use the correct value, the function will enforce the intended minimum deposit amount and ensure consistency throughout the contract.


## QA-3 : Incorrect variable comparison in `OUSGInstantManager::setMinimumRedemptionAmount` function

### Proof of Concept
The `setMinimumRedemptionAmount` function in the OUSGInstantManager contract compares the `_minimumRedemptionAmount` parameter with the `FEE_GRANULARITY` constant to ensure that the minimum redemption amount is not too small. However, based on the provided comment, the comparison should be made with the value `50_000e6` instead.

Take a look at: https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L603
```solidity
function setMinimumRedemptionAmount(uint256 _minimumRedemptionAmount) external override onlyRole(CONFIGURER_ROLE) {
    require(
	    // @audit - there should be use >= 50_000e6
        _minimumRedemptionAmount >= FEE_GRANULARITY, "setMinimumRedemptionAmount: Amount too small");
    emit MinimumRedemptionAmountSet(
        minimumRedemptionAmount,
        _minimumRedemptionAmount
    );
    minimumRedemptionAmount = _minimumRedemptionAmount;
}
```
In the code above, the `_minimumRedemptionAmount` parameter is compared with `FEE_GRANULARITY`, which is not the intended comparison. The comment suggests that the comparison should be made with the value `50_000e6`.

### Impact
Using the incorrect variable for comparison in the `setMinimumRedemptionAmount` function can lead to unintended behavior and allow setting a minimum redemption amount that is smaller than the intended value.

### Recommended Mitigation Steps
Update the `setMinimumRedemptionAmount` function to compare the `_minimumRedemptionAmount` parameter with the correct value of `50_000e6`:
```diff
function setMinimumRedemptionAmount(uint256 _minimumRedemptionAmount) external override onlyRole(CONFIGURER_ROLE) {
    require(
-        _minimumRedemptionAmount >= FEE_GRANULARITY, "setMinimumRedemptionAmount: Amount too small");
+        _minimumRedemptionAmount >= 50_000e6, "setMinimumRedemptionAmount: Amount too small");
    emit MinimumRedemptionAmountSet(
        minimumRedemptionAmount,
        _minimumRedemptionAmount
    );
    minimumRedemptionAmount = _minimumRedemptionAmount;
}
```
By updating the comparison to use the correct value, the function will enforce the intended minimum redemption amount and ensure consistency throughout the contract.

## QA-4 : Missing input validation for minimum BUIDL redemption amount

### Proof of Concept
The `OUSGInstantManager::setMinimumBUIDLRedemptionAmount` function is for setting the minimum BUIDL redemption amount. However, it lacks input validation to ensure that the provided `_minimumBUIDLRedemptionAmount` is greater than or equal to the expected minimum value of `250_000e6`. This can lead to setting an invalid or unintended minimum BUIDL redemption amount. The devs did this in most of the setter function but they maybe be missed in this one.

Take a look at: https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L622-L630
```solidity
function setMinimumBUIDLRedemptionAmount(uint256 _minimumBUIDLRedemptionAmount) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit MinimumBUIDLRedemptionAmountSet(
        minBUIDLRedeemAmount,
        _minimumBUIDLRedemptionAmount
    );
    // @audit - there is no check that it is greater than the minimum, >= 250_000e6
    minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
}
```
In the code above, the `setMinimumBUIDLRedemptionAmount` function directly assigns the `_minimumBUIDLRedemptionAmount` value to the `minBUIDLRedeemAmount` state variable without performing any input validation. There is no check to ensure that the provided value is greater than or equal to the expected minimum of `250_000e6`.

### Impact
It allows setting a minimum BUIDL redemption amount that is lower than the expected value of  `250_000e6`, which may not meet the intended requirements of the system.

### Recommended Mitigation Steps
Update the `setMinimumBUIDLRedemptionAmount` function to include input validation:
```solidity
function setMinimumBUIDLRedemptionAmount(uint256 _minimumBUIDLRedemptionAmount) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    require(
        _minimumBUIDLRedemptionAmount >= 250_000e6,
        "setMinimumBUIDLRedemptionAmount: Amount too small"
    );
    emit MinimumBUIDLRedemptionAmountSet(
        minBUIDLRedeemAmount,
        _minimumBUIDLRedemptionAmount
    );
    minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
}
```



## QA-5 : No storage gaps for `rOUSG.sol` contract might lead to storage slot collision

### Impact
For upgradeable contracts, inheriting contracts may introduce new variables. In order to be able to add new variables to the upgradeable contract without causing storage collisions, a storage gap should be added to the upgradeable contract.

If no storage gap is added, when the upgradable contract introduces new variables, it may override the variables in the inheriting contract.

Storage gaps are a convention for reserving storage slots in a base contract, allowing future versions of that contract to use up those slots without affecting the storage layout of child contracts.  
To create a storage gap, declare a fixed-size array in the base contract with an initial number of slots.  
This can be an array of uint256 so that each element reserves a 32 byte slot. Use the naming convention  `__gap`  so that OpenZeppelin Upgrades will recognize the gap.

As [rOUSG.sol](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol) is an Upgradable contract, it should have storage gap

### Recommended Mitigation Steps
Consider adding a storage gap at the end of the `rOUSG.sol` contract
```solidity
uint256[50] private  __gap;
```

## QA-6 : Potential inconsistency between `paused` state and `mintPaused`/`redeemPaused` states in `ousgInstantManager.sol` contract

### Proof of Concept
The `OUSGInstantManager` contract inherits from the `PausableUpgradeable` contract, which provides a `paused` state variable and functions to pause and unpause the contract. However, the contract also defines separate `mintPaused` and `redeemPaused` state variables and functions to pause and unpause minting and redeeming separately. This could lead to inconsistencies if the `paused` state and the individual `mintPaused`/`redeemPaused` states are not kept in sync.
```solidity
contract OUSGInstantManager is
    // ...
    PausableUpgradeable,
    // ...
{
    // ...
    bool public mintPaused;
    bool public redeemPaused;
    // ...
}
```
### Impact
If the `paused` state and the individual `mintPaused`/`redeemPaused` states are not properly synchronized, it could lead to confusion and unexpected behavior when pausing and unpausing the contract or specific functionalities.

### Recommended Mitigation Steps
Consider removing the separate `mintPaused` and `redeemPaused` state variables and functions, and rely solely on the `paused` state provided by the `PausableUpgradeable` contract.


## QA-7 : Unnecessary  `onlyInitializing`  modifier in `rOUSG.sol` contract

### Proof of Concept
The `__rOUSG_init_unchained()` function in the ROUSG contract is marked with the `onlyInitializing` modifier, which is not needed since the function is already called from the `__rOUSG_init()` function that has the modifier.
```solidity
function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
) internal onlyInitializing {
    // ...
}
```
### Impact
The unnecessary `onlyInitializing` modifier adds redundant code to the contract and may confuse developers who are trying to understand the initialization process.

### Recommended Mitigation Steps
Remove the `onlyInitializing` modifier from `__rOUSG_init_unchained()`


## QA-8 : Lack of slippage protection in  `ousgInstantManager::mint`  and  `ousgInstantManager::redeem`  functions

### Proof of Concept
The `mint` and `redeem` functions in the OUSGInstantManager contract do not provide any slippage protection for users. If the OUSG price changes significantly between the time a user submits a transaction and when it is processed, the user may receive an unexpectedly low amount of tokens or USDC.

```solidity
function mint(uint256 usdcAmountIn) external override nonReentrant whenMintNotPaused returns (uint256 ousgAmountOut) {
    ousgAmountOut = _mint(usdcAmountIn, msg.sender);
    emit InstantMintOUSG(msg.sender, usdcAmountIn, ousgAmountOut);
}


function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {

    //..

    require(
      ousgAmountOut > 0,
      "OUSGInstantManager::_mint: net mint amount can't be zero"
    );

    //..
}
```

```solidity

function redeem(uint256 ousgAmountIn) external override nonReentrant whenRedeemNotPaused returns (uint256 usdcAmountOut) {
    require(ousg.allowance(msg.sender, address(this)) >= ousgAmountIn, "OUSGInstantManager::redeem: Insufficient allowance");
    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
    usdcAmountOut = _redeem(ousgAmountIn);
    emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut);
}



function _redeem(
    uint256 ousgAmountIn
  ) internal returns (uint256 usdcAmountOut) {

    //..

    require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    );

    //..

}
```
### Impact
Users may suffer financial losses if the OUSG price moves unfavorably between the submission and execution of their minting or redeeming transactions. This lack of slippage protection exposes users to the risks associated with price volatility.

### Recommended Mitigation Steps
Add Slippage protection
