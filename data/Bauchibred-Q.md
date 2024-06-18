# QA Report for **Predy**

## Table of Contents

| Issue ID                                                                                                                                                                     | Description                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [QA-01](<#qa-01-decaylib#decay2()-should-prevent-division-by-zero>)                                                                                                          | `DecayLib#decay2()` should prevent division by zero                                                                                                          |
| [QA-02](<#qa-02-pricefeed#getsqrtprice()-could-over/undervalue-the-quote-price-leading-to-wrong-liquidation-decisions>)                                                      | `PriceFeed#getSqrtPrice()` could over/undervalue the quote price leading to wrong liquidation decisions                                                      |
| [QA-03](#qa-03-valid-liquidations-would-fail-in-turbulent-situations-because-the-max-slippage-idea-is-applied-thats-3%)                                                      | Valid liquidations would fail in turbulent situations because the max slippage idea is applied that's 3%                                                     |
| [QA-04](#qa-04-the-current-pricefeed.sol-could-become-completely-unavailable)                                                                                                | The current `pricefeed.sol` could become completely unavailable                                                                                              |
| [QA-05](#qa-05-no-deadlines-applies-during-swaps-which-would-then-cause-for-swaps-to-be-potentially-maliciously-executed)                                                    | No deadlines applies during swaps which would then cause for swaps to be potentially maliciously executed                                                    |
| [QA-06](#qa-06-liquidations-can-be-stolen-from-honest-users)                                                                                                                 | Liquidations can be stolen from honest users                                                                                                                 |
| [QA-07](<#qa-07-external-queries-from-pricefeed#getsqrtprice()-should-be-be-wrapped-in-a-try-catch>)                                                                         | External queries from `PriceFeed#getSqrtPrice()` should be be wrapped in a try catch                                                                         |
| [QA-08](#qa-08-a-user-can-frontrun-liquidations-of-their-unhealthy-accounts-by-liquidating-in-small-portions-by-themselves)                                                  | A user can frontrun liquidations of their unhealthy accounts by liquidating in small portions by themselves                                                  |
| [QA-09](#qa-09-trades-are-being-finalized-with-an-easily-manipulatable-prices-which-might-cause-frequent-reverts)                                                            | Trades are being finalized with an easily manipulatable prices which might cause frequent reverts                                                            |
| [QA-10](#qa-10-a-filler-can-front/back-run-the-execution-of-a-trade-to-immediately-liquidate-a-user)                                                                         | A filler can front/back run the execution of a trade to immediately liquidate a user                                                                         |
| [QA-11](<#qa-11-external-queries-from-getsqrtprice()-should-be-done-more-accurately>)                                                                                        | External queries from `getSqrtPrice()` should be done more accurately                                                                                        |
| [QA-12](#qa-12-valid-pairs-seem-to-wrongly-invalidated)                                                                                                                      | Valid pairs seem to wrongly invalidated                                                                                                                      |
| [QA-13](#qa-13-users-could-be-liquidated-in-the-next-block)                                                                                                                  | Users could be liquidated in the next block                                                                                                                  |
| [QA-14](#qa-14-implement-better-naming-conventions-to-codes-&-fix-typos)                                                                                                     | Implement better naming conventions to codes & fix typos                                                                                                     |
| [QA-15](<#qa-15-predypool#uniswapv3mintcallback()-is-potentially-vulnerable-to-some-attacks>)                                                                                | `PredyPool#uniswapV3MintCallback()` is potentially vulnerable to some attacks                                                                                |
| [QA-16](<#qa-16-supplylogic#burnbondandtransfertoken()-could-revert-for-some-tokens-in-the-future>)                                                                          | `SupplyLogic#burnBondAndTransferToken()` could revert for some tokens in the future                                                                          |
| [QA-17](<#qa-17-some-locks-would-be-un-initializable-due-to-direct-balanceof()-call>)                                                                                        | Some locks would be un-initializable due to direct `balanceOf()` call                                                                                        |
| [QA-18](#qa-18-deployment-of-new-supply-tokens-would-fail-for-some-tokens)                                                                                                   | Deployment of new supply tokens would fail for some tokens                                                                                                   |
| [QA-19](#qa-19-solmates-safetransferlib-shouldnt-be-used-as-it-doesnt-check-for-account-existence)                                                                           | Solmate's `SafeTransferLib` shouldn't be used as it doesn't check for account existence                                                                      |
| [QA-20](#qa-20-setters-dont-have-equality-checkers)                                                                                                                          | Setters don't have equality checkers                                                                                                                         |
| [QA-21](#qa-21-oracle-price-updates-could-be-front-run-to-game-the-system)                                                                                                   | Oracle price updates could be front run to game the system                                                                                                   |
| [QA-22](<#qa-22-make-predypool#withdrawcreatorrevenue()-more-effective>)                                                                                                     | Make `PredyPool#withdrawCreatorRevenue()` more effective                                                                                                     |
| [QA-23](<#qa-23--uniswapsettlement#swapexactin()-should-be-made-safer>)                                                                                                      | `UniswapSettlement#swapExactIn()` should be made safer                                                                                                       |
| [QA-24](<#qa-24--pricefeed#getsqrtprice()-query-to-latestrounddata()-is-done-in-a-wrong-way-since-there-is-no-check-first-to-see-if-the-sequencer-is-down>)                  | `PriceFeed#getSqrtPrice()` query to `latestRoundData()` is done in a wrong way since there is no check first to see if the sequencer is down                 |
| [QA-25](#qa-25-pricefeedgetsqrtprice-might-be-broken-in-the-future-due-to-its-integration-with-pyths-expo-value)                                                             | `PriceFeed#getSqrtPrice()` might be broken in the future due to it's integration with Pyth's `expo` value                                                    |
| [QA-26](#qa-26-protocol-uses-two-diferent-price-source-when-querying-prices-which-is-riskier-than-using-one-sure-source-or-having-the-second-confirmed-source-as-a-fallback) | Protocol uses two diferent price source when querying prices which is riskier than using one sure source or having the second confirmed source as a fallback |

## QA-01 `DecayLib#decay2()` should prevent division by zero

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/DecayLib.sol#L16-L37

```solidity
    function decay2(uint256 startPrice, uint256 endPrice, uint256 decayStartTime, uint256 decayEndTime, uint256 value)
        internal
        pure
        returns (uint256 decayedPrice)
    {
        if (decayEndTime < decayStartTime) {
            revert EndTimeBeforeStartTime();
        } else if (decayEndTime <= value) {
            decayedPrice = endPrice;
        } else if (decayStartTime >= value) {
            decayedPrice = startPrice;
        } else {
            uint256 elapsed = value - decayStartTime;
            uint256 duration = decayEndTime - decayStartTime;

            if (endPrice < startPrice) {
                decayedPrice = startPrice - (startPrice - endPrice) * elapsed / duration;
            } else {
                decayedPrice = startPrice + (endPrice - startPrice) * elapsed / duration;
            }
        }
    }
```

Evidently, in the edge case where `decayEndTime == decayStartTime` this leads to protocol to then have `duration` as `0` making the execution to attempt dividing by `0`.

### Impact

Panic reverts due to division by zero... bad code practise.

### Recommended Mitigation Steps

Consider having the check to revert being non-strict and then maybe change the error message, since it doesn't make sense to even have `decayEndTime == decayStartTime` in the first place, i.e apply these changes:

```diff
    function decay2(uint256 startPrice, uint256 endPrice, uint256 decayStartTime, uint256 decayEndTime, uint256 value)
        internal
        pure
        returns (uint256 decayedPrice)
    {
-        if (decayEndTime < decayStartTime) {
-            revert EndTimeBeforeStartTime();
+        if (decayEndTime < =decayStartTime) {
+            revert EndTimeBeforeOrEqualToStartTime();
        } else if (decayEndTime <= value) {
            decayedPrice = endPrice;
        } else if (decayStartTime >= value) {
            decayedPrice = startPrice;
        } else {
            uint256 elapsed = value - decayStartTime;
            uint256 duration = decayEndTime - decayStartTime;

            if (endPrice < startPrice) {
                decayedPrice = startPrice - (startPrice - endPrice) * elapsed / duration;
            } else {
                decayedPrice = startPrice + (endPrice - startPrice) * elapsed / duration;
            }
        }
    }
```

## QA-02 `PriceFeed#getSqrtPrice()` could over/undervalue the quote price leading to wrong liquidation decisions

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

```solidity
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();  //@audit
        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
```

This function returns the square root of the baseToken price quoted in quoteToken, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`.

Problem however is that that Chainlink's `latestRoundData` is being queried, but no min/max checks are applied, leading to contracts working with flawed pricing.

> Keep in mind that the `PriceFeed#getSqrtPrice()` function is heavily used within the protocol in multiple core logics from getting the vault's TVL in the Liquidation logic to see if the vault is safe or not.

### Impact

If the prices ever go over the min/max boundary then protocol is going to ingest heavily inflated/deflated pricing data as the prices returned would be wrong.

Considering protocol plans to support a lot of tokens this would to be a problem as multiple tokens would have their source feed's aggregators with this min/max circuit breakers and as such it should be checked for an asset that has it, since this has quite a high impact with a low likelihood, but would be key to note that this has happened before with `LUNA`.

### Recommended Mitigation Steps

Consider attaching the min/max checkers for aggregators that have it and then route the pricing logic to a fallback oracle in the case where the returned prices are at these boundaries.

## QA-03 Valid liquidations would fail in turbulent situations because the max slippage idea is applied that's 3%

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39-L119

```solidity
    function liquidate(
        uint256 vaultId,
        uint256 closeRatio,
        GlobalDataLibrary.GlobalData storage globalData,
        bytes memory settlementData
    ) external returns (IPredyPool.TradeResult memory tradeResult) {
        require(closeRatio > 0 && closeRatio <= 1e18, "ICR");
        DataType.Vault storage vault = globalData.vaults[vaultId];
        DataType.PairStatus storage pairStatus = globalData.pairs[vault.openPosition.pairId];

        // update interest growth
        ApplyInterestLib.applyInterestForToken(globalData.pairs, vault.openPosition.pairId);

        // update rebalance interest growth
        Perp.updateRebalanceInterestGrowth(pairStatus, pairStatus.sqrtAssetStatus);

        // Checks the vault is danger
        (uint256 sqrtOraclePrice, uint256 slippageTolerance) =
            checkVaultIsDanger(pairStatus, vault, globalData.rebalanceFeeGrowthCache);

        IPredyPool.TradeParams memory tradeParams = IPredyPool.TradeParams(
            vault.openPosition.pairId,
            vaultId,
            -vault.openPosition.perp.amount * int256(closeRatio) / 1e18,
            -vault.openPosition.sqrtPerp.amount * int256(closeRatio) / 1e18,
            ""
        );

        tradeResult = Trade.trade(globalData, tradeParams, settlementData);

        vault.margin += tradeResult.fee + tradeResult.payoff.perpPayoff + tradeResult.payoff.sqrtPayoff;

        tradeResult.sqrtTwap = sqrtOraclePrice;

        bool hasPosition;

        (tradeResult.minMargin,, hasPosition,) =
            PositionCalculator.calculateMinMargin(pairStatus, vault, DataType.FeeAmount(0, 0));

        // Check if the price is within the slippage tolerance range to ensure that the price does not become
        // excessively favorable to the liquidator.
        SlippageLib.checkPrice(
            sqrtOraclePrice,
            tradeResult,
            slippageTolerance,
            tradeParams.tradeAmountSqrt == 0 ? 0 : _MAX_ACCEPTABLE_SQRT_PRICE_RANGE//@audit
        );

        uint256 sentMarginAmount = 0;

        if (!hasPosition) {
            int256 remainingMargin = vault.margin;

            if (remainingMargin > 0) {
                if (vault.recipient != address(0)) {
                    // Send the remaining margin to the recipient.
                    vault.margin = 0;

                    sentMarginAmount = uint256(remainingMargin);

                    ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);
                }
            } else if (remainingMargin < 0) {
                vault.margin = 0;

                // To prevent the liquidator from unfairly profiting through arbitrage trades in the AMM and passing losses onto the protocol,
                // any losses that cannot be covered by the vault must be compensated by the liquidator
                ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));
            }
        }

        emit PositionLiquidated(
            tradeParams.vaultId,
            tradeParams.pairId,
            tradeParams.tradeAmount,
            tradeParams.tradeAmountSqrt,
            tradeResult.payoff,
            tradeResult.fee,
            sentMarginAmount
        );
    }
```

This function is used to liquidate a vault that is now in danger as the name suggests and it takes in several parameters, including the vault ID, a close ratio, global data, and settlement data, issue however as hinted with the @audit tag is with the integration of the `_MAX_ACCEPTABLE_SQRT_PRICE_RANGE` [which is hardcoded as 3%](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L27) so in a case where this attempt at liquidating validly pushes the price above this limit the transaction erroneously reverts when checking the slippage

### Impact

Borderline medium/low, since this leads to a DOS to liquidations in turbulent situations, which then hints how protocol are allowing themselves more risks

### Recommended Mitigation Steps

Consider not hardcoding this value so it's settable depending on the current market situation.

## QA-04 The current `pricefeed.sol` could become completely unavailable

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L28-L33

```solidity

contract PriceFeed {
    address private immutable _quotePriceFeed;
    address private immutable _pyth;
    uint256 private immutable _decimalsDiff;
    bytes32 private immutable _priceId;
```

And https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

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

We can see that this is how the pricing logic works and this is used throughout the pricing logic present in the codebase for core functionalities like liquidating, etc.

Problem here however is that the `feedIds` are hardcoded and have been made immutable, but this is a wrong concept considering the underlying feed address could be changed later on for whatever reasons for example by Chainlink, which would then make this function always revert `     (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();` since the feed would be considered non-existing, protocol also understands how this bug logic is problematic which is why in the `AddPairLogic` there is a logic to update feeds https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L112-L117

```solidity
    function updatePriceOracle(DataType.PairStatus storage _pairStatus, address _priceOracle) external {
        _pairStatus.priceFeed = _priceOracle;

        emit PriceOracleUpdated(_pairStatus.id, _priceOracle);
    }

```

However since this functionality is absent in `Pricefeed.sol` this means that when an oracle goes down, completely all logics routing through the pricefeed's `getSqrtPrice()` would be permanently DOS'd

### Impact

Borderline medium/low
Impact here is very high considering even liquidations of vaults in danger now would be impossible, however considering the likelihood of this is very minimal I assume it to be an L severity.

> If the judge sees fit they should upgrade as there are valid arguments for this being an M severity.

### Recommended Mitigation Steps

Consider integrating a similar functionality of updating the feeds as is present in the `AddPairLogic`.

## QA-05 No deadlines applies during swaps which would then cause for swaps to be potentially maliciously executed

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L22-L56

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

        amountOut = _swapRouter.exactInput(
            ISwapRouter.ExactInputParams(data, recipient, block.timestamp, amountIn, amountOutMinimum)
        );
    }

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

        amountIn = _swapRouter.exactOutput(
            ISwapRouter.ExactOutputParams(data, recipient, block.timestamp, amountOut, amountInMaximum)
        );

        if (amountInMaximum > amountIn) {
            ERC20(quoteToken).safeTransfer(msg.sender, amountInMaximum - amountIn);
        }
    }
```

These functions are present in the helper uniswap settlement contract ad are used to swap via uniswap, problem here however is that this attempts at swapping are done without any real deadline whatsoever, which then causes for the transaction to be potentially maliciously executed since the transaction can then be forced to sit in the mempool for very long.

### Impact

Users could lose out on their assets, albeit in this case in `USD` value since a slippage value is set, however this still leads to loss for users considering while the transaction is sitting in the mempool, the value of the token could be fast dropping, leading to the slippage to not really be a slippage.

### Recommended Mitigation Steps

Consider passing in a valid deadline value.

## QA-06 Liquidations can be stolen from honest users

### Proof of Concept

Protocol integrates a [liquidation mechanism](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39) however this is not done in a commit-reveal pattern which then leaves this approach to be able to be stolen by a third party, normally this could be via a classic front run however since the chains protocol is going to deploy in is optimistic L2 chains then this leaves protocol more to bug ideas like the liquidations being stolen during a re-org or sequencer downtime or even front-rins on slower sequencer ingestion chains.

### Impact

Rewards from liquidations would be stolen from honest users/liquidators.

### Recommended Mitigation Steps

Consider integrating a commit-reveal scheme.

## QA-07 External queries from `PriceFeed#getSqrtPrice()` should be be wrapped in a try catch

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

```solidity
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();  //@audit
        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
```

This function returns the square root of the baseToken price quoted in quoteToken, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`.

Problem however is that that Chainlink's `latestRoundData` is being queried, but this call lacks error handling for the potential failure of ` source.latestRoundData()` which could fail due to the call to `oracle.latestRoundData()` , note that Chainlink pricefeeds could revert due to whatever reason, i.e say maintenance or maybe the Chainlink team decide to change the underlying address. Now this omission of not considering this call failing would lead to systemic issues, since calls to this would now revert halting any action that requires this call to succeed.

> Keep in mind that the `PriceFeed#getSqrtPrice()` function is heavily used within the protocol in multiple core logics from getting the vault's TVL in the Liquidation logic to see if the vault is safe or not.

### Impact

Borderline medium/low, as this essentially breaks core functionalities like liquidating and whatever requires for the usd value of an asset to be queried since there would be a complete revert.

Considering protocol plans to support a lot of tokens this would to be a problem as multiple tokens would have their source feed's aggregators with this min/max circuit breakers and as such it should be checked for an asset that has it, since this has quite a high impact with a low likelihood, but would be key to note that this has happened before with `LUNA`.

### Recommended Mitigation Steps

Wrap the ` .latestRoundData()` call in a try-catch block, then handle the error (e.g., revert with a specific message or use an alternative pricing method, the latter is a better fix as it ensures the protocol still functions as expected on the fallback oracle.

## QA-08 A user can frontrun liquidations of their unhealthy accounts by liquidating in small portions by themselves

### Proof of Concept

When [liquidating](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L45) ther eis the idea of a `closefactor` which a liquidator attaches to see how much of the vault they want to liquidate, i.e https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39-L45

```solidity
    function liquidate(
        uint256 vaultId,
        uint256 closeRatio,
        GlobalDataLibrary.GlobalData storage globalData,
        bytes memory settlementData
    ) external returns (IPredyPool.TradeResult memory tradeResult) {
        require(closeRatio > 0 && closeRatio <= 1e18, "ICR");
```

Now this liquidation attempt, doesn't block users themselves from liquidating their own accounts, i.e `msg.sender` should not be the recipeint of the margin of the vault when it gets liquidated, now since this check/logic is not applied, this then allows for a bug flow like the below to be possible:

- A position becomes partially liquidatable _partially here could be as high as 90%_
- A liquidator passes in the attempt to liquidate this position providing their preferred `closeFactor`.
- Since the owner of the position themselves can pass in a liquidation for their positions
- They can then frontrun the valid call to `liquidate` with their own liquidation call, albeit in this instance they would be passing in **a very little closeFactor** makes the honest call to liquidate to be off.
- Considering the closeFactor attached to the liquidate call ends up determining if the vault is liquidatable or not.
- So a _malicious_ user can then skim off the `closeFactor` by oing this to make the end trasaction revert.

### Impact

Borderline low/medium, attached as QA considering this needs to logic of frontruns which is not readily avaialable on the L2 chains where protocol is going to be deployed.

### Recommended Mitigation Steps

Consider not allowing the `msg.sender` to liquidate their own positions.

## QA-09 Trades are being finalized with an easily manipulatable prices which might cause frequent reverts

### Proof of Concept

Take a look at the fucntion that ends up being called whenever there is a need to exefcute a trade of any kind https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L32-L74

```solidity
    function trade(
        GlobalDataLibrary.GlobalData storage globalData,
        IPredyPool.TradeParams memory tradeParams,
        bytes memory settlementData
    ) external returns (IPredyPool.TradeResult memory tradeResult) {
        DataType.PairStatus storage pairStatus = globalData.pairs[tradeParams.pairId];
        Perp.UserStatus storage openPosition = globalData.vaults[tradeParams.vaultId].openPosition;

        // settle user balance and fee
        DataType.FeeAmount memory realizedFee =
            settleUserBalanceAndFee(pairStatus, globalData.rebalanceFeeGrowthCache, openPosition);

        // calculate required token amounts
        (int256 underlyingAmountForSqrt, int256 stableAmountForSqrt) = Perp.computeRequiredAmounts(
            pairStatus.sqrtAssetStatus, pairStatus.isQuoteZero, openPosition, tradeParams.tradeAmountSqrt
        );

        tradeResult.sqrtPrice = getSqrtPrice(pairStatus.sqrtAssetStatus.uniswapPool, pairStatus.isQuoteZero);//@audit slot0 is used to place trades which is easily manipulatable

        // swap tokens

        SwapStableResult memory swapResult = swap(
            globalData,
            tradeParams.pairId,
            SwapStableResult(-tradeParams.tradeAmount, underlyingAmountForSqrt, realizedFee.feeAmountBase, 0),
            settlementData,
            tradeResult.sqrtPrice,//@audit
            tradeParams.vaultId
        );

        tradeResult.averagePrice = swapResult.averagePrice;

        // add asset or debt
        tradeResult.payoff = Perp.updatePosition(
            pairStatus,
            openPosition,
            Perp.UpdatePerpParams(tradeParams.tradeAmount, swapResult.amountPerp),
            Perp.UpdateSqrtPerpParams(tradeParams.tradeAmountSqrt, swapResult.amountSqrtPerp + stableAmountForSqrt)
        );

        tradeResult.fee = realizedFee.feeAmountQuote + swapResult.fee;
        tradeResult.vaultId = tradeParams.vaultId;
    }
```

Function works fine, only issue is that it hardcodes the use of `slot0` when chosing the price that the swap gets finalized on.

Going to the implementation of `getSqrtPrice` we can see that it ends up querying the `UniHelper.getSqrtPrice` i.e https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L112-L114

```solidity
    function getSqrtPrice(address uniswapPoolAddress, bool isQuoteZero) internal view returns (uint256 sqrtPriceX96) {
        return UniHelper.convertSqrtPrice(UniHelper.getSqrtPrice(uniswapPoolAddress), isQuoteZero);
    }
```

Now going to the implementation of UniHelper.getSqrtPrice we can see that tthe price data that is returned from this is the from `slot0` https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L13-L16

```solidity
    function getSqrtPrice(address uniswapPoolAddress) internal view returns (uint160 sqrtPrice) {
        (sqrtPrice,,,,,,) = IUniswapV3Pool(uniswapPoolAddress).slot0();
    }

```

WHich showcases that at the end of the day trades executions are being done with the price from `slot0`. Now Uniswap.slot0 is the most recent data point and can be manipulated easily via MEV bots and Flashloans with sandwich attacks; which can cause the loss of funds or leak of value to protocol when users are interacting with this function, which showcases how trades that end up being executed by this could be affected especially when non-tech savvy users are integrating it.

### Impact

QA, I assume users should be tech-savvy enough to place slippages around their trades, to ensure there is a revert in case the price used goes out of their accepted bounds, hwoever in the case where they don't apply a good enough slippage their assets could be skimmed off.

### Recommended Mitigation Steps

Reconsider the logic

## QA-10 A filler can front/back run the execution of a trade to immediately liquidate a user

### Proof of Concept

Whenever a trade is placed, in short to pass the order to a filler, the trader is required to sign the order and passes the order and signature to the filler. After which the filler calls `executeOrderV3` or `executeTrade()`.

Now would be key to note that, for some trades prices are required from Pyth, however protocol does not enforce that the prices are updated before being integrated.

This then allows for a filler to:

- Take a signed trade,
- Execute the trade using stale prices.-
- Back run the tx to game the execution.
- That is in the case the position is liquidatable with either of the pricing, the filler can just route their logic to ensure they make the most gain from the executions.

This is because the pythprice is not updated when placing the trade and since pyth prices can be queried twice in a block the fillers can just front/back run the tx and liquidate a user.

Would be key to note that asides the price data being manually updated, Pyth oracles also allow for the reading of two different prices in the same transaction which could be used as an avenue for heavy arbitraging. This is because the Pyth network is constantly updating the latest price (every 400ms), so when a new price is submitted on-chain it is not necessary that the price is the latest one. Otherwise, the process of querying the data off-chain, building the transaction, and submitting it on-chain would be required to be done with a latency of less than 400ms, which is not feasible. So this makes it possible to submit two different prices in the same transaction and, thus, fetch two different prices in the same transaction, showcasing how the front back running could easily be feasible, putting users at risk.

### Impact

Borderline low/medium.

> On one hand this means that in the case of liquidations, users could be _unfairly_ liquidated due to the nature of Pyth being able to return two distince prices in a transaction, on another hand this seems to be like user error, so leaving to judge to upgrade as they see fit.

### Recommended Mitigation Steps

At the very least all pricing data that are to be ingested from pyth during the execution of a trade should ensure that they query Pyth's `updatePriceFeeds()` function as has been documented: https://docs.pyth.network/price-feeds/api-reference/evm/update-price-feeds. Which would then ensure the right prices are being ingested and the chance of having a massive difference ecven in the case where two different prices are gotten would be minimal considering the price was updated.

## QA-11 External queries from `getSqrtPrice()` should be done more accurately

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

```solidity
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();  //@audit
        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
```

This function returns the square root of the baseToken price quoted in quoteToken, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`.

Problem however is that that Chainlink's `latestRoundData` is being queried, but this call lacks a check to see the amount of decimals the feed has, unlike the ` require(basePrice.expo == -8, "INVALID_EXP");` check applied for the pyth Oracle which ensures that the decimal is indeed `8`.

This then means that in the case where a feed like AMPL/USD is integrated that has a different amount of decimals compared to it's pairs the price calculated is going to be massively inaccurate in our case here it is going to be heavrily inflated as the price returned from chainlink is used as the numerator in the operation.

> Keep in mind that the `PriceFeed#getSqrtPrice()` function is heavily used within the protocol in multiple core logics from getting the vault's TVL in the Liquidation logic to see if the vault is safe or not.

### Impact

Seems to be QA considering one would assume the protocol to do all the vetting before integrating a pricefeed.

### Recommended Mitigation Steps

Consider calling AggregatorV3Interface.decimals() to get the exact number of decimals for the price feed being called.

## QA-12 Valid pairs seem to wrongly invalidated

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L26-L32

```solidity
    function validateVaultId(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId) internal view {
        if (vaultId <= 0 || globalData.vaultCount <= vaultId) revert IPredyPool.InvalidPairId();
    }

    function validate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal view {
        if (pairId <= 0 || globalData.pairsCount <= pairId) revert IPredyPool.InvalidPairId();//@audit
    }
```

These functions are used to validate the vaultIds or pairIds, issue however is that these functions use a non-strict check when doing this validation, which then leads to the validations to fail when the pair/vault Id is the freshest of the bunc, i.e we expect the last pair to be `globalData.pairsCount` and the last vaultId to be equal to `globalData.vaultCount` but currently passing in these values would cause an invalidation of them.

### Impact

Intended fucntionality seems to be broken as Ids that are valid are percevied as invalid for both the vaults and the pairs.

### Recommended Mitigation Steps

Consider making the checks strict, i.e

```diff
    function validateVaultId(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId) internal view {
-        if (vaultId <= 0 || globalData.vaultCount <= vaultId) revert IPredyPool.InvalidPairId();
+        if (vaultId <= 0 || globalData.vaultCount < vaultId) revert IPredyPool.InvalidPairId();
    }

    function validate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal view {
-        if (pairId <= 0 || globalData.pairsCount <= pairId) revert IPredyPool.InvalidPairId();
+        if (pairId <= 0 || globalData.pairsCount < pairId) revert IPredyPool.InvalidPairId();
    }
```

## QA-13 Users could be liquidated in the next block

### Proof of Concept

Protocol integrates a [liquidation mechanism](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39) however this logic does not include any buffer whatsoever, now users are allowed to borrow with a condition where `liquidatable state == to the liquidating threshold`, which would mean that they could be liquidatable immeditaely in the next block.

More info on this bug case can be seen here:

- https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/1038 still here, otherwise - https://github.com/code-423n4/2024-03-revert-lend-findings/issues/363

### Impact

Users could unfailr be liquidated in the next block

### Recommended Mitigation Steps

Consider when creating a position to always have a gap between the ` user's liquidatable sstate` & ` thier liquidating threshold`, this way we can ensure they are not imediately liquidated in the next block.

## QA-14 Implement better naming conventions to codes & fix typos

### Proof of Concept

Multiple instances accross code, for example take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/LPMath.sol#L30-L66

```solidity
    function calculateAmount0ForLiquidity(
        uint160 sqrtRatioA,
        uint160 sqrtRatioB,
        uint256 liquidityAmount,
        bool isRoundUp
    ) internal pure returns (int256) {
        if (liquidityAmount == 0 || sqrtRatioA == sqrtRatioB) {
            return 0;
        }

        bool swaped = sqrtRatioA > sqrtRatioB;//@audit

        if (sqrtRatioA > sqrtRatioB) (sqrtRatioA, sqrtRatioB) = (sqrtRatioB, sqrtRatioA);

        int256 r;

        bool _isRoundUp = swaped ? !isRoundUp : isRoundUp;
        uint256 numerator = liquidityAmount;

        if (_isRoundUp) {
            uint256 r0 = FullMath.mulDivRoundingUp(numerator, FixedPoint96.Q96, sqrtRatioA);
            uint256 r1 = FullMath.mulDiv(numerator, FixedPoint96.Q96, sqrtRatioB);

            r = SafeCast.toInt256(r0) - SafeCast.toInt256(r1);
        } else {
            uint256 r0 = FullMath.mulDiv(numerator, FixedPoint96.Q96, sqrtRatioA);
            uint256 r1 = FullMath.mulDivRoundingUp(numerator, FixedPoint96.Q96, sqrtRatioB);

            r = SafeCast.toInt256(r0) - SafeCast.toInt256(r1);
        }

        if (swaped) {
            return -r;
        } else {
            return r;
        }
    }
```

As hinted by the @audit tag, this function uses a `swaped` bool value, however this shold instead be `swap**P**ed`

- Another instance is the below where **required** hasn't been rightly spelled: https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Perp.sol#L421-L439

```solidity

    /**
     * @notice Computes reuired amounts to increase or decrease sqrt positions.
     * (L/sqrt{x}, L * sqrt{x})
     */
    function computeRequiredAmounts(
        SqrtPerpAssetStatus storage _sqrtAssetStatus,
        bool _isQuoteZero,
        UserStatus memory _userStatus,
        int256 _tradeSqrtAmount
    ) internal returns (int256 requiredAmountUnderlying, int256 requiredAmountStable) {
        if (_tradeSqrtAmount == 0) {
            return (0, 0);
        }

        if (!Reallocation.isInRange(_sqrtAssetStatus)) {
            revert OutOfRangeError();
        }

```

### Impact

Bad naming conventions, hard to understand code.

### Recommended Mitigation Steps

Consider applying these fixes https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/LPMath.sol#L30-L66

```diff
    function calculateAmount0ForLiquidity(
        uint160 sqrtRatioA,
        uint160 sqrtRatioB,
        uint256 liquidityAmount,
        bool isRoundUp
    ) internal pure returns (int256) {
        if (liquidityAmount == 0 || sqrtRatioA == sqrtRatioB) {
            return 0;
        }

-        bool swaped = sqrtRatioA > sqrtRatioB;
+        bool swapped = sqrtRatioA > sqrtRatioB;

        if (sqrtRatioA > sqrtRatioB) (sqrtRatioA, sqrtRatioB) = (sqrtRatioB, sqrtRatioA);

        int256 r;

-        bool _isRoundUp = swaped ? !isRoundUp : isRoundUp;
+        bool _isRoundUp = swapped ? !isRoundUp : isRoundUp;
        uint256 numerator = liquidityAmount;

        if (_isRoundUp) {
            uint256 r0 = FullMath.mulDivRoundingUp(numerator, FixedPoint96.Q96, sqrtRatioA);
            uint256 r1 = FullMath.mulDiv(numerator, FixedPoint96.Q96, sqrtRatioB);

            r = SafeCast.toInt256(r0) - SafeCast.toInt256(r1);
        } else {
            uint256 r0 = FullMath.mulDiv(numerator, FixedPoint96.Q96, sqrtRatioA);
            uint256 r1 = FullMath.mulDivRoundingUp(numerator, FixedPoint96.Q96, sqrtRatioB);

            r = SafeCast.toInt256(r0) - SafeCast.toInt256(r1);
        }

-        if (swaped) {
+        if (swapped) {
            return -r;
        } else {
            return r;
        }
    }
```

## QA-15 `PredyPool#uniswapV3MintCallback()` is potentially vulnerable to some attacks

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L77-L91

```solidity

    function uniswapV3MintCallback(uint256 amount0, uint256 amount1, bytes calldata) external override {
        // Only the uniswap pool has access to this function.
        require(allowedUniswapPools[msg.sender]);

        IUniswapV3Pool uniswapPool = IUniswapV3Pool(msg.sender);

        if (amount0 > 0) {
            ERC20(uniswapPool.token0()).safeTransfer(msg.sender, amount0);
        }
        if (amount1 > 0) {
            ERC20(uniswapPool.token1()).safeTransfer(msg.sender, amount1);
        }
    }

```

Now the only verification that's applied to this address is the fact that it's been validated under this mapping:
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L38

```solidity
    mapping(address => bool) public allowedUniswapPools;
```

This makes the attempt at verifying insufficient and effectively leaves it potentially vulnerable to a collision attack.

More on this attack idea can be seen from these sources:

1. [EIP-3607](https://eips.ethereum.org/EIPS/eip-3607) whose rationale addresses this exact attack. The EIP is in its final state.
2. Past issues: [1](https://github.com/code-423n4/2024-04-panoptic-findings/issues?q=is%3Aissue+is%3Aopen+address+collision+during+pool+deployment+allows+for+complete+draining+of+the+pool), [2](https://github.com/sherlock-audit/2023-07-kyber-swap-judging/issues?q=is%3Aissue+is%3Aopen+Router.sol+is+vulnerable+to+address+collission) & [3](https://github.com/sherlock-audit/2023-12-arcadia-judging/issues/59)
3. A [blog post](https://mystenlabs.com/blog/ambush-attacks-on-160bit-objectids-addresses) discussing the cost (both in money and time) of this exact attack. Which all explain how a collision could occur with the addresses and then make the protocol assume that the caller is a valid pool, which in Predy's case would then lead to them stealing out all the tokens in the pool due to this part of the callback function

```solidity
        if (amount0 > 0) {
            ERC20(uniswapPool.token0()).safeTransfer(msg.sender, amount0);
        }
        if (amount1 > 0) {
            ERC20(uniswapPool.token1()).safeTransfer(msg.sender, amount1);
        }
```

> TLDR: Is that one could

### Impact

N/A

> Submitted as QA, due to time restrictions during the contest to really dive deeper within the bug window to see how much it could affect Predy if at all

### Recommended Mitigation Steps

Consider validating that the pool is really deployed.

## QA-16 `SupplyLogic#burnBondAndTransferToken()` could revert for some tokens in the future

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L79-L91

```solidity
    function burnBondAndTransferToken(Perp.AssetPoolStatus storage _pool, uint256 _amount)
        internal
        returns (uint256 finalburntAmount, uint256 finalWithdrawalAmount)
    {
        address supplyTokenAddress = _pool.supplyTokenAddress;

        (finalburntAmount, finalWithdrawalAmount) =
            _pool.tokenStatus.removeAsset(ERC20(supplyTokenAddress).balanceOf(msg.sender), _amount);

        ISupplyToken(supplyTokenAddress).burn(msg.sender, finalburntAmount);

        ERC20(_pool.token).safeTransfer(msg.sender, finalWithdrawalAmount);
    }
```

This function is used to burn the bond and then transfer the token, we can see that to do this it also needs to query the `balanceOf()` on the supply token's address, issue however is that this implementation would always revert for some tokens like Aura's stash tokens which do not implement the `balanceOf()` functionality.

### Impact

DOS to `SupplyLogic#burnBondAndTransferToken()`

### Recommended Mitigation Steps

Consider querying the balance of on a low level.

## QA-17 Some locks would be un-initializable due to direct `balanceOf()` call

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L35-L45

```solidity
    function initializeLock(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal {
        if (globalData.lockData.locker != address(0)) {
            revert IPredyPool.LockedBy(globalData.lockData.locker);
        }

        globalData.lockData.quoteReserve = ERC20(globalData.pairs[pairId].quotePool.token).balanceOf(address(this));
        globalData.lockData.baseReserve = ERC20(globalData.pairs[pairId].basePool.token).balanceOf(address(this));
        globalData.lockData.locker = msg.sender;
        globalData.lockData.pairId = pairId;
    }

```

This function is used to intialize a lock,problem however is that this function directly queries the `balanceOf()` function whic would then cause the attempt to fail for tokens that don't quite support this

### Impact

Inability to initialize these locks.

### Recommended Mitigation Steps

Consider querying the `balanceOf()` on a low level instead.

## QA-18 Deployment of new supply tokens would fail for some tokens

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L192-L203

```solidity
    function deploySupplyToken(address _tokenAddress) internal returns (address) {
        IERC20Metadata erc20 = IERC20Metadata(_tokenAddress);

        return address(
            new SupplyToken(
                address(this),
                string.concat("Predy6-Supply-", erc20.name()),
                string.concat("p", erc20.symbol()),
                erc20.decimals()
            )
        );
    }
```

This function is used to deploy new supply tokens however it would always fail for some to be integrated tokens, considering not all ERC2o support the .name() or .symbol() function which would then essentially mean a permanent DOS to the creating these new supply tokens.

### Impact

Permanent DOS to the creating these new supply tokens.

### Recommended Mitigation Steps

Consider using a try/catch and a default fallback symbol/name when the token doesn't support it.

## QA-19 Solmate's `SafeTransferLib` shouldn't be used as it doesn't check for account existence

### Proof of Concept

Protocol heavily uses Solmate's `SafeTransferLib` accross in-scope contracts, this can easily be confirmed by using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-05-predy+import+%7BSafeTransferLib%7D+from+%22%40solmate%2Fsrc%2Futils%2FSafeTransferLib.sol%22%3B+language%3A%22Gerber+Image%22&type=code&l=Gerber+Image](https://github.com/search?q=repo%3Acode-423n4%2F2024-05-predy+import+%7BSafeTransferLib%7D+from+%22%40solmate%2Fsrc%2Futils%2FSafeTransferLib.sol%22%3B+language%3A%22Gerber+Image%22&type=code&l=Gerber+Image).

Now, there is a subtle difference between the implementation of solady (solmate’s) SafeTransferLib and OZ’s SafeERC20: OZ’s SafeERC20 checks if the token is a contract or not, solady’s SafeTransferLib does not. (it's based on solmate safetransferlib)
See: https://github.com/Vectorized/solady/blob/main/src/utils/SafeTransferLib.sol#L10
Note that none of the functions in this library check that a token has code at all! That responsibility is delegated to the caller.
As a result, when the token’s address has no code, the transaction will just succeed with no error.
This attack vector was made well-known by the [qBridge hack back in Jan 2022](https://www.halborn.com/blog/post/explained-the-qubit-hack-january-2022).

It’s becoming popular for protocols to deploy their token across multiple networks and when they do so, a common practice is to deploy the token contract from the same deployer address and with the same nonce so that the token address can be the same for all the networks.

A sophisticated attacker can exploit it by taking advantage of that and setting traps on multiple potential tokens to create fake deposits. For example: 1INCH is using the same token address for both Ethereum and BSC; Gelato's $GEL token is using the same token address for Ethereum, Fantom and Polygon. Also, attacker can frontrun one new token deployment and create fake deposits before it hit the chain, so this attack vector can be exploited via deposits.

### Impact

QA, considering there is a list of whitelisted tokens, however this should be considered if more tokens are ever going to be integrated.

### Recommended Mitigation Steps

Verify if the token has code before integrating.

## QA-20 Setters don't have equality checkers

### Proof of Concept

Multiple instances across in-scope contracts, for example take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L91-L103

```solidity

    /**
     * @notice Sets new operator
     * @dev Only operator can call this function.
     * @param newOperator The address of new operator
     */
    function setOperator(address newOperator) external onlyOperator {
        require(newOperator != address(0));
        operator = newOperator;

        emit OperatorUpdated(newOperator);
    }

```

Now see https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L286-L292

```solidity
    function updateRecepient(uint256 vaultId, address recipient) external onlyVaultOwner(vaultId) {
        DataType.Vault storage vault = globalData.vaults[vaultId];

        vault.recipient = recipient;

        emit RecepientUpdated(vaultId, recipient);
    }
```

### Impact

Bad code, unnecessary execution.

### Recommended Mitigation Steps

Consider checking if the value to be stored is the already stored value and if yes skip re-storing it

## QA-21 Oracle price updates could be front run to game the system

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L44-L58

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

This function returns the square root of the baseToken price quoted in quoteToken, and this price data ends up being used in core areas accross protocol, issue explained in this report is the fact that the price used is gotten from Chainlink however there are no protections on popular bug cases like an attacker frontrunning the price update from Chainlink to gain the most from the system, more on how this bug can be of an effect to the protocol can be seen from:

- Past finding: https://github.com/code-423n4/2024-04-dyad-findings/issues/1205
- A blog on how this works: https://medium.com/cyfrin/chainlink-oracle-defi-attacks-93b6cb6541bf#f123

### Impact

Seems to be QA at most, considering deployment is being done on optimistic L2s.

### Recommended Mitigation Steps

Consider applying fees to logics that directly use the price returned from here, this way we can always ensure minimal arbitrage is done away with since the profits might be engulfed by the fees.

## QA-22 Make `PredyPool#withdrawCreatorRevenue()` more effective

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L199-L213

```solidity
    function withdrawCreatorRevenue(uint256 pairId, bool isQuoteToken) external onlyPoolOwner(pairId) {
        Perp.AssetPoolStatus storage pool = _getAssetStatusPool(pairId, isQuoteToken);

        uint256 amount = pool.accumulatedCreatorRevenue;

        require(amount > 0, "AZ");

        pool.accumulatedCreatorRevenue = 0;

        if (amount > 0) {
            ERC20(pool.token).safeTransfer(msg.sender, amount);
        }

        emit CreatorRevenueWithdrawn(pairId, isQuoteToken, amount);
    }
```

This function is used to withdraw the accumulated creator revenue.
and only the pool owner is expected to have access to this function problem however is that this function erroneously checks that amount is > 0 twice.

### Impact

Bade code writing, hints potential error in code

### Recommended Mitigation Steps

Change to considering the first requirement already ensured the amount != 0

```diff
    function withdrawCreatorRevenue(uint256 pairId, bool isQuoteToken) external onlyPoolOwner(pairId) {
        Perp.AssetPoolStatus storage pool = _getAssetStatusPool(pairId, isQuoteToken);

        uint256 amount = pool.accumulatedCreatorRevenue;

        require(amount > 0, "AZ");

        pool.accumulatedCreatorRevenue = 0;

-        if (amount > 0) {
            ERC20(pool.token).safeTransfer(msg.sender, amount);
-        }

        emit CreatorRevenueWithdrawn(pairId, isQuoteToken, amount);
    }
```

## QA-23 `UniswapSettlement#swapExactIn()` should be made safer

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L22-L37

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

        amountOut = _swapRouter.exactInput(
            ISwapRouter.ExactInputParams(data, recipient, block.timestamp, amountIn, amountOutMinimum)
        );
    }

```

Multiple issues with how the approval is being done here:

1. It doesn't check the return value to ensure the approval was successful.
2. Protocol uses native `  ERC20.approve()` function whose definition has a boolean return value: `   function approve(address spender, uint256 amount) public virtual returns (bool)`, this then means that in the case where this is an interface and the integrated token for example is `USDT`, whose approval definition doesn't have this bool return value i.e `    function approve(address spender, uint256 amount) public virtual {` then attempting to approve on `USDT` would always fail considering the compiler would revert when it's expecting a return value and doesn't receive one.

### Impact

Bad integration, potential incompatibility with tokens, causing a DOS to swaps.

### Recommended Mitigation Steps

Consider using the safer option of `approve()`

## QA-24 `PriceFeed#getSqrtPrice()` query to `latestRoundData()` is done in a wrong way since there is no check first to see if the sequencer is down

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

```solidity
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData(); //@audit
        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
```

This function returns the square root of the baseToken price quoted in quoteToken, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`.

Problem however is that unlike the way Pyth is being queried which includes a `VALID_TIME_PERIOD` to act as a stale check for Pyth's `getPriceNoOlderThan()`, in the case of Chainlink the protocol just ingests whatever price is returned from the feed even though it might be stale/not safe.

One thing with using Chainlink on L2 chains is that there is a need to check if the sequencer is down to avoid prices from looking like they are fresh although they are not. The bug could then be leveraged by malicious actors to take advantage of the sequencer downtime.

### Impact

Core functionalities across protocol would be somewhat broken on L2 chains where the networks could be down for a while.

As this in it's sense is like a `pausing` functionality on the chain and any action that's time-restricted has a potential of been flawly finalized, popular bug ideas include users not being able say add collateral if they had borrowed a position making them immediately liquidatable when the sequencer comes back on, etc. but this could be coined to fit into any time-restricted logic.

If the sequencer goes down, the protocol will allow users to continue to operate at the previous (stale) prices.

### Recommended Mitigation Steps

Consider reimplementing the timing logics on the L2 side of the protocol to take the fact that the sequencer could indeed be down into account.

Additionally, since Chainlink recommends that all Optimistic L2 oracles consult the Sequencer Uptime Feed to ensure that the sequencer is live before trusting the data returned by the oracle introduce a seqeuncer check to ensure that the sequencer is active and prices returned are accurate.

## QA-25 `PriceFeed#getSqrtPrice()` might be broken in the future due to it's integration with Pyth's `expo` value

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

```solidity
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();
    //@audit
        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
```

This function returns the square root of the baseToken price quoted in quoteToken, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`... extensively it also is used for all other pricing logics, nw it includes an expo, check with has the value of the expo be `== - 8`.

However, going to the implementation of Pyth natively, i.e theP yth Client, we can see that the actual exp value can indeed be negative and positive:

- [add_price.rs#L44](https://github.com/pyth-network/pyth-client/blob/main/program/rust/src/processor/add_price.rs#L44): When you add a price, it checks the exponent.
  • [utils.rs#L101-L106](https://github.com/pyth-network/pyth-client/blob/main/program/rust/src/utils.rs#L101-L106): It can be between +-MAX_NUM_DECIMALS
  • [c_oracle_header.rs#L14](https://github.com/pyth-network/pyth-client/blob/main/program/rust/src/c_oracle_header.rs#L14): The MAX_NUM_DECIMALS has a value of 12 so theoretically it can be +-12.

Furthermore, based on a Spearbit discussion with the Pyth team on a previous audit, _(see 5.2.2 from [this report](https://github.com/euler-xyz/euler-price-oracle/blob/c4074ab7a7aa0c6ffbc555391d9f0bfe1ee5fd6f/audits/Euler_Price_Oracle_Spearbit_Report_DRAFT.pdf))_ the Pyth team have confirmed that currently they have set [the `expo` must be -ve check in the SDK](https://github.com/pyth-network/pyth-crosschain/blob/a888ba318c0325c29070eaf5afcc3a4d443b058c/target_chains/ethereum/sdk/solidity/PythUtils.sol#L18) to facilitate the discussions but they do not exclude the fact that this value can be positive in the future.

### Impact

QA, considering this affects future code, however this means that valid prices would not be ingested.

### Recommendation

Consider supporting positive `8` exp value also for a more generalized integration of the PythOracle.

## QA-26 Protocol uses two diferent price source when querying prices which is riskier than using one sure source or having the second confirmed source as a fallback

### Proof of Concept

Take a look at `PriceFeed#getSqrtPrice()` here https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

```solidity
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();  //@audit
        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
```

This function returns the square root of the baseToken price quoted in quoteToken, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`, problem however is that the current logic is unsafe, considering a failure from one of the supported oracle sources, causes the whole attempt to revert.

Understandably, one can assume protocol is implementing two sources to ensure an attacker manipulating one source would nnot easily manipulate the other, but this leaves the execution vulnerable to the bug case where if one of the sources fail, the whole attempt fails.

### Impact

Protocol seems to wrongly integrate multiple oracles, cause currently if one of the oracles bubblle up an error the whole attempt at pricing the tokens fail, where as generally adopted logic would be to query one source and if it fails, query the other, which ensures the failure would occur 50% less than what's been implemented now.

### Recommended Mitigation Steps

Consider correctly integrating multiple oracles atempt to query both prices from one source, if it fails then query the other source for both prices, or leave this implementation but have it in a try/catch and if any attempt fails, then query another source.
