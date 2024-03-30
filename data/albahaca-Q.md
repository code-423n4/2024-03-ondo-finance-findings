## L001 - Initializers could be front-run:

Initializers could be front-run, allowing an attacker to either set their own values, take ownership of the contract, and in the best case forcing a re-deployment


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


102       function initialize(
103         address _kycRegistry,
104         uint256 requirementGroup,
105         address _ousg,
106         address guardian,
107         address _oracle
108       ) public virtual initializer {
109         __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
110       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102:110

## L002 - Loss of precision due to division by large numbers:

Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


728         return (usdcAmount * redeemFee) / FEE_GRANULARITY;


716         return (usdcAmount * mintFee) / FEE_GRANULARITY;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L716:716

## L003 - Division by zero not prevented:

The divisions below take an input parameter which does not have any zero-value checks, which may lead to the functions reverting when zero is passed.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


748         return amount / decimalsMultiplier;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L748:748


## L004 - Missing checks for `address(0x0)` when assigning values to address state variables:

This issue arises when an address state variable is assigned a value without a preceding check to ensure it isn't address(0x0). This can lead to unexpected behavior as address(0x0) often represents an uninitialized address.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


642         oracle = IRWAOracle(_oracle);


670         investorBasedRateLimiter = IInvestorBasedRateLimiter(
671           _investorBasedRateLimiter
672         );


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L670:672

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


136         ousg = IERC20(_ousg);


137         oracle = IRWAOracle(_oracle);


615         oracle = IRWAOracle(_oracle);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L615:615

</details>

## L005 - Upgradeable contract is missing a __gap[50] storage variable to allow for new storage variables in later versions:

This issue arises when an upgradeable contract doesn't include a __gap[50] storage variable. This variable is crucial for facilitating future upgrades and preserving storage layout.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55


## L006 - Prefer continue over revert model in iteration:

Preferably, it's better to skip operations on array indices when a condition is not met instead of reverting the entire transaction. Reverting could be exploited by malicious actors who might intentionally introduce array objects failing conditional checks, disrupting group operations. It's advisable to skip array indices rather than revert, unless there are valid security or logic reasons for doing otherwise


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


804         for (uint256 i = 0; i < exCallData.length; ++i) {
805           (bool success, bytes memory ret) = address(exCallData[i].target).call{
806             value: exCallData[i].value
807           }(exCallData[i].data);
808           require(success, "Call Failed");
809           results[i] = ret;
810         }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804:810

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


125         for (uint256 i = 0; i < exCallData.length; ++i) {
126           (bool success, bytes memory ret) = address(exCallData[i].target).call{
127             value: exCallData[i].value
128           }(exCallData[i].data);
129           require(success, "Call Failed");
130           results[i] = ret;
131         }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125:131

## L007 - Upgradeable contract not initialized:

Upgradeable contracts are initialized via an initializer function rather than by a constructor. Leaving such a contract uninitialized may lead to it being taken over by a malicious user.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55

## L008 - External call recipient may consume all transaction gas:

There is no limit specified on the amount of gas used, so the recipient can use up all of the transaction's gas, causing it to revert. Use `addr.call{gas: <amount>}()` or [this](https://github.com/nomad-xyz/ExcessivelySafeCall) library instead.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


805           (bool success, bytes memory ret) = address(exCallData[i].target).call{
806             value: exCallData[i].value
807           }(exCallData[i].data);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805:807

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


126           (bool success, bytes memory ret) = address(exCallData[i].target).call{
127             value: exCallData[i].value
128           }(exCallData[i].data);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126:128

## L009 - Setters should have initial value check:

Setters should have initial value check to prevent assigning wrong value to the variable. Assginment of wrong value can lead to unexpected behavior of the contract.


<details>
<summary>Click to show 15 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


498       function setInstantMintLimit(
499         uint256 _instantMintLimit
500       ) external override onlyRole(CONFIGURER_ROLE) {
501         _setInstantMintLimit(_instantMintLimit);
502       }


512       function setInstantRedemptionLimit(
513         uint256 _instantRedemptionLimit
514       ) external override onlyRole(CONFIGURER_ROLE) {
515         _setInstantRedemptionLimit(_instantRedemptionLimit);
516       }


526       function setInstantMintLimitDuration(
527         uint256 _instantMintLimitDuration
528       ) external override onlyRole(CONFIGURER_ROLE) {
529         _setInstantMintLimitDuration(_instantMintLimitDuration);
530       }


540       function setInstantRedemptionLimitDuration(
541         uint256 _instantRedemptionLimitDuratioin
542       ) external override onlyRole(CONFIGURER_ROLE) {
543         _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
544       }


554       function setMintFee(
555         uint256 _mintFee
556       ) external override onlyRole(CONFIGURER_ROLE) {
557         require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558         emit MintFeeSet(mintFee, _mintFee);
559         mintFee = _mintFee;
560       }


567       function setRedeemFee(
568         uint256 _redeemFee
569       ) external override onlyRole(CONFIGURER_ROLE) {
570         require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571         emit RedeemFeeSet(redeemFee, _redeemFee);
572         redeemFee = _redeemFee;
573       }


581       function setMinimumDepositAmount(
582         uint256 _minimumDepositAmount
583       ) external override onlyRole(CONFIGURER_ROLE) {
584         require(
585           _minimumDepositAmount >= FEE_GRANULARITY,
586           "setMinimumDepositAmount: Amount too small"
587         );
588     
589         emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
590         minimumDepositAmount = _minimumDepositAmount;
591       }


599       function setMinimumRedemptionAmount(
600         uint256 _minimumRedemptionAmount
601       ) external override onlyRole(CONFIGURER_ROLE) {
602         require(
603           _minimumRedemptionAmount >= FEE_GRANULARITY,
604           "setMinimumRedemptionAmount: Amount too small"
605         );
606         emit MinimumRedemptionAmountSet(
607           minimumRedemptionAmount,
608           _minimumRedemptionAmount
609         );
610         minimumRedemptionAmount = _minimumRedemptionAmount;
611       }


622       function setMinimumBUIDLRedemptionAmount(
623         uint256 _minimumBUIDLRedemptionAmount
624       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
625         emit MinimumBUIDLRedemptionAmountSet(
626           minBUIDLRedeemAmount,
627           _minimumBUIDLRedemptionAmount
628         );
629         minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
630       }


638       function setOracle(
639         address _oracle
640       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
641         emit OracleSet(address(oracle), _oracle);
642         oracle = IRWAOracle(_oracle);
643       }


650       function setFeeReceiver(
651         address _feeReceiver
652       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
653         require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
654         emit FeeReceiverSet(feeReceiver, _feeReceiver);
655         feeReceiver = _feeReceiver;
656       }


663       function setInvestorBasedRateLimiter(
664         address _investorBasedRateLimiter
665       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
666         emit InvestorBasedRateLimiterSet(
667           address(investorBasedRateLimiter),
668           _investorBasedRateLimiter
669         );
670         investorBasedRateLimiter = IInvestorBasedRateLimiter(
671           _investorBasedRateLimiter
672         );
673       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663:673

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


613       function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
614         emit OracleSet(address(oracle), _oracle);
615         oracle = IRWAOracle(_oracle);
616       }


650       function setKYCRegistry(
651         address registry
652       ) external override onlyRole(CONFIGURER_ROLE) {
653         _setKYCRegistry(registry);
654       }


656       function setKYCRequirementGroup(
657         uint256 group
658       ) external override onlyRole(CONFIGURER_ROLE) {
659         _setKYCRequirementGroup(group);
660       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:660

</details>

## L010 - Constant decimal values:

The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations. Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations. Always retrieve and use the decimals() function from the token contract itself when performing calculations involving token amounts.


<details>
<summary>Click to show 6 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


689         uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;


704         usdcOwed = _scaleDown(amountE36 / 1e18);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704:704

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


190           (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);


202           (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);


367           (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();


375           (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L375:375

</details>

## L011 - No limits when setting state variable amounts:

It is important to ensure state variables numbers are set to a reasonable value.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


559         mintFee = _mintFee;


572         redeemFee = _redeemFee;


629         minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L629:629

## L012 - Allowed fees/rates should be capped by smart contracts:

Fees/rates should be required to be below 100%, preferably at a much lower limit, to ensure users don't have to monitor the blockchain for changes prior to using the protocol.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


554       function setMintFee(
555         uint256 _mintFee
556       ) external override onlyRole(CONFIGURER_ROLE) {
557         require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558         emit MintFeeSet(mintFee, _mintFee);
559         mintFee = _mintFee;
560       }


567       function setRedeemFee(
568         uint256 _redeemFee
569       ) external override onlyRole(CONFIGURER_ROLE) {
570         require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571         emit RedeemFeeSet(redeemFee, _redeemFee);
572         redeemFee = _redeemFee;
573       }


650       function setFeeReceiver(
651         address _feeReceiver
652       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
653         require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
654         emit FeeReceiverSet(feeReceiver, _feeReceiver);
655         feeReceiver = _feeReceiver;
656       }


663       function setInvestorBasedRateLimiter(
664         address _investorBasedRateLimiter
665       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
666         emit InvestorBasedRateLimiterSet(
667           address(investorBasedRateLimiter),
668           _investorBasedRateLimiter
669         );
670         investorBasedRateLimiter = IInvestorBasedRateLimiter(
671           _investorBasedRateLimiter
672         );
673       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663:673

</details>

## L013 - Owner can renounce ownership while system is paused:

The contract owner is not prevented from renouncing the ownership while the contract is paused, which would cause any user assets stored in the protocol to be locked indefinitely.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


642       function pause() external onlyRole(PAUSER_ROLE) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642:642

## L014 - Constructor contains no validation:

In Solidity, when values are being assigned in constructors to unsigned or integer variables, it's crucial to ensure the provided values adhere to the protocol's specific operational boundaries as laid out in the project specifications and documentation. If the constructors lack appropriate validation checks, there's a risk of setting state variables with values that could cause unexpected and potentially detrimental behavior within the contract's operations, violating the intended logic of the protocol. This can compromise the contract's security and impact the maintainability and reliability of the system. In order to avoid such issues, it is recommended to incorporate rigorous validation checks in constructors. These checks should align with the project's defined rules and constraints, making use of Solidity's built-in require function to enforce these conditions. If the validation checks fail, the require function will cause the transaction to revert, ensuring the integrity and adherence to the protocol's expected behavior.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


47        constructor(address _guardian) {
48          guardian = _guardian;
49        }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47:49

## L015 - For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS:

In Solidity, for loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where for loops can lead to DoS attacks: Nested for loops can become exceptionally gas expensive and should be used sparingly.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


794       function multiexcall(
795         ExCallData[] calldata exCallData
796       )
797         external
798         payable
799         override
800         onlyRole(DEFAULT_ADMIN_ROLE)
801         returns (bytes[] memory results)
802       {
803         results = new bytes[](exCallData.length);
804         for (uint256 i = 0; i < exCallData.length; ++i) {
805           (bool success, bytes memory ret) = address(exCallData[i].target).call{
806             value: exCallData[i].value
807           }(exCallData[i].data);
808           require(success, "Call Failed");
809           results[i] = ret;
810         }
811       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794:811

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


121       function multiexcall(
122         ExCallData[] calldata exCallData
123       ) external payable override onlyGuardian returns (bytes[] memory results) {
124         results = new bytes[](exCallData.length);
125         for (uint256 i = 0; i < exCallData.length; ++i) {
126           (bool success, bytes memory ret) = address(exCallData[i].target).call{
127             value: exCallData[i].value
128           }(exCallData[i].data);
129           require(success, "Call Failed");
130           results[i] = ret;
131         }
132       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121:132

## L016 - External calls in an unbounded for-loop may result in a DoS:

Consider limiting the number of iterations in for-loops that make external calls.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


804         for (uint256 i = 0; i < exCallData.length; ++i) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804:804

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


125         for (uint256 i = 0; i < exCallData.length; ++i) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125:125

## L017 - Contracts are not using their OZ Upgradeable counterparts:

The non-upgradeable standard version of OpenZeppelin’s library is inherited/used by the contracts. It would be safer to use the upgradeable versions of the library contracts to avoid unexpected behavior.

Use the contracts from `@openzeppelin/contracts-upgradeable` instead of `@openzeppelin/contracts` where applicable. See https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/tree/master/contracts for a list of available upgradeable contracts


<details>
<summary>Click to show 11 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


19      import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";


20      import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";


18      import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L18:18

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


19      import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19:19

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


23      import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";


20      import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";


19      import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";


21      import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";


18      import "contracts/external/openzeppelin/contracts/token/IERC20.sol";


22      import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";


24      import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L24:24

</details>

## L018 - Consider implementing two-step procedure for updating protocol addresses:

Lack of two-step procedure for critical operations leaves them error-prone. Consider adding two step procedure on the critical functions. See similar findings in previous Code4rena contests for reference: https://code4rena.com/reports/2022-06-illuminate/#2-critical-changes-should-use-two-step-procedure


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


638       function setOracle(


650       function setFeeReceiver(


663       function setInvestorBasedRateLimiter(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663:663

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


613       function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613:613

</details>

## L019 - `decimals()` is not a part of the ERC-20 standard:

The `decimals()` function is not a part of the [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20), and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.


<details>
<summary>Click to show 6 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


187           IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),


396           IERC20Metadata(address(buidl)).decimals() == 6,


392           IERC20Metadata(address(usdc)).decimals() == 6,


283           IERC20Metadata(address(usdc)).decimals() == 6,


191           IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),


204             (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L204:204

</details>



## L022 - Governance functions should be controlled by time locks:

Governance functions (such as upgrading contracts, setting critical parameters) should be controlled using time locks to introduce a delay between a proposal and its execution. This gives users time to exit before a potentially dangerous or malicious operation is applied.


<details>
<summary>Click to show 24 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


780       function pauseRedeem() external onlyRole(PAUSER_ROLE) {

554       function setMintFee(
555         uint256 _mintFee
556       ) external override onlyRole(CONFIGURER_ROLE) {

498       function setInstantMintLimit(
499         uint256 _instantMintLimit
500       ) external override onlyRole(CONFIGURER_ROLE) {

526       function setInstantMintLimitDuration(
527         uint256 _instantMintLimitDuration
528       ) external override onlyRole(CONFIGURER_ROLE) {

567       function setRedeemFee(
568         uint256 _redeemFee
569       ) external override onlyRole(CONFIGURER_ROLE) {

581       function setMinimumDepositAmount(
582         uint256 _minimumDepositAmount
583       ) external override onlyRole(CONFIGURER_ROLE) {

622       function setMinimumBUIDLRedemptionAmount(
623         uint256 _minimumBUIDLRedemptionAmount
624       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

638       function setOracle(
639         address _oracle
640       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

819       function retrieveTokens(
820         address token,
821         address to,
822         uint256 amount
823       ) external onlyRole(DEFAULT_ADMIN_ROLE) {

650       function setFeeReceiver(
651         address _feeReceiver
652       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

794       function multiexcall(
795         ExCallData[] calldata exCallData
796       )
797         external
798         payable
799         override
800         onlyRole(DEFAULT_ADMIN_ROLE)
801         returns (bytes[] memory results)
802       {

768       function pauseMint() external onlyRole(PAUSER_ROLE) {

599       function setMinimumRedemptionAmount(
600         uint256 _minimumRedemptionAmount
601       ) external override onlyRole(CONFIGURER_ROLE) {

540       function setInstantRedemptionLimitDuration(
541         uint256 _instantRedemptionLimitDuratioin
542       ) external override onlyRole(CONFIGURER_ROLE) {

774       function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {

512       function setInstantRedemptionLimit(
513         uint256 _instantRedemptionLimit
514       ) external override onlyRole(CONFIGURER_ROLE) {

663       function setInvestorBasedRateLimiter(
664         address _investorBasedRateLimiter
665       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

786       function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L786:789

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


656       function setKYCRequirementGroup(
657         uint256 group
658       ) external override onlyRole(CONFIGURER_ROLE) {

642       function pause() external onlyRole(PAUSER_ROLE) {

613       function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {

646       function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {

650       function setKYCRegistry(
651         address registry
652       ) external override onlyRole(CONFIGURER_ROLE) {

624       function burn(
625         address _account,
626         uint256 _amount
627       ) external onlyRole(BURNER_ROLE) {

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624:640

</details>

## L024 - approve()/safeApprove() may revert if the current approval is not zero:

Calling approve() without first calling approve(0) if the current approval is non-zero will revert with some tokens, such as Tether (USDT). While Tether is known to do this, it applies to other tokens as well, which are trying to protect against this attack vector. safeApprove() itself also implements this protection.Always reset the approval to zero before changing it to a new value (SafeERC20.forceApprove() does this for you), or use safeIncreaseAllowance()/safeDecreaseAllowance()


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


264         ousg.approve(address(rousg), ousgAmountOut);


464         buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L464:464



## NC002 - Events that mark critical parameter changes should contain both the old and the new value:

This should especially be done if the new value is not required to be different from the old value.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


641         emit OracleSet(address(oracle), _oracle);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L641:641

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


614         emit OracleSet(address(oracle), _oracle);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L614:614

## NC003 - Use scientific notation (e.g. 1e18) rather than exponentiation (e.g. 10**18):

While the compiler knows to optimize away the exponentiation, it's still better coding practice to use idioms that do not require compiler optimization, if they exist.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


203           10 **
204             (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L203:204

## NC004 - Event is not properly indexed:

Index event fields make the field more quickly accessible to off-chain tools that parse events. This is especially useful when it comes to filtering based on an address. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Where applicable, each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three applicable fields, all of the applicable fields should be indexed.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


141       event rOUSGDeployed(
142         address proxy,
143         address proxyAdmin,
144         address implementation,
145         string name,
146         string ticker
147       );


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141:147

## NC006 - Imports could be organized more systematically:

This issue arises when the contract's interface is not imported first, followed by each of the interfaces it uses, followed by all other files.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


20      import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L20:20

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


22      import "contracts/interfaces/IMulticall.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L22:22

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


26      import "contracts/rwaOracles/IRWAOracle.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L26:26

## NC007 - Constants in comparisons should appear on the left side:

This issue arises when constants in comparisons appear on the right side, which can lead to typo bugs.


<details>
<summary>Click to show 11 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


283           IERC20Metadata(address(usdc)).decimals() == 6,


311           ousgAmountOut > 0,


316         if (usdcfees > 0) {


392           IERC20Metadata(address(usdc)).decimals() == 6,


396           IERC20Metadata(address(buidl)).decimals() == 6,


418           usdcAmountOut > 0,


450         if (usdcFees > 0) {


557         require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");


570         require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570:570

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


416         require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");


432         require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432:432

</details>

## NC008 - Events may be emitted out of order due to reentrancy:

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls


<details>
<summary>Click to show 13 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


/// @audit transferFrom() called before event
321         emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);


/// @audit transfer() called before event
453         emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);


/// @audit transfer() called before event
270         emit InstantMintRebasingOUSG(
271           msg.sender,
272           usdcAmountIn,
273           ousgAmountOut,
274           rousgAmountOut
275         );


/// @audit transfer() called before event
435           emit MinimumBUIDLRedemption(
436             msg.sender,
437             minBUIDLRedeemAmount,
438             usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
439           );


/// @audit transferFrom() called before event
380         emit InstantRedemptionRebasingOUSG(
381           msg.sender,
382           rousgAmountIn,
383           ousgAmountIn,
384           usdcAmountOut
385         );


/// @audit transferFrom() called before event
350         emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut);


/// @audit transfer() called before event
443           emit BUIDLRedemptionSkipped(
444             msg.sender,
445             usdcAmountToRedeem,
446             usdcBalance - usdcAmountToRedeem
447           );


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L443:447

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


/// @audit transfer() called before event
442         emit TransferShares(msg.sender, address(0), ousgSharesAmount);


/// @audit transfer() called before event
441         emit Transfer(msg.sender, address(0), _rOUSGAmount);


/// @audit transfer() called before event
639         emit TransferShares(_account, address(0), ousgSharesAmount);


/// @audit transfer() called before event
638         emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));


/// @audit transferFrom() called before event
420         emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));


/// @audit transferFrom() called before event
421         emit TransferShares(address(0), msg.sender, ousgSharesAmount);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L421:421

</details>

## NC009 - Import declarations should import specific identifiers, rather than the whole file:

Using import declarations of the form import {<identifier_name>} from 'some/file.sol' avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation


<details>
<summary>Click to show 11 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


18      import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";


19      import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";


20      import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L20:20

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


19      import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19:19

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


18      import "contracts/external/openzeppelin/contracts/token/IERC20.sol";


19      import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";


20      import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";


21      import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";


22      import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";


23      import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";


24      import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L24:24

</details>

## NC010 - Public functions not called by the contract should be declared external instead:

Contracts [are allowed](https://docs.soliditylang.org/en/latest/contracts.html#function-overriding) to override their parents' functions and change the visibility from `external` to `public`.


<details>
<summary>Click to show 12 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


166       function name() public pure returns (string memory) {
167         return "Rebasing OUSG";
168       }


174       function symbol() public pure returns (string memory) {
175         return "rOUSG";
176       }


181       function decimals() public pure returns (uint8) {
182         return 18;
183       }


188       function totalSupply() public view returns (uint256) {
189         return
190           (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
191       }


199       function balanceOf(address _account) public view returns (uint256) {
200         return
201           (_sharesOf(_account) * getOUSGPrice()) /
202           (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
203       }


231       function allowance(
232         address _owner,
233         address _spender
234       ) public view returns (uint256) {
235         return allowances[_owner][_spender];
236       }


251       function approve(address _spender, uint256 _amount) public returns (bool) {
252         _approve(msg.sender, _spender, _amount);
253         return true;
254       }


302       function increaseAllowance(
303         address _spender,
304         uint256 _addedValue
305       ) public returns (bool) {
306         _approve(
307           msg.sender,
308           _spender,
309           allowances[msg.sender][_spender] + _addedValue
310         );
311         return true;
312       }


328       function decreaseAllowance(
329         address _spender,
330         uint256 _subtractedValue
331       ) public returns (bool) {
332         uint256 currentAllowance = allowances[msg.sender][_spender];
333         require(
334           currentAllowance >= _subtractedValue,
335           "DECREASED_ALLOWANCE_BELOW_ZERO"
336         );
337         _approve(msg.sender, _spender, currentAllowance - _subtractedValue);
338         return true;
339       }


347       function getTotalShares() public view returns (uint256) {
348         return totalShares;
349       }


356       function sharesOf(address _account) public view returns (uint256) {
357         return _sharesOf(_account);
358       }


397       function transferShares(
398         address _recipient,
399         uint256 _sharesAmount
400       ) public returns (uint256) {
401         _transferShares(msg.sender, _recipient, _sharesAmount);
402         emit TransferShares(msg.sender, _recipient, _sharesAmount);
403         uint256 tokensAmount = getROUSGByShares(_sharesAmount);
404         emit Transfer(msg.sender, _recipient, tokensAmount);
405         return tokensAmount;
406       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397:406

</details>

## NC011 - Constant redefined elsewhere:

Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A cheap way to store constants in a single location is to create an internal constant in a library. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;

  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");

  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95:95

## NC012 - Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, for readability:

Well-organized data structures make code reviews easier, which may lead to fewer bugs. Consider combining related mappings into mappings to structs, so it's clear what data is related


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


72        mapping(address => uint256) private shares;
73      
74        /// @dev Allowances are nominated in tokens, not token shares.
75        mapping(address => mapping(address => uint256)) private allowances;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72:75

## NC013 - Variables need not be initialized to zero:

The default value for variables is zero, so initializing them to zero is superfluous.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


804         for (uint256 i = 0; i < exCallData.length; ++i) {


99        uint256 public mintFee = 0;


102       uint256 public redeemFee = 0;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L102:102

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


125         for (uint256 i = 0; i < exCallData.length; ++i) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125:125

</details>

## NC014 - Variable names for `immutable`s should use CONSTANT_CASE:

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE).


<details>
<summary>Click to show 8 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


72        IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;


75        IRWALike public immutable ousg;


78        ROUSG public immutable rousg;


81        IERC20 public immutable buidl;


84        IBUIDLRedeemer public immutable buidlRedeemer;


87        uint256 public immutable decimalsMultiplier;


90        address public immutable usdcReceiver;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90:90

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


40        address internal immutable guardian;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40:40

</details>

## NC015 - Lines are too long:

Usually lines in source code are limited to 80 characters. Today's screens are much larger so it's reasonable to stretch this in some cases. The solidity style guide recommends a maximumum line length of 120 characters, so the lines below should be split when they reach that length.


<details>
<summary>Click to show 10 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


‚Ėą‚Ėą ,‚Ėą‚Ėą¬¨ ‚ĖĄ‚Ėą‚Ėą‚Ėą‚Ėą‚ĖĄ  ‚ĖÄ‚Ėą‚ĖĄ ‚ēô‚Ėą‚ĖĄ      ‚ĖĄ‚Ėą‚Ėą‚Ėą‚ĖÄ‚ĖÄ‚Ėą‚Ėą‚Ėą‚ĖĄ   ‚Ėą‚Ėą‚Ėą‚ĖĄ    ‚Ėą‚Ėą  ‚Ėą‚Ėą‚Ėą‚ĖÄ‚ĖÄ‚ĖÄ‚Ėą‚Ėą‚Ėą‚ĖĄ    ‚ĖĄ‚Ėą‚Ėą‚Ėą‚ĖÄ‚ĖÄ‚Ėą‚Ėą‚Ėą,

‚Ėą‚Ėą  ‚Ėą‚Ėą ‚ēí‚Ėą‚ĖÄ'   ‚ēô‚Ėą‚ĖĆ ‚ēô‚Ėą‚ĖĆ ‚Ėą‚Ėą     ‚Ėź‚Ėą‚Ėą      ‚Ėą‚Ėą‚Ėą  ‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą,  ‚Ėą‚Ėą  ‚Ėą‚Ėą‚ĖĆ    ‚ĒĒ‚Ėą‚Ėą‚ĖĆ  ‚Ėą‚Ėą‚ĖĆ     ‚ĒĒ‚Ėą‚Ėą‚ĖĆ

‚Ėą‚Ėą ‚Ėź‚Ėą‚ĖĆ ‚Ėą‚Ėą      ‚ēü‚Ėą  ‚Ėą‚ĖĆ ‚ēü‚Ėą     ‚Ėą‚Ėą‚ĖĆ      ‚Ėź‚Ėą‚Ėą  ‚Ėą‚Ėą ‚ĒĒ‚Ėą‚Ėą‚Ėą ‚Ėą‚Ėą  ‚Ėą‚Ėą‚ĖĆ     ‚ēü‚Ėą‚Ėą j‚Ėą‚Ėą       ‚ēü‚Ėą‚Ėą

‚ēü‚Ėą  ‚Ėą‚Ėą ‚ēô‚Ėą‚Ėą    ‚ĖĄ‚Ėą‚ĖÄ ‚Ėź‚Ėą‚ĖĆ ‚Ėą‚Ėą     ‚ēô‚Ėą‚Ėą      ‚Ėą‚Ėą‚ĖĆ  ‚Ėą‚Ėą   ‚ēô‚Ėą‚Ėą‚Ėą‚Ėą  ‚Ėą‚Ėą‚ĖĆ    ‚ĖĄ‚Ėą‚Ėą‚ĖÄ  ‚Ėą‚Ėą‚ĖĆ     ,‚Ėą‚Ėą‚ĖÄ

‚Ėą‚Ėą "‚Ėą‚Ėą, ‚ēô‚ĖÄ‚ĖÄ‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ćź      ‚ēô‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚ĖÄ   ‚Ėą‚Ėą     ‚ēô‚Ėą‚Ėą  ‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚ĖÄ‚ĖÄ     ‚ēô‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚ĖÄ`

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L10:10

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


‚Ėą‚Ėą ,‚Ėą‚Ėą¬¨ ‚ĖĄ‚Ėą‚Ėą‚Ėą‚Ėą‚ĖĄ  ‚ĖÄ‚Ėą‚ĖĄ ‚ēô‚Ėą‚ĖĄ      ‚ĖĄ‚Ėą‚Ėą‚Ėą‚ĖÄ‚ĖÄ‚Ėą‚Ėą‚Ėą‚ĖĄ   ‚Ėą‚Ėą‚Ėą‚ĖĄ    ‚Ėą‚Ėą  ‚Ėą‚Ėą‚Ėą‚ĖÄ‚ĖÄ‚ĖÄ‚Ėą‚Ėą‚Ėą‚ĖĄ    ‚ĖĄ‚Ėą‚Ėą‚Ėą‚ĖÄ‚ĖÄ‚Ėą‚Ėą‚Ėą,

‚Ėą‚Ėą  ‚Ėą‚Ėą ‚ēí‚Ėą‚ĖÄ'   ‚ēô‚Ėą‚ĖĆ ‚ēô‚Ėą‚ĖĆ ‚Ėą‚Ėą     ‚Ėź‚Ėą‚Ėą      ‚Ėą‚Ėą‚Ėą  ‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą,  ‚Ėą‚Ėą  ‚Ėą‚Ėą‚ĖĆ    ‚ĒĒ‚Ėą‚Ėą‚ĖĆ  ‚Ėą‚Ėą‚ĖĆ     ‚ĒĒ‚Ėą‚Ėą‚ĖĆ

‚Ėą‚Ėą ‚Ėź‚Ėą‚ĖĆ ‚Ėą‚Ėą      ‚ēü‚Ėą  ‚Ėą‚ĖĆ ‚ēü‚Ėą     ‚Ėą‚Ėą‚ĖĆ      ‚Ėź‚Ėą‚Ėą  ‚Ėą‚Ėą ‚ĒĒ‚Ėą‚Ėą‚Ėą ‚Ėą‚Ėą  ‚Ėą‚Ėą‚ĖĆ     ‚ēü‚Ėą‚Ėą j‚Ėą‚Ėą       ‚ēü‚Ėą‚Ėą

‚ēü‚Ėą  ‚Ėą‚Ėą ‚ēô‚Ėą‚Ėą    ‚ĖĄ‚Ėą‚ĖÄ ‚Ėź‚Ėą‚ĖĆ ‚Ėą‚Ėą     ‚ēô‚Ėą‚Ėą      ‚Ėą‚Ėą‚ĖĆ  ‚Ėą‚Ėą   ‚ēô‚Ėą‚Ėą‚Ėą‚Ėą  ‚Ėą‚Ėą‚ĖĆ    ‚ĖĄ‚Ėą‚Ėą‚ĖÄ  ‚Ėą‚Ėą‚ĖĆ     ,‚Ėą‚Ėą‚ĖÄ

‚Ėą‚Ėą "‚Ėą‚Ėą, ‚ēô‚ĖÄ‚ĖÄ‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ćź      ‚ēô‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚ĖÄ   ‚Ėą‚Ėą     ‚ēô‚Ėą‚Ėą  ‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚ĖÄ‚ĖÄ     ‚ēô‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚Ėą‚ĖÄ`

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L10:10

</details>

## NC016 - Function declarations should have NatSpec descriptions:

Function declarations should be preceded by a NatSpec comment.


<details>
<summary>Click to show 8 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


794       function multiexcall(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794:794

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


47        constructor(address _guardian) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47:47

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


102       function initialize(


378       function getOUSGPrice() public view returns (uint256 price) {


642       function pause() external onlyRole(PAUSER_ROLE) {


646       function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {


650       function setKYCRegistry(


656       function setKYCRequirementGroup(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:656

</details>

## NC017 - Contract declarations should have `@notice` tags:

`@notice` is used to explain to end users what the contract does, and the compiler interprets `///` or `/**` comments as this tag if one wasn't explicitly provided.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


49      contract OUSGInstantManager is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49:49

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


37      contract ROUSGFactory is IMulticall {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37:37

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55

## NC018 - Error declarations should have NatSpec descriptions:




```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


90        error UnwrapTooSmall();


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90:90

## NC019 - Contract does not follow the Solidity style guide's suggested layout ordering:

The [style guide](https://docs.soliditylang.org/en/v0.8.16/style-guide.html#order-of-layout) says that, within a contract, the ordering should be 1) Type declarations, 2) State variables, 3) Events, 4) Modifiers, and 5) Functions, but the contract(s) below do not follow this ordering.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


756       modifier whenMintNotPaused() {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L756:756

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


141       event rOUSGDeployed(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141:141

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


149       event TransferShares(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L149:149

## NC020 - Non-external/public variable names should begin with an underscore:

According to the Solidity Style Guide, non-external/public variable names should begin with an underscore


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


40        address internal immutable guardian;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40:40

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


72        mapping(address => uint256) private shares;


75        mapping(address => mapping(address => uint256)) private allowances;


78        uint256 private totalShares;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L78:78

</details>

## NC021 - Expressions for constant values such as a call to `keccak256()`, should use `immutable` rather than `constant`:

While it **doesn't save any gas** because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between `constant` variables and `immutable` variables, and they should each be used in their appropriate contexts. `constants` should be used for literal values written into the code, and `immutable` variables should be used for expressions, or values calculated in, or passed into the constructor.


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


57        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


60        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60:60

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


93        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


94        bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");


95        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95:95

</details>

## NC022 - Contracts should have full test coverage:

While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.


```solidity
File: Various Files


None

```

## NC023 - Large or complicated code bases should implement invariant tests:

Large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts, should implement invariant fuzzing tests. Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold. Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers, with properly and extensively-written invariants, can close this testing gap significantly.


```solidity
File: Various Files


None

```

## NC024 - Long functions should be refactored into multiple, smaller, functions:




```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


144       constructor(
145         address defaultAdmin,
146         address _usdc,
147         address _usdcReciever,
148         address _feeReceiver,
149         address _ousgOracle,
150         address _ousg,
151         address _rousg,
152         address _buidl,
153         address _buidlRedeemer,
154         RateLimiterConfig memory rateLimiterConfig
155       )
156         InstantMintTimeBasedRateLimiter(
157           rateLimiterConfig.mintLimitDuration,
158           rateLimiterConfig.redeemLimitDuration,
159           rateLimiterConfig.mintLimit,
160           rateLimiterConfig.redeemLimit
161         )
162       {
163         require(
164           address(_usdc) != address(0),
165           "OUSGInstantManager: USDC cannot be 0x0"
166         );
167         require(
168           address(_usdcReciever) != address(0),
169           "OUSGInstantManager: USDC Receiver cannot be 0x0"
170         );
171         require(
172           address(_feeReceiver) != address(0),
173           "OUSGInstantManager: feeReceiver cannot be 0x0"
174         );
175         require(
176           address(_ousgOracle) != address(0),
177           "OUSGInstantManager: OUSG Oracle cannot be 0x0"
178         );
179         require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180         require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181         require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
182         require(
183           address(_buidlRedeemer) != address(0),
184           "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
185         );
186         require(
187           IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
188           "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
189         );
190         require(
191           IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
192           "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
193         );
194         usdc = IERC20(_usdc);
195         usdcReceiver = _usdcReciever;
196         feeReceiver = _feeReceiver;
197         oracle = IRWAOracle(_ousgOracle);
198         ousg = IRWALike(_ousg);
199         rousg = ROUSG(_rousg);
200         buidl = IERC20(_buidl);
201         buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
202         decimalsMultiplier =
203           10 **
204             (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());
205         require(
206           OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
207             rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
208           "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
209         );
210     
211         _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
212         _grantRole(CONFIGURER_ROLE, defaultAdmin);
213         _grantRole(PAUSER_ROLE, defaultAdmin);
214       }


388       function _redeem(
389         uint256 ousgAmountIn
390       ) internal returns (uint256 usdcAmountOut) {
391         require(
392           IERC20Metadata(address(usdc)).decimals() == 6,
393           "OUSGInstantManager::_redeem: USDC decimals must be 6"
394         );
395         require(
396           IERC20Metadata(address(buidl)).decimals() == 6,
397           "OUSGInstantManager::_redeem: BUIDL decimals must be 6"
398         );
399         uint256 ousgPrice = getOUSGPrice();
400         uint256 usdcAmountToRedeem = _getRedemptionAmount(ousgAmountIn, ousgPrice);
401     
402         require(
403           usdcAmountToRedeem >= minimumRedemptionAmount,
404           "OUSGInstantManager::_redeem: Redemption amount too small"
405         );
406         _checkAndUpdateInstantRedemptionLimit(usdcAmountToRedeem);
407     
408         if (address(investorBasedRateLimiter) != address(0)) {
409           investorBasedRateLimiter.checkAndUpdateRedeemLimit(
410             msg.sender,
411             usdcAmountToRedeem
412           );
413         }
414     
415         uint256 usdcFees = _getInstantRedemptionFees(usdcAmountToRedeem);
416         usdcAmountOut = usdcAmountToRedeem - usdcFees;
417         require(
418           usdcAmountOut > 0,
419           "OUSGInstantManager::_redeem: redeem amount can't be zero"
420         );
421     
422         ousg.burn(ousgAmountIn);
423     
424         uint256 usdcBalance = usdc.balanceOf(address(this));
425     
426         if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
427           // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
428           // to cover the full amount
429           _redeemBUIDL(usdcAmountToRedeem);
430         } else if (usdcAmountToRedeem > usdcBalance) {
431           // There isn't enough USDC held by this contract to cover the redemption,
432           // so we perform a BUIDL redemption of BUIDL's minimum required amount.
433           // The remaining amount of USDC will be held in the contract for future redemptions.
434           _redeemBUIDL(minBUIDLRedeemAmount);
435           emit MinimumBUIDLRedemption(
436             msg.sender,
437             minBUIDLRedeemAmount,
438             usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
439           );
440         } else {
441           // We have enough USDC sitting in this contract already, so use it
442           // to cover the redemption and fees without redeeming more BUIDL.
443           emit BUIDLRedemptionSkipped(
444             msg.sender,
445             usdcAmountToRedeem,
446             usdcBalance - usdcAmountToRedeem
447           );
448         }
449     
450         if (usdcFees > 0) {
451           usdc.transfer(feeReceiver, usdcFees);
452         }
453         emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);
454     
455         usdc.transfer(msg.sender, usdcAmountOut);
456       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388:456

## NC025 - Strings should use double quotes rather than single quotes:

See the Solidity Style <a href="https://docs.soliditylang.org/en/v0.8.20/style-guide.html#other-recommendations">Guide</a>


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


594           require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");


604           require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd");


599           require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L599:599

## NC026 - Consider bounding input array length:

The functions below take in an unbounded array, and make function calls for entries in the array. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to `require()` that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


804         for (uint256 i = 0; i < exCallData.length; ++i) {
805           (bool success, bytes memory ret) = address(exCallData[i].target).call{
806             value: exCallData[i].value
807           }(exCallData[i].data);
808           require(success, "Call Failed");
809           results[i] = ret;
810         }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804:810

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


125         for (uint256 i = 0; i < exCallData.length; ++i) {
126           (bool success, bytes memory ret) = address(exCallData[i].target).call{
127             value: exCallData[i].value
128           }(exCallData[i].data);
129           require(success, "Call Failed");
130           results[i] = ret;
131         }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125:131

## NC027 - Variables should be named in mixedCase style:

As the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#naming-styles) suggests: arguments, local variables and mutable state variables should be named in mixedCase style.


<details>
<summary>Click to show 9 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


120       uint256 public minBUIDLRedeemAmount = 250_000e6;


623         uint256 _minimumBUIDLRedemptionAmount


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L623:623

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


41        ROUSG public rOUSGImplementation;


84          ROUSG rOUSGProxied = ROUSG(address(rOUSGProxy));


43        TokenProxy public rOUSGProxy;


42        ProxyAdmin public rOUSGProxyAdmin;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L42:42

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


431       function unwrap(uint256 _rOUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


364         uint256 _rOUSGAmount


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L364:364

</details>

## NC028 - Consider using named mappings:

Consider moving to solidity version 0.8.18 or later, and using [named mappings](https://ethereum.stackexchange.com/a/145555) to make it easier to understand the purpose of each mapping.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


72        mapping(address => uint256) private shares;


75        mapping(address => mapping(address => uint256)) private allowances;


75        mapping(address => mapping(address => uint256)) private allowances;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75:75

## NC029 - Use allowlist/denylist rather than whitelist/blacklist:

Use alternative variants, e.g. allowlist/denylist instead of whitelist/blacklist.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


294        * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42


319        * https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/IERC20.sol#L42


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L319:319

## NC030 - Function names should use lowerCamelCase:

According to the Solidity [style guide](https://docs.soliditylang.org/en/latest/style-guide.html#function-names) function names should be in `mixedCase` (lowerCamelCase).


<details>
<summary>Click to show 13 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


254       function mintRebasingOUSG(


362       function redeemRebasingOUSG(


458       function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {


479       function getOUSGPrice() public view returns (uint256 price) {


622       function setMinimumBUIDLRedemptionAmount(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622:622

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


70        function deployRebasingOUSG(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70:70

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


112       function __rOUSG_init(


128       function __rOUSG_init_unchained(


363       function getSharesByROUSG(


373       function getROUSGByShares(uint256 _shares) public view returns (uint256) {


378       function getOUSGPrice() public view returns (uint256 price) {


650       function setKYCRegistry(


656       function setKYCRequirementGroup(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:656

</details>

## NC031 - Consider adding a deny-list:

Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


49      contract OUSGInstantManager is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49:49

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


37      contract ROUSGFactory is IMulticall {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37:37

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55

## NC032 - Custom errors should be used rather than `revert()`/`require()`:

Custom errors are available from solidity version 0.8.4. Custom errors are more easily processed in `try`-`catch` blocks, and are easier to re-use and maintain.


<details>
<summary>Click to show 50 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


163         require(


167         require(


171         require(


175         require(


179         require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");


180         require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");


181         require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");


182         require(


186         require(


190         require(


205         require(


282         require(


286         require(


298         require(


310         require(


344         require(


371         require(


391         require(


395         require(


402         require(


417         require(


459         require(


466         require(


481         require(


557         require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");


570         require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");


584         require(


602         require(


653         require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");


757         require(!mintPaused, "OUSGInstantManager: Mint paused");


763         require(!redeemPaused, "OUSGInstantManager: Redeem paused");


808           require(success, "Call Failed");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L808:808

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


76          require(!initialized, "ROUSGFactory: rOUSG already deployed");


129           require(success, "Call Failed");


150         require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L150:150

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


282         require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");


333         require(


416         require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");


432         require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");


477         require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");


478         require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");


506         require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");


507         require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");


512         require(


533         require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");


558         require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS");


563         require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE");


594           require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");


599           require(_getKYCStatus(from), "rOUSG: 'from' address not KYC'd");


604           require(_getKYCStatus(to), "rOUSG: 'to' address not KYC'd");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L604:604

</details>

## NC033 - Custom error has no error details:

Consider adding parameters to the error to indicate which user or values caused the failure.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


90        error UnwrapTooSmall();


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90:90

## NC034 - Contract uses both `require()`/`revert()` as well as custom errors:

Consider using just one method in a single file


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55

## NC035 - Consider moving `msg.sender` checks to a common authorization `modifier`:




<details>
<summary>Click to show 4 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


298         require(
299           usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
300           "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
301         );


344         require(
345           ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
346           "OUSGInstantManager::redeem: Insufficient allowance"
347         );


371         require(
372           rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
373           "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
374         );


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L371:374

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


594           require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594:594

</details>

## NC036 - Events are missing sender information:

When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the msg.sender the events of these types of action will make events much more useful to end users. Include `msg.sender` in the event output.


<details>
<summary>Click to show 11 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


558         emit MintFeeSet(mintFee, _mintFee);


571         emit RedeemFeeSet(redeemFee, _redeemFee);


589         emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);


606         emit MinimumRedemptionAmountSet(
607           minimumRedemptionAmount,
608           _minimumRedemptionAmount
609         );


625         emit MinimumBUIDLRedemptionAmountSet(
626           minBUIDLRedeemAmount,
627           _minimumBUIDLRedemptionAmount
628         );


641         emit OracleSet(address(oracle), _oracle);


654         emit FeeReceiverSet(feeReceiver, _feeReceiver);


666         emit InvestorBasedRateLimiterSet(
667           address(investorBasedRateLimiter),
668           _investorBasedRateLimiter
669         );


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L666:669

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


96          emit rOUSGDeployed(
97            address(rOUSGProxy),
98            address(rOUSGProxyAdmin),
99            address(rOUSGImplementation),
100           rOUSGProxied.name(),
101           rOUSGProxied.symbol()
102         );


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L96:102

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


614         emit OracleSet(address(oracle), _oracle);


639         emit TransferShares(_account, address(0), ousgSharesAmount);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L639:639

</details>

## NC037 - SPDX-License-Identifier should be on the first line:

The SPDX-License-Identifier is not on the first line of the file, it should always be on the first line.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


1       /**SPDX-License-Identifier: BUSL-1.1


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L1:1

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


1       /**SPDX-License-Identifier: BUSL-1.1


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L1:1

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


1       /**SPDX-License-Identifier: BUSL-1.1


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L1:1

## NC038 - Zero as a function argument should have a descriptive meaning:

Consider using descriptive constants or an enum instead of passing zero directly on function calls, as that might be error-prone, to fully describe the caller's intention.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


38        bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);


38        bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38:38

## NC039 - Function names should differ to make the code more readable:

In Solidity, while function overriding allows for functions with the same name to coexist, it is advisable to avoid this practice to enhance code readability and maintainability. Having multiple functions with the same name, even with different parameters or in inherited contracts, can cause confusion and increase the likelihood of errors during development, testing, and debugging. Using distinct and descriptive function names not only clarifies the purpose and behavior of each function, but also helps prevent unintended function calls or incorrect overriding. By adopting a clear and consistent naming convention, developers can create more comprehensible and maintainable smart contracts.


<details>
<summary>Click to show 6 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }

  function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }

  function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794:811

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
  }

  function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613:616

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


  function multiexcall(
    ExCallData[] calldata exCallData
  ) external payable override onlyGuardian returns (bytes[] memory results) {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121:132

</details>

## NC040 - It is standard for all external and public functions to be override from an interface:

This is to ensure the whole API is extracted in an interface


<details>
<summary>Click to show 51 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


230       function mint(
231         uint256 usdcAmountIn
232       )
233         external
234         override
235         nonReentrant
236         whenMintNotPaused
237         returns (uint256 ousgAmountOut)
238       {
239         ousgAmountOut = _mint(usdcAmountIn, msg.sender);
240         emit InstantMintOUSG(msg.sender, usdcAmountIn, ousgAmountOut);
241       }


254       function mintRebasingOUSG(
255         uint256 usdcAmountIn
256       )
257         external
258         override
259         nonReentrant
260         whenMintNotPaused
261         returns (uint256 rousgAmountOut)
262       {
263         uint256 ousgAmountOut = _mint(usdcAmountIn, address(this));
264         ousg.approve(address(rousg), ousgAmountOut);
265         rousg.wrap(ousgAmountOut);
266         rousgAmountOut = rousg.getROUSGByShares(
267           ousgAmountOut * OUSG_TO_ROUSG_SHARES_MULTIPLIER
268         );
269         rousg.transfer(msg.sender, rousgAmountOut);
270         emit InstantMintRebasingOUSG(
271           msg.sender,
272           usdcAmountIn,
273           ousgAmountOut,
274           rousgAmountOut
275         );
276       }


335       function redeem(
336         uint256 ousgAmountIn
337       )
338         external
339         override
340         nonReentrant
341         whenRedeemNotPaused
342         returns (uint256 usdcAmountOut)
343       {
344         require(
345           ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
346           "OUSGInstantManager::redeem: Insufficient allowance"
347         );
348         ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
349         usdcAmountOut = _redeem(ousgAmountIn);
350         emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut);
351       }


362       function redeemRebasingOUSG(
363         uint256 rousgAmountIn
364       )
365         external
366         override
367         nonReentrant
368         whenRedeemNotPaused
369         returns (uint256 usdcAmountOut)
370       {
371         require(
372           rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
373           "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
374         );
375         rousg.transferFrom(msg.sender, address(this), rousgAmountIn);
376         rousg.unwrap(rousgAmountIn);
377         uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /
378           OUSG_TO_ROUSG_SHARES_MULTIPLIER;
379         usdcAmountOut = _redeem(ousgAmountIn);
380         emit InstantRedemptionRebasingOUSG(
381           msg.sender,
382           rousgAmountIn,
383           ousgAmountIn,
384           usdcAmountOut
385         );
386       }


479       function getOUSGPrice() public view returns (uint256 price) {
480         (price, ) = oracle.getPriceData();
481         require(
482           price > MINIMUM_OUSG_PRICE,
483           "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
484         );
485       }


498       function setInstantMintLimit(
499         uint256 _instantMintLimit
500       ) external override onlyRole(CONFIGURER_ROLE) {
501         _setInstantMintLimit(_instantMintLimit);
502       }


512       function setInstantRedemptionLimit(
513         uint256 _instantRedemptionLimit
514       ) external override onlyRole(CONFIGURER_ROLE) {
515         _setInstantRedemptionLimit(_instantRedemptionLimit);
516       }


526       function setInstantMintLimitDuration(
527         uint256 _instantMintLimitDuration
528       ) external override onlyRole(CONFIGURER_ROLE) {
529         _setInstantMintLimitDuration(_instantMintLimitDuration);
530       }


540       function setInstantRedemptionLimitDuration(
541         uint256 _instantRedemptionLimitDuratioin
542       ) external override onlyRole(CONFIGURER_ROLE) {
543         _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
544       }


554       function setMintFee(
555         uint256 _mintFee
556       ) external override onlyRole(CONFIGURER_ROLE) {
557         require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558         emit MintFeeSet(mintFee, _mintFee);
559         mintFee = _mintFee;
560       }


567       function setRedeemFee(
568         uint256 _redeemFee
569       ) external override onlyRole(CONFIGURER_ROLE) {
570         require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571         emit RedeemFeeSet(redeemFee, _redeemFee);
572         redeemFee = _redeemFee;
573       }


581       function setMinimumDepositAmount(
582         uint256 _minimumDepositAmount
583       ) external override onlyRole(CONFIGURER_ROLE) {
584         require(
585           _minimumDepositAmount >= FEE_GRANULARITY,
586           "setMinimumDepositAmount: Amount too small"
587         );
588     
589         emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
590         minimumDepositAmount = _minimumDepositAmount;
591       }


599       function setMinimumRedemptionAmount(
600         uint256 _minimumRedemptionAmount
601       ) external override onlyRole(CONFIGURER_ROLE) {
602         require(
603           _minimumRedemptionAmount >= FEE_GRANULARITY,
604           "setMinimumRedemptionAmount: Amount too small"
605         );
606         emit MinimumRedemptionAmountSet(
607           minimumRedemptionAmount,
608           _minimumRedemptionAmount
609         );
610         minimumRedemptionAmount = _minimumRedemptionAmount;
611       }


622       function setMinimumBUIDLRedemptionAmount(
623         uint256 _minimumBUIDLRedemptionAmount
624       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
625         emit MinimumBUIDLRedemptionAmountSet(
626           minBUIDLRedeemAmount,
627           _minimumBUIDLRedemptionAmount
628         );
629         minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
630       }


638       function setOracle(
639         address _oracle
640       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
641         emit OracleSet(address(oracle), _oracle);
642         oracle = IRWAOracle(_oracle);
643       }


650       function setFeeReceiver(
651         address _feeReceiver
652       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
653         require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
654         emit FeeReceiverSet(feeReceiver, _feeReceiver);
655         feeReceiver = _feeReceiver;
656       }


663       function setInvestorBasedRateLimiter(
664         address _investorBasedRateLimiter
665       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
666         emit InvestorBasedRateLimiterSet(
667           address(investorBasedRateLimiter),
668           _investorBasedRateLimiter
669         );
670         investorBasedRateLimiter = IInvestorBasedRateLimiter(
671           _investorBasedRateLimiter
672         );
673       }


768       function pauseMint() external onlyRole(PAUSER_ROLE) {
769         mintPaused = true;
770         emit MintPaused();
771       }


774       function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {
775         mintPaused = false;
776         emit MintUnpaused();
777       }


780       function pauseRedeem() external onlyRole(PAUSER_ROLE) {
781         redeemPaused = true;
782         emit RedeemPaused();
783       }


786       function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {
787         redeemPaused = false;
788         emit RedeemUnpaused();
789       }


794       function multiexcall(
795         ExCallData[] calldata exCallData
796       )
797         external
798         payable
799         override
800         onlyRole(DEFAULT_ADMIN_ROLE)
801         returns (bytes[] memory results)
802       {
803         results = new bytes[](exCallData.length);
804         for (uint256 i = 0; i < exCallData.length; ++i) {
805           (bool success, bytes memory ret) = address(exCallData[i].target).call{
806             value: exCallData[i].value
807           }(exCallData[i].data);
808           require(success, "Call Failed");
809           results[i] = ret;
810         }
811       }


819       function retrieveTokens(
820         address token,
821         address to,
822         uint256 amount
823       ) external onlyRole(DEFAULT_ADMIN_ROLE) {
824         IERC20(token).transfer(to, amount);
825       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819:825

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


70        function deployRebasingOUSG(
71          address kycRegistry,
72          uint256 requirementGroup,
73          address ousg,
74          address oracle
75        ) external onlyGuardian returns (address, address, address) {
76          require(!initialized, "ROUSGFactory: rOUSG already deployed");
77          rOUSGImplementation = new ROUSG();
78          rOUSGProxyAdmin = new ProxyAdmin();
79          rOUSGProxy = new TokenProxy(
80            address(rOUSGImplementation),
81            address(rOUSGProxyAdmin),
82            ""
83          );
84          ROUSG rOUSGProxied = ROUSG(address(rOUSGProxy));
85          rOUSGProxied.initialize(
86            kycRegistry,
87            requirementGroup,
88            ousg,
89            guardian,
90            oracle
91          );
92      
93          rOUSGProxyAdmin.transferOwnership(guardian);
94          assert(rOUSGProxyAdmin.owner() == guardian);
95          initialized = true;
96          emit rOUSGDeployed(
97            address(rOUSGProxy),
98            address(rOUSGProxyAdmin),
99            address(rOUSGImplementation),
100           rOUSGProxied.name(),
101           rOUSGProxied.symbol()
102         );
103         return (
104           address(rOUSGProxy),
105           address(rOUSGProxyAdmin),
106           address(rOUSGImplementation)
107         );
108       }


121       function multiexcall(
122         ExCallData[] calldata exCallData
123       ) external payable override onlyGuardian returns (bytes[] memory results) {
124         results = new bytes[](exCallData.length);
125         for (uint256 i = 0; i < exCallData.length; ++i) {
126           (bool success, bytes memory ret) = address(exCallData[i].target).call{
127             value: exCallData[i].value
128           }(exCallData[i].data);
129           require(success, "Call Failed");
130           results[i] = ret;
131         }
132       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121:132

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


102       function initialize(
103         address _kycRegistry,
104         uint256 requirementGroup,
105         address _ousg,
106         address guardian,
107         address _oracle
108       ) public virtual initializer {
109         __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
110       }


166       function name() public pure returns (string memory) {
167         return "Rebasing OUSG";
168       }


174       function symbol() public pure returns (string memory) {
175         return "rOUSG";
176       }


181       function decimals() public pure returns (uint8) {
182         return 18;
183       }


188       function totalSupply() public view returns (uint256) {
189         return
190           (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
191       }


199       function balanceOf(address _account) public view returns (uint256) {
200         return
201           (_sharesOf(_account) * getOUSGPrice()) /
202           (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
203       }


220       function transfer(address _recipient, uint256 _amount) public returns (bool) {
221         _transfer(msg.sender, _recipient, _amount);
222         return true;
223       }


231       function allowance(
232         address _owner,
233         address _spender
234       ) public view returns (uint256) {
235         return allowances[_owner][_spender];
236       }


251       function approve(address _spender, uint256 _amount) public returns (bool) {
252         _approve(msg.sender, _spender, _amount);
253         return true;
254       }


276       function transferFrom(
277         address _sender,
278         address _recipient,
279         uint256 _amount
280       ) public returns (bool) {
281         uint256 currentAllowance = allowances[_sender][msg.sender];
282         require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");
283     
284         _transfer(_sender, _recipient, _amount);
285         _approve(_sender, msg.sender, currentAllowance - _amount);
286         return true;
287       }


302       function increaseAllowance(
303         address _spender,
304         uint256 _addedValue
305       ) public returns (bool) {
306         _approve(
307           msg.sender,
308           _spender,
309           allowances[msg.sender][_spender] + _addedValue
310         );
311         return true;
312       }


328       function decreaseAllowance(
329         address _spender,
330         uint256 _subtractedValue
331       ) public returns (bool) {
332         uint256 currentAllowance = allowances[msg.sender][_spender];
333         require(
334           currentAllowance >= _subtractedValue,
335           "DECREASED_ALLOWANCE_BELOW_ZERO"
336         );
337         _approve(msg.sender, _spender, currentAllowance - _subtractedValue);
338         return true;
339       }


347       function getTotalShares() public view returns (uint256) {
348         return totalShares;
349       }


356       function sharesOf(address _account) public view returns (uint256) {
357         return _sharesOf(_account);
358       }


363       function getSharesByROUSG(
364         uint256 _rOUSGAmount
365       ) public view returns (uint256) {
366         return
367           (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
368       }


373       function getROUSGByShares(uint256 _shares) public view returns (uint256) {
374         return
375           (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
376       }


378       function getOUSGPrice() public view returns (uint256 price) {
379         (price, ) = oracle.getPriceData();
380       }


397       function transferShares(
398         address _recipient,
399         uint256 _sharesAmount
400       ) public returns (uint256) {
401         _transferShares(msg.sender, _recipient, _sharesAmount);
402         emit TransferShares(msg.sender, _recipient, _sharesAmount);
403         uint256 tokensAmount = getROUSGByShares(_sharesAmount);
404         emit Transfer(msg.sender, _recipient, tokensAmount);
405         return tokensAmount;
406       }


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {
416         require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");
417         uint256 ousgSharesAmount = _OUSGAmount * OUSG_TO_ROUSG_SHARES_MULTIPLIER;
418         _mintShares(msg.sender, ousgSharesAmount);
419         ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
420         emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
421         emit TransferShares(address(0), msg.sender, ousgSharesAmount);
422       }


431       function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
432         require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");
433         uint256 ousgSharesAmount = getSharesByROUSG(_rOUSGAmount);
434         if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
435           revert UnwrapTooSmall();
436         _burnShares(msg.sender, ousgSharesAmount);
437         ousg.transfer(
438           msg.sender,
439           ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
440         );
441         emit Transfer(msg.sender, address(0), _rOUSGAmount);
442         emit TransferShares(msg.sender, address(0), ousgSharesAmount);
443       }


613       function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
614         emit OracleSet(address(oracle), _oracle);
615         oracle = IRWAOracle(_oracle);
616       }


624       function burn(
625         address _account,
626         uint256 _amount
627       ) external onlyRole(BURNER_ROLE) {
628         uint256 ousgSharesAmount = getSharesByROUSG(_amount);
629         if (ousgSharesAmount < OUSG_TO_ROUSG_SHARES_MULTIPLIER)
630           revert UnwrapTooSmall();
631     
632         _burnShares(_account, ousgSharesAmount);
633     
634         ousg.transfer(
635           msg.sender,
636           ousgSharesAmount / OUSG_TO_ROUSG_SHARES_MULTIPLIER
637         );
638         emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
639         emit TransferShares(_account, address(0), ousgSharesAmount);
640       }


642       function pause() external onlyRole(PAUSER_ROLE) {
643         _pause();
644       }


646       function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
647         _unpause();
648       }


650       function setKYCRegistry(
651         address registry
652       ) external override onlyRole(CONFIGURER_ROLE) {
653         _setKYCRegistry(registry);
654       }


656       function setKYCRequirementGroup(
657         uint256 group
658       ) external override onlyRole(CONFIGURER_ROLE) {
659         _setKYCRequirementGroup(group);
660       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:660

</details>

## NC041 - Consider adding formal verification proofs:

Consider using formal verification to mathematically prove that your code does what is intended, and does not have any edge cases with unexpected behavior. The solidity compiler itself has this functionality [built in based off of SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html#smtchecker-and-formal-verification).


```solidity
File: Various Files


None

```

## NC042 - Large multiples of ten should use scientific notation (e.g. 1e6) rather than decimal literals (e.g. 1000000), for readability:

Using scientific notation for large multiples of ten improves code readability. Instead of writing large decimal literals, consider using scientific notation.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


69        uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


66        uint256 public constant FEE_GRANULARITY = 10_000;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L66:66

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


87        uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L87:87

## NC043 - Event names should use CamelCase:

According to the Solidity [style guide](https://docs.soliditylang.org/en/latest/style-guide.html#event-names) event names should be in `CamelCase`.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


141       event rOUSGDeployed(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141:141

## NC044 - Error messages should descriptive, rather that cryptic:




<details>
<summary>Click to show 10 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


282         require(currentAllowance >= _amount, "TRANSFER_AMOUNT_EXCEEDS_ALLOWANCE");


333         require(


477         require(_owner != address(0), "APPROVE_FROM_ZERO_ADDRESS");


478         require(_spender != address(0), "APPROVE_TO_ZERO_ADDRESS");


506         require(_sender != address(0), "TRANSFER_FROM_THE_ZERO_ADDRESS");


507         require(_recipient != address(0), "TRANSFER_TO_THE_ZERO_ADDRESS");


512         require(


533         require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");


558         require(_account != address(0), "BURN_FROM_THE_ZERO_ADDRESS");


563         require(_sharesAmount <= accountShares, "BURN_AMOUNT_EXCEEDS_BALANCE");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L563:563

</details>

## NC045 - Missing timelock for critical parameter change:

Timelocks prevent users from being surprised by changes.


<details>
<summary>Click to show 9 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


559         mintFee = _mintFee;


572         redeemFee = _redeemFee;


590         minimumDepositAmount = _minimumDepositAmount;


610         minimumRedemptionAmount = _minimumRedemptionAmount;


629         minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;


642         oracle = IRWAOracle(_oracle);


655         feeReceiver = _feeReceiver;


670         investorBasedRateLimiter = IInvestorBasedRateLimiter(
671           _investorBasedRateLimiter
672         );


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L670:672

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


615         oracle = IRWAOracle(_oracle);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L615:615

</details>

## NC046 - Setters should prevent re-setting of the same value:

This especially problematic when the setter also emits the same value, which may be confusing to offline parsers.


<details>
<summary>Click to show 15 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


498       function setInstantMintLimit(
499         uint256 _instantMintLimit
500       ) external override onlyRole(CONFIGURER_ROLE) {
501         _setInstantMintLimit(_instantMintLimit);
502       }


512       function setInstantRedemptionLimit(
513         uint256 _instantRedemptionLimit
514       ) external override onlyRole(CONFIGURER_ROLE) {
515         _setInstantRedemptionLimit(_instantRedemptionLimit);
516       }


526       function setInstantMintLimitDuration(
527         uint256 _instantMintLimitDuration
528       ) external override onlyRole(CONFIGURER_ROLE) {
529         _setInstantMintLimitDuration(_instantMintLimitDuration);
530       }


540       function setInstantRedemptionLimitDuration(
541         uint256 _instantRedemptionLimitDuratioin
542       ) external override onlyRole(CONFIGURER_ROLE) {
543         _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
544       }


554       function setMintFee(
555         uint256 _mintFee
556       ) external override onlyRole(CONFIGURER_ROLE) {
557         require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558         emit MintFeeSet(mintFee, _mintFee);
559         mintFee = _mintFee;
560       }


567       function setRedeemFee(
568         uint256 _redeemFee
569       ) external override onlyRole(CONFIGURER_ROLE) {
570         require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571         emit RedeemFeeSet(redeemFee, _redeemFee);
572         redeemFee = _redeemFee;
573       }


581       function setMinimumDepositAmount(
582         uint256 _minimumDepositAmount
583       ) external override onlyRole(CONFIGURER_ROLE) {
584         require(
585           _minimumDepositAmount >= FEE_GRANULARITY,
586           "setMinimumDepositAmount: Amount too small"
587         );
588     
589         emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
590         minimumDepositAmount = _minimumDepositAmount;
591       }


599       function setMinimumRedemptionAmount(
600         uint256 _minimumRedemptionAmount
601       ) external override onlyRole(CONFIGURER_ROLE) {
602         require(
603           _minimumRedemptionAmount >= FEE_GRANULARITY,
604           "setMinimumRedemptionAmount: Amount too small"
605         );
606         emit MinimumRedemptionAmountSet(
607           minimumRedemptionAmount,
608           _minimumRedemptionAmount
609         );
610         minimumRedemptionAmount = _minimumRedemptionAmount;
611       }


622       function setMinimumBUIDLRedemptionAmount(
623         uint256 _minimumBUIDLRedemptionAmount
624       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
625         emit MinimumBUIDLRedemptionAmountSet(
626           minBUIDLRedeemAmount,
627           _minimumBUIDLRedemptionAmount
628         );
629         minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
630       }


638       function setOracle(
639         address _oracle
640       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
641         emit OracleSet(address(oracle), _oracle);
642         oracle = IRWAOracle(_oracle);
643       }


650       function setFeeReceiver(
651         address _feeReceiver
652       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
653         require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
654         emit FeeReceiverSet(feeReceiver, _feeReceiver);
655         feeReceiver = _feeReceiver;
656       }


663       function setInvestorBasedRateLimiter(
664         address _investorBasedRateLimiter
665       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
666         emit InvestorBasedRateLimiterSet(
667           address(investorBasedRateLimiter),
668           _investorBasedRateLimiter
669         );
670         investorBasedRateLimiter = IInvestorBasedRateLimiter(
671           _investorBasedRateLimiter
672         );
673       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663:673

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


613       function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
614         emit OracleSet(address(oracle), _oracle);
615         oracle = IRWAOracle(_oracle);
616       }


650       function setKYCRegistry(
651         address registry
652       ) external override onlyRole(CONFIGURER_ROLE) {
653         _setKYCRegistry(registry);
654       }


656       function setKYCRequirementGroup(
657         uint256 group
658       ) external override onlyRole(CONFIGURER_ROLE) {
659         _setKYCRequirementGroup(group);
660       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:660

</details>

## NC047 - Use of override is unnecessary:

Starting with Solidity version 0.8.8, using the override keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.


<details>
<summary>Click to show 20 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


  function mint(
    uint256 usdcAmountIn
  )
    external
    override
    nonReentrant
    whenMintNotPaused
    returns (uint256 ousgAmountOut)
  {
    ousgAmountOut = _mint(usdcAmountIn, msg.sender);
    emit InstantMintOUSG(msg.sender, usdcAmountIn, ousgAmountOut);
  }

  function mintRebasingOUSG(
    uint256 usdcAmountIn
  )
    external
    override
    nonReentrant
    whenMintNotPaused
    returns (uint256 rousgAmountOut)
  {
    uint256 ousgAmountOut = _mint(usdcAmountIn, address(this));
    ousg.approve(address(rousg), ousgAmountOut);
    rousg.wrap(ousgAmountOut);
    rousgAmountOut = rousg.getROUSGByShares(
      ousgAmountOut * OUSG_TO_ROUSG_SHARES_MULTIPLIER
    );
    rousg.transfer(msg.sender, rousgAmountOut);
    emit InstantMintRebasingOUSG(
      msg.sender,
      usdcAmountIn,
      ousgAmountOut,
      rousgAmountOut
    );
  }

  function redeem(
    uint256 ousgAmountIn
  )
    external
    override
    nonReentrant
    whenRedeemNotPaused
    returns (uint256 usdcAmountOut)
  {
    require(
      ousg.allowance(msg.sender, address(this)) >= ousgAmountIn,
      "OUSGInstantManager::redeem: Insufficient allowance"
    );
    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
    usdcAmountOut = _redeem(ousgAmountIn);
    emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut);
  }

  function redeemRebasingOUSG(
    uint256 rousgAmountIn
  )
    external
    override
    nonReentrant
    whenRedeemNotPaused
    returns (uint256 usdcAmountOut)
  {
    require(
      rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
      "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
    );
    rousg.transferFrom(msg.sender, address(this), rousgAmountIn);
    rousg.unwrap(rousgAmountIn);
    uint256 ousgAmountIn = rousg.getSharesByROUSG(rousgAmountIn) /
      OUSG_TO_ROUSG_SHARES_MULTIPLIER;
    usdcAmountOut = _redeem(ousgAmountIn);
    emit InstantRedemptionRebasingOUSG(
      msg.sender,
      rousgAmountIn,
      ousgAmountIn,
      usdcAmountOut
    );
  }

  function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setInstantMintLimit(_instantMintLimit);
  }

  function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setInstantRedemptionLimit(_instantRedemptionLimit);
  }

  function setInstantMintLimitDuration(
    uint256 _instantMintLimitDuration
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setInstantMintLimitDuration(_instantMintLimitDuration);
  }

  function setInstantRedemptionLimitDuration(
    uint256 _instantRedemptionLimitDuratioin
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
  }

  function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
    emit MintFeeSet(mintFee, _mintFee);
    mintFee = _mintFee;
  }

  function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
    emit RedeemFeeSet(redeemFee, _redeemFee);
    redeemFee = _redeemFee;
  }

  function setMinimumDepositAmount(
    uint256 _minimumDepositAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(
      _minimumDepositAmount >= FEE_GRANULARITY,
      "setMinimumDepositAmount: Amount too small"
    );

    emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
    minimumDepositAmount = _minimumDepositAmount;
  }

  function setMinimumRedemptionAmount(
    uint256 _minimumRedemptionAmount
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(
      _minimumRedemptionAmount >= FEE_GRANULARITY,
      "setMinimumRedemptionAmount: Amount too small"
    );
    emit MinimumRedemptionAmountSet(
      minimumRedemptionAmount,
      _minimumRedemptionAmount
    );
    minimumRedemptionAmount = _minimumRedemptionAmount;
  }

  function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit MinimumBUIDLRedemptionAmountSet(
      minBUIDLRedeemAmount,
      _minimumBUIDLRedemptionAmount
    );
    minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
  }

  function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }

  function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
    emit FeeReceiverSet(feeReceiver, _feeReceiver);
    feeReceiver = _feeReceiver;
  }

  function setInvestorBasedRateLimiter(
    address _investorBasedRateLimiter
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit InvestorBasedRateLimiterSet(
      address(investorBasedRateLimiter),
      _investorBasedRateLimiter
    );
    investorBasedRateLimiter = IInvestorBasedRateLimiter(
      _investorBasedRateLimiter
    );
  }

  function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794:811

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


  function multiexcall(
    ExCallData[] calldata exCallData
  ) external payable override onlyGuardian returns (bytes[] memory results) {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121:132

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


  function setKYCRegistry(
    address registry
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setKYCRegistry(registry);
  }

  function setKYCRequirementGroup(
    uint256 group
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setKYCRequirementGroup(group);
  }

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:660

</details>

## NC048 - Put all system-wide constants in one file:

Putting all the system-wide constants in a single file improves code readability, makes it easier to understand the basic configuration and limitations of the system, and makes maintenance easier.


<details>
<summary>Click to show 10 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


57        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


60        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


63        uint256 public constant MINIMUM_OUSG_PRICE = 105e18;


66        uint256 public constant FEE_GRANULARITY = 10_000;


69        uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L69:69

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


38        bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L38:38

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


87        uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


93        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


94        bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");


95        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95:95

</details>

## NC049 - Add inline comments for unnamed variables:

`function foo(address x, address)` -> `function foo(address x, address /* y */)`


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


586       function _beforeTokenTransfer(
587         address from,
588         address to,
589         uint256
590       ) internal view {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L586:590

## NC050 - Named imports of parent contracts are missing:




<details>
<summary>Click to show 13 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


52        AccessControlEnumerable,


54        IMulticall


50        ReentrancyGuard,


51        InstantMintTimeBasedRateLimiter,


53        IOUSGInstantManager,


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L53:53

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


37      contract ROUSGFactory is IMulticall {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37:37

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


62        IERC20MetadataUpgradeable


61        IERC20Upgradeable,


58        PausableUpgradeable,


57        ContextUpgradeable,


59        AccessControlEnumerableUpgradeable,


56        Initializable,


60        KYCRegistryClientUpgradeable,


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L60:60

</details>

## NC051 - Style guide: State and local variables should be named using lowerCamelCase:

The Solidity style guide says to use mixedCase for local and state variable names. Note that while OpenZeppelin may not follow this advice, it still is the recommended way of naming variables.


<details>
<summary>Click to show 15 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415:415

</details>

## NC052 - Unnecessary cast:

The variable is being cast to its own type


<details>
<summary>Click to show 5 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


164           address(_usdc) != address(0),


168           address(_usdcReciever) != address(0),


172           address(_feeReceiver) != address(0),


176           address(_ousgOracle) != address(0),


183           address(_buidlRedeemer) != address(0),


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L183:183

</details>

## NC053 - Use the latest solidity (prior to 0.8.20 if on L2s) for deployment:

Since deployed contracts should not use floating pragmas, I've flagged all instances where a version prior to 0.8.19 is allowed by the version pragma


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


16      pragma solidity 0.8.16;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L16:16

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


16      pragma solidity 0.8.16;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L16:16

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


16      pragma solidity 0.8.16;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L16:16

## NC054 - Events should use parameters to convey information:

For example, rather than using event Paused() and event Unpaused(), use event PauseState(address indexed whoChangedIt, bool wasPaused, bool isNowPaused)


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


770         emit MintPaused();


776         emit MintUnpaused();


782         emit RedeemPaused();


788         emit RedeemUnpaused();


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L788:788

</details>

## NC055 - Event declarations should have NatSpec @param annotations:

Documents a parameter just like in Doxygen (must be followed by parameter name)


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


149       event TransferShares(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L149:149

## NC056 - Event declarations should have NatSpec @dev annotations:

Explain to a developer any extra details


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


161       event OracleSet(address indexed oldOracle, address indexed newOracle);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L161:161

## NC057 - Function definitions should have NatSpec @dev annotations:

Explain to a developer any extra details


<details>
<summary>Click to show 48 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


278       function _mint(


388       function _redeem(


458       function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {


498       function setInstantMintLimit(


512       function setInstantRedemptionLimit(


526       function setInstantMintLimitDuration(


540       function setInstantRedemptionLimitDuration(


554       function setMintFee(


567       function setRedeemFee(


581       function setMinimumDepositAmount(


599       function setMinimumRedemptionAmount(


622       function setMinimumBUIDLRedemptionAmount(


638       function setOracle(


650       function setFeeReceiver(


663       function setInvestorBasedRateLimiter(


685       function _getMintAmount(


699       function _getRedemptionAmount(


713       function _getInstantMintFees(


725       function _getInstantRedemptionFees(


768       function pauseMint() external onlyRole(PAUSER_ROLE) {


774       function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {


780       function pauseRedeem() external onlyRole(PAUSER_ROLE) {


786       function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {


794       function multiexcall(


819       function retrieveTokens(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819:819

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


47        constructor(address _guardian) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47:47

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


98        constructor() {


102       function initialize(


112       function __rOUSG_init(


128       function __rOUSG_init_unchained(


166       function name() public pure returns (string memory) {


174       function symbol() public pure returns (string memory) {


181       function decimals() public pure returns (uint8) {


188       function totalSupply() public view returns (uint256) {


302       function increaseAllowance(


328       function decreaseAllowance(


363       function getSharesByROUSG(


373       function getROUSGByShares(uint256 _shares) public view returns (uint256) {


378       function getOUSGPrice() public view returns (uint256 price) {


450       function _transfer(


472       function _approve(


487       function _sharesOf(address _account) internal view returns (uint256) {


501       function _transferShares(


529       function _mintShares(


642       function pause() external onlyRole(PAUSER_ROLE) {


646       function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {


650       function setKYCRegistry(


656       function setKYCRequirementGroup(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:656

</details>

## NC058 - Function definitions should have NatSpec @notice annotations:

Explain to an end user what this does


<details>
<summary>Click to show 27 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


278       function _mint(


388       function _redeem(


458       function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {


650       function setFeeReceiver(


794       function multiexcall(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794:794

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


47        constructor(address _guardian) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47:47

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


98        constructor() {


102       function initialize(


112       function __rOUSG_init(


128       function __rOUSG_init_unchained(


166       function name() public pure returns (string memory) {


174       function symbol() public pure returns (string memory) {


181       function decimals() public pure returns (uint8) {


188       function totalSupply() public view returns (uint256) {


199       function balanceOf(address _account) public view returns (uint256) {


231       function allowance(


347       function getTotalShares() public view returns (uint256) {


356       function sharesOf(address _account) public view returns (uint256) {


363       function getSharesByROUSG(


373       function getROUSGByShares(uint256 _shares) public view returns (uint256) {


378       function getOUSGPrice() public view returns (uint256 price) {


487       function _sharesOf(address _account) internal view returns (uint256) {


586       function _beforeTokenTransfer(


642       function pause() external onlyRole(PAUSER_ROLE) {


646       function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {


650       function setKYCRegistry(


656       function setKYCRequirementGroup(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:656

</details>

## NC059 - Modifier definitions should have Natspec @notice annotations:

Explain to an end user what this does


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


149       modifier onlyGuardian() {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149:149

## NC060 - Modifier definitions should have Natspec @dev annotations:

Explain to a developer any extra details


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


756       modifier whenMintNotPaused() {


762       modifier whenRedeemNotPaused() {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L762:762

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


149       modifier onlyGuardian() {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149:149

## NC061 - Contract definitions should have Natspec @title annotations:

 title that should describe the contract


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55

## NC062 - Contract definitions should have Natspec @author annotations:

The name of the author


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55

## NC063 - Contract definitions should have Natspec @notice annotations:

Explain to an end user what this does


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55

## NC064 - Contract definitions should have Natspec @dev annotations:

Explain to a developer any extra details


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


37      contract ROUSGFactory is IMulticall {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37:37

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:55

## NC065 - Event definitions should have Natspec @notice annotations:

Explain to an end user what this does


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


141       event rOUSGDeployed(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141:141

## NC066 - State variable declarations should have Natspec @notice annotations:

Explain to an end user what this does


<details>
<summary>Click to show 37 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


57        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


60        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


63        uint256 public constant MINIMUM_OUSG_PRICE = 105e18;


66        uint256 public constant FEE_GRANULARITY = 10_000;


69        uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


72        IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;


75        IRWALike public immutable ousg;


78        ROUSG public immutable rousg;


81        IERC20 public immutable buidl;


84        IBUIDLRedeemer public immutable buidlRedeemer;


87        uint256 public immutable decimalsMultiplier;


90        address public immutable usdcReceiver;


93        IRWAOracle public oracle;


96        address public feeReceiver;


99        uint256 public mintFee = 0;


102       uint256 public redeemFee = 0;


106       uint256 public minimumDepositAmount = 100_000e6;


110       uint256 public minimumRedemptionAmount = 50_000e6;


113       bool public mintPaused;


116       bool public redeemPaused;


120       uint256 public minBUIDLRedeemAmount = 250_000e6;


123       IInvestorBasedRateLimiter public investorBasedRateLimiter;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L123:123

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


38        bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);


40        address internal immutable guardian;


41        ROUSG public rOUSGImplementation;


42        ProxyAdmin public rOUSGProxyAdmin;


43        TokenProxy public rOUSGProxy;


45        bool public initialized = false;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45:45

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


72        mapping(address => uint256) private shares;


75        mapping(address => mapping(address => uint256)) private allowances;


78        uint256 private totalShares;


81        IRWAOracle public oracle;


84        IERC20 public ousg;


87        uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


93        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


94        bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");


95        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95:95

</details>

## NC067 - State variable declarations should have Natspec @dev annotations:

Explain to a developer any extra details


<details>
<summary>Click to show 34 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


57        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


60        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


63        uint256 public constant MINIMUM_OUSG_PRICE = 105e18;


66        uint256 public constant FEE_GRANULARITY = 10_000;


69        uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


72        IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;


75        IRWALike public immutable ousg;


78        ROUSG public immutable rousg;


81        IERC20 public immutable buidl;


84        IBUIDLRedeemer public immutable buidlRedeemer;


87        uint256 public immutable decimalsMultiplier;


90        address public immutable usdcReceiver;


93        IRWAOracle public oracle;


96        address public feeReceiver;


99        uint256 public mintFee = 0;


102       uint256 public redeemFee = 0;


106       uint256 public minimumDepositAmount = 100_000e6;


110       uint256 public minimumRedemptionAmount = 50_000e6;


113       bool public mintPaused;


116       bool public redeemPaused;


120       uint256 public minBUIDLRedeemAmount = 250_000e6;


123       IInvestorBasedRateLimiter public investorBasedRateLimiter;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L123:123

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


38        bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);


40        address internal immutable guardian;


41        ROUSG public rOUSGImplementation;


42        ProxyAdmin public rOUSGProxyAdmin;


43        TokenProxy public rOUSGProxy;


45        bool public initialized = false;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L45:45

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


78        uint256 private totalShares;


81        IRWAOracle public oracle;


84        IERC20 public ousg;


87        uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;


94        bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");


95        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95:95

</details>

## NC068 - Functions should have Natspec @return annotations:

Documents the return variables of a contract’s function


<details>
<summary>Click to show 15 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


278       function _mint(


388       function _redeem(


685       function _getMintAmount(


699       function _getRedemptionAmount(


713       function _getInstantMintFees(


725       function _getInstantRedemptionFees(


737       function _scaleUp(uint256 amount) internal view returns (uint256) {


747       function _scaleDown(uint256 amount) internal view returns (uint256) {


794       function multiexcall(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794:794

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


121       function multiexcall(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121:121

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


302       function increaseAllowance(


328       function decreaseAllowance(


378       function getOUSGPrice() public view returns (uint256 price) {


529       function _mintShares(


554       function _burnShares(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554:554

</details>

## NC069 - Functions should have Natspec @param annotations:

Documents a parameter just like in Doxygen (must be followed by parameter name)


<details>
<summary>Click to show 44 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


278       function _mint(


388       function _redeem(


458       function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {


479       function getOUSGPrice() public view returns (uint256 price) {


737       function _scaleUp(uint256 amount) internal view returns (uint256) {


747       function _scaleDown(uint256 amount) internal view returns (uint256) {


768       function pauseMint() external onlyRole(PAUSER_ROLE) {


774       function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {


780       function pauseRedeem() external onlyRole(PAUSER_ROLE) {


786       function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {


794       function multiexcall(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794:794

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/939692fb-46d1-4491-ba0c-0dafad6fc3ac.sol


47        constructor(address _guardian) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47:47

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


98        constructor() {


102       function initialize(


112       function __rOUSG_init(


128       function __rOUSG_init_unchained(


166       function name() public pure returns (string memory) {


174       function symbol() public pure returns (string memory) {


181       function decimals() public pure returns (uint8) {


188       function totalSupply() public view returns (uint256) {


199       function balanceOf(address _account) public view returns (uint256) {


220       function transfer(address _recipient, uint256 _amount) public returns (bool) {


231       function allowance(


251       function approve(address _spender, uint256 _amount) public returns (bool) {


276       function transferFrom(


302       function increaseAllowance(


328       function decreaseAllowance(


347       function getTotalShares() public view returns (uint256) {


356       function sharesOf(address _account) public view returns (uint256) {


363       function getSharesByROUSG(


373       function getROUSGByShares(uint256 _shares) public view returns (uint256) {


378       function getOUSGPrice() public view returns (uint256 price) {


397       function transferShares(


450       function _transfer(


472       function _approve(


487       function _sharesOf(address _account) internal view returns (uint256) {


501       function _transferShares(


529       function _mintShares(


554       function _burnShares(


586       function _beforeTokenTransfer(


642       function pause() external onlyRole(PAUSER_ROLE) {


646       function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {


650       function setKYCRegistry(


656       function setKYCRequirementGroup(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:656

</details>

## NC070 - Missing events in sensitive functions:

Sensitive setter functions in smart contracts often alter critical state variables. Without events emitted in these functions, external observers or dApps cannot easily track or react to these state changes. Missing events can obscure contract activity, hampering transparency and making integration more challenging. To resolve this, incorporate appropriate event emissions within these functions. Events offer an efficient way to log crucial changes, aiding in real-time tracking and post-transaction verification..


<details>
<summary>Click to show 6 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


498       function setInstantMintLimit(
499         uint256 _instantMintLimit
500       ) external override onlyRole(CONFIGURER_ROLE) {
501         _setInstantMintLimit(_instantMintLimit);
502       }


512       function setInstantRedemptionLimit(
513         uint256 _instantRedemptionLimit
514       ) external override onlyRole(CONFIGURER_ROLE) {
515         _setInstantRedemptionLimit(_instantRedemptionLimit);
516       }


526       function setInstantMintLimitDuration(
527         uint256 _instantMintLimitDuration
528       ) external override onlyRole(CONFIGURER_ROLE) {
529         _setInstantMintLimitDuration(_instantMintLimitDuration);
530       }


540       function setInstantRedemptionLimitDuration(
541         uint256 _instantRedemptionLimitDuratioin
542       ) external override onlyRole(CONFIGURER_ROLE) {
543         _setInstantRedemptionLimitDuration(_instantRedemptionLimitDuratioin);
544       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540:544

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


650       function setKYCRegistry(
651         address registry
652       ) external override onlyRole(CONFIGURER_ROLE) {
653         _setKYCRegistry(registry);
654       }


656       function setKYCRequirementGroup(
657         uint256 group
658       ) external override onlyRole(CONFIGURER_ROLE) {
659         _setKYCRequirementGroup(group);
660       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656:660

</details>

## NC071 - A event should be emitted if a non immutable state variable is set in a constructor:




```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


144       constructor(
145         address defaultAdmin,
146         address _usdc,
147         address _usdcReciever,
148         address _feeReceiver,
149         address _ousgOracle,
150         address _ousg,
151         address _rousg,
152         address _buidl,
153         address _buidlRedeemer,
154         RateLimiterConfig memory rateLimiterConfig
155       )
156         InstantMintTimeBasedRateLimiter(
157           rateLimiterConfig.mintLimitDuration,
158           rateLimiterConfig.redeemLimitDuration,
159           rateLimiterConfig.mintLimit,
160           rateLimiterConfig.redeemLimit
161         )
162       {
163         require(
164           address(_usdc) != address(0),
165           "OUSGInstantManager: USDC cannot be 0x0"
166         );
167         require(
168           address(_usdcReciever) != address(0),
169           "OUSGInstantManager: USDC Receiver cannot be 0x0"
170         );
171         require(
172           address(_feeReceiver) != address(0),
173           "OUSGInstantManager: feeReceiver cannot be 0x0"
174         );
175         require(
176           address(_ousgOracle) != address(0),
177           "OUSGInstantManager: OUSG Oracle cannot be 0x0"
178         );
179         require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180         require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181         require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
182         require(
183           address(_buidlRedeemer) != address(0),
184           "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
185         );
186         require(
187           IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
188           "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
189         );
190         require(
191           IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
192           "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
193         );
194         usdc = IERC20(_usdc);
195         usdcReceiver = _usdcReciever;
196         feeReceiver = _feeReceiver;
197         oracle = IRWAOracle(_ousgOracle);
198         ousg = IRWALike(_ousg);
199         rousg = ROUSG(_rousg);
200         buidl = IERC20(_buidl);
201         buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
202         decimalsMultiplier =
203           10 **
204             (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());
205         require(
206           OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
207             rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
208           "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
209         );
210     
211         _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
212         _grantRole(CONFIGURER_ROLE, defaultAdmin);
213         _grantRole(PAUSER_ROLE, defaultAdmin);
214       }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144:214

## NC072 - It is best practice to use linear inheritance:

In Solidity, complex inheritance structures can obfuscate code understanding, introducing potential security risks. Multiple inheritance, especially with overlapping function names or state variables, can cause unintentional overrides or ambiguous behavior. Resolution: Strive for linear and simple inheritance chains. Avoid diamond or circular inheritance patterns. Clearly document the purpose and relationships of base contracts, ensuring that overrides are intentional. Tools like Remix or Hardhat can visualize inheritance chains, assisting in verification. Keeping inheritance streamlined aids in better code readability, reduces potential errors, and ensures smoother audits and upgrades.


```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


49      contract OUSGInstantManager is
50        ReentrancyGuard,
51        InstantMintTimeBasedRateLimiter,
52        AccessControlEnumerable,
53        IOUSGInstantManager,
54        IMulticall


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49:54

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


55      contract ROUSG is
56        Initializable,
57        ContextUpgradeable,
58        PausableUpgradeable,
59        AccessControlEnumerableUpgradeable,
60        KYCRegistryClientUpgradeable,
61        IERC20Upgradeable,
62        IERC20MetadataUpgradeable


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55:62

## NC073 - Use a struct to encapsulate multiple function parameters:

Using a struct to encapsulate multiple parameters in Solidity functions can significantly enhance code readability and maintainability. Instead of passing a long list of arguments, which can be error-prone and hard to manage, a struct allows grouping related data into a single, coherent entity. This approach simplifies function signatures and makes the code more organized. It also enhances code clarity, as developers can easily understand the relationship between the parameters. Moreover, it aids in future code modifications and expansions, as adding or modifying a parameter only requires changes in the struct definition, rather than in every function that uses these parameters.


<details>
<summary>Click to show 4 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


144       constructor(
145         address defaultAdmin,
146         address _usdc,
147         address _usdcReciever,
148         address _feeReceiver,
149         address _ousgOracle,
150         address _ousg,
151         address _rousg,
152         address _buidl,
153         address _buidlRedeemer,
154         RateLimiterConfig memory rateLimiterConfig
155       )
156         InstantMintTimeBasedRateLimiter(
157           rateLimiterConfig.mintLimitDuration,
158           rateLimiterConfig.redeemLimitDuration,
159           rateLimiterConfig.mintLimit,
160           rateLimiterConfig.redeemLimit
161         )
162       {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144:162

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


102       function initialize(
103         address _kycRegistry,
104         uint256 requirementGroup,
105         address _ousg,
106         address guardian,
107         address _oracle
108       ) public virtual initializer {


112       function __rOUSG_init(
113         address _kycRegistry,
114         uint256 requirementGroup,
115         address _ousg,
116         address guardian,
117         address _oracle
118       ) internal onlyInitializing {


128       function __rOUSG_init_unchained(
129         address _kycRegistry,
130         uint256 _requirementGroup,
131         address _ousg,
132         address guardian,
133         address _oracle
134       ) internal onlyInitializing {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128:134

</details>

## NC074 - Defining All External/Public Functions in Contract Interfaces:

It is preferable to have all the external and public function in an interface to make using them easier by developers. This helps ensure the whole API is extracted in a interface.


<details>
<summary>Click to show 19 findings</summary>

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/f38f658a-e236-41d8-9475-18074078977c.sol


479       function getOUSGPrice() public view returns (uint256 price) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479:479

```solidity
File: tmp/ed555f33-884f-42b5-b953-b3aed6ecb754/188581eb-81e6-4035-ba4d-daba79b68609.sol


102       function initialize(
103         address _kycRegistry,
104         uint256 requirementGroup,
105         address _ousg,
106         address guardian,
107         address _oracle
108       ) public virtual initializer {


166       function name() public pure returns (string memory) {


174       function symbol() public pure returns (string memory) {


181       function decimals() public pure returns (uint8) {


188       function totalSupply() public view returns (uint256) {


199       function balanceOf(address _account) public view returns (uint256) {


220       function transfer(address _recipient, uint256 _amount) public returns (bool) {


231       function allowance(
232         address _owner,
233         address _spender
234       ) public view returns (uint256) {


251       function approve(address _spender, uint256 _amount) public returns (bool) {


276       function transferFrom(
277         address _sender,
278         address _recipient,
279         uint256 _amount
280       ) public returns (bool) {


302       function increaseAllowance(
303         address _spender,
304         uint256 _addedValue
305       ) public returns (bool) {


328       function decreaseAllowance(
329         address _spender,
330         uint256 _subtractedValue
331       ) public returns (bool) {


347       function getTotalShares() public view returns (uint256) {


356       function sharesOf(address _account) public view returns (uint256) {


363       function getSharesByROUSG(
364         uint256 _rOUSGAmount
365       ) public view returns (uint256) {


373       function getROUSGByShares(uint256 _shares) public view returns (uint256) {


378       function getOUSGPrice() public view returns (uint256 price) {


397       function transferShares(
398         address _recipient,
399         uint256 _sharesAmount
400       ) public returns (uint256) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397:400

</details>

