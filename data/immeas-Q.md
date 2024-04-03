# QA Report


## Summary

| id | title |
| --- | --- |
| [L-01](#l-01-no-oracle-price-staleness-checks) | no oracle price staleness checks |
| [L-02](#l-02-user-blocked-by-circle-cannot-redeem) | user blocked by Circle cannot redeem |
| [L-03](#l-03-usdcreceiver-is-immutable) | `usdcReceiver` is immutable |
| [L-04](#l-04-ousginstantmanagermintredeem-lacks-slippage-parameter) | `ousgInstantManager::mint`/`redeem` lacks slippage parameter |
| [L-05](#l-05-lack-of-safe-transfer-wrapper) | lack of safe transfer wrapper |
| [NC-01](#nc-01-unnecessary-checks) | unnecessary checks |
| [NC-02](#nc-02-usdcfees-doesnt-follow-camelcase) | `usdcfees` doesn't follow camelCase |
| [NC-03](#nc-03-inconsistent-address0-checks) | inconsistent `address(0)` checks |
| [NC-04](#nc-04-erroneous-math-in-documentation) | erroneous math in documentation |
| [NC-05](#nc-05-misspelled-parameter) | misspelled parameter |


## Low


### L-01 no oracle price staleness checks

Both `ousgInstantManager` and `rOUSG` uses an oracle to determine the price of `OUSG`.

[`rOUSG::getOUSGPrice`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378-L380):
```solidity
File: contracts/ousg/rOUSG.sol

378:  function getOUSGPrice() public view returns (uint256 price) {
379:    (price, ) = oracle.getPriceData();
380:  }
```
Very similar in [`ousgInstantManager::getOUSGPrice`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479-L485) but with a lowest price check.


Here only the first param, `price` is used. However the second parameter returned is the [`priceTimestamp`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/rwaOracles/RWAOracleExternalComparisonCheck.sol#L127). Which is the timestamp at which the price was updated.

If this is old it can lead to incorrect `OUSG` prices used for `rOUSG` or instant `minting`/`redeeming`.

#### Recommendations
Consider adding a check that the price used isn't stale.


### L-02 user blocked by Circle cannot redeem

When instant redeeming either `OUSG` or `rOUSG`, at the end the user is funded their `USDC`
[`ousgInstantManager::_redeem`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L455):
```solidity
File: contracts/ousg/ousgInstantManager.sol

455:    usdc.transfer(msg.sender, usdcAmountOut);
```

The issue is that Circle (owner of `USDC`) can add addresses to a blocklist. If the user holding `OUSG` (or `rOUSG`) is blocked by Circle they will never be able to redeem.

#### Recommendations
Consider adding an `address to` for redemptions so that they can send the `USDC` to an address that is not blocked by Circle.


### L-03 `usdcReceiver` is immutable

Whenever someone mints, their `USDC` payment is sent to the address `usdcReciver`, [`ousgInstantManager::_mint`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L319):
```solidity
File: contracts/ousg/ousgInstantManager.sol

319:    usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
```

The issue is that `usdcReceiver` is [immutable](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90):
```solidity
File: contracts/ousg/ousgInstantManager.sol

90:  address public immutable usdcReceiver;
```

Where this address to be blocked by Circle minting in `ousgInstantManager` would stop to work and a new `ousgInstantManager` would have to be deployed using a new `usdcReceiver`. This could be confusing for users.

#### Recommendation
Consider making `usdcReceiver` mutable and add a way for the protocol to change it.


### L-04 `ousgInstantManager::mint`/`redeem` lacks slippage parameter

In `ousgInstantManager` you can mint either `rOUSG` or `OUSG` using `USDC` and then redeem back to `USDC`. Both of these use an oracle to track the price of `OUSG`. This price can vary between when a transaction is sent to when it is executed.

This can cause a user to mint or redeem at a different price than they intended.

#### Recommendation
Consider adding a `minOut` parameter for `ousgInstantManager::mint` and `redeem` calls.


### L-05 lack of safe transfer wrapper
In `ousgInstantManager` the admin can make a call to transfer any tokens out of the contract, [`ousgInstantManager::retrieveTokens`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819-L825):
```solidity
File: contracts/ousg/ousgInstantManager.sol

819:  function retrieveTokens(
820:    address token,
821:    address to,
822:    uint256 amount
823:  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
824:    IERC20(token).transfer(to, amount);
825:  }
```

Some tokens behave [weirdly](https://github.com/d-xo/weird-erc20?tab=readme-ov-file#revert-on-zero-value-transfers) when transferred and need some extra attention.

#### Recommendations
Consider using OZ `safeTransfer` wrapper to transfer tokens for better compatibility with different tokens


## Informational / Non critical


### NC-01 unnecessary checks

[`ousgInstantManager::_redeem`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L415-L420):
```solidity
File: contracts/ousg/ousgInstantManager.sol

415:    uint256 usdcFees = _getInstantRedemptionFees(usdcAmountToRedeem);
416:    usdcAmountOut = usdcAmountToRedeem - usdcFees;
417:    require(
418:      usdcAmountOut > 0,
419:      "OUSGInstantManager::_redeem: redeem amount can't be zero"
420:    );
```

`usdcAmountOut` can never be `0` here. As there is already [a check](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L402-L405) that `usdcAmountToRedeem` is greater than `minimumRedemptionAmount` and `minimumRedemptionAmount` can be at [the lowest `10_000`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602-L605).

The `redeemFee` can also be [no bigger than 2%](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570).

Hence, `usdcAmountOut` can never be lower than `9_800` (`10_000 - ((10_000 * 200) / 10_000)`).

The same logic applies to the `ousgAmountOut` in [`_mint`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310-L313), however the math is a bit more complicated since the lowest possible `9_800` usdc is converted to OUSG. However, due to the price having a lower cap, neither this can ever be `0`.

Consider removing these two checks.


### NC-02 `usdcfees` doesn't follow camelCase

[`ousgInstantManager::_mint`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L303):
```solidity
File: contracts/ousg/ousgInstantManager.sol

303:    uint256 usdcfees = _getInstantMintFees(usdcAmountIn);
```

Here `usdcfees` isn't camel cased. In [`_redeem`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L415) the same variable is using camel case, which is the naming convention used throughout the code.

Consider using camel case for `usdcfees` in `_mint` as well.


### NC-03 inconsistent `address(0)` checks

[`ousgInstantManager::setOracle`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638-L643), [`setFeeReceiver`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650-L656) and [`setInvestorBasedRateLimiter`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L673) all lets admin change various addresses to external contracts.

However, only `setFeeReceiver` checks for `address(0)` before assigning.

Consider checking for `address(0)` in all or none of the calls to have consistent behavior.


### NC-04 erroneous math in documentation

In the documentation for `rOUSG` it says:
[`rOUSG#L36-L45`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L36-L45):
```solidity
File: contracts/ousg/rOUSG.sol

36: * For example, assume that we have:
37: *
38: *   ousgPrice = 100.505
39: *   sharesOf(user1) -> 100
40: *   sharesOf(user2) -> 400
41: *
42: * Therefore:
43: *
44: *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
45: *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
```

This is confusing as firstly, one share is one ten-thousandth of a `OUSG` hence it is unclear what a "share" means here. And the math is wrong, `100 * 100.505 / 100 = 100.505` and `400 * 100.505 / 100 = 402.02`.

Consider updating the documentation.


### NC-05 misspelled parameter

[`ousgInstantManager::setInstantRedemptionLimitDuration`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540-L544):
```solidity
File: contracts/ousg/ousgInstantManager.sol

540:  function setInstantRedemptionLimitDuration(
541:    uint256 _instantRedemptionLimitDuratioin
542:  ) external override onlyRole(CONFIGURER_ROLE) {
543:    _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
544:  }
```

Here `_instantRedemptionLimitDuratioin` is misspelled, also in the [natspec](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L536) for the call.

Consider changing it to `_instantRedemptionLimitDuration`