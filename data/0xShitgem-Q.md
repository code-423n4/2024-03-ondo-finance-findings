# [L01] - Pausable mechanism is not initialized inside `rOUSG`
rOusg is meant to be an upgradeable rebase ERC20 token. It uses a pausable mechanism, however inside `__rOUSG_init_unchained` it's not initialized.

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

#### Mitigation
Add `__Pausable_init()`

```diff
function __rOUSG_init_unchained(
    address _kycRegistry,
    uint256 _requirementGroup,
    address _ousg,
    address guardian,
    address _oracle
  ) internal onlyInitializing {
    __KYCRegistryClientInitializable_init(_kycRegistry, _requirementGroup);
+   __Pausable_init();
    ousg = IERC20(_ousg);
    oracle = IRWAOracle(_oracle);
    _grantRole(DEFAULT_ADMIN_ROLE, guardian);
    _grantRole(PAUSER_ROLE, guardian);
    _grantRole(BURNER_ROLE, guardian);
    _grantRole(CONFIGURER_ROLE, guardian);
  }
```

Code Snippet:
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/rOUSG.sol#L128-L143

# [L-02] Checks for decimals of tokens should be made inside the constructor
Inside a couple of functions (snippets below), protocol checks if USDC and BUIDL have decimals as `6`. However, when the protocol is deployed with different decimals for those tokens, almost the entire protocol is unusable. It's better to do this inside the constructor.

#### Mitigation
Instead checking for decimals inside functions - check it inside constructor

Code Snippets:
https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L391-L398

https://github.com/code-423n4/2024-03-ondo-finance/blob/be2e9ebca6fca460c5b0253970ab280701a15ca1/contracts/ousg/ousgInstantManager.sol#L282-L285

# [NC-01] Change `keccak256("BURN_ROLE")` to `keccak256("BURNER_ROLE")`
Inside `rOUSG.sol` BURNER_ROLE is set as `keccak256("BURN_ROLE")`. However inside `ousg.sol` - `keccak256("BURNER_ROLE")`

Change to keep variables the same.








