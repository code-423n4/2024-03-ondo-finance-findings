### Unnecessary Assert
Unnecessary `assert` statements in Solidity contracts can have several detrimental impacts on code readability, gas efficiency, and overall contract functionality. `assert` statements are typically used to check for conditions that should never occur under normal circumstances. While they can be valuable for catching unexpected errors and halting contract execution, their misuse can lead to unnecessary complexity and increased gas costs.


```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

94:    assert(rOUSGProxyAdmin.owner() == guardian);	// @audit-issue
```
[94](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L94-L94), 


#### Recommendation

Use 'assert' statements in Solidity judiciously, reserving them for conditions that indicate critical and unforeseen errors. Avoid overuse to maintain code clarity and prevent unnecessary gas consumption due to these costly checks.

### Cache Local Variable Array Length In For Loop
If not cached, the solidity compiler will always read the length of the array during each iteration. If it is a memory array, this is an extra mload operation (3 additional gas for each iteration except for the first).

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

125:    for (uint256 i = 0; i < exCallData.length; ++i) {	// @audit-issue
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L125-L125), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

804:    for (uint256 i = 0; i < exCallData.length; ++i) {	// @audit-issue
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L804-L804), 


#### Recommendation

To optimize gas consumption, cache the length of memory arrays before for loop iterations in Solidity. This reduces redundant mload operations, saving 3 gas per iteration after the first and improving overall contract efficiency.

### Another Constant With Same Value Is Already Defined
Defining multiple constants with the same value in a Solidity contract introduces unnecessary redundancy and can lead to confusion and potential errors in contract maintenance. Constants are used to define values that remain unchanged throughout the contract's lifecycle, enhancing readability and efficiency. However, when multiple constants representing the same value are defined, it not only clutters the code but also complicates the process of updating values and understanding the contract's logic. Consolidating these constants into a single definition improves code clarity and maintainability.

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

69:  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;	// @audit-issue: Same value `10_000` is already defined on line `66` as variable: `FEE_GRANULARITY`
```
[69](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L69-L69), 


#### Recommendation

Identify and consolidate duplicate constants in your Solidity contracts. Examine your contract's constants to find any with identical values and refactor your code to use a single constant definition for each unique value. This may involve choosing the most descriptive and appropriate name for the consolidated constant and updating all references accordingly. Such consolidation not only makes your contract more concise and easier to read but also simplifies future updates to constant values. Document the purpose and usage of each constant clearly, ensuring that the chosen names accurately reflect their role within the contract.

### Unnecessary casting as variable is already of the same type
In Solidity, explicitly casting a variable to a type that it already represents is redundant and can lead to confusion and clutter in the code. This unnecessary casting doesn't typically consume additional gas since Solidity's optimizer often removes such redundant conversions during compilation. However, it does affect code readability and may obscure the actual intent of the code, making it harder for developers to understand and maintain. Ensuring that casting is used only when necessary helps maintain clean, clear, and efficient code.

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

164:      address(_usdc) != address(0),	// @audit-issue: Variable `_usdc` is converted to `address` from type `address`.

168:      address(_usdcReciever) != address(0),	// @audit-issue: Variable `_usdcReciever` is converted to `address` from type `address`.

172:      address(_feeReceiver) != address(0),	// @audit-issue: Variable `_feeReceiver` is converted to `address` from type `address`.

176:      address(_ousgOracle) != address(0),	// @audit-issue: Variable `_ousgOracle` is converted to `address` from type `address`.

183:      address(_buidlRedeemer) != address(0),	// @audit-issue: Variable `_buidlRedeemer` is converted to `address` from type `address`.
```
[164](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L164-L164), [168](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L168-L168), [172](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L172-L172), [176](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L176-L176), [183](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L183-L183), 


#### Recommendation

Review your Solidity code for instances of unnecessary casting where variables are cast to their own type. Remove these redundant casts to enhance code clarity and maintainability. When writing new code, ensure that casting is only applied when changing a variable's type is genuinely needed. This practice helps in keeping the codebase straightforward and understandable, reducing potential confusion and errors associated with misinterpreting the variable types.


