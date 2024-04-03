## Gas Findings

|    | Issue | Instances | Total Gas Saved |
|----|-------|:---------:|:---------:|
| [G-01] | State variables can be packed into fewer storage slots | 1 | 20000 |
| [G-02] | A `memory` array's `length` should not be looked up in every iteration of a `for`/`while`-loop | 2 | 6 |
| [G-03] | `do`-`while` is cheaper than `for`-loops when the initial check can be skipped | 2 | 510 |
| [G-04] | Use `assembly` for Efficient Event Emission | 33 | 12540 |
| [G-05] | Use custom errors rather than `require()/assert()/revert(with msg)` with string to save gas | 51 | 2550 |
| [G-06] | Enable IR-based code generation | 3 | - |
| [G-07] | Avoid Explicit Initialization to Zero for Non-Constant/Non-Immutable State Variables | 2 | 5800 |
| [G-08] | Assembly: Check `msg.sender` using xor and the scratch space | 3 | 63 |
| [G-09] | Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct` | 2 | - |
| [G-10] | Assembly: Use scratch space when building emitted events with two data arguments | 1 | 15 |
| [G-11] | Stack variable is only used once | 5 | 15 |
| [G-12] | Using `require()` instead of `assert()` safes gas | 1 | 33 |
| [G-13] | Use `assembly` to write mutable storage values | 26 | 286 |
| [G-14] | Use `revert()` to gain maximum gas savings | 53 | 2650 |
| [G-15] | Use local variables for emitting | 9 | 900 |
| [G-16] | Initializers can be marked as payable | 1 | - |
| [G-17] | Shorten the array rather than copying to a new on | 2 | 0 |
| [G-18] | Using `delete` on a `bool` variable is cheaper than assigning it to `false` | 2 | 48 |
| [G-19] | Use `Array.unsafeAccess()` to avoid repeated array length checks | 2 | 4200 |
| [G-20] | Counting down when iterating, saves gas | 2 | 18 |
| [G-21] | `>=` costs less gas than `>` | 6 | 36 |
| [G-22] | Consider pre-calculating the address of `address(this)` to save gas | 11 | 0 |
| [G-23] | Constructors can be marked `payable` | 3 | 72 |
| [G-24] | Optimize Increment and Decrement in loops with `unchecked` keyword | 2 | 120 |
| [G-25] | Reduce gas usage by moving to Solidity 0.8.19 or later | 3 | - |
| [G-26] | Reduce deployment costs by tweaking contracts' metadata | 3 | 31800 |
| [G-27] | Nesting `if`-statements is cheaper than using `&&` | 1 | 6 |
| [G-28] | Avoid transferring amounts of zero in order to save gas | 6 | 600 |
| [G-29] | Cache Function Calls for Efficiency | 2 | - |
| [G-30] | Use `unchecked` for Math Operations if they already checked | 4 | 340 |
| [G-31] | Using `private` rather than `public`, saves gas | 33 | 726000 |
| [G-32] | Refactor duplicated require()/revert() checks to save gas | 2 | - |
| [G-33] | Use Assembly for Efficient Memory Management in Multiple External Calls | 15 | 40000 |
| [G-34] | Optimize `require/revert` Statements with Assembly | 50 | 15000 |
| [G-35] | Use Cached Contracts for Multiple External Calls | 2 | 336 |
| [G-36] | Consider using solady's `FixedPointMathLib` | 31 | - |
| [G-37] | Avoid Zero to Non-Zero Storage Writes Where Possible | 14 | 309400 |
| [G-38] | Avoid Unnecessary Gas Usage with Shorter `require()/revert()` Strings | 35 | 630 |
| [G-39] | Use `unchecked` for division which do not divide by -X sonce they can't overflow | 12 | 240 |
| [G-40] | Use solady library where possible to save gas | 11 | 11000 |
| [G-41] | Use `uint256(1)`/`uint256(2)` instead of `true`/`false` to save gas for changes | 3 | 51000 |
| [G-42] | Mark Functions That Revert For Normal Users As `payable` | 28 | 588 |
| [G-43] | Prefer `private` over `public` for Constants to Save Gas | 10 | 30000 |
| [G-44] | `<x> += <y>` costs more gas than `<x> = <x> + <y>` for state variables | 2 | 226 |
| [G-45] | Using `bool`s for storage incurs overhead | 3 | 300 |
| [G-46] | Optimize Gas by Using Only Named Returns | 24 | 1056 |
| [G-47] | Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead | 1 | 6 |
| [G-48] | Unlimited gas consumption risk due to external call recipients | 2 | - |
| [G-49] | Use assembly to check for `address(0)` | 19 | 1102 |
| [G-50] | `internal`/`private` functions only called once can be inlined to save gas | 9 | 180 |
| [G-51] | Consider using OZ EnumerateSet in place of nested mappings | 1 | 1000 |
| [G-52] | Declare `immutable` as `private` to save gas | 7 | 21000 |
| [G-53] | State variables should be cached in stack rather than re-reading them from storage | 21 | 2813 |
| [G-54] | Optimize names to save gas | 3 | 60 |
| [G-55] | Avoid updating storage when the value hasn't changed | 12 | 9600 |
| [G-56] | Optimize External Calls with Assembly for Memory Efficiency | 30 | 6600 |

Total: 624 instances of 56 issues with 1310745 gas saved

## Gas Findings Details

### [G-01] State variables can be packed into fewer storage slots

Each slot saved can avoid an extra Gsset (20000 gas). Reads and writes (if two variables that occupy the same slot are written by the same function) will have a cheaper gas consumption.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit - State variables use 9 storage slots, but can be packed to 8 storage slots.
//	IInvestorBasedRateLimiter public investorBasedRateLimiter
//	uint256 public minBUIDLRedeemAmount = 250_000e6
//	uint256 public minimumRedemptionAmount = 50_000e6
//	uint256 public minimumDepositAmount = 100_000e6
//	uint256 public redeemFee = 0
//	uint256 public mintFee = 0
//	IRWAOracle public oracle
//	address public feeReceiver
//	bool public redeemPaused
//	bool public mintPaused

49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
```
[49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49)
</details>

### [G-02] A `memory` array's `length` should not be looked up in every iteration of a `for`/`while`-loop

It is more efficient to cache the array length instead of looking it up in every iteration of a for-loop.

Example:

```solidity
- for(uint i = 0; i < array.length; i++)
+ uint length = array.length;
+ for(uint i = 0; i < length; i++);
```

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

804: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
File: contracts/ousg/rOUSGFactory.sol

125: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)
</details>

### [G-03] `do`-`while` is cheaper than `for`-loops when the initial check can be skipped

Using `do-while` loops instead of `for` loops can be more gas-efficient. 
Even if you add an `if` condition to account for the case where the loop doesn't execute at all, a `do-while` loop can still be cheaper in terms of gas.

Example:
```solidity
/// 774 gas cost
function forLoop() public pure {
    for (uint256 i; i < 10;) {
        unchecked {
            ++i;
        }
    }
}
/// 519 gas cost
function doWhileLoop() public pure {
    uint256 i;
    do {
        unchecked {
            ++i;
        }
    } while (i < 10);
}
```

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

804: for (uint256 i = 0; i < exCallData.length; ++i)
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
File: contracts/ousg/rOUSGFactory.sol

125: for (uint256 i = 0; i < exCallData.length; ++i)
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)
</details>

### [G-04] Use `assembly` for Efficient Event Emission

To efficiently emit events, consider utilizing assembly by making use of scratch space and the free memory pointer.
This approach can potentially avoid the costs associated with memory expansion.

However, it's crucial to cache and restore the free memory pointer for safe optimization.
Good examples of such practices can be found in well-optimized [Solady's codebases](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167).
Please review your code and consider the potential gas savings of this approach.

<details>
<summary><i>33 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

240: emit InstantMintOUSG(msg.sender, usdcAmountIn, ousgAmountOut)
270: emit InstantMintRebasingOUSG(
      msg.sender,
      usdcAmountIn,
      ousgAmountOut,
      rousgAmountOut
    )
321: emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn)
350: emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut)
380: emit InstantRedemptionRebasingOUSG(
      msg.sender,
      rousgAmountIn,
      ousgAmountIn,
      usdcAmountOut
    )
435: emit MinimumBUIDLRedemption(
        msg.sender,
        minBUIDLRedeemAmount,
        usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
      )
443: emit BUIDLRedemptionSkipped(
        msg.sender,
        usdcAmountToRedeem,
        usdcBalance - usdcAmountToRedeem
      )
453: emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut)
558: emit MintFeeSet(mintFee, _mintFee)
571: emit RedeemFeeSet(redeemFee, _redeemFee)
589: emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount)
606: emit MinimumRedemptionAmountSet(
      minimumRedemptionAmount,
      _minimumRedemptionAmount
    )
625: emit MinimumBUIDLRedemptionAmountSet(
      minBUIDLRedeemAmount,
      _minimumBUIDLRedemptionAmount
    )
641: emit OracleSet(address(oracle), _oracle)
654: emit FeeReceiverSet(feeReceiver, _feeReceiver)
666: emit InvestorBasedRateLimiterSet(
      address(investorBasedRateLimiter),
      _investorBasedRateLimiter
    )
770: emit MintPaused()
776: emit MintUnpaused()
782: emit RedeemPaused()
788: emit RedeemUnpaused()
```
[240](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L240) | [270](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L270) | [321](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L321) | [350](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L350) | [380](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L380) | [435](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L435) | [443](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L443) | [453](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L453) | [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L558) | [571](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L571) | [589](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L589) | [606](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L606) | [625](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L625) | [641](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L641) | [654](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L654) | [666](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L666) | [770](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L770) | [776](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L776) | [782](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L782) | [788](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L788)

```solidity
File: contracts/ousg/rOUSG.sol

