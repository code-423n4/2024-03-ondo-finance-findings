| №   | Title                                                                                                                                          | Severity |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| 1   | Burning is centralized                                                                                                                         | Low      |
| 2   | Using an older Solidity compiler version                                                                                                       | Low      |
| 3   | Outstanding `USDC` approvals during minting and `OUSG` approvals during redemption in `OUSGInstantManager.sol` contract                        | Low      |
| 4   | `usdcReceiver` in `OUSGInstantManager.sol` contract cannot be changed                                                                          | Low      |
| 5   | The `minBUIDLRedeemAmount` state variable in `OUSGInstantManager.sol` can be changed, which is completely unwanted behaviour by contest README | Low      |
| 6   | Change the `getOUSGPrice()` function to check if `price` is greater or equals to `MINIMUM_OUSG_PRICE` value                                    | Low      |
| 7   | No default fees configuration (`mintFee` and `redeemFee`)                                                                                      | Low      |
| 8   | Missing calls to base initializers in rUSDY                                                                                                    | Low      |
| 9   | Consider bounding input array length                                                                                                           | Low      |
| 10  | Constant decimal values                                                                                                                        | Low      |
| 11  | `constructor`/`initialize` function lacks parameter validation                                                                                 | Low      |
| 12  | `require()` should be used instead of `assert()`                                                                                               | Low      |
| 13  | Setters should prevent re-setting of the same value                                                                                            | Low      |
| 14  | Upgradeable contract is missing a `__gap[50]` storage variable at the end to allow for new storage variables in later versions                 | Low      |
| 15  | `@openzeppelin/contracts` should be upgraded to a newer version                                                                                | Low      |
| 16  | Add inline comments for unnamed variables                                                                                                      | NC       |
| 17  | Consider using `SafeTransferLib.safeTransferETH()` or `Address.sendValue()` for clearer semantic meaning                                       | NC       |
| 18  | Contract uses both `require()`/`revert()` as well as custom errors                                                                             | NC       |
| 19  | Custom `error` without details                                                                                                                 | NC       |
| 20  | Custom errors should be used rather than `revert()`/`require()`                                                                                | NC       |
| 21  | Event emit should emit a parameter                                                                                                             | NC       |
| 22  | Event is missing `indexed` fields                                                                                                              | NC       |
| 23  | Events are missing sender information                                                                                                          | NC       |
| 24  | Events may be emitted out of order due to reentrancy                                                                                           | NC       |
| 25  | Events should be emitted before external calls                                                                                                 | NC       |
| 26  | Events that mark critical parameter changes should contain both the old and the new value                                                      | NC       |
| 27  | Multiple NatSpec Bugs/Improvements                                                                                                             | NC       |
| 28  | Non-`external`/`public` state variables should begin with an underscore                                                                        | NC       |
| 29  | Not using the latest versions of project dependencies                                                                                          | NC       |
| 30  | Prefer skip over revert model in iteration                                                                                                     | NC       |
| 31  | Use `@inheritdoc` for overridden functions                                                                                                     | NC       |
| 32  | Use of `override` is unnecessary                                                                                                               | NC       |
| 33  | Variables need not be initialized to zero                                                                                                      | NC       |

---

## 1. Burning is centralized

### GitHub Links
- [rOUSG.sol#burn()](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L624-L640)

### Description
The burning mechanism in the `rOUSG` contract is controlled by a designated `BURNER_ROLE`, which in turn is managed by the `DEFAULT_ADMIN_ROLE`. This setup centralizes the capability to burn tokens, granting the admin or any account with the `BURNER_ROLE` the power to remove tokens from circulation without the token holder's consent. In scenarios where the admin or burner accounts are either compromised or act maliciously, this could lead to unauthorized burning of user tokens, potentially leading to loss of funds for the token holders. Additionally, the control over burning could be exploited to manipulate the token's supply, impacting its overall economy and trust.

```solidity
  /**
   * @notice Admin burn function to burn rOUSG tokens from any account
   * @param _account The account to burn tokens from
   * @param _amount  The amount of rOUSG tokens to burn
   * @dev Transfers burned shares (OUSG) to `msg.sender`
   */
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

**Impact:**
High, as token supply can be endlessly inflated and user tokens can be burned on demand

**Likelihood:**
Low, as it requires a malicious or compromised admin/burner.

### Recommended Mitigation Steps
Give those roles only to contracts that have a Timelock mechanism so that users have enough time to exit their `rOUSG` positions if they decide that they don't agree with a transaction of the admin/burner.


## 2. Using an older Solidity compiler version

### Description
Currently the protocol contracts use pragma solidity 0.8.16; which is a version that according to the List of Known Bugs in Solidity contains some Low severity issues. It is highly suggested to update the compiler version to a more recent one to make use of bugfixes and optimizations.

## 3. Outstanding `USDC` approvals during minting and `OUSG` approvals during redemption in `OUSGInstantManager.sol` contract

## 4. `usdcReceiver` in `OUSGInstantManager.sol` contract cannot be changed

### GitHub Links
- [OUSGInstantManager.sol#usdcReceiver state variable](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L90)

### Description
The `usdcReceiver` address in the `OUSGInstantManager.sol` contract is immutable, meaning it cannot be changed after contract deployment. If this address gets compromised, there's no mechanism to update it, potentially leading to loss of funds as all USDC meant for the protocol would be sent to a malicious address.

```solidity
  // The address that receives USDC for subscriptions
  address public immutable usdcReceiver;
```

### Recommended Mitigation Steps
Introduce a secure function to update the `usdcReceiver` address. This function should be guarded by appropriate access control measures to ensure only authorized parties can change the address. Also it would be helpful in this function to implement check if the the current `usdcReceiver` address have zero balance of USDC and only then to allow the changing of `usdcReceiver` address.  

## 5. The `minBUIDLRedeemAmount` state variable in `OUSGInstantManager.sol` can be changed, which is completely unwanted behavuour by contest README

### GitHub Links
- [OUSGInstantManager.sol#minBUIDLRedeemAmount state variable](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L118-L120)

### Description

In the contest README write the [following](https://code4rena.com/audits/2024-03-ondo-finance#top):
> There is a BUIDL redemption minimum requirement that can assumed to be 250,000 BUIDL tokens that we do not to inherit for OUSG/rOUSG holders. To bypass this,
we have added logic to ensure that the minimum amount of BUIDL that this contract redeems is always at least 250,000. As a consequence, there will sometimes be leftover USDC held inthe contract. We also have logic to use the USDC to cover the redemptions when the redemption amount is less than the contracts USDC balance.

The `minBUIDLRedeemAmount` is a critical parameter in the `OUSGInstantManager.sol` contract, intended to ensure that a minimum amount of BUIDL tokens is redeemed, aligning with the protocol's economic mechanisms and incentives. The ability to change this variable could lead to potential disruptions in the protocol's intended functionality, especially if set to values that diverge from the original design and intentions outlined in the project's documentation.

```solidity
  // The minimum amount of BUIDL that must be redeemed in a single redemption
  // with the BUIDLRedeemer contract
  uint256 public minBUIDLRedeemAmount = 250_000e6;
```

### Recommended Mitigation Steps
If the `minBUIDLRedeemAmount` is meant to be a constant or only updated under very specific circumstances, consider implementing mechanisms to lock this value or strictly limit its mutability. This could involve using a governance process for changes or setting it as immutable if it truly should never change.

## 6. Change the `getOUSGPrice()` function to check if `price` is greater or equals to `MINIMUM_OUSG_PRICE` value

### GitHub Links
- [OUSGInstantManager.sol#getOUSGPrice()](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479-L485) function

### Description
Change the getOUSGPrice() function to check if price is greater or equals to MINIMUM_OUSG_PRICE value for better understanding, because the specific for MINIMUM_OUSG_PRICE is: A uint256 constant set to 105e18 to act as a safety circuit breaker in case of Oracle malfunction. This ensures that the price of OUSG doesn't fall below this minimum threshold.

```solidity
 function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

Same for the checks and in `setMintFee()`, `setRedeemFee()` functions.

### Recommended Mitigation Steps
Modify the `getOUSGPrice()` function as following:
```diff
 function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
-   require(
-     price > MINIMUM_OUSG_PRICE,
-     "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
-   );
+  require(
+     price >= MINIMUM_OUSG_PRICE,
+     "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
+   );
  }
```

## 7. No default fees configuration (`mintFee` and `redeemFee`)

### Description
The absence of default configurations for `mintFee` and `redeemFee` can lead to unpredictability in fee structures, potentially causing confusion among users or unintentionally zero fees if not set post-deployment.

### Recommended Mitigation Steps
Establish sensible default values for both `mintFee` and `redeemFee` within the contract, ensuring that fee structures are in place immediately upon deployment. Also include checks in the contract's initialization function to ensure that fees are explicitly set before the contract becomes operational.

## 8. Missing calls to base initializers in rUSDY

### Description
The `__rOUSG_init()` function doesn't call the initializers for some of the base contracts:

- `Initializable`
- `ContextUpgradeable`
- `PausableUpgradeable`
- `AccessControlEnumerableUpgradeable`

### Recommended Mitigation Steps
Modify the `__rOUSG_init()` function to call the initializers of all base contracts. This may include manually invoking each base initializer or utilizing a tool like OpenZeppelin's `Initializable` pattern to streamline the process.

---

## 9. Consider bounding input array length

The functions below take in an unbounded array, and make function calls for entries in the array. While the function will revert if it eventually runs out of gas, it may be a nicer user experience to `require()` that the length of the array is below some reasonable maximum, so that the user doesn't have to use up a full transaction's gas only to see that the transaction reverts.

<details>
<summary><i>There are 2 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

804:     for (uint256 i = 0; i < exCallData.length; ++i) {
805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
806:         value: exCallData[i].value
807:       }(exCallData[i].data);
808:       require(success, "Call Failed");
809:       results[i] = ret;
810:     }
```

[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804-L810)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

/// @audit exCallData.length not bounded
125:     for (uint256 i = 0; i < exCallData.length; ++i) {
126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
127:         value: exCallData[i].value
128:       }(exCallData[i].data);
129:       require(success, "Call Failed");
130:       results[i] = ret;
131:     }
```

