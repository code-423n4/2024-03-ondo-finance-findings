![Pic](https://code4rena.com/_next/image?url=https%3A%2F%2Fstorage.googleapis.com%2Fcdn-c4-uploads-v0%2Fuploads%2FV7zbmr544bm.0&w=256&q=75)

# Ondo Finance Security Analysis Report


## Overview

The introduction of rOUSG and the OUSGInstantManager contract represents a sophisticated blend of traditional finance principles with DeFi's innovation, offering a stable investment vehicle and efficient transaction mechanisms. While promising, the success of these components will depend on effective management of the outlined considerations, especially regarding user accessibility and third-party dependencies. This initiative by Ondo Finance underscores the ongoing evolution and potential of the DeFi sector to offer complex financial instruments in a more accessible and decentralized manner.

This report provides a detailed security analysis of Ondo Finance, highlighting critical issues, medium to high-severity vulnerabilities, and areas requiring attention to ensure the robustness and integrity of the platform. 



## Scope of Audit

- contracts/ousg/ousgInstantManager.sol
- contracts/ousg/rOUSG.sol
- contracts/ousg/rOUSGFactory.sol


## Architecture

The inclusion of distinct contracts for managing instant transactions (ousgInstantManager.sol), the rebasing token mechanism (rOUSG.sol), and token generation (rOUSGFactory.sol) suggests a modular approach to system architecture. This modularity can enhance readability, maintainability, and upgradability of the codebase, provided that clear interfaces and secure interaction patterns between modules are established.

Ensure robustness through comprehensive interface definitions and consistent handling of cross-contract calls, especially considering reentrancy attacks and unexpected interactions.

The system's functionality, particularly around the rebasing mechanism and value transfers, relies on external price feeds (oracles) and third-party contracts for liquidity swaps.

Ensure the integrity and reliability of external data sources through the use of decentralized oracles where possible and implement fail-safes or fallback mechanisms for oracle failure. For interactions with third-party contracts, rigorous vetting and consideration of worst-case scenarios are critical.


## Approach

I undertook an in-depth manual review of Ondo Finance's smart contracts. This examination involved a line-by-line inspection of the codebase, with a focus on identifying vulnerabilities and pinpointing opportunities for enhancement. My approach was strictly manual, eschewing automated tools to ensure a thorough and nuanced understanding of the protocol's complexities. This hands-on method of engagement with the code not only aimed to improve the security and operational efficacy of the protocol but also enriched my understanding of smart contract development and the intricate interactions within blockchain systems.

## Findings
Below, you will find a summary of the principal findings and insights from this audit.

| ID | Issue Title |
|----|-------------|
| H-01 | Incorrect Balance Check for BUIDL Redemptions will lead to reverts and Partial Redemption Fulfillments |
| H-02 | Malicious KYC’d Users can Front-run Wrap/Unwrap Transactions in Their Favour |
| M-01 | Incorrect Decimals Comparison in constructor |
| L-01 | Admin Setter Functions Can Be Misused Due to Lack of Explicit Sanity Checks |
| L-02 | Lack of User-defined Slippage in Mint and Redeem Operations |
| L-03 | Lack of Explicit Balance Checks Before Token Transfers |
| L-04 | Misspelled Variable Name Will Lead to Confusion and Inconsistency |
| L-05 | Lack of Interface Support Checks |
| L-06 | Optimize the Mint Events with More Context |
| L-07 | Allowance Check Redundancy |
| L-08 | Extend Sanity Check Scope for getOUSGPrice to Include Extremely High Prices |
| L-09 | Lack of Granular Error Handling of Failed Batch Operations in multiexcall Function |
| L-10 | Missing Address Zero Validations in deployRebasingOUSG |
| L-11 | Parameterize the Guardian Address in deployRebasingOUSG |
| L-12 | increaseAllowance/decreaseAllowance are Susceptible to Phishing Attacks |
| L-13 | Lack of Max Mint Amount Validation |
| L-14 | Add Checks for Stale Oracle Prices |
| L-15 | Implement Fallback Mechanism in Case of Oracle Failure |
| L-16 | Add Excessive Volatility Check in getOUSGPrice |
| L-17 | Consider Implementing Whitelists and Blacklists for Configuration Settings Involving Addresses |
| L-18 | Dynamically Update Rate Limits and Fees Based on Market Conditions Instead of Admin Control Only |
| L-19 | Lack of Emergency Withdrawal Mechanism for Users |
| L-20 | Compromised Admin Can Grant Critical Roles to Malicious Addresses Unchecked |
| L-21 | Utilize EIP-2612 Permits for Approvals |

## Centralization Risks

The audit findings for Ondo Finance's codebase reveal several areas where centralization risks could potentially impact the system's security, efficiency, and trustworthiness. Centralization, especially in DeFi projects, can introduce points of failure, diminish censorship resistance, and compromise the foundational principle of decentralization in blockchain technology. Here are some centralization risks highlighted by the audit findings:

### Admin Control and Governance
Issues like **L-01**, where admin setter functions lack stringent sanity checks, highlight the risk of over-reliance on admin roles. Centralized control over critical parameters (fees, minting limits, etc.) without adequate checks or community governance mechanisms can lead to misuse or mismanagement, affecting user trust and system stability.

### Oracle Dependence
Findings **L-14**, **L-15**, and **L-16** underscore the system's reliance on external oracles for price feeds. Centralized oracles represent single points of failure and can be manipulated or become inaccurate, affecting critical operations like minting and redeeming. The lack of fallback mechanisms or decentralized oracle solutions amplifies this risk.

### Role Assignment and Permissions
**L-20** illustrates the dangers of compromised admin accounts being able to grant critical roles unchecked. This not only increases the risk of malicious activities if admin accounts are compromised but also concentrates power within a small group, deviating from the decentralized ethos of blockchain systems.

### Address Validation and Role Management
The absence of checks for zero addresses and the lack of a robust role management framework (**L-10**, **L-11**, **L-17**) can lead to operational errors or vulnerabilities. Centralized decision-making in updating critical contract addresses or roles without community input or transparent governance processes can lead to operational risks and reduced system integrity.

### Emergency Protocols
**L-19**'s identification of the lack of an emergency withdrawal mechanism for users highlights a centralization risk in terms of platform reliability and user asset safety. Centralized control over funds without mechanisms for users to independently recover their assets in emergencies can erode trust and limit user control over their investments.


## Conclusion

The security audit of Ondo Finance's deployment of rOUSG and the OUSGInstantManager contract has illuminated several areas of improvement, ranging from high to low priority issues. Our detailed analysis highlights the innovative approach Ondo Finance has taken to blend traditional financial instruments with the cutting-edge capabilities of decentralized finance (DeFi). This synergy aims to provide users with a stable and efficient platform for engaging with tokenized US Short Term Government Bonds, reflecting a significant step forward in the evolution of DeFi.

### Time spent:
32 hours