402: emit TransferShares(msg.sender, _recipient, _sharesAmount)
404: emit Transfer(msg.sender, _recipient, tokensAmount)
420: emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount))
421: emit TransferShares(address(0), msg.sender, ousgSharesAmount)
441: emit Transfer(msg.sender, address(0), _rOUSGAmount)
442: emit TransferShares(msg.sender, address(0), ousgSharesAmount)
457: emit Transfer(_sender, _recipient, _amount)
458: emit TransferShares(_sender, _recipient, _sharesToTransfer)
481: emit Approval(_owner, _spender, _amount)
614: emit OracleSet(address(oracle), _oracle)
638: emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount))
639: emit TransferShares(_account, address(0), ousgSharesAmount)
```
[402](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L402) | [404](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L404) | [420](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L420) | [421](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L421) | [441](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L441) | [442](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L442) | [457](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L457) | [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L458) | [481](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L481) | [614](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L614) | [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L638) | [639](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L639)

```solidity
File: contracts/ousg/rOUSGFactory.sol

96: emit rOUSGDeployed(
      address(rOUSGProxy),
      address(rOUSGProxyAdmin),
      address(rOUSGImplementation),
      rOUSGProxied.name(),
      rOUSGProxied.symbol()
    )
```
[96](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L96)
</details>

### [G-05] Use custom errors rather than `require()/assert()/revert(with msg)` with string to save gas

Custom errors are available from solidity version 0.8.4.
Custom errors save [~50](https://gist.github.com/IllIllI000/ad1bd0d29a0101b25e57c293b4b0c746) gas each time they're hit by [avoiding having to allocate and store the revert string](https://soliditylang.org/blog/2021/04/21/custom-errors/#errors-in-depth).
Alse Custom error are cheaper than `assert()`.
```solidity
    revert CustomError(); // 157 gas
    assert(false); // 164 gas
    revert("Custom Error"); // 406 gas
    require(false, "Custom Error"); // 421 gas
```


<details>
<summary><i>51 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

163: require(
      address(_usdc) != address(0),
      "OUSGInstantManager: USDC cannot be 0x0"
    )
167: require(
      address(_usdcReciever) != address(0),
      "OUSGInstantManager: USDC Receiver cannot be 0x0"
    )
171: require(
      address(_feeReceiver) != address(0),
      "OUSGInstantManager: feeReceiver cannot be 0x0"
    )
175: require(
      address(_ousgOracle) != address(0),
      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
    )
179: require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0")
180: require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0")
181: require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0")
182: require(
      address(_buidlRedeemer) != address(0),
      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    )
186: require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    )
190: require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    )
205: require(
      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
    )
282: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_mint: USDC decimals must be 6"
    )
286: require(
      usdcAmountIn >= minimumDepositAmount,
      "OUSGInstantManager::_mint: Deposit amount too small"
    )
298: require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    )
310: require(
      ousgAmountOut > 0,
      "OUSGInstantManager::_mint: net mint amount can't be zero"
    )
344: require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    )
371: require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    )
391: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_redeem: USDC decimals must be 6"
    )
395: require(
      IERC20Metadata(address(buidl)).decimals() == 6,
      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    )
402: require(
      usdcAmountToRedeem >= minimumRedemptionAmount,
      "OUSGInstantManager::_redeem: Redemption amount too small"
    )
417: require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    )
459: require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    )
466: require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    )
481: require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    )
557: require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high")
570: require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high")
584: require(
      _minimumDepositAmount >= FEE_GRANULARITY,
      "setMinimumDepositAmount: Amount too small"
    )
602: require(
      _minimumRedemptionAmount >= FEE_GRANULARITY,
      "setMinimumRedemptionAmount: Amount too small"
    )
653: require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0")
757: require(!mintPaused, "OUSGInstantManager: Mint paused")
763: require(!redeemPaused, "OUSGInstantManager: Redeem paused")
808: require(success, "Call Failed")
```
[163](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L163) | [167](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L167) | [171](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L171) | [175](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L175) | [179](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L179) | [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L180) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L181) | [182](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L182) | [186](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L186) | [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L190) | [205](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L205) | [282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L282) | [286](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L286) | [298](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L298) | [310](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310) | [344](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L344) | [371](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L371) | [391](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L391) | [395](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L395) | [402](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L402) | [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L417) | [459](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L459) | [466](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L466) | [481](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L481) | [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557) | [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570) | [584](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L584) | [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602) | [653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L653) | [757](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L757) | [763](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L763) | [808](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L808)

```solidity
File: contracts/ousg/rOUSG.sol

282: require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE")
333: require(
      currentAllowance >= _subtractedValue,
      "DECREASED_ALLOWANCE_BELOW_ZERO"
    )
416: require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens")
432: require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens")
477: require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS")
478: require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS")
506: require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS")
507: require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS")
512: require(
      _sharesAmount <= currentSenderShares,
      "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
    )
533: require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS")
558: require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS")
563: require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE")
594: require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd")
599: require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd")
604: require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd")
```
[282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L282) | [333](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L333) | [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416) | [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432) | [477](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L477) | [478](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L478) | [506](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506) | [507](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L507) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L512) | [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533) | [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L558) | [563](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L563) | [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L599) | [604](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L604)

```solidity
File: contracts/ousg/rOUSGFactory.sol

76: require(!initialized, "ROUSGFactory: rOUSG already deployed")
94: assert(rOUSGProxyAdmin.owner() == guardian)
129: require(success, "Call Failed")
150: require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian")
```
[76](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L76) | [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94) | [129](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L129) | [150](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L150)
</details>

### [G-06] Enable IR-based code generation

The `--via-ir` command line option activates the IR-based code generator in Solidity, which is designed to enable powerful optimization passes that can span across functions. The end result may be a contract that requires less gas to execute its functions.

We recommend you enable this feature, run tests, and benchmark the gas usage of your contract to evaluate if it leads to any tangible gas savings. Experimenting with this feature could lead to a more gas-efficient contract.

[Solidity Documentation](https://docs.soliditylang.org/en/v0.8.20/ir-breaking-changes.html#solidity-ir-based-codegen-changes).

<details>
<summary><i>3 issue instances in 1 files:</i></summary>

```solidity

File: contracts/ousg/ousgInstantManager.sol
File: contracts/ousg/rOUSG.sol
File: contracts/ousg/rOUSGFactory.sol
```
[1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L1) | [1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L1) | [1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L1)
</details>

### [G-07] Avoid Explicit Initialization to Zero for Non-Constant/Non-Immutable State Variables

Explicitly initializing non-constant/non-immutable state variables to zero is not efficient from a gas perspective. 
Letting Solidity use the default zero for uninitialized storage variables avoids a Gsreset, which costs 2900 gas, during deployment.
Consider removing these unnecessary initializations to optimize gas usage.
```solidity
    uint256 public foo = 0; // tx 69107 gas | exec 14669 gas
    uint256 public foo;     // tx 66854 gas | exec 12464 gas
``` 

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

99: uint256 public mintFee = 0
102: uint256 public redeemFee = 0
```
[99](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L99) | [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L102)
</details>

### [G-08] Assembly: Check `msg.sender` using xor and the scratch space

See [this](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender) prior finding for details on the conversion

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

593: if (from != msg.sender && to != msg.sender) {
593: if (from != msg.sender && to != msg.sender) {
```
[593](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L593) | [593](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L593)

```solidity
File: contracts/ousg/rOUSGFactory.sol

150: require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");
```
[150](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L150)
</details>

### [G-09] Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`

Combining multiple address/ID mappings into a single mapping to a struct can lead to gas savings.
By refactoring multiple mappings into a singular mapping with a struct, you can save on storage slots, which in turn can reduce the gas cost in certain operations.
Prioritize this refactor if optimizing gas is a primary concern for your contract's operations.

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

72: mapping(address => uint256) private shares
75: mapping(address => mapping(address => uint256)) private allowances
```
[72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72) | [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75)
</details>

### [G-10] Assembly: Use scratch space when building emitted events with two data arguments

Using the scratch space for more than one, but at most two words worth of data (non-indexed arguments) will save gas over needing Solidity's abi memory expansion used for emitting normally.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

96: emit rOUSGDeployed(
      address(rOUSGProxy),
      address(rOUSGProxyAdmin),
      address(rOUSGImplementation),
      rOUSGProxied.name(),
      rOUSGProxied.symbol()
    )
```
[96](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L96)
</details>

### [G-11] Stack variable is only used once

If the variable is only accessed once, it's cheaper to use the assigned value directly that one time, and save the 3 gas the extra stack assignment would spend

<details>
<summary><i>5 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit - `ousgPrice` variable
307: uint256 ousgPrice = getOUSGPrice()
/// @audit - `ousgPrice` variable
399: uint256 ousgPrice = getOUSGPrice()
/// @audit - `usdcBalanceBefore` variable
463: uint256 usdcBalanceBefore = usdc.balanceOf(address(this))
/// @audit - `amountE36` variable
689: uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18
/// @audit - `amountE36` variable
703: uint256 amountE36 = ousgAmountBurned * price
```
[307](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L307) | [399](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L399) | [463](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L463) | [689](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L689) | [703](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L703)
</details>

### [G-12] Using `require()` instead of `assert()` safes gas

Since `assert()` can't contain any message, it is recommended to use `require()` without message instead.
Using `require()` saves 33 gas per call.
```solidity
    require(false); // 133 gas
    assert(false); // 166 gas 
```


<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

94: assert(rOUSGProxyAdmin.owner() == guardian)
```
[94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94)
</details>

### [G-13] Use `assembly` to write mutable storage values

Writing to storage using `assembly` is more gas efficient.
```solidity
    function writeStorage() external {
        // storageNumber = 10; // 2358 gas
        // assembly {
        //     sstore(storageNumber.slot, 10) // 2350 gas
        // }
        // storageAddr = 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc3; // 2411 gas
        // assembly {
        //     sstore(storageAddr.slot, 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc3) // 2350 gas
        // }
    }
```

<details>
<summary><i>26 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

196: feeReceiver = _feeReceiver
197: oracle = IRWAOracle(_ousgOracle)
559: mintFee = _mintFee
572: redeemFee = _redeemFee
590: minimumDepositAmount = _minimumDepositAmount
610: minimumRedemptionAmount = _minimumRedemptionAmount
629: minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount
642: oracle = IRWAOracle(_oracle)
655: feeReceiver = _feeReceiver
670: investorBasedRateLimiter = IInvestorBasedRateLimiter(
      _investorBasedRateLimiter
    )
769: mintPaused = true
775: mintPaused = false
781: redeemPaused = true
787: redeemPaused = false
```
[196](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L196) | [197](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L197) | [559](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L559) | [572](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L572) | [590](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L590) | [610](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L610) | [629](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L629) | [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L642) | [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L655) | [670](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L670) | [769](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L769) | [775](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L775) | [781](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L781) | [787](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L787)

```solidity
File: contracts/ousg/rOUSG.sol

136: ousg = IERC20(_ousg)
137: oracle = IRWAOracle(_oracle)
480: allowances[_owner][_spender] = _amount
517: shares[_sender] = currentSenderShares - _sharesAmount
518: shares[_recipient] = shares[_recipient] + _sharesAmount
539: shares[_recipient] = shares[_recipient] + _sharesAmount
567: shares[_account] = accountShares - _sharesAmount
615: oracle = IRWAOracle(_oracle)
```
[136](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L136) | [137](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L137) | [480](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L480) | [517](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L517) | [518](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L518) | [539](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L539) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L567) | [615](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L615)

```solidity
File: contracts/ousg/rOUSGFactory.sol

77: rOUSGImplementation = new ROUSG()
78: rOUSGProxyAdmin = new ProxyAdmin()
79: rOUSGProxy = new TokenProxy(
      address(rOUSGImplementation),
      address(rOUSGProxyAdmin),
      ""
    )
95: initialized = true
```
[77](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L77) | [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L78) | [79](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L79) | [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L95)
</details>

### [G-14] Use `revert()` to gain maximum gas savings

If you dont need Error messages, or you want gain maximum gas savings - `revert()` is a cheapest way to revert transaction in terms of gas.
```solidity
    revert(); // 117 gas 
    require(false); // 132 gas
    revert CustomError(); // 157 gas
    assert(false); // 164 gas
    revert("Custom Error"); // 406 gas
    require(false, "Custom Error"); // 421 gas
```


<details>
<summary><i>53 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

163: require(
      address(_usdc) != address(0),
      "OUSGInstantManager: USDC cannot be 0x0"
    )
167: require(
      address(_usdcReciever) != address(0),
      "OUSGInstantManager: USDC Receiver cannot be 0x0"
    )
171: require(
      address(_feeReceiver) != address(0),
      "OUSGInstantManager: feeReceiver cannot be 0x0"
    )
175: require(
      address(_ousgOracle) != address(0),
      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
    )
179: require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0")
180: require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0")
181: require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0")
182: require(
      address(_buidlRedeemer) != address(0),
      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    )
186: require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    )
190: require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    )
205: require(
      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
    )
282: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_mint: USDC decimals must be 6"
    )
286: require(
      usdcAmountIn >= minimumDepositAmount,
      "OUSGInstantManager::_mint: Deposit amount too small"
    )
298: require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    )
310: require(
      ousgAmountOut > 0,
      "OUSGInstantManager::_mint: net mint amount can't be zero"
    )
344: require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    )
371: require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    )
391: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_redeem: USDC decimals must be 6"
    )
395: require(
      IERC20Metadata(address(buidl)).decimals() == 6,
      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    )
402: require(
      usdcAmountToRedeem >= minimumRedemptionAmount,
      "OUSGInstantManager::_redeem: Redemption amount too small"
    )
417: require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    )
459: require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    )
466: require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    )
481: require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    )
557: require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high")
570: require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high")
584: require(
      _minimumDepositAmount >= FEE_GRANULARITY,
      "setMinimumDepositAmount: Amount too small"
    )
602: require(
      _minimumRedemptionAmount >= FEE_GRANULARITY,
      "setMinimumRedemptionAmount: Amount too small"
    )
653: require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0")
757: require(!mintPaused, "OUSGInstantManager: Mint paused")
763: require(!redeemPaused, "OUSGInstantManager: Redeem paused")
808: require(success, "Call Failed")
```
[163](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L163) | [167](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L167) | [171](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L171) | [175](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L175) | [179](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L179) | [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L180) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L181) | [182](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L182) | [186](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L186) | [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L190) | [205](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L205) | [282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L282) | [286](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L286) | [298](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L298) | [310](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310) | [344](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L344) | [371](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L371) | [391](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L391) | [395](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L395) | [402](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L402) | [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L417) | [459](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L459) | [466](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L466) | [481](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L481) | [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557) | [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570) | [584](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L584) | [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602) | [653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L653) | [757](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L757) | [763](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L763) | [808](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L808)