### `address(this)` should be cached
Cacheing saves gas when compared to repeating the calculation at each point it is used in the contract.

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

345:      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,	// @audit-issue: `adress(this)` also used on line(s): [348]

375:    rousg.transferFrom(msg.sender, address(this), rousgAmountIn);	// @audit-issue: `adress(this)` also used on line(s): [372]

463:    uint256 usdcBalanceBefore = usdc.balanceOf(address(this));	// @audit-issue: `adress(this)` also used on line(s): [467, 460]
```
[345](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L345-L345), [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L375-L375), [463](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L463-L463), 


#### Recommendation

To enhance gas efficiency, cache the contract's address by storing `address(this)` in a state variable at the point of contract deployment or initialization. Use this cached address throughout the contract instead of repeatedly calling `address(this)`. This practice reduces the gas cost associated with multiple computations of the contract's address, leading to more efficient contract execution, especially in scenarios with frequent usage of the contract's address.

### It is a waste of GAS to emit variable literals
Emitting variable literals (true, false, address(0), 1 etc...) in events is inefficient, as it consumes extra gas without providing added value. These literals are fixed values that can be accessed or hardcoded elsewhere in the smart contract or application, making their inclusion in events redundant and an unnecessary drain on resources during transaction execution.

```solidity
Path: ./contracts/ousg/rOUSG.sol

420:    emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));	// @audit-issue

421:    emit TransferShares(address(0), msg.sender, ousgSharesAmount);	// @audit-issue

441:    emit Transfer(msg.sender, address(0), _rOUSGAmount);	// @audit-issue

442:    emit TransferShares(msg.sender, address(0), ousgSharesAmount);	// @audit-issue

638:    emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));	// @audit-issue

639:    emit TransferShares(_account, address(0), ousgSharesAmount);	// @audit-issue
```
[420](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L420-L420), [421](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L421-L421), [441](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L441-L441), [442](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L442-L442), [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L638-L638), [639](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L639-L639), 


#### Recommendation

Refrain from including fixed variable literals as parameters in your Solidity contract events. Evaluate your event emissions and remove literals that do not provide dynamic information about contract state or actions. For instance, instead of emitting an event with a `true` literal to indicate success, consider naming the event in a way that inherently indicates success or failure, such as `ActionSuccessful()`:
```solidity
// Before optimization
event ActionTaken(bool success);

// After optimization
event ActionSuccessful();
event ActionFailed();
```


### Revert String Size Optimization
Shortening the revert strings to fit within 32 bytes will decrease deployment time and decrease runtime Gas when the revert condition is met.

Revert strings that are longer than 32 bytes require at least one additional `mstore`, along with additional overhead to calculate memory offset, etc.



```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

76:    require(!initialized, "ROUSGFactory: rOUSG already deployed");	// @audit-issue: String length is `36`

150:    require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");	// @audit-issue: String length is `38`
```
[76](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L76-L76), [150](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L150-L150), 


```solidity
Path: ./contracts/ousg/rOUSG.sol

282:    require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");	// @audit-issue: String length is `33`

416:    require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");	// @audit-issue: String length is `34`

432:    require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");	// @audit-issue: String length is `37`

