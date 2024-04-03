The content section shows only 10 examples, subsequent cases are listed as links.

## Summary

### Low Risk Issues

|                 | Issue                                                                                                  | Instances |
| --------------- | :----------------------------------------------------------------------------------------------------- | :-------: |
| [[L-01](#l-01)] | increase/decrease allowance should be used instead of approve                                          |     4     |
| [[L-02](#l-02)] | Must approve or increase allowance first                                                               |     4     |
| [[L-03](#l-03)] | Emitting storage values instead of the memory one.                                                     |    13     |
| [[L-04](#l-04)] | Missing contract-existence checks before low-level calls                                               |     2     |
| [[L-05](#l-05)] | Functions calling contracts/addresses with transfer hooks are missing reentrancy guards                |     4     |
| [[L-06](#l-06)] | Approve zero first                                                                                     |     2     |
| [[L-07](#l-07)] | Code does not follow the best practice of check-effects-interaction                                    |    15     |
| [[L-08](#l-08)] | Consider bounding input array length                                                                   |     2     |
| [[L-09](#l-09)] | `approve` will always revert as the `IERC20` interface mismatch                                        |     2     |
| [[L-10](#l-10)] | Return values of `approve` not checked                                                                 |     2     |
| [[L-11](#l-11)] | Large transfers may not work with some `ERC20` tokens                                                  |     9     |
| [[L-12](#l-12)] | Large approvals may not work with some `ERC20` tokens                                                  |     2     |
| [[L-13](#l-13)] | Use `increaseAllowance()`/`decreaseAllowance()` instead of `approve()`/`safeApprove()`                 |     2     |
| [[L-14](#l-14)] | Consider the case where `totalSupply` is zero                                                          |     1     |

### NonCritical Risk Issues

|                 | Issue                                                                                                  | Instances |
| --------------- | :----------------------------------------------------------------------------------------------------- | :-------: |
| [[N-01](#n-01)] | Keccak state variables should be immutable not constant                                                |     5     |
| [[N-02](#n-02)] | Private and internal state variables should have a preceding _ in their name unless they are constants |     4     |
| [[N-03](#n-03)] | Emits without `msg.sender` parameter                                                                   |     1     |
| [[N-04](#n-04)] | NatSpec `@param` is missing                                                                            |    30     |
| [[N-05](#n-05)] | Use multiple `require()` and `if` statements instead of `&&`                                           |     1     |
| [[N-06](#n-06)] | `Import` only specific files                                                                           |    23     |
| [[N-07](#n-07)] | `Constants` in comparisons should appear on the left side                                              |    33     |
| [[N-08](#n-08)] | Consider using `delete` rather than assigning zero/false to clear values                               |     2     |
| [[N-09](#n-09)] | Unused contract variables                                                                              |     1     |
| [[N-10](#n-10)] | Remaining eth may not be refunded to users                                                             |     2     |
| [[N-11](#n-11)] | External calls in an un-bounded `for`-loop may result in a DOS                                         |     2     |
| [[N-12](#n-12)] | `constructor` missing zero address check                                                               |     2     |
| [[N-13](#n-13)] | Large multiples of ten should use scientific notation                                                  |     3     |
| [[N-14](#n-14)] | Complex math should be split into multiple steps                                                       |     1     |
| [[N-15](#n-15)] | Duplicated `require/if` statements should be refactored                                                |    19     |
| [[N-16](#n-16)] | Variable names don't follow the Solidity naming convention                                             |     1     |
| [[N-17](#n-17)] | Contract functions should use an `interface`                                                           |    22     |
| [[N-18](#n-18)] | State variables should include comments                                                                |    34     |
| [[N-19](#n-19)] | Missing NatSpec from contract declarations                                                             |     1     |
| [[N-20](#n-20)] | Inconsistent usage of `require`/`error`                                                                |    17     |
| [[N-21](#n-21)] | Use of `override` is unnecessary                                                                       |    20     |
| [[N-22](#n-22)] | Modifier declarations should have NatSpec descriptions                                                 |     1     |
| [[N-23](#n-23)] | Function declarations should have NatSpec descriptions                                                 |    13     |
| [[N-24](#n-24)] | Function names should use lowerCamelCase                                                               |    13     |
| [[N-25](#n-25)] | Setters should prevent re-setting of the same value                                                    |    11     |
| [[N-26](#n-26)] | Consider disallowing transfers to `address(this)`                                                      |     4     |
| [[N-27](#n-27)] | Named imports of parent contracts are missing                                                          |     3     |
| [[N-28](#n-28)] | Events may be emitted out of order due to reentrancy                                                   |     9     |
| [[N-29](#n-29)] | Missing zero address check in initializer                                                              |     1     |
| [[N-30](#n-30)] | Missing NatSpec `@author` from contract declaration                                                    |     1     |
| [[N-31](#n-31)] | Missing NatSpec `@dev` from contract declaration                                                       |     2     |
| [[N-32](#n-32)] | Missing NatSpec `@notice` from contract declaration                                                    |     1     |
| [[N-33](#n-33)] | Missing NatSpec from error declaration                                                                 |     1     |
| [[N-34](#n-34)] | Missing NatSpec `@dev` from error declaration                                                          |     1     |
| [[N-35](#n-35)] | Missing NatSpec `@notice` from error declaration                                                       |     1     |
| [[N-36](#n-36)] | Missing NatSpec `@param` from error declaration                                                        |     1     |
| [[N-37](#n-37)] | Missing NatSpec `@dev` from event declaration                                                          |     1     |
| [[N-38](#n-38)] | Missing NatSpec `@notice` from event declaration                                                       |     1     |
| [[N-39](#n-39)] | Missing NatSpec `@param` from event declaration                                                        |     1     |
| [[N-40](#n-40)] | Missing NatSpec from modifiers definitions                                                             |     1     |
| [[N-41](#n-41)] | Missing NatSpec `@dev` from modifier declaration                                                       |     3     |
| [[N-42](#n-42)] | Missing NatSpec `@notice` from modifier declaration                                                    |     1     |
| [[N-43](#n-43)] | Missing NatSpec `@param` from modifier declaration                                                     |     3     |
| [[N-44](#n-44)] | Missing NatSpec `@dev` from function declaration                                                       |    48     |
| [[N-45](#n-45)] | Missing NatSpec `@notice` from function declaration                                                    |    26     |
| [[N-46](#n-46)] | Simplify complex require statements                                                                    |     1     |
| [[N-47](#n-47)] | Events should be emitted before external calls                                                         |    14     |
| [[N-48](#n-48)] | Use `@inheritdoc` for overridden functions                                                             |    20     |
| [[N-49](#n-49)] | Missing NatSpec from variable declarations                                                             |    34     |
| [[N-50](#n-50)] | Contract name does not follow the Solidity Style Guide                                                 |     3     |
| [[N-51](#n-51)] | Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES                                 |     8     |
| [[N-52](#n-52)] | Use a single file for system wide constants                                                            |    10     |
| [[N-53](#n-53)] | Contracts should have full test coverage                                                               |     1     |
| [[N-54](#n-54)] | Large or complicated code bases should implement invariant tests                                       |     1     |
| [[N-55](#n-55)] | Codebase should implement formal verification testing                                                  |     1     |
| [[N-56](#n-56)] | State variables not capped at reasonable values                                                        |     1     |
| [[N-57](#n-57)] | Consider adding a block/deny-list                                                                      |     3     |
| [[N-58](#n-58)] | Expressions for constant values should use `immutable` rather than `constant`                          |     6     |
| [[N-59](#n-59)] | Lines are too long                                                                                     |    15     |
| [[N-60](#n-60)] | Typos                                                                                                  |     1     |

### Low Risk Issues

### [L-01]<a name="l-01"></a> increase/decrease allowance should be used instead of approve

In order to prevent front running, increase/decrease allowance should be used in place of approve where possible

*There are 4 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
252	    _approve(msg.sender, _spender, _amount);
...
285	    _approve(_sender, msg.sender, currentAllowance - _amount);
...
306	    _approve(
307	      msg.sender,
308	      _spender,
309	      allowances[msg.sender][_spender] + _addedValue
310	    );
...
337	    _approve(msg.sender, _spender, currentAllowance - _subtractedValue);
```

*GitHub* : [252](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L252), [285](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L285), [306..310](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L306-L310), [337](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L337)

### [L-02]<a name="l-02"></a> Must approve or increase allowance first

In the context of ERC20 tokens, a token holder needs to "approve" another account to transfer a certain amount of their tokens on their behalf. This is accomplished by calling the `approve()` function, which takes the address of the spender and the amount they're allowed to spend as parameters. 

This approval step is a crucial part of the ERC20 standard because it allows for secure delegated transfers. A common use case for this feature is in decentralized exchanges or DeFi protocols, where a user can approve a smart contract to transfer tokens on their behalf. 

After the approval step, the approved account (or contract) can then transfer tokens up to the approved amount from the token holder's account by calling the `transferFrom()` function. This function takes three parameters: the address of the token holder, the recipient's address, and the amount to transfer.

If an account tries to call `transferFrom()` before the token holder has called `approve()`, the transaction will fail because the ERC20 contract checks whether the `transferFrom()` caller has an adequate allowance. 

In summary, if a contract or user needs to move ERC20 tokens on behalf of another account, it's necessary to ensure that the token holder has first called `approve()` to set a sufficient allowance. This is a key aspect of ERC20 token security and functionality. 

*There are 4 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
 // @audit function call transfer from, but not approve
278	  function _mint(
279	    uint256 usdcAmountIn,
280	    address to
281	  ) internal returns (uint256 ousgAmountOut) {
...
317	      usdc.transferFrom(msg.sender, feeReceiver, usdcfees);
...
319	    usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
...
 // @audit function call transfer from, but not approve
335	  function redeem(
336	    uint256 ousgAmountIn
337	  )
338	    external
339	    override
340	    nonReentrant
341	    whenRedeemNotPaused
342	    returns (uint256 usdcAmountOut)
343	  {
...
348	    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
```

*GitHub* : [317](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L317), [319](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L319), [348](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L348)


---

	 - contracts/ousg/rOUSG.sol

```solidity
 // @audit function call transfer from, but not approve
415	  function wrap(uint256 _OUSGAmount) external whenNotPaused {
...
419	    ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
```

*GitHub* : [419](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L419)

### [L-03]<a name="l-03"></a> Emitting storage values instead of the memory one.

Emitted values should not be read from storage again. Instead, the existing values from memory should be used.

*There are 13 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
321	    emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);
...
435	      emit MinimumBUIDLRedemption(
436	        msg.sender,
437	        minBUIDLRedeemAmount,
438	        usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
439	      );
...
453	    emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);
...
558	    emit MintFeeSet(mintFee, _mintFee);
...
571	    emit RedeemFeeSet(redeemFee, _redeemFee);
...
589	    emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
...
606	    emit MinimumRedemptionAmountSet(
607	      minimumRedemptionAmount,
608	      _minimumRedemptionAmount
609	    );
...
625	    emit MinimumBUIDLRedemptionAmountSet(
626	      minBUIDLRedeemAmount,
627	      _minimumBUIDLRedemptionAmount
628	    );
...
641	    emit OracleSet(address(oracle), _oracle);
...
654	    emit FeeReceiverSet(feeReceiver, _feeReceiver);
```

*GitHub* : [321](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L321), [435..439](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L435-L439), [453](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L453), [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L558), [571](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L571), [589](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L589), [606..609](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L606-L609), [625..628](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L625-L628), [641](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L641), [654](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L654), [666..669](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L666-L669)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [614](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L614)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [96..102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L96-L102)

### [L-04]<a name="l-04"></a> Missing contract-existence checks before low-level calls

Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `<address>.code.length > 0`

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit contract existance not checked before this call
805	      (bool success, bytes memory ret) = address(exCallData[i].target).call{
```

*GitHub* : [805](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
// @audit contract existance not checked before this call
126	      (bool success, bytes memory ret) = address(exCallData[i].target).call{
```

*GitHub* : [126](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126)

### [L-05]<a name="l-05"></a> Functions calling contracts/addresses with transfer hooks are missing reentrancy guards

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to [read-only reentrancies](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect against it, except by block-listing the whole protocol.`

*There are 4 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
819	  function retrieveTokens(
820	    address token,
821	    address to,
822	    uint256 amount
823	  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
...
// @audit Function `retrieveTokens` doesn't  have the `nonReentrant` modifier
824	    IERC20(token).transfer(to, amount);
```

*GitHub* : [824](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L824)


---

	 - contracts/ousg/rOUSG.sol

```solidity
415	  function wrap(uint256 _OUSGAmount) external whenNotPaused {
...
// @audit Function `wrap` doesn't  have the `nonReentrant` modifier
419	    ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
...
431	  function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
...
// @audit Function `unwrap` doesn't  have the `nonReentrant` modifier
437	    ousg.transfer(
...
624	  function burn(
625	    address _account,
626	    uint256 _amount
627	  ) external onlyRole(BURNER_ROLE) {
...
// @audit Function `burn` doesn't  have the `nonReentrant` modifier
634	    ousg.transfer(
```

*GitHub* : [419](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L419), [437](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L437), [634](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L634)

### [L-06]<a name="l-06"></a> Approve zero first

Some ERC20 tokens (like USDT) do not work when changing the allowance from an existing non-zero allowance value. For example Tether (USDT)'s `approve()` function will revert if the current approval is not zero, to protect against front-running changes of approvals.

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
254	  function mintRebasingOUSG(
255	    uint256 usdcAmountIn
256	  )
257	    external
258	    override
259	    nonReentrant
260	    whenMintNotPaused
261	    returns (uint256 rousgAmountOut)
262	  {
263	    uint256 ousgAmountOut = _mint(usdcAmountIn, address(this));
264	    ousg.approve(address(rousg), ousgAmountOut);
265	    rousg.wrap(ousgAmountOut);
266	    rousgAmountOut = rousg.getROUSGByShares(
267	      ousgAmountOut * OUSG_TO_ROUSG_SHARES_MULTIPLIER
268	    );
269	    rousg.transfer(msg.sender, rousgAmountOut);
270	    emit InstantMintRebasingOUSG(
271	      msg.sender,
272	      usdcAmountIn,
273	      ousgAmountOut,
274	      rousgAmountOut
275	    );
276	  }
...
458	  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
459	    require(
460	      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
461	      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
462	    );
463	    uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
464	    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
465	    buidlRedeemer.redeem(buidlAmountToRedeem);
466	    require(
467	      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
468	      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
469	    );
470	  }
```

*GitHub* : [254..276](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254-L276), [458..470](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458-L470)

### [L-07]<a name="l-07"></a> Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

*There are 15 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit Some statements does not follow CEI
335	  function redeem(
336	    uint256 ousgAmountIn
337	  )
338	    external
339	    override
340	    nonReentrant
341	    whenRedeemNotPaused
342	    returns (uint256 usdcAmountOut)
343	  {
...
// @audit Statement out of CEI order
349	    usdcAmountOut = _redeem(ousgAmountIn);
...
// @audit Some statements does not follow CEI
362	  function redeemRebasingOUSG(
363	    uint256 rousgAmountIn
364	  )
365	    external
366	    override
367	    nonReentrant
368	    whenRedeemNotPaused
369	    returns (uint256 usdcAmountOut)
370	  {
...
// @audit Statement out of CEI order
379	    usdcAmountOut = _redeem(ousgAmountIn);
...
// @audit Some statements does not follow CEI
554	  function setMintFee(
555	    uint256 _mintFee
556	  ) external override onlyRole(CONFIGURER_ROLE) {
...
// @audit Statement out of CEI order
559	    mintFee = _mintFee;
...
// @audit Some statements does not follow CEI
567	  function setRedeemFee(
568	    uint256 _redeemFee
569	  ) external override onlyRole(CONFIGURER_ROLE) {
...
// @audit Statement out of CEI order
572	    redeemFee = _redeemFee;
...
// @audit Some statements does not follow CEI
581	  function setMinimumDepositAmount(
582	    uint256 _minimumDepositAmount
583	  ) external override onlyRole(CONFIGURER_ROLE) {
...
// @audit Statement out of CEI order
590	    minimumDepositAmount = _minimumDepositAmount;
```

*GitHub* : [349](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L349), [379](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L379), [559](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L559), [572](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L572), [590](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L590), [610](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L610), [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L655), [809](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L809)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [403](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L403), [480](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L480), [518](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L518), [539](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L539), [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L567)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L95), [130](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L130)

### [L-08]<a name="l-08"></a> Consider bounding input array length

The functions below take in an unbounded array, and make function calls for entries in the array. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to `require()` that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit array parameter `exCallData` is used as loop condition and length is not cheched in function
795	    ExCallData[] calldata exCallData
...
// @audit loop uses unbounded parameter
804	    for (uint256 i = 0; i < exCallData.length; ++i) {
```

*GitHub* : [804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
// @audit array parameter `exCallData` is used as loop condition and length is not cheched in function
122	    ExCallData[] calldata exCallData
...
// @audit loop uses unbounded parameter
125	    for (uint256 i = 0; i < exCallData.length; ++i) {
```

*GitHub* : [125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)

### [L-09]<a name="l-09"></a> `approve` will always revert as the `IERC20` interface mismatch

Some tokens, such as [USDT](https://etherscan.io/token/0xdac17f958d2ee523a2206206994597c13d831ec7#code#L199), have a different implementation for the approve function: when the address is cast to a compliant `IERC20` interface and the approve function is used, it will always revert due to the interface mismatch.

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
264	    ousg.approve(address(rousg), ousgAmountOut);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
464	    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
```

*GitHub* : [264](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L264), [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L464)

### [L-10]<a name="l-10"></a> Return values of `approve` not checked

Not all `IERC20` implementations (e.g. USDT, KNC) `revert` when there's a failure in `approve`. The function signature has a boolean return value and they indicate errors that way instead.

By not checking the return value, operations that should have marked as failed, may potentially go through without actually approving anything.

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
264	    ousg.approve(address(rousg), ousgAmountOut);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
464	    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
```

*GitHub* : [264](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L264), [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L464)

### [L-11]<a name="l-11"></a> Large transfers may not work with some `ERC20` tokens

Some `IERC20` implementations (e.g `UNI`, `COMP`) may fail if the valued `transferred` is larger than `uint96`. [Source](https://github.com/d-xo/weird-erc20/blob/main/src/Uint96.sol).

*There are 9 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
317	      usdc.transferFrom(msg.sender, feeReceiver, usdcfees);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
319	    usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
348	    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
451	      usdc.transfer(feeReceiver, usdcFees);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
455	    usdc.transfer(msg.sender, usdcAmountOut);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
824	    IERC20(token).transfer(to, amount);
```

*GitHub* : [317](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L317), [319](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L319), [348](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L348), [451](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L451), [455](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L455), [824](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L824)


---

	 - contracts/ousg/rOUSG.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
419	    ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
437	    ousg.transfer(
438	      msg.sender,
439	      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
440	    );
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
634	    ousg.transfer(
635	      msg.sender,
636	      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
637	    );
```

*GitHub* : [419](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L419), [437..440](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L437-L440), [634..637](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L634-L637)

### [L-12]<a name="l-12"></a> Large approvals may not work with some `ERC20` tokens

Not all `IERC20` implementations are totally compliant, and some (e.g `UNI`, `COMP`) may fail if the valued passed to `approve` is larger than `uint96`. If the approval amount is `type(uint256).max`, which may cause issues with systems that expect the value passed to approve to be reflected in the allowances mapping.

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
264	    ousg.approve(address(rousg), ousgAmountOut);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
464	    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
```

*GitHub* : [264](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L264), [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L464)

### [L-13]<a name="l-13"></a> Use `increaseAllowance()`/`decreaseAllowance()` instead of `approve()`/`safeApprove()`

Changing an allowance with `approve()` brings the risk that someone may use both the old and the new allowance by unfortunate transaction ordering. Refer to [ERC20 API: An Attack Vector on the Approve/TransferFrom Methods](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM).
It is recommended to use the `increaseAllowance()`/`decreaseAllowance()` to avoid ths problem.

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
264	    ousg.approve(address(rousg), ousgAmountOut);
...
// @audit Contracts that implement `ERC20`: `ERC20`, `IERC20`, `IERC20Metadata`, `IOMMF`, `IRWALike`, `IUSDY`, `IWOMMF`, `MockUSDC`, `SafeTransferLib`, `SafeERC20`
464	    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
```

*GitHub* : [264](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L264), [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L464)

### [L-14]<a name="l-14"></a> Consider the case where `totalSupply` is zero

The following functions should handle the edge case where the totalSupply is zero, for example to avoid division by zero errors, as such errors may negatively impact the logic of these functions.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
188	  function totalSupply() public view returns (uint256) {
189	    return
190	      (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
191	  }
```

*GitHub* : [188..191](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188-L191)

### NonCritical Risk Issues

### [N-01]<a name="n-01"></a> Keccak state variables should be immutable not constant

Constant keccak variables should be replaced with immutable variables in Solidity contracts to optimize gas usage and enhance efficiency. While constant variables are evaluated and computed at runtime, immutable variables are assigned during contract deployment and stored directly in the contract bytecode. By using immutable for keccak variables, their hash values are computed only once during deployment, reducing the gas cost associated with repeated computations at runtime. This approach leads to more efficient execution, conserving resources for users, and allowing for smoother contract interactions, ultimately benefiting the overall performance and user experience.

*There are 5 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
57	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
...
60	  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57), [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60)


---

	 - contracts/ousg/rOUSG.sol

```solidity
93	  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
...
94	  bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
...
95	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```

*GitHub* : [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L93), [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94), [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)

### [N-02]<a name="n-02"></a> Private and internal state variables should have a preceding _ in their name unless they are constants

Add a preceding underscore to the state variable name, take care to refactor where there variables are read/wrote

*There are 4 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
72	  mapping(address => uint256) private shares;
...
75	  mapping(address => mapping(address => uint256)) private allowances;
...
78	  uint256 private totalShares;
```

*GitHub* : [72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72), [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75), [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L78)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
40	  address internal immutable guardian;
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40)

### [N-03]<a name="n-03"></a> Emits without `msg.sender` parameter

If `msg.sender` play a part in the functionality of a function, any emits of this function should include msg.sender to ensure transparency with users

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
// @audit Current function use `msg.sender`, but do not emit it
639	    emit TransferShares(_account, address(0), ousgSharesAmount);
```

*GitHub* : [639](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L639)

### [N-04]<a name="n-04"></a> NatSpec `@param` is missing



*There are 30 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
278	  function _mint(
279	    uint256 usdcAmountIn,
280	    address to
281	  ) internal returns (uint256 ousgAmountOut) {
...
388	  function _redeem(
389	    uint256 ousgAmountIn
390	  ) internal returns (uint256 usdcAmountOut) {
...
458	  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
...
731	  /**
732	   * @notice Scale provided amount up by `decimalsMultiplier`
733	   *
734	   * @dev This helper is used for converting a USDC amount's decimals
735	   *      representation to the rOUSG/OUSG decimals representation.
736	   */
737	  function _scaleUp(uint256 amount) internal view returns (uint256) {
...
741	  /**
742	   * @notice Scale provided amount down by `decimalsMultiplier`
743	   *
744	   * @dev This helper is used for converting an rOUSG/OUSG amount's decimals
745	   *      representation to the USDC decimals representation.
746	   */
747	  function _scaleDown(uint256 amount) internal view returns (uint256) {
...
794	  function multiexcall(
795	    ExCallData[] calldata exCallData
796	  )
797	    external
798	    payable
799	    override
800	    onlyRole(DEFAULT_ADMIN_ROLE)
801	    returns (bytes[] memory results)
802	  {
```

*GitHub* : [278..281](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278-L281), [388..390](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388-L390), [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458), [731..737](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L731-L737), [741..747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L741-L747), [794..802](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)


---

	 - contracts/ousg/rOUSG.sol

```solidity
102	  function initialize(
103	    address _kycRegistry,
104	    uint256 requirementGroup,
105	    address _ousg,
106	    address guardian,
107	    address _oracle
108	  ) public virtual initializer {
...
112	  function __rOUSG_init(
113	    address _kycRegistry,
114	    uint256 requirementGroup,
115	    address _ousg,
116	    address guardian,
117	    address _oracle
118	  ) internal onlyInitializing {
...
128	  function __rOUSG_init_unchained(
129	    address _kycRegistry,
130	    uint256 _requirementGroup,
131	    address _ousg,
132	    address guardian,
133	    address _oracle
134	  ) internal onlyInitializing {
...
193	  /**
194	   * @return the amount of tokens owned by the `_account`.
195	   *
196	   * @dev Balances are dynamic and equal the `_account`'s OUSG shares multiplied
197	   *      by the price of OUSG
198	   */
199	  function balanceOf(address _account) public view returns (uint256) {
```

*GitHub* : [102..108](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108), [112..118](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112-L118), [128..134](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128-L134), [193..199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L193-L199), [205..220](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L205-L220), [225..234](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L225-L234), [238..251](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L238-L251), [256..280](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L256-L280), [289..305](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L289-L305), [314..331](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L314-L331), [351..356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L351-L356), [360..365](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L360-L365), [370..373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L370-L373), [382..400](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L382-L400), [445..454](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L445-L454), [461..476](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L461-L476), [484..487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L484-L487), [491..505](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L491-L505), [521..532](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L521-L532), [544..557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L544-L557), [572..590](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L572-L590), [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656..658](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)

### [N-05]<a name="n-05"></a> Use multiple `require()` and `if` statements instead of `&&`

Using multiple `require()` and `if` improves code readability and makes it easier to debug.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
593	    if (from != msg.sender && to != msg.sender) {
594	      require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");
595	    }
```

*GitHub* : [593..595](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L593-L595)

### [N-06]<a name="n-06"></a> `Import` only specific files

Using import declarations of the form `import {<identifier_name>} from "some/file.sol"` avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation

*There are 23 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
18	import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";
...
19	import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";
...
20	import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";
...
21	import "contracts/ousg/rOUSG.sol";
...
22	import "contracts/interfaces/IRWALike.sol";
...
23	import "contracts/interfaces/IBUIDLRedeemer.sol";
...
24	import "contracts/InstantMintTimeBasedRateLimiter.sol";
...
25	import "contracts/interfaces/IOUSGInstantManager.sol";
...
26	import "contracts/interfaces/IMulticall.sol";
...
27	import "contracts/interfaces/IInvestorBasedRateLimiter.sol";
```

*GitHub* : [18](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L18), [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L19), [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L20), [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L21), [22](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L22), [23](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L23), [24](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L24), [25](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L25), [26](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L26), [27](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L27)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [18](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L18), [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L19), [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L20), [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L21), [22](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L22), [23](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L23), [24](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L24), [25](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L25), [26](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L26)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19), [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L20), [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L21), [22](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L22)

### [N-07]<a name="n-07"></a> `Constants` in comparisons should appear on the left side

Doing so will prevent [typo bugs](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html)

*There are 33 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
164	      address(_usdc) != address(0),
...
168	      address(_usdcReciever) != address(0),
...
172	      address(_feeReceiver) != address(0),
...
176	      address(_ousgOracle) != address(0),
...
179	    require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
...
180	    require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
...
181	    require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
...
183	      address(_buidlRedeemer) != address(0),
...
283	      IERC20Metadata(address(usdc)).decimals() == 6,
...
291	    if (address(investorBasedRateLimiter) != address(0)) {
```

*GitHub* : [164](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L164), [168](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L168), [172](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L172), [176](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L176), [179](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L179), [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L180), [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L181), [183](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L183), [283](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L283), [291](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L291), [311](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L311), [316](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L316), [392](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L392), [396](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L396), [408](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L408), [418](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L418), [450](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L450), [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557), [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570), [653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L653), [689](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L689), [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367), [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416), [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432), [477](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L477), [478](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L478), [506](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506), [507](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L507), [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533), [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L558), [597](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L597), [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L602)

### [N-08]<a name="n-08"></a> Consider using `delete` rather than assigning zero/false to clear values

The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
775	    mintPaused = false;
...
787	    redeemPaused = false;
```

*GitHub* : [775](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L775), [787](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L787)

### [N-09]<a name="n-09"></a> Unused contract variables

Note that there may be cases where a variable appears to be used, but this is only because there are multiple definitions of the varible in different files. In such cases, the variable definition should be moved into a separate file. The instances below are the unused variables.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
38	  bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

*GitHub* : [38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38)

### [N-10]<a name="n-10"></a> Remaining eth may not be refunded to users

 When a contract function accepts Ethereum and executes a `.call()` or similar function that also forwards Ethereum value, it's important to check for and refund any remaining balance. This is because some of the supplied value may not be used during the call execution due to gas constraints, a revert in the called contract, or simply because not all the value was needed.

If you do not account for this remaining balance, it can become "locked" in the contract. It's crucial to either return the remaining balance to the sender or handle it in a way that ensures it is not permanently stuck. Neglecting to do so can lead to loss of funds and degradation of the contract's reliability. Furthermore, it's good practice to ensure fairness and trust with your users by returning unused funds. 

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
794	  function multiexcall(
795	    ExCallData[] calldata exCallData
796	  )
797	    external
798	    payable
799	    override
800	    onlyRole(DEFAULT_ADMIN_ROLE)
801	    returns (bytes[] memory results)
802	  {
```

*GitHub* : [794..802](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
121	  function multiexcall(
122	    ExCallData[] calldata exCallData
123	  ) external payable override onlyGuardian returns (bytes[] memory results) {
```

*GitHub* : [121..123](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121-L123)

### [N-11]<a name="n-11"></a> External calls in an un-bounded `for`-loop may result in a DOS

Consider limiting the number of iterations in `for`-loops that make external calls

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
804	    for (uint256 i = 0; i < exCallData.length; ++i) {
805	      (bool success, bytes memory ret) = address(exCallData[i].target).call{
806	        value: exCallData[i].value
807	      }(exCallData[i].data);
808	      require(success, "Call Failed");
809	      results[i] = ret;
810	    }
```

*GitHub* : [804..810](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804-L810)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
125	    for (uint256 i = 0; i < exCallData.length; ++i) {
126	      (bool success, bytes memory ret) = address(exCallData[i].target).call{
127	        value: exCallData[i].value
128	      }(exCallData[i].data);
129	      require(success, "Call Failed");
130	      results[i] = ret;
131	    }
```

*GitHub* : [125..131](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125-L131)

### [N-12]<a name="n-12"></a> `constructor` missing zero address check

It is important to ensure that the constructor does not allow zero address to be set.
    This is a common mistake that can lead to loss of funds or redeployment of the contract.

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
144	  constructor(
145	    address defaultAdmin,
146	    address _usdc,
147	    address _usdcReciever,
148	    address _feeReceiver,
149	    address _ousgOracle,
150	    address _ousg,
151	    address _rousg,
152	    address _buidl,
153	    address _buidlRedeemer,
154	    RateLimiterConfig memory rateLimiterConfig
155	  )
156	    InstantMintTimeBasedRateLimiter(
157	      rateLimiterConfig.mintLimitDuration,
158	      rateLimiterConfig.redeemLimitDuration,
159	      rateLimiterConfig.mintLimit,
160	      rateLimiterConfig.redeemLimit
161	    )
162	  {
```

*GitHub* : [144..162](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144-L162)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
47	  constructor(address _guardian) {
```

*GitHub* : [47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)

### [N-13]<a name="n-13"></a> Large multiples of ten should use scientific notation

Use a scientific notation rather than decimal literals (e.g. `1e6` instead of `1000000`), for better code readability. The same for exponentiation  (e.g. `1e18` instead of `10**18`): although the compiler is capable of optimizing it, it is considered good coding practice to utilize idioms that don't rely on compiler optimization, whenever possible.

*There are 3 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
66	  uint256 public constant FEE_GRANULARITY = 10_000;
...
69	  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
```

*GitHub* : [66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66), [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69)


---

	 - contracts/ousg/rOUSG.sol

```solidity
87	  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87)

### [N-14]<a name="n-14"></a> Complex math should be split into multiple steps

Consider splitting long arithmetic calculations into multiple steps to improve the code readability.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
367	      (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
```

*GitHub* : [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367)

### [N-15]<a name="n-15"></a> Duplicated `require/if` statements should be refactored

These statements should be refactored to a separate function, as there are multiple parts of the codebase that use the same logic, to improve the code readability and reduce code duplication.



*There are 19 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
283	      IERC20Metadata(address(usdc)).decimals() == 6,
...
291	    if (address(investorBasedRateLimiter) != address(0)) {
...
392	      IERC20Metadata(address(usdc)).decimals() == 6,
...
396	      IERC20Metadata(address(buidl)).decimals() == 6,
...
408	    if (address(investorBasedRateLimiter) != address(0)) {
...
164	      address(_usdc) != address(0),
...
168	      address(_usdcReciever) != address(0),
...
172	      address(_feeReceiver) != address(0),
...
176	      address(_ousgOracle) != address(0),
...
183	      address(_buidlRedeemer) != address(0),
```

*GitHub* : [283](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L283), [291](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L291), [392](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L392), [396](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L396), [408](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L408), [164](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L164), [168](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L168), [172](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L172), [176](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L176), [183](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L183), [187](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L187), [191](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L191)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [434](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L434), [507](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L507), [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533), [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594), [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L599), [604](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L604), [629](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L629)

### [N-16]<a name="n-16"></a> Variable names don't follow the Solidity naming convention

Use `mixedCase` for local and state variables that are not constants, and add a trailing underscore for internal variables. [Documentation](https://docs.soliditylang.org/en/latest/style-guide.html#local-and-state-variable-names)

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
455	    uint256 _sharesToTransfer = getSharesByROUSG(_amount);
```

*GitHub* : [455](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L455)

### [N-17]<a name="n-17"></a> Contract functions should use an `interface`

All `external`/`public` functions should extend an `interface`. This is useful to make sure that the whole API is extracted.

*There are 22 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
479	  function getOUSGPrice() public view returns (uint256 price) {
...
768	  function pauseMint() external onlyRole(PAUSER_ROLE) {
...
774	  function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {
...
780	  function pauseRedeem() external onlyRole(PAUSER_ROLE) {
...
786	  function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {
...
819	  function retrieveTokens(
820	    address token,
821	    address to,
822	    uint256 amount
823	  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
```

*GitHub* : [479](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479), [768](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L768), [774](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L774), [780](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L780), [786](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L786), [819..823](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819-L823)


---

	 - contracts/ousg/rOUSG.sol

```solidity
102	  function initialize(
103	    address _kycRegistry,
104	    uint256 requirementGroup,
105	    address _ousg,
106	    address guardian,
107	    address _oracle
108	  ) public virtual initializer {
...
302	  function increaseAllowance(
303	    address _spender,
304	    uint256 _addedValue
305	  ) public returns (bool) {
...
328	  function decreaseAllowance(
329	    address _spender,
330	    uint256 _subtractedValue
331	  ) public returns (bool) {
...
347	  function getTotalShares() public view returns (uint256) {
```

*GitHub* : [102..108](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108), [302..305](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302-L305), [328..331](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328-L331), [347](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L347), [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356), [363..365](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363-L365), [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373), [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378), [397..400](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397-L400), [415](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415), [431](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L431), [613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613), [624..627](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624-L627), [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642), [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [70..75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70-L75)

### [N-18]<a name="n-18"></a> State variables should include comments

Consider adding some comments on critical state variables to explain what they are supposed to do: this will help for future code reviews.

*There are 34 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
57	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
...
60	  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
...
63	  uint256 public constant MINIMUM_OUSG_PRICE = 105e18;
...
66	  uint256 public constant FEE_GRANULARITY = 10_000;
...
69	  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
...
72	  IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;
...
75	  IRWALike public immutable ousg;
...
78	  ROUSG public immutable rousg;
...
81	  IERC20 public immutable buidl;
...
84	  IBUIDLRedeemer public immutable buidlRedeemer;
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57), [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60), [63](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L63), [66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66), [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69), [72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72), [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L75), [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L78), [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L81), [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L84), [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L87), [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90), [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L93), [96](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L96), [99](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L99), [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L102), [106](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L106), [110](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L110), [113](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L113), [116](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L116), [120](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L120), [123](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L123)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L78), [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L81), [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L84), [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87), [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94), [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38), [40](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40), [41](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L41), [42](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L42), [43](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L43), [45](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45)

### [N-19]<a name="n-19"></a> Missing NatSpec from contract declarations

Some contracts miss a `@dev`/`@notice` NatSpec, which should be a [best practice](https://docs.soliditylang.org/en/latest/natspec-format.html) to add as a documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
28	/**
29	 * @title Interest-bearing ERC20-like token for OUSG.
30	 *
31	 * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
32	 * controlled by the protocol. To calculate each account's balance, we do
33	 *
34	 *   shares[account] * ousgPrice
35	 *
36	 * For example, assume that we have:
37	 *
38	 *   ousgPrice = 100.505
39	 *   sharesOf(user1) -> 100
40	 *   sharesOf(user2) -> 400
41	 *
42	 * Therefore:
43	 *
44	 *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
45	 *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
46	 *
47	 * Since balances of all token holders change when the price of OUSG changes, this
48	 * token cannot fully implement ERC20 standard: it only emits `Transfer` events
49	 * upon explicit transfer between holders. In contrast, when total amount of pooled
50	 * Cash increases, no `Transfer` events are generated: doing so would require emitting
51	 * an event for each token holder and thus running an unbounded loop.
52	 *
53	 */
54	
55	contract ROUSG is
56	  Initializable,
57	  ContextUpgradeable,
58	  PausableUpgradeable,
59	  AccessControlEnumerableUpgradeable,
60	  KYCRegistryClientUpgradeable,
61	  IERC20Upgradeable,
62	  IERC20MetadataUpgradeable
63	{
64	  /**
65	   * @dev rOUSG balances are dynamic and are calculated based on the accounts' shares (OUSG)
66	   * and the the price of OUSG. Account shares aren't
67	   * normalized, so the contract also stores the sum of all shares to calculate
68	   * each account's token balance which equals to:
69	   *
70	   *   shares[account] * ousgPrice
71	   */
72	  mapping(address => uint256) private shares;
```

*GitHub* : [28..72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L28-L72)

### [N-20]<a name="n-20"></a> Inconsistent usage of `require`/`error`

Some parts of the codebase use `require` statements, while others use custom errors. Consider refactoring the code to use the same approach: the following findings represent the minority of `require` vs error, and they show the first occurance in each file, for brevity.

*There are 17 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
435	      revert UnwrapTooSmall();
...
630	      revert UnwrapTooSmall();
...
282	    require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");
...
333	    require(
334	      currentAllowance >= _subtractedValue,
335	      "DECREASED_ALLOWANCE_BELOW_ZERO"
336	    );
...
416	    require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");
...
432	    require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
...
477	    require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");
...
478	    require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");
...
506	    require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");
...
507	    require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");
```

*GitHub* : [435](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L435), [630](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L630), [282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L282), [333..336](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L333-L336), [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416), [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432), [477](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L477), [478](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L478), [506](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506), [507](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L507), [512..515](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L512-L515), [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533), [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L558), [563](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L563), [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594), [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L599), [604](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L604)

### [N-21]<a name="n-21"></a> Use of `override` is unnecessary

Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the `override` keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.

*There are 20 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
230	  function mint(
231	    uint256 usdcAmountIn
232	  )
233	    external
234	    override
235	    nonReentrant
236	    whenMintNotPaused
237	    returns (uint256 ousgAmountOut)
238	  {
...
254	  function mintRebasingOUSG(
255	    uint256 usdcAmountIn
256	  )
257	    external
258	    override
259	    nonReentrant
260	    whenMintNotPaused
261	    returns (uint256 rousgAmountOut)
262	  {
...
335	  function redeem(
336	    uint256 ousgAmountIn
337	  )
338	    external
339	    override
340	    nonReentrant
341	    whenRedeemNotPaused
342	    returns (uint256 usdcAmountOut)
343	  {
...
362	  function redeemRebasingOUSG(
363	    uint256 rousgAmountIn
364	  )
365	    external
366	    override
367	    nonReentrant
368	    whenRedeemNotPaused
369	    returns (uint256 usdcAmountOut)
370	  {
...
498	  function setInstantMintLimit(
499	    uint256 _instantMintLimit
500	  ) external override onlyRole(CONFIGURER_ROLE) {
...
512	  function setInstantRedemptionLimit(
513	    uint256 _instantRedemptionLimit
514	  ) external override onlyRole(CONFIGURER_ROLE) {
...
526	  function setInstantMintLimitDuration(
527	    uint256 _instantMintLimitDuration
528	  ) external override onlyRole(CONFIGURER_ROLE) {
...
540	  function setInstantRedemptionLimitDuration(
541	    uint256 _instantRedemptionLimitDuratioin
542	  ) external override onlyRole(CONFIGURER_ROLE) {
...
554	  function setMintFee(
555	    uint256 _mintFee
556	  ) external override onlyRole(CONFIGURER_ROLE) {
...
567	  function setRedeemFee(
568	    uint256 _redeemFee
569	  ) external override onlyRole(CONFIGURER_ROLE) {
```

*GitHub* : [230..238](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L230-L238), [254..262](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254-L262), [335..343](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335-L343), [362..370](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362-L370), [498..500](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498-L500), [512..514](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512-L514), [526..528](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526-L528), [540..542](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540-L542), [554..556](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554-L556), [567..569](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567-L569), [581..583](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581-L583), [599..601](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599-L601), [622..624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622-L624), [638..640](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638-L640), [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650-L652), [663..665](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L665), [794..802](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656..658](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [121..123](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121-L123)

### [N-22]<a name="n-22"></a> Modifier declarations should have NatSpec descriptions



*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
149	  modifier onlyGuardian() {
150	    require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");
151	    _;
152	  }
```

*GitHub* : [149..152](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149-L152)

### [N-23]<a name="n-23"></a> Function declarations should have NatSpec descriptions



*There are 13 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
278	  function _mint(
279	    uint256 usdcAmountIn,
280	    address to
281	  ) internal returns (uint256 ousgAmountOut) {
...
388	  function _redeem(
389	    uint256 ousgAmountIn
390	  ) internal returns (uint256 usdcAmountOut) {
...
458	  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
...
794	  function multiexcall(
795	    ExCallData[] calldata exCallData
796	  )
797	    external
798	    payable
799	    override
800	    onlyRole(DEFAULT_ADMIN_ROLE)
801	    returns (bytes[] memory results)
802	  {
```

*GitHub* : [278..281](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278-L281), [388..390](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388-L390), [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458), [794..802](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)


---

	 - contracts/ousg/rOUSG.sol

```solidity
102	  function initialize(
103	    address _kycRegistry,
104	    uint256 requirementGroup,
105	    address _ousg,
106	    address guardian,
107	    address _oracle
108	  ) public virtual initializer {
...
112	  function __rOUSG_init(
113	    address _kycRegistry,
114	    uint256 requirementGroup,
115	    address _ousg,
116	    address guardian,
117	    address _oracle
118	  ) internal onlyInitializing {
...
128	  function __rOUSG_init_unchained(
129	    address _kycRegistry,
130	    uint256 _requirementGroup,
131	    address _ousg,
132	    address guardian,
133	    address _oracle
134	  ) internal onlyInitializing {
...
378	  function getOUSGPrice() public view returns (uint256 price) {
...
642	  function pause() external onlyRole(PAUSER_ROLE) {
...
646	  function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
```

*GitHub* : [102..108](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108), [112..118](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112-L118), [128..134](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128-L134), [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378), [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642), [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646), [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656..658](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)

### [N-24]<a name="n-24"></a> Function names should use lowerCamelCase

According to the Solidity [style guide](https://docs.soliditylang.org/en/latest/style-guide.html#function-names) function names should be in `mixedCase` (lowerCamelCase)

*There are 13 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
254	  function mintRebasingOUSG(
255	    uint256 usdcAmountIn
256	  )
257	    external
258	    override
259	    nonReentrant
260	    whenMintNotPaused
261	    returns (uint256 rousgAmountOut)
262	  {
...
362	  function redeemRebasingOUSG(
363	    uint256 rousgAmountIn
364	  )
365	    external
366	    override
367	    nonReentrant
368	    whenRedeemNotPaused
369	    returns (uint256 usdcAmountOut)
370	  {
...
458	  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
...
479	  function getOUSGPrice() public view returns (uint256 price) {
...
622	  function setMinimumBUIDLRedemptionAmount(
623	    uint256 _minimumBUIDLRedemptionAmount
624	  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
```

*GitHub* : [254..262](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254-L262), [362..370](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362-L370), [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458), [479](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479), [622..624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622-L624)


---

	 - contracts/ousg/rOUSG.sol

```solidity
112	  function __rOUSG_init(
113	    address _kycRegistry,
114	    uint256 requirementGroup,
115	    address _ousg,
116	    address guardian,
117	    address _oracle
118	  ) internal onlyInitializing {
...
128	  function __rOUSG_init_unchained(
129	    address _kycRegistry,
130	    uint256 _requirementGroup,
131	    address _ousg,
132	    address guardian,
133	    address _oracle
134	  ) internal onlyInitializing {
...
363	  function getSharesByROUSG(
364	    uint256 _rOUSGAmount
365	  ) public view returns (uint256) {
...
373	  function getROUSGByShares(uint256 _shares) public view returns (uint256) {
...
378	  function getOUSGPrice() public view returns (uint256 price) {
```

*GitHub* : [112..118](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112-L118), [128..134](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128-L134), [363..365](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363-L365), [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373), [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378), [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656..658](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [70..75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70-L75)

### [N-25]<a name="n-25"></a> Setters should prevent re-setting of the same value

This especially problematic when the setter also emits the same value, which may be confusing to offline parsers

*There are 11 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
554	  function setMintFee(
555	    uint256 _mintFee
556	  ) external override onlyRole(CONFIGURER_ROLE) {
...
567	  function setRedeemFee(
568	    uint256 _redeemFee
569	  ) external override onlyRole(CONFIGURER_ROLE) {
...
581	  function setMinimumDepositAmount(
582	    uint256 _minimumDepositAmount
583	  ) external override onlyRole(CONFIGURER_ROLE) {
...
599	  function setMinimumRedemptionAmount(
600	    uint256 _minimumRedemptionAmount
601	  ) external override onlyRole(CONFIGURER_ROLE) {
...
622	  function setMinimumBUIDLRedemptionAmount(
623	    uint256 _minimumBUIDLRedemptionAmount
624	  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
...
638	  function setOracle(
639	    address _oracle
640	  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
...
650	  function setFeeReceiver(
651	    address _feeReceiver
652	  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
...
663	  function setInvestorBasedRateLimiter(
664	    address _investorBasedRateLimiter
665	  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
```

*GitHub* : [554..556](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554-L556), [567..569](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567-L569), [581..583](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581-L583), [599..601](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599-L601), [622..624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622-L624), [638..640](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638-L640), [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650-L652), [663..665](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L665)


---

	 - contracts/ousg/rOUSG.sol

```solidity
128	  function __rOUSG_init_unchained(
129	    address _kycRegistry,
130	    uint256 _requirementGroup,
131	    address _ousg,
132	    address guardian,
133	    address _oracle
134	  ) internal onlyInitializing {
...
472	  function _approve(
473	    address _owner,
474	    address _spender,
475	    uint256 _amount
476	  ) internal whenNotPaused {
```

*GitHub* : [128..134](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128-L134), [472..476](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L472-L476), [613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613)

### [N-26]<a name="n-26"></a> Consider disallowing transfers to `address(this)`



*There are 4 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
819	  function retrieveTokens(
820	    address token,
821	    address to,
822	    uint256 amount
823	  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
```

*GitHub* : [819..823](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819-L823)


---

	 - contracts/ousg/rOUSG.sol

```solidity
220	  function transfer(address _recipient, uint256 _amount) public returns (bool) {
...
431	  function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
...
624	  function burn(
625	    address _account,
626	    uint256 _amount
627	  ) external onlyRole(BURNER_ROLE) {
```

*GitHub* : [220](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L220), [431](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L431), [624..627](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624-L627)

### [N-27]<a name="n-27"></a> Named imports of parent contracts are missing



*There are 3 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
49	contract OUSGInstantManager is
50	  ReentrancyGuard,
51	  InstantMintTimeBasedRateLimiter,
52	  AccessControlEnumerable,
53	  IOUSGInstantManager,
54	  IMulticall
55	{
56	  // Role to configure the contract
57	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```

*GitHub* : [49..57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49-L57)


---

	 - contracts/ousg/rOUSG.sol

```solidity
55	contract ROUSG is
56	  Initializable,
57	  ContextUpgradeable,
58	  PausableUpgradeable,
59	  AccessControlEnumerableUpgradeable,
60	  KYCRegistryClientUpgradeable,
61	  IERC20Upgradeable,
62	  IERC20MetadataUpgradeable
63	{
64	  /**
65	   * @dev rOUSG balances are dynamic and are calculated based on the accounts' shares (OUSG)
66	   * and the the price of OUSG. Account shares aren't
67	   * normalized, so the contract also stores the sum of all shares to calculate
68	   * each account's token balance which equals to:
69	   *
70	   *   shares[account] * ousgPrice
71	   */
72	  mapping(address => uint256) private shares;
```

*GitHub* : [55..72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55-L72)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
37	contract ROUSGFactory is IMulticall {
38	  bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

*GitHub* : [37..38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37-L38)

### [N-28]<a name="n-28"></a> Events may be emitted out of order due to reentrancy

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls

*There are 9 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
254	  function mintRebasingOUSG(
255	    uint256 usdcAmountIn
256	  )
257	    external
258	    override
259	    nonReentrant
260	    whenMintNotPaused
261	    returns (uint256 rousgAmountOut)
262	  {
...
278	  function _mint(
279	    uint256 usdcAmountIn,
280	    address to
281	  ) internal returns (uint256 ousgAmountOut) {
...
335	  function redeem(
336	    uint256 ousgAmountIn
337	  )
338	    external
339	    override
340	    nonReentrant
341	    whenRedeemNotPaused
342	    returns (uint256 usdcAmountOut)
343	  {
...
362	  function redeemRebasingOUSG(
363	    uint256 rousgAmountIn
364	  )
365	    external
366	    override
367	    nonReentrant
368	    whenRedeemNotPaused
369	    returns (uint256 usdcAmountOut)
370	  {
...
388	  function _redeem(
389	    uint256 ousgAmountIn
390	  ) internal returns (uint256 usdcAmountOut) {
```

*GitHub* : [254..262](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254-L262), [278..281](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278-L281), [335..343](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335-L343), [362..370](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362-L370), [388..390](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388-L390)


---

	 - contracts/ousg/rOUSG.sol

```solidity
415	  function wrap(uint256 _OUSGAmount) external whenNotPaused {
...
431	  function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
...
624	  function burn(
625	    address _account,
626	    uint256 _amount
627	  ) external onlyRole(BURNER_ROLE) {
```

*GitHub* : [415](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415), [431](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L431), [624..627](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624-L627)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
70	  function deployRebasingOUSG(
71	    address kycRegistry,
72	    uint256 requirementGroup,
73	    address ousg,
74	    address oracle
75	  ) external onlyGuardian returns (address, address, address) {
```

*GitHub* : [70..75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70-L75)

### [N-29]<a name="n-29"></a> Missing zero address check in initializer



*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
102	  function initialize(
103	    address _kycRegistry,
104	    uint256 requirementGroup,
105	    address _ousg,
106	    address guardian,
107	    address _oracle
108	  ) public virtual initializer {
```

*GitHub* : [102..108](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108)

### [N-30]<a name="n-30"></a> Missing NatSpec `@author` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@author` notation to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
28	/**
29	 * @title Interest-bearing ERC20-like token for OUSG.
30	 *
31	 * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
32	 * controlled by the protocol. To calculate each account's balance, we do
33	 *
34	 *   shares[account] * ousgPrice
35	 *
36	 * For example, assume that we have:
37	 *
38	 *   ousgPrice = 100.505
39	 *   sharesOf(user1) -> 100
40	 *   sharesOf(user2) -> 400
41	 *
42	 * Therefore:
43	 *
44	 *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
45	 *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
46	 *
47	 * Since balances of all token holders change when the price of OUSG changes, this
48	 * token cannot fully implement ERC20 standard: it only emits `Transfer` events
49	 * upon explicit transfer between holders. In contrast, when total amount of pooled
50	 * Cash increases, no `Transfer` events are generated: doing so would require emitting
51	 * an event for each token holder and thus running an unbounded loop.
52	 *
53	 */
54	
55	contract ROUSG is
56	  Initializable,
57	  ContextUpgradeable,
58	  PausableUpgradeable,
59	  AccessControlEnumerableUpgradeable,
60	  KYCRegistryClientUpgradeable,
61	  IERC20Upgradeable,
62	  IERC20MetadataUpgradeable
63	{
64	  /**
65	   * @dev rOUSG balances are dynamic and are calculated based on the accounts' shares (OUSG)
66	   * and the the price of OUSG. Account shares aren't
67	   * normalized, so the contract also stores the sum of all shares to calculate
68	   * each account's token balance which equals to:
69	   *
70	   *   shares[account] * ousgPrice
71	   */
72	  mapping(address => uint256) private shares;
```

*GitHub* : [28..72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L28-L72)

### [N-31]<a name="n-31"></a> Missing NatSpec `@dev` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@dev` notation to improve the code documentation.

*There are 2 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
28	/**
29	 * @title Interest-bearing ERC20-like token for OUSG.
30	 *
31	 * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
32	 * controlled by the protocol. To calculate each account's balance, we do
33	 *
34	 *   shares[account] * ousgPrice
35	 *
36	 * For example, assume that we have:
37	 *
38	 *   ousgPrice = 100.505
39	 *   sharesOf(user1) -> 100
40	 *   sharesOf(user2) -> 400
41	 *
42	 * Therefore:
43	 *
44	 *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
45	 *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
46	 *
47	 * Since balances of all token holders change when the price of OUSG changes, this
48	 * token cannot fully implement ERC20 standard: it only emits `Transfer` events
49	 * upon explicit transfer between holders. In contrast, when total amount of pooled
50	 * Cash increases, no `Transfer` events are generated: doing so would require emitting
51	 * an event for each token holder and thus running an unbounded loop.
52	 *
53	 */
54	
55	contract ROUSG is
56	  Initializable,
57	  ContextUpgradeable,
58	  PausableUpgradeable,
59	  AccessControlEnumerableUpgradeable,
60	  KYCRegistryClientUpgradeable,
61	  IERC20Upgradeable,
62	  IERC20MetadataUpgradeable
63	{
64	  /**
65	   * @dev rOUSG balances are dynamic and are calculated based on the accounts' shares (OUSG)
66	   * and the the price of OUSG. Account shares aren't
67	   * normalized, so the contract also stores the sum of all shares to calculate
68	   * each account's token balance which equals to:
69	   *
70	   *   shares[account] * ousgPrice
71	   */
72	  mapping(address => uint256) private shares;
```

*GitHub* : [28..72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L28-L72)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
24	/**
25	 * @title ROUSGFactory
26	 * @author Ondo Finance
27	 * @notice This contract serves as a Factory for the upgradable rOUSG token contract.
28	 *         Upon calling `deployRebasingOUSG` the `guardian` address (set in constructor) will
29	 *         deploy the following:
30	 *         1) rOUSG - The implementation contract, ERC20 contract with the initializer disabled
31	 *         2) ProxyAdmin - OZ ProxyAdmin contract, used to upgrade the proxy instance.
32	 *                         @notice Owner is set to `guardian` address.
33	 *         3) TransparentUpgradeableProxy - OZ, proxy contract. Admin is set to `address(proxyAdmin)`.
34	 *                                          `_logic' is set to `address(rOUSG)`.
35	 * @notice `guardian` address in constructor is a msig.
36	 */
37	contract ROUSGFactory is IMulticall {
38	  bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

*GitHub* : [24..38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L24-L38)

### [N-32]<a name="n-32"></a> Missing NatSpec `@notice` from contract declaration

Some contract definitions have an incomplete NatSpec: add a `@notice` notation to describe the contract to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
28	/**
29	 * @title Interest-bearing ERC20-like token for OUSG.
30	 *
31	 * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
32	 * controlled by the protocol. To calculate each account's balance, we do
33	 *
34	 *   shares[account] * ousgPrice
35	 *
36	 * For example, assume that we have:
37	 *
38	 *   ousgPrice = 100.505
39	 *   sharesOf(user1) -> 100
40	 *   sharesOf(user2) -> 400
41	 *
42	 * Therefore:
43	 *
44	 *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
45	 *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
46	 *
47	 * Since balances of all token holders change when the price of OUSG changes, this
48	 * token cannot fully implement ERC20 standard: it only emits `Transfer` events
49	 * upon explicit transfer between holders. In contrast, when total amount of pooled
50	 * Cash increases, no `Transfer` events are generated: doing so would require emitting
51	 * an event for each token holder and thus running an unbounded loop.
52	 *
53	 */
54	
55	contract ROUSG is
56	  Initializable,
57	  ContextUpgradeable,
58	  PausableUpgradeable,
59	  AccessControlEnumerableUpgradeable,
60	  KYCRegistryClientUpgradeable,
61	  IERC20Upgradeable,
62	  IERC20MetadataUpgradeable
63	{
64	  /**
65	   * @dev rOUSG balances are dynamic and are calculated based on the accounts' shares (OUSG)
66	   * and the the price of OUSG. Account shares aren't
67	   * normalized, so the contract also stores the sum of all shares to calculate
68	   * each account's token balance which equals to:
69	   *
70	   *   shares[account] * ousgPrice
71	   */
72	  mapping(address => uint256) private shares;
```

*GitHub* : [28..72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L28-L72)

### [N-33]<a name="n-33"></a> Missing NatSpec from error declaration

Consider adding some comments on error declarations to explain what they are supposed to do: this will help for future code reviews.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
90	  error UnwrapTooSmall();
```

*GitHub* : [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)

### [N-34]<a name="n-34"></a> Missing NatSpec `@dev` from error declaration

Some errors have an incomplete NatSpec: add a `@dev` notation to describe the error to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
90	  error UnwrapTooSmall();
```

*GitHub* : [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)

### [N-35]<a name="n-35"></a> Missing NatSpec `@notice` from error declaration

Some errors have an incomplete NatSpec: add a `@notice` notation to describe the error to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
90	  error UnwrapTooSmall();
```

*GitHub* : [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)

### [N-36]<a name="n-36"></a> Missing NatSpec `@param` from error declaration

Some errors have an incomplete NatSpec: add a `@param` notation to describe the error parameters to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
90	  error UnwrapTooSmall();
```

*GitHub* : [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)

### [N-37]<a name="n-37"></a> Missing NatSpec `@dev` from event declaration

Some events have an incomplete NatSpec: add a `@dev` notation to describe the event to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
155	  /**
156	   * @notice Emitted when the oracle address is set
157	   *
158	   * @param oldOracle The address of the old oracle
159	   * @param newOracle The address of the new oracle
160	   */
161	  event OracleSet(address indexed oldOracle, address indexed newOracle);
```

*GitHub* : [155..161](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L155-L161)

### [N-38]<a name="n-38"></a> Missing NatSpec `@notice` from event declaration

Some events have an incomplete NatSpec: add a `@notice` notation to describe the event to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
134	  /**
135	   * @dev Event emitted when upgradable rOUSG is deployed
136	   *
137	   * @param proxy             The address for the proxy contract
138	   * @param proxyAdmin        The address for the proxy admin contract
139	   * @param implementation    The address for the implementation contract
140	   */
141	  event rOUSGDeployed(
```

*GitHub* : [134..141](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L134-L141)

### [N-39]<a name="n-39"></a> Missing NatSpec `@param` from event declaration

Some events have an incomplete NatSpec: add a `@param` notation to describe the event to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
144	  /**
145	   * @notice An executed shares transfer from `sender` to `recipient`.
146	   *
147	   * @dev emitted in pair with an ERC20-defined `Transfer` event.
148	   */
149	  event TransferShares(
```

*GitHub* : [144..149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L144-L149)

### [N-40]<a name="n-40"></a> Missing NatSpec from modifiers definitions

Consider adding some comments on modifier declarations to explain what they are supposed to do: this will help for future code reviews.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
149	  modifier onlyGuardian() {
```

*GitHub* : [149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149)

### [N-41]<a name="n-41"></a> Missing NatSpec `@dev` from modifier declaration

Some modifiers have an incomplete NatSpec: add a `@dev` notation to describe the modifier to improve the code documentation.

*There are 3 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
755	  /// @notice Ensure that the mint functionality is not paused
756	  modifier whenMintNotPaused() {
...
761	  /// @notice Ensure that the redeem functionality is not paused
762	  modifier whenRedeemNotPaused() {
```

*GitHub* : [755..756](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L755-L756), [761..762](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L761-L762)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
149	  modifier onlyGuardian() {
```

*GitHub* : [149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149)

### [N-42]<a name="n-42"></a> Missing NatSpec `@notice` from modifier declaration

Some modifiers have an incomplete NatSpec: add a `@notice` notation to describe the modifier to improve the code documentation.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
149	  modifier onlyGuardian() {
```

*GitHub* : [149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149)

### [N-43]<a name="n-43"></a> Missing NatSpec `@param` from modifier declaration

Some modifiers have an incomplete NatSpec: add a `@param` notation to describe the modifier parameters to improve the code documentation.

*There are 3 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
755	  /// @notice Ensure that the mint functionality is not paused
756	  modifier whenMintNotPaused() {
...
761	  /// @notice Ensure that the redeem functionality is not paused
762	  modifier whenRedeemNotPaused() {
```

*GitHub* : [755..756](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L755-L756), [761..762](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L761-L762)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
149	  modifier onlyGuardian() {
```

*GitHub* : [149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149)

### [N-44]<a name="n-44"></a> Missing NatSpec `@dev` from function declaration

Some functions have an incomplete NatSpec: add a `@dev` notation to describe the function to improve the code documentation.

*There are 48 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
278	  function _mint(
279	    uint256 usdcAmountIn,
280	    address to
281	  ) internal returns (uint256 ousgAmountOut) {
...
388	  function _redeem(
389	    uint256 ousgAmountIn
390	  ) internal returns (uint256 usdcAmountOut) {
...
458	  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
...
490	  /**
491	   * @notice Set the mintLimit constraint inside the InstantMintTimeBasedRateLimiter
492	   *         base contract
493	   *
494	   * @param _instantMintLimit New limit that dicates how much USDC can be transfered
495	   *                     for minting in a specified duration
496	   *                     (in 6 decimals per the USDC contract)
497	   */
498	  function setInstantMintLimit(
499	    uint256 _instantMintLimit
500	  ) external override onlyRole(CONFIGURER_ROLE) {
...
504	  /**
505	   * @notice Set the redeemLimit constraint inside the InstantMintTimeBasedRateLimiter
506	   *         base contract
507	   *
508	   * @param _instantRedemptionLimit New limit that dicates how much USDC
509	   *                       can be redeemed in a specified duration
510	   *                       (in 6 decimals per the USDC contract)
511	   */
512	  function setInstantRedemptionLimit(
513	    uint256 _instantRedemptionLimit
514	  ) external override onlyRole(CONFIGURER_ROLE) {
...
518	  /**
519	   * @notice Sets mintLimitDuration constraint inside the InstantMintTimeBasedRateLimiter
520	   *         base contract
521	   *
522	   * @param _instantMintLimitDuration New limit that specifies the interval
523	   *                             (in seconds) in which only `mintLimit` USDC
524	   *                             can be used for minting within
525	   */
526	  function setInstantMintLimitDuration(
527	    uint256 _instantMintLimitDuration
528	  ) external override onlyRole(CONFIGURER_ROLE) {
...
532	  /**
533	   * @notice Sets redeemLimitDuration inside the InstantMintTimeBasedRateLimiter
534	   *         base contract
535	   *
536	   * @param _instantRedemptionLimitDuratioin New limit that specifies the interval
537	   *                               (in seconds) in which only `redeemLimit` USDC
538	   *                               can be redeemed within
539	   */
540	  function setInstantRedemptionLimitDuration(
541	    uint256 _instantRedemptionLimitDuratioin
542	  ) external override onlyRole(CONFIGURER_ROLE) {
...
549	  /**
550	   * @notice Sets the mint fee
551	   *
552	   * @param _mintFee new mint fee specified in basis points
553	   */
554	  function setMintFee(
555	    uint256 _mintFee
556	  ) external override onlyRole(CONFIGURER_ROLE) {
...
562	  /**
563	   * @notice Sets the redeem fee.
564	   *
565	   * @param _redeemFee new redeem fee specified in basis points
566	   */
567	  function setRedeemFee(
568	    uint256 _redeemFee
569	  ) external override onlyRole(CONFIGURER_ROLE) {
...
575	  /**
576	   * @notice Admin function to set the minimum amount required for a deposit
577	   *
578	   * @param _minimumDepositAmount The minimum amount required to submit a deposit
579	   *                          request
580	   */
581	  function setMinimumDepositAmount(
582	    uint256 _minimumDepositAmount
583	  ) external override onlyRole(CONFIGURER_ROLE) {
```

*GitHub* : [278..281](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278-L281), [388..390](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388-L390), [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458), [490..500](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L490-L500), [504..514](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L504-L514), [518..528](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L518-L528), [532..542](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L532-L542), [549..556](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L549-L556), [562..569](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L562-L569), [575..583](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L575-L583), [593..601](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L593-L601), [617..624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L617-L624), [632..640](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L632-L640), [645..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L645-L652), [658..665](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L658-L665), [679..688](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L679-L688), [693..702](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L693-L702), [707..715](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L707-L715), [719..727](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L719-L727), [767..768](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L767-L768), [773..774](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L773-L774), [779..780](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L779-L780), [785..786](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L785-L786), [794..802](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802), [813..823](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L813-L823)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [97..98](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L97-L98), [102..108](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108), [112..118](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112-L118), [128..134](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128-L134), [163..166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L163-L166), [170..174](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L170-L174), [178..181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L178-L181), [185..188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L185-L188), [289..305](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L289-L305), [314..331](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L314-L331), [360..365](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L360-L365), [370..373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L370-L373), [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378), [445..454](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L445-L454), [461..476](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L461-L476), [484..487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L484-L487), [491..505](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L491-L505), [521..532](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L521-L532), [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642), [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646), [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656..658](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)

### [N-45]<a name="n-45"></a> Missing NatSpec `@notice` from function declaration

Some functions have an incomplete NatSpec: add a `@notice` notation to describe the function to improve the code documentation.

*There are 26 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
278	  function _mint(
279	    uint256 usdcAmountIn,
280	    address to
281	  ) internal returns (uint256 ousgAmountOut) {
...
388	  function _redeem(
389	    uint256 ousgAmountIn
390	  ) internal returns (uint256 usdcAmountOut) {
...
458	  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
...
794	  function multiexcall(
795	    ExCallData[] calldata exCallData
796	  )
797	    external
798	    payable
799	    override
800	    onlyRole(DEFAULT_ADMIN_ROLE)
801	    returns (bytes[] memory results)
802	  {
```

*GitHub* : [278..281](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278-L281), [388..390](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388-L390), [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458), [794..802](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)


---

	 - contracts/ousg/rOUSG.sol

```solidity
97	  /// @custom:oz-upgrades-unsafe-allow constructor
98	  constructor() {
...
102	  function initialize(
103	    address _kycRegistry,
104	    uint256 requirementGroup,
105	    address _ousg,
106	    address guardian,
107	    address _oracle
108	  ) public virtual initializer {
...
112	  function __rOUSG_init(
113	    address _kycRegistry,
114	    uint256 requirementGroup,
115	    address _ousg,
116	    address guardian,
117	    address _oracle
118	  ) internal onlyInitializing {
...
128	  function __rOUSG_init_unchained(
129	    address _kycRegistry,
130	    uint256 _requirementGroup,
131	    address _ousg,
132	    address guardian,
133	    address _oracle
134	  ) internal onlyInitializing {
...
163	  /**
164	   * @return the name of the token.
165	   */
166	  function name() public pure returns (string memory) {
...
170	  /**
171	   * @return the symbol of the token, usually a shorter version of the
172	   * name.
173	   */
174	  function symbol() public pure returns (string memory) {
```

*GitHub* : [97..98](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L97-L98), [102..108](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108), [112..118](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112-L118), [128..134](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128-L134), [163..166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L163-L166), [170..174](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L170-L174), [178..181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L178-L181), [185..188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L185-L188), [193..199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L193-L199), [225..234](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L225-L234), [341..347](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L341-L347), [351..356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L351-L356), [360..365](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L360-L365), [370..373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L370-L373), [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378), [484..487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L484-L487), [572..590](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L572-L590), [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642), [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646), [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656..658](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)

### [N-46]<a name="n-46"></a> Simplify complex require statements

Simplifying complex `require` statements with local variables and `if`(or `revert`) statements can improve readability, make debugging easier, and promote modularity and reusability in the code.

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
466	    require(
467	      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
468	      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
469	    );
```

*GitHub* : [466..469](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L466-L469)

### [N-47]<a name="n-47"></a> Events should be emitted before external calls

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls

*There are 14 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @audit functions: `approve`, `wrap`, `getROUSGByShares`, `transfer` called before this event
270	    emit InstantMintRebasingOUSG(
271	      msg.sender,
272	      usdcAmountIn,
273	      ousgAmountOut,
274	      rousgAmountOut
275	    );
...
// @audit functions: `decimals`, `checkAndUpdateMintLimit`, `allowance`, `transferFrom`, `transferFrom` called before this event
321	    emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);
...
// @audit functions: `allowance`, `transferFrom` called before this event
350	    emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut);
...
// @audit functions: `allowance`, `transferFrom`, `unwrap`, `getSharesByROUSG` called before this event
380	    emit InstantRedemptionRebasingOUSG(
381	      msg.sender,
382	      rousgAmountIn,
383	      ousgAmountIn,
384	      usdcAmountOut
385	    );
...
// @audit functions: `decimals`, `decimals`, `checkAndUpdateRedeemLimit`, `burn`, `balanceOf` called before this event
443	      emit BUIDLRedemptionSkipped(
444	        msg.sender,
445	        usdcAmountToRedeem,
446	        usdcBalance - usdcAmountToRedeem
447	      );
...
// @audit functions: `decimals`, `decimals`, `checkAndUpdateRedeemLimit`, `burn`, `balanceOf` called before this event
435	      emit MinimumBUIDLRedemption(
436	        msg.sender,
437	        minBUIDLRedeemAmount,
438	        usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
439	      );
...
// @audit functions: `decimals`, `decimals`, `checkAndUpdateRedeemLimit`, `burn`, `balanceOf`, `transfer` called before this event
453	    emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);
```

*GitHub* : [270..275](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L270-L275), [321](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L321), [350](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L350), [380..385](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L380-L385), [443..447](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L443-L447), [435..439](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L435-L439), [453](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L453)


---

	 - contracts/ousg/rOUSG.sol

```solidity
// @audit functions: `transferFrom` called before this event
420	    emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
...
// @audit functions: `transferFrom` called before this event
421	    emit TransferShares(address(0), msg.sender, ousgSharesAmount);
...
// @audit functions: `transfer` called before this event
441	    emit Transfer(msg.sender, address(0), _rOUSGAmount);
```

*GitHub* : [420](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L420), [421](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L421), [441](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L441), [442](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L442), [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L638), [639](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L639)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [96..102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L96-L102)

### [N-48]<a name="n-48"></a> Use `@inheritdoc` for overridden functions

It is recommended to use `@inheritdoc` for overridden functions.

*There are 20 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
219	  /**
220	   * @notice Calculates fees and triggers minting OUSG for a given amount of USDC
221	   *
222	   * @dev Please note that the fees are accumulated in `feeReceiver`
223	   *
224	   * @param usdcAmountIn amount of USDC exchanged for OUSG (in whatever decimals
225	   *                     specifed by usdc token contract)
226	   *
227	   * @return ousgAmountOut The quantity of OUSG minted for the user
228	   *                       (18 decimals per OUSG contract)
229	   */
230	  function mint(
231	    uint256 usdcAmountIn
232	  )
233	    external
234	    override
235	    nonReentrant
236	    whenMintNotPaused
237	    returns (uint256 ousgAmountOut)
238	  {
...
243	  /**
244	   * @notice Calculates fees and triggers minting rOUSG for a given amount of USDC
245	   *
246	   * @dev Please note that the fees are accumulated in `feeReceiver`
247	   *
248	   * @param usdcAmountIn amount of USDC exchanged for rOUSG (in whatever decimals
249	   *                     specifed by usdc token contract)
250	   *
251	   * @return rousgAmountOut The quantity of rOUSG minted for the user
252	   *                        (18 decimals per rOUSG contract)
253	   */
254	  function mintRebasingOUSG(
255	    uint256 usdcAmountIn
256	  )
257	    external
258	    override
259	    nonReentrant
260	    whenMintNotPaused
261	    returns (uint256 rousgAmountOut)
262	  {
...
326	  /**
327	   * @notice Calculates fees and triggers a redemption of OUSG for a given amount of USDC
328	   *
329	   * @dev Please note that the fees are accumulated in `feeReceiver`
330	   *
331	   * @param ousgAmountIn Amount of OUSG to redeem
332	   *
333	   * @return usdcAmountOut The amount of USDC returned to the user
334	   */
335	  function redeem(
336	    uint256 ousgAmountIn
337	  )
338	    external
339	    override
340	    nonReentrant
341	    whenRedeemNotPaused
342	    returns (uint256 usdcAmountOut)
343	  {
...
353	  /**
354	   * @notice Calculates fees and triggers minting rOUSG for a given amount of USDC
355	   *
356	   * @dev Please note that the fees are actually accumulated in `feeReceiver`
357	   *
358	   * @param rousgAmountIn Amount of rOUSG to redeem
359	   *
360	   * @return usdcAmountOut The amount of USDC returned to the user
361	   */
362	  function redeemRebasingOUSG(
363	    uint256 rousgAmountIn
364	  )
365	    external
366	    override
367	    nonReentrant
368	    whenRedeemNotPaused
369	    returns (uint256 usdcAmountOut)
370	  {
...
490	  /**
491	   * @notice Set the mintLimit constraint inside the InstantMintTimeBasedRateLimiter
492	   *         base contract
493	   *
494	   * @param _instantMintLimit New limit that dicates how much USDC can be transfered
495	   *                     for minting in a specified duration
496	   *                     (in 6 decimals per the USDC contract)
497	   */
498	  function setInstantMintLimit(
499	    uint256 _instantMintLimit
500	  ) external override onlyRole(CONFIGURER_ROLE) {
...
504	  /**
505	   * @notice Set the redeemLimit constraint inside the InstantMintTimeBasedRateLimiter
506	   *         base contract
507	   *
508	   * @param _instantRedemptionLimit New limit that dicates how much USDC
509	   *                       can be redeemed in a specified duration
510	   *                       (in 6 decimals per the USDC contract)
511	   */
512	  function setInstantRedemptionLimit(
513	    uint256 _instantRedemptionLimit
514	  ) external override onlyRole(CONFIGURER_ROLE) {
...
518	  /**
519	   * @notice Sets mintLimitDuration constraint inside the InstantMintTimeBasedRateLimiter
520	   *         base contract
521	   *
522	   * @param _instantMintLimitDuration New limit that specifies the interval
523	   *                             (in seconds) in which only `mintLimit` USDC
524	   *                             can be used for minting within
525	   */
526	  function setInstantMintLimitDuration(
527	    uint256 _instantMintLimitDuration
528	  ) external override onlyRole(CONFIGURER_ROLE) {
...
532	  /**
533	   * @notice Sets redeemLimitDuration inside the InstantMintTimeBasedRateLimiter
534	   *         base contract
535	   *
536	   * @param _instantRedemptionLimitDuratioin New limit that specifies the interval
537	   *                               (in seconds) in which only `redeemLimit` USDC
538	   *                               can be redeemed within
539	   */
540	  function setInstantRedemptionLimitDuration(
541	    uint256 _instantRedemptionLimitDuratioin
542	  ) external override onlyRole(CONFIGURER_ROLE) {
...
549	  /**
550	   * @notice Sets the mint fee
551	   *
552	   * @param _mintFee new mint fee specified in basis points
553	   */
554	  function setMintFee(
555	    uint256 _mintFee
556	  ) external override onlyRole(CONFIGURER_ROLE) {
...
562	  /**
563	   * @notice Sets the redeem fee.
564	   *
565	   * @param _redeemFee new redeem fee specified in basis points
566	   */
567	  function setRedeemFee(
568	    uint256 _redeemFee
569	  ) external override onlyRole(CONFIGURER_ROLE) {
```

*GitHub* : [219..238](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L219-L238), [243..262](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L243-L262), [326..343](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L326-L343), [353..370](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L353-L370), [490..500](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L490-L500), [504..514](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L504-L514), [518..528](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L518-L528), [532..542](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L532-L542), [549..556](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L549-L556), [562..569](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L562-L569), [575..583](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L575-L583), [593..601](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L593-L601), [617..624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L617-L624), [632..640](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L632-L640), [645..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L645-L652), [658..665](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L658-L665), [794..802](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [650..652](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656..658](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [110..123](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L110-L123)

### [N-49]<a name="n-49"></a> Missing NatSpec from variable declarations

Some variables miss a NatSpec, which should be a [best practice](https://docs.soliditylang.org/en/latest/natspec-format.html) to add as a documentation.

Even if Natspec for internal and private variables is not parsed (but this may change in the future, according to the official docs), it still helps while reviewing the codebase.

*There are 34 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
57	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
...
60	  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
...
63	  uint256 public constant MINIMUM_OUSG_PRICE = 105e18;
...
66	  uint256 public constant FEE_GRANULARITY = 10_000;
...
69	  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
...
72	  IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;
...
75	  IRWALike public immutable ousg;
...
78	  ROUSG public immutable rousg;
...
81	  IERC20 public immutable buidl;
...
84	  IBUIDLRedeemer public immutable buidlRedeemer;
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57), [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60), [63](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L63), [66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66), [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69), [72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72), [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L75), [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L78), [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L81), [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L84), [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L87), [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90), [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L93), [96](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L96), [99](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L99), [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L102), [106](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L106), [110](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L110), [113](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L113), [116](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L116), [120](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L120), [123](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L123)


---

	 - contracts/ousg/rOUSG.sol


*GitHub* : [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L78), [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L81), [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L84), [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87), [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94), [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)


---

	 - contracts/ousg/rOUSGFactory.sol


*GitHub* : [38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38), [40](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40), [41](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L41), [42](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L42), [43](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L43), [45](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45)

### [N-50]<a name="n-50"></a> Contract name does not follow the Solidity Style Guide

According to the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#contract-and-library-names), contracts and libraries should be named using the CapWords style.

*There are 3 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
49	contract OUSGInstantManager is
50	  ReentrancyGuard,
51	  InstantMintTimeBasedRateLimiter,
52	  AccessControlEnumerable,
53	  IOUSGInstantManager,
54	  IMulticall
55	{
56	  // Role to configure the contract
57	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```

*GitHub* : [49..57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49-L57)


---

	 - contracts/ousg/rOUSG.sol

```solidity
55	contract ROUSG is
56	  Initializable,
57	  ContextUpgradeable,
58	  PausableUpgradeable,
59	  AccessControlEnumerableUpgradeable,
60	  KYCRegistryClientUpgradeable,
61	  IERC20Upgradeable,
62	  IERC20MetadataUpgradeable
63	{
64	  /**
65	   * @dev rOUSG balances are dynamic and are calculated based on the accounts' shares (OUSG)
66	   * and the the price of OUSG. Account shares aren't
67	   * normalized, so the contract also stores the sum of all shares to calculate
68	   * each account's token balance which equals to:
69	   *
70	   *   shares[account] * ousgPrice
71	   */
72	  mapping(address => uint256) private shares;
```

*GitHub* : [55..72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55-L72)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
37	contract ROUSGFactory is IMulticall {
38	  bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

*GitHub* : [37..38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37-L38)

### [N-51]<a name="n-51"></a> Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (UPPER_CASE_WITH_UNDERSCORES)

*There are 8 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
72	  IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;
...
75	  IRWALike public immutable ousg;
...
78	  ROUSG public immutable rousg;
...
81	  IERC20 public immutable buidl;
...
84	  IBUIDLRedeemer public immutable buidlRedeemer;
...
87	  uint256 public immutable decimalsMultiplier;
...
90	  address public immutable usdcReceiver;
```

*GitHub* : [72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72), [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L75), [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L78), [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L81), [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L84), [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L87), [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
40	  address internal immutable guardian;
```

*GitHub* : [40](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40)

### [N-52]<a name="n-52"></a> Use a single file for system wide constants

Consider grouping all the system constants under a single file.

*There are 10 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
57	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
...
60	  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
...
63	  uint256 public constant MINIMUM_OUSG_PRICE = 105e18;
...
66	  uint256 public constant FEE_GRANULARITY = 10_000;
...
69	  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57), [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60), [63](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L63), [66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66), [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69)


---

	 - contracts/ousg/rOUSG.sol

```solidity
87	  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
...
93	  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
...
94	  bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
...
95	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```

*GitHub* : [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87), [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L93), [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94), [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
38	  bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

*GitHub* : [38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38)

### [N-53]<a name="n-53"></a> Contracts should have full test coverage

A 100% test coverage is not foolproof, but it helps immensely in reducing the amount of bugs that may occur.

*There are 1 instance(s) of this issue:*

*GitHub* : [project\2024-03-ondo-finance](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/#L0)

### [N-54]<a name="n-54"></a> Large or complicated code bases should implement invariant tests

This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts.

Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold.

Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.

*There are 1 instance(s) of this issue:*

*GitHub* : [project\2024-03-ondo-finance](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/#L0)

### [N-55]<a name="n-55"></a> Codebase should implement formal verification testing

Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.

Some tools that are currently available to perform these tests on smart contracts are [SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html) and [Certora Prover](https://www.certora.com/).

*There are 1 instance(s) of this issue:*

*GitHub* : [project\2024-03-ondo-finance](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/#L0)

### [N-56]<a name="n-56"></a> State variables not capped at reasonable values

Consider adding minimum/maximum value checks to ensure that the state variables below can never be used to excessively harm users, including via griefing

*There are 1 instance(s) of this issue:*


---

	 - contracts/ousg/rOUSG.sol

```solidity
// @audit: parameter `_amount` is not limited in function body
626	    uint256 _amount
```

*GitHub* : [626](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L626)

### [N-57]<a name="n-57"></a> Consider adding a block/deny-list

Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens

*There are 3 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
49	contract OUSGInstantManager is
50	  ReentrancyGuard,
51	  InstantMintTimeBasedRateLimiter,
52	  AccessControlEnumerable,
53	  IOUSGInstantManager,
54	  IMulticall
55	{
56	  // Role to configure the contract
57	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```

*GitHub* : [49..57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49-L57)


---

	 - contracts/ousg/rOUSG.sol

```solidity
55	contract ROUSG is
56	  Initializable,
57	  ContextUpgradeable,
58	  PausableUpgradeable,
59	  AccessControlEnumerableUpgradeable,
60	  KYCRegistryClientUpgradeable,
61	  IERC20Upgradeable,
62	  IERC20MetadataUpgradeable
63	{
64	  /**
65	   * @dev rOUSG balances are dynamic and are calculated based on the accounts' shares (OUSG)
66	   * and the the price of OUSG. Account shares aren't
67	   * normalized, so the contract also stores the sum of all shares to calculate
68	   * each account's token balance which equals to:
69	   *
70	   *   shares[account] * ousgPrice
71	   */
72	  mapping(address => uint256) private shares;
```

*GitHub* : [55..72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55-L72)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
37	contract ROUSGFactory is IMulticall {
38	  bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

*GitHub* : [37..38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37-L38)

### [N-58]<a name="n-58"></a> Expressions for constant values should use `immutable` rather than `constant`

While it does not save gas for some simple binary expressions because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between `constant` variables and `immutable` variables, and they should each be used in their appropriate contexts. `constants` should be used for literal values written into the code, and `immutable` variables should be used for expressions, or values calculated in, or passed into the constructor.

*There are 6 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
57	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
...
60	  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
```

*GitHub* : [57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57), [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60)


---

	 - contracts/ousg/rOUSG.sol

```solidity
93	  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
...
94	  bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
...
95	  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```

*GitHub* : [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L93), [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94), [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
38	  bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

*GitHub* : [38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38)

### [N-59]<a name="n-59"></a> Lines are too long

Maximum suggested line length is 120 characters according to the [documentation](https://docs.soliditylang.org/en/latest/style-guide.html#maximum-line-length).

*There are 15 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
6	 ██ ,██¬ ▄████▄  ▀█▄ ╙█▄      ▄███▀▀███▄   ███▄    ██  ███▀▀▀███▄    ▄███▀▀███,
...
7	██  ██ ╒█▀'   ╙█▌ ╙█▌ ██     ▐██      ███  █████,  ██  ██▌    └██▌  ██▌     └██▌
...
8	██ ▐█▌ ██      ╟█  █▌ ╟█     ██▌      ▐██  ██ └███ ██  ██▌     ╟██ j██       ╟██
...
9	╟█  ██ ╙██    ▄█▀ ▐█▌ ██     ╙██      ██▌  ██   ╙████  ██▌    ▄██▀  ██▌     ,██▀
...
10	 ██ "██, ╙▀▀███████████⌐      ╙████████▀   ██     ╙██  ███████▀▀     ╙███████▀`
```

*GitHub* : [6](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L6), [7](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L7), [8](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L8), [9](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L9), [10](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L10)


---

	 - contracts/ousg/rOUSG.sol

```solidity
6	 ██ ,██¬ ▄████▄  ▀█▄ ╙█▄      ▄███▀▀███▄   ███▄    ██  ███▀▀▀███▄    ▄███▀▀███,
...
7	██  ██ ╒█▀'   ╙█▌ ╙█▌ ██     ▐██      ███  █████,  ██  ██▌    └██▌  ██▌     └██▌
...
8	██ ▐█▌ ██      ╟█  █▌ ╟█     ██▌      ▐██  ██ └███ ██  ██▌     ╟██ j██       ╟██
...
9	╟█  ██ ╙██    ▄█▀ ▐█▌ ██     ╙██      ██▌  ██   ╙████  ██▌    ▄██▀  ██▌     ,██▀
...
10	 ██ "██, ╙▀▀███████████⌐      ╙████████▀   ██     ╙██  ███████▀▀     ╙███████▀`
```

*GitHub* : [6](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L6), [7](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L7), [8](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L8), [9](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L9), [10](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L10)


---

	 - contracts/ousg/rOUSGFactory.sol

```solidity
6	 ██ ,██¬ ▄████▄  ▀█▄ ╙█▄      ▄███▀▀███▄   ███▄    ██  ███▀▀▀███▄    ▄███▀▀███,
...
7	██  ██ ╒█▀'   ╙█▌ ╙█▌ ██     ▐██      ███  █████,  ██  ██▌    └██▌  ██▌     └██▌
...
8	██ ▐█▌ ██      ╟█  █▌ ╟█     ██▌      ▐██  ██ └███ ██  ██▌     ╟██ j██       ╟██
...
9	╟█  ██ ╙██    ▄█▀ ▐█▌ ██     ╙██      ██▌  ██   ╙████  ██▌    ▄██▀  ██▌     ,██▀
...
10	 ██ "██, ╙▀▀███████████⌐      ╙████████▀   ██     ╙██  ███████▀▀     ╙███████▀`
```

*GitHub* : [6](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L6), [7](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L7), [8](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L8), [9](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L9), [10](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L10)

### [N-60]<a name="n-60"></a> Typos



*There are 1 instance(s) of this issue:*

```bash
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:42:32
   |
42 |  *      OUSG, rOUSG, USDC, and BUIDL. This contract multiplies
   |                                ^^^^^
   |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:80:6
   |
80 |   // BUIDL token contract
   |      ^^^^^
   |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:81:27
   |
81 |   IERC20 public immutable buidl;
   |                           ^^^^^
   |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:83:56
   |
83 |   // Redeemer contract used for instant redemptions of BUIDL
   |                                                        ^^^^^
   |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:84:35
   |
84 |   IBUIDLRedeemer public immutable buidlRedeemer;
   |                                   ^^^^^
   |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:118:28
    |
118 |   // The minimum amount of BUIDL that must be redeemed in a single redemption
    |                            ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:119:15
    |
119 |   // with the BUIDLRedeemer contract
    |               ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:120:21
    |
120 |   uint256 public minBUIDLRedeemAmount = 250_000e6;
    |                     ^^^^^
    |
error: `Reciever` should be `Receiver`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:130:18
    |
130 |    * @param _usdcReciever       Address that receives USDC during minting
    |                  ^^^^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:135:14
    |
135 |    * @param _buidl              BUIDL token contract address
    |              ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:135:33
    |
135 |    * @param _buidl              BUIDL token contract address
    |                                 ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:136:14
    |
136 |    * @param _buidlRedeemer      Contract address used for instant redemptions of BUIDL
    |              ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:136:82
    |
136 |    * @param _buidlRedeemer      Contract address used for instant redemptions of BUIDL
    |                                                                                  ^^^^^
    |
error: `Reciever` should be `Receiver`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:147:18
    |
147 |     address _usdcReciever,
    |                  ^^^^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:152:14
    |
152 |     address _buidl,
    |              ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:153:14
    |
153 |     address _buidlRedeemer,
    |              ^^^^^
    |
error: `Reciever` should be `Receiver`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:168:20
    |
168 |       address(_usdcReciever) != address(0),
    |                    ^^^^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:181:14
    |
181 |     require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
    |              ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:181:56
    |
181 |     require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
    |                                                        ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:183:16
    |
183 |       address(_buidlRedeemer) != address(0),
    |                ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:184:28
    |
184 |       "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    |                            ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:191:59
    |
191 |       IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
    |                                                           ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:192:59
    |
192 |       "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    |                                                           ^^^^^
    |
error: `Reciever` should be `Receiver`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:195:25
    |
195 |     usdcReceiver = _usdcReciever;
    |                         ^^^^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:200:5
    |
200 |     buidl = IERC20(_buidl);
    |     ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:200:21
    |
200 |     buidl = IERC20(_buidl);
    |                     ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:201:5
    |
201 |     buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
    |     ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:201:37
    |
201 |     buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
    |                                     ^^^^^
    |
error: `specifed` should be `specified`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:225:26
    |
225 |    *                     specifed by usdc token contract)
    |                          ^^^^^^^^
    |
error: `specifed` should be `specified`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:249:26
    |
249 |    *                     specifed by usdc token contract)
    |                          ^^^^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:396:30
    |
396 |       IERC20Metadata(address(buidl)).decimals() == 6,
    |                              ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:397:37
    |
397 |       "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    |                                     ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:426:34
    |
426 |     if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
    |                                  ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:427:43
    |
427 |       // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
    |                                           ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:427:67
    |
427 |       // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
    |                                                                   ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:429:14
    |
429 |       _redeemBUIDL(usdcAmountToRedeem);
    |              ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:432:26
    |
432 |       // so we perform a BUIDL redemption of BUIDL's minimum required amount.
    |                          ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:432:46
    |
432 |       // so we perform a BUIDL redemption of BUIDL's minimum required amount.
    |                                              ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:434:14
    |
434 |       _redeemBUIDL(minBUIDLRedeemAmount);
    |              ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:434:23
    |
434 |       _redeemBUIDL(minBUIDLRedeemAmount);
    |                       ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:435:19
    |
435 |       emit MinimumBUIDLRedemption(
    |                   ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:437:12
    |
437 |         minBUIDLRedeemAmount,
    |            ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:438:26
    |
438 |         usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
    |                          ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:442:66
    |
442 |       // to cover the redemption and fees without redeeming more BUIDL.
    |                                                                  ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:443:12
    |
443 |       emit BUIDLRedemptionSkipped(
    |            ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:458:19
    |
458 |   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    |                   ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:458:33
    |
458 |   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    |                                 ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:460:7
    |
460 |       buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
    |       ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:460:44
    |
460 |       buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
    |                                            ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:461:35
    |
461 |       "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    |                                   ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:461:55
    |
461 |       "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    |                                                       ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:464:5
    |
464 |     buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
    |     ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:464:27
    |
464 |     buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
    |                           ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:464:43
    |
464 |     buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
    |                                           ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:465:5
    |
465 |     buidlRedeemer.redeem(buidlAmountToRedeem);
    |     ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:465:26
    |
465 |     buidlRedeemer.redeem(buidlAmountToRedeem);
    |                          ^^^^^
    |
error: `buidl` should be `build`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:467:60
    |
467 |       usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
    |                                                            ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:468:35
    |
468 |       "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    |                                   ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:468:42
    |
468 |       "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    |                                          ^^^^^
    |
error: `dicates` should be `dictates`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:494:46
    |
494 |    * @param _instantMintLimit New limit that dicates how much USDC can be transfered
    |                                              ^^^^^^^
    |
error: `transfered` should be `transferred`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:494:75
    |
494 |    * @param _instantMintLimit New limit that dicates how much USDC can be transfered
    |                                                                           ^^^^^^^^^^
    |
error: `dicates` should be `dictates`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:508:52
    |
508 |    * @param _instantRedemptionLimit New limit that dicates how much USDC
    |                                                    ^^^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:618:74
    |
618 |    * @notice Admin function to set the minimum amount required to redeem BUIDL
    |                                                                          ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:620:21
    |
620 |    * @param _minimumBUIDLRedemptionAmount The minimum amount required to redeem BUIDL
    |                     ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:620:81
    |
620 |    * @param _minimumBUIDLRedemptionAmount The minimum amount required to redeem BUIDL
    |                                                                                 ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:622:22
    |
622 |   function setMinimumBUIDLRedemptionAmount(
    |                      ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:623:21
    |
623 |     uint256 _minimumBUIDLRedemptionAmount
    |                     ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:625:17
    |
625 |     emit MinimumBUIDLRedemptionAmountSet(
    |                 ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:626:10
    |
626 |       minBUIDLRedeemAmount,
    |          ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:627:15
    |
627 |       _minimumBUIDLRedemptionAmount
    |               ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:629:8
    |
629 |     minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
    |        ^^^^^
    |
error: `BUIDL` should be `BUILD`
  --> project\2024-03-ondo-finance\contracts\ousg\ousgInstantManager.sol:629:36
    |
629 |     minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
    |                                    ^^^^^
    |

```

*GitHub* : [1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L1)




proof: 
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/README.md?plain=1#L113-L114


*There are 4 instance(s) of this issue:*


---

	 - contracts/ousg/ousgInstantManager.sol

```solidity
// @proof: https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/README.md?plain=1#L113-L114
// @context 
317	      usdc.transferFrom(msg.sender, feeReceiver, usdcfees);
...
// @proof: https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/README.md?plain=1#L113-L114
// @context 
319	    usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
...
// @proof: https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/README.md?plain=1#L113-L114
// @context 
348	    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
```

*GitHub* : [317](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L317), [319](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L319), [348](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L348)


---

	 - contracts/ousg/rOUSG.sol

```solidity
// @proof: https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/README.md?plain=1#L113-L114
// @context 
419	    ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
```

*GitHub* : [419](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L419)