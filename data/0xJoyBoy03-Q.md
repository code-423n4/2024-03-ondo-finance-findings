### [L-1] The burning process will decrease the `rOUSG::totalSupply` Contrary to what was said in natspec 

**Description** the `rOUSG::_burnShares` function which is implemented in `unwrap` and `burn` functions will decrease the `rOUSG::totalSupply` contrary to what was said in the natspec. The natspec says that the total supply will not decrease.
```java
  /**
   * @notice Destroys `_sharesAmount` shares from `_account`'s holdings, decreasing the total amount of shares.
@> * @dev This doesn't decrease the token total supply.   <--- this is a lie because it does decrease the total supply
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
```


**Proof of Concept:**
add this test in `rOUSG.t.sol` :
```java 
    function test_TotalSupplyDecreaseAfterBurning() public dealAliceROUSG(1e18) {
    uint256 initialTotalSupply = rOUSGToken.totalSupply();
    vm.prank(alice);
    rOUSGToken.unwrap(1e18);
    assertEq(rOUSGToken.totalSupply(), initialTotalSupply - 1e18);
  }
```

*Logs*:
```js
[PASS] test_TotalSupplyDecreaseAfterBurning() (gas: 231776)
Logs:
  ROUSG deployed 0x7ff9C67c93D9f7318219faacB5c619a773AFeF6A
  OUSG Instant Manager deployed 0xa0Cb889707d426A7A386870A03bc70d1b0697598

Suite result: ok. 1 passed; 0 failed; 0 skipped; finished in 12.48ms (2.26ms CPU time)
```

**Recommend Mitigation** mention this in Known issues or remove the line in natspec
```diff
  /**
   * @notice Destroys `_sharesAmount` shares from `_account`'s holdings, decreasing the total amount of shares.
-  * @dev This doesn't decrease the token total supply.   <--- this is a lie because it does decrease the total supply
   *
   * Requirements:
   *
   * - `_account` cannot be the zero address.
   * - `_account` must hold at least `_sharesAmount` shares.
   * - the contract must not be paused.
   */
```




### [L-2] there is a simple scenario where you can keep emitting Approval event without actually approving any tokens

**Description** the `approve` function will emit the `Approval` event even if the `_value` is 0. This is not a security issue but it is a bug because the event should not be emitted if the `_value` is 0. 

```java
  function approve(address _spender, uint256 _value) external whenNotPaused returns (bool) {
    require(_spender != address(0), "ROUSG: approve to the zero address");
    _allowances[msg.sender][_spender] = _value;
@>    emit Approval(msg.sender, _spender, _value);
    return true;
  }
```

**Impact** this is not a security issue but it is a bug because the event should not be emitted if the `_value` is 0 and it just breaks the logic of the function and wastes gas.

**Proof of Concept:** add this test to the `rOUSG.t.sol`:
```java
  function test_ApproveZeroValue() public dealAliceROUSG(1e18) {
    uint256 initialAllowance = rOUSGToken.allowance(alice, bob);
    rOUSGToken.approve(bob, 0);
    assertEq(rOUSGToken.allowance(alice, bob), 0);
    assertEq(rOUSGToken.allowance(alice, bob), initialAllowance);
  }
```

logs:
```java
Ran 1 test for forge-tests/ousg/rOUSG.t.sol:Test_rOUSG_ETH
[PASS] test_ApproveZeroValue() (gas: 196180)
Logs:
  ROUSG deployed 0x7ff9C67c93D9f7318219faacB5c619a773AFeF6A
  OUSG Instant Manager deployed 0xa0Cb889707d426A7A386870A03bc70d1b0697598

Suite result: ok. 1 passed; 0 failed; 0 skipped; finished in 24.89ms (1.44ms CPU time)
```

**Recommend Mitigation** ensure that the value is not 0 before emitting the event
```diff
  function _approve(
    address _owner,
    address _spender,
    uint256 _amount
  ) internal whenNotPaused {
    require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");
    require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");
    _allowances[msg.sender][_spender] = _value;
+    if (_value != 0) {
      emit Approval(msg.sender, _spender, _value);
}
  }
```