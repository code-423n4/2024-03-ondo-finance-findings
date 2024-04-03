# 1. Redemptions can be partially blocked if `BUIDL` gets paused.

Lines of code* 

https://etherscan.io/address/0x603bb6909be14f83282e03632280d91be7fb83b2#readContract#F32
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L426C1-L440C6

### Impact

In certain cases during redemption, the protocol might need to redeem `BUIDL` to buff up the amount of `USDC` in the contract. `Buidl` token is pausable and when paused, will not be transferrable. This can lead to temporary halting of redemptions for users swapping large amounts. 
```
  function _redeem(
    uint256 ousgAmountIn
  ) internal returns (uint256 usdcAmountOut) {
...
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
...
  }
```

***

# 2. User exit methods should not be pausable

Lines of code* 

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L341
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L368

### Impact

The `redeem` and `redeemRebasingOUSG` functions in ousgInstantManager contract hold a `whenRedeemNotPaused` modifier. This can put users' funds at risk if the contract is paused other than by design. Considering that admin roles can be renounced, the funds can be stuck in the contract forever.

```
  function redeem(
    uint256 ousgAmountIn
  )
    external
    override
    nonReentrant
    whenRedeemNotPaused
    returns (uint256 usdcAmountOut)
  {..
  }
```

```
  function redeemRebasingOUSG(
    uint256 rousgAmountIn
  )
    external
    override
    nonReentrant
    whenRedeemNotPaused
    returns (uint256 usdcAmountOut)
  {
...
  }
  ```

### Recommended Mitigation Steps

Remove the `whenRedeemNotPaused` modifiers.

***

# 3. Allowance check before `transferFrom` is not necessary.

Lines of code* 

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L344-L347

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L371-L374

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L298-L301

### Impact

The below functions check for the caller's given allowance to the contract before calling the `transferFrom` function. This however is not needed as the `transferFrom` function already checks for the spender's available allowance.

```
  function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {
...
    require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    );
...
    // Transfer USDC
    if (usdcfees > 0) {
      usdc.transferFrom(msg.sender, feeReceiver, usdcfees);
    }
    usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);

    emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);

    ousg.mint(to, ousgAmountOut);
  }
```
```
  function redeem(
    uint256 ousgAmountIn
  )
...
    require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    );
    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
  }
```
```
  function redeemRebasingOUSG(
    uint256 rousgAmountIn
  )
...
  {
    require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    );
    rousg.transferFrom(msg.sender, address(this), rousgAmountIn);
```

As an example, `rOUSG`'s `transferFrom` function.

```
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
### Recommended Mitigation Steps
Remove the allowance checks as they're not required.

***

# 4. Add an option for users to specify recipient in cases where users get blocklisted by `USDC`

Lines of code* 

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L455
https://etherscan.io/address/0x43506849d7c04f9138d1a2050bbf3a0c054402dd#readContract#F12

### Impact

During redemption, `USDC` is transferred directly to `msg.sender`. However, `usdc` holds blocklisting properties and as such, a blocklisted user will not be able to redeem his `OUSG`/`rOUSG` for `USDC` leaving them stuck in the contract. A potential way to bypass this is to include a receiver parameter in the redeem functions. That way, users can specify the address that they'd like to receive their `USDC` into.
```
  function _redeem(
    uint256 ousgAmountIn
  ) internal returns (uint256 usdcAmountOut) {
...

    if (usdcFees > 0) {
      usdc.transfer(feeReceiver, usdcFees);
    }
    emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);

    usdc.transfer(msg.sender, usdcAmountOut);
  }
```

***


# 5. Setting the `minBUIDLRedeemAmount` less than `BUIDL` redemption minimum requirement can unintentionally lock redemption.

Lines of code*

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L622

### Impact
The protocol works with the assumption that `BUIDL` has a redemption limit of about 250_000 BUIDL tokens. But the `setMinimumBUIDLRedemptionAmount` doesn't validate that the amount set is greater than this amount. 
```
  function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
...
    minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
  }
```
The redemption process can therefore be temporarily blocked in those cases where the `minBUIDLRedeemAmount` is needed to be redeemed.

```
  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
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
  }
```
### Recommended Mitigation Steps
Add a check to ensure that `minimumBUIDLRedemptionAmount` set is not less than minimum redemption amount required by `BUIDL`. 

***

# 6. Consider introducing a permit functionality

Lines of code*
 
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L231

### Impact

The ERC20 permit functionality is a streamlined, gas efficient and pretty secure way of granting approvals (with limits and deadlines) to spenders. It's become a major feature of many ERC20 tokens and many protocols in the sphere. The `rOUSG` token however doesn't hold a permit function, thereby missing out on its various advantages and flexibility. Consider introducing the functionality to improve user experience and help with external integrations.

***


# 7. Should account for max approval during `transferFrom`

Lines of code*
 
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L276-L287

### Impact
The `transferFrom` function checks for spender's allowance and decreases accordingly before transfer. It however doesn't account for approval type.(uint256)max, which is universally considered to be max approval. Due to the possibly large amounts of tokens that will be in move in the protocol, checking for max approval is a nice feature to have. 
```
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
### Recommended Mitigation Steps
Consider not reducing user's approval is they're max approved.
```
  function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
    uint256 currentAllowance = allowances[_sender][msg.sender];
    if (currentAllowance == type(uint256).max) {
        _transfer(_sender, _recipient, _amount);
    }
    else {
    require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");
    _transfer(_sender, _recipient, _amount);
    _approve(_sender, msg.sender, currentAllowance - _amount);
    }
    return true;
  }
```
***

# 8. Should account for `msg.sender` == `_sender` during `transferFrom`

Lines of code* 

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L276-L287

### Impact

In certain cases, the token owner might want to perform a `transferFrom` from itself to another user. A nice to have feature is to not require the owner to have to approve himself to spend his own tokens before he can perform a `tranferFrom`. This can be fixed by skipping the allowance check if `msg.sender` == `_sender`.
### Recommended Mitigation Steps
```
  function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
    uint256 currentAllowance = allowances[_sender][msg.sender];
    if (currentAllowance == type(uint256).max || msg.sender == _sender) {
        _transfer(_sender, _recipient, _amount);
    }
    else {
    require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");
    _transfer(_sender, _recipient, _amount);
    _approve(_sender, msg.sender, currentAllowance - _amount);
  }
    return true;
  }
```

***


# 9. Redemption will be completely broken if `USDC` gets paused

Lines of code*
 
https://etherscan.io/address/0x43506849d7c04f9138d1a2050bbf3a0c054402dd#readContract#F19
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L317
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L319
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L451
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L455

### Impact

`ousgInstantManager` is fully dependent `USDC` token for deposits and redemption. The issue is that `USDC` is a pausable token, upon which its transfers are prohibited. If this happens, token redemptions will be completely blocked.

### Recommended Mitigation Steps
Consider introducing an emergency token, like `USDT` that users can redeem their `OUSG` and `rOUSG` for.

***

# 10. Admin roles can be reounced

Lines of code* 

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlUpgradeable.sol#L219
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/external/openzeppelin/contracts/access/AccessControl.sol#L191
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L24
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L18

### Impact
`rOUSG.sol` and  `ousgInstantManager.sol` inherit openzeppelin's `AccessControlEnumerable` and `AccessControlEnumerableUpgradeable` contracts, which both feature the `renounceRole` function. Permissioned functions in these contracts will be lost if these roles are renounced not by design.

### Recommended Mitigation Steps
Consider overriding the `renounceRole` functions and reverting when they're called.
***

***

# 11. `whenNotPaused` modifier can be moved from major functions into a general internal function

Lines of code* 

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L415
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L431
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L505
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L529
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L557

### Impact
The whenNotPaused modifier is used on the `wrap`, `unwrap`, `_mintShares`, `_burnShares` and `_transferShares` functions. These functions all call the `_beforeTokenTransfer` hook. As a bit of refactoring, consider moving the modifier from these functions into the `beforeTokenTransfer` function instead.

```solidity
  function _beforeTokenTransfer(
    address from,
    address to,
    uint256
  ) internal view whenNotPaused {
    // Check constraints when `transferFrom` is called to facliitate
    // a transfer between two parties that are not `from` or `to`.
    if (from != msg.sender && to != msg.sender) {
      require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");
    }

    if (from != address(0)) {
      // If not minting
      require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd");
    }

    if (to != address(0)) {
      // If not burning
      require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd");
    }
  }
```
***
# 12. Excess ETH from multicall not refunded 

Lines of code* 

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L794
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L121

### Impact
In `rOUSGFactory` and `ousgInstantManager` contracts, the `multiexcall` is payable and takes in `ETH`.  After calling an external contract and forwards some ETH value, the contract balance should be checked. If there is excess eth left over due to a failed call, or more eth being delivered than needed, or any other reason, this eth must be refunded handled appropriately, otherwise the eth may be frozen in the contract forever.

```solidity
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
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }
```
### Recommended Mitigation Steps
Consider including a check for excess tokens and returning it to the sender
***
***

# 13. `retrieveTokens` function cannot withdraw `ETH`

Lines of code* 
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L819

### Impact

The `ousgInstantManager` contract can receive `ETH` through the `multiexcall` function which is marked `payable`. The function however doesn't refund any excess `ETH` sent back to the sender. A possible way to handle this is through the `retrieveTokens` function which the admin can use to rescue any possible stranded tokens in the contract. 
However, the function doesn't account for `ETH` which means that any excess `ETH` sent to the contract will be lost.

```solidity
  function retrieveTokens(
    address token,
    address to,
    uint256 amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
    IERC20(token).transfer(to, amount);
  }
```
### Recommended Mitigation Steps

Consider refactoring the function to handle `ETH` too, as an example.
```solidity
  function retrieveTokens(
    address token,
    address to,
    uint256 amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
    if (token == ETH){
     to.call{value: amount}("");
     }
    else{
    IERC20(token).transfer(to, amount);
    }
  }
```
***