594:      require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");	// @audit-issue: String length is `33`
```
[282](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L282-L282), [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L416-L416), [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L432-L432), [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L594-L594), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

163:    require(	// @audit-issue: String length is `38`
164:      address(_usdc) != address(0),
165:      "OUSGInstantManager: USDC cannot be 0x0"
166:    );

167:    require(	// @audit-issue: String length is `47`
168:      address(_usdcReciever) != address(0),
169:      "OUSGInstantManager: USDC Receiver cannot be 0x0"
170:    );

171:    require(	// @audit-issue: String length is `45`
172:      address(_feeReceiver) != address(0),
173:      "OUSGInstantManager: feeReceiver cannot be 0x0"
174:    );

175:    require(	// @audit-issue: String length is `45`
176:      address(_ousgOracle) != address(0),
177:      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
178:    );

179:    require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");	// @audit-issue: String length is `38`

180:    require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");	// @audit-issue: String length is `39`

181:    require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");	// @audit-issue: String length is `39`

182:    require(	// @audit-issue: String length is `48`
183:      address(_buidlRedeemer) != address(0),
184:      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
185:    );

186:    require(	// @audit-issue: String length is `64`
187:      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
188:      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
189:    );

190:    require(	// @audit-issue: String length is `65`
191:      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
192:      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
193:    );

205:    require(	// @audit-issue: String length is `76`
206:      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
207:        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
208:      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
209:    );

282:    require(	// @audit-issue: String length is `50`
283:      IERC20Metadata(address(usdc)).decimals() == 6,
284:      "OUSGInstantManager::_mint: USDC decimals must be 6"
285:    );

286:    require(	// @audit-issue: String length is `51`
287:      usdcAmountIn >= minimumDepositAmount,
288:      "OUSGInstantManager::_mint: Deposit amount too small"
289:    );

298:    require(	// @audit-issue: String length is `72`
299:      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
300:      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
301:    );

310:    require(	// @audit-issue: String length is `56`
311:      ousgAmountOut > 0,
312:      "OUSGInstantManager::_mint: net mint amount can't be zero"
313:    );

344:    require(	// @audit-issue: String length is `50`
345:      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
346:      "OUSGInstantManager::redeem: Insufficient allowance"
347:    );

371:    require(	// @audit-issue: String length is `62`
372:      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
373:      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
374:    );

391:    require(	// @audit-issue: String length is `52`
392:      IERC20Metadata(address(usdc)).decimals() == 6,
393:      "OUSGInstantManager::_redeem: USDC decimals must be 6"
394:    );

395:    require(	// @audit-issue: String length is `53`
396:      IERC20Metadata(address(buidl)).decimals() == 6,
397:      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
398:    );

402:    require(	// @audit-issue: String length is `56`
403:      usdcAmountToRedeem >= minimumRedemptionAmount,
404:      "OUSGInstantManager::_redeem: Redemption amount too small"
405:    );

417:    require(	// @audit-issue: String length is `56`
418:      usdcAmountOut > 0,
419:      "OUSGInstantManager::_redeem: redeem amount can't be zero"
420:    );

459:    require(	// @audit-issue: String length is `60`
460:      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
461:      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
462:    );

466:    require(	// @audit-issue: String length is `52`
467:      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
468:      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
469:    );

481:    require(	// @audit-issue: String length is `56`
482:      price > MINIMUM_OUSG_PRICE,
483:      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
484:    );

557:    require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");	// @audit-issue: String length is `44`

570:    require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");	// @audit-issue: String length is `46`

584:    require(	// @audit-issue: String length is `41`
585:      _minimumDepositAmount >= FEE_GRANULARITY,
586:      "setMinimumDepositAmount: Amount too small"
587:    );

602:    require(	// @audit-issue: String length is `44`
603:      _minimumRedemptionAmount >= FEE_GRANULARITY,
604:      "setMinimumRedemptionAmount: Amount too small"
605:    );

763:    require(!redeemPaused, "OUSGInstantManager: Redeem paused");	// @audit-issue: String length is `33`
```
[163](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L163-L166), [167](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L167-L170), [171](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L171-L174), [175](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L175-L178), [179](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L179-L179), [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L180-L180), [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L181-L181), [182](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L182-L185), [186](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L186-L189), [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L190-L193), [205](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L205-L209), [282](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L282-L285), [286](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L286-L289), [298](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L298-L301), [310](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L310-L313), [344](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L344-L347), [371](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L371-L374), [391](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L391-L394), [395](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L395-L398), [402](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L402-L405), [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L417-L420), [459](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L459-L462), [466](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L466-L469), [481](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L481-L484), [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L557-L557), [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L570-L570), [584](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L584-L587), [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L602-L605), [763](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L763-L763), 


#### Recommendation


To optimize Gas usage in your Solidity contract, it is recommended to keep revert strings as short as possible and to ensure that they fit within 32 bytes. It is possible to use abbreviations or simplified error messages to keep the string length short. Doing so can reduce the amount of Gas used during deployment and runtime when the revert condition is met.


