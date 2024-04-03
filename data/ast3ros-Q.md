# [NC-1] Wrong error message

When validating the ousg and rousg decimals, the error messages wrongly states that it is checking OUSG and USDC.

```solidity
    require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    );
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/11e77a3f64e7b055d12ccc914fa54051391ba24d/contracts/ousg/ousgInstantManager.sol#L186-L189

# [NC-2] Unused constant is declared

        bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);

https://github.com/code-423n4/2024-03-ondo-finance/blob/4791cd1946f834f27addbc162c1817e897de7bf9/contracts/ousg/rOUSGFactory.sol#L38

The constant DEFAULT_ADMIN_ROLE isn't used in the rOUSGFactory contract and can be removed.