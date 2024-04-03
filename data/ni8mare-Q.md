## [L - 1] - The require statements in `setMintFee` and `setRedeemFee` are wrong

The require statement in `setMintFee` is as follows:
```
require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
```
The condition is checking the max fee condition on the state variable `mintFee` which has already been set. Instead, it should be checking this condition on `_mintFee` argument in the function. Because of this improper check, it still allows the `CONFIGURER_ROLE` to set the mint fees to a higher value than 200.

Similarly, redeem fees can be set higher than 200 by the `CONFIGURER_ROLE`.

Code snippet:
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L557
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L570

## [L - 2] Incorrect check in the require statement of `_redeemBUIDL` function

```
  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
```

The `_redeemBUIDL` function, the check `buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount` should be `buidl.balanceOf(address(this)) >= buidlAmountToRedeem`, as the amount of tokens being transferred equals `buidlAmountToRedeem` and this amount can be more than `minBUIDLRedeemAmount`. Hence, the check should be updated.

## [L - 3] Redundant allowance checks

For example, in the redeem function, this allowance check is redundant:

```
    require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    );
```

This is because in the following `transferFrom` call in redeem function, this check is internally being called. Hence, the above check is not needed. It increases the gas cost of the function.

## [L - 4] Users can prevent their tokens from being burnt by the admin

It was made clear by the sponsor that a KYCed account can hold multiple addresses. So, if they ever notice a transaction by the admin that is trying to burn their tokens, they can send small amounts of their balance to multiple addresses that they own by exploiting this condition in the `burn` function:

```
    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
      revert UnwrapTooSmall();
```

This check is redundant. It could have been used to prevent zero-value transfers in the following `transfer` call. But, for that a check to see whether the amount being transferred is above zero would suffice. Hence, the check above can be removed.
