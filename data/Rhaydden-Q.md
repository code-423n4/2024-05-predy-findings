# QA for Predy

## Table of Contents

| Issue ID | Description |
| -------- | ----------- |
| [QA-01](#qa-01-dutch-orders-without-duration-benefit-the-filler-in-decaylibsol) | Dutch Orders Without Duration Benefit the Filler in `DecayLib.sol` |
| [QA-02](#qa-02-inaccurate-price-calculation-during-stablecoin-depeg-events) | Inaccurate Price Calculation During Stablecoin Depeg Events |
| [QA-03](#qa-03-solmates-erc20-does-not-check-for-token-contracts-existence-opening-up-the-possibility-for-a-honeypot-attack) | Solmate's ERC20 does not check for token contract's existence, opening up the possibility for a honeypot attack |
| [QA-04](#qa-04-inconsistent-protocol-behavior-due-to-partial-token-implementations-across-target-chains) | Inconsistent Protocol Behavior Due to Partial Token Implementations Across Target Chains |
| [QA-05](#qa-05-predy-is-to-be-deployed-on-some-optimistic-l2-chains-but-in-no-instance-do-they-consider-the-sequencer-going-down) | Predy is to be deployed on some optimistic L2 chains but in no instance do they consider the sequencer going down |
| [QA-06](#qa-06-incorrect-sign-handling-in-swapforoutofrange-function-may-lead-to-incorrect-position-adjustments) | Incorrect Sign Handling in `swapForOutOfRange` Function May Lead to Incorrect Position Adjustments |
| [QA-07](#qa-07-unrestricted-token-transfer-by-locker-contract-in-take-function) | Unrestricted Token Transfer by Locker Contract in `take` Function |
| [QA-08](#qa-08-incorrect-boolean-assignments-in-decodeperporderv3params-can-lead-to-wrong-order-parameters) | Incorrect boolean assignments in `decodePerpOrderV3Params` can lead to wrong order parameters |
| [QA-09](#qa-09-potential-manipulation-in-autohedge-and-autoclose-mechanisms-in-gammatrademarketsol) | Potential Manipulation in `autoHedge` and `autoClose` Mechanisms in `GammaTradeMarket.sol` |
| [QA-10](#qa-10-not-calling-approve0-before-setting-a-new-approval-causes-the-call-to-revert-when-used-with-tether-usdt) | Not calling `approve(0)` before setting a new approval causes the call to revert when used with Tether (USDT) |
| [QA-11](#qa-11-negative-margin-handling-leads-to-potential-underflow-vulnerability-in-liquidation-logic) | Negative Margin Handling Leads to Potential Underflow Vulnerability in Liquidation Logic |
| [QA-12](#qa-12-incorrect-use-of-memory-instead-of-storage-reference) | Incorrect Use of Memory Instead of Storage Reference |
| [QA-13](#qa-13-lack-of-vault-existence-check) | Lack of Vault Existence Check |
| [QA-14](#qa-14-possibility-of-division-by-zero) | Possibility of Division by Zero |
| [QA-15](#qa-15-incorrect-handling-of-zero-vaultid-in-_executeorderv3-leading-to-accessing-non-existent-vault) | Incorrect Handling of Zero `vaultId` in `_executeOrderV3` Leading to Accessing Non-existent Vault |
| [QA-16](#qa-16-incorrect-update-of-lastrebalancetotalsquartamount-in-settlerebalanceinterest-function-leading-to-inaccurate-tracking-of-rebalance-amounts) | Incorrect Update of `lastRebalanceTotalSquartAmount` in `settleRebalanceInterest` Function Leading to Inaccurate Tracking of Rebalance Amounts |
| [QA-17](#qa-17-incorrect-price-comparison-logic-in-checkprice-function-leading-to-potentially-flawed-trade-validations) | Incorrect Price Comparison Logic in `checkPrice` Function Leading to Potentially Flawed Trade Validations |
| [QA-18](#qa-18-incorrect-timestamp-comparison-prevents-interest-application) | Incorrect Timestamp Comparison Prevents Interest Application |
| [QA-19](#qa-19-incorrect-validation-logic-in-validatevaultid-and-validate-functions-leading-to-potential-misidentification-of-invalid-ids) | Incorrect Validation Logic in `validateVaultId` and `validate` Functions Leading to Potential Misidentification of Invalid IDs |
| [QA-20](#qa-20-potential-out-of-bounds-error-in-getitemindex-function-when-item-is-not-found) | Potential Out-of-Bounds Error in `getItemIndex` Function When Item is Not Found |
| [QA-21](#qa-21-potential-misbehavior-due-to-lack-of-validation-for-price-range-in-decay-function) | Potential Misbehavior Due to Lack of Validation for Price Range in Decay Function |
| [QA-22](#qa-22-unnecessary-existence-check-in-getvault-function-can-cause-issues) | Unnecessary existence check in `getVault` function can cause issues |
| [QA-23](#qa-23-incorrect-distribution-of-rebalance-position-to-the-last-user-potentially-leading-to-unfair-allocation-of-funds) | Incorrect distribution of rebalance position to the last user, potentially leading to unfair allocation of funds |
| [QA-24](#qa-24-pricefeed-contract-vulnerable-to-arbitrage) | PriceFeed contract vulnerable to arbitrage |
| [QA-25](#qa-25-possible-re-org-attack-in-pricefeedsol) | Possible Re-org attack in PriceFeed.sol |
| [QA-26](#qa-26-calluniswapobserve-will-show-incorrect-price-for-negative-ticks-because-it-does-not-round-up-for-them) | `callUniswapObserve` will show incorrect price for negative ticks because it does not round up for them |
| [QA-27](#qa-27-missing-deadline-parameter-in-swapexactin-and-swapexactout-functions-in-uniswapsettlementsol-allowing-outdated-slippage-and-allowing-pending-transactions-to-be-executed-unexpectedly) | Missing deadline parameter in `swapExactIn` and `swapExactOut` functions in `UniswapSettlement.sol` allowing outdated slippage and allowing pending transactions to be executed unexpectedly. |
| [QA-28](#qa-28-incorrect-accounting-of-total-and-borrowed-amounts-in-updatesqrtposition-function-leading-to-potential-fund-loss) | Incorrect accounting of total and borrowed amounts in `updateSqrtPosition` function leading to potential fund loss |
| [QA-29](#qa-29-make-the-error-messages-more-descriptive-to-avoid-confusion) | Make the error messages more descriptive to avoid confusion |
| [QA-30](#qa-30-fix-typos) | Fix typos |





## [QA-01] Dutch Orders Without Duration Benefit the Filler in `DecayLib.sol`

### Impact
The Dutch order implements a linear decay function. From `decayStartTime` to `decayEndTime` the amount of input or output tokens goes from `startPrice` (best rate for swapper) to `endPrice` (worst rate the swapper agrees with).

In the current implementation of the `decay` function in `DecayLib.sol`, it is possible to provide the same value for `decayStartTime` and `decayEndTime`. In this case, the Dutch order acts like a limit order, and the final price will be equal to the `endPrice`, which benefits the filler over the swapper.

### Proof of Concept

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/DecayLib.sol#L16-L39

```solidity
function decay(uint256 startPrice, uint256 endPrice, uint256 decayStartTime, uint256 decayEndTime)
    internal
    view
    returns (uint256 decayedPrice)
{
    if (decayEndTime < decayStartTime) {
        revert EndTimeBeforeStartTime();
    } else if (decayEndTime <= value) {
        decayedPrice = endPrice;
    } else if (decayStartTime >= value) {
        decayedPrice = startPrice;
    } else {
        uint256 elapsed = block.timestamp - decayStartTime;
        uint256 duration = decayEndTime - decayStartTime;

        if (endPrice < startPrice) {
            decayedPrice = startPrice - (startPrice - endPrice) * elapsed / duration;
        } else {
            decayedPrice = startPrice + (endPrice - startPrice) * elapsed / duration;
        }
    }
}
```

### Recommended Mitigation Steps
##### Option 1: Swap the `else-if` blocks to favor the swapper

```diff
function decay(uint256 startPrice, uint256 endPrice, uint256 decayStartTime, uint256 decayEndTime)
    internal
    view
    returns (uint256 decayedPrice)
{
    if (decayEndTime < decayStartTime) {
        revert EndTimeBeforeStartTime();
-    } else if (decayEndTime <= value) {
+    } else if (decayStartTime >= value) {
        decayedPrice = startPrice;
-    } else if (decayStartTime >= value) {
+    } else if (decayEndTime <= value) {
        decayedPrice = endPrice;
    } else {
        uint256 elapsed = block.timestamp - decayStartTime;
        uint256 duration = decayEndTime - decayStartTime;

        if (endPrice < startPrice) {
            decayedPrice = startPrice - (startPrice - endPrice) * elapsed / duration;
        } else {
            decayedPrice = startPrice + (endPrice - startPrice) * elapsed / duration;
        }
    }
}
```

##### Option 2: Restrict usage to ensure non-zero duration

```diff
function decay(uint256 startPrice, uint256 endPrice, uint256 decayStartTime, uint256 decayEndTime)
    internal
    view
    returns (uint256 decayedPrice)
{
-    if (decayEndTime < decayStartTime) {
+    if (decayEndTime <= decayStartTime) {
        revert EndTimeBeforeStartTime();
    } else if (decayEndTime <= value) {
        decayedPrice = endPrice;
    } else if (decayStartTime >= value) {
        decayedPrice = startPrice;
    } else {
        uint256 elapsed = block.timestamp - decayStartTime;
        uint256 duration = decayEndTime - decayStartTime;

        if (endPrice < startPrice) {
            decayedPrice = startPrice - (startPrice - endPrice) * elapsed / duration;
        } else {
            decayedPrice = startPrice + (endPrice - startPrice) * elapsed / duration;
        }
    }
}
```

These changes will ensure that the Dutch order behaves as expected and does not benefit the filler over the swapper when `decayStartTime` is equal to `decayEndTime`.




## [QA-02] Inaccurate Price Calculation During Stablecoin Depeg Events

### Impact

N/b: The Pyth oracle price only has feeds for ASSET/USD, but not ASSET/USDT or ASSET/USDC. [See here](https://pyth.network/price-feeds).
First of all, we note that Pyth [does have feeds](https://pyth.network/price-feeds) for ASSET/USD, but not ASSET/USDT or ASSET/USDC. That means that during a depegging event, assets will be wrongly priced.

If the quote token (e.g., USDT or USDC) experiences a significant depeg event, the `PriceFeed` contract may calculate an inaccurate price for the base token. This is because the contract relies on the `_quotePriceFeed` oracle, which may not accurately reflect the market price of the depegged stablecoin.

### Proof of Concept

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L59

1. The `PriceFeed` contract retrieves the price of the quote token from the `_quotePriceFeed` using the `latestRoundData()` function of the `AggregatorV3Interface`:
   ```solidity
   (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();
   ```
2. If the quote token (e.g., USDT or USDC) experiences a depeg event, and the `_quotePriceFeed` does not accurately reflect the market price of the depegged stablecoin, the `quoteAnswer` variable will not represent the true market value of the quote token.
3. The contract then calculates the `price` variable using the base token price obtained from the Pyth oracle and the `quoteAnswer`:
   ```solidity
   uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
   price = price * Constants.Q96 / _decimalsDiff;
   ```
4. The Pyth oracle provides the USD price of the base token, not the price in terms of the quote token (e.g., USDT or USDC). Therefore, if the quote token depegs significantly from USD, the calculated `price` will be inaccurate.
5. This inaccurate price calculation can lead to unfair token withdrawals and potential losses for liquidity providers, as the contract will not accurately reflect the true market value of the base token in terms of the depegged quote token.

### Recommended Mitigation Steps
Consider using a `<quote-token>/USD` oracle to convert the `<base-token>/USD` price obtained from the Pyth oracle to a `<base-token>/<quote-token>` price. This will ensure that the calculated price accurately reflects the market value of the base token in terms of the quote token, even during depeg events.






## [QA-03] Solmate's ERC20 does not check for token contract's existence, opening up the possibility for a honeypot attack

### Impact
The use of [Solmate's `SafeTransferLib`](https://github.com/transmissions11/solmate/blob/main/src/utils/SafeTransferLib.sol#L9)  in several contracts across the protocol does not check if the token contract exists. This can lead to a situation where a transfer succeeds silently without actually transferring any tokens if a non-existent token address is used. 

This error opens up room for a honeypot attack similar to the [Qubit Finance](https://www.halborn.com/blog/post/explained-the-qubit-hack-january-2022) hack of January 2022.

In particular, it has became popular for protocols to deploy their token across multiple networks using the same deploying address, so that they can control the address nonce and ensuring a consistent token address across different networks.

For example, 1INCH has the same token address on Ethereum and BSC, and GEL token has the same address on Ethereum, Fantom and Polygon. There are other protocols have same contract addresses across different chains, and it's not hard to imagine such thing for their protocol token too, if any.


### Proof of Concept

This is just one instance:
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/SettlementCallbackLib.sol#L105

Assuming that Alice is the attacker, Bob is the victim. Alice has two accounts, namely Alice1 and Alice2. Denote token Q as the quote token.

- Token Q has been launched on other chains, but not on the local chain yet. It is expected that token Q will be launched on the local chain with a consistent address as other chains.
- Alice1 places an auction with some baseToken, and a token Q as the quoteToken.
- Alice2 places a bid with 1000e18 quote tokens.
- The transfer succeeds, but the contract is not credited any tokens.
- Token Q is launched on the local chain.
- Bob places a bid with 1001e18 quote tokens.
- Alice2 cancels her own bid, recovering her (supposedly) 1000e18 refund bid back.
- Alice1 cancels her auction, recovering her base tokens back.
- As a result, the contract's Q token balance is 1e18, Alice gets away with all her base tokens and 1000e18 Q tokens that are Bob's. Alice has stolen Bob's funds.



### Recommended Mitigation Steps
Consider using OpenZeppelin's `SafeERC20` library instead, which includes checks to ensure that the token contract exists. 




## [QA-04] Inconsistent Protocol Behavior Due to Partial Token Implementations Across Target Chains


### Impact
While the probability of unsupported implementations emerging is low, the potential impact, such as asset losses, is significant.

### Proof of Concept
The README states that the protocol is expected to integrate with tokens such as WETH, USDC, ARB, USDT, DAI, and WBTC, and targets deployment on Arbitrum, Base, and Optimism chains. 

|Question|	Answer|
|-|-|	
|ERC20 used by the protocol|	WETH, USDC, ARB, USDT, DAI, WBTC|
|Chains the protocol will be deployed on|	Arbitrum,Base,Optimism|


However, USDT currently has no trusted implementation on the Base chain (https://basescan.org/tokens). This absence means that the protocol's integration with these tokens cannot be guaranteed.


### Recommended Mitigation Steps
Revise the list of supported tokens on the Base chains based on the current availability of trusted implementations.





## [QA-05] Predy is to be deployed on some optimistic L2 chains but in no instance do they consider the sequencer going down

### Proof of Concept
First note that protocol is to be deployed on multiple chains as outlined for this contest here: https://github.com/code-423n4/2024-05-predy#general-questions

```
### General questions

| Question                                | Answer                                                                     |
| --------------------------------------- | -------------------------------------------------------------------------- |
| Chains the protocol will be deployed on | Arbitrum,Base,Optimism |
```

This list includes multiple optimistic L2s, and with optimistic L2s like Arbitrum, Blast, Optimisim, the sequencer could infact go down, which then leads us to the issue with the timing logics across protocol.

This in short breaks multiple/any timing logics for the L2 to-deploy contracts, keep in mind that in instances where the L2 goes down, the time still counts.

Take a look at this: https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L44-L60

```solidity
  /// @notice This function returns the square root of the baseToken price quoted in quoteToken.
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
@>        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
}

```

We can see that this is the logic for getting the `getSqrtPrice` and it queries prices from Chainlink that's implemented in the protocol, note that a call to latestRoundData() is being made.

However, one thing with using Chainlink on L2 chains is that there is a need to check if the sequencer is down to avoid prices from looking like they are fresh although they are not. The bug could be leveraged by malicious actors to take advantage of the sequencer downtime.

### Impact
Core functionalities across protocol would be somewhat broken on L2 chains where the networks could be down for a while.

### Recommended Mitigation Steps
Consider reimplementing the timing logics on the L2 side of the protocol to take the fact that the sequencer could indeed be down into account.

Additionally, since Chainlink recommends that all Optimistic L2 oracles consult the Sequencer Uptime Feed to ensure that the sequencer is live before trusting the data returned by the oracle introduce a seqeuncer check to ensure that the sequencer is active and prices returned are accurate.




## [QA-06] Incorrect Sign Handling in `swapForOutOfRange` Function May Lead to Incorrect Position Adjustments

### Impact
The `swapForOutOfRange` function incorrectly handles the signs of `deltaPosition0` and `deltaPosition1` when assigning them to `deltaPositionBase` and `deltaPositionQuote`, potentially leading to incorrect adjustments in liquidity positions during swaps. This issue affects the accuracy of position updates when adding or removing liquidity, as the negation applied does not consider the operation's nature (addition or removal of liquidity), which could result in unintended position adjustments.

### Proof of Concept


https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Perp.sol#L321-L326

```solidity
if (pairStatus.isQuoteZero) {
    deltaPositionQuote = -deltaPosition0;
    deltaPositionBase = -deltaPosition1;
} else {
    deltaPositionBase = -deltaPosition0;
    deltaPositionQuote = -deltaPosition1;
}
```

As seen above, it shows that `deltaPositionBase` and `deltaPositionQuote` are assigned the negated values of `deltaPosition0` and `deltaPosition1`, regardless of whether the operation is adding or removing liquidity. This approach assumes a specific directionality based on the `isQuoteZero` flag, which indicates whether the quote token is token0 or token1 in the pair. However, the sign of `deltaPosition0` and `deltaPosition1` should inherently reflect the direction of the operation (adding or removing liquidity) as calculated by `calculateAmount0ForLiquidity` and `calculateAmount1ForLiquidity` functions from the `LPMath` library. These calculations are based on the current and target ticks, the total liquidity amount, and a boolean indicating if the operation increases (`true`) or decreases (`false`) liquidity. The subsequent negation of these values when assigning to `deltaPositionBase` and `deltaPositionQuote` seems to assume a uniform behavior across all scenarios, which might not align with the actual intent of adjusting positions based on the operation's nature (addition vs. removal of liquidity).

### Recommended Mitigation Steps
Differentiate between adding and removing liquidity, ensuring that the signs accurately reflect the intended changes in positions. 




## [QA-07] Unrestricted Token Transfer by Locker Contract in `take` Function

### Impact
The `take` function allows the contract currently locking the funds (the "locker") to arbitrarily transfer tokens out of the PredyPool contract. This poses a significant risk as a malicious or buggy locker contract could drain all the tokens from the PredyPool. This unrestricted access to transfer tokens opens up a major attack vector on the PredyPool funds. The `take` function permissions and logic should be revisited to prevent potential fund loss.

### Proof of Concept
The `take` function in the PredyPool contract:

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L329-L331

```solidity
function take(bool isQuoteAsset, address to, uint256 amount) external onlyByLocker {
    globalData.take(isQuoteAsset, to, amount);
}
```

The `onlyByLocker` modifier:

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L52-L56

```solidity
modifier onlyByLocker() {
    address locker = globalData.lockData.locker;
    if (msg.sender != locker) revert LockedBy(locker);
    _;
}
```

The `take` function can be called by any contract that has locked the PredyPool funds via the `onlyByLocker` modifier. The `to` address and `amount` are not restricted, allowing the locker to transfer arbitrary amounts of tokens to any address.

### Recommended Mitigation Steps
Consider impose strict limits on the `amount` that can be transferred out in the `take` function, based on the actual trade/liquidation amounts. Allternative, it'd be smarter to consider a design where PredyPool transfers the required tokens to the settlement contract, instead of giving the settlement contract free reign to transfer tokens from PredyPool.










## [QA-08] Incorrect boolean assignments in `decodePerpOrderV3Params` can lead to wrong order parameters

### Impact
The `decodePerpOrderV3Params` function incorrectly assigns boolean values based on the decoded `uint8` values. This can result in incorrect order parameters being returned.

### Proof of Concept
Take a look at this part of the code:

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/L2Decoder.sol#L50-L73

```solidity
uint8 reduceOnlyUint;
uint8 closePositionUint;
uint8 sideUint;

assembly {
    // ...
    reduceOnlyUint := and(shr(136, args), 0xFF)
    closePositionUint := and(shr(144, args), 0xFF)
    sideUint := and(shr(152, args), 0xFF)
}

reduceOnly = reduceOnlyUint == 1;
closePosition = closePositionUint == 1;
side = sideUint == 1;
```

The decoded `uint8` values (`reduceOnlyUint`, `closePositionUint`, `sideUint`) can hold any value between `0` and `255`. Albeit, the current implementation assumes that these values will always be either 0 or 1.
However, since they are decoded as `uint8`, they can potentially hold any value between 0 and 255. If any of these values happen to be greater than 1, the corresponding boolean variables (`reduceOnly`, `closePosition`, `side`) will be incorrectly set to `false`, even though the intention might have been to set them to `true`.

### Recommended Mitigation Steps
Modify the code to explicitly check if the decoded values are non-zero instead of comparing them to 1:

```diff
- reduceOnly = reduceOnlyUint == 1;
- closePosition = closePositionUint == 1;
- side = sideUint == 1;
+ reduceOnly = reduceOnlyUint != 0;
+ closePosition = closePositionUint != 0;
+ side = sideUint != 0;
```

As seen, by changing the comparisons to `!= 0`, the boolean variables will be set to `true` if the corresponding decoded values are non-zero, and `false` if they are zero. This ensures that the boolean variables accurately reflect the intended values based on the decoded uint8 values.








## [QA-09] Potential Manipulation in `autoHedge` and `autoClose` Mechanisms in `GammaTradeMarket.sol`

### Impact
The discretionary power vested in the contract owner to trigger auto-hedge and auto-close operations without adequate safeguards poses a risk of manipulation. This could lead to suboptimal execution prices for users, potentially resulting in financial losses due to unfavorable hedging or premature position closures.

### Proof of Concept

In the `autoHedge` function, the contract owner can initiate hedging based on predefined conditions without ensuring the hedge is beneficial for the user. This lack of oversight could allow for front-running or timing manipulation, leading to hedging at prices detrimental to the user's position.

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L226-L272

```solidity
function autoHedge(uint256 positionId, SettlementParamsV3 memory settlementParams)
    external 
    returns (IPredyPool.TradeResult memory tradeResult)
{
    //...
    (bool hedgeRequired, uint256 slippageTorelance, GammaTradeMarketLib.CallbackType triggerType) =
        GammaTradeMarketLib.validateHedgeCondition(userPosition, sqrtPrice);

    if (hedgeRequired) {
        //... execute hedge trade...
    }
}
```


Similarly, the `autoClose` function enables the contract owner to close a user's position when specific price thresholds are reached. The absence of controls to prevent the execution at the least favorable price within these thresholds risks closing positions at the worst possible price for the user.

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L274-L313

```solidity
function autoClose(uint256 positionId, SettlementParamsV3 memory settlementParams)
    external
    returns (IPredyPool.TradeResult memory tradeResult) 
{
    //...
    (bool closeRequired, uint256 slippageTorelance, GammaTradeMarketLib.CallbackType triggerType) =
        GammaTradeMarketLib.validateCloseCondition(userPosition, sqrtPrice);
    
    if (closeRequired) {
        //... execute close trade...
    }
}
```

### Recommended Mitigation Steps
I could only think of a few:
- Implement maximum slippage limits for hedge and close operations to protect against theese unfavorable execution prices.
- Allow users to set permissible price ranges for auto-closure to avoid executing at the worst possible price.
- Automate the initiation of auto-hedge and auto-close operations based on transparent so as to reduce reliance on manual intervention.









## [QA-10] Not calling `approve(0)` before setting a new approval causes the call to revert when used with Tether (USDT)

### Impact
According to the [README](https://github.com/code-423n4/2024-05-predy#general-questions) which says that `USDT` is one of the tokens used by Predy
Now, tokens such as USDT do not implement the ERC20 standard properly and will revert if the current approval is not zero when a new approval is set. For example Tether (USDT)'s approve() function will revert if the current approval is not zero, to protect against front-running changes of approvals. This issue prevents these tokens from being used in the UniswapSettlement contract, which relies heavily on Uniswap. This limitation hampers the future growth and availability of the protocol.

### Proof of Concept

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L31

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L47

```solidity
ERC20(baseToken).approve(address(_swapRouter), amountIn);
```

```solidity
ERC20(quoteToken).approve(address(_swapRouter), amountInMaximum);
```

### Recommended Mitigation Steps
To address this issue, reset the approval to zero before setting a new approval value. This can be done using OpenZeppelin’s `SafeERC20` library, which provides a `safeApprove` function that handles this correctly









## [QA-11] Negative Margin Handling Leads to Potential Underflow Vulnerability in Liquidation Logic

### Impact
As seen below, the implementation of handling negative margins during the liquidation process in `LiquidationLogic.sol` can cause an underflow. Specifically, when the remaining margin is negative, the code attempts to transfer an incorrect amount of tokens from the liquidator to the contract, potentially causing the transaction to fail or leading to unintended consequences due to the wrapping behavior of unsigned integers in Solidity.

### Proof of Concept
Here is the part of the code: https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L101-L108

```solidity
if (remainingMargin < 0) {
    vault.margin = 0;

    // To prevent the liquidator from unfairly profiting through arbitrage trades in the AMM and passing losses onto the protocol,
    // any losses that cannot be covered by the vault must be compensated by the liquidator
    ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));
}
```

As seen, `uint256(-remainingMargin)` is used, which, due to the nature of two's complement representation, results in a very large number close to `2^256` when `-remainingMargin` is a negative integer. This could lead to an attempt to transfer more tokens than the liquidator owns, causing the transaction to fail or, in a malicious scenario, allowing a liquidator to exploit the system by manipulating the margin to trigger this condition and potentially bypassing intended checks.

### Recommended Mitigation Steps
Ensure that negative margins are handled correctly by avoiding direct casting of negative signed integers to unsigned integers. Implement a check for negative values and handle them appropriately, possibly by using the absolute value of the margin or redesigning the logic to prevent underflow.






## [QA-12] Incorrect Use of Memory Instead of Storage Reference

### Impact
Using a memory reference instead of a storage reference when attempting to modify state variables can lead to unintended behavior. Specifically, modifications to the `vault` variable within the `createOrGetVault` function do not persist beyond the scope of the function call, potentially causing inconsistencies in the smart contract's state.

### Proof of Concept
In the `createOrGetVault` function, when handling an existing `vaultId` (i.e., `vaultId!= 0`), the `vault` variable is declared as a memory type:

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L48

```solidity
DataType.Vault memory vault = globalData.vaults[vaultId];
```

This declaration means that any modifications to `vault` within this scope will not affect the actual storage state of the contract, leading to a mismatch between the expected and actual state of the vault.

### Recommended Mitigation Steps
So as to ensure that modifications to the `vault` variable are persisted in the contract's state, declare `vault` as a storage reference instead of a memory reference:

```diff
-    DataType.Vault memory vault = globalData.vaults[vaultId];
+ DataType.Vault storage vault = globalData.vaults[vaultId];
```









## [QA-13] Lack of Vault Existence Check

### Impact
Without checking if a vault exists before proceeding with operations, the contract may perform actions on non-existent vaults, leading to incorrect assumptions about the state of the contract.

### Proof of Concept
In the `createOrGetVault` function, there is no explicit check to verify that a vault exists when a non-zero `vaultId` is provided. Take a look:

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L30-L48

```solidity
 if (vaultId == 0) {
            uint256 finalVaultId = globalData.vaultCount;

            // Initialize a new vault
            DataType.Vault storage vault = globalData.vaults[finalVaultId];

            vault.id = finalVaultId;
            vault.owner = msg.sender;
            vault.recipient = msg.sender;
            vault.openPosition.pairId = pairId;
            vault.quoteToken = quoteToken;

            globalData.vaultCount++;

            emit VaultCreated(vault.id, vault.owner, quoteToken, pairId);

            return vault.id;
        } else {
            DataType.Vault memory vault = globalData.vaults[vaultId];
```

This omission can lead to operations being performed on uninitialized or non-existent vaults, resulting in errors or unexpected behavior.

### Recommended Mitigation Steps
Implement a check to ensure that a vault exists before performing operations on it. This can be done by verifying that the `owner` field of the vault is not the zero address, indicating that the vault has been initialized:

```solidity
if (vaultId!= 0 && globalData.vaults[vaultId].owner == address(0)) {
    revert IPredyPool.VaultDoesNotExist();
}
```









## [QA-14] Possibility of Division by Zero 

The `swap` function in Trade.sol has a division by zero vulnerability when `totalBaseAmount` is zero, which can lead to unexpected behavior or transaction reverts.

### Impact
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L76-L110

If `totalBaseAmount` is zero, the `swap` function calls `divToStable` with `amountBase` set to `int256(1e18)`. However, inside `divToStable`, division operations are performed using `amountBase` as the denominator. If `amountBase` is zero, it will result in a division by zero error, causing the transaction to revert.

### Proof of Concept
Relevant code snippets:

```solidity
// Trade.sol
function swap(
    GlobalDataLibrary.GlobalData storage globalData,
    uint256 pairId,
    SwapStableResult memory swapParams,
    bytes memory settlementData,
    uint256 sqrtPrice,
    uint256 vaultId
) internal returns (SwapStableResult memory) {
    // ...

    if (totalBaseAmount == 0) {
        int256 amountQuote = calculateStableAmount(sqrtPrice, 1e18).toInt256();

        return divToStable(swapParams, int256(1e18), amountQuote, 0);
    }

    // ...
}

function divToStable(
    SwapStableResult memory swapParams,
    int256 amountBase,
    int256 amountQuote,
    int256 totalAmountStable
) internal pure returns (SwapStableResult memory swapResult) {
    swapResult.amountPerp = amountQuote * swapParams.amountPerp / amountBase;
    swapResult.amountSqrtPerp = amountQuote * swapParams.amountSqrtPerp / amountBase;
    // ...
}
```

When `totalBaseAmount` is zero, the `swap` function calls `divToStable` with `amountBase` set to `int256(1e18)`. Inside `divToStable`, the division operations `amountQuote * swapParams.amountPerp / amountBase` and `amountQuote * swapParams.amountSqrtPerp / amountBase` will result in a division by zero error if `amountBase` is zero.

### Recommended Mitigation Steps
Add a check in the `divToStable` function to handle the case when `amountBase` is zero, either by returning a default value or reverting the transaction with an appropriate error message.











## [QA-15] Incorrect Handling of Zero `vaultId` in `_executeOrderV3` Leading to Accessing Non-existent Vault

### Impact
When executing an order using the `_executeOrderV3` function, if the user doesn't have an existing position (i.e., `userPosition.vaultId` is zero), it attempts to access a non-existent vault in the `_predyPool` to calculate the `tradeAmount`. This can revert the transaction if the `_predyPool.getVault` function doesn't handle the case of a non-existent vault gracefully.

### Proof of Concept
Look at this part of the contract: https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L172-L208

```solidity
UserPosition storage userPosition = userPositions[perpOrder.info.trader][perpOrder.pairId];

userPosition.lastLeverage = perpOrder.leverage;

int256 tradeAmount = PerpMarketLib.getFinalTradeAmount(
    _predyPool.getVault(userPosition.vaultId).openPosition.perp.amount,
    perpOrder.side,
    perpOrder.quantity,
    perpOrder.reduceOnly,
    perpOrder.closePosition
);

// ...

if (userPosition.vaultId == 0) {
    userPosition.vaultId = tradeResult.vaultId;

    _predyPool.updateRecepient(tradeResult.vaultId, perpOrder.info.trader);
}
```

When `userPosition.vaultId` is zero, indicating that the user doesn't have an existing position, the code assigns `tradeResult.vaultId` to `userPosition.vaultId` after the trade is executed. However, before executing the trade, it retrieves the `openPosition.perp.amount` using `_predyPool.getVault(userPosition.vaultId)` to calculate the `tradeAmount`. If `userPosition.vaultId` is 0 at this point, it means that it is trying to access a non-existent vault in the `_predyPool`.


### Recommended Mitigation Steps
Handle the case when `userPosition.vaultId` is zero before calculating the `tradeAmount`. 













## [QA-16] Incorrect Update of `lastRebalanceTotalSquartAmount` in `settleRebalanceInterest` Function Leading to Inaccurate Tracking of Rebalance Amounts

### Impact
The incorrect update of `lastRebalanceTotalSquartAmount` can cause an inaccurate tracking of the total rebalance amounts, which can lead to incorrect fee calculations and settlements.

### Proof of Concept
Look at this part of the code: https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PerpFee.sol#L136-L155

```solidity
function settleRebalanceInterest(
    uint256 pairId,
    Perp.SqrtPerpAssetStatus storage assetStatus,
    mapping(uint256 => DataType.RebalanceFeeGrowthCache) storage rebalanceFeeGrowthCache,
    Perp.UserStatus storage userStatus
) internal returns (int256 rebalanceInterestBase, int256 rebalanceInterestQuote) {
    if (userStatus.sqrtPerp.amount != 0 && userStatus.lastNumRebalance < assetStatus.numRebalance) {
        (rebalanceInterestBase, rebalanceInterestQuote) =
            computeRebalanceInterest(pairId, assetStatus, rebalanceFeeGrowthCache, userStatus);

        uint256 rebalanceAmount = Math.abs(userStatus.sqrtPerp.amount);

        assetStatus.lastRebalanceTotalSquartAmount -= rebalanceAmount;
    }

    // if the user has no position, initialize lastNumRebalance to the current numRebalance
    userStatus.lastNumRebalance = assetStatus.numRebalance;
}
```

As seen above, the function `settleRebalanceInterest` updates `assetStatus.lastRebalanceTotalSquartAmount` by subtracting `rebalanceAmount`. However, it does not add the `rebalanceAmount` back if the user has a new position. This could lead to an incorrect total amount being tracked.

 The `userStatus.lastNumRebalance` is updated to `assetStatus.numRebalance` regardless of whether the user has a position or not. This could skip some rebalances if the user opens a new position after settling.

### Recommended Mitigation Steps
Ensure that `lastRebalanceTotalSquartAmount` is correctly updated for both adding and subtracting `rebalanceAmount`. Only update `userStatus.lastNumRebalance` if the user has no position.












## [QA-17] Incorrect Price Comparison Logic in `checkPrice` Function Leading to Potentially Flawed Trade Validations

### Impact
The current logic for comparing `tradeResult.averagePrice` assumes that `averagePrice` can be negative, which is incorrect. This can lead to flawed conditions in the `checkPrice` function, potentially causing valid trades to be rejected or invalid trades to be accepted.

### Proof of Concept

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/SlippageLib.sol#L38

```solidity
if (tradeResult.averagePrice > 0) {
    // short
    if (basePrice.lower(slippageTolerance) > uint256(tradeResult.averagePrice)) {
        revert SlippageTooLarge();
    }
} else if (tradeResult.averagePrice < 0) {
    // long
    if (basePrice.upper(slippageTolerance) < uint256(-tradeResult.averagePrice)) {
        revert SlippageTooLarge();
    }
}
```
The issue is that:
1. **Negative Prices**: The condition `tradeResult.averagePrice < 0` is invalid because prices should always be non-negative.
2. **Incorrect Logic for Long and Short**: The logic for determining "short" and "long" positions based on the sign of `averagePrice` is flawed. The sign should not be used to determine the type of trade.

### Recommended Mitigation Steps
Ensure `averagePrice` is always non-negative and use an explicit flag or a more effective method to determine if the position is long or short.









## [QA-18] Incorrect Timestamp Comparison Prevents Interest Application

### Impact
The current logic prevents the application of interest if the `lastUpdateTimestamp` is exactly equal to the current block timestamp. This can lead to situations where interest is not applied when it should be, potentially resulting in financial discrepancies and loss of expected interest revenue.

### Proof of Concept
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ApplyInterestLib.sol#L31-L34

```solidity
    // avoid applying interest rate multiple times in the same block
    if (pairStatus.lastUpdateTimestamp >= block.timestamp) {
        return;
    }
```

The condition `if (pairStatus.lastUpdateTimestamp >= block.timestamp)` is intended to prevent applying interest multiple times within the same block. However, using `>=` means that if `pairStatus.lastUpdateTimestamp` is exactly equal to `block.timestamp`, the function will return early and not apply the interest. This can lead to a scenario where interest is not applied when it should be, causing a loss of expected interest revenue.

### Recommended Mitigation Steps
Change the condition to use `>` instead of `>=` to ensure that interest is applied correctly.

### Diff Format Recommendation
```diff
    // avoid applying interest rate multiple times in the same block
-    if (pairStatus.lastUpdateTimestamp >= block.timestamp) {
+    if (pairStatus.lastUpdateTimestamp > block.timestamp) {
        return;
    }
```



## [QA-19] Incorrect Validation Logic in `validateVaultId` and `validate` Functions Leading to Potential Misidentification of Invalid IDs

## Impact
The current logic in the `validateVaultId` and `validate` functions incorrectly checks if `vaultId` and `pairId` are less than or equal to 0, which is not possible for unsigned integers. This could lead to improper validation and potential misidentification of invalid IDs. Additionally, the error message in `validateVaultId` uses `InvalidPairId` instead of the more appropriate `InvalidVaultId`, which can cause confusion.

## Proof of Concept

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L25-L32

The current implementation of the `validateVaultId` function:
```solidity
function validateVaultId(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId) internal view {
    if (vaultId <= 0 || globalData.vaultCount <= vaultId) revert IPredyPool.InvalidPairId();
}
```

The current implementation of the `validate` function:
```solidity
function validate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal view {
    if (pairId <= 0 || globalData.pairsCount <= pairId) revert IPredyPool.InvalidPairId();
}
```

## Recommended Mitigation Steps
1. Change the condition `vaultId <= 0` to `vaultId == 0` in the `validateVaultId` function since `vaultId` is an unsigned integer and cannot be less than 0.
2. Update the error message in the `validateVaultId` function to `InvalidVaultId` to accurately reflect the context of the validation.
3. Change the condition `pairId <= 0` to `pairId == 0` in the `validate` function since `pairId` is an unsigned integer and cannot be less than 0.

Also `InvalidVaultId` error message should be defined in the `IPredyPool` interface.





## [QA-20] Potential Out-of-Bounds Error in `getItemIndex` Function When Item is Not Found

### Impact
Returning `type(uint256).max` as an index when the item is not found can lead to out-of-bounds errors if not properly checked by the calling code. This can cause runtime errors in the contract.

### Proof of Concept
The `getItemIndex` function returns `type(uint256).max` if the item is not found in the array:

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/ArrayLib.sol#L9-L33

```solidity
function getItemIndex(uint256[] memory items, uint256 item) internal pure returns (uint256) {
    uint256 index = type(uint256).max;

    for (uint256 i = 0; i < items.length; i++) {
        if (items[i] == item) {
            index = i;
            break;
        }
    }

    return index;
}
```

If the calling code does not properly handle this case, it can lead to out-of-bounds errors. For example:

```solidity
function removeItem(uint256[] storage items, uint256 item) internal {
    uint256 index = getItemIndex(items, item);

    removeItemByIndex(items, index); // Potential out-of-bounds error if item is not found
}
```

### Recommended Mitigation Steps
Consider modifying the `getItemIndex` function to return a boolean indicating whether the item was found, along with the index. Update the calling code to handle the case where the item is not found.






## [QA-21] Potential Misbehavior Due to Lack of Validation for Price Range in Decay Function

### Impact
The `decay2` function does not validate that the `startPrice` is greater than or equal to the `endPrice`. This could cause unexpected behavior if the function is called with invalid price parameters, causing incorrect price calculations in the context of a Dutch auction.

### Proof of Concept

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/DecayLib.sol#L16-L38

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

### Recommended Mitigation Steps
Add a validation check at the beginning of the `decay2` function to ensure that `startPrice` is greater than or equal to `endPrice`. This will prevent the function from executing with invalid inputs.






## [QA-22] Unnecessary existence check in `getVault` function can cause issues
### Impact
The `getVault` function does not properly check if a vault exists before verifying ownership. This can lead to issues where non-existent vaults are treated as valid.

### Proof of Concept
Look at this part of the code: https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L48-L53

```solidity
function getVault(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId)
    internal
    view
    returns (DataType.Vault storage vault)
{
    vault = globalData.vaults[vaultId];

    // Ensure the caller is the owner of the existing vault
    if (vault.owner != msg.sender) {
        revert IPredyPool.CallerIsNotVaultOwner();
    }
}
```
- The function retrieves the vault from storage without checking if the `vaultId` is valid.
- If the `vaultId` does not exist, `globalData.vaults[vaultId]` will return a vault with default values (e.g., `owner` is `0`).
- The ownership check will pass for non-existent vaults, leading to potential misuse or security issues.

### Recommended Mitigation Steps
Add a check to ensure the vault exists before verifying ownership.
```diff
function getVault(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId)
    internal
    view
    returns (DataType.Vault storage vault)
{
+    if (vaultId >= globalData.vaultCount) {
+        revert IPredyPool.VaultDoesNotExist();
+    }

    vault = globalData.vaults[vaultId];

    // Ensure the caller is the owner of the existing vault
    if (vault.owner != msg.sender) {
        revert IPredyPool.CallerIsNotVaultOwner();
    }
}
```

This will ensure that the function first checks if the `vaultId` is valid and exists before proceeding with the ownership verification.










## [QA-23] Incorrect distribution of rebalance position to the last user, potentially leading to unfair allocation of funds

### Impact
The last user who settles the rebalance position when `_assetStatus.lastRebalanceTotalSquartAmount` is zero will receive the entire rebalance position, while other users who have settled their rebalance positions earlier will not receive their fair share. This can result in an unfair distribution of funds and may lead to financial losses for users who settled earlier.

### Proof of Concept

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Perp.sol#L633-L639

```solidity
if (_assetStatus.lastRebalanceTotalSquartAmount == 0) {
    // last user who settles rebalance position
    _userStatus.rebalanceLastTickLower = _assetStatus.tickLower;
    _userStatus.rebalanceLastTickUpper = _assetStatus.tickUpper;

    return
        (_assetStatus.rebalancePositionBase.positionAmount, _assetStatus.rebalancePositionQuote.positionAmount);
}
```

When `_assetStatus.lastRebalanceTotalSquartAmount` is zero, the function returns the entire `rebalancePositionBase` and `rebalancePositionQuote` amounts to the last user who settles the rebalance position. This means that the last user will receive the entire rebalance position, while other users who have settled their rebalance positions earlier will not receive their share.

Scenario: Suppose there are three users (A, B, and C) who have settled their rebalance positions. User A settles first, followed by User B, and finally User C. If the total rebalance position is 100 tokens and `_assetStatus.lastRebalanceTotalSquartAmount` becomes zero when User C settles, User C will receive the entire 100 tokens, while User A and User B will not receive any tokens from the rebalance position. This is unfair and can lead to financial losses for User A and User B.

### Recommended Mitigation Steps
Distribute the rebalance position proportionally among all users who have settled their rebalance positions based on their share of the total amount.



## [QA-24] PriceFeed contract vulnerable to arbitrage 

### Impact
The PriceFeed contract calculates the square root price of a base token in terms of a quote token using prices from two different oracles. If there is a price discrepancy between the oracles, an attacker can exploit the contract by buying the base token at the lower price calculated by the PriceFeed contract and selling it immediately at the higher market price, profiting from the price difference. This can lead to a loss of funds for users relying on the PriceFeed contract for accurate pricing information.

### Proof of Concept
The PriceFeed contract calculates the price using the following code:

```solidity
uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
price = price * Constants.Q96 / _decimalsDiff;

sqrtPrice = FixedPointMathLib.sqrt(price);
```

Suppose the base token (Token A) has a price of $0.99 from the Pyth oracle, and the quote token (Token B) has a price of $1 from the quote price feed. The PriceFeed contract would calculate the price as follows:

```
price = 0.99 * Q96 / 1
price = price * Q96 / decimalsDiff
sqrtPrice = sqrt(price)
```

The calculated `sqrtPrice` would be lower than the actual market price. An attacker could exploit this by:

1. Buying Token A using the PriceFeed contract at the lower calculated price
2. Selling Token A immediately on the market at the higher price of $0.99
3. Profiting from the price difference

For example, if the attacker buys 1000 Token A using the PriceFeed contract, they would spend less than $990. However, they could sell the same 1000 Token A on the market for $990, making a profit at the expense of other users relying on the PriceFeed contract.

### Recommended Mitigation Steps
To mitigate this issue, the PriceFeed contract should:

1. Consider prices from both the base token oracle (Pyth) and the quote token oracle (quote price feed).
2. Use the lower bound price between the two oracles for calculations to ensure that the calculated price is always equal to or lower than the actual market price.
3. Implement separate oracles for lower-bound and upper-bound prices, allowing lending protocols to use the lower-bound price for determining collateral value.















## [QA-25]  Possible Re-org attack in PriceFeed.sol

### Impact
Allowing creation of new PriceFeeds by Re-org attack may adversely affect pricing in PriceFeed.sol contracts.

### Proof of Concept
The `PriceFeedFactory.sol#createPriceFeed()` function deploys a new `PriceFeed` using the `new` keyword, where the address derivation depends only on the arguments passed. This internally uses the `CREATE` opcode, which can be susceptible to reorg attacks. 

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L18-L25

```solidity
File: PriceFeedFactory.sol
         function createPriceFeed(address quotePrice, bytes32 priceId, uint256 decimalsDiff) external returns (address) {
@>    PriceFeed priceFeed = new PriceFeed(quotePrice, _pyth, priceId, decimalsDiff); 
        emit PriceFeedCreated(quotePrice, priceId, decimalsDiff, address(priceFeed));
        return address(priceFeed);
}
```

The `create` opcode is used when deploying new contracts using the new keyword. This opcode can be susceptible to reorg attacks because the address of the newly created contract is deterministic and depends only on the sender's address and nonce. In the case of optimistic rollups like Optimism and Arbitrum, reorgs can occur if a fraud proof is submitted, causing blocks to be reverted.

According to the [README](https://github.com/code-423n4/2024-05-predy#general-questions), the protocol is going to be deployed on Arbitrum, Optimism and Base.


Optimistic rollups like Optimism/Arbitrum are also suspect to reorgs since if someone finds a fraud the blocks will be reverted, even though the user receives a confirmation.

Similar issues were also reported in past audits. See links below:
- https://github.com/code-423n4/2024-03-abracadabra-money-findings/issues/211#issuecomment-2000142573

- https://github.com/code-423n4/2023-08-pooltogether-findings/issues/31


### Recommended Mitigation Steps
Try the deployment using `create2` with salt that includes real `msg.sender`.




## [QA-26]  `callUniswapObserve` will show incorrect price for negative ticks because it does not round up for them


### Impact
In case if `int24(tickCumulatives[i] - tickCumulatives[i+1])` is negative and `((tickCumulatives[i] - tickCumulatives[i+1]) % secondsAgo != 0`, then returned tick will be bigger than it should be which opens possibility for some price manipulations and arbitrage opportunities.
If `int24(tickCumulatives[1] - tickCumulatives[0])` is negative and `((tickCumulatives[1] - tickCumulatives[0]) % secondsAgo != 0`, then returned tick will be bigger than it should be which places Predy protocol wanting prices to be right not be able to achieve this goal.

### Proof of Concept
Take a look at: https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L35-L74

```solidity
function callUniswapObserve(IUniswapV3Pool uniswapPool, uint256 ago) internal view returns (uint160, uint256) {
        uint32[] memory secondsAgos = new uint32[](2);

        secondsAgos[0] = uint32(ago);
        secondsAgos[1] = 0;

        (bool success, bytes memory data) =
            address(uniswapPool).staticcall(abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos));

        if (!success) {
            if (keccak256(data) != keccak256(abi.encodeWithSignature("Error(string)", "OLD"))) {
                revertBytes(data);
            }

            (,, uint16 index, uint16 cardinality,,,) = uniswapPool.slot0();

            (uint32 oldestAvailableAge,,, bool initialized) = uniswapPool.observations((index + 1) % cardinality);

            if (!initialized) {
                (oldestAvailableAge,,,) = uniswapPool.observations(0);
            }

            ago = block.timestamp - oldestAvailableAge;
            secondsAgos[0] = uint32(ago);

            (success, data) = address(uniswapPool).staticcall(
                abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos)
            );
            if (!success) {
                revertBytes(data);
            }
        }

        int56[] memory tickCumulatives = abi.decode(data, (int56[]));

        int24 tick = int24((tickCumulatives[1] - tickCumulatives[0]) / int56(int256(ago)));

        uint160 sqrtPriceX96 = TickMath.getSqrtRatioAtTick(tick);

        return (sqrtPriceX96, ago);
```
This function is used to get twap price tick using uniswap. It gets `tickCumulatives` array which is then used to calculate `int24 tick`. 

The problem is that if `int24(tickCumulatives[1] - tickCumulatives[0])` is negative, then the tick should be rounded down as it's done in the[ uniswap library](https://github.com/Uniswap/v3-periphery/blob/main/contracts/libraries/OracleLibrary.sol#L36).

As result, in case if `int24(tickCumulatives[1] - tickCumulatives[0])` is negative and `(tickCumulatives[1] - tickCumulatives[0]) % secondsAgo != 0,` then returned tick will be bigger then it should be, which opens possibility for price manipulations and arbitrage opportunities.

### Recommeded Mitigation Steps
Add this line.
```solidity
if (tickCumulatives[1] - tickCumulatives[0] < 0 && (tickCumulatives[1] - tickCumulatives[0]) % secondsAgo != 0) timeWeightedTick --;
```

















## [QA-27]  Missing deadline parameter in `swapExactIn` and `swapExactOut` functions in `UniswapSettlement.sol` allowing outdated slippage and allowing pending transactions to be executed unexpectedly.

### Impact
Potential loss of funds/tokens for users due to transactions executing at unfavorable rates if delayed.
### Proof of Concept
AMMs provide their users with an option to limit the execution of their pending actions, such as swaps or adding and removing liquidity. The most common solution is to include a deadline timestamp as a parameter (for example see [UniswapV2](https://github.com/Uniswap/v2-periphery/blob/0335e8f7e1bd1e8d8329fd300aea2ef2f36dd19f/contracts/UniswapV2Router02.sol#L70C35-L70C35) and [Uniswap V3](https://github.com/Uniswap/v3-periphery/blob/6cce88e63e176af1ddb6cc56e029110289622317/contracts/SwapRouter.sol#L119). If such an option is not present, users can unknowingly perform bad trades.

For instance, imagine Alice wants to exchange 100 tokens for 1 WETH and later sell that 1 WETH for 1000 DAI. She submits the transaction to the mempool but sets a transaction fee too low to attract miners. As a result, her transaction remains pending in the mempool for an extended period, potentially lasting hours, days, weeks, or even longer.

Eventually, when the average gas fee decreases enough to make her transaction appealing to miners, it will be executed. However, during this waiting period, the price of WETH could have fluctuated significantly. Although Alice will still receive 1 WETH, the DAI value of that WETH might be substantially lower. Consequently, she ends up making a poor trade due to the forgotten pending transaction.

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/settlements/UniswapSettlement.sol#L22-L56

The functions `swapExactIn` and `swapExactOut` in `UniswapSettlement.sol` use the following methods to swap tokens:

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

    amountIn = _swapRouter.exactOutput(
        ISwapRouter.ExactOutputParams(data, recipient, block.timestamp, amountOut, amountInMaximum)
    );

    if (amountInMaximum > amountIn) {
        ERC20(quoteToken).safeTransfer(msg.sender, amountInMaximum - amountIn);
    }
}
```

Both functions ensure to pass slippage `amountInMaximum` and `amountOutMinimum` parameters but miss providing the deadline, which is crucial to avoid unexpected trades/losses for users and the protocol.

Without a deadline, the transaction might be left hanging in the mempool and be executed much later than the user intended. This could lead to users/protocol getting a worse price because a validator can hold onto the transaction and execute it at a later time.

Check here for further reference: https://blog.bytes032.xyz/p/why-you-should-stop-using-block-timestamp-as-deadline-in-swaps

### Recommended Mitigation Steps
Let users provide a fixed deadline as a parameter, and also never set the deadline to `block.timestamp`. 


























## [QA-28]  Incorrect accounting of total and borrowed amounts in `updateSqrtPosition` function leading to potential fund loss

### Impact
Incorrect accounting of total and borrowed amounts in the `updateSqrtPosition` function can lead to discrepancies in the contract's internal state. This could potentially allow users to withdraw more funds than they should be able to, resulting in fund loss for the contract owner or other users.

### Proof of Concept
Look at this part of the code from the `updateSqrtPosition` function (lines 552-558):

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Perp.sol#L551-L558

```solidity
if (closeAmount > 0) {
    _assetStatus.borrowedAmount -= uint256(closeAmount);
} else if (closeAmount < 0) {
    if (getAvailableSqrtAmount(_assetStatus, true) < uint256(-closeAmount)) {
        revert SqrtAssetCanNotCoverBorrow();
    }
    _assetStatus.totalAmount -= uint256(-closeAmount);
}
```

The problem lies in the fact that when `closeAmount` is negative (i.e., closing a borrowed position), the code subtracts the absolute value of `closeAmount` from `totalAmount`. However, it should subtract the absolute value of `closeAmount` from `borrowedAmount` instead.

Scenario:
1. User A opens a borrowed position with `borrowedAmount` of 100 tokens.
2. User B opens a regular position with `totalAmount` of 200 tokens.
3. User A closes their borrowed position, which should decrease `borrowedAmount` by 100 tokens.
4. However, due to the logic issue, `totalAmount` is decreased by 100 tokens instead of `borrowedAmount`.
5. Now, the contract's internal state incorrectly reflects a `totalAmount` of 100 tokens and a `borrowedAmount` of 100 tokens.
6. User B tries to close their position and withdraw their 200 tokens.
7. The contract allows the withdrawal because it thinks the `totalAmount` is sufficient to cover the withdrawal.
8. As a result, User B withdraws 200 tokens, while the contract only has 100 tokens in `totalAmount`, leading to a fund loss of 100 tokens.


### Recommended Mitigation Steps
```diff
 if (closeAmount > 0) {
-    _assetStatus.borrowedAmount -= uint256(closeAmount);
+    _assetStatus.totalAmount -= uint256(closeAmount);
 } else if (closeAmount < 0) {
     if (getAvailableSqrtAmount(_assetStatus, true) < uint256(-closeAmount)) {
         revert SqrtAssetCanNotCoverBorrow();
     }
-    _assetStatus.totalAmount -= uint256(-closeAmount);
+    _assetStatus.borrowedAmount -= uint256(-closeAmount);
 }
```

The mitigation steps involve updating the code to ensure that when closing a position:
- If `closeAmount` is positive (closing a long position), subtract `closeAmount` from `totalAmount`.
- If `closeAmount` is negative (closing a borrowed position), subtract the absolute value of `closeAmount` from `borrowedAmount`.



## [QA-29] Make the error messages more descriptive to avoid confusion

### Impact
The use of non-descriptive error messages throughout the `AddPairLogic` hinders the ability of developers and auditors and even users to quickly diagnose issues and comprehend. 

### Proof of Concept
Below are all instances of the confusing error messages found within the `AddPairLogic.sol` contract:

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L60-L227

1. **"AAA"**
   ```solidity
   require(_pairs[_pairId].id == 0, "AAA");
   ```
   Indicates an attempt to add a pair with an existing ID.

2. **"C4"**
   ```solidity
   require(_irmParams.baseRate <= 1e18 && _irmParams.kinkRate <= 1e18 && _irmParams.slope1 <= 1e18 && _irmParams.slope2 <= 10 * 1e18, "C4");
   ```
   Indicates invalid interest rate model parameters.

3. **"C0"** (First instance)
   ```solidity
   require(1e8 < _assetRiskParams.riskRatio && _assetRiskParams.riskRatio <= 10 * 1e8, "C0");
   ```
   Indicates invalid risk ratio parameter.

4. **"C0"** (Second instance)
   ```solidity
   require(_assetRiskParams.rangeSize > 0 && _assetRiskParams.rebalanceThreshold > 0, "C0");
   ```
   Indicates range size or rebalance threshold must be greater than 0.

5. **"ADDZ"**
   ```solidity
   require(_poolOwner!= address(0), "ADDZ");
   ```
   Indicates an invalid pool owner address.

6. **"FEE"**
   ```solidity
   require(_fee <= 20, "FEE");
   ```
   Indicates an invalid fee ratio.

7. **"C3"**
   ```solidity
   require(uniswapPool.token0() == stableTokenAddress || uniswapPool.token1() == stableTokenAddress, "C3");
   ```
   Ensures one of the tokens in the Uniswap pool matches the stable token address.

8. **"MAXP"**
   ```solidity
   require(pairId < Constants.MAX_PAIRS, "MAXP");
   ```
   Indicates that the maximum number of pairs has been reached.

### Recommended Mitigation Steps
Replace all non-descriptive error messages with clear, concise descriptions that accurately reflect the error condition to enhance contract readability and ease of debugging.


## [QA-30] Fix typos
`Recepient` should be corrected to `Recipient`

Here are the instances: 
- https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L286
- https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L291
- https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L43