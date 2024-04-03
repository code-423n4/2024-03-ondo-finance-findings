## Low Findings

|    | Issue | Instances |
|----|-------|:---------:|
| [L-01] | Unsafe use of `transfer()/transferFrom()` with IERC20 | 1 |
| [L-02] | Centralization issue caused by admin privileges | 28 |
| [L-03] | `decimals()` is not part of the ERC20 standard | 1 |
| [L-04] | Large transfers may not work with some `ERC20` tokens | 1 |
| [L-05] | `assert()` should only be used for tests | 1 |
| [L-06] | Code does not follow the best practice of check-effects-interaction | 1 |
| [L-07] | Initializers can be front-run | 1 |
| [L-08] | `.call` bypasses function existence check, type checking and argument packing | 2 |
| [L-09] | Unbounded loop may run out of gas | 2 |
| [L-10] | Lack of index element validation in external/public function | 5 |
| [L-11] | Consider checking that transfer to `address(this)` is disabled | 2 |
| [L-12] | Unsafe solidity low-level call can cause gas grief attack | 2 |
| [L-13] | Possible division by 0 is not prevented | 2 |
| [L-14] | Initializer missing `address(0)` Check before assignment | 3 |
| [L-15] | Missing checks for `address(0)` when updating state variables | 3 |
| [L-16] | Risk of Renouncing Ownership While System is Paused | 1 |
| [L-17] | Consider the case where `totalSupply` is zero | 1 |
| [L-18] | Missing checks for state variable assignments | 6 |
| [L-19] | Missing checks in constructor/initialize | 2 |
| [L-20] | Missing contract-existence checks before low-level calls | 2 |
| [L-21] | Events may be emitted out of order due to reentrancy | 11 |
| [L-22] | Critical functions should be a two step procedure | 15 |
| [L-23] | Implement two-step ownership transfers | 1 |
| [L-24] | Loss of precision on division | 12 |
| [L-25] | Unbounded Gas Consumption on External Calls | 2 |
| [L-26] | Lack of two-step update for updating protocol addresses | 3 |
| [L-27] | Potential Re-org Attack Vector | 3 |
| [L-28] | Missing checks for `address(0)` in constructor | 2 |
| [L-29] | Missing `__gap[50]` storage variable in Upgradeable contracts | 1 |
| [L-30] | Using a vulnerable dependency from some libraries | 1 |

Total: 118 instances of 30 issues

## NonCritical Findings

|    | Issue | Instances |
|----|-------|:---------:|
| [N-01] | Use custom errors instead of `require()/assert()` | 51 |
| [N-02] | Missing Event Emission After Critical Initialize() Function | 1 |
| [N-03] | Variables need not be initialized to zero | 4 |
| [N-04] | Variables need not be initialized to false | 1 |
| [N-05] | Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, for readability | 2 |
| [N-06] | Consider returning a `struct` rather than having multiple `return` values | 1 |
| [N-07] | Consider using a `struct` rather than having many function input parameters | 4 |
| [N-08] | Avoid using constant decimals in expressions | 6 |
| [N-09] | Custom error has no error details | 1 |
| [N-10] | Consider using `delete` rather than assigning `false` to clear values | 2 |
| [N-11] | Consider emitting an event at the end of the constructor | 3 |
| [N-12] | Consider using named returns | 24 |
| [N-13] | Consider using named function arguments | 3 |
| [N-14] | Function Parameters in Public Accessible Functions Need `address(0)` Check | 17 |
| [N-15] | Events are missing sender information | 15 |
| [N-16] | Leverage Recent Solidity Features with `0.8.23` | 3 |
| [N-17] | NatSpec: Function `@param` tag is missing | 30 |
| [N-18] | NatSpec: Function declarations should have descriptions | 15 |
| [N-19] | Contract uses both `require()`/`revert()` as well as custom errors | 1 |
| [N-20] | Event Names Not Following `CapWords` Style (CamelCase) | 1 |
| [N-21] | Inconsistent spacing in comments | 20 |
| [N-22] | Critical system parameter changes should be behind a timelock | 15 |
| [N-23] | Outdated Solidity Version | 3 |
| [N-24] | Function/Constructor Argument Names Not in mixedCase | 38 |
| [N-25] | NatSpec: Function `@return` tag is missing | 15 |
| [N-26] | State-Altering Functions Should Emit Events | 3 |
| [N-27] | Upgrade `openzeppelin` to the Latest Version - 5.0.0 | 11 |
| [N-28] | Duplicated `require()`/`revert()` checks should be refactored to a modifier or function | 2 |
| [N-29] | Non-specific Imports | 23 |
| [N-30] | Event is not properly `indexed` | 2 |
| [N-31] | Missing NatSpec Descriptions for Modifier Declarations | 1 |
| [N-32] | NatSpec: Public State variable declarations should have descriptions | 32 |
| [N-33] | Non-uppercase/Constant-case Naming for `immutable` Variables | 8 |
| [N-34] | Function Names Not in mixedCase | 13 |
| [N-35] | Insufficient Comments in Complex Functions | 3 |
| [N-36] | Common functions should be refactored to a common base contract | 4 |
| [N-37] | NatSpec: Error declarations should have descriptions | 1 |
| [N-38] | NatSpec: Non-public state variable declarations should use `@dev` tags | 2 |
| [N-39] | `constant`s should be defined rather than using magic numbers | 12 |
| [N-40] | Consider moving `msg.sender` checks to a common authorization `modifier` | 5 |
| [N-41] | NatSpec: Contract declarations should have `@author` tag | 1 |
| [N-42] | Consider defining system-wide constants in a single file | 10 |
| [N-43] | Add inline comments for unnamed variables | 1 |
| [N-44] | Consider making contracts `Upgradeable` | 2 |
| [N-45] | Style guide: Non-`external`/`public` variable names should begin with an underscore | 4 |
| [N-46] | Style guide: Contract does not follow the Solidity style guide's suggested layout ordering | 4 |
| [N-47] | Consider bounding input array length | 2 |
| [N-48] | NatSpec: Function declarations should have `@notice` tag | 19 |
| [N-49] | Constants in comparisons should appear on the left side | 8 |
| [N-50] | NatSpec: Contract declarations should have `@notice` tag | 1 |
| [N-51] | Named Imports of Parent Contracts Are Missing | 13 |
| [N-52] | Long functions should be refactored into multiple, smaller, functions | 3 |
| [N-53] | NatSpec: Contract declarations should have `@dev` tags | 2 |
| [N-54] | `public` functions not called by the contract should be declared `external` instead | 9 |
| [N-55] | Large multiples of ten should use scientific notation | 3 |
| [N-56] | `approve` can revert if the current approval is not zero | 1 |
| [N-57] | Style guide: Function ordering does not follow the Solidity style guide | 14 |
| [N-58] | Style guide: Extraneous whitespace | 3 |
| [N-59] | Contract/Libraries Names Do Not Match Their Filenames | 3 |
| [N-60] | Unused import | 3 |
| [N-61] | Consider using named mappings | 2 |
| [N-62] | Use of `override` is unnecessary | 20 |
| [N-63] | Setters should prevent re-setting of the same value | 12 |
| [N-64] | Use Unchecked for Divisions on Constant or Immutable Values | 6 |
| [N-65] | Contracts should have full test coverage | 1 |
| [N-66] | Large or complicated code bases should implement invariant tests | 1 |
| [N-67] | Implement Formal Verification Proofs to Improve Security | 1 |

Total: 547 instances of 67 issues

## Low Findings Details

### [L-01] Unsafe use of `transfer()/transferFrom()` with IERC20

Not all tokens adhere strictly to the ERC20 standard, even if they are largely accepted as compliant.
A prominent example is Tether (USDT) on L1, where the transfer() and transferFrom() functions do not return booleans, contrary to the standard's requirements.
Instead, these functions provide no return value at all.
This discrepancy can lead to issues when such tokens are cast to IERC20: their non-standard function signatures can cause calls to revert.
As a safer alternative, consider using OpenZeppelin's SafeERC20 library, which offers safeTransfer() and safeTransferFrom() functions to address these incompatibilities.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

824: IERC20(token).transfer(to, amount);
```
[824](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L824)
</details>

### [L-02] Centralization issue caused by admin privileges

There are priviliged roles that are a single point of failure, who can use critical functions, posing a centralization issue.

<details>
<summary><i>28 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

498: function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE)
512: function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE)
526: function setInstantMintLimitDuration(
    uint256 _instantMintLimitDuration
  ) external override onlyRole(CONFIGURER_ROLE)
540: function setInstantRedemptionLimitDuration(
    uint256 _instantRedemptionLimitDuratioin
  ) external override onlyRole(CONFIGURER_ROLE)
554: function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE)
567: function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE)
581: function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE)
599: function setMinimumRedemptionAmount(
    uint256 _minimumRedemptionAmount
  ) external override onlyRole(CONFIGURER_ROLE)
622: function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE)
638: function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE)
650: function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE)
663: function setInvestorBasedRateLimiter(
    address _investorBasedRateLimiter
  ) external override onlyRole(DEFAULT_ADMIN_ROLE)
768: function pauseMint() external onlyRole(PAUSER_ROLE)
774: function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE)
780: function pauseRedeem() external onlyRole(PAUSER_ROLE)
786: function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE)
794: function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
819: function retrieveTokens(
    address token,
    address to,
    uint256 amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE)
```
[498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512) | [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526) | [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567) | [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599) | [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622) | [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650) | [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663) | [768](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L768) | [774](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L774) | [780](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L780) | [786](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L786) | [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794) | [819](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819)

```solidity
File: contracts/ousg/rOUSG.sol

112: function __rOUSG_init(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing
128: function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing
613: function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE)
624: function burn(
    address _account,
    uint256 _amount
  ) external onlyRole(BURNER_ROLE)
642: function pause() external onlyRole(PAUSER_ROLE)
646: function unpause() external onlyRole(DEFAULT_ADMIN_ROLE)
650: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE)
656: function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE)
```
[112](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112) | [128](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128) | [613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613) | [624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624) | [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642) | [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650) | [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656)

```solidity
File: contracts/ousg/rOUSGFactory.sol

70: function deployRebasingOUSG(
    address kycRegistry,
    uint256 requirementGroup,
    address ousg,
    address oracle
  ) external onlyGuardian returns (address, address, address)
121: function multiexcall(
    ExCallData[] calldata exCallData
  ) external payable override onlyGuardian returns (bytes[] memory results)
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70) | [121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121)
</details>

### [L-03] `decimals()` is not part of the ERC20 standard

The `decimals` function is not part of the `ERC20` standard, and they may revert with some tokens if the don't also extend the `IERC20Metadata` interface.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

396: IERC20Metadata(address(buidl)).decimals() == 6,
```
[396](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L396)
</details>

### [L-04] Large transfers may not work with some `ERC20` tokens

Some `IERC20` implementations (e.g `UNI`, `COMP`)
            
