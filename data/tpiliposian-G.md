# [G-01] Gas Efficiency Improvement for ROUSG Token Contract

## Description

Most probably the users will have MAX approval for transferring tokens, so the `rOUSG::transferFrom()` can be optimized like it is done in `Lido`, i.e. add a check whether the user has MAX approval then call the new function which will do the approval. Here is the commit of Lido's change done recently to optimize the function:

https://github.com/lidofinance/lido-dao/commit/e9509d77f010fec76899e25ccde785c8de47bd42

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

# [G-02] Public functions can be marked as external

## Description

All `public` functions in the `rOUSG.sol` contract, which are not called inside the contract, can be marked as `external` in order to save gas:

```solidity
function allowance(address _owner, address _spender) public view returns (uint256) {}
function getTotalShares() public view returns (uint256) {}
function sharesOf(address _account) public view returns (uint256) {}
function getSharesByROUSG(uint256 _rOUSGAmount) public view returns (uint256) {}
function getROUSGByShares(uint256 _shares) public view returns (uint256) {}
function getOUSGPrice() public view returns (uint256 price) {}
function _sharesOf(address _account) internal view returns (uint256) {}
function _approve(address _owner, address _spender, uint256 _amount) internal whenNotPaused {}
```

