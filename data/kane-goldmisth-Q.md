## Title

Missing Information about maximum redeemFee and mintFee 

## Impact

After documentation review and analyzing the contract implementation, it's noted that essential details concerning the maximum redeemFee and mintFee are missing. Moreover, hardcoded values of 200 within the setMintFee() and setRedeemFee() functions were identified. This absence of crucial information and presence of hardcoded values may cause confusion and potentially resulting in incorrect utilization of the contract.
## Proof of Concepts
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L570
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L557
The documentation lacks any mention of maximum redeemFee and mintFee requirements, leaving users uninformed about these crucial parameters.
The presence of a hardcoded value (200) in the setMintFee() and setRedeemFee() functions indicates a lack of flexibility and scalability in the contract design.

## Recommended Mitigation:

1. Update the documentation with information about the maximum redeemFee and mintFee.
2. Avoid magic numbers. The function contains 200, which is a magic number. It is better to initialize it as a constant if that is appropriate in the context of the protocol.

