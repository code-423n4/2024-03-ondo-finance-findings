# QA

## Low Issues

## 1.  [`ROUSG.sol` Missing `OpenZeppelinUpgradeable` contract initialization](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L98-L142)

Current initialization only make single call `__rOUSG_init`. And does not call other `OpenZeppelinUpgradeable` contract init function.

```solidity
    constructor() {
    _disableInitializers();
  }

  function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
    __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
  }//@audit M missing init of other openzeppelin upgradable contracts
```

All `OpenZeppelinUpgrade` have their own init function for proxy contract to call. Which are:

- `ContextUpgradeable.__Context_init()`
- `PausableUpgradeable.__Pausable_init()`
- `AccessControlEnumerableUpgradeable.__AccessControlEnumerable_init()`

Except `PausableUpgrade` set `pausable` value from `false` to `false`.

```solidity
  function __Pausable_init_unchained() internal onlyInitializing {
    _paused = false;
  }
```

Other upgradeable contract only have empty init function. So there is no reason to call them for now.
Its still a good practice to call them in case they have some init logic in the future.

```solidity
  function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
    __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
++    __Context_init();
++    __Pausable_init();
++    __AccessControlEnumerable_init();
  }
```

## 2. `rOUSG.sol` allow ERC20 zero amount transfer and self transfer. Spamming event log

`rOUSG.sol` contract will be deployed on L2 network where gas price is cheap.
This allow spammer to make call transfer call really cheap.

While transfer 0 token make not sense between KYC user.
It still create event log and sending notifications to users. Usually email notification.
This can be little bit annoying for some users.

Include `amount != 0` and `from!=to` check inside `ERC20.Transfer()` like in Openzeppelin  will just save people time and energy.
