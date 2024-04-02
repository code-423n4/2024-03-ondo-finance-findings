## Summary

### Low Risk Issues

| |Issue|Instances|
|-|:-|:-:|
| [[L&#x2011;1](#l1-vulnerable-versions-of-packages-are-being-used)] | Vulnerable versions of packages are being used | 1 | 
| [[L&#x2011;2](#l2-for-loops-in-public-or-external-functions-should-be-avoided-due-to-high-gas-costs-and-possible-dos)] | For loops in public or external functions should be avoided due to high gas costs and possible DOS | 2 | 
| [[L&#x2011;3](#l3-external-call-recipient-may-consume-all-transaction-gas-gas-griefing)] | External call `recipient` may consume all transaction gas (gas griefing) | 2 | 
| [[L&#x2011;4](#l4-constant-decimal-values)] | Constant decimal values | 11 | 
| [[L&#x2011;5](#l5-increase-decrease-or-forceapprove-allowance-should-be-used-instead-of-approve)] | increase/decrease or forceApprove allowance should be used instead of approve | 2 | 
| [[L&#x2011;6](#l6-loss-of-precision)] | Loss of precision | 2 | 
| [[L&#x2011;7](#l7-missing-contract-existence-checks-before-low-level-calls)] | Missing contract-existence checks before low-level calls | 2 | 
| [[L&#x2011;8](#l8-governance-operations-should-be-behind-a-timelock)] | Governance operations should be behind a timelock | 28 | 
| [[L&#x2011;9](#l9-large-transfers-may-not-work-with-some-erc20-tokens)] | Large transfers may not work with some `ERC20` tokens | 1 | 
| [[L&#x2011;10](#l10-consider-implementing-two-step-procedure-for-updating-protocol-addresses)] | Consider implementing two-step procedure for updating protocol addresses | 1 | 
| [[L&#x2011;11](#l11-upgradeable-contract-is-missing-a-gap-50-storage-variable-to-allow-for-new-storage-variables-in-later-versions)] | Upgradeable contract is missing a `__gap[50]` storage variable to allow for new storage variables in later versions | 1 | 
| [[L&#x2011;12](#l12-check-of-division-by-zero)] | Check of division by zero | 1 | 
| [[L&#x2011;13](#l13-some-function-should-not-be-marked-as-payable)] | Some function should not be marked as payable | 2 | 
| [[L&#x2011;14](#l14-prevent-re-setting-a-state-variable-with-the-same-value)] | prevent re-setting a state variable with the same value | 15 | 

Total: 71 instances over 14 issues

### Non-critical Issues

| |Issue|Instances|
|-|:-|:-:|
| [[NC&#x2011;1](#nc1-natspec-natspec-author-is-missing-from-contract)] | [NatSpec] Natspec `@author` is missing from `contract` | 1 | 
| [[NC&#x2011;2](#nc2-constant-redefined-elsewhere)] | Constant redefined elsewhere | 3 | 
| [[NC&#x2011;3](#nc3-constants-in-comparisons-should-appear-on-the-left-side)] | Constants in comparisons should appear on the left side | 16 | 
| [[NC&#x2011;4](#nc4-natspec-natspec-description-is-missing-from-contract)] | [NatSpec] Natspec description is missing from `contract` | 49 | 
| [[NC&#x2011;5](#nc5-control-structures-do-not-follow-the-solidity-style-guide)] | Control structures do not follow the Solidity Style Guide | 44 | 
| [[NC&#x2011;6](#nc6-custom-error-has-no-error-details)] | Custom error has no error details | 1 | 
| [[NC&#x2011;7](#nc7-consider-adding-emergency-stop-functionality)] | Consider adding emergency-stop functionality | 1 | 
| [[NC&#x2011;8](#nc8-events-are-missing-sender-information)] | Events are missing sender information | 18 | 
| [[NC&#x2011;9](#nc9-defining-all-external-public-functions-in-contract-interfaces)] | Defining All External/Public Functions in Contract Interfaces | 20 | 
| [[NC&#x2011;10](#nc10-duplicated-require-checks-should-be-refactored-to-a-modifier-or-function)] | Duplicated `require()` checks should be refactored to a modifier or function | 1 | 
| [[NC&#x2011;11](#nc11-imports-could-be-organized-more-systematically)] | Imports could be organized more systematically | 2 | 
| [[NC&#x2011;12](#nc12-import-declarations-should-import-specific-identifiers-rather-than-the-whole-file)] | Import declarations should import specific identifiers, rather than the whole file | 23 | 
| [[NC&#x2011;13](#nc13-inconsistent-spacing-in-comments)] | Inconsistent spacing in comments | 1 | 
| [[NC&#x2011;14](#nc14-inconsistent-usage-of-require-error)] | Inconsistent usage of `require`/`error` | 2 | 
| [[NC&#x2011;15](#nc15-long-functions-should-be-refactored-into-multiple-smaller-functions)] | Long functions should be refactored into multiple, smaller, functions | 3 | 
| [[NC&#x2011;16](#nc16-long-lines-of-code)] | Long lines of code | 15 | 
| [[NC&#x2011;17](#nc17-consider-using-later-versions-of-solidity-for-more-cappabilities)] | Consider using later versions of solidity for more cappabilities | 3 | 
| [[NC&#x2011;18](#nc18-some-error-strings-are-not-descriptive)] | Some error strings are not descriptive | 2 | 
| [[NC&#x2011;19](#nc19-use-of-override-is-unnecessary)] | Use of `override` is unnecessary | 20 | 
| [[NC&#x2011;20](#nc20-redundant-inheritance-specifier)] | Redundant inheritance specifier | 3 | 
| [[NC&#x2011;21](#nc21-setters-should-prevent-re-setting-of-the-same-value)] | Setters should prevent re-setting of the same value | 6 | 
| [[NC&#x2011;22](#nc22-consider-using-safetransferlib-safetransfereth-or-address-sendvalue-for-clearer-semantic-meaning)] | Consider using `SafeTransferLib.safeTransferETH()` or `Address.sendValue()` for clearer semantic meaning | 2 | 
| [[NC&#x2011;23](#nc23-large-multiples-of-ten-should-use-scientific-notation-e-g-1e6-rather-than-decimal-literals-e-g-1000000-for-readability)] | Large multiples of ten should use scientific notation (e.g. `1e6`) rather than decimal literals (e.g. `1000000`), for readability | 3 | 
| [[NC&#x2011;24](#nc24-consider-moving-msg-sender-checks-to-a-common-authorization-modifier)] | Consider moving `msg.sender` checks to a common authorization `modifier` | 3 | 
| [[NC&#x2011;25](#nc25-state-variables-should-have-natspec-comments)] | State variables should have `Natspec` comments | 34 | 
| [[NC&#x2011;26](#nc26-contracts-should-have-full-test-coverage)] | Contracts should have full test coverage | 1 | 
| [[NC&#x2011;27](#nc27-top-level-pragma-declarations-should-be-separated-by-two-blank-lines)] | Top level pragma declarations should be separated by two blank lines | 2 | 
| [[NC&#x2011;28](#nc28-critical-functions-should-be-a-two-step-procedure)] | Critical functions should be a two step procedure | 15 | 
| [[NC&#x2011;29](#nc29-typos)] | Typos | 2 | 
| [[NC&#x2011;30](#nc30-unused-import)] | Unused Import | 2 | 
| [[NC&#x2011;31](#nc31-missing-upgradability-functionality)] | Missing upgradability functionality | 1 | 
| [[NC&#x2011;32](#nc32-use-the-latest-solidity-prior-to-0-8-20-if-on-l2s-for-deployment)] | Use the latest solidity (prior to 0.8.20 if on L2s) for deployment | 3 | 
| [[NC&#x2011;33](#nc33-use-a-single-file-for-system-wide-constants)] | Use a single file for system wide constants | 3 | 
| [[NC&#x2011;34](#nc34-consider-using-smtchecker)] | Consider using SMTChecker | 3 | 
| [[NC&#x2011;35](#nc35-whitespace-in-expressions)] | Whitespace in Expressions | 12 | 
| [[NC&#x2011;36](#nc36-consider-bounding-input-array-length)] | Consider bounding input array length | 2 | 
| [[NC&#x2011;37](#nc37-natspec-natspec-dev-is-missing-from-contract)] | [NatSpec] Natspec `@dev` is missing from `contract` | 55 | 
| [[NC&#x2011;38](#nc38-add-inline-comments-for-unnamed-variables)] | Add inline comments for unnamed variables | 5 | 
| [[NC&#x2011;39](#nc39-contract-should-expose-an-interface)] | Contract should expose an `interface` | 19 | 
| [[NC&#x2011;40](#nc40-named-imports-of-parent-contracts-are-missing)] | Named imports of parent contracts are missing | 13 | 
| [[NC&#x2011;41](#nc41-natspec-natspec-notice-is-missing-from-contract)] | [NatSpec] Natspec `@notice` is missing from `contract` | 30 | 
| [[NC&#x2011;42](#nc42-event-names-should-use-camelcase)] | Event names should use CamelCase | 1 | 
| [[NC&#x2011;43](#nc43-expressions-for-constant-values-should-use-immutable-rather-than-constant)] | Expressions for constant values should use `immutable` rather than `constant` | 6 | 
| [[NC&#x2011;44](#nc44-top-level-declarations-should-be-separated-by-at-least-two-lines)] | Top-level declarations should be separated by at least two lines | 3 | 
| [[NC&#x2011;45](#nc45-contract-uses-both-require-revert-as-well-as-custom-errors)] | Contract uses both `require()`/`revert()` as well as custom errors | 2 | 
| [[NC&#x2011;46](#nc46-consider-using-accesscontroldefaultadminrules-rather-than-accesscontrol)] | Consider using `AccessControlDefaultAdminRules` rather than `AccessControl` | 1 | 
| [[NC&#x2011;47](#nc47-immutable-variable-names-don-t-follow-the-solidity-style-guide)] | `immutable` variable names don\'t follow the Solidity style guide | 8 | 
| [[NC&#x2011;48](#nc48-add-inline-comments-for-unnamed-parameters)] | Add inline comments for unnamed parameters | 14 | 
| [[NC&#x2011;49](#nc49-use-the-latest-solidity-version-for-better-security)] | Use the latest Solidity version for better security | 3 | 
| [[NC&#x2011;50](#nc50-consider-adding-formal-verification-proofs)] | Consider adding formal verification proofs | 1 | 
| [[NC&#x2011;51](#nc51-missing-zero-address-check-in-functions-with-address-parameters)] | Missing zero address check in functions with address parameters | 3 | 
| [[NC&#x2011;52](#nc52-use-a-struct-to-encapsulate-multiple-function-parameters)] | Use a struct to encapsulate multiple function parameters | 4 | 
| [[NC&#x2011;53](#nc53-use-custom-errors-rather-than-revert-require-strings-for-better-readability)] | Use custom errors rather than `revert()`/`require()` strings for better readability | 50 | 
| [[NC&#x2011;54](#nc54-use-inheritdoc-for-overridden-functions)] | Use `@inheritdoc` for overridden functions | 20 | 
| [[NC&#x2011;55](#nc55-multiple-mappings-with-same-keys-can-be-combined-into-a-single-struct-mapping-for-readability)] | Multiple mappings with same keys can be combined into a single struct mapping for readability | 2 | 
| [[NC&#x2011;56](#nc56-constructor-should-emit-an-event)] | constructor should emit an event | 3 | 
| [[NC&#x2011;57](#nc57-complex-functions-should-include-comments)] | Complex functions should include comments | 3 | 
| [[NC&#x2011;58](#nc58-solidity-all-verbatim-blocks-are-considered-identical-by-deduplicator-and-can-incorrectly-be-unified)] | [Solidity]: All `verbatim` blocks are considered identical by deduplicator and can incorrectly be unified | 3 | 
| [[NC&#x2011;59](#nc59-natspec-natspec-param-is-missing-from-error)] | [NatSpec] Natspec `@param` is missing from `error` | 31 | 
| [[NC&#x2011;60](#nc60-openzeppelin-libraries-should-be-upgraded-to-a-newer-version)] | OpenZeppelin libraries should be upgraded to a newer version | 11 | 
| [[NC&#x2011;61](#nc61-not-using-the-latest-version-of-prb-math-from-dependencies)] | Not using the latest version of `prb-math` from dependencies | 1 | 
| [[NC&#x2011;62](#nc62-enforcing-lowercase-and-underscores-only-in-the-name-field-of-package-json)] | Enforcing Lowercase and Underscores Only in the `name` Field of package.json | 1 | 
| [[NC&#x2011;63](#nc63-consider-making-private-state-variables-internal-to-increase-flexibility)] | Consider making private state variables internal to increase flexibility | 3 | 
| [[NC&#x2011;64](#nc64-using-low-level-call-for-transfers)] | Using Low-Level Call for Transfers | 2 | 
| [[NC&#x2011;65](#nc65-a-event-should-be-emitted-if-a-non-immutable-state-variable-is-set-in-a-constructor)] | A event should be emitted if a non immutable state variable is set in a constructor | 10 | 
| [[NC&#x2011;66](#nc66-solidity-order-of-argument-evaluation-disrupted-in-non-expression-split-code-by-optimizer-sequences-with-fullinliner)] | [Solidity]: Order of Argument Evaluation Disrupted in Non-Expression-Split Code by Optimizer Sequences with FullInliner | 3 | 
| [[NC&#x2011;67](#nc67-use-named-return-values)] | Use named return values | 24 | 
| [[NC&#x2011;68](#nc68-consider-moving-duplicated-strings-to-constants)] | Consider moving duplicated strings to constants | 24 | 
| [[NC&#x2011;69](#nc69-missing-checks-for-uint-state-variable-assignments)] | Missing checks for uint state variable assignments | 5 | 
| [[NC&#x2011;70](#nc70-consider-adding-validation-of-user-inputs)] | Consider adding validation of user inputs | 25 | 
| [[NC&#x2011;71](#nc71-consider-disallowing-transfers-to-address-this)] | Consider disallowing transfers to `address(this)` | 3 | 
| [[NC&#x2011;72](#nc72-consider-using-named-function-calls)] | Consider using named function calls | 28 | 

Total: 742 instances over 72 issues

## Low Risk Issues

### [L&#x2011;1] Vulnerable versions of packages are being used 
This project's specific package versions are vulnerable to the specific CVEs listed below. Consider switching to more recent versions of these packages that don't have these vulnerabilities


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: package.json


<details><summary>Vulnerabilities related to `@openzeppelin/contracts`:</summary>


- [CVE-2023-34459](https://github.com/OpenZeppelin/openzeppelin-contracts/security/advisories/GHSA-wprv-93r4-jj2p) :When the verifyMultiProof, verifyMultiProofCalldata, processMultiProof, or processMultiProofCalldata functions are in use, it is possible to construct merkle trees that allow forging a valid multiproof for an arbitrary set of leaves.
A contract may be vulnerable if it uses multiproofs for verification and the merkle tree that is processed includes a node with value 0 at depth 1(just under the root).This could happen inadvertently for balanced trees with 3 leaves or less, if the leaves are not hashed.This could happen deliberately if a malicious tree builder includes such a node in the tree.
A contract is not vulnerable if it uses single- leaf proving(verify, verifyCalldata, processProof, or processProofCalldata), or if it uses multiproofs with a known tree that has hashed leaves.Standard merkle trees produced or validated with the @openzeppelin/merkle-tree library are safe.


- [CVE-2023-34234](https://github.com/OpenZeppelin/openzeppelin-contracts/security/advisories/GHSA-5h3x-9wvq-w4m2) :By frontrunning the creation of a proposal, an attacker can become the proposer and gain the ability to cancel it. The attacker can do this repeatedly to try to prevent a proposal from being proposed at all.
This impacts the Governor contract in v4.9.0 only, and the GovernorCompatibilityBravo contract since v4.3.0.
</details>
1: 


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//package.json#L1-L1) 


</details>


### [L&#x2011;2] For loops in public or external functions should be avoided due to high gas costs and possible DOS 
In Solidity, for loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where for loops can lead to DoS attacks: Nested for loops can become exceptionally gas expensive and should be used sparingly


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

794:   function multiexcall(
795:     ExCallData[] calldata exCallData
796:   )
797:     external
798:     payable
799:     override
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
803:     results = new bytes[](exCallData.length);
804:     for (uint256 i = 0; i < exCallData.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L804) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {
124:     results = new bytes[](exCallData.length);
125:     for (uint256 i = 0; i < exCallData.length; ++i) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L121-L125) 


</details>


### [L&#x2011;3] External call `recipient` may consume all transaction gas (gas griefing) 
There is no limit specified on the amount of gas used, so the recipient can use up all of the transaction's gas, causing it to revert. Use `addr.call{ gas: <amount>}("")` or [this](https://github.com/nomad-xyz/ExcessivelySafeCall) library instead.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L805-L805) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L126-L126) 


</details>


### [L&#x2011;4] Constant decimal values 
The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations.Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations.
Always retrieve and use the `decimals()` function from the token contract itself when performing calculations involving token amounts.This ensures that your contract correctly handles tokens with any number of decimal places, mitigating the risk of numerical errors or under / overflows that could jeopardize contract integrity and user funds. 


*There are 11 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

689:     uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;

704:     usdcOwed = _scaleDown(amountE36 / 1e18);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L689-L689) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L704-L704)


```solidity

File: ./contracts/ousg/rOUSG.sol

190:       (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);

190:       (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);

202:       (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);

202:       (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);

367:       (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();

367:       (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();

367:       (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();

375:       (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);

375:       (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L190-L190) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L190-L190), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L202-L202), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L202-L202), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L367-L367), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L367-L367), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L367-L367), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L375-L375), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L375-L375)


</details>


### [L&#x2011;5] increase/decrease or forceApprove allowance should be used instead of approve 
In order to prevent front running, increase/decrease or forceApprove allowance should be used in place of approve where possible 


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

264:     ousg.approve(address(rousg), ousgAmountOut);

464:     buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L264-L264) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L464-L464)


</details>


### [L&#x2011;6] Loss of precision 
Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

690:     ousgAmountOut = amountE36 / price;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L690-L690) 


```solidity

File: ./contracts/ousg/rOUSG.sol

367:       (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L367-L367) 


</details>


### [L&#x2011;7] Missing contract-existence checks before low-level calls 
Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `<address>.code.length > 0`


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
806:         value: exCallData[i].value


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L805-L806) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
127:         value: exCallData[i].value


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L126-L127) 


</details>


### [L&#x2011;8] Governance operations should be behind a timelock 
All critical and governance operations should be protected by a timelock. For example from the point of view of a user, the changing of the owner of a contract is a high risk operation that may have outcomes ranging from an attacker gaining control over the protocol, to the function no longer functioning due to a typo in the destination address. To give users plenty of warning so that they can validate any ownership changes, changes of ownership should be behind a timelock.


*There are 28 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

498:   function setInstantMintLimit(
499:     uint256 _instantMintLimit
500:   ) external override onlyRole(CONFIGURER_ROLE) {
501:     _setInstantMintLimit(_instantMintLimit);
502:   }

512:   function setInstantRedemptionLimit(
513:     uint256 _instantRedemptionLimit
514:   ) external override onlyRole(CONFIGURER_ROLE) {
515:     _setInstantRedemptionLimit(_instantRedemptionLimit);
516:   }

526:   function setInstantMintLimitDuration(
527:     uint256 _instantMintLimitDuration
528:   ) external override onlyRole(CONFIGURER_ROLE) {
529:     _setInstantMintLimitDuration(_instantMintLimitDuration);
530:   }

540:   function setInstantRedemptionLimitDuration(
541:     uint256 _instantRedemptionLimitDuratioin
542:   ) external override onlyRole(CONFIGURER_ROLE) {
543:     _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
544:   }

554:   function setMintFee(
555:     uint256 _mintFee
556:   ) external override onlyRole(CONFIGURER_ROLE) {
557:     require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558:     emit MintFeeSet(mintFee, _mintFee);
559:     mintFee = _mintFee;
560:   }

567:   function setRedeemFee(
568:     uint256 _redeemFee
569:   ) external override onlyRole(CONFIGURER_ROLE) {
570:     require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571:     emit RedeemFeeSet(redeemFee, _redeemFee);
572:     redeemFee = _redeemFee;
573:   }

581:   function setMinimumDepositAmount(
582:     uint256 _minimumDepositAmount
583:   ) external override onlyRole(CONFIGURER_ROLE) {
584:     require(
585:       _minimumDepositAmount >= FEE_GRANULARITY,
586:       "setMinimumDepositAmount: Amount too small"
587:     );
588: 
589:     emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
590:     minimumDepositAmount = _minimumDepositAmount;
591:   }

599:   function setMinimumRedemptionAmount(
600:     uint256 _minimumRedemptionAmount
601:   ) external override onlyRole(CONFIGURER_ROLE) {
602:     require(
603:       _minimumRedemptionAmount >= FEE_GRANULARITY,
604:       "setMinimumRedemptionAmount: Amount too small"
605:     );
606:     emit MinimumRedemptionAmountSet(
607:       minimumRedemptionAmount,
608:       _minimumRedemptionAmount
609:     );
610:     minimumRedemptionAmount = _minimumRedemptionAmount;
611:   }

622:   function setMinimumBUIDLRedemptionAmount(
623:     uint256 _minimumBUIDLRedemptionAmount
624:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
625:     emit MinimumBUIDLRedemptionAmountSet(
626:       minBUIDLRedeemAmount,
627:       _minimumBUIDLRedemptionAmount
628:     );
629:     minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
630:   }

638:   function setOracle(
639:     address _oracle
640:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
641:     emit OracleSet(address(oracle), _oracle);
642:     oracle = IRWAOracle(_oracle);
643:   }

650:   function setFeeReceiver(
651:     address _feeReceiver
652:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
653:     require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
654:     emit FeeReceiverSet(feeReceiver, _feeReceiver);
655:     feeReceiver = _feeReceiver;
656:   }

663:   function setInvestorBasedRateLimiter(
664:     address _investorBasedRateLimiter
665:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
666:     emit InvestorBasedRateLimiterSet(
667:       address(investorBasedRateLimiter),
668:       _investorBasedRateLimiter
669:     );
670:     investorBasedRateLimiter = IInvestorBasedRateLimiter(
671:       _investorBasedRateLimiter
672:     );
673:   }

768:   function pauseMint() external onlyRole(PAUSER_ROLE) {
769:     mintPaused = true;
770:     emit MintPaused();
771:   }

774:   function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {
775:     mintPaused = false;
776:     emit MintUnpaused();
777:   }

780:   function pauseRedeem() external onlyRole(PAUSER_ROLE) {
781:     redeemPaused = true;
782:     emit RedeemPaused();
783:   }

786:   function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {
787:     redeemPaused = false;
788:     emit RedeemUnpaused();
789:   }

794:   function multiexcall(
795:     ExCallData[] calldata exCallData
796:   )
797:     external
798:     payable
799:     override
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
803:     results = new bytes[](exCallData.length);
804:     for (uint256 i = 0; i < exCallData.length; ++i) {
805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
806:         value: exCallData[i].value
807:       }(exCallData[i].data);
808:       require(success, "Call Failed");
809:       results[i] = ret;
810:     }
811:   }

819:   function retrieveTokens(
820:     address token,
821:     address to,
822:     uint256 amount
823:   ) external onlyRole(DEFAULT_ADMIN_ROLE) {
824:     IERC20(token).transfer(to, amount);
825:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L498-L502) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L512-L516), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L526-L530), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L540-L544), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L554-L560), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L567-L573), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L581-L591), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L599-L611), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L622-L630), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L638-L643), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L656), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L663-L673), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L768-L771), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L774-L777), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L780-L783), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L786-L789), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L811), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L819-L825)


```solidity

File: ./contracts/ousg/rOUSG.sol

112:   function __rOUSG_init(
113:     address _kycRegistry,
114:     uint256 requirementGroup,
115:     address _ousg,
116:     address guardian,
117:     address _oracle
118:   ) internal onlyInitializing {
119:     __rOUSG_init_unchained(
120:       _kycRegistry,
121:       requirementGroup,
122:       _ousg,
123:       guardian,
124:       _oracle
125:     );
126:   }

128:   function __rOUSG_init_unchained(
129:     address _kycRegistry,
130:     uint256 _requirementGroup,
131:     address _ousg,
132:     address guardian,
133:     address _oracle
134:   ) internal onlyInitializing {
135:     __KYCRegistryClientInitializable_init(_kycRegistry, _requirementGroup);
136:     ousg = IERC20(_ousg);
137:     oracle = IRWAOracle(_oracle);
138:     _grantRole(DEFAULT_ADMIN_ROLE, guardian);
139:     _grantRole(PAUSER_ROLE, guardian);
140:     _grantRole(BURNER_ROLE, guardian);
141:     _grantRole(CONFIGURER_ROLE, guardian);
142:   }

613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
614:     emit OracleSet(address(oracle), _oracle);
615:     oracle = IRWAOracle(_oracle);
616:   }

624:   function burn(
625:     address _account,
626:     uint256 _amount
627:   ) external onlyRole(BURNER_ROLE) {
628:     uint256 ousgSharesAmount = getSharesByROUSG(_amount);
629:     if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
630:       revert UnwrapTooSmall();
631: 
632:     _burnShares(_account, ousgSharesAmount);
633: 
634:     ousg.transfer(
635:       msg.sender,
636:       ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
637:     );
638:     emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
639:     emit TransferShares(_account, address(0), ousgSharesAmount);
640:   }

642:   function pause() external onlyRole(PAUSER_ROLE) {
643:     _pause();
644:   }

646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
647:     _unpause();
648:   }

650:   function setKYCRegistry(
651:     address registry
652:   ) external override onlyRole(CONFIGURER_ROLE) {
653:     _setKYCRegistry(registry);
654:   }

656:   function setKYCRequirementGroup(
657:     uint256 group
658:   ) external override onlyRole(CONFIGURER_ROLE) {
659:     _setKYCRequirementGroup(group);
660:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L112-L126) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L128-L142), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L613-L616), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L624-L640), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L642-L644), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L646-L648), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L654), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L660)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

070:   function deployRebasingOUSG(
071:     address kycRegistry,
072:     uint256 requirementGroup,
073:     address ousg,
074:     address oracle
075:   ) external onlyGuardian returns (address, address, address) {
076:     require(!initialized, "ROUSGFactory: rOUSG already deployed");
077:     rOUSGImplementation = new ROUSG();
078:     rOUSGProxyAdmin = new ProxyAdmin();
079:     rOUSGProxy = new TokenProxy(
080:       address(rOUSGImplementation),
081:       address(rOUSGProxyAdmin),
082:       ""
083:     );
084:     ROUSG rOUSGProxied = ROUSG(address(rOUSGProxy));
085:     rOUSGProxied.initialize(
086:       kycRegistry,
087:       requirementGroup,
088:       ousg,
089:       guardian,
090:       oracle
091:     );
092: 
093:     rOUSGProxyAdmin.transferOwnership(guardian);
094:     assert(rOUSGProxyAdmin.owner() == guardian);
095:     initialized = true;
096:     emit rOUSGDeployed(
097:       address(rOUSGProxy),
098:       address(rOUSGProxyAdmin),
099:       address(rOUSGImplementation),
100:       rOUSGProxied.name(),
101:       rOUSGProxied.symbol()
102:     );
103:     return (
104:       address(rOUSGProxy),
105:       address(rOUSGProxyAdmin),
106:       address(rOUSGImplementation)
107:     );
108:   }

121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {
124:     results = new bytes[](exCallData.length);
125:     for (uint256 i = 0; i < exCallData.length; ++i) {
126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
127:         value: exCallData[i].value
128:       }(exCallData[i].data);
129:       require(success, "Call Failed");
130:       results[i] = ret;
131:     }
132:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L70-L108) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L121-L132)


</details>


### [L&#x2011;9] Large transfers may not work with some `ERC20` tokens 
Some `IERC20` implementations (e.g `UNI`, `COMP`) may fail if the valued transferred is larger than `uint96`. [Source](https://github.com/d-xo/weird-erc20#revert-on-large-approvals--transfers)


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

824:     IERC20(token).transfer(to, amount);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L824-L824) 


</details>


### [L&#x2011;10] Consider implementing two-step procedure for updating protocol addresses 
A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must 'accept' the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement [EIP-165](https://eips.ethereum.org/EIPS/eip-165), and to have the 'set' functions ensure that the recipient is of the right interface type.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

650:   function setFeeReceiver(
651:     address _feeReceiver
652:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
653:     require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
654:     emit FeeReceiverSet(feeReceiver, _feeReceiver);
655:     feeReceiver = _feeReceiver;
656:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L656) 


</details>


### [L&#x2011;11] Upgradeable contract is missing a `__gap[50]` storage variable to allow for new storage variables in later versions 
See [this](https://docs.openzeppelin.com/contracts/4.x/upgradeable#storage_gaps) link for a description of this storage variable. While some contracts may not currently be sub-classed, adding the variable now protects against forgetting to add it in the future.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

55: contract ROUSG is


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L55-L55) 


</details>


### [L&#x2011;12] Check of division by zero 



*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

690:     ousgAmountOut = amountE36 / price;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L690-L690) 


</details>


### [L&#x2011;13] Some function should not be marked as payable 
Some function should not be marked as payable, otherwise the ETH that mistakenly sent along with the function call is locked in the contract


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

794:   function multiexcall(
795:     ExCallData[] calldata exCallData
796:   )
797:     external
798:     payable
799:     override
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
803:     results = new bytes[](exCallData.length);
804:     for (uint256 i = 0; i < exCallData.length; ++i) {
805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
806:         value: exCallData[i].value
807:       }(exCallData[i].data);
808:       require(success, "Call Failed");
809:       results[i] = ret;
810:     }
811:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L811) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {
124:     results = new bytes[](exCallData.length);
125:     for (uint256 i = 0; i < exCallData.length; ++i) {
126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
127:         value: exCallData[i].value
128:       }(exCallData[i].data);
129:       require(success, "Call Failed");
130:       results[i] = ret;
131:     }
132:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L121-L132) 


</details>


### [L&#x2011;14] prevent re-setting a state variable with the same value 
Not only is wasteful in terms of gas, but this is especially problematic when an event is emitted and the old and new values set are the same, as listeners might not expect this kind of scenario.


*There are 15 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

498:   function setInstantMintLimit(

512:   function setInstantRedemptionLimit(

526:   function setInstantMintLimitDuration(

540:   function setInstantRedemptionLimitDuration(

554:   function setMintFee(

567:   function setRedeemFee(

581:   function setMinimumDepositAmount(

599:   function setMinimumRedemptionAmount(

622:   function setMinimumBUIDLRedemptionAmount(

638:   function setOracle(

650:   function setFeeReceiver(

663:   function setInvestorBasedRateLimiter(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L498-L498) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L512-L512), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L526-L526), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L540-L540), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L554-L554), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L567-L567), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L581-L581), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L599-L599), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L622-L622), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L638-L638), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L663-L663)


```solidity

File: ./contracts/ousg/rOUSG.sol

613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L613-L613) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L656)


</details>


## Non-critical Issues

### [NC&#x2011;1] [NatSpec] Natspec `@author` is missing from `contract` 



*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

28: /**
29:  * @title Interest-bearing ERC20-like token for OUSG.
30:  *
31:  * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
32:  * controlled by the protocol. To calculate each account's balance, we do
33:  *
34:  *   shares[account] * ousgPrice
35:  *
36:  * For example, assume that we have:
37:  *
38:  *   ousgPrice = 100.505
39:  *   sharesOf(user1) -> 100
40:  *   sharesOf(user2) -> 400
41:  *
42:  * Therefore:
43:  *
44:  *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
45:  *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
46:  *
47:  * Since balances of all token holders change when the price of OUSG changes, this
48:  * token cannot fully implement ERC20 standard: it only emits `Transfer` events
49:  * upon explicit transfer between holders. In contrast, when total amount of pooled
50:  * Cash increases, no `Transfer` events are generated: doing so would require emitting
51:  * an event for each token holder and thus running an unbounded loop.
52:  *
53:  */


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L28-L53) 


</details>


### [NC&#x2011;2] Constant redefined elsewhere 
Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A [cheap way](https://medium.com/coinmonks/gas-cost-of-solidity-library-functions-dbe0cedd4678) to store constants in a single location is to create an `internal constant` in a `library`. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

//@audit The same constant is already defined on file : ./contracts/ousg/ousgInstantManager.sol
87:   uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;

//@audit The same constant is already defined on file : ./contracts/ousg/ousgInstantManager.sol
93:   bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");

//@audit The same constant is already defined on file : ./contracts/ousg/ousgInstantManager.sol
95:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L87-L87) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L93-L93), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L95-L95)


</details>


### [NC&#x2011;3] Constants in comparisons should appear on the left side 



*There are 16 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit `0`
316:     if (usdcfees > 0) {

//@audit `6`
283:       IERC20Metadata(address(usdc)).decimals() == 6,

//@audit `0`
311:       ousgAmountOut > 0,

//@audit `0`
450:     if (usdcFees > 0) {

//@audit `6`
392:       IERC20Metadata(address(usdc)).decimals() == 6,

//@audit `6`
396:       IERC20Metadata(address(buidl)).decimals() == 6,

//@audit `0`
418:       usdcAmountOut > 0,

//@audit `MINIMUM_OUSG_PRICE`
482:       price > MINIMUM_OUSG_PRICE,

//@audit `200`
557:     require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");

//@audit `200`
570:     require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");

//@audit `FEE_GRANULARITY`
585:       _minimumDepositAmount >= FEE_GRANULARITY,

//@audit `FEE_GRANULARITY`
603:       _minimumRedemptionAmount >= FEE_GRANULARITY,


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L316-L316) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L283-L283), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L311-L311), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L450-L450), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L392-L392), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L396-L396), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L418-L418), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L482-L482), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L557-L557), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L570-L570), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L585-L585), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L603-L603)


```solidity

File: ./contracts/ousg/rOUSG.sol

//@audit `0`
416:     require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");

//@audit `OUSG_TO_ROUSG_SHARES_MULTIPLIER`
434:     if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)

//@audit `0`
432:     require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");

//@audit `OUSG_TO_ROUSG_SHARES_MULTIPLIER`
629:     if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L416-L416) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L434-L434), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L432-L432), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L629-L629)


</details>


### [NC&#x2011;4] [NatSpec] Natspec description is missing from `contract` 
It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as Defi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.[source](https://docs.soliditylang.org/en/v0.8.15/natspec-format.html)


*There are 49 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

57:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");

60:   bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");

63:   uint256 public constant MINIMUM_OUSG_PRICE = 105e18;

66:   uint256 public constant FEE_GRANULARITY = 10_000;

69:   uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;

72:   IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;

75:   IRWALike public immutable ousg;

78:   ROUSG public immutable rousg;

81:   IERC20 public immutable buidl;

84:   IBUIDLRedeemer public immutable buidlRedeemer;

87:   uint256 public immutable decimalsMultiplier;

90:   address public immutable usdcReceiver;

93:   IRWAOracle public oracle;

96:   address public feeReceiver;

99:   uint256 public mintFee = 0;

102:   uint256 public redeemFee = 0;

106:   uint256 public minimumDepositAmount = 100_000e6;

110:   uint256 public minimumRedemptionAmount = 50_000e6;

113:   bool public mintPaused;

116:   bool public redeemPaused;

120:   uint256 public minBUIDLRedeemAmount = 250_000e6;

123:   IInvestorBasedRateLimiter public investorBasedRateLimiter;

278:   function _mint(

388:   function _redeem(

458:   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {

794:   function multiexcall(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L57-L57) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L60-L60), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L63-L63), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L69-L69), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L72-L72), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L75-L75), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L78-L78), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L84-L84), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L87-L87), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L90-L90), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L93-L93), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L96-L96), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L99-L99), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L106-L106), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L110-L110), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L113-L113), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L116-L116), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L120-L120), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L123-L123), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L278-L278), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L388-L388), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L458-L458), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L794)


```solidity

File: ./contracts/ousg/rOUSG.sol

78:   uint256 private totalShares;

81:   IRWAOracle public oracle;

84:   IERC20 public ousg;

87:   uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;

90:   error UnwrapTooSmall();

94:   bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");

95:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");

102:   function initialize(

112:   function __rOUSG_init(

128:   function __rOUSG_init_unchained(

378:   function getOUSGPrice() public view returns (uint256 price) {

642:   function pause() external onlyRole(PAUSER_ROLE) {

646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L78-L78) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L84-L84), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L87-L87), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L90-L90), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L94-L94), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L95-L95), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L378-L378), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L642-L642), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L646-L646), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L656)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

38:   bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);

40:   address internal immutable guardian;

41:   ROUSG public rOUSGImplementation;

42:   ProxyAdmin public rOUSGProxyAdmin;

43:   TokenProxy public rOUSGProxy;

45:   bool public initialized = false;

47:   constructor(address _guardian) {

149:   modifier onlyGuardian() {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L38-L38) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L40-L40), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L41-L41), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L42-L42), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L43-L43), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L45-L45), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L47-L47), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L149-L149)


</details>


### [NC&#x2011;5] Control structures do not follow the Solidity Style Guide 
See the [control structures](https://docs.soliditylang.org/en/latest/style-guide.html#control-structures) section of the Solidity Style Guide


*There are 44 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

230:   function mint(

254:   function mintRebasingOUSG(

278:   function _mint(

335:   function redeem(

362:   function redeemRebasingOUSG(

388:   function _redeem(

498:   function setInstantMintLimit(

512:   function setInstantRedemptionLimit(

526:   function setInstantMintLimitDuration(

540:   function setInstantRedemptionLimitDuration(

554:   function setMintFee(

567:   function setRedeemFee(

581:   function setMinimumDepositAmount(

599:   function setMinimumRedemptionAmount(

622:   function setMinimumBUIDLRedemptionAmount(

638:   function setOracle(

650:   function setFeeReceiver(

663:   function setInvestorBasedRateLimiter(

685:   function _getMintAmount(

699:   function _getRedemptionAmount(

713:   function _getInstantMintFees(

725:   function _getInstantRedemptionFees(

794:   function multiexcall(

819:   function retrieveTokens(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L230-L230) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L254-L254), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L278-L278), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L335-L335), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L362-L362), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L388-L388), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L498-L498), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L512-L512), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L526-L526), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L540-L540), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L554-L554), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L567-L567), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L581-L581), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L599-L599), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L622-L622), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L638-L638), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L663-L663), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L685-L685), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L699-L699), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L713-L713), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L725-L725), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L794), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L819-L819)


```solidity

File: ./contracts/ousg/rOUSG.sol

102:   function initialize(

112:   function __rOUSG_init(

128:   function __rOUSG_init_unchained(

231:   function allowance(

276:   function transferFrom(

302:   function increaseAllowance(

328:   function decreaseAllowance(

363:   function getSharesByROUSG(

397:   function transferShares(

450:   function _transfer(

472:   function _approve(

501:   function _transferShares(

529:   function _mintShares(

554:   function _burnShares(

586:   function _beforeTokenTransfer(

624:   function burn(

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L102-L102) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L231-L231), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L276-L276), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L302-L302), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L328-L328), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L363-L363), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L397-L397), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L450-L450), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L472-L472), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L501-L501), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L529-L529), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L554-L554), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L586-L586), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L624-L624), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L656)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

70:   function deployRebasingOUSG(

121:   function multiexcall(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L70-L70) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L121-L121)


</details>


### [NC&#x2011;6] Custom error has no error details 
Consider adding parameters to the error to indicate which user or values caused the failure


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

90:   error UnwrapTooSmall();


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L90-L90) 


</details>


### [NC&#x2011;7] Consider adding emergency-stop functionality 
In the event of a security breach or any unforeseen emergency, swiftly suspending all protocol operations becomes crucial. Having a mechanism in place to halt all functions collectively, instead of pausing individual contracts separately, substantially enhances the efficiency of mitigating ongoing attacks or vulnerabilities. This not only quickens the response time to potential threats but also reduces operational stress during these critical periods. Therefore, consider integrating a 'circuit breaker' or 'emergency stop' function into the smart contract system architecture. Such a feature would provide the capability to suspend the entire protocol instantly, which could prove invaluable during a time-sensitive crisis management situation.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

//@audit `PausableUpgradeable`
55: contract ROUSG is


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L55-L55) 


</details>


### [NC&#x2011;8] Events are missing sender information 
When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.


*There are 18 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

558:     emit MintFeeSet(mintFee, _mintFee);

571:     emit RedeemFeeSet(redeemFee, _redeemFee);

589:     emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);

606:     emit MinimumRedemptionAmountSet(
607:       minimumRedemptionAmount,
608:       _minimumRedemptionAmount
609:     );

625:     emit MinimumBUIDLRedemptionAmountSet(
626:       minBUIDLRedeemAmount,
627:       _minimumBUIDLRedemptionAmount
628:     );

641:     emit OracleSet(address(oracle), _oracle);

654:     emit FeeReceiverSet(feeReceiver, _feeReceiver);

666:     emit InvestorBasedRateLimiterSet(
667:       address(investorBasedRateLimiter),
668:       _investorBasedRateLimiter
669:     );

770:     emit MintPaused();

776:     emit MintUnpaused();

782:     emit RedeemPaused();

788:     emit RedeemUnpaused();


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L558-L558) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L571-L571), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L589-L589), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L606-L609), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L625-L628), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L641-L641), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L654-L654), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L666-L669), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L770-L770), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L776-L776), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L782-L782), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L788-L788)


```solidity

File: ./contracts/ousg/rOUSG.sol

457:     emit Transfer(_sender, _recipient, _amount);

458:     emit TransferShares(_sender, _recipient, _sharesToTransfer);

481:     emit Approval(_owner, _spender, _amount);

614:     emit OracleSet(address(oracle), _oracle);

639:     emit TransferShares(_account, address(0), ousgSharesAmount);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L457-L457) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L458-L458), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L481-L481), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L614-L614), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L639-L639)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

096:     emit rOUSGDeployed(
097:       address(rOUSGProxy),
098:       address(rOUSGProxyAdmin),
099:       address(rOUSGImplementation),
100:       rOUSGProxied.name(),
101:       rOUSGProxied.symbol()
102:     );


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L96-L102) 


</details>


### [NC&#x2011;9] Defining All External/Public Functions in Contract Interfaces 
It is preferable to have all the external and public function in an interface to make using them easier by developers. This helps ensure the whole API is extracted in a interface.


*There are 20 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

479:   function getOUSGPrice() public view returns (uint256 price) {
480:     (price, ) = oracle.getPriceData();

768:   function pauseMint() external onlyRole(PAUSER_ROLE) {
769:     mintPaused = true;

774:   function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {
775:     mintPaused = false;

780:   function pauseRedeem() external onlyRole(PAUSER_ROLE) {
781:     redeemPaused = true;

786:   function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {
787:     redeemPaused = false;

819:   function retrieveTokens(
820:     address token,
821:     address to,
822:     uint256 amount
823:   ) external onlyRole(DEFAULT_ADMIN_ROLE) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L479-L480) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L768-L769), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L774-L775), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L780-L781), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L786-L787), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L819-L823)


```solidity

File: ./contracts/ousg/rOUSG.sol

102:   function initialize(
103:     address _kycRegistry,
104:     uint256 requirementGroup,
105:     address _ousg,
106:     address guardian,
107:     address _oracle
108:   ) public virtual initializer {

302:   function increaseAllowance(
303:     address _spender,
304:     uint256 _addedValue
305:   ) public returns (bool) {

328:   function decreaseAllowance(
329:     address _spender,
330:     uint256 _subtractedValue
331:   ) public returns (bool) {

347:   function getTotalShares() public view returns (uint256) {
348:     return totalShares;

356:   function sharesOf(address _account) public view returns (uint256) {
357:     return _sharesOf(_account);

363:   function getSharesByROUSG(
364:     uint256 _rOUSGAmount
365:   ) public view returns (uint256) {

373:   function getROUSGByShares(uint256 _shares) public view returns (uint256) {
374:     return

378:   function getOUSGPrice() public view returns (uint256 price) {
379:     (price, ) = oracle.getPriceData();

397:   function transferShares(
398:     address _recipient,
399:     uint256 _sharesAmount
400:   ) public returns (uint256) {

415:   function wrap(uint256 _OUSGAmount) external whenNotPaused {
416:     require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");

431:   function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
432:     require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");

642:   function pause() external onlyRole(PAUSER_ROLE) {
643:     _pause();

646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
647:     _unpause();


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L102-L108) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L302-L305), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L328-L331), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L347-L348), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L356-L357), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L363-L365), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L373-L374), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L378-L379), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L397-L400), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L415-L416), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L431-L432), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L642-L643), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L646-L647)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

70:   function deployRebasingOUSG(
71:     address kycRegistry,
72:     uint256 requirementGroup,
73:     address ousg,
74:     address oracle
75:   ) external onlyGuardian returns (address, address, address) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L70-L75) 


</details>


### [NC&#x2011;10] Duplicated `require()` checks should be refactored to a modifier or function 
The compiler will inline the function, which will avoid `JUMP` instructions usually associated with functions


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

808:       require(success, "Call Failed");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L808-L808) 


</details>


### [NC&#x2011;11] Imports could be organized more systematically 
The contract used interfaces should be imported first, followed by all other files. The examples below do not follow this layout.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

20: import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L20-L20) 


```solidity

File: ./contracts/ousg/rOUSG.sol

26: import "contracts/rwaOracles/IRWAOracle.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L26-L26) 


</details>


### [NC&#x2011;12] Import declarations should import specific identifiers, rather than the whole file 
Using import declarations of the form `import {<identifier_name>} from "some/ file.sol"` avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation


*There are 23 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

18: import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";

19: import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";

20: import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";

21: import "contracts/ousg/rOUSG.sol";

22: import "contracts/interfaces/IRWALike.sol";

23: import "contracts/interfaces/IBUIDLRedeemer.sol";

24: import "contracts/InstantMintTimeBasedRateLimiter.sol";

25: import "contracts/interfaces/IOUSGInstantManager.sol";

26: import "contracts/interfaces/IMulticall.sol";

27: import "contracts/interfaces/IInvestorBasedRateLimiter.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L19-L19), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L20-L20), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L21-L21), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L22-L22), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L23-L23), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L24-L24), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L25-L25), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L26-L26), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L27-L27)


```solidity

File: ./contracts/ousg/rOUSG.sol

18: import "contracts/external/openzeppelin/contracts/token/IERC20.sol";

19: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";

20: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";

21: import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";

22: import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";

23: import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";

24: import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";

25: import "contracts/kyc/KYCRegistryClientUpgradeable.sol";

26: import "contracts/rwaOracles/IRWAOracle.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L19-L19), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L20-L20), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L21-L21), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L22-L22), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L23-L23), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L24-L24), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L25-L25), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L26-L26)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

19: import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";

20: import "contracts/Proxy.sol";

21: import "contracts/ousg/rOUSG.sol";

22: import "contracts/interfaces/IMulticall.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L19-L19) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L20-L20), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L21-L21), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L22-L22)


</details>


### [NC&#x2011;13] Inconsistent spacing in comments 
Some lines use `// x` and some use `//x`. The instances below point out the usages that don't follow the majority, within each file


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

1: //SPDX-License-Identifier: BUSL-1.1


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L1-L1) 


</details>


### [NC&#x2011;14] Inconsistent usage of `require`/`error` 
Some parts of the codebase use `require` statements, while others use custom `error`s. Consider refactoring the code to use the same approach: the following findings represent the minority of `require` vs `error`, and they show the first occurance in each file, for brevity.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

435:       revert UnwrapTooSmall();

630:       revert UnwrapTooSmall();


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L435-L435) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L630-L630)


</details>


### [NC&#x2011;15] Long functions should be refactored into multiple, smaller, functions 



*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

278:   function _mint(

388:   function _redeem(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L278-L278) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L388-L388)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

70:   function deployRebasingOUSG(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L70-L70) 


</details>


### [NC&#x2011;16] Long lines of code 
Usually lines in source code are limited to [80](https://softwareengineering.stackexchange.com/questions/148677/why-is-80-characters-the-standard-limit-for-code-width) characters. Today's screens are much larger so it's reasonable to stretch this in some cases. The solidity style guide recommends a maximumum line length of [120 characters](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#maximum-line-length), so the lines below should be split when they reach that length.


*There are 15 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

6:  bb ,bbB, bbbbbb  b�bb bbb      bbbbb�b�bbbb   bbbb    bb  bbbb�b�b�bbbb    bbbbb�b�bbb,

7: bb  bb bbb�'   bbb bbb bb     bbb      bbb  bbbbb,  bb  bbb    bbbb  bbb     bbbb

8: bb bbb bb      bb  bb bb     bbb      bbb  bb bbbb bb  bbb     bbb jbb       bbb

9: bb  bb bbb    bbb� bbb bb     bbb      bbb  bb   bbbbb  bbb    bbbb�  bbb     ,bbb�

10:  bb "bb, bb�b�bbbbbbbbbbbb      bbbbbbbbbb�   bb     bbb  bbbbbbbb�b�     bbbbbbbbb�`


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L6-L6) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L7-L7), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L8-L8), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L9-L9), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L10-L10)


```solidity

File: ./contracts/ousg/rOUSG.sol

6:  baabaa ,baabaaB, baabaabaabaabaabaa  baabaabaa baabaabaa      baabaabaabaabaabaabaabaabaabaa   baabaabaabaa    baabaa  baabaabaabaabaabaabaabaabaabaa    baabaabaabaabaabaabaabaabaa,

7: baabaa  baabaa baabaabaa'   baabaabaa baabaabaa baabaa     baabaabaa      baabaabaa  baabaabaabaabaa,  baabaa  baabaabaa    baabaabaabaa  baabaabaa     baabaabaabaa

8: baabaa baabaabaa baabaa      baabaa  baabaa baabaa     baabaabaa      baabaabaa  baabaa baabaabaabaa baabaa  baabaabaa     baabaabaa jbaabaa       baabaabaa

9: baabaa  baabaa baabaabaa    baabaabaa baabaabaa baabaa     baabaabaa      baabaabaa  baabaa   baabaabaabaabaa  baabaabaa    baabaabaabaa  baabaabaa     ,baabaabaa

10:  baabaa "baabaa, baabaabaabaabaabaabaabaabaabaabaabaabaabaabaa      baabaabaabaabaabaabaabaabaabaa   baabaa     baabaabaa  baabaabaabaabaabaabaabaabaa     baabaabaabaabaabaabaabaabaa`


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L6-L6) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L7-L7), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L8-L8), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L9-L9), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L10-L10)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

6:  bb ,bbB, bbbbbb  b�bb bbb      bbbbb�b�bbbb   bbbb    bb  bbbb�b�b�bbbb    bbbbb�b�bbb,

7: bb  bb bbb�'   bbb bbb bb     bbb      bbb  bbbbb,  bb  bbb    bbbb  bbb     bbbb

8: bb bbb bb      bb  bb bb     bbb      bbb  bb bbbb bb  bbb     bbb jbb       bbb

9: bb  bb bbb    bbb� bbb bb     bbb      bbb  bb   bbbbb  bbb    bbbb�  bbb     ,bbb�

10:  bb "bb, bb�b�bbbbbbbbbbbb      bbbbbbbbbb�   bb     bbb  bbbbbbbb�b�     bbbbbbbbb�`


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L6-L6) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L7-L7), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L8-L8), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L9-L9), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L10-L10)


</details>


### [NC&#x2011;17] Consider using later versions of solidity for more cappabilities 
Consider using solidity 0.8.18 or later to benefit from multiple things including the named mappings [named mappings](https://ethereum.stackexchange.com/a/145555) to make it easier to understand the purpose of each mapping


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L16-L16) 


</details>


### [NC&#x2011;18] Some error strings are not descriptive 
Consider adding more detail to these error strings


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit This message need more details : Call Failed
808:       require(success, "Call Failed");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L808-L808) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

//@audit This message need more details : Call Failed
129:       require(success, "Call Failed");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L129-L129) 


</details>


### [NC&#x2011;19] Use of `override` is unnecessary 
Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the `override` keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.


*There are 20 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

230:   function mint(
231:     uint256 usdcAmountIn
232:   )
233:     external
234:     override

254:   function mintRebasingOUSG(
255:     uint256 usdcAmountIn
256:   )
257:     external
258:     override

335:   function redeem(
336:     uint256 ousgAmountIn
337:   )
338:     external
339:     override

362:   function redeemRebasingOUSG(
363:     uint256 rousgAmountIn
364:   )
365:     external
366:     override

498:   function setInstantMintLimit(
499:     uint256 _instantMintLimit
500:   ) external override onlyRole(CONFIGURER_ROLE) {

512:   function setInstantRedemptionLimit(
513:     uint256 _instantRedemptionLimit
514:   ) external override onlyRole(CONFIGURER_ROLE) {

526:   function setInstantMintLimitDuration(
527:     uint256 _instantMintLimitDuration
528:   ) external override onlyRole(CONFIGURER_ROLE) {

540:   function setInstantRedemptionLimitDuration(
541:     uint256 _instantRedemptionLimitDuratioin
542:   ) external override onlyRole(CONFIGURER_ROLE) {

554:   function setMintFee(
555:     uint256 _mintFee
556:   ) external override onlyRole(CONFIGURER_ROLE) {

567:   function setRedeemFee(
568:     uint256 _redeemFee
569:   ) external override onlyRole(CONFIGURER_ROLE) {

581:   function setMinimumDepositAmount(
582:     uint256 _minimumDepositAmount
583:   ) external override onlyRole(CONFIGURER_ROLE) {

599:   function setMinimumRedemptionAmount(
600:     uint256 _minimumRedemptionAmount
601:   ) external override onlyRole(CONFIGURER_ROLE) {

622:   function setMinimumBUIDLRedemptionAmount(
623:     uint256 _minimumBUIDLRedemptionAmount
624:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

638:   function setOracle(
639:     address _oracle
640:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

650:   function setFeeReceiver(
651:     address _feeReceiver
652:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

663:   function setInvestorBasedRateLimiter(
664:     address _investorBasedRateLimiter
665:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

794:   function multiexcall(
795:     ExCallData[] calldata exCallData
796:   )
797:     external
798:     payable
799:     override


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L230-L234) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L254-L258), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L335-L339), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L362-L366), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L498-L500), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L512-L514), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L526-L528), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L540-L542), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L554-L556), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L567-L569), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L581-L583), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L599-L601), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L622-L624), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L638-L640), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L652), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L663-L665), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L799)


```solidity

File: ./contracts/ousg/rOUSG.sol

650:   function setKYCRegistry(
651:     address registry
652:   ) external override onlyRole(CONFIGURER_ROLE) {

656:   function setKYCRequirementGroup(
657:     uint256 group
658:   ) external override onlyRole(CONFIGURER_ROLE) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L652) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L658)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L121-L123) 


</details>


### [NC&#x2011;20] Redundant inheritance specifier 
The contracts below already extend the specified contract, so there is no need to list it in the inheritance list again


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

//@audit `Initializable` is already inherited by `ContextUpgradeable` 
55: contract ROUSG is
56:   Initializable,
57:   ContextUpgradeable,

//@audit `ContextUpgradeable` is already inherited by `PausableUpgradeable` 
55: contract ROUSG is
56:   Initializable,
57:   ContextUpgradeable,
58:   PausableUpgradeable,

//@audit `IERC20Upgradeable` is already inherited by `IERC20MetadataUpgradeable` 
55: contract ROUSG is
56:   Initializable,
57:   ContextUpgradeable,
58:   PausableUpgradeable,
59:   AccessControlEnumerableUpgradeable,
60:   KYCRegistryClientUpgradeable,
61:   IERC20Upgradeable,
62:   IERC20MetadataUpgradeable


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L55-L57) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L55-L58), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L55-L62)


</details>


### [NC&#x2011;21] Setters should prevent re-setting of the same value 
This especially problematic when the setter also emits the same value, which may be confusing to offline parsers


*There are 6 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit `mintFee` and `_mintFee` are never checked for the same value setting
554:   function setMintFee(
555:     uint256 _mintFee
556:   ) external override onlyRole(CONFIGURER_ROLE) {
557:     require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558:     emit MintFeeSet(mintFee, _mintFee);
559:     mintFee = _mintFee;

//@audit `redeemFee` and `_redeemFee` are never checked for the same value setting
567:   function setRedeemFee(
568:     uint256 _redeemFee
569:   ) external override onlyRole(CONFIGURER_ROLE) {
570:     require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571:     emit RedeemFeeSet(redeemFee, _redeemFee);
572:     redeemFee = _redeemFee;

//@audit `minimumDepositAmount` and `_minimumDepositAmount` are never checked for the same value setting
581:   function setMinimumDepositAmount(
582:     uint256 _minimumDepositAmount
583:   ) external override onlyRole(CONFIGURER_ROLE) {
584:     require(
585:       _minimumDepositAmount >= FEE_GRANULARITY,
586:       "setMinimumDepositAmount: Amount too small"
587:     );
588: 
589:     emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
590:     minimumDepositAmount = _minimumDepositAmount;

//@audit `minimumRedemptionAmount` and `_minimumRedemptionAmount` are never checked for the same value setting
599:   function setMinimumRedemptionAmount(
600:     uint256 _minimumRedemptionAmount
601:   ) external override onlyRole(CONFIGURER_ROLE) {
602:     require(
603:       _minimumRedemptionAmount >= FEE_GRANULARITY,
604:       "setMinimumRedemptionAmount: Amount too small"
605:     );
606:     emit MinimumRedemptionAmountSet(
607:       minimumRedemptionAmount,
608:       _minimumRedemptionAmount
609:     );
610:     minimumRedemptionAmount = _minimumRedemptionAmount;

//@audit `minBUIDLRedeemAmount` and `_minimumBUIDLRedemptionAmount` are never checked for the same value setting
622:   function setMinimumBUIDLRedemptionAmount(
623:     uint256 _minimumBUIDLRedemptionAmount
624:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
625:     emit MinimumBUIDLRedemptionAmountSet(
626:       minBUIDLRedeemAmount,
627:       _minimumBUIDLRedemptionAmount
628:     );
629:     minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;

//@audit `feeReceiver` and `_feeReceiver` are never checked for the same value setting
650:   function setFeeReceiver(
651:     address _feeReceiver
652:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
653:     require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
654:     emit FeeReceiverSet(feeReceiver, _feeReceiver);
655:     feeReceiver = _feeReceiver;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L554-L559) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L567-L572), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L581-L590), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L599-L610), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L622-L629), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L655)


</details>


### [NC&#x2011;22] Consider using `SafeTransferLib.safeTransferETH()` or `Address.sendValue()` for clearer semantic meaning 
These Functions indicate their purpose with their name more clearly than using low-level calls.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L805-L805) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L126-L126) 


</details>


### [NC&#x2011;23] Large multiples of ten should use scientific notation (e.g. `1e6`) rather than decimal literals (e.g. `1000000`), for readability 
While the compiler knows to optimize away the exponentiation, it's still better coding practice to use idioms that do not require compiler optimization, if they exist


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit `10_000`
66:   uint256 public constant FEE_GRANULARITY = 10_000;

//@audit `10_000`
69:   uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L66-L66) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L69-L69)


```solidity

File: ./contracts/ousg/rOUSG.sol

//@audit `10_000`
87:   uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L87-L87) 


</details>


### [NC&#x2011;24] Consider moving `msg.sender` checks to a common authorization `modifier` 



*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

299:       usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,

345:       ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,

372:       rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L299-L299) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L345-L345), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L372-L372)


</details>


### [NC&#x2011;25] State variables should have `Natspec` comments 
Consider adding some `Natspec` comments on critical state variables to explain what they are supposed to do: this will help for future code reviews.


*There are 34 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit CONFIGURER_ROLE need comments
57:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");

//@audit PAUSER_ROLE need comments
60:   bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");

//@audit MINIMUM_OUSG_PRICE need comments
63:   uint256 public constant MINIMUM_OUSG_PRICE = 105e18;

//@audit FEE_GRANULARITY need comments
66:   uint256 public constant FEE_GRANULARITY = 10_000;

//@audit OUSG_TO_ROUSG_SHARES_MULTIPLIER need comments
69:   uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;

//@audit usdc need comments
72:   IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;

//@audit ousg need comments
75:   IRWALike public immutable ousg;

//@audit rousg need comments
78:   ROUSG public immutable rousg;

//@audit buidl need comments
81:   IERC20 public immutable buidl;

//@audit buidlRedeemer need comments
84:   IBUIDLRedeemer public immutable buidlRedeemer;

//@audit decimalsMultiplier need comments
87:   uint256 public immutable decimalsMultiplier;

//@audit usdcReceiver need comments
90:   address public immutable usdcReceiver;

//@audit oracle need comments
93:   IRWAOracle public oracle;

//@audit feeReceiver need comments
96:   address public feeReceiver;

//@audit mintFee need comments
99:   uint256 public mintFee = 0;

//@audit redeemFee need comments
102:   uint256 public redeemFee = 0;

//@audit minimumDepositAmount need comments
106:   uint256 public minimumDepositAmount = 100_000e6;

//@audit minimumRedemptionAmount need comments
110:   uint256 public minimumRedemptionAmount = 50_000e6;

//@audit mintPaused need comments
113:   bool public mintPaused;

//@audit redeemPaused need comments
116:   bool public redeemPaused;

//@audit minBUIDLRedeemAmount need comments
120:   uint256 public minBUIDLRedeemAmount = 250_000e6;

//@audit investorBasedRateLimiter need comments
123:   IInvestorBasedRateLimiter public investorBasedRateLimiter;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L57-L57) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L60-L60), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L63-L63), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L66-L66), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L69-L69), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L72-L72), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L75-L75), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L78-L78), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L84-L84), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L87-L87), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L90-L90), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L93-L93), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L96-L96), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L99-L99), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L106-L106), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L110-L110), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L113-L113), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L116-L116), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L120-L120), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L123-L123)


```solidity

File: ./contracts/ousg/rOUSG.sol

//@audit totalShares need comments
78:   uint256 private totalShares;

//@audit oracle need comments
81:   IRWAOracle public oracle;

//@audit ousg need comments
84:   IERC20 public ousg;

//@audit OUSG_TO_ROUSG_SHARES_MULTIPLIER need comments
87:   uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;

//@audit BURNER_ROLE need comments
94:   bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");

//@audit CONFIGURER_ROLE need comments
95:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L78-L78) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L84-L84), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L87-L87), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L94-L94), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L95-L95)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

//@audit DEFAULT_ADMIN_ROLE need comments
38:   bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);

//@audit guardian need comments
40:   address internal immutable guardian;

//@audit rOUSGImplementation need comments
41:   ROUSG public rOUSGImplementation;

//@audit rOUSGProxyAdmin need comments
42:   ProxyAdmin public rOUSGProxyAdmin;

//@audit rOUSGProxy need comments
43:   TokenProxy public rOUSGProxy;

//@audit initialized need comments
45:   bool public initialized = false;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L38-L38) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L40-L40), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L41-L41), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L42-L42), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L43-L43), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L45-L45)


</details>


### [NC&#x2011;26] Contracts should have full test coverage 
While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

@audit Multiple files
1: 


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L1-L1) 


</details>


### [NC&#x2011;27] Top level pragma declarations should be separated by two blank lines 



*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;
17: 
18: import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L16-L18) 


```solidity

File: ./contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;
17: 
18: import "contracts/external/openzeppelin/contracts/token/IERC20.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L16-L18) 


</details>


### [NC&#x2011;28] Critical functions should be a two step procedure 
Critical functions in Solidity contracts should follow a two-step procedure to enhance security, minimize human error, and ensure proper access control. By dividing sensitive operations into distinct phases, such as initiation and confirmation, developers can introduce a safeguard against unintended actions or unauthorized access.


*There are 15 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

498:   function setInstantMintLimit(

512:   function setInstantRedemptionLimit(

526:   function setInstantMintLimitDuration(

540:   function setInstantRedemptionLimitDuration(

554:   function setMintFee(

567:   function setRedeemFee(

581:   function setMinimumDepositAmount(

599:   function setMinimumRedemptionAmount(

622:   function setMinimumBUIDLRedemptionAmount(

638:   function setOracle(

650:   function setFeeReceiver(

663:   function setInvestorBasedRateLimiter(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L498-L498) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L512-L512), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L526-L526), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L540-L540), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L554-L554), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L567-L567), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L581-L581), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L599-L599), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L622-L622), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L638-L638), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L663-L663)


```solidity

File: ./contracts/ousg/rOUSG.sol

613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L613-L613) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L656)


</details>


### [NC&#x2011;29] Typos 
Modifiers in Solidity can improve code readability and modularity by encapsulating repetitive checks, such as address validity checks, into a reusable construct. For example, an `onlyOwner` modifier can be used to replace repetitive `require(msg.sender == owner)` checks across several functions, reducing code redundancy and enhancing maintainability. To implement, define a modifier with the check, then apply the modifier to relevant functions.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit `specifed` is misspelled
219:   /**
220:    * @notice Calculates fees and triggers minting OUSG for a given amount of USDC
221:    *
222:    * @dev Please note that the fees are accumulated in `feeReceiver`
223:    *
224:    * @param usdcAmountIn amount of USDC exchanged for OUSG (in whatever decimals
225:    *                     specifed by usdc token contract)
226:    *
227:    * @return ousgAmountOut The quantity of OUSG minted for the user
228:    *                       (18 decimals per OUSG contract)
229:    */

//@audit `specifed` is misspelled
243:   /**
244:    * @notice Calculates fees and triggers minting rOUSG for a given amount of USDC
245:    *
246:    * @dev Please note that the fees are accumulated in `feeReceiver`
247:    *
248:    * @param usdcAmountIn amount of USDC exchanged for rOUSG (in whatever decimals
249:    *                     specifed by usdc token contract)
250:    *
251:    * @return rousgAmountOut The quantity of rOUSG minted for the user
252:    *                        (18 decimals per rOUSG contract)
253:    */


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L219-L229) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L243-L253)


</details>


### [NC&#x2011;30] Unused Import 
Some files/Items are imported but never used


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit `rOUSG` is not used
21: import "contracts/ousg/rOUSG.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L21-L21) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

//@audit `rOUSG` is not used
21: import "contracts/ousg/rOUSG.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L21-L21) 


</details>


### [NC&#x2011;31] Missing upgradability functionality 
At the begining of a project, there is always the need to modify of add something to the source code especialy if any vulnerability is discovered. Therefore, having such system is crusial at least at the first stages of the project


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

49: contract OUSGInstantManager is


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L49-L49) 


</details>


### [NC&#x2011;32] Use the latest solidity (prior to 0.8.20 if on L2s) for deployment 
```
When deploying contracts, you should use the latest released version of Solidity.Apart from exceptional cases, only the latest version receives security fixes.
```
https://docs.soliditylang.org/en/v0.8.20/


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L16-L16) 


</details>


### [NC&#x2011;33] Use a single file for system wide constants 
Consider grouping all the system constants under a single file. This finding shows only the first constant for each file.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

57:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L57-L57) 


```solidity

File: ./contracts/ousg/rOUSG.sol

87:   uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L87-L87) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

38:   bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L38-L38) 


</details>


### [NC&#x2011;34] Consider using SMTChecker 
The SMTChecker is a valuable tool for Solidity developers as it helps detect potential vulnerabilities and logical errors in the contract's code. By utilizing Satisfiability Modulo Theories (SMT) solvers, it can reason about the potential states a contract can be in, and therefore, identify conditions that could lead to undesirable behavior. This automatic formal verification can catch issues that might otherwise be missed in manual code reviews or standard testing, enhancing the overall contract's security and reliability.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L16-L16) 


</details>


### [NC&#x2011;35] Whitespace in Expressions 
See the [Whitespace in Expressions](https://docs.soliditylang.org/en/latest/style-guide.html#whitespace-in-expressions) section of the Solidity Style Guide


*There are 12 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit remove the whiteSpace before the ',' char
4:    bbbb�b ,bbbb, 'b�bbb
5:   bbb� bbbb�b�bbb�b�bbb bbbB5           ,,       ,,      ,     ,,,            ,,,

//@audit remove the whiteSpace before the ',' char
5:   bbb� bbbb�b�bbb�b�bbb bbbB5           ,,       ,,      ,     ,,,            ,,,
6:  bb ,bbB, bbbbbb  b�bb bbb      bbbbb�b�bbbb   bbbb    bb  bbbb�b�b�bbbb    bbbbb�b�bbb,

//@audit remove the whiteSpace before the ',' char
6:  bb ,bbB, bbbbbb  b�bb bbb      bbbbb�b�bbbb   bbbb    bb  bbbb�b�b�bbbb    bbbbb�b�bbb,
7: bb  bb bbb�'   bbb bbb bb     bbb      bbb  bbbbb,  bb  bbb    bbbb  bbb     bbbb

//@audit remove the whiteSpace before the ')' char
480:     (price, ) = oracle.getPriceData();
481:     require(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L4-L5) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L5-L6), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L6-L7), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L480-L481)


```solidity

File: ./contracts/ousg/rOUSG.sol

//@audit remove the whiteSpace before the ',' char
4:    baabaabaabaabaa ,baabaabaabaa, 'baabaabaabaa
5:   baabaabaa baabaabaabaabaabaabaabaabaabaabaabaa baabaabaaB5           ,,       ,,      ,     ,,,            ,,,

//@audit remove the whiteSpace before the ',' char
5:   baabaabaa baabaabaabaabaabaabaabaabaabaabaabaa baabaabaaB5           ,,       ,,      ,     ,,,            ,,,
6:  baabaa ,baabaaB, baabaabaabaabaabaa  baabaabaa baabaabaa      baabaabaabaabaabaabaabaabaabaa   baabaabaabaa    baabaa  baabaabaabaabaabaabaabaabaabaa    baabaabaabaabaabaabaabaabaa,

//@audit remove the whiteSpace before the ',' char
6:  baabaa ,baabaaB, baabaabaabaabaabaa  baabaabaa baabaabaa      baabaabaabaabaabaabaabaabaabaa   baabaabaabaa    baabaa  baabaabaabaabaabaabaabaabaabaa    baabaabaabaabaabaabaabaabaa,
7: baabaa  baabaa baabaabaa'   baabaabaa baabaabaa baabaa     baabaabaa      baabaabaa  baabaabaabaabaa,  baabaa  baabaabaa    baabaabaabaa  baabaabaa     baabaabaabaa

//@audit remove the whiteSpace before the ',' char
09: baabaa  baabaa baabaabaa    baabaabaa baabaabaa baabaa     baabaabaa      baabaabaa  baabaa   baabaabaabaabaa  baabaabaa    baabaabaabaa  baabaabaa     ,baabaabaa
10:  baabaa "baabaa, baabaabaabaabaabaabaabaabaabaabaabaabaabaabaa      baabaabaabaabaabaabaabaabaabaa   baabaa     baabaabaa  baabaabaabaabaabaabaabaabaa     baabaabaabaabaabaabaabaabaa`

//@audit remove the whiteSpace before the ')' char
379:     (price, ) = oracle.getPriceData();
380:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L4-L5) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L5-L6), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L6-L7), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L9-L10), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L379-L380)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

//@audit remove the whiteSpace before the ',' char
4:    bbbb�b ,bbbb, 'b�bbb
5:   bbb� bbbb�b�bbb�b�bbb bbbB5           ,,       ,,      ,     ,,,            ,,,

//@audit remove the whiteSpace before the ',' char
5:   bbb� bbbb�b�bbb�b�bbb bbbB5           ,,       ,,      ,     ,,,            ,,,
6:  bb ,bbB, bbbbbb  b�bb bbb      bbbbb�b�bbbb   bbbb    bb  bbbb�b�b�bbbb    bbbbb�b�bbb,

//@audit remove the whiteSpace before the ',' char
6:  bb ,bbB, bbbbbb  b�bb bbb      bbbbb�b�bbbb   bbbb    bb  bbbb�b�b�bbbb    bbbbb�b�bbb,
7: bb  bb bbb�'   bbb bbb bb     bbb      bbb  bbbbb,  bb  bbb    bbbb  bbb     bbbb


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L4-L5) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L5-L6), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L6-L7)


</details>


### [NC&#x2011;36] Consider bounding input array length 
The functions below take in an unbounded array, and make function calls for entries in the array. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to `require()` that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit array name exCallData
794:   function multiexcall(
795:     ExCallData[] calldata exCallData
796:   )
797:     external
798:     payable
799:     override
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
803:     results = new bytes[](exCallData.length);
804:     for (uint256 i = 0; i < exCallData.length; ++i) {
805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
806:         value: exCallData[i].value
807:       }(exCallData[i].data);
808:       require(success, "Call Failed");
809:       results[i] = ret;
810:     }
811:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L811) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

//@audit array name exCallData
121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {
124:     results = new bytes[](exCallData.length);
125:     for (uint256 i = 0; i < exCallData.length; ++i) {
126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
127:         value: exCallData[i].value
128:       }(exCallData[i].data);
129:       require(success, "Call Failed");
130:       results[i] = ret;
131:     }
132:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L121-L132) 


</details>


### [NC&#x2011;37] [NatSpec] Natspec `@dev` is missing from `contract` 



*There are 55 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

278:   function _mint(

388:   function _redeem(

458:   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {

490:   /**
491:    * @notice Set the mintLimit constraint inside the InstantMintTimeBasedRateLimiter
492:    *         base contract
493:    *
494:    * @param _instantMintLimit New limit that dicates how much USDC can be transfered
495:    *                     for minting in a specified duration
496:    *                     (in 6 decimals per the USDC contract)
497:    */

504:   /**
505:    * @notice Set the redeemLimit constraint inside the InstantMintTimeBasedRateLimiter
506:    *         base contract
507:    *
508:    * @param _instantRedemptionLimit New limit that dicates how much USDC
509:    *                       can be redeemed in a specified duration
510:    *                       (in 6 decimals per the USDC contract)
511:    */

518:   /**
519:    * @notice Sets mintLimitDuration constraint inside the InstantMintTimeBasedRateLimiter
520:    *         base contract
521:    *
522:    * @param _instantMintLimitDuration New limit that specifies the interval
523:    *                             (in seconds) in which only `mintLimit` USDC
524:    *                             can be used for minting within
525:    */

532:   /**
533:    * @notice Sets redeemLimitDuration inside the InstantMintTimeBasedRateLimiter
534:    *         base contract
535:    *
536:    * @param _instantRedemptionLimitDuratioin New limit that specifies the interval
537:    *                               (in seconds) in which only `redeemLimit` USDC
538:    *                               can be redeemed within
539:    */

549:   /**
550:    * @notice Sets the mint fee
551:    *
552:    * @param _mintFee new mint fee specified in basis points
553:    */

562:   /**
563:    * @notice Sets the redeem fee.
564:    *
565:    * @param _redeemFee new redeem fee specified in basis points
566:    */

575:   /**
576:    * @notice Admin function to set the minimum amount required for a deposit
577:    *
578:    * @param _minimumDepositAmount The minimum amount required to submit a deposit
579:    *                          request
580:    */

593:   /**
594:    * @notice Admin function to set the minimum amount to redeem
595:    *
596:    * @param _minimumRedemptionAmount The minimum amount required to submit a
597:    *                                 redemption request
598:    */

617:   /**
618:    * @notice Admin function to set the minimum amount required to redeem BUIDL
619:    *
620:    * @param _minimumBUIDLRedemptionAmount The minimum amount required to redeem BUIDL
621:    */

632:   /**
633:    * @notice Admin function to set the oracle address
634:    *
635:    * @param _oracle The address of the oracle that provides the OUSG price
636:    *                in USDC
637:    */

645:   /**
646:    * @notice Admin function to set the fee receiver address
647: 
648:    * @param _feeReceiver The address to receive the mint and redemption fees
649:    */

658:   /**
659:    * @notice Admin function to set the optional investor-based rate limiter
660:    *
661:    * @param _investorBasedRateLimiter The address of the investor-based rate limiter contract
662:    */

679:   /**
680:    * @notice Given a deposit amount and a price, returns the OUSG amount due
681:    *
682:    * @param usdcAmountIn The amount deposited in units of USDC
683:    * @param price        The price at which to mint
684:    */

693:   /**
694:    * @notice Given a redemption amount and a price, returns the USDC amount due
695:    *
696:    * @param ousgAmountBurned The amount of OUSG burned for a redemption
697:    * @param price            The price at which to redeem
698:    */

707:   /**
708:    * @notice Given amount of USDC, returns how much in fees are owed
709:    *
710:    * @param usdcAmount Amount of USDC to calculate fees
711:    *                   (in 6 decimals)
712:    */

719:   /**
720:    * @notice Given amount of USDC, returns how much in fees are owed
721:    *
722:    * @param usdcAmount Amount USDC to calculate fees
723:    *                   (in decimals of USDC)
724:    */

755:   /// @notice Ensure that the mint functionality is not paused

761:   /// @notice Ensure that the redeem functionality is not paused

767:   /// @notice Pause the mint functionality

773:   /// @notice Unpause the mint functionality

779:   /// @notice Pause the redeem functionality

785:   /// @notice Unpause the redeem functionality

794:   function multiexcall(

813:   /**
814:    * @notice Rescue and transfer tokens locked in this contract
815:    * @param token The address of the token
816:    * @param to The address of the recipient
817:    * @param amount The amount of token to transfer
818:    */


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L278-L278) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L388-L388), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L458-L458), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L490-L497), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L504-L511), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L518-L525), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L532-L539), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L549-L553), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L562-L566), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L575-L580), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L593-L598), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L617-L621), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L632-L637), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L645-L649), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L658-L662), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L679-L684), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L693-L698), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L707-L712), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L719-L724), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L755-L755), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L761-L761), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L767-L767), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L773-L773), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L779-L779), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L785-L785), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L794), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L813-L818)


```solidity

File: ./contracts/ousg/rOUSG.sol

28: /**
29:  * @title Interest-bearing ERC20-like token for OUSG.
30:  *
31:  * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
32:  * controlled by the protocol. To calculate each account's balance, we do
33:  *
34:  *   shares[account] * ousgPrice
35:  *
36:  * For example, assume that we have:
37:  *
38:  *   ousgPrice = 100.505
39:  *   sharesOf(user1) -> 100
40:  *   sharesOf(user2) -> 400
41:  *
42:  * Therefore:
43:  *
44:  *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
45:  *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
46:  *
47:  * Since balances of all token holders change when the price of OUSG changes, this
48:  * token cannot fully implement ERC20 standard: it only emits `Transfer` events
49:  * upon explicit transfer between holders. In contrast, when total amount of pooled
50:  * Cash increases, no `Transfer` events are generated: doing so would require emitting
51:  * an event for each token holder and thus running an unbounded loop.
52:  *
53:  */

90:   error UnwrapTooSmall();

97:   /// @custom:oz-upgrades-unsafe-allow constructor

102:   function initialize(

112:   function __rOUSG_init(

128:   function __rOUSG_init_unchained(

155:   /**
156:    * @notice Emitted when the oracle address is set
157:    *
158:    * @param oldOracle The address of the old oracle
159:    * @param newOracle The address of the new oracle
160:    */

163:   /**
164:    * @return the name of the token.
165:    */

170:   /**
171:    * @return the symbol of the token, usually a shorter version of the
172:    * name.
173:    */

178:   /**
179:    * @return the number of decimals for getting user representation of a token amount.
180:    */

185:   /**
186:    * @return the amount of tokens in existence.
187:    */

289:   /**
290:    * @notice Atomically increases the allowance granted to `_spender` by the caller by `_addedValue`.
291:    *
292:    * This is an alternative to `approve` that can be used as a mitigation for
293:    * problems described in:
294:    * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42
295:    * Emits an `Approval` event indicating the updated allowance.
296:    *
297:    * Requirements:
298:    *
299:    * - `_spender` cannot be the the zero address.
300:    * - the contract must not be paused.
301:    */

314:   /**
315:    * @notice Atomically decreases the allowance granted to `_spender` by the caller by `_subtractedValue`.
316:    *
317:    * This is an alternative to `approve` that can be used as a mitigation for
318:    * problems described in:
319:    * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42
320:    * Emits an `Approval` event indicating the updated allowance.
321:    *
322:    * Requirements:
323:    *
324:    * - `_spender` cannot be the zero address.
325:    * - `_spender` must have allowance for the caller of at least `_subtractedValue`.
326:    * - the contract must not be paused.
327:    */

360:   /**
361:    * @return the amount of shares that corresponds to `_rOUSGAmount` of rOUSG
362:    */

370:   /**
371:    * @return the amount of rOUSG that corresponds to `_shares` of OUSG.
372:    */

378:   function getOUSGPrice() public view returns (uint256 price) {

445:   /**
446:    * @notice Moves `_amount` tokens from `_sender` to `_recipient`.
447:    * Emits a `Transfer` event.
448:    * Emits a `TransferShares` event.
449:    */

461:   /**
462:    * @notice Sets `_amount` as the allowance of `_spender` over the `_owner` s tokens.
463:    *
464:    * Emits an `Approval` event.
465:    *
466:    * Requirements:
467:    *
468:    * - `_owner` cannot be the zero address.
469:    * - `_spender` cannot be the zero address.
470:    * - the contract must not be paused.
471:    */

484:   /**
485:    * @return the amount of shares owned by `_account`.
486:    */

491:   /**
492:    * @notice Moves `_sharesAmount` shares from `_sender` to `_recipient`.
493:    *
494:    * Requirements:
495:    *
496:    * - `_sender` cannot be the zero address.
497:    * - `_recipient` cannot be the zero address.
498:    * - `_sender` must hold at least `_sharesAmount` shares.
499:    * - the contract must not be paused.
500:    */

521:   /**
522:    * @notice Creates `_sharesAmount` shares and assigns them to `_recipient`, increasing the total amount of shares.
523:    *
524:    * Requirements:
525:    *
526:    * - `_recipient` cannot be the zero address.
527:    * - the contract must not be paused.
528:    */

642:   function pause() external onlyRole(PAUSER_ROLE) {

646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L28-L53) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L90-L90), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L97-L97), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L155-L160), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L163-L165), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L170-L173), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L178-L180), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L185-L187), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L289-L301), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L314-L327), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L360-L362), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L370-L372), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L378-L378), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L445-L449), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L461-L471), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L484-L486), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L491-L500), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L521-L528), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L642-L642), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L646-L646), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L656)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

24: /**
25:  * @title ROUSGFactory
26:  * @author Ondo Finance
27:  * @notice This contract serves as a Factory for the upgradable rOUSG token contract.
28:  *         Upon calling `deployRebasingOUSG` the `guardian` address (set in constructor) will
29:  *         deploy the following:
30:  *         1) rOUSG - The implementation contract, ERC20 contract with the initializer disabled
31:  *         2) ProxyAdmin - OZ ProxyAdmin contract, used to upgrade the proxy instance.
32:  *                         @notice Owner is set to `guardian` address.
33:  *         3) TransparentUpgradeableProxy - OZ, proxy contract. Admin is set to `address(proxyAdmin)`.
34:  *                                          `_logic' is set to `address(rOUSG)`.
35:  * @notice `guardian` address in constructor is a msig.
36:  */

47:   constructor(address _guardian) {

149:   modifier onlyGuardian() {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L24-L36) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L47-L47), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L149-L149)


</details>


### [NC&#x2011;38] Add inline comments for unnamed variables 
`function foo(address x, address)` -> `function foo(address x, address /* y */)`


*There are 5 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit parameters 1, need comment
335:   function redeem(
336:     uint256 ousgAmountIn

//@audit parameters 1, need comment
362:   function redeemRebasingOUSG(
363:     uint256 rousgAmountIn

//@audit parameters 1, need comment
581:   function setMinimumDepositAmount(
582:     uint256 _minimumDepositAmount

//@audit parameters 1, need comment
599:   function setMinimumRedemptionAmount(
600:     uint256 _minimumRedemptionAmount

//@audit parameters 1, need comment
650:   function setFeeReceiver(
651:     address _feeReceiver


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L335-L336) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L362-L363), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L581-L582), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L599-L600), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L651)


</details>


### [NC&#x2011;39] Contract should expose an `interface` 
The `contract`s should expose an `interface` so that other projects can more easily integrate with it, without having to develop their own non-standard variants.


*There are 19 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

479:   function getOUSGPrice() public view returns (uint256 price) {

768:   function pauseMint() external onlyRole(PAUSER_ROLE) {

774:   function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {

780:   function pauseRedeem() external onlyRole(PAUSER_ROLE) {

786:   function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {

819:   function retrieveTokens(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L479-L479) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L768-L768), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L774-L774), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L780-L780), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L786-L786), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L819-L819)


```solidity

File: ./contracts/ousg/rOUSG.sol

302:   function increaseAllowance(

328:   function decreaseAllowance(

347:   function getTotalShares() public view returns (uint256) {

356:   function sharesOf(address _account) public view returns (uint256) {

363:   function getSharesByROUSG(

373:   function getROUSGByShares(uint256 _shares) public view returns (uint256) {

378:   function getOUSGPrice() public view returns (uint256 price) {

397:   function transferShares(

415:   function wrap(uint256 _OUSGAmount) external whenNotPaused {

431:   function unwrap(uint256 _rOUSGAmount) external whenNotPaused {

642:   function pause() external onlyRole(PAUSER_ROLE) {

646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L302-L302) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L328-L328), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L347-L347), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L356-L356), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L363-L363), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L373-L373), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L378-L378), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L397-L397), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L415-L415), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L431-L431), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L642-L642), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L646-L646)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

70:   function deployRebasingOUSG(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L70-L70) 


</details>


### [NC&#x2011;40] Named imports of parent contracts are missing 



*There are 13 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit `ReentrancyGuard`
50:   ReentrancyGuard,

//@audit `InstantMintTimeBasedRateLimiter`
51:   InstantMintTimeBasedRateLimiter,

//@audit `AccessControlEnumerable`
52:   AccessControlEnumerable,

//@audit `IOUSGInstantManager`
53:   IOUSGInstantManager,

//@audit `IMulticall`
54:   IMulticall


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L50-L50) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L51-L51), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L52-L52), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L53-L53), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L54-L54)


```solidity

File: ./contracts/ousg/rOUSG.sol

//@audit `Initializable`
56:   Initializable,

//@audit `ContextUpgradeable`
57:   ContextUpgradeable,

//@audit `PausableUpgradeable`
58:   PausableUpgradeable,

//@audit `AccessControlEnumerableUpgradeable`
59:   AccessControlEnumerableUpgradeable,

//@audit `KYCRegistryClientUpgradeable`
60:   KYCRegistryClientUpgradeable,

//@audit `IERC20Upgradeable`
61:   IERC20Upgradeable,

//@audit `IERC20MetadataUpgradeable`
62:   IERC20MetadataUpgradeable


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L56-L56) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L57-L57), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L58-L58), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L59-L59), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L60-L60), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L61-L61), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L62-L62)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

//@audit `IMulticall`
37: contract ROUSGFactory is IMulticall {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L37-L37) 


</details>


### [NC&#x2011;41] [NatSpec] Natspec `@notice` is missing from `contract` 



*There are 30 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

278:   function _mint(

388:   function _redeem(

458:   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {

794:   function multiexcall(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L278-L278) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L388-L388), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L458-L458), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L794)


```solidity

File: ./contracts/ousg/rOUSG.sol

28: /**
29:  * @title Interest-bearing ERC20-like token for OUSG.
30:  *
31:  * rOUSG balances are dynamic and represent the holder's share of the underlying OUSG
32:  * controlled by the protocol. To calculate each account's balance, we do
33:  *
34:  *   shares[account] * ousgPrice
35:  *
36:  * For example, assume that we have:
37:  *
38:  *   ousgPrice = 100.505
39:  *   sharesOf(user1) -> 100
40:  *   sharesOf(user2) -> 400
41:  *
42:  * Therefore:
43:  *
44:  *   balanceOf(user1) -> 105 tokens which corresponds 105 rOUSG
45:  *   balanceOf(user2) -> 420 tokens which corresponds 420 rOUSG
46:  *
47:  * Since balances of all token holders change when the price of OUSG changes, this
48:  * token cannot fully implement ERC20 standard: it only emits `Transfer` events
49:  * upon explicit transfer between holders. In contrast, when total amount of pooled
50:  * Cash increases, no `Transfer` events are generated: doing so would require emitting
51:  * an event for each token holder and thus running an unbounded loop.
52:  *
53:  */

90:   error UnwrapTooSmall();

97:   /// @custom:oz-upgrades-unsafe-allow constructor

102:   function initialize(

112:   function __rOUSG_init(

128:   function __rOUSG_init_unchained(

163:   /**
164:    * @return the name of the token.
165:    */

170:   /**
171:    * @return the symbol of the token, usually a shorter version of the
172:    * name.
173:    */

178:   /**
179:    * @return the number of decimals for getting user representation of a token amount.
180:    */

185:   /**
186:    * @return the amount of tokens in existence.
187:    */

193:   /**
194:    * @return the amount of tokens owned by the `_account`.
195:    *
196:    * @dev Balances are dynamic and equal the `_account`'s OUSG shares multiplied
197:    *      by the price of OUSG
198:    */

225:   /**
226:    * @return the remaining number of tokens that `_spender` is allowed to spend
227:    * on behalf of `_owner` through `transferFrom`. This is zero by default.
228:    *
229:    * @dev This value changes when `approve` or `transferFrom` is called.
230:    */

341:   /**
342:    * @return the total amount of shares in existence.
343:    *
344:    * @dev The sum of all accounts' shares can be an arbitrary number, therefore
345:    * it is necessary to store it in order to calculate each account's relative share.
346:    */

351:   /**
352:    * @return the amount of shares owned by `_account`.
353:    *
354:    * @dev This is the equivalent to the amount of OUSG wrapped by `_account`.
355:    */

360:   /**
361:    * @return the amount of shares that corresponds to `_rOUSGAmount` of rOUSG
362:    */

370:   /**
371:    * @return the amount of rOUSG that corresponds to `_shares` of OUSG.
372:    */

378:   function getOUSGPrice() public view returns (uint256 price) {

484:   /**
485:    * @return the amount of shares owned by `_account`.
486:    */

572:   /**
573:    * @dev Hook that is called before any transfer of tokens. This includes
574:    * minting and burning.
575:    *
576:    * Calling conditions:
577:    *
578:    * - when `from` and `to` are both non-zero, `amount` of ``from``'s tokens
579:    * will be transferred to `to`.
580:    * - when `from` is zero, `amount` tokens will be minted for `to`.
581:    * - when `to` is zero, `amount` of ``from``'s tokens will be burned.
582:    * - `from` and `to` are never both zero.
583:    *
584:    * To learn more about hooks, head to xref:ROOT:extending-contracts.adoc#using-hooks[Using Hooks].
585:    */

642:   function pause() external onlyRole(PAUSER_ROLE) {

646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L28-L53) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L90-L90), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L97-L97), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L102-L102), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L163-L165), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L170-L173), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L178-L180), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L185-L187), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L193-L198), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L225-L230), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L341-L346), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L351-L355), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L360-L362), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L370-L372), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L378-L378), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L484-L486), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L572-L585), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L642-L642), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L646-L646), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L656)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

47:   constructor(address _guardian) {

134:   /**
135:    * @dev Event emitted when upgradable rOUSG is deployed
136:    *
137:    * @param proxy             The address for the proxy contract
138:    * @param proxyAdmin        The address for the proxy admin contract
139:    * @param implementation    The address for the implementation contract
140:    */

149:   modifier onlyGuardian() {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L47-L47) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L134-L140), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L149-L149)


</details>


### [NC&#x2011;42] Event names should use CamelCase 



*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSGFactory.sol

//@audit `rOUSGDeployed` is not in CamelCase
141:   event rOUSGDeployed(
142:     address proxy,
143:     address proxyAdmin,
144:     address implementation,
145:     string name,
146:     string ticker
147:   );


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L141-L147) 


</details>


### [NC&#x2011;43] Expressions for constant values should use `immutable` rather than `constant` 
While it does not save gas for some simple binary expressions because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between `constant` variables and `immutable` variables, and they should each be used in their appropriate contexts. `constants` should be used for literal values written into the code, and `immutable` variables should be used for expressions, or values calculated in, or passed into the constructor.


*There are 6 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

57:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");

60:   bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L57-L57) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L60-L60)


```solidity

File: ./contracts/ousg/rOUSG.sol

93:   bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");

94:   bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");

95:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L93-L93) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L94-L94), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L95-L95)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

38:   bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L38-L38) 


</details>


### [NC&#x2011;44] Top-level declarations should be separated by at least two lines 



*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

100:   }
101: 
102:   function initialize(

110:   }
111: 
112:   function __rOUSG_init(

126:   }
127: 
128:   function __rOUSG_init_unchained(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L100-L102) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L110-L112), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L126-L128)


</details>


### [NC&#x2011;45] Contract uses both `require()`/`revert()` as well as custom errors 
Consider using just one method in a single file. The below instances represents the less used technique


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

435:       revert UnwrapTooSmall();

630:       revert UnwrapTooSmall();


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L435-L435) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L630-L630)


</details>


### [NC&#x2011;46] Consider using `AccessControlDefaultAdminRules` rather than `AccessControl` 
These contracts inherits from the OpenZeppelin's AccessControl library. However, this library does not follow some security best practices, for example, the DEFAULT_ADMIN_ROLE is also its own admin, meaning it has permissions to grant and revoke this role [ref](https://docs.openzeppelin.com/contracts/3.x/access-control). \nConsider following security best practices and OpenZeppelin's recommendations, and use the AccessControlDefaultAdminRules extension to enforce additional security measures over this role.[ref](https://docs.openzeppelin.com/contracts/5.x/api/access#AccessControlDefaultAdminRules)


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

49: contract OUSGInstantManager is
50:   ReentrancyGuard,


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L49-L50) 


</details>


### [NC&#x2011;47] `immutable` variable names don\'t follow the Solidity style guide 
For `immutable` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE)


*There are 8 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

72:   IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;

75:   IRWALike public immutable ousg;

78:   ROUSG public immutable rousg;

81:   IERC20 public immutable buidl;

84:   IBUIDLRedeemer public immutable buidlRedeemer;

87:   uint256 public immutable decimalsMultiplier;

90:   address public immutable usdcReceiver;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L72-L72) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L75-L75), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L78-L78), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L81-L81), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L84-L84), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L87-L87), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L90-L90)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

40:   address internal immutable guardian;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L40-L40) 


</details>


### [NC&#x2011;48] Add inline comments for unnamed parameters 
`function func(address a, address)` -> `function func(address a, address /* b */)`


*There are 14 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit parameter number 0 starting from left need inline comment
335:   function redeem(

//@audit parameter number 0 starting from left need inline comment
362:   function redeemRebasingOUSG(

//@audit parameter number 0 starting from left need inline comment
581:   function setMinimumDepositAmount(

//@audit parameter number 0 starting from left need inline comment
599:   function setMinimumRedemptionAmount(

//@audit parameter number 0 starting from left need inline comment
650:   function setFeeReceiver(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L335-L335) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L362-L362), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L581-L581), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L599-L599), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L650)


```solidity

File: ./contracts/ousg/rOUSG.sol

//@audit parameter number 2 starting from left need inline comment
276:   function transferFrom(

//@audit parameter number 1 starting from left need inline comment
328:   function decreaseAllowance(

//@audit parameter number 0 starting from left need inline comment
415:   function wrap(uint256 _OUSGAmount) external whenNotPaused {

//@audit parameter number 0 starting from left need inline comment
431:   function unwrap(uint256 _rOUSGAmount) external whenNotPaused {

//@audit parameter number 0 starting from left need inline comment
//@audit parameter number 1 starting from left need inline comment
472:   function _approve(

//@audit parameter number 0 starting from left need inline comment
//@audit parameter number 1 starting from left need inline comment
501:   function _transferShares(

//@audit parameter number 0 starting from left need inline comment
529:   function _mintShares(

//@audit parameter number 0 starting from left need inline comment
554:   function _burnShares(

//@audit parameter number 2 starting from left need inline comment
586:   function _beforeTokenTransfer(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L276-L276) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L328-L328), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L415-L415), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L431-L431), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L472-L472), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L501-L501), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L529-L529), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L554-L554), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L586-L586)


</details>


### [NC&#x2011;49] Use the latest Solidity version for better security 
Using the latest solidity version will help avoid old compiler related vulnerabilities


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L16-L16) 


</details>


### [NC&#x2011;50] Consider adding formal verification proofs 
Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The solidity compiler itself has this functionality [built in](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification)


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

@audit Should implement invariant tests
1: 


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L1-L1) 


</details>


### [NC&#x2011;51] Missing zero address check in functions with address parameters 
Adding a zero address check for each address type parameter can prevent errors.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

//@audit _owner, _spender,  are not checked
231:   function allowance(
232:     address _owner,
233:     address _spender
234:   ) public view returns (uint256) {

//@audit _account,  are not checked
487:   function _sharesOf(address _account) internal view returns (uint256) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L231-L234) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L487-L487)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

//@audit _guardian,  are not checked
47:   constructor(address _guardian) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L47-L47) 


</details>


### [NC&#x2011;52] Use a struct to encapsulate multiple function parameters 
If a function has too many parameters, replacing them with a struct can improve code readability and maintainability, increase reusability, and reduce the likelihood of errors when passing the parameters.


*There are 4 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

144:   constructor(
145:     address defaultAdmin,
146:     address _usdc,
147:     address _usdcReciever,
148:     address _feeReceiver,
149:     address _ousgOracle,
150:     address _ousg,
151:     address _rousg,
152:     address _buidl,
153:     address _buidlRedeemer,
154:     RateLimiterConfig memory rateLimiterConfig
155:   )
156:     InstantMintTimeBasedRateLimiter(
157:       rateLimiterConfig.mintLimitDuration,
158:       rateLimiterConfig.redeemLimitDuration,
159:       rateLimiterConfig.mintLimit,
160:       rateLimiterConfig.redeemLimit
161:     )
162:   {
163:     require(
164:       address(_usdc) != address(0),
165:       "OUSGInstantManager: USDC cannot be 0x0"
166:     );
167:     require(
168:       address(_usdcReciever) != address(0),
169:       "OUSGInstantManager: USDC Receiver cannot be 0x0"
170:     );
171:     require(
172:       address(_feeReceiver) != address(0),
173:       "OUSGInstantManager: feeReceiver cannot be 0x0"
174:     );
175:     require(
176:       address(_ousgOracle) != address(0),
177:       "OUSGInstantManager: OUSG Oracle cannot be 0x0"
178:     );
179:     require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180:     require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181:     require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
182:     require(
183:       address(_buidlRedeemer) != address(0),
184:       "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
185:     );
186:     require(
187:       IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
188:       "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
189:     );
190:     require(
191:       IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
192:       "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
193:     );
194:     usdc = IERC20(_usdc);
195:     usdcReceiver = _usdcReciever;
196:     feeReceiver = _feeReceiver;
197:     oracle = IRWAOracle(_ousgOracle);
198:     ousg = IRWALike(_ousg);
199:     rousg = ROUSG(_rousg);
200:     buidl = IERC20(_buidl);
201:     buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
202:     decimalsMultiplier =
203:       10 **
204:         (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());
205:     require(
206:       OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
207:         rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
208:       "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
209:     );
210: 
211:     _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
212:     _grantRole(CONFIGURER_ROLE, defaultAdmin);
213:     _grantRole(PAUSER_ROLE, defaultAdmin);
214:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L144-L214) 


```solidity

File: ./contracts/ousg/rOUSG.sol

102:   function initialize(
103:     address _kycRegistry,
104:     uint256 requirementGroup,
105:     address _ousg,
106:     address guardian,
107:     address _oracle
108:   ) public virtual initializer {
109:     __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
110:   }

112:   function __rOUSG_init(
113:     address _kycRegistry,
114:     uint256 requirementGroup,
115:     address _ousg,
116:     address guardian,
117:     address _oracle
118:   ) internal onlyInitializing {
119:     __rOUSG_init_unchained(
120:       _kycRegistry,
121:       requirementGroup,
122:       _ousg,
123:       guardian,
124:       _oracle
125:     );
126:   }

128:   function __rOUSG_init_unchained(
129:     address _kycRegistry,
130:     uint256 _requirementGroup,
131:     address _ousg,
132:     address guardian,
133:     address _oracle
134:   ) internal onlyInitializing {
135:     __KYCRegistryClientInitializable_init(_kycRegistry, _requirementGroup);
136:     ousg = IERC20(_ousg);
137:     oracle = IRWAOracle(_oracle);
138:     _grantRole(DEFAULT_ADMIN_ROLE, guardian);
139:     _grantRole(PAUSER_ROLE, guardian);
140:     _grantRole(BURNER_ROLE, guardian);
141:     _grantRole(CONFIGURER_ROLE, guardian);
142:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L102-L110) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L112-L126), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L128-L142)


</details>


### [NC&#x2011;53] Use custom errors rather than `revert()`/`require()` strings for better readability 
Custom errors are available from solidity version 0.8.4. Custom errors are more easily processed in try-catch blocks, and are easier to re-use and maintain.


*There are 50 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

163:     require(
164:       address(_usdc) != address(0),
165:       "OUSGInstantManager: USDC cannot be 0x0"
166:     );

167:     require(
168:       address(_usdcReciever) != address(0),
169:       "OUSGInstantManager: USDC Receiver cannot be 0x0"
170:     );

171:     require(
172:       address(_feeReceiver) != address(0),
173:       "OUSGInstantManager: feeReceiver cannot be 0x0"
174:     );

175:     require(
176:       address(_ousgOracle) != address(0),
177:       "OUSGInstantManager: OUSG Oracle cannot be 0x0"
178:     );

179:     require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");

180:     require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");

181:     require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");

182:     require(
183:       address(_buidlRedeemer) != address(0),
184:       "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
185:     );

186:     require(
187:       IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
188:       "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
189:     );

190:     require(
191:       IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
192:       "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
193:     );

205:     require(
206:       OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
207:         rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
208:       "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
209:     );

282:     require(
283:       IERC20Metadata(address(usdc)).decimals() == 6,
284:       "OUSGInstantManager::_mint: USDC decimals must be 6"
285:     );

286:     require(
287:       usdcAmountIn >= minimumDepositAmount,
288:       "OUSGInstantManager::_mint: Deposit amount too small"
289:     );

298:     require(
299:       usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
300:       "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
301:     );

310:     require(
311:       ousgAmountOut > 0,
312:       "OUSGInstantManager::_mint: net mint amount can't be zero"
313:     );

344:     require(
345:       ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
346:       "OUSGInstantManager::redeem: Insufficient allowance"
347:     );

371:     require(
372:       rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
373:       "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
374:     );

391:     require(
392:       IERC20Metadata(address(usdc)).decimals() == 6,
393:       "OUSGInstantManager::_redeem: USDC decimals must be 6"
394:     );

395:     require(
396:       IERC20Metadata(address(buidl)).decimals() == 6,
397:       "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
398:     );

402:     require(
403:       usdcAmountToRedeem >= minimumRedemptionAmount,
404:       "OUSGInstantManager::_redeem: Redemption amount too small"
405:     );

417:     require(
418:       usdcAmountOut > 0,
419:       "OUSGInstantManager::_redeem: redeem amount can't be zero"
420:     );

459:     require(
460:       buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
461:       "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
462:     );

466:     require(
467:       usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
468:       "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
469:     );

481:     require(
482:       price > MINIMUM_OUSG_PRICE,
483:       "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
484:     );

557:     require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");

570:     require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");

584:     require(
585:       _minimumDepositAmount >= FEE_GRANULARITY,
586:       "setMinimumDepositAmount: Amount too small"
587:     );

602:     require(
603:       _minimumRedemptionAmount >= FEE_GRANULARITY,
604:       "setMinimumRedemptionAmount: Amount too small"
605:     );

653:     require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");

757:     require(!mintPaused, "OUSGInstantManager: Mint paused");

763:     require(!redeemPaused, "OUSGInstantManager: Redeem paused");

808:       require(success, "Call Failed");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L163-L166) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L167-L170), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L171-L174), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L175-L178), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L179-L179), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L180-L180), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L181-L181), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L182-L185), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L186-L189), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L190-L193), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L205-L209), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L282-L285), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L286-L289), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L298-L301), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L310-L313), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L344-L347), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L371-L374), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L391-L394), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L395-L398), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L402-L405), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L417-L420), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L459-L462), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L466-L469), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L481-L484), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L557-L557), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L570-L570), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L584-L587), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L602-L605), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L653-L653), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L757-L757), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L763-L763), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L808-L808)


