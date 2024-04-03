### Low Risk and Non Critical issues


## [L-1] Code does not follow the best practice of check-effects-interaction
Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

**Total Instances:** 9

```solidity
File: contracts/ousg/ousgInstantManager.sol

 /// @audit  decimals() prior to this assignment
 194:     usdc = IERC20(_usdc);

 /// @audit  decimals() prior to this assignment
 195:     usdcReceiver = _usdcReciever;

 /// @audit  decimals() prior to this assignment
 196:     feeReceiver = _feeReceiver;

 /// @audit  decimals() prior to this assignment
 197:     oracle = IRWAOracle(_ousgOracle);

 /// @audit  decimals() prior to this assignment
 198:     ousg = IRWALike(_ousg);

 /// @audit  decimals() prior to this assignment
 199:     rousg = ROUSG(_rousg);

 /// @audit  decimals() prior to this assignment
 200:     buidl = IERC20(_buidl);

 /// @audit  decimals() prior to this assignment
 201:     buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);

 /// @audit  decimals() prior to this assignment
 202:     decimalsMultiplier =

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L202


## [L-2] Consider implementing two-step procedure for updating protocol addresses
A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must "accept" the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement [EIP-165](https://eips.ethereum.org/EIPS/eip-165), and to have the "set" functions ensure that the recipient is of the right interface type.

**Total Instances:** 5

```solidity
File: contracts/ousg/ousgInstantManager.sol

 638:   function setOracle(
         address _oracle
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

 650:   function setFeeReceiver(
         address _feeReceiver
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

 663:   function setInvestorBasedRateLimiter(
         address _investorBasedRateLimiter
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L638

```solidity
File: contracts/ousg/rOUSG.sol

 613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {

 650:   function setKYCRegistry(
         address registry
       ) external override onlyRole(CONFIGURER_ROLE) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L650



## [L-3] External function calls within loops
Calling external functions within loops can easily result in insufficient gas. This greatly increases the likelihood of transaction failures, DOS attacks, and other unexpected actions. It is recommended to limit the number of loops within loops that call external functions, and to limit the gas line for each external call.

**Total Instances:** 2

```solidity
File: contracts/ousg/ousgInstantManager.sol

 805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L805

```solidity
File: contracts/ousg/rOUSGFactory.sol

 126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L126


## [L-4] Function can return unassigned variable
Make sure that functions with a return value always return a valid and assigned value. Even if the default value is as expected, it should be assigned with the default value for code clarity and to reduce confusion.

**Total Instances:** 1

```solidity
File: contracts/ousg/rOUSG.sol

 /// @audit  totalShares is unassigned!
 348:     return totalShares;

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L348


## [L-5] Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard
Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks opens the users of this protocol up to [read-only reentrancy vulnerability](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect them except by block-listing the entire protocol.

**Total Instances:** 1

```solidity
File: contracts/ousg/ousgInstantManager.sol

 824:     IERC20(token).transfer(to, amount);

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L824


## [L-6] Governance functions should be controlled by time locks
Governance functions (such as upgrading contracts, setting critical parameters) should be controlled using time locks to introduce a delay between a proposal and its execution. This gives users time to exit before a potentially dangerous or malicious operation is applied.

**Total Instances:** 9

```solidity
File: contracts/ousg/ousgInstantManager.sol

 554:   function setMintFee(
         uint256 _mintFee
       ) external override onlyRole(CONFIGURER_ROLE) {

 567:   function setRedeemFee(
         uint256 _redeemFee
       ) external override onlyRole(CONFIGURER_ROLE) {

 581:   function setMinimumDepositAmount(
         uint256 _minimumDepositAmount
       ) external override onlyRole(CONFIGURER_ROLE) {

 599:   function setMinimumRedemptionAmount(
         uint256 _minimumRedemptionAmount
       ) external override onlyRole(CONFIGURER_ROLE) {

 622:   function setMinimumBUIDLRedemptionAmount(
         uint256 _minimumBUIDLRedemptionAmount
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

 638:   function setOracle(
         address _oracle
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

 650:   function setFeeReceiver(
         address _feeReceiver
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

 663:   function setInvestorBasedRateLimiter(
         address _investorBasedRateLimiter
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L554

```solidity
File: contracts/ousg/rOUSG.sol

 613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L613



## [L-7] Missing checks for `address(0x0)` in the constructor
'Constructors often take address parameters to initialize important components of a contract, such as owner or linked contracts. However, without a checking, there's a risk that an address parameter could be mistakenly set to the zero address (0x0). This could be due to an error or oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address, and any funds sent to it will be irretrievable. It's therefore crucial to include a zero address check in constructors to prevent such potential problems. If a zero address is detected, the constructor should revert the transaction.'

**Total Instances:** 2

```solidity
File: contracts/ousg/ousgInstantManager.sol

 /// @audit  defaultAdmin, _usdc, _usdcReciever, _feeReceiver, _ousgOracle, _buidlRedeemer not checked!
 144:   constructor(
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

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L144

```solidity
File: contracts/ousg/rOUSGFactory.sol

 /// @audit  _guardian not checked!
 47:   constructor(address _guardian) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L47


## [L-8] Missing checks for `address(0x0)` in the initializer
Consider adding a zero address check for address type variables in the initializer

**Total Instances:** 1

```solidity
File: contracts/ousg/rOUSG.sol

 /// @audit  _kycRegistry, _ousg, guardian, _oracle not checked!
 102:   function initialize(
         address _kycRegistry,
         uint256 requirementGroup,
         address _ousg,
         address guardian,
         address _oracle
       ) public virtual initializer {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L102



## [L-9] Missing contract-existence checks before low-level calls
Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `<address>.code.length > 0`

**Total Instances:** 2

```solidity
File: contracts/ousg/ousgInstantManager.sol

 805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L805

```solidity
File: contracts/ousg/rOUSGFactory.sol

 126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L126


## [L-10] `require()` should be used instead of `assert()`
Prior to solidity version 0.8.0, hitting an assert consumes the remainder of the transaction’s available gas rather than returning it, as `require()`/`revert()` do. `assert()` should be avoided even past solidity version 0.8.0 as its [documentation](https://docs.soliditylang.org/en/v0.8.14/control-structures.html#panic-via-assert-and-error-via-require) states that “The assert function creates an error of type Panic(uint256). … Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix”.

**Total Instances:** 1

```solidity
File: contracts/ousg/rOUSGFactory.sol

 94:     assert(rOUSGProxyAdmin.owner() == guardian);

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L94


## [L-11] Revert on transfer to the zero address
It’s good practice to revert a token transfer transaction if the recipient’s address is the zero address. This can prevent unintentional transfers to the zero address due to accidental operations or programming errors. Many token contracts implement such a safeguard, such as `OpenZeppelin - ERC20`, `OpenZeppelin - ERC721`.

**Total Instances:** 1

```solidity
File: contracts/ousg/ousgInstantManager.sol

 824:     IERC20(token).transfer(to, amount);

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L824




## [NC-1] Custom error has no error details
Consider adding parameters to the error to indicate which user or values caused the failure.

**Total Instances:** 1

```solidity
File: contracts/ousg/rOUSG.sol

 90:   error UnwrapTooSmall();

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L90

## [NC-2] Use a struct instead of returning multiple values
Functions that return many variables can become difficult to read and maintain. Using a struct to encapsulate these return values can improve code readability, increase reusability, and reduce the likelihood of errors. Consider refactoring functions that return more than three variables to use a struct instead.

**Total Instances:** 1

```solidity
File: contracts/ousg/rOUSGFactory.sol

 70:   function deployRebasingOUSG(
        address kycRegistry,
        uint256 requirementGroup,
        address ousg,
        address oracle
      ) external onlyGuardian returns (address, address, address) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L70



## [NC-3] Use a struct to encapsulate multiple function parameters
If a function has too many parameters, replacing them with a struct can improve code readability and maintainability, increase reusability, and reduce the likelihood of errors when passing the parameters.

**Total Instances:** 1

```solidity
File: contracts/ousg/ousgInstantManager.sol

 144:   constructor(
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

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L144


## [NC-4] Avoid the use of sensitive terms
Use [alternative variants](https://www.zdnet.com/article/mysql-drops-master-slave-and-blacklist-whitelist-terminology/), e.g. allowlist/denylist instead of whitelist/blacklist.

**Total Instances:** 2

```solidity
File: contracts/ousg/rOUSG.sol

 294:    * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42

 319:    * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L319



## [NC-5] Contract uses both require()/revert() as well as custom errors
Consider using just one method in a single file. The below instances represents the less used technique.

**Total Instances:** 2

```solidity
File: contracts/ousg/rOUSG.sol

 435:       revert UnwrapTooSmall();

 630:       revert UnwrapTooSmall();

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L630



## [NC-6] Named imports of parent contracts are missing
Named imports of parent contracts are missing.

**Total Instances:** 3

```solidity
File: contracts/ousg/ousgInstantManager.sol

 /// @audit  ReentrancyGuard, InstantMintTimeBasedRateLimiter, AccessControlEnumerable, IOUSGInstantManager, IMulticall
 49: contract OUSGInstantManager is

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L49

```solidity
File: contracts/ousg/rOUSG.sol

 /// @audit  Initializable, ContextUpgradeable, PausableUpgradeable, AccessControlEnumerableUpgradeable, KYCRegistryClientUpgradeable, IERC20Upgradeable, IERC20MetadataUpgradeable
 55: contract ROUSG is

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L55

```solidity
File: contracts/ousg/rOUSGFactory.sol

 /// @audit  IMulticall
 37: contract ROUSGFactory is IMulticall {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L37



## [NC-7] address parameters should be sanitized
Implement a zero address check in functions with `address` parameters to prevent unexpected behavior.

**Total Instances:** 14

```solidity
File: contracts/ousg/ousgInstantManager.sol

 /// @audit  '_oracle' not checked
 638:   function setOracle(
         address _oracle
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

 /// @audit  '_investorBasedRateLimiter' not checked
 663:   function setInvestorBasedRateLimiter(
         address _investorBasedRateLimiter
       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

 /// @audit  'token', 'to' not checked
 819:   function retrieveTokens(
         address token,
         address to,
         uint256 amount
       ) external onlyRole(DEFAULT_ADMIN_ROLE) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L638

```solidity
File: contracts/ousg/rOUSG.sol

 /// @audit  '_kycRegistry', '_ousg', 'guardian', '_oracle' not checked
 102:   function initialize(
         address _kycRegistry,
         uint256 requirementGroup,
         address _ousg,
         address guardian,
         address _oracle
       ) public virtual initializer {

 /// @audit  '_recipient' not checked
 220:   function transfer(address _recipient, uint256 _amount) public returns (bool) {

 /// @audit  '_spender' not checked
 251:   function approve(address _spender, uint256 _amount) public returns (bool) {

 /// @audit  '_sender', '_recipient' not checked
 276:   function transferFrom(
         address _sender,
         address _recipient,
         uint256 _amount
       ) public returns (bool) {

 /// @audit  '_spender' not checked
 302:   function increaseAllowance(
         address _spender,
         uint256 _addedValue
       ) public returns (bool) {

 /// @audit  '_spender' not checked
 328:   function decreaseAllowance(
         address _spender,
         uint256 _subtractedValue
       ) public returns (bool) {

 /// @audit  '_recipient' not checked
 397:   function transferShares(
         address _recipient,
         uint256 _sharesAmount
       ) public returns (uint256) {

 /// @audit  '_oracle' not checked
 613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {

 /// @audit  '_account' not checked
 624:   function burn(
         address _account,
         uint256 _amount
       ) external onlyRole(BURNER_ROLE) {

 /// @audit  'registry' not checked
 650:   function setKYCRegistry(
         address registry
       ) external override onlyRole(CONFIGURER_ROLE) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L102

```solidity
File: contracts/ousg/rOUSGFactory.sol

 /// @audit  'kycRegistry', 'ousg', 'oracle' not checked
 70:   function deployRebasingOUSG(
        address kycRegistry,
        uint256 requirementGroup,
        address ousg,
        address oracle
      ) external onlyGuardian returns (address, address, address) {

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L70



## [NC-8] Unnecessary cast
The variable is being cast to its own type

**Total Instances:** 5

```solidity
File: contracts/ousg/ousgInstantManager.sol

 /// @audit  _usdc
 164:       address(_usdc) != address(0),

 /// @audit  _usdcReciever
 168:       address(_usdcReciever) != address(0),

 /// @audit  _feeReceiver
 172:       address(_feeReceiver) != address(0),

 /// @audit  _ousgOracle
 176:       address(_ousgOracle) != address(0),

 /// @audit  _buidlRedeemer
 183:       address(_buidlRedeemer) != address(0),

```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L183
