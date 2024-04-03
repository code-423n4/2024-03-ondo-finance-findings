## L-01 Admin setter functions can be misused due to lack of explicit sanity checks

The setMintFee and setRedeemFee functions allow an admin to set fees for minting and redeeming operations. While there's a basic check `require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");`, it's relatively loose and only ensures that fees are below 200 basis points (2%). There's a risk that fees could be set unreasonally high within the allowed range, potentially deterring users from engaging with the contract or eroding trust.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554

```solidity
function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
    emit MintFeeSet(mintFee, _mintFee);
    mintFee = _mintFee;
  }
```
### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567

```solidity
function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
    emit RedeemFeeSet(redeemFee, _redeemFee);
    redeemFee = _redeemFee;
  }
```

The setMinimumDepositAmount and setMinimumRedemptionAmount functions enforce minimum amounts for deposits and redemptions. The only check is that the set amounts are not too small, compared to a granularity constant. If set too high, these minimums could lock out smaller investors or create barriers to entry. Conversely, if set too low, they might not effectively mitigate spam or dust transactions.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L581

```solidity
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
```

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L599

```solidity
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

```

The setInstantMintLimit and setInstantRedemptionLimit settings control the total USDC that can be minted or redeemed within certain intervals. The contract does not enforce specific sanity checks beyond the role-based access control. Incorrectly configured limits could either halt normal contract operation by being too restrictive or fail to prevent abuse by being too lenient.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L498

```solidity
function setInstantMintLimit(
    uint256 _instantMintLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setInstantMintLimit(_instantMintLimit);
  }
```

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512

```solidity
function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setInstantRedemptionLimit(_instantRedemptionLimit);
  }
```

The contract allows changing the oracle address without specifying checks on the new oracle's validity or its response consistency. Setting an incorrect or malicious oracle could lead to wrong pricing information, affecting all minting and redeeming operations.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638

```solidity
function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }
```

The setFeeReceiver function sets the address that receives minting and redemption fees. The only check is that the new address is not the zero address. If the fee receiver is set to a non-recoverable address by mistake, accumulated fees would be lost. If set to a malicious address, it could potentially redirect funds.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650

```solidity
function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
    emit FeeReceiverSet(feeReceiver, _feeReceiver);
    feeReceiver = _feeReceiver;
  }
```



## L-02 Lack of User-defined Slippage in Mint and Redeem Operations

This contract does not provide users the option to set such minimums for the amount of OUSG/rOUSG they receive when minting or the amount of USDC they receive when redeeming.

The amount received from minting or redeeming operations is strictly based on the current oracle price. While the oracle price ensures a reference to market value, it does not protect users from slippage caused by market volatility in the short period between transaction initiation and execution.

Allows users to define slippage thresholds they are comfortable with or implement dynamic slippage control mechanisms.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L230

```solidity
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
```

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L254

```solidity
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
```

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L335

```solidity
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
```

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362

```solidity
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
```

## L-03 Lack of Explicit Balance Checks Before Token Transfers

The contract lacks explicit checks right before executing asset transfers to ensure that the amount being redeemed is not less than expected due to potential contract balance issues. This could lead to situations where the contract might attempt to transfer more assets than it holds, leading to transaction failures.

While the contract takes measures to ensure the logical correctness of redemption amounts through fees, minimum amounts, and oracle prices, it does not explicitly verify its ability to fulfill these redemptions by checking its balance of USDC (or BUIDL for BUIDL redemptions) immediately before executing the transfer.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L455

```solidity
usdc.transfer(msg.sender, usdcAmountOut);
```
### Mitigation
Check that the contract has enough USDC to cover the fees and redemption amount.

Change to:

```solidity
    uint256 contractUSDCBalance = usdc.balanceOf(address(this));
    require(contractUSDCBalance >= usdcFees + usdcAmountOut, "OUSGInstantManager::_redeem: Insufficient USDC balance for redemption");

    if (usdcFees > 0) {
        usdc.transfer(feeReceiver, usdcFees);
    }
    
    usdc.transfer(msg.sender, usdcAmountOut);

```