```solidity

File: ./contracts/ousg/rOUSG.sol

282:     require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");

333:     require(
334:       currentAllowance >= _subtractedValue,
335:       "DECREASED_ALLOWANCE_BELOW_ZERO"
336:     );

416:     require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");

432:     require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");

477:     require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");

478:     require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");

506:     require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");

507:     require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");

512:     require(
513:       _sharesAmount <= currentSenderShares,
514:       "TRANSFER_AMOUNT_EXCEEDS_BALANCE"
515:     );

533:     require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");

558:     require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS");

563:     require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE");

594:       require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");

599:       require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd");

604:       require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L282-L282) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L333-L336), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L416-L416), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L432-L432), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L477-L477), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L478-L478), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L506-L506), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L507-L507), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L512-L515), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L533-L533), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L558-L558), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L563-L563), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L594-L594), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L599-L599), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L604-L604)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

76:     require(!initialized, "ROUSGFactory: rOUSG already deployed");

150:     require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");

129:       require(success, "Call Failed");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L76-L76) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L150-L150), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L129-L129)


</details>


### [NC&#x2011;54] Use `@inheritdoc` for overridden functions 



*There are 20 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

219:   /**
220:    * @notice Calculates fees and triggers minting OUSG for a given amount of USDC
221:    *
222:    * @dev Please note that the fees are accumulated in `feeReceiver`
223:    *
224:    * @param usdcAmountIn amount of USDC exchanged for OUSG (in whatever decimals
225:    *                     specifed by usdc token contract)
226:    *
227:    * @return ousgAmountOut The quantity of OUSG minted for the user
228:    *                       (18 decimals per OUSG contract)
229:    */

243:   /**
244:    * @notice Calculates fees and triggers minting rOUSG for a given amount of USDC
245:    *
246:    * @dev Please note that the fees are accumulated in `feeReceiver`
247:    *
248:    * @param usdcAmountIn amount of USDC exchanged for rOUSG (in whatever decimals
249:    *                     specifed by usdc token contract)
250:    *
251:    * @return rousgAmountOut The quantity of rOUSG minted for the user
252:    *                        (18 decimals per rOUSG contract)
253:    */

326:   /**
327:    * @notice Calculates fees and triggers a redemption of OUSG for a given amount of USDC
328:    *
329:    * @dev Please note that the fees are accumulated in `feeReceiver`
330:    *
331:    * @param ousgAmountIn Amount of OUSG to redeem
332:    *
333:    * @return usdcAmountOut The amount of USDC returned to the user
334:    */

353:   /**
354:    * @notice Calculates fees and triggers minting rOUSG for a given amount of USDC
355:    *
356:    * @dev Please note that the fees are actually accumulated in `feeReceiver`
357:    *
358:    * @param rousgAmountIn Amount of rOUSG to redeem
359:    *
360:    * @return usdcAmountOut The amount of USDC returned to the user
361:    */

490:   /**
491:    * @notice Set the mintLimit constraint inside the InstantMintTimeBasedRateLimiter
492:    *         base contract
493:    *
494:    * @param _instantMintLimit New limit that dicates how much USDC can be transfered
495:    *                     for minting in a specified duration
496:    *                     (in 6 decimals per the USDC contract)
497:    */

504:   /**
505:    * @notice Set the redeemLimit constraint inside the InstantMintTimeBasedRateLimiter
506:    *         base contract
507:    *
508:    * @param _instantRedemptionLimit New limit that dicates how much USDC
509:    *                       can be redeemed in a specified duration
510:    *                       (in 6 decimals per the USDC contract)
511:    */

518:   /**
519:    * @notice Sets mintLimitDuration constraint inside the InstantMintTimeBasedRateLimiter
520:    *         base contract
521:    *
522:    * @param _instantMintLimitDuration New limit that specifies the interval
523:    *                             (in seconds) in which only `mintLimit` USDC
524:    *                             can be used for minting within
525:    */

532:   /**
533:    * @notice Sets redeemLimitDuration inside the InstantMintTimeBasedRateLimiter
534:    *         base contract
535:    *
536:    * @param _instantRedemptionLimitDuratioin New limit that specifies the interval
537:    *                               (in seconds) in which only `redeemLimit` USDC
538:    *                               can be redeemed within
539:    */

549:   /**
550:    * @notice Sets the mint fee
551:    *
552:    * @param _mintFee new mint fee specified in basis points
553:    */

562:   /**
563:    * @notice Sets the redeem fee.
564:    *
565:    * @param _redeemFee new redeem fee specified in basis points
566:    */

575:   /**
576:    * @notice Admin function to set the minimum amount required for a deposit
577:    *
578:    * @param _minimumDepositAmount The minimum amount required to submit a deposit
579:    *                          request
580:    */

593:   /**
594:    * @notice Admin function to set the minimum amount to redeem
595:    *
596:    * @param _minimumRedemptionAmount The minimum amount required to submit a
597:    *                                 redemption request
598:    */

617:   /**
618:    * @notice Admin function to set the minimum amount required to redeem BUIDL
619:    *
620:    * @param _minimumBUIDLRedemptionAmount The minimum amount required to redeem BUIDL
621:    */

632:   /**
633:    * @notice Admin function to set the oracle address
634:    *
635:    * @param _oracle The address of the oracle that provides the OUSG price
636:    *                in USDC
637:    */

645:   /**
646:    * @notice Admin function to set the fee receiver address
647: 
648:    * @param _feeReceiver The address to receive the mint and redemption fees
649:    */

658:   /**
659:    * @notice Admin function to set the optional investor-based rate limiter
660:    *
661:    * @param _investorBasedRateLimiter The address of the investor-based rate limiter contract
662:    */

794:   function multiexcall(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L219-L229) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L243-L253), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L326-L334), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L353-L361), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L490-L497), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L504-L511), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L518-L525), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L532-L539), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L549-L553), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L562-L566), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L575-L580), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L593-L598), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L617-L621), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L632-L637), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L645-L649), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L658-L662), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L794)


```solidity

