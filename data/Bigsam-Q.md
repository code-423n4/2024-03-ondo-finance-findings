---
## [L-01] Address Zero Check Missing in State variable updates

---

**Github code**
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L663-L673

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L638-L643

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L650-L654

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L608-L616

 
The `setInvestorBasedRateLimiter` and `setOracle` functions allow the modification of the investor-based rate limiter and the oracle address, respectively. The impact of the finding is that there is no check to ensure that the newly passed addresses are not address zero (`0x0000000000000000000000000000000000000000`). These functions are crucial to the contract as the contract relies on them for input for sensitive data compilation. Although these functions are only called by the admin, efforts should be made to ensure that only valid addresses are passed. Without proper checks, such a scenario can lead to unexpected behavior and potential vulnerabilities in the smart contract. Therefore, it is considered good practice to implement checks for address(0x0) prior to assigning new values to address state variables.

## Proof of Concept
The following is the code snippet of the `setInvestorBasedRateLimiter` and `setOracle` functions:

```solidity
/**
 * @notice Admin function to set the investor-based rate limiter
 *
 * @param _investorBasedRateLimiter The address of the investor-based rate limiter
 */
function setInvestorBasedRateLimiter(
  address _investorBasedRateLimiter
) external override onlyRole(DEFAULT_ADMIN_ROLE) {
  emit InvestorBasedRateLimiterSet(
    address(investorBasedRateLimiter),
    _investorBasedRateLimiter
  );
 >> @audit  investorBasedRateLimiter = IInvestorBasedRateLimiter(
    _investorBasedRateLimiter
  );
}

/**
 * @notice Admin function to set the oracle address
 *
 * @param _oracle The address of the oracle that provides the OUSG price
 *                in USDC
 */
function setOracle(
  address _oracle
) external override onlyRole(DEFAULT_ADMIN_ROLE) {
  emit OracleSet(address(oracle), _oracle);
  >> @audit oracle = IRWAOracle(_oracle);
}
```


## Tools Used

- Manual Code Analysis

## Recommended Mitigation Steps
To address the identified issues in the `setInvestorBasedRateLimiter` and `setOracle` functions, consider the following steps:

**Add Address Zero Check:** Add checks to ensure that the newly passed addresses are not address zero.
   ```solidity
   require(_investorBasedRateLimiter != address(0), "OUSGInstantManager::setInvestorBasedRateLimiter: Invalid address");

.........................


   require(_oracle != address(0), "OUSGInstantManager::setOracle: Invalid address");
   ```







---

## [L-02]  Incorrect Error Message in Decimal Comparison

---

**Github code**
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L186-L189



### Impact
The current implementation of the require statement for decimal comparison in the `OUSGInstantManager` contract produces an inaccurate error message. The error message incorrectly states that "OUSG decimals must be equal to USDC decimals," while the actual comparison is between `OUSG` and `ROUSG` decimals. This misleading error message can cause confusion during debugging and auditing processes.

### Proof of Concept
line 188  OUSGInstantManager.sol
```solidity
require(
    IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
    "OUSGInstantManager: OUSG decimals must be equal to USDC decimals" //@note audit USDC should be OUSG
);
```

### Tools Used
Manual code analysis

### Recommended Mitigation Steps

To address this issue and provide a clear and accurate error message, the require statement should be updated to compare `OUSG` and `ROUSG` decimals directly.

**Mitigation**:

Update the require statement as follows:

```solidity
require(
    IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
    "OUSGInstantManager: OUSG decimals must be equal to ROUSG decimals"
);
```



---

---

## [L-03]  Possible limitations with Fee Setting Functions With a Maximum Cap of 200 

---
**Github code**
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L548-L573


## Impact
The setMintFee and setRedeemFee functions are used to set the mint and redeem fees, respectively, specified in basis points. Currently, the functions contain a requirement that the fee must be less than 200 basis points. Lowering the fee below this threshold may introduce several vulnerabilities and risks to the system, especially when other requirements like minimum deposits do not have a maximum cap limit thus when we reach a point based in the market cycle (bull and bear market scenario) that the fees collected will no longer be sufficiently equivalent to the corresponding market situation we are left with no option to update the fee. BNB,Eth and other token experiences gas fee increase for transactions when
 1. increase in market price (bull markets) 
 2. congestions e.t.c.

## Proof of Concept

The following is the code snippet of the `setMintFee` and `setRedeemFee` functions:

```solidity
/**
 * @notice Sets the mint fee
 *
 * @param _mintFee new mint fee specified in basis points
 */
function setMintFee(
  uint256 _mintFee
) external override onlyRole(CONFIGURER_ROLE) {
  require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
  emit MintFeeSet(mintFee, _mintFee);
  mintFee = _mintFee;
}


/**
 * @notice Sets the redeem fee.
 *
 * @param _redeemFee new redeem fee specified in basis points
 */
function setRedeemFee(
  uint256 _redeemFee
) external override onlyRole(CONFIGURER_ROLE) {
  require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
  emit RedeemFeeSet(redeemFee, _redeemFee);
  redeemFee = _redeemFee;
}
```
The presence of a maximum fee basic in these function and an absence of a maximum amount in other function makes this redundant in a ever changing crypto scape.

## Tool Used
- Manual Code Analysis

## Recommended Mitigation Steps
To address the identified issues in the `setMintFee` and `setRedeemFee` functions, consider the following steps:
since other state variables as a function that regulates their total limit, Consider using a new variable (MAXFEE) that can be set like our limits.
 

---

## [L-04]  Insufficient comment in rOUSG Contract

---


**Github code** 
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L618-L640

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L544-L570

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L408-L443


The rOUSG contract is designed to manage the wrapping and unwrapping of OUSG tokens. The contract includes functionalities like wrapping OUSG tokens to mint rOUSG tokens, unwrapping rOUSG tokens to redeem OUSG tokens, and burning rOUSG tokens. This report aims to highlight and address the insufficiency of comments in the code and potential issues related to the contract's functionality.


 1. Insufficient Comments in `burn` Function

The `burn` function in the rOUSG contract has insufficient comments, which could lead to misunderstanding or misuse of the function. 

```solidity
/**
 * @notice Admin burn function to burn rOUSG tokens from any account
 * @param _account The account to burn tokens from
 * @param _amount  The amount of rOUSG tokens to burn
 * @dev Transfers burned shares (OUSG) to `msg.sender`
 */
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

 Pause Mechanism Issue in `burn` and `_burnShares` Functions

The `burn` function calls the `_burnShares` function, which has a `whenNotPaused` modifier. This means that if the contract is paused, the `burn` function will revert.

```solidity
/**
 * @notice Destroys `_sharesAmount` shares from `_account`'s holdings, decreasing the total amount of shares.
 * @dev This doesn't decrease the token total supply.
 *
 * Requirements:
 *
 * - `_account` cannot be the zero address.
 * - `_account` must hold at least `_sharesAmount` shares.
 * - the contract must not be paused.
 */
function _burnShares(
  address _account,
  uint256 _sharesAmount
) internal whenNotPaused returns (uint256) {
  ......  
}
```

 2. Insufficient Comments in `wrap` and `unwrap` Functions

The `wrap` and `unwrap` functions also have insufficient comments, which can lead to misunderstandings or misuse.

```solidity
/**
 * @notice Function called by users to wrap their OUSG tokens
 *
 * @param _OUSGAmount The amount of OUSG Tokens to wrap
 *
 * @dev KYC checks implicit in OUSG Transfer
 */
function wrap(uint256 _OUSGAmount) external whenNotPaused {
  require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");
  uint256 ousgSharesAmount = _OUSGAmount * OUSG_TO_ROUSG_SHARES_MULTIPLIER;
  _mintShares(msg.sender, ousgSharesAmount);
  ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
  emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
  emit TransferShares(address(0), msg.sender, ousgSharesAmount);
}   

/**
 * @notice Function called by users to unwrap their rOUSG tokens
 *
 * @param _rOUSGAmount The amount of rOUSG to unwrap
 *
 * @dev KYC checks implicit in OUSG Transfer
 */
function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
  require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
  uint256 ousgSharesAmount = getSharesByROUSG(_rOUSGAmount);
  if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
    revert UnwrapTooSmall();
  _burnShares(msg.sender, ousgSharesAmount);
  ousg.transfer(
    msg.sender,
    ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
  );
  emit Transfer(msg.sender, address(0), _rOUSGAmount);
  emit TransferShares(msg.sender, address(0), ousgSharesAmount);
}
```
The functions has a `whenNotPaused` modifier. This means that if the contract is paused, they will revert.


## Recommendations

 Update Comments in `burn`, `wrap`, and `unwrap` Functions

Update the comments in the `burn`, `wrap`, and `unwrap` functions to provide clear and comprehensive explanations of the functions' functionalities and requirements.

```solidity
   * - the contract must not be paused.
```