- [COMP (Compound Protocol)](https://github.com/compound-finance/compound-protocol/blob/a3214f67b73310d547e00fc578e8355911c9d376/contracts/Governance/Comp.sol#L115-L142)
- [UNI (Uniswap)](https://github.com/Uniswap/governance/blob/eabd8c71ad01f61fb54ed6945162021ee419998e/contracts/Uni.sol#L209-L236)
            
may fail if the valued `transferred` is larger than `uint96`.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

824: IERC20(token).transfer(to, amount)
```
[824](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L824)
</details>

### [L-05] `assert()` should only be used for tests

From (documentation)[https://docs.soliditylang.org/en/v0.8.20/control-structures.html#panic-via-assert-and-error-via-require]:
```text
The assert function creates an error of type Panic(uint256). The same error is created by the compiler in certain situations as listed below.
Assert should only be used to test for internal errors, and to check invariants. Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix. Language analysis tools can evaluate your contract to identify the conditions and function calls which will cause a Panic.
```

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

94: assert(rOUSGProxyAdmin.owner() == guardian)
```
[94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94)
</details>

### [L-06] Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [CEI](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit - State change after external call: `rOUSGProxyAdmin.transferOwnership(guardian)`
95: initialized = true
```
[95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L95)
</details>

### [L-07] Initializers can be front-run

Initializers could be vulnerable to front-running attacks.
This might allow an attacker to set their own values, take ownership of the contract, or force a redeployment in the best-case scenario.
Be cautious of potential front-running risks in the following instances found in the code.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer
```
[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102)
</details>

### [L-08] `.call` bypasses function existence check, type checking and argument packing

Using the `.call` method in Solidity enables direct communication with an address, bypassing function existence checks, type checking, and argument packing.
While this can save gas and provide flexibility, it can also introduce security risks and potential errors. The absence of these checks can lead to unexpected behavior if the callee contract's interface changes or if the input parameters are not crafted with care.
The resolution to these issues is to use Solidity's high-level interface for calling functions when possible, as it automatically manages these aspects.
If using `.call` is necessary, ensure that the inputs are carefully validated and that awareness of the called contract's behavior is maintained.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

805: address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data)
```
[805](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805)

```solidity
File: contracts/ousg/rOUSGFactory.sol

126: address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data)
```
[126](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126)
</details>

### [L-09] Unbounded loop may run out of gas

Unbounded loops in smart contracts pose a risk because they iterate over an unknown number of elements, potentially consuming all available gas for a transaction.
This can result in unintended transaction failures. Gas consumption increases linearly with the number of iterations, and if it surpasses the gas limit, the transaction reverts, wasting the gas spent.
To mitigate this, developers should either set a maximum limit on loop iterations.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

804: for (uint256 i = 0; i < exCallData.length; ++i)
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
File: contracts/ousg/rOUSGFactory.sol

125: for (uint256 i = 0; i < exCallData.length; ++i)
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)
</details>

### [L-10] Lack of index element validation in external/public function

There's no validation to check whether the index element provided as an argument actually exists in the call. This omission could lead to unintended behavior if an element that does not exist in the call is passed to the function.

The function should validate that the provided index element exists in the call before proceeding.

Without this validation, the function could cause unintended behaviour as it will call an non-existing index element. This could lead to inconsistencies in data and potentially affect the integrity of the call structure.

<details>
<summary><i>5 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

235: allowances[_owner][_spender]
235: allowances[_owner]
281: allowances[_sender]
309: allowances[msg.sender][_spender]
332: allowances[msg.sender][_spender]
```
[235](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L235) | [235](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L235) | [281](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L281) | [309](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L309) | [332](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L332)
</details>

### [L-11] Consider checking that transfer to `address(this)` is disabled

Functions allowing users to specify the receiving address should check whether the referenced address is not `address(this)`.

This would prevent tokens to remain lock inside the contract due to an incorrect `transfer` or `mint`.

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

323: ousg.mint(to, ousgAmountOut)
824: IERC20(token).transfer(to, amount)
```
[323](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L323) | [824](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L824)
</details>

### [L-12] Unsafe solidity low-level call can cause gas grief attack

Using the low-level calls of a solidity address can leave the contract open to gas grief attacks.
These attacks occur when the called contract returns a large amount of data. So when calling an external contract, it is necessary to check the length of the return data before reading/copying it (using returndatasize()).

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

805: (bool success, bytes memory ret) = address(exCallData[i].target).call{
```
[805](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805)

```solidity
File: contracts/ousg/rOUSGFactory.sol

126: (bool success, bytes memory ret) = address(exCallData[i].target).call{
```
[126](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126)
</details>

### [L-13] Possible division by 0 is not prevented

These functions can be called with 0 value in the input and this value is not checked for being bigger than 0, that means in some scenarios this can potentially trigger a division by zero.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit pric - can be zero
690: ousgAmountOut = amountE36 / price;
```
[690](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L690)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit gtOUSGPric - can be zero
367: (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
```
[367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367)
</details>

### [L-14] Initializer missing `address(0)` Check before assignment

The initializer does not include a check for `address(0)` when initializing state variables that hold addresses.
Initializing a state variable with `address(0)` can lead to unintended behavior and vulnerabilities in the contract, 
such as sending funds to an inaccessible address. 
It is recommended to include a validation step to ensure that address parameters are not set to `address(0)`.

<details>
<summary><i>3 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit `_kycRegistry` has lack of `address(0)` check before use
101: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
/// @audit `_kycRegistry` has lack of `address(0)` check before use
111: function __rOUSG_init(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
/// @audit `_kycRegistry` has lack of `address(0)` check before use
/// @audit `_ousg` has lack of `address(0)` check before use
/// @audit `guardian` has lack of `address(0)` check before use
/// @audit `_oracle` has lack of `address(0)` check before use
127: function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
```
[101](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L101) | [111](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L111) | [127](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L127)
</details>

### [L-15] Missing checks for `address(0)` when updating state variables

Check for zero-address to avoid the risk of setting `address(0)` for state variables after an update.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

137: oracle = IRWAOracle(_oracle);
136: ousg = IERC20(_ousg);
```
[137](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L137) | [136](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L136)

```solidity
File: contracts/ousg/rOUSGFactory.sol

79: rOUSGProxy = new TokenProxy(
      address(rOUSGImplementation),
      address(rOUSGProxyAdmin),
      ""
    );
```
[79](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L79)
</details>

### [L-16] Risk of Renouncing Ownership While System is Paused

If the owner or a role-holder renounce or loses their role/ownership while the system is paused, it can lead to user assets becoming permanently locked.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

641: function pause() external onlyRole(PAUSER_ROLE) {
```
[641](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L641)
</details>

### [L-17] Consider the case where `totalSupply` is zero

The following functions should handle the edge case where the `totalSupply` is zero, for example to avoid division by zero errors, as such errors may negatively impact the logic of these functions.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

188: function totalSupply() public view returns (uint256) {
```
[188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188)
</details>

### [L-18] Missing checks for state variable assignments

There are some missing checks in these functions, and this could lead to unexpected scenarios. Consider always adding a sanity check for state variables.

<details>
<summary><i>6 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

501: _setInstantMintLimit(_instantMintLimit);
515: _setInstantRedemptionLimit(_instantRedemptionLimit);
529: _setInstantMintLimitDuration(_instantMintLimitDuration);
543: _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
```
[501](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L501) | [515](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L515) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L529) | [543](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L543)

```solidity
File: contracts/ousg/rOUSG.sol

653: _setKYCRegistry(registry);
659: _setKYCRequirementGroup(group);
```
[653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L653) | [659](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L659)
</details>

### [L-19] Missing checks in constructor/initialize

There are some missing checks in these functions, and this could lead to unexpected scenarios. Consider always adding a sanity check for state variables.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `rateLimiterConfig` passed to inherited constructor is not validated
144: constructor(
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
[144](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit `requirementGroup` is not validated before use
102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
```
[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102)
</details>

### [L-20] Missing contract-existence checks before low-level calls

Low-level calls return success if there is no code present at the specified address, and this could lead to unexpected scenarios.

Ensure that the code is initialized by checking `<address>.code.length > 0`

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

805: (bool success, bytes memory ret) = address(exCallData[i].target).call{
```
[805](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805)

```solidity
File: contracts/ousg/rOUSGFactory.sol

126: (bool success, bytes memory ret) = address(exCallData[i].target).call{
```
[126](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126)
</details>

### [L-21] Events may be emitted out of order due to reentrancy

It's essential to ensure that events follow the best practice of check-effects-interaction and are emitted before any external calls to prevent out-of-order events due to reentrancy.
Emitting events post external interactions may cause them to be out of order due to reentrancy, which can be misleading or erroneous for event listeners.
[Refer to the Solidity Documentation for best practices.](https://solidity.readthedocs.io/en/latest/security-considerations.html#reentrancy)

<details>
<summary><i>11 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `transfer()` before `InstantMintRebasingOUSG` event emit
270: emit InstantMintRebasingOUSG(
      msg.sender,
      usdcAmountIn,
      ousgAmountOut,
      rousgAmountOut
    );
/// @audit `transferFrom()` before `MintFeesDeducted` event emit
320: emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);
/// @audit `transferFrom()` before `InstantRedemptionOUSG` event emit
350: emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut);
/// @audit `transferFrom()` before `InstantRedemptionRebasingOUSG` event emit
380: emit InstantRedemptionRebasingOUSG(
      msg.sender,
      rousgAmountIn,
      ousgAmountIn,
      usdcAmountOut
    );
/// @audit `transfer()` before `RedeemFeesDeducted` event emit
453: emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);
```
[270](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L270) | [320](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L320) | [350](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L350) | [380](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L380) | [453](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L453)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit `transferFrom()` before `Transfer` event emit
420: emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
/// @audit `transferFrom()` before `TransferShares` event emit
421: emit TransferShares(address(0), msg.sender, ousgSharesAmount);
/// @audit `transfer()` before `Transfer` event emit
441: emit Transfer(msg.sender, address(0), _rOUSGAmount);
/// @audit `transfer()` before `TransferShares` event emit
442: emit TransferShares(msg.sender, address(0), ousgSharesAmount);
/// @audit `transfer()` before `Transfer` event emit
638: emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
/// @audit `transfer()` before `TransferShares` event emit
639: emit TransferShares(_account, address(0), ousgSharesAmount);
```
[420](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L420) | [421](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L421) | [441](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L441) | [442](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L442) | [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L638) | [639](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L639)
</details>

### [L-22] Critical functions should be a two step procedure

Critical functions in Solidity contracts should follow a two-step procedure to enhance security, minimize human error, and ensure proper access control. By dividing sensitive operations into distinct phases, such as initiation and confirmation, developers can introduce a safeguard against unintended actions or unauthorized access.

<details>
<summary><i>15 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

498: function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
512: function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
526: function setInstantMintLimitDuration(
    uint256 _instantMintLimitDuration
  ) external override onlyRole(CONFIGURER_ROLE) {
540: function setInstantRedemptionLimitDuration(
    uint256 _instantRedemptionLimitDuratioin
  ) external override onlyRole(CONFIGURER_ROLE) {
554: function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
567: function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {
581: function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
599: function setMinimumRedemptionAmount(
    uint256 _minimumRedemptionAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
622: function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
638: function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
650: function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
663: function setInvestorBasedRateLimiter(
    address _investorBasedRateLimiter
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
```
[498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512) | [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526) | [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567) | [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599) | [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622) | [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650) | [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663)

```solidity
File: contracts/ousg/rOUSG.sol

613: function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
649: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
655: function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE) {
```
[613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613) | [649](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L649) | [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L655)
</details>

### [L-23] Implement two-step ownership transfers

Single-step ownership transfers can be risky due to the potential for errors or wrong address inputs.
In worst-case scenarios, your contract could become `ownerless`.
To mitigate these risks, consider using a two-step ownership transfers.
In this process, a new potential owner is first designated, and then they must accept the ownership to complete the transfer.
This two-step procedure ensures a more secure and reliable transfer of contract ownership.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

93: rOUSGProxyAdmin.transferOwnership(guardian);
```
[93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L93)
</details>

### [L-24] Loss of precision on division

Solidity doesn't support fractions, so divisions by large numbers could result in the quotient being zero.

To avoid this, it's recommended to require a minimum numerator amount to ensure that it is always greater than the denominator.

<details>
<summary><i>12 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

377: uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /
      OUSG_TO_ROUSG_SHARES_MULTIPLIER;
690: ousgAmountOut = amountE36 / price;
704: usdcOwed = _scaleDown(amountE36 / 1e18);
716: return (usdcAmount * mintFee) / FEE_GRANULARITY;
728: return (usdcAmount * redeemFee) / FEE_GRANULARITY;
748: return amount / decimalsMultiplier;
```
[377](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L377) | [690](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L690) | [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704) | [716](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L716) | [728](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L728) | [748](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L748)

```solidity
File: contracts/ousg/rOUSG.sol

190: (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
201: (_sharesOf(_account) * getOUSGPrice()) /
      (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
367: (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
375: (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
439: ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
636: ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
```
[190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L190) | [201](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L201) | [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L375) | [439](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L439) | [636](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L636)
</details>

### [L-25] Unbounded Gas Consumption on External Calls

Consider using `addr.call{gas: <amount>}("")` to set a gas limit and prevent potential reversion due to gas consumption.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

805: (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
```
[805](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805)

```solidity
File: contracts/ousg/rOUSGFactory.sol

126: (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
```
[126](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126)
</details>

### [L-26] Lack of two-step update for updating protocol addresses

Add a two-step process for any critical address changes.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `feeReceiver` is changed
655: feeReceiver = _feeReceiver;
```
[655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L655)

```solidity
File: contracts/ousg/rOUSG.sol

653: _setKYCRegistry(registry);
659: _setKYCRequirementGroup(group);
```
[653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L653) | [659](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L659)
</details>

### [L-27] Potential Re-org Attack Vector

The contract appears to deploy new contracts using the `new` keyword.
In a re-org attack scenario, such deployments can be exploited by a malicious actor who might rewrite the blockchain's history and deploy the contract at an expected address. 

Consider deploying the contract via `CREATE2` opcode with a specific salt that includes `msg.sender` and the existing contract address.
This will ensure a predictable contract address, reducing the chances of such an attack.

<details>
<summary><i>3 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

77: rOUSGImplementation = new ROUSG();
78: rOUSGProxyAdmin = new ProxyAdmin();
79: rOUSGProxy = new TokenProxy(
```
[77](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L77) | [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L78) | [79](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L79)
</details>

### [L-28] Missing checks for `address(0)` in constructor

Check for zero-address to avoid the risk of setting `address(0)` for state variables when deploying.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `defaultAdmin` has lack of `address(0)` check before use
144: constructor(
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
[144](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit `_guardian` has lack of `address(0)` check before use
46: constructor(address _guardian) {
```
[46](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L46)
</details>

### [L-29] Missing `__gap[50]` storage variable in Upgradeable contracts

In the context of upgradeable contracts, ensuring forward compatibility between different contract versions is a critical concern. One key strategy for ensuring this compatibility is the use of a `__gap` storage variable.

The `__gap` variable acts as a reserved space in the contract's storage layout. This space can then be utilized for adding new state variables in future contract upgrades, while maintaining the original storage layout of the contract.

Without the `__gap` storage variable, adding new state variables in a contract upgrade can risk overwriting the existing contract storage, potentially leading to unpredictable behavior or data loss.

Therefore, if your contract is designed to be upgradeable, it's crucial to include a `__gap` storage variable. The absence of this variable in an upgradeable contract can signify a potential risk for future upgrades.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
```
[54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54)
</details>

### [L-30] Using a vulnerable dependency from some libraries

The package.json configuration file says that the project is using OZ which has a not last update version.
Latest non vulnerable version `4.9.3` for @openzeppelin/contracts and @openzeppelin/contracts-upgradeable.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: app/2024-03-ondo-finance/package.json

33: "@openzeppelin/contracts": "^4.8.3",
```
[33](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/app/2024-03-ondo-finance/package.json#L33)
</details>


## NonCritical Findings Details

### [N-01] Use custom errors instead of `require()/assert()`

Starting from Solidity 0.8.4, custom errors have been introduced to improve readability and clarity in your code. Instead of using `require()/assert()` with strings, custom errors can provide more expressive and understandable error conditions.

This change not only reduces unnecessary clutter in your codebase but also promotes a more streamlined contract structure, ultimately improving the quality of your Solidity code.

<details>
<summary><i>51 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

163: require(
      address(_usdc) != address(0),
      "OUSGInstantManager: USDC cannot be 0x0"
    )
167: require(
      address(_usdcReciever) != address(0),
      "OUSGInstantManager: USDC Receiver cannot be 0x0"
    )
171: require(
      address(_feeReceiver) != address(0),
      "OUSGInstantManager: feeReceiver cannot be 0x0"
    )
175: require(
      address(_ousgOracle) != address(0),
      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
    )
179: require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0")
180: require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0")
181: require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0")
182: require(
      address(_buidlRedeemer) != address(0),
      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    )
186: require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    )
190: require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    )
205: require(
      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
    )
282: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_mint: USDC decimals must be 6"
    )
286: require(
      usdcAmountIn >= minimumDepositAmount,
      "OUSGInstantManager::_mint: Deposit amount too small"
    )
298: require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    )
310: require(
      ousgAmountOut > 0,
      "OUSGInstantManager::_mint: net mint amount can't be zero"
    )
344: require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    )
371: require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    )
391: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_redeem: USDC decimals must be 6"
    )
395: require(
      IERC20Metadata(address(buidl)).decimals() == 6,
      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    )
402: require(
      usdcAmountToRedeem >= minimumRedemptionAmount,
      "OUSGInstantManager::_redeem: Redemption amount too small"
    )
417: require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    )
459: require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    )
466: require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    )
481: require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    )
557: require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high")
570: require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high")
584: require(
      _minimumDepositAmount >= FEE_GRANULARITY,
      "setMinimumDepositAmount: Amount too small"
    )
