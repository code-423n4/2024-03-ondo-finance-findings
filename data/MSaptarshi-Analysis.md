# Overview
Ondo Finance is a blockchain platform that offers investment opportunities with cryptocurrencies backed by U.S. dollar bank deposits (OUSG). OUSG earns interest over time, increasing its value. Ondo Finance introduces rOUSG, a variant of OUSG that automatically adjusts in quantity to reflect interest but maintains a nominal value of 1 dollar per token. Oracles track the value of OUSG. Ondo Finance enables asset transfers between blockchains through bridge contracts.

# System Overview
 For minting OUSG and rOUSG, KYC'd users will grant USDC approval to this contract

[ousgInstantManager](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol): allows for instant mints and instant redemptions of OUSG and rOUSG. It optionally supports mint fees, redemption fees. It also has a hook for investor based rate limits to be integrated with on a later date.Investors can also opt to rebase their tokens directly through `mintRebasingOUSG(uint256)` or redeem them through `redeemRebasingOUSG` 

`[rOUSG](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol):  upgradeable rebasing token contract that be thought of as a "reverse wrapped" version of OUSG. It allows users to hold a rebasing variant of Ondo's OUSG (Ondo US Short Term Government Bond) token.It also allows users can wrap and unwrap their OUSG tokens to earn interest. It also includes features for access control and address management

[rOUSGFactory](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol): factory contract that allows the deployment of upgradable instances of the rOUSG token contract. It is managed by a guardian address, and the deployment process involves creating an implementation contract, a proxy admin contract, and a proxy contract for the token. The code is designed to facilitate the upgradeability of the rOUSG token and includes functions for batched external calls.

# Privileged Roles
The ousgInstantManager contract has these roles :

> *PAUSER_ROLE:* This role can pause and unpause the operations of the rOUSG contract. When the contract is paused, transfers and other operations are not available.

> *LIST_CONFIGURER_ROLE:* This role is used to configure the blocklist, allowlist, and sanctions list. Administrators with this role can change the addresses in these lists.

the rOUSG contract, we found some roles, such as:
> *PAUSER_ROLE:* This role can pause and unpause the operations of the rOUSG contract. When the contract is paused, transfers and other operations are not available.

> *BURNER_ROLE:* This role allows administrators to burn (delete) rOUSG from a specific account using the burn function.

> *LIST_CONFIGURER_ROLE:* This role is used to configure the blocklist, allowlist, and sanctions list. Administrators with this role can change the addresses in these lists.

The rOUSGFactory contract defines the following privilege roles:

> *DEFAULT_ADMIN_ROLE:* This role represents the default administrator role. It has access to certain administrative functions in the contract.

> *onlyGuardian:* This modifier ensures that only the guardian address has access to certain functions of the contract, such as deployrUSDY.

# Code workflow 
## 1.Mint
people who want to  mint rOUSG by depositing USDC can be done by 2 ways 
i. by depositing USDC and then get OUSG, & then go to `rOUSG.sol` to wrap their OUSG to form rOUSG 
``` mint -> _mint || -> wrap  ```

ii. by depositing USDC and directly get rOUSG

 > [*NOTE:* As said by the sponsors many investers would directly like to get rOUSG , instead of going through the hassale]

``` mintRebaseOUSG -> _mint ,approve , wrap , getROUSGByShares, transfer ```
 The internal _mint functions
```
_mint(checks: usdc.dec == 6 ,usdcAmtIn = > minAmtIn ,usdc.Allowance = > minAmtIn, ousgAmtOut > 0) 
-> Interface._checkAndUpdateInstantMintLimit(),Interface.checkAndUpdateMintLimit, 
_getInstantMintfees, getOusgPrice, _getMintAmtOut 
```

## Redeem 
This is main part which i had a bit of a problem understanding, but the protocol code cleaness and comments and docs were just to the point
people who want to  redeem USDC using their OUSG/rOUSG can be done by 2 ways 
i.by depositing OUSG and then get USDC, or else if they want to take the long route 1st unwrap their token in `rOUSG.sol` to form OUSG  then use normal redeem `(Although latter is unlikely because for latter they will use 2nd path directly)`
``` 
redeem(checks:ousg.allowance = > ousgAmtIn) -> transferFrom -> _redeem  ||  -> unwrap -> getSharesbyROUSG
```
ii.they directly deposit their rOUSG, then get back USDC
```
redeemRebasingOUSG(checks:ousg.allowance = > ousgAmtIn)-> transferFrom,unwrap,getSharesbyrOUSG,_redeem, 
```
Although the main redeem logic is happening in _redeem where we are actually not taking USDC but we are taking BUIDL tokens instead and then swapping them for USDC through a external contract. I would suggest if one would like to know more about BUIDL tokens they go through the protocol websites. And in that protocol checks 
i. `if (usdcAmountToRedeem >= minBUIDLRedeemAmount)` then redeems `usdcAmountToRedeem`
ii. ` else if (usdcAmountToRedeem > usdcBalance)` then redeems `minBUIDLRedeemAmount`
iii. `else // We have enough USDC sitting in this contract already, so use it to cover the redemption and fees without redeeming more BUIDL.` just emits and event