### Increments can be `unchecked` in for-loops
Newer versions of the Solidity compiler will check for integer overflows and underflows automatically. This provides safety but increases gas costs.
When an unsigned integer is guaranteed to never overflow, the unchecked feature of Solidity can be used to save gas costs.A common case for this is for-loops using a strictly-less-than comparision in their conditional statement.

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

125:    for (uint256 i = 0; i < exCallData.length; ++i) {	// @audit-issue
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L125-L125), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

804:    for (uint256 i = 0; i < exCallData.length; ++i) {	// @audit-issue
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L804-L804), 


#### Recommendation

Use unchecked math to block overflow / underflow check to save Gas.

### Divisions can be unchecked to save gas
The expression type(int).min/(-1) is the only case where division causes an overflow. Therefore, uncheck can be used to save gas in scenarios where it is certain that such an overflow will not occur.

```solidity
Path: ./contracts/ousg/rOUSG.sol

190:      (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);	// @audit-issue

201:      (_sharesOf(_account) * getOUSGPrice()) /	// @audit-issue

367:      (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();	// @audit-issue

375:      (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);	// @audit-issue

439:      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER	// @audit-issue

636:      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER	// @audit-issue
```
[190](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L190-L190), [201](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L201-L201), [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L367-L367), [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L375-L375), [439](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L439-L439), [636](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L636-L636), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

377:    uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /	// @audit-issue

690:    ousgAmountOut = amountE36 / price;	// @audit-issue

704:    usdcOwed = _scaleDown(amountE36 / 1e18);	// @audit-issue

716:    return (usdcAmount * mintFee) / FEE_GRANULARITY;	// @audit-issue

728:    return (usdcAmount * redeemFee) / FEE_GRANULARITY;	// @audit-issue

748:    return amount / decimalsMultiplier;	// @audit-issue
```
[377](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L377-L377), [690](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L690-L690), [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L704-L704), [716](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L716-L716), [728](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L728-L728), [748](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L748-L748), 


#### Recommendation

Utilize 'unchecked' blocks in Solidity for divisions where overflow is impossible, such as when 'type(int).min/(-1)' is not a concern. This can save gas by bypassing overflow checks in these specific cases.


### Stack variable is only used once
If the variable is only accessed once, it's cheaper to use the assigned value directly that one time, and save the 3 gas the extra stack assignment would spend

```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

307:    uint256 ousgPrice = getOUSGPrice();	// @audit-issue: ousgPrice used only on line: 308

399:    uint256 ousgPrice = getOUSGPrice();	// @audit-issue: ousgPrice used only on line: 400

463:    uint256 usdcBalanceBefore = usdc.balanceOf(address(this));	// @audit-issue: usdcBalanceBefore used only on line: 467

689:    uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;	// @audit-issue: amountE36 used only on line: 690

703:    uint256 amountE36 = ousgAmountBurned * price;	// @audit-issue: amountE36 used only on line: 704
```
[307](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L307-L307), [399](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L399-L399), [463](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L463-L463), [689](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L689-L689), [703](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L703-L703), 


#### Recommendation

Eliminate single-use stack variables in Solidity to optimize gas consumption. Directly use the assigned value in the place of the variable. This approach saves the 3 gas typically used for the extra stack assignment, streamlining the function's execution and enhancing overall gas efficiency.

### Avoid Using State Variables Directly in `emit` for Gas Efficiency
In Solidity, emitting events is a common way to log contract activity and changes, especially for off-chain monitoring and interfacing. However, using state variables directly in `emit` statements can lead to increased gas costs. Each access to a state variable incurs gas due to storage reading operations. When these variables are used directly in `emit` statements, especially within functions that perform multiple operations, the cumulative gas cost can become significant. Instead, caching state variables in memory and using these local copies in `emit` statements can optimize gas usage.


```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

96:    emit rOUSGDeployed(
97:      address(rOUSGProxy),	// @audit-issue: `rOUSGProxy` is a state variable and used on line(s): ['84', '104']
98:      address(rOUSGProxyAdmin),
99:      address(rOUSGImplementation),
100:      rOUSGProxied.name(),
101:      rOUSGProxied.symbol()
102:    );

