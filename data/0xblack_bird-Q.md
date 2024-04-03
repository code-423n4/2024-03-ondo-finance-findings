## L-1: Unsafe ERC20 Operations should not be used

ERC20 functions may not behave as expected. For example: return values are not always meaningful.Missing Error Handling, Raw calls don't provide detailed error information if a transfer fails. This can make debugging and identifying issues challenging. 

**Instances**

- Found in contracts/ousg/ousgInstantManager.sol [Line: 264](contracts/ousg/ousgInstantManager.sol#L264)

	```solidity
	    ousg.approve(address(rousg), ousgAmountOut);
	```


- Found in contracts/ousg/ousgInstantManager.sol [Line: 319](contracts/ousg/ousgInstantManager.sol#L319)

	```solidity
	      usdc.transferFrom(msg.sender, feeReceiver, usdcfees);
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 321](contracts/ousg/ousgInstantManager.sol#L321)

	```solidity
	    usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 350](contracts/ousg/ousgInstantManager.sol#L350)

	```solidity
	    ousg.transferFrom(msg.sender, address(this), ousgAmountIn);
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 377](contracts/ousg/ousgInstantManager.sol#L377)

	```solidity
	    rousg.transferFrom(msg.sender, address(this), rousgAmountIn);
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 453](contracts/ousg/ousgInstantManager.sol#L453)

	```solidity
	      usdc.transfer(feeReceiver, usdcFees);
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 458](contracts/ousg/ousgInstantManager.sol#L458)

	```solidity
	    usdc.transfer(msg.sender, usdcAmountOut);
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 467](contracts/ousg/ousgInstantManager.sol#L467)

	```solidity
	    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem);
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 829](contracts/ousg/ousgInstantManager.sol#L829)

	```solidity
	    IERC20(token).transfer(to, amount);
	```

- Found in contracts/ousg/rOUSG.sol [Line: 420](contracts/ousg/rOUSG.sol#L420)

	```solidity
	    ousg.transferFrom(msg.sender, address(this), _OUSGAmount);
	```

- Found in contracts/ousg/rOUSG.sol [Line: 438](contracts/ousg/rOUSG.sol#L438)

	```solidity
	    ousg.transfer(
	```

- Found in contracts/ousg/rOUSG.sol [Line: 635](contracts/ousg/rOUSG.sol#L635)

	```solidity
	    ousg.transfer(
	```
recommendation:It is recommended to use OpenZeppelin's SafeERC20 library.


# NC Issues


## NC-1: Missing checks for `address(0)` when assigning values to address state variables


Assigning values to address state variables without checking for `address(0)`.

**Instances**

- Found in contracts/ousg/ousgInstantManager.sol [Line: 196](contracts/ousg/ousgInstantManager.sol#L196)

	```solidity
	    feeReceiver = _feeReceiver;
	```
## NC-2: Functions not used internally could be marked external

**Instances**

- Found in contracts/ousg/rOUSG.sol [Line: 102](contracts/ousg/rOUSG.sol#L102)

	```solidity
	  function initialize(
	```

- Found in contracts/ousg/rOUSG.sol [Line: 166](contracts/ousg/rOUSG.sol#L166)

	```solidity
	  function name() public pure returns (string memory) {
	```

- Found in contracts/ousg/rOUSG.sol [Line: 174](contracts/ousg/rOUSG.sol#L174)

	```solidity
	  function symbol() public pure returns (string memory) {
	```

- Found in contracts/ousg/rOUSG.sol [Line: 181](contracts/ousg/rOUSG.sol#L181)

	```solidity
	  function decimals() public pure returns (uint8) {
	```

- Found in contracts/ousg/rOUSG.sol [Line: 188](contracts/ousg/rOUSG.sol#L188)

	```solidity
	  function totalSupply() public view returns (uint256) {
	```

- Found in contracts/ousg/rOUSG.sol [Line: 199](contracts/ousg/rOUSG.sol#L199)

	```solidity
	  function balanceOf(address _account) public view returns (uint256) {
	```

- Found in contracts/ousg/rOUSG.sol [Line: 220](contracts/ousg/rOUSG.sol#L220)

	```solidity
	  function transfer(address _recipient, uint256 _amount) public returns (bool) {
	```

- Found in contracts/ousg/rOUSG.sol [Line: 231](contracts/ousg/rOUSG.sol#L231)

	```solidity
	  function allowance(
	```

- Found in contracts/ousg/rOUSG.sol [Line: 251](contracts/ousg/rOUSG.sol#L251)

	```solidity
	  function approve(address _spender, uint256 _amount) public returns (bool) {
	```

- Found in contracts/ousg/rOUSG.sol [Line: 276](contracts/ousg/rOUSG.sol#L276)

	```solidity
	  function transferFrom(
	```

- Found in contracts/ousg/rOUSG.sol [Line: 302](contracts/ousg/rOUSG.sol#L302)

	```solidity
	  function increaseAllowance(
	```

	
## NC-3: Constants should be defined and used instead of literals

**Instances**


- Found in contracts/ousg/ousgInstantManager.sol [Line: 203](contracts/ousg/ousgInstantManager.sol#L203)

	```solidity
	      10 **
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 283](contracts/ousg/ousgInstantManager.sol#L283)

	```solidity
	      IERC20Metadata(address(usdc)).decimals() == 6,
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 394](contracts/ousg/ousgInstantManager.sol#L394)

	```solidity
	      IERC20Metadata(address(usdc)).decimals() == 6,
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 398](contracts/ousg/ousgInstantManager.sol#L398)

	```solidity
	      IERC20Metadata(address(buidl)).decimals() == 6,
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 693](contracts/ousg/ousgInstantManager.sol#L693)

	```solidity
	    uint256 amountE36 = _scaleUp(usdcAmountIn) * 1e18;
	```

- Found in contracts/ousg/ousgInstantManager.sol [Line: 708](contracts/ousg/ousgInstantManager.sol#L708)

	```solidity
	    usdcOwed = _scaleDown(amountE36 / 1e18);
	```

- Found in contracts/ousg/rOUSG.sol [Line: 182](contracts/ousg/rOUSG.sol#L182)

	```solidity
	    return 18;
	```

- Found in contracts/ousg/rOUSG.sol [Line: 190](contracts/ousg/rOUSG.sol#L190)

	```solidity
	      (totalShares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
	```

- Found in contracts/ousg/rOUSG.sol [Line: 202](contracts/ousg/rOUSG.sol#L202)

	```solidity
	      (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
	```

- Found in contracts/ousg/rOUSG.sol [Line: 367](contracts/ousg/rOUSG.sol#L367)

	```solidity
	      (_rOUSGAmount * 1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER) / getOUSGPrice();
	```

- Found in contracts/ousg/rOUSG.sol [Line: 375](contracts/ousg/rOUSG.sol#L375)

	```solidity
	      (_shares * getOUSGPrice()) / (1e18 * OUSG_TO_ROUSG_SHARES_MULTIPLIER);
	```
## NC-4: Event is missing `indexed` fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

**Instances**

- Found in contracts/ousg/rOUSG.sol [Line: 149](contracts/ousg/rOUSG.sol#L149)

	```solidity
	  event TransferShares(
	```

- Found in contracts/ousg/rOUSGFactory.sol [Line: 141](contracts/ousg/rOUSGFactory.sol#L141)

	```solidity
	  event rOUSGDeployed(
	```
