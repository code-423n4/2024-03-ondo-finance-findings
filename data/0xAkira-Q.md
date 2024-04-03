# [NC-1] No check for address(0)

## Vulnerability Details

In the [`rOUSG.sol::setOracle()`]([https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613-L616]) contract, the function has no check for `address(0)` 
```solidity
function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }
```

## Recommendations

Consider adding a require check on `address(0)`
```diff
function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
+   require(_oracle != address(0));
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }
```
---

# [Low-1] Strict requirement 

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479-L485

## Vulnerability Details
```solidity 
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

The contract has a Safety Circuit Breaker in the event of an Oracle failure `MINIMUM_OUSG_PRICE = 105e18;` 

The [function](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479-L485) has a check that the price will be greater than the minimum price. This is a very strict requirement 

## Recommendations
It is necessary to consider not such a strict requirement
```diff
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
+       price >= MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

