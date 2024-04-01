
### Return values of `transfer()`/`transferFrom()` not checked
Not all `ERC20` implementations `revert()` when there's a failure in `transfer()` or `transferFrom()`. The function signature has a boolean return value and they indicate errors that way instead. By not checking the return value, operations that should have marked as failed, may potentially go through without actually transfer anything.

```solidity
Path: ./contracts/ousg/rOUSG.sol

419:    ousg.transferFrom(msg.sender, address(this), _OUSGAmount);	// @audit-issue

437:    ousg.transfer(	// @audit-issue

634:    ousg.transfer(	// @audit-issue
```
[419](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L419-L419), [437](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L437-L437), [634](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L634-L634), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

269:    rousg.transfer(msg.sender, rousgAmountOut);	// @audit-issue

317:      usdc.transferFrom(msg.sender, feeReceiver, usdcfees);	// @audit-issue

319:    usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);	// @audit-issue

348:    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);	// @audit-issue

375:    rousg.transferFrom(msg.sender, address(this), rousgAmountIn);	// @audit-issue

451:      usdc.transfer(feeReceiver, usdcFees);	// @audit-issue

455:    usdc.transfer(msg.sender, usdcAmountOut);	// @audit-issue

824:    IERC20(token).transfer(to, amount);	// @audit-issue
```
[269](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L269-L269), [317](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L317-L317), [319](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L319-L319), [348](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L348-L348), [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L375-L375), [451](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L451-L451), [455](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L455-L455), [824](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L824-L824), 


#### Recommendation

To ensure the reliability and security of token transfers in your smart contract, it's crucial to check the return values of the `transfer()` and `transferFrom()` functions. These functions often return a boolean value indicating the success or failure of the transfer operation. By checking this return value, you can accurately determine whether the transfer was successful and handle any potential errors or failures accordingly. Failing to check the return value may lead to unintended and unhandled transfer failures, which could 
have security and usability implications.


### `decimals()` is not a part of the `ERC-20` standard
The `decimals()` function is not a part of the [ERC-20](https://eips.ethereum.org/EIPS/eip-20) standard, and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid `ERC20` tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

187:      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),	// @audit-issue

191:      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),	// @audit-issue

204:        (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());	// @audit-issue

283:      IERC20Metadata(address(usdc)).decimals() == 6,	// @audit-issue

392:      IERC20Metadata(address(usdc)).decimals() == 6,	// @audit-issue

396:      IERC20Metadata(address(buidl)).decimals() == 6,	// @audit-issue
```
[187](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L187-L187), [191](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L191-L191), [204](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L204-L204), [283](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L283-L283), [392](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L392-L392), [396](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L396-L396), 


#### Recommendation

When working with ERC-20 tokens in your Solidity code, be aware that the `decimals()` function is not a part of the ERC-20 standard and is considered an optional extension. Not all valid ERC-20 tokens implement this interface, so avoid blindly casting all tokens to this interface and calling the `decimals()` function. Instead, check the token's documentation or contract to determine whether it supports this extension before using it.

### The Contract Should `approve(0)` First
Some tokens (like USDT L199) do not work when changing the allowance from an existing non-zero allowance value. They must first be approved by zero and then the actual allowance must be approved.

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

264:    ousg.approve(address(rousg), ousgAmountOut);	// @audit-issue

464:    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);	// @audit-issue
```
[264](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L264-L264), [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L464-L464), 


#### Recommendation

When developing functions that update allowances for ERC20 tokens, especially when interacting with tokens known to require this pattern, implement a two-step approval process. This process first sets the allowance for a spender to zero, and then sets it to the desired new value. For example:
```solidity
function resetAndApprove(address token, address spender, uint256 amount) public {
    IERC20(token).approve(spender, 0);
    IERC20(token).approve(spender, amount);
}
```


### `symbol()` is not a part of the `ERC-20` standard
The `symbol()` function is not a part of the [ERC-20](https://eips.ethereum.org/EIPS/eip-20) standard, and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid `ERC20` tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.


```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