## L-04 Misspelled variable name will lead to confusion and inconsistency

The variable _usdcReciever is misspelled. It should be _usdcReceiver for clarity and consistency.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L147

```solidity
address _usdcReciever,
```


## L-05 Lack of Interface Support Checks

The constructor assumes the passed addresses implement certain interfaces (IERC20, IERC20Metadata, IRWAOracle, IRWALike, ROUSG, IBUIDLRedeemer). There's no explicit on-chain check to ensure these contracts implement the expected interfaces e.g using ERC-165.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L22C1-L28C1

```solidity
import "contracts/interfaces/IRWALike.sol";
import "contracts/interfaces/IBUIDLRedeemer.sol";
import "contracts/InstantMintTimeBasedRateLimiter.sol";
import "contracts/interfaces/IOUSGInstantManager.sol";
import "contracts/interfaces/IMulticall.sol";
import "contracts/interfaces/IInvestorBasedRateLimiter.sol";
```

## L-06 Optimize the Mint Events with more Context

The MintFeesDeducted event is helpful for tracking fee deductions. It might also be beneficial to include the net amount of USDC used for minting (usdcAmountAfterFee) and the amount of OUSG minted (ousgAmountOut) in the event logs for complete transparency and auditability of the minting 

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L321

```solidity
emit MintFeesDeducted(msg.sender, feeReceiver, usdcfees, usdcAmountIn);
```

## L-07 Allowance Check Redundancy

The contract checks that the allowance the user has set for the contract is at least usdcAmountIn. This is good practice, but it's worth noting that transferFrom will automatically revert if the allowance is insufficient. Thus, while this check makes the requirement explicit and potentially provides a clearer error message, it might be seen as redundant by some, since the ERC-20 transferFrom function inherently checks for sufficient allowance.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L299

```solidity
require(
      usdc.allowance(msg.sender, address(this)) >= usdcAmountIn,
      "OUSGInstantManager::_mint: Allowance must be given to OUSGInstantManager"
    );
```

## L-08 Extend Sanity Check scope for getOUSGPrice to include extremely high prices

The sanity check ensures the price is not below MINIMUM_OUSG_PRICE, which is a good practice to avoid erroneous or manipulated data affecting the system. However, depending on the system's requirements, it might also be prudent to check for excessively high prices 

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479

```solidity
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

## L-09 Lack of Granular Error Handling of Failed Batch operations in multiexcall function

Instead of requiring all calls to succeed, you can modify the function to return a success or failure flag for each call alongside the return data. This approach allows the caller to identify which calls failed and which succeeded, making debugging easier.

For more sophisticated error handling, Solidity 0.8.x introduces custom error types. You can define custom errors for different failure modes in multiexcall and throw these errors accordingly. This method is gas-efficient and provides clear and concise error messages.

### Loc
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
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }
```
### Loc
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

### Mitigation

```solidity
function multiexcall(ExCallData[] calldata exCallData)
    external
    payable
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bool[] memory success, bytes[] memory results)
{
    uint256 length = exCallData.length;
    success = new bool[](length);
    results = new bytes[](length);

    for (uint256 i = 0; i < length; ++i) {
        (success[i], results[i]) = address(exCallData[i].target).call{
            value: exCallData[i].value
        }(exCallData[i].data);
    }
}


```

## L-10 Missing address zero validations in deployRebasingOUSG

Verify that the addresses passed as parameters (kycRegistry, ousg, oracle) are valid (i.e., not the zero address). This is a common check to avoid mistakes or malicious inputs:

*Instances missed by bot*

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70

```solidity
require(kycRegistry != address(0), "ROUSGFactory: KYC Registry address is invalid");
require(ousg != address(0), "ROUSGFactory: OUSG address is invalid");
require(oracle != address(0), "ROUSGFactory: Oracle address is invalid");
```

