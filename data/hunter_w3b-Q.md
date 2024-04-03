# Low Issues

| Num    | Issue                                                                                                  |
| ------ | :----------------------------------------------------------------------------------------------------- |
| [L-01] | Loss of precision due to division by large numbers                                                     |
| [L-02] | Setters should have initial value check                                                                |
| [L-03] | Constant decimal values                                                                                |
| [L-04] | No limits when setting state variable amounts                                                          |
| [L-05] | Allowed `fees/rates` should be capped by smart contracts                                               |
| [L-06] | Owner can renounce ownership while system is paused                                                    |
| [L-07] | Constructor contains no validation                                                                     |
| [L-08] | For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS |
| [L-09] | External calls in an unbounded for-loop may result in a DoS                                            |
| [L-10] | Contracts are not using their OZ Upgradeable counterparts                                              |
| [L-11] | `decimals()` is not a part of the ERC-20 standard                                                      |
| [L-12] | Missing checks for `address(0)` in the initializer                                                     |
| [L-13] | Governance functions should be controlled by time locks                                                |
| [L-14] | Prefer continue over revert model in iteration                                                         |

## [L-01] Loss of precision due to division by large numbers

Division by large numbers may result in the result being zero, due to solidity not supporting fractions. Consider requiring a minimum amount for the numerator to ensure that it is always larger than the denominator.

```solidity
File: contracts/ousg/ousgInstantManager.sol


728         return (usdcAmount * redeemFee) / FEE_GRANULARITY;


716         return (usdcAmount * mintFee) / FEE_GRANULARITY;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L728

## [L-02] Setters should have initial value check

Setters should have initial value check to prevent assigning wrong value to the variable. Assginment of wrong value can lead to unexpected behavior of the contract.

```solidity
File: main/contracts/ousg/rOUSG.sol


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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L661

```solidity
File: contracts/ousg/ousgInstantManager.sol


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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498

## [L-03] Constant decimal values

The use of fixed decimal values such as `1e18` or `1e8` in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations. Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations. Always retrieve and use the decimals() function from the token contract itself when performing calculations involving token amounts.

```solidity
File: contracts/ousg/rOUSG.sol


190           (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);


202           (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);


