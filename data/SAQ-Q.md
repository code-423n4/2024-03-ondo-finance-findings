
## Summary

### Low Issues

no | Issue |Instances|
|-|:-|:-:|
| [L-1] |  External calls in an un-bounded `for`-loop may result in a DOS | 1 |
| [L-2] | Consider implementing two-step procedure for updating protocol addresses | 1 |
| [L-3] | Missing contract-existence checks before low-level calls | 2 |
| [L-4] | Missing checks for `address(0x0)` in the `constructor/initializer` | 2 |
| [L-5] | Initialization can be front-run | 1 |


### Non-Critical Issues

no | Issue |Instances|
|-|:-|:-:|
| [NC-1] | `public`functions not called by the contract should be declared `external` instead | 3 |
| [NC-2] | Duplicated `require()/revert()` checks should be refactored to a modifier or function | 4 |
| [NC-3] | Typos | 11 |
| [NC-4] | File is missing `NatSpec` | Various |
| [NC-5] | Incomplete NatSpec: @param | 16 |
| [NC-6] | Custom errors should be used rather than `revert()/require()` | 28 |
| [NC-7] | Variable names for` immutables` should use `CONSTANT_CASE` | 7 |
| [NC-8] | Invalid NatSpec comment style | 26 |
| [NC-9] | Style guide: `Non-external/public` function names should begin with an underscore | 5 |


## Low Risk Issues

### [L-1] External calls in an un-bounded `for`-loop may result in a DOS

Consider limiting the number of iterations in for-loops that make external calls

```solidity
file: /contracts/ousg/rOUSGFactory.sol

126      (bool success, bytes memory ret) = address(exCallData[i].target).call{

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126C1-L126C77



### [L-2] Consider implementing two-step procedure for updating protocol addresses

A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must 'accept' the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement EIP-165, and to have the 'set' functions ensure that the recipient is of the right interface type.

```solidity
file: /contracts/ousg/ousgInstantManager.sol

650  function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
    emit FeeReceiverSet(feeReceiver, _feeReceiver);
    feeReceiver = _feeReceiver;         /// feeReceiver

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650C1-L655C32



### [L-3] Missing contract-existence checks before low-level calls

Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that  `<address>.code.length > 0`

```solidity
file: /contracts/ousg/ousgInstantManager.sol

824    IERC20(token).transfer(to, amount);

323    ousg.mint(to, ousgAmountOut);

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L824


### [L-4] Missing checks for `address(0x0)` in the `constructor/initializer`

```solidity
file: /contracts/ousg/rOUSGFactory.sol

47  constructor(address _guardian) {
    guardian = _guardian;
  }


```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47C1-L49C4


```solidity
file: /contracts/ousg/rOUSG.sol

102  function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
    __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
  }

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102C1-L110C4



### [L-5]  Initialization can be front-run

```solidity
file: /contracts/ousg/rOUSG.sol

102  function initialize(

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102



## Non Critical Issues


### [NC-1] `public`functions not called by the contract should be declared `external` instead

Contracts [are allowed](https://docs.soliditylang.org/en/latest/contracts.html#function-overriding) to override their parents' functions and change the visibility from external to public.
```solidity
file: /contracts/ousg/rOUSG.sol

