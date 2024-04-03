### [L-1] Unchecked boolean values 

**Description:** transfer() and transferFrom() function of IERC20 returns a boolean value, which should be checked before further steps in the function. The function must revert if the transfer of token fails for some reason.
Example of this vulnerability:
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L419

**Impact:** The unchecked return values vulnerability may seem trivial, but it can lead to significant consequences, including fund loss. Developers should not underestimate the power of return values and should adopt best practices to safeguard their contracts against such vulnerabilities.


**Recommended Mitigation:** We can store the returned boolean value in a local variable and check it the transfer was successful or not. We can use either require() and string error or custom error along with if-statements.
```
+ error TransferFailed();
  (bool success, ) = ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
+ if(!success) revert TransferFailed();
```

### [L-2] Unchecked parameter in function that can be called specific roles only, which can lead to problems like oracle manipulation

**Description:** The contract has function that changes crucial variable but can be only called by users with certain roles. For example `setMintFee()` and `setOracle()`. The protocol must not trust these users blindly and should have checks parameter in this function. 

**Impact:** If in certain cases, malicious attacker gets control of these roles/account, he can easily manipulate these data. For example,
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613
here user with `DEFAULT_ADMIN_ROLE` can call this function with _oracle as address(0) and manipulate the oracle.

**Possible Mitigations:** Check parameter in this function before changing variables.
```
function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
+   require(_oracle == address(0), "address cannot be zero");
    emit OracleSet(address(oracle), _oracle);
    oracle = IRWAOracle(_oracle);
  }
```
```
function setMintFee(
    uint256 _mintFee
  ) external override onlyRole(CONFIGURER_ROLE) {
+   require(mintFee != 0, "fee cannot be zero");
    require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
    emit MintFeeSet(mintFee, _mintFee);
    mintFee = _mintFee;
  }
```