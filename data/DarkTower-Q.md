**[L-1] PausableUpgradeable is not initialized in `rOUSG`**
-

In the `rOUSG.sol` contract, pausing functionality is not initialized by calling `__Pausable_init()` inside the `initialize` function. Thus, the contract cannot be `paused`.
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L58
```solidity
contract ROUSG is
  ...
@>  PausableUpgradeable,
  ...
{
```

As can be seen, the `initialize` function lacks initialization of the pausing mechanism:
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L110
```solidity
function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
    __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle); // @doesn't init pausable
  }
```

Pausing mechanism should be setup like so:
```diff
function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
    __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
+   __Pausable_init();
  }
```

**[L-2] Transfer event topics of the `burn()` function is in the wrong order**
-

In the `rOUSG.sol` contract, the `burn()` function emits the `Transfer` event topics in the wrong order.
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L638
```solidity
function burn(
    address _account,
    uint256 _amount
  ) external onlyRole(BURNER_ROLE) {
    ...

    _burnShares(_account, ousgSharesAmount);

    ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
@>  emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount)); // @audit-low wrong order of topics
    emit TransferShares(_account, address(0), ousgSharesAmount);
  }
```

As can be seen in the EIP20, the `Transfer` event should follow the below order:
https://eips.ethereum.org/EIPS/eip-20
```solidity
event Transfer(address indexed _from, address indexed _to, uint256 _value)
```

A note from the EIP 20 specification:
> A token contract which creates new tokens SHOULD trigger a Transfer event with the _from address set to 0x0 when tokens are created.

But as we can see above in the `Transfer` event implementation of the `burn()` function, the topics are in the wrong order as we are not creating or minting new tokens to be setting the `from` address as the `0x0` address. Instead, the `from` address should be the address the `rOUSG` is being burnt from and the `to` address should be the `0x0` address.

Hence, the order of topics should be as follows:
```diff
function burn(
    address _account,
    uint256 _amount
  ) external onlyRole(BURNER_ROLE) {
    ...

    _burnShares(_account, ousgSharesAmount);

    ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
+    emit Transfer(_account, address(0), getROUSGByShares(ousgSharesAmount));
-    emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
    emit TransferShares(_account, address(0), ousgSharesAmount);
  }
```

**[N-1] Employ a more uniform naming convention for `BURNER_ROLE`**
-

In the `rOUSG.sol` contract, roles are not uniformly named and hashed into their `bytes32` equivalent.
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94
```solidity
 bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE"); <--
```

A better naming to follow similarly how the `PAUSER_ROLE` was setup should be:
```diff
  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
- bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
+ bytes32 public constant BURNER_ROLE = keccak256("BURNER_ROLE");
```

**[N-2] `_mintShares` can do without the `whenNotPaused` modifier as the `wrap()`  function already enforces it**
-

In the `rOUSG.sol` contract, minting of shares are possible when the contract is not paused. When two functions (public/external & private/internal) reference the same `whenNotPaused` modifier, the inner function can do without the modifier in the case that such inner function won't be reached any other way other than the outer function.
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415
```solidity
function wrap(uint256 _OUSGAmount) external whenNotPaused { // note: pause mechanism protection
    ...
@>  _mintShares(msg.sender, ousgSharesAmount);
    ...
  }
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L532
```solidity
 function _mintShares(
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) { <-----@
    ...
  }
```

Get rid the inner `whenNotPaused` modifier in the `_mintShares` function:
```diff
  function _mintShares(
    address _recipient,
    uint256 _sharesAmount
+  ) internal returns (uint256) {
-  ) internal whenNotPaused returns (uint256) {
   ...
  }
```