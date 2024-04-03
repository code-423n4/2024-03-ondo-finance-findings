### [G-1] Use custom errors and if statement instead of require()

**Description:** In a function, it's parameter are usually checked initially and to save gas we are using require() here. This consume more gas as it uses a string to explain. For instance in,
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533

**Impact:** Using this practice multiple time has increased gas consumption, which can be saved.


**Recommended Mitigation:** We can create custom errors and use if-statement to verify the parameter.
```
+ error AddressCannotBeZero();
- require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");
+ if(_recipient == address(0)) rever AddressCannoteZero();
```