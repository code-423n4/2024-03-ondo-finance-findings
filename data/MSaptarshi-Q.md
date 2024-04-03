# [L-01] Emit events before externall cals
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L350
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L380

# Recommendation
Always emit events before external calls

# [L-02] Missing calls to base initializers in rOUSG
https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L112

The _rOUSG_INIT() function doesn't call the initializers for some of the base contracts:
> Initializable 

> ContextUpgradable

> PausableUpgradable

> AccessControlUpgradable