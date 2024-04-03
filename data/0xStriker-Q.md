# Summary



# Low Risk Issues    
| no    | Issue                                             | Instances |       |
| ----- | :------------------------------------------------ | :-------: | :---: |
| [L-1] | insufficient contract balance                     |     1     |
| [L-2] | no zero address checks                            |     7     |
| [L-3] | decimal checks should be moved to the constructor |     2     |


# Non-critical
| no     | Issue                                                                         | Instances |       |
| ------ | :---------------------------------------------------------------------------- | :-------: | :---: |
| [N-1]  | No need for check                                                             |     1     |
| [N-2]  | Consider moving to solidity version 0.8.18 or later                           |     3     |
| [N-3]  | consider using named imports                                                  |    23     |
| [N-4]  | Contract does not follow the Solidity style guide's suggested layout ordering |     3     |
| [N-5]  | functions are missing natspec descriptions                                    |    13     |
| [N-6]  | consider emitting an event at the end of the constructor                      |     2     |
| [N-7]  | event is missing indexed fields                                               |     1     |
| [N-8]  | consider using named mappings                                                 |     2     |
| [N-9]  | the code could be shortened                                                   |     4     |
| [N-10] | spell error in comments                                                       |     2     |
| [N-11] | should emit an event after redeeming buidl                                     |     1     |
| [N-12] | code vs comment difference                                                    |     1     |

## [L-1] insufficient contract balance 
in the _redeemBUIDL function there is this problem where if the buidlAmountToRedeem is suppose 300 the buidl balance of address(this) is 270 and the minBUIDLRedeemAmount is 250, the contract will attempt to redeem 300 tokens whilst having only 270 which will cause the function to fail because it tries to redeem more tokens than available. This oversight can lead to failed transactions and wasted gas fees. The contract should include logic to check its BUIDL balance against buidlAmountToRedeem and handle the case where the balance is insufficient.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L458-L470

## [L-2] no zero address checks 
the contracts does not provide checks for these address if they are zero

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L48
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L73-L74
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L131
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L133
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L145
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L639


## [L-3] decimal checks should be moved to the constructor
the _redeem() function, before redeeming, checks for the decimals of usdc and buidl to be 6 and if not, the function will revert. But this check needs to happen in the constructor of the contract because if suppose a value is set for usdc which doesn't have 6 decimals the redeeming operation will always fail, so if this check happens in the constructor then there will be no need for the _redeem() function to check for these values, and we will be sure that the decimals of these tokens are indeed 6 because they were checked in the constructor.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L392
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L396



## [N-1] No need for check 
this check in the redeem function after the fees is deducted from the value it checks if the usdcAmountOut is more than zero before proceeding to the next logic, but here is the thing no matter what the fee is after deduction the usdcAmountOut can never be zero, so this check is unrealistic and not needed. The max value for the fee can be 199 basis points and the minimumRedemptionAmount, which is already checked before checking if the usdcAmountOut is more than zero, and the minimumRedemptionAmount's value is always more than or equal to the FEE_GRANULARITY, who's value is 10000.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L418

## [N-2] Consider moving to solidity version 0.8.18 or later 
Upgrading to Solidity version 0.8.18 or later can provide access to the latest language features, optimizations, and security fixes, enhancing contract capabilities and robustness.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L16
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L16
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L16

## [N-3] consider using named imports
Using named imports in Solidity clarifies the origin of imported contracts or libraries, improving code readability and maintainability. It helps prevent naming conflicts and makes it easier to identify dependencies within the code base.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L18-L27
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L18-L26
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L19-L22

## [N-4] Contract does not follow the Solidity style guide's suggested layout ordering
The style guide says that, within a contract, the ordering should be 1) Type declarations, 2) State variables, 3) Events, 4) Errors 5) Modifiers, and 6) Functions, but the contract(s) below do not follow this ordering

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L1
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L1
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L1

## [N-5] functions are missing natspec descriptions 
functions listed below does not have natspec description, which is considered a good practice

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L47
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L149
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L102
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L112
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L128
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L642
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L646
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L650
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L656
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L278
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L388
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L458
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L794

## [N-6] consider emitting an event at the end of the constructor 

This will allow users to easily exactly pinpoint when and by whom a contract was constructed

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L144
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L47

## [N-7] event is missing indexed fields 

Index event fields make the field more quickly accessible to off-chain tools that parse events. This is especially useful when it comes to filtering based on an address. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Where applicable, each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three applicable fields, all of the applicable fields should be indexed.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L141

## [N-8] consider using named mappings 
Consider moving to solidity version 0.8.18 or later, and using named mappings to make it easier to understand the purpose of each mapping

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L72
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L75

## [N-9] the code could be shortened
the code below could be shortened
```solidity
shares[_sender] = currentSenderShares - _sharesAmount;
shares[_recipient] = shares[_recipient] + _sharesAmount;
```
to this 
```solidity
shares[_sender] -= _sharesAmount;
shares[_recipient] += _sharesAmount;
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L517-L518
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L539
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L567

## [N-10] spell error in comments
there are two spelling errors in comments, the word in the comment is "dicates" which should be "dictates"

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L494
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L508

## [N-11] should emit an event after redeeming buidl 
in the function _redeem() when buidl is redeemed no event is emitted

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L429

## [N-12] code vs comment difference 
in the below block of code which is in the ousgInstantManager contract, the code compares ousg decimals with rousg decimals, but in the comments of this code it says that ousg decimals must be equal to that of usdc, which is different from the code and should be fixed.
```solidity
require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    );
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L188

In another part of the contract ousgInstantManager in the function redeem(), the comment incorrectly suggests that OUSG is being redeemed for a specific amount of USDC, but the function actually takes an amount of OUSG as input and returns the corresponding amount of USDC
```solidity
/**
   * @notice Calculates fees and triggers a redemption of OUSG for a given amount of USDC
   *
   * @dev Please note that the fees are accumulated in `feeReceiver`
   *
   * @param ousgAmountIn Amount of OUSG to redeem
   *
   * @return usdcAmountOut The amount of USDC returned to the user
   */
  function redeem(
    uint256 ousgAmountIn
  )
    external
    override
    nonReentrant
    whenRedeemNotPaused
    returns (uint256 usdcAmountOut)
```
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L327