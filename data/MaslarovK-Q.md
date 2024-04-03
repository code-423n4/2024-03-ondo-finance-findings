### Low Risk

| Count | Title |
| --- | --- |
| [L-01] | ROUSG::transferFrom() not following CEI pattern |
| [L-02] | OUSGInstantManager::getOUSGPrice contains off-by-one issue |

| Total Low Risk Issues | 2 |
| --- | --- |

## Low Risks

## [L-01] `ROUSG::transferFrom()` not following CEI pattern

**Issue Description:**

The function transfers tokens from one address to another before updating the  allowances array.

[rOUSG.sol#L276-L287](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L276-L287)

```solidity
function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
    uint256 currentAllowance = allowances[_sender][msg.sender];
    require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");

    _transfer(_sender, _recipient, _amount);
    _approve(_sender, msg.sender, currentAllowance - _amount);
    return true;
  }
```

**Recommendation:**

Consider putting the `_approve` first:
```
```solidity
function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
    uint256 currentAllowance = allowances[_sender][msg.sender];
    require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");

    _approve(_sender, msg.sender, currentAllowance - _amount);
    _transfer(_sender, _recipient, _amount);

    return true;
  }
```

## [L-02] `OUSGInstantManager::getOUSGPrice` contains off-by-one issue

**Issue Description:**

In the `getOUSGPrice` function there is a require statement which reverts if the price is not more than `MINIMUM_OUSG_PRICE`, but it should be inclusive of the `MINIMUM_OUSG_PRICE` as value.

```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

**Recommendation:**

Change the require statement as follows:

```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price >= MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```
so that the `MINIMUM_OUSG_PRICE` would be inclusive as it should be, given that this is the minimum price and not below minimum price value.

