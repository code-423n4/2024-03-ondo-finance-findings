# [01] rOUSG.sol :: allowances do not follow the ERC20 standard
The rOSUG token uses the mapping for allowances under the name **`allowances`**, diverging from the convention of **`_allowances`** as per the ERC20 standard. While the protocol mandates ERC20 compatibility, it's crucial to ensure adherence to ERC20 standards for seamless integration with existing ecosystems.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L75
```Solidity
mapping(address => mapping(address => uint256)) private allowances;
```
POC: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/cb2aaaa04a292887c49839cd958b08a83979d746/contracts/token/ERC20/ERC20.sol#L32

Change the mapping name to **`_allowances`**.

# [02] rOSUG.sol :: getOUSGPrice() does not check the MINIMUM_OUSG_PRICE
**`getOUSGPrice()`** in **`rOSUG.sol`** doesn't verify the **`MINIMUM_OUSG_PRICE`** whereas in **`ousgInstantManager.sol`**, the same function does perform this check against the **`MINIMUM_OUSG_PRICE`**.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L378-L380
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L479-L485

- rOUSG.sol
```Solidity
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
  }
```
- ousgInstantManager.sol 
```Solidity
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```
Validate the **`MINIMUM_OUSG_PRICE`** within the **`getOUSGPrice()`** function in **`rOUSG.sol`**.