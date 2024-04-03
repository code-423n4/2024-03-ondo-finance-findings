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

