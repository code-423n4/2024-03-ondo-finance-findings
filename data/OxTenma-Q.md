# QA Findings of Ondo Finance

## [L-01] Oracle price in `rOUSG` contract isn't sanitized with `MINIMUM_OUSG_PRICE` as in `OUSGInstantManager` contract.
##### Details: 
The oracle returned by the oracle in `OUSGInstantManager` contract is correctly sanitized with `MINIMUM_OUSG_PRICE` but it is left unsanitized in the `rOUSG` contract, which may cause protocol to loss OUSG when the price goes below the minimum price OUSG than protocol decided price by `MINIMUM_OUSG_PRICE`.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378

```solidity 
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
  }
```

##### Recommendation
Add this require statement:
```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
@>  require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```
## [L-02] The upper limit of the oracle isn't checked.
##### Details
While `getOUSDPrice` functions for Oracle price perfectly account for lower limit of oracle price but upper limit wasn't checked properly which may lead protocol facing unwanted risk when the oracle price goes too above than a valid range.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479

```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    ); // @audit no upper limit
  }
```
##### Recommendation
Add a valid upper limit similar to minimum price. 

## [L-03] `setMinimumBUIDLRedemptionAmount` doesn't check if `_minimumRedemptionAmount` is lower than `FEE_GRANULARITY`
##### Details
The function `setMinimumBUIDLRedemptionAmount` should if the new buidl redemption amount is greater than `FEE_GRANULARITY` because `FEE_GRANULARITY` is divided each time fee is calculated, if not checked it will lead to 0 fee.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L622

```solidity
  function setMinimumBUIDLRedemptionAmount(
    uint256 _minimumBUIDLRedemptionAmount
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit MinimumBUIDLRedemptionAmountSet(
      minBUIDLRedeemAmount,
      _minimumBUIDLRedemptionAmount
    );
    minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
  }
```
##### Recommendation
The function `setMinimumRedemptionAmount` in the contract perfectly check this statement. To fix it similarly, add this line: 
```solidity
require(
      _minimumRedemptionAmount >= FEE_GRANULARITY,
      "setMinimumRedemptionAmount: Amount too small"
    );
```


## [L-04] Frontrunning the KYC de-allocation functionality will allow users from being redeeming/minting/burning/transfering shares. 
##### Details
If Ondo team changes the KYC status of user to false then she/he can frontrun the transaction and perform redeeming/minting/burning/transferring shares functions before his/her KYC de-allocation.

`_beforeTokenTransfer` is called before `mint`, `burn`, `transferShares` functions in `ROUSG` contract.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L586

```solidity
  function _beforeTokenTransfer(
    address from,
    address to,
    uint256
  ) internal view {
    // Check constraints when `transferFrom` is called to facliitate
    // a transfer between two parties that are not `from` or `to`.
    if (from != msg.sender && to != msg.sender) {
      //  can send to msg.sender to msg.sender
      require(_getKYCStatus(msg.sender), "rOUSG: 'sender' address not KYC'd");
    }

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

##### Recommendation 
Make sure when user perform redeeming/minting/burning/transferring shares, there is a delay before performing the functions again so that Ondo Team can set KYC status of user to false.


## [L-05] Centralization Risk on `retrieveTokens` function 
##### Details
The function `retrieveTokens` can drain the all the tokens to a admin controlled address which is a definite centralization risk for its user.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819

```solidity
  function retrieveTokens(
    address token,
    address to,
    uint256 amount
  ) external onlyRole(DEFAULT_ADMIN_ROLE) {
    IERC20(token).transfer(to, amount);
    // @audit Centralization risk [low]
  }
```

##### Recommendation 
Remove the function to avoid the risk.

## [L-06] Use `safeMint` instead of `mint`
##### Details
`_mint()` is discouraged in favor of _safeMint() which ensures that the recipient is either an EOA or implements IERC721Receiver. Both OpenZeppelin and solmate have versions of this function so that NFTs aren't lost if they're minted to contracts that cannot transfer them back out.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L323

```solidity

  function _mint(
    uint256 usdcAmountIn,
    address to
  ) internal returns (uint256 ousgAmountOut) {
    require(
      IERC20Metadata(address(usdc)).decimals() == 6,
      "OUSGInstantManager::_mint: USDC decimals must be 6"
    );
    ...
    ...
    ousg.mint(to, ousgAmountOut); // use safemint instead of mint. @audit

  }

```
##### Recommendation 
Use OpenZeppelin's `_safeMint`

## [L-07] Missing contract existence checks before low-level calls
##### Details
Before calling a low level call to a contract it should check the if contract code exists or not. 

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794
	
```solidity
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
@>      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);

      require(success, "Call Failed");
      results[i] = ret;
    }
  }
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L121

```solidity
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

## [NC-01] Use newer solidity version than 0.8.16 
##### Details
Upgrading to a newer Solidity release can optimize gas usage, take advantage of new features and improve overall contract efficiency. Where possible, based on compatibility requirements, it is recommended to use newer/latest solidity version to take advantage of the latest optimizations and features.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L16

```solidity
pragma solidity 0.8.16;
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L16

```solidity
pragma solidity 0.8.16;
```

##### Recommendation 
Use latest version of solidity which is above 0.8.20

