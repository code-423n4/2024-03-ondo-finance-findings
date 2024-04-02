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