## [L-01] `ROUSGFactory` uses outdated versions of OZ contracts

Most of the contracts used to deploy `ProxyAdmin` and `TokenProxy` use the older v4 versions. The newer v5 versions are much more lean and compact in code and size. It's always preferred to use the latest stable versions of dependencies.

Latest versions can be found here:
https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/proxy/transparent

## [L-02] Approval is disabled during pause
In case the ROUSG contract gets paused because of some risky conditions, the users will not be able to withdrawal all their approvals and prevent possible damage once the contract gets unpaused

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L476

```solidity
 function _approve(
    address _owner,
    address _spender,
    uint256 _amount
  ) internal whenNotPaused {
....
}
```

Consider removing the `whenNotPaused` modifier from `_approve()`.

## [L-03] `ROUSGFactory.Multicall()` is susceptible to returnbomb attack

Since the returndata from every call inside Multicall is not consumed using assembly it can be DOSed by returning too much data from the target address

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L126

```solidity
  function multiexcall(
    ExCallData[] calldata exCallData
  ) external payable override onlyGuardian returns (bytes[] memory results) {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }
```

Use assembly to limit the bytes of data that will be loaded into memory

## [L-04] Missing safe wrapper for ERC20 transfer in `OUSGInstantManager.retrieveTokens()`

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L819

Use a “safe” wrapper to execute ERC20 transfer for better compatibility.

ERC20 operations on arbitrary tokens should be [safely wrapped](https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#SafeERC20) to account for incompatible implementations.

## [L-05] Updating `instantMintLimit` inside TimeBasedRateLimiter does not reset the `currentInstantMintAmount` if set to 0, leading to overflow errors

This is how rate limiting gets calculated inside the `TimeBasedRateLimiter`:

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/InstantMintTimeBasedRateLimiter.sol#L93

```solidity
function _checkAndUpdateInstantMintLimit(uint256 amount) internal {
    ....
    if (
      block.timestamp >= lastResetInstantMintTime + resetInstantMintDuration
    ) {
      // time has passed, reset
      currentInstantMintAmount = 0;
      lastResetInstantMintTime = block.timestamp;
    }
    require(
      amount <= instantMintLimit - currentInstantMintAmount,
      "RateLimit: Mint exceeds rate limit"
    );

    .....
  }
```

In case `instantMintLimit` is set to 0 (disable minting) and `currentInstantMintAmount` is not reset it will revert with overflow error

Update setter function like so:

```solidity
function _setInstantMintLimit(uint256 _instantMintLimit) internal {
    if(_instantMintLimit== 0){
     currentInstantMintAmount = 0; <----------------
    };

    instantMintLimit = _instantMintLimit;
    emit InstantMintLimitSet(_instantMintLimit);
  }
```
## [L-06] Switch checks inside `OUSGInstantManager._redeem()`

In the following succession of checks:

```solidity
 if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
      // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
      // to cover the full amount
      _redeemBUIDL(usdcAmountToRedeem);
    } else if (usdcAmountToRedeem > usdcBalance) {
      // There isn't enough USDC held by this contract to cover the redemption,
      // so we perform a BUIDL redemption of BUIDL's minimum required amount.
      // The remaining amount of USDC will be held in the contract for future redemptions.
      _redeemBUIDL(minBUIDLRedeemAmount);
      emit MinimumBUIDLRedemption(
        msg.sender,
        minBUIDLRedeemAmount,
        usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
      );
    } else {
      // We have enough USDC sitting in this contract already, so use it
      // to cover the redemption and fees without redeeming more BUIDL.
      emit BUIDLRedemptionSkipped(
        msg.sender,
        usdcAmountToRedeem,
        usdcBalance - usdcAmountToRedeem
      );
```

The `if(usdcAmountToRedeem < usdcBalance)` check should be placed first, this way if there is is enough leftover USDC in the contract, no BUILD redemptions will be made => less USDC which does not earn yield will stay in the contract.

## [L-07] Missing zero address checks at a couple of functions

- `ROUSG.__rOUSG_init_unchained()` - no check for `_ousg, _oracle, guardian` addresses
- `ROUSGFactory.constructor()` - no check for the `guardian` address
- `OUSGInstantManager.retrieveTokens()` - `to` address
- `OUSGInstantManager.setInvestorBasedRateLimiter()` - `_investorBasedRateLimiter` address
- `OUSGInstantManager.setOracle()` - `_oracle` address

## [N-01] Missing calls to base initializers in ROUSG

`ROUSG` does not call the following initializers of parent contracts:
- `__AccessControl_init`
-  `__Pausable_init()`

## [N-02] Increase/DecreaseAllowance methods can be removed from `ROUSG`

The 2 methods have recently been removed from the OZ ERC20 standard due to reported risk of phishing attack. You can consider removing them.

Here is the discussion:
https://github.com/OpenZeppelin/openzeppelin-contracts/issues/4583

## [N-03] Consider adding a conditional event emitting flag to `ROUSG._approve()`

To save gas OZ implements an `emitEvent` flag  to `_approve()` like so:

```
function _approve(address owner, address spender, uint256 value, bool emitEvent) internal virtual {
```

And this is the explanation behind it:

https://github.com/OpenZeppelin/openzeppelin-contracts/blob/cb2aaaa04a292887c49839cd958b08a83979d746/contracts/token/ERC20/ERC20.sol#L265-L270

```
By default (when calling {_approve}) the flag is set to true. On the other hand, approval changes made by
     * `_spendAllowance` during the `transferFrom` operation set the flag to false. This saves gas by not emitting any
     * `Approval` event during `transferFrom` operations.
     *
     * Anyone who wishes to continue emitting `Approval` events on the`transferFrom` operation can force the flag to
     * true using the following override:
```

## [N-03] Unused constant variable inside `ROUSGFactory`

The `DEFAULT_ADMIN_ROLE` is defined inside `ROUSGFactory.sol`, but it is never used. It should be removed to reduce contract size and provide better readability

## [N-04] Consider adding `AccessControlDefaultAdminRules` as inherited contract by `OUSGInstantManager`

Since `DEFAULT_ADMIN_ROLE` is the admin role for all roles this carries significant risk. OpenZeppelin provides and recommends that contracts implementing `AccesControl` also add `AccessControlDefaultAdminRules` as dependency which introduces numerous safety measures to prevent some common scenarios from happening - like for example revoking unintentionaly the admin.


Docs:
https://docs.openzeppelin.com/contracts/5.x/api/access#AccessControlDefaultAdminRules

## [N-04] No check if array is empty in `OUSGInstantManager.multiexcall()`

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L803

```
 function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
     ......
    }
  }
```

Add the following check at the start of the function to prevent needless variable initializations and reads 

```
require(exCallData.length > 0, "Empty calldata");
```

## [N-06] `OUSGInstantManager` setters do not check if values are the same

The setter functions listed don’t check if the new value is different from the old value, causing unnecessary storage writes.