602: require(
      _minimumRedemptionAmount >= FEE_GRANULARITY,
      "setMinimumRedemptionAmount: Amount too small"
    )
653: require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0")
757: require(!mintPaused, "OUSGInstantManager: Mint paused")
763: require(!redeemPaused, "OUSGInstantManager: Redeem paused")
808: require(success, "Call Failed")
```
[163](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L163) | [167](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L167) | [171](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L171) | [175](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L175) | [179](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L179) | [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L180) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L181) | [182](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L182) | [186](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L186) | [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L190) | [205](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L205) | [282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L282) | [286](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L286) | [298](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L298) | [310](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310) | [344](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L344) | [371](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L371) | [391](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L391) | [395](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L395) | [402](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L402) | [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L417) | [459](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L459) | [466](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L466) | [481](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L481) | [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557) | [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570) | [584](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L584) | [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602) | [653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L653) | [757](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L757) | [763](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L763) | [808](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L808)

```solidity
File: contracts/ousg/rOUSG.sol

282: require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE")
333: require(
      currentAllowance >= _subtractedValue,
      "DECREASED_ALLOWANCE_BELOW_ZERO"
    )
416: require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens")
432: require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens")
477: require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS")
478: require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS")
506: require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS")
507: require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS")
512: require(
      _sharesAmount <= currentSenderShares,
      "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
    )
533: require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS")
558: require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS")
563: require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE")
594: require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd")
599: require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd")
604: require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd")
```
[282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L282) | [333](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L333) | [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416) | [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432) | [477](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L477) | [478](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L478) | [506](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506) | [507](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L507) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L512) | [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533) | [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L558) | [563](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L563) | [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L599) | [604](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L604)

```solidity
File: contracts/ousg/rOUSGFactory.sol

76: require(!initialized, "ROUSGFactory: rOUSG already deployed")
94: assert(rOUSGProxyAdmin.owner() == guardian)
129: require(success, "Call Failed")
150: require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian")
```
[76](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L76) | [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94) | [129](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L129) | [150](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L150)
</details>

### [N-02] Missing Event Emission After Critical Initialize() Function

Emitting an initialization event offers clear, on-chain evidence of the contract's initialization state, enhancing transparency and auditability.
This practice aids users and developers in accurately tracking the contract's lifecycle, pinpointing the precise moment of its initialization.
Moreover, it aligns with best practices for event logging in smart contracts, ensuring that significant state changes are both observable and verifiable through emitted events.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer
```
[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102)
</details>

### [N-03] Variables need not be initialized to zero

By default, `int/uint` variables in Solidity are initialized to `zero`.
Explicitly setting variables to zero during their declaration is redundant and might cause confusion.
Removing the explicit zero initialization can improve code readability and understanding.

<details>
<summary><i>4 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

99: uint256 public mintFee = 0;
102: uint256 public redeemFee = 0;
804: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[99](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L99) | [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L102) | [804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
File: contracts/ousg/rOUSGFactory.sol

125: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)
</details>

### [N-04] Variables need not be initialized to false

By default, boolean variables in Solidity are initialized to `false`.
Explicitly setting variables to `false` during their declaration is redundant and might cause confusion.
Removing the explicit zero initialization can improve code readability and understanding.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

45: bool public initialized = false;
```
[45](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45)
</details>

### [N-05] Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, for readability

Combining multiple address/ID mappings into a single mapping to a struct can enhance code clarity and maintainability. 
Consider refactoring multiple mappings into a single mapping with a struct for cleaner code structure.
This arrangement also promotes a more organized contract structure, making it easier for developers to navigate and understand.

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

72: mapping(address => uint256) private shares
75: mapping(address => mapping(address => uint256)) private allowances
```
[72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72) | [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75)
</details>

### [N-06] Consider returning a `struct` rather than having multiple `return` values

Functions that return many variables can become difficult to read and maintain.
Using a struct to encapsulate these return values can improve code readability, increase reusability, and reduce the likelihood of errors.
Consider refactoring functions that return more than three variables to use a struct instead.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

70: function deployRebasingOUSG(
    address kycRegistry,
    uint256 requirementGroup,
    address ousg,
    address oracle
  ) external onlyGuardian returns (address, address, address)
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70)
</details>

### [N-07] Consider using a `struct` rather than having many function input parameters

Functions with many parameters can become difficult to read and maintain. 
Using a struct to encapsulate these parameters can improve code readability, increase reusability, and reduce the likelihood of errors.
Consider refactoring functions that take more than three parameters to use a struct instead.

<details>
<summary><i>4 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