96:    emit rOUSGDeployed(
97:      address(rOUSGProxy),
98:      address(rOUSGProxyAdmin),	// @audit-issue: `rOUSGProxyAdmin` is a state variable and used on line(s): ['105', '93', '81', '94']
99:      address(rOUSGImplementation),
100:      rOUSGProxied.name(),
101:      rOUSGProxied.symbol()
102:    );

96:    emit rOUSGDeployed(
97:      address(rOUSGProxy),
98:      address(rOUSGProxyAdmin),
99:      address(rOUSGImplementation),	// @audit-issue: `rOUSGImplementation` is a state variable and used on line(s): ['80', '106']
100:      rOUSGProxied.name(),
101:      rOUSGProxied.symbol()
102:    );
```
[97](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L96-L102), [98](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L96-L102), [99](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L96-L102), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

321:    emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);	// @audit-issue: `feeReceiver` is a state variable and used on line(s): ['317']

435:      emit MinimumBUIDLRedemption(
436:        msg.sender,
437:        minBUIDLRedeemAmount,	// @audit-issue: `minBUIDLRedeemAmount` is a state variable and used on line(s): ['434', '426', '438']
438:        usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
439:      );

435:      emit MinimumBUIDLRedemption(
436:        msg.sender,
437:        minBUIDLRedeemAmount,
438:        usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem	// @audit-issue: `minBUIDLRedeemAmount` is a state variable and used on line(s): ['437', '434', '426']
439:      );

453:    emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);	// @audit-issue: `feeReceiver` is a state variable and used on line(s): ['451']

558:    emit MintFeeSet(mintFee, _mintFee);	// @audit-issue: `mintFee` is a state variable and used on line(s): ['557']

571:    emit RedeemFeeSet(redeemFee, _redeemFee);	// @audit-issue: `redeemFee` is a state variable and used on line(s): ['570']
```
[321](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L321-L321), [437](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L435-L439), [438](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L435-L439), [453](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L453-L453), [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L558-L558), [571](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L571-L571), 


#### Recommendation


To optimize gas efficiency, cache state variables in memory when they are used multiple times within a function, including in `emit` statements.


### Consider pre-calculating the address of `address(this)` to save gas
Use `foundry`'s [`script.sol`](https://book.getfoundry.sh/reference/forge-std/compute-create-address) or `solady`'s [`LibRlp.sol`](https://github.com/Vectorized/solady/blob/main/src/utils/LibRLP.sol) to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.

```solidity
Path: ./contracts/ousg/rOUSG.sol

419:    ousg.transferFrom(msg.sender, address(this), _OUSGAmount);	// @audit-issue
```
[419](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L419-L419), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

263:    uint256 ousgAmountOut = _mint(usdcAmountIn, address(this));	// @audit-issue

299:      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,	// @audit-issue

345:      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,	// @audit-issue

348:    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);	// @audit-issue

372:      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,	// @audit-issue

375:    rousg.transferFrom(msg.sender, address(this), rousgAmountIn);	// @audit-issue

424:    uint256 usdcBalance = usdc.balanceOf(address(this));	// @audit-issue

460:      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,	// @audit-issue

463:    uint256 usdcBalanceBefore = usdc.balanceOf(address(this));	// @audit-issue

467:      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,	// @audit-issue
```
[263](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L263-L263), [299](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L299-L299), [345](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L345-L345), [348](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L348-L348), [372](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L372-L372), [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L375-L375), [424](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L424-L424), [460](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L460-L460), [463](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L463-L463), [467](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L467-L467), 


#### Recommendation

To enhance gas efficiency, cache the contract's address by storing `address(this)` in a state variable at the point of contract deployment or initialization. Use this cached address throughout the contract instead of repeatedly calling `address(this)`. This practice reduces the gas cost associated with multiple computations of the contract's address, leading to more efficient contract execution, especially in scenarios with frequent usage of the contract's address.

### Counting down in for statements is more gas efficient
Looping downwards in Solidity is more gas efficient due to how the EVM compares variables. In a 'for' loop that counts down, the end condition is usually to compare with zero, which is cheaper than comparing with another number. As such, restructure your loops to count downwards where possible.

```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

125:    for (uint256 i = 0; i < exCallData.length; ++i) {	// @audit-issue
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L125-L125), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