File: ./contracts/ousg/rOUSG.sol

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L650) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L656)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

110:   /**
111:    * @notice Allows for arbitrary batched calls
112:    *
113:    * @dev All external calls made through this function will
114:    *      msg.sender == contract address
115:    *
116:    * @param exCallData Struct consisting of
117:    *       1) target - contract to call
118:    *       2) data - data to call target with
119:    *       3) value - eth value to call target with
120:    */


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L110-L120) 


</details>


### [NC&#x2011;55] Multiple mappings with same keys can be combined into a single struct mapping for readability 
Well-organized data structures make code reviews easier, which may lead to fewer bugs. Consider combining related mappings into mappings to structs, so it's clear what data is related.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

72:   mapping(address => uint256) private shares;

75:   mapping(address => mapping(address => uint256)) private allowances;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L72-L72) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L75-L75)


</details>


### [NC&#x2011;56] constructor should emit an event 
Use events to signal significant changes to off-chain monitoring tools.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

144:   constructor(
145:     address defaultAdmin,
146:     address _usdc,
147:     address _usdcReciever,
148:     address _feeReceiver,
149:     address _ousgOracle,
150:     address _ousg,
151:     address _rousg,
152:     address _buidl,
153:     address _buidlRedeemer,
154:     RateLimiterConfig memory rateLimiterConfig
155:   )
156:     InstantMintTimeBasedRateLimiter(
157:       rateLimiterConfig.mintLimitDuration,
158:       rateLimiterConfig.redeemLimitDuration,
159:       rateLimiterConfig.mintLimit,
160:       rateLimiterConfig.redeemLimit
161:     )
162:   {
163:     require(
164:       address(_usdc) != address(0),
165:       "OUSGInstantManager: USDC cannot be 0x0"
166:     );
167:     require(
168:       address(_usdcReciever) != address(0),
169:       "OUSGInstantManager: USDC Receiver cannot be 0x0"
170:     );
171:     require(
172:       address(_feeReceiver) != address(0),
173:       "OUSGInstantManager: feeReceiver cannot be 0x0"
174:     );
175:     require(
176:       address(_ousgOracle) != address(0),
177:       "OUSGInstantManager: OUSG Oracle cannot be 0x0"
178:     );
179:     require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180:     require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181:     require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
182:     require(
183:       address(_buidlRedeemer) != address(0),
184:       "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
185:     );
186:     require(
187:       IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
188:       "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
189:     );
190:     require(
191:       IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
192:       "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
193:     );
194:     usdc = IERC20(_usdc);
195:     usdcReceiver = _usdcReciever;
196:     feeReceiver = _feeReceiver;
197:     oracle = IRWAOracle(_ousgOracle);
198:     ousg = IRWALike(_ousg);
199:     rousg = ROUSG(_rousg);
200:     buidl = IERC20(_buidl);
201:     buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
202:     decimalsMultiplier =
203:       10 **
204:         (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());
205:     require(
206:       OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
207:         rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
208:       "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
209:     );
210: 
211:     _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
212:     _grantRole(CONFIGURER_ROLE, defaultAdmin);
213:     _grantRole(PAUSER_ROLE, defaultAdmin);
214:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L144-L214) 