367           (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();


375           (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L190

```solidity
File: contracts/ousg/ousgInstantManager.sol


689         uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;


704         usdcOwed = _scaleDown(amountE36 / 1e18);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L689

## [L-04] No limits when setting state variable amounts

It is important to ensure state variables numbers are set to a reasonable value.

```solidity
File: contracts/ousg/ousgInstantManager.sol


559         mintFee = _mintFee;


572         redeemFee = _redeemFee;


629         minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L559

## [L-05] Allowed `fees/rates` should be capped by smart contracts

Fees/rates should be required to be below `100%`, preferably at a much lower limit, to ensure users don't have to monitor the blockchain for changes prior to using the protocol.

```solidity
File: contracts/ousg/ousgInstantManager.sol


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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554

## [L-06] Owner can renounce ownership while system is paused

The contract owner is not prevented from renouncing the ownership while the contract is paused, which would cause any user assets stored in the protocol to be locked indefinitely.

```solidity
File: contracts/ousg/rOUSG.sol


642       function pause() external onlyRole(PAUSER_ROLE) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642

## [L-07] Constructor contains no validation

In Solidity, when values are being assigned in constructors to unsigned or integer variables, it's crucial to ensure the provided values adhere to the protocol's specific operational boundaries as laid out in the project specifications and documentation. If the constructors lack appropriate validation checks, there's a risk of setting state variables with values that could cause unexpected and potentially detrimental behavior within the contract's operations, violating the intended logic of the protocol. This can compromise the contract's security and impact the maintainability and reliability of the system. In order to avoid such issues, it is recommended to incorporate rigorous validation checks in constructors. These checks should align with the project's defined rules and constraints, making use of Solidity's built-in require function to enforce these conditions. If the validation checks fail, the require function will cause the transaction to revert, ensuring the integrity and adherence to the protocol's expected behavior.

```solidity
File: contracts/ousg/rOUSGFactory.sol


47        constructor(address _guardian) {
48          guardian = _guardian;
49        }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47

## [L-08] For loops in `public` or `external` functions should be avoided due to high gas costs and possible DOS

In Solidity, for loops can potentially cause Denial of Service (DoS) attacks if not handled carefully. DoS attacks can occur when an attacker intentionally exploits the gas cost of a function, causing it to run out of gas or making it too expensive for other users to call. Below are some scenarios where for loops can lead to DoS attacks: Nested for loops can become exceptionally gas expensive and should be used sparingly.

```solidity
File: contracts/ousg/rOUSGFactory.sol


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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121

```solidity
File: contracts/ousg/ousgInstantManager.sol


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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794

## [L-09] External calls in an unbounded for-loop may result in a DoS

Consider limiting the number of iterations in for-loops that make external calls.

```solidity
File: contracts/ousg/ousgInstantManager.sol


804         for (uint256 i = 0; i < exCallData.length; ++i) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804

```solidity
File: contracts/ousg/rOUSGFactory.sol


125         for (uint256 i = 0; i < exCallData.length; ++i) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125

## [L-10] Contracts are not using their OZ Upgradeable counterparts

The `non-upgradeable` standard version of OpenZeppelin’s library is inherited/used by the contracts. It would be safer to use the upgradeable versions of the library contracts to avoid unexpected behavior.

Use the contracts from `@openzeppelin/contracts-upgradeable` instead of `@openzeppelin/contracts` where applicable. See https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/tree/master/contracts for a list of available upgradeable contracts

```solidity
File: contracts/ousg/rOUSG.sol


23      import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";


20      import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";


19      import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";


21      import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";


18      import "contracts/external/openzeppelin/contracts/token/IERC20.sol";


22      import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";


24      import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L23

```solidity
File: contracts/ousg/ousgInstantManager.sol


19      import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";


20      import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";


18      import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L19

```solidity
File: contracts/ousg/rOUSGFactory.sol


19      import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19

## [L-11] `decimals()` is not a part of the ERC-20 standard

The `decimals()` function is not a part of the [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20), and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.

```solidity
File: contracts/ousg/ousgInstantManager.sol


187           IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),


396           IERC20Metadata(address(buidl)).decimals() == 6,


392           IERC20Metadata(address(usdc)).decimals() == 6,


283           IERC20Metadata(address(usdc)).decimals() == 6,


191           IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),


204             (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L187

## [L-12] Missing checks for `address(0)` in the initializer

```solidity
File: contracts/ousg/rOUSG.sol


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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102

## [L-13] Governance functions should be controlled by time locks

Governance functions (such as upgrading contracts, setting critical parameters) should be controlled using time locks to introduce a delay between a proposal and its execution. This gives users time to exit before a potentially dangerous or malicious operation is applied.

```solidity
File: contracts/ousg/rOUSG.sol


613       function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {

624       function burn(
625         address _account,
626         uint256 _amount
627       ) external onlyRole(BURNER_ROLE) {

646       function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {

656       function setKYCRequirementGroup(
657         uint256 group
658       ) external override onlyRole(CONFIGURER_ROLE) {

650       function setKYCRegistry(
651         address registry
652       ) external override onlyRole(CONFIGURER_ROLE) {

642       function pause() external onlyRole(PAUSER_ROLE) {

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613

```solidity
File: contracts/ousg/ousgInstantManager.sol


567       function setRedeemFee(
568         uint256 _redeemFee
569       ) external override onlyRole(CONFIGURER_ROLE) {

819       function retrieveTokens(
820         address token,
821         address to,
822         uint256 amount
823       ) external onlyRole(DEFAULT_ADMIN_ROLE) {

663       function setInvestorBasedRateLimiter(
664         address _investorBasedRateLimiter
665       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

581       function setMinimumDepositAmount(
582         uint256 _minimumDepositAmount
583       ) external override onlyRole(CONFIGURER_ROLE) {

622       function setMinimumBUIDLRedemptionAmount(
623         uint256 _minimumBUIDLRedemptionAmount
624       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

554       function setMintFee(
555         uint256 _mintFee
556       ) external override onlyRole(CONFIGURER_ROLE) {

786       function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {

540       function setInstantRedemptionLimitDuration(
541         uint256 _instantRedemptionLimitDuratioin
542       ) external override onlyRole(CONFIGURER_ROLE) {

512       function setInstantRedemptionLimit(
513         uint256 _instantRedemptionLimit
514       ) external override onlyRole(CONFIGURER_ROLE) {

768       function pauseMint() external onlyRole(PAUSER_ROLE) {

774       function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {

498       function setInstantMintLimit(
499         uint256 _instantMintLimit
500       ) external override onlyRole(CONFIGURER_ROLE) {

526       function setInstantMintLimitDuration(
527         uint256 _instantMintLimitDuration
528       ) external override onlyRole(CONFIGURER_ROLE) {

638       function setOracle(
639         address _oracle
640       ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

780       function pauseRedeem() external onlyRole(PAUSER_ROLE) {

599       function setMinimumRedemptionAmount(
600         uint256 _minimumRedemptionAmount
601       ) external override onlyRole(CONFIGURER_ROLE) {

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

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567

## [L-14] Prefer continue over revert model in iteration

Preferably, it's better to skip operations on array indices when a condition is not met instead of reverting the entire transaction. Reverting could be exploited by malicious actors who might intentionally introduce array objects failing conditional checks, disrupting group operations. It's advisable to skip array indices rather than revert, unless there are valid security or logic reasons for doing otherwise

```solidity
File: contracts/ousg/ousgInstantManager.sol


804         for (uint256 i = 0; i < exCallData.length; ++i) {
805           (bool success, bytes memory ret) = address(exCallData[i].target).call{
806             value: exCallData[i].value
807           }(exCallData[i].data);
808           require(success, "Call Failed");
809           results[i] = ret;
810         }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804

```solidity
File: contracts/ousg/rOUSGFactory.sol


125         for (uint256 i = 0; i < exCallData.length; ++i) {
126           (bool success, bytes memory ret) = address(exCallData[i].target).call{
127             value: exCallData[i].value
128           }(exCallData[i].data);
129           require(success, "Call Failed");
130           results[i] = ret;
131         }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125

# Non-critical Issues

| Num     | Issue                                                                                                                    |
| ------- | :----------------------------------------------------------------------------------------------------------------------- |
| [NC-01] | Use scientific notation (`e.g. 1e18`) rather than exponentiation (e.g. `10**18`)                                         |
| [NC-02] | Imports could be organized more systematically                                                                           |
| [NC-03] | Constants in comparisons should appear on the left side                                                                  |
| [NC-04] | Events may be emitted out of order due to reentrancy                                                                     |
| [NC-05] | Import declarations should import specific identifiers, rather than the whole file                                       |
| [NC-06] | Constant redefined elsewhere                                                                                             |
| [NC-07] | Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, for readability |
| [NC-08] | Variable names for `immutable`s should use CONSTANT_CASE                                                                 |
| [NC-09] | Function declarations should have NatSpec descriptions                                                                   |
| [NC-10] | Contract declarations should have `@notice` tags                                                                         |
| [NC-11] | Expressions for constant values such as a call to `keccak256()`, should use `immutable` rather than `constant`           |
| [NC-12] | Consider bounding input array length                                                                                     |
| [NC-13] | Variables should be named in `mixedCase` style                                                                           |
| [NC-14] | Consider moving `msg.sender` checks to a common authorization `modifier`                                                 |

## [NC-01] Use scientific notation (`e.g. 1e18`) rather than exponentiation (e.g. `10**18`)

While the compiler knows to optimize away the exponentiation, it's still better coding practice to use idioms that do not require compiler optimization, if they exist.

```solidity
File: contracts/ousg/ousgInstantManager.sol


203           10 **
204             (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L203-L204

## [NC-02] Imports could be organized more systematically

This issue arises when the contract's interface is not imported first, followed by each of the interfaces it uses, followed by all other files.

```solidity
File: contracts/ousg/rOUSG.sol


26      import "contracts/rwaOracles/IRWAOracle.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L26

```solidity
File: contracts/ousg/ousgInstantManager.sol


20      import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L20

```solidity
File: contracts/ousg/rOUSGFactory.sol


22      import "contracts/interfaces/IMulticall.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L22

## [NC-03] Constants in comparisons should appear on the left side

This issue arises when constants in comparisons appear on the right side, which can lead to typo bugs.

```solidity
File: contracts/ousg/rOUSG.sol


416         require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");


432         require(_rOUSGAmount > 0, "rOUSG: can't unwrap zero rOUSG tokens");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416

```solidity
File: contracts/ousg/ousgInstantManager.sol


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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L283

## [NC-04] Events may be emitted out of order due to reentrancy

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls

```solidity
File: contracts/ousg/rOUSG.sol


/// @audit transferFrom() called before event
420         emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));


/// @audit transfer() called before event
639         emit TransferShares(_account, address(0), ousgSharesAmount);


/// @audit transfer() called before event
441         emit Transfer(msg.sender, address(0), _rOUSGAmount);


/// @audit transferFrom() called before event
421         emit TransferShares(address(0), msg.sender, ousgSharesAmount);


/// @audit transfer() called before event
442         emit TransferShares(msg.sender, address(0), ousgSharesAmount);


/// @audit transfer() called before event
638         emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L420

```solidity
File: contracts/ousg/ousgInstantManager.sol


/// @audit transferFrom() called before event
350         emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut);


/// @audit transfer() called before event
443           emit BUIDLRedemptionSkipped(
444             msg.sender,
445             usdcAmountToRedeem,
446             usdcBalance - usdcAmountToRedeem
447           );


/// @audit transferFrom() called before event
380         emit InstantRedemptionRebasingOUSG(
381           msg.sender,
382           rousgAmountIn,
383           ousgAmountIn,
384           usdcAmountOut
385         );


/// @audit transferFrom() called before event
321         emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);


/// @audit transfer() called before event
435           emit MinimumBUIDLRedemption(
436             msg.sender,
437             minBUIDLRedeemAmount,
438             usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
439           );


/// @audit transfer() called before event
270         emit InstantMintRebasingOUSG(
271           msg.sender,
272           usdcAmountIn,
273           ousgAmountOut,
274           rousgAmountOut
275         );


/// @audit transfer() called before event
453         emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L350

## [NC-05] Import declarations should import specific identifiers, rather than the whole file

Using import declarations of the form import {<identifier_name>} from 'some/file.sol' avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation

```solidity
File: contracts/ousg/rOUSG.sol


18      import "contracts/external/openzeppelin/contracts/token/IERC20.sol";


19      import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";


20      import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";


21      import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";


22      import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";


23      import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";


24      import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L18

```solidity
File: contracts/ousg/ousgInstantManager.sol


18      import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";


19      import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";


20      import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L18

```solidity
File: contracts/ousg/rOUSGFactory.sol


19      import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19

## [NC-06] Constant redefined elsewhere

Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A cheap way to store constants in a single location is to create an internal constant in a library. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.

```solidity
File: contracts/ousg/ousgInstantManager.sol


  bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");

  bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");

  uint256 public constant OUSG_TO_ROUSG_SHARES_MULTIPLIER = 10_000;

```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57

## [NC-07] Multiple `address`/ID mappings can be combined into a single `mapping` of an `address`/ID to a `struct`, for readability

Well-organized data structures make code reviews easier, which may lead to fewer bugs. Consider combining related mappings into mappings to structs, so it's clear what data is related

```solidity
File: contracts/ousg/rOUSG.sol


72        mapping(address => uint256) private shares;

75        mapping(address => mapping(address => uint256)) private allowances;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72

## [NC-08] Variable names for `immutable`s should use CONSTANT_CASE

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (CONSTANT_CASE).

```solidity
File: contracts/ousg/ousgInstantManager.sol


72        IERC20 public immutable usdc; // 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;


75        IRWALike public immutable ousg;


78        ROUSG public immutable rousg;


81        IERC20 public immutable buidl;


84        IBUIDLRedeemer public immutable buidlRedeemer;


87        uint256 public immutable decimalsMultiplier;


90        address public immutable usdcReceiver;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L72

```solidity
File: contracts/ousg/rOUSGFactory.sol


40        address internal immutable guardian;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L40

## [NC-09] Function declarations should have NatSpec descriptions

Function declarations should be preceded by a NatSpec comment.

```solidity
File: contracts/ousg/ousgInstantManager.sol


102       function initialize(


378       function getOUSGPrice() public view returns (uint256 price) {


642       function pause() external onlyRole(PAUSER_ROLE) {


646       function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {


650       function setKYCRegistry(


656       function setKYCRequirementGroup(


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479

```solidity
File:


47        constructor(address _guardian) {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47

## [NC-10] Contract declarations should have `@notice` tags

`@notice` is used to explain to end users what the contract does, and the compiler interprets `///` or `/**` comments as this tag if one wasn't explicitly provided.

```solidity
File: contracts/ousg/rOUSG.sol


55      contract ROUSG is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55

```solidity
File: contracts/ousg/ousgInstantManager.sol


49      contract OUSGInstantManager is


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49

```solidity
File: contracts/ousg/rOUSGFactory.sol


37      contract ROUSGFactory is IMulticall {


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L37

## [NC-11] Expressions for constant values such as a call to `keccak256()`, should use `immutable` rather than `constant`

While it **doesn't save any gas** because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between `constant` variables and `immutable` variables, and they should each be used in their appropriate contexts. `constants` should be used for literal values written into the code, and `immutable` variables should be used for expressions, or values calculated in, or passed into the constructor.

```solidity
File: contracts/ousg/ousgInstantManager.sol


93        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


94        bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");


95        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60

```solidity
File: contracts/ousg/rOUSG.sol


57        bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");


60        bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95

## [NC-12] Consider bounding input array length

The functions below take in an unbounded array, and make function calls for entries in the array. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to `require()` that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.

```solidity
File: contracts/ousg/rOUSGFactory.sol


804         for (uint256 i = 0; i < exCallData.length; ++i) {
805           (bool success, bytes memory ret) = address(exCallData[i].target).call{
806             value: exCallData[i].value
807           }(exCallData[i].data);
808           require(success, "Call Failed");
809           results[i] = ret;
810         }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125

```solidity
File: contracts/ousg/ousgInstantManager.sol


125         for (uint256 i = 0; i < exCallData.length; ++i) {
126           (bool success, bytes memory ret) = address(exCallData[i].target).call{
127             value: exCallData[i].value
128           }(exCallData[i].data);
129           require(success, "Call Failed");
130           results[i] = ret;
131         }


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804

## [NC-13] Variables should be named in `mixedCase` style

As the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#naming-styles) suggests: arguments, local variables and mutable state variables should be named in mixedCase style.

```solidity
File: contracts/ousg/rOUSG.sol


431       function unwrap(uint256 _rOUSGAmount) external whenNotPaused {


415       function wrap(uint256 _OUSGAmount) external whenNotPaused {


364         uint256 _rOUSGAmount


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L431

```solidity
File: contracts/ousg/ousgInstantManager.sol


120       uint256 public minBUIDLRedeemAmount = 250_000e6;


623         uint256 _minimumBUIDLRedemptionAmount


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L120

```solidity
File: contracts/ousg/rOUSGFactory.sol


41        ROUSG public rOUSGImplementation;


84          ROUSG rOUSGProxied = ROUSG(address(rOUSGProxy));


43        TokenProxy public rOUSGProxy;


42        ProxyAdmin public rOUSGProxyAdmin;


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L41

## [NC-14] Consider moving `msg.sender` checks to a common authorization `modifier`

```solidity
File: contracts/ousg/rOUSG.sol


594           require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");


```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594

```solidity
File: contracts/ousg/ousgInstantManager.sol


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

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L298