```solidity
File: contracts/ousg/rOUSG.sol

282: require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE")
333: require(
      currentAllowance >= _subtractedValue,
      "DECREASED_ALLOWANCE_BELOW_ZERO"
    )
416: require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens")
432: require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens")
477: require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS")
478: require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS")
506: require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS")
507: require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS")
512: require(
      _sharesAmount <= currentSenderShares,
      "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
    )
533: require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS")
558: require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS")
563: require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE")
594: require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd")
599: require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd")
604: require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd")
435: revert UnwrapTooSmall()
630: revert UnwrapTooSmall()
```
[282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L282) | [333](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L333) | [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416) | [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432) | [477](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L477) | [478](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L478) | [506](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506) | [507](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L507) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L512) | [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533) | [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L558) | [563](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L563) | [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L599) | [604](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L604) | [435](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L435) | [630](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L630)

```solidity
File: contracts/ousg/rOUSGFactory.sol

76: require(!initialized, "ROUSGFactory: rOUSG already deployed")
94: assert(rOUSGProxyAdmin.owner() == guardian)
129: require(success, "Call Failed")
150: require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian")
```
[76](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L76) | [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94) | [129](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L129) | [150](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L150)
</details>

### [G-15] Use local variables for emitting

Use the function/modifier's local copy of the state variable, rather than incurring an extra Gwarmaccess (100 gas).
In the unlikely event that the state variable hasn't already been used by the function/modifier, consider whether it is really necessary to include it in the event, given the fact that it incurs a Gcoldsload (2100 gas), or whether it can be passed in to or back out of the functions that do use it.

<details>
<summary><i>9 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

321: emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn)
435: emit MinimumBUIDLRedemption(
        msg.sender,
        minBUIDLRedeemAmount,
        usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
      )
453: emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut)
558: emit MintFeeSet(mintFee, _mintFee)
571: emit RedeemFeeSet(redeemFee, _redeemFee)
589: emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount)
606: emit MinimumRedemptionAmountSet(
      minimumRedemptionAmount,
      _minimumRedemptionAmount
    )
625: emit MinimumBUIDLRedemptionAmountSet(
      minBUIDLRedeemAmount,
      _minimumBUIDLRedemptionAmount
    )
654: emit FeeReceiverSet(feeReceiver, _feeReceiver)
```
[321](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L321) | [435](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L435) | [453](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L453) | [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L558) | [571](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L571) | [589](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L589) | [606](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L606) | [625](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L625) | [654](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L654)
</details>

### [G-16] Initializers can be marked as payable

Payable functions cost less gas to execute, because the compiler does not have to add extra checks to ensure that no payment is provided.
Initializers can be safely marked as payable, because only the deployer or the factory contract would call the function without carrying any funds.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

102: function initialize(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) public virtual initializer
```
[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102)
</details>

### [G-17] Shorten the array rather than copying to a new on

In Solidity, harnessing inline assembly empowers you to modify an array's length slot directly, obviating the need to duplicate elements into a new array of the desired size.
This method shines in terms of gas efficiency, as it sidesteps the computational overhead tied to array replication.
However, it's important to exercise caution when using this technique, as it bypasses the type-checking and safety features of high-level Solidity.

Always exercise due diligence to ensure that the array doesn't contain critical data beyond the adjusted length.
Data exceeding the new length will become inaccessible, yet it will still occupy storage space.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

803: results = new bytes[](exCallData.length)
```
[803](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L803)

```solidity
File: contracts/ousg/rOUSGFactory.sol

124: results = new bytes[](exCallData.length)
```
[124](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L124)
</details>

### [G-18] Using `delete` on a `bool` variable is cheaper than assigning it to `false`

```solidity
function test() external {
    delete bar; // 5184 gas
    bar = false; // 5208 gas
}
```

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

775: mintPaused = false
787: redeemPaused = false
```
[775](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L775) | [787](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L787)
</details>

### [G-19] Use `Array.unsafeAccess()` to avoid repeated array length checks

When using storage arrays, solidity adds an internal lookup of the array's length (a Gcoldsload 2100 gas) to ensure you don't read past the array's end.
You can avoid this lookup by using `Array.unsafeAccess()` in cases where the length has already been checked, as is the case with the instances below.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

804: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
File: contracts/ousg/rOUSGFactory.sol

125: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)
</details>

### [G-20] Counting down when iterating, saves gas

Counting down saves 6 gas per loop, since checks for zero are more efficient than checks against any other value.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

804: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
File: contracts/ousg/rOUSGFactory.sol

125: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)
</details>

### [G-21] `>=` costs less gas than `>`

The compiler uses opcodes GT and ISZERO for solidity code that uses >, but only requires LT for >=, which saves 3 gas. If < is being used, the condition can be inverted.
In cases where a for-loop is being used, one can count down rather than up, in order to use the optimal operator.

<details>
<summary><i>6 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