```solidity

File: ./contracts/ousg/rOUSG.sol

098:   constructor() {
099:     _disableInitializers();
100:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L98-L100) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

47:   constructor(address _guardian) {
48:     guardian = _guardian;
49:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L47-L49) 


</details>


### [NC&#x2011;57] Complex functions should include comments 
Large and/or complex functions should include comments to make them easier to understand and reduce margin for error.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

254:   function mintRebasingOUSG(

362:   function redeemRebasingOUSG(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L254-L254) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L362-L362)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

70:   function deployRebasingOUSG(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L70-L70) 


</details>


### [NC&#x2011;58] [Solidity]: All `verbatim` blocks are considered identical by deduplicator and can incorrectly be unified 
The block deduplicator is a step of the opcode-based optimizer which identifies equivalent assembly blocks and merges them into a single one. However, when blocks contained `verbatim`, their comparison was performed incorrectly, leading to the collapse of assembly blocks which are identical except for the contents of the ``verbatim`` items. Since `verbatim` is only available in Yul, compilation of Solidity sources is not affected. For more details check the following [link](https://blog.soliditylang.org/2023/11/08/verbatim-invalid-deduplication-bug/)


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L16-L16) 


</details>


### [NC&#x2011;59] [NatSpec] Natspec `@param` is missing from `error` 



*There are 31 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

278:   function _mint(

388:   function _redeem(

458:   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {

731:   /**
732:    * @notice Scale provided amount up by `decimalsMultiplier`
733:    *
734:    * @dev This helper is used for converting a USDC amount's decimals
735:    *      representation to the rOUSG/OUSG decimals representation.
736:    */

741:   /**
742:    * @notice Scale provided amount down by `decimalsMultiplier`
743:    *
744:    * @dev This helper is used for converting an rOUSG/OUSG amount's decimals
745:    *      representation to the USDC decimals representation.
746:    */

794:   function multiexcall(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L278-L278) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L388-L388), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L458-L458), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L731-L736), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L741-L746), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L794-L794)


```solidity