[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125-L131)

</details>

---

## 10. Constant decimal values

The use of fixed decimal values such as 1e18 or 1e8 in Solidity contracts can lead to inaccuracies, bugs, and vulnerabilities, particularly when interacting with tokens having different decimal configurations. Not all ERC20 tokens follow the standard 18 decimal places, and assumptions about decimal places can lead to miscalculations.

<details>
<summary><i>There are 3 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

689:     uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;

704:     usdcOwed = _scaleDown(amountE36 / 1e18);
```

[689](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L689), [704](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L704)

```solidity
📁 File: contracts/ousg/rOUSG.sol

367:       (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
```

[367](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L367)

</details>

---

## 11. `constructor`/`initialize` function lacks parameter validation

Constructors and initialization functions play a critical role in contracts by setting important initial states when the contract is first deployed before the system starts. The parameters passed to the constructor and initialization functions directly affect the behavior of the contract / protocol. If incorrect parameters are provided, the system may fail to run, behave abnormally, be unstable, or lack security. Therefore, it's crucial to carefully check each parameter in the constructor and initialization functions. If an exception is found, the transaction should be rolled back.

<details>
<summary><i>There are 3 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

/// @audit defaultAdmin , rateLimiterConfig
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
```

[144](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144-L162)

```solidity
📁 File: contracts/ousg/rOUSG.sol

/// @audit _kycRegistry , requirementGroup , _ousg , guardian , _oracle
102:   function initialize(
103:     address _kycRegistry,
104:     uint256 requirementGroup,
105:     address _ousg,
106:     address guardian,
107:     address _oracle
108:   ) public virtual initializer {
```

[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

/// @audit _guardian
47:   constructor(address _guardian) {
```

[47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)

</details>

---

### Initialize function does not use the initializer modifier

The `initialize()` functions below are not called by another contract atomically after the contract is deployed, so it's possible for a malicious user to call `initialize()` which, if it's noticed in time, would require the project to re-deploy the contract in order to properly initialize. Consider creating a factory contract, which will `new` and `initialize()` each contract atomically.

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

102:   function initialize(
103:     address _kycRegistry,
104:     uint256 requirementGroup,
105:     address _ousg,
106:     address guardian,
107:     address _oracle
108:   ) public virtual initializer {
```

[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108)

---

## 12. `require()` should be used instead of `assert()`

Prior to solidity version 0.8.0, hitting an assert consumes the **remainder of the transaction's available gas** rather than returning it, as `require()`/`revert()` do. `assert()` should be avoided even past solidity version 0.8.0 as its [documentation](https://docs.soliditylang.org/en/v0.8.14/control-structures.html#panic-via-assert-and-error-via-require) states that "The assert function creates an error of type Panic(uint256). ... Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix".

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

94:     assert(rOUSGProxyAdmin.owner() == guardian);
```

[94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94)

---

## 13. Setters should prevent re-setting of the same value

This especially problematic when the setter also emits the same value, which may be confusing to offline parsers

<details>
<summary><i>There are 6 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

/// @note Confidence: 100.00%
554:   function setMintFee(
555:     uint256 _mintFee
556:   ) external override onlyRole(CONFIGURER_ROLE) {
557:     require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558:     emit MintFeeSet(mintFee, _mintFee);
559:     mintFee = _mintFee;
560:   }

/// @note Confidence: 100.00%
567:   function setRedeemFee(
568:     uint256 _redeemFee
569:   ) external override onlyRole(CONFIGURER_ROLE) {
570:     require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571:     emit RedeemFeeSet(redeemFee, _redeemFee);
572:     redeemFee = _redeemFee;
573:   }

/// @note Confidence: 100.00%
622:   function setMinimumBUIDLRedemptionAmount(
623:     uint256 _minimumBUIDLRedemptionAmount
624:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
625:     emit MinimumBUIDLRedemptionAmountSet(
626:       minBUIDLRedeemAmount,
627:       _minimumBUIDLRedemptionAmount
628:     );
629:     minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
630:   }

/// @note Confidence: 100.00%
638:   function setOracle(
639:     address _oracle
640:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
641:     emit OracleSet(address(oracle), _oracle);
642:     oracle = IRWAOracle(_oracle);
643:   }

/// @note Confidence: 100.00%
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
```

[554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554-L560), [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567-L573), [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622-L630), [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638-L643), [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L673)

```solidity
📁 File: contracts/ousg/rOUSG.sol

/// @note Confidence: 100.00%
613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
614:     emit OracleSet(address(oracle), _oracle);
615:     oracle = IRWAOracle(_oracle);
616:   }
```

[613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613-L616)

</details>

---

## 14. Upgradeable contract is missing a `__gap[50]` storage variable at the end to allow for new storage variables in later versions

See [this](https://docs.openzeppelin.com/contracts/4.x/upgradeable#storage_gaps) link for a description of this storage variable. While some contracts may not currently be sub-classed, adding the variable now protects against forgetting to add it in the future.

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

55: contract ROUSG is
56:   Initializable,
57:   ContextUpgradeable,
58:   PausableUpgradeable,
59:   AccessControlEnumerableUpgradeable,
60:   KYCRegistryClientUpgradeable,
```

[55](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55-L60)

---

## 15. `@openzeppelin/contracts` should be upgraded to a newer version

These contracts import contracts from `@openzeppelin/contracts`, but they are not using the [latest version](https://github.com/OpenZeppelin/openzeppelin-contracts/releases).

> ❗ Issue is removed from: (pech, sme6en)

<details>
<summary><i>There are 11 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

18: import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";
19: import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";
20: import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";
```

[18](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L18-L20)

```solidity
📁 File: contracts/ousg/rOUSG.sol

18: import "contracts/external/openzeppelin/contracts/token/IERC20.sol";
19: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";
20: import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";
21: import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";
22: import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";
23: import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";
24: import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";
```

[18](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L18-L24)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

19: import "contracts/external/openzeppelin/contracts/proxy/ProxyAdmin.sol";
```

[19](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L19)

</details>

---

## 16. Add inline comments for unnamed variables

`function foo(address x, address)` -> `function foo(address x, address /* y */)`

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

586:   function _beforeTokenTransfer(
587:     address from,
588:     address to,
589:     uint256
590:   ) internal view {
```

[586](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L586-L590)

---

## 17. Consider using `SafeTransferLib.safeTransferETH()` or `Address.sendValue()` for clearer semantic meaning

These Functions indicate their purpose with their name more clearly than using low-level calls.

<details>
<summary><i>There are 2 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

805:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
806:         value: exCallData[i].value
807:       }(exCallData[i].data);
```

[805](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805-L807)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

126:       (bool success, bytes memory ret) = address(exCallData[i].target).call{
127:         value: exCallData[i].value
128:       }(exCallData[i].data);
```

[126](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L126-L128)

</details>

---

## 18. Contract uses both `require()`/`revert()` as well as custom errors

Consider using just one method in a single file

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

55: contract ROUSG is
```

[55](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55)

---

## 19. Custom `error` without details

Consider adding some parameters to the error to indicate which user or values caused the failure.

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

90:   error UnwrapTooSmall();
```

[90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)

---

## 20. Custom errors should be used rather than `revert()`/`require()`

Custom errors are available from solidity version 0.8.4. Custom errors are more easily processed in try-catch blocks, and are easier to re-use and maintain.

<details>
<summary><i>There are 50 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

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

[163](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L163-L193), [205](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L205-L209), [282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L282-L289), [298](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L298-L301), [310](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L310-L313), [344](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L344-L347), [371](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L371-L374), [391](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L391-L398), [402](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L402-L405), [417](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L417-L420), [459](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L459-L462), [466](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L466-L469), [481](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L481-L484), [557](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L557), [570](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L570), [584](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L584-L587), [602](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L602-L605), [653](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L653), [757](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L757), [763](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L763), [808](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L808)

```solidity
📁 File: contracts/ousg/rOUSG.sol

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

[282](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L282), [333](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L333-L336), [416](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L416), [432](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L432), [477](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L477-L478), [506](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L506-L507), [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L512-L515), [533](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L533), [558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L558), [563](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L563), [594](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L594), [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L599), [604](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L604)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

76:     require(!initialized, "ROUSGFactory: rOUSG already deployed");

129:       require(success, "Call Failed");

150:     require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");
```

[76](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L76), [129](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L129), [150](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L150)

</details>

---

## 22. Event emit should emit a parameter

Some emitted events do not have any emitted parameters. It is recommended to add some parameter such as state changes or value changes when events are emitted

<i>There are 4 instaces of this issue:</i>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

770:     emit MintPaused();

776:     emit MintUnpaused();

782:     emit RedeemPaused();

788:     emit RedeemUnpaused();
```

[770](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L770), [776](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L776), [782](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L782), [788](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L788)

---

## 22. Event is missing `indexed` fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

<details>
<summary><i>There are 2 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/rOUSG.sol

149:   event TransferShares(
150:     address indexed from,
151:     address indexed to,
152:     uint256 sharesValue
153:   );
```

[149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L149-L153)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

141:   event rOUSGDeployed(
142:     address proxy,
143:     address proxyAdmin,
144:     address implementation,
145:     string name,
146:     string ticker
147:   );
```

[141](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141-L147)

</details>

---

## 23. Events are missing sender information

When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the msg.sender the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

<details>
<summary><i>There are 16 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

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

[558](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L558), [571](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L571), [589](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L589), [606](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L606-L609), [625](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L625-L628), [641](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L641), [654](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L654), [666](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L666-L669), [770](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L770), [776](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L776), [782](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L782), [788](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L788)

```solidity
📁 File: contracts/ousg/rOUSG.sol

457:     emit Transfer(_sender, _recipient, _amount);
458:     emit TransferShares(_sender, _recipient, _sharesToTransfer);

614:     emit OracleSet(address(oracle), _oracle);

639:     emit TransferShares(_account, address(0), ousgSharesAmount);
```

[457](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L457-L458), [614](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L614), [639](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L639)

</details>

---

## 24. Events may be emitted out of order due to reentrancy

If a reentrancy occurs, some events may be emitted in an unexpected order, and this may be a problem if a third party expects a specific order for these events. Ensure that events follow the best practice of CEI.

<details>
<summary><i>There are 8 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

240:     emit InstantMintOUSG(msg.sender, usdcAmountIn, ousgAmountOut);

270:     emit InstantMintRebasingOUSG(
271:       msg.sender,
272:       usdcAmountIn,
273:       ousgAmountOut,
274:       rousgAmountOut
275:     );
```

[240](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L240), [270](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L270-L275)

```solidity
📁 File: contracts/ousg/rOUSG.sol

402:     emit TransferShares(msg.sender, _recipient, _sharesAmount);

404:     emit Transfer(msg.sender, _recipient, tokensAmount);

420:     emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
421:     emit TransferShares(address(0), msg.sender, ousgSharesAmount);

457:     emit Transfer(_sender, _recipient, _amount);
458:     emit TransferShares(_sender, _recipient, _sharesToTransfer);
```

[402](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L402), [404](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L404), [420](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L420-L421), [457](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L457-L458)

</details>

---

## 25. Events should be emitted before external calls

Ensure that events follow the best practice of check-effects-interaction, and are emitted before external calls.

<details>
<summary><i>There are 14 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

/// @audit transfer() on line 269
270:     emit InstantMintRebasingOUSG(
271:       msg.sender,
272:       usdcAmountIn,
273:       ousgAmountOut,
274:       rousgAmountOut
275:     );

/// @audit transferFrom() on line 319
321:     emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);

/// @audit transferFrom() on line 348
350:     emit InstantRedemptionOUSG(msg.sender, ousgAmountIn, usdcAmountOut);

/// @audit unwrap() on line 376
380:     emit InstantRedemptionRebasingOUSG(
381:       msg.sender,
382:       rousgAmountIn,
383:       ousgAmountIn,
384:       usdcAmountOut
385:     );

/// @audit burn() on line 422
435:       emit MinimumBUIDLRedemption(
436:         msg.sender,
437:         minBUIDLRedeemAmount,
438:         usdcBalance + minBUIDLRedeemAmount - usdcAmountToRedeem
439:       );

/// @audit burn() on line 422
443:       emit BUIDLRedemptionSkipped(
444:         msg.sender,
445:         usdcAmountToRedeem,
446:         usdcBalance - usdcAmountToRedeem
447:       );

/// @audit transfer() on line 451
453:     emit RedeemFeesDeducted(msg.sender, feeReceiver, usdcFees, usdcAmountOut);
```

[270](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L270-L275), [321](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L321), [350](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L350), [380](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L380-L385), [435](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L435-L439), [443](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L443-L447), [453](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L453)

```solidity
📁 File: contracts/ousg/rOUSG.sol

/// @audit transferFrom() on line 419
420:     emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
/// @audit transferFrom() on line 419
421:     emit TransferShares(address(0), msg.sender, ousgSharesAmount);

/// @audit transfer() on line 437
441:     emit Transfer(msg.sender, address(0), _rOUSGAmount);
/// @audit transfer() on line 437
442:     emit TransferShares(msg.sender, address(0), ousgSharesAmount);

/// @audit transfer() on line 634
638:     emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
/// @audit transfer() on line 634
639:     emit TransferShares(_account, address(0), ousgSharesAmount);
```

[420](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L420-L421), [441](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L441-L442), [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L638-L639)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

/// @audit owner() on line 94
96:     emit rOUSGDeployed(
97:       address(rOUSGProxy),
98:       address(rOUSGProxyAdmin),
99:       address(rOUSGImplementation),
100:       rOUSGProxied.name(),
101:       rOUSGProxied.symbol()
102:     );
```

[96](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L96-L102)

</details>

---

## 26. Events that mark critical parameter changes should contain both the old and the new value

This should especially be done if the new value is not required to be different from the old value

<details>
<summary><i>There are 3 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

638:   function setOracle(
639:     address _oracle
640:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
641:     emit OracleSet(address(oracle), _oracle);
642:     oracle = IRWAOracle(_oracle);
643:   }

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
```

[638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638-L643), [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L673)

```solidity
📁 File: contracts/ousg/rOUSG.sol

613:   function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
614:     emit OracleSet(address(oracle), _oracle);
615:     oracle = IRWAOracle(_oracle);
616:   }
```

[613](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613-L616)

</details>

---

## 27. Multiple NatSpec Bugs/Improvements

### NatSpec documentation for `constructor` is missing

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

47:   constructor(address _guardian) {
```

[47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)

---

### NatSpec: Constructor declarations should have `@notice` tags

<details>
<summary><i>There are 2 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/rOUSG.sol

98:   constructor() {
```

[98](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L98)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

47:   constructor(address _guardian) {
```

[47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47)

</details>

---

### NatSpec: Contract declarations should have `@author` tags

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

54:
55: contract ROUSG is
56:   Initializable,
```

[54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54-L56)

---

### NatSpec: Contract declarations should have `@dev` tags

<details>
<summary><i>There are 2 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/rOUSG.sol

54:
55: contract ROUSG is
56:   Initializable,
```

[54](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L54-L56)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

36:  */
37: contract ROUSGFactory is IMulticall {
38:   bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

[36](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L36-L38)

</details>

---

### NatSpec: Error declarations should have `@notice` tags

`@notice` is used to explain to end users what the error does, and the compiler interprets `///` or `/**` comments as this tag if one was't explicitly provided

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

90:   error UnwrapTooSmall();
```

[90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)

---

### NatSpec: Error declarations should have NatSpec descriptions

It is recommended that errors are fully annotated using NatSpec. It is clearly stated in the Solidity official documentation.

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

90:   error UnwrapTooSmall();
```

[90](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L90)

---

### NatSpec: Error missing NatSpec `@dev` tag

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

89:   // Error when redeeming shares < `OUSG_TO_ROUSG_SHARES_MULTIPLIER`
90:   error UnwrapTooSmall();
91:
```

[89](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L89-L91)

---

### NatSpec: Event declarations should have `@notice` tags

`@notice` is used to explain to end users what the event emits, and the compiler interprets `///` or `/**` comments as this tag if one was't explicitly provided

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

141:   event rOUSGDeployed(
142:     address proxy,
143:     address proxyAdmin,
144:     address implementation,
145:     string name,
146:     string ticker
147:   );
```

[141](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141-L147)

---

### NatSpec: Event missing NatSpec `@dev` tag

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

160:    */
161:   event OracleSet(address indexed oldOracle, address indexed newOracle);
162:
```

[160](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L160-L162)

---

### NatSpec: Event missing NatSpec `@param` tag

<details>
<summary><i>There are 3 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/rOUSG.sol

/// @audit Missing @param for all event parameters
149:   event TransferShares(
150:     address indexed from,
151:     address indexed to,
152:     uint256 sharesValue
153:   );

/// @audit Missing @param for all event parameters
161:   event OracleSet(address indexed oldOracle, address indexed newOracle);
```

[149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L149-L153), [161](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L161)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

/// @audit Missing @param for `proxyAdmin`, `name`, `ticker`
141:   event rOUSGDeployed(
142:     address proxy,
143:     address proxyAdmin,
144:     address implementation,
145:     string name,
146:     string ticker
147:   );
```

[141](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L141-L147)

</details>

---

### NatSpec: Function declarations should have `@notice` tags

`@notice` is used to explain to end users what the function does, and the compiler interprets `///` or `/**` comments as this tag if one was't explicitly provided

<details>
<summary><i>There are 19 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

278:   function _mint(
279:     uint256 usdcAmountIn,
280:     address to
281:   ) internal returns (uint256 ousgAmountOut) {

388:   function _redeem(
389:     uint256 ousgAmountIn
390:   ) internal returns (uint256 usdcAmountOut) {

458:   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {

794:   function multiexcall(
795:     ExCallData[] calldata exCallData
796:   )
797:     external
798:     payable
799:     override
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
```

[278](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278-L281), [388](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388-L390), [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458), [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)

```solidity
📁 File: contracts/ousg/rOUSG.sol

102:   function initialize(
103:     address _kycRegistry,
104:     uint256 requirementGroup,
105:     address _ousg,
106:     address guardian,
107:     address _oracle
108:   ) public virtual initializer {

112:   function __rOUSG_init(
113:     address _kycRegistry,
114:     uint256 requirementGroup,
115:     address _ousg,
116:     address guardian,
117:     address _oracle
118:   ) internal onlyInitializing {

128:   function __rOUSG_init_unchained(
129:     address _kycRegistry,
130:     uint256 _requirementGroup,
131:     address _ousg,
132:     address guardian,
133:     address _oracle
134:   ) internal onlyInitializing {

166:   function name() public pure returns (string memory) {

181:   function decimals() public pure returns (uint8) {

188:   function totalSupply() public view returns (uint256) {

356:   function sharesOf(address _account) public view returns (uint256) {

363:   function getSharesByROUSG(
364:     uint256 _rOUSGAmount
365:   ) public view returns (uint256) {

373:   function getROUSGByShares(uint256 _shares) public view returns (uint256) {

378:   function getOUSGPrice() public view returns (uint256 price) {

487:   function _sharesOf(address _account) internal view returns (uint256) {

642:   function pause() external onlyRole(PAUSER_ROLE) {

646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {

650:   function setKYCRegistry(
651:     address registry
652:   ) external override onlyRole(CONFIGURER_ROLE) {

656:   function setKYCRequirementGroup(
657:     uint256 group
658:   ) external override onlyRole(CONFIGURER_ROLE) {
```

[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108), [112](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112-L118), [128](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128-L134), [166](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L166), [181](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L181), [188](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L188), [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356), [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363-L365), [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373), [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378), [487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L487), [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642), [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646), [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)

</details>

---

### NatSpec: Function declarations should have NatSpec descriptions

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as DeFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

<details>
<summary><i>There are 12 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

278:   function _mint(

388:   function _redeem(

458:   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {

794:   function multiexcall(
```

[278](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278), [388](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388), [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458), [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794)

```solidity
📁 File: contracts/ousg/rOUSG.sol

102:   function initialize(

112:   function __rOUSG_init(

128:   function __rOUSG_init_unchained(

378:   function getOUSGPrice() public view returns (uint256 price) {

642:   function pause() external onlyRole(PAUSER_ROLE) {

646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {

650:   function setKYCRegistry(

656:   function setKYCRequirementGroup(
```

[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102), [112](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112), [128](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128), [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378), [642](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L642), [646](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L646), [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650), [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656)

</details>

---

### NatSpec: Functions missing NatSpec `@dev` tag

<details>
<summary><i>There are 48 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

277:
278:   function _mint(
279:     uint256 usdcAmountIn,

387:
388:   function _redeem(
389:     uint256 ousgAmountIn

457:
458:   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
459:     require(

497:    */
498:   function setInstantMintLimit(
499:     uint256 _instantMintLimit

511:    */
512:   function setInstantRedemptionLimit(
513:     uint256 _instantRedemptionLimit

525:    */
526:   function setInstantMintLimitDuration(
527:     uint256 _instantMintLimitDuration

539:    */
540:   function setInstantRedemptionLimitDuration(
541:     uint256 _instantRedemptionLimitDuratioin

553:    */
554:   function setMintFee(
555:     uint256 _mintFee

566:    */
567:   function setRedeemFee(
568:     uint256 _redeemFee

580:    */
581:   function setMinimumDepositAmount(
582:     uint256 _minimumDepositAmount

598:    */
599:   function setMinimumRedemptionAmount(
600:     uint256 _minimumRedemptionAmount

621:    */
622:   function setMinimumBUIDLRedemptionAmount(
623:     uint256 _minimumBUIDLRedemptionAmount

637:    */
638:   function setOracle(
639:     address _oracle

649:    */
650:   function setFeeReceiver(
651:     address _feeReceiver

662:    */
663:   function setInvestorBasedRateLimiter(
664:     address _investorBasedRateLimiter

684:    */
685:   function _getMintAmount(
686:     uint256 usdcAmountIn,

698:    */
699:   function _getRedemptionAmount(
700:     uint256 ousgAmountBurned,

712:    */
713:   function _getInstantMintFees(
714:     uint256 usdcAmount

724:    */
725:   function _getInstantRedemptionFees(
726:     uint256 usdcAmount

767:   /// @notice Pause the mint functionality
768:   function pauseMint() external onlyRole(PAUSER_ROLE) {
769:     mintPaused = true;

773:   /// @notice Unpause the mint functionality
774:   function unpauseMint() external onlyRole(DEFAULT_ADMIN_ROLE) {
775:     mintPaused = false;

779:   /// @notice Pause the redeem functionality
780:   function pauseRedeem() external onlyRole(PAUSER_ROLE) {
781:     redeemPaused = true;

785:   /// @notice Unpause the redeem functionality
786:   function unpauseRedeem() external onlyRole(DEFAULT_ADMIN_ROLE) {
787:     redeemPaused = false;

793:   //////////////////////////////////////////////////////////////*/
794:   function multiexcall(
795:     ExCallData[] calldata exCallData

818:    */
819:   function retrieveTokens(
820:     address token,
```

[277](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L277-L279), [387](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L387-L389), [457](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L457-L459), [497](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L497-L499), [511](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L511-L513), [525](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L525-L527), [539](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L539-L541), [553](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L553-L555), [566](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L566-L568), [580](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L580-L582), [598](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L598-L600), [621](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L621-L623), [637](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L637-L639), [649](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L649-L651), [662](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L662-L664), [684](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L684-L686), [698](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L698-L700), [712](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L712-L714), [724](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L724-L726), [767](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L767-L769), [773](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L773-L775), [779](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L779-L781), [785](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L785-L787), [793](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L793-L795), [818](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L818-L820)

```solidity
📁 File: contracts/ousg/rOUSG.sol

97:   /// @custom:oz-upgrades-unsafe-allow constructor
98:   constructor() {
99:     _disableInitializers();

101:
102:   function initialize(
103:     address _kycRegistry,

111:
112:   function __rOUSG_init(
113:     address _kycRegistry,

127:
128:   function __rOUSG_init_unchained(
129:     address _kycRegistry,

165:    */
166:   function name() public pure returns (string memory) {
167:     return "Rebasing OUSG";

173:    */
174:   function symbol() public pure returns (string memory) {
175:     return "rOUSG";

180:    */
181:   function decimals() public pure returns (uint8) {
182:     return 18;

187:    */
188:   function totalSupply() public view returns (uint256) {
189:     return

301:    */
302:   function increaseAllowance(
303:     address _spender,

327:    */
328:   function decreaseAllowance(
329:     address _spender,

362:    */
363:   function getSharesByROUSG(
364:     uint256 _rOUSGAmount

372:    */
373:   function getROUSGByShares(uint256 _shares) public view returns (uint256) {
374:     return

377:
378:   function getOUSGPrice() public view returns (uint256 price) {
379:     (price, ) = oracle.getPriceData();

449:    */
450:   function _transfer(
451:     address _sender,

471:    */
472:   function _approve(
473:     address _owner,

486:    */
487:   function _sharesOf(address _account) internal view returns (uint256) {
488:     return shares[_account];

500:    */
501:   function _transferShares(
502:     address _sender,

528:    */
529:   function _mintShares(
530:     address _recipient,

641:
642:   function pause() external onlyRole(PAUSER_ROLE) {
643:     _pause();

645:
646:   function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
647:     _unpause();

649:
650:   function setKYCRegistry(
651:     address registry

655:
656:   function setKYCRequirementGroup(
657:     uint256 group
```

[97](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L97-L99), [101](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L101-L103), [111](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L111-L113), [127](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L127-L129), [165](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L165-L167), [173](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L173-L175), [180](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L180-L182), [187](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L187-L189), [301](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L301-L303), [327](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L327-L329), [362](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L362-L364), [372](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L372-L374), [377](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L377-L379), [449](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L449-L451), [471](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L471-L473), [486](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L486-L488), [500](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L500-L502), [528](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L528-L530), [641](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L641-L643), [645](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L645-L647), [649](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L649-L651), [655](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L655-L657)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

46:
47:   constructor(address _guardian) {
48:     guardian = _guardian;
```

[46](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L46-L48)

</details>

---

### NatSpec: Functions missing NatSpec `@param` tag

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as DeFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

<details>
<summary><i>There are 54 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

/// @audit Missing @param for `defaultAdmin`, `_usdcReciever`, `_feeReceiver`, `_ousgOracle`, `_buidlRedeemer`, `rateLimiterConfig`
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

/// @audit Missing @param for all function parameters
230:   function mint(
231:     uint256 usdcAmountIn
232:   )
233:     external
234:     override
235:     nonReentrant
236:     whenMintNotPaused
237:     returns (uint256 ousgAmountOut)
238:   {

/// @audit Missing @param for all function parameters
254:   function mintRebasingOUSG(
255:     uint256 usdcAmountIn
256:   )
257:     external
258:     override
259:     nonReentrant
260:     whenMintNotPaused
261:     returns (uint256 rousgAmountOut)
262:   {

/// @audit Missing @param for all function parameters
278:   function _mint(
279:     uint256 usdcAmountIn,
280:     address to
281:   ) internal returns (uint256 ousgAmountOut) {

/// @audit Missing @param for all function parameters
335:   function redeem(
336:     uint256 ousgAmountIn
337:   )
338:     external
339:     override
340:     nonReentrant
341:     whenRedeemNotPaused
342:     returns (uint256 usdcAmountOut)
343:   {

/// @audit Missing @param for all function parameters
362:   function redeemRebasingOUSG(
363:     uint256 rousgAmountIn
364:   )
365:     external
366:     override
367:     nonReentrant
368:     whenRedeemNotPaused
369:     returns (uint256 usdcAmountOut)
370:   {

/// @audit Missing @param for all function parameters
388:   function _redeem(
389:     uint256 ousgAmountIn
390:   ) internal returns (uint256 usdcAmountOut) {

/// @audit Missing @param for all function parameters
458:   function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {

/// @audit Missing @param for all function parameters
498:   function setInstantMintLimit(
499:     uint256 _instantMintLimit
500:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
512:   function setInstantRedemptionLimit(
513:     uint256 _instantRedemptionLimit
514:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
526:   function setInstantMintLimitDuration(
527:     uint256 _instantMintLimitDuration
528:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
540:   function setInstantRedemptionLimitDuration(
541:     uint256 _instantRedemptionLimitDuratioin
542:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
554:   function setMintFee(
555:     uint256 _mintFee
556:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
567:   function setRedeemFee(
568:     uint256 _redeemFee
569:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
581:   function setMinimumDepositAmount(
582:     uint256 _minimumDepositAmount
583:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
599:   function setMinimumRedemptionAmount(
600:     uint256 _minimumRedemptionAmount
601:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
622:   function setMinimumBUIDLRedemptionAmount(
623:     uint256 _minimumBUIDLRedemptionAmount
624:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

/// @audit Missing @param for all function parameters
650:   function setFeeReceiver(
651:     address _feeReceiver
652:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

/// @audit Missing @param for all function parameters
663:   function setInvestorBasedRateLimiter(
664:     address _investorBasedRateLimiter
665:   ) external override onlyRole(DEFAULT_ADMIN_ROLE) {

/// @audit Missing @param for `usdcAmountIn`
685:   function _getMintAmount(
686:     uint256 usdcAmountIn,
687:     uint256 price
688:   ) internal view returns (uint256 ousgAmountOut) {

/// @audit Missing @param for `ousgAmountBurned`
699:   function _getRedemptionAmount(
700:     uint256 ousgAmountBurned,
701:     uint256 price
702:   ) internal view returns (uint256 usdcOwed) {

/// @audit Missing @param for all function parameters
713:   function _getInstantMintFees(
714:     uint256 usdcAmount
715:   ) internal view returns (uint256) {

/// @audit Missing @param for all function parameters
725:   function _getInstantRedemptionFees(
726:     uint256 usdcAmount
727:   ) internal view returns (uint256) {

/// @audit Missing @param for all function parameters
737:   function _scaleUp(uint256 amount) internal view returns (uint256) {

/// @audit Missing @param for all function parameters
747:   function _scaleDown(uint256 amount) internal view returns (uint256) {

/// @audit Missing @param for all function parameters
794:   function multiexcall(
795:     ExCallData[] calldata exCallData
796:   )
797:     external
798:     payable
799:     override
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
```

[144](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144-L162), [230](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L230-L238), [254](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254-L262), [278](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278-L281), [335](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335-L343), [362](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362-L370), [388](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388-L390), [458](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L458), [498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498-L500), [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512-L514), [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526-L528), [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540-L542), [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554-L556), [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567-L569), [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581-L583), [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599-L601), [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622-L624), [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650-L652), [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L665), [685](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L685-L688), [699](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L699-L702), [713](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L713-L715), [725](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L725-L727), [737](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L737), [747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L747), [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)

```solidity
📁 File: contracts/ousg/rOUSG.sol

/// @audit Missing @param for all function parameters
102:   function initialize(
103:     address _kycRegistry,
104:     uint256 requirementGroup,
105:     address _ousg,
106:     address guardian,
107:     address _oracle
108:   ) public virtual initializer {

/// @audit Missing @param for all function parameters
112:   function __rOUSG_init(
113:     address _kycRegistry,
114:     uint256 requirementGroup,
115:     address _ousg,
116:     address guardian,
117:     address _oracle
118:   ) internal onlyInitializing {

/// @audit Missing @param for all function parameters
128:   function __rOUSG_init_unchained(
129:     address _kycRegistry,
130:     uint256 _requirementGroup,
131:     address _ousg,
132:     address guardian,
133:     address _oracle
134:   ) internal onlyInitializing {

/// @audit Missing @param for all function parameters
199:   function balanceOf(address _account) public view returns (uint256) {

/// @audit Missing @param for all function parameters
220:   function transfer(address _recipient, uint256 _amount) public returns (bool) {

/// @audit Missing @param for all function parameters
231:   function allowance(
232:     address _owner,
233:     address _spender
234:   ) public view returns (uint256) {

/// @audit Missing @param for all function parameters
251:   function approve(address _spender, uint256 _amount) public returns (bool) {

/// @audit Missing @param for all function parameters
276:   function transferFrom(
277:     address _sender,
278:     address _recipient,
279:     uint256 _amount
280:   ) public returns (bool) {

/// @audit Missing @param for all function parameters
302:   function increaseAllowance(
303:     address _spender,
304:     uint256 _addedValue
305:   ) public returns (bool) {

/// @audit Missing @param for all function parameters
328:   function decreaseAllowance(
329:     address _spender,
330:     uint256 _subtractedValue
331:   ) public returns (bool) {

/// @audit Missing @param for all function parameters
356:   function sharesOf(address _account) public view returns (uint256) {

/// @audit Missing @param for all function parameters
363:   function getSharesByROUSG(
364:     uint256 _rOUSGAmount
365:   ) public view returns (uint256) {

/// @audit Missing @param for all function parameters
373:   function getROUSGByShares(uint256 _shares) public view returns (uint256) {

/// @audit Missing @param for all function parameters
397:   function transferShares(
398:     address _recipient,
399:     uint256 _sharesAmount
400:   ) public returns (uint256) {

/// @audit Missing @param for all function parameters
415:   function wrap(uint256 _OUSGAmount) external whenNotPaused {

/// @audit Missing @param for all function parameters
431:   function unwrap(uint256 _rOUSGAmount) external whenNotPaused {

/// @audit Missing @param for all function parameters
450:   function _transfer(
451:     address _sender,
452:     address _recipient,
453:     uint256 _amount
454:   ) internal {

/// @audit Missing @param for all function parameters
472:   function _approve(
473:     address _owner,
474:     address _spender,
475:     uint256 _amount
476:   ) internal whenNotPaused {

/// @audit Missing @param for all function parameters
487:   function _sharesOf(address _account) internal view returns (uint256) {

/// @audit Missing @param for all function parameters
501:   function _transferShares(
502:     address _sender,
503:     address _recipient,
504:     uint256 _sharesAmount
505:   ) internal whenNotPaused {

/// @audit Missing @param for all function parameters
529:   function _mintShares(
530:     address _recipient,
531:     uint256 _sharesAmount
532:   ) internal whenNotPaused returns (uint256) {

/// @audit Missing @param for all function parameters
554:   function _burnShares(
555:     address _account,
556:     uint256 _sharesAmount
557:   ) internal whenNotPaused returns (uint256) {

/// @audit Missing @param for all function parameters
586:   function _beforeTokenTransfer(
587:     address from,
588:     address to,
589:     uint256
590:   ) internal view {

/// @audit Missing @param for all function parameters
650:   function setKYCRegistry(
651:     address registry
652:   ) external override onlyRole(CONFIGURER_ROLE) {

/// @audit Missing @param for all function parameters
656:   function setKYCRequirementGroup(
657:     uint256 group
658:   ) external override onlyRole(CONFIGURER_ROLE) {
```

[102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L102-L108), [112](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112-L118), [128](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128-L134), [199](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L199), [220](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L220), [231](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L231-L234), [251](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L251), [276](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L276-L280), [302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302-L305), [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328-L331), [356](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L356), [363](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L363-L365), [373](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L373), [397](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L397-L400), [415](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415), [431](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L431), [450](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L450-L454), [472](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L472-L476), [487](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L487), [501](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L501-L505), [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529-L532), [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554-L557), [586](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L586-L590), [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

/// @audit Missing @param for all function parameters
47:   constructor(address _guardian) {

/// @audit Missing @param for `kycRegistry`, `requirementGroup`
70:   function deployRebasingOUSG(
71:     address kycRegistry,
72:     uint256 requirementGroup,
73:     address ousg,
74:     address oracle
75:   ) external onlyGuardian returns (address, address, address) {

/// @audit Missing @param for all function parameters
121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {
```

[47](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L47), [70](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70-L75), [121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121-L123)

</details>

---

### NatSpec: Functions missing NatSpec `@return` tag

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as DeFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

<details>
<summary><i>There are 19 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

/// @audit Missing @return for all function parameters
230:   function mint(
231:     uint256 usdcAmountIn
232:   )
233:     external
234:     override
235:     nonReentrant
236:     whenMintNotPaused
237:     returns (uint256 ousgAmountOut)
238:   {

/// @audit Missing @return for all function parameters
254:   function mintRebasingOUSG(
255:     uint256 usdcAmountIn
256:   )
257:     external
258:     override
259:     nonReentrant
260:     whenMintNotPaused
261:     returns (uint256 rousgAmountOut)
262:   {

/// @audit Missing @return for all function parameters
278:   function _mint(
279:     uint256 usdcAmountIn,
280:     address to
281:   ) internal returns (uint256 ousgAmountOut) {

/// @audit Missing @return for all function parameters
335:   function redeem(
336:     uint256 ousgAmountIn
337:   )
338:     external
339:     override
340:     nonReentrant
341:     whenRedeemNotPaused
342:     returns (uint256 usdcAmountOut)
343:   {

/// @audit Missing @return for all function parameters
362:   function redeemRebasingOUSG(
363:     uint256 rousgAmountIn
364:   )
365:     external
366:     override
367:     nonReentrant
368:     whenRedeemNotPaused
369:     returns (uint256 usdcAmountOut)
370:   {

/// @audit Missing @return for all function parameters
388:   function _redeem(
389:     uint256 ousgAmountIn
390:   ) internal returns (uint256 usdcAmountOut) {

/// @audit Missing @return for all function parameters
685:   function _getMintAmount(
686:     uint256 usdcAmountIn,
687:     uint256 price
688:   ) internal view returns (uint256 ousgAmountOut) {

/// @audit Missing @return for all function parameters
699:   function _getRedemptionAmount(
700:     uint256 ousgAmountBurned,
701:     uint256 price
702:   ) internal view returns (uint256 usdcOwed) {

/// @audit Missing @return for all function parameters
713:   function _getInstantMintFees(
714:     uint256 usdcAmount
715:   ) internal view returns (uint256) {

/// @audit Missing @return for all function parameters
725:   function _getInstantRedemptionFees(
726:     uint256 usdcAmount
727:   ) internal view returns (uint256) {

/// @audit Missing @return for all function parameters
737:   function _scaleUp(uint256 amount) internal view returns (uint256) {

/// @audit Missing @return for all function parameters
747:   function _scaleDown(uint256 amount) internal view returns (uint256) {

/// @audit Missing @return for all function parameters
794:   function multiexcall(
795:     ExCallData[] calldata exCallData
796:   )
797:     external
798:     payable
799:     override
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
```

[230](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L230-L238), [254](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254-L262), [278](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L278-L281), [335](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335-L343), [362](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362-L370), [388](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L388-L390), [685](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L685-L688), [699](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L699-L702), [713](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L713-L715), [725](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L725-L727), [737](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L737), [747](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L747), [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)

```solidity
📁 File: contracts/ousg/rOUSG.sol

/// @audit Missing @return for all function parameters
302:   function increaseAllowance(
303:     address _spender,
304:     uint256 _addedValue
305:   ) public returns (bool) {

/// @audit Missing @return for all function parameters
328:   function decreaseAllowance(
329:     address _spender,
330:     uint256 _subtractedValue
331:   ) public returns (bool) {

/// @audit Missing @return for all function parameters
378:   function getOUSGPrice() public view returns (uint256 price) {

/// @audit Missing @return for all function parameters
529:   function _mintShares(
530:     address _recipient,
531:     uint256 _sharesAmount
532:   ) internal whenNotPaused returns (uint256) {

/// @audit Missing @return for all function parameters
554:   function _burnShares(
555:     address _account,
556:     uint256 _sharesAmount
557:   ) internal whenNotPaused returns (uint256) {
```

[302](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302-L305), [328](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L328-L331), [378](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378), [529](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529-L532), [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554-L557)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

/// @audit Missing @return for all function parameters
121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {
```

[121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121-L123)

</details>

---

### NatSpec: Modifier declarations should have NatSpec descriptions

It is recommended that modifiers are fully annotated using NatSpec.

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

149:   modifier onlyGuardian() {
```

[149](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L149)

---

### NatSpec: Modifier missing NatSpec `@dev` tag

<details>
<summary><i>There are 3 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

755:   /// @notice Ensure that the mint functionality is not paused
756:   modifier whenMintNotPaused() {
757:     require(!mintPaused, "OUSGInstantManager: Mint paused");

761:   /// @notice Ensure that the redeem functionality is not paused
762:   modifier whenRedeemNotPaused() {
763:     require(!redeemPaused, "OUSGInstantManager: Redeem paused");
```

[755](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L755-L757), [761](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L761-L763)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

148:
149:   modifier onlyGuardian() {
150:     require(msg.sender == guardian, "ROUSGFactory: You are not the Guardian");
```

[148](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L148-L150)

</details>

---

## 28. Non-`external`/`public` state variables should begin with an underscore

According to the Solidity Style Guide, Non-`external`/`public` state variables should begin with an <a href="https://docs.soliditylang.org/en/latest/style-guide.html#underscore-prefix-for-non-external-functions-and-variables">underscore</a>.

> ❗ Issue is removed from: (pech)

<i>There are 3 instaces of this issue:</i>

```solidity
📁 File: contracts/ousg/rOUSG.sol

/// @audit _shares
72:   mapping(address => uint256) private shares;

/// @audit _allowances
75:   mapping(address => mapping(address => uint256)) private allowances;

/// @audit _totalShares
78:   uint256 private totalShares;
```

[72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72), [75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75), [78](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L78)

---

## 29. Not using the latest versions of project dependencies

Update the project dependencies to their latest versions wherever possible.

Use tools such as `retire.js`, `npm audit`, and `yarn audit` to confirm that no vulnerable dependencies remain.

|        Dependency        | Current Version | Latest Version |
| :----------------------: | :-------------: | :------------: |
|       `forge-std`        |      1.5.3      |     1.8.1      |
| `openzeppelin-contracts` |      4.8.3      |     5.0.2      |

<i>There is one instance of this issue:</i>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

1: /**SPDX-License-Identifier: BUSL-1.1
```

[1](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L1)

---

## 30. Prefer skip over revert model in iteration

It is preferable to skip operations on an array index when a condition is not met rather than reverting the whole transaction as reverting can introduce the possiblity of malicous actors purposefully introducing array objects which fail conditional checks within for/while loops so group operations fail. As such it is recommended to simply skip such array indices over reverting unless there is a valid security or logic reason behind not doing so.

<details>
<summary><i>There are 2 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

/// @audit reverts on line: 808
804:     for (uint256 i = 0; i < exCallData.length; ++i) {
```

[804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

/// @audit reverts on line: 129
125:     for (uint256 i = 0; i < exCallData.length; ++i) {
```

[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)

</details>

---

## 31. Use `@inheritdoc` for overridden functions

<details>
<summary><i>There are 20 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

230:   function mint(
231:     uint256 usdcAmountIn
232:   )
233:     external
234:     override
235:     nonReentrant
236:     whenMintNotPaused
237:     returns (uint256 ousgAmountOut)
238:   {

254:   function mintRebasingOUSG(
255:     uint256 usdcAmountIn
256:   )
257:     external
258:     override
259:     nonReentrant
260:     whenMintNotPaused
261:     returns (uint256 rousgAmountOut)
262:   {

335:   function redeem(
336:     uint256 ousgAmountIn
337:   )
338:     external
339:     override
340:     nonReentrant
341:     whenRedeemNotPaused
342:     returns (uint256 usdcAmountOut)
343:   {

362:   function redeemRebasingOUSG(
363:     uint256 rousgAmountIn
364:   )
365:     external
366:     override
367:     nonReentrant
368:     whenRedeemNotPaused
369:     returns (uint256 usdcAmountOut)
370:   {

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
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
```

[230](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L230-L238), [254](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254-L262), [335](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335-L343), [362](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362-L370), [498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498-L500), [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512-L514), [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526-L528), [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540-L542), [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554-L556), [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567-L569), [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581-L583), [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599-L601), [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622-L624), [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638-L640), [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650-L652), [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L665), [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)

```solidity
📁 File: contracts/ousg/rOUSG.sol

650:   function setKYCRegistry(
651:     address registry
652:   ) external override onlyRole(CONFIGURER_ROLE) {

656:   function setKYCRequirementGroup(
657:     uint256 group
658:   ) external override onlyRole(CONFIGURER_ROLE) {
```

[650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {
```

[121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121-L123)

</details>

---

## 32. Use of `override` is unnecessary

Starting with Solidity version [0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), using the override keyword when the function solely overrides an interface function, and the function doesn't exist in multiple base contracts, is unnecessary.

<details>
<summary><i>There are 20 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

230:   function mint(
231:     uint256 usdcAmountIn
232:   )
233:     external
234:     override
235:     nonReentrant
236:     whenMintNotPaused
237:     returns (uint256 ousgAmountOut)
238:   {

254:   function mintRebasingOUSG(
255:     uint256 usdcAmountIn
256:   )
257:     external
258:     override
259:     nonReentrant
260:     whenMintNotPaused
261:     returns (uint256 rousgAmountOut)
262:   {

335:   function redeem(
336:     uint256 ousgAmountIn
337:   )
338:     external
339:     override
340:     nonReentrant
341:     whenRedeemNotPaused
342:     returns (uint256 usdcAmountOut)
343:   {

362:   function redeemRebasingOUSG(
363:     uint256 rousgAmountIn
364:   )
365:     external
366:     override
367:     nonReentrant
368:     whenRedeemNotPaused
369:     returns (uint256 usdcAmountOut)
370:   {

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
800:     onlyRole(DEFAULT_ADMIN_ROLE)
801:     returns (bytes[] memory results)
802:   {
```

[230](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L230-L238), [254](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254-L262), [335](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335-L343), [362](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362-L370), [498](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498-L500), [512](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512-L514), [526](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L526-L528), [540](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L540-L542), [554](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554-L556), [567](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567-L569), [581](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581-L583), [599](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599-L601), [622](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622-L624), [638](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638-L640), [650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650-L652), [663](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663-L665), [794](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794-L802)

```solidity
📁 File: contracts/ousg/rOUSG.sol

650:   function setKYCRegistry(
651:     address registry
652:   ) external override onlyRole(CONFIGURER_ROLE) {

656:   function setKYCRequirementGroup(
657:     uint256 group
658:   ) external override onlyRole(CONFIGURER_ROLE) {
```

[650](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L650-L652), [656](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L656-L658)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

121:   function multiexcall(
122:     ExCallData[] calldata exCallData
123:   ) external payable override onlyGuardian returns (bytes[] memory results) {
```

[121](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121-L123)

</details>

---

## 33. Variables need not be initialized to zero

The default value for variables is zero, so initializing them to zero is superfluous.

<details>
<summary><i>There are 4 instances of this issue:</i></summary>

```solidity
📁 File: contracts/ousg/ousgInstantManager.sol

99:   uint256 public mintFee = 0;

102:   uint256 public redeemFee = 0;

804:     for (uint256 i = 0; i < exCallData.length; ++i) {
```

[99](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L99), [102](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L102), [804](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L804)

```solidity
📁 File: contracts/ousg/rOUSGFactory.sol

125:     for (uint256 i = 0; i < exCallData.length; ++i) {
```

[125](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L125)

</details>

---

## 34. 
## Impact

`OUSG` & `rOUSG` tokens can not be instant minted under certain condition

## Proof of Concept

`OUSG` & `rOUSG` tokens can not be instant minted under certain situation: 1. `OUSGInstantManager.sol#minimumDepositAmount = 60_000e6; InstantMintTimeBasedRateLimiter.sol#instantMintLimit = 50_000e6;` 2. Alice tries to mint (deposit) `60_000e6`, but the mint function will revert, because in `InstantMintTimeBasedRateLimiter.sol#_checkAndUpdateInstantMintLimit()` function this check will revert (`60_000e6 < 50_000e6`):

```solidity
    require(
      amount <= instantMintLimit - currentInstantMintAmount,
      "RateLimit: Mint exceeds rate limit"
    );
```

The problem cause when `OUSGInstantManager.sol#minimumDepositAmount` is greater than `InstantMintTimeBasedRateLimiter.sol#instantMintLimit`.

The exact same issue exists and in redemption process.

Important to note that this situation and the issue overall is different from the instant mint/redeem flow.

## Tools Used

Manual Review

## Recommended Mitigation Steps

During the changing of `instantMintLimit` and `instantRedemptionLimit` doesn't allow to can be set with values smaller than `minimumDepositAmount` and `minimumRedemptionAmount`.
