[L-01] Missing checks for address(0x0) when updating address state variables
State variables that are of type address should always be checked to ensure that they are not being assigned the null address (address(0x0)). A null address often implies an error or omission in the code. Without proper checks, such a scenario can lead to unexpected behavior and potential vulnerabilities in the smart contract. Therefore, it is considered good practice to implement checks for address(0x0) prior to assigning new values to address state variables.


---
[L-02]  Incorrect Error Message in Decimal Comparison

---

### Impact
The current implementation of the require statement for decimal comparison in the `OUSGInstantManager` contract produces an inaccurate error message. The error message incorrectly states that "OUSG decimals must be equal to USDC decimals," while the actual comparison is between `OUSG` and `ROUSG` decimals. This misleading error message can cause confusion during debugging and auditing processes.

### Proof of Concept

```solidity
require(
    IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
    "OUSGInstantManager: OUSG decimals must be equal to USDC decimals" //@note audit USDC should be OUSG
);
```

### Tools Used
Manual code analysis

### Recommended Mitigation Steps

To address this issue and provide a clear and accurate error message, the require statement should be updated to compare `OUSG` and `ROUSG` decimals directly.

**Mitigation**:

Update the require statement as follows:

```solidity
require(
    IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
    "OUSGInstantManager: OUSG decimals must be equal to ROUSG decimals"
);
```



---
