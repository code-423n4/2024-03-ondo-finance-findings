---
sponsor: "Ondo Finance"
slug: "2024-03-ondo-finance"
date: "2024-04-24"
title: "Ondo Finance"
findings: "https://github.com/code-423n4/2024-03-ondo-finance-findings/issues"
contest: 357
---

# Overview

## About C4

Code4rena (C4) is an open organization consisting of security researchers, auditors, developers, and individuals with domain expertise in smart contracts.

A C4 audit is an event in which community participants, referred to as Wardens, review, audit, or analyze smart contract logic in exchange for a bounty provided by sponsoring projects.

During the audit outlined in this document, C4 conducted an analysis of the Ondo Finance smart contract system written in Solidity. The audit took place between March 29 — April 3, 2024.

## Wardens

74 Wardens contributed reports to Ondo Finance:

  1. [asui](https://code4rena.com/@asui)
  2. [Breeje](https://code4rena.com/@Breeje)
  3. [immeas](https://code4rena.com/@immeas)
  4. [Arz](https://code4rena.com/@Arz)
  5. [HChang26](https://code4rena.com/@HChang26)
  6. [Limbooo](https://code4rena.com/@Limbooo)
  7. [Bigsam](https://code4rena.com/@Bigsam)
  8. [carrotsmuggler](https://code4rena.com/@carrotsmuggler)
  9. [radev\_sw](https://code4rena.com/@radev_sw)
  10. [dvrkzy](https://code4rena.com/@dvrkzy)
  11. [0xmystery](https://code4rena.com/@0xmystery)
  12. [0xCiphky](https://code4rena.com/@0xCiphky)
  13. [ZanyBonzy](https://code4rena.com/@ZanyBonzy)
  14. [popeye](https://code4rena.com/@popeye)
  15. [b0g0](https://code4rena.com/@b0g0)
  16. [Krace](https://code4rena.com/@Krace)
  17. [ni8mare](https://code4rena.com/@ni8mare)
  18. [ast3ros](https://code4rena.com/@ast3ros)
  19. [Shubham](https://code4rena.com/@Shubham)
  20. [kartik\_giri\_47538](https://code4rena.com/@kartik_giri_47538)
  21. [kaden](https://code4rena.com/@kaden)
  22. [Tychai0s](https://code4rena.com/@Tychai0s)
  23. [leegh](https://code4rena.com/@leegh)
  24. [yotov721](https://code4rena.com/@yotov721)
  25. [SpicyMeatball](https://code4rena.com/@SpicyMeatball)
  26. [0xDemon](https://code4rena.com/@0xDemon)
  27. [m4ttm](https://code4rena.com/@m4ttm)
  28. [JC](https://code4rena.com/@JC)
  29. [SAQ](https://code4rena.com/@SAQ)
  30. [zabihullahazadzoi](https://code4rena.com/@zabihullahazadzoi)
  31. [MaslarovK](https://code4rena.com/@MaslarovK)
  32. [cheatc0d3](https://code4rena.com/@cheatc0d3)
  33. [0xMosh](https://code4rena.com/@0xMosh)
  34. [OxTenma](https://code4rena.com/@OxTenma)
  35. [Stormreckson](https://code4rena.com/@Stormreckson)
  36. [samuraii77](https://code4rena.com/@samuraii77)
  37. [0xGreyWolf](https://code4rena.com/@0xGreyWolf)
  38. [Honour](https://code4rena.com/@Honour)
  39. [niser93](https://code4rena.com/@niser93)
  40. [Dots](https://code4rena.com/@Dots)
  41. [bareli](https://code4rena.com/@bareli)
  42. [grearlake](https://code4rena.com/@grearlake)
  43. [pkqs90](https://code4rena.com/@pkqs90)
  44. [slvDev](https://code4rena.com/@slvDev)
  45. [baz1ka](https://code4rena.com/@baz1ka)
  46. [0xJaeger](https://code4rena.com/@0xJaeger)
  47. [0xabhay](https://code4rena.com/@0xabhay)
  48. [0xlemon](https://code4rena.com/@0xlemon)
  49. [jaydhales](https://code4rena.com/@jaydhales)
  50. [0xAkira](https://code4rena.com/@0xAkira)
  51. [pfapostol](https://code4rena.com/@pfapostol)
  52. [btk](https://code4rena.com/@btk)
  53. [arnie](https://code4rena.com/@arnie)
  54. [Omik](https://code4rena.com/@Omik)
  55. [Abdessamed](https://code4rena.com/@Abdessamed)
  56. [EaglesSecurity](https://code4rena.com/@EaglesSecurity) ([julian\_avantgarde](https://code4rena.com/@julian_avantgarde) and [kane-goldmisth](https://code4rena.com/@kane-goldmisth))
  57. [oualidpro](https://code4rena.com/@oualidpro)
  58. [Aymen0909](https://code4rena.com/@Aymen0909)
  59. [0xweb3boy](https://code4rena.com/@0xweb3boy)
  60. [DanielArmstrong](https://code4rena.com/@DanielArmstrong)
  61. [FastChecker](https://code4rena.com/@FastChecker)
  62. [IceBear](https://code4rena.com/@IceBear)
  63. [igbinosuneric](https://code4rena.com/@igbinosuneric)
  64. [caglankaan](https://code4rena.com/@caglankaan)
  65. [VAD37](https://code4rena.com/@VAD37)
  66. [Aamir](https://code4rena.com/@Aamir)
  67. [nonn\_ac](https://code4rena.com/@nonn_ac)
  68. [DarkTower](https://code4rena.com/@DarkTower) ([0xrex](https://code4rena.com/@0xrex) and [haxatron](https://code4rena.com/@haxatron))
  69. [Tigerfrake](https://code4rena.com/@Tigerfrake)
  70. [dd0x7e8](https://code4rena.com/@dd0x7e8)
  71. [albahaca](https://code4rena.com/@albahaca)
  72. [K42](https://code4rena.com/@K42)

This audit was judged by [3docSec](https://code4rena.com/@3docsec).

Final report assembled by [thebrittfactor](https://twitter.com/brittfactorC4).

# Summary

The C4 analysis yielded an aggregated total of 5 unique vulnerabilities. Of these vulnerabilities, 1 received a risk rating in the category of HIGH severity and 4 received a risk rating in the category of MEDIUM severity.

Additionally, C4 analysis included 64 reports detailing issues with a risk rating of LOW severity or non-critical.

All of the issues presented here are linked back to their original finding.

# Scope

The code under review can be found within the [C4 Ondo Finance repository](https://github.com/code-423n4/2024-03-ondo-finance), and is composed of 3 smart contracts written in the Solidity programming language and includes 851 lines of Solidity code.

# Severity Criteria

C4 assesses the severity of disclosed vulnerabilities based on three primary risk categories: high, medium, and low/non-critical.

High-level considerations for vulnerabilities span the following key areas when conducting assessments:

- Malicious Input Handling
- Escalation of privileges
- Arithmetic
- Gas use

For more information regarding the severity criteria referenced throughout the submission review process, please refer to the documentation provided on [the C4 website](https://code4rena.com), specifically our section on [Severity Categorization](https://docs.code4rena.com/awarding/judging-criteria/severity-categorization).

# High Risk Findings (1)
## [[H-01] `OUSGInstantManager` will allow excessive `OUSG` token minting during `USDC` depeg event](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/278)
*Submitted by [Breeje](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/278), also found by [Arz](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/297), [HChang26](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/289), and [immeas](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/161)*

Any user can use `mint` function in `ousgInstantManager` contract to mint `OUSG` tokens by providing `USDC` token. It calls internal function `_mint` where the main logic resides.

```solidity

  function _mint(uint256 usdcAmountIn, address to) internal returns (uint256 ousgAmountOut) {
    
    // SNIP: Validation

    uint256 usdcfees = _getInstantMintFees(usdcAmountIn);
    uint256 usdcAmountAfterFee = usdcAmountIn - usdcfees;

    // Calculate the mint amount based on mint fees and usdc quantity
    uint256 ousgPrice = getOUSGPrice();
    ousgAmountOut = _getMintAmount(usdcAmountAfterFee, ousgPrice);

    require(ousgAmountOut > 0, "OUSGInstantManager::_mint: net mint amount can't be zero");

    // SNIP: Transfering USDC

    ousg.mint(to, ousgAmountOut);
  }
```

### Two important points to understand

**`OUSG` Price Stability:**

The contract depends on the `OUSG` price obtained from an oracle, which is heavily constrained (as per Readme) to ensure stability.

> `OUSG` Price - The `OUSG` price tracks an off chain portfolio of cash equivalents and treasury bills, price changes are heavily constrained in the `OUSG` Oracle, which uses the change in the price of SHV to set the allowable `OUSG` price in between updates. We are aware that the SHV price could differ from the `OUSG` portfolio, so any findings related to this price discrepancy is out of scope. Also, scenarios where the `OUSG` price increases by many orders of magnitudes are not realistic and consequently not considered valid.

As per `RWAOracleRateCheck` Oracle, constraints includes:

1. `OUSG` price updates restricted to once every `23 hours`.
2. Price deviations limited to a maximum of `1%`.

```solidity
      function setPrice(int256 newPrice) external onlyRole(SETTER_ROLE) {
        if (newPrice <= 0) {
          revert InvalidPrice();
        }
 @->    if (block.timestamp - priceTimestamp < MIN_PRICE_UPDATE_WINDOW) {
          revert PriceUpdateWindowViolation();
        }
 @->    if (_getPriceChangeBps(rwaPrice, newPrice) > MAX_CHANGE_DIFF_BPS) {
          revert DeltaDifferenceConstraintViolation();
        }

        // Set new price
        int256 oldPrice = rwaPrice;
        rwaPrice = newPrice;
        priceTimestamp = block.timestamp;

        emit RWAPriceSet(oldPrice, newPrice, block.timestamp);
      }
```

These constraints ensure relative stability of the `OUSG` price.

**Calculation Assumptions:**

The calculation of the amount of `OUSG` tokens to mint assumes a fixed conversion rate of `1 USDC = 1 USD`.

Key point: The `_getMintAmount` function calculates the `OUSG` amount based on the provided `USDC` amount and the `OUSG` price obtained from the oracle (by just upscaling and dividing).

```solidity
  function _getMintAmount(
    uint256 usdcAmountIn,
    uint256 price
  ) internal view returns (uint256 ousgAmountOut) {
    uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;
    ousgAmountOut = amountE36 / price;
  }
```

Here, there are no validation checks implemented regarding the current `USDC` price.

### Scenario of the issue

Consider Alice's attempt to mint `OUSG` tokens by providing `100,000 USDC`, assuming no minting fees and `OUSG` price of `105e18` `USD`. The calculation yields: `100_000e36 / 105e18` which is approximately `95_000e18` or `95_000` `OUSG` tokens for the `100_000` `USDC` provided.

However, in the event of a `USDC` depeg, where `USDC`'s value deviates from 1 `USD`:

- The contract's calculation logic remains unchanged.
- Despite the depeg, the `OUSG` price remains fairly constant (maximum 1% deviation allowed in 23 hours).

This scenario leads to Alice getting close to `95_000` `OUSG` tokens again for `100_000 USDC` provided. But this time, `100_000 USDC` can be worth as low as `87_000` `USD` if we take recent depeg event in March 2023, where `USDC` price went as low as 87 cents ([reference](https://decrypt.co/123211/usdc-stablecoin-depegs-90-cents-circle-exposure-silicon-valley-bank)).

This way, contract will allow users to mint excessive `OUSG` tokens during the depeg event.

### Impact

Minting of excessive token in case of `USDC` depeg.

### Tools Used

VS Code

### Recommended Mitigation Steps

Ideally, there needs to be an additional Oracle to check current price of `USDC` and take its price into the consideration when calculation `OUSG` tokens to mint.

### Assessed type

Context

**[3docSec (judge) increased severity to High and commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/278#issuecomment-2044628674):**
 > Upgraded as High because there is risk of value extraction from the protocol under conditions that can be monitored by an attacker.

**[cameronclifton (Ondo) confirmed, but disagreed with severity and commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/278#issuecomment-2052670415):**
 > After further review, we will be mitigating this by adding a Chainlink `USDC`/`USD` oracle to the `OUSGInstantManager` contract.  If the price is lower than what we are comfortable with, all mints and redemptions will be blocked. While we think it is unlikely that we won't be able to convert `USDC->USD` 1:1 in our backend systems, we decided to do this out of extreme caution.  

*Note: For full discussion, see [here](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/278).*

***

# Medium Risk Findings (4)
## [[M-01] Integration issue in `ousgInstantManager` with `BUIDL` if `minUSTokens` is set by blackrock](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/309)
*Submitted by [asui](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/309)*

Integration issues with `BUIDL`, in the case blackrock decides to set a minimum amount of `BUIDL` tokens that should be held by its holders.

### Proof of Concept

Blackrock implements a `minUSTokens;` variable where it sets a minimum amount to be held by the whitelisted addresses at all times. This check is done at every transfer. Currently, this is set to `0`; but this could be set by blackrock at anytime.

```javascript
    // get min us tokens 
    function getMinUSTokens() public view override returns (uint256) {
        return minUSTokens;
    }
    
    // set min us tokens  
    function setMinUSTokens(uint256 _value) public override onlyTransferAgentOrAbove {
        emit DSComplianceUIntRuleSet("minUSTokens", minUSTokens, _value);
        minUSTokens = _value;
    }
```

This is the code from the [`BUIDL token's contracts/compliance/ComplianceConfigurationService.Sol`](https://etherscan.deth.net/token/0x7712c34205737192402172409a8f7ccef8aa2aec#code) where the admin could set values for `minUSTokens`.

Also the line 238 in the [contracts/compliance/Compliance/ServiceRegulated.sol](https://etherscan.deth.net/token/0x7712c34205737192402172409a8f7ccef8aa2aec#code) is called when transferring token.

```javascript
if (  
                _args.fromInvestorBalance > _args.value &&
                _args.fromInvestorBalance - _args.value < IDSComplianceConfigurationService(_services[COMPLIANCE_CONFIGURATION_SERVICE]).getMinUSTokens() 
            ) {
                return (51, AMOUNT_OF_TOKENS_UNDER_MIN);
            }
```

This essentially checks that the sender has at least the minimum amount of tokens after the transfer.

The problem is the `ousgInstantManager` doesn't require that it always has this much amount of `BUIDL`. When redeeming, suppose it has 300k `BUIDL` and the minimum is say 10k `BUIDL` and an investor in Ondo wants to redeem 300k `BUIDL` tokens. It would still revert even though the contract has it, which could unexpectedly revert; violating one the main functionalities for Ondo (i.e. the instant redeem).

### Code

Create a new test file and paste this code below:

```solidity
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import {Test, console} from "forge-std/Test.sol";
import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

interface IBUILDPause {
    function pause() external;
    function isPaused() external returns(bool);
    
}

interface IBUiLDRedeemer {
    function redeem(uint256 amount) external;
}
// 0x1e695A689CF29c8fE0AF6848A957e3f84B61Fe69
contract testBUILD is Test {
    // holders of BUILD tokens; just for test 
    address holder1 = 0x72Be8C14B7564f7a61ba2f6B7E50D18DC1D4B63D;
    address holder2 = 0xEd71aa0dA4fdBA512FfA398fcFf9db8C49A5Cf72;
    address holder3 = 0xdc77C1D2A1dC61A31BE81e4840368DffEFAC3add;
    address holder4 = 0x1e695A689CF29c8fE0AF6848A957e3f84B61Fe69;
    address holder5 = 0xBc2cb4bF5510A1cc06863C96196a2361C8462525;
    address holder6 = 0xc02Ac677e58e40b66f100be3a721bA944807C2D7;
    address holder7 = 0x12c0de58D3b720024324d5B216DDFE8B29adB0b4;
    address holder8 = 0xb3c62fbe3E797502A978f418582ee92a5F327C23;
    address holder9 = 0x568430C66F9A256f609Ac07190d70c2c2573E065;
    
    // we get the owner form etherscan 
    address ownerOfBUILD = 0xe01605f6b6dC593b7d2917F4a0940db2A625b09e;
    
    address build = 0x7712c34205737192402172409a8F7ccef8aA2AEc; // build token address 
    IERC20 BUILD;   


    uint256 MAINNET_FORK;

    function setUp() external {
        MAINNET_FORK = vm.createFork("https://eth-mainnet.g.alchemy.com/v2/IrK2bvsF-q028QswCasD1dQqxV8nqGMs");
        vm.selectFork(MAINNET_FORK);
        BUILD = IERC20(build);
    }

    function testBUILDHolderTransfer() public {
        address sender = holder1;
        address to = holder9;
        uint amountToSend = 90000000e6;

        uint totalBalance = BUILD.balanceOf(sender);
        
        vm.startPrank(sender); // random 5 million holder
        BUILD.transfer(to, amountToSend); // transfer 1 million to alice 
        console.log(totalBalance);
        console.log(BUILD.balanceOf(sender));
        console.log(BUILD.balanceOf(to));
    }


    function testMinTokensUS() external { //0x1dc378568cefD4596C5F9f9A14256D8250b56369
        COMPLIANCE compliance = COMPLIANCE(0x1dc378568cefD4596C5F9f9A14256D8250b56369); // compliance configuration service
        console.log(compliance.getMinUSTokens());
        console.log(compliance.getUSLockPeriod());

        vm.startPrank(0xe01605f6b6dC593b7d2917F4a0940db2A625b09e); // owner address form etherscan 
        compliance.setMinUSTokens(10000000e6);

        console.log(compliance.getMinUSTokens());
        vm.stopPrank();

        address sender = holder1;
        address to = holder9;
        uint amountToSend = 90000000e6;

        
        
        vm.startPrank(sender); 
        BUILD.transfer(to, amountToSend);
        uint totalBalance = BUILD.balanceOf(sender); 
        console.log(totalBalance);
        console.log(BUILD.balanceOf(sender));
        console.log(BUILD.balanceOf(to));

    }
```

Run `forge test --mt testBUILDHolderTransfer` which will pass but run `forge test --mt testMinTokensUS -vvv`, i.e. with the same amount after owner sets `minUSTokens` to 10 million, it will revert.

Note: 10 million is a very large amount and not realistic, it is just to show for the test because the holder 1 has more than 90 million `BUIDL`. I just set to 10 million to show it will revert. The real value set could be significantly lower than this.

Here in our example, when holder1 tries to transfer the code checks and notice that after transfer the holder will have less than the minimum, i.e. 10 million, so it reverts.

### Tools Used

Foundry

### Recommended Mitigation Steps

Import `IDSComplianceConfigurationService` or create an interface just for the `getMinUSTokens()` function and consider replacing the require statement in the `_redeemBUIDL` function with:

```javascript
 function _redeemBUIDL(uint256 buidlAmountToRedeem) internal { 
    require(
      buidl.balanceOf(address(this)) - IDSComplianceConfigurationService(0x1dc378568cefD4596C5F9f9A14256D8250b56369).getMinUSTokens >= minBUIDLRedeemAmount,  
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance" 
    );
```

The contract will never try to redeem more than its minimum allowed to hold and appropriately reverts with our error message: **"`OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance`"**

We get the address `0x1dc378568cefD4596C5F9f9A14256D8250b56369` of the `complianceConfigurationService` proxy by querying the `BUIDL` [contract](https://etherscan.io/readContract?m=light\&a=0x7712c34205737192402172409a8f7ccef8aa2aec\&n=mainnet\&v=0x603bb6909be14f83282e03632280d91be7fb83b2#readCollapse27) in etherscan using the function `no.27 getDSService` with 256 as the argument.

This minimum amount required may not be set currently but could be set by the admin in the future. So, implementing it now should be more compatible with `BUIDL`, even if in the future blackrock decides to set it.

### Assessed type

Invalid Validation

**[cameronclifton (Ondo) acknowledged, but disagreed with severity and commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/309#issuecomment-2048004225):**
 > We will not mitigate this in the smart contract code. We plan to work with the BUIDL team to better understand the conditions in which `minUSTokens` will be set. 

*Note: For full discussion, see [here](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/309).*

***

## [[M-02] Inadequate handling of `BUIDL` redemption limit in `OUSG` instant manager](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/306)
*Submitted by [Limbooo](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/306), also found by [Bigsam](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/68)*

<https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L426-L429> 

<https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L460>

### Impact

The `OUSG` Instant Redemption Manager contract contains an oversight in its `redeem` function, specifically in the handling of `BUIDL` redemption limits. This oversight can potentially lead to failed redemption attempts when the redemption balance exceeds the `BUIDL` balance held by the manager contract while it has a right amount if its concatenated with USDC amount left by another redemption process. The impact of this issue is significant as it affects the usability of the redemption feature and can result in user frustration and loss of trust in the system.

### Proof of Concept

The following POC demonstrates the issue. Use it as part of `forge-tests/ousg/OUSGInstantManager/redeem.t.sol` file.

Run using this command:

```
npm run test-forge -- --match-test test_POC_redeem_fail_when_alice_redeemtion_balance_is_over_manager_BUIDL_balance
```

```solidity
  function test_POC_redeem_fail_when_alice_redeemtion_balance_is_over_manager_BUIDL_balance()
    public
    setupSecuritize(500_000e6, 500_000e6)
  {    
    uint256 aliceOUSGRedeemAmount = 1667e18; 
    uint256 aliceUSDCAmount = 250_100e6;

    uint256 bobOUSGRedeemAmount = 1666e18;
    uint256 bobUSDCAmount = 249_900e6;


    // Mint OUSG tokens for Alice and Bob
    vm.prank(address(ousgInstantManager));
    ousg.mint(alice, aliceOUSGRedeemAmount);

    vm.prank(address(ousgInstantManager));
    ousg.mint(bob, bobOUSGRedeemAmount);

    // Bob redeems OUSG tokens successfully
    vm.startPrank(bob);
    ousg.approve(address(ousgInstantManager), (bobOUSGRedeemAmount));
    ousgInstantManager.redeem(bobOUSGRedeemAmount);
    vm.stopPrank();

    // Alice attempts to redeem OUSG tokens, but the redemption fails due to insufficient BUIDL balance
    vm.startPrank(alice);
    ousg.approve(address(ousgInstantManager), (aliceOUSGRedeemAmount));
    vm.expectRevert('Not enough tokens');
    ousgInstantManager.redeem(aliceOUSGRedeemAmount);
    vm.stopPrank();

    assertEq(USDC.balanceOf(bob), bobUSDCAmount);

    assertEq(
      BUIDL.balanceOf(address(ousgInstantManager)) + USDC.balanceOf(address(ousgInstantManager)),
      aliceUSDCAmount
    );

    // However if Alice try to reddem an amount that will be in usdc amount <= minBUIDLRedeemAmount in ousgInstantManager it will success
    vm.startPrank(alice);
    ousgInstantManager.redeem(aliceOUSGRedeemAmount - 10e18);
    vm.stopPrank();

    // Tokens remaining in Alice's balance after successful redemption
    assertEq(ousg.balanceOf(alice), 10e18);

  }
```

### Tools Used

Foundry

### Recommended Mitigation Steps

To address this issue, the `OUSG` Instant Redemption Manager contract should implement a mechanism to ensure that redemption requests do not exceed the available `BUIDL` balance held by the manager contract. This can be achieved by incorporating proper checks and balances in the redemption process, such as verifying the `BUIDL` balance before processing redemption requests and adjusting the redemption amount accordingly. Additionally, consider an redeem implementation that concatenate the balance of remaining USDC amount with the `BUIDL` redeemed balance if the corresponding `USDC` amount or redeem amount of `OUSG` is more than `minBUIDLRedeemAmount`.

### Assessed type

Error

**[cameronclifton (Ondo) confirmed and commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/306#issuecomment-2071074179):**
> Due to changing requirements, the contract will now concatenate the USDC amount with `BUIDL` when performing redemptions. (This should mitigate this already known issue). 

*Note: For full discussion, see [here](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/306).*

***

## [[M-03] Users can lose access to funds due to minimum withdrawal limits](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/142)
*Submitted by [carrotsmuggler](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/142), also found by [Breeje](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/347), [0xmystery](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/270), [radev\_sw](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/230), [dvrkzy](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/44), and [0xCiphky](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/19)*

The `InstantManager` contract restricts deposits and withdrawals to certain minimum amounts. Users can deposit a minimum of 100k `USDC` tokens, and withdraw a minimum of 50k `USDC` tokens.

The issue is that the minimum withdrawal limit can lead to users losing access to part of their funds. Say a user deposits 100k `USDC` tokens and then later withdraws 60k `USDC` tokens. Now, the user only has 40k `USDC` worth holdings in their account, and cannot withdraw the full amount. This is because it falls below the minimum withdrawal limit of 50k `USDC` tokens. The user is now stuck with 40k `USDC` tokens in their account, and cannot withdraw them.

The only option the user has is to deposit 100k `USDC` more, and then withdraw the whole 140k `USDC` amount. This will incur fees on the extra 100k `USDC` the user brings as well. Thus this is a Medium severity issue.

### Proof of Concept

The scenario can be recreated in the following steps:

1. User ALICE deposits 100k `USDC` tokens.
2. User ALICE withdraws 60k `USDC` tokens.
3. User ALICE tries to withdraw 40k `USDC` tokens. The contract reverts, as the amount is below the minimum withdrawal limit of 50k `USDC` tokens.

### Recommended Mitigation Steps

Allow users to remove all their funds from the contract even if it is below the minimum limit. Since the protocol now uses a more liquid system such as the `BUIDL` token, this should be possible and should not affect the protocol's functioning.

**[3docSec (judge) commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/142#issuecomment-2044819320):**
 > I acknowledge this behavior is a design decision. However, I would keep this as a valid Medium for an audit report:
> - There is an availability impact for users, in a condition that they did not necessarily have to purposely create for themselves.
> - Users can decide to still withdraw for a loss in fees "for minting more to redeem all".
> - The report highlights what I find to be a very reasonable mitigation - which could be the behavior users reasonably expect:
> 
> > Allow users to remove all their funds from the contract even if it is below the minimum limit.
> 
> This mitigation seems feasible and difficult to exploit for systematic, abusive bypasses of `minimumRedemptionAmount`, because both `OUSG` and `rOUSG` have a KYC requirement on token holders.

**[cameronclifton (Ondo) disputed and commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/142#issuecomment-2073178615):**
 > We will not be removing minimum redemption requirement from the smart contract as there are other means in which users can redeem OUSG or rOUSG tokens from Ondo Finance.

*Note: For full discussion, see [here](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/142).*

***

## [[M-04] The `BURNER` cannot burn tokens from accounts not KYC verified due to the check in `_beforeTokenTransfer`.](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/32)
*Submitted by [Krace](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/32), also found by [ni8mare](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/329), [Limbooo](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/314), [leegh](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/265), [ast3ros](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/237), [radev\_sw](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/231), [Shubham](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/210), [kartik\_giri\_47538](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/206), [Arz](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/147), [kaden](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/138), [Tychai0s](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/125), [yotov721](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/105), [SpicyMeatball](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/104), [ZanyBonzy](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/40), [dvrkzy](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/33), and [0xDemon](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/26)*

<https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L586-L606>

<https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L624-L640>

### Impact

The `BURNER_ROLE` cannot burn tokens if the target `account` has been removed from the KYC list.

### Proof of Concept

When the `BURNER_ROLE` burns tokens of `_account`, it invokes `_burnShares` and then calls `_beforeTokenTransfer` to verify the KYC status of `_account`.

In accordance with a previous audit [report](https://code4rena.com/reports/2023-09-ondo#m-04-admin-cant-burn-tokens-from-blocklisted-addresses-because-of-a-check-in-\_beforetokentransfer-), the `BURNER_ROLE` should have the capability to burn tokens of any account, even if the account is blacklisted; or, in this case, not KYC verified. However, there is no mechanism that allows `BURNER_ROLE` to burn tokens of accounts that are removed from KYC list.

```solidity
  function burn(
    address _account,
    uint256 _amount
  ) external onlyRole(BURNER_ROLE) {
    uint256 ousgSharesAmount = getSharesByROUSG(_amount);
    if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
      revert UnwrapTooSmall();

    _burnShares(_account, ousgSharesAmount);

    ousg.transfer(
      msg.sender,
      ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
    emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
    emit TransferShares(_account, address(0), ousgSharesAmount);
  }
```

```solidity
  function _beforeTokenTransfer(
    address from,
    address to,
    uint256
  ) internal view {
    // Check constraints when `transferFrom` is called to facliitate
    // a transfer between two parties that are not `from` or `to`.
    if (from != msg.sender && to != msg.sender) {
      require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");
    }
// When from is not KYC, BURNER can not burn their tokens
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

### POC

Add the test to `forge-tests/ousg/rOUSG.t.sol` and run it with:

```
    forge test --fork-url $(grep -w ETHEREUM_RPC_URL .env | cut -d '=' -f2) --fork-block-number $(grep -w FORK_FROM_BLOCK_NUMBER_MAINNET .env | cut -d '=' -f2) --nmc ASSERT_FORK --match-test test_burn_with_NOKYC
```

```diff
diff --git a/forge-tests/ousg/rOUSG.t.sol b/forge-tests/ousg/rOUSG.t.sol
index 67faa15..b39b4ac 100644
--- a/forge-tests/ousg/rOUSG.t.sol
+++ b/forge-tests/ousg/rOUSG.t.sol
@@ -13,6 +13,7 @@ contract Test_rOUSG_ETH is OUSG_BasicDeployment {
     CashKYCSenderReceiver ousgProxied = CashKYCSenderReceiver(address(ousg));
     vm.startPrank(OUSG_GUARDIAN);
     ousgProxied.grantRole(ousgProxied.MINTER_ROLE(), OUSG_GUARDIAN);
+    ousgProxied.grantRole(ousgProxied.BURNER_ROLE(), OUSG_GUARDIAN);
     vm.stopPrank();

     // Sanity Asserts
@@ -26,6 +27,15 @@ contract Test_rOUSG_ETH is OUSG_BasicDeployment {
     assertTrue(registry.getKYCStatus(OUSG_KYC_REQUIREMENT_GROUP, alice));
   }

+  function test_burn_with_NOKYC() public dealAliceROUSG(1e18) {
+      vm.startPrank(OUSG_GUARDIAN);
+      _removeAddressFromKYC(OUSG_KYC_REQUIREMENT_GROUP, alice);
+      vm.stopPrank();
+
+      vm.startPrank(OUSG_GUARDIAN);
+      rOUSGToken.burn(alice, 1e18);
+      vm.stopPrank();
+  }
   /*//////////////////////////////////////////////////////////////
                         rOUSG Metadata Tests
   //////////////////////////////////////////////////////////////*/
```

Result:

    Ran 1 test for forge-tests/ousg/rOUSG.t.sol:Test_rOUSG_ETH
    [FAIL. Reason: revert: rOUSG: 'from' address not KYC'd] test_burn_with_NOKYC() (gas: 246678)
    Suite result: FAILED. 0 passed; 1 failed; 0 skipped; finished in 11.44ms (1.15ms CPU time)

    Ran 1 test suite in 1.12s (11.44ms CPU time): 0 tests passed, 1 failed, 0 skipped (1 total tests)

    Failing tests:
    Encountered 1 failing test in forge-tests/ousg/rOUSG.t.sol:Test_rOUSG_ETH
    [FAIL. Reason: revert: rOUSG: 'from' address not KYC'd] test_burn_with_NOKYC() (gas: 246678)

    Encountered a total of 1 failing tests, 0 tests succeeded

### Tools Used

Foundry

### Recommended Mitigation Steps

Allow the `BURNER` to burn tokens without checking the KYC of `from` address.

```diff
diff --git a/contracts/ousg/rOUSG.sol b/contracts/ousg/rOUSG.sol
index 29d9112..6809a28 100644
--- a/contracts/ousg/rOUSG.sol
+++ b/contracts/ousg/rOUSG.sol
@@ -594,7 +594,7 @@ contract ROUSG is
       require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");
     }

-    if (from != address(0)) {
+    if (from != address(0) && !hasRole(BURNER_ROLE, msg.sender)) {
       // If not minting
       require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd");
     }
```

### Assessed type

Invalid Validation

**[3docSec (judge) commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/32#issuecomment-2068138063):**
 >The reasons why I opted to keep this as Medium is:
> - The possibility of changing a contract implementation (in this case the registry) to a new implementation (that is not in scope) [is not something that is generally accepted as a severity mitigation](https://docs.code4rena.com/awarding/judging-criteria/supreme-court-decisions-fall-2023#verdict-using-contract-upgradability-as-a-severity-mitigation)
> - The same finding was already judged [as a valid Medium](https://github.com/code-423n4/2023-09-ondo-findings/issues/136) in a previous audit with a different scope (rUSDY), that was not explicitly marked as a known issue in the README

**[cameronclifton (Ondo) disputed and commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/32#issuecomment-2068129831):**
 > We will not be addressing this as we have a safe workaround for this exact scenario.

*Note: For full discussion, see [here](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/32).*

***

# Low Risk and Non-Critical Issues

For this audit, 64 reports were submitted by wardens detailing low risk and non-critical issues. The [report highlighted below](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/162) by **immeas** received the top score from the judge.

*The following wardens also submitted reports: [popeye](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/294), [asui](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/287), [Breeje](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/279), [b0g0](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/134), [ZanyBonzy](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/42), [m4ttm](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/333), [JC](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/332), [SAQ](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/323), [zabihullahazadzoi](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/319), [MaslarovK](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/316), [HChang26](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/312), [cheatc0d3](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/307), [ni8mare](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/301), [0xMosh](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/290), [OxTenma](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/285), [Stormreckson](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/284), [samuraii77](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/276), [0xGreyWolf](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/268), [Honour](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/250), [niser93](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/246), [Dots](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/245), [ast3ros](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/238), [bareli](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/224), [radev\_sw](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/217), [grearlake](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/213), [pkqs90](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/204), [slvDev](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/199), [baz1ka](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/195), [0xJaeger](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/187), [0xabhay](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/186), [0xlemon](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/185), [jaydhales](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/181), [0xAkira](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/164), [Shubham](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/163), [pfapostol](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/159), [0xmystery](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/158), [btk](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/155), [arnie](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/154), [Omik](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/150), [carrotsmuggler](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/143), [kaden](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/139), [Abdessamed](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/124), [Tychai0s](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/121), [EaglesSecurity](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/120), [kartik\_giri\_47538](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/106), [oualidpro](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/102), [Aymen0909](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/100), [0xweb3boy](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/96), [DanielArmstrong](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/94), [FastChecker](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/91), [IceBear](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/87), [igbinosuneric](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/85), [caglankaan](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/72), [VAD37](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/66), [Aamir](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/63), [nonn\_ac](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/47), [DarkTower](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/30), [Tigerfrake](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/29), [0xCiphky](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/20), [dd0x7e8](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/14), [albahaca](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/12), [K42](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/11), and [Krace](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/5).*

## Summary

| ID | Title |
| --- | --- |
| [L-01] | No oracle price staleness checks |
| [L-02] | User blocked by Circle cannot redeem |
| [L-03] | `usdcReceiver` is immutable |
| [L-04] | `ousgInstantManager::mint`/`redeem` lacks slippage parameter |
| [L-05] | Lack of safe transfer wrapper |
| [NC-01] | Unnecessary checks |
| [NC-02] | `usdcfees` doesn't follow `camelCase` |
| [NC-03] | Inconsistent `address(0)` checks |
| [NC-04] | Erroneous math in documentation |
| [NC-05] | Misspelled parameter |

## [L-01] No oracle price staleness checks

Both `ousgInstantManager` and `rOUSG` uses an oracle to determine the price of `OUSG`.

[`rOUSG::getOUSGPrice`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378-L380):

```solidity
File: contracts/ousg/rOUSG.sol

378:  function getOUSGPrice() public view returns (uint256 price) {
379:    (price, ) = oracle.getPriceData();
380:  }
```

Very similar in [`ousgInstantManager::getOUSGPrice`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479-L485) but with a "lowest" price check.

Here only the first parameter, `price` is used. However, the second parameter returned is the [`priceTimestamp`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/rwaOracles/RWAOracleExternalComparisonCheck.sol#L127), which is the timestamp at which the price was updated. If this is old it can lead to incorrect `OUSG` prices used for `rOUSG` or instant `minting`/`redeeming`.

### Recommendation

Consider adding a check to confirm the price used isn't stale.

## [L-02] User blocked by Circle cannot redeem

When instant redeeming either `OUSG` or `rOUSG`, at the end the user is funded their `USDC`.

[`ousgInstantManager::_redeem`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L455):

```solidity
File: contracts/ousg/ousgInstantManager.sol

455:    usdc.transfer(msg.sender, usdcAmountOut);
```

The issue is that Circle (owner of `USDC`) can add addresses to a blocklist. If the user holding `OUSG` (or `rOUSG`) is blocked by Circle, they will never be able to redeem.

### Recommendation

Consider adding an `address to` for redemptions so that they can send the `USDC` to an address that is not blocked by Circle.

## [L-03] `usdcReceiver` is immutable

Whenever someone mints, their `USDC` payment is sent to the address `usdcReciver`.

[`ousgInstantManager::_mint`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L319):

```solidity
File: contracts/ousg/ousgInstantManager.sol

319:    usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
```

The issue is that `usdcReceiver` is [immutable](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90):

```solidity
File: contracts/ousg/ousgInstantManager.sol

90:  address public immutable usdcReceiver;
```

Where this address is to be blocked by Circle, minting in `ousgInstantManager` would stop to work and a new `ousgInstantManager` would have to be deployed using a new `usdcReceiver`. This could be confusing for users.

### Recommendation

Consider making `usdcReceiver` mutable and add a way for the protocol to change it.

## [L-04] `ousgInstantManager::mint`/`redeem` lacks slippage parameter

In `ousgInstantManager` you can mint either `rOUSG` or `OUSG` using `USDC` and then redeem back to `USDC`. Both of these use an oracle to track the price of `OUSG`. This price can vary between when a transaction is sent to when it is executed. This can cause a user to mint or redeem at a different price than they intended.

### Recommendation

Consider adding a `minOut` parameter for `ousgInstantManager::mint` and `redeem` calls.

## [L-05] Lack of safe transfer wrapper

In `ousgInstantManager` the admin can make a call to transfer any tokens out of the contract.

[`ousgInstantManager::retrieveTokens`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819-L825):

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

### Recommendation

Consider using OZ `safeTransfer` wrapper to transfer tokens for better compatibility with different tokens.


## [NC-01] Unnecessary checks

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

`usdcAmountOut` can never be `0` here, as there is already [a check](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L402-L405) that `usdcAmountToRedeem` is greater than `minimumRedemptionAmount` and `minimumRedemptionAmount` can be at [the lowest `10_000`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602-L605).

The `redeemFee` can also be [no larger than 2%](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570). Hence, `usdcAmountOut` can never be lower than `9_800` (`10_000 - ((10_000 * 200) / 10_000)`).

The same logic applies to the `ousgAmountOut` in [`_mint`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310-L313); however, the math is a bit more complicated since the lowest possible `9_800` `usdc` is converted to `OUSG`. However, due to the price having a lower cap, neither this can ever be `0`.

Consider removing these two checks.

## [NC-02] `usdcfees` doesn't follow `camelCase`

[`ousgInstantManager::_mint`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L303):

```solidity
File: contracts/ousg/ousgInstantManager.sol

303:    uint256 usdcfees = _getInstantMintFees(usdcAmountIn);
```

Here `usdcfees` isn't camel cased. In [`_redeem`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L415) the same variable is using `camelCase`, which is the naming convention used throughout the code.

Consider using `camelCase` for `usdcfees` in `_mint` as well.

## [NC-03] Inconsistent `address(0)` checks

[`ousgInstantManager::setOracle`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638-L643), [`setFeeReceiver`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650-L656) and [`setInvestorBasedRateLimiter`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L673) all let admin change various addresses to external contracts.

However, only `setFeeReceiver` checks for `address(0)` before assigning. Consider checking for `address(0)` in all or none of the calls to have consistent behavior.

## [NC-04] Erroneous math in documentation

In the documentation for `rOUSG` it says [`rOUSG#L36-L45`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L36-L45):

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

This is confusing. As first, one share is one ten-thousandth of a `OUSG`; it is unclear what a "share" means here. Second, the math is wrong, `100 * 100.505 / 100 = 100.505` and `400 * 100.505 / 100 = 402.02`.

Consider updating the documentation.

## [NC-05] Misspelled parameter

[`ousgInstantManager::setInstantRedemptionLimitDuration`](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540-L544):

```solidity
File: contracts/ousg/ousgInstantManager.sol

540:  function setInstantRedemptionLimitDuration(
541:    uint256 _instantRedemptionLimitDuratioin
542:  ) external override onlyRole(CONFIGURER_ROLE) {
543:    _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
544:  }
```

Here `_instantRedemptionLimitDuratioin` is misspelled, also in the [natspec](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L536) for the call. Consider changing it to `_instantRedemptionLimitDuration`.

**[cameronclifton (Ondo) confirmed and commented](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/162#issuecomment-2071080011):**
> [L-01] - Will not be addressing, the existing functionality is desired.<br>
>[L-02] - Will not be addressing.<br>
> [L-03] - Addressed, `usdcReceiver` is now settable.<br>
> [L-04] - Will not be addressing.<br>
> [L-05] - Will not be addressing.
>
> All Non-Criticals - Addressed.

*Note: For full discussion, see [here](https://github.com/code-423n4/2024-03-ondo-finance-findings/issues/162).*

***

# Disclosures

C4 is an open organization governed by participants in the community.

C4 audits incentivize the discovery of exploits, vulnerabilities, and bugs in smart contracts. Security researchers are rewarded at an increasing rate for finding higher-risk issues. Audit submissions are judged by a knowledgeable security researcher and solidity developer and disclosed to sponsoring developers. C4 does not conduct formal verification regarding the provided code but instead provides final verification.

C4 does not provide any guarantee or warranty regarding the security of this project. All smart contract software should be used at the sole risk and responsibility of users.
