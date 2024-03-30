## Make the require statement in the constructor in single check

Combining the `require` statements can help reduce gas costs by reducing the number of separate checks and conditional jumps in the bytecode.

## Please note these instances were not included in the bot reports.
In the constructor there are many 0 address checks in `OUSGInstantManager` contract

<details>

<summary>Details</summary>


```javascript
file: contracts/ousg/ousgInstantManager.sol

163:    require(
164:      address(_usdc) != address(0),
165:      "OUSGInstantManager: USDC cannot be 0x0"
166:    );
167:    require(
168:      address(_usdcReciever) != address(0),
169:      "OUSGInstantManager: USDC Receiver cannot be 0x0"
170:    );
171:    require(
172:      address(_feeReceiver) != address(0),
173:      "OUSGInstantManager: feeReceiver cannot be 0x0"
174:    );
175:    require(
176:      address(_ousgOracle) != address(0),
177:      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
178:    );

```

```diff
file: contracts/ousg/ousgInstantManager.sol

-    require(
-      address(_usdc) != address(0),
-      "OUSGInstantManager: USDC cannot be 0x0"
-    );
-    require(
-      address(_usdcReciever) != address(0),
-      "OUSGInstantManager: USDC Receiver cannot be 0x0"
-    );
-    require(
-     address(_feeReceiver) != address(0),
-      "OUSGInstantManager: feeReceiver cannot be 0x0"
-   );
-    require(
-      address(_ousgOracle) != address(0),
-      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
-    );

+   require(
+        address(_usdc) != address(0) && 
+        address(_usdcReciever) != address(0) &&
+        address(_feeReceiver) != address(0) &&
+        address(_ousgOracle) != address(0),
+        "OUSGInstantManager: Invalid zero address"
+    );
```

```javascript
file: contracts/ousg/ousgInstantManager.sol

179:    require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180:    require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181:    require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");

```

```diff
file: contracts/ousg/ousgInstantManager.sol 

-    require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
-    require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
-    require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");

+    require(_ousg != address(0) && _rousg != address(0) && _buidl != address(0), "OUSGInstantManager: OUSG, rOUSG, and BUIDL cannot be 0x0");

```
```
Estimated gas savings 400 in each require statement.
```

</details>

By combining the checks into a single `require` statement with logical AND (`&&`) operators, the Solidity compiler will generate bytecode that performs all the checks together. This reduces the number of conditional jumps and saves gas compared to having separate `require` statements.

The error message is also combined into a single message to provide a clearer indication of the condition that caused the revert, which is "OUSGInstantManager: Invalid zero address". This message is generic enough to cover all cases where any of the addresses are zero.