311: ousgAmountOut > 0,
316: if (usdcfees > 0) {
418: usdcAmountOut > 0,
450: if (usdcFees > 0) {
```
[311](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L311) | [316](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L316) | [418](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L418) | [450](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L450)

```solidity
File: contracts/ousg/rOUSG.sol

416: require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");
432: require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
```
[416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416) | [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432)
</details>

### [G-22] Consider pre-calculating the address of `address(this)` to save gas

Use foundry's script.sol or solady's LibRlp.sol to save the value in a constant, which will avoid having to spend gas to push the value on the stack every time it's used.

<details>
<summary><i>11 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

263: uint256 ousgAmountOut = _mint(usdcAmountIn, address(this));
299: usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
345: ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
348: ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
372: rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
375: rousg.transferFrom(msg.sender, address(this), rousgAmountIn);
424: uint256 usdcBalance = usdc.balanceOf(address(this));
460: buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
463: uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
467: usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
```
[263](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L263) | [299](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L299) | [345](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L345) | [348](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L348) | [372](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L372) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L375) | [424](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L424) | [460](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L460) | [463](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L463) | [467](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L467)

```solidity
File: contracts/ousg/rOUSG.sol

419: ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
```
[419](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L419)
</details>

### [G-23] Constructors can be marked `payable`

Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided.

A constructor can safely be marked as `payable`, since only the deployer would be able to pass funds, and the project itself would not pass any funds. 
T
his could save an average of about 21 gas per call, in addition to the extra deployment cost.

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

144: constructor(
    address defaultAdmin,
    address _usdc,
    address _usdcReciever,
    address _feeReceiver,
    address _ousgOracle,
    address _ousg,
    address _rousg,
    address _buidl,
    address _buidlRedeemer,
    RateLimiterConfig memory rateLimiterConfig
  )
    InstantMintTimeBasedRateLimiter(
      rateLimiterConfig.mintLimitDuration,
      rateLimiterConfig.redeemLimitDuration,
      rateLimiterConfig.mintLimit,
      rateLimiterConfig.redeemLimit
    )
  {
```
[144](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144)

```solidity
File: contracts/ousg/rOUSG.sol

98: constructor() {
```
[98](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L98)

```solidity
File: contracts/ousg/rOUSGFactory.sol

46: constructor(address _guardian) {
```
[46](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L46)
</details>

### [G-24] Optimize Increment and Decrement in loops with `unchecked` keyword

Use `unchecked{i++}` or `unchecked{++i}` instead of `i++` or `++i` when it is not possible for them to overflow.
This is applicable for Solidity version `0.8.0` or higher to `0.8.23` and saves 30-40 gas per loop.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

804: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
File: contracts/ousg/rOUSGFactory.sol

125: for (uint256 i = 0; i < exCallData.length; ++i) {
```
[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)
</details>

### [G-25] Reduce gas usage by moving to Solidity 0.8.19 or later

See [this](https://soliditylang.org/blog/2023/02/22/solidity-0.8.19-release-announcement/#preventing-dead-code-in-runtime-bytecode) link for the full details. Additionally, every new release has new optimizations, which will save gas.

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L16)

```solidity
File: contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L16)

```solidity
File: contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;
```
[16](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L16)
</details>

### [G-26] Reduce deployment costs by tweaking contracts' metadata

The Solidity compiler appends 53 bytes of metadata to the smart contract code which translates to an extra 10,600 gas (200 per bytecode) + the calldata cost (16 gas per non-zero bytes, 4 gas per zero-byte).
This translates to up to 848 additional gas in calldata cost.
One way to reduce this cost is by optimizing the IPFS hash that gets appended to the smart contract code.

Why is this important?
- The metadata adds an extra 53 bytes, resulting in an additional 10,600 gas cost for deployment.
- It also incurs up to 848 additional gas in calldata cost.

Options to Reduce Gas:
1. Use the `--no-cbor-metadata` compiler option to exclude metadata, but this might affect contract verification.
2. Mine for code comments that lead to an IPFS hash with more zeros, reducing calldata costs.

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L1)

```solidity
File: contracts/ousg/rOUSG.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L1)

```solidity
File: contracts/ousg/rOUSGFactory.sol

1: Consider optimizing the IPFS hash during deployment.
```
[1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L1)
</details>

### [G-27] Nesting `if`-statements is cheaper than using `&&`

Optimization of condition checks in your smart contract is a crucial aspect in ensuring gas efficiency. Specifically, substituting multiple `&&` checks with nested `if` statements can lead to substantial gas savings.

When evaluating multiple conditions within a single `if` statement using the `&&` operator, each condition will consume gas even if a preceding condition fails. However, if these checks are broken down into nested `if` statements, execution halts as soon as a condition fails, saving the gas that would have been consumed by subsequent checks.

This practice is especially beneficial in scenarios where the `if` statement isn't followed by an `else` statement. The reason being, when an `else` statement is present, all conditions must be checked regardless to determine the correct branch of execution.

By reworking your code to utilize nested `if` statements, you can optimize gas usage, reduce execution cost, and enhance your contract's performance.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

593: if (from != msg.sender && to != msg.sender) {
```
[593](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L593)
</details>

### [G-28] Avoid transferring amounts of zero in order to save gas

Performing token or Ether transfers with a zero amount may result in unnecessary gas consumption. 
The absence of a zero-amount check before a transfer or send operation can lead to wasted gas, as the state of the contract remains the same even if the amount is zero. 
Adding a conditional check for zero amounts can prevent these costly, unnecessary operations, thereby optimizing the contract's gas usage.

<details>
<summary><i>6 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit `rousgAmountOut` has not been checked for zero value before transfer
269: rousg.transfer(msg.sender, rousgAmountOut);
/// @audit `usdcAmountAfterFee` has not been checked for zero value before transfer
319: usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
/// @audit `ousgAmountIn` has not been checked for zero value before transfer
348: ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
/// @audit `rousgAmountIn` has not been checked for zero value before transfer
375: rousg.transferFrom(msg.sender, address(this), rousgAmountIn);
```
[269](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L269) | [319](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L319) | [348](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L348) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L375)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit `ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER` has not been checked for zero value before transfer
437: ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
/// @audit `ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER` has not been checked for zero value before transfer
634: ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
```
[437](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L437) | [634](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L634)
</details>

### [G-29] Cache Function Calls for Efficiency

Function calls, especially external function calls, can be quite expensive in terms of gas. 
If you need to retrieve the same data more than once in a function, it is more efficient to call 
the function once, store the result in a local variable, and then use that variable later in the 
code instead of making the function call again.

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

463: uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
467: usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
```
[463](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L463) | [467](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L467)
</details>

### [G-30] Use `unchecked` for Math Operations if they already checked

Some subtraction operations in the contract have implicit checks that prevent underflow. 
To optimize gas, consider wrapping such operations in an `unchecked` block. 
Always review the logic thoroughly before making changes to ensure the safety of operations.

<details>
<summary><i>4 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit - mathematical operation `currentAllowance - _amount` checked above in line:
/// 282: require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");
285: _approve(_sender, msg.sender, currentAllowance - _amount);
/// @audit - mathematical operation `currentAllowance - _subtractedValue` checked above in line:
/// 333: require(
      currentAllowance >= _subtractedValue,
      "DECREASED_ALLOWANCE_BELOW_ZERO"
    );
337: _approve(msg.sender, _spender, currentAllowance - _subtractedValue);
/// @audit - mathematical operation `currentSenderShares - _sharesAmount` checked above in line:
/// 512: require(
      _sharesAmount <= currentSenderShares,
      "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
    );
517: shares[_sender] = currentSenderShares - _sharesAmount;
/// @audit - mathematical operation `accountShares - _sharesAmount` checked above in line:
/// 563: require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE");
567: shares[_account] = accountShares - _sharesAmount;
```
[285](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L285) | [337](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L337) | [517](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L517) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L567)
</details>

### [G-31] Using `private` rather than `public`, saves gas

Public storage variables increase the contract's size due to the implicit generation of public getter functions. 
This makes the contract larger and could increase deployment and interaction costs.

If you do not require other contracts to read these variables, consider making them `private`. 

Example:
```solidity
/// 145426 gas to deploy
contract PublicState {
    address public first;
    address public second;
}
/// 77126 gas to deploy
contract PrivateState {
    address private first;
    address private second;
}
```

<details>
<summary><i>33 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

57: bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
60: bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
63: uint256 public constant MINIMUM_OUSG_PRICE = 105e18;
66: uint256 public constant FEE_GRANULARITY = 10_000;
69: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
72: IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;
75: IRWALike public immutable ousg;
78: ROUSG public immutable rousg;
81: IERC20 public immutable buidl;
84: IBUIDLRedeemer public immutable buidlRedeemer;
87: uint256 public immutable decimalsMultiplier;
90: address public immutable usdcReceiver;
93: IRWAOracle public oracle;
96: address public feeReceiver;
99: uint256 public mintFee = 0;
102: uint256 public redeemFee = 0;
106: uint256 public minimumDepositAmount = 100_000e6;
110: uint256 public minimumRedemptionAmount = 50_000e6;
113: bool public mintPaused;
116: bool public redeemPaused;
120: uint256 public minBUIDLRedeemAmount = 250_000e6;
123: IInvestorBasedRateLimiter public investorBasedRateLimiter;
```
[57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57) | [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60) | [63](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L63) | [66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66) | [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69) | [72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72) | [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L75) | [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L78) | [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L81) | [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L84) | [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L87) | [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90) | [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L93) | [96](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L96) | [99](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L99) | [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L102) | [106](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L106) | [110](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L110) | [113](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L113) | [116](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L116) | [120](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L120) | [123](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L123)

```solidity
File: contracts/ousg/rOUSG.sol

81: IRWAOracle public oracle;
84: IERC20 public ousg;
87: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
93: bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
94: bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
95: bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```
[81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L81) | [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L84) | [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87) | [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L93) | [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94) | [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)

```solidity
File: contracts/ousg/rOUSGFactory.sol

38: bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
41: ROUSG public rOUSGImplementation;
42: ProxyAdmin public rOUSGProxyAdmin;
43: TokenProxy public rOUSGProxy;
45: bool public initialized = false;
```
[38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38) | [41](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L41) | [42](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L42) | [43](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L43) | [45](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45)
</details>

### [G-32] Refactor duplicated require()/revert() checks to save gas

Duplicate require()/revert() checks can be refactored into a modifier or function, saving deployment costs.

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

434: if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
      revert UnwrapTooSmall();
629: if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
      revert UnwrapTooSmall();
```
[434](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L434) | [629](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L629)
</details>

### [G-33] Use Assembly for Efficient Memory Management in Multiple External Calls

When making multiple external calls in a Solidity contract, it may be more efficient to use inline assembly to reuse the memory space allocated for function arguments and return data.
This can prevent unnecessary memory expansion and reduce gas costs.

Example:
```solidity
contract Solidity {
    // cost: 7262
    function call(address calledAddress) external pure returns(uint256) {
        Called called = Called(calledAddress);
        uint256 res1 = called.add(1, 2);
        uint256 res2 = called.add(3, 4);

        uint256 res = res1 + res2;
        return res;
    }
}

contract Assembly {
    // cost: 5281
    function call(address calledAddress) external view returns(uint256) {
        assembly {
            // check that calledAddress has code deployed to it
            if iszero(extcodesize(calledAddress)) {
                revert(0x00, 0x00)
            }

            // first call
            mstore(0x00, hex"771602f7")
            mstore(0x04, 0x01)
            mstore(0x24, 0x02)
            let success := staticcall(gas(), calledAddress, 0x00, 0x44, 0x60, 0x20)
            if iszero(success) {
                revert(0x00, 0x00)
            }
            let res1 := mload(0x60)

            // second call
            mstore(0x04, 0x03)
            mstore(0x24, 0x4)
            success := staticcall(gas(), calledAddress, 0x00, 0x44, 0x60, 0x20)
            if iszero(success) {
                revert(0x00, 0x00)
            }
            let res2 := mload(0x60)

            // add results
            let res := add(res1, res2)

            // return data
            mstore(0x60, res)
            return(0x60, 0x20)
        }
    }
}
```

<details>
<summary><i>15 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit function `mintRebasingOUSG()` has multiple external calls
264: ousg.approve(address(rousg), ousgAmountOut);
265: rousg.wrap(ousgAmountOut);
266: rousgAmountOut = rousg.getROUSGByShares(
      ousgAmountOut * OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
/// @audit function `_mint()` has multiple external calls
292: investorBasedRateLimiter.checkAndUpdateMintLimit(
        msg.sender,
        usdcAmountIn
      );
299: usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    );
/// @audit function `redeemRebasingOUSG()` has multiple external calls
372: rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    );
376: rousg.unwrap(rousgAmountIn);
377: uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /
      OUSG_TO_ROUSG_SHARES_MULTIPLIER;
/// @audit function `_redeem()` has multiple external calls
409: investorBasedRateLimiter.checkAndUpdateRedeemLimit(
        msg.sender,
        usdcAmountToRedeem
      );
424: uint256 usdcBalance = usdc.balanceOf(address(this));
/// @audit function `_redeemBUIDL()` has multiple external calls
460: buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
463: uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
464: buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
465: buidlRedeemer.redeem(buidlAmountToRedeem);
467: usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
```
[264](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L264) | [265](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L265) | [266](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L266) | [292](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L292) | [299](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L299) | [372](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L372) | [376](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L376) | [377](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L377) | [409](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L409) | [424](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L424) | [460](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L460) | [463](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L463) | [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L464) | [465](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L465) | [467](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L467)
</details>

### [G-34] Optimize `require/revert` Statements with Assembly

Using inline assembly for revert statements in Solidity can offer gas optimizations.
The typical `require` or `revert` statements in Solidity perform additional memory operations and type checks which can be avoided by using low-level assembly code.

In certain contracts, particularly those that might revert often or are otherwise sensitive to gas costs, using assembly to handle reversion can offer meaningful savings.
These savings primarily come from avoiding memory expansion costs and extra type checks that the Solidity compiler performs.

Example:
```solidity
/// calling restrictedAction(2) with a non-owner address: 24042
function restrictedAction(uint256 num)  external {
    require(owner == msg.sender, "caller is not owner");
    specialNumber = num;
}

// calling restrictedAction(2) with a non-owner address: 23734
function restrictedAction(uint256 num)  external {
    assembly {
        if sub(caller(), sload(owner.slot)) {
            mstore(0x00, 0x20) // store offset to where length of revert message is stored
            mstore(0x20, 0x13) // store length (19)
            mstore(0x40, 0x63616c6c6572206973206e6f74206f776e657200000000000000000000000000) // store hex representation of message
            revert(0x00, 0x60) // revert with data
        }
    }
    specialNumber = num;
}
```

<details>
<summary><i>50 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

163: require(
      address(_usdc) != address(0),
      "OUSGInstantManager: USDC cannot be 0x0"
    );
167: require(
      address(_usdcReciever) != address(0),
      "OUSGInstantManager: USDC Receiver cannot be 0x0"
    );
171: require(
      address(_feeReceiver) != address(0),
      "OUSGInstantManager: feeReceiver cannot be 0x0"
    );
175: require(
      address(_ousgOracle) != address(0),
      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
    );
179: require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180: require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181: require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
182: require(
      address(_buidlRedeemer) != address(0),
      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    );
186: require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    );
190: require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    );
205: require(
      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
    );
