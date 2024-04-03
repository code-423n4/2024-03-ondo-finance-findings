# [G-01] Gas Efficiency Improvement for ROUSG Token Contract

## Description

Most probably the users will have MAX approval for transferring tokens, so the `rOUSG::transferFrom()` can be optimized like it is done in `Lido`, i.e. add a check whether the user has MAX approval then call the new function which will do the approval. Here is the commit of Lido's change done recently to optimize the function:

https://github.com/lidofinance/lido-dao/commit/e9509d77f010fec76899e25ccde785c8de47bd42

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L276-L287

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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol

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

# [G-03] Redundant requires

## Descritpion

In the `ousgInstantManager.sol` there are two redundant requires which are wasting gas:

1. One of these requirement is redundant:

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L391-L398

```solidity
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_redeem: USDC decimals must be 6"
    );
    require(
      IERC20Metadata(address(buidl)).decimals() == 6,
      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    );
```

As there is a check in the constructor that:

```solidity
    require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    );
```

So if one of them has 6 decimals, consequently another one has 6 as well.

2. This check is redundant as the values of the `OUSG_TO_ROUSG_SHARES_MULTIPLIER` are constant and the same 10_000, moreover there is no need to have a separate `OUSG_TO_ROUSG_SHARES_MULTIPLIER` in this contract, as they designed to have the same value and `OUSGInstantManager` contract imports `rOUSG` where that parameter already set:

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L205-L209

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L21

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L87

```solidity

import "contracts/ousg/rOUSG.sol";

uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;

    require(
      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
    );
```

