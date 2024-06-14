## Missing `vaultId` validation in `LiquidationLogic.liquidate`

### Affected Lines

- [src/libraries/logic/LiquidationLogic.sol:39](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/logic/LiquidationLogic.sol#L39)

### Impact

When performing a liquidation through the `LiquidationLogic.liquidate` library function, the `valutID` parameter is not validated, allowing an invalid vault with `vaultID` of 0 to be referenced.

**`LiquidationLogic.liquidate`**:

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
        ...

```

Performing these calls with an invalid/zero `vaultID` leads to a revert in subsequent inner calls, leading to unnecessary gas usage and increasing the chances of unsafe calls being made on an invalid vault struct. This may carry additional risks given that data derived from the invalid vault struct is used to make an external call to `observe` via [UniHelper.callUniswapObserve](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/UniHelper.sol#L35).

### Proof of Concept

Add the following test case to [test/market/perp/ExecLiquidationCall.t.sol](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/test/market/perp/ExecLiquidationCall.t.sol)
<details>

```solidity
    function testLiquidateZeroVault() public {
        PerpOrderV3 memory order = PerpOrderV3(
            OrderInfo(address(perpMarket), from1, 0, block.timestamp + 100),
            1,
            address(currency1),
            "Sell",
            4 * 1e8,
            101000000,
            0,
            0,
            4,
            false,
            false,
            abi.encode(PerpMarketLib.AuctionParams(Constants.Q96 / 2, Constants.Q96 / 2, 0, 0))
        );

        IFillerMarket.SignedOrder memory signedOrder = _createSignedOrder(order, fromPrivateKey1);

        perpMarket.executeOrderV3(signedOrder, _getUniSettlementDataV3(0));

        _movePrice(true, 6 * 1e16);

        vm.warp(block.timestamp + 30 minutes);

        perpMarket.execLiquidationCall(0, 1e18, _getUniSettlementDataV3(Constants.Q96 * 12 / 10));
    }
```

</details>

**Result**

```solidity
    ├─ [168495] PerpMarket::execLiquidationCall(0, 1000000000000000000 [1e18], SettlementParamsV3({ contractAddress: 0x51F2C580cd70552c6447313519C5A6704a0B80C1, encodedData: 0x7167da2c29e6991eecf14985b7b41495862ef5630001f444c5c8e61e159198294fa08ff29b84297ca23a46, maxQuoteAmountPrice: 95073795017117205112252740403 [9.507e28], minQuoteAmountPrice: 0, price: 0, feePrice: 0, minFee: 0 }))
    │   ├─ [164414] PredyPool::execLiquidationCall(0, 1000000000000000000 [1e18], 0x000000000000000000000000000000000000000000000000000000000000002000000000000000000000000062c20aa1e0272312bc100b4e23b4dc1ed96dd7d100000000000000000000000051f2c580cd70552c6447313519c5a6704a0b80c1000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000013333333333333333333333330000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002b7167da2c29e6991eecf14985b7b41495862ef5630001f444c5c8e61e159198294fa08ff29b84297ca23a46000000000000000000000000000000000000000000)
    │   │   ├─ [156307] LiquidationLogic::4f9983d4(00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000de0b6b3a7640000000000000000000000000000000000000000000000000000000000000000003400000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000180000000000000000000000000000000000000000000000000000000000000002000000000000000000000000062c20aa1e0272312bc100b4e23b4dc1ed96dd7d100000000000000000000000051f2c580cd70552c6447313519c5a6704a0b80c1000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000013333333333333333333333330000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002b7167da2c29e6991eecf14985b7b41495862ef5630001f444c5c8e61e159198294fa08ff29b84297ca23a46000000000000000000000000000000000000000000) [delegatecall]
    │   │   │   ├─ [0] 0x0000000000000000000000000000000000000000::observe([1800, 0]) [staticcall]
    │   │   │   │   └─ ← ()
    │   │   │   └─ ← ()
    │   │   └─ ← EvmError: Revert
    │   └─ ← EvmError: Revert
    └─ ← EvmError: Revert
```

### Recommended Mitigation Steps

- Consider using [`GlobalData.validateVaultId`](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/types/GlobalData.sol#L26) in `LiquidationLogic.liquidate` to ensure `vaultId` is valid.