282: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_mint: USDC decimals must be 6"
    );
286: require(
      usdcAmountIn >= minimumDepositAmount,
      "OUSGInstantManager::_mint: Deposit amount too small"
    );
298: require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    );
310: require(
      ousgAmountOut > 0,
      "OUSGInstantManager::_mint: net mint amount can't be zero"
    );
344: require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    );
371: require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    );
391: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_redeem: USDC decimals must be 6"
    );
395: require(
      IERC20Metadata(address(buidl)).decimals() == 6,
      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    );
402: require(
      usdcAmountToRedeem >= minimumRedemptionAmount,
      "OUSGInstantManager::_redeem: Redemption amount too small"
    );
417: require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    );
459: require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
466: require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
481: require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
557: require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
570: require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
584: require(
      _minimumDepositAmount >= FEE_GRANULARITY,
      "setMinimumDepositAmount: Amount too small"
    );
602: require(
      _minimumRedemptionAmount >= FEE_GRANULARITY,
      "setMinimumRedemptionAmount: Amount too small"
    );
653: require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
757: require(!mintPaused, "OUSGInstantManager: Mint paused");
763: require(!redeemPaused, "OUSGInstantManager: Redeem paused");
808: require(success, "Call Failed");
```
[163](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L163) | [167](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L167) | [171](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L171) | [175](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L175) | [179](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L179) | [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L180) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L181) | [182](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L182) | [186](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L186) | [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L190) | [205](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L205) | [282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L282) | [286](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L286) | [298](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L298) | [310](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310) | [344](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L344) | [371](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L371) | [391](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L391) | [395](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L395) | [402](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L402) | [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L417) | [459](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L459) | [466](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L466) | [481](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L481) | [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557) | [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570) | [584](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L584) | [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602) | [653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L653) | [757](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L757) | [763](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L763) | [808](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L808)

```solidity
File: contracts/ousg/rOUSG.sol

282: require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");
333: require(
      currentAllowance >= _subtractedValue,
      "DECREASED_ALLOWANCE_BELOW_ZERO"
    );
416: require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");
432: require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
477: require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");
478: require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");
506: require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");
507: require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");
512: require(
      _sharesAmount <= currentSenderShares,
      "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
    );
533: require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");
558: require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS");
563: require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE");
594: require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");
599: require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd");
604: require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd");
```
[282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L282) | [333](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L333) | [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416) | [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432) | [477](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L477) | [478](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L478) | [506](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506) | [507](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L507) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L512) | [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533) | [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L558) | [563](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L563) | [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L599) | [604](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L604)

```solidity
File: contracts/ousg/rOUSGFactory.sol

76: require(!initialized, "ROUSGFactory: rOUSG already deployed");
129: require(success, "Call Failed");
150: require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");
```
[76](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L76) | [129](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L129) | [150](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L150)
</details>

### [G-35] Use Cached Contracts for Multiple External Calls

When function makes multiple calls to the same external contract, it is more gas-efficient to use a local copy of the contract.
This is because the EVM will cache the contract in memory, and subsequent calls will be cheaper.
It's especially true for contracts that are large and/or have many functions.
```solidity
    // local cache -> 6561 gas
    IToken localCache = storageContract;
    localCache.externalCall();
    localCache.externalCall();

    // direct call 6683 gas
    storageContract.externalCall();
    storageContract.externalCall();
```

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit function deployRebasingOUSG() make external call of `rOUSGProxyAdmin` - 2 times
93: rOUSGProxyAdmin.transferOwnership(guardian);
94: assert(rOUSGProxyAdmin.owner() == guardian);
```
[93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L93) | [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94)
</details>

### [G-36] Consider using solady's `FixedPointMathLib`

