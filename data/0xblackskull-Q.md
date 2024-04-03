[N-1] Remove redundant `whenNotPaused` modifier from `ROUSG::wrap()` and `ROUSG::unwrap()` becoz `whenNotPaused` modifier already present in  `ROUSG::_mintShares()` and `ROUSG::_burnShares()` respectively.
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L431-L443
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L415-L422

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L554-L557
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L529-L532

[N-2] Missing 0 amount check
    - for `ousgAmountIn > 0` in `OUSGInstantManager::redeem`
    https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L336C13-L336C25
    - for `rousgAmountIn > 0` in `OUSGInstantManager::redeemRebasingOUSG`
    https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L363
    - for `ousgAmountIn > 0` in `OUSGInstantManager::redeemRebasingOUSG`
    https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L379C29-L379C41


[N-3] `ROUSG::getOUSGPrice()` and `OUSGInstantManager::getOUSGPrice()` need to check price is current not old/stale price

[N-4] Admin can rug pull the contrack `OUSGInstantManager::retrieveTokens`, use multisig wallet
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L819-L825



