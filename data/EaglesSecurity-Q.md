## Title

Inconsistent Error Message

## Impact

The smart contract contains an inconsistency in the error message regarding the difference between the variables usdc and _rousg. This inconsistency could lead to confusion for developers and users trying to interpret error messages related to these variables.
The inconsistency in error messages may result in misunderstandings during contract execution and debugging processes. Developers relying on error messages to diagnose issues may encounter difficulties due to the discrepancy between expected and actual variable names.

## Proof of Concept

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L186-L189

The smart contract contains an inconsistency in the error message regarding the difference between the variables usdc and _rousg. This inconsistency can lead to confusion for developers who rely on error messages to diagnose problems and users trying to interpret error messages.

## Recommended Mitigation Steps
Update the error message from 'USDC' to 'rOUSG'.
