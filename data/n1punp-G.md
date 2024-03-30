## Use `unchecked` subtraction for instances where underflow are already checked

Instances (3):

```diff
function _transferShares(
    address _sender,
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused {
    require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");
    require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");

    _beforeTokenTransfer(_sender, _recipient, _sharesAmount);

    uint256 currentSenderShares = shares[_sender];
    require(
      _sharesAmount <= currentSenderShares,
      "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
    );

+   unchecked {
        shares[_sender] = currentSenderShares - _sharesAmount;
+   }
    shares[_recipient] = shares[_recipient] + _sharesAmount;
  }
```

```diff
function _burnShares(
    address _account,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
    require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS");

    _beforeTokenTransfer(_account, address(0), _sharesAmount);

    uint256 accountShares = shares[_account];
    require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE");

+   unchecked {
        totalShares -= _sharesAmount;

        shares[_account] = accountShares - _sharesAmount;
+   }

    return totalShares;
  }
```

```diff
function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
    uint256 currentAllowance = allowances[_sender][msg.sender];
    require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");

    _transfer(_sender, _recipient, _amount);
+   unchecked {
        _approve(_sender, msg.sender, currentAllowance - _amount);
+   }
    return true;
  }
```
