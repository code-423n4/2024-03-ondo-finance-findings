#### 1. Missing Address Zero Check in deployRebasingOUSG Function

# Summary
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol
The deployRebasingOUSG function lacks an essential address zero check, which could lead to unintended behavior or vulnerabilities. This report highlights the issue and its potential impact.

# Vulnerability Detail
The vulnerability lies in the absence of a check for zero addresses (address(0) or 0x0) when initializing the rOUSGProxied contract. Specifically, the following lines of code do not verify whether the provided addresses (kycRegistry, ousg, guardian, and oracle) are valid:


rOUSGProxied.initialize(
  kycRegistry,
  requirementGroup,
  ousg,
  guardian,
  oracle
);

Without this check, the contract may encounter unexpected behavior or even revert transactions due to invalid addresses. For instance, if any of the input addresses are zero, it could lead to unintended state changes or contract failures.

# Impact
The impact of this vulnerability can vary depending on the context in which the deployRebasingOUSG function is used. Possible consequences include:

Contract Deployment Failures: If any of the input addresses are zero, the contract deployment will fail, preventing the creation of the rOUSGProxied contract.
Runtime Errors: During contract execution, if an invalid address is passed (e.g., zero address), it may result in runtime errors, such as reverts or unexpected behavior.
Security Risks: If the uninitialized contract is used in critical operations (e.g., handling funds), it could lead to security risks, including unauthorized access or manipulation.
## Recommendation
To mitigate this vulnerability, add address zero checks before initializing the rOUSGProxied contract. Ensure that all input addresses are non-zero and valid. For example:

require(kycRegistry != address(0), "Invalid KYC registry address");
require(ousg != address(0), "Invalid OUSD Governance address");
require(guardian != address(0), "Invalid guardian address");
require(oracle != address(0), "Invalid oracle address");

rOUSGProxied.initialize(
  kycRegistry,
  requirementGroup,
  ousg,
  guardian,
  oracle
);

By implementing these checks, you can enhance the security and reliability of the deployRebasingOUSG function.




#### 2. Missing Event Emission in _redeem internal Function
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol
# Summary
The _redeem function, responsible for minting BUID tokens, lacks an event emission in the first if statement. This omission could hinder transparency and make it challenging to track BUIDL redemptions.

# Vulnerability Detail:
The vulnerability lies in the following code snippet:

if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
  // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
  // to cover the full amount
  _redeemBUIDL(usdcAmountToRedeem); // Missing event emission
}

The issue is that there is no corresponding event emitted when the condition is met. Events play a crucial role in notifying external systems and users about significant contract state changes. Without an event, it becomes challenging to monitor BUIDL redemptions triggered by this condition.

# Impact
The impact of this vulnerability includes:

Lack of Transparency: The absence of an event makes it difficult for external systems (such as dApps or other smart contracts) to track BUIDL redemptions accurately. Transparency is essential for trust and auditability.
Missed Analytics: Without emitted events, analytics platforms won’t capture BUIDL redemption data associated with this condition. This hinders data-driven decision-making and monitoring.
Debugging Challenges: In case of unexpected behavior related to BUIDL redemptions, developers won’t have clear logs to diagnose issues. Events provide valuable debugging information.
## Recommendation:
To address this vulnerability, consider emitting an event when the condition is met:

if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
  // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
  // to cover the full amount
  _redeemBUIDL(usdcAmountToRedeem);
  emit BUIDLRedemption(msg.sender, usdcAmountToRedeem);
}

### 3.Missing Amount Validation in redeemRebasingOUSG Function
https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol
# Summary:
The redeemRebasingOUSG function lacks proper validation to ensure that the input rousgAmountIn is greater than zero. This oversight could lead to unintended behavior or erroneous redemptions.

# Vulnerability Detail:
The vulnerability lies in the following code snippet:

require(
  rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
  "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
);

While this line checks if the user’s allowance for rousgAmountIn is sufficient, it does not verify whether the actual rousgAmountIn value is greater than zero. Without this validation, users could mistakenly attempt to redeem zero or negative amounts, leading to unexpected results.

# Impact:
The impact of this vulnerability includes:

Incorrect Redemptions: Users may unintentionally redeem zero or negative amounts, resulting in incorrect behavior within the system.
Loss of Funds: If a user mistakenly redeems a zero or negative amount, they may lose the intended redemption value without receiving any corresponding USDC.
Contract State Inconsistencies: Incorrect redemptions could lead to inconsistencies in the contract’s internal state, affecting subsequent operations.
# Recommendation
To address this vulnerability, add a check to ensure that rousgAmountIn is greater than zero before proceeding with the redemption:

require(rousgAmountIn > 0, "Invalid rOUSG amount");
require(
  rousg.allowance(msg.sender, address(this)) >= rousgAmountIn,
  "OUSGInstantManager::redeemRebasingOUSG: Insufficient allowance"
);

// Rest of the function logic...


similar functions that lack same validation -redeem(), mint(), mintRebasingOUSG(), _mint(), redeemRebasingOUSG()