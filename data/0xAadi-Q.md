# [L-01] Missing Import of `IRWAOracle.sol` in `OUSGInstantManager` Contract

## Summary
The `OUSGInstantManager` contract references the `IRWAOracle` interface but does not import the corresponding `IRWAOracle.sol` file, which may lead to compilation errors and hinder contract deployment.

## Impact
Without the import statement, the contract may fail to compile, preventing deployment.

## Proof of Concept
The `OUSGInstantManager` contract uses `IRWAOracle` on [line 93](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L93), but `IRWAOracle.sol` is not imported anywhere in the contract.

- Reference to `IRWAOracle` in `OUSGInstantManager`: [GitHub link to line](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L93)
- Absence of import statement for `IRWAOracle.sol`: [GitHub link to file](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/interfaces/IRWAOracle.sol)

## Tools Used
Manual code review.

## Recommended Mitigation Steps
Import `IRWAOracle.sol` at the beginning of the `OUSGInstantManager.sol` file by adding the following line:

```solidity
    import "contracts/rwaOracles/IRWAOracle.sol";
```

# [L-02] Unnecessary `.decimals() == 6` Checks in Mint and Redeem Functions

## Summary
The `OUSGInstantManager` contract includes checks for `.decimals() == 6` within the `_mint` and `_redeem` functions. These checks are redundant as the decimal validation should be performed in the constructor to ensure that the correct token contracts are set.

## Impact
If the checks fail at runtime during `mint` or `redeem` operations, it indicates a critical deployment error that cannot be rectified without redeploying the contract. This could lead to a complete halt of contract functionality.

## Proof of Concept
- Redundant checks found in `_mint` function: [GitHub link to line](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L282C5-L285C7)

```solidity
    require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_mint: USDC decimals must be 6"
    );
```
- Redundant checks found in `_redeem` function: [GitHub link to line](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L391C4-L398C7)

```solidity
    require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_redeem: USDC decimals must be 6"
    );
    require(
      IERC20Metadata(address(buidl)).decimals() == 6,
      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    );
```

## Tools Used
Manual code review.

## Recommended Mitigation Steps
Remove the `.decimals() == 6` checks from the `_mint` and `_redeem` functions. Instead, ensure that the decimals are validated once in the constructor. This approach prevents the need for repeated checks and guarantees that the contract is initialized with the correct token addresses and decimal settings.

```solidity
constructor(...) {
  // ...
  require(
    IERC20Metadata(_usdc).decimals() == 6,
    "OUSGInstantManager: USDC must have 6 decimals"
  );
  require(
    IERC20Metadata(_buidl).decimals() == 6,
    "OUSGInstantManager: BUIDL must have 6 decimals"
  );
```