## L-11 Parameterize the Guardian Address in deployRebasingOUSG

To make the function more flexible and explicit, consider adding guardian as a function parameter. This makes the deployment function more transparent and adaptable to different guardian addresses without requiring modifications to contract state or assumptions about external variables.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L70

```solidity
function deployRebasingOUSG(
  address kycRegistry,
  uint256 requirementGroup,
  address ousg,
  address oracle,
  address guardian // Newly added parameter
)
```

## L-12 increaseAllowance/decreaseAllowance are Susceptible to Phishing Attacks

The increaseAllowance and decreaseAllowance functions are part of the ERC-20 token standard extensions that allow token holders to safely adjust the allowance they've granted to a third party. However, if not properly managed, these functions can be susceptible to phishing attacks, especially in scenarios where users are tricked into approving transactions that adjust allowances in ways they did not intend.

*Different issue from issue specified by bot*

See here: [Discussion to remove increaseAllowance and decreaseAllowance from ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/4583)

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L302

## L-13 Lack of Max Mint Amount Validation

While there's a check for a minimum deposit amount, there doesn't appear to be a check for a maximum mint amount. Such a limit could prevent excessively large mints that could impact the token's economics or liquidity.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L286

```solidity
require(
      usdcAmountIn >= minimumDepositAmount,
      "OUSGInstantManager::_mint: Deposit amount too small"
    );
```

## L-14 Add checks for Stale Oracle Prices

If the getOUSGPrice function relies on external data or an oracle, it's important to ensure that the price data is fresh. This could involve checking the timestamp of the last update and ensuring it's within an acceptable range to prevent price manipulation or stale data usage.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479

```solidity
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

## L-15 Implement fallback mechanism in case of oracle failure

The getOUSGPrice function currently does not handle potential failures in calling the oracle (e.g., if the oracle contract does not respond or returns invalid data). Implementing a fallback mechanism or error handling can prevent the function from failing silently or becoming unusable in case of oracle issues.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479

```solidity
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

## L-16 Add Excessive Volatility Check in getOUSGPrice

While the getOUSGPrice function checks for the price not being too low, it might also be beneficial to check for signs of excessive volatility or unrealistic price spikes that could indicate market manipulation or oracle issues.

### Loc

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479

```solidity
function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

## L-17 Consider Implementing whitelists and blacklists for Configuration settings involving addresses

Whitelists allow you to specify which addresses are permitted to perform certain actions, enhancing security by restricting access to trusted entities. Blacklists, conversely, enable you to block addresses from performing actions, providing a mechanism to respond to malicious activity or comply with regulatory requirements. Incorporating these lists into configuration settings can mitigate risks and provide better control over your contract's operations. This will also further safeguard against malicious settings by compromised admin.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638

```solidity
function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }
```

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650

```solidity
function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
    emit FeeReceiverSet(feeReceiver, _feeReceiver);
    feeReceiver = _feeReceiver;
  }
```
### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663

```solidity
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
```

### Mitigtion

To address the issue, you can implement whitelists and blacklists for critical functions within your contract, such as setting configuration parameters or performing minting and redeeming operations. Here's an approach to integrate these lists into your contract:

First, define storage variables to hold your whitelists and blacklists. Use `mapping(address => bool)` to efficiently check if an address is included.

```solidity
mapping(address => bool) private _whitelist;
mapping(address => bool) private _blacklist;
```

Create modifiers to check if an address is whitelisted or not blacklisted. These modifiers can be applied to functions to enforce restrictions.

```solidity
modifier onlyWhitelisted() {
    require(_whitelist[msg.sender], "Not whitelisted");
    _;
}

