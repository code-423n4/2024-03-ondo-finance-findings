---
## [L-01] Address Zero Check Missing in State variable updates

---

**Github code**
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L663-L673

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L638-L643


 Missing checks for address(0x0) when updating address state variables
State variables that are of type address should always be checked to ensure that they are not being assigned the null address (address(0x0)). A null address often implies an error or omission in the code. Without proper checks, such a scenario can lead to unexpected behavior and potential vulnerabilities in the smart contract. Therefore, it is considered good practice to implement checks for address(0x0) prior to assigning new values to address state variables.
The `setInvestorBasedRateLimiter` and `setOracle` functions allow the modification of the investor-based rate limiter and the oracle address, respectively. The impact of the finding is that there is no check to ensure that the newly passed addresses are not address zero (`0x0000000000000000000000000000000000000000`). These functions are crucial to the contract as the contract relies on them for input for sensitive data compilation. Although these functions are only called by the admin, efforts should be made to ensure that only valid addresses are passed.

## Proof of Concept
The following is the code snippet of the `setInvestorBasedRateLimiter` and `setOracle` functions:

```solidity
/**
 * @notice Admin function to set the investor-based rate limiter
 *
 * @param _investorBasedRateLimiter The address of the investor-based rate limiter
 */
function setInvestorBasedRateLimiter(
  address _investorBasedRateLimiter
) external override onlyRole(DEFAULT_ADMIN_ROLE) {
  emit InvestorBasedRateLimiterSet(
    address(investorBasedRateLimiter),
    _investorBasedRateLimiter
  );
 >> @audit  investorBasedRateLimiter = IInvestorBasedRateLimiter(
    _investorBasedRateLimiter
  );
}

/**
 * @notice Admin function to set the oracle address
 *
 * @param _oracle The address of the oracle that provides the OUSG price
 *                in USDC
 */
function setOracle(
  address _oracle
) external override onlyRole(DEFAULT_ADMIN_ROLE) {
  emit OracleSet(address(oracle), _oracle);
  >> @audit oracle = IRWAOracle(_oracle);
}
```


## Tools Used

- Manual Code Analysis

## Recommended Mitigation Steps
To address the identified issues in the `setInvestorBasedRateLimiter` and `setOracle` functions, consider the following steps:

**Add Address Zero Check:** Add checks to ensure that the newly passed addresses are not address zero.
   ```solidity
   require(_investorBasedRateLimiter != address(0), "OUSGInstantManager::setInvestorBasedRateLimiter: Invalid address");

.........................


   require(_oracle != address(0), "OUSGInstantManager::setOracle: Invalid address");
   ```







---

## [L-02]  Incorrect Error Message in Decimal Comparison

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