File: ./contracts/ousg/rOUSG.sol

102:   function initialize(

112:   function __rOUSG_init(

128:   function __rOUSG_init_unchained(

144:   /**
145:    * @notice An executed shares transfer from `sender` to `recipient`.
146:    *
147:    * @dev emitted in pair with an ERC20-defined `Transfer` event.
148:    */

193:   /**
194:    * @return the amount of tokens owned by the `_account`.
195:    *
196:    * @dev Balances are dynamic and equal the `_account`'s OUSG shares multiplied
197:    *      by the price of OUSG
198:    */

205:   /**
206:    * @notice Moves `_amount` tokens from the caller's account to the `_recipient` account.
207:    *
208:    * @return a boolean value indicating whether the operation succeeded.
209:    * Emits a `Transfer` event.
210:    * Emits a `TransferShares` event.
211:    *
212:    * Requirements:
213:    *
214:    * - `_recipient` cannot be the zero address.
215:    * - the caller must have a balance of at least `_amount`.
216:    * - the contract must not be paused.
217:    *
218:    * @dev The `_amount` argument is the amount of tokens, not shares.
219:    */

225:   /**
226:    * @return the remaining number of tokens that `_spender` is allowed to spend
227:    * on behalf of `_owner` through `transferFrom`. This is zero by default.
228:    *
229:    * @dev This value changes when `approve` or `transferFrom` is called.
230:    */

238:   /**
239:    * @notice Sets `_amount` as the allowance of `_spender` over the caller's tokens.
240:    *
241:    * @return a boolean value indicating whether the operation succeeded.
242:    * Emits an `Approval` event.
243:    *
244:    * Requirements:
245:    *
246:    * - `_spender` cannot be the zero address.
247:    * - the contract must not be paused.
248:    *
249:    * @dev The `_amount` argument is the amount of tokens, not shares.
250:    */

256:   /**
257:    * @notice Moves `_amount` tokens from `_sender` to `_recipient` using the
258:    * allowance mechanism. `_amount` is then deducted from the caller's
259:    * allowance.
260:    *
261:    * @return a boolean value indicating whether the operation succeeded.
262:    *
263:    * Emits a `Transfer` event.
264:    * Emits a `TransferShares` event.
265:    * Emits an `Approval` event indicating the updated allowance.
266:    *
267:    * Requirements:
268:    *
269:    * - `_sender` and `_recipient` cannot be the zero addresses.
270:    * - `_sender` must have a balance of at least `_amount`.
271:    * - the caller must have allowance for `_sender`'s tokens of at least `_amount`.
272:    * - the contract must not be paused.
273:    *
274:    * @dev The `_amount` argument is the amount of tokens, not shares.
275:    */

289:   /**
290:    * @notice Atomically increases the allowance granted to `_spender` by the caller by `_addedValue`.
291:    *
292:    * This is an alternative to `approve` that can be used as a mitigation for
293:    * problems described in:
294:    * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42
295:    * Emits an `Approval` event indicating the updated allowance.
296:    *
297:    * Requirements:
298:    *
299:    * - `_spender` cannot be the the zero address.
300:    * - the contract must not be paused.
301:    */

314:   /**
315:    * @notice Atomically decreases the allowance granted to `_spender` by the caller by `_subtractedValue`.
316:    *
317:    * This is an alternative to `approve` that can be used as a mitigation for
318:    * problems described in:
319:    * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42
320:    * Emits an `Approval` event indicating the updated allowance.
321:    *
322:    * Requirements:
323:    *
324:    * - `_spender` cannot be the zero address.
325:    * - `_spender` must have allowance for the caller of at least `_subtractedValue`.
326:    * - the contract must not be paused.
327:    */

351:   /**
352:    * @return the amount of shares owned by `_account`.
353:    *
354:    * @dev This is the equivalent to the amount of OUSG wrapped by `_account`.
355:    */

360:   /**
361:    * @return the amount of shares that corresponds to `_rOUSGAmount` of rOUSG
362:    */

370:   /**
371:    * @return the amount of rOUSG that corresponds to `_shares` of OUSG.
372:    */

382:   /**
383:    * @notice Moves `_sharesAmount` token shares from the caller's account to the `_recipient` account.
384:    *
385:    * @return amount of transferred tokens.
386:    * Emits a `TransferShares` event.
387:    * Emits a `Transfer` event.
388:    *
389:    * Requirements:
390:    *
391:    * - `_recipient` cannot be the zero address.
392:    * - the caller must have at least `_sharesAmount` shares.
393:    * - the contract must not be paused.
394:    *
395:    * @dev The `_sharesAmount` argument is the amount of shares, not tokens.
396:    */

445:   /**
446:    * @notice Moves `_amount` tokens from `_sender` to `_recipient`.
447:    * Emits a `Transfer` event.
448:    * Emits a `TransferShares` event.
449:    */

461:   /**
462:    * @notice Sets `_amount` as the allowance of `_spender` over the `_owner` s tokens.
463:    *
464:    * Emits an `Approval` event.
465:    *
466:    * Requirements:
467:    *
468:    * - `_owner` cannot be the zero address.
469:    * - `_spender` cannot be the zero address.
470:    * - the contract must not be paused.
471:    */

484:   /**
485:    * @return the amount of shares owned by `_account`.
486:    */

491:   /**
492:    * @notice Moves `_sharesAmount` shares from `_sender` to `_recipient`.
493:    *
494:    * Requirements:
495:    *
496:    * - `_sender` cannot be the zero address.
497:    * - `_recipient` cannot be the zero address.
498:    * - `_sender` must hold at least `_sharesAmount` shares.
499:    * - the contract must not be paused.
500:    */

521:   /**
522:    * @notice Creates `_sharesAmount` shares and assigns them to `_recipient`, increasing the total amount of shares.
523:    *
524:    * Requirements:
525:    *
526:    * - `_recipient` cannot be the zero address.
527:    * - the contract must not be paused.
528:    */

544:   /**
545:    * @notice Destroys `_sharesAmount` shares from `_account`'s holdings, decreasing the total amount of shares.
546:    * @dev This doesn't decrease the token total supply.
547:    *
548:    * Requirements:
549:    *
550:    * - `_account` cannot be the zero address.
551:    * - `_account` must hold at least `_sharesAmount` shares.
552:    * - the contract must not be paused.
553:    */

572:   /**
573:    * @dev Hook that is called before any transfer of tokens. This includes
574:    * minting and burning.
575:    *
576:    * Calling conditions:
577:    *
578:    * - when `from` and `to` are both non-zero, `amount` of ``from``'s tokens
579:    * will be transferred to `to`.
580:    * - when `from` is zero, `amount` tokens will be minted for `to`.
581:    * - when `to` is zero, `amount` of ``from``'s tokens will be burned.
582:    * - `from` and `to` are never both zero.
583:    *
584:    * To learn more about hooks, head to xref:ROOT:extending-contracts.adoc#using-hooks[Using Hooks].
585:    */

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L102-L102) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L112-L112), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L128-L128), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L144-L148), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L193-L198), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L205-L219), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L225-L230), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L238-L250), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L256-L275), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L289-L301), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L314-L327), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L351-L355), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L360-L362), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L370-L372), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L382-L396), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L445-L449), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L461-L471), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L484-L486), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L491-L500), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L521-L528), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L544-L553), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L572-L585), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L650), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L656-L656)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

