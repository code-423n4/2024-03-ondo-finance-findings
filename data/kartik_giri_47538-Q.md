### Missing calls to base initializers in `rOUSG` contract

**Description:** 
The `rOUSG` contract is using OpenZeppelin's upgradeable contracts, such as ContextUpgradeable, PausableUpgradeable, and AccessControlEnumerableUpgradeable, but it not calling the init functions for these contracts in its own initializer `__rOUSG_init` function.

**Proof of Concept:**
The `PausableUpgradeable` contract have `__Pausable_init()` function which is used to Initializes the contract in unpaused state. but the `rOUSG::__rOUSG_init` is not calling it.

```
  /**
   * @dev Initializes the contract in unpaused state.
   */
  function __Pausable_init() internal onlyInitializing {
    __Pausable_init_unchained();
  }

  function __Pausable_init_unchained() internal onlyInitializing {
    _paused = false;
  }
```

**Recommended Mitigation:** 
Ensure that the initializer `__rOUSG_init` function of the contract `rOUSG` calls the init functions of all inherited upgradeable contracts.