## [NC-02] Custom errors should be used rather than revert()/require()	
##### Details
According to Solidity doc, it is not recommended to use `assert()`
> Assert should only be used to test for internal errors, and to check invariants. Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94

```solidity
assert(rOUSGProxyAdmin.owner() == guardian);
```
##### Recommendation 
Use `require/revert` instead of `assert`

## [NC-03] NatSpec documentation for function is missing
##### Details	
It is recommended to use natspec documentation for function. It is missing in the `multiexcall` function of `OUSGInstantManager` contract.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L794

```solidity
  /*//////////////////////////////////////////////////////////////
                          Miscellaneous
  //////////////////////////////////////////////////////////////*/
  // @audit missing natspac [nc]
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
##### Recommendation
Add natspec documenation so that developers can understand the function properly.

## [NC-04] Contract name does not follow the Solidity Style Guide
##### Details
According to the Solidity Style Guide, contracts and libraries should be named using the CapWords style and match their filenames.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L55

```solidity 
contract ROUSG is
```
##### Recommendation
Should change the contract name to `Rousg` instead.

## [NC-05] Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard.
##### Details
Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks opens the users of this protocol up to read-only reentrancy vulnerability with no way to protect them except by block-listing the entire protocol.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L431

```
  function unwrap(uint256 _rOUSGAmount) external whenNotPaused {
    ...
  }
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415

```
 function wrap(uint256 _OUSGAmount) external whenNotPaused {
    require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");
    ...
 }
```

##### Recommendation
Use `nonReentrant` Modifier of Openzeppelin in both of these two function.

## [NC-06] Commented code section should be deleted.
##### Details
Remove unnecessary commented code section should be deleted.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L608C1-L661C2

```solidity
  /**
   * @notice Sets the Oracle address
   * @dev The new oracle must comply with the IRWAOracle interface
   * @param _oracle Address of the new oracle
   */
  function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }

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

  function pause() external onlyRole(PAUSER_ROLE) {
    _pause();
  }

  function unpause() external onlyRole(DEFAULT_ADMIN_ROLE) {
    _unpause();
  }

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

## [NC-07] Typos
##### Details
The comment in this natspec is incorrect. It should be 
>* @dev Balances are dynamic and equal *to* the `_account`'s OUSG shares multiplied

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L196

```solidity
  /**
   * @return the amount of tokens owned by the `_account`.
   *
   * @dev Balances are dynamic and equal the `_account`'s OUSG shares multiplied
   *      by the price of OUSG // @audit typo
   */
  function balanceOf(address _account) public view returns (uint256) {
    return
      (_sharesOf(_account) * getOUSGPrice()) /
      (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
  }
```

## [NC-08] whenNotPaused modifier in `_mintShare` is unnecessary as it is there with `wrap()` function.

##### Details
As we see these two functions `warp` and `_mintShares` are enforcing same `whenNotPaused` modifier which is unnecessary. We can remove the modifier from the `_mintShares` function.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415

`warp`:
```solidity
function wrap(uint256 _OUSGAmount) external whenNotPaused {
    require(_OUSGAmount > 0, "rOUSG: can't wrap zero OUSG tokens");

    ...
}
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529

`_mintShares`:
```solidity
function _mintShares(
    address _recipient,
    uint256 _sharesAmount
@>  ) internal whenNotPaused returns (uint256) {
    require(_recipient != address(0), "MINT_TO_THE_ZERO_ADDRESS");
}
```
##### Recommendation
Remove the `whenNotPaused` in `_mintShares` function.

## [NC-09] Specific parameters should be imported instead of all parameters of a contract
##### Details
When importing from other contracts, specific parameters which are used in the contract that imports should be taken from the contract. It is risky to import all the parameters of a contract.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L18C1-L26C46

```
import "contracts/external/openzeppelin/contracts/token/IERC20.sol";
import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20Upgradeable.sol";
import "contracts/external/openzeppelin/contracts-upgradeable/token/ERC20/IERC20MetadataUpgradeable.sol";
import "contracts/external/openzeppelin/contracts-upgradeable/proxy/Initializable.sol";
import "contracts/external/openzeppelin/contracts-upgradeable/utils/ContextUpgradeable.sol";
import "contracts/external/openzeppelin/contracts-upgradeable/security/PausableUpgradeable.sol";
import "contracts/external/openzeppelin/contracts-upgradeable/access/AccessControlEnumerableUpgradeable.sol";
import "contracts/kyc/KYCRegistryClientUpgradeable.sol";
import "contracts/rwaOracles/IRWAOracle.sol";
```

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L18C1-L27C61

```
import "contracts/external/openzeppelin/contracts/access/AccessControlEnumerable.sol";
import "contracts/external/openzeppelin/contracts/security/ReentrancyGuard.sol";
import "contracts/external/openzeppelin/contracts/token/IERC20Metadata.sol";
import "contracts/ousg/rOUSG.sol";
import "contracts/interfaces/IRWALike.sol";
import "contracts/interfaces/IBUIDLRedeemer.sol";
import "contracts/InstantMintTimeBasedRateLimiter.sol";
import "contracts/interfaces/IOUSGInstantManager.sol";
import "contracts/interfaces/IMulticall.sol";
import "contracts/interfaces/IInvestorBasedRateLimiter.sol";
```
