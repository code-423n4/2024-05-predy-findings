## 1. Protocol can be completely taken over by frontrunning initializer

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L70-L75

### Impact

The initialize function sets the protocol's controller operator as the caller of the function. The stakes here are higher as the operator has a lot of administrative functions in the protocol. Frontrunning the initializer can give the frontrunner such power. 

```solidity
    function initialize(address uniswapFactory) public initializer { 
        __ReentrancyGuard_init();
        AddPairLogic.initializeGlobalData(globalData, uniswapFactory);

        operator = msg.sender;
    }
```
### Recommended Mitigation Steps
Consider setting the operator to msg.sender in the constructor instead, and adding a check in `initialize` function that msg.sender is the operator.

***
 
## 2. Use of a single step operator change.

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L97-L102

### Impact
The existing `setOperator` function immediately changes to the new address. This can lead to operatorship being irrecoverably lost if a wrong address is entered.


```solidity
    function setOperator(address newOperator) external onlyOperator {
        require(newOperator != address(0));
        operator = newOperator;

        emit OperatorUpdated(newOperator);
    }
```
### Recommended Mitigation Steps
Consider implementing a two-step variant, where the 'newOperator' must call a separate function to accept the transfer.

***
 
## 3. Redundant check for zero amount when withdrawing protocol and creator revenue

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L182-L188

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L204-L210

### Impact

The `withdrawProtocolRevenue` function first requires that the accumlated protocol revenue is greater than 0. If it's not the function reverts. Before transferring the amount however, a check for amount > 0 is performed again which is now no longer needed.
```solidity
        require(amount > 0, "AZ"); 

        pool.accumulatedProtocolRevenue = 0; 

        if (amount > 0) {
            ERC20(pool.token).safeTransfer(msg.sender, amount);
        }
```

The same can be observed in the `withdrawCreatorRevenue` function.

```solidity
        require(amount > 0, "AZ");

        pool.accumulatedCreatorRevenue = 0; 

        if (amount > 0) {
            ERC20(pool.token).safeTransfer(msg.sender, amount); 
        }
```

### Recommended Mitigation Steps

Consider removing the `if (amount > 0)` checks as they're not needed.

***
 
## 4. Consider allowing `withdrawProtocolRevenue` and `withdrawCreatorRevenue` to specify recipeints

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L177

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L199

### Impact

`withdrawProtocolRevenue` and `withdrawCreatorRevenue` functions allow the protocol operator and creator to withdraw accumulated revenue, which is sent to the callers (i.e msg.sender). A nice to have feature is to allow the callers to be able to specify a recipient to which the funds can be sent to. This can help incase of unforseen circumstances including address blocklists. Consider introducing this feature.
 
***
 
## 5. Consider using safer CREATE methods to create new pricefeed contracts to protect from blockreorgs.

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L18-L24

### Impact

The use of vanilla CREATE1 can lead to the the price feed contract being deployed to a different address in case of a block reorg upon deployment. Since the protocol aims to deploy to L2s including optimistic and base which are known for having reorgs, the chances of this happening is not very low. Any dependence on prior precomputation of the address upon deployment will lead to the wrong address being used after the reorg.

```solidity
    function createPriceFeed(address quotePrice, bytes32 priceId, uint256 decimalsDiff) external returns (address) {
        PriceFeed priceFeed = new PriceFeed(quotePrice, _pyth, priceId, decimalsDiff);

        emit PriceFeedCreated(quotePrice, priceId, decimalsDiff, address(priceFeed));

        return address(priceFeed);
    }
```

### Recommended Mitigation Steps
Consider using create2 with salt and `msg.sender to deploy instead.
 
***
 
## 6. No check for stale prices upon querying chainlink tokens

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L46


### Impact

The `getSqrtPrice` function queries chainlink's `latestRoundData` but doesn't check if the price returned is stale. Using a stale price can cause the calculations depending on the `getSqrtPrice` function to be inaccurate, which, for example, can mistakenly consider a user to be ripe for liquidation when in reality they're not and unexpectedly allow the user to be liquidated.

```solidity
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
```

### Recommended Mitigation Steps

Consider checking for stale prices.

```solidity
(uint80 roundID, int256 feedPrice, , uint256 timestamp, uint80 answeredInRound) = feed.latestRoundData();
require(feedPrice > 0, "Chainlink price <= 0"); 
require(answeredInRound >= roundID, "Stale price");
require(timestamp != 0, "Round not complete");
require(timeStamp < block.timestamp - staleTime, "Stale price")
```
 
***
 
## 7. No check for sequencer uptime on L2s when querying chainlink prices

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L46

### Impact
Chainlink recommends that all Optimistic L2 oracles consult the Sequencer Uptime Feed to ensure that the sequencer is live before trusting the data returned by the oracle. This check is not implemented in PriceFeed.sol causing if the sequencer goes down that the oracle data will not be kept up to date, and thus could become stale. Using this stale data will cause incorrect pricing which will lead to a host of bad effects in functions depending on the `getSqrtPrice`function.

```solidity
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
```

### Recommended Mitigation Steps

Consider checking for the sequencer being down before getting prices.


***


## 8. Ineffective deadline check during interactions with uniswap router

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L34

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L50

### Impact

The `swapExactIn` and `swapExactOut` functions in UniswapSettlement.sol interact with uniswap's swap router to swap tokens. They both however use `block.timestamp` as the deadline parameter. The use of block.timestamp signifies to the miners that the transaction can be held in the mempool for a long time to be maliciously executed at a later point and can be used to steal otherwise positive slippage from the protocol swaps. Transactions that provide an insufficient amount of gas such that they are not mined within a reasonable amount of time, can be picked by malicious actors or MEV bots and executed later in detriment of the submitter.

```solidity
    function swapExactIn(
...
        amountOut = _swapRouter.exactInput(
            ISwapRouter.ExactInputParams(data, recipient, block.timestamp, amountIn, amountOutMinimum)
        );
    }
```
```solidity
    function swapExactOut(
...
        amountIn = _swapRouter.exactOutput(
            ISwapRouter.ExactOutputParams(data, recipient, block.timestamp, amountOut, amountInMaximum)
        );
...
    }
```

### Recommended Mitigation Steps

Consider using a more hardcoded reasonable value, or allowing users to pass the value in in the originating calls.
 
***

## 9. Consider also checking for min-max prices on chainlink pricefeed

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L46

### Impact
Chainlink aggregators have a built-in circuit breaker if the price of an asset goes outside of a predetermined price band.
The result is that if an asset experiences a huge drop in value (i.e. LUNA crash) the price of the oracle will continue to return the minPrice instead of the actual price of the asset.

***

 
## 10. Redundant check in `getAssetFee` and `getDebtFee`

Links to affected code *

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ScaledAsset.sol#L160

### Impact

The `getAssetFee` and `getDebtFee` are only used in the `computeUserFee` function which selects which of the functions to call based on a check for position amount.

```solidity
    function computeUserFee(ScaledAsset.AssetStatus memory _assetStatus, ScaledAsset.UserStatus memory _userStatus)
        internal
        pure
        returns (int256 interestFee)
    {
        if (_userStatus.positionAmount > 0) {
            interestFee = (getAssetFee(_assetStatus, _userStatus)).toInt256();
        } else {
            interestFee = -(getDebtFee(_assetStatus, _userStatus)).toInt256();
        }
    }
```
These checks are then repeated again in the functions, making them redundant.

```solidity
        require(accountState.positionAmount >= 0, "S1");
```
and get debt fee


```solidity
    require(accountState.positionAmount <= 0, "S1"); 

```

### Recommended Mitigation Steps
Considering that the functions are only used in the `computeUserFee` in the entire protocol, consider removing it as its just dead code.

***