modifier notBlacklisted() {
    require(!_blacklist[msg.sender], "Blacklisted");
    _;
}
```

Provide functions to manage these lists, allowing addresses with the appropriate roles to add or remove addresses. Ensure you're following the principle of least privilege, allowing only trusted roles to modify these lists.

```solidity
function addToWhitelist(address _address) external onlyRole(DEFAULT_ADMIN_ROLE) {
    _whitelist[_address] = true;
}

function removeFromWhitelist(address _address) external onlyRole(DEFAULT_ADMIN_ROLE) {
    _whitelist[_address] = false;
}

function addToBlacklist(address _address) external onlyRole(DEFAULT_ADMIN_ROLE) {
    _blacklist[_address] = true;
}

function removeFromBlacklist(address _address) external onlyRole(DEFAULT_ADMIN_ROLE) {
    _blacklist[_address] = false;
}
```

Apply the `onlyWhitelisted` and `notBlacklisted` modifiers to sensitive functions, such as those changing configuration settings or handling minting and redeeming operations.

```solidity
function setFeeReceiver(address _feeReceiver) external onlyRole(DEFAULT_ADMIN_ROLE) onlyWhitelisted notBlacklisted {
    require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
    emit FeeReceiverSet(feeReceiver, _feeReceiver);
    feeReceiver = _feeReceiver;
}
```


## L-18 Dynamically update Rate Limits and Fees based on market conditions instead of admin control only

Oracles can supply the contract with real-time data about market conditions, such as volatility indices, transaction volumes, or asset prices. By integrating oracles, you can adjust rate limits and fees dynamically based on this data.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L554

```solidity
function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
    emit MintFeeSet(mintFee, _mintFee);
    mintFee = _mintFee;
  }
```

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L567

```solidity
function setRedeemFee(
    uint256 _redeemFee
  ) external override onlyRole(CONFIGURER_ROLE) {
    require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
    emit RedeemFeeSet(redeemFee, _redeemFee);
    redeemFee = _redeemFee;
  }
```

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L512

```solidity
function setInstantRedemptionLimit(
    uint256 _instantRedemptionLimit
  ) external override onlyRole(CONFIGURER_ROLE) {
    _setInstantRedemptionLimit(_instantRedemptionLimit);
  }
```

## L-19 Lack of Emergency Withdrawal Mechanism for Users 

Integrating an emergency withdrawal mechanism allows users to retrieve their assets in unforeseen circumstances, enhancing trust and security within your smart contract environment. This feature is particularly crucial in decentralized finance (DeFi) applications, where user funds should remain accessible even if the smart contract's primary functions become compromised or if there's a significant bug.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L49

## L-20 Compromised admin can grant critical roles to malicious addresses unchecked

If an administrator's account becomes compromised, malicious actors could gain unfettered access to sensitive functionalities of the smart contract, leading to potential abuse, theft, or irreparable damage to the system. The risk is significantly heightened in scenarios where a compromised admin can, without checks or balances, grant critical roles to other addresses, including those controlled by attackers.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L638

```solidity
function setOracle(
    address _oracle
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }
```

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L650

```solidity
function setFeeReceiver(
    address _feeReceiver
  ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
    require(_feeReceiver != address(0), "FeeReceiver cannot be 0x0");
    emit FeeReceiverSet(feeReceiver, _feeReceiver);
    feeReceiver = _feeReceiver;
  }
```
### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L663

```solidity
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
```

### Mitigation
Introduce a timelock mechanism for sensitive administrative operations. When a role assignment is initiated, there's a mandatory delay before the action can be finalized. This delay provides an observation window during which malicious actions can be identified and potentially reverted by other administrators

## L-21 Utilize EIP-2612 Permits for Approvals

EIP-2612 introduces the permit function, allowing token holders to approve spending via signatures. This method can potentially reduce phishing risks by eliminating the need for users to directly interact with potentially malicious contract functions for approving tokens.

### Loc
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L251

```solidity
function approve(address _spender, uint256 _amount) public returns (bool) {
    _approve(msg.sender, _spender, _amount);
    return true;
  }
```
