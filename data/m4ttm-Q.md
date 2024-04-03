Low/QA/NC

### DEFAULT_ADMIN_ROLE never used in ROUSGFactory

`ROUSGFactory` declares a `DEFAULT\_ADMIN\_ROLE` but this is never used and the contract does not use role based access control at all. Consider removing this.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSGFactory.sol#L38

```solidity
bytes32 public constant DEFAULT_ADMIN_ROLE = bytes32(0);
```

### Incorrect Event Parameters

When `ROUSG` is being burned with `burn`, a `Transfer` event with incorrect parameters is emitted. Currently the code is:

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L638

```solidity
emit Transfer(address(0), msg.sender, getROUSGByShares(ousgSharesAmount));
```

However, this should be:

```solidity
emit Transfer(_account, address(0), getROUSGByShares(ousgSharesAmount));
```

### Add burnShares function in addition to the existing burn function

`ROUSG` currently has a permissioned function for a burner to burn any account's tokens, however since the balance is represented internally by shares it is not possible to fully clear a balance due to precision errors. Consider adding a `burnShares` function to allow a users shares to be fully burned.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L624-L640

### UUPS is recommended over transparent proxy

`ROUSGFactory` uses the Transparent Proxy Pattern but OpenZeppelin's current recommendation is UUPS over the Transparent Proxy Pattern which is an older design.

[https://docs.openzeppelin.com/contracts/4.x/api/proxy#:~:text=Transparent vs UUPS Proxies,-The original proxies&text=While both of these share,logic in the proxy itself](https://docs.openzeppelin.com/contracts/4.x/api/proxy#:~:text=Transparent%20vs%20UUPS%20Proxies,-The%20original%20proxies&text=While%20both%20of%20these%20share,logic%20in%20the%20proxy%20itself).

### Calls to parent initialiser should be in `__rOUSG_init` not `__rOUSG_init_unchained`

When using upgradable contracts, calls to the parent initialisers should go in the \_init method with only the contract specific logic going in the \_init_unchained method. These two methods are supposed to separate the logic which would usually go in the constructor header and constructor body.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L128-L142

```solidity
function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
    __KYCRegistryClientInitializable_init(_kycRegistry, _requirementGroup);
    ousg = IERC20(_ousg);
    oracle = IRWAOracle(_oracle);
    _grantRole(DEFAULT_ADMIN_ROLE, guardian);
    _grantRole(PAUSER_ROLE, guardian);
    _grantRole(BURNER_ROLE, guardian);
    _grantRole(CONFIGURER_ROLE, guardian);
  }
```

### Redundant require statements

Redudant require statements are abundant throughout the codebase, where the code would revert further along its path and no new cases are caught. Consider removing these:

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L282

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L333-L336

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L477

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L512-L515

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L563

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L298-L301

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L344-L347

### Redundant `whenNotPaused` modifier

The use of `whenNotPaused` on `wrap` and `unwrap` is redundant since they call `_mintShares` and `_burnShares` respectively, which also use this modifier.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L415

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L431

### Make totalShares a public variable and remove public getter function

`totalShares` is a private variable and has a public getter `getTotalShares`. Consider making `totalShares` public and removing the getter.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L347-L349

### Use y+=x not y=y+x

Prefer the use of `y+=x` over `y=y+x` due to readability.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L518

### Unneccassary decimals check for USDC and BUIDL

Decimals are checked on `USDC` and `BUIDL` before every redemption, this should not be necessary because these are not intended to change.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L391-L398

### retrieveTokens is redundant since the admin can already perform abitrary external calls

`OUSGInstantManager` has a `retrieveTokens` for the admin to rescue any ERC20 functions from the contract but since the admin can already perform any arbitrary external calls with `multiexcall` this is redundant. Consider removing this.

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L819-L825

### Refactor to remove duplicated logic

Duplicated code exists in several places, this could be refactored to only exist in a single place.

- In `ROUSG`, `totalSupply` and `balanceOf` could make use of `getROUSGByShares` instead of reimplementing calculation logic.
- In `ROUSG`, `burn` duplicates logic from `unwrap` which could go in a single `_unwrap function`.
- `OUSG_TO_ROUSG_SHARES_MULTIPLIER` is a constant used twice, this could be declared in a single contract which is inherited from.
- `multiexcall` is a function written twice, this could be inherited from a single contract