47:   constructor(address _guardian) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L47-L47) 


</details>


### [NC&#x2011;60] OpenZeppelin libraries should be upgraded to a newer version 
These contracts import some OpenZeppelin libraries, but they are using an old version.


*There are 11 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

18: import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";

19: import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";

20: import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L19-L19), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L20-L20)


```solidity

File: ./contracts/ousg/rOUSG.sol

18: import "contracts/external/openzeppelin/contracts/token/IERC20.sol";

19: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";

20: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";

21: import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";

22: import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";

23: import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";

24: import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L18-L18) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L19-L19), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L20-L20), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L21-L21), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L22-L22), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L23-L23), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L24-L24)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

19: import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L19-L19) 


</details>


### [NC&#x2011;61] Not using the latest version of `prb-math` from dependencies 
`prb-math` is an important mathematical library The package.json configuration file says that the project is using an old version of `prb-math`.


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: package.json

//@audit `prb-math` version is 
1: 


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//package.json#L1-L1) 


</details>


### [NC&#x2011;62] Enforcing Lowercase and Underscores Only in the `name` Field of package.json 
package.json name variable should only consist of lowercase letters and underscores


*There are 1 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: package.json

//@audit package.json name is ondo-cash-flux
1: {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//package.json#L1-L1) 


</details>


### [NC&#x2011;63] Consider making private state variables internal to increase flexibility 
In Solidity, `private` state variables are strictly confined to the contract they are defined in and can't be accessed or modified by its derived contracts. While this offers strong encapsulation, it can limit contract extensibility and modification in inheritance chains. On the other hand, `internal` variables can be accessed and potentially overridden by child contracts, granting more flexibility in contract development and upgrades. Therefore, it's recommended to use `private` only when you explicitly want to prevent child contract access. Otherwise, prefer `internal` to maintain a balance between encapsulation and the flexibility offered by inheritance patterns in Solidity.


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/rOUSG.sol

72:   mapping(address => uint256) private shares;

75:   mapping(address => mapping(address => uint256)) private allowances;

78:   uint256 private totalShares;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L72-L72) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L75-L75), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L78-L78)


</details>


### [NC&#x2011;64] Using Low-Level Call for Transfers 
Utilizing low-level calls like `.call{value: value}` for Ether transfers in Ethereum can be risky, as it can inadvertently allow malicious contract executions through fallback functions. To mitigate these risks and ensure safer Ether transfers, it is recommended to adopt more secure and explicit methods provided by reputable libraries such as OpenZeppelin. Functions like `Address.sendValue()` from OpenZeppelin provide a clearer and safer alternative for sending Ether, as they encapsulate necessary checks and error handling, ensuring that Ether is transferred securely and any errors are appropriately dealt with. This not only enhances the security of your smart contract but also improves code readability and maintainability, aligning with modern Solidity development practices.


*There are 2 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
806:         value: exCallData[i].value
807:       }(exCallData[i].data);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L805-L807) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
127:         value: exCallData[i].value
128:       }(exCallData[i].data);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L126-L128) 


</details>


### [NC&#x2011;65] A event should be emitted if a non immutable state variable is set in a constructor 



*There are 10 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

194:     usdc = IERC20(_usdc);

195:     usdcReceiver = _usdcReciever;

196:     feeReceiver = _feeReceiver;

197:     oracle = IRWAOracle(_ousgOracle);

198:     ousg = IRWALike(_ousg);

199:     rousg = ROUSG(_rousg);

200:     buidl = IERC20(_buidl);

201:     buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);

202:     decimalsMultiplier =
203:       10 **
204:         (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L194-L194) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L195-L195), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L196-L196), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L197-L197), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L198-L198), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L199-L199), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L200-L200), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L201-L201), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L202-L204)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

48:     guardian = _guardian;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L48-L48) 


</details>


### [NC&#x2011;66] [Solidity]: Order of Argument Evaluation Disrupted in Non-Expression-Split Code by Optimizer Sequences with FullInliner 
Function call arguments in Yul are evaluated right to left. This order matters when the argument expressions have side-effects, and changing it may change contract behavior. FullInliner is an optimizer step that can replace a function call with the body of that function. The transformation involves assigning argument expressions to temporary variables, which imposes an explicit evaluation order. FullInliner was written with the assumption that this order does not necessarily have to match usual argument evaluation order because the argument expressions have no side-effects. In most circumstances this assumption is true because the default optimization step sequence contains the ExpressionSplitter step. ExpressionSplitter ensures that the code is in *expression-split form*, which means that function calls cannot appear nested inside expressions, and all function call arguments have to be variables. The assumption is, however, not guaranteed to be true in general. Version 0.6.7 introduced a setting allowing users to specify an arbitrary optimization step sequence, making it possible for the FullInliner to actually encounter argument expressions with side-effects, which can result in behavior differences between optimized and unoptimized bytecode. Contracts compiled without optimization or with the default optimization sequence are not affected. To trigger the bug the user has to explicitly choose compiler settings that contain a sequence with FullInliner step not preceded by ExpressionSplitter. [Ref](https://blog.soliditylang.org/2023/07/19/full-inliner-non-expression-split-argument-evaluation-order-bug/)


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSG.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L16-L16) 


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

16: pragma solidity 0.8.16;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L16-L16) 


</details>


### [NC&#x2011;67] Use named return values 
Using named returns makes the code more self-documenting, makes it easier to fill out NatSpec, and in some cases can save gas. The cases below are where there currently is at most one return statement, which is ideal for named returns.


*There are 24 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

713:   function _getInstantMintFees(
714:     uint256 usdcAmount
715:   ) internal view returns (uint256) {

725:   function _getInstantRedemptionFees(
726:     uint256 usdcAmount
727:   ) internal view returns (uint256) {

737:   function _scaleUp(uint256 amount) internal view returns (uint256) {

747:   function _scaleDown(uint256 amount) internal view returns (uint256) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L713-L715) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L725-L727), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L737-L737), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L747-L747)


```solidity