144: constructor(
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
```
[144](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144)

```solidity
File: contracts/ousg/rOUSG.sol

102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer
112: function __rOUSG_init(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing
128: function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing
```
[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102) | [112](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112) | [128](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128)
</details>

### [N-08] Avoid using constant decimals in expressions

The use of fixed decimal values such as `1e18/10 ** 18` in Solidity contracts can lead to bugs, and vulnerabilities, when interacting with tokens having different decimal configurations.
Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations.
        
Always retrieve and use the `decimals()` function from the token contract itself when performing calculations involving token amounts.
This ensures that your contract correctly handles tokens with any number of decimal places, mitigating the risk of numerical errors or under/overflows.

<details>
<summary><i>6 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

689: uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;
704: usdcOwed = _scaleDown(amountE36 / 1e18);
```
[689](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L689) | [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704)

```solidity
File: contracts/ousg/rOUSG.sol

190: (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
202: (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
367: (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
375: (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
```
[190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L190) | [202](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L202) | [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L375)
</details>

### [N-09] Custom error has no error details

Take advantage of custom error's return value property. 

An important feature of Custom Error is that values such as address, tokenID, msg.value can be written inside the () sign, providing a serious advantage in debugging and examining the revert details of dapps such as Tenderly.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

90: error UnwrapTooSmall()
```
[90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)
</details>

### [N-10] Consider using `delete` rather than assigning `false` to clear values

The use of the delete keyword is recommended over simply assigning values to false when you intend to reset the state of a variable.
The delete keyword more closely aligns with the semantic intent of clearing or resetting a variable.
This practice also makes the code more readable and highlights the change in state, which may encourage a more thorough audit of the surrounding logic.

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

775: mintPaused = false
787: redeemPaused = false
```
[775](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L775) | [787](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L787)
</details>

### [N-11] Consider emitting an event at the end of the constructor

This will allow users to easily exactly pinpoint when and by whom a contract was constructed.

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

144: constructor(
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
```
[144](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144)

```solidity
File: contracts/ousg/rOUSG.sol

98: constructor()
```
[98](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L98)

```solidity
File: contracts/ousg/rOUSGFactory.sol

47: constructor(address _guardian)
```
[47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)
</details>

### [N-12] Consider using named returns

Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas.
The cases below are where there currently is at most one return statement, which is ideal for named returns.

<details>
<summary><i>24 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

713: function _getInstantMintFees(
    uint256 usdcAmount
  ) internal view returns (uint256)
725: function _getInstantRedemptionFees(
    uint256 usdcAmount
  ) internal view returns (uint256)
737: function _scaleUp(uint256 amount) internal view returns (uint256)
747: function _scaleDown(uint256 amount) internal view returns (uint256)
```
[713](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L713) | [725](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L725) | [737](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L737) | [747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L747)

```solidity
File: contracts/ousg/rOUSG.sol

166: function name() public pure returns (string memory)
174: function symbol() public pure returns (string memory)
181: function decimals() public pure returns (uint8)
188: function totalSupply() public view returns (uint256)
199: function balanceOf(address _account) public view returns (uint256)
220: function transfer(address _recipient, uint256 _amount) public returns (bool)
231: function allowance(
    address _owner,
    address _spender
  ) public view returns (uint256)
251: function approve(address _spender, uint256 _amount) public returns (bool)
276: function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool)
302: function increaseAllowance(
    address _spender,
    uint256 _addedValue
  ) public returns (bool)
328: function decreaseAllowance(
    address _spender,
    uint256 _subtractedValue
  ) public returns (bool)
347: function getTotalShares() public view returns (uint256)
356: function sharesOf(address _account) public view returns (uint256)
363: function getSharesByROUSG(
    uint256 _rOUSGAmount
  ) public view returns (uint256)
373: function getROUSGByShares(uint256 _shares) public view returns (uint256)
397: function transferShares(
    address _recipient,
    uint256 _sharesAmount
  ) public returns (uint256)
487: function _sharesOf(address _account) internal view returns (uint256)
529: function _mintShares(
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256)
554: function _burnShares(
    address _account,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256)
```
[166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L166) | [174](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L174) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L181) | [188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188) | [199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L199) | [220](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L220) | [231](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L231) | [251](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L251) | [276](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L276) | [302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302) | [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328) | [347](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L347) | [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356) | [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363) | [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373) | [397](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397) | [487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L487) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554)

```solidity
File: contracts/ousg/rOUSGFactory.sol

70: function deployRebasingOUSG(
    address kycRegistry,
    uint256 requirementGroup,
    address ousg,
    address oracle
  ) external onlyGuardian returns (address, address, address)
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70)
</details>

### [N-13] Consider using named function arguments

When calling functions in external contracts with multiple arguments, consider using named function parameters, rather than positional ones.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

292: investorBasedRateLimiter.checkAndUpdateMintLimit(
        msg.sender,
        usdcAmountIn
      )
409: investorBasedRateLimiter.checkAndUpdateRedeemLimit(
        msg.sender,
        usdcAmountToRedeem
      )
```
[292](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L292) | [409](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L409)

```solidity
File: contracts/ousg/rOUSGFactory.sol

85: rOUSGProxied.initialize(
      kycRegistry,
      requirementGroup,
      ousg,
      guardian,
      oracle
    )
```
[85](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L85)
</details>

### [N-14] Function Parameters in Public Accessible Functions Need `address(0)` Check

Parameters of type `address` in your functions should be checked to ensure that they are not assigned the null address (`address(0x0)`). 
Failure to validate these parameters can lead to transaction reverts, wasted gas, the need for transaction resubmission, and may even require redeployment of contracts within the protocol in certain situations.
Implement checks for `address(0x0)` to avoid these potential issues.

<details>
<summary><i>17 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `_oracle` parameter without address(0) check
638: function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
/// @audit `_investorBasedRateLimiter` parameter without address(0) check
663: function setInvestorBasedRateLimiter(
    address _investorBasedRateLimiter
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
/// @audit `token` parameter without address(0) check
/// @audit `to` parameter without address(0) check
819: function retrieveTokens(
    address token,
    address to,
    uint256 amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
```
[638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638) | [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663) | [819](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit `_kycRegistry` parameter without address(0) check
/// @audit `_ousg` parameter without address(0) check
/// @audit `guardian` parameter without address(0) check
/// @audit `_oracle` parameter without address(0) check
102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
/// @audit `_account` parameter without address(0) check
199: function balanceOf(address _account) public view returns (uint256) {
/// @audit `_recipient` parameter without address(0) check
220: function transfer(address _recipient, uint256 _amount) public returns (bool) {
/// @audit `_owner` parameter without address(0) check
/// @audit `_spender` parameter without address(0) check
231: function allowance(
    address _owner,
    address _spender
  ) public view returns (uint256) {
/// @audit `_spender` parameter without address(0) check
251: function approve(address _spender, uint256 _amount) public returns (bool) {
/// @audit `_sender` parameter without address(0) check
/// @audit `_recipient` parameter without address(0) check
276: function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
/// @audit `_spender` parameter without address(0) check
302: function increaseAllowance(
    address _spender,
    uint256 _addedValue
  ) public returns (bool) {
/// @audit `_spender` parameter without address(0) check
328: function decreaseAllowance(
    address _spender,
    uint256 _subtractedValue
  ) public returns (bool) {
/// @audit `_account` parameter without address(0) check
356: function sharesOf(address _account) public view returns (uint256) {
/// @audit `_recipient` parameter without address(0) check
397: function transferShares(
    address _recipient,
    uint256 _sharesAmount
  ) public returns (uint256) {
/// @audit `_oracle` parameter without address(0) check
613: function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
/// @audit `_account` parameter without address(0) check
624: function burn(
    address _account,
    uint256 _amount
  ) external onlyRole(BURNER_ROLE) {
/// @audit `registry` parameter without address(0) check
650: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
```
[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102) | [199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L199) | [220](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L220) | [231](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L231) | [251](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L251) | [276](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L276) | [302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302) | [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328) | [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356) | [397](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397) | [613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613) | [624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit `kycRegistry` parameter without address(0) check
/// @audit `ousg` parameter without address(0) check
/// @audit `oracle` parameter without address(0) check
70: function deployRebasingOUSG(
    address kycRegistry,
    uint256 requirementGroup,
    address ousg,
    address oracle
  ) external onlyGuardian returns (address, address, address) {
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70)
</details>

### [N-15] Events are missing sender information

Events should include the sender information when emitted in `public` or `external` functions for better traceability.

<details>
<summary><i>15 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit external function `setMintFee()` emits an event without sender information
558: emit MintFeeSet(mintFee, _mintFee);
/// @audit external function `setRedeemFee()` emits an event without sender information
571: emit RedeemFeeSet(redeemFee, _redeemFee);
/// @audit external function `setMinimumDepositAmount()` emits an event without sender information
588: emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
/// @audit external function `setMinimumRedemptionAmount()` emits an event without sender information
606: emit MinimumRedemptionAmountSet(
      minimumRedemptionAmount,
      _minimumRedemptionAmount
    );
/// @audit external function `setMinimumBUIDLRedemptionAmount()` emits an event without sender information
625: emit MinimumBUIDLRedemptionAmountSet(
      minBUIDLRedeemAmount,
      _minimumBUIDLRedemptionAmount
    );
/// @audit external function `setOracle()` emits an event without sender information
641: emit OracleSet(address(oracle), _oracle);
/// @audit external function `setFeeReceiver()` emits an event without sender information
654: emit FeeReceiverSet(feeReceiver, _feeReceiver);
/// @audit external function `setInvestorBasedRateLimiter()` emits an event without sender information
666: emit InvestorBasedRateLimiterSet(
      address(investorBasedRateLimiter),
      _investorBasedRateLimiter
    );
/// @audit external function `pauseMint()` emits an event without sender information
770: emit MintPaused();
/// @audit external function `unpauseMint()` emits an event without sender information
776: emit MintUnpaused();
/// @audit external function `pauseRedeem()` emits an event without sender information
782: emit RedeemPaused();
/// @audit external function `unpauseRedeem()` emits an event without sender information
788: emit RedeemUnpaused();
```
[558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L558) | [571](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L571) | [588](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L588) | [606](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L606) | [625](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L625) | [641](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L641) | [654](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L654) | [666](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L666) | [770](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L770) | [776](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L776) | [782](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L782) | [788](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L788)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit external function `setOracle()` emits an event without sender information
614: emit OracleSet(address(oracle), _oracle);
/// @audit external function `burn()` emits an event without sender information
639: emit TransferShares(_account, address(0), ousgSharesAmount);
```
[614](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L614) | [639](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L639)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit external function `deployRebasingOUSG()` emits an event without sender information
96: emit rOUSGDeployed(
      address(rOUSGProxy),
      address(rOUSGProxyAdmin),
      address(rOUSGImplementation),
      rOUSGProxied.name(),
      rOUSGProxied.symbol()
    );
```
[96](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L96)
</details>

### [N-16] Leverage Recent Solidity Features with `0.8.23`

The recent updates in Solidity provide several features and optimizations that, when leveraged appropriately, can significantly improve your contract's code clarity and maintainability.
Key enhancements include the use of push0 for placing 0 on the stack for EVM versions starting from "Shanghai", making your code simpler and more straightforward.
Moreover, Solidity has extended NatSpec documentation support to enum and struct definitions, facilitating more comprehensive and insightful code documentation.

Additionally, the re-implementation of the UnusedAssignEliminator and UnusedStoreEliminator in the Solidity optimizer provides the ability to remove unused assignments in deeply nested loops.
This results in a cleaner, more efficient contract code, reducing clutter and potential points of confusion during code review or debugging.
It's recommended to make full use of these features and optimizations to enhance the robustness and readability of your smart contracts.

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L16)

```solidity
File: contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L16)

```solidity
File: contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L16)
</details>

### [N-17] NatSpec: Function `@param` tag is missing

Natural Specification (NatSpec) comments are crucial for understanding the role of function arguments in your Solidity code.
Including `@param` tags will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose.

[More information in Documentation](https://docs.soliditylang.org/en/develop/natspec-format.html)

<details>
<summary><i>30 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit Missed @param `usdcAmountIn, to`
278: function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {
/// @audit Missed @param `ousgAmountIn`
388: function _redeem(
    uint256 ousgAmountIn
  ) internal returns (uint256 usdcAmountOut) {
/// @audit Missed @param `buidlAmountToRedeem`
458: function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
/// @audit Missed @param `amount`
737: function _scaleUp(uint256 amount) internal view returns (uint256) {
/// @audit Missed @param `amount`
747: function _scaleDown(uint256 amount) internal view returns (uint256) {
/// @audit Missed @param `exCallData`
794: function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
```
[278](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278) | [388](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388) | [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458) | [737](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L737) | [747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L747) | [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit Missed @param `_kycRegistry, requirementGroup, _ousg, guardian, _oracle`
102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
/// @audit Missed @param `_kycRegistry, requirementGroup, _ousg, guardian, _oracle`
112: function __rOUSG_init(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
/// @audit Missed @param `_kycRegistry, _requirementGroup, _ousg, guardian, _oracle`
128: function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
/// @audit Missed @param `_account`
199: function balanceOf(address _account) public view returns (uint256) {
/// @audit Missed @param `_recipient, _amount`
220: function transfer(address _recipient, uint256 _amount) public returns (bool) {
/// @audit Missed @param `_owner, _spender`
231: function allowance(
    address _owner,
    address _spender
  ) public view returns (uint256) {
/// @audit Missed @param `_spender, _amount`
251: function approve(address _spender, uint256 _amount) public returns (bool) {
/// @audit Missed @param `_sender, _recipient, _amount`
276: function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
/// @audit Missed @param `_spender, _addedValue`
302: function increaseAllowance(
    address _spender,
    uint256 _addedValue
  ) public returns (bool) {
/// @audit Missed @param `_spender, _subtractedValue`
328: function decreaseAllowance(
    address _spender,
    uint256 _subtractedValue
  ) public returns (bool) {
/// @audit Missed @param `_account`
356: function sharesOf(address _account) public view returns (uint256) {
/// @audit Missed @param `_rOUSGAmount`
363: function getSharesByROUSG(
    uint256 _rOUSGAmount
  ) public view returns (uint256) {
/// @audit Missed @param `_shares`
373: function getROUSGByShares(uint256 _shares) public view returns (uint256) {
/// @audit Missed @param `_recipient, _sharesAmount`
397: function transferShares(
    address _recipient,
    uint256 _sharesAmount
  ) public returns (uint256) {
/// @audit Missed @param `_sender, _recipient, _amount`
450: function _transfer(
    address _sender,
    address _recipient,
    uint256 _amount
  ) internal {
/// @audit Missed @param `_owner, _spender, _amount`
472: function _approve(
    address _owner,
    address _spender,
    uint256 _amount
  ) internal whenNotPaused {
/// @audit Missed @param `_account`
487: function _sharesOf(address _account) internal view returns (uint256) {
/// @audit Missed @param `_sender, _recipient, _sharesAmount`
501: function _transferShares(
    address _sender,
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused {
/// @audit Missed @param `_recipient, _sharesAmount`
529: function _mintShares(
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
/// @audit Missed @param `_account, _sharesAmount`
554: function _burnShares(
    address _account,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
/// @audit Missed @param `from, to, uint256`
586: function _beforeTokenTransfer(
    address from,
    address to,
    uint256
  ) internal view {
/// @audit Missed @param `registry`
650: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
/// @audit Missed @param `group`
656: function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE) {
```
[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102) | [112](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112) | [128](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128) | [199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L199) | [220](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L220) | [231](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L231) | [251](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L251) | [276](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L276) | [302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302) | [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328) | [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356) | [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363) | [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373) | [397](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397) | [450](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L450) | [472](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L472) | [487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L487) | [501](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L501) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554) | [586](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L586) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650) | [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit Missed @param `_guardian`
47: constructor(address _guardian) {
```
[47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)
</details>

### [N-18] NatSpec: Function declarations should have descriptions

The Ethereum Natural Specification Format (NatSpec) is an integral part of the Solidity language, serving as a rich, machine-readable, language-agnostic metadata tool.

Documenting all functions, irrespective of their visibility, significantly enhances code readability and auditability.
This is especially vital in complex projects, where clear comprehension of functions, their arguments, and returns is paramount.

Specifically, the `@notice` tag should be used for explanations that anyone should understand, making it a key element in providing a clear understanding of a function's intention.
[More information in Documentation](https://docs.soliditylang.org/en/develop/natspec-format.html)

<details>
<summary><i>15 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

794: function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
```
[794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794)

```solidity
File: contracts/ousg/rOUSG.sol

98: constructor() {
102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
166: function name() public pure returns (string memory) {
174: function symbol() public pure returns (string memory) {
181: function decimals() public pure returns (uint8) {
188: function totalSupply() public view returns (uint256) {
363: function getSharesByROUSG(
    uint256 _rOUSGAmount
  ) public view returns (uint256) {
373: function getROUSGByShares(uint256 _shares) public view returns (uint256) {
378: function getOUSGPrice() public view returns (uint256 price) {
642: function pause() external onlyRole(PAUSER_ROLE) {
646: function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
650: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
656: function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE) {
```
[98](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L98) | [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102) | [166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L166) | [174](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L174) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L181) | [188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188) | [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363) | [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373) | [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378) | [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642) | [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650) | [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656)

```solidity
File: contracts/ousg/rOUSGFactory.sol

47: constructor(address _guardian) {
```
[47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)
</details>

### [N-19] Contract uses both `require()`/`revert()` as well as custom errors

The contract uses both `require()/revert()` and `custom errors` for error handling.

It's recommended to use a consistent approach for error handling in a single file.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
```
[54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54)
</details>

### [N-20] Event Names Not Following `CapWords` Style (CamelCase)

Event names should adhere to the `CapWords` style for better readability and to maintain consistency with Solidity style guidelines.
Examples of best practices in naming include: TransferCompleted, ApprovalGranted, NewDeposit, OwnershipTransferred.
[Refer to Solidity's Documentation for Style Guidelines](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#event-names)

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

141: event rOUSGDeployed(
    address proxy,
    address proxyAdmin,
    address implementation,
    string name,
    string ticker
  );
```
[141](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141)
</details>

### [N-21] Inconsistent spacing in comments

Some lines use // x and some use //x. The instances below point out the usages that don't follow the majority, within each file:

<details>
<summary><i>20 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

216: /*//////////////////////////////////////////////////////////////
218: //////////////////////////////////////////////////////////////*/
487: /*//////////////////////////////////////////////////////////////
489: //////////////////////////////////////////////////////////////*/
546: /*//////////////////////////////////////////////////////////////
548: //////////////////////////////////////////////////////////////*/
613: /*//////////////////////////////////////////////////////////////
615: //////////////////////////////////////////////////////////////*/
675: /*//////////////////////////////////////////////////////////////
677: //////////////////////////////////////////////////////////////*/
751: /*//////////////////////////////////////////////////////////////
753: //////////////////////////////////////////////////////////////*/
755: /// @notice Ensure that the mint functionality is not paused
761: /// @notice Ensure that the redeem functionality is not paused
767: /// @notice Pause the mint functionality
773: /// @notice Unpause the mint functionality
779: /// @notice Pause the redeem functionality
785: /// @notice Unpause the redeem functionality
791: /*//////////////////////////////////////////////////////////////
793: //////////////////////////////////////////////////////////////*/
```
[216](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L216) | [218](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L218) | [487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L487) | [489](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L489) | [546](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L546) | [548](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L548) | [613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L613) | [615](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L615) | [675](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L675) | [677](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L677) | [751](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L751) | [753](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L753) | [755](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L755) | [761](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L761) | [767](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L767) | [773](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L773) | [779](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L779) | [785](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L785) | [791](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L791) | [793](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L793)
</details>

### [N-22] Critical system parameter changes should be behind a timelock

It is a good practice to give time for users to react and adjust to critical changes. A timelock provides more guarantees and reduces the level of trust required, thus decreasing risk for users. It also indicates that the project is legitimate (less risk of a malicious owner making a sandwich attack on a user).

<details>
<summary><i>15 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

498: function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
512: function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
526: function setInstantMintLimitDuration(
    uint256 _instantMintLimitDuration
  ) external override onlyRole(CONFIGURER_ROLE) {
540: function setInstantRedemptionLimitDuration(
    uint256 _instantRedemptionLimitDuratioin
  ) external override onlyRole(CONFIGURER_ROLE) {
554: function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
567: function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {
581: function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
599: function setMinimumRedemptionAmount(
    uint256 _minimumRedemptionAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
622: function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
638: function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
650: function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
663: function setInvestorBasedRateLimiter(
    address _investorBasedRateLimiter
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
```
[498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512) | [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526) | [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567) | [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599) | [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622) | [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650) | [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663)

```solidity
File: contracts/ousg/rOUSG.sol

613: function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
649: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
655: function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE) {
```
[613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613) | [649](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L649) | [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L655)
</details>

### [N-23] Outdated Solidity Version

The current Solidity version used in the contract is outdated.
Consider using a more recent version for improved features and security.

0.8.4: bytes.concat() instead of abi.encodePacked(,)

0.8.12: string.concat() instead of abi.encodePacked(,)

0.8.13: Ability to use using for with a list of free functions

0.8.14:
    ABI Encoder: When ABI-encoding values from calldata that contain nested arrays, correctly validate the nested array length against calldatasize() in all cases. Override Checker: Allow changing data location for parameters only when overriding external functions.

0.8.15:
    Code Generation: Avoid writing dirty bytes to storage when copying bytes arrays. Yul Optimizer: Keep all memory side-effects of inline assembly blocks.

0.8.16:
    Code Generation: Fix data corruption that affected ABI-encoding of calldata values represented by tuples: structs at any nesting level; argument lists of external functions, events and errors; return value lists of external functions. The 32 leading bytes of the first dynamically-encoded value in the tuple would get zeroed when the last component contained a statically-encoded array.

0.8.17:
    Yul Optimizer: Prevent the incorrect removal of storage writes before calls to Yul functions that conditionally terminate the external EVM call.

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L16)

```solidity
File: contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L16)

```solidity
File: contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L16)
</details>

### [N-24] Function/Constructor Argument Names Not in mixedCase

Underscore before of after function argument names is a common convention in Solidity NOT a documentation requirement.

Function arguments should use mixedCase for better readability and consistency with Solidity style guidelines. 
Examples of good practice include: initialSupply, account, recipientAddress, senderAddress, newOwner. 
[More information in Documentation](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#function-argument-names)

Rule exceptions
- Allow constant variable name/symbol/decimals to be lowercase (ERC20).
- Allow `_` at the beginning of the mixedCase match for `private variables` and `unused parameters`.

<details>
<summary><i>38 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

498: function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
512: function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
526: function setInstantMintLimitDuration(
    uint256 _instantMintLimitDuration
  ) external override onlyRole(CONFIGURER_ROLE) {
540: function setInstantRedemptionLimitDuration(
    uint256 _instantRedemptionLimitDuratioin
  ) external override onlyRole(CONFIGURER_ROLE) {
554: function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
567: function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {
581: function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
599: function setMinimumRedemptionAmount(
    uint256 _minimumRedemptionAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
622: function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
638: function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
650: function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
663: function setInvestorBasedRateLimiter(
    address _investorBasedRateLimiter
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
144: constructor(
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
[498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512) | [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526) | [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567) | [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599) | [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622) | [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650) | [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663) | [144](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144)

```solidity
File: contracts/ousg/rOUSG.sol

101: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
111: function __rOUSG_init(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
127: function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
199: function balanceOf(address _account) public view returns (uint256) {
220: function transfer(address _recipient, uint256 _amount) public returns (bool) {
231: function allowance(
    address _owner,
    address _spender
  ) public view returns (uint256) {
251: function approve(address _spender, uint256 _amount) public returns (bool) {
276: function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
302: function increaseAllowance(
    address _spender,
    uint256 _addedValue
  ) public returns (bool) {
328: function decreaseAllowance(
    address _spender,
    uint256 _subtractedValue
  ) public returns (bool) {
356: function sharesOf(address _account) public view returns (uint256) {
363: function getSharesByROUSG(
    uint256 _rOUSGAmount
  ) public view returns (uint256) {
373: function getROUSGByShares(uint256 _shares) public view returns (uint256) {
397: function transferShares(
    address _recipient,
    uint256 _sharesAmount
  ) public returns (uint256) {
415: function wrap(uint256 _OUSGAmount) external whenNotPaused {
431: function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
450: function _transfer(
    address _sender,
    address _recipient,
    uint256 _amount
  ) internal {
472: function _approve(
    address _owner,
    address _spender,
    uint256 _amount
  ) internal whenNotPaused {
487: function _sharesOf(address _account) internal view returns (uint256) {
501: function _transferShares(
    address _sender,
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused {
529: function _mintShares(
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
554: function _burnShares(
    address _account,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
613: function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
624: function burn(
    address _account,
    uint256 _amount
  ) external onlyRole(BURNER_ROLE) {
```
[101](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L101) | [111](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L111) | [127](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L127) | [199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L199) | [220](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L220) | [231](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L231) | [251](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L251) | [276](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L276) | [302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302) | [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328) | [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356) | [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363) | [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373) | [397](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397) | [415](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415) | [431](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L431) | [450](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L450) | [472](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L472) | [487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L487) | [501](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L501) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554) | [613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613) | [624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624)

```solidity
File: contracts/ousg/rOUSGFactory.sol

46: constructor(address _guardian) {
```
[46](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L46)
</details>

### [N-25] NatSpec: Function `@return` tag is missing

Natural Specification (NatSpec) comments are crucial for understanding the role of function arguments in your Solidity code.
Including `@return` tag will not only improve your code's readability but also its maintainability by clearly defining each argument's purpose.

[More information in Documentation](https://docs.soliditylang.org/en/develop/natspec-format.html)

<details>
<summary><i>15 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit Missed @return `ousgAmountOut`
278: function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {
/// @audit Missed @return `usdcAmountOut`
388: function _redeem(
    uint256 ousgAmountIn
  ) internal returns (uint256 usdcAmountOut) {
/// @audit Missed @return `ousgAmountOut`
685: function _getMintAmount(
    uint256 usdcAmountIn,
    uint256 price
  ) internal view returns (uint256 ousgAmountOut) {
/// @audit Missed @return `usdcOwed`
699: function _getRedemptionAmount(
    uint256 ousgAmountBurned,
    uint256 price
  ) internal view returns (uint256 usdcOwed) {
/// @audit Missed @return ``
713: function _getInstantMintFees(
    uint256 usdcAmount
  ) internal view returns (uint256) {
/// @audit Missed @return ``
725: function _getInstantRedemptionFees(
    uint256 usdcAmount
  ) internal view returns (uint256) {
/// @audit Missed @return ``
737: function _scaleUp(uint256 amount) internal view returns (uint256) {
/// @audit Missed @return ``
747: function _scaleDown(uint256 amount) internal view returns (uint256) {
/// @audit Missed @return `results`
794: function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
```
[278](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278) | [388](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388) | [685](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L685) | [699](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L699) | [713](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L713) | [725](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L725) | [737](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L737) | [747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L747) | [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit Missed @return ``
302: function increaseAllowance(
    address _spender,
    uint256 _addedValue
  ) public returns (bool) {
/// @audit Missed @return ``
328: function decreaseAllowance(
    address _spender,
    uint256 _subtractedValue
  ) public returns (bool) {
/// @audit Missed @return `price`
378: function getOUSGPrice() public view returns (uint256 price) {
/// @audit Missed @return ``
529: function _mintShares(
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
/// @audit Missed @return ``
554: function _burnShares(
    address _account,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
```
[302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302) | [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328) | [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit Missed @return `results`
121: function multiexcall(
    ExCallData[] calldata exCallData
  ) external payable override onlyGuardian returns (bytes[] memory results) {
```
[121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121)
</details>

### [N-26] State-Altering Functions Should Emit Events

Functions that alter state should emit events to inform users of the state change.
This is crucial for functions that modify the state and don't return a value.
The absence of events in such scenarios could lead to lack of transparency and traceability, undermining the contract's reliability.

<details>
<summary><i>3 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

136: ousg = IERC20(_ousg);
537: totalShares += _sharesAmount;
565: totalShares -= _sharesAmount;
```
[136](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L136) | [537](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L537) | [565](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L565)
</details>

### [N-27] Upgrade `openzeppelin` to the Latest Version - 5.0.0

These contracts import contracts from @openzeppelin/contracts but they are not using the latest version.
For more information, please visit: [OpenZeppelin GitHub Releases](https://github.com/OpenZeppelin/openzeppelin-contracts/releases)
It is recommended to always use the latest version to take advantage of updates and security fixes.

<details>
<summary><i>11 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

18: import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";
19: import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";
20: import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";
```
[18](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L18) | [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L19) | [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L20)

```solidity
File: contracts/ousg/rOUSG.sol

18: import "contracts/external/openzeppelin/contracts/token/IERC20.sol";
19: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";
20: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";
21: import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";
22: import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";
23: import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";
24: import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";
```
[18](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L18) | [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L19) | [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L20) | [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L21) | [22](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L22) | [23](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L23) | [24](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L24)

```solidity
File: contracts/ousg/rOUSGFactory.sol

19: import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";
```
[19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19)
</details>

### [N-28] Duplicated `require()`/`revert()` checks should be refactored to a modifier or function

Duplicated require() or revert() checks should be refactored to a modifier or function.
This helps in maintaining a clean and organized codebase and saves deployment costs.

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

434: if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
      revert UnwrapTooSmall();
629: if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
      revert UnwrapTooSmall();
```
[434](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L434) | [629](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L629)
</details>

### [N-29] Non-specific Imports

The current form of relative path import is not recommended for use because it can unpredictably pollute the namespace.
Instead, the Solidity docs recommend specifying imported symbols explicitly.
https://docs.soliditylang.org/en/v0.8.15/layout-of-source-files.html#importing-other-source-files

Example:
import {OwnableUpgradeable} from "openzeppelin-contracts-upgradeable/contracts/access/OwnableUpgradeable.sol";
import {SafeTransferLib} from "solmate/utils/SafeTransferLib.sol";

<details>
<summary><i>23 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

18: import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";
19: import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";
20: import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";
21: import "contracts/ousg/rOUSG.sol";
22: import "contracts/interfaces/IRWALike.sol";
23: import "contracts/interfaces/IBUIDLRedeemer.sol";
24: import "contracts/InstantMintTimeBasedRateLimiter.sol";
25: import "contracts/interfaces/IOUSGInstantManager.sol";
26: import "contracts/interfaces/IMulticall.sol";
27: import "contracts/interfaces/IInvestorBasedRateLimiter.sol";
```
[18](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L18) | [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L19) | [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L20) | [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L21) | [22](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L22) | [23](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L23) | [24](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L24) | [25](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L25) | [26](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L26) | [27](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L27)

```solidity
File: contracts/ousg/rOUSG.sol

18: import "contracts/external/openzeppelin/contracts/token/IERC20.sol";
19: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";
20: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";
21: import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";
22: import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";
23: import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";
24: import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";
25: import "contracts/kyc/KYCRegistryClientUpgradeable.sol";
26: import "contracts/rwaOracles/IRWAOracle.sol";
```
[18](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L18) | [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L19) | [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L20) | [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L21) | [22](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L22) | [23](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L23) | [24](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L24) | [25](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L25) | [26](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L26)

```solidity
File: contracts/ousg/rOUSGFactory.sol

19: import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";
20: import "contracts/Proxy.sol";
21: import "contracts/ousg/rOUSG.sol";
22: import "contracts/interfaces/IMulticall.sol";
```
[19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19) | [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L20) | [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L21) | [22](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L22)
</details>

### [N-30] Event is not properly `indexed`

Index event fields make the field more quickly accessible to off-chain tools that parse events.
This is especially useful when it comes to filtering based on an address. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields).
Where applicable, each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question.
If there are fewer than three applicable fields, all of the applicable fields should be indexed.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

149: event TransferShares(
    address indexed from,
    address indexed to,
    uint256 sharesValue
  );
```
[149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L149)

```solidity
File: contracts/ousg/rOUSGFactory.sol

141: event rOUSGDeployed(
    address proxy,
    address proxyAdmin,
    address implementation,
    string name,
    string ticker
  );
```
[141](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141)
</details>

### [N-31] Missing NatSpec Descriptions for Modifier Declarations

Modifiers in the contract should include NatSpec comments, specifically with the `@dev` or `@notice` tags to elucidate their role and input parameters.
These annotations assist in offering a clearer insight into the contract's operation for developers, auditors, and end-users.
[Additional Details in Solidity Documentation](https://docs.soliditylang.org/en/latest/natspec-format.html)

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

149: modifier onlyGuardian() {
```
[149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149)
</details>

### [N-32] NatSpec: Public State variable declarations should have descriptions

State variables should ideally be accompanied by NatSpec comments to describe their purpose and usage. 
This aids developers in understanding the function and purpose of each variable, especially in large and complex contracts.
Consider adding `@dev` or `@notice` descriptions to your state variables.

<details>
<summary><i>32 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

57: bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
60: bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
63: uint256 public constant MINIMUM_OUSG_PRICE = 105e18;
66: uint256 public constant FEE_GRANULARITY = 10_000;
69: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
72: IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;
75: IRWALike public immutable ousg;
78: ROUSG public immutable rousg;
81: IERC20 public immutable buidl;
84: IBUIDLRedeemer public immutable buidlRedeemer;
87: uint256 public immutable decimalsMultiplier;
90: address public immutable usdcReceiver;
93: IRWAOracle public oracle;
96: address public feeReceiver;
99: uint256 public mintFee = 0;
102: uint256 public redeemFee = 0;
106: uint256 public minimumDepositAmount = 100_000e6;
110: uint256 public minimumRedemptionAmount = 50_000e6;
113: bool public mintPaused;
116: bool public redeemPaused;
120: uint256 public minBUIDLRedeemAmount = 250_000e6;
123: IInvestorBasedRateLimiter public investorBasedRateLimiter;
```
[57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57) | [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60) | [63](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L63) | [66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66) | [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69) | [72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72) | [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L75) | [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L78) | [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L81) | [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L84) | [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L87) | [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90) | [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L93) | [96](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L96) | [99](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L99) | [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L102) | [106](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L106) | [110](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L110) | [113](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L113) | [116](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L116) | [120](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L120) | [123](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L123)

```solidity
File: contracts/ousg/rOUSG.sol

81: IRWAOracle public oracle;
84: IERC20 public ousg;
87: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
94: bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
95: bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```
[81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L81) | [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L84) | [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87) | [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94) | [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)

```solidity
File: contracts/ousg/rOUSGFactory.sol

38: bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
41: ROUSG public rOUSGImplementation;
42: ProxyAdmin public rOUSGProxyAdmin;
43: TokenProxy public rOUSGProxy;
45: bool public initialized = false;
```
[38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38) | [41](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L41) | [42](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L42) | [43](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L43) | [45](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45)
</details>

### [N-33] Non-uppercase/Constant-case Naming for `immutable` Variables

For better readability and adherence to common naming conventions, variable names declared as immutable should be written in all uppercase letters.

<details>
<summary><i>8 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

72: IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;
75: IRWALike public immutable ousg;
78: ROUSG public immutable rousg;
81: IERC20 public immutable buidl;
84: IBUIDLRedeemer public immutable buidlRedeemer;
87: uint256 public immutable decimalsMultiplier;
90: address public immutable usdcReceiver;
```
[72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72) | [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L75) | [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L78) | [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L81) | [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L84) | [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L87) | [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90)

```solidity
File: contracts/ousg/rOUSGFactory.sol

40: address internal immutable guardian;
```
[40](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40)
</details>

### [N-34] Function Names Not in mixedCase

Function names should use mixedCase for better readability and consistency with Solidity style guidelines. 
Examples of good practice include: getBalance, transfer, verifyOwner, addMember, changeOwner. 
[More information in Documentation](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#function-names)

<details>
<summary><i>13 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

254: function mintRebasingOUSG(
362: function redeemRebasingOUSG(
457: function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
479: function getOUSGPrice() public view returns (uint256 price) {
622: function setMinimumBUIDLRedemptionAmount(
```
[254](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254) | [362](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362) | [457](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L457) | [479](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479) | [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622)

```solidity
File: contracts/ousg/rOUSG.sol

111: function __rOUSG_init(
127: function __rOUSG_init_unchained(
363: function getSharesByROUSG(
373: function getROUSGByShares(uint256 _shares) public view returns (uint256) {
377: function getOUSGPrice() public view returns (uint256 price) {
649: function setKYCRegistry(
655: function setKYCRequirementGroup(
```
[111](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L111) | [127](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L127) | [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363) | [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373) | [377](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L377) | [649](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L649) | [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L655)

```solidity
File: contracts/ousg/rOUSGFactory.sol

70: function deployRebasingOUSG(
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70)
</details>

### [N-35] Insufficient Comments in Complex Functions

Complex functions spanning multiple lines should have more comments to better explain the purpose of each logic step.
Proper commenting can greatly improve the readability and maintainability of the codebase. Consider adding explicit comments
to provide insights into the function's operation.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit function with 33 lines has only 2 comment lines
277: function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {
/// @audit function with 50 lines has only 7 comment lines
387: function _redeem(
    uint256 ousgAmountIn
  ) internal returns (uint256 usdcAmountOut) {
```
[277](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L277) | [387](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L387)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit function with 31 lines has only 0 comment lines
70: function deployRebasingOUSG(
    address kycRegistry,
    uint256 requirementGroup,
    address ousg,
    address oracle
  ) external onlyGuardian returns (address, address, address) {
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70)
</details>

### [N-36] Common functions should be refactored to a common base contract

The codebase contains several functions with the same implementations across multiple files.
To enhance maintainability and reduce potential errors, consider refactoring these common functions into a shared base contract.
This practice promotes code reuse and easier future upgrades.

<details>
<summary><i>4 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

638: function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }
794: function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }
```
[638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638) | [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794)

```solidity
File: contracts/ousg/rOUSG.sol

613: function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }
```
[613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613)

```solidity
File: contracts/ousg/rOUSGFactory.sol

121: function multiexcall(
    ExCallData[] calldata exCallData
  ) external payable override onlyGuardian returns (bytes[] memory results) {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }
```
[121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121)
</details>

### [N-37] NatSpec: Error declarations should have descriptions

NatSpec comments are essential for understanding the purpose and functionality of error declarations. 
Adding descriptive comments improves readability and can aid in debugging.
It's a best practice to provide NatSpec comments for all error declarations in your Solidity contract.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

90: error UnwrapTooSmall();
```
[90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)
</details>

### [N-38] NatSpec: Non-public state variable declarations should use `@dev` tags

Non-public state variables in smart contracts often have specialized purposes that may not be immediately clear to developers who did not write the original code.
Adding comments to explain the role and functionality of these variables can greatly aid in code readability and maintainability.
This is especially beneficial for future code reviews and audits.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

78: uint256 private totalShares;
```
[78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L78)

```solidity
File: contracts/ousg/rOUSGFactory.sol

40: address internal immutable guardian;
```
[40](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40)
</details>

### [N-39] `constant`s should be defined rather than using magic numbers

Magic numbers are hardcoded numerical values used directly in the code, making it harder to read and maintain.
Consider using constants instead of magic numbers.

<details>
<summary><i>12 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit 100_000
106: uint256 public minimumDepositAmount = 100_000e6;
/// @audit 50_000
110: uint256 public minimumRedemptionAmount = 50_000e6;
/// @audit 250_000
120: uint256 public minBUIDLRedeemAmount = 250_000e6;
/// @audit 200
557: require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
/// @audit 200
570: require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
/// @audit 1e18
689: uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;
/// @audit 1e18
704: usdcOwed = _scaleDown(amountE36 / 1e18);
```
[106](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L106) | [110](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L110) | [120](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L120) | [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557) | [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570) | [689](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L689) | [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit 18
182: return 18;
/// @audit 1e18
190: (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
/// @audit 1e18
202: (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
/// @audit 1e18
367: (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
/// @audit 1e18
375: (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
```
[182](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L182) | [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L190) | [202](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L202) | [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L375)
</details>

### [N-40] Consider moving `msg.sender` checks to a common authorization `modifier`

Functions that are only allowed to be called by a specific actor should use a modifier to check if the caller is the specified actor (e.g., owner, specific role, etc.).
Using `require` to check `msg.sender` in the function body is less efficient and less clear.

Consider refactoring these `require` statements into a modifier for better readability, organization, and gas efficiency.

<details>
<summary><i>5 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

297: require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
344: require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
371: require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
```
[297](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L297) | [344](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L344) | [371](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L371)

```solidity
File: contracts/ousg/rOUSG.sol

593: if (from != msg.sender && to != msg.sender) {
594: require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");
```
[593](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L593) | [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594)
</details>

### [N-41] NatSpec: Contract declarations should have `@author` tag

In the world of decentralized code, giving credit is key. NatSpec's `@author` tag acknowledges the minds behind the code.
It appears this Solidity contract omits the `@author` directive in its NatSpec annotations.
Properly attributing code to its contributors not only recognizes effort but also aids in establishing trust and credibility.
[Dive Deeper into NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

55: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
```
[55](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55)
</details>

### [N-42] Consider defining system-wide constants in a single file

System-wide constants should be declared in a single file for better maintainability and readability.
This contract seems to contain constants which could potentially be system-wide and could be better managed if they were centralized in a single location.

<details>
<summary><i>10 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

57: bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
60: bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
63: uint256 public constant MINIMUM_OUSG_PRICE = 105e18;
66: uint256 public constant FEE_GRANULARITY = 10_000;
69: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
```
[57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57) | [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60) | [63](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L63) | [66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66) | [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69)

```solidity
File: contracts/ousg/rOUSG.sol

87: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
93: bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
94: bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
95: bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```
[87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87) | [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L93) | [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94) | [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)

```solidity
File: contracts/ousg/rOUSGFactory.sol

38: bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```
[38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38)
</details>

### [N-43] Add inline comments for unnamed variables

Having unnamed variables in function definitions can be confusing and decrease the code readability. 
Adding inline comments to explain the purpose of unnamed variables could make the code easier to understand and maintain.

For example, convert function declarations like `function foo(address x, address)` to `function foo(address x, address /* y */)` to indicate that the unnamed variable could have been named 'y'.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit - `uint256`
586: function _beforeTokenTransfer(
    address from,
    address to,
    uint256
  ) internal view {
```
[586](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L586)
</details>

### [N-44] Consider making contracts `Upgradeable`

Contract uses a non-upgradeable design.
Transitioning to an upgradeable contract structure is more aligned with contemporary smart contract practices.
This approach not only enhances flexibility but also allows for continuous improvement and adaptation, ensuring the contract stays relevant and robust in an ever-evolving ecosystem.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit - Contract `OUSGInstantManager` is not upgradeable
49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
{
```
[49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit - Contract `ROUSGFactory` is not upgradeable
37: contract ROUSGFactory is IMulticall {
```
[37](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37)
</details>

### [N-45] Style guide: Non-`external`/`public` variable names should begin with an underscore

The naming convention for non-public (private and internal) variables in Solidity recommends the use of a leading underscore.

Since `constants` can be public, to avoid confusion, they should also be prefixed with an underscore.

This practice clearly differentiates between public/external and non-public variables, enhancing code clarity and reducing the likelihood of misinterpretation or errors.
Following this convention improves code readability and maintainability.

<details>
<summary><i>4 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

72: mapping(address => uint256) private shares;
75: mapping(address => mapping(address => uint256)) private allowances;
78: uint256 private totalShares;
```
[72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72) | [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75) | [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L78)

```solidity
File: contracts/ousg/rOUSGFactory.sol

40: address internal immutable guardian;
```
[40](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40)
</details>

### [N-46] Style guide: Contract does not follow the Solidity style guide's suggested layout ordering

Adhering to a recommended order in Solidity contracts enhances code readability and maintenance.
[More information in Documentation](https://docs.soliditylang.org/en/latest/style-guide.html#order-of-layout)
It's recommended to use the following order:
1. Type declarations
2. State variables
3. Events
4. Errors
5. Modifiers
6. Functions

<details>
<summary><i>4 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `modifier` declared after `function`
756: modifier whenMintNotPaused() {
```
[756](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L756)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit `state variable` declared after `error`
93: bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
/// @audit `event` declared after `function`
149: event TransferShares(
    address indexed from,
    address indexed to,
    uint256 sharesValue
  );
```
[93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L93) | [149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L149)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit `event` declared after `function`
141: event rOUSGDeployed(
    address proxy,
    address proxyAdmin,
    address implementation,
    string name,
    string ticker
  );
```
[141](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141)
</details>

### [N-47] Consider bounding input array length

The functions in question operate on arrays without established boundaries, executing function calls for each of their entries.
If these arrays become excessively long, a function might revert due to gas constraints.
To enhance user experience, consider incorporating a `require()` statement that enforces a sensible maximum array length.
This approach can avoid unnecessary computational work and ensure smoother transactions.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `exCallData` is a function array parameter and `exCallData.length` is not bounded
804: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit `exCallData` is a function array parameter and `exCallData.length` is not bounded
125: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)
</details>

### [N-48] NatSpec: Function declarations should have `@notice` tag

In Solidity, the `@notice` tag in NatSpec comments is used to provide important explanations to end users about what a function does. 
It appears that this contract's function declarations are missing `@notice` tags in their NatSpec annotations.

The absence of `@notice` tags reduces the contract's transparency and could lead to misunderstandings about a function's purpose and behavior.
Note that the Solidity compiler treats comments beginning with `///` or `/**` as `@notice` tags if one wasn't explicitly provided.
[Learn More About NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

<details>
<summary><i>19 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

794: function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
```
[794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794)

```solidity
File: contracts/ousg/rOUSG.sol

98: constructor() {
102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
166: function name() public pure returns (string memory) {
174: function symbol() public pure returns (string memory) {
181: function decimals() public pure returns (uint8) {
188: function totalSupply() public view returns (uint256) {
199: function balanceOf(address _account) public view returns (uint256) {
231: function allowance(
    address _owner,
    address _spender
  ) public view returns (uint256) {
347: function getTotalShares() public view returns (uint256) {
356: function sharesOf(address _account) public view returns (uint256) {
363: function getSharesByROUSG(
    uint256 _rOUSGAmount
  ) public view returns (uint256) {
373: function getROUSGByShares(uint256 _shares) public view returns (uint256) {
378: function getOUSGPrice() public view returns (uint256 price) {
642: function pause() external onlyRole(PAUSER_ROLE) {
646: function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
650: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
656: function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE) {
```
[98](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L98) | [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102) | [166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L166) | [174](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L174) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L181) | [188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188) | [199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L199) | [231](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L231) | [347](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L347) | [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356) | [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363) | [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373) | [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378) | [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642) | [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650) | [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656)

```solidity
File: contracts/ousg/rOUSGFactory.sol

47: constructor(address _guardian) {
```
[47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)
</details>

### [N-49] Constants in comparisons should appear on the left side

Placing constants on the left side of comparison statements can help prevent accidental assignments and improve code readability.
In languages like C, placing constants on the left can protect against unintended assignments that would be treated as true conditions, leading to bugs.
Although Solidity does not have this specific issue, using the same practice can still be beneficial for code readability and consistency.

Consider placing constants on the left side of comparison operators like `==`, `!=`, `<`, `>`, `<=`, and `>=`."

<details>
<summary><i>8 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

310: require(
      ousgAmountOut > 0,
      "OUSGInstantManager::_mint: net mint amount can't be zero"
    );
316: if (usdcfees > 0) {
417: require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    );
450: if (usdcFees > 0) {
557: require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
570: require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
```
[310](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310) | [316](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L316) | [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L417) | [450](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L450) | [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557) | [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570)

```solidity
File: contracts/ousg/rOUSG.sol

416: require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");
432: require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
```
[416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416) | [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432)
</details>

### [N-50] NatSpec: Contract declarations should have `@notice` tag

The `@notice` tag in NatSpec annotations serves to provide information about the contract's functionality that is visible to end-users.
Including `@notice` comments helps to improve the contract's transparency and ease of understanding, contributing to the overall trust and credibility of the code.
[NatSpec Guidelines](https://docs.soliditylang.org/en/develop/natspec-format.html)

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

55: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
```
[55](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55)
</details>

### [N-51] Named Imports of Parent Contracts Are Missing

It's important to have named imports for parent contracts to ensure code readability and maintainability.
Missing named imports can make it difficult to understand the code hierarchy and can lead to issues in the future.

<details>
<summary><i>13 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit Missing named import for parent contract: `ReentrancyGuard`
49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
{
/// @audit Missing named import for parent contract: `InstantMintTimeBasedRateLimiter`
49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
{
/// @audit Missing named import for parent contract: `AccessControlEnumerable`
49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
{
/// @audit Missing named import for parent contract: `IOUSGInstantManager`
49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
{
/// @audit Missing named import for parent contract: `IMulticall`
49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
{
```
[49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49) | [49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49) | [49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49) | [49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49) | [49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit Missing named import for parent contract: `Initializable`
54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
/// @audit Missing named import for parent contract: `ContextUpgradeable`
54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
/// @audit Missing named import for parent contract: `PausableUpgradeable`
54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
/// @audit Missing named import for parent contract: `AccessControlEnumerableUpgradeable`
54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
/// @audit Missing named import for parent contract: `KYCRegistryClientUpgradeable`
54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
/// @audit Missing named import for parent contract: `IERC20Upgradeable`
54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
/// @audit Missing named import for parent contract: `IERC20MetadataUpgradeable`
54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
```
[54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54) | [54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54) | [54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54) | [54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54) | [54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54) | [54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54) | [54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit Missing named import for parent contract: `IMulticall`
37: contract ROUSGFactory is IMulticall {
```
[37](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37)
</details>

### [N-52] Long functions should be refactored into multiple, smaller, functions

Functions that span many lines can be hard to understand and maintain.
It is often beneficial to refactor long functions into multiple smaller functions.
This improves readability, makes testing easier, and can even lead to gas optimization if it eliminates the need for variables that would otherwise have to be stored in memory.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

 /// @audit 33 lines (excluding comments)
277: function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {
 /// @audit 50 lines (excluding comments)
387: function _redeem(
    uint256 ousgAmountIn
  ) internal returns (uint256 usdcAmountOut) {
```
[277](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L277) | [387](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L387)

```solidity
File: contracts/ousg/rOUSGFactory.sol

 /// @audit 31 lines (excluding comments)
70: function deployRebasingOUSG(
    address kycRegistry,
    uint256 requirementGroup,
    address ousg,
    address oracle
  ) external onlyGuardian returns (address, address, address) {
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70)
</details>

### [N-53] NatSpec: Contract declarations should have `@dev` tags

NatSpec comments are a critical part of Solidity's documentation system, designed to help developers and others understand the behavior and purpose of a contract.
The `@dev` tag, in particular, provides context and insight into the contract's development considerations.
A missing `@dev` comment can lead to misunderstandings about the contract, making it harder for others to contribute to or use the contract effectively.
Therefore, it's highly recommended to include `@dev` comments in the documentation to enhance code readability and maintainability.
[Refer to NatSpec Documentation](https://docs.soliditylang.org/en/develop/natspec-format.html)

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

55: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
```
[55](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55)

```solidity
File: contracts/ousg/rOUSGFactory.sol

37: contract ROUSGFactory is IMulticall {
```
[37](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37)
</details>

### [N-54] `public` functions not called by the contract should be declared `external` instead

Contracts are allowed to override their parents' functions and change the visibility from `external` to `public`.
If a `public` function is not called internally within the contract, it should be declared as `external` to save gas.

<details>
<summary><i>9 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

166: function name() public pure returns (string memory) {
174: function symbol() public pure returns (string memory) {
181: function decimals() public pure returns (uint8) {
188: function totalSupply() public view returns (uint256) {
231: function allowance(
    address _owner,
    address _spender
  ) public view returns (uint256) {
302: function increaseAllowance(
    address _spender,
    uint256 _addedValue
  ) public returns (bool) {
328: function decreaseAllowance(
    address _spender,
    uint256 _subtractedValue
  ) public returns (bool) {
347: function getTotalShares() public view returns (uint256) {
397: function transferShares(
    address _recipient,
    uint256 _sharesAmount
  ) public returns (uint256) {
```
[166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L166) | [174](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L174) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L181) | [188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188) | [231](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L231) | [302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302) | [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328) | [347](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L347) | [397](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397)
</details>

### [N-55] Large multiples of ten should use scientific notation

Large multiples of ten should use scientific notation (e.g., 1e4) instead of decimal literals (e.g., 10000)
for better code readability.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `10_000` should be written as `1e4`
66: uint256 public constant FEE_GRANULARITY = 10_000;
/// @audit `10_000` should be written as `1e4`
69: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
```
[66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66) | [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit `10_000` should be written as `1e4`
87: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
```
[87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87)
</details>

### [N-56] `approve` can revert if the current approval is not zero

Some tokens like USDT check for the current approval, and they revert if it's not zero.
While Tether is known to do this, it applies to other tokens as well, which are trying to protect against [this](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit#heading=h.m9fhqynw2xvt) attack vector.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

464: buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
```
[464](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L464)
</details>

### [N-57] Style guide: Function ordering does not follow the Solidity style guide

Ordering helps readers identify which functions they can call and to find the constructor and fallback definitions easier.
But there are contracts in the project that do not comply with this.
Functions should be grouped according to their visibility and ordered:
- constructor 
- receive function (if exists)
- fallback function (if exists)
- external
- public
- internal
- private.

<details>
<summary><i>14 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `internal` function `_mint()` declared before `external` function `redeem()`
277: function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {
335: function redeem(
    uint256 ousgAmountIn
  )
    external
    override
    nonReentrant
    whenRedeemNotPaused
    returns (uint256 usdcAmountOut)
  {
/// @audit `internal` function `_redeemBUIDL()` declared before `public` function `getOUSGPrice()`
457: function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
479: function getOUSGPrice() public view returns (uint256 price) {
/// @audit `public` function `getOUSGPrice()` declared before `external` function `setInstantMintLimit()`
479: function getOUSGPrice() public view returns (uint256 price) {
498: function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
/// @audit `internal` function `_scaleDown()` declared before `external` function `pauseMint()`
747: function _scaleDown(uint256 amount) internal view returns (uint256) {
768: function pauseMint() external onlyRole(PAUSER_ROLE) {
```
[277](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L277) | [335](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335) | [457](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L457) | [479](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479) | [479](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479) | [498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498) | [747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L747) | [768](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L768)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit `internal` function `__rOUSG_init_unchained()` declared before `public` function `name()`
127: function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
166: function name() public pure returns (string memory) {
/// @audit `public` function `transferShares()` declared before `external` function `wrap()`
397: function transferShares(
    address _recipient,
    uint256 _sharesAmount
  ) public returns (uint256) {
415: function wrap(uint256 _OUSGAmount) external whenNotPaused {
/// @audit `internal` function `_beforeTokenTransfer()` declared before `external` function `setOracle()`
586: function _beforeTokenTransfer(
    address from,
    address to,
    uint256
  ) internal view {
613: function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
```
[127](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L127) | [166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L166) | [397](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397) | [415](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415) | [586](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L586) | [613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613)
</details>

### [N-58] Style guide: Extraneous whitespace

See the [whitespace](https://docs.soliditylang.org/en/v0.8.24/style-guide.html#whitespace-in-expressions) section of the Solidity Style Guide

<details>
<summary><i>3 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `Immediately inside parenthesis, brackets or braces, with the exception of single line function declarations.`
480: (price, ) = oracle.getPriceData();
/// @audit `More than one space around an assignment or other operator to align with another`
206: OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
```
[480](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L480) | [202](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L202) | [206](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L206)
</details>

### [N-59] Contract/Libraries Names Do Not Match Their Filenames

According to the Solidity Style Guide, contract names should match their filenames. 
Mismatching contract names and filenames can lead to confusion and make the code harder to maintain and review.

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
{
```
[49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49)

```solidity
File: contracts/ousg/rOUSG.sol

54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
```
[54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54)

```solidity
File: contracts/ousg/rOUSGFactory.sol

37: contract ROUSGFactory is IMulticall {
```
[37](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37)
</details>

### [N-60] Unused import

The contract contains import statements for libraries or other contracts that are not utilized within the code.
Excessive or unused imports can clutter the codebase, leading to inefficiency and potential confusion.
Consider removing any imports that are not essential to the contract's functionality.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit - rOUSG imported but not used
21: import "contracts/ousg/rOUSG.sol";
```
[21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L21)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit - Proxy imported but not used
20: import "contracts/Proxy.sol";
/// @audit - rOUSG imported but not used
21: import "contracts/ousg/rOUSG.sol";
```
[20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L20) | [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L21)
</details>

### [N-61] Consider using named mappings

As of Solidity version 0.8.18, it is possible to use named mappings to clarify the purpose of each mapping in the code. 
It is recommended to use this feature for better code readability and maintainability.

More information: [Solidity 0.8.18 Release Announcement](https://blog.soliditylang.org/2023/02/01/solidity-0.8.18-release-announcement/)

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

72: mapping(address => uint256) private shares;
75: mapping(address => mapping(address => uint256)) private allowances;
```
[72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72) | [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75)
</details>

### [N-62] Use of `override` is unnecessary

In Solidity version 0.8.8 and later, the use of the `override` keyword becomes superfluous when a function is overriding solely from an interface and the function isn't present in multiple base contracts.
Previously, the `override` keyword was required as an explicit indication to the compiler. However, this is no longer the case, and the extraneous use of the keyword can make the code less clean and more verbose.

Solidity documentation on [Function Overriding](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding).

<details>
<summary><i>20 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

230: function mint(
    uint256 usdcAmountIn
  )
    external
    override
    nonReentrant
    whenMintNotPaused
    returns (uint256 ousgAmountOut)
  {
254: function mintRebasingOUSG(
    uint256 usdcAmountIn
  )
    external
    override
    nonReentrant
    whenMintNotPaused
    returns (uint256 rousgAmountOut)
  {
335: function redeem(
    uint256 ousgAmountIn
  )
    external
    override
    nonReentrant
    whenRedeemNotPaused
    returns (uint256 usdcAmountOut)
  {
362: function redeemRebasingOUSG(
    uint256 rousgAmountIn
  )
    external
    override
    nonReentrant
    whenRedeemNotPaused
    returns (uint256 usdcAmountOut)
  {
498: function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
512: function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
526: function setInstantMintLimitDuration(
    uint256 _instantMintLimitDuration
  ) external override onlyRole(CONFIGURER_ROLE) {
540: function setInstantRedemptionLimitDuration(
    uint256 _instantRedemptionLimitDuratioin
  ) external override onlyRole(CONFIGURER_ROLE) {
554: function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
567: function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {
581: function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
599: function setMinimumRedemptionAmount(
    uint256 _minimumRedemptionAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
622: function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
638: function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
650: function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
663: function setInvestorBasedRateLimiter(
    address _investorBasedRateLimiter
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
794: function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
```
[230](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L230) | [254](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254) | [335](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335) | [362](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362) | [498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512) | [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526) | [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567) | [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599) | [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622) | [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650) | [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663) | [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794)

```solidity
File: contracts/ousg/rOUSG.sol

649: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
655: function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE) {
```
[649](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L649) | [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L655)

```solidity
File: contracts/ousg/rOUSGFactory.sol

121: function multiexcall(
    ExCallData[] calldata exCallData
  ) external payable override onlyGuardian returns (bytes[] memory results) {
```
[121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121)
</details>

### [N-63] Setters should prevent re-setting of the same value

Setter functions should include a condition to check if the new value being assigned is different from the current value. This practice prevents redundant state changes and the emission of unnecessary events, ensuring that changes only occur when actual updates to the values are made.

This not only helps to maintain the integrity of the contract's state but also keeps the event logs cleaner and more meaningful by avoiding the recording of identical consecutive values. Such an approach can improve the clarity and efficiency of debugging and data tracking processes.

<details>
<summary><i>12 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit Missing `_instantMintLimit` check before state change
501: _setInstantMintLimit(_instantMintLimit);
/// @audit Missing `_instantRedemptionLimit` check before state change
515: _setInstantRedemptionLimit(_instantRedemptionLimit);
/// @audit Missing `_instantMintLimitDuration` check before state change
529: _setInstantMintLimitDuration(_instantMintLimitDuration);
/// @audit Missing `_instantRedemptionLimitDuratioin` check before state change
543: _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
/// @audit Missing `_mintFee` check before state change
559: mintFee = _mintFee;
/// @audit Missing `_redeemFee` check before state change
572: redeemFee = _redeemFee;
/// @audit Missing `_minimumDepositAmount` check before state change
590: minimumDepositAmount = _minimumDepositAmount;
/// @audit Missing `_minimumRedemptionAmount` check before state change
610: minimumRedemptionAmount = _minimumRedemptionAmount;
/// @audit Missing `_minimumBUIDLRedemptionAmount` check before state change
629: minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
/// @audit Missing `_feeReceiver` check before state change
655: feeReceiver = _feeReceiver;
```
[501](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L501) | [515](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L515) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L529) | [543](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L543) | [559](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L559) | [572](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L572) | [590](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L590) | [610](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L610) | [629](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L629) | [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L655)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit Missing `registry` check before state change
653: _setKYCRegistry(registry);
/// @audit Missing `group` check before state change
659: _setKYCRequirementGroup(group);
```
[653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L653) | [659](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L659)
</details>

### [N-64] Use Unchecked for Divisions on Constant or Immutable Values

Unsigned divisions on constant or immutable values do not result in overflow.
Therefore, these operations can be marked as unchecked, optimizing gas usage without compromising safety.

For instance, if `a` is an unsigned integer and `b` is a constant or immutable, a / b can be safely rewritten as: unchecked { a / b }

<details>
<summary><i>6 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

377: uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /
      OUSG_TO_ROUSG_SHARES_MULTIPLIER;
716: return (usdcAmount * mintFee) / FEE_GRANULARITY;
728: return (usdcAmount * redeemFee) / FEE_GRANULARITY;
748: return amount / decimalsMultiplier;
```
[377](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L377) | [716](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L716) | [728](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L728) | [748](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L748)

```solidity
File: contracts/ousg/rOUSG.sol

439: ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
636: ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
```
[439](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L439) | [636](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L636)
</details>

### [N-65] Contracts should have full test coverage

It's recommended to have full test coverage for all contracts.
While 100% code coverage does not guarantee absence of bugs, it can catch simple bugs and reduce regressions during code modifications.
Moreover, to achieve full coverage, authors often have to refactor their code into more modular components, each testable separately.
This leads to lower interdependencies, and results in code that is easier to understand and audit.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: app/2024-03-ondo-finance

1: All files
```
[1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/app/2024-03-ondo-finance#L1)
</details>

### [N-66] Large or complicated code bases should implement invariant tests

Large or complex code bases should include invariant fuzzing tests, such as those provided by Echidna.
These tests require the identification of invariants that should not be violated under any circumstances, with the fuzzer testing various inputs and function calls to ensure these invariants always hold.
This is especially important for code with a lot of inline-assembly, complicated math, or complex interactions between contracts. Despite having 100% code coverage, bugs can still occur due to the order of operations a user performs.
Extensive and well-written invariant tests can significantly reduce this testing gap.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: app/2024-03-ondo-finance

1: All files
```
[1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/app/2024-03-ondo-finance#L1)
</details>

### [N-67] Implement Formal Verification Proofs to Improve Security

Formal verification offers a mathematical proof confirming that your code operates as intended and is devoid of edge cases 
that may lead to unintended behavior. By leveraging this rigorous audit technique, you not only enhance the robustness 
of your code but also strengthen the trust of stakeholders in the safety of your contract.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: app/2024-03-ondo-finance

1: All files
```
[1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/app/2024-03-ondo-finance#L1)
</details>

