`OUSGInstantManager::multiexcall` is susceptible to returnbomb attack

The `multiexcall` function defined in OUSGInstantManager.sol is a valuable addition for batch processing or executing multiple external calls in a single transaction. However, it lacks the use of assembly for consuming the returned data, making it vulnerable to returnbomb attacks. Given its versatility, including the potential for interacting with untrusted external contracts, this poses a genuine risk for griefing attacks:

[OUSGInstantManager.sol#L794-L811](https://github.com/code-423n4/2024-03-ondo-finance/blob/78779c30bebfd46e6f416b03066c55d587e8b30b/contracts/ousg/ousgInstantManager.sol#L794C1-L811C4)

```solidity
  function multiexcall(
    ExCallData[] calldata exCallData
  )
    external
    payable
    override
    onlyRole(DEFAULT_ADMIN_ROLE)
    returns (bytes[] memory results)
  {
    results = new bytes[](exCallData.length);
    for (uint256 i = 0; i < exCallData.length; ++i) {
      (bool success, bytes memory ret) = address(exCallData[i].target).call{
        value: exCallData[i].value
      }(exCallData[i].data);
      require(success, "Call Failed");
      results[i] = ret;
    }
  }

```

Recommendation
Consider using [ExcessivelySafeCall](https://github.com/nomad-xyz/ExcessivelySafeCall/blob/main/src/ExcessivelySafeCall.sol) library or assembly to remove the potential vulnerability.