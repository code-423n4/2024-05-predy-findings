# QA Report

## Findings Summary

Label   | Title
------- | -----
[L-01](#L-01-critical-roles-are-not-transferred-using-a-two-step-process)  | Critical roles are not transferred using a two-step process
[L-02](#L-02-orderid-parameter-of-perpmarketv1_executeorderv3-is-hardcoded-to-0)  | `orderId` parameter of `PerpMarketV1::_executeOrderV3` is hardcoded to `0`.
[L-03](#L-03-predypoolgetvault-does-not-uses-the-vaultlib-library-thus-missing-important-checks)  | `PredyPool::getVault` does not uses the `VaultLib` library, thus missing important checks.
[L-04](#L-04-an-lp-blacklisted-by-usdcusdt-cannot-withdraw-their-funds)  | An LP blacklisted by USDC/USDT cannot withdraw their funds
[L-05](#L-05-incorrect-comments-in-basemarketupgradablesol)  | Incorrect comments in `BaseMarketUpgradable.sol`
[NC-01](#NC-01-missing-event-emissions-for-important-state-changes) | Missing event emissions for important state changes
[NC-02](#NC-02-unnecessary-checks) | Unnecessary checks
[NC-03](#NC-03-misleading-variable-names) | Misleading variable names


## [L-01] Critical roles are not transferred using a two-step process
### Description
The `operator` and `filler` roles have the privileges necessary for the protocol to function.
E.g. 
- The `executeOrder` functions in all the `market contracts` can only be called by the `filler`.
- Only `operator` can call the `withdrawProtocolRevenue` function in `PredyPool.sol`.
### Impact
It is possible that these roles are transferred to a wrong address via `PredyPool::setOperator` and `BaseMarketUpgradable::updateWhitelistFiller` which will make the protocol non-functional.
### Recommendation
Use a two-step process to transfer these roles.

## [L-02] `orderId` parameter of `PerpMarketV1::_executeOrderV3` is hardcoded to `0`.
### Description
The `orderId` parameter of `PerpMarketV1::_executeOrderV3` is hardcoded to `0` in `PerpMarketV1::executeOrderV3` unlike its `L2` counterpart, `PerpMarket::executeOrderV3L2` which takes the `orderId` as a parameter.

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarketV1.sol#L156

```js
file: src/markets/perp/PerpMarketV1.sol

156: return _executeOrderV3(perpOrder, order.sig, settlementParams, 0);
```

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/markets/perp/PerpMarket.sol#L28-L32

This hardcoded `0` is eventually emitted via the `PerpTraded2` event in `PerpMarketV1::predyTradeAfterCallback` which can be misleading.
### Recommendation
A few possible mitigations are:
1. Pass the `orderId` parameter to `PerpMarketV1::_executeOrderV3` in `PerpMarketV1::executeOrderV3`.
2. Declare an `orderId` state variable, which is incrementted after each successful order execution, in `PerpMarketV1` and use it as the `orderId` parameter in `PerpMarketV1::_executeOrderV3`.

## [L-03] `PredyPool::getVault` does not uses the `VaultLib` library, thus missing important checks.
### Description
Instead of calling the `getVault` function in `VaultLib` library, `PredyPool::getVault` directly accesses the `vaults` mapping which leads to missing an important check.
```js
file: src/PredyPool.sol

364:    function getVault(uint256 vaultId) external view returns (DataType.Vault memory) {
365: @>    return globalData.vaults[vaultId];
366:    }
```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L365

```js
file: src/libraries/VaultLib.sol

11: function getVault(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId)
12:        internal
13:        view
14:        returns (DataType.Vault storage vault)
15:    {
16:        vault = globalData.vaults[vaultId];
17:
18:        // Ensure the caller is the owner of the existing vault
19: @>     if (vault.owner != msg.sender) {
20:            revert IPredyPool.CallerIsNotVaultOwner();
21:        }
22:    }
```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L19

### Recommendation
Use the `getVault` function in `VaultLib` library to ensure that the caller is the owner of the existing vault.

```diff
file: src/PredyPool.sol

    function getVault(uint256 vaultId) external view returns (DataType.Vault memory) {
-       return globalData.vaults[vaultId];
+       return VaultLib.getVault(globalData, vaultId);
    }
```

## [L-04] An LP blacklisted by USDC/USDT cannot withdraw their funds
### Description
An LP who has deposited USDC/USDT in the `PredyPool` contract can be potentially blacklisted by Circle/Tether. This will prevent the LP from withdrawing their funds via `PredyPool::withdraw`.

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L237

### Recommendation
Consider adding a `address receipient` parameter to `PredyPool::withdraw` which will allow the LP to withdraw their funds to a different address.

```diff
file: src/PredyPool.sol

-   function withdraw(uint256 pairId, bool isQuoteAsset, uint256 withdrawAmount)
+   function withdraw(uint256 pairId, bool isQuoteAsset, uint256 withdrawAmount, address receipient)
        external
        nonReentrant
        returns (uint256 finalBurnAmount, uint256 finalWithdrawAmount)
    {
-       return SupplyLogic.withdraw(globalData, pairId, withdrawAmount, isQuoteAsset);
+       return SupplyLogic.withdraw(globalData, pairId, withdrawAmount, isQuoteAsset, receipient);
    }
```

```diff
file: src/libraries/logic/SupplyLogic.sol

-   function withdraw(GlobalDataLibrary.GlobalData storage globalData, uint256 _pairId, uint256 _amount, bool _isStable) 
+   function withdraw(GlobalDataLibrary.GlobalData storage globalData, uint256 _pairId, uint256 _amount, bool _isStable, address _receipient)
    ...

        if (_isStable) {
-           (finalburntAmount, finalWithdrawalAmount) = burnBondAndTransferToken(pair.quotePool, _amount);
+           (finalburntAmount, finalWithdrawalAmount) = burnBondAndTransferToken(pair.quotePool, _amount, _receipient);
        } else {
-           (finalburntAmount, finalWithdrawalAmount) = burnBondAndTransferToken(pair.basePool, _amount);
+           (finalburntAmount, finalWithdrawalAmount) = burnBondAndTransferToken(pair.basePool, _amount, _receipient);
        }
    ...
    }

-   function burnBondAndTransferToken(Perp.AssetPoolStatus storage _pool, uint256 _amount)
+   function burnBondAndTransferToken(Perp.AssetPoolStatus storage _pool, uint256 _amount, address _receipient)
    {
        ...
-       ERC20(_pool.token).safeTransfer(msg.sender, finalWithdrawalAmount);
+       ERC20(_pool.token).safeTransfer(_receipient, finalWithdrawalAmount);
        ...
    }

```

## [L-05] Incorrect comments in `BaseMarketUpgradable.sol`

Change the natspec comments:
- "only owner can call this function" to "only filler can call this function" in `BaseMarketUpgradable::updateWhitelistFiller`.
- "only owner can call this function" to "only filler can call this function" in `BaseMarketUpgradable::updateWhitelistSettlement`.

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L126

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/base/BaseMarketUpgradable.sol#L138

## [NC-01] Missing event emissions for important state changes
Consider emitting events for important state changes like `filler` role transfer

```diff
file: src/markets/base/BaseMarketUpgradable.sol

    +   event WhitelistFillerUpdated(address newWhitelistFiller);
    
    ...

    function updateWhitelistFiller(address newWhitelistFiller) external onlyFiller {
        whitelistFiller = newWhitelistFiller;
    +   emit WhitelistFillerUpdated(newWhitelistFiller);
    }
        
```

## [NC-02] Unnecessary checks
In `PredyPool.sol`:

```js
    function withdrawProtocolRevenue(uint256 pairId, bool isQuoteToken) external onlyOperator {
        ...
    @>  require(amount > 0, "AZ");
        ...
        // @audit redundant check because of above require statement
    @>  if (amount > 0) {
            ...
        }
        ...
    }

    function withdrawCreatorRevenue(uint256 pairId, bool isQuoteToken) external onlyPoolOwner(pairId) {
        ...
    @>  require(amount > 0, "AZ");
        ...
        // @audit redundant check because of above require statement
    @>  if (amount > 0) {
            ...
        }
        ...
    }
```
https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L186

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/PredyPool.sol#L208

In `ScaledAsset.sol`:

```js
    function computeUserFee(ScaledAsset.AssetStatus memory _assetStatus, ScaledAsset.UserStatus memory _userStatus) internal pure returns (int256 interestFee)
    {
    @>  if (_userStatus.positionAmount > 0) {
            interestFee = (getAssetFee(_assetStatus, _userStatus)).toInt256();
    @>  } else {
            interestFee = -(getDebtFee(_assetStatus, _userStatus)).toInt256();
        }
    }

    // only called by computeUserFee
    function getAssetFee(AssetStatus memory tokenState, UserStatus memory accountState) internal pure returns (uint256)
    {
        // @audit redundant check
    @>  require(accountState.positionAmount >= 0, "S1");
        ...
    }

    // only called by computeUserFee
    function getDebtFee(AssetStatus memory tokenState, UserStatus memory accountState) internal pure returns (uint256)
    {
        // @audit redundant check
    @>  require(accountState.positionAmount <= 0, "S1");
        ...
    }

```

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ScaledAsset.sol#L160

https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/ScaledAsset.sol#L175

## [NC-03] Misleading variable names
- `owner` field in `Vault` struct stores the address corresponding to one of the market contracts, not the actual trader in most cases since only markets (or contracts which implements the necessary hooks) are used to open a position, which creates a vault.

```js
file: src/libraries/VaultLib.sol

    function createOrGetVault(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId, uint256 pairId)
        internal
        returns (uint256)
    {
        ...
        if (vaultId == 0) {
            ...
        @>  vault.owner = msg.sender;
            ...
        }
            ...
    }

``` 
 https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/src/libraries/VaultLib.sol#L37

- `GlobalDataLibrary` has a `GlobalData` struct which has `pairsCount` and `vaultCount` fields. These fields do not store the count, but rather the `IDs` of `pairs` and `vaults` mappings respectively.