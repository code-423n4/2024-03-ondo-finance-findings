## [LOW] Check KYCStatus of 'spender' and 'msg.sender' in function rOUSG.sol::approve()

## Instances(1)

If KYCStatus of 'spender' and 'msg.sender' is not checked and get stored in mapping allowances it is a waste of storage and transaction as when 'spender' tries to transfer from owner transaction will revert because of KYCStatus checking in rOUSG.sol::__beforeTokenTransfer(). 

https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/rOUSG.sol#L251C1-L254C4

## Recommendation
It is recommended to check KYCStatus at rOUSG.sol::approve() before storing it in mapping allowances so that user's transactions won't wasted.

Should add these lines in rOUSG.sol::approve()

require(_getKYCStatus(_spender), "rOUSG: 'spender' address not KYC'd");
require(_getKYCStatus(msg.sender), "rOUSG: 'owner' address not KYC'd");
