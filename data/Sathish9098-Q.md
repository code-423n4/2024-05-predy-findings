 ## QA Reports

##

## [L-1] Risk of Permanent Token Loss Due to Address Blocklisting in USDC, USDT 

In Predy, if tokens such as USDC or USDT are used as supply tokens, and a lender's address is added to a blocklist after they have supplied tokens to the pool, there is a risk that the lender could permanently lose access to their tokens. This is because certain tokens have a contract-level admin-controlled address blocklist, which prevents transfers to and from addresses on the blocklist. If the lender's address is blocklisted, it would be unable to withdraw or transfer their tokens from the pool, resulting in a potential loss of those assets.


```solidity
FILE: 2024-05-predy/src/libraries/logic
/SupplyLogic.sol

 ERC20(_pool.token).safeTransfer(msg.sender, finalWithdrawalAmount);

```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L90C8-L90C76

### Recommended Mitigation
- Create an admin-controlled override function that can be used to manually transfer tokens from a blocklisted address to a safe address. 

- Implement an emergency withdrawal function that allows users to withdraw their tokens to a different address if their original address gets blocklisted.


##

## [L-2] Usage of `slot0` is extremely easy to manipulate

### Impact
The function uses slot0 to obtain the current tick (tickCurrent). Since slot0 is easy to manipulate, attackers can influence the value of tickCurrent.

Manipulating tickCurrent can lead to incorrect values for feeGrowthBelow0X128, feeGrowthBelow1X128, feeGrowthAbove0X128, and feeGrowthAbove1X128. Consequently, feeGrowthInside0X128 and feeGrowthInside1X128 values will also be incorrect.

