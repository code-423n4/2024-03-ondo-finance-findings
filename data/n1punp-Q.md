## 1. Limit function visibility from `public` to `external` for functions that are not intended for internal usages.

Instances (1): 

```solidity
// In rOUSG.sol
function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer {
    __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
  }
```

This function is never called internally, so it is recommended to limit this to *external* visibility. 

## 2. Use SafeERC20's `safeTransfer` for `retrieveTokens` in `ousgInstantManager.sol` to handle USDT token rescue.

```diff
+ import "contracts/external/openzeppelin/contracts/token/SafeERC20.sol";

function retrieveTokens(
    address token,
    address to,
    uint256 amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
-    IERC20(token).transfer(to, amount);
+    IERC20(token).safeTransfer(to, amount);
  }
```