File: ./contracts/ousg/rOUSG.sol

166:   function name() public pure returns (string memory) {

174:   function symbol() public pure returns (string memory) {

181:   function decimals() public pure returns (uint8) {

188:   function totalSupply() public view returns (uint256) {

199:   function balanceOf(address _account) public view returns (uint256) {

220:   function transfer(address _recipient, uint256 _amount) public returns (bool) {

231:   function allowance(
232:     address _owner,
233:     address _spender
234:   ) public view returns (uint256) {

251:   function approve(address _spender, uint256 _amount) public returns (bool) {

276:   function transferFrom(
277:     address _sender,
278:     address _recipient,
279:     uint256 _amount
280:   ) public returns (bool) {

302:   function increaseAllowance(
303:     address _spender,
304:     uint256 _addedValue
305:   ) public returns (bool) {

328:   function decreaseAllowance(
329:     address _spender,
330:     uint256 _subtractedValue
331:   ) public returns (bool) {

347:   function getTotalShares() public view returns (uint256) {

356:   function sharesOf(address _account) public view returns (uint256) {

363:   function getSharesByROUSG(
364:     uint256 _rOUSGAmount
365:   ) public view returns (uint256) {

373:   function getROUSGByShares(uint256 _shares) public view returns (uint256) {

397:   function transferShares(
398:     address _recipient,
399:     uint256 _sharesAmount
400:   ) public returns (uint256) {

487:   function _sharesOf(address _account) internal view returns (uint256) {

529:   function _mintShares(
530:     address _recipient,
531:     uint256 _sharesAmount
532:   ) internal whenNotPaused returns (uint256) {

554:   function _burnShares(
555:     address _account,
556:     uint256 _sharesAmount
557:   ) internal whenNotPaused returns (uint256) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L166-L166) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L174-L174), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L181-L181), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L188-L188), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L199-L199), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L220-L220), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L231-L234), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L251-L251), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L276-L280), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L302-L305), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L328-L331), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L347-L347), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L356-L356), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L363-L365), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L373-L373), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L397-L400), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L487-L487), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L529-L532), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L554-L557)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

