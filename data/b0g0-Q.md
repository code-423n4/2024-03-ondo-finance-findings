## [L-01] Approval is disabled during pause
In case the ROUSG contract gets paused because of some risky conditions, the users will not be able to withdrawal all their approvals and prevent possible damage once the contract gets unpaused

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L476

```solidity
 function _approve(
    address _owner,
    address _spender,
    uint256 _amount
  ) internal whenNotPaused {
....
}
```

Consider removing the `whenNotPaused` modifier from `_approve()`.

## [L-04] Missing zero address checks at a couple of functions

- `ROUSG.__rOUSG_init_unchained()` - no check for `_ousg, _oracle, guardian` addresses
- `ROUSGFactory.constructor()` - no check for the `guardian` address

## [N-01] Missing calls to base initializers in ROUSG

`ROUSG` does not call the following initializers of parent contracts:
- `__AccessControl_init`
-  `__Pausable_init()`

## [N-02] Increase/DecreaseAllowance methods can be removed 

The 2 methods have recently been removed from the OZ ERC20 standard due to reported risk of phishing attack. You can consider removing them.

Here is the discussion:
https://github.com/OpenZeppelin/openzeppelin-contracts/issues/4583

## [N-03] Consider adding a conditional event emitting flag to `ROUSG._approve()`

To save gas OZ implements an `emitEvent` flag  to `_approve()` like so:

```
function _approve(address owner, address spender, uint256 value, bool emitEvent) internal virtual {
```

And this is the explanation behind it:

https://github.com/OpenZeppelin/openzeppelin-contracts/blob/cb2aaaa04a292887c49839cd958b08a83979d746/contracts/token/ERC20/ERC20.sol#L265-L270

```
By default (when calling {_approve}) the flag is set to true. On the other hand, approval changes made by
     * `_spendAllowance` during the `transferFrom` operation set the flag to false. This saves gas by not emitting any
     * `Approval` event during `transferFrom` operations.
     *
     * Anyone who wishes to continue emitting `Approval` events on the`transferFrom` operation can force the flag to
     * true using the following override:
```

## [N-03] Unused constant variable inside `ROUSGFactory`

The `DEFAULT_ADMIN_ROLE` is defined inside `ROUSGFactory.sol`, but it is never used. It should be removed to reduce contract size and provide better readability