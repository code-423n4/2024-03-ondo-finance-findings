In `OUSGInstantManager` contract have several roles like `DEFAULT_ADMIN_ROLE`, `CONFIGURER_ROLE` and `PAUSER_ROLE`.

But in `constructor` of the `OUSGInstantManager`, these roles are assigned to one address.

So `CONFIGURER_ROLE` and `PAUSER_ROLE` are not required.

https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144-L214

```
  constructor(
    address defaultAdmin,
    address _usdc,
    address _usdcReciever,
    address _feeReceiver,
    address _ousgOracle,
    address _ousg,
    address _rousg,
    address _buidl,
    address _buidlRedeemer,
    RateLimiterConfig memory rateLimiterConfig
  )
    InstantMintTimeBasedRateLimiter(
      rateLimiterConfig.mintLimitDuration,
      rateLimiterConfig.redeemLimitDuration,
      rateLimiterConfig.mintLimit,
      rateLimiterConfig.redeemLimit
    )
  {
    require(
      address(_usdc) != address(0),
      "OUSGInstantManager: USDC cannot be 0x0"
    );
    require(
      address(_usdcReciever) != address(0),
      "OUSGInstantManager: USDC Receiver cannot be 0x0"
    );
    require(
      address(_feeReceiver) != address(0),
      "OUSGInstantManager: feeReceiver cannot be 0x0"
    );
    require(
      address(_ousgOracle) != address(0),
      "OUSGInstantManager: OUSG Oracle cannot be 0x0"
    );
    require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
    require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
    require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
    require(
      address(_buidlRedeemer) != address(0),
      "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
    );
    require(
      IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
      "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
    );
    require(
      IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
      "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
    );
    usdc = IERC20(_usdc);
    usdcReceiver = _usdcReciever;
    feeReceiver = _feeReceiver;
    oracle = IRWAOracle(_ousgOracle);
    ousg = IRWALike(_ousg);
    rousg = ROUSG(_rousg);
    buidl = IERC20(_buidl);
    buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
    decimalsMultiplier =
      10 **
        (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());
    require(
      OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
        rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
      "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
    );

    _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
    _grantRole(CONFIGURER_ROLE, defaultAdmin);
    _grantRole(PAUSER_ROLE, defaultAdmin);
  }
```
We can remove the `CONFIGURER_ROLE` and `PAUSER_ROLE`.
```
 _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
 _grantRole(CONFIGURER_ROLE, defaultAdmin);
 _grantRole(PAUSER_ROLE, defaultAdmin);
```