101:      rOUSGProxied.symbol()	// @audit-issue
```
[101](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L101-L101), 


#### Recommendation

When working with ERC-20 tokens in your Solidity code, be aware that the `symbol()` function is not a part of the ERC-20 standard and is considered an optional extension. Not all valid ERC-20 tokens implement this interface, so avoid blindly casting all tokens to this interface and calling the `symbol()` function. Instead, check the token's documentation or contract to determine whether it supports this extension before using it.

### State variables not limited to reasonable values
Consider adding appropriate minimum/maximum value checks to ensure that the following state variables can never be used to excessively harm users, including via griefing.

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

629:    minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;	// @audit-issue
```
[629](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L629-L629), 


#### Recommendation


Implement validation checks for state variables to enforce minimum and maximum value limits. This can be achieved by adding modifiers or require statements in Solidity functions that modify these state variables. Ensure that these limits are reasonable and reflect the intended use of the contract. Additionally, consider implementing a mechanism to update these limits through a governance process or a trusted role, if applicable, to maintain flexibility and adaptability of the contract over time.



### Missing contract existence checks before low-level calls
Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `<address>.code.length > 0`.

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

126:      (bool success, bytes memory ret) = address(exCallData[i].target).call{	// @audit-issue
```
[126](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L126-L126), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

805:      (bool success, bytes memory ret) = address(exCallData[i].target).call{	// @audit-issue
```
[805](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L805-L805), 


#### Recommendation

To enhance the security and reliability of your Solidity smart contracts, always include contract existence checks before making low-level calls. In addition to verifying that the address is not the zero address, also confirm that `<address>.code.length > 0`. These checks help ensure that the target address corresponds to a valid and functioning contract, reducing the risk of unexpected behavior and vulnerabilities in your contract interactions.


### Use `increaseAllowance()`/`decreaseAllowance()` instead of `approve()`/`safeApprove()`
Changing an allowance with `approve()` brings the risk that someone may use both the old and the new allowance by unfortunate transaction ordering. [Refer to ERC20 API: An Attack Vector on the Approve/TransferFrom Methods](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit#heading=h.m9fhqynw2xvt). It is recommended to use the `increaseAllowance()`/`decreaseAllowance()` to avoid ths problem.

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

264:    ousg.approve(address(rousg), ousgAmountOut);	// @audit-issue

464:    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);	// @audit-issue
```
[264](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L264-L264), [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L464-L464), 


#### Recommendation

To enhance the security of your Solidity smart contracts and avoid potential issues related to transaction ordering, it is advisable to use the `increaseAllowance()` and `decreaseAllowance()` functions instead of `approve()` or `safeApprove()`. These functions provide a safer and more atomic way to modify allowances and mitigate the risk associated with potential attack vectors like those described in the [ERC20 API: An Attack Vector on the Approve/TransferFrom Methods](https://docs.google.com/document/d/1YLPtQxZu1UAvO9cZ1O2RPXBbT0mooh4DYKjA_jp-RLM/edit#heading=h.m9fhqynw2xvt) document.

### Vulnerable versions of packages are being used
This project is using specific package versions which are vulnerable to the specific CVEs listed below. Consider switching to more recent versions of these packages that don't have these vulnerabilities.


```solidity
Path: ./contracts/ousg/rOUSGFactory.sol
- [CVE-2023-40014](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-40014) - **MEDIUM** - (`openzeppelin/contracts >=4.0.0 <4.9.3`): OpenZeppelin Contracts is a library for secure smart contract development. Starting in version 4.0.0 and prior to version 4.9.3, contracts using `ERC2771Context` along with a custom trusted forwarder may see `_msgSender` return `address(0)` in calls that originate from the forwarder with calldata shorter than 20 bytes. This combination of circumstances does not appear to be common, in particular it is not the case for `MinimalForwarder` from OpenZeppelin Contracts, or any deployed forwarder the team is aware of, given that the signer address is appended to all calls that originate from these forwarders. The problem has been patched in v4.9.3.

```


#### Recommendation

Consider updating packages to safest version.

### Potential division by zero should have zero checks in place
In Solidity, division by zero is a critical issue that can lead to exceptions and disrupt the normal flow of a contract. It's essential to ensure that the divisor in any division operation is not zero before performing the operation. Failing to check for zero can result in transaction reversion or other unintended consequences. This is especially important in financial contracts or any contract where division operations are used to determine distributions, rewards, or similar calculations. Implementing checks to ensure the divisor is not zero before performing division enhances the robustness and reliability of the contract.

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

690:    ousgAmountOut = amountE36 / price;	// @audit-issue: Variable `price` not checked.
```
[690](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L690-L690), 


#### Recommendation

Before performing any division operation in Solidity, implement a check to ensure that the divisor is not zero. Use a `require()` statement or a similar assertion to validate the divisor. For example, use `require(divisor != 0, "Divisor cannot be zero");` before executing the division. This precaution prevents exceptions due to division by zero and ensures that your contract remains stable and predictable under all operational conditions. Regularly review your contract's logic to identify and safeguard against potential division by zero occurrences.


### Return values of `approve` not checked.
Not all `IERC20` implementations `revert` when there's a failure in `approve`. The function signature has a boolean return value and they indicate errors that way instead.

By not checking the return value, operations that should have marked as failed, may potentially go through without actually approving anything. 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

264:    ousg.approve(address(rousg), ousgAmountOut);	// @audit-issue

464:    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);	// @audit-issue
```
[264](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L264-L264), [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L464-L464), 


#### Recommendation

To ensure the accuracy of token approvals and prevent potential issues, it's important to check the return values when calling the `approve` function of an `IERC20` contract. While some implementations use a boolean return value to indicate errors, not checking this return value may allow operations to proceed without the intended approval. Always verify the return value to confirm the success of the approval operation.


### Unneeded initializations of bool variable to `false`.
In Solidity, it is common practice to initialize variables with default values when declaring them. However, initializing `bool`variables to `false` when they are not subsequently used in the code can lead to unnecessary gas consumption and code clutter. This issue points out instances where such initializations are present but serve no functional purpose.

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

45:  bool public initialized = false;	// @audit-issue
```
[45](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L45-L45), 


