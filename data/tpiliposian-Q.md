# 1. Combine double event emitting into a single function

## Description

In the `rOUSG.sol` contract combine all `Transfer` and `TransferShares` event emitting into one function like in `Lido`:
https://github.com/lidofinance/lido-dao/blob/5fcedc6e9a9f3ec154e69cff47c2b9e25503a78a/contracts/0.4.24/StETH.sol#L520-L523

Instead of every time emitting them one by one. These emissions into a single function will make the code more readable and reduce redundancy.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L397

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L420-L421

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L441-L442

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L457-L458

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L638-L639

# 2. Typo in the default roles

## Description

In the `rOUSG.sol` contract, there is a typo in the definition of one of the role identifiers. Specifically, the constant `BURN_ROLE` is defined using the identifier `keccak256("BURN_ROLE")`, but it seems to be intended as `BURNER_ROLE` based on its usage throughout the contract. This inconsistency in the role identifier could lead to confusion and potential issues during contract interaction and access control.

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L94

Code Snippet:
```solidity
  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
  bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```

Correct the typo in the `BURN_ROLE` definition to match the intended role identifier, `BURNER_ROLE`.

# 3. Wrong parameter name

## Description

In the `rOUSG::unwrap(uint256 _rOUSGAmount)` the parameter name is wrong, if the user places here the `_rOUSGAmount` the function will revert, as the function is designed to take `_OUSGAmount` and do calculations. Suppose Alice wrapped 100 OUSG tokens, and now she has 100 * 10_000 = 1_000_000 shares. Now if she calls the `unwrap()` with 1mln it will not work, as the function itself needs to multiply the number by `OUSG_TO_ROUSG_SHARES_MULTIPLIER` in the `getSharesByROUSG()` function:

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L363-L368

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L431-L443

```solidity
  function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
    require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
    uint256 ousgSharesAmount = getSharesByROUSG(_rOUSGAmount);
    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
      revert UnwrapTooSmall();
    _burnShares(msg.sender, ousgSharesAmount);
    ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
    emit Transfer(msg.sender, address(0), _rOUSGAmount);
    emit TransferShares(msg.sender, address(0), ousgSharesAmount);
  }

  function getSharesByROUSG(
    uint256 _rOUSGAmount
  ) public view returns (uint256) {
    return
      (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
  }
```

# 4. Wrong comment

## Description

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L188

In the `ousgInstantManager.sol`'s constructor there is comment which states:
"OUSG decimals must be equal to USDC decimals" however the check is for OUSG and rOUSG:

```solidity
    require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    );
```

