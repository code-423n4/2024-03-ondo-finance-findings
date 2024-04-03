## NC-01 : `__rOUSG_init` function is redundant.  
`__rOUSG_init` function  is used for initializing rOUSG contract and only called from the `initialize ` function  . But this function is redundant because all it does is forwarding all the params to `__rOUSG_init_unchained` function . 
Same execution can be achieved by calling `__rOUSG_init_unchained` function from 
`initialize ` function . 
Code Link : https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L112
### Recommendation : 
The `initialize ` function can rewritten in this way removing the redundant code : 
```diff
  function initialize(
    //....params..
  ) public virtual initializer {
-    __rOUSG_init(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
+    __rOUSG_init_unchained(_kycRegistry, requirementGroup, _ousg, guardian, _oracle);
  }
```



## NC-02 : Typo in `constructor` of `ousgInstantManager.sol` 
The require statement checks and compare between OUSG and rOUSG decimals .But error statement describes something else . 
```solidity
require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"//@audit Typo
    );
```

Code Link : https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L188
### Recommendation : 
Correct statement is : " "OUSGInstantManager: OUSG decimals must be equal to rOUSG decimals""

## NC-03 : No oracle set event emitted in `__rOUSG_init_unchained` function 
Events are emitted in important state changes . But in the `__rOUSG_init_unchained` function while setting the oracle , No event is emitted !  
Code Link : https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L128
### Recommendation : 
Emit an OracleSet event for the logging . 
```diff
 function __rOUSG_init_unchained(
    //...params 
  ) internal onlyInitializing {
    __KYCRegistryClientInitializable_init(_kycRegistry, _requirementGroup);
    ousg = IERC20(_ousg);
    oracle = IRWAOracle(_oracle);//@audit no oracle set event emitted  ! 
    //...code 
+   emit OracleSet(address(0), _oracle);
  }
```

## NC-04 : Typo in event 
Typo in `rOUSGDeployed` event is named `ticker` instead of `symbol `. 
Code Link : https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L146
### Recommendation : 
It should be renamed to symbol in this way : 
```diff
event rOUSGDeployed(
    //....
-    string ticker//@audit QA should be symbol 
+    string symbol 
  );

```


## Low -01 : Zero address returns `true` in low level calls , But no checks for that . 
The `multiexcall` function is for  multiple executions in a single transaction . It is done by low level calls . Low level calls returns `true ` on calling to zero addresses . There should be checks regarding this scenario for avoiding unwanted scenario .  
```solidity
   for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
```

Code Link : https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L805
### Recommendation : 
A zero address check should be added inside the loop 
```diff
 for (uint256 i = 0; i < exCallData.length; ++i) {
+     require( exCallData[i].target != address(0), " zero address" );
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
```