#### Recommendation


It is recommended not to initialize boolean variables to `false` to save some Gas.


### Unneeded initializations of integer variable to `0`.
In Solidity, it is common practice to initialize variables with default values when declaring them. However, initializing integer variables to `0` when they are not subsequently used in the code can lead to unnecessary gas consumption and code clutter. This issue points out instances where such initializations are present but serve no functional purpose.

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

125:    for (uint256 i = 0; i < exCallData.length; ++i) {	// @audit-issue
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L125-L125), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

99:  uint256 public mintFee = 0;	// @audit-issue

102:  uint256 public redeemFee = 0;	// @audit-issue

804:    for (uint256 i = 0; i < exCallData.length; ++i) {	// @audit-issue
```
[99](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L99-L99), [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L102-L102), [804](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L804-L804), 


#### Recommendation


It is recommended not to initialize integer variables to `0` to save some Gas.


### Use transfer libraries instead of low level calls
Consider using `SafeTransferLib.safeTransferETH` or `Address.sendValue` for clearer semantic meaning instead of using a low level call.

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

126:      (bool success, bytes memory ret) = address(exCallData[i].target).call{	// @audit-issue
```
[126](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L126-L126), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

805:      (bool success, bytes memory ret) = address(exCallData[i].target).call{	// @audit-issue
```
[805](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L805-L805), 


#### Recommendation

To improve code readability and safety, consider using higher-level transfer libraries like `SafeTransferLib.safeTransferETH` or `Address.sendValue` instead of low-level calls for handling Ether transfers. These libraries provide clearer semantic meaning and help prevent common pitfalls associated with low-level calls.


### Excessive Authorization in Contract Functions
A contract where a high percentage of functions require authorization (e.g., restricted to the contract owner or specific roles) may indicate over-centralization or excessive control. This could limit the contract's flexibility, reduce trust among users, and potentially create bottleneck points that could be exploited or become failure points. While some level of control is necessary for administrative purposes, overly restrictive access can detract from the decentralized nature of blockchain applications and concentrate too much power in the hands of a few.

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

37:contract ROUSGFactory is IMulticall {	// @audit-issue: %100.0 amount of external/public and non-view/non-pure functions are required authorization to call.
	List of total functions: `multiexcall`, `deployRebasingOUSG`
	List of functions that require authorization: `multiexcall`, `deployRebasingOUSG`
	List of functions that doesn't require authorization: None
```
[37](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L37-L37), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

49:contract OUSGInstantManager is	// @audit-issue: %81.81818181818183 amount of external/public and non-view/non-pure functions are required authorization to call.
	List of total functions: `setMinimumRedemptionAmount`, `setInvestorBasedRateLimiter`, `redeemRebasingOUSG`, `setInstantMintLimitDuration`, `setMinimumBUIDLRedemptionAmount`, `pauseMint`, `mint`, `setInstantRedemptionLimitDuration`, `unpauseMint`, `redeem`, `setInstantRedemptionLimit`, `setMintFee`, `setFeeReceiver`, `retrieveTokens`, `setMinimumDepositAmount`, `setRedeemFee`, `mintRebasingOUSG`, `pauseRedeem`, `unpauseRedeem`, `multiexcall`, `setOracle`, `setInstantMintLimit`
	List of functions that require authorization: `retrieveTokens`, `setMinimumDepositAmount`, `pauseMint`, `setRedeemFee`, `setMinimumRedemptionAmount`, `setInvestorBasedRateLimiter`, `setInstantMintLimitDuration`, `setFeeReceiver`, `pauseRedeem`, `setInstantRedemptionLimitDuration`, `unpauseMint`, `setOracle`, `setInstantRedemptionLimit`, `setMintFee`, `unpauseRedeem`, `multiexcall`, `setInstantMintLimit`, `setMinimumBUIDLRedemptionAmount`
	List of functions that doesn't require authorization: `mint`, `redeem`, `mintRebasingOUSG`, `redeemRebasingOUSG`
```
[49](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L49-L49), 


#### Recommendation

Make contract more decentralized.


### Custom error has no error details
Consider adding parameters to the error to indicate which user or values caused the failure

```solidity
Path: ./contracts/ousg/rOUSG.sol

90:  error UnwrapTooSmall();	// @audit-issue
```
[90](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L90-L90), 


#### Recommendation

When defining custom errors, consider adding parameters or error details that provide information about the specific conditions or inputs that caused the error. Including error details can make debugging and troubleshooting easier by providing context on the cause of the failure.



### Consider using `delete` rather than assigning values to `false`
The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic.


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

775:    mintPaused = false;	// @audit-issue

787:    redeemPaused = false;	// @audit-issue
```
[775](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L775-L775), [787](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L787-L787), 


#### Recommendation

Prefer using the `delete` keyword to reset state variables to their initial values instead of assigning `false` or other values, as it makes the intent clearer and helps with auditing.

### Event is not properly `indexed`
Index event fields make the field more quickly accessible [to off-chain tools](https://ethereum.stackexchange.com/questions/40396/can-somebody-please-explain-the-concept-of-event-indexing) that parse events. This is especially useful when it comes to filtering based on an address. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Where applicable, each `event` should use three `indexed` fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three applicable fields, all of the applicable fields should be `indexed`.

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

141:  event rOUSGDeployed(	// @audit-issue
142:    address proxy,
143:    address proxyAdmin,
144:    address implementation,
145:    string name,
146:    string ticker
147:  );
```
[141](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L141-L147), 


#### Recommendation

Enhance smart contract efficiency post-deployment by utilizing indexed events. This approach aids in efficiently tracking contract activities, significantly contributing to the reduction of gas costs.

### Avoid the use of sensitive terms
Use [alternative variants](https://www.zdnet.com/article/mysql-drops-master-slave-and-blacklist-whitelist-terminology/), e.g. allowlist/denylist instead of whitelist/blacklist.

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

475:   * @dev Sanity check: this function will revert if the price is unexpectedly low	// @audit-issue: Replace `sanity check` with `quick check`
```
[475](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L475-L475), 


#### Recommendation

To promote inclusive language and avoid insensitive terminology, consider using alternative terms such as 'allowlist' instead of 'whitelist' and 'denylist' instead of 'blacklist.' These alternatives help create a more welcoming and inclusive environment in code and documentation.