804:    for (uint256 i = 0; i < exCallData.length; ++i) {	// @audit-issue
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L804-L804), 


#### Recommendation

Where feasible, refactor `for` loops in your Solidity contracts to count downwards. Adjust the loop initialization, condition, and iteration statements to decrement the loop variable and terminate the loop when it reaches zero. This approach can lead to gas savings, making your contract more efficient in terms of execution costs. Ensure that this refactoring aligns with the logic and requirements of your contract, and thoroughly test to confirm that the revised loop behavior matches the intended functionality.

### Use solady library where possible to save gas
The following OpenZeppelin imports have a Solady equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible

```solidity
Path: ./contracts/ousg/rOUSG.sol

18:import "contracts/external/openzeppelin/contracts/token/IERC20.sol";	// @audit-issue

19:import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";	// @audit-issue

20:import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";	// @audit-issue

23:import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";	// @audit-issue

24:import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";	// @audit-issue
```
[18](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L18-L18), [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L19-L19), [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L20-L20), [23](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L23-L23), [24](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L24-L24), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

18:import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";	// @audit-issue

19:import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";	// @audit-issue

20:import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";	// @audit-issue
```
[18](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L18-L18), [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L19-L19), [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L20-L20), 


#### Recommendation

Evaluate and, where appropriate, integrate Solady modules in your Solidity contracts as alternatives to similar OpenZeppelin imports. Focus on areas where gas efficiency can be significantly improved. Ensure that any replacement with Solady's modules does not compromise the security or functionality of your contracts. Conduct thorough testing and code reviews when making such substitutions to confirm compatibility and maintain the integrity of your application. Stay informed about updates and community feedback on both libraries to make informed decisions about their use in your projects.

### Consider using solady's 'FixedPointMathLib'
Using Solady's "FixedPointMathLib" for multiplication or division operations in Solidity can lead to significant gas savings. This library is designed to optimize fixed-point arithmetic operations, which are common in financial calculations involving tokens or currencies. By implementing more efficient algorithms and assembly optimizations, "FixedPointMathLib" minimizes the computational resources required for these operations. For contracts that frequently perform such calculations, integrating this library can reduce transaction costs, thereby enhancing overall performance and cost-effectiveness. However, developers must ensure compatibility with their existing codebase and thoroughly test for accuracy and expected behavior to avoid any unintended consequences.

```solidity
Path: ./contracts/ousg/rOUSG.sol

190:      (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);	// @audit-issue

201:      (_sharesOf(_account) * getOUSGPrice()) /	// @audit-issue

202:      (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);	// @audit-issue

367:      (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();	// @audit-issue

375:      (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);	// @audit-issue

417:    uint256 ousgSharesAmount = _OUSGAmount * OUSG_TO_ROUSG_SHARES_MULTIPLIER;	// @audit-issue

439:      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER	// @audit-issue

636:      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER	// @audit-issue
```
[190](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L190-L190), [201](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L201-L201), [202](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L202-L202), [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L367-L367), [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L375-L375), [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L417-L417), [439](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L439-L439), [636](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L636-L636), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

267:      ousgAmountOut * OUSG_TO_ROUSG_SHARES_MULTIPLIER	// @audit-issue

377:    uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /	// @audit-issue

689:    uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;	// @audit-issue

690:    ousgAmountOut = amountE36 / price;	// @audit-issue

703:    uint256 amountE36 = ousgAmountBurned * price;	// @audit-issue

704:    usdcOwed = _scaleDown(amountE36 / 1e18);	// @audit-issue

716:    return (usdcAmount * mintFee) / FEE_GRANULARITY;	// @audit-issue

728:    return (usdcAmount * redeemFee) / FEE_GRANULARITY;	// @audit-issue

738:    return amount * decimalsMultiplier;	// @audit-issue

748:    return amount / decimalsMultiplier;	// @audit-issue
```
[267](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L267-L267), [377](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L377-L377), [689](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L689-L689), [690](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L690-L690), [703](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L703-L703), [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L704-L704), [716](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L716-L716), [728](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L728-L728), [738](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L738-L738), [748](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L748-L748), 


#### Recommendation

Consider integrating Solady's 'FixedPointMathLib' into your Solidity contracts for optimized fixed-point arithmetic operations. This library can provide substantial gas savings and enhance the performance of your contract. Before integration, evaluate how 'FixedPointMathLib' aligns with your contract’s requirements. Ensure thorough testing for accuracy and compatibility with your existing contract logic. Carefully document any changes and keep track of how these optimizations affect your contract's operations to maintain transparency and reliability in your application. Adopting 'FixedPointMathLib' should be a considered decision, balancing the benefits of gas efficiency with the need for maintaining code clarity and functionality.


### Reduce Gas Usage by Moving to Solidity 0.8.19 or Later
This issue highlights the opportunity to reduce gas consumption in a smart contract by upgrading the Solidity compiler version to 0.8.19 or a later release. Gas usage is a critical consideration in Ethereum smart contracts, as it directly affects transaction costs and contract execution efficiency. Newer compiler versions often come with optimizations and improvements that can lead to reduced gas costs for certain operations and contract structures.


```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

16:pragma solidity 0.8.16;	// @audit-issue
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L16-L16), 


```solidity
Path: ./contracts/ousg/rOUSG.sol

16:pragma solidity 0.8.16;	// @audit-issue
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L16-L16), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

