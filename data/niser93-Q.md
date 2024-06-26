# L1 - Lack of address(0) checks

In [ousgInstantManager.sol#L144-L214](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L144-L214) the `Constructor` checks
many addresses to assure they are different from `address(0)`. However, there is no check for `defaultAdmin` address, and that address is set as `DEFAULT_ADMIN_ROLE`, `CONFIGURER_ROLE`, `PAUSER_ROLE`. Let's add 0-address check inside `Constructor`:

```diff
144    constructor(
145      address defaultAdmin,
146      address _usdc,
147      address _usdcReciever,
148      address _feeReceiver,
149      address _ousgOracle,
150      address _ousg,
151      address _rousg,
152      address _buidl,
153      address _buidlRedeemer,
154      RateLimiterConfig memory rateLimiterConfig
155    )
156      InstantMintTimeBasedRateLimiter(
157        rateLimiterConfig.mintLimitDuration,
158        rateLimiterConfig.redeemLimitDuration,
159        rateLimiterConfig.mintLimit,
160        rateLimiterConfig.redeemLimit
161      )
162    {
+        require(
+          address(defaultAdmin) != address(0),
+          "OUSGInstantManager: defaultAdmin cannot be 0x0"
+        );
163      require(
164        address(_usdc) != address(0),
165        "OUSGInstantManager: USDC cannot be 0x0"
166      );
167      require(
168        address(_usdcReciever) != address(0),
169        "OUSGInstantManager: USDC Receiver cannot be 0x0"
170      );
171      require(
172        address(_feeReceiver) != address(0),
173        "OUSGInstantManager: feeReceiver cannot be 0x0"
174      );
175      require(
176        address(_ousgOracle) != address(0),
177        "OUSGInstantManager: OUSG Oracle cannot be 0x0"
178      );
179      require(_ousg != address(0), "OUSGInstantManager: OUSG cannot be 0x0");
180      require(_rousg != address(0), "OUSGInstantManager: rOUSG cannot be 0x0");
181      require(_buidl != address(0), "OUSGInstantManager: BUIDL cannot be 0x0");
182      require(
183        address(_buidlRedeemer) != address(0),
184        "OUSGInstantManager: BUIDL Redeemer cannot be 0x0"
185      );
186      require(
187        IERC20Metadata(_ousg).decimals() == IERC20Metadata(_rousg).decimals(),
188        "OUSGInstantManager: OUSG decimals must be equal to USDC decimals"
189      );
190      require(
191        IERC20Metadata(_usdc).decimals() == IERC20Metadata(_buidl).decimals(),
192        "OUSGInstantManager: USDC decimals must be equal to BUIDL decimals"
193      );
194      usdc = IERC20(_usdc);
195      usdcReceiver = _usdcReciever;
196      feeReceiver = _feeReceiver;
197      oracle = IRWAOracle(_ousgOracle);
198      ousg = IRWALike(_ousg);
199      rousg = ROUSG(_rousg);
200      buidl = IERC20(_buidl);
201      buidlRedeemer = IBUIDLRedeemer(_buidlRedeemer);
202      decimalsMultiplier =
203        10 **
204          (IERC20Metadata(_ousg).decimals() - IERC20Metadata(_usdc).decimals());
205      require(
206        OUSG_TO_ROUSG_SHARES_MULTIPLIER ==
207          rousg.OUSG_TO_ROUSG_SHARES_MULTIPLIER(),
208        "OUSGInstantManager: OUSG to rOUSG shares multiplier must be equal to rOUSG's"
209      );
210  
211      _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
212      _grantRole(CONFIGURER_ROLE, defaultAdmin);
213      _grantRole(PAUSER_ROLE, defaultAdmin);
214    }
```

In [rOUSG.sol#L613-L616](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L613-L616)
there is no 0-address check when `DEFAULT_ADMIN_ROLE` updates oracle address:

```
613     function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
614         emit OracleSet(address(oracle), _oracle);
615         oracle = IRWAOracle(_oracle);
616     }
```


# NC1 - Typos
In [ousgInstantManager.sol#L147](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L147)
is defined the function parameter `_usdcReciever`, instead of `_usdcReceiver`. We didn't found error due to this, but in
future developments this could lead to errors.

```
147     address _usdcReciever,
```

In [ousgInstantManager.sol#L225](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L225)
and [ousgInstantManager.sol#L249](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L249)
the word `specifed` is wrong. Use `specified` instead.

```
225     *                     specifed by usdc token contract)
249     *                     specifed by usdc token contract)
```

In [ousgInstantManager.sol#L494](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L494)
and [ousgInstantManager.sol#L508](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L508)
the word `dicates` is wrong. Use `indicates` instead.

```
494     * @param _instantMintLimit New limit that dicates how much USDC can be transfered
508     * @param _instantRedemptionLimit New limit that dicates how much USDC
```

In [ousgInstantManager.sol#L494](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L494)
the word `transfered` is wrong. Use `transferred` instead.

```
494     * @param _instantMintLimit New limit that dicates how much USDC can be transfered
```

In [rOUSG.sol#L591](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L591)
the word `facliitate` is wrong. Use `facilitate` instead.

```
591      // Check constraints when `transferFrom` is called to facliitate
```

# NC2 - OUSGInstantManager.redeemRebasingOUSG() has a wrong description

The comment above [OUSGInstantManager.redeemRebasingOUSG()](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L362-L386)
doesn't describe correctly the function behavior. Probably, it was copy and paste from the `mint()` function.

```
353    /**
354     * @notice Calculates fees and triggers minting rOUSG for a given amount of USDC
355     *
356     * @dev Please note that the fees are actually accumulated in `feeReceiver`
357     *
358     * @param rousgAmountIn Amount of rOUSG to redeem
359     *
360     * @return usdcAmountOut The amount of USDC returned to the user
361     */
```

# NC3 - Use a common utility contract to implement some common functionalities, like getOUSGPrice()

In scope there are two `getOUSGPrice()` functions [ousgInstantManager.getOUSGPrice()](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L479-L485) and [rOUSG.getOUSGPrice()](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L378-L380).

They are quite different. We reported in another issue that `rOUSG.getOUSGPrice()` doesn't have a protection against too low price from oracle.
It can be useful to create a common contract and use it to implement common functionalities.

# NC4 - ```require()``` should be used instead of ```assert()```
The ```assert()``` statement is used in development, but ```require()``` should be used in production.
The is 1 instance of this in [rOUSGFactory.sol#L94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94)

```
94       assert(rOUSGProxyAdmin.owner() == guardian);
```

# NC5 - Let's use named mapping
The ```assert()``` statement is used in development, but ```require()``` should be used in production.
The is 1 instance of this in [rOUSGFactory.sol#L94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSGFactory.sol#L94)

[rOUSG.sol#L72](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L72)

[rOUSG.sol#L75](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L75)

```
72     mapping(address => uint256) private shares;
75     mapping(address => mapping(address => uint256)) private allowances;
```

# NC6 - Calls to ```keccak256()``` should use ```immutable``` rather than ```constant```

[ousgInstantManager.sol#L57](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L57)

[ousgInstantManager.sol#L60](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/ousgInstantManager.sol#L60)
```
57     bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
60     bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
```


[rOUSG.sol#93](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L93)

[rOUSG.sol#94](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L94)

[rOUSG.sol#95](https://github.com/code-423n4/2024-03-ondo-finance/blob/main/contracts/ousg/rOUSG.sol#L95)

```
93     bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
94     bytes32 public constant BURNER_ROLE = keccak256("BURN_ROLE");
95     bytes32 public constant CONFIGURER_ROLE = keccak256("CONFIGURER_ROLE");
```

# NC7 - Setters should prevent re-setting of the same value
This especially problematic when the setter also emits the same value, which may be confusing to offline parsers.
Moreover, when it is set a state variable, it wastes gas.

```
File: ousgInstantManager.sol

@audit: values to prevent: _mintFee
554    function setMintFee(
555      uint256 _mintFee
556    ) external override onlyRole(CONFIGURER_ROLE) {
557      require(mintFee < 200, "OUSGInstantManager::setMintFee: Fee too high");
558      emit MintFeeSet(mintFee, _mintFee);
559      mintFee = _mintFee;
560    }

@audit: values to prevent: _redeemFee
567    function setRedeemFee(
568      uint256 _redeemFee
569    ) external override onlyRole(CONFIGURER_ROLE) {
570      require(redeemFee < 200, "OUSGInstantManager::setRedeemFee: Fee too high");
571      emit RedeemFeeSet(redeemFee, _redeemFee);
572      redeemFee = _redeemFee;
573    }

@audit: values to prevent: _minimumDepositAmount
581    function setMinimumDepositAmount(
582      uint256 _minimumDepositAmount
583    ) external override onlyRole(CONFIGURER_ROLE) {
584      require(
585        _minimumDepositAmount >= FEE_GRANULARITY,
586        "setMinimumDepositAmount: Amount too small"
587      );
588  
589      emit MinimumDepositAmountSet(minimumDepositAmount, _minimumDepositAmount);
590      minimumDepositAmount = _minimumDepositAmount;
591    }

@audit: values to prevent: _minimumRedemptionAmount
599    function setMinimumRedemptionAmount(
600      uint256 _minimumRedemptionAmount
601    ) external override onlyRole(CONFIGURER_ROLE) {
602      require(
603        _minimumRedemptionAmount >= FEE_GRANULARITY,
604        "setMinimumRedemptionAmount: Amount too small"
605      );
606      emit MinimumRedemptionAmountSet(
607        minimumRedemptionAmount,
608        _minimumRedemptionAmount
609      );
610      minimumRedemptionAmount = _minimumRedemptionAmount;
611    }

@audit: values to prevent: _minimumBUIDLRedemptionAmount
622    function setMinimumBUIDLRedemptionAmount(
623      uint256 _minimumBUIDLRedemptionAmount
624    ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
625      emit MinimumBUIDLRedemptionAmountSet(
626        minBUIDLRedeemAmount,
627        _minimumBUIDLRedemptionAmount
628      );
629      minBUIDLRedeemAmount = _minimumBUIDLRedemptionAmount;
630    }

@audit: values to prevent: _oracle
638    function setOracle(
639      address _oracle
640    ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
641      emit OracleSet(address(oracle), _oracle);
642      oracle = IRWAOracle(_oracle);
643    }

@audit: values to prevent: _investorBasedRateLimiter
663    function setInvestorBasedRateLimiter(
664      address _investorBasedRateLimiter
665    ) external override onlyRole(DEFAULT_ADMIN_ROLE) {
666      emit InvestorBasedRateLimiterSet(
667        address(investorBasedRateLimiter),
668        _investorBasedRateLimiter
669      );
670      investorBasedRateLimiter = IInvestorBasedRateLimiter(
671        _investorBasedRateLimiter
672      );
673    }

```

```
File: rOUSG.sol

@audit: values to prevent: _oracle
613    function setOracle(address _oracle) external onlyRole(DEFAULT_ADMIN_ROLE) {
614      emit OracleSet(address(oracle), _oracle);
615      oracle = IRWAOracle(_oracle);
616    }

```