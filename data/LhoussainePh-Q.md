### L-01 Transactions may revert because of a deadline

In the `UniswapSettlement`, the ` ISwapRouter.ExactInputParams` is called and the `block.timestamp` is passed as `deadline`. This means that if the execution takes longer than the current timestamp, the transaction will revert as it can be seen from the [Uniswap documentation](https://docs.uniswap.org/contracts/v2/reference/smart-contracts/router-02). It is the same for `_swapRouter.exactOutput` and `_swapRouter.exactInput`.

```javascript
    function swapExactIn(
        address,
        address baseToken,
        bytes memory data,
        uint256 amountIn,
        uint256 amountOutMinimum,
        address recipient
    ) external override returns (uint256 amountOut) {

        //@audit-issue what if the tx takes longer and and block.timestamp will bigger ?? 
        amountOut = _swapRouter.exactInput(
            ISwapRouter.ExactInputParams(data, recipient, block.timestamp, amountIn, amountOutMinimum)
        );

     }
```
```javascript
    function swapExactOut(
        address quoteToken,
        address,
        bytes memory data,
        uint256 amountIn,
        uint256 amountOutMinimum,
        address recipient
    ) external override returns (uint256 amountOut) {

        //@audit-issue what if the tx takes loger and and block.timestamp will bigger ?? 
        amountOut = _swapRouter.exactOutput(
            ISwapRouter.ExactInputParams(data, recipient, block.timestamp, amountIn, amountOutMinimum)
        );

     }
```
```javascript
			
            modifier checkDeadline(uint256 deadline) {
                require(_blockTimestamp() <= deadline, 'Transaction too old');
                _;
            }

```
If a user chose a transaction fee that is too low for miners to be interested in including the transaction in a
block, the transaction stays pending in the mempool for extended periods, which could be hours, days,
weeks, or even longer.
This could lead to users getting a worse price, because a validator can just hold onto the transaction.

**Recommendations**
Protocols should let users who interact with AMMs set expiration deadlines. Without this, there's a risk of a
serious loss of funds for anyone starting a swap, especially if there's no slippage parameter.
Use a user supplied deadline instead of `block.timestamp`.

### L-02 Missing checks for `address(0)` when assigning values to address state variables

Assigning values to address state variables without checking for `address(0)`.

```solidity

    constructor(address quotePrice, address pyth, bytes32 priceId, uint256 decimalsDiff) {
        //@audit-L  miss zero addr check
        
        _quotePriceFeed = quotePrice;
        _pyth = pyth;
        _priceId = priceId;
        _decimalsDiff = decimalsDiff;
    }

```
- Found in src/base/BaseHookCallbackUpgradable.sol [Line: 22](src\base\BaseHookCallbackUpgradable.sol#L22)

	```solidity
	        _predyPool = predyPool;
	```

- Found in src/base/BaseMarket.sol [Line: 25](src\base\BaseMarket.sol#L25)

	```solidity
	        whitelistFiller = _whitelistFiller;
	```

- Found in src/base/BaseMarket.sol [Line: 91](src\base\BaseMarket.sol#L91)

	```solidity
	        whitelistFiller = newWhitelistFiller;
	```

- Found in src/base/BaseMarketUpgradable.sol [Line: 45](src\base\BaseMarketUpgradable.sol#L45)

	```solidity
	        whitelistFiller = _whitelistFiller;
	```

- Found in src/base/BaseMarketUpgradable.sol [Line: 132](src\base\BaseMarketUpgradable.sol#L132)

	```solidity
	        whitelistFiller = newWhitelistFiller;
	```
### L-03 Use two-step ownership transfer approach
The owner role is crucial for the protocol as there are a lot of functions with the onlyOwner modifier. Make sure to use a two-step ownership transfer approach by using `Ownable2Step` from ``OpenZeppelin`` as opposed to `solmate's Owned` as it gives you the security of not unintentionally sending the owner role to an address you do not control.

### L-04 Some tokens revert on transfer of zero amount

**description** Some tokens revert on transfer of zero amount and can cause issues in certain integrations and operations. 
```solidity
    function sell(
        IPredyPool predyPool,
        address quoteToken,
        address baseToken,
        SettlementParams memory settlementParams,
        address sender,
        uint256 price,
        uint256 sellAmount
    ) internal {

        if (settlementParams.contractAddress == address(0)) {
            // direct fill
            uint256 quoteAmount = sellAmount * price / Constants.Q96;

            predyPool.take(false, sender, sellAmount);

            //@audit-L miss zero check quoteAmount
            ERC20(quoteToken).safeTransferFrom(sender, address(predyPool), quoteAmount);

            return;
        }

        predyPool.take(false, address(this), sellAmount);
        ERC20(baseToken).approve(address(settlementParams.contractAddress), sellAmount);

        uint256 quoteAmountFromUni = ISettlement(settlementParams.contractAddress).swapExactIn(
            quoteToken,
            baseToken,
            settlementParams.encodedData,
            sellAmount,
            settlementParams.maxQuoteAmount,
            address(this)
        );

        if (price == 0) {

            //@audit-L miss zero check for quoteAmountFromUni 
            ERC20(quoteToken).safeTransfer(address(predyPool), quoteAmountFromUni);
        } else {
            uint256 quoteAmount = sellAmount * price / Constants.Q96;

            if (quoteAmount > quoteAmountFromUni) {
                ERC20(quoteToken).safeTransferFrom(sender, address(this), quoteAmount - quoteAmountFromUni);
            } else if (quoteAmountFromUni > quoteAmount) {
                ERC20(quoteToken).safeTransfer(sender, quoteAmountFromUni - quoteAmount);
            }

            //@audit-L miss zero check quoteAmount
            ERC20(quoteToken).safeTransfer(address(predyPool), quoteAmount);
        }
    }

```

```solidity

    function buy(
        IPredyPool predyPool,
        address quoteToken,
        address baseToken,
        SettlementParams memory settlementParams,
        address sender,
        uint256 price,
        uint256 buyAmount
    ) internal {
        if (settlementParams.contractAddress == address(0)) {
            // direct fill
            uint256 quoteAmount = buyAmount * price / Constants.Q96;

            predyPool.take(true, sender, quoteAmount);

            //@audit-L miss zero check buyAmount
            ERC20(baseToken).safeTransferFrom(sender, address(predyPool), buyAmount);

            return;
        }

        predyPool.take(true, address(this), settlementParams.maxQuoteAmount);
        ERC20(quoteToken).approve(address(settlementParams.contractAddress), settlementParams.maxQuoteAmount);

        uint256 quoteAmountToUni = ISettlement(settlementParams.contractAddress).swapExactOut(
            quoteToken,
            baseToken,
            settlementParams.encodedData,
            buyAmount,
            settlementParams.maxQuoteAmount,
            address(predyPool)
        );

        if (price == 0) {

            //@audit-L miss zero check 
            ERC20(quoteToken).safeTransfer(address(predyPool), settlementParams.maxQuoteAmount - quoteAmountToUni);
        } else {
            uint256 quoteAmount = buyAmount * price / Constants.Q96;

            if (quoteAmount > quoteAmountToUni) {
                ERC20(quoteToken).safeTransfer(sender, quoteAmount - quoteAmountToUni);
            } else if (quoteAmountToUni > quoteAmount) {
                ERC20(quoteToken).safeTransferFrom(sender, address(this), quoteAmountToUni - quoteAmount);
            }

            //@audit-L miss zero check 
            ERC20(quoteToken).safeTransfer(address(predyPool), settlementParams.maxQuoteAmount - quoteAmount);
        }
    }
    
```

```solidity
    function receiveTokenAndMintBond(Perp.AssetPoolStatus storage _pool, uint256 _amount)
        internal
        returns (uint256 mintAmount)
    {
        mintAmount = _pool.tokenStatus.addAsset(_amount); // return 0 if amount = 0
        //@audit-L miss zero  check
        ERC20(_pool.token).safeTransferFrom(msg.sender, address(this), _amount);
        ISupplyToken(_pool.supplyTokenAddress).mint(msg.sender, mintAmount);
    }

```

```solidity

    function swapExactIn(
        address,
        address baseToken,
        bytes memory data,
        uint256 amountIn,
        uint256 amountOutMinimum,
        address recipient
    ) external override returns (uint256 amountOut) {
        ERC20(baseToken).safeTransferFrom(msg.sender, address(this), amountIn);

```

**Recommandation** Transfer only when the amount is positive.

### L-05 Division before multiplication in `PriceFeed::getSqrtPrice` function

**description** 
We have the following code in `PriceFeed::getSqrtPrice` :

```solidity

    /// @notice This function returns the square root of the baseToken price quoted in quoteToken.
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {

        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        //@audit-L div before mult 
        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }

```
We can see that when price is calculated there is division, but then price is used in multiplication.
This way there is no division before multiplication, which can result in a loss of precision.

### L-06 `recipient` can be `address(0)` in `updateRecepient`

**description** `updateRecepient` function responsible for update the recipient address , but if the vault owner set `recipient` to `address(0)` by mistak this causing the protocol may  never transfers margin. 
```solidity
  /**
     * @notice Updates the recipient. If the position is liquidated, the remaining margin is sent to the recipient.
     * @param vaultId The id of the vault.
     * @param recipient if recipient is zero address, protocol never transfers margin.
     */
    function updateRecepient(uint256 vaultId, address recipient) external onlyVaultOwner(vaultId) {
        //@audit-L  miss zero check => recipient is zero address, protocol never transfers margin
        DataType.Vault storage vault = globalData.vaults[vaultId];

        vault.recipient = recipient;

        emit RecepientUpdated(vaultId, recipient);
    }

```
**impact** the protocol may  never transfers margin.

**Recommandation** add a require for zero address

```diff
+ require(recipent != address(0));
```
### L-07 missing checks for  `recipient` in `swapExactIn` & `swapExactOut` causing the fund to gone

**description** The `swapExactIn` & `swapExactOut` functions respons for swap the tokens , and `recipient` is the address who receive the output amout , but if the the swapper est the address to `address(0)` by mistak the fund well be gone or make it a contract so revert the fund or really anything in the case of attacker.

```solidity
    function swapExactOut(
        address quoteToken,
        address,
        bytes memory data,
        uint256 amountOut,
        uint256 amountInMaximum,
        address recipient
    ) external override returns (uint256 amountIn) {
        ERC20(quoteToken).safeTransferFrom(msg.sender, address(this), amountInMaximum);
        ERC20(quoteToken).approve(address(_swapRouter), amountInMaximum);
        
        //@audit-L miss  recipient  check
        amountIn = _swapRouter.exactOutput(
            ISwapRouter.ExactOutputParams(data, recipient, block.timestamp, amountOut, amountInMaximum)
        );
```
```solidity
    function swapExactIn(
        address,
        address baseToken,
        bytes memory data,
        uint256 amountIn,
        uint256 amountOutMinimum,
        address recipient
    ) external override returns (uint256 amountOut) {
        ERC20(baseToken).safeTransferFrom(msg.sender, address(this), amountIn);
        ERC20(baseToken).approve(address(_swapRouter), amountIn);

        //@audit-L miss  recipient check
        amountOut = _swapRouter.exactInput(
            ISwapRouter.ExactInputParams(data, recipient, block.timestamp, amountIn, amountOutMinimum)
        );

```

**impact** lose the fund

**Recommandation** Add some check for all the cases in the `swapExactIn` & `swapExactOut` functions.

### L-08 Division by zero 

**description** 

```solidity
        
    function lower(uint256 price, uint256 bps) internal pure returns (uint256) {
        //@audit-L div by zero
        return (price * ONE) / bps;
    }
```

```solidity
        uint256 lowerPrice = _sqrtPrice * RISK_RATIO_ONE / _riskRatio;

```
```solidity
        uint160 sqrtPrice = ((available * FixedPoint96.Q96) / liquidityAmount).toUint160();
```
```solidity
        swapResult.amountPerp = (amountQuote * swapParams.amountPerp) / amountBase;
```
```solidity
        
    return uint160((Constants.Q96 << Constants.RESOLUTION) / sqrtPriceX96);
```
```solidity
     
     return perpAmount + (_sqrtAmount * int256(Constants.Q96)) / sqrtPrice;

```
```solidity
    if (endPrice < startPrice) {
     //@audit-L div by zero
    decayedPrice = startPrice - ((startPrice - endPrice) * elapsed) /  duration;
```

**Recommandation** should check before do any division .

### L-09 Use `abi.encodeCall` instead of `abi.encodeWithSelector`

**description** The problem with `abi.encodeWithSelector` is that the compiler does not check whether the supplied values actually match the types expected by the called function. `abi.encodeCall` which is similar to `abi.encodeWithSelector`, just that it does perform these type checks. Note that `abi.encodeCall` is available from version `pragma solidity 0.8.11`.

```solidity
    function callUniswapObserve(
        IUniswapV3Pool uniswapPool,
        uint256 ago
    ) internal view returns (uint160, uint256) {
        uint32[] memory secondsAgos = new uint32[](2);

        secondsAgos[0] = uint32(ago);
        secondsAgos[1] = 0;
        //@audit-L Use `abi.encodeCall` instead of `abi.encodeWithSelector`
        (bool success, bytes memory data) = address(uniswapPool).staticcall(
            abi.encodeWithSelector(
                IUniswapV3PoolOracle.observe.selector,
                secondsAgos
            )
        );

        if (!success) {
            if (
                keccak256(data) !=
                keccak256(abi.encodeWithSignature("Error(string)", "OLD"))
            ) {
                revertBytes(data);
            }

            (, , uint16 index, uint16 cardinality, , , ) = uniswapPool.slot0();

            (uint32 oldestAvailableAge, , , bool initialized) = uniswapPool
                .observations((index + 1) % cardinality);

            if (!initialized) {
                (oldestAvailableAge, , , ) = uniswapPool.observations(0);
            }

            ago = block.timestamp - oldestAvailableAge;
            secondsAgos[0] = uint32(ago);
            //@audit-L Use `abi.encodeCall` instead of `abi.encodeWithSelector`
            (success, data) = address(uniswapPool).staticcall(
                abi.encodeWithSelector(
                    IUniswapV3PoolOracle.observe.selector,
                    secondsAgos
                )
            );
            if (!success) {
                revertBytes(data);
            }
        }

        int56[] memory tickCumulatives = abi.decode(data, (int56[]));

        int24 tick = int24(
            (tickCumulatives[1] - tickCumulatives[0]) / int56(int256(ago))
        );

        uint160 sqrtPriceX96 = TickMath.getSqrtRatioAtTick(tick);

        return (sqrtPriceX96, ago);
    }

```

### L-10 `abi.encodePacked()` should not be used with dynamic types when passing the result to a hash function such as `keccak256()`

**description** Use `abi.encode()` instead which will pad items to 32 bytes, which will [prevent hash collisions](https://docs.soliditylang.org/en/v0.8.13/abi-spec.html#non-standard-packed-mode) (e.g. `abi.encodePacked(0x123,0x456)` => `0x123456` => `abi.encodePacked(0x1,0x23456)`, but `abi.encode(0x123,0x456)` => `0x0...1230...456`). "Unless there is a compelling reason, `abi.encode` should be preferred". If there is only one argument to `abi.encodePacked()` it can often be cast to `bytes()` or `bytes32()` [instead](https://ethereum.stackexchange.com/questions/30912/how-to-compare-strings-in-solidity#answer-82739).

If all arguments are strings and or bytes, `bytes.concat()` should be used instead.

```solidity
    bytes internal constant GAMMA_ORDER_TYPE = abi.encodePacked(
        "GammaOrder(",
        "OrderInfo info,",
        "uint64 pairId,",
        "uint256 positionId,",
        "address entryTokenAddress,",
        "int256 quantity,",
        "int256 quantitySqrt,",
        "int256 marginAmount,",
        "uint256 baseSqrtPrice,",
        "uint32 slippageTolerance,",
        "uint8 leverage,",
        "GammaModifyInfo modifyInfo)"
    );
    bytes internal constant ORDER_TYPE =
        abi.encodePacked(GAMMA_ORDER_TYPE, GammaModifyInfoLib.GAMMA_MODIFY_INFO_TYPE, OrderInfoLib.ORDER_INFO_TYPE);
    bytes32 internal constant GAMMA_ORDER_TYPE_HASH = keccak256(ORDER_TYPE);

```
```solidity
    bytes internal constant PERP_ORDER_TYPE = abi.encodePacked(
        "PerpOrder(",
        "OrderInfo info,",
        "uint64 pairId,",
        "address entryTokenAddress,",
        "int256 tradeAmount,",
        "int256 marginAmount,",
        "uint256 takeProfitPrice,",
        "uint256 stopLossPrice,",
        "uint64 slippageTolerance,",
        "uint8 leverage,",
        "address validatorAddress,",
        "bytes validationData)"
    );

    /// @dev Note that sub-structs have to be defined in alphabetical order in the EIP-712 spec
    bytes internal constant ORDER_TYPE = abi.encodePacked(PERP_ORDER_TYPE, OrderInfoLib.ORDER_INFO_TYPE);
    bytes32 internal constant PERP_ORDER_TYPE_HASH = keccak256(ORDER_TYPE);

```
```solidity
    string internal constant PERMIT2_ORDER_TYPE = string(
        abi.encodePacked("PerpOrder witness)", OrderInfoLib.ORDER_INFO_TYPE, PERP_ORDER_TYPE, TOKEN_PERMISSIONS_TYPE)
    );
```

### L-11 The Consctructor not disable

**description** The `initialize` function is respons to initialze the contract , and we add the `initializer` modifier to make sure it will initialize only one time. but we have the constructor not disable so that break the process of using `initialize` function with `initializer` modifier.

```solidity (src/markets/gamma/GammaTradeMarket.sol)
    constructor() {}

```
```solidity (src\PredyPool.sol)
    constructor() {}

```
**Recommandation** Should disable the constructor :

```diff

+ /// @custom:oz-upgrades-unsafe-allow constructor
+ constructor() {
+     _disableInitializers();
+ }

```

