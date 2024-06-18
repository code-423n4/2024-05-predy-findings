## Summary

| |Issue|Instances| 
|-|:-|:-:|
| [[L-01](#l-01)] | Large transfers may not work with some `ERC20` tokens | 26| 
| [[L-02](#l-02)] | Solmate's SafeTransferLib does not check for token contract's existence | 26| 
| [[L-03](#l-03)] | Missing L2 sequencer checks for Chainlink oracle | 1| 
| [[L-04](#l-04)] | Chainlink oracle will return the wrong price if the aggregator hits `minAnswer` | 1| 
| [[L-05](#l-05)] | Consider adding validation of user inputs | 26| 
| [[L-06](#l-06)] | Execution at deadlines should be allowed(Not captured by 4nalyzer) | 1| 
| [[L-07](#l-07)] | Consider bounding input array length | 2| 
| [[L-08](#l-08)] | Privileged functions can create points of failure(Not captured by 4nalyzer) | 24| 
| [[L-09](#l-09)] | Code does not follow the best practice of check-effects-interaction | 3| 
| [[L-10](#l-10)] | Do not leave an implementation contract uninitialized | 3| 
| [[L-11](#l-11)] | Events may be emitted out of order due to reentrancy | 14| 
| [[L-12](#l-12)] | `forceApprove` should be used instead of `approve` | 4| 
| [[L-13](#l-13)] | Functions calling contracts/addresses with transfer hooks are missing reentrancy guards | 15| 
| [[L-14](#l-14)] | Initializers can be front-run(Not captured by 4nalyzer) | 1| 
| [[L-15](#l-15)] | Library function isn't `internal` or `private` | 18| 
| [[L-16](#l-16)] | Loss of precision on division(Not captured by 4nalyzer) | 1| 
| [[L-17](#l-17)] | Mapping arrays can grow in size without a way to shrink them | 1| 
| [[L-18](#l-18)] | Missing zero address check in constructor | 6| 
| [[L-19](#l-19)] | Missing checks for `address(0x0)` when updating `address` state variables | 8| 
| [[L-20](#l-20)] | Named return variable used before assignment | 1| 
| [[L-21](#l-21)] | Variables shadowing other definitions | 23| 
| [[L-22](#l-22)] | File allows a version of solidity that is susceptible to `.selector` related optimizer bug | 2| 
| [[L-23](#l-23)] | File allows a version of solidity that is susceptible to an assembly optimizer bug | 55| 
| [[L-24](#l-24)] | Solidity version `0.8.20` may not work on other chains due to `PUSH0` | 55| 
| [[L-25](#l-25)] | State variables not capped at reasonable values | 1| 
| [[L-26](#l-26)] | Consider implementing two-step procedure for updating protocol addresses | 7| 
| [[L-27](#l-27)] | Consider using OpenZeppelin's SafeCast library to prevent unexpected overflows when downcasting | 1| 
| [[L-28](#l-28)] | Using zero as a parameter | 3| 
| [[L-29](#l-29)] | Some `ERC20` can revert on a zero value `transfer` | 22| 

### Low Risk Issues

### [L-01]<a name="l-01"></a> Large transfers may not work with some `ERC20` tokens

Some `IERC20` implementations (e.g `UNI`, `COMP`) may fail if the valued transferred is larger than `uint96`. [Source](https://github.com/d-xo/weird-erc20#revert-on-large-approvals--transfers)

*There are 26 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

85:             ERC20(uniswapPool.token0()).safeTransfer(msg.sender, amount0);

88:             ERC20(uniswapPool.token1()).safeTransfer(msg.sender, amount1);

187:             ERC20(pool.token).safeTransfer(msg.sender, amount);

209:             ERC20(pool.token).safeTransfer(msg.sender, amount);

```


*GitHub* : [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L85-L85), [88](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L88-L88), [187](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L187-L187), [209](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L209-L209)

```solidity
📁 File: src/base/SettlementCallbackLib.sol

48:             ERC20(quoteToken).safeTransferFrom(

105:             ERC20(quoteToken).safeTransferFrom(sender, address(predyPool), quoteAmount);

123:             ERC20(quoteToken).safeTransfer(address(predyPool), quoteAmountFromUni);

128:                 ERC20(quoteToken).safeTransferFrom(sender, address(this), quoteAmount - quoteAmountFromUni);

130:                 ERC20(quoteToken).safeTransfer(sender, quoteAmountFromUni - quoteAmount);

133:             ERC20(quoteToken).safeTransfer(address(predyPool), quoteAmount);

152:             ERC20(baseToken).safeTransferFrom(sender, address(predyPool), buyAmount);

170:             ERC20(quoteToken).safeTransfer(address(predyPool), settlementParams.maxQuoteAmount - quoteAmountToUni);

175:                 ERC20(quoteToken).safeTransfer(sender, quoteAmount - quoteAmountToUni);

177:                 ERC20(quoteToken).safeTransferFrom(sender, address(this), quoteAmountToUni - quoteAmount);

180:             ERC20(quoteToken).safeTransfer(address(predyPool), settlementParams.maxQuoteAmount - quoteAmount);

```


*GitHub* : [48](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L48-L48), [105](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L105-L105), [123](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L123-L123), [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L128-L128), [130](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L130-L130), [133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L133-L133), [152](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L152-L152), [170](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L170-L170), [175](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L175-L175), [177](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L177-L177), [180](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L180-L180)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

99:                     ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);

106:                 ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));

```


*GitHub* : [99](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L99-L99), [106](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L106-L106)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

69:                     ERC20(pairStatus.quotePool.token).safeTransfer(msg.sender, uint256(exceedsQuote));

```


*GitHub* : [69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L69-L69)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

52:         ERC20(_pool.token).safeTransferFrom(msg.sender, address(this), _amount);

90:         ERC20(_pool.token).safeTransfer(msg.sender, finalWithdrawalAmount);

```


*GitHub* : [52](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L52-L52), [90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L90-L90)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

118:                     quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));

```


*GitHub* : [118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L118-L118)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

126:                 quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));

```


*GitHub* : [126](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L126-L126)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

30:         ERC20(baseToken).safeTransferFrom(msg.sender, address(this), amountIn);

46:         ERC20(quoteToken).safeTransferFrom(msg.sender, address(this), amountInMaximum);

54:             ERC20(quoteToken).safeTransfer(msg.sender, amountInMaximum - amountIn);

```


*GitHub* : [30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L30-L30), [46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L46-L46), [54](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L54-L54)

```solidity
📁 File: src/types/GlobalData.sol

85:         ERC20(currency).safeTransfer(to, amount);

```


*GitHub* : [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L85-L85)

### [L-02]<a name="l-02"></a> Solmate's SafeTransferLib does not check for token contract's existence

There is a subtle difference between the implementation of solmate’s SafeTransferLib and OZ’s SafeERC20: OZ’s SafeERC20 checks if the token is a contract or not, solmate’s SafeTransferLib does not.
https://github.com/transmissions11/solmate/blob/main/src/utils/SafeTransferLib.sol#L9 
`@dev Note that none of the functions in this library check that a token has code at all! That responsibility is delegated to the caller` 


*There are 26 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

85:             ERC20(uniswapPool.token0()).safeTransfer(msg.sender, amount0);

88:             ERC20(uniswapPool.token1()).safeTransfer(msg.sender, amount1);

187:             ERC20(pool.token).safeTransfer(msg.sender, amount);

209:             ERC20(pool.token).safeTransfer(msg.sender, amount);

```


*GitHub* : [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L85-L85), [88](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L88-L88), [187](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L187-L187), [209](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L209-L209)

```solidity
📁 File: src/base/SettlementCallbackLib.sol

48:             ERC20(quoteToken).safeTransferFrom(

105:             ERC20(quoteToken).safeTransferFrom(sender, address(predyPool), quoteAmount);

123:             ERC20(quoteToken).safeTransfer(address(predyPool), quoteAmountFromUni);

128:                 ERC20(quoteToken).safeTransferFrom(sender, address(this), quoteAmount - quoteAmountFromUni);

130:                 ERC20(quoteToken).safeTransfer(sender, quoteAmountFromUni - quoteAmount);

133:             ERC20(quoteToken).safeTransfer(address(predyPool), quoteAmount);

152:             ERC20(baseToken).safeTransferFrom(sender, address(predyPool), buyAmount);

170:             ERC20(quoteToken).safeTransfer(address(predyPool), settlementParams.maxQuoteAmount - quoteAmountToUni);

175:                 ERC20(quoteToken).safeTransfer(sender, quoteAmount - quoteAmountToUni);

177:                 ERC20(quoteToken).safeTransferFrom(sender, address(this), quoteAmountToUni - quoteAmount);

180:             ERC20(quoteToken).safeTransfer(address(predyPool), settlementParams.maxQuoteAmount - quoteAmount);

```


*GitHub* : [48](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L48-L48), [105](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L105-L105), [123](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L123-L123), [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L128-L128), [130](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L130-L130), [133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L133-L133), [152](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L152-L152), [170](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L170-L170), [175](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L175-L175), [177](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L177-L177), [180](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L180-L180)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

99:                     ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);

106:                 ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));

```


*GitHub* : [99](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L99-L99), [106](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L106-L106)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

69:                     ERC20(pairStatus.quotePool.token).safeTransfer(msg.sender, uint256(exceedsQuote));

```


*GitHub* : [69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L69-L69)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

52:         ERC20(_pool.token).safeTransferFrom(msg.sender, address(this), _amount);

90:         ERC20(_pool.token).safeTransfer(msg.sender, finalWithdrawalAmount);

```


*GitHub* : [52](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L52-L52), [90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L90-L90)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

118:                     quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));

```


*GitHub* : [118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L118-L118)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

126:                 quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));

```


*GitHub* : [126](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L126-L126)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

30:         ERC20(baseToken).safeTransferFrom(msg.sender, address(this), amountIn);

46:         ERC20(quoteToken).safeTransferFrom(msg.sender, address(this), amountInMaximum);

54:             ERC20(quoteToken).safeTransfer(msg.sender, amountInMaximum - amountIn);

```


*GitHub* : [30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L30-L30), [46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L46-L46), [54](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L54-L54)

```solidity
📁 File: src/types/GlobalData.sol

85:         ERC20(currency).safeTransfer(to, amount);

```


*GitHub* : [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L85-L85)

### [L-03]<a name="l-03"></a> Missing L2 sequencer checks for Chainlink oracle

Using Chainlink in L2 chains such as Arbitrum [requires](https://docs.chain.link/data-feeds/l2-sequencer-feeds) to check if the sequencer is down to avoid prices from looking like they are fresh although they are not.

The bug could be leveraged by malicious actors to take advantage of the sequencer downtime.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/PriceFeed.sol

// @audit missing sequencer up or down checks
// @audit missing sequencer uptime, grace period checks
46:         (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

```


*GitHub* : [46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L46-L46)

### [L-04]<a name="l-04"></a> Chainlink oracle will return the wrong price if the aggregator hits `minAnswer`

Chainlink aggregators have a built-in circuit breaker if the price of an asset goes outside of a predetermined price band.

The result is that if an asset experiences a huge drop in value (i.e. LUNA crash) the price of the oracle will continue to return the minPrice instead of the actual price of the asset.

This would allow users to continue borrowing with the asset but at the wrong price. This is exactly what happened to Venus on BSC when LUNA [crashed](https://rekt.news/venus-blizz-rekt/).

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/PriceFeed.sol

// @audit missing min/max price check
46:         (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

```


*GitHub* : [46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L46-L46)

### [L-05]<a name="l-05"></a> Consider adding validation of user inputs

There are no validations done on the arguments below. Consider that the Solidity [documentation](https://docs.soliditylang.org/en/latest/control-structures.html#panic-via-assert-and-error-via-require) states that `Properly functioning code should never create a Panic, not even on invalid external input. If this happens, then there is a bug in your contract which you should fix`. This means that there should be explicit checks for expected ranges of inputs. Underflows/overflows result in panics should not be used as range checks, and allowing funds to be sent to `0x0`, which is the default value of address variables and has many gotchas, should be avoided.

*There are 26 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

// @audit missing checks for -->  uniswapFactory
70:     function initialize(address uniswapFactory) public initializer {

// @audit missing checks for -->  poolOwner
157:     function updatePoolOwner(uint256 pairId, address poolOwner) external onlyPoolOwner(pairId) {

// @audit missing checks for -->  priceFeed
167:     function updatePriceOracle(uint256 pairId, address priceFeed) external onlyPoolOwner(pairId) {

// @audit missing checks for -->  recipient
286:     function updateRecepient(uint256 vaultId, address recipient) external onlyVaultOwner(vaultId) {

// @audit missing checks for -->  trader
300:     function allowTrader(uint256 pairId, address trader, bool enabled) external onlyPoolOwner(pairId) {

// @audit missing checks for -->  to
329:     function take(bool isQuoteAsset, address to, uint256 amount) external onlyByLocker {

```


*GitHub* : [70](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L70-L70), [157](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L157-L157), [167](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L167-L167), [286](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L286-L286), [300](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L300-L300), [329](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L329-L329)

```solidity
📁 File: src/PriceFeed.sol

// @audit missing checks for -->  quotePrice
18:     function createPriceFeed(address quotePrice, bytes32 priceId, uint256 decimalsDiff) external returns (address) {

```


*GitHub* : [18](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L18-L18)

```solidity
📁 File: src/base/BaseMarket.sol

// @audit missing checks for -->  quoteToken, baseToken
28:     function predySettlementCallback(
29:         address quoteToken,
30:         address baseToken,
31:         bytes memory settlementData,
32:         int256 baseAmountDelta
33:     ) external onlyPredyPool {

// @audit missing checks for -->  newWhitelistFiller
84:     function updateWhitelistFiller(address newWhitelistFiller) external onlyOwner {

// @audit missing checks for -->  settlementContractAddress
92:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyOwner {

```


*GitHub* : [28](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L28-L33), [84](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L84-L84), [92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L92-L92)

```solidity
📁 File: src/base/BaseMarketUpgradable.sol

// @audit missing checks for -->  quoteToken, baseToken
49:     function predySettlementCallback(
50:         address quoteToken,
51:         address baseToken,
52:         bytes memory settlementData,
53:         int256 baseAmountDelta
54:     ) external onlyPredyPool {

// @audit missing checks for -->  newWhitelistFiller
128:     function updateWhitelistFiller(address newWhitelistFiller) external onlyFiller {

// @audit missing checks for -->  newQuoter
132:     function updateQuoter(address newQuoter) external onlyFiller {

// @audit missing checks for -->  settlementContractAddress
140:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyFiller {

```


*GitHub* : [49](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L49-L54), [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L128-L128), [132](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L132-L132), [140](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L140-L140)

```solidity
📁 File: src/libraries/logic/AddPairLogic.sol

// @audit missing checks for -->  uniswapFactory
44:     function initializeGlobalData(GlobalDataLibrary.GlobalData storage global, address uniswapFactory) external {

// @audit missing checks for -->  _poolOwner
104:     function updatePoolOwner(DataType.PairStatus storage _pairStatus, address _poolOwner) external {

// @audit missing checks for -->  _priceOracle
112:     function updatePriceOracle(DataType.PairStatus storage _pairStatus, address _priceOracle) external {

```


*GitHub* : [44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L44-L44), [104](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L104-L104), [112](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L112-L112)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

// @audit missing checks for -->  predyPool, permit2Address, whitelistFiller, quoterAddress
69:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)
70:         public
71:         initializer
72:     {

// @audit missing checks for -->  owner
361:     function getUserPositions(address owner) external returns (UserPositionResult[] memory) {

```


*GitHub* : [69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L69-L72), [361](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L361-L361)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

// @audit missing checks for -->  predyPool, permit2Address, whitelistFiller, quoterAddress
92:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)
93:         public
94:         initializer
95:     {

// @audit missing checks for -->  owner
247:     function getUserPosition(address owner, uint256 pairId)
248:         external
249:         returns (
250:             UserPosition memory userPosition,
251:             IPredyPool.VaultStatus memory vaultStatus,
252:             DataType.Vault memory vault
253:         )
254:     {

// @audit missing checks for -->  filler
275:     function quoteExecuteOrderV3(
276:         PerpOrderV3 memory perpOrder,
277:         SettlementParamsV3 memory settlementParams,
278:         address filler
279:     ) external {

```


*GitHub* : [92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L92-L95), [247](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L247-L254), [275](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L275-L279)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

// @audit missing checks for -->  baseToken, recipient
22:     function swapExactIn(
23:         address,
24:         address baseToken,
25:         bytes memory data,
26:         uint256 amountIn,
27:         uint256 amountOutMinimum,
28:         address recipient
29:     ) external override returns (uint256 amountOut) {

// @audit missing checks for -->  quoteToken, recipient
38:     function swapExactOut(
39:         address quoteToken,
40:         address,
41:         bytes memory data,
42:         uint256 amountOut,
43:         uint256 amountInMaximum,
44:         address recipient
45:     ) external override returns (uint256 amountIn) {

```


*GitHub* : [22](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L22-L29), [38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L38-L45)

```solidity
📁 File: src/tokenization/SupplyToken.sol

// @audit missing checks for -->  account
21:     function mint(address account, uint256 amount) external virtual override onlyController {

// @audit missing checks for -->  account
25:     function burn(address account, uint256 amount) external virtual override onlyController {

```


*GitHub* : [21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/tokenization/SupplyToken.sol#L21-L21), [25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/tokenization/SupplyToken.sol#L25-L25)

### [L-06]<a name="l-06"></a> Execution at deadlines should be allowed(Not captured by 4nalyzer)

The condition may be wrong in these cases, as when block.timestamp is equal to the compared `>` or `<` variable these blocks will not be executed.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/libraries/orders/ResolvedOrder.sol

28:         if (block.timestamp > resolvedOrder.info.deadline) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/ResolvedOrder.sol#L28-L28)

### [L-07]<a name="l-07"></a> Consider bounding input array length

Unbounded array inputs in functions can lead to unintentional excessive gas consumption, potentially causing a transaction to revert after expending substantial gas. To enhance user experience and prevent such scenarios, consider implementing a `require()` statement that limits the array length to a defined maximum. This constraint ensures that transactions won't proceed if they're likely to hit gas limits due to array size, saving users from unnecessary gas costs and offering a more predictable interaction with the contract.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/markets/gamma/ArrayLib.sol

//@audit items.length not bounded 
23:         for (uint256 i = 0; i < items.length; i++) {

```


*GitHub* : [23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/ArrayLib.sol#L23-L23)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

//@audit userPositionIDs.length not bounded 
366:         for (uint64 i = 0; i < userPositionIDs.length; i++) {

```


*GitHub* : [366](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L366-L366)

### [L-08]<a name="l-08"></a> Privileged functions can create points of failure(Not captured by 4nalyzer)

Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

*There are 24 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

97:     function setOperator(address newOperator) external onlyOperator {

109:     function registerPair(AddPairLogic.AddPairParams memory addPairParam) external onlyOperator returns (uint256) {

119:     function updateAssetRiskParams(uint256 pairId, Perp.AssetRiskParams memory riskParams)
120:         external
121:         onlyPoolOwner(pairId)
122:     {

133:     function updateIRMParams(
134:         uint256 pairId,
135:         InterestRateModel.IRMParams memory quoteIrmParams,
136:         InterestRateModel.IRMParams memory baseIrmParams
137:     ) external onlyPoolOwner(pairId) {

147:     function updateFeeRatio(uint256 pairId, uint8 feeRatio) external onlyPoolOwner(pairId) {

157:     function updatePoolOwner(uint256 pairId, address poolOwner) external onlyPoolOwner(pairId) {

167:     function updatePriceOracle(uint256 pairId, address priceFeed) external onlyPoolOwner(pairId) {

177:     function withdrawProtocolRevenue(uint256 pairId, bool isQuoteToken) external onlyOperator {

199:     function withdrawCreatorRevenue(uint256 pairId, bool isQuoteToken) external onlyPoolOwner(pairId) {

286:     function updateRecepient(uint256 vaultId, address recipient) external onlyVaultOwner(vaultId) {

300:     function allowTrader(uint256 pairId, address trader, bool enabled) external onlyPoolOwner(pairId) {

329:     function take(bool isQuoteAsset, address to, uint256 amount) external onlyByLocker {

```


*GitHub* : [97](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L97-L97), [109](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L109-L109), [119](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L119-L122), [133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L133-L137), [147](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L147-L147), [157](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L157-L157), [167](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L167-L167), [177](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L177-L177), [199](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L199-L199), [286](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L286-L286), [300](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L300-L300), [329](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L329-L329)

```solidity
📁 File: src/base/BaseHookCallbackUpgradable.sol

20:     function __BaseHookCallback_init(IPredyPool predyPool) internal onlyInitializing {

```


*GitHub* : [20](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseHookCallbackUpgradable.sol#L20-L20)

```solidity
📁 File: src/base/BaseMarket.sol

28:     function predySettlementCallback(
29:         address quoteToken,
30:         address baseToken,
31:         bytes memory settlementData,
32:         int256 baseAmountDelta
33:     ) external onlyPredyPool {

```


*GitHub* : [28](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L28-L33)

```solidity
📁 File: src/base/BaseMarketUpgradable.sol

38:     function __BaseMarket_init(IPredyPool predyPool, address _whitelistFiller, address quoterAddress)
39:         internal
40:         onlyInitializing
41:     {

49:     function predySettlementCallback(
50:         address quoteToken,
51:         address baseToken,
52:         bytes memory settlementData,
53:         int256 baseAmountDelta
54:     ) external onlyPredyPool {

128:     function updateWhitelistFiller(address newWhitelistFiller) external onlyFiller {

132:     function updateQuoter(address newQuoter) external onlyFiller {

140:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyFiller {

```


*GitHub* : [38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L38-L41), [49](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L49-L54), [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L128-L128), [132](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L132-L132), [140](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L140-L140)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

79:     function predyTradeAfterCallback(
80:         IPredyPool.TradeParams memory tradeParams,
81:         IPredyPool.TradeResult memory tradeResult
82:     ) external override(BaseHookCallbackUpgradable) onlyPredyPool {

392:     function removePosition(uint256 positionId) external onlyFiller {

```


*GitHub* : [79](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L79-L82), [392](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L392-L392)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

102:     function predyTradeAfterCallback(
103:         IPredyPool.TradeParams memory tradeParams,
104:         IPredyPool.TradeResult memory tradeResult
105:     ) external override(BaseHookCallbackUpgradable) onlyPredyPool {

```


*GitHub* : [102](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L102-L105)

```solidity
📁 File: src/tokenization/SupplyToken.sol

21:     function mint(address account, uint256 amount) external virtual override onlyController {

25:     function burn(address account, uint256 amount) external virtual override onlyController {

```


*GitHub* : [21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/tokenization/SupplyToken.sol#L21-L21), [25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/tokenization/SupplyToken.sol#L25-L25)

### [L-09]<a name="l-09"></a> Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [CEI](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

// @audit AddPairLogic.initializeGlobalData() called on line 72 
74:         operator = msg.sender;

// @audit globalData.validate() called on line 270 
276:         tradeParams.vaultId = globalData.createOrGetVault(tradeParams.vaultId, tradeParams.pairId);

```


*GitHub* : [74](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L74-L74), [276](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L276-L276)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

// @audit  ERC20(baseToken).approve() called on line 31 
33:         amountOut = _swapRouter.exactInput(

```


*GitHub* : [33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L33-L33)

### [L-10]<a name="l-10"></a> Do not leave an implementation contract uninitialized

An uninitialized implementation contract can be taken over by an attacker, which may impact the proxy. To prevent the implementation contract from being used, it's advisable to invoke the `_disableInitializers` function in the constructor to automatically lock it when it is deployed. This should look similar to this:
```solidity
  /// @custom:oz-upgrades-unsafe-allow constructor
  constructor() {
      _disableInitializers();
  }
```

Sources:
- https://docs.openzeppelin.com/contracts/4.x/api/proxy#Initializable-_disableInitializers--
- https://twitter.com/0xCygaar/status/1621417995905167360?s=20

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

68:     constructor() {}

```


*GitHub* : [68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L68-L68)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

67:     constructor() {}

```


*GitHub* : [67](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L67-L67)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

90:     constructor() {}

```


*GitHub* : [90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L90-L90)

### [L-11]<a name="l-11"></a> Events may be emitted out of order due to reentrancy

If a reentrancy occurs, some events may be emitted in an unexpected order, and this may be a problem if a third party expects a specific order for these events. Ensure that events are emitted before external calls and follow the best practice of CEI.

*There are 14 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

190:         emit ProtocolRevenueWithdrawn(pairId, isQuoteToken, amount);

212:         emit CreatorRevenueWithdrawn(pairId, isQuoteToken, amount);

```


*GitHub* : [190](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L190-L190), [212](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L212-L212)

```solidity
📁 File: src/libraries/Perp.sol

411:         emit PremiumGrowthUpdated(_pairId, _assetStatus.totalAmount, _assetStatus.borrowedAmount, f0, f1, spreadParam);

```


*GitHub* : [411](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Perp.sol#L411-L411)

```solidity
📁 File: src/libraries/Trade.sol

107:         emit Swapped(pairId, vaultId, msg.sender, settledQuoteAmount, settledBaseAmount);

```


*GitHub* : [107](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L107-L107)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

110:         emit PositionLiquidated(
111:             tradeParams.vaultId,
112:             tradeParams.pairId,
113:             tradeParams.tradeAmount,
114:             tradeParams.tradeAmountSqrt,
115:             tradeResult.payoff,
116:             tradeResult.fee,
117:             sentMarginAmount
118:         );

```


*GitHub* : [110](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L110-L118)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

73:             emit Rebalanced(
74:                 pairId,
75:                 relocationOccurred,
76:                 pairStatus.sqrtAssetStatus.tickLower,
77:                 pairStatus.sqrtAssetStatus.tickUpper,
78:                 deltaPositionBase,
79:                 deltaPositionQuote
80:             );

```


*GitHub* : [73](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L73-L80)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

43:         emit TokenSupplied(msg.sender, pair.id, _isStable, _amount);

76:         emit TokenWithdrawn(msg.sender, pair.id, _isStable, finalWithdrawalAmount);

```


*GitHub* : [43](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L43-L43), [76](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L76-L76)

```solidity
📁 File: src/libraries/logic/TradeLogic.sol

58:         emit PositionUpdated(
59:             tradeParams.vaultId,
60:             tradeParams.pairId,
61:             tradeParams.tradeAmount,
62:             tradeParams.tradeAmountSqrt,
63:             tradeResult.payoff,
64:             tradeResult.fee
65:         );

85:         emit MarginUpdated(tradeParams.vaultId, marginAmountUpdate);

```


*GitHub* : [58](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/TradeLogic.sol#L58-L65), [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/TradeLogic.sol#L85-L85)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

101:                 emit GammaPositionTraded(
102:                     callbackData.trader,
103:                     tradeParams.pairId,
104:                     tradeParams.vaultId,
105:                     tradeParams.tradeAmount,
106:                     tradeParams.tradeAmountSqrt,
107:                     tradeResult.payoff,
108:                     tradeResult.fee,
109:                     -vault.margin,
110:                     callbackData.callbackType == GammaTradeMarketLib.CallbackType.TRADE
111:                         ? GammaTradeMarketLib.CallbackType.CLOSE
112:                         : callbackData.callbackType
113:                 );

123:                 emit GammaPositionTraded(
124:                     callbackData.trader,
125:                     tradeParams.pairId,
126:                     tradeParams.vaultId,
127:                     tradeParams.tradeAmount,
128:                     tradeParams.tradeAmountSqrt,
129:                     tradeResult.payoff,
130:                     tradeResult.fee,
131:                     marginAmountUpdate,
132:                     callbackData.callbackType
133:                 );

440:             emit GammaPositionModified(userPosition.owner, userPosition.pairId, userPosition.vaultId, modifyInfo);

```


*GitHub* : [101](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L101-L113), [123](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L123-L133), [440](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L440-L440)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

131:             emit PerpTraded2(
132:                 callbackData.trader,
133:                 tradeParams.pairId,
134:                 tradeResult.vaultId,
135:                 tradeParams.tradeAmount,
136:                 tradeResult.payoff,
137:                 tradeResult.fee,
138:                 marginAmountUpdate,
139:                 callbackData.orderId
140:             );

```


*GitHub* : [131](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L131-L140)

### [L-12]<a name="l-12"></a> `forceApprove` should be used instead of `approve`

Code uses the `approve` method to set allowance for ERC20 tokens. This will cause revert if the target ERC20 was a non-standard token that has different function signature for `approve()`.Eg:[USDT](https://etherscan.io/address/0xdac17f958d2ee523a2206206994597c13d831ec7#code#L126)

Use OpenZeppelin’s `SafeERC20:: forceApprove` method instead to support all the ERC20 tokens.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/base/SettlementCallbackLib.sol

111:         ERC20(baseToken).approve(address(settlementParams.contractAddress), sellAmount);

158:         ERC20(quoteToken).approve(address(settlementParams.contractAddress), settlementParams.maxQuoteAmount);

```


*GitHub* : [111](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L111-L111), [158](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L158-L158)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

31:         ERC20(baseToken).approve(address(_swapRouter), amountIn);

47:         ERC20(quoteToken).approve(address(_swapRouter), amountInMaximum);

```


*GitHub* : [31](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L31-L31), [47](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L47-L47)

### [L-13]<a name="l-13"></a> Functions calling contracts/addresses with transfer hooks are missing reentrancy guards

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks will open the users of this protocol up to [read-only reentrancies](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect against it, except by block-listing the whole protocol.

*There are 15 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

// @audit function 'uniswapV3MintCallback()' is missing Reentrancy guard
85:             ERC20(uniswapPool.token0()).safeTransfer(msg.sender, amount0);

// @audit function 'withdrawProtocolRevenue()' is missing Reentrancy guard
187:             ERC20(pool.token).safeTransfer(msg.sender, amount);

// @audit function 'withdrawCreatorRevenue()' is missing Reentrancy guard
209:             ERC20(pool.token).safeTransfer(msg.sender, amount);

```


*GitHub* : [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L85-L85), [187](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L187-L187), [209](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L209-L209)

```solidity
📁 File: src/base/SettlementCallbackLib.sol

// @audit function 'execSettlement()' is missing Reentrancy guard
48:             ERC20(quoteToken).safeTransferFrom(

// @audit function 'sell()' is missing Reentrancy guard
105:             ERC20(quoteToken).safeTransferFrom(sender, address(predyPool), quoteAmount);

// @audit function 'buy()' is missing Reentrancy guard
152:             ERC20(baseToken).safeTransferFrom(sender, address(predyPool), buyAmount);

```


*GitHub* : [48](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L48-L48), [105](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L105-L105), [152](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L152-L152)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

// @audit function 'liquidate()' is missing Reentrancy guard
99:                     ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);

```


*GitHub* : [99](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L99-L99)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

// @audit function 'reallocate()' is missing Reentrancy guard
69:                     ERC20(pairStatus.quotePool.token).safeTransfer(msg.sender, uint256(exceedsQuote));

```


*GitHub* : [69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L69-L69)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

// @audit function 'receiveTokenAndMintBond()' is missing Reentrancy guard
52:         ERC20(_pool.token).safeTransferFrom(msg.sender, address(this), _amount);

// @audit function 'burnBondAndTransferToken()' is missing Reentrancy guard
90:         ERC20(_pool.token).safeTransfer(msg.sender, finalWithdrawalAmount);

```


*GitHub* : [52](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L52-L52), [90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L90-L90)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

// @audit function 'predyTradeAfterCallback()' is missing Reentrancy guard
118:                     quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));

```


*GitHub* : [118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L118-L118)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

// @audit function 'predyTradeAfterCallback()' is missing Reentrancy guard
126:                 quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));

```


*GitHub* : [126](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L126-L126)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

// @audit function 'swapExactIn()' is missing Reentrancy guard
30:         ERC20(baseToken).safeTransferFrom(msg.sender, address(this), amountIn);

// @audit function 'swapExactOut()' is missing Reentrancy guard
46:         ERC20(quoteToken).safeTransferFrom(msg.sender, address(this), amountInMaximum);

```


*GitHub* : [30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L30-L30), [46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L46-L46)

```solidity
📁 File: src/types/GlobalData.sol

// @audit function 'take()' is missing Reentrancy guard
85:         ERC20(currency).safeTransfer(to, amount);

```


*GitHub* : [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L85-L85)

### [L-14]<a name="l-14"></a> Initializers can be front-run(Not captured by 4nalyzer)

Initializers could be front-run, allowing an attacker to either set their own values, take ownership of the contract, and in the best case forcing a re-deployment.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/libraries/logic/AddPairLogic.sol

44:     function initializeGlobalData(GlobalDataLibrary.GlobalData storage global, address uniswapFactory) external {
45:         global.pairsCount = 1;
46:         global.vaultCount = 1;
47:         global.uniswapFactory = uniswapFactory;
48:     }

```


*GitHub* : [44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L44-L48)

### [L-15]<a name="l-15"></a> Library function isn't `internal` or `private`

In a library, using an external or public visibility means that we won't be going through the library with a DELEGATECALL but with a CALL. This changes the context and should be done carefully.

*There are 18 instance(s) of this issue:*

```solidity
📁 File: src/libraries/Trade.sol

32:     function trade(
33:         GlobalDataLibrary.GlobalData storage globalData,
34:         IPredyPool.TradeParams memory tradeParams,
35:         bytes memory settlementData
36:     ) external returns (IPredyPool.TradeResult memory tradeResult) {
37:         DataType.PairStatus storage pairStatus = globalData.pairs[tradeParams.pairId];
38:         Perp.UserStatus storage openPosition = globalData.vaults[tradeParams.vaultId].openPosition;
39: 
40:         // settle user balance and fee
41:         DataType.FeeAmount memory realizedFee =
42:             settleUserBalanceAndFee(pairStatus, globalData.rebalanceFeeGrowthCache, openPosition);
43: 
44:         // calculate required token amounts
45:         (int256 underlyingAmountForSqrt, int256 stableAmountForSqrt) = Perp.computeRequiredAmounts(
46:             pairStatus.sqrtAssetStatus, pairStatus.isQuoteZero, openPosition, tradeParams.tradeAmountSqrt
47:         );
48: 
49:         tradeResult.sqrtPrice = getSqrtPrice(pairStatus.sqrtAssetStatus.uniswapPool, pairStatus.isQuoteZero);
50: 
51:         // swap tokens
52: 
53:         SwapStableResult memory swapResult = swap(
54:             globalData,
55:             tradeParams.pairId,
56:             SwapStableResult(-tradeParams.tradeAmount, underlyingAmountForSqrt, realizedFee.feeAmountBase, 0),
57:             settlementData,
58:             tradeResult.sqrtPrice,
59:             tradeParams.vaultId
60:         );
61: 
62:         tradeResult.averagePrice = swapResult.averagePrice;
63: 
64:         // add asset or debt
65:         tradeResult.payoff = Perp.updatePosition(
66:             pairStatus,
67:             openPosition,
68:             Perp.UpdatePerpParams(tradeParams.tradeAmount, swapResult.amountPerp),
69:             Perp.UpdateSqrtPerpParams(tradeParams.tradeAmountSqrt, swapResult.amountSqrtPerp + stableAmountForSqrt)
70:         );
71: 
72:         tradeResult.fee = realizedFee.feeAmountQuote + swapResult.fee;
73:         tradeResult.vaultId = tradeParams.vaultId;
74:     }

```


*GitHub* : [32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L32-L74)

```solidity
📁 File: src/libraries/logic/AddPairLogic.sol

44:     function initializeGlobalData(GlobalDataLibrary.GlobalData storage global, address uniswapFactory) external {
45:         global.pairsCount = 1;
46:         global.vaultCount = 1;
47:         global.uniswapFactory = uniswapFactory;
48:     }

53:     function addPair(
54:         GlobalDataLibrary.GlobalData storage _global,
55:         mapping(address => bool) storage allowedUniswapPools,
56:         AddPairParams memory _addPairParam
57:     ) external returns (uint256 pairId) {
58:         pairId = _global.pairsCount;
59: 
60:         require(pairId < Constants.MAX_PAIRS, "MAXP");
61: 
62:         IUniswapV3Pool uniswapPool = IUniswapV3Pool(_addPairParam.uniswapPool);
63: 
64:         address stableTokenAddress = _addPairParam.quoteToken;
65: 
66:         IUniswapV3Factory uniswapV3Factory = IUniswapV3Factory(_global.uniswapFactory);
67: 
68:         // check the uniswap pool is registered in UniswapV3Factory
69:         if (
70:             uniswapV3Factory.getPool(uniswapPool.token0(), uniswapPool.token1(), uniswapPool.fee())
71:                 != _addPairParam.uniswapPool
72:         ) {
73:             revert InvalidUniswapPool();
74:         }
75: 
76:         require(uniswapPool.token0() == stableTokenAddress || uniswapPool.token1() == stableTokenAddress, "C3");
77: 
78:         bool isQuoteZero = uniswapPool.token0() == stableTokenAddress;
79: 
80:         _storePairStatus(
81:             stableTokenAddress,
82:             _global.pairs,
83:             pairId,
84:             isQuoteZero ? uniswapPool.token1() : uniswapPool.token0(),
85:             isQuoteZero,
86:             _addPairParam
87:         );
88: 
89:         allowedUniswapPools[_addPairParam.uniswapPool] = true;
90: 
91:         _global.pairsCount++;
92: 
93:         emit PairAdded(pairId, _addPairParam.quoteToken, _addPairParam.uniswapPool);
94:     }

96:     function updateFeeRatio(DataType.PairStatus storage _pairStatus, uint8 _feeRatio) external {
97:         validateFeeRatio(_feeRatio);
98: 
99:         _pairStatus.feeRatio = _feeRatio;
100: 
101:         emit FeeRatioUpdated(_pairStatus.id, _feeRatio);
102:     }

104:     function updatePoolOwner(DataType.PairStatus storage _pairStatus, address _poolOwner) external {
105:         validatePoolOwner(_poolOwner);
106: 
107:         _pairStatus.poolOwner = _poolOwner;
108: 
109:         emit PoolOwnerUpdated(_pairStatus.id, _poolOwner);
110:     }

112:     function updatePriceOracle(DataType.PairStatus storage _pairStatus, address _priceOracle) external {
113:         _pairStatus.priceFeed = _priceOracle;
114: 
115:         emit PriceOracleUpdated(_pairStatus.id, _priceOracle);
116:     }

118:     function updateAssetRiskParams(DataType.PairStatus storage _pairStatus, Perp.AssetRiskParams memory _riskParams)
119:         external
120:     {
121:         validateRiskParams(_riskParams);
122: 
123:         _pairStatus.riskParams = _riskParams;
124: 
125:         emit AssetRiskParamsUpdated(_pairStatus.id, _riskParams);
126:     }

128:     function updateIRMParams(
129:         DataType.PairStatus storage _pairStatus,
130:         InterestRateModel.IRMParams memory _quoteIrmParams,
131:         InterestRateModel.IRMParams memory _baseIrmParams
132:     ) external {
133:         validateIRMParams(_quoteIrmParams);
134:         validateIRMParams(_baseIrmParams);
135: 
136:         _pairStatus.quotePool.irmParams = _quoteIrmParams;
137:         _pairStatus.basePool.irmParams = _baseIrmParams;
138: 
139:         emit IRMParamsUpdated(_pairStatus.id, _quoteIrmParams, _baseIrmParams);
140:     }

```


*GitHub* : [44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L44-L48), [53](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L53-L94), [96](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L96-L102), [104](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L104-L110), [112](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L112-L116), [118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L118-L126), [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L128-L140)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

39:     function liquidate(
40:         uint256 vaultId,
41:         uint256 closeRatio,
42:         GlobalDataLibrary.GlobalData storage globalData,
43:         bytes memory settlementData
44:     ) external returns (IPredyPool.TradeResult memory tradeResult) {
45:         require(closeRatio > 0 && closeRatio <= 1e18, "ICR");
46:         DataType.Vault storage vault = globalData.vaults[vaultId];
47:         DataType.PairStatus storage pairStatus = globalData.pairs[vault.openPosition.pairId];
48: 
49:         // update interest growth
50:         ApplyInterestLib.applyInterestForToken(globalData.pairs, vault.openPosition.pairId);
51: 
52:         // update rebalance interest growth
53:         Perp.updateRebalanceInterestGrowth(pairStatus, pairStatus.sqrtAssetStatus);
54: 
55:         // Checks the vault is danger
56:         (uint256 sqrtOraclePrice, uint256 slippageTolerance) =
57:             checkVaultIsDanger(pairStatus, vault, globalData.rebalanceFeeGrowthCache);
58: 
59:         IPredyPool.TradeParams memory tradeParams = IPredyPool.TradeParams(
60:             vault.openPosition.pairId,
61:             vaultId,
62:             -vault.openPosition.perp.amount * int256(closeRatio) / 1e18,
63:             -vault.openPosition.sqrtPerp.amount * int256(closeRatio) / 1e18,
64:             ""
65:         );
66: 
67:         tradeResult = Trade.trade(globalData, tradeParams, settlementData);
68: 
69:         vault.margin += tradeResult.fee + tradeResult.payoff.perpPayoff + tradeResult.payoff.sqrtPayoff;
70: 
71:         tradeResult.sqrtTwap = sqrtOraclePrice;
72: 
73:         bool hasPosition;
74: 
75:         (tradeResult.minMargin,, hasPosition,) =
76:             PositionCalculator.calculateMinMargin(pairStatus, vault, DataType.FeeAmount(0, 0));
77: 
78:         // Check if the price is within the slippage tolerance range to ensure that the price does not become
79:         // excessively favorable to the liquidator.
80:         SlippageLib.checkPrice(
81:             sqrtOraclePrice,
82:             tradeResult,
83:             slippageTolerance,
84:             tradeParams.tradeAmountSqrt == 0 ? 0 : _MAX_ACCEPTABLE_SQRT_PRICE_RANGE
85:         );
86: 
87:         uint256 sentMarginAmount = 0;
88: 
89:         if (!hasPosition) {
90:             int256 remainingMargin = vault.margin;
91: 
92:             if (remainingMargin > 0) {
93:                 if (vault.recipient != address(0)) {
94:                     // Send the remaining margin to the recipient.
95:                     vault.margin = 0;
96: 
97:                     sentMarginAmount = uint256(remainingMargin);
98: 
99:                     ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);
100:                 }
101:             } else if (remainingMargin < 0) {
102:                 vault.margin = 0;
103: 
104:                 // To prevent the liquidator from unfairly profiting through arbitrage trades in the AMM and passing losses onto the protocol,
105:                 // any losses that cannot be covered by the vault must be compensated by the liquidator
106:                 ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));
107:             }
108:         }
109: 
110:         emit PositionLiquidated(
111:             tradeParams.vaultId,
112:             tradeParams.pairId,
113:             tradeParams.tradeAmount,
114:             tradeParams.tradeAmountSqrt,
115:             tradeResult.payoff,
116:             tradeResult.fee,
117:             sentMarginAmount
118:         );
119:     }

```


*GitHub* : [39](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39-L119)

```solidity
📁 File: src/libraries/logic/ReaderLogic.sol

16:     function getPairStatus(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) external {
17:         ApplyInterestLib.applyInterestForToken(globalData.pairs, pairId);
18: 
19:         DataType.PairStatus memory pairStatus = globalData.pairs[pairId];
20: 
21:         revertPairStatus(pairStatus);
22:     }

24:     function getVaultStatus(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId) external {
25:         DataType.Vault memory vault = globalData.vaults[vaultId];
26:         DataType.PairStatus storage pairStatus = globalData.pairs[vault.openPosition.pairId];
27: 
28:         ApplyInterestLib.applyInterestForToken(globalData.pairs, vault.openPosition.pairId);
29: 
30:         Perp.updateRebalanceInterestGrowth(pairStatus, pairStatus.sqrtAssetStatus);
31: 
32:         DataType.FeeAmount memory feeAmount =
33:             PerpFee.computeUserFee(pairStatus, globalData.rebalanceFeeGrowthCache, vault.openPosition);
34: 
35:         (int256 minMargin, int256 vaultValue,, uint256 oraclePice) =
36:             PositionCalculator.calculateMinMargin(pairStatus, vault, feeAmount);
37: 
38:         revertVaultStatus(
39:             IPredyPool.VaultStatus(vaultId, vaultValue, minMargin, oraclePice, feeAmount, getPosition(vault, feeAmount))
40:         );
41:     }

```


*GitHub* : [16](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReaderLogic.sol#L16-L22), [24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReaderLogic.sol#L24-L41)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

27:     function reallocate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId, bytes memory settlementData)
28:         external
29:         returns (bool isRangeChanged)
30:     {
31:         // Checks the pair exists
32:         globalData.validate(pairId);
33: 
34:         // Updates interest rate related to the pair
35:         ApplyInterestLib.applyInterestForToken(globalData.pairs, pairId);
36: 
37:         DataType.PairStatus storage pairStatus = globalData.pairs[pairId];
38: 
39:         // Clear rebalance interests up to this block and update interest growth variables
40:         Perp.updateRebalanceInterestGrowth(pairStatus, pairStatus.sqrtAssetStatus);
41: 
42:         bool relocationOccurred;
43: 
44:         {
45:             int256 deltaPositionBase;
46:             int256 deltaPositionQuote;
47: 
48:             (relocationOccurred, isRangeChanged, deltaPositionBase, deltaPositionQuote) =
49:                 Perp.reallocate(pairStatus, pairStatus.sqrtAssetStatus);
50: 
51:             if (deltaPositionBase != 0) {
52:                 globalData.initializeLock(pairId);
53: 
54:                 globalData.callSettlementCallback(settlementData, deltaPositionBase);
55: 
56:                 (int256 settledQuoteAmount, int256 settledBaseAmount) = globalData.finalizeLock();
57: 
58:                 int256 exceedsQuote = settledQuoteAmount + deltaPositionQuote;
59: 
60:                 if (exceedsQuote < 0) {
61:                     revert IPredyPool.QuoteTokenNotSettled();
62:                 }
63: 
64:                 if (settledBaseAmount + deltaPositionBase != 0) {
65:                     revert IPredyPool.BaseTokenNotSettled();
66:                 }
67: 
68:                 if (exceedsQuote > 0) {
69:                     ERC20(pairStatus.quotePool.token).safeTransfer(msg.sender, uint256(exceedsQuote));
70:                 }
71:             }
72: 
73:             emit Rebalanced(
74:                 pairId,
75:                 relocationOccurred,
76:                 pairStatus.sqrtAssetStatus.tickLower,
77:                 pairStatus.sqrtAssetStatus.tickUpper,
78:                 deltaPositionBase,
79:                 deltaPositionQuote
80:             );
81:         }
82: 
83:         if (relocationOccurred) {
84:             globalData.rebalanceFeeGrowthCache[PairLib.getRebalanceCacheId(
85:                 pairId, pairStatus.sqrtAssetStatus.numRebalance
86:             )] = DataType.RebalanceFeeGrowthCache(
87:                 pairStatus.sqrtAssetStatus.rebalanceInterestGrowthQuote,
88:                 pairStatus.sqrtAssetStatus.rebalanceInterestGrowthBase
89:             );
90: 
91:             Perp.finalizeReallocation(pairStatus.sqrtAssetStatus);
92:         }
93:     }

```


*GitHub* : [27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L27-L93)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

22:     function supply(GlobalDataLibrary.GlobalData storage globalData, uint256 _pairId, uint256 _amount, bool _isStable)
23:         external
24:         returns (uint256 mintAmount)
25:     {
26:         // Checks pair exists
27:         globalData.validate(_pairId);
28:         // Checks amount is not 0
29:         if (_amount <= 0) {
30:             revert IPredyPool.InvalidAmount();
31:         }
32:         // Updates interest rate related to the pair
33:         ApplyInterestLib.applyInterestForToken(globalData.pairs, _pairId);
34: 
35:         DataType.PairStatus storage pair = globalData.pairs[_pairId];
36: 
37:         if (_isStable) {
38:             mintAmount = receiveTokenAndMintBond(pair.quotePool, _amount);
39:         } else {
40:             mintAmount = receiveTokenAndMintBond(pair.basePool, _amount);
41:         }
42: 
43:         emit TokenSupplied(msg.sender, pair.id, _isStable, _amount);
44:     }

57:     function withdraw(GlobalDataLibrary.GlobalData storage globalData, uint256 _pairId, uint256 _amount, bool _isStable)
58:         external
59:         returns (uint256 finalburntAmount, uint256 finalWithdrawalAmount)
60:     {
61:         // Checks pair exists
62:         globalData.validate(_pairId);
63:         // Checks amount is not 0
64:         require(_amount > 0, "AZ");
65:         // Updates interest rate related to the pair
66:         ApplyInterestLib.applyInterestForToken(globalData.pairs, _pairId);
67: 
68:         DataType.PairStatus storage pair = globalData.pairs[_pairId];
69: 
70:         if (_isStable) {
71:             (finalburntAmount, finalWithdrawalAmount) = burnBondAndTransferToken(pair.quotePool, _amount);
72:         } else {
73:             (finalburntAmount, finalWithdrawalAmount) = burnBondAndTransferToken(pair.basePool, _amount);
74:         }
75: 
76:         emit TokenWithdrawn(msg.sender, pair.id, _isStable, finalWithdrawalAmount);
77:     }

```


*GitHub* : [22](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L22-L44), [57](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L57-L77)

```solidity
📁 File: src/libraries/logic/TradeLogic.sol

29:     function trade(
30:         GlobalDataLibrary.GlobalData storage globalData,
31:         IPredyPool.TradeParams memory tradeParams,
32:         bytes memory settlementData
33:     ) external returns (IPredyPool.TradeResult memory tradeResult) {
34:         DataType.PairStatus storage pairStatus = globalData.pairs[tradeParams.pairId];
35: 
36:         // update interest growth
37:         ApplyInterestLib.applyInterestForToken(globalData.pairs, tradeParams.pairId);
38: 
39:         // update rebalance interest growth
40:         Perp.updateRebalanceInterestGrowth(pairStatus, pairStatus.sqrtAssetStatus);
41: 
42:         tradeResult = Trade.trade(globalData, tradeParams, settlementData);
43: 
44:         globalData.vaults[tradeParams.vaultId].margin +=
45:             tradeResult.fee + tradeResult.payoff.perpPayoff + tradeResult.payoff.sqrtPayoff;
46: 
47:         (tradeResult.minMargin,,, tradeResult.sqrtTwap) = PositionCalculator.calculateMinMargin(
48:             pairStatus, globalData.vaults[tradeParams.vaultId], DataType.FeeAmount(0, 0)
49:         );
50: 
51:         // The caller deposits or withdraws margin from the callback that is called below.
52:         callTradeAfterCallback(globalData, tradeParams, tradeResult);
53: 
54:         // check vault safety
55:         tradeResult.minMargin =
56:             PositionCalculator.checkSafe(pairStatus, globalData.vaults[tradeParams.vaultId], DataType.FeeAmount(0, 0));
57: 
58:         emit PositionUpdated(
59:             tradeParams.vaultId,
60:             tradeParams.pairId,
61:             tradeParams.tradeAmount,
62:             tradeParams.tradeAmountSqrt,
63:             tradeResult.payoff,
64:             tradeResult.fee
65:         );
66:     }

```


*GitHub* : [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/TradeLogic.sol#L29-L66)

```solidity
📁 File: src/markets/gamma/GammaTradeMarketLib.sol

59:     function validateHedgeCondition(GammaTradeMarketLib.UserPosition memory userPosition, uint256 sqrtIndexPrice)
60:         external
61:         view
62:         returns (bool, uint256 slippageTolerance, GammaTradeMarketLib.CallbackType)
63:     {
64:         if (
65:             userPosition.hedgeInterval > 0
66:                 && userPosition.lastHedgedTime + userPosition.hedgeInterval <= block.timestamp
67:         ) {
68:             return (
69:                 true,
70:                 calculateSlippageTolerance(
71:                     userPosition.lastHedgedTime + userPosition.hedgeInterval,
72:                     block.timestamp,
73:                     userPosition.auctionParams
74:                     ),
75:                 GammaTradeMarketLib.CallbackType.HEDGE_BY_TIME
76:             );
77:         }
78: 
79:         // if sqrtPriceTrigger is 0, it means that the user doesn't want to use this feature
80:         if (userPosition.sqrtPriceTrigger == 0) {
81:             return (false, 0, GammaTradeMarketLib.CallbackType.NONE);
82:         }
83: 
84:         uint256 upperThreshold = userPosition.lastHedgedSqrtPrice * userPosition.sqrtPriceTrigger / Bps.ONE;
85:         uint256 lowerThreshold = userPosition.lastHedgedSqrtPrice * Bps.ONE / userPosition.sqrtPriceTrigger;
86: 
87:         if (lowerThreshold >= sqrtIndexPrice) {
88:             return (
89:                 true,
90:                 calculateSlippageToleranceByPrice(sqrtIndexPrice, lowerThreshold, userPosition.auctionParams),
91:                 GammaTradeMarketLib.CallbackType.HEDGE_BY_PRICE
92:             );
93:         }
94: 
95:         if (upperThreshold <= sqrtIndexPrice) {
96:             return (
97:                 true,
98:                 calculateSlippageToleranceByPrice(upperThreshold, sqrtIndexPrice, userPosition.auctionParams),
99:                 GammaTradeMarketLib.CallbackType.HEDGE_BY_PRICE
100:             );
101:         }
102: 
103:         return (false, 0, GammaTradeMarketLib.CallbackType.NONE);
104:     }

106:     function validateCloseCondition(UserPosition memory userPosition, uint256 sqrtIndexPrice)
107:         external
108:         view
109:         returns (bool, uint256 slippageTolerance, CallbackType)
110:     {
111:         if (userPosition.expiration <= block.timestamp) {
112:             return (
113:                 true,
114:                 calculateSlippageTolerance(userPosition.expiration, block.timestamp, userPosition.auctionParams),
115:                 CallbackType.CLOSE_BY_TIME
116:             );
117:         }
118: 
119:         uint256 upperThreshold = userPosition.upperLimit;
120:         uint256 lowerThreshold = userPosition.lowerLimit;
121: 
122:         if (lowerThreshold > 0 && lowerThreshold >= sqrtIndexPrice) {
123:             return (
124:                 true,
125:                 calculateSlippageToleranceByPrice(sqrtIndexPrice, lowerThreshold, userPosition.auctionParams),
126:                 CallbackType.CLOSE_BY_PRICE
127:             );
128:         }
129: 
130:         if (upperThreshold > 0 && upperThreshold <= sqrtIndexPrice) {
131:             return (
132:                 true,
133:                 calculateSlippageToleranceByPrice(upperThreshold, sqrtIndexPrice, userPosition.auctionParams),
134:                 CallbackType.CLOSE_BY_PRICE
135:             );
136:         }
137: 
138:         return (false, 0, CallbackType.NONE);
139:     }

189:     function saveUserPosition(GammaTradeMarketLib.UserPosition storage userPosition, GammaModifyInfo memory modifyInfo)
190:         external
191:         returns (bool)
192:     {
193:         if (!modifyInfo.isEnabled) {
194:             return false;
195:         }
196: 
197:         if (0 < modifyInfo.hedgeInterval && 10 minutes > modifyInfo.hedgeInterval) {
198:             revert TooShortHedgeInterval();
199:         }
200: 
201:         require(modifyInfo.maxSlippageTolerance >= modifyInfo.minSlippageTolerance);
202:         require(modifyInfo.maxSlippageTolerance <= 2 * Bps.ONE);
203:         require(-1e6 < modifyInfo.maximaDeviation && modifyInfo.maximaDeviation < 1e6);
204: 
205:         // auto close condition
206:         userPosition.expiration = modifyInfo.expiration;
207:         userPosition.lowerLimit = modifyInfo.lowerLimit;
208:         userPosition.upperLimit = modifyInfo.upperLimit;
209: 
210:         // auto hedge condition
211:         userPosition.maximaDeviation = modifyInfo.maximaDeviation;
212:         userPosition.hedgeInterval = modifyInfo.hedgeInterval;
213:         userPosition.sqrtPriceTrigger = modifyInfo.sqrtPriceTrigger;
214:         userPosition.auctionParams.minSlippageTolerance = modifyInfo.minSlippageTolerance;
215:         userPosition.auctionParams.maxSlippageTolerance = modifyInfo.maxSlippageTolerance;
216:         userPosition.auctionParams.auctionPeriod = modifyInfo.auctionPeriod;
217:         userPosition.auctionParams.auctionRange = modifyInfo.auctionRange;
218: 
219:         return true;
220:     }

```


*GitHub* : [59](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketLib.sol#L59-L104), [106](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketLib.sol#L106-L139), [189](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketLib.sol#L189-L220)

### [L-16]<a name="l-16"></a> Loss of precision on division(Not captured by 4nalyzer)

Solidity doesn't support fractions, so divisions by large numbers could result in the quotient being zero. To avoid this, it's recommended to require a minimum numerator amount to ensure that it is always greater than the denominator.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

233:         return (netValue / leverage).toInt256() - _calculatePositionValue(vault, sqrtPrice);

```


*GitHub* : [233](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L233-L233)

### [L-17]<a name="l-17"></a> Mapping arrays can grow in size without a way to shrink them

It's a good practice to maintain control over the size of array mappings in Solidity, especially if they are dynamically updated. If a contract includes a mechanism to push items into an array, it should ideally also provide a mechanism to remove items. This is because Solidity arrays don't automatically shrink when items are deleted - their length needs to be manually adjusted.

Ignoring this can lead to bloated and inefficient contracts. For instance, iterating over a large array can cause your contract to hit the block gas limit. Additionally, if entries are only marked for deletion but never actually removed, you may end up dealing with stale or irrelevant data, which can cause logical errors.

Therefore, implementing a method to 'pop' items from mapping arrays helps manage contract's state, improve efficiency and prevent potential issues related to gas limits or stale data. Always ensure to handle potential underflow conditions when popping elements from the mapping array.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

50:     mapping(address owner => uint256[]) internal positionIDs;

```


*GitHub* : [50](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L50-L50)

### [L-18]<a name="l-18"></a> Missing zero address check in constructor

Constructors often take address parameters to initialize important components of a contract, such as owner or linked contracts. However, without a checking, there's a risk that an address parameter could be mistakenly set to the zero address `(0x0)`. This could be due to an error or oversight during contract deployment. A zero address in a crucial role can cause serious issues, as it cannot perform actions like a normal address, and any funds sent to it will be irretrievable. It's therefore crucial to include a zero address check in constructors to prevent such potential problems. If a zero address is detected, the constructor should revert the transaction.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: src/PriceFeed.sol

// @audit missing checks for -->  pyth
14:     constructor(address pyth) {

// @audit missing checks for -->  quotePrice, pyth
37:     constructor(address quotePrice, address pyth, bytes32 priceId, uint256 decimalsDiff) {

```


*GitHub* : [14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L14-L14), [37](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L37-L37)

```solidity
📁 File: src/base/BaseHookCallback.sol

// @audit missing checks for -->  predyPool
12:     constructor(IPredyPool predyPool) {

```


*GitHub* : [12](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseHookCallback.sol#L12-L12)

```solidity
📁 File: src/base/BaseMarket.sol

// @audit missing checks for -->  predyPool, _whitelistFiller, quoterAddress
19:     constructor(IPredyPool predyPool, address _whitelistFiller, address quoterAddress)
20:         BaseHookCallback(predyPool)
21:         Owned(msg.sender)
22:     {

```


*GitHub* : [19](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L19-L22)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

// @audit missing checks for -->  swapRouterAddress, quoterAddress
16:     constructor(address swapRouterAddress, address quoterAddress) {

```


*GitHub* : [16](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L16-L16)

```solidity
📁 File: src/tokenization/SupplyToken.sol

// @audit missing checks for -->  controller
15:     constructor(address controller, string memory _name, string memory _symbol, uint8 __decimals)
16:         ERC20(_name, _symbol, __decimals)
17:     {

```


*GitHub* : [15](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/tokenization/SupplyToken.sol#L15-L17)

### [L-19]<a name="l-19"></a> Missing checks for `address(0x0)` when updating `address` state variables

Explore the imperative need for meticulous checks in smart contract development, specifically addressing the absence of validations for address(0x0) during state variable updates. This concise overview sheds light on the potential risks associated with this omission and offers practical insights into rectifying the vulnerability. Stay vigilant, stay secure.

*There are 8 instance(s) of this issue:*

```solidity
📁 File: src/PriceFeed.sol

15:         _pyth = pyth;

38:         _quotePriceFeed = quotePrice;

39:         _pyth = pyth;

```


*GitHub* : [15](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L15-L15), [38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L38-L38), [39](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L39-L39)

```solidity
📁 File: src/base/BaseMarket.sol

23:         whitelistFiller = _whitelistFiller;

85:         whitelistFiller = newWhitelistFiller;

```


*GitHub* : [23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L23-L23), [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L85-L85)

```solidity
📁 File: src/base/BaseMarketUpgradable.sol

44:         whitelistFiller = _whitelistFiller;

129:         whitelistFiller = newWhitelistFiller;

```


*GitHub* : [44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L44-L44), [129](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L129-L129)

```solidity
📁 File: src/tokenization/SupplyToken.sol

18:         _controller = controller;

```


*GitHub* : [18](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/tokenization/SupplyToken.sol#L18-L18)

### [L-20]<a name="l-20"></a> Named return variable used before assignment

As no value is written to the variable, the default value is always read. This is usually due to a bug in the code logic that causes an invalid value to be used.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

// @audit result
380:             return result;

```


*GitHub* : [380](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L380-L380)

### [L-21]<a name="l-21"></a> Variables shadowing other definitions

A variable declaration shadowing any other existing definition is error-prone. It can cause confusion for developers, potentially introduce bugs, and reduce the readability and maintainability.

*There are 23 instance(s) of this issue:*

```solidity
📁 File: src/base/SettlementCallbackLib.sol

// @audit Shadows state variable  _whiteListedSettlements
29:     function validate(
30:         mapping(address settlementContractAddress => bool) storage _whiteListedSettlements,
31:         SettlementParams memory settlementParams
32:     ) internal view {

```


*GitHub* : [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L29-L32)

```solidity
📁 File: src/libraries/Trade.sol

// @audit Shadows state variable  globalData
32:     function trade(
33:         GlobalDataLibrary.GlobalData storage globalData,
34:         IPredyPool.TradeParams memory tradeParams,
35:         bytes memory settlementData
36:     ) external returns (IPredyPool.TradeResult memory tradeResult) {

// @audit Shadows state variable  globalData
76:     function swap(
77:         GlobalDataLibrary.GlobalData storage globalData,
78:         uint256 pairId,
79:         SwapStableResult memory swapParams,
80:         bytes memory settlementData,
81:         uint256 sqrtPrice,
82:         uint256 vaultId
83:     ) internal returns (SwapStableResult memory) {

```


*GitHub* : [32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L32-L36), [76](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L76-L83)

```solidity
📁 File: src/libraries/VaultLib.sol

// @audit Shadows state variable  globalData
11:     function getVault(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId)
12:         internal
13:         view
14:         returns (DataType.Vault storage vault)
15:     {

// @audit Shadows state variable  globalData
24:     function createOrGetVault(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId, uint256 pairId)
25:         internal
26:         returns (uint256)
27:     {

```


*GitHub* : [11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L11-L15), [24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L24-L27)

```solidity
📁 File: src/libraries/logic/AddPairLogic.sol

// @audit Shadows state variable  allowedUniswapPools
53:     function addPair(
54:         GlobalDataLibrary.GlobalData storage _global,
55:         mapping(address => bool) storage allowedUniswapPools,
56:         AddPairParams memory _addPairParam
57:     ) external returns (uint256 pairId) {

```


*GitHub* : [53](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L53-L57)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

// @audit Shadows state variable  globalData
39:     function liquidate(
40:         uint256 vaultId,
41:         uint256 closeRatio,
42:         GlobalDataLibrary.GlobalData storage globalData,
43:         bytes memory settlementData
44:     ) external returns (IPredyPool.TradeResult memory tradeResult) {

```


*GitHub* : [39](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39-L44)

```solidity
📁 File: src/libraries/logic/ReaderLogic.sol

// @audit Shadows state variable  globalData
16:     function getPairStatus(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) external {

// @audit Shadows state variable  globalData
24:     function getVaultStatus(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId) external {

```


*GitHub* : [16](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReaderLogic.sol#L16-L16), [24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReaderLogic.sol#L24-L24)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

// @audit Shadows state variable  globalData
27:     function reallocate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId, bytes memory settlementData)
28:         external
29:         returns (bool isRangeChanged)
30:     {

```


*GitHub* : [27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L27-L30)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

// @audit Shadows state variable  globalData
22:     function supply(GlobalDataLibrary.GlobalData storage globalData, uint256 _pairId, uint256 _amount, bool _isStable)
23:         external
24:         returns (uint256 mintAmount)
25:     {

// @audit Shadows state variable  globalData
57:     function withdraw(GlobalDataLibrary.GlobalData storage globalData, uint256 _pairId, uint256 _amount, bool _isStable)
58:         external
59:         returns (uint256 finalburntAmount, uint256 finalWithdrawalAmount)
60:     {

```


*GitHub* : [22](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L22-L25), [57](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L57-L60)

```solidity
📁 File: src/libraries/logic/TradeLogic.sol

// @audit Shadows state variable  globalData
29:     function trade(
30:         GlobalDataLibrary.GlobalData storage globalData,
31:         IPredyPool.TradeParams memory tradeParams,
32:         bytes memory settlementData
33:     ) external returns (IPredyPool.TradeResult memory tradeResult) {

// @audit Shadows state variable  globalData
68:     function callTradeAfterCallback(
69:         GlobalDataLibrary.GlobalData storage globalData,
70:         IPredyPool.TradeParams memory tradeParams,
71:         IPredyPool.TradeResult memory tradeResult
72:     ) internal {

```


*GitHub* : [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/TradeLogic.sol#L29-L33), [68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/TradeLogic.sol#L68-L72)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

// @audit Shadows state variable  whitelistFiller
69:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)
70:         public
71:         initializer
72:     {

```


*GitHub* : [69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L69-L72)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

// @audit Shadows state variable  whitelistFiller
92:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)
93:         public
94:         initializer
95:     {

```


*GitHub* : [92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L92-L95)

```solidity
📁 File: src/types/GlobalData.sol

// @audit Shadows state variable  globalData
26:     function validateVaultId(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId) internal view {

// @audit Shadows state variable  globalData
30:     function validate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal view {

// @audit Shadows state variable  globalData
35:     function initializeLock(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal {

// @audit Shadows state variable  globalData
46:     function callSettlementCallback(
47:         GlobalDataLibrary.GlobalData storage globalData,
48:         bytes memory settlementData,
49:         int256 deltaBaseAmount
50:     ) internal {

// @audit Shadows state variable  globalData
62:     function finalizeLock(GlobalDataLibrary.GlobalData storage globalData)
63:         internal
64:         returns (int256 paidQuote, int256 paidBase)
65:     {

// @audit Shadows state variable  globalData
72:     function take(GlobalDataLibrary.GlobalData storage globalData, bool isQuoteAsset, address to, uint256 amount)
73:         internal
74:     {

// @audit Shadows state variable  globalData
88:     function settle(GlobalDataLibrary.GlobalData storage globalData, bool isQuoteAsset)
89:         internal
90:         returns (int256 paid)
91:     {

```


*GitHub* : [26](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L26-L26), [30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L30-L30), [35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L35-L35), [46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L46-L50), [62](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L62-L65), [72](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L72-L74), [88](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L88-L91)

### [L-22]<a name="l-22"></a> File allows a version of solidity that is susceptible to `.selector` related optimizer bug

In solidity versions prior to `0.8.21`, there is a legacy code generation [bug](https://soliditylang.org/blog/2023/07/19/missing-side-effects-on-selector-access-bug/) where if `foo().selector` is called, `foo()` doesn't actually get evaluated. It is listed as low-severity, because projects usually use the contract name rather than a function call to look up the selector.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/libraries/UniHelper.sol

42:             address(uniswapPool).staticcall(abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos));

61:                 abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos)

```


*GitHub* : [42](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L42-L42), [61](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L61-L61)

### [L-23]<a name="l-23"></a> File allows a version of solidity that is susceptible to an assembly optimizer bug

In solidity versions `0.8.13` and `0.8.14`, there is an [optimizer bug](https://github.com/ethereum/solidity-blog/blob/499ab8abc19391be7b7b34f88953a067029a5b45/_posts/2022-06-15-inline-assembly-memory-side-effects-bug.md) where, if the use of a variable is in a separate `assembly` block from the block in which it was stored, the `mstore` operation is optimized out, leading to uninitialized memory. The code currently does not have such a pattern of execution, but it does use `mstore`s in `assembly` blocks, so it is a risk for future changes. The affected solidity versions should be avoided if at all possible.

*There are 55 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L2-L2)

```solidity
📁 File: src/PriceFeed.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L2-L2)

```solidity
📁 File: src/base/BaseHookCallback.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseHookCallback.sol#L2-L2)

```solidity
📁 File: src/base/BaseHookCallbackUpgradable.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseHookCallbackUpgradable.sol#L2-L2)

```solidity
📁 File: src/base/BaseMarket.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L2-L2)

```solidity
📁 File: src/base/BaseMarketUpgradable.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L2-L2)

```solidity
📁 File: src/base/SettlementCallbackLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L2-L2)

```solidity
📁 File: src/libraries/ApplyInterestLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ApplyInterestLib.sol#L2-L2)

```solidity
📁 File: src/libraries/Constants.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Constants.sol#L2-L2)

```solidity
📁 File: src/libraries/DataType.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/DataType.sol#L2-L2)

```solidity
📁 File: src/libraries/InterestRateModel.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/InterestRateModel.sol#L2-L2)

```solidity
📁 File: src/libraries/PairLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PairLib.sol#L2-L2)

```solidity
📁 File: src/libraries/Perp.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Perp.sol#L2-L2)

```solidity
📁 File: src/libraries/PerpFee.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PerpFee.sol#L2-L2)

```solidity
📁 File: src/libraries/PositionCalculator.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PositionCalculator.sol#L2-L2)

```solidity
📁 File: src/libraries/PremiumCurveModel.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PremiumCurveModel.sol#L2-L2)

```solidity
📁 File: src/libraries/Reallocation.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Reallocation.sol#L2-L2)

```solidity
📁 File: src/libraries/ScaledAsset.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ScaledAsset.sol#L2-L2)

```solidity
📁 File: src/libraries/SlippageLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/SlippageLib.sol#L2-L2)

```solidity
📁 File: src/libraries/Trade.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L2-L2)

```solidity
📁 File: src/libraries/UniHelper.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L2-L2)

```solidity
📁 File: src/libraries/VaultLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/AddPairLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/ReaderLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReaderLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/TradeLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/TradeLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/math/Bps.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/Bps.sol#L2-L2)

```solidity
📁 File: src/libraries/math/LPMath.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/LPMath.sol#L2-L2)

```solidity
📁 File: src/libraries/math/Math.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/Math.sol#L2-L2)

```solidity
📁 File: src/libraries/orders/DecayLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/DecayLib.sol#L2-L2)

```solidity
📁 File: src/libraries/orders/OrderInfoLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/OrderInfoLib.sol#L2-L2)

```solidity
📁 File: src/libraries/orders/Permit2Lib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/Permit2Lib.sol#L2-L2)

```solidity
📁 File: src/libraries/orders/ResolvedOrder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/ResolvedOrder.sol#L2-L2)

```solidity
📁 File: src/markets/L2Decoder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/L2Decoder.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/ArrayLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/ArrayLib.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaOrder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaOrder.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaTradeMarketL2.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketL2.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaTradeMarketLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketLib.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaTradeMarketWrapper.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketWrapper.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/L2GammaDecoder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/L2GammaDecoder.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpMarket.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarket.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpMarketLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketLib.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpOrder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpOrder.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpOrderV3.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpOrderV3.sol#L2-L2)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L2-L2)

```solidity
📁 File: src/tokenization/SupplyToken.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/tokenization/SupplyToken.sol#L2-L2)

```solidity
📁 File: src/types/GlobalData.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L2-L2)

```solidity
📁 File: src/types/LockData.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/LockData.sol#L2-L2)

```solidity
📁 File: src/vendors/AggregatorV3Interface.sol

2: pragma solidity ^0.8.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/vendors/AggregatorV3Interface.sol#L2-L2)

```solidity
📁 File: src/vendors/IPyth.sol

2: pragma solidity ^0.8.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/vendors/IPyth.sol#L2-L2)

```solidity
📁 File: src/vendors/IUniswapV3PoolOracle.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/vendors/IUniswapV3PoolOracle.sol#L2-L2)

### [L-24]<a name="l-24"></a> Solidity version `0.8.20` may not work on other chains due to `PUSH0`

In Solidity `0.8.20`'s compiler, the default target EVM version has been changed to Shanghai. This version introducesa new opcode called `PUSH0`. However, not all Layer 2 solutions have implemented this opcode yet, leading to deployment failures on thesechains. To overcome this problem, it is recommended to utilize an earlier EVM version.

*There are 55 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L2-L2)

```solidity
📁 File: src/PriceFeed.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L2-L2)

```solidity
📁 File: src/base/BaseHookCallback.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseHookCallback.sol#L2-L2)

```solidity
📁 File: src/base/BaseHookCallbackUpgradable.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseHookCallbackUpgradable.sol#L2-L2)

```solidity
📁 File: src/base/BaseMarket.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L2-L2)

```solidity
📁 File: src/base/BaseMarketUpgradable.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L2-L2)

```solidity
📁 File: src/base/SettlementCallbackLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L2-L2)

```solidity
📁 File: src/libraries/ApplyInterestLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ApplyInterestLib.sol#L2-L2)

```solidity
📁 File: src/libraries/Constants.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Constants.sol#L2-L2)

```solidity
📁 File: src/libraries/DataType.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/DataType.sol#L2-L2)

```solidity
📁 File: src/libraries/InterestRateModel.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/InterestRateModel.sol#L2-L2)

```solidity
📁 File: src/libraries/PairLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PairLib.sol#L2-L2)

```solidity
📁 File: src/libraries/Perp.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Perp.sol#L2-L2)

```solidity
📁 File: src/libraries/PerpFee.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PerpFee.sol#L2-L2)

```solidity
📁 File: src/libraries/PositionCalculator.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PositionCalculator.sol#L2-L2)

```solidity
📁 File: src/libraries/PremiumCurveModel.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PremiumCurveModel.sol#L2-L2)

```solidity
📁 File: src/libraries/Reallocation.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Reallocation.sol#L2-L2)

```solidity
📁 File: src/libraries/ScaledAsset.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ScaledAsset.sol#L2-L2)

```solidity
📁 File: src/libraries/SlippageLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/SlippageLib.sol#L2-L2)

```solidity
📁 File: src/libraries/Trade.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L2-L2)

```solidity
📁 File: src/libraries/UniHelper.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L2-L2)

```solidity
📁 File: src/libraries/VaultLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/AddPairLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/ReaderLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReaderLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/logic/TradeLogic.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/TradeLogic.sol#L2-L2)

```solidity
📁 File: src/libraries/math/Bps.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/Bps.sol#L2-L2)

```solidity
📁 File: src/libraries/math/LPMath.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/LPMath.sol#L2-L2)

```solidity
📁 File: src/libraries/math/Math.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/Math.sol#L2-L2)

```solidity
📁 File: src/libraries/orders/DecayLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/DecayLib.sol#L2-L2)

```solidity
📁 File: src/libraries/orders/OrderInfoLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/OrderInfoLib.sol#L2-L2)

```solidity
📁 File: src/libraries/orders/Permit2Lib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/Permit2Lib.sol#L2-L2)

```solidity
📁 File: src/libraries/orders/ResolvedOrder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/ResolvedOrder.sol#L2-L2)

```solidity
📁 File: src/markets/L2Decoder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/L2Decoder.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/ArrayLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/ArrayLib.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaOrder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaOrder.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaTradeMarketL2.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketL2.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaTradeMarketLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketLib.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/GammaTradeMarketWrapper.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarketWrapper.sol#L2-L2)

```solidity
📁 File: src/markets/gamma/L2GammaDecoder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/L2GammaDecoder.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpMarket.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarket.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpMarketLib.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketLib.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpOrder.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpOrder.sol#L2-L2)

```solidity
📁 File: src/markets/perp/PerpOrderV3.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpOrderV3.sol#L2-L2)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L2-L2)

```solidity
📁 File: src/tokenization/SupplyToken.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/tokenization/SupplyToken.sol#L2-L2)

```solidity
📁 File: src/types/GlobalData.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L2-L2)

```solidity
📁 File: src/types/LockData.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/LockData.sol#L2-L2)

```solidity
📁 File: src/vendors/AggregatorV3Interface.sol

2: pragma solidity ^0.8.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/vendors/AggregatorV3Interface.sol#L2-L2)

```solidity
📁 File: src/vendors/IPyth.sol

2: pragma solidity ^0.8.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/vendors/IPyth.sol#L2-L2)

```solidity
📁 File: src/vendors/IUniswapV3PoolOracle.sol

2: pragma solidity ^0.8.17;

```


*GitHub* : [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/vendors/IUniswapV3PoolOracle.sol#L2-L2)

### [L-25]<a name="l-25"></a> State variables not capped at reasonable values

Consider adding minimum/maximum value checks to ensure that the state variables below can never be used to excessively harm users, including via griefing

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/PriceFeed.sol

// @audit decimalsDiff
41:         _decimalsDiff = decimalsDiff;

```


*GitHub* : [41](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L41-L41)

### [L-26]<a name="l-26"></a> Consider implementing two-step procedure for updating protocol addresses

A copy-paste error or a typo may end up bricking protocol functionality, or sending tokens to an address with no known private key. Consider implementing a two-step procedure for updating protocol addresses, where the recipient is set as pending, and must 'accept' the assignment by making an affirmative call. A straight forward way of doing this would be to have the target contracts implement [EIP-165](https://eips.ethereum.org/EIPS/eip-165), and to have the 'set' functions ensure that the recipient is of the right interface type.

*There are 7 instance(s) of this issue:*

```solidity
📁 File: src/PredyPool.sol

97:     function setOperator(address newOperator) external onlyOperator {

286:     function updateRecepient(uint256 vaultId, address recipient) external onlyVaultOwner(vaultId) {

```


*GitHub* : [97](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L97-L97), [286](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L286-L286)

```solidity
📁 File: src/base/BaseMarket.sol

84:     function updateWhitelistFiller(address newWhitelistFiller) external onlyOwner {

92:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyOwner {

```


*GitHub* : [84](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L84-L84), [92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarket.sol#L92-L92)

```solidity
📁 File: src/base/BaseMarketUpgradable.sol

38:     function __BaseMarket_init(IPredyPool predyPool, address _whitelistFiller, address quoterAddress)
39:         internal
40:         onlyInitializing
41:     {

128:     function updateWhitelistFiller(address newWhitelistFiller) external onlyFiller {

140:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyFiller {

```


*GitHub* : [38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L38-L41), [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L128-L128), [140](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L140-L140)

### [L-27]<a name="l-27"></a> Consider using OpenZeppelin's SafeCast library to prevent unexpected overflows when downcasting

Downcasting from `uint256`/`int256` in Solidity does not revert on overflow. This can result in undesired exploitation or bugs, since developers usually assume that overflows raise errors. [OpenZeppelin's SafeCast library](https://docs.openzeppelin.com/contracts/3.x/api/utils#SafeCast) restores this intuition by reverting the transaction when such an operation overflows. Using this library eliminates an entire class of bugs, so it's recommended to use it always. Some exceptions are acceptable like with the classic `uint256(uint160(address(variable)))`

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/libraries/UniHelper.sol

// @audit int56 -> int256
70:         int24 tick = int24((tickCumulatives[1] - tickCumulatives[0]) / int56(int256(ago)));

```


*GitHub* : [70](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L70-L70)

### [L-28]<a name="l-28"></a> Using zero as a parameter

Passing `0` or `0x0` as a function argument can sometimes result in a security issue(e.g. passing zero as the slippage parameter). A historical example is the infamous 0x0 address bug where numerous tokens were lost. This happens because `0` can be interpreted as an uninitialized address, leading to transfers to the `0x0` address, effectively burning tokens. Moreover, `0` as a denominator in division operations would cause a runtime exception. It's also often indicative of a logical error in the caller's code.

Consider using a constant variable with a descriptive name, so it's clear that the argument is intentionally being used, and for the right reasons.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/libraries/Trade.sol

53:         SwapStableResult memory swapResult = swap(
54:             globalData,
55:             tradeParams.pairId,
56:             SwapStableResult(-tradeParams.tradeAmount, underlyingAmountForSqrt, realizedFee.feeAmountBase, 0),
57:             settlementData,
58:             tradeResult.sqrtPrice,
59:             tradeParams.vaultId
60:         );

89:             return divToStable(swapParams, int256(1e18), amountQuote, 0);

```


*GitHub* : [53](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L53-L60), [89](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L89-L89)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

156:         return _executeOrderV3(perpOrder, order.sig, settlementParams, 0);

```


*GitHub* : [156](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L156-L156)

### [L-29]<a name="l-29"></a> Some `ERC20` can revert on a zero value `transfer`

In spite of the fact that [EIP-20](https://github.com/ethereum/EIPs/blob/46b9b698815abbfa628cd1097311deee77dd45c5/EIPS/eip-20.md?plain=1#L116) states that zero-valued transfers must be accepted, some tokens, such as `LEND` will revert if this is attempted, which may cause transactions that involve other tokens (such as batch operations) to fully revert. Consider skipping the transfer if the amount is zero, which will also save gas.

*There are 22 instance(s) of this issue:*

```solidity
📁 File: src/base/SettlementCallbackLib.sol

48:             ERC20(quoteToken).safeTransferFrom(
49:                 settlementParams.sender, address(predyPool), uint256(-settlementParams.fee)
50:             );

105:             ERC20(quoteToken).safeTransferFrom(sender, address(predyPool), quoteAmount);

123:             ERC20(quoteToken).safeTransfer(address(predyPool), quoteAmountFromUni);

128:                 ERC20(quoteToken).safeTransferFrom(sender, address(this), quoteAmount - quoteAmountFromUni);

130:                 ERC20(quoteToken).safeTransfer(sender, quoteAmountFromUni - quoteAmount);

133:             ERC20(quoteToken).safeTransfer(address(predyPool), quoteAmount);

152:             ERC20(baseToken).safeTransferFrom(sender, address(predyPool), buyAmount);

170:             ERC20(quoteToken).safeTransfer(address(predyPool), settlementParams.maxQuoteAmount - quoteAmountToUni);

175:                 ERC20(quoteToken).safeTransfer(sender, quoteAmount - quoteAmountToUni);

177:                 ERC20(quoteToken).safeTransferFrom(sender, address(this), quoteAmountToUni - quoteAmount);

180:             ERC20(quoteToken).safeTransfer(address(predyPool), settlementParams.maxQuoteAmount - quoteAmount);

```


*GitHub* : [48](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L48-L50), [105](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L105-L105), [123](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L123-L123), [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L128-L128), [130](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L130-L130), [133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L133-L133), [152](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L152-L152), [170](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L170-L170), [175](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L175-L175), [177](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L177-L177), [180](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L180-L180)

```solidity
📁 File: src/libraries/logic/LiquidationLogic.sol

99:                     ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);

106:                 ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));

```


*GitHub* : [99](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L99-L99), [106](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L106-L106)

```solidity
📁 File: src/libraries/logic/ReallocationLogic.sol

69:                     ERC20(pairStatus.quotePool.token).safeTransfer(msg.sender, uint256(exceedsQuote));

```


*GitHub* : [69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/ReallocationLogic.sol#L69-L69)

```solidity
📁 File: src/libraries/logic/SupplyLogic.sol

52:         ERC20(_pool.token).safeTransferFrom(msg.sender, address(this), _amount);

90:         ERC20(_pool.token).safeTransfer(msg.sender, finalWithdrawalAmount);

```


*GitHub* : [52](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L52-L52), [90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L90-L90)

```solidity
📁 File: src/markets/gamma/GammaTradeMarket.sol

118:                     quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));

```


*GitHub* : [118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L118-L118)

```solidity
📁 File: src/markets/perp/PerpMarketV1.sol

126:                 quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));

```


*GitHub* : [126](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L126-L126)

```solidity
📁 File: src/settlements/UniswapSettlement.sol

30:         ERC20(baseToken).safeTransferFrom(msg.sender, address(this), amountIn);

46:         ERC20(quoteToken).safeTransferFrom(msg.sender, address(this), amountInMaximum);

54:             ERC20(quoteToken).safeTransfer(msg.sender, amountInMaximum - amountIn);

```


*GitHub* : [30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L30-L30), [46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L46-L46), [54](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L54-L54)

```solidity
📁 File: src/types/GlobalData.sol

85:         ERC20(currency).safeTransfer(to, amount);

```


*GitHub* : [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L85-L85)