Utilizing gas-optimized math functions from libraries like [Solady](https://github.com/Vectorized/solady/blob/main/src/utils/FixedPointMathLib.sol) can lead to more efficient smart contracts.
This is particularly beneficial in contracts where these operations are frequently used.

<details>
<summary><i>31 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

267: ousgAmountOut * OUSG_TO_ROUSG_SHARES_MULTIPLIER
689: uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;
703: uint256 amountE36 = ousgAmountBurned * price;
716: return (usdcAmount * mintFee) / FEE_GRANULARITY;
728: return (usdcAmount * redeemFee) / FEE_GRANULARITY;
738: return amount * decimalsMultiplier;
217: Mint/Redeem
377: uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /
      OUSG_TO_ROUSG_SHARES_MULTIPLIER;
547: Mint/Redeem Configuration
690: ousgAmountOut = amountE36 / price;
704: usdcOwed = _scaleDown(amountE36 / 1e18);
716: return (usdcAmount * mintFee) / FEE_GRANULARITY;
728: return (usdcAmount * redeemFee) / FEE_GRANULARITY;
748: return amount / decimalsMultiplier;
752: Pause/Unpause
203: 10 **
        (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());
```
[267](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L267) | [689](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L689) | [703](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L703) | [716](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L716) | [728](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L728) | [738](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L738) | [217](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L217) | [377](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L377) | [547](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L547) | [690](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L690) | [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704) | [716](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L716) | [728](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L728) | [748](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L748) | [752](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L752) | [203](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L203)

```solidity
File: contracts/ousg/rOUSG.sol

190: (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
190: (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
201: (_sharesOf(_account) * getOUSGPrice()) /
202: (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
367: (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
367: (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
375: (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
375: (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
417: uint256 ousgSharesAmount = _OUSGAmount * OUSG_TO_ROUSG_SHARES_MULTIPLIER;
190: (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
201: (_sharesOf(_account) * getOUSGPrice()) /
      (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
367: (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
375: (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
439: ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
636: ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
```
[190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L190) | [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L190) | [201](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L201) | [202](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L202) | [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367) | [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L375) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L375) | [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L417) | [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L190) | [201](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L201) | [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L375) | [439](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L439) | [636](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L636)
</details>

### [G-37] Avoid Zero to Non-Zero Storage Writes Where Possible

Changing a storage variable from zero to non-zero costs 22,100 gas in total. (20,000 gas for a zero to non-zero write and 2,100 for a cold storage access)
Consider using non-zero architecture to avoid high gas costs for zero to non-zero storage writes.

Example:

```solidity
- uint256 public counter = 0;  // rewrite this costs more
+ uint256 public counter = 1;  // rewrite this costs less
```

<details>
<summary><i>14 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

559: mintFee = _mintFee;
572: redeemFee = _redeemFee;
590: minimumDepositAmount = _minimumDepositAmount;
610: minimumRedemptionAmount = _minimumRedemptionAmount;
629: minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
769: mintPaused = true;
775: mintPaused = false;
781: redeemPaused = true;
787: redeemPaused = false;
```
[559](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L559) | [572](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L572) | [590](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L590) | [610](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L610) | [629](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L629) | [769](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L769) | [775](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L775) | [781](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L781) | [787](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L787)

```solidity
File: contracts/ousg/rOUSG.sol

517: shares[_sender] = currentSenderShares - _sharesAmount;
518: shares[_recipient] = shares[_recipient] + _sharesAmount;
565: totalShares -= _sharesAmount;
567: shares[_account] = accountShares - _sharesAmount;
```
[517](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L517) | [518](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L518) | [565](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L565) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L567)

```solidity
File: contracts/ousg/rOUSGFactory.sol

95: initialized = true;
```
[95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L95)
</details>

### [G-38] Avoid Unnecessary Gas Usage with Shorter `require()/revert()` Strings

Long require() or revert() strings that exceed 32 bytes can lead to extra gas costs.

This unnecessary gas consumption can be avoided by ensuring your `require()` or `revert()` strings are 32 bytes or shorter.
This optimizes your contract's gas efficiency without compromising the clarity and specificity of your error messages.

<details>
<summary><i>35 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

163: require(
      address(_usdc) != address(0),
      "OUSGInstantManager: USDC cannot be 0x0"
    );
167: require(
      address(_usdcReciever) != address(0),
      "OUSGInstantManager: USDC Receiver cannot be 0x0"
    );
171: require(
      address(_feeReceiver) != address(0),
      "OUSGInstantManager: feeReceiver cannot be 0x0"
    );
175: require(
      address(_ousgOracle) != address(0),
      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
    );
179: require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180: require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181: require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
182: require(
      address(_buidlRedeemer) != address(0),
      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    );
186: require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    );
190: require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    );
205: require(
      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
    );
282: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_mint: USDC decimals must be 6"
    );
286: require(
      usdcAmountIn >= minimumDepositAmount,
      "OUSGInstantManager::_mint: Deposit amount too small"
    );
298: require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    );
310: require(
      ousgAmountOut > 0,
      "OUSGInstantManager::_mint: net mint amount can't be zero"
    );
344: require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    );
371: require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    );
391: require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_redeem: USDC decimals must be 6"
    );
395: require(
      IERC20Metadata(address(buidl)).decimals() == 6,
      "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
    );
402: require(
      usdcAmountToRedeem >= minimumRedemptionAmount,
      "OUSGInstantManager::_redeem: Redemption amount too small"
    );
417: require(
      usdcAmountOut > 0,
      "OUSGInstantManager::_redeem: redeem amount can't be zero"
    );
459: require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
466: require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
481: require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
557: require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
570: require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
584: require(
      _minimumDepositAmount >= FEE_GRANULARITY,
      "setMinimumDepositAmount: Amount too small"
    );
602: require(
      _minimumRedemptionAmount >= FEE_GRANULARITY,
      "setMinimumRedemptionAmount: Amount too small"
    );
763: require(!redeemPaused, "OUSGInstantManager: Redeem paused");
```
[163](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L163) | [167](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L167) | [171](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L171) | [175](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L175) | [179](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L179) | [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L180) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L181) | [182](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L182) | [186](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L186) | [190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L190) | [205](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L205) | [282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L282) | [286](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L286) | [298](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L298) | [310](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310) | [344](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L344) | [371](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L371) | [391](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L391) | [395](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L395) | [402](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L402) | [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L417) | [459](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L459) | [466](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L466) | [481](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L481) | [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557) | [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570) | [584](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L584) | [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602) | [763](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L763)

```solidity
File: contracts/ousg/rOUSG.sol

282: require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");
416: require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");
432: require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
594: require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");
```
[282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L282) | [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416) | [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432) | [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594)

```solidity
File: contracts/ousg/rOUSGFactory.sol

76: require(!initialized, "ROUSGFactory: rOUSG already deployed");
150: require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");
```
[76](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L76) | [150](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L150)
</details>

### [G-39] Use `unchecked` for division which do not divide by -X sonce they can't overflow

Solidity introduced the `unchecked` block in version 0.8.0 as a measure to provide control over arithmetic operations. 
Any operation inside this block will not trigger the built-in overflow and underflow checks, thus saving gas costs. 
Since a division operation between two `uint`s (unsigned integers) can never result in an overflow or underflow, it's an ideal candidate for the use of `unchecked {}` block.
This practice enables optimal gas usage without risking any arithmetic anomalies.

<details>
<summary><i>12 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

377: uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /
      OUSG_TO_ROUSG_SHARES_MULTIPLIER;
690: ousgAmountOut = amountE36 / price;
704: usdcOwed = _scaleDown(amountE36 / 1e18);
716: return (usdcAmount * mintFee) / FEE_GRANULARITY;
728: return (usdcAmount * redeemFee) / FEE_GRANULARITY;
748: return amount / decimalsMultiplier;
```
[377](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L377) | [690](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L690) | [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704) | [716](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L716) | [728](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L728) | [748](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L748)

```solidity
File: contracts/ousg/rOUSG.sol

190: (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
201: (_sharesOf(_account) * getOUSGPrice()) /
      (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
367: (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
375: (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
439: ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
636: ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
```
[190](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L190) | [201](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L201) | [367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L375) | [439](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L439) | [636](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L636)
</details>

### [G-40] Use solady library where possible to save gas

The following OpenZeppelin imports have a Solady equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible.

<details>
<summary><i>11 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

17: import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";
19: import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";
20: import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";
```
[17](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L17) | [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L19) | [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L20)

```solidity
File: contracts/ousg/rOUSG.sol

17: import "contracts/external/openzeppelin/contracts/token/IERC20.sol";
19: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";
20: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";
21: import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";
22: import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";
23: import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";
24: import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";
```
[17](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L17) | [19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L19) | [20](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L20) | [21](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L21) | [22](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L22) | [23](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L23) | [24](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L24)

```solidity
File: contracts/ousg/rOUSGFactory.sol

19: import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";
```
[19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19)
</details>

### [G-41] Use `uint256(1)`/`uint256(2)` instead of `true`/`false` to save gas for changes

Boolean variables in Solidity are more expensive than `uint256` or any type that takes up a full word, due to additional gas costs associated with write operations.
When using boolean variables, each write operation emits an extra SLOAD to read the slot's contents, replace the bits taken up by the boolean, and then write back.
This process cannot be disabled and leads to extra gas consumption.

By using `uint256(1)` and `uint256(2)` for representing true and false states, you can avoid a `Gwarmaccess` (100 gas) cost and also avoid a `Gsset` (20000 gas) cost when changing from `false` to `true`, after having been `true` in the past.
This approach helps in optimizing gas usage, making your contract more cost-effective.

[Usage in OpenZeppelin ReentrancyGuard.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27)

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

113: bool public mintPaused;
116: bool public redeemPaused;
```
[113](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L113) | [116](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L116)

```solidity
File: contracts/ousg/rOUSGFactory.sol

45: bool public initialized = false;
```
[45](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45)
</details>

### [G-42] Mark Functions That Revert For Normal Users As `payable`

Functions guaranteed to revert when called by normal users can be marked `payable`.
If a function modifier such as onlyOwner is used, the function will revert if a normal user tries to pay the function.
Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.

The extra opcodes avoided are CALLVALUE(2),DUP1(3),ISZERO(3),PUSH2(3),JUMPI(10),PUSH1(3),DUP1(3),REVERT(0),JUMPDEST(1),POP(2), which costs an average of about 21 gas per call to the function, in addition to the extra deployment cost.

<details>
<summary><i>28 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

498: function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
512: function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
526: function setInstantMintLimitDuration(
    uint256 _instantMintLimitDuration
  ) external override onlyRole(CONFIGURER_ROLE) {
540: function setInstantRedemptionLimitDuration(
    uint256 _instantRedemptionLimitDuratioin
  ) external override onlyRole(CONFIGURER_ROLE) {
554: function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
567: function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {
581: function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
599: function setMinimumRedemptionAmount(
    uint256 _minimumRedemptionAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
622: function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
638: function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
650: function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
663: function setInvestorBasedRateLimiter(
    address _investorBasedRateLimiter
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
768: function pauseMint() external onlyRole(PAUSER_ROLE) {
774: function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {
780: function pauseRedeem() external onlyRole(PAUSER_ROLE) {
786: function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {
794: function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
819: function retrieveTokens(
    address token,
    address to,
    uint256 amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
```
[498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498) | [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512) | [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526) | [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554) | [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567) | [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581) | [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599) | [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622) | [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638) | [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650) | [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663) | [768](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L768) | [774](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L774) | [780](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L780) | [786](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L786) | [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794) | [819](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819)

```solidity
File: contracts/ousg/rOUSG.sol

111: function __rOUSG_init(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
127: function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
613: function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
624: function burn(
    address _account,
    uint256 _amount
  ) external onlyRole(BURNER_ROLE) {
641: function pause() external onlyRole(PAUSER_ROLE) {
645: function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
649: function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
655: function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE) {
```
[111](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L111) | [127](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L127) | [613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613) | [624](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624) | [641](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L641) | [645](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L645) | [649](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L649) | [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L655)

```solidity
File: contracts/ousg/rOUSGFactory.sol

70: function deployRebasingOUSG(
    address kycRegistry,
    uint256 requirementGroup,
    address ousg,
    address oracle
  ) external onlyGuardian returns (address, address, address) {
121: function multiexcall(
    ExCallData[] calldata exCallData
  ) external payable override onlyGuardian returns (bytes[] memory results) {
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70) | [121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121)
</details>

### [G-43] Prefer `private` over `public` for Constants to Save Gas

Using `private` instead of `public` for constants can save gas.

The compiler doesn't need to create non-payable getter functions for deployment calldata, store the bytes of the value outside of where it's used, or add another entry to the method ID table, saving 3406-3606 gas in deployment.

If needed, the values can be read from the verified contract source code, or a single getter function that returns a tuple of the values of all currently public constants can be implemented.

<details>
<summary><i>10 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

57: bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
60: bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
63: uint256 public constant MINIMUM_OUSG_PRICE = 105e18;
66: uint256 public constant FEE_GRANULARITY = 10_000;
69: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
```
[57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57) | [60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60) | [63](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L63) | [66](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66) | [69](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69)

```solidity
File: contracts/ousg/rOUSG.sol

87: uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;
93: bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
94: bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
95: bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```
[87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87) | [93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L93) | [94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94) | [95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)

```solidity
File: contracts/ousg/rOUSGFactory.sol

38: bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```
[38](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38)
</details>

### [G-44] `<x> += <y>` costs more gas than `<x> = <x> + <y>` for state variables

Using the addition operator instead of plus-equals saves gas.
Replace `<x> += <y>` or `<x> -= <y>` with `<x> = <x> + <y>` or `<x> = <x> - <y>`.

<details>
<summary><i>2 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

537: totalShares += _sharesAmount;
565: totalShares -= _sharesAmount;
```
[537](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L537) | [565](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L565)
</details>

### [G-45] Using `bool`s for storage incurs overhead

Utilizing booleans for storage is less gas-efficient compared to using types that consume a full word like uint256.
Every write operation on a boolean necessitates an extra SLOAD operation to read the slot's current value, modify the boolean bits, and then write back.
This additional step is the compiler's measure against contract upgrades and pointer aliasing.

To enhance gas efficiency, consider using `uint256(0)` for false and `uint256(1)` for true, bypassing the extra Gwarmaccess (100 gas) incurred by the SLOAD.

<details>
<summary><i>3 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

113: bool public mintPaused;
116: bool public redeemPaused;
```
[113](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L113) | [116](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L116)

```solidity
File: contracts/ousg/rOUSGFactory.sol

45: bool public initialized = false;
```
[45](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45)
</details>

### [G-46] Optimize Gas by Using Only Named Returns

The Solidity compiler can generate more efficient bytecode when using named returns.
It's recommended to replace anonymous returns with named returns for potential gas savings.

Example:
```solidity
/// 985 gas cost
function add(uint256 x, uint256 y) public pure returns (uint256) {
    return x + y;
}
/// 941 gas cost
function addNamed(uint256 x, uint256 y) public pure returns (uint256 res) {
    res = x + y;
}
```

<details>
<summary><i>24 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

713: function _getInstantMintFees(
    uint256 usdcAmount
  ) internal view returns (uint256) {
725: function _getInstantRedemptionFees(
    uint256 usdcAmount
  ) internal view returns (uint256) {
737: function _scaleUp(uint256 amount) internal view returns (uint256) {
747: function _scaleDown(uint256 amount) internal view returns (uint256) {
```
[713](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L713) | [725](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L725) | [737](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L737) | [747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L747)

```solidity
File: contracts/ousg/rOUSG.sol

166: function name() public pure returns (string memory) {
174: function symbol() public pure returns (string memory) {
181: function decimals() public pure returns (uint8) {
188: function totalSupply() public view returns (uint256) {
199: function balanceOf(address _account) public view returns (uint256) {
220: function transfer(address _recipient, uint256 _amount) public returns (bool) {
231: function allowance(
    address _owner,
    address _spender
  ) public view returns (uint256) {
251: function approve(address _spender, uint256 _amount) public returns (bool) {
276: function transferFrom(
    address _sender,
    address _recipient,
    uint256 _amount
  ) public returns (bool) {
302: function increaseAllowance(
    address _spender,
    uint256 _addedValue
  ) public returns (bool) {
328: function decreaseAllowance(
    address _spender,
    uint256 _subtractedValue
  ) public returns (bool) {
347: function getTotalShares() public view returns (uint256) {
356: function sharesOf(address _account) public view returns (uint256) {
363: function getSharesByROUSG(
    uint256 _rOUSGAmount
  ) public view returns (uint256) {
373: function getROUSGByShares(uint256 _shares) public view returns (uint256) {
397: function transferShares(
    address _recipient,
    uint256 _sharesAmount
  ) public returns (uint256) {
487: function _sharesOf(address _account) internal view returns (uint256) {
529: function _mintShares(
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
554: function _burnShares(
    address _account,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
```
[166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L166) | [174](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L174) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L181) | [188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188) | [199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L199) | [220](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L220) | [231](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L231) | [251](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L251) | [276](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L276) | [302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302) | [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328) | [347](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L347) | [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356) | [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363) | [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373) | [397](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397) | [487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L487) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529) | [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554)

```solidity
File: contracts/ousg/rOUSGFactory.sol

70: function deployRebasingOUSG(
    address kycRegistry,
    uint256 requirementGroup,
    address ousg,
    address oracle
  ) external onlyGuardian returns (address, address, address) {
```
[70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70)
</details>

### [G-47] Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead

Usage of uints/ints smaller than 32 bytes (256 bits) incurs overhead. The Ethereum Virtual Machine (EVM) operates on 32 bytes at a time. Therefore, if an element is smaller than 32 bytes, the EVM must use more operations to reduce the size of the element from 32 bytes to the desired size. 

Operations involving smaller size uints/ints cost extra gas due to the compiler having to clear the higher bits of the memory word before operating on the small size integer. This also includes the associated stack operations of doing so. 

It's recommended to use larger sizes and downcast where needed to optimize for gas efficiency.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

181: function decimals() public pure returns (uint8) {
```
[181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L181)
</details>

### [G-48] Unlimited gas consumption risk due to external call recipients

When calling an external function without specifying a gas limit , the called contract may consume all the remaining gas, causing the tx to be reverted.
To mitigate this, it is recommended to explicitly set a gas limit when making low level external calls.

<details>
<summary><i>2 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

805: (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
```
[805](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805)

```solidity
File: contracts/ousg/rOUSGFactory.sol

126: (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
```
[126](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126)
</details>

### [G-49] Use assembly to check for `address(0)`

The usage of inline assembly to check if variable is the zero can save gas compared to traditional `require` or `if` statement checks. 

The assembly check uses the `extcodesize` operation which is generally cheaper in terms of gas.

[More information can be found here.](https://medium.com/@kalexotsu/solidity-assembly-checking-if-an-address-is-0-efficiently-d2bfe071331)

<details>
<summary><i>19 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

163: require(
      address(_usdc) != address(0),
      "OUSGInstantManager: USDC cannot be 0x0"
    );
167: require(
      address(_usdcReciever) != address(0),
      "OUSGInstantManager: USDC Receiver cannot be 0x0"
    );
171: require(
      address(_feeReceiver) != address(0),
      "OUSGInstantManager: feeReceiver cannot be 0x0"
    );
175: require(
      address(_ousgOracle) != address(0),
      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
    );
179: require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180: require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181: require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
182: require(
      address(_buidlRedeemer) != address(0),
      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    );
291: if (address(investorBasedRateLimiter) != address(0)) {
      investorBasedRateLimiter.checkAndUpdateMintLimit(
        msg.sender,
        usdcAmountIn
      );
408: if (address(investorBasedRateLimiter) != address(0)) {
      investorBasedRateLimiter.checkAndUpdateRedeemLimit(
        msg.sender,
        usdcAmountToRedeem
      );
653: require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
```
[163](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L163) | [167](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L167) | [171](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L171) | [175](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L175) | [179](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L179) | [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L180) | [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L181) | [182](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L182) | [291](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L291) | [408](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L408) | [653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L653)

```solidity
File: contracts/ousg/rOUSG.sol

477: require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");
478: require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");
506: require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");
507: require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");
533: require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");
558: require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS");
597: if (from != address(0)) {
      // If not minting
      require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd");
602: if (to != address(0)) {
      // If not burning
      require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd");
```
[477](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L477) | [478](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L478) | [506](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506) | [507](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L507) | [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533) | [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L558) | [597](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L597) | [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L602)
</details>

### [G-50] `internal`/`private` functions only called once can be inlined to save gas

`internal` functions that are only called once should be inlined to save gas. 
Not inlining such functions costs an extra 20 to 40 gas due to the additional `JUMP` instructions and stack operations required for function calls.

<details>
<summary><i>9 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit function `_getMintAmount()` called only once
685: function _getMintAmount(
    uint256 usdcAmountIn,
    uint256 price
  ) internal view returns (uint256 ousgAmountOut) {
/// @audit function `_getRedemptionAmount()` called only once
699: function _getRedemptionAmount(
    uint256 ousgAmountBurned,
    uint256 price
  ) internal view returns (uint256 usdcOwed) {
/// @audit function `_getInstantMintFees()` called only once
713: function _getInstantMintFees(
    uint256 usdcAmount
  ) internal view returns (uint256) {
/// @audit function `_getInstantRedemptionFees()` called only once
725: function _getInstantRedemptionFees(
    uint256 usdcAmount
  ) internal view returns (uint256) {
/// @audit function `_scaleUp()` called only once
737: function _scaleUp(uint256 amount) internal view returns (uint256) {
/// @audit function `_scaleDown()` called only once
747: function _scaleDown(uint256 amount) internal view returns (uint256) {
```
[685](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L685) | [699](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L699) | [713](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L713) | [725](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L725) | [737](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L737) | [747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L747)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit function `__rOUSG_init()` called only once
112: function __rOUSG_init(
    address _kycRegistry,
    uint256 requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
/// @audit function `__rOUSG_init_unchained()` called only once
128: function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
/// @audit function `_mintShares()` called only once
529: function _mintShares(
    address _recipient,
    uint256 _sharesAmount
  ) internal whenNotPaused returns (uint256) {
```
[112](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112) | [128](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529)
</details>

### [G-51] Consider using OZ EnumerateSet in place of nested mappings

Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).

A possible optimization involves manually concatenating the keys followed by a single hash operation and an sstore. However, this technique introduces the risk of storage collision, especially when there are other nested hash maps in the contract that use the same key types. Because Solidity is unaware of the number and structure of nested hash maps in a contract, it follows a conservative approach in computing the storage slot to avoid possible collisions.

OpenZeppelin's EnumerableSet provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios.

<details>
<summary><i>1 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/rOUSG.sol

75: mapping(address => mapping(address => uint256)) private allowances;
```
[75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75)
</details>

### [G-52] Declare `immutable` as `private` to save gas

Using `private` instead of `public` for immutables saves gas.

The compiler doesn't need to create non-payable getter functions for deployment calldata, store the bytes of the value outside of where it's used, or add another entry to the method ID table, saving 3406-3606 gas in deployment.

<details>
<summary><i>7 issue instances in 1 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

72: IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;
75: IRWALike public immutable ousg;
78: ROUSG public immutable rousg;
81: IERC20 public immutable buidl;
84: IBUIDLRedeemer public immutable buidlRedeemer;
87: uint256 public immutable decimalsMultiplier;
90: address public immutable usdcReceiver;
```
[72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72) | [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L75) | [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L78) | [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L81) | [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L84) | [87](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L87) | [90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90)
</details>

### [G-53] State variables should be cached in stack rather than re-reading them from storage

Caching state variables in local variables can optimize gas usage, as accessing the stack is cheaper than accessing storage.

The instances below point to the second+ access of a state variable within a function.

<details>
<summary><i>21 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit function _mint() uses state variable `feeReceiver` 2 times
317: usdc.transferFrom(msg.sender, feeReceiver, usdcfees);
321: emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);
/// @audit function _redeem() uses state variable `feeReceiver` 2 times
451: usdc.transfer(feeReceiver, usdcFees);
453: emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);
/// @audit function _redeem() uses state variable `minBUIDLRedeemAmount` 4 times
426: if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
434: _redeemBUIDL(minBUIDLRedeemAmount);
427: // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
438: usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
/// @audit function setMintFee() uses state variable `mintFee` 2 times
557: require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558: emit MintFeeSet(mintFee, _mintFee);
/// @audit function setRedeemFee() uses state variable `redeemFee` 2 times
570: require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571: emit RedeemFeeSet(redeemFee, _redeemFee);
```
[317](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L317) | [321](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L321) | [451](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L451) | [453](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L453) | [426](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L426) | [434](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L434) | [427](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L427) | [438](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L438) | [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557) | [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L558) | [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570) | [571](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L571)

```solidity
File: contracts/ousg/rOUSGFactory.sol

/// @audit function deployRebasingOUSG() uses state variable `rOUSGImplementation` 3 times
80: address(rOUSGImplementation),
80: address(rOUSGImplementation),
80: address(rOUSGImplementation),
/// @audit function deployRebasingOUSG() uses state variable `rOUSGProxyAdmin` 3 times
81: address(rOUSGProxyAdmin),
81: address(rOUSGProxyAdmin),
81: address(rOUSGProxyAdmin),
/// @audit function deployRebasingOUSG() uses state variable `rOUSGProxy` 3 times
84: ROUSG rOUSGProxied = ROUSG(address(rOUSGProxy));
97: address(rOUSGProxy),
97: address(rOUSGProxy),
```
[80](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L80) | [80](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L80) | [80](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L80) | [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L81) | [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L81) | [81](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L81) | [84](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L84) | [97](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L97) | [97](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L97)
</details>

### [G-54] Optimize names to save gas

Function names for public and external methods, as well as public state variable names, can be optimized to achieve gas savings.
By renaming functions to generate method IDs with two leading zero bytes, you can save 128 gas during contract deployment.
Further, renaming functions for lower method IDs can conserve 22 gas per call for each sorted position shifted.

Optimizing function names for gas efficiency can result in significant savings, especially for frequently called functions or heavily deployed contracts. 
Reference: [Solidity Gas Optimizations - Function Name](https://blog.emn178.cc/en/post/solidity-gas-optimization-function-name/)

<details>
<summary><i>3 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

49: contract OUSGInstantManager is
  ReentrancyGuard,
  InstantMintTimeBasedRateLimiter,
  AccessControlEnumerable,
  IOUSGInstantManager,
  IMulticall
{
```
[49](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49)

```solidity
File: contracts/ousg/rOUSG.sol

54: contract ROUSG is
  Initializable,
  ContextUpgradeable,
  PausableUpgradeable,
  AccessControlEnumerableUpgradeable,
  KYCRegistryClientUpgradeable,
  IERC20Upgradeable,
  IERC20MetadataUpgradeable
{
```
[54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54)

```solidity
File: contracts/ousg/rOUSGFactory.sol

37: contract ROUSGFactory is IMulticall {
```
[37](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37)
</details>

### [G-55] Avoid updating storage when the value hasn't changed

A check regarding whether the current value and the new value are the same should be added.
This helps prevent unnecessary state changes and events in case the new value is the same as the current value.

<details>
<summary><i>12 issue instances in 2 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

/// @audit Missing `_instantMintLimit` check before state change
501: _setInstantMintLimit(_instantMintLimit);
/// @audit Missing `_instantRedemptionLimit` check before state change
515: _setInstantRedemptionLimit(_instantRedemptionLimit);
/// @audit Missing `_instantMintLimitDuration` check before state change
529: _setInstantMintLimitDuration(_instantMintLimitDuration);
/// @audit Missing `_instantRedemptionLimitDuratioin` check before state change
543: _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
/// @audit Missing `_mintFee` check before state change
559: mintFee = _mintFee;
/// @audit Missing `_redeemFee` check before state change
572: redeemFee = _redeemFee;
/// @audit Missing `_minimumDepositAmount` check before state change
590: minimumDepositAmount = _minimumDepositAmount;
/// @audit Missing `_minimumRedemptionAmount` check before state change
610: minimumRedemptionAmount = _minimumRedemptionAmount;
/// @audit Missing `_minimumBUIDLRedemptionAmount` check before state change
629: minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
/// @audit Missing `_feeReceiver` check before state change
655: feeReceiver = _feeReceiver;
```
[501](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L501) | [515](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L515) | [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L529) | [543](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L543) | [559](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L559) | [572](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L572) | [590](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L590) | [610](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L610) | [629](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L629) | [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L655)

```solidity
File: contracts/ousg/rOUSG.sol

/// @audit Missing `registry` check before state change
653: _setKYCRegistry(registry);
/// @audit Missing `group` check before state change
659: _setKYCRequirementGroup(group);
```
[653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L653) | [659](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L659)
</details>

### [G-56] Optimize External Calls with Assembly for Memory Efficiency

Using interfaces to make external contract calls in Solidity is convenient but can be inefficient in terms of memory utilization.
Each such call involves creating a new memory location to store the data being passed, thus incurring memory expansion costs. 

Inline assembly allows for optimized memory usage by re-using already allocated memory spaces or using the scratch space for smaller datasets.
This can result in notable gas savings, especially for contracts that make frequent external calls.

Additionally, using inline assembly enables important safety checks like verifying if the target address has code deployed to it using `extcodesize(addr)` before making the call, mitigating risks associated with contract interactions.

<details>
<summary><i>30 issue instances in 3 files:</i></summary>

```solidity
File: contracts/ousg/ousgInstantManager.sol

264: ousg.approve(address(rousg), ousgAmountOut);
265: rousg.wrap(ousgAmountOut);
266: rousgAmountOut = rousg.getROUSGByShares(
      ousgAmountOut * OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
269: rousg.transfer(msg.sender, rousgAmountOut);
292: investorBasedRateLimiter.checkAndUpdateMintLimit(
        msg.sender,
        usdcAmountIn
      );
299: usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    );
317: usdc.transferFrom(msg.sender, feeReceiver, usdcfees);
319: usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
323: ousg.mint(to, ousgAmountOut);
345: ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    );
348: ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
372: rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    );
375: rousg.transferFrom(msg.sender, address(this), rousgAmountIn);
376: rousg.unwrap(rousgAmountIn);
377: uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /
      OUSG_TO_ROUSG_SHARES_MULTIPLIER;
409: investorBasedRateLimiter.checkAndUpdateRedeemLimit(
        msg.sender,
        usdcAmountToRedeem
      );
422: ousg.burn(ousgAmountIn);
424: uint256 usdcBalance = usdc.balanceOf(address(this));
451: usdc.transfer(feeReceiver, usdcFees);
455: usdc.transfer(msg.sender, usdcAmountOut);
460: buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
463: uint256 usdcBalanceBefore = usdc.balanceOf(address(this));
464: buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
465: buidlRedeemer.redeem(buidlAmountToRedeem);
467: usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
824: IERC20(token).transfer(to, amount);
```
[264](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L264) | [265](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L265) | [266](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L266) | [269](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L269) | [292](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L292) | [299](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L299) | [317](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L317) | [319](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L319) | [323](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L323) | [345](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L345) | [348](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L348) | [372](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L372) | [375](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L375) | [376](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L376) | [377](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L377) | [409](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L409) | [422](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L422) | [424](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L424) | [451](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L451) | [455](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L455) | [460](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L460) | [463](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L463) | [464](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L464) | [465](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L465) | [467](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L467) | [824](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L824)

```solidity
File: contracts/ousg/rOUSG.sol

419: ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
437: ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
634: ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
```
[419](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L419) | [437](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L437) | [634](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L634)

```solidity
File: contracts/ousg/rOUSGFactory.sol

93: rOUSGProxyAdmin.transferOwnership(guardian);
```
[93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L93)
</details>

