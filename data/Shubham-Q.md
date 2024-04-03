## Low Risk Issues

| |Issue|Instances|
|-|:-|:-:|
| [L-01](#L-01) | Initial minimum mint amount is high | 1 |

## Non-Critical Issues

| |Issue|Instances|
|-|:-|:-:|
| [NC-1](#NC-1) | Incorrect error message | 1 |
| [NC-2](#NC-2) | Contradicting comments in the scope of the contest | 1 |
| [NC-3](#NC-3) | `constructor` should emit an event | 2 |


## [L-01] Initial minimum mint amount is high

To mint either OUSG or rOUSG tokens, there is a minimum amount of usdc that the user should have. The initial minimum amount is set at `100_000e6` which is seems high for an average user.

```solidity
File: OUSGInstantManager

104:    // Minimum amount of USDC that must be deposited to mint OUSG or rOUSG
105:    // Denoted in 6 decimals for USDC
106:    uint256 public minimumDepositAmount = 100_000e6;
```
Although it can be set to a lower value calling `setMinimumDepositAmount()` but until that happens only a few users who can afford a minimum of 100k worth of usdc can only interact with the protocol. 

The major impact would be that only a few selected premium users can interact & hold OUSG & rOUSG tokens. 


## [N-01] Incorrect error message
Incoorect message will be displayed incase of an revert

```solidity
File: OUSGInstantManager

    require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"                
    ); 
```

### Recommendation

```solidity
File: OUSGInstantManager

    require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to rOUSG decimals"                
    ); 
```

## [N-02] Contradicting comments in the scope of the contest

Inside the contest page under **Main Invariants section**, the first point is 
> - OUSG & rOUSG can not be instant minted .

whereas under **New Code: Introduction to OUSGInstantManager**, it says
> This contract allows for instant mints and instant redemptions of OUSG and rOUSG.

Thus the invariant is broken because users can mint/redeem instantly as there is no constraint of time between calling the function & actually minting it.

*Although it was cleared up in the contest channel on Discord, just mentioning it here incase it is judged as a H/M.*

## [N-03] `constructor` should emit an event
Use events to signal significant changes to off-chain monitoring tools.

There are 2 instance(s) of this issue:

```solidity
File: ROUSGFactory
47:   constructor(address _guardian) {
```
```solidity
File: OUSGInstantManager
144:  constructor(
```