# Documents 
The documentation of the Ondo Finance project is quite comprehensive and detailed, providing a solid overview of how Ondo is structured and how its various aspects function. However, we have noticed that there is room for additional details, such as diagrams, to gain a deeper understanding of how different contracts interact and the functions they implement. With considerable enthusiasm, we have dedicated some days to creating diagrams for each of the contracts.
> *NOTE* :Each rOUSG token is worth 1 dollar, as OUSG accrues value (appreciates in price) rOUSG will rebase accordingly. Where as the price of a single OUSG token varies over time, the price of a single rOUSG token is fixed at a price of 1 dollar, with yield being accrued in the form of additional rOUSG tokens.

# Time Spent
A total of 4 days (25 hours) were dedicated to completing this audit, distributed as follows:

1st Day: Devoted to comprehending the protocol’s functionalities and implementation.
2nd Day: Initiated the analysis process, leveraging the documentation offered by Ondo Finance.
3rd Day: Focused on conducting a thorough analysis, incorporating meticulously crafted diagrams derived from the contracts and information provided by the protocol.

# Architectural Feedback

The architecture of the Ondo Finance project seems solid in general, but there is always room for improvements and adjustments. Here are some areas that could be improved:

> *Upgradeability:*  Since the contracts rOUSG and rOUSGFactory are upgradeable, having a clear and secure process for performing upgrades is important. It may also be useful to implement time limits for upgrades or allow a majority of users to approve upgrades.

> *Governance:* Consider incorporating a governance system to allow users to vote on key decisions, such as changes in interest rates or adjustments to system parameters.

> *Testing and Simulations:* Even though the project implements several tests, upon reviewing the codebase, there are several crucial functions that don’t, such as rOUSG:transferFrom. Conduct thorough testing of all contracts and functions and simulations to understand how they will behave under various market conditions. This can help anticipate potential issues.

# Systemic & Centralization Risks
Here’s an analysis of potential systemic and centralization risks in the provided contracts:

> *Loss of Funds Risk:* If the contract stores or manages digital assets (such as tokens), there is an inherent risk of funds being lost due to errors in the contract’s logic or malicious attacks.

The protocol uses a proxy, and according to the Documentation, the type of proxy is:
rUOUSGFactory.sol
```
* 3) TransparentUpgradeableProxy - OZ, proxy contract. Admin is set to `address(proxyAdmin)`.
*                            
```

If the logic controlling the proxy is not implemented correctly, there could be vulnerabilities that allow an attacker to modify the underlying contract, or the proxy itself, in an unintended way.

> Centralized Administration Risk: If the contract has administrator roles that can modify settings or pause the contract, there is a risk that these capabilities may be used improperly or become targets for attacks.

> Third-Party Dependency Risk: Contracts rely on external data sources, such as @openzeppelin/contracts, and there is a risk that if any issues are found with these dependencies in your contracts, the Ondo finance protocol could also be affected.

That’s why we strongly recommend that once the issues in the codebase identified by C4 Wardens are known, the Ondo Finance team takes action to implement the mitigations and make their protocol a robust financial ecosystem for all participants

# Monitoring Recommendations

While audits help in identifying code-level issues in the current implementation and potentially the code deployed in production, the Ondo Finance team is encouraged to consider incorporating monitoring activities in the production environment. Ongoing monitoring of deployed contracts helps identify potential threats and issues affecting production environments. With the goal of providing a complete security assessment.

### Time spent:
25 hours