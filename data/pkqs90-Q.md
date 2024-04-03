# QA Report

## [L-01] `rOUSG.sol#getOUSGPrice()` does not have sanity check when fetching from oracle

### Bug Description

In `rOUSG.sol#getOUSGPrice()`, when fetching the price from the oracle, it does not perform any sanity checks, such as checking the updated timestamp, or whether the price is too low/high. In comparison, the same function in `ousgInstantManager.sol` contract does have a check that requires the price to be larger than 105e18 (`MINIMUM_OUSG_PRICE`).

rOUSG.sol:
```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
  }
```

ousgInstantManager.sol:
```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

The impact are mainly 2 parts, if the OUSGPrice is lower than an expected price:

1. In `_transfer()` function, the `uint256 _sharesToTransfer = getSharesByROUSG(_amount);` would be larger, and users would transfer more than expected shares during transferring.
2. In `unwrap()` function, the calculated `uint256 ousgSharesAmount = getSharesByROUSG(_rOUSGAmount);` would be larger, and users unwrapping rOUSG would burn more shares than expected. However, since the burned shares will be given to users as OUSG, so this doesn't matter that much.

Impact 1 may be an issue since it would be unfair for users (to burn more shares) who does a transfer while the oracle price is too low.

### Code Snippet

- https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378-L380

### Recommendation

Add a price sanity check for `MINIMUM_OUSG_PRICE` and keep consistent with `ousgInstantManager.sol`.

## [L-02] `rOUSG.sol#burn()` emits incorrect `Transfer` event

### Bug description

During `rOUSG.sol#burn()`, a Transfer event is emitted. However, this event has ambiguous meanings. What the function really does is it burns rOUGS and sends the `msg.sender` OUGS. For ERC20 tokens, emitting a Transfer event of `Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));` usually means minting of the token, instead of burning.

Also, the `ougs.transfer(...)` already emits a Transfer event to the `msg.sender`, so there is no need to emit an additional Transfer event.

```solidity
    function burn(
        address _account,
        uint256 _amount
    ) external onlyRole(BURNER_ROLE) {
        uint256 ousgSharesAmount = getSharesByROUSG(_amount);
        if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
        revert UnwrapTooSmall();

        _burnShares(_account, ousgSharesAmount);

        ousg.transfer(
        msg.sender,
        ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
        );
@>      emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
        emit TransferShares(_account, address(0), ousgSharesAmount);
    }
```

### Code Snippet

- https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L638

### Recommendation

Either remove this Transfer event emit, or change it to `Transfer(_account, address(0), _amount)`, if the original intention was to emit a event for burning rOUGS.

## [L-03] `ousgInstantManager.sol#_redeemBUIDL` performs incorrect balance check

### Bug description

The `_redeemBUIDL()` function redeems USDC from `buildRedeemer` by exchanging with BUIDL tokens in the contract. The amount of BUIDL tokens to exchange is `buidlAmountToRedeem`, however, the `require` statements checks for `minBUIDLRedeemAmount`, which is incorrect.

```solidity
  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    require(
@>    buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
    uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
    buidlRedeemer.redeem(buidlAmountToRedeem);
    require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
  }
```

### Code Snippet

- https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458-L470

### Recommendation

```diff
     require(
-      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
+      buidl.balanceOf(address(this)) >= buidlAmountToRedeem,
       "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
     );
```

## [NC-01] Incorrect natspec comment for multiple functions

The natspec comment for some functions are incorrect.

### 1. `rOUSG.sol`

There are two parts:

1. The balanceOf(user) is calculated incorrectly, they should be 10050 and 40202 respectively.
2. The comments claim that `Transfer` event emits only when explicit transfer between users happen, but for wrap/unwrap/burn functions, they are emitted.

- `wrap()`: `emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));`
- `unwrap()`: `emit Transfer(msg.sender, address(0), _rOUSGAmount);`
- `burn()`: `emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));`

```solidity
/**
 * @title Interest-bearing ERC20-like token for OUSG.
 *
 * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
 * controlled by the protocol. To calculate each account's balance, we do
 *
 *   shares[account] * ousgPrice
 *
 * For example, assume that we have:
 *
 *   ousgPrice = 100.505
 *   sharesOf(user1) -> 100
 *   sharesOf(user2) -> 400
 *
 * Therefore:
 *
 *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
 *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
 *
 * Since balances of all token holders change when the price of OUSG changes, this
 * token cannot fully implement ERC20 standard: it only emits `Transfer` events
 * upon explicit transfer between holders. In contrast, when total amount of pooled
 * Cash increases, no `Transfer` events are generated: doing so would require emitting
 * an event for each token holder and thus running an unbounded loop.
 *
 */
```

### 2. ousgInstantManager.sol#redeemRebasingOUSG

The @notice part should be `minting USDC for a given amount of rOUSG` instead.

```solidity
  /**
   * @notice Calculates fees and triggers minting rOUSG for a given amount of USDC
   *
   * @dev Please note that the fees are actually accumulated in `feeReceiver`
   *
   * @param rousgAmountIn Amount of rOUSG to redeem
   *
   * @return usdcAmountOut The amount of USDC returned to the user
   */
```

### Code Snippet

- https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L28C1-L53C4
- https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L353-L361

### Recommendation

Fix the comments.