16:pragma solidity 0.8.16;	// @audit-issue
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L16-L16), 


#### Recommendation

Consider upgrading to Solidity version 0.8.19 or later to leverage compiler optimizations for reduced gas consumption. Newer versions often include improvements that enhance transaction cost-efficiency and overall contract execution.

### Constant Keccak Variables Are Treated As Expressions, Not Constants
In Solidity, state variables or local variables declared with the `constant` keyword are expected to represent constant values that are determined at compile time. These constants typically do not incur any gas costs when accessed since their values are hard-coded into the contract bytecode.

However, this expected behavior deviates when using the `keccak256()` function. When a variable is initialized with a `keccak256()` hash computation, even if declared as `constant`, it isn't truly treated as a constant in the resulting bytecode. Instead, every time this "constant" is referenced, the EVM recalculates the hash. This behavior contrasts with other true constants, which are embedded directly into the bytecode and accessed without additional computations.


```solidity
Path: ./contracts/ousg/rOUSG.sol

93:  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");	// @audit-issue

94:  bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");	// @audit-issue

95:  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");	// @audit-issue
```
[93](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L93-L93), [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L94-L94), [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSG.sol#L95-L95), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

57:  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");	// @audit-issue

60:  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");	// @audit-issue
```
[57](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L57-L57), [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L60-L60), 


#### Recommendation

Avoid using 'keccak256()' to initialize 'constant' variables in Solidity. Instead, precompute the hash value outside of the contract and assign this precomputed value to the constant. This ensures the variable is a true constant, eliminating redundant hash computations and saving gas.


### Using `bool`s for storage incurs overhead
[Booleans are more expensive than uint256](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27) or any type that takes up a full word because each write operation emits an extra SLOAD to first read the slot's contents, replace the bits taken up by the boolean, and then write back. This is the compiler's defense against contract upgrades and pointer aliasing, and it cannot be disabled.
Use `uint256(0)` and `uint256(1)` for true/false to avoid a Gwarmaccess (**[100 gas](https://gist.github.com/IllIllI000/1b70014db712f8572a72378321250058)**) for the extra SLOAD.


```solidity
Path: ./contracts/ousg/rOUSGFactory.sol

45:  bool public initialized = false;	// @audit-issue
```
[45](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/rOUSGFactory.sol#L45-L45), 


```solidity
Path: ./contracts/ousg/ousgInstantManager.sol

113:  bool public mintPaused;	// @audit-issue

116:  bool public redeemPaused;	// @audit-issue
```
[113](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L113-L113), [116](https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/./contracts/ousg/ousgInstantManager.sol#L116-L116), 


#### Recommendation

To minimize gas overhead in your Solidity contracts, consider using `uint256(1)` and `uint256(2)` to represent `true` and `false`, respectively, instead of `bool` types for storage. This approach avoids additional `SLOAD` and `SSTORE` operations, resulting in more gas-efficient code.