188  function totalSupply() public view returns (uint256) {

199  function balanceOf(address _account) public view returns (uint256) {

251  function approve(address _spender, uint256 _amount) public returns (bool) {  

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188C1-L188C57


### [NC-2] Duplicated `require()/revert()` checks should be refactored to a modifier or function

The compiler will inline the function, which will avoid JUMP instructions usually associated with functions
 
```solidity
file: /contracts/ousg/ousgInstantManager.sol

291    if (address(investorBasedRateLimiter) != address(0)) {

408    if (address(investorBasedRateLimiter) != address(0)) { 

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L291C1-L291C59


```solidity
file: /contracts/ousg/rOUSG.sol

435      revert UnwrapTooSmall();

630      revert UnwrapTooSmall();

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L435C1-L435C31


### [NC-3] Typos

```solidity
file: /contracts/ousg/ousgInstantManager.sol

633   * @notice Admin function to set the oracle address

817   * @param amount The amount of token to transfer

755   /// @notice Ensure that the mint functionality is not paused

732   * @notice Scale provided amount up by `decimalsMultiplier`

680   * @notice Given a deposit amount and a price, returns the OUSG amount due


562  /**
   * @notice Sets the redeem fee.
   *
   * @param _redeemFee new redeem fee specified in basis points
   */

473   * @notice Returns the current price of OUSG in USDC  

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L817C1-L817C51


```solidity
file: /contracts/ousg/rOUSG.sol

89  // Error when redeeming shares < `OUSG_TO_ROUSG_SHARES_MULTIPLIER`

545   * @notice Destroys `_sharesAmount` shares from `_account`'s holdings, decreasing the total amount of shares.

609   * @notice Sets the Oracle address
   * @dev The new oracle must comply with the IRWAOracle interface
   * @param _oracle Address of the new oracle
   */ 

591    // Check constraints when `transferFrom` is called to facliitate
592    // a transfer between two parties that are not `from` or `to`.  

619   * @notice Admin burn function to burn rOUSG tokens from any account

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L619C1-L619C71

### [NC-4] File is missing `NatSpec`

```solidity
file: /contracts/ousg/ousgInstantManager.sol

    Various functions

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol


### [NC-5] Incomplete NatSpec: @param


```solidity
file: /contracts/ousg/ousgInstantManager.sol


458  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {


```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458


```solidity
file: /contracts/ousg/rOUSG.sol

102  function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {


112   function __rOUSG_init(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {   


128  function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {   

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102C1-L108C33


### [NC-6] Custom errors should be used rather than `revert()/require()`

Custom errors are available from solidity version 0.8.4. Custom errors are more easily processed in try-catch blocks, and are easier to re-use and maintain.

```solidity
file: /contracts/ousg/ousgInstantManager.sol

163    require(
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
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    );
    require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    );


282    require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_mint: USDC decimals must be 6"
    );
    require(
      usdcAmountIn >= minimumDepositAmount,
      "OUSGInstantManager::_mint: Deposit amount too small"
    );


    require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    );


    require(
      ousgAmountOut > 0,
      "OUSGInstantManager::_mint: net mint amount can't be zero"
    );
    


371    require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    );

    require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_redeem: USDC decimals must be 6"
    );
    require(
      IERC20Metadata(address(buidl)).decimals() == 6,
      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    );

    require(
      usdcAmountToRedeem >= minimumRedemptionAmount,
      "OUSGInstantManager::_redeem: Redemption amount too small"
    );

    require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    );
    

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L163C3-L193C7


```solidity
file: /contracts/ousg/rOUSG.sol

282     require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");

333    require(
      currentAllowance >= _subtractedValue,
      "DECREASED_ALLOWANCE_BELOW_ZERO"
    );

461    require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");

432    require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");

477    require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");
478    require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");

506    require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");
    require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");

    require(
      _sharesAmount <= currentSenderShares,
      "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
    );


```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L282C1-L282C79


### [NC-7] Variable names for` immutables` should use `CONSTANT_CASE`

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE)
```solidity
file: /contracts/ousg/ousgInstantManager.sol

72  IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;

  // OUSG contract
75  IRWALike public immutable ousg;

  // Rebasing OUSG Contract
78  ROUSG public immutable rousg;

  // BUIDL token contract
81  IERC20 public immutable buidl;

  // Redeemer contract used for instant redemptions of BUIDL
84  IBUIDLRedeemer public immutable buidlRedeemer;

  // Scaling factor to account for differences in decimals between OUSG/rOUSG and BUIDL/USDC
87  uint256 public immutable decimalsMultiplier;

  // The address that receives USDC for subscriptions
90  address public immutable usdcReceiver;

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72C1-L90C41


### [NC-8]  Invalid NatSpec comment style

NatSpec must begin with `///`, or use `/* ... */` syntax

```solidity
file: /contracts/ousg/ousgInstantManager.sol

56  // Role to configure the contract

59  // Role to pause minting and redemptions

  // Safety circuit breaker in case of Oracle malfunction

  // Helper constant that allows us to precisely specify fees in basis points

  // Helper constant that allows us to convert between OUSG and rOUSG shares

  // USDC contract

  // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;

  // OUSG contract

  // Rebasing OUSG Contract

  // BUIDL token contract

  // Redeemer contract used for instant redemptions of BUIDL

  // Scaling factor to account for differences in decimals between OUSG/rOUSG and BUIDL/USDC

  // The address that receives USDC for subscriptions

  // Address of the oracle that provides the `ousgPrice`

  // The address in which USDC should be sent to as a fee for minting and redeeming

  // Fee collected when minting OUSG (in basis points)

  // Fee collected when redeeming OUSG (in basis points)

  // Minimum amount of USDC that must be deposited to mint OUSG or rOUSG
  // Denoted in 6 decimals for USDC

  // Minimum amount of USDC that must be redeemed for to redeem OUSG or rOUSG
  // Denoted in 6 decimals for USDC

  // Whether minting is paused for this contract

  // Whether redemptions are paused for this contract

  // The minimum amount of BUIDL that must be redeemed in a single redemption
  // with the BUIDLRedeemer contract

122  // Optional investor-based rate limiting contract reference

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L56C2-L122C62

### [NC-9]  Style guide: `Non-external/public` function names should begin with an underscore

According to the Solidity Style Guide, `non-external/public` function names should begin with an underscore

```solidity
file: /contracts/ousg/ousgInstantManager.sol

335  function redeem(
    uint256 ousgAmountIn
  )

362  function redeemRebasingOUSG(
    uint256 rousgAmountIn
  )  

458  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335C1-L337C4


```solidity
file: /contracts/ousg/rOUSG.sol

586  function _beforeTokenTransfer(
    address from,
    address to,
    uint256
  ) internal view {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L586C1-L590C20