70:   function deployRebasingOUSG(
71:     address kycRegistry,
72:     uint256 requirementGroup,
73:     address ousg,
74:     address oracle
75:   ) external onlyGuardian returns (address, address, address) {


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L70-L75) 


</details>


### [NC&#x2011;68] Consider moving duplicated strings to constants 



*There are 24 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

57:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");

60:   bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");

808:       require(success, "Call Failed");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L57-L57) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L60-L60), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L808-L808)


```solidity

File: ./contracts/ousg/rOUSG.sol

95:   bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");

93:   bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");

94:   bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");

167:     return "Rebasing OUSG";

175:     return "rOUSG";

282:     require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");

335:       "DECREASED_ALLOWANCE_BELOW_ZERO"

416:     require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");

432:     require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");

477:     require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");

478:     require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");

506:     require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");

507:     require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");

514:       "TRANSFER_AMOUNT_EXCEEDS_BALANCE"

533:     require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");

558:     require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS");

563:     require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE");

594:       require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");

599:       require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd");

604:       require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L95-L95) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L93-L93), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L94-L94), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L167-L167), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L175-L175), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L282-L282), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L335-L335), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L416-L416), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L432-L432), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L477-L477), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L478-L478), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L506-L506), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L507-L507), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L514-L514), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L533-L533), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L558-L558), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L563-L563), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L594-L594), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L599-L599), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L604-L604)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

129:       require(success, "Call Failed");


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L129-L129) 


</details>


### [NC&#x2011;69] Missing checks for uint state variable assignments 
Consider whether reasonable bounds checks for variables would be useful


*There are 5 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

559:     mintFee = _mintFee;

572:     redeemFee = _redeemFee;

590:     minimumDepositAmount = _minimumDepositAmount;

610:     minimumRedemptionAmount = _minimumRedemptionAmount;

629:     minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L559-L559) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L572-L572), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L590-L590), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L610-L610), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L629-L629)


</details>


### [NC&#x2011;70] Consider adding validation of user inputs 



*There are 25 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

//@audit these parameters `to`, are not checked
278:   function _mint(
279:     uint256 usdcAmountIn,
280:     address to

//@audit these parameters `_oracle`, are not checked
638:   function setOracle(
639:     address _oracle

//@audit these parameters ``, are not checked
650:   function setFeeReceiver(
651:     address _feeReceiver

//@audit these parameters `_investorBasedRateLimiter`, are not checked
663:   function setInvestorBasedRateLimiter(
664:     address _investorBasedRateLimiter

//@audit these parameters `token`,`to`, are not checked
819:   function retrieveTokens(
820:     address token,
821:     address to,
822:     uint256 amount


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L278-L280) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L638-L639), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L650-L651), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L663-L664), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L819-L822)


```solidity

File: ./contracts/ousg/rOUSG.sol

//@audit these parameters `_kycRegistry`,`_ousg`,`guardian`,`_oracle`, are not checked
102:   function initialize(
103:     address _kycRegistry,
104:     uint256 requirementGroup,
105:     address _ousg,
106:     address guardian,
107:     address _oracle

//@audit these parameters `_kycRegistry`,`_ousg`,`guardian`,`_oracle`, are not checked
112:   function __rOUSG_init(
113:     address _kycRegistry,
114:     uint256 requirementGroup,
115:     address _ousg,
116:     address guardian,
117:     address _oracle

//@audit these parameters `_kycRegistry`,`_ousg`,`guardian`,`_oracle`, are not checked
128:   function __rOUSG_init_unchained(
129:     address _kycRegistry,
130:     uint256 _requirementGroup,
131:     address _ousg,
132:     address guardian,
133:     address _oracle

//@audit these parameters `_recipient`, are not checked
220:   function transfer(address _recipient, uint256 _amount) public returns (bool) {

//@audit these parameters `_owner`,`_spender`, are not checked
231:   function allowance(
232:     address _owner,
233:     address _spender

//@audit these parameters `_spender`, are not checked
251:   function approve(address _spender, uint256 _amount) public returns (bool) {

//@audit these parameters `_sender`,`_recipient`, are not checked
276:   function transferFrom(
277:     address _sender,
278:     address _recipient,
279:     uint256 _amount

//@audit these parameters `_spender`, are not checked
328:   function decreaseAllowance(
329:     address _spender,
330:     uint256 _subtractedValue

//@audit these parameters `_account`, are not checked
356:   function sharesOf(address _account) public view returns (uint256) {

//@audit these parameters `_recipient`, are not checked
397:   function transferShares(
398:     address _recipient,
399:     uint256 _sharesAmount

//@audit these parameters `_sender`,`_recipient`, are not checked
450:   function _transfer(
451:     address _sender,
452:     address _recipient,
453:     uint256 _amount

//@audit these parameters ``,``, are not checked
472:   function _approve(
473:     address _owner,
474:     address _spender,
475:     uint256 _amount

//@audit these parameters `_account`, are not checked
487:   function _sharesOf(address _account) internal view returns (uint256) {

//@audit these parameters ``,``, are not checked
501:   function _transferShares(
502:     address _sender,
503:     address _recipient,
504:     uint256 _sharesAmount

//@audit these parameters ``, are not checked
529:   function _mintShares(
530:     address _recipient,
531:     uint256 _sharesAmount

//@audit these parameters ``, are not checked
554:   function _burnShares(
555:     address _account,
556:     uint256 _sharesAmount

//@audit these parameters `_oracle`, are not checked
613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {

//@audit these parameters `_account`, are not checked
624:   function burn(
625:     address _account,
626:     uint256 _amount

//@audit these parameters `registry`, are not checked
650:   function setKYCRegistry(
651:     address registry


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L102-L107) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L112-L117), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L128-L133), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L220-L220), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L231-L233), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L251-L251), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L276-L279), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L328-L330), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L356-L356), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L397-L399), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L450-L453), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L472-L475), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L487-L487), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L501-L504), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L529-L531), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L554-L556), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L613-L613), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L624-L626), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L650-L651)


```solidity

File: ./contracts/ousg/rOUSGFactory.sol

//@audit these parameters `kycRegistry`,`ousg`,`oracle`, are not checked
70:   function deployRebasingOUSG(
71:     address kycRegistry,
72:     uint256 requirementGroup,
73:     address ousg,
74:     address oracle


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSGFactory.sol#L70-L74) 


</details>


### [NC&#x2011;71] Consider disallowing transfers to `address(this)` 
Consider preventing a contract's tokens from being transferred/minted to the contract itself


*There are 3 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

230:   function mint(
231:     uint256 usdcAmountIn
232:   )
233:     external
234:     override
235:     nonReentrant
236:     whenMintNotPaused
237:     returns (uint256 ousgAmountOut)
238:   {
239:     ousgAmountOut = _mint(usdcAmountIn, msg.sender);
240:     emit InstantMintOUSG(msg.sender, usdcAmountIn, ousgAmountOut);
241:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L230-L241) 


```solidity

File: ./contracts/ousg/rOUSG.sol

220:   function transfer(address _recipient, uint256 _amount) public returns (bool) {
221:     _transfer(msg.sender, _recipient, _amount);
222:     return true;
223:   }

276:   function transferFrom(
277:     address _sender,
278:     address _recipient,
279:     uint256 _amount
280:   ) public returns (bool) {
281:     uint256 currentAllowance = allowances[_sender][msg.sender];
282:     require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");
283: 
284:     _transfer(_sender, _recipient, _amount);
285:     _approve(_sender, msg.sender, currentAllowance - _amount);
286:     return true;
287:   }


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L220-L223) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L276-L287)


</details>


### [NC&#x2011;72] Consider using named function calls 
Named function calls in Solidity greatly improve code readability by explicitly mapping arguments to their respective parameter names. This clarity becomes critical when dealing with functions that have numerous or complex parameters, reducing potential errors due to misordered arguments. Therefore, adopting named function calls contributes to more maintainable and less error-prone code.


*There are 28 instances of this issue:*



<details>
<summary>see instances</summary>


```solidity
File: ./contracts/ousg/ousgInstantManager.sol

211:     _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);

212:     _grantRole(CONFIGURER_ROLE, defaultAdmin);

213:     _grantRole(PAUSER_ROLE, defaultAdmin);

263:     uint256 ousgAmountOut = _mint(usdcAmountIn, address(this));

400:     uint256 usdcAmountToRedeem = _getRedemptionAmount(ousgAmountIn, ousgPrice);

239:     ousgAmountOut = _mint(usdcAmountIn, msg.sender);

308:     ousgAmountOut = _getMintAmount(usdcAmountAfterFee, ousgPrice);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L211-L211) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L212-L212), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L213-L213), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L263-L263), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L400-L400), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L239-L239), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/ousgInstantManager.sol#L308-L308)


```solidity

File: ./contracts/ousg/rOUSG.sol

109:     __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);

119:     __rOUSG_init_unchained(
120:       _kycRegistry,
121:       requirementGroup,
122:       _ousg,
123:       guardian,
124:       _oracle
125:     );

135:     __KYCRegistryClientInitializable_init(_kycRegistry, _requirementGroup);

138:     _grantRole(DEFAULT_ADMIN_ROLE, guardian);

139:     _grantRole(PAUSER_ROLE, guardian);

140:     _grantRole(BURNER_ROLE, guardian);

141:     _grantRole(CONFIGURER_ROLE, guardian);

221:     _transfer(msg.sender, _recipient, _amount);

252:     _approve(msg.sender, _spender, _amount);

284:     _transfer(_sender, _recipient, _amount);

285:     _approve(_sender, msg.sender, currentAllowance - _amount);

306:     _approve(
307:       msg.sender,
308:       _spender,
309:       allowances[msg.sender][_spender] + _addedValue
310:     );

337:     _approve(msg.sender, _spender, currentAllowance - _subtractedValue);

401:     _transferShares(msg.sender, _recipient, _sharesAmount);

418:     _mintShares(msg.sender, ousgSharesAmount);

436:     _burnShares(msg.sender, ousgSharesAmount);

456:     _transferShares(_sender, _recipient, _sharesToTransfer);

509:     _beforeTokenTransfer(_sender, _recipient, _sharesAmount);

535:     _beforeTokenTransfer(address(0), _recipient, _sharesAmount);

560:     _beforeTokenTransfer(_account, address(0), _sharesAmount);

632:     _burnShares(_account, ousgSharesAmount);


```

[link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L109-L109) , [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L119-L125), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L135-L135), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L138-L138), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L139-L139), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L140-L140), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L141-L141), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L221-L221), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L252-L252), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L284-L284), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L285-L285), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L306-L310), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L337-L337), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L401-L401), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L418-L418), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L436-L436), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L456-L456), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L509-L509), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L535-L535), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L560-L560), [link](https://github.com/code-423n4/2024-03-ondo-finance/blob/main//./contracts/ousg/rOUSG.sol#L632-L632)


</details>
