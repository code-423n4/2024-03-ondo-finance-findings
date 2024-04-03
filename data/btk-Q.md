## Ai Arena Overview


## Findings Summary

| Risk   | Title                                                            |
| ------ | -----------------------------------------------------------------|
| [L-01] | Funds will become inaccessible when USDC blacklists a user       |
| [L-02] | Investors can't instant redeem when buidl token is paused        |
| [L-03] | No price validation check in rOUSG                               |
| [L-04] | rOUSG is not erc20 compliant                                     |
| [L-05] | Incorrect check in _redeemBUIDL                                  |
| [L-06] | Minting will get DoSed if the usdcReceiver got blocklisted      |

## [L-01] Funds will become inaccessible when USDC blacklists a user

## Impact

If an investor is blacklisted by the USDC contract, they will be unable to redeem their OUSG/ROUSG tokens.

## Description

Some ERC-20 tokens like for example USDC (which is used by the system) have the functionality to blacklist specific addresses, so that they are no longer able to transfer and receive tokens. Sending funds to these addresses will lead to a revert. The issue is that the  [_redeem](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L455) function transfers funds to the msg.sender:

```solidity
    usdc.transfer(msg.sender, usdcAmountOut);
```

Therefore, if an investor is blacklisted by the USDC address, they will be unable to redeem their OUSG/ROUSG tokens.

## Recommended Mitigation Steps

Consider allowing investors to specify a receiver address.

## [L-02] Investors can't instant redeem when buidl token is paused

## Impact

The OUSGInstantManager contract is designed to facilitate instant mints and instant redemptions of OUSG and rOUSG. However, investors are unable to redeem their OUSG/rOUSG when the buidl token is paused.

## Description

Certain ERC-20 tokens, such as buidl (utilized within the system), possess the capability to pause token transfers in emergencies. This functionality is exemplified [here](https://etherscan.deth.net/token/0x7712c34205737192402172409a8f7ccef8aa2aec#code):

```solidity
    function pause() public onlyTransferAgentOrAbove whenNotPaused {
        paused = true;
        emit Pause();
    }
```

The issue arises when the buidl token is paused, rendering OUSGInstantManager unable to fulfill its instant redemption commitments. Consequently, this situation detrimentally impacts the protocol's reputation.

## Recommended Mitigation Steps

Consider documenting scenarios where OUSGInstantManager may fail to provide instant redemption.

## [L-03] No price validation check in rOUSG

## Impact

rOUSG lacks validation for the price returned by the oracle. Consequently, if the price unexpectedly drops to a low value, transactions won't revert, potentially resulting in loss of funds for investors due to oracle price manipulation.

## Description

The OUSGInstantManager contract validates the price returned by the oracle as follows:

```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > MINIMUM_OUSG_PRICE,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }
```

The OUSGInstantManager.getOUSGPrice function reverts if the price is unexpectedly low (i.e., when the price is less than 105e18).

However, the rOUSG token lacks a similar sanity check, as seen [here](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378-L380):

```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
  }
```

Consequently, if the returned price is too low due to price manipulation, the transaction will succeed, resulting in a loss of funds for investors.

## Recommended Mitigation Steps

Consider adding a similar check for the rOUSG contract:

```solidity
  function getOUSGPrice() public view returns (uint256 price) {
    (price, ) = oracle.getPriceData();
    require(
      price > 105e18,
      "OUSGInstantManager::getOUSGPrice: Price unexpectedly low"
    );
  }

```

## [L-04] rOUSG is not erc20 compliant

## Impact

The rOUSG contract does not adhere to EIP-20 specifications.

## Description

[EIP-20](https://eips.ethereum.org/EIPS/eip-20) state that: 

> Callers MUST handle false from returns (bool success). Callers MUST NOT assume that false is never returned!

The rOUSG interacts with the OUSG token assuming it will always revert instead of returning false. While the current implementation of OUSG does revert instead of returning false, the OUSG contract is upgradeable, meaning the implementation can change in the future, breaking the rOUSG integration with EIP-20.

## Recommended Mitigation Steps

Consider checking the returned value and reverting if false is returned. For example:

```solidity
require(ousg.transferFrom(msg.sender, address(this), _OUSGAmount), "Transfer failed");
```

## [L-05] Incorrect check in _redeemBUIDL

## Impact

The _redeemBUIDL function within OUSGInstantManager contains an incorrect check that triggers the buidlRedeemer.redeem function even when there is "Insufficient BUIDL balance." This leads to unnecessary wastage of investors' gas fees.

## Description

The _redeemBUIDL function contains a check to ensure there is sufficient BUIDL balance in the contract. However, it erroneously checks the wrong value:

```solidity
  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    require(
      buidl.balanceOf(address(this)) >= minBUIDLRedeemAmount,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
    uint256 usdcBalanceBefore = usdc.balanceOf(address(this)); // ok
    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem); // ok
    buidlRedeemer.redeem(buidlAmountToRedeem);
    require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
  }
```

The _redeemBUIDL function is called when usdcAmountToRedeem >= minBUIDLRedeemAmount, as shown here:

```solidity
if (usdcAmountToRedeem >= minBUIDLRedeemAmount) {
      // amount of USDC needed is over minBUIDLRedeemAmount, do a BUIDL redemption
      // to cover the full amount
      _redeemBUIDL(usdcAmountToRedeem);
```

For example, if usdcAmountToRedeem is 300k USDC, and minBUIDLRedeemAmount is 250k BUIDL, _redeemBUIDL is called with usdcAmountToRedeem. The issue arises because it checks if the OUSGInstantManager BUIDL balance is more than minBUIDLRedeemAmount instead of usdcAmountToRedeem. Consequently, if there were 260k BUIDL in the OUSGInstantManager, the check ensuring sufficient balance would pass even when there is an insufficient balance, leading to wasted investor gas in a no-op situation.

## Recommended Mitigation Steps

Consider updating the _redeemBUIDL function check as follows:

```solidity
  function _redeemBUIDL(uint256 buidlAmountToRedeem) internal {
    require(
      buidl.balanceOf(address(this)) >= buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: Insufficient BUIDL balance"
    );
    uint256 usdcBalanceBefore = usdc.balanceOf(address(this)); // ok
    buidl.approve(address(buidlRedeemer), buidlAmountToRedeem); // ok
    buidlRedeemer.redeem(buidlAmountToRedeem);
    require(
      usdc.balanceOf(address(this)) == usdcBalanceBefore + buidlAmountToRedeem,
      "OUSGInstantManager::_redeemBUIDL: BUIDL:USDC not 1:1"
    );
  }
```

## [L-06] Minting will get DoSed if the usdcReceiver got blocklisted

## Impact

OUSGInstantManager minting will get DoSed if the usdcReceiver got blocklisted by USDC.

## Description

Some ERC-20 tokens like for example USDC (which is used by the system) have the functionality to blacklist specific addresses, so that they are no longer able to transfer and receive tokens. Sending funds to these addresses will lead to a revert. Currently, the usdcReceiver address in the OUSGInstantManager contract is immutable and cannot be changed:

```solidity
address public immutable usdcReceiver;
```

If the usdcReceiver address is blacklisted by USDC, attempts to transfer tokens to it will always revert, potentially leading to a permanent DoS during minting:

```solidity
usdc.transferFrom(msg.sender, usdcReceiver, usdcAmountAfterFee);
```

## Recommended Mitigation Steps

Consider making the usdcReceiver address mutable and implementing a function to update it in case of blacklisting by USDC.