[slot0(https://docs.uniswap.org/contracts/v3/reference/core/interfaces/pool/IUniswapV3PoolState#slot0) is the most recent data point and is therefore extremely easy to manipulate.


```solidity
FILE:2024-05-predy/src/libraries/UniHelper.sol

104: (, int24 tickCurrent,,,,,) = IUniswapV3Pool(uniswapPoolAddress).slot0();

```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L104

### Recommended Mitigations
To make any calculation use a TWAP instead of slot0.

##

## [L-3] Calculating Fee Growth for Ill-Defined Tick Range Leading to Nonsensical Values

### Impact
When tickLower and tickUpper are the same, the function tries to calculate fee growth within a zero-width range.

The variables feeGrowthBelow0X128, feeGrowthBelow1X128, feeGrowthAbove0X128, and feeGrowthAbove1X128 are determined based on comparisons between tickCurrent, tickLower, and tickUpper.

Since the range is ill-defined, the fee growth values calculated are nonsensical and do not represent any real liquidity position.
This can lead to incorrect fee distributions, as the calculated fee growth inside the range does not correspond to any actual accrued fees.

```solidity
FILE: 2024-05-predy/src/libraries/UniHelper.sol

 function getFeeGrowthInside(address uniswapPoolAddress, int24 tickLower, int24 tickUpper)
        internal
        view
        returns (uint256 feeGrowthInside0X128, uint256 feeGrowthInside1X128)
    {
        (, int24 tickCurrent,,,,,) = IUniswapV3Pool(uniswapPoolAddress).slot0();

        uint256 feeGrowthGlobal0X128 = IUniswapV3Pool(uniswapPoolAddress).feeGrowthGlobal0X128();
        uint256 feeGrowthGlobal1X128 = IUniswapV3Pool(uniswapPoolAddress).feeGrowthGlobal1X128();

        // calculate fee growth below
        uint256 feeGrowthBelow0X128;
        uint256 feeGrowthBelow1X128;

        unchecked {
            {
                (,, uint256 lowerFeeGrowthOutside0X128, uint256 lowerFeeGrowthOutside1X128,,,,) =
                    IUniswapV3Pool(uniswapPoolAddress).ticks(tickLower);

                if (tickCurrent >= tickLower) {
                    feeGrowthBelow0X128 = lowerFeeGrowthOutside0X128;
                    feeGrowthBelow1X128 = lowerFeeGrowthOutside1X128;
                } else {
                    feeGrowthBelow0X128 = feeGrowthGlobal0X128 - lowerFeeGrowthOutside0X128;
                    feeGrowthBelow1X128 = feeGrowthGlobal1X128 - lowerFeeGrowthOutside1X128;
                }
            }

            // calculate fee growth above
            uint256 feeGrowthAbove0X128;
            uint256 feeGrowthAbove1X128;

            {
                (,, uint256 upperFeeGrowthOutside0X128, uint256 upperFeeGrowthOutside1X128,,,,) =
                    IUniswapV3Pool(uniswapPoolAddress).ticks(tickUpper);

                if (tickCurrent < tickUpper) {
                    feeGrowthAbove0X128 = upperFeeGrowthOutside0X128;
                    feeGrowthAbove1X128 = upperFeeGrowthOutside1X128;
                } else {
                    feeGrowthAbove0X128 = feeGrowthGlobal0X128 - upperFeeGrowthOutside0X128;
                    feeGrowthAbove1X128 = feeGrowthGlobal1X128 - upperFeeGrowthOutside1X128;
                }
            }

            feeGrowthInside0X128 = feeGrowthGlobal0X128 - feeGrowthBelow0X128 - feeGrowthAbove0X128;
            feeGrowthInside1X128 = feeGrowthGlobal1X128 - feeGrowthBelow1X128 - feeGrowthAbove1X128;
        }

```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L99-L147

### Example Scenario
Consider a scenario where tickLower and tickUpper are both set to 500.

Current Tick:

Let's assume tickCurrent is 500.
Fee Growth Calculation:

The function retrieves global fee growth values and fee growth outside the ticks.
Since tickLower == tickUpper == tickCurrent, the calculations for feeGrowthBelow and feeGrowthAbove will involve comparing the same values, leading to:

```solidity
feeGrowthBelow0X128 = lowerFeeGrowthOutside0X128;
feeGrowthBelow1X128 = lowerFeeGrowthOutside1X128;
feeGrowthAbove0X128 = upperFeeGrowthOutside0X128;
feeGrowthAbove1X128 = upperFeeGrowthOutside1X128;

```

Fee Growth Inside:

```solidity

feeGrowthInside0X128 = feeGrowthGlobal0X128 - feeGrowthBelow0X128 - feeGrowthAbove0X128;
feeGrowthInside1X128 = feeGrowthGlobal1X128 - feeGrowthBelow1X128 - feeGrowthAbove1X128;

```
This results in nonsensical values as feeGrowthBelow and feeGrowthAbove do not accurately represent the fee growth inside a zero-width range.

### Recommended Mitigation
Add this code to ensure both values are different 

```solidity

require(tickLower < tickUpper, "Invalid tick range");

```


##

## [L-4] Revenue Discrepancies in ``poolStatus.accumulatedProtocolRevenue`` and ``poolStatus.accumulatedCreatorRevenue`` Due to Ineffective Fee Division 

### Impact 
As the transaction volume increases, the cumulative loss due to ineffective fee division becomes significantly larger.

Solidity uses integer division, which discards any fractional part. For example, if totalProtocolFee is 5, dividing it by 2 results in 2, with a remainder of 1.
This remainder is lost if not handled properly.

Each time the division happens, the remainder is discarded. Over many transactions, these small remainders add up, leading to a significant loss in total accumulated revenue.

### POC

In the original fee division approach, integer division causes loss of precision. For example, dividing 1001 by 2 results in 500 each for protocol and creator revenues, with a remainder of 1 being lost.

### Original Method:
Calculation: totalProtocolFee = 1001
Division: halfFee = 1001 / 2 = 500, remainder = 1001 % 2 = 1
Revenue: protocolRevenue += 500, creatorRevenue += 500 (1 unit lost)
Over 1000 transactions, this results in a loss of 1000 units.

### Improved Method:
Calculation: totalProtocolFee = 1001
Division: halfFee = 1001 / 2 = 500, remainder = 1001 % 2 = 1
Revenue: protocolRevenue += 500 + 1, creatorRevenue += 500 (no units lost)

RemainingFee += remainder ;

By adding the remainder to one of the accounts, no units are lost, ensuring accurate revenue distribution. The remaining Fee can be accumulated the this fee can be shared to  protocolRevenue and creatorRevenue instead of losing 1000 uints.


```solidity
FILE:2024-05-predy/src/libraries/ApplyInterestLib.sol

poolStatus.accumulatedProtocolRevenue += totalProtocolFee / 2;
poolStatus.accumulatedCreatorRevenue += totalProtocolFee / 2;

```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ApplyInterestLib.sol#L71-L72

### Recommended Mitigation
As per POC ensures that all calculated fees are accurately accounted for, preventing any loss due to integer division. 

##

## [L-5] Chainlink's latestRoundData return stale or incorrect result

### Impact

On PriceFeed.sol, you are using latestRoundData, but there is no check if the return value indicates stale data. The current check ``quoteAnswer > 0`` not enough to ensure the staleness . 

This could lead to stale prices according to the Chainlink documentation: https://docs.chain.link/data-feeds/price-feeds/historical-data Related report: https://github.com/code-423n4/2021-05-fairside-findings/issues/70

```solidity
FILE:2024-05-predy/src/PriceFeed.sol

    (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        

```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L46-L52

### Recommended Mitigation
Incorporate the required checks to ensure the staleness 

```diff

(, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

+    (uint80 roundID,int256 quoteAnswer,uint256 timestamp,uint256 updatedAt,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

+ require(updatedAt >= roundID, "Stale price");
+ require(timestamp != 0,"Round not complete");

+ if (updatedAt < block.timestamp - maxDelayTime) //maxDelayTime minimum allowed delay 
+            revert PRICE_OUTDATED();
        
        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

```

##

## [L-6] Unable to remove pairs once added in the predy system

 In automated market makers (AMMs), liquidity pools represent the order book. Non-performing pairs can clutter the system, making it harder for users to find active trading pairs. Without the ability to prune inactive pairs, governance mechanisms become overwhelmed with managing an ever-growing list of pairs, complicating decision-making processes.


```solidity
FILE: 2024-05-predy/src/PredyPool.sol 

function registerPair(AddPairLogic.AddPairParams memory addPairParam) external onlyOperator returns (uint256) {
        return AddPairLogic.addPair(globalData, allowedUniswapPools, addPairParam);
    }

``` 

##

## [L-7] Risk of Operator Self-Assignment Hindering Protocol Updates and Security 

The function setOperator(address newOperator) external onlyOperator allows the current operator to change the operator address to a new one. 

- If the protocol requires updates or changes that the current operator does not agree with or that do not align with their interests, they can block these changes by refusing to set a new, neutral operator or owner. 

- In the worst-case scenario, a malicious operator can use this privilege to set the operator address to a contract or address that acts in bad faith, potentially leading to exploits, fund mismanagement, or other malicious activities.


```solidity
FILE: 2024-05-predy/src/PredyPool.sol

 function setOperator(address newOperator) external onlyOperator {
        require(newOperator != address(0));
        operator = newOperator;

        emit OperatorUpdated(newOperator);
    }

```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L97-L102

### Recommended Mitigation
- Restrict the ability to change the operator to the contract owner by using the onlyOwner modifier. This ensures that only a trusted and secure entity can make such critical changes.

- Use a multi-signature wallet to manage ownership and critical changes.

##

## [L-8]  Redundant Timestamp Comparison in pairStatus.lastUpdateTimestamp >= block.timestamp

The condition if (pairStatus.lastUpdateTimestamp >= block.timestamp) is used to determine if the lastUpdateTimestamp is greater than or equal to the current block's timestamp. While the equality check (==) is valid and necessary, the greater-than check (>) is redundant and practically impossible because block.timestamp represents the current block's timestamp and cannot be in the future.

```solidity
FILE: 2024-05-predy/src/libraries/ApplyInterestLib.sol

 // avoid applying interest rate multiple times in the same block
        if (pairStatus.lastUpdateTimestamp >= block.timestamp) {
            return;
        }

 // Update last update timestamp
        pairStatus.lastUpdateTimestamp = block.timestamp;


```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ApplyInterestLib.sol#L31-L34

### Recommended Mitigation

```solidity

if (pairStatus.lastUpdateTimestamp == block.timestamp) {
    return; // Skip the update if it's within the same block
}

```

##

## [L-9] ``onlyPoolOwner`` can intentionally sets ``feeRatio`` to 0 

The updateFeeRatio function currently lacks a check for a minimum fee ratio, which means that the pool owner can mistakenly or maliciously set the fee ratio to 0. This can have significant negative implications for the protocol,

- Setting the fee ratio to 0 would result in no fees being collected, which would impact the revenue for liquidity providers and the protocol itself.
- Without fees, the protocol may not be able to cover operational costs.
-  Zero fees could lead to abnormal trading behavior, including potential market manipulation.

```solidity
FILE:2024-05-predy/src/libraries/logic/AddPairLogic.sol

 function updateFeeRatio(DataType.PairStatus storage _pairStatus, uint8 _feeRatio) external {
        validateFeeRatio(_feeRatio);

        _pairStatus.feeRatio = _feeRatio;

        emit FeeRatioUpdated(_pairStatus.id, _feeRatio);
    }


```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L96-L102

### Recommended Mitigation
Enforce the MinFee check to avoid unintended consequences

```solidity
require(_feeRatio >= MIN_FEE_RATIO, "FEE_TOO_LOW");

``` 

##

## [L-10] Inappropriate Non-Positive Check on Unsigned Integer

The condition if (_amount <= 0) in Solidity is inappropriate when _amount is of type uint (unsigned integer). In Solidity, uint cannot be negative, and the only non-positive value it can take is 0. Therefore, checking if _amount is less than or equal to 0 is redundant, as 0 is the only possible value that could satisfy this condition.

```diff
FILE: 2024-05-predy/src/libraries/logic/SupplyLogic.sol

- 29: if (_amount <= 0) {
+ 29: if (_amount > 0) {

```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L29

##

## [L-11] Risk of Duplicate Uniswap Pools Leading to Data Redundancy and Inconsistency 

### Impact

- Users and smart contracts interacting with the protocol may retrieve or reference different pairIds for the same pool, leading to inconsistent behavior and potential errors in operations such as trading, liquidity provision, and fee calculations.

-  This can lead to logical errors in smart contracts, incorrect data aggregation, and flawed analytics, impacting decision-making and automated processes within the protocol.

The current implementation of the addPair function can allow the same Uniswap pool to be added multiple times due to the way it handles the allowedUniswapPools check and the pairId generation.

- This increases the attack surface for malicious actors, who could exploit discrepancies between different instances to manipulate the protocol or extract undue benefits.

### Pair ID Assignment and Increment:

pairId = _global.pairsCount assigns the current pair count to pairId.
_global.pairsCount is incremented at the end of the function.

### No Check for Duplicate Pools:

The function checks if pairId is less than Constants.MAX_PAIRS but does not check if the uniswapPool has already been added.
The allowedUniswapPools[_addPairParam.uniswapPool] = true; line is executed after the pair status is stored, but there is no pre-check to prevent adding the same pool if it already exists in the allowedUniswapPools mapping.

### Duplicate Addition Scenario:

If a user calls addPair with the same uniswapPool multiple times, each call will assign a new pairId because _global.pairsCount is incremented after each addition.
Since there is no check before adding to allowedUniswapPools, the same uniswapPool can be added multiple times, each with a different pairId.

```soldiity

function addPair(
        GlobalDataLibrary.GlobalData storage _global,
        mapping(address => bool) storage allowedUniswapPools,
        AddPairParams memory _addPairParam
    ) external returns (uint256 pairId) {
        pairId = _global.pairsCount;

        require(pairId < Constants.MAX_PAIRS, "MAXP");

        IUniswapV3Pool uniswapPool = IUniswapV3Pool(_addPairParam.uniswapPool);

        address stableTokenAddress = _addPairParam.quoteToken;

        IUniswapV3Factory uniswapV3Factory = IUniswapV3Factory(_global.uniswapFactory);

        // check the uniswap pool is registered in UniswapV3Factory
        if (
            uniswapV3Factory.getPool(uniswapPool.token0(), uniswapPool.token1(), uniswapPool.fee())
                != _addPairParam.uniswapPool
        ) {
            revert InvalidUniswapPool();
        }

        require(uniswapPool.token0() == stableTokenAddress || uniswapPool.token1() == stableTokenAddress, "C3");

        bool isQuoteZero = uniswapPool.token0() == stableTokenAddress;

        _storePairStatus(
            stableTokenAddress,
            _global.pairs,
            pairId,
            isQuoteZero ? uniswapPool.token1() : uniswapPool.token0(),
            isQuoteZero,
            _addPairParam
        );

        allowedUniswapPools[_addPairParam.uniswapPool] = true;

        _global.pairsCount++;

        emit PairAdded(pairId, _addPairParam.quoteToken, _addPairParam.uniswapPool);
    }


```

```solidity

 function _storePairStatus(
        address quoteToken,
        mapping(uint256 => DataType.PairStatus) storage _pairs,
        uint256 _pairId,
        address _tokenAddress,
        bool _isQuoteZero,
        AddPairParams memory _addPairParam
    ) internal {
        validateRiskParams(_addPairParam.assetRiskParams);
        validateFeeRatio(_addPairParam.fee);

        require(_pairs[_pairId].id == 0, "AAA");

        _pairs[_pairId] = DataType.PairStatus(
            _pairId,
            quoteToken,
            _addPairParam.poolOwner,
            Perp.AssetPoolStatus(
                quoteToken,
                deploySupplyToken(quoteToken),
                ScaledAsset.createAssetStatus(),
                _addPairParam.quoteIrmParams,
                0,
                0
            ),
            Perp.AssetPoolStatus(
                _tokenAddress,
                deploySupplyToken(_tokenAddress),
                ScaledAsset.createAssetStatus(),
                _addPairParam.baseIrmParams,
                0,
                0
            ),
            _addPairParam.assetRiskParams,
            Perp.createAssetStatus(
                _addPairParam.uniswapPool,
                -_addPairParam.assetRiskParams.rangeSize,
                _addPairParam.assetRiskParams.rangeSize
            ),
            _addPairParam.priceFeed,
            _isQuoteZero,
            _addPairParam.allowlistEnabled,
            _addPairParam.fee,
            block.timestamp
        );

        emit AssetRiskParamsUpdated(_pairId, _addPairParam.assetRiskParams);
        emit IRMParamsUpdated(_pairId, _addPairParam.quoteIrmParams, _addPairParam.baseIrmParams);
    }

```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L53-L94

### Recommended Mitigation
Add require check to ensure pool already allowed or not in addPair() function

```
require(!allowedUniswapPools[_addPairParam.uniswapPool] , "Pool already created");

```













