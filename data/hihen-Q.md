# QA Report

## Summary

### Low Issues

Total **80 instances** over **16 issues**:

|ID|Issue|Instances|
|:--:|:---|:--:|
| [[L-01]](#l-01-a-year-is-not-always-365-days) | A year is not always 365 days | 1 |
| [[L-02]](#l-02-multiplication-on-the-result-of-a-division) | Multiplication on the result of a division | 2 |
| [[L-03]](#l-03-variables-shadowing-other-definitions) | Variables shadowing other definitions | 2 |
| [[L-04]](#l-04-upgradable-contracts-need-a-constructor-to-init-and-lock-the-implementation-contract) | Upgradable contracts need a constructor to init and lock the implementation contract | 8 |
| [[L-05]](#l-05-missing-zero-address-check-in-initializer) | Missing zero address check in initializer | 9 |
| [[L-06]](#l-06-named-return-variable-used-before-assignment) | Named return variable used before assignment | 3 |
| [[L-07]](#l-07-written-only-contract-variables) | Written only contract variables | 1 |
| [[L-08]](#l-08-use-abiencodecall-instead-of-abiencodewithsignatureabiencodewithselector) | Use `abi.encodeCall()` instead of `abi.encodeWithSignature()`/`abi.encodeWithSelector()` | 3 |
| [[L-09]](#l-09-constructor--initialization-function-lacks-parameter-validation) | Constructor / initialization function lacks parameter validation | 2 |
| [[L-10]](#l-10-unsafe-solidity-low-level-call-can-cause-gas-grief-attack) | Unsafe solidity low-level call can cause gas grief attack | 2 |
| [[L-11]](#l-11-functions-calling-contractsaddresses-with-transfer-hooks-should-be-protected-by-reentrancy-guard) | Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard | 24 |
| [[L-12]](#l-12-critical-functions-should-be-controlled-by-time-locks) | Critical functions should be controlled by time locks | 9 |
| [[L-13]](#l-13-missing-contract-existence-checks-before-low-level-calls) | Missing contract existence checks before low-level calls | 2 |
| [[L-14]](#l-14-tokens-may-be-minted-to-the-zero-address) | Tokens may be minted to the zero address | 4 |
| [[L-15]](#l-15-function-name-is-not-a-part-of-the-erc-20-standard) | Function `name()` is not a part of the ERC-20 standard | 1 |
| [[L-16]](#l-16-code-does-not-follow-the-best-practice-of-check-effects-interaction) | Code does not follow the best practice of check-effects-interaction | 7 |

### Non Critical Issues

Total **868 instances** over **61 issues**:

|ID|Issue|Instances|
|:--:|:---|:--:|
| [[N-01]](#n-01-import-declarations-should-import-specific-identifiers-rather-than-the-whole-file) | Import declarations should import specific identifiers, rather than the whole file | 67 |
| [[N-02]](#n-02-visibility-of-state-variables-is-not-explicitly-defined) | Visibility of state variables is not explicitly defined | 4 |
| [[N-03]](#n-03-names-of-privateinternal-functions-should-be-prefixed-with-an-underscore) | Names of `private`/`internal` functions should be prefixed with an underscore | 162 |
| [[N-04]](#n-04-names-of-privateinternal-state-variables-should-be-prefixed-with-an-underscore) | Names of `private`/`internal` state variables should be prefixed with an underscore | 3 |
| [[N-05]](#n-05-redundant-inheritance-specifier) | Redundant inheritance specifier | 2 |
| [[N-06]](#n-06-use-of-override-is-unnecessary) | Use of `override` is unnecessary | 10 |
| [[N-07]](#n-07-add-inline-comments-for-unnamed-parameters) | Add inline comments for unnamed parameters | 3 |
| [[N-08]](#n-08-consider-providing-a-ranged-getter-for-array-state-variables) | Consider providing a ranged getter for array state variables | 1 |
| [[N-09]](#n-09-assembly-blocks-should-have-extensive-comments) | Assembly blocks should have extensive comments | 11 |
| [[N-10]](#n-10-consider-splitting-complex-checks-into-multiple-steps) | Consider splitting complex checks into multiple steps | 2 |
| [[N-11]](#n-11-missing-checks-for-empty-bytes-when-updating-bytes-state-variables) | Missing checks for empty bytes when updating bytes state variables | 1 |
| [[N-12]](#n-12-complex-casting) | Complex casting | 1 |
| [[N-13]](#n-13-complex-math-should-be-split-into-multiple-steps) | Complex math should be split into multiple steps | 5 |
| [[N-14]](#n-14-consider-adding-a-blockdeny-list) | Consider adding a block/deny-list | 4 |
| [[N-15]](#n-15-constantsimmutables-redefined-elsewhere) | Constants/Immutables redefined elsewhere | 12 |
| [[N-16]](#n-16-convert-simple-if-statements-to-ternary-expressions) | Convert simple `if`-statements to ternary expressions | 9 |
| [[N-17]](#n-17-contracts-should-each-be-defined-in-separate-files) | Contracts should each be defined in separate files | 2 |
| [[N-18]](#n-18-contract-name-does-not-match-its-filename) | Contract name does not match its filename | 5 |
| [[N-19]](#n-19-consider-emitting-an-event-at-the-end-of-the-constructor) | Consider emitting an event at the end of the constructor | 11 |
| [[N-20]](#n-20-empty-function-body-without-comments) | Empty function body without comments | 5 |
| [[N-21]](#n-21-events-are-emitted-without-the-sender-information) | Events are emitted without the sender information | 16 |
| [[N-22]](#n-22-inconsistent-floating-version-pragma) | Inconsistent floating version pragma | 2 |
| [[N-23]](#n-23-imports-could-be-organized-more-systematically) | Imports could be organized more systematically | 27 |
| [[N-24]](#n-24-interfaces-should-be-indicated-with-an-i-prefix-in-the-contract-name) | Interfaces should be indicated with an `I` prefix in the contract name | 1 |
| [[N-25]](#n-25-openzeppelincontracts-should-be-upgraded-to-a-newer-version) | @openzeppelin/contracts should be upgraded to a newer version | 13 |
| [[N-26]](#n-26-lib-uniswapv3-periphery-should-be-upgraded-to-a-newer-version) | Lib @uniswap/v3-periphery should be upgraded to a newer version | 4 |
| [[N-27]](#n-27-expressions-for-constant-values-should-use-immutable-rather-than-constant) | Expressions for constant values should use `immutable` rather than `constant` | 15 |
| [[N-28]](#n-28-consider-moving-duplicated-strings-to-constants) | Consider moving duplicated strings to constants | 14 |
| [[N-29]](#n-29-contract-uses-both-requirerevert-as-well-as-custom-errors) | Contract uses both `require()`/`revert()` as well as custom errors | 7 |
| [[N-30]](#n-30-functions-should-be-named-in-mixedcase-style) | Functions should be named in mixedCase style | 6 |
| [[N-31]](#n-31-variable-names-for-immutables-should-use-upper_case_with_underscores) | Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES | 10 |
| [[N-32]](#n-32-named-imports-of-parent-contracts-are-missing) | Named imports of parent contracts are missing | 6 |
| [[N-33]](#n-33-constants-should-be-put-on-the-left-side-of-comparisons) | Constants should be put on the left side of comparisons | 111 |
| [[N-34]](#n-34-libraries-should-be-defined-in-separate-files) | Libraries should be defined in separate files | 2 |
| [[N-35]](#n-35-else-block-not-required) | `else`-block not required | 22 |
| [[N-36]](#n-36-large-multiples-of-ten-should-use-scientific-notation) | Large multiples of ten should use scientific notation | 7 |
| [[N-37]](#n-37-high-cyclomatic-complexity) | High cyclomatic complexity | 1 |
| [[N-38]](#n-38-typos) | Typos | 16 |
| [[N-39]](#n-39-unnecessary-casting) | Unnecessary casting | 3 |
| [[N-40]](#n-40-unused-contract-variables) | Unused contract variables | 1 |
| [[N-41]](#n-41-unused-named-return) | Unused named return | 19 |
| [[N-42]](#n-42-use-delete-instead-of-assigning-values-to-false) | Use delete instead of assigning values to `false` | 3 |
| [[N-43]](#n-43-consider-using-delete-rather-than-assigning-zero-to-clear-values) | Consider using `delete` rather than assigning zero to clear values | 5 |
| [[N-44]](#n-44-use-the-latest-solidity-version) | Use the latest Solidity version | 52 |
| [[N-45]](#n-45-use-a-struct-to-encapsulate-multiple-function-parameters) | Use a struct to encapsulate multiple function parameters | 2 |
| [[N-46]](#n-46-returning-a-struct-instead-of-a-bunch-of-variables-is-better) | Returning a struct instead of a bunch of variables is better | 5 |
| [[N-47]](#n-47-contract-variables-should-have-comments) | Contract variables should have comments | 20 |
| [[N-48]](#n-48-missing-event-when-a-state-variables-is-set-in-constructor) | Missing event when a state variables is set in constructor | 1 |
| [[N-49]](#n-49-empty-bytes-check-is-missing) | Empty bytes check is missing | 17 |
| [[N-50]](#n-50-dont-define-functions-with-the-same-name-in-a-contract) | Don't define functions with the same name in a contract | 2 |
| [[N-51]](#n-51-multiple-mappings-with-same-keys-can-be-combined-into-a-single-struct-mapping-for-readability) | Multiple mappings with same keys can be combined into a single struct mapping for readability | 2 |
| [[N-52]](#n-52-missing-event-for-critical-changes) | Missing event for critical changes | 2 |
| [[N-53]](#n-53-non-assembly-method-available) | Non-assembly method available | 5 |
| [[N-54]](#n-54-consider-adding-emergency-stop-functionality) | Consider adding emergency-stop functionality | 10 |
| [[N-55]](#n-55-avoid-the-use-of-sensitive-terms) | Avoid the use of sensitive terms | 40 |
| [[N-56]](#n-56-use-the-modern-upgradeable-contract-paradigm) | Use the Modern Upgradeable Contract Paradigm | 3 |
| [[N-57]](#n-57-large-or-complicated-code-bases-should-implement-invariant-tests) | Large or complicated code bases should implement invariant tests | 1 |
| [[N-58]](#n-58-the-default-value-is-manually-set-when-it-is-declared) | The default value is manually set when it is declared | 5 |
| [[N-59]](#n-59-contracts-should-have-all-publicexternal-functions-exposed-by-interfaces) | Contracts should have all `public`/`external` functions exposed by `interface`s | 8 |
| [[N-60]](#n-60-consider-adding-formal-verification-proofs) | Consider adding formal verification proofs | 55 |
| [[N-61]](#n-61-use-scopes-sparingly) | Use scopes sparingly | 7 |

## Low Issues

### [L-01] A year is not always 365 days

A year is not always 365 days or any fixed days or seconds. On leap years, the number of days is 366, so calculations during those years will return the wrong value.

There is 1 instance:

- *ApplyInterestLib.sol* ( [67-67](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L67-L67) ):

```solidity
67:             * (block.timestamp - lastUpdateTimestamp) / 365 days;
```

### [L-02] Multiplication on the result of a division

Dividing a number by another often results in a loss of precision. Multiplying the result by another number increases the loss of precision, often significantly.
For example: `x*(y/z)` should be re-written as `(x*z)/y`.

There are 2 instances:

- *ScaledAsset.sol* ( [194-198](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L194-L198), [201-207](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L201-L207) ):

```solidity
194:         uint256 protocolFee = FixedPointMathLib.mulDivDown(
195:             FixedPointMathLib.mulDivDown(_interestRate, getTotalDebtValue(tokenState), Constants.ONE),
196:             _reserveFactor,
197:             100
198:         );

201:         uint256 supplyInterestRate = FixedPointMathLib.mulDivDown(
202:             FixedPointMathLib.mulDivDown(
203:                 _interestRate, getTotalDebtValue(tokenState), getTotalCollateralValue(tokenState)
204:             ),
205:             100 - _reserveFactor,
206:             100
207:         );
```

### [L-03] Variables shadowing other definitions

A variable declaration shadowing any other existing definition is error-prone. It can cause confusion for developers, potentially introduce bugs, and reduce the readability and maintainability.

There are 2 instances:

- *GammaTradeMarket.sol* ( [69-69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L69-L69) ):

```solidity
/// @audit Shadows `state variable whitelistFiller`
69:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)
```

- *PerpMarketV1.sol* ( [92-92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L92-L92) ):

```solidity
/// @audit Shadows `state variable whitelistFiller`
92:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)
```

### [L-04] Upgradable contracts need a constructor to init and lock the implementation contract

An uninitialized contract can be taken over by an attacker. For an upgradable contract, this applies to both the proxy and its implementation contract, which may impact the proxy.
To prevent the implementation contract from being used, we should trigger the initialization in the constructor to automatically lock it when it is deployed.
For contracts that inherit `Initializable`, the `_disableInitializers()` function [is suggested to do this job](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/4d9d9073b84f56fe3eea360e5067c6ffd864c43d/contracts/proxy/utils/Initializable.sol#L43-L56).

<details>
<summary>There are 8 instances (click to show):</summary>

- *PredyPool.sol* ( [68-68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L68-L68) ):

```solidity
68:     constructor() {}
```

- *BaseHookCallbackUpgradable.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L13-L13) ):

```solidity
13:     constructor() {}
```

- *BaseMarketUpgradable.sol* ( [36-36](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L36-L36) ):

```solidity
36:     constructor() {}
```

- *GammaTradeMarket.sol* ( [67-67](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L67-L67) ):

```solidity
67:     constructor() {}
```

- *GammaTradeMarketL2.sol* ( [40](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol#L40) ):

```solidity
/// @audit Missing constructor to initialize the implementation contract
40: contract GammaTradeMarketL2 is GammaTradeMarket {
```

- *GammaTradeMarketWrapper.sol* ( [10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketWrapper.sol#L10) ):

```solidity
/// @audit Missing constructor to initialize the implementation contract
10: contract GammaTradeMarketWrapper is GammaTradeMarketL2 {
```

- *PerpMarket.sol* ( [27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarket.sol#L27) ):

```solidity
/// @audit Missing constructor to initialize the implementation contract
27: contract PerpMarket is PerpMarketV1 {
```

- *PerpMarketV1.sol* ( [90-90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L90-L90) ):

```solidity
90:     constructor() {}
```

</details>

### [L-05] Missing zero address check in initializer

Consider adding a zero address check for each address type parameter in initializer.

There are 9 instances:

- *PredyPool.sol* ( [70-70](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L70-L70) ):

```solidity
/// @audit `uniswapFactory not checked`
70:     function initialize(address uniswapFactory) public initializer {
```

- *GammaTradeMarket.sol* ( [69-69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L69-L69) ):

```solidity
/// @audit `predyPool not checked`
/// @audit `permit2Address not checked`
/// @audit `whitelistFiller not checked`
/// @audit `quoterAddress not checked`
69:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)
```

- *PerpMarketV1.sol* ( [92-92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L92-L92) ):

```solidity
/// @audit `predyPool not checked`
/// @audit `permit2Address not checked`
/// @audit `whitelistFiller not checked`
/// @audit `quoterAddress not checked`
92:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)
```

### [L-06] Named return variable used before assignment

As no value is written to the variable, the default value is always read. This is usually due to a bug in the code logic that causes an invalid value to be used.

There are 3 instances:

- *GammaTradeMarket.sol* ( [380-380](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L380-L380) ):

```solidity
/// @audit result
380:             return result;
```

- *PerpMarketV1.sol* ( [259-259](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L259-L259), [259-259](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L259-L259) ):

```solidity
/// @audit vaultStatus
259:             return (userPosition, vaultStatus, vault);

/// @audit vault
259:             return (userPosition, vaultStatus, vault);
```

### [L-07] Written only contract variables

Write only contract variables are only written in the contract and are never read and cannot be accessed through an interface.
It is recommended to check if there is a bug causing the missing readings, or if some `view` interfaces should be provided. If not, consider removing them to improve code clarity, avoid confusion, and save gas.

There is 1 instance:

- *BaseMarket.sol* ( [25-25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L25-L25) ):

```solidity
25:         _quoter = PredyPoolQuoter(quoterAddress);
```

### [L-08] Use `abi.encodeCall()` instead of `abi.encodeWithSignature()`/`abi.encodeWithSelector()`

Function `abi.encodeCall()` provides [type-safe encode utility](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/3693) comparing with `abi.encodeWithSignature()`/`abi.encodeWithSelector()`.

There are 3 instances:

- *UniHelper.sol* ( [42-42](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L42-L42), [45-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L45-L45), [61-61](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L61-L61) ):

```solidity
42:             address(uniswapPool).staticcall(abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos));

45:             if (keccak256(data) != keccak256(abi.encodeWithSignature("Error(string)", "OLD"))) {

61:                 abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos)
```

### [L-09] Constructor / initialization function lacks parameter validation

Constructors and initialization functions play a critical role in contracts by setting important initial states when the contract is first deployed before the system starts. The parameters passed to the constructor and initialization functions directly affect the behavior of the contract / protocol. If incorrect parameters are provided, the system may fail to run, behave abnormally, be unstable, or lack security. Therefore, it's crucial to carefully check each parameter in the constructor and initialization functions. If an exception is found, the transaction should be rolled back.

There are 2 instances:

- *PriceFeed.sol* ( [37-37](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L37-L37) ):

```solidity
/// @audit `priceId`
/// @audit `decimalsDiff`
37:     constructor(address quotePrice, address pyth, bytes32 priceId, uint256 decimalsDiff) {
```

### [L-10] Unsafe solidity low-level call can cause gas grief attack

Using the low-level calls of a solidity address can leave the contract open to gas grief attacks. These attacks occur when the called contract returns a large amount of data.
So when calling an external contract, it is necessary to check the length of the return data before reading/copying it (using `returndatasize()`).

There are 2 instances:

- *UniHelper.sol* ( [42-42](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L42-L42), [60-62](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L60-L62) ):

```solidity
42:             address(uniswapPool).staticcall(abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos));

60:             (success, data) = address(uniswapPool).staticcall(
61:                 abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos)
62:             );
```

### [L-11] Functions calling contracts/addresses with transfer hooks should be protected by reentrancy guard

Even if the function follows the best practice of check-effects-interaction, not using a reentrancy guard when there may be transfer hooks opens the users of this protocol up to [read-only reentrancy vulnerability](https://chainsecurity.com/curve-lp-oracle-manipulation-post-mortem/) with no way to protect them except by block-listing the entire protocol.

<details>
<summary>There are 24 instances (click to show):</summary>

- *PredyPool.sol* ( [187-187](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L187-L187), [209-209](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L209-L209) ):

```solidity
187:             ERC20(pool.token).safeTransfer(msg.sender, amount);

209:             ERC20(pool.token).safeTransfer(msg.sender, amount);
```

- *SettlementCallbackLib.sol* ( [48-50](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L48-L50), [105-105](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L105-L105), [123-123](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L123-L123), [128-128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L128-L128), [130-130](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L130-L130), [133-133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L133-L133), [152-152](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L152-L152), [170-170](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L170-L170), [175-175](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L175-L175), [177-177](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L177-L177), [180-180](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L180-L180) ):

```solidity
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

- *LiquidationLogic.sol* ( [99-99](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L99-L99), [106-106](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L106-L106) ):

```solidity
99:                     ERC20(pairStatus.quotePool.token).safeTransfer(vault.recipient, sentMarginAmount);

106:                 ERC20(pairStatus.quotePool.token).safeTransferFrom(msg.sender, address(this), uint256(-remainingMargin));
```

- *ReallocationLogic.sol* ( [69-69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReallocationLogic.sol#L69-L69) ):

```solidity
69:                     ERC20(pairStatus.quotePool.token).safeTransfer(msg.sender, uint256(exceedsQuote));
```

- *SupplyLogic.sol* ( [52-52](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L52-L52), [90-90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L90-L90) ):

```solidity
52:         ERC20(_pool.token).safeTransferFrom(msg.sender, address(this), _amount);

90:         ERC20(_pool.token).safeTransfer(msg.sender, finalWithdrawalAmount);
```

- *GammaTradeMarket.sol* ( [118-118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L118-L118) ):

```solidity
118:                     quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));
```

- *PerpMarketV1.sol* ( [126-126](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L126-L126) ):

```solidity
126:                 quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));
```

- *UniswapSettlement.sol* ( [30-30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L30-L30), [46-46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L46-L46), [54-54](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L54-L54) ):

```solidity
30:         ERC20(baseToken).safeTransferFrom(msg.sender, address(this), amountIn);

46:         ERC20(quoteToken).safeTransferFrom(msg.sender, address(this), amountInMaximum);

54:             ERC20(quoteToken).safeTransfer(msg.sender, amountInMaximum - amountIn);
```

- *GlobalData.sol* ( [85-85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L85-L85) ):

```solidity
85:         ERC20(currency).safeTransfer(to, amount);
```

</details>

### [L-12] Critical functions should be controlled by time locks

It is a good practice to give time for users to react and adjust to critical changes. A timelock provides more guarantees and reduces the level of trust required, thus decreasing risk for users. It also indicates that the project is legitimate (less risk of a malicious owner making a sandwich attack on a user).

<details>
<summary>There are 9 instances (click to show):</summary>

- *PredyPool.sol* ( [157-157](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L157-L157), [167-167](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L167-L167), [286-286](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L286-L286) ):

```solidity
157:     function updatePoolOwner(uint256 pairId, address poolOwner) external onlyPoolOwner(pairId) {

167:     function updatePriceOracle(uint256 pairId, address priceFeed) external onlyPoolOwner(pairId) {

286:     function updateRecepient(uint256 vaultId, address recipient) external onlyVaultOwner(vaultId) {
```

- *BaseMarket.sol* ( [84-84](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L84-L84), [92-92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L92-L92) ):

```solidity
84:     function updateWhitelistFiller(address newWhitelistFiller) external onlyOwner {

92:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyOwner {
```

- *BaseMarketUpgradable.sol* ( [128-128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L128-L128), [132-132](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L132-L132), [140-140](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L140-L140) ):

```solidity
128:     function updateWhitelistFiller(address newWhitelistFiller) external onlyFiller {

132:     function updateQuoter(address newQuoter) external onlyFiller {

140:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyFiller {
```

- *GammaTradeMarket.sol* ( [388-388](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L388-L388) ):

```solidity
388:     function _addPositionIndex(address trader, uint256 newPositionId) internal {
```

</details>

### [L-13] Missing contract existence checks before low-level calls

Low-level calls return success if there is no code present at the specified address. In addition to the zero-address checks, add a check to verify that `<address>.code.length > 0`.

There are 2 instances:

- *UniHelper.sol* ( [42-42](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L42-L42), [60-62](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L60-L62) ):

```solidity
42:             address(uniswapPool).staticcall(abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos));

60:             (success, data) = address(uniswapPool).staticcall(
61:                 abi.encodeWithSelector(IUniswapV3PoolOracle.observe.selector, secondsAgos)
62:             );
```

### [L-14] Tokens may be minted to the zero address

Neither the listed functions, nor `_mint()` prevent minting to `address(0x0)`

There are 4 instances:

- *Perp.sol* ( [279-281](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L279-L281), [711-713](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L711-L713) ):

```solidity
279:         (uint256 requiredAmount0, uint256 requiredAmount1) = IUniswapV3Pool(_sqrtAssetStatus.uniswapPool).mint(
280:             address(this), _sqrtAssetStatus.tickLower, _sqrtAssetStatus.tickUpper, _totalLiquidityAmount, ""
281:         );

711:         (uint256 amount0, uint256 amount1) = IUniswapV3Pool(_assetStatus.uniswapPool).mint(
712:             address(this), _assetStatus.tickLower, _assetStatus.tickUpper, _liquidityAmount.safeCastTo128(), ""
713:         );
```

- *SupplyLogic.sol* ( [54-54](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L54-L54) ):

```solidity
54:         ISupplyToken(_pool.supplyTokenAddress).mint(msg.sender, mintAmount);
```

- *SupplyToken.sol* ( [21-21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L21-L21) ):

```solidity
21:     function mint(address account, uint256 amount) external virtual override onlyController {
```

### [L-15] Function `name()` is not a part of the ERC-20 standard

The `name()` function is not a part of the [ERC-20 standard](https://eips.ethereum.org/EIPS/eip-20), and was added later as an [optional extension](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/IERC20Metadata.sol). As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.

There is 1 instance:

- *AddPairLogic.sol* ( [198-198](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L198-L198) ):

```solidity
198:                 string.concat("Predy6-Supply-", erc20.name()),
```

### [L-16] Code does not follow the best practice of check-effects-interaction

Code should follow the best-practice of [check-effects-interaction](https://blockchain-academy.hs-mittweida.de/courses/solidity-coding-beginners-to-intermediate/lessons/solidity-11-coding-patterns/topic/checks-effects-interactions/), where state variables are updated before any external calls are made. Doing so prevents a large class of reentrancy bugs.

<details>
<summary>There are 7 instances (click to show):</summary>

- *GammaTradeMarket.sol* ( [163-176](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L163-L176), [191-191](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L191-L191), [194-194](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L194-L194), [195-195](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L195-L195) ):

```solidity
/// @audit `_verifyOrder()` is called on line 160, triggering an external call - `permitWitnessTransferFrom()`
163:         tradeResult = _predyPool.trade(
164:             IPredyPool.TradeParams(
165:                 gammaOrder.pairId,
166:                 gammaOrder.positionId,
167:                 gammaOrder.quantity,
168:                 gammaOrder.quantitySqrt,
169:                 abi.encode(
170:                     CallbackData(
171:                         GammaTradeMarketLib.CallbackType.TRADE, gammaOrder.info.trader, gammaOrder.marginAmount
172:                     )
173:                 )
174:             ),
175:             _getSettlementDataFromV3(settlementParams, msg.sender)
176:         );

/// @audit `_verifyOrder()` is called on line 160, triggering an external call - `permitWitnessTransferFrom()`
191:         userPosition.leverage = gammaOrder.leverage;

/// @audit `_verifyOrder()` is called on line 160, triggering an external call - `permitWitnessTransferFrom()`
194:         userPosition.lastHedgedSqrtPrice = tradeResult.sqrtTwap;

/// @audit `_verifyOrder()` is called on line 160, triggering an external call - `permitWitnessTransferFrom()`
195:         userPosition.lastHedgedTime = block.timestamp;
```

- *PerpMarketV1.sol* ( [208-208](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L208-L208) ):

```solidity
/// @audit `trade()` is called on line 185
208:             userPosition.vaultId = tradeResult.vaultId;
```

- *UniswapSettlement.sol* ( [33-35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L33-L35), [49-51](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L49-L51) ):

```solidity
/// @audit `safeTransferFrom()` is called on line 30
33:         amountOut = _swapRouter.exactInput(
34:             ISwapRouter.ExactInputParams(data, recipient, block.timestamp, amountIn, amountOutMinimum)
35:         );

/// @audit `safeTransferFrom()` is called on line 46
49:         amountIn = _swapRouter.exactOutput(
50:             ISwapRouter.ExactOutputParams(data, recipient, block.timestamp, amountOut, amountInMaximum)
51:         );
```

</details>

## Non Critical Issues

### [N-01] Import declarations should import specific identifiers, rather than the whole file

Using import declarations of the form `import {<identifier_name>} from "some/file.sol"` avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation (but does not save any gas).

<details>
<summary>There are 67 instances (click to show):</summary>

- *BaseHookCallback.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol#L5) ):

```solidity
4: import "../interfaces/IPredyPool.sol";

5: import "../interfaces/IHooks.sol";
```

- *BaseHookCallbackUpgradable.sol* ( [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L5), [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L6) ):

```solidity
5: import "../interfaces/IPredyPool.sol";

6: import "../interfaces/IHooks.sol";
```

- *BaseMarket.sol* ( [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L5), [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L7), [8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L8) ):

```solidity
5: import "./BaseHookCallback.sol";

7: import "../interfaces/IFillerMarket.sol";

8: import "./SettlementCallbackLib.sol";
```

- *BaseMarketUpgradable.sol* ( [8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L8), [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L9) ):

```solidity
8: import "../interfaces/IFillerMarket.sol";

9: import "./SettlementCallbackLib.sol";
```

- *ApplyInterestLib.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L5), [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L6) ):

```solidity
4: import "./Perp.sol";

5: import "./ScaledAsset.sol";

6: import "./DataType.sol";
```

- *Perp.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L5), [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L6), [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L7), [8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L8), [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L9), [11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L11), [12](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L12), [13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L13), [14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L14), [16](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L16), [17](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L17), [18](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L18), [19](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L19) ):

```solidity
4: import "@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol";

5: import "@uniswap/v3-periphery/contracts/libraries/PositionKey.sol";

6: import "@uniswap/v3-core/contracts/libraries/FixedPoint96.sol";

7: import "@uniswap/v3-core/contracts/libraries/TickMath.sol";

8: import "@solmate/src/utils/SafeCastLib.sol";

9: import "@openzeppelin/contracts/utils/math/SafeCast.sol";

11: import "./ScaledAsset.sol";

12: import "./InterestRateModel.sol";

13: import "./PremiumCurveModel.sol";

14: import "./Constants.sol";

16: import "./UniHelper.sol";

17: import "./math/LPMath.sol";

18: import "./math/Math.sol";

19: import "./Reallocation.sol";
```

- *PerpFee.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L5), [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L6), [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L7), [8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L8) ):

```solidity
4: import "@openzeppelin/contracts/utils/math/SafeCast.sol";

5: import "./PairLib.sol";

6: import "./Perp.sol";

7: import "./DataType.sol";

8: import "./Constants.sol";
```

- *PositionCalculator.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L5), [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L6), [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L7), [8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L8), [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L9), [10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L10), [11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L11), [12](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L12) ):

```solidity
4: import "@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol";

5: import "@uniswap/v3-core/contracts/libraries/FullMath.sol";

6: import "@openzeppelin/contracts/utils/math/SafeCast.sol";

7: import "./UniHelper.sol";

8: import "./Perp.sol";

9: import "./DataType.sol";

10: import "./Constants.sol";

11: import "./math/Math.sol";

12: import "../PriceFeed.sol";
```

- *PremiumCurveModel.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PremiumCurveModel.sol#L4) ):

```solidity
4: import "./Constants.sol";
```

- *Reallocation.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L5), [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L6), [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L7), [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L9), [10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L10) ):

```solidity
4: import "@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol";

5: import "@uniswap/v3-core/contracts/libraries/TickMath.sol";

6: import "@uniswap/v3-core/contracts/libraries/FixedPoint96.sol";

7: import "@openzeppelin/contracts/utils/math/SafeCast.sol";

9: import "./Perp.sol";

10: import "./ScaledAsset.sol";
```

- *UniHelper.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L5), [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L6), [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L7), [8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L8) ):

```solidity
4: import "@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol";

5: import "@uniswap/v3-core/contracts/libraries/TickMath.sol";

6: import "@uniswap/v3-periphery/contracts/libraries/PositionKey.sol";

7: import "../vendors/IUniswapV3PoolOracle.sol";

8: import "./Constants.sol";
```

- *LPMath.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L5), [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L6), [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L7) ):

```solidity
4: import "@uniswap/v3-core/contracts/libraries/FullMath.sol";

5: import "@uniswap/v3-core/contracts/libraries/TickMath.sol";

6: import "@uniswap/v3-core/contracts/libraries/FixedPoint96.sol";

7: import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *Math.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L4) ):

```solidity
4: import "@uniswap/v3-core/contracts/libraries/FullMath.sol";
```

- *PerpMarketV1.sol* ( [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L9), [12](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L12), [13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L13), [20](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L20), [21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L21) ):

```solidity
9: import "../../interfaces/IPredyPool.sol";

12: import "../../libraries/orders/Permit2Lib.sol";

13: import "../../libraries/orders/ResolvedOrder.sol";

20: import "./PerpOrder.sol";

21: import "./PerpOrderV3.sol";
```

- *UniswapSettlement.sol* ( [8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L8) ):

```solidity
8: import "../interfaces/ISettlement.sol";
```

- *GlobalData.sol* ( [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L7), [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L9), [10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L10) ):

```solidity
7: import "../interfaces/IPredyPool.sol";

9: import "../libraries/DataType.sol";

10: import "./LockData.sol";
```

- *LockData.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/LockData.sol#L4) ):

```solidity
4: import "../interfaces/IPredyPool.sol";
```

</details>

### [N-02] Visibility of state variables is not explicitly defined

To avoid misunderstandings and unexpected state accesses, it is recommended to explicitly define the visibility of each state variable.

There are 4 instances:

- *BaseHookCallback.sol* ( [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol#L8-L8) ):

```solidity
8:     IPredyPool immutable _predyPool;
```

- *BaseHookCallbackUpgradable.sol* ( [9-9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L9-L9) ):

```solidity
9:     IPredyPool _predyPool;
```

- *LiquidationLogic.sol* ( [27-27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L27-L27) ):

```solidity
27:     uint256 constant _MAX_ACCEPTABLE_SQRT_PRICE_RANGE = 101488915;
```

- *SupplyToken.sol* ( [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L8-L8) ):

```solidity
8:     address immutable _controller;
```

### [N-03] Names of `private`/`internal` functions should be prefixed with an underscore

It is recommended by the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#underscore-prefix-for-non-external-functions-and-variables).

<details>
<summary>There are 162 instances (click to show):</summary>

- *BaseMarketUpgradable.sol* ( [61-64](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L61-L64) ):

```solidity
61:     function decodeParamsV3(bytes memory settlementData, int256 baseAmountDelta)
62:         internal
63:         pure
64:         returns (SettlementCallbackLib.SettlementParams memory)
```

- *SettlementCallbackLib.sol* ( [25-25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L25-L25), [29-32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L29-L32), [40-46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L40-L46), [60-66](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L60-L66), [90-98](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L90-L98), [137-145](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L137-L145) ):

```solidity
25:     function decodeParams(bytes memory settlementData) internal pure returns (SettlementParams memory) {

29:     function validate(
30:         mapping(address settlementContractAddress => bool) storage _whiteListedSettlements,
31:         SettlementParams memory settlementParams
32:     ) internal view {

40:     function execSettlement(
41:         IPredyPool predyPool,
42:         address quoteToken,
43:         address baseToken,
44:         SettlementParams memory settlementParams,
45:         int256 baseAmountDelta
46:     ) internal {

60:     function execSettlementInternal(
61:         IPredyPool predyPool,
62:         address quoteToken,
63:         address baseToken,
64:         SettlementParams memory settlementParams,
65:         int256 baseAmountDelta
66:     ) internal {

90:     function sell(
91:         IPredyPool predyPool,
92:         address quoteToken,
93:         address baseToken,
94:         SettlementParams memory settlementParams,
95:         address sender,
96:         uint256 price,
97:         uint256 sellAmount
98:     ) internal {

137:     function buy(
138:         IPredyPool predyPool,
139:         address quoteToken,
140:         address baseToken,
141:         SettlementParams memory settlementParams,
142:         address sender,
143:         uint256 price,
144:         uint256 buyAmount
145:     ) internal {
```

- *ApplyInterestLib.sol* ( [26-26](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L26-L26), [50-52](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L50-L52), [75-81](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L75-L81) ):

```solidity
26:     function applyInterestForToken(mapping(uint256 => DataType.PairStatus) storage pairs, uint256 pairId) internal {

50:     function applyInterestForPoolStatus(Perp.AssetPoolStatus storage poolStatus, uint256 lastUpdateTimestamp, uint8 fee)
51:         internal
52:         returns (uint256 interestRate, uint256 totalProtocolFee)

75:     function emitInterestGrowthEvent(
76:         DataType.PairStatus memory assetStatus,
77:         uint256 interestRateQuote,
78:         uint256 interestRateBase,
79:         uint256 totalProtocolFeeQuote,
80:         uint256 totalProtocolFeeBase
81:     ) internal {
```

- *InterestRateModel.sol* ( [18-21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/InterestRateModel.sol#L18-L21) ):

```solidity
18:     function calculateInterestRate(IRMParams memory irmParams, uint256 utilizationRatio)
19:         internal
20:         pure
21:         returns (uint256)
```

- *PairLib.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PairLib.sol#L5-L5) ):

```solidity
5:     function getRebalanceCacheId(uint256 pairId, uint64 rebalanceId) internal pure returns (uint256) {
```

- *Perp.sol* ( [119-122](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L119-L122), [145-145](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L145-L145), [159-162](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L159-L162), [202-205](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L202-L205), [262-267](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L262-L267), [305-310](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L305-L310), [332-337](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L332-L337), [345-345](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L345-L345), [373-373](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L373-L373), [414-414](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L414-L414), [426-431](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L426-L431), [470-475](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L470-L475), [526-531](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L526-L531), [585-588](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L585-L588), [604-604](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L604-L604), [618-622](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L618-L622), [673-676](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L673-L676), [707-709](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L707-L709), [719-721](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L719-L721), [745-751](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L745-L751), [790-794](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L790-L794), [815-815](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L815-L815) ):

```solidity
119:     function createAssetStatus(address uniswapPool, int24 tickLower, int24 tickUpper)
120:         internal
121:         pure
122:         returns (SqrtPerpAssetStatus memory)

145:     function createPerpUserStatus(uint64 _pairId) internal pure returns (UserStatus memory) {

159:     function updateRebalanceInterestGrowth(
160:         DataType.PairStatus memory _pairStatus,
161:         SqrtPerpAssetStatus storage _sqrtAssetStatus
162:     ) internal {

202:     function reallocate(
203:         DataType.PairStatus storage _assetStatusUnderlying,
204:         SqrtPerpAssetStatus storage _sqrtAssetStatus
205:     ) internal returns (bool, bool, int256 deltaPositionBase, int256 deltaPositionQuote) {

262:     function rebalanceForInRange(
263:         DataType.PairStatus storage _assetStatusUnderlying,
264:         SqrtPerpAssetStatus storage _sqrtAssetStatus,
265:         int24 _currentTick,
266:         uint128 _totalLiquidityAmount
267:     ) internal {

305:     function swapForOutOfRange(
306:         DataType.PairStatus storage pairStatus,
307:         uint160 _currentSqrtPrice,
308:         int24 _tick,
309:         uint128 _totalLiquidityAmount
310:     ) internal returns (int256 deltaPositionBase, int256 deltaPositionQuote) {

332:     function getAvailableLiquidityAmount(
333:         address _controllerAddress,
334:         address _uniswapPool,
335:         int24 _tickLower,
336:         int24 _tickUpper
337:     ) internal view returns (uint128) {

345:     function settleUserBalance(DataType.PairStatus storage _pairStatus, UserStatus storage _userStatus) internal {

373:     function updateFeeAndPremiumGrowth(uint256 _pairId, SqrtPerpAssetStatus storage _assetStatus) internal {

414:     function saveLastFeeGrowth(SqrtPerpAssetStatus storage _assetStatus) internal {

426:     function computeRequiredAmounts(
427:         SqrtPerpAssetStatus storage _sqrtAssetStatus,
428:         bool _isQuoteZero,
429:         UserStatus memory _userStatus,
430:         int256 _tradeSqrtAmount
431:     ) internal returns (int256 requiredAmountUnderlying, int256 requiredAmountStable) {

470:     function updatePosition(
471:         DataType.PairStatus storage _pairStatus,
472:         UserStatus storage _userStatus,
473:         UpdatePerpParams memory _updatePerpParams,
474:         UpdateSqrtPerpParams memory _updateSqrtPerpParams
475:     ) internal returns (IPredyPool.Payoff memory payoff) {

526:     function updateSqrtPosition(
527:         uint256 _pairId,
528:         SqrtPerpAssetStatus storage _assetStatus,
529:         UserStatus storage _userStatus,
530:         int256 _amount
531:     ) internal {

585:     function getAvailableSqrtAmount(SqrtPerpAssetStatus memory _assetStatus, bool _isWithdraw)
586:         internal
587:         pure
588:         returns (uint256)

604:     function getUtilizationRatio(SqrtPerpAssetStatus memory _assetStatus) internal pure returns (uint256) {

618:     function updateRebalanceEntry(
619:         SqrtPerpAssetStatus storage _assetStatus,
620:         UserStatus storage _userStatus,
621:         bool _isQuoteZero
622:     ) internal returns (int256 rebalancePositionUpdateUnderlying, int256 rebalancePositionUpdateStable) {

673:     function calculateEntry(int256 _positionAmount, int256 _entryValue, int256 _tradeAmount, int256 _valueUpdate)
674:         internal
675:         pure
676:         returns (int256 deltaEntry, int256 payoff)

707:     function increase(SqrtPerpAssetStatus memory _assetStatus, uint256 _liquidityAmount)
708:         internal
709:         returns (int256 requiredAmount0, int256 requiredAmount1)

719:     function decrease(SqrtPerpAssetStatus memory _assetStatus, uint256 _liquidityAmount)
720:         internal
721:         returns (int256 receivedAmount0, int256 receivedAmount1)

745:     function calculateSqrtPerpOffset(
746:         UserStatus memory _userStatus,
747:         int24 _tickLower,
748:         int24 _tickUpper,
749:         int256 _tradeSqrtAmount,
750:         bool _isQuoteZero
751:     ) internal pure returns (int256 offsetUnderlying, int256 offsetStable) {

790:     function updateRebalancePosition(
791:         DataType.PairStatus storage _pairStatus,
792:         int256 _updateAmount0,
793:         int256 _updateAmount1
794:     ) internal {

815:     function finalizeReallocation(SqrtPerpAssetStatus storage sqrtPerpStatus) internal {
```

- *PerpFee.sol* ( [16-20](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L16-L20), [41-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L41-L45), [65-68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L65-L68), [95-97](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L95-L97), [111-116](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L111-L116), [136-141](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L136-L141) ):

```solidity
16:     function computeUserFee(
17:         DataType.PairStatus memory assetStatus,
18:         mapping(uint256 => DataType.RebalanceFeeGrowthCache) storage rebalanceFeeGrowthCache,
19:         Perp.UserStatus memory userStatus
20:     ) internal view returns (DataType.FeeAmount memory) {

41:     function settleUserFee(
42:         DataType.PairStatus storage assetStatus,
43:         mapping(uint256 => DataType.RebalanceFeeGrowthCache) storage rebalanceFeeGrowthCache,
44:         Perp.UserStatus storage userStatus
45:     ) internal returns (DataType.FeeAmount memory) {

65:     function computePremium(DataType.PairStatus memory baseAssetStatus, Perp.SqrtPositionStatus memory sqrtPerp)
66:         internal
67:         pure
68:         returns (int256 feeUnderlying, int256 feeStable)

95:     function settlePremium(DataType.PairStatus memory baseAssetStatus, Perp.SqrtPositionStatus storage sqrtPerp)
96:         internal
97:         returns (int256 feeUnderlying, int256 feeStable)

111:     function computeRebalanceInterest(
112:         uint256 pairId,
113:         Perp.SqrtPerpAssetStatus memory assetStatus,
114:         mapping(uint256 => DataType.RebalanceFeeGrowthCache) storage rebalanceFeeGrowthCache,
115:         Perp.UserStatus memory userStatus
116:     ) internal view returns (int256 rebalanceInterestBase, int256 rebalanceInterestQuote) {

136:     function settleRebalanceInterest(
137:         uint256 pairId,
138:         Perp.SqrtPerpAssetStatus storage assetStatus,
139:         mapping(uint256 => DataType.RebalanceFeeGrowthCache) storage rebalanceFeeGrowthCache,
140:         Perp.UserStatus storage userStatus
141:     ) internal returns (int256 rebalanceInterestBase, int256 rebalanceInterestQuote) {
```

- *PositionCalculator.sol* ( [34-38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L34-L38), [49-53](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L49-L53), [63-67](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L63-L67), [75-79](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L75-L79), [102-102](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L102-L102), [117-122](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L117-L122), [135-135](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L135-L135), [141-141](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L141-L141), [151-154](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L151-L154), [163-166](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L163-L166), [175-175](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L175-L175), [186-189](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L186-L189), [231-231](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L231-L231), [238-241](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L238-L241) ):

```solidity
34:     function isLiquidatable(
35:         DataType.PairStatus memory pairStatus,
36:         DataType.Vault memory _vault,
37:         DataType.FeeAmount memory feeAmount
38:     ) internal view returns (bool _isLiquidatable, int256 minMargin, int256 vaultValue, uint256 sqrtOraclePrice) {

49:     function checkSafe(
50:         DataType.PairStatus memory pairStatus,
51:         DataType.Vault memory _vault,
52:         DataType.FeeAmount memory feeAmount
53:     ) internal view returns (int256 minMargin) {

63:     function getIsSafe(
64:         DataType.PairStatus memory pairStatus,
65:         DataType.Vault memory _vault,
66:         DataType.FeeAmount memory feeAmount
67:     ) internal view returns (int256 minMargin, bool isSafe, bool hasPosition) {

75:     function calculateMinMargin(
76:         DataType.PairStatus memory pairStatus,
77:         DataType.Vault memory vault,
78:         DataType.FeeAmount memory feeAmount
79:     ) internal view returns (int256 minMargin, int256 vaultValue, bool hasPosition, uint256 sqrtOraclePrice) {

102:     function calculateRequiredCollateralWithDebt(uint128 debtRiskRatio) internal pure returns (uint256) {

117:     function calculateMinValue(
118:         int256 marginAmount,
119:         PositionParams memory positionParams,
120:         uint256 sqrtPrice,
121:         uint256 riskRatio
122:     ) internal pure returns (int256 minValue, int256 vaultValue, uint256 debtValue, bool hasPosition) {

135:     function getHasPosition(DataType.Vault memory _vault) internal pure returns (bool hasPosition) {

141:     function getSqrtIndexPrice(DataType.PairStatus memory pairStatus) internal view returns (uint256 sqrtPriceX96) {

151:     function getPositionWithFeeAmount(Perp.UserStatus memory perpUserStatus, DataType.FeeAmount memory feeAmount)
152:         internal
153:         pure
154:         returns (PositionParams memory positionParams)

163:     function getPosition(Perp.UserStatus memory _perpUserStatus)
164:         internal
165:         pure
166:         returns (PositionParams memory positionParams)

175:     function getHasPositionFlag(PositionParams memory _positionParams) internal pure returns (bool) {

186:     function calculateMinValue(uint256 _sqrtPrice, PositionParams memory _positionParams, uint256 _riskRatio)
187:         internal
188:         pure
189:         returns (int256 minValue)

231:     function calculateValue(uint256 _sqrtPrice, PositionParams memory _positionParams) internal pure returns (int256) {

238:     function calculateSquartDebtValue(uint256 _sqrtPrice, PositionParams memory positionParams)
239:         internal
240:         pure
241:         returns (uint256)
```

- *PremiumCurveModel.sol* ( [14-14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PremiumCurveModel.sol#L14-L14) ):

```solidity
14:     function calculatePremiumCurve(uint256 utilization) internal pure returns (uint256) {
```

- *Reallocation.sol* ( [18-21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L18-L21), [92-92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L92-L92), [109-109](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L109-L109), [126-131](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L126-L131), [147-152](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L147-L152), [165-168](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L165-L168), [179-182](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L179-L182) ):

```solidity
18:     function getNewRange(DataType.PairStatus memory _assetStatusUnderlying, int24 currentTick)
19:         internal
20:         view
21:         returns (int24 lower, int24 upper)

92:     function isInRange(Perp.SqrtPerpAssetStatus memory sqrtAssetStatus) internal view returns (bool) {

109:     function calculateUsableTick(int24 _tick, int24 tickSpacing) internal pure returns (int24 result) {

126:     function calculateMinLowerTick(
127:         int24 currentLowerTick,
128:         uint256 available,
129:         uint256 liquidityAmount,
130:         int24 tickSpacing
131:     ) internal pure returns (int24 minLowerTick) {

147:     function calculateMaxUpperTick(
148:         int24 currentUpperTick,
149:         uint256 available,
150:         uint256 liquidityAmount,
151:         int24 tickSpacing
152:     ) internal pure returns (int24 maxUpperTick) {

165:     function calculateAmount1ForLiquidity(uint160 sqrtRatioA, uint256 available, uint256 liquidityAmount)
166:         internal
167:         pure
168:         returns (uint160)

179:     function calculateAmount0ForLiquidity(uint160 sqrtRatioB, uint256 available, uint256 liquidityAmount)
180:         internal
181:         pure
182:         returns (uint160)
```

- *ScaledAsset.sol* ( [29-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L29-L29), [33-33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L33-L33), [37-37](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L37-L37), [47-49](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L47-L49), [72-72](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L72-L72), [76-82](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L76-L82), [130-133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L130-L133), [142-144](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L142-L144), [155-158](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L155-L158), [170-173](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L170-L173), [186-188](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L186-L188), [217-217](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L217-L217), [222-222](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L222-L222), [226-226](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L226-L226), [230-230](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L230-L230) ):

```solidity
29:     function createAssetStatus() internal pure returns (AssetStatus memory) {

33:     function createUserStatus() internal pure returns (UserStatus memory) {

37:     function addAsset(AssetStatus storage tokenState, uint256 _amount) internal returns (uint256 claimAmount) {

47:     function removeAsset(AssetStatus storage tokenState, uint256 _supplyTokenAmount, uint256 _amount)
48:         internal
49:         returns (uint256 finalBurnAmount, uint256 finalWithdrawAmount)

72:     function isSameSign(int256 a, int256 b) internal pure returns (bool) {

76:     function updatePosition(
77:         ScaledAsset.AssetStatus storage tokenStatus,
78:         ScaledAsset.UserStatus storage userStatus,
79:         int256 _amount,
80:         uint256 _pairId,
81:         bool _isStable
82:     ) internal {

130:     function computeUserFee(ScaledAsset.AssetStatus memory _assetStatus, ScaledAsset.UserStatus memory _userStatus)
131:         internal
132:         pure
133:         returns (int256 interestFee)

142:     function settleUserFee(ScaledAsset.AssetStatus memory _assetStatus, ScaledAsset.UserStatus storage _userStatus)
143:         internal
144:         returns (int256 interestFee)

155:     function getAssetFee(AssetStatus memory tokenState, UserStatus memory accountState)
156:         internal
157:         pure
158:         returns (uint256)

170:     function getDebtFee(AssetStatus memory tokenState, UserStatus memory accountState)
171:         internal
172:         pure
173:         returns (uint256)

186:     function updateScaler(AssetStatus storage tokenState, uint256 _interestRate, uint8 _reserveFactor)
187:         internal
188:         returns (uint256)

217:     function getTotalCollateralValue(AssetStatus memory tokenState) internal pure returns (uint256) {

222:     function getTotalDebtValue(AssetStatus memory tokenState) internal pure returns (uint256) {

226:     function getAvailableCollateralValue(AssetStatus memory tokenState) internal pure returns (uint256) {

230:     function getUtilizationRatio(AssetStatus memory tokenState) internal pure returns (uint256) {
```

- *SlippageLib.sol* ( [21-26](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/SlippageLib.sol#L21-L26) ):

```solidity
21:     function checkPrice(
22:         uint256 sqrtBasePrice,
23:         IPredyPool.TradeResult memory tradeResult,
24:         uint256 slippageTolerance,
25:         uint256 maxAcceptableSqrtPriceRange
26:     ) internal pure {
```

- *Trade.sol* ( [76-83](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L76-L83), [112-112](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L112-L112), [116-116](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L116-L116), [122-127](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L122-L127), [135-139](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L135-L139) ):

```solidity
76:     function swap(
77:         GlobalDataLibrary.GlobalData storage globalData,
78:         uint256 pairId,
79:         SwapStableResult memory swapParams,
80:         bytes memory settlementData,
81:         uint256 sqrtPrice,
82:         uint256 vaultId
83:     ) internal returns (SwapStableResult memory) {

112:     function getSqrtPrice(address uniswapPoolAddress, bool isQuoteZero) internal view returns (uint256 sqrtPriceX96) {

116:     function calculateStableAmount(uint256 currentSqrtPrice, uint256 baseAmount) internal pure returns (uint256) {

122:     function divToStable(
123:         SwapStableResult memory swapParams,
124:         int256 amountBase,
125:         int256 amountQuote,
126:         int256 totalAmountStable
127:     ) internal pure returns (SwapStableResult memory swapResult) {

135:     function settleUserBalanceAndFee(
136:         DataType.PairStatus storage _pairStatus,
137:         mapping(uint256 => DataType.RebalanceFeeGrowthCache) storage rebalanceFeeGrowthCache,
138:         Perp.UserStatus storage _userStatus
139:     ) internal returns (DataType.FeeAmount memory realizedFee) {
```

- *UniHelper.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L13-L13), [20-20](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L20-L20), [27-27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L27-L27), [35-35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L35-L35), [77-77](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L77-L77), [87-90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L87-L90), [99-102](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L99-L102) ):

```solidity
13:     function getSqrtPrice(address uniswapPoolAddress) internal view returns (uint160 sqrtPrice) {

20:     function getSqrtTWAP(address uniswapPoolAddress) internal view returns (uint160 sqrtTwapX96) {

27:     function convertSqrtPrice(uint160 sqrtPriceX96, bool isQuoteZero) internal pure returns (uint160) {

35:     function callUniswapObserve(IUniswapV3Pool uniswapPool, uint256 ago) internal view returns (uint160, uint256) {

77:     function revertBytes(bytes memory errMsg) internal pure {

87:     function getFeeGrowthInsideLast(address uniswapPoolAddress, int24 tickLower, int24 tickUpper)
88:         internal
89:         view
90:         returns (uint256 feeGrowthInside0LastX128, uint256 feeGrowthInside1LastX128)

99:     function getFeeGrowthInside(address uniswapPoolAddress, int24 tickLower, int24 tickUpper)
100:         internal
101:         view
102:         returns (uint256 feeGrowthInside0X128, uint256 feeGrowthInside1X128)
```

- *VaultLib.sol* ( [11-14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/VaultLib.sol#L11-L14), [24-26](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/VaultLib.sol#L24-L26) ):

```solidity
11:     function getVault(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId)
12:         internal
13:         view
14:         returns (DataType.Vault storage vault)

24:     function createOrGetVault(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId, uint256 pairId)
25:         internal
26:         returns (uint256)
```

- *AddPairLogic.sol* ( [192-192](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L192-L192), [205-205](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L205-L205), [209-209](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L209-L209), [213-213](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L213-L213), [219-219](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L219-L219) ):

```solidity
192:     function deploySupplyToken(address _tokenAddress) internal returns (address) {

205:     function validateFeeRatio(uint8 _fee) internal pure {

209:     function validatePoolOwner(address _poolOwner) internal pure {

213:     function validateRiskParams(Perp.AssetRiskParams memory _assetRiskParams) internal pure {

219:     function validateIRMParams(InterestRateModel.IRMParams memory _irmParams) internal pure {
```

- *LiquidationLogic.sol* ( [129-133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L129-L133), [159-162](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L159-L162) ):

```solidity
129:     function checkVaultIsDanger(
130:         DataType.PairStatus memory pairStatus,
131:         DataType.Vault memory vault,
132:         mapping(uint256 => DataType.RebalanceFeeGrowthCache) storage rebalanceFeeGrowthCache
133:     ) internal view returns (uint256 sqrtOraclePrice, uint256 slippageTolerance) {

159:     function calculateSlippageTolerance(int256 minMargin, int256 vaultValue, Perp.AssetRiskParams memory riskParams)
160:         internal
161:         pure
162:         returns (uint256)
```

- *ReaderLogic.sol* ( [43-46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L43-L46), [56-56](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L56-L56), [64-64](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L64-L64) ):

```solidity
43:     function getPosition(DataType.Vault memory vault, DataType.FeeAmount memory feeAmount)
44:         internal
45:         pure
46:         returns (IPredyPool.Position memory)

56:     function revertPairStatus(DataType.PairStatus memory pairStatus) internal pure {

64:     function revertVaultStatus(IPredyPool.VaultStatus memory vaultStatus) internal pure {
```

- *SupplyLogic.sol* ( [46-48](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L46-L48), [79-81](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L79-L81) ):

```solidity
46:     function receiveTokenAndMintBond(Perp.AssetPoolStatus storage _pool, uint256 _amount)
47:         internal
48:         returns (uint256 mintAmount)

79:     function burnBondAndTransferToken(Perp.AssetPoolStatus storage _pool, uint256 _amount)
80:         internal
81:         returns (uint256 finalburntAmount, uint256 finalWithdrawalAmount)
```

- *TradeLogic.sol* ( [68-72](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/TradeLogic.sol#L68-L72) ):

```solidity
68:     function callTradeAfterCallback(
69:         GlobalDataLibrary.GlobalData storage globalData,
70:         IPredyPool.TradeParams memory tradeParams,
71:         IPredyPool.TradeResult memory tradeResult
72:     ) internal {
```

- *Bps.sol* ( [7-7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Bps.sol#L7-L7), [11-11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Bps.sol#L11-L11) ):

```solidity
7:     function upper(uint256 price, uint256 bps) internal pure returns (uint256) {

11:     function lower(uint256 price, uint256 bps) internal pure returns (uint256) {
```

- *LPMath.sol* ( [10-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L10-L13), [20-23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L20-L23), [30-35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L30-L35), [68-73](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L68-L73), [108-111](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L108-L111), [119-122](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L119-L122), [134-137](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L134-L137), [145-148](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L145-L148) ):

```solidity
10:     function calculateAmount0ForLiquidityWithTicks(int24 tickA, int24 tickB, uint256 liquidityAmount, bool isRoundUp)
11:         internal
12:         pure
13:         returns (int256)

20:     function calculateAmount1ForLiquidityWithTicks(int24 tickA, int24 tickB, uint256 liquidityAmount, bool isRoundUp)
21:         internal
22:         pure
23:         returns (int256)

30:     function calculateAmount0ForLiquidity(
31:         uint160 sqrtRatioA,
32:         uint160 sqrtRatioB,
33:         uint256 liquidityAmount,
34:         bool isRoundUp
35:     ) internal pure returns (int256) {

68:     function calculateAmount1ForLiquidity(
69:         uint160 sqrtRatioA,
70:         uint160 sqrtRatioB,
71:         uint256 liquidityAmount,
72:         bool isRoundUp
73:     ) internal pure returns (int256) {

108:     function calculateAmount0OffsetWithTick(int24 upper, uint256 liquidityAmount, bool isRoundUp)
109:         internal
110:         pure
111:         returns (int256)

119:     function calculateAmount0Offset(uint160 sqrtRatio, uint256 liquidityAmount, bool isRoundUp)
120:         internal
121:         pure
122:         returns (uint256)

134:     function calculateAmount1OffsetWithTick(int24 lower, uint256 liquidityAmount, bool isRoundUp)
135:         internal
136:         pure
137:         returns (int256)

145:     function calculateAmount1Offset(uint160 sqrtRatio, uint256 liquidityAmount, bool isRoundUp)
146:         internal
147:         pure
148:         returns (uint256)
```

- *Math.sol* ( [12-12](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L12-L12), [16-16](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L16-L16), [20-20](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L20-L20), [24-24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L24-L24), [34-34](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L34-L34), [44-44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L44-L44), [54-54](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L54-L54), [62-62](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L62-L62) ):

```solidity
12:     function abs(int256 x) internal pure returns (uint256) {

16:     function max(uint256 a, uint256 b) internal pure returns (uint256) {

20:     function min(uint256 a, uint256 b) internal pure returns (uint256) {

24:     function fullMulDivInt256(int256 x, uint256 y, uint256 z) internal pure returns (int256) {

34:     function fullMulDivDownInt256(int256 x, uint256 y, uint256 z) internal pure returns (int256) {

44:     function mulDivDownInt256(int256 x, uint256 y, uint256 z) internal pure returns (int256) {

54:     function addDelta(uint256 a, int256 b) internal pure returns (uint256) {

62:     function calSqrtPriceToPrice(uint256 sqrtPrice) internal pure returns (uint256 price) {
```

- *DecayLib.sol* ( [8-11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/DecayLib.sol#L8-L11), [16-19](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/DecayLib.sol#L16-L19) ):

```solidity
8:     function decay(uint256 startPrice, uint256 endPrice, uint256 decayStartTime, uint256 decayEndTime)
9:         internal
10:         view
11:         returns (uint256 decayedPrice)

16:     function decay2(uint256 startPrice, uint256 endPrice, uint256 decayStartTime, uint256 decayEndTime, uint256 value)
17:         internal
18:         pure
19:         returns (uint256 decayedPrice)
```

- *OrderInfoLib.sol* ( [18-18](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/OrderInfoLib.sol#L18-L18) ):

```solidity
18:     function hash(OrderInfo memory info) internal pure returns (bytes32) {
```

- *Permit2Lib.sol* ( [10-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/Permit2Lib.sol#L10-L13), [23-26](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/Permit2Lib.sol#L23-L26) ):

```solidity
10:     function toPermit(ResolvedOrder memory order)
11:         internal
12:         pure
13:         returns (ISignatureTransfer.PermitTransferFrom memory)

23:     function transferDetails(ResolvedOrder memory order, address to)
24:         internal
25:         pure
26:         returns (ISignatureTransfer.SignatureTransferDetails memory)
```

- *ResolvedOrder.sol* ( [23-23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/ResolvedOrder.sol#L23-L23) ):

```solidity
23:     function validate(ResolvedOrder memory resolvedOrder) internal view {
```

- *L2Decoder.sol* ( [5-15](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L5-L15), [38-41](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L38-L41), [50-53](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L50-L53) ):

```solidity
5:     function decodeSpotOrderParams(bytes32 args1, bytes32 args2)
6:         internal
7:         pure
8:         returns (
9:             bool isLimit,
10:             uint64 startTime,
11:             uint64 endTime,
12:             uint64 deadline,
13:             uint128 startAmount,
14:             uint128 endAmount
15:         )

38:     function decodePerpOrderParams(bytes32 args)
39:         internal
40:         pure
41:         returns (uint64 deadline, uint64 pairId, uint8 leverage)

50:     function decodePerpOrderV3Params(bytes32 args)
51:         internal
52:         pure
53:         returns (uint64 deadline, uint64 pairId, uint8 leverage, bool reduceOnly, bool closePosition, bool side)
```

- *ArrayLib.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/ArrayLib.sol#L5-L5), [9-9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/ArrayLib.sol#L9-L9), [15-15](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/ArrayLib.sol#L15-L15), [20-20](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/ArrayLib.sol#L20-L20) ):

```solidity
5:     function addItem(uint256[] storage items, uint256 item) internal {

9:     function removeItem(uint256[] storage items, uint256 item) internal {

15:     function removeItemByIndex(uint256[] storage items, uint256 index) internal {

20:     function getItemIndex(uint256[] memory items, uint256 item) internal pure returns (uint256) {
```

- *GammaOrder.sol* ( [43-43](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L43-L43), [115-115](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L115-L115), [134-134](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L134-L134) ):

```solidity
43:     function hash(GammaModifyInfo memory info) internal pure returns (bytes32) {

115:     function hash(GammaOrder memory order) internal pure returns (bytes32) {

134:     function resolve(GammaOrder memory gammaOrder, bytes memory sig) internal pure returns (ResolvedOrder memory) {
```

- *GammaTradeMarketLib.sol* ( [48-51](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L48-L51), [141-144](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L141-L144), [167-170](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L167-L170) ):

```solidity
48:     function calculateDelta(uint256 _sqrtPrice, int64 maximaDeviation, int256 _sqrtAmount, int256 perpAmount)
49:         internal
50:         pure
51:         returns (int256)

141:     function calculateSlippageTolerance(uint256 startTime, uint256 currentTime, AuctionParams memory auctionParams)
142:         internal
143:         pure
144:         returns (uint256)

167:     function calculateSlippageToleranceByPrice(uint256 price1, uint256 price2, AuctionParams memory auctionParams)
168:         internal
169:         pure
170:         returns (uint256)
```

- *L2GammaDecoder.sol* ( [7-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L7-L10), [38-41](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L38-L41), [51-63](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L51-L63) ):

```solidity
7:     function decodeGammaModifyInfo(bytes32 args, uint256 lowerLimit, uint256 upperLimit, int64 maximaDeviation)
8:         internal
9:         pure
10:         returns (GammaModifyInfo memory)

38:     function decodeGammaParam(bytes32 args)
39:         internal
40:         pure
41:         returns (uint64 deadline, uint64 pairId, uint32 slippageTolerance, uint8 leverage)

51:     function decodeGammaModifyParam(bytes32 args)
52:         internal
53:         pure
54:         returns (
55:             bool isEnabled,
56:             uint64 expiration,
57:             uint32 hedgeInterval,
58:             uint32 sqrtPriceTrigger,
59:             uint32 minSlippageTolerance,
60:             uint32 maxSlippageTolerance,
61:             uint16 auctionPeriod,
62:             uint32 auctionRange
63:         )
```

- *PerpMarketLib.sol* ( [26-32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L26-L32), [80-86](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L80-L86), [118-121](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L118-L121), [138-144](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L138-L144), [178-178](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L178-L178), [188-191](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L188-L191) ):

```solidity
26:     function getFinalTradeAmount(
27:         int256 currentPositionAmount,
28:         string memory side,
29:         uint256 quantity,
30:         bool reduceOnly,
31:         bool closePosition
32:     ) internal pure returns (int256 finalTradeAmount) {

80:     function validateTrade(
81:         IPredyPool.TradeResult memory tradeResult,
82:         int256 tradeAmount,
83:         uint256 limitPrice,
84:         uint256 stopPrice,
85:         bytes memory auctionData
86:     ) internal view {

118:     function validateLimitPrice(uint256 tradePrice, int256 tradeAmount, uint256 limitPrice)
119:         internal
120:         pure
121:         returns (bool)

138:     function validateStopPrice(
139:         uint256 oraclePrice,
140:         uint256 tradePrice,
141:         int256 tradeAmount,
142:         uint256 stopPrice,
143:         bytes memory auctionData
144:     ) internal pure returns (bool) {

178:     function ratio(uint256 price1, uint256 price2) internal pure returns (uint256) {

188:     function validateMarketOrder(uint256 tradePrice, int256 tradeAmount, bytes memory auctionData)
189:         internal
190:         view
191:         returns (bool)
```

- *PerpOrder.sol* ( [54-54](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L54-L54), [73-73](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L73-L73) ):

```solidity
54:     function hash(PerpOrder memory order) internal pure returns (bytes32) {

73:     function resolve(PerpOrder memory perpOrder, bytes memory sig) internal pure returns (ResolvedOrder memory) {
```

- *PerpOrderV3.sol* ( [58-58](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L58-L58), [78-78](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L78-L78) ):

```solidity
58:     function hash(PerpOrderV3 memory order) internal pure returns (bytes32) {

78:     function resolve(PerpOrderV3 memory perpOrder, bytes memory sig) internal pure returns (ResolvedOrder memory) {
```

- *GlobalData.sol* ( [26-26](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L26-L26), [30-30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L30-L30), [35-35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L35-L35), [46-50](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L46-L50), [62-64](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L62-L64), [72-74](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L72-L74), [88-90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L88-L90) ):

```solidity
26:     function validateVaultId(GlobalDataLibrary.GlobalData storage globalData, uint256 vaultId) internal view {

30:     function validate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal view {

35:     function initializeLock(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId) internal {

46:     function callSettlementCallback(
47:         GlobalDataLibrary.GlobalData storage globalData,
48:         bytes memory settlementData,
49:         int256 deltaBaseAmount
50:     ) internal {

62:     function finalizeLock(GlobalDataLibrary.GlobalData storage globalData)
63:         internal
64:         returns (int256 paidQuote, int256 paidBase)

72:     function take(GlobalDataLibrary.GlobalData storage globalData, bool isQuoteAsset, address to, uint256 amount)
73:         internal
74:     {

88:     function settle(GlobalDataLibrary.GlobalData storage globalData, bool isQuoteAsset)
89:         internal
90:         returns (int256 paid)
```

</details>

### [N-04] Names of `private`/`internal` state variables should be prefixed with an underscore

It is recommended by the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.20/style-guide.html#underscore-prefix-for-non-external-functions-and-variables).

There are 3 instances:

- *PriceFeed.sol* ( [35-35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L35-L35) ):

```solidity
35:     uint256 private constant VALID_TIME_PERIOD = 5 * 60;
```

- *GammaTradeMarket.sol* ( [50-50](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L50-L50), [51-51](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L51-L51) ):

```solidity
50:     mapping(address owner => uint256[]) internal positionIDs;

51:     mapping(uint256 positionId => GammaTradeMarketLib.UserPosition) internal userPositions;
```

### [N-05] Redundant inheritance specifier

The contracts below already extend the specified contract, so there is no need to list it in the inheritance list again.

There are 2 instances:

- *PredyPool.sol* ( [28-28](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L28-L28) ):

```solidity
/// @audit ReentrancyGuardUpgradeable already extends Initializable
28: contract PredyPool is IPredyPool, IUniswapV3MintCallback, Initializable, ReentrancyGuardUpgradeable {
```

- *GammaTradeMarket.sol* ( [24-24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L24-L24) ):

```solidity
/// @audit BaseMarketUpgradable already extends IFillerMarket
24: contract GammaTradeMarket is IFillerMarket, BaseMarketUpgradable, ReentrancyGuardUpgradeable {
```

### [N-06] Use of `override` is unnecessary

[Starting from Solidity 0.8.8](https://docs.soliditylang.org/en/v0.8.20/contracts.html#function-overriding), the override keyword is not required when overriding an interface function, except for the case where the function is defined in multiple bases.

<details>
<summary>There are 10 instances (click to show):</summary>

- *PredyPool.sol* ( [78-78](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L78-L78) ):

```solidity
78:     function uniswapV3MintCallback(uint256 amount0, uint256 amount1, bytes calldata) external override {
```

- *GammaTradeMarket.sol* ( [79-82](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L79-L82), [138-142](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L138-L142) ):

```solidity
79:     function predyTradeAfterCallback(
80:         IPredyPool.TradeParams memory tradeParams,
81:         IPredyPool.TradeResult memory tradeResult
82:     ) external override(BaseHookCallbackUpgradable) onlyPredyPool {

138:     function execLiquidationCall(
139:         uint256 vaultId,
140:         uint256 closeRatio,
141:         IFillerMarket.SettlementParamsV3 memory settlementParams
142:     ) external override returns (IPredyPool.TradeResult memory tradeResult) {
```

- *PerpMarketV1.sol* ( [102-105](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L102-L105) ):

```solidity
102:     function predyTradeAfterCallback(
103:         IPredyPool.TradeParams memory tradeParams,
104:         IPredyPool.TradeResult memory tradeResult
105:     ) external override(BaseHookCallbackUpgradable) onlyPredyPool {
```

- *UniswapSettlement.sol* ( [22-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L22-L29), [38-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L38-L45), [58-58](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L58-L58), [62-62](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L62-L62) ):

```solidity
22:     function swapExactIn(
23:         address,
24:         address baseToken,
25:         bytes memory data,
26:         uint256 amountIn,
27:         uint256 amountOutMinimum,
28:         address recipient
29:     ) external override returns (uint256 amountOut) {

38:     function swapExactOut(
39:         address quoteToken,
40:         address,
41:         bytes memory data,
42:         uint256 amountOut,
43:         uint256 amountInMaximum,
44:         address recipient
45:     ) external override returns (uint256 amountIn) {

58:     function quoteSwapExactIn(bytes memory data, uint256 amountIn) external override returns (uint256 amountOut) {

62:     function quoteSwapExactOut(bytes memory data, uint256 amountOut) external override returns (uint256 amountIn) {
```

- *SupplyToken.sol* ( [21-21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L21-L21), [25-25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L25-L25) ):

```solidity
21:     function mint(address account, uint256 amount) external virtual override onlyController {

25:     function burn(address account, uint256 amount) external virtual override onlyController {
```

</details>

### [N-07] Add inline comments for unnamed parameters

`function func(address a, address)` -> `function func(address a, address /* b */)`

There are 3 instances:

- *PredyPool.sol* ( [78-78](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L78-L78) ):

```solidity
78:     function uniswapV3MintCallback(uint256 amount0, uint256 amount1, bytes calldata) external override {
```

- *UniswapSettlement.sol* ( [22-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L22-L29), [38-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L38-L45) ):

```solidity
22:     function swapExactIn(
23:         address,
24:         address baseToken,
25:         bytes memory data,
26:         uint256 amountIn,
27:         uint256 amountOutMinimum,
28:         address recipient
29:     ) external override returns (uint256 amountOut) {

38:     function swapExactOut(
39:         address quoteToken,
40:         address,
41:         bytes memory data,
42:         uint256 amountOut,
43:         uint256 amountInMaximum,
44:         address recipient
45:     ) external override returns (uint256 amountIn) {
```

### [N-08] Consider providing a ranged getter for array state variables

While the compiler automatically provides a getter for accessing single elements within a public state variable array, it doesn't provide a way to fetch the whole array, or subsets thereof. Consider adding a function to allow the fetching of slices of the array, especially if the contract doesn't already have multicall functionality.

There is 1 instance:

- *GammaTradeMarket.sol* ( [50-50](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L50-L50) ):

```solidity
50:     mapping(address owner => uint256[]) internal positionIDs;
```

### [N-09] Assembly blocks should have extensive comments

Assembly blocks take a lot more time to audit than normal Solidity code, and often have gotchas and side-effects that the Solidity versions of the same code do not. Consider adding more comments explaining what is being done in every step of the assembly code, and describe why assembly is being used instead of Solidity.

<details>
<summary>There are 11 instances (click to show):</summary>

- *BaseMarket.sol* ( [117-119](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L117-L119) ):

```solidity
117:         assembly {
118:             revert(add(32, data), mload(data))
119:         }
```

- *BaseMarketUpgradable.sol* ( [165-167](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L165-L167) ):

```solidity
165:         assembly {
166:             revert(add(32, data), mload(data))
167:         }
```

- *UniHelper.sol* ( [79-81](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L79-L81) ):

```solidity
79:             assembly {
80:                 revert(add(32, errMsg), mload(errMsg))
81:             }
```

- *ReaderLogic.sol* ( [59-61](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L59-L61), [67-69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L67-L69) ):

```solidity
59:         assembly {
60:             revert(add(32, data), mload(data))
61:         }

67:         assembly {
68:             revert(add(32, data), mload(data))
69:         }
```

- *L2Decoder.sol* ( [19-24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L19-L24), [32-35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L32-L35), [43-47](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L43-L47), [59-66](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L59-L66) ):

```solidity
19:         assembly {
20:             deadline := and(args1, 0xFFFFFFFFFFFFFFFF)
21:             startTime := and(shr(64, args1), 0xFFFFFFFFFFFFFFFF)
22:             endTime := and(shr(128, args1), 0xFFFFFFFFFFFFFFFF)
23:             isLimitUint := and(shr(192, args1), 0xFFFFFFFF)
24:         }

32:         assembly {
33:             startAmount := and(args2, 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF)
34:             endAmount := and(shr(128, args2), 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF)
35:         }

43:         assembly {
44:             deadline := and(args, 0xFFFFFFFFFFFFFFFF)
45:             pairId := and(shr(64, args), 0xFFFFFFFFFFFFFFFF)
46:             leverage := and(shr(128, args), 0xFF)
47:         }

59:         assembly {
60:             deadline := and(args, 0xFFFFFFFFFFFFFFFF)
61:             pairId := and(shr(64, args), 0xFFFFFFFFFFFFFFFF)
62:             leverage := and(shr(128, args), 0xFF)
63:             reduceOnlyUint := and(shr(136, args), 0xFF)
64:             closePositionUint := and(shr(144, args), 0xFF)
65:             sideUint := and(shr(152, args), 0xFF)
66:         }
```

- *L2GammaDecoder.sol* ( [43-48](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L43-L48), [67-76](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L67-L76) ):

```solidity
43:         assembly {
44:             deadline := and(args, 0xFFFFFFFFFFFFFFFF)
45:             pairId := and(shr(64, args), 0xFFFFFFFFFFFFFFFF)
46:             slippageTolerance := and(shr(128, args), 0xFFFFFFFF)
47:             leverage := and(shr(160, args), 0xFF)
48:         }

67:         assembly {
68:             expiration := and(args, 0xFFFFFFFFFFFFFFFF)
69:             hedgeInterval := and(shr(64, args), 0xFFFFFFFF)
70:             sqrtPriceTrigger := and(shr(96, args), 0xFFFFFFFF)
71:             minSlippageTolerance := and(shr(128, args), 0xFFFFFFFF)
72:             maxSlippageTolerance := and(shr(160, args), 0xFFFFFFFF)
73:             auctionRange := and(shr(192, args), 0xFFFFFFFF)
74:             isEnabledUint := and(shr(224, args), 0xFFFF)
75:             auctionPeriod := and(shr(240, args), 0xFFFF)
76:         }
```

</details>

### [N-10] Consider splitting complex checks into multiple steps

Assign the expression's parts to intermediate local variables, and check against those instead.

There are 2 instances:

- *GammaTradeMarket.sol* ( [212-212](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L212-L212), [395-395](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L395-L395) ):

```solidity
212:         if (gammaOrder.quantity != 0 || gammaOrder.quantitySqrt != 0 || gammaOrder.marginAmount != 0) {

395:         if (vault.margin != 0 || vault.openPosition.perp.amount != 0 || vault.openPosition.sqrtPerp.amount != 0) {
```

### [N-11] Missing checks for empty bytes when updating bytes state variables

Unless the code is attempting to `delete` the state variable, the caller shouldn't have to write `""` to the state variable

There is 1 instance:

- *PriceFeed.sol* ( [40-40](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L40-L40) ):

```solidity
40:         _priceId = priceId;
```

### [N-12] Complex casting

Consider whether the number of casts is really necessary, or whether using a different type would be more appropriate. Alternatively, add comments to explain in detail why the casts are necessary, and any implicit reasons why the cast does not introduce an overflow.

There is 1 instance:

- *UniHelper.sol* ( [70-70](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L70-L70) ):

```solidity
70:         int24 tick = int24((tickCumulatives[1] - tickCumulatives[0]) / int56(int256(ago)));
```

### [N-13] Complex math should be split into multiple steps

Consider splitting long arithmetic calculations into multiple steps to improve the code readability.

<details>
<summary>There are 5 instances (click to show):</summary>

- *Perp.sol* ( [398-400](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L398-L400), [401-403](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L401-L403) ):

```solidity
398:         _assetStatus.fee0Growth += FullMath.mulDiv(
399:             f0, _assetStatus.totalAmount + _assetStatus.borrowedAmount * spreadParam / 1000, _assetStatus.totalAmount
400:         );

401:         _assetStatus.fee1Growth += FullMath.mulDiv(
402:             f1, _assetStatus.totalAmount + _assetStatus.borrowedAmount * spreadParam / 1000, _assetStatus.totalAmount
403:         );
```

- *LiquidationLogic.sol* ( [59-65](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L59-L65) ):

```solidity
59:         IPredyPool.TradeParams memory tradeParams = IPredyPool.TradeParams(
60:             vault.openPosition.pairId,
61:             vaultId,
62:             -vault.openPosition.perp.amount * int256(closeRatio) / 1e18,
63:             -vault.openPosition.sqrtPerp.amount * int256(closeRatio) / 1e18,
64:             ""
65:         );
```

- *DecayLib.sol* ( [32-32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/DecayLib.sol#L32-L32), [34-34](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/DecayLib.sol#L34-L34) ):

```solidity
32:                 decayedPrice = startPrice - (startPrice - endPrice) * elapsed / duration;

34:                 decayedPrice = startPrice + (endPrice - startPrice) * elapsed / duration;
```

</details>

### [N-14] Consider adding a block/deny-list

Doing so will significantly increase centralization, but will help to prevent hackers from using stolen tokens

There are 4 instances:

- *PredyPool.sol* ( [28](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L28) ):

```solidity
28: contract PredyPool is IPredyPool, IUniswapV3MintCallback, Initializable, ReentrancyGuardUpgradeable {
```

- *GammaTradeMarket.sol* ( [24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L24) ):

```solidity
24: contract GammaTradeMarket is IFillerMarket, BaseMarketUpgradable, ReentrancyGuardUpgradeable {
```

- *PerpMarketV1.sol* ( [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L29) ):

```solidity
29: contract PerpMarketV1 is BaseMarketUpgradable, ReentrancyGuardUpgradeable {
```

- *UniswapSettlement.sol* ( [10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L10) ):

```solidity
10: contract UniswapSettlement is ISettlement {
```

### [N-15] Constants/Immutables redefined elsewhere

Consider defining in only one contract so that values cannot become out of sync when only one location is updated. A [cheap way](https://medium.com/coinmonks/gas-cost-of-solidity-library-functions-dbe0cedd4678) to store constants/immutables in a single location is to create an `internal constant` in a `library`. If the variable is a local cache of another contract's value, consider making the cache variable internal or private, which will require external users to query the contract with the source of truth, so that callers don't get out of sync.

<details>
<summary>There are 12 instances (click to show):</summary>

- *PriceFeed.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L10-L10), [31-31](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L31-L31) ):

```solidity
/// @audit Seen in ./src/PriceFeed.sol#31
10:     address private immutable _pyth;

/// @audit Seen in ./src/PriceFeed.sol#10
31:     address private immutable _pyth;
```

- *Constants.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Constants.sol#L5-L5) ):

```solidity
/// @audit Seen in ./src/libraries/math/Bps.sol#5
5:     uint256 internal constant ONE = 1e18;
```

- *Bps.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Bps.sol#L5-L5) ):

```solidity
/// @audit Seen in ./src/libraries/Constants.sol#5
5:     uint32 public constant ONE = 1e6;
```

- *GammaOrder.sol* ( [97-98](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L97-L98), [101-101](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L101-L101), [102-110](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L102-L110) ):

```solidity
/// @audit Seen in ./src/markets/perp/PerpOrder.sol#43
97:     bytes internal constant ORDER_TYPE =
98:         abi.encodePacked(GAMMA_ORDER_TYPE, GammaModifyInfoLib.GAMMA_MODIFY_INFO_TYPE, OrderInfoLib.ORDER_INFO_TYPE);

/// @audit Seen in ./src/markets/perp/PerpOrder.sol#46
101:     string internal constant TOKEN_PERMISSIONS_TYPE = "TokenPermissions(address token,uint256 amount)";

/// @audit Seen in ./src/markets/perp/PerpOrder.sol#47
102:     string internal constant PERMIT2_ORDER_TYPE = string(
103:         abi.encodePacked(
104:             "GammaOrder witness)",
105:             GammaModifyInfoLib.GAMMA_MODIFY_INFO_TYPE,
106:             GAMMA_ORDER_TYPE,
107:             OrderInfoLib.ORDER_INFO_TYPE,
108:             TOKEN_PERMISSIONS_TYPE
109:         )
110:     );
```

- *PerpOrder.sol* ( [43-43](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L43-L43), [46-46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L46-L46), [47-49](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L47-L49) ):

```solidity
/// @audit Seen in ./src/markets/gamma/GammaOrder.sol#97
43:     bytes internal constant ORDER_TYPE = abi.encodePacked(PERP_ORDER_TYPE, OrderInfoLib.ORDER_INFO_TYPE);

/// @audit Seen in ./src/markets/gamma/GammaOrder.sol#101
46:     string internal constant TOKEN_PERMISSIONS_TYPE = "TokenPermissions(address token,uint256 amount)";

/// @audit Seen in ./src/markets/gamma/GammaOrder.sol#102
47:     string internal constant PERMIT2_ORDER_TYPE = string(
48:         abi.encodePacked("PerpOrder witness)", OrderInfoLib.ORDER_INFO_TYPE, PERP_ORDER_TYPE, TOKEN_PERMISSIONS_TYPE)
49:     );
```

- *PerpOrderV3.sol* ( [48-48](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L48-L48), [49-53](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L49-L53) ):

```solidity
/// @audit Seen in ./src/markets/perp/PerpOrder.sol#46
48:     string internal constant TOKEN_PERMISSIONS_TYPE = "TokenPermissions(address token,uint256 amount)";

/// @audit Seen in ./src/markets/perp/PerpOrder.sol#47
49:     string internal constant PERMIT2_ORDER_TYPE = string(
50:         abi.encodePacked(
51:             "PerpOrderV3 witness)", OrderInfoLib.ORDER_INFO_TYPE, PERP_ORDER_V3_TYPE, TOKEN_PERMISSIONS_TYPE
52:         )
53:     );
```

</details>

### [N-16] Convert simple `if`-statements to ternary expressions

Converting some if statements to ternaries (such as `z = (a < b) ? x : y`) can make the code more concise and easier to read.

<details>
<summary>There are 9 instances (click to show):</summary>

- *ScaledAsset.sol* ( [59-63](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L59-L63), [135-139](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L135-L139), [148-152](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L148-L152) ):

```solidity
59:         if (_supplyTokenAmount < burnAmount) {
60:             finalBurnAmount = _supplyTokenAmount;
61:         } else {
62:             finalBurnAmount = burnAmount;
63:         }

135:         if (_userStatus.positionAmount > 0) {
136:             interestFee = (getAssetFee(_assetStatus, _userStatus)).toInt256();
137:         } else {
138:             interestFee = -(getDebtFee(_assetStatus, _userStatus)).toInt256();
139:         }

148:         if (_userStatus.positionAmount > 0) {
149:             _userStatus.lastFeeGrowth = _assetStatus.assetGrowth;
150:         } else {
151:             _userStatus.lastFeeGrowth = _assetStatus.debtGrowth;
152:         }
```

- *SupplyLogic.sol* ( [37-41](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L37-L41), [70-74](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L70-L74) ):

```solidity
37:         if (_isStable) {
38:             mintAmount = receiveTokenAndMintBond(pair.quotePool, _amount);
39:         } else {
40:             mintAmount = receiveTokenAndMintBond(pair.basePool, _amount);
41:         }

70:         if (_isStable) {
71:             (finalburntAmount, finalWithdrawalAmount) = burnBondAndTransferToken(pair.quotePool, _amount);
72:         } else {
73:             (finalburntAmount, finalWithdrawalAmount) = burnBondAndTransferToken(pair.basePool, _amount);
74:         }
```

- *DecayLib.sol* ( [31-35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/DecayLib.sol#L31-L35) ):

```solidity
31:             if (endPrice < startPrice) {
32:                 decayedPrice = startPrice - (startPrice - endPrice) * elapsed / duration;
33:             } else {
34:                 decayedPrice = startPrice + (endPrice - startPrice) * elapsed / duration;
35:             }
```

- *L2Decoder.sol* ( [26-30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L26-L30) ):

```solidity
26:         if (isLimitUint == 1) {
27:             isLimit = true;
28:         } else {
29:             isLimit = false;
30:         }
```

- *L2GammaDecoder.sol* ( [78-82](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L78-L82) ):

```solidity
78:         if (isEnabledUint == 1) {
79:             isEnabled = true;
80:         } else {
81:             isEnabled = false;
82:         }
```

- *GlobalData.sol* ( [79-83](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L79-L83) ):

```solidity
79:         if (isQuoteAsset) {
80:             currency = pairStatus.quotePool.token;
81:         } else {
82:             currency = pairStatus.basePool.token;
83:         }
```

</details>

### [N-17] Contracts should each be defined in separate files

Keeping each contract in a separate file makes it easier to work with multiple people, makes the code easier to maintain, and is a common practice on most projects. The following files each contains more than one contract/library/interface.

There are 2 instances:

- [*PriceFeed.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol)

- [*GammaOrder.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol)

### [N-18] Contract name does not match its filename

According to the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html#contract-and-library-names), contract and library names should also match their filenames.

<details>
<summary>There are 5 instances (click to show):</summary>

- *ResolvedOrder.sol* ( [14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/ResolvedOrder.sol#L14) ):

```solidity
/// @audit Not match filename `ResolvedOrder.sol`
14: library ResolvedOrderLib {
```

- *PerpOrder.sol* ( [24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L24) ):

```solidity
/// @audit Not match filename `PerpOrder.sol`
24: library PerpOrderLib {
```

- *PerpOrderV3.sol* ( [25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L25) ):

```solidity
/// @audit Not match filename `PerpOrderV3.sol`
25: library PerpOrderV3Lib {
```

- *GlobalData.sol* ( [12](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L12) ):

```solidity
/// @audit Not match filename `GlobalData.sol`
12: library GlobalDataLibrary {
```

- *LockData.sol* ( [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/LockData.sol#L6) ):

```solidity
/// @audit Not match filename `LockData.sol`
6: library LockDataLibrary {
```

</details>

### [N-19] Consider emitting an event at the end of the constructor

This will allow users to easily exactly pinpoint when and by whom a contract was constructed.

<details>
<summary>There are 11 instances (click to show):</summary>

- *PredyPool.sol* ( [68-68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L68-L68) ):

```solidity
68:     constructor() {}
```

- *PriceFeed.sol* ( [14-14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L14-L14), [37-37](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L37-L37) ):

```solidity
14:     constructor(address pyth) {

37:     constructor(address quotePrice, address pyth, bytes32 priceId, uint256 decimalsDiff) {
```

- *BaseHookCallback.sol* ( [12-12](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol#L12-L12) ):

```solidity
12:     constructor(IPredyPool predyPool) {
```

- *BaseHookCallbackUpgradable.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L13-L13) ):

```solidity
13:     constructor() {}
```

- *BaseMarket.sol* ( [19-22](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L19-L22) ):

```solidity
19:     constructor(IPredyPool predyPool, address _whitelistFiller, address quoterAddress)
20:         BaseHookCallback(predyPool)
21:         Owned(msg.sender)
22:     {
```

- *BaseMarketUpgradable.sol* ( [36-36](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L36-L36) ):

```solidity
36:     constructor() {}
```

- *GammaTradeMarket.sol* ( [67-67](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L67-L67) ):

```solidity
67:     constructor() {}
```

- *PerpMarketV1.sol* ( [90-90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L90-L90) ):

```solidity
90:     constructor() {}
```

- *UniswapSettlement.sol* ( [16-16](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L16-L16) ):

```solidity
16:     constructor(address swapRouterAddress, address quoterAddress) {
```

- *SupplyToken.sol* ( [15-17](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L15-L17) ):

```solidity
15:     constructor(address controller, string memory _name, string memory _symbol, uint8 __decimals)
16:         ERC20(_name, _symbol, __decimals)
17:     {
```

</details>

### [N-20] Empty function body without comments

Empty function body in solidity is not recommended, consider adding some comments to the body.

There are 5 instances:

- *PredyPool.sol* ( [68-68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L68-L68) ):

```solidity
68:     constructor() {}
```

- *BaseHookCallbackUpgradable.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L13-L13) ):

```solidity
13:     constructor() {}
```

- *BaseMarketUpgradable.sol* ( [36-36](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L36-L36) ):

```solidity
36:     constructor() {}
```

- *GammaTradeMarket.sol* ( [67-67](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L67-L67) ):

```solidity
67:     constructor() {}
```

- *PerpMarketV1.sol* ( [90-90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L90-L90) ):

```solidity
90:     constructor() {}
```

### [N-21] Events are emitted without the sender information

When an action is triggered based on a user's action, not being able to filter based on who triggered the action makes event processing a lot more cumbersome. Including the `msg.sender` the events of these types of action will make events much more useful to end users, especially when `msg.sender` is not `tx.origin`.

<details>
<summary>There are 16 instances (click to show):</summary>

- *PredyPool.sol* ( [101-101](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L101-L101), [190-190](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L190-L190) ):

```solidity
101:         emit OperatorUpdated(newOperator);

190:         emit ProtocolRevenueWithdrawn(pairId, isQuoteToken, amount);
```

- *PriceFeed.sol* ( [21-21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L21-L21) ):

```solidity
21:         emit PriceFeedCreated(quotePrice, priceId, decimalsDiff, address(priceFeed));
```

- *VaultLib.sol* ( [44-44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/VaultLib.sol#L44-L44) ):

```solidity
44:             emit VaultCreated(vault.id, vault.owner, quoteToken, pairId);
```

- *AddPairLogic.sol* ( [93-93](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L93-L93), [101-101](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L101-L101), [115-115](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L115-L115), [125-125](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L125-L125), [139-139](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L139-L139) ):

```solidity
93:         emit PairAdded(pairId, _addPairParam.quoteToken, _addPairParam.uniswapPool);

101:         emit FeeRatioUpdated(_pairStatus.id, _feeRatio);

115:         emit PriceOracleUpdated(_pairStatus.id, _priceOracle);

125:         emit AssetRiskParamsUpdated(_pairStatus.id, _riskParams);

139:         emit IRMParamsUpdated(_pairStatus.id, _quoteIrmParams, _baseIrmParams);
```

- *LiquidationLogic.sol* ( [110-118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L110-L118) ):

```solidity
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

- *ReallocationLogic.sol* ( [73-80](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReallocationLogic.sol#L73-L80) ):

```solidity
73:             emit Rebalanced(
74:                 pairId,
75:                 relocationOccurred,
76:                 pairStatus.sqrtAssetStatus.tickLower,
77:                 pairStatus.sqrtAssetStatus.tickUpper,
78:                 deltaPositionBase,
79:                 deltaPositionQuote
80:             );
```

- *TradeLogic.sol* ( [58-65](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/TradeLogic.sol#L58-L65), [85-85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/TradeLogic.sol#L85-L85) ):

```solidity
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

- *GammaTradeMarket.sol* ( [101-113](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L101-L113), [123-133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L123-L133) ):

```solidity
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
```

- *PerpMarketV1.sol* ( [131-140](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L131-L140) ):

```solidity
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

</details>

### [N-22] Inconsistent floating version pragma

Source files are using different floating version syntax, this is prone to compilation errors, and is not conducive to the code reliability and maintainability.

There are 2 instances:

- *PredyPool.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *AggregatorV3Interface.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/vendors/AggregatorV3Interface.sol#L2) ):

```solidity
2: pragma solidity ^0.8.0;
```

### [N-23] Imports could be organized more systematically

The contract's interface should be imported first, followed by each of the interfaces it uses, followed by all other files. The examples below do not follow this layout.

<details>
<summary>There are 27 instances (click to show):</summary>

- *PredyPool.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L10-L10) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
10: import {IPredyPool} from "./interfaces/IPredyPool.sol";
```

- *PriceFeed.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {AggregatorV3Interface} from "./vendors/AggregatorV3Interface.sol";
```

- *BaseHookCallbackUpgradable.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import "../interfaces/IPredyPool.sol";
```

- *BaseMarket.sol* ( [7-7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L7-L7) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
7: import "../interfaces/IFillerMarket.sol";
```

- *BaseMarketUpgradable.sol* ( [6-6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L6-L6), [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L8-L8) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IPredyPool} from "../interfaces/IPredyPool.sol";

/// @audit Out of order with the prev import️ ⬆
8: import "../interfaces/IFillerMarket.sol";
```

- *SettlementCallbackLib.sol* ( [6-6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L6-L6), [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L10-L10) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IPredyPool} from "../interfaces/IPredyPool.sol";

/// @audit Out of order with the prev import️ ⬆
10: import {IFillerMarket} from "../interfaces/IFillerMarket.sol";
```

- *Perp.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L10-L10) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
10: import {IPredyPool} from "../interfaces/IPredyPool.sol";
```

- *Trade.sol* ( [6-6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IPredyPool} from "../interfaces/IPredyPool.sol";
```

- *UniHelper.sol* ( [7-7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L7-L7) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
7: import "../vendors/IUniswapV3PoolOracle.sol";
```

- *LiquidationLogic.sol* ( [6-6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IPredyPool} from "../../interfaces/IPredyPool.sol";
```

- *ReallocationLogic.sol* ( [6-6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReallocationLogic.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {ISettlement} from "../../interfaces/ISettlement.sol";
```

- *SupplyLogic.sol* ( [6-6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IPredyPool} from "../../interfaces/IPredyPool.sol";
```

- *GammaOrder.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IFillerMarket} from "../../interfaces/IFillerMarket.sol";
```

- *GammaTradeMarket.sol* ( [7-7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L7-L7) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
7: import {IPermit2} from "@uniswap/permit2/src/interfaces/IPermit2.sol";
```

- *GammaTradeMarketL2.sol* ( [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol#L8-L8) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
8: import {IPredyPool} from "../../interfaces/IPredyPool.sol";
```

- *GammaTradeMarketLib.sol* ( [7-7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L7-L7) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
7: import {IPredyPool} from "../../interfaces/IPredyPool.sol";
```

- *GammaTradeMarketWrapper.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketWrapper.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IPredyPool} from "../../interfaces/IPredyPool.sol";
```

- *PerpMarket.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarket.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IPredyPool} from "../../interfaces/IPredyPool.sol";
```

- *PerpMarketV1.sol* ( [6-6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L6-L6), [9-9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L9-L9) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {IPermit2} from "@uniswap/permit2/src/interfaces/IPermit2.sol";

/// @audit Out of order with the prev import️ ⬆
9: import "../../interfaces/IPredyPool.sol";
```

- *PerpOrder.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IFillerMarket} from "../../interfaces/IFillerMarket.sol";
```

- *PerpOrderV3.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {IFillerMarket} from "../../interfaces/IFillerMarket.sol";
```

- *UniswapSettlement.sol* ( [6-6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L6-L6) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
6: import {ISwapRouter} from "@uniswap/v3-periphery/contracts/interfaces/ISwapRouter.sol";
```

- *SupplyToken.sol* ( [5-5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L5-L5) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
5: import {ISupplyToken} from "../interfaces/ISupplyToken.sol";
```

- *GlobalData.sol* ( [7-7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L7-L7) ):

```solidity
/// @audit Out of order with the prev import️ ⬆
7: import "../interfaces/IPredyPool.sol";
```

</details>

### [N-24] Interfaces should be indicated with an `I` prefix in the contract name

Interfaces should be indicated with an `I` prefix in the contract name

There is 1 instance:

- *AggregatorV3Interface.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/vendors/AggregatorV3Interface.sol#L4) ):

```solidity
4: interface AggregatorV3Interface {
```

### [N-25] @openzeppelin/contracts should be upgraded to a newer version

These contracts import contracts from `@openzeppelin/contracts`, but they are not using [the latest version](https://github.com/OpenZeppelin/openzeppelin-contracts/releases). Using the latest version ensures contract security with fixes for known vulnerabilities, access to the latest feature updates, and enhanced community support and engagement.

The imported version is `4.9.5`.

<details>
<summary>There are 13 instances (click to show):</summary>

- *Perp.sol* ( [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L9) ):

```solidity
9: import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *PerpFee.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L4) ):

```solidity
4: import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *PositionCalculator.sol* ( [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L6) ):

```solidity
6: import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *Reallocation.sol* ( [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L7) ):

```solidity
7: import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *ScaledAsset.sol* ( [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L5) ):

```solidity
5: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *Trade.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L5) ):

```solidity
4: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

5: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *AddPairLogic.sol* ( [4](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L4), [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L5) ):

```solidity
4: import {IERC20Metadata} from "@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol";

5: import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";
```

- *LPMath.sol* ( [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L7) ):

```solidity
7: import "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *Math.sol* ( [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L6) ):

```solidity
6: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *PerpMarketV1.sol* ( [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L7) ):

```solidity
7: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

- *GlobalData.sol* ( [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L5) ):

```solidity
5: import {SafeCast} from "@openzeppelin/contracts/utils/math/SafeCast.sol";
```

</details>

### [N-26] Lib @uniswap/v3-periphery should be upgraded to a newer version

These contracts import contracts from lib @uniswap/v3-periphery, but they are not using [the latest version](https://github.com/Uniswap/v3-periphery).

The imported version is `^1.4.3`.

There are 4 instances:

- *Perp.sol* ( [5](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L5) ):

```solidity
5: import "@uniswap/v3-periphery/contracts/libraries/PositionKey.sol";
```

- *UniHelper.sol* ( [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L6) ):

```solidity
6: import "@uniswap/v3-periphery/contracts/libraries/PositionKey.sol";
```

- *UniswapSettlement.sol* ( [6](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L6), [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L7) ):

```solidity
6: import {ISwapRouter} from "@uniswap/v3-periphery/contracts/interfaces/ISwapRouter.sol";

7: import {IQuoterV2} from "@uniswap/v3-periphery/contracts/interfaces/IQuoterV2.sol";
```

### [N-27] Expressions for constant values should use `immutable` rather than `constant`

While it doesn't save any gas because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between `constant` variables and `immutable` variables, and they should each be used in their appropriate contexts. `constants` should be used for literal values written into the code, and `immutable` variables should be used for expressions, or values calculated in, or passed into the constructor.

<details>
<summary>There are 15 instances (click to show):</summary>

- *OrderInfoLib.sol* ( [14-14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/OrderInfoLib.sol#L14-L14) ):

```solidity
14:     bytes32 internal constant ORDER_INFO_TYPE_HASH = keccak256(ORDER_INFO_TYPE);
```

- *GammaOrder.sol* ( [24-37](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L24-L37), [39-39](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L39-L39), [81-94](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L81-L94), [97-98](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L97-L98), [99-99](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L99-L99), [102-110](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L102-L110) ):

```solidity
24:     bytes internal constant GAMMA_MODIFY_INFO_TYPE = abi.encodePacked(
25:         "GammaModifyInfo(",
26:         "bool isEnabled,",
27:         "uint64 expiration,",
28:         "int64 maximaDeviation,",
29:         "uint256 lowerLimit,",
30:         "uint256 upperLimit,",
31:         "uint32 hedgeInterval,",
32:         "uint32 sqrtPriceTrigger,",
33:         "uint32 minSlippageTolerance,",
34:         "uint32 maxSlippageTolerance,",
35:         "uint16 auctionPeriod,",
36:         "uint32 auctionRange)"
37:     );

39:     bytes32 internal constant GAMMA_MODIFY_INFO_TYPE_HASH = keccak256(GAMMA_MODIFY_INFO_TYPE);

81:     bytes internal constant GAMMA_ORDER_TYPE = abi.encodePacked(
82:         "GammaOrder(",
83:         "OrderInfo info,",
84:         "uint64 pairId,",
85:         "uint256 positionId,",
86:         "address entryTokenAddress,",
87:         "int256 quantity,",
88:         "int256 quantitySqrt,",
89:         "int256 marginAmount,",
90:         "uint256 baseSqrtPrice,",
91:         "uint32 slippageTolerance,",
92:         "uint8 leverage,",
93:         "GammaModifyInfo modifyInfo)"
94:     );

97:     bytes internal constant ORDER_TYPE =
98:         abi.encodePacked(GAMMA_ORDER_TYPE, GammaModifyInfoLib.GAMMA_MODIFY_INFO_TYPE, OrderInfoLib.ORDER_INFO_TYPE);

99:     bytes32 internal constant GAMMA_ORDER_TYPE_HASH = keccak256(ORDER_TYPE);

102:     string internal constant PERMIT2_ORDER_TYPE = string(
103:         abi.encodePacked(
104:             "GammaOrder witness)",
105:             GammaModifyInfoLib.GAMMA_MODIFY_INFO_TYPE,
106:             GAMMA_ORDER_TYPE,
107:             OrderInfoLib.ORDER_INFO_TYPE,
108:             TOKEN_PERMISSIONS_TYPE
109:         )
110:     );
```

- *PerpOrder.sol* ( [27-40](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L27-L40), [43-43](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L43-L43), [44-44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L44-L44), [47-49](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L47-L49) ):

```solidity
27:     bytes internal constant PERP_ORDER_TYPE = abi.encodePacked(
28:         "PerpOrder(",
29:         "OrderInfo info,",
30:         "uint64 pairId,",
31:         "address entryTokenAddress,",
32:         "int256 tradeAmount,",
33:         "int256 marginAmount,",
34:         "uint256 takeProfitPrice,",
35:         "uint256 stopLossPrice,",
36:         "uint64 slippageTolerance,",
37:         "uint8 leverage,",
38:         "address validatorAddress,",
39:         "bytes validationData)"
40:     );

43:     bytes internal constant ORDER_TYPE = abi.encodePacked(PERP_ORDER_TYPE, OrderInfoLib.ORDER_INFO_TYPE);

44:     bytes32 internal constant PERP_ORDER_TYPE_HASH = keccak256(ORDER_TYPE);

47:     string internal constant PERMIT2_ORDER_TYPE = string(
48:         abi.encodePacked("PerpOrder witness)", OrderInfoLib.ORDER_INFO_TYPE, PERP_ORDER_TYPE, TOKEN_PERMISSIONS_TYPE)
49:     );
```

- *PerpOrderV3.sol* ( [28-42](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L28-L42), [45-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L45-L45), [46-46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L46-L46), [49-53](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L49-L53) ):

```solidity
28:     bytes internal constant PERP_ORDER_V3_TYPE = abi.encodePacked(
29:         "PerpOrderV3(",
30:         "OrderInfo info,",
31:         "uint64 pairId,",
32:         "address entryTokenAddress,",
33:         "string side,",
34:         "uint256 quantity,",
35:         "uint256 marginAmount,",
36:         "uint256 limitPrice,",
37:         "uint256 stopPrice,",
38:         "uint8 leverage,",
39:         "bool reduceOnly,",
40:         "bool closePosition,",
41:         "bytes auctionData)"
42:     );

45:     bytes internal constant ORDER_V3_TYPE = abi.encodePacked(PERP_ORDER_V3_TYPE, OrderInfoLib.ORDER_INFO_TYPE);

46:     bytes32 internal constant PERP_ORDER_V3_TYPE_HASH = keccak256(ORDER_V3_TYPE);

49:     string internal constant PERMIT2_ORDER_TYPE = string(
50:         abi.encodePacked(
51:             "PerpOrderV3 witness)", OrderInfoLib.ORDER_INFO_TYPE, PERP_ORDER_V3_TYPE, TOKEN_PERMISSIONS_TYPE
52:         )
53:     );
```

</details>

### [N-28] Consider moving duplicated strings to constants

Moving duplicate strings to constants can improve code maintainability and readability.

<details>
<summary>There are 14 instances (click to show):</summary>

- *PredyPool.sol* ( [182-182](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L182-L182), [204-204](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L204-L204) ):

```solidity
182:         require(amount > 0, "AZ");

204:         require(amount > 0, "AZ");
```

- *ScaledAsset.sol* ( [67-67](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L67-L67), [85-85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L85-L85), [87-87](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L87-L87), [108-108](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L108-L108), [118-118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L118-L118), [160-160](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L160-L160), [175-175](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L175-L175) ):

```solidity
67:         require(getAvailableCollateralValue(tokenState) >= finalWithdrawAmount, "S0");

85:             require(userStatus.lastFeeGrowth == tokenStatus.assetGrowth, "S2");

87:             require(userStatus.lastFeeGrowth == tokenStatus.debtGrowth, "S2");

108:             require(getAvailableCollateralValue(tokenStatus) >= uint256(-closeAmount), "S0");

118:             require(getAvailableCollateralValue(tokenStatus) >= uint256(-openAmount), "S0");

160:         require(accountState.positionAmount >= 0, "S1");

175:         require(accountState.positionAmount <= 0, "S1");
```

- *AddPairLogic.sol* ( [214-214](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L214-L214), [216-216](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L216-L216) ):

```solidity
214:         require(1e8 < _assetRiskParams.riskRatio && _assetRiskParams.riskRatio <= 10 * 1e8, "C0");

216:         require(_assetRiskParams.rangeSize > 0 && _assetRiskParams.rebalanceThreshold > 0, "C0");
```

- *SupplyLogic.sol* ( [64-64](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L64-L64) ):

```solidity
64:         require(_amount > 0, "AZ");
```

- *PerpMarket.sol* ( [41-41](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarket.sol#L41-L41) ):

```solidity
41:             side: side ? "Buy" : "Sell",
```

- *PerpMarketLib.sol* ( [33-33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L33-L33) ):

```solidity
33:         bool isLong = (keccak256(bytes(side))) == keccak256(bytes("Buy"));
```

</details>

### [N-29] Contract uses both `require()`/`revert()` as well as custom errors

Consider using just one method in a single file.

<details>
<summary>There are 7 instances (click to show):</summary>

- *PredyPool.sol* ( [28](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L28) ):

```solidity
28: contract PredyPool is IPredyPool, IUniswapV3MintCallback, Initializable, ReentrancyGuardUpgradeable {
```

- *BaseMarketUpgradable.sol* ( [11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L11) ):

```solidity
11: abstract contract BaseMarketUpgradable is IFillerMarket, BaseHookCallbackUpgradable {
```

- *AddPairLogic.sol* ( [16](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L16) ):

```solidity
16: library AddPairLogic {
```

- *LiquidationLogic.sol* ( [21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L21) ):

```solidity
21: library LiquidationLogic {
```

- *SupplyLogic.sol* ( [14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L14) ):

```solidity
14: library SupplyLogic {
```

- *GammaTradeMarketLib.sol* ( [11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L11) ):

```solidity
11: library GammaTradeMarketLib {
```

- *PerpMarketV1.sol* ( [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L29) ):

```solidity
29: contract PerpMarketV1 is BaseMarketUpgradable, ReentrancyGuardUpgradeable {
```

</details>

### [N-30] Functions should be named in mixedCase style

As the [Solidity Style Guide](https://docs.soliditylang.org/en/v0.8.21/style-guide.html#function-names) suggests: functions should be named in mixedCase style.

<details>
<summary>There are 6 instances (click to show):</summary>

- *PredyPool.sol* ( [133](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L133) ):

```solidity
133:     function updateIRMParams(
```

- *BaseHookCallbackUpgradable.sol* ( [20](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L20) ):

```solidity
20:     function __BaseHookCallback_init(IPredyPool predyPool) internal onlyInitializing {
```

- *BaseMarketUpgradable.sol* ( [38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L38) ):

```solidity
38:     function __BaseMarket_init(IPredyPool predyPool, address _whitelistFiller, address quoterAddress)
```

- *UniHelper.sol* ( [20](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L20) ):

```solidity
20:     function getSqrtTWAP(address uniswapPoolAddress) internal view returns (uint160 sqrtTwapX96) {
```

- *AddPairLogic.sol* ( [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L128), [219](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L219) ):

```solidity
128:     function updateIRMParams(

219:     function validateIRMParams(InterestRateModel.IRMParams memory _irmParams) internal pure {
```

</details>

### [N-31] Variable names for `immutable`s should use UPPER_CASE_WITH_UNDERSCORES

For `immutable` variable names, each word should use all capital letters, with underscores separating each word (UPPER_CASE_WITH_UNDERSCORES)

<details>
<summary>There are 10 instances (click to show):</summary>

- *PriceFeed.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L10-L10), [30-30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L30-L30), [31-31](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L31-L31), [32-32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L32-L32), [33-33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L33-L33) ):

```solidity
10:     address private immutable _pyth;

30:     address private immutable _quotePriceFeed;

31:     address private immutable _pyth;

32:     uint256 private immutable _decimalsDiff;

33:     bytes32 private immutable _priceId;
```

- *BaseHookCallback.sol* ( [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol#L8-L8) ):

```solidity
8:     IPredyPool immutable _predyPool;
```

- *BaseMarket.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L13-L13) ):

```solidity
13:     PredyPoolQuoter internal immutable _quoter;
```

- *UniswapSettlement.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L13-L13), [14-14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L14-L14) ):

```solidity
13:     ISwapRouter private immutable _swapRouter;

14:     IQuoterV2 private immutable _quoterV2;
```

- *SupplyToken.sol* ( [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L8-L8) ):

```solidity
8:     address immutable _controller;
```

</details>

### [N-32] Named imports of parent contracts are missing

Consider adding named imports for all parent contracts.

<details>
<summary>There are 6 instances (click to show):</summary>

- *BaseHookCallback.sol* ( [7-7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol#L7-L7) ):

```solidity
/// @audit IHooks
7: abstract contract BaseHookCallback is IHooks {
```

- *BaseHookCallbackUpgradable.sol* ( [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L8-L8) ):

```solidity
/// @audit IHooks
8: abstract contract BaseHookCallbackUpgradable is Initializable, IHooks {
```

- *BaseMarket.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L10-L10) ):

```solidity
/// @audit IFillerMarket
/// @audit BaseHookCallback
10: abstract contract BaseMarket is IFillerMarket, BaseHookCallback, Owned {
```

- *BaseMarketUpgradable.sol* ( [11-11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L11-L11) ):

```solidity
/// @audit IFillerMarket
11: abstract contract BaseMarketUpgradable is IFillerMarket, BaseHookCallbackUpgradable {
```

- *UniswapSettlement.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L10-L10) ):

```solidity
/// @audit ISettlement
10: contract UniswapSettlement is ISettlement {
```

</details>

### [N-33] Constants should be put on the left side of comparisons

Putting constants on the left side of comparison statements is a best practice known as [Yoda conditions](https://en.wikipedia.org/wiki/Yoda_conditions).
Although solidity's static typing system prevents accidental assignments within conditionals, adopting this practice can improve code readability and consistency, especially when working across multiple languages.

<details>
<summary>There are 111 instances (click to show):</summary>

- *PredyPool.sol* ( [98](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L98) ):

```solidity
/// @audit put `address(0)` on the left
98:         require(newOperator != address(0));
```

- *PriceFeed.sol* ( [50](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L50) ):

```solidity
/// @audit put `-8` on the left
50:         require(basePrice.expo == -8, "INVALID_EXP");
```

- *BaseMarket.sol* ( [98](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L98), [105](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L105) ):

```solidity
/// @audit put `address(0)` on the left
98:         if (_quoteTokenMap[pairId] == address(0)) {

/// @audit put `address(0)` on the left
105:         require(_quoteTokenMap[pairId] != address(0) && entryTokenAddress == _quoteTokenMap[pairId]);
```

- *BaseMarketUpgradable.sol* ( [146](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L146), [153](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L153) ):

```solidity
/// @audit put `address(0)` on the left
146:         if (_quoteTokenMap[pairId] == address(0)) {

/// @audit put `address(0)` on the left
153:         require(_quoteTokenMap[pairId] != address(0) && entryTokenAddress == _quoteTokenMap[pairId]);
```

- *SettlementCallbackLib.sol* ( [34](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L34), [99](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L99), [122](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L122), [146](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L146), [169](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L169) ):

```solidity
/// @audit put `address(0)` on the left
34:             settlementParams.contractAddress != address(0) && !_whiteListedSettlements[settlementParams.contractAddress]

/// @audit put `address(0)` on the left
99:         if (settlementParams.contractAddress == address(0)) {

/// @audit put `0` on the left
122:         if (price == 0) {

/// @audit put `address(0)` on the left
146:         if (settlementParams.contractAddress == address(0)) {

/// @audit put `0` on the left
169:         if (price == 0) {
```

- *ApplyInterestLib.sol* ( [61](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L61) ):

```solidity
/// @audit put `0` on the left
61:         if (utilizationRatio == 0) {
```

- *Perp.sol* ( [223](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L223), [349](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L349), [349](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L349), [374](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L374), [390](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L390), [390](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L390), [432](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L432), [593](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L593), [605](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L605), [626](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L626), [633](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L633), [678](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L678), [766](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L766), [784](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L784) ):

```solidity
/// @audit put `0` on the left
223:         if (totalLiquidityAmount == 0) {

/// @audit put `0` on the left
349:         if (deltaPositionUnderlying == 0 && deltaPositionStable == 0) {

/// @audit put `0` on the left
349:         if (deltaPositionUnderlying == 0 && deltaPositionStable == 0) {

/// @audit put `0` on the left
374:         if (_assetStatus.totalAmount == 0) {

/// @audit put `0` on the left
390:         if (f0 == 0 && f1 == 0) {

/// @audit put `0` on the left
390:         if (f0 == 0 && f1 == 0) {

/// @audit put `0` on the left
432:         if (_tradeSqrtAmount == 0) {

/// @audit put `0` on the left
593:         if (_isWithdraw && _assetStatus.borrowedAmount == 0) {

/// @audit put `0` on the left
605:         if (_assetStatus.totalAmount == 0) {

/// @audit put `0` on the left
626:         if (_userStatus.sqrtPerp.amount == 0) {

/// @audit put `0` on the left
633:         if (_assetStatus.lastRebalanceTotalSquartAmount == 0) {

/// @audit put `0` on the left
678:         if (_tradeAmount == 0) {

/// @audit put `0` on the left
766:         if (openAmount != 0) {

/// @audit put `0` on the left
784:         if (closeAmount != 0) {
```

- *PerpFee.sol* ( [117](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L117), [142](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L142) ):

```solidity
/// @audit put `0` on the left
117:         if (userStatus.sqrtPerp.amount != 0 && userStatus.lastNumRebalance < assetStatus.numRebalance) {

/// @audit put `0` on the left
142:         if (userStatus.sqrtPerp.amount != 0 && userStatus.lastNumRebalance < assetStatus.numRebalance) {
```

- *PositionCalculator.sol* ( [43](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L43), [72](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L72), [103](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L103), [142](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L142), [176](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L176), [176](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L176) ):

```solidity
/// @audit put `0` on the left
43:         bool isSafe = vaultValue >= minMargin && _vault.margin >= 0;

/// @audit put `0` on the left
72:         isSafe = vaultValue >= minMargin && _vault.margin >= 0;

/// @audit put `0` on the left
103:         if (debtRiskRatio == 0) {

/// @audit put `address(0)` on the left
142:         if (pairStatus.priceFeed != address(0)) {

/// @audit put `0` on the left
176:         return _positionParams.amountSqrt != 0 || _positionParams.amountBase != 0;

/// @audit put `0` on the left
176:         return _positionParams.amountSqrt != 0 || _positionParams.amountBase != 0;
```

- *ScaledAsset.sol* ( [38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L38), [51](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L51), [73](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L73), [73](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L73), [160](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L160), [175](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L175), [190](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L190), [190](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L190), [231](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L231), [231](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L231) ):

```solidity
/// @audit put `0` on the left
38:         if (_amount == 0) {

/// @audit put `0` on the left
51:         if (_amount == 0) {

/// @audit put `0` on the left
73:         return (a >= 0 && b >= 0) || (a < 0 && b < 0);

/// @audit put `0` on the left
73:         return (a >= 0 && b >= 0) || (a < 0 && b < 0);

/// @audit put `0` on the left
160:         require(accountState.positionAmount >= 0, "S1");

/// @audit put `0` on the left
175:         require(accountState.positionAmount <= 0, "S1");

/// @audit put `0` on the left
190:         if (tokenState.totalCompoundDeposited == 0 && tokenState.totalNormalDeposited == 0) {

/// @audit put `0` on the left
190:         if (tokenState.totalCompoundDeposited == 0 && tokenState.totalNormalDeposited == 0) {

/// @audit put `0` on the left
231:         if (tokenState.totalCompoundDeposited == 0 && tokenState.totalNormalDeposited == 0) {

/// @audit put `0` on the left
231:         if (tokenState.totalCompoundDeposited == 0 && tokenState.totalNormalDeposited == 0) {
```

- *SlippageLib.sol* ( [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/SlippageLib.sol#L29) ):

```solidity
/// @audit put `0` on the left
29:         if (tradeResult.averagePrice == 0) {
```

- *Trade.sol* ( [86](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L86) ):

```solidity
/// @audit put `0` on the left
86:         if (totalBaseAmount == 0) {
```

- *VaultLib.sol* ( [30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/VaultLib.sol#L30) ):

```solidity
/// @audit put `0` on the left
30:         if (vaultId == 0) {
```

- *AddPairLogic.sol* ( [153](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L153), [206](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L206), [210](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L210), [214](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L214), [221](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L221), [221](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L221), [221](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L221), [222](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L222) ):

```solidity
/// @audit put `0` on the left
153:         require(_pairs[_pairId].id == 0, "AAA");

/// @audit put `20` on the left
206:         require(_fee <= 20, "FEE");

/// @audit put `address(0)` on the left
210:         require(_poolOwner != address(0), "ADDZ");

/// @audit put `10 * 1e8` on the left
214:         require(1e8 < _assetRiskParams.riskRatio && _assetRiskParams.riskRatio <= 10 * 1e8, "C0");

/// @audit put `1e18` on the left
221:             _irmParams.baseRate <= 1e18 && _irmParams.kinkRate <= 1e18 && _irmParams.slope1 <= 1e18

/// @audit put `1e18` on the left
221:             _irmParams.baseRate <= 1e18 && _irmParams.kinkRate <= 1e18 && _irmParams.slope1 <= 1e18

/// @audit put `1e18` on the left
221:             _irmParams.baseRate <= 1e18 && _irmParams.kinkRate <= 1e18 && _irmParams.slope1 <= 1e18

/// @audit put `10 * 1e18` on the left
222:                 && _irmParams.slope2 <= 10 * 1e18,
```

- *LiquidationLogic.sol* ( [45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L45), [84](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L84), [93](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L93), [164](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L164), [164](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L164) ):

```solidity
/// @audit put `1e18` on the left
45:         require(closeRatio > 0 && closeRatio <= 1e18, "ICR");

/// @audit put `0` on the left
84:             tradeParams.tradeAmountSqrt == 0 ? 0 : _MAX_ACCEPTABLE_SQRT_PRICE_RANGE

/// @audit put `address(0)` on the left
93:                 if (vault.recipient != address(0)) {

/// @audit put `0` on the left
164:         if (vaultValue <= 0 || minMargin == 0) {

/// @audit put `0` on the left
164:         if (vaultValue <= 0 || minMargin == 0) {
```

- *ReallocationLogic.sol* ( [51](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReallocationLogic.sol#L51) ):

```solidity
/// @audit put `0` on the left
51:             if (deltaPositionBase != 0) {
```

- *SupplyLogic.sol* ( [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L29) ):

```solidity
/// @audit put `0` on the left
29:         if (_amount <= 0) {
```

- *TradeLogic.sol* ( [79](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/TradeLogic.sol#L79) ):

```solidity
/// @audit put `0` on the left
79:         if (settledBaseAmount != 0) {
```

- *LPMath.sol* ( [36](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L36), [74](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L74) ):

```solidity
/// @audit put `0` on the left
36:         if (liquidityAmount == 0 || sqrtRatioA == sqrtRatioB) {

/// @audit put `0` on the left
74:         if (liquidityAmount == 0 || sqrtRatioA == sqrtRatioB) {
```

- *Math.sol* ( [13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L13), [25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L25), [35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L35), [45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L45), [55](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L55) ):

```solidity
/// @audit put `0` on the left
13:         return uint256(x >= 0 ? x : -x);

/// @audit put `0` on the left
25:         if (x == 0) {

/// @audit put `0` on the left
35:         if (x == 0) {

/// @audit put `0` on the left
45:         if (x == 0) {

/// @audit put `0` on the left
55:         if (b >= 0) {
```

- *L2Decoder.sol* ( [26](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L26), [68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L68), [69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L69), [70](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L70) ):

```solidity
/// @audit put `1` on the left
26:         if (isLimitUint == 1) {

/// @audit put `1` on the left
68:         reduceOnly = reduceOnlyUint == 1;

/// @audit put `1` on the left
69:         closePosition = closePositionUint == 1;

/// @audit put `1` on the left
70:         side = sideUint == 1;
```

- *GammaTradeMarket.sol* ( [89](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L89), [90](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L90), [146](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L146), [186](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L186), [197](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L197), [212](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L212), [212](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L212), [212](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L212), [233](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L233), [256](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L256), [281](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L281), [306](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L306), [306](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L306), [342](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L342), [342](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L342), [378](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L378), [395](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L395), [395](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L395), [395](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L395), [421](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L421), [421](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L421) ):

```solidity
/// @audit put `0` on the left
89:             if (tradeResult.minMargin == 0) {

/// @audit put `0` on the left
90:                 if (callbackData.marginAmountUpdate != 0) {

/// @audit put `1e18` on the left
146:         if (closeRatio == 1e18) {

/// @audit put `0` on the left
186:             tradeResult.vaultId, gammaOrder.positionId == 0, gammaOrder.info.trader, gammaOrder.pairId

/// @audit put `0` on the left
197:         if (gammaOrder.positionId == 0) {

/// @audit put `0` on the left
212:         if (gammaOrder.quantity != 0 || gammaOrder.quantitySqrt != 0 || gammaOrder.marginAmount != 0) {

/// @audit put `0` on the left
212:         if (gammaOrder.quantity != 0 || gammaOrder.quantitySqrt != 0 || gammaOrder.marginAmount != 0) {

/// @audit put `0` on the left
212:         if (gammaOrder.quantity != 0 || gammaOrder.quantitySqrt != 0 || gammaOrder.marginAmount != 0) {

/// @audit put `0` on the left
233:         if (userPosition.vaultId == 0 || positionId != userPosition.vaultId) {

/// @audit put `0` on the left
256:         if (delta == 0) {

/// @audit put `0` on the left
281:         if (userPosition.vaultId == 0 || positionId != userPosition.vaultId) {

/// @audit put `0` on the left
306:         if (tradeParams.tradeAmount == 0 && tradeParams.tradeAmountSqrt == 0) {

/// @audit put `0` on the left
306:         if (tradeParams.tradeAmount == 0 && tradeParams.tradeAmountSqrt == 0) {

/// @audit put `0` on the left
342:         if (vault.openPosition.perp.amount == 0 && vault.openPosition.sqrtPerp.amount == 0) {

/// @audit put `0` on the left
342:         if (vault.openPosition.perp.amount == 0 && vault.openPosition.sqrtPerp.amount == 0) {

/// @audit put `0` on the left
378:         if (userPosition.vaultId == 0) {

/// @audit put `0` on the left
395:         if (vault.margin != 0 || vault.openPosition.perp.amount != 0 || vault.openPosition.sqrtPerp.amount != 0) {

/// @audit put `0` on the left
395:         if (vault.margin != 0 || vault.openPosition.perp.amount != 0 || vault.openPosition.sqrtPerp.amount != 0) {

/// @audit put `0` on the left
395:         if (vault.margin != 0 || vault.openPosition.perp.amount != 0 || vault.openPosition.sqrtPerp.amount != 0) {

/// @audit put `0` on the left
421:         if (positionId == 0 || userPosition.vaultId == 0) {

/// @audit put `0` on the left
421:         if (positionId == 0 || userPosition.vaultId == 0) {
```

- *GammaTradeMarketLib.sol* ( [80](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L80) ):

```solidity
/// @audit put `0` on the left
80:         if (userPosition.sqrtPriceTrigger == 0) {
```

- *L2GammaDecoder.sol* ( [78](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L78) ):

```solidity
/// @audit put `1` on the left
78:         if (isEnabledUint == 1) {
```

- *PerpMarketLib.sol* ( [38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L38), [42](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L42), [50](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L50), [92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L92), [92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L92), [123](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L123), [199](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L199) ):

```solidity
/// @audit put `0` on the left
38:             if (isLong && currentPositionAmount >= 0) {

/// @audit put `0` on the left
42:             if (!isLong && currentPositionAmount <= 0) {

/// @audit put `0` on the left
50:             if (currentPositionAmount == 0) {

/// @audit put `0` on the left
92:         if (limitPrice == 0 && stopPrice == 0) {

/// @audit put `0` on the left
92:         if (limitPrice == 0 && stopPrice == 0) {

/// @audit put `0` on the left
123:         if (tradeAmount == 0) {

/// @audit put `0` on the left
199:         if (tradeAmount != 0) {
```

- *PerpMarketV1.sol* ( [181](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L181), [207](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L207), [257](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L257), [290](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L290) ):

```solidity
/// @audit put `0` on the left
181:         if (tradeAmount == 0) {

/// @audit put `0` on the left
207:         if (userPosition.vaultId == 0) {

/// @audit put `0` on the left
257:         if (userPosition.vaultId == 0) {

/// @audit put `0` on the left
290:         if (tradeAmount == 0) {
```

- *GlobalData.sol* ( [27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L27), [31](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L31), [36](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L36) ):

```solidity
/// @audit put `0` on the left
27:         if (vaultId <= 0 || globalData.vaultCount <= vaultId) revert IPredyPool.InvalidPairId();

/// @audit put `0` on the left
31:         if (pairId <= 0 || globalData.pairsCount <= pairId) revert IPredyPool.InvalidPairId();

/// @audit put `address(0)` on the left
36:         if (globalData.lockData.locker != address(0)) {
```

</details>

### [N-34] Libraries should be defined in separate files

The libraries below should be defined in separate files, so that it's easier for future projects to import them, and to avoid duplication later on if they need to be used elsewhere in the project.

There are 2 instances:

- *GammaOrder.sol* ( [23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L23), [78](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L78) ):

```solidity
23: library GammaModifyInfoLib {

78: library GammaOrderLib {
```

### [N-35] `else`-block not required

One level of nesting can be removed by not having an `else` block when the `if`-block always jumps at the end. For example:
```solidity
if (condition) {
    body1...
    return x;
} else {
    body2...
}
```
can be changed to:
```solidity
if (condition) {
    body1...
    return x;
}
body2...
```

<details>
<summary>There are 22 instances (click to show):</summary>

- *PredyPool.sol* ( [385-387](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L385-L387) ):

```solidity
385:         if (isQuoteToken) {
386:             return globalData.pairs[pairId].quotePool;
387:         } else {
```

- *Perp.sol* ( [597-599](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L597-L599) ):

```solidity
597:         if (available >= buffer) {
598:             return available - buffer;
599:         } else {
```

- *PositionCalculator.sol* ( [103-105](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L103-L105), [142-144](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L142-L144) ):

```solidity
103:         if (debtRiskRatio == 0) {
104:             return Constants.BASE_MIN_COLLATERAL_WITH_DEBT;
105:         } else {

142:         if (pairStatus.priceFeed != address(0)) {
143:             return PriceFeed(pairStatus.priceFeed).getSqrtPrice();
144:         } else {
```

- *UniHelper.sol* ( [28-30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L28-L30) ):

```solidity
28:         if (isQuoteZero) {
29:             return uint160((Constants.Q96 << Constants.RESOLUTION) / sqrtPriceX96);
30:         } else {
```

- *VaultLib.sol* ( [30-47](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/VaultLib.sol#L30-L47) ):

```solidity
30:         if (vaultId == 0) {
31:             uint256 finalVaultId = globalData.vaultCount;
32: 
33:             // Initialize a new vault
34:             DataType.Vault storage vault = globalData.vaults[finalVaultId];
35: 
36:             vault.id = finalVaultId;
37:             vault.owner = msg.sender;
38:             vault.recipient = msg.sender;
39:             vault.openPosition.pairId = pairId;
40:             vault.quoteToken = quoteToken;
41: 
42:             globalData.vaultCount++;
43: 
44:             emit VaultCreated(vault.id, vault.owner, quoteToken, pairId);
45: 
46:             return vault.id;
47:         } else {
```

- *LPMath.sol* ( [61-63](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L61-L63), [98-100](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L98-L100), [124-126](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L124-L126), [150-152](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L150-L152) ):

```solidity
61:         if (swaped) {
62:             return -r;
63:         } else {

98:         if (swaped) {
99:             return -r;
100:         } else {

124:         if (isRoundUp) {
125:             return FullMath.mulDivRoundingUp(liquidityAmount, FixedPoint96.Q96, sqrtRatio);
126:         } else {

150:         if (isRoundUp) {
151:             return FullMath.mulDivRoundingUp(liquidityAmount, sqrtRatio, FixedPoint96.Q96);
152:         } else {
```

- *Math.sol* ( [25-27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L25-L27), [27-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L27-L29), [35-37](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L35-L37), [37-39](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L37-L39), [45-47](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L45-L47), [47-49](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L47-L49), [55-57](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L55-L57) ):

```solidity
25:         if (x == 0) {
26:             return 0;
27:         } else if (x > 0) {

27:         } else if (x > 0) {
28:             return FullMath.mulDiv(uint256(x), y, z).toInt256();
29:         } else {

35:         if (x == 0) {
36:             return 0;
37:         } else if (x > 0) {

37:         } else if (x > 0) {
38:             return FullMath.mulDiv(uint256(x), y, z).toInt256();
39:         } else {

45:         if (x == 0) {
46:             return 0;
47:         } else if (x > 0) {

47:         } else if (x > 0) {
48:             return FixedPointMathLib.mulDivDown(uint256(x), y, z).toInt256();
49:         } else {

55:         if (b >= 0) {
56:             return a + uint256(b);
57:         } else {
```

- *DecayLib.sol* ( [21-23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/DecayLib.sol#L21-L23) ):

```solidity
21:         if (decayEndTime < decayStartTime) {
22:             revert EndTimeBeforeStartTime();
23:         } else if (decayEndTime <= value) {
```

- *PerpMarketLib.sol* ( [56-58](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L56-L58), [66-68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L66-L68), [179-181](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L179-L181), [181-183](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L181-L183) ):

```solidity
56:                     if (currentPositionAmount > -tradeAmount) {
57:                         return tradeAmount;
58:                     } else {

66:                     if (-currentPositionAmount > tradeAmount) {
67:                         return tradeAmount;
68:                     } else {

179:         if (price1 == price2) {
180:             return 0;
181:         } else if (price1 > price2) {

181:         } else if (price1 > price2) {
182:             return (price1 - price2) * Bps.ONE / price2;
183:         } else {
```

</details>

### [N-36] Large multiples of ten should use scientific notation

Use a scientific notation rather than decimal literals (e.g. `1e6` instead of `1000000`), for better code readability.

There are 7 instances:

- *Constants.sol* ( [23-23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Constants.sol#L23-L23) ):

```solidity
/// @audit 1000 -> 1e3
23:     uint256 internal constant BASE_MIN_COLLATERAL_WITH_DEBT = 1000;
```

- *Perp.sol* ( [399-399](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L399-L399), [402-402](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L402-L402), [405-405](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L405-L405), [406-406](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L406-L406) ):

```solidity
/// @audit 1000 -> 1e3
399:             f0, _assetStatus.totalAmount + _assetStatus.borrowedAmount * spreadParam / 1000, _assetStatus.totalAmount

/// @audit 1000 -> 1e3
402:             f1, _assetStatus.totalAmount + _assetStatus.borrowedAmount * spreadParam / 1000, _assetStatus.totalAmount

/// @audit 1000 -> 1e3
/// @audit 1000 -> 1e3
405:         _assetStatus.borrowPremium0Growth += FullMath.mulDiv(f0, 1000 + spreadParam, 1000);

/// @audit 1000 -> 1e3
/// @audit 1000 -> 1e3
406:         _assetStatus.borrowPremium1Growth += FullMath.mulDiv(f1, 1000 + spreadParam, 1000);
```

### [N-37] High cyclomatic complexity

Consider breaking down these blocks into more manageable units, by splitting things into utility functions, by reducing nesting, and by using early returns.

<details>
<summary>There is 1 instance (click to show):</summary>

- *PerpMarketV1.sol* ( [102-142](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L102-L142) ):

```solidity
102:     function predyTradeAfterCallback(
103:         IPredyPool.TradeParams memory tradeParams,
104:         IPredyPool.TradeResult memory tradeResult
105:     ) external override(BaseHookCallbackUpgradable) onlyPredyPool {
106:         CallbackData memory callbackData = abi.decode(tradeParams.extraData, (CallbackData));
107:         ERC20 quoteToken = ERC20(_getQuoteTokenAddress(tradeParams.pairId));
108: 
109:         if (callbackData.callbackSource == CallbackSource.QUOTE) {
110:             _revertTradeResult(tradeResult);
111:         } else if (callbackData.callbackSource == CallbackSource.QUOTE3) {
112:             _revertTradeResult(tradeResult);
113:         } else if (callbackData.callbackSource == CallbackSource.TRADE3) {
114:             int256 marginAmountUpdate =
115:                 _calculateInitialMargin(tradeParams.vaultId, tradeParams.pairId, callbackData.leverage);
116: 
117:             uint256 cost = 0;
118: 
119:             if (marginAmountUpdate > 0) {
120:                 cost = uint256(marginAmountUpdate);
121:             }
122: 
123:             _verifyOrderV3(callbackData.resolvedOrder, cost);
124: 
125:             if (marginAmountUpdate > 0) {
126:                 quoteToken.safeTransfer(address(_predyPool), uint256(marginAmountUpdate));
127:             } else if (marginAmountUpdate < 0) {
128:                 _predyPool.take(true, callbackData.trader, uint256(-marginAmountUpdate));
129:             }
130: 
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
141:         }
142:     }
```

</details>

### [N-38] Typos

All typos should be corrected.

<details>
<summary>There are 16 instances (click to show):</summary>

- *PredyPool.sol* ( [43](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L43), [286](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L286), [291](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L291) ):

```solidity
/// @audit Recepient
43:     event RecepientUpdated(uint256 vaultId, address recipient);

/// @audit Recepient
286:     function updateRecepient(uint256 vaultId, address recipient) external onlyVaultOwner(vaultId) {

/// @audit Recepient
291:         emit RecepientUpdated(vaultId, recipient);
```

- *BaseMarket.sol* ( [103](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L103) ):

```solidity
/// @audit registerd
103:     /// @notice Checks if entryTokenAddress is registerd for the pair
```

- *BaseMarketUpgradable.sol* ( [151](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L151) ):

```solidity
/// @audit registerd
151:     /// @notice Checks if entryTokenAddress is registerd for the pair
```

- *ReaderLogic.sol* ( [35](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L35), [39](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L39) ):

```solidity
/// @audit Pice
35:         (int256 minMargin, int256 vaultValue,, uint256 oraclePice) =

/// @audit Pice
39:             IPredyPool.VaultStatus(vaultId, vaultValue, minMargin, oraclePice, feeAmount, getPosition(vault, feeAmount))
```

- *LPMath.sol* ( [40](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L40), [46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L46), [61](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L61), [78](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L78), [84](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L84), [98](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L98) ):

```solidity
/// @audit swaped
40:         bool swaped = sqrtRatioA > sqrtRatioB;

/// @audit swaped
46:         bool _isRoundUp = swaped ? !isRoundUp : isRoundUp;

/// @audit swaped
61:         if (swaped) {

/// @audit swaped
78:         bool swaped = sqrtRatioA < sqrtRatioB;

/// @audit swaped
84:         bool _isRoundUp = swaped ? !isRoundUp : isRoundUp;

/// @audit swaped
98:         if (swaped) {
```

- *ResolvedOrder.sol* ( [22](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/ResolvedOrder.sol#L22) ):

```solidity
/// @audit resovled
22:     /// @param resolvedOrder resovled order
```

- *GammaTradeMarket.sol* ( [200](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L200) ):

```solidity
/// @audit Recepient
200:             _predyPool.updateRecepient(tradeResult.vaultId, gammaOrder.info.trader);
```

- *PerpMarketV1.sol* ( [210](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L210) ):

```solidity
/// @audit Recepient
210:             _predyPool.updateRecepient(tradeResult.vaultId, perpOrder.info.trader);
```

</details>

### [N-39] Unnecessary casting

Unnecessary castings can be removed.

There are 3 instances:

- *SettlementCallbackLib.sol* ( [111-111](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L111-L111), [158-158](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L158-L158) ):

```solidity
/// @audit address(settlementParams.contractAddress)
111:         ERC20(baseToken).approve(address(settlementParams.contractAddress), sellAmount);

/// @audit address(settlementParams.contractAddress)
158:         ERC20(quoteToken).approve(address(settlementParams.contractAddress), settlementParams.maxQuoteAmount);
```

- *ResolvedOrder.sol* ( [24-24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/ResolvedOrder.sol#L24-L24) ):

```solidity
/// @audit address(resolvedOrder.info.market)
24:         if (address(this) != address(resolvedOrder.info.market)) {
```

### [N-40] Unused contract variables

The following state variables are defined but not used.
It is recommended to check the code for logical omissions that cause them not to be used. If it's determined that they are not needed anywhere, it's best to remove them from the codebase to improve code clarity and minimize confusion.

There is 1 instance:

- *BaseMarket.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L13-L13) ):

```solidity
13:     PredyPoolQuoter internal immutable _quoter;
```

### [N-41] Unused named return

Declaring named returns, but not using them, is confusing to the reader. Consider either completely removing them (by declaring just the type without a name), or remove the return statement and do a variable assignment. This would improve the readability of the code, and it may also help reduce regressions during future code refactors.

<details>
<summary>There are 19 instances (click to show):</summary>

- *PredyPool.sol* ( [222-225](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L222-L225), [237-240](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L237-L240), [251-254](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L251-L254), [265-268](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L265-L268), [313-316](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L313-L316) ):

```solidity
/// @audit finalSuppliedAmount
222:     function supply(uint256 pairId, bool isQuoteAsset, uint256 supplyAmount)
223:         external
224:         nonReentrant
225:         returns (uint256 finalSuppliedAmount)

/// @audit finalBurnAmount
/// @audit finalWithdrawAmount
237:     function withdraw(uint256 pairId, bool isQuoteAsset, uint256 withdrawAmount)
238:         external
239:         nonReentrant
240:         returns (uint256 finalBurnAmount, uint256 finalWithdrawAmount)

/// @audit relocationOccurred
251:     function reallocate(uint256 pairId, bytes memory settlementData)
252:         external
253:         nonReentrant
254:         returns (bool relocationOccurred)

/// @audit tradeResult
265:     function trade(TradeParams memory tradeParams, bytes memory settlementData)
266:         external
267:         nonReentrant
268:         returns (TradeResult memory tradeResult)

/// @audit tradeResult
313:     function execLiquidationCall(uint256 vaultId, uint256 closeRatio, bytes memory settlementData)
314:         external
315:         nonReentrant
316:         returns (TradeResult memory tradeResult)
```

- *BaseMarket.sol* ( [40-42](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L40-L42) ):

```solidity
/// @audit relocationOccurred
40:     function reallocate(uint256 pairId, IFillerMarket.SettlementParams memory settlementParams)
41:         external
42:         returns (bool relocationOccurred)
```

- *BaseMarketUpgradable.sol* ( [89-91](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L89-L91) ):

```solidity
/// @audit relocationOccurred
89:     function reallocate(uint256 pairId, IFillerMarket.SettlementParamsV3 memory settlementParams)
90:         external
91:         returns (bool relocationOccurred)
```

- *PositionCalculator.sol* ( [141-141](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L141-L141), [151-154](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L151-L154), [163-166](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L163-L166) ):

```solidity
/// @audit sqrtPriceX96
141:     function getSqrtIndexPrice(DataType.PairStatus memory pairStatus) internal view returns (uint256 sqrtPriceX96) {

/// @audit positionParams
151:     function getPositionWithFeeAmount(Perp.UserStatus memory perpUserStatus, DataType.FeeAmount memory feeAmount)
152:         internal
153:         pure
154:         returns (PositionParams memory positionParams)

/// @audit positionParams
163:     function getPosition(Perp.UserStatus memory _perpUserStatus)
164:         internal
165:         pure
166:         returns (PositionParams memory positionParams)
```

- *Reallocation.sol* ( [18-21](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L18-L21) ):

```solidity
/// @audit lower
/// @audit upper
18:     function getNewRange(DataType.PairStatus memory _assetStatusUnderlying, int24 currentTick)
19:         internal
20:         view
21:         returns (int24 lower, int24 upper)
```

- *Trade.sol* ( [112-112](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L112-L112) ):

```solidity
/// @audit sqrtPriceX96
112:     function getSqrtPrice(address uniswapPoolAddress, bool isQuoteZero) internal view returns (uint256 sqrtPriceX96) {
```

- *GammaTradeMarketL2.sol* ( [42-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol#L42-L45) ):

```solidity
/// @audit tradeResult
42:     function executeTradeL2(GammaOrderL2 memory order, bytes memory sig, SettlementParamsV3 memory settlementParams)
43:         external
44:         nonReentrant
45:         returns (IPredyPool.TradeResult memory tradeResult)
```

- *GammaTradeMarketLib.sol* ( [59-62](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L59-L62), [106-109](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L106-L109) ):

```solidity
/// @audit slippageTolerance
59:     function validateHedgeCondition(GammaTradeMarketLib.UserPosition memory userPosition, uint256 sqrtIndexPrice)
60:         external
61:         view
62:         returns (bool, uint256 slippageTolerance, GammaTradeMarketLib.CallbackType)

/// @audit slippageTolerance
106:     function validateCloseCondition(UserPosition memory userPosition, uint256 sqrtIndexPrice)
107:         external
108:         view
109:         returns (bool, uint256 slippageTolerance, CallbackType)
```

- *GammaTradeMarketWrapper.sol* ( [12-14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketWrapper.sol#L12-L14) ):

```solidity
/// @audit tradeResult
12:     function executeTrade(GammaOrder memory gammaOrder, bytes memory sig, SettlementParamsV3 memory settlementParams)
13:         external
14:         returns (IPredyPool.TradeResult memory tradeResult)
```

- *PerpMarketLib.sol* ( [26-32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L26-L32) ):

```solidity
/// @audit finalTradeAmount
26:     function getFinalTradeAmount(
27:         int256 currentPositionAmount,
28:         string memory side,
29:         uint256 quantity,
30:         bool reduceOnly,
31:         bool closePosition
32:     ) internal pure returns (int256 finalTradeAmount) {
```

</details>

### [N-42] Use delete instead of assigning values to `false`

The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic.

There are 3 instances:

- *Perp.sol* ( [242-242](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L242-L242) ):

```solidity
242:             isOutOfRange = false;
```

- *L2Decoder.sol* ( [29-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L29-L29) ):

```solidity
29:             isLimit = false;
```

- *L2GammaDecoder.sol* ( [81-81](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L81-L81) ):

```solidity
81:             isEnabled = false;
```

### [N-43] Consider using `delete` rather than assigning zero to clear values

The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic.

There are 5 instances:

- *PredyPool.sol* ( [184-184](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L184-L184), [206-206](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L206-L206) ):

```solidity
184:         pool.accumulatedProtocolRevenue = 0;

206:         pool.accumulatedCreatorRevenue = 0;
```

- *UniHelper.sol* ( [39-39](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L39-L39) ):

```solidity
39:         secondsAgos[1] = 0;
```

- *LiquidationLogic.sol* ( [95-95](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L95-L95), [102-102](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L102-L102) ):

```solidity
95:                     vault.margin = 0;

102:                 vault.margin = 0;
```

### [N-44] Use the latest Solidity version

Upgrading to the [latest solidity version](https://github.com/ethereum/solc-js/tags) (0.8.19 for L2s) can optimize gas usage, take advantage of new features and improve overall contract efficiency. Where possible, based on compatibility requirements, it is recommended to use newer/latest solidity version to take advantage of the latest optimizations and features.

<details>
<summary>There are 52 instances (click to show):</summary>

- *PredyPool.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PriceFeed.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *BaseHookCallback.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *BaseHookCallbackUpgradable.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *BaseMarket.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *BaseMarketUpgradable.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *SettlementCallbackLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *ApplyInterestLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *Constants.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Constants.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *DataType.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/DataType.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *InterestRateModel.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/InterestRateModel.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PairLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PairLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *Perp.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PerpFee.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PositionCalculator.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PremiumCurveModel.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PremiumCurveModel.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *Reallocation.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *ScaledAsset.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *SlippageLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/SlippageLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *Trade.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *UniHelper.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *VaultLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/VaultLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *AddPairLogic.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *LiquidationLogic.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *ReaderLogic.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *ReallocationLogic.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReallocationLogic.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *SupplyLogic.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *TradeLogic.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/TradeLogic.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *Bps.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Bps.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *LPMath.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *Math.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *DecayLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/DecayLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *OrderInfoLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/OrderInfoLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *Permit2Lib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/Permit2Lib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *ResolvedOrder.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/ResolvedOrder.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *L2Decoder.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *ArrayLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/ArrayLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *GammaOrder.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *GammaTradeMarket.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *GammaTradeMarketL2.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *GammaTradeMarketLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *GammaTradeMarketWrapper.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketWrapper.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *L2GammaDecoder.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PerpMarket.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarket.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PerpMarketLib.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PerpMarketV1.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PerpOrder.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *PerpOrderV3.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *UniswapSettlement.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *SupplyToken.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *GlobalData.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

- *LockData.sol* ( [2](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/LockData.sol#L2) ):

```solidity
2: pragma solidity ^0.8.17;
```

</details>

### [N-45] Use a struct to encapsulate multiple function parameters

If a function has too many parameters, replacing them with a struct can improve code readability and maintainability, increase reusability, and reduce the likelihood of errors when passing the parameters.

There are 2 instances:

- *UniswapSettlement.sol* ( [22-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L22-L29), [38-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L38-L45) ):

```solidity
22:     function swapExactIn(
23:         address,
24:         address baseToken,
25:         bytes memory data,
26:         uint256 amountIn,
27:         uint256 amountOutMinimum,
28:         address recipient
29:     ) external override returns (uint256 amountOut) {

38:     function swapExactOut(
39:         address quoteToken,
40:         address,
41:         bytes memory data,
42:         uint256 amountOut,
43:         uint256 amountInMaximum,
44:         address recipient
45:     ) external override returns (uint256 amountIn) {
```

### [N-46] Returning a struct instead of a bunch of variables is better

If a function returns [too many variables](https://docs.soliditylang.org/en/v0.8.21/contracts.html#returning-multiple-values), replacing them with a struct can improve code readability, maintainability and reusability.

<details>
<summary>There are 5 instances (click to show):</summary>

- *PredyPool.sol* ( [237-240](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L237-L240) ):

```solidity
237:     function withdraw(uint256 pairId, bool isQuoteAsset, uint256 withdrawAmount)
238:         external
239:         nonReentrant
240:         returns (uint256 finalBurnAmount, uint256 finalWithdrawAmount)
```

- *GammaTradeMarket.sol* ( [333-336](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L333-L336) ):

```solidity
333:     function checkAutoHedgeAndClose(uint256 positionId)
334:         external
335:         view
336:         returns (bool hedgeRequired, bool closeRequired, uint256 resultPositionId)
```

- *PerpMarketV1.sol* ( [247-253](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L247-L253) ):

```solidity
247:     function getUserPosition(address owner, uint256 pairId)
248:         external
249:         returns (
250:             UserPosition memory userPosition,
251:             IPredyPool.VaultStatus memory vaultStatus,
252:             DataType.Vault memory vault
253:         )
```

- *AggregatorV3Interface.sol* ( [8-11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/vendors/AggregatorV3Interface.sol#L8-L11), [12-15](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/vendors/AggregatorV3Interface.sol#L12-L15) ):

```solidity
8:     function getRoundData(uint80 _roundId)
9:         external
10:         view
11:         returns (uint80 roundId, int256 answer, uint256 startedAt, uint256 updatedAt, uint80 answeredInRound);

12:     function latestRoundData()
13:         external
14:         view
15:         returns (uint80 roundId, int256 answer, uint256 startedAt, uint256 updatedAt, uint80 answeredInRound);
```

</details>

### [N-47] Contract variables should have comments

Consider adding some comments on non-public contract variables to explain what they are supposed to do. This will help for future code reviews.

<details>
<summary>There are 20 instances (click to show):</summary>

- *PriceFeed.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L10-L10), [30-30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L30-L30), [31-31](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L31-L31), [32-32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L32-L32), [33-33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L33-L33) ):

```solidity
10:     address private immutable _pyth;

30:     address private immutable _quotePriceFeed;

31:     address private immutable _pyth;

32:     uint256 private immutable _decimalsDiff;

33:     bytes32 private immutable _priceId;
```

- *BaseHookCallback.sol* ( [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol#L8-L8) ):

```solidity
8:     IPredyPool immutable _predyPool;
```

- *BaseHookCallbackUpgradable.sol* ( [9-9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol#L9-L9) ):

```solidity
9:     IPredyPool _predyPool;
```

- *BaseMarket.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L13-L13), [15-15](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L15-L15), [17-17](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L17-L17) ):

```solidity
13:     PredyPoolQuoter internal immutable _quoter;

15:     mapping(uint256 pairId => address quoteTokenAddress) internal _quoteTokenMap;

17:     mapping(address settlementContractAddress => bool) internal _whiteListedSettlements;
```

- *BaseMarketUpgradable.sol* ( [25-25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L25-L25), [27-27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L27-L27), [29-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L29-L29) ):

```solidity
25:     PredyPoolQuoter internal _quoter;

27:     mapping(uint256 pairId => address quoteTokenAddress) internal _quoteTokenMap;

29:     mapping(address settlementContractAddress => bool) internal _whiteListedSettlements;
```

- *GammaTradeMarket.sol* ( [48-48](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L48-L48), [50-50](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L50-L50), [51-51](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L51-L51) ):

```solidity
48:     IPermit2 internal _permit2;

50:     mapping(address owner => uint256[]) internal positionIDs;

51:     mapping(uint256 positionId => GammaTradeMarketLib.UserPosition) internal userPositions;
```

- *PerpMarketV1.sol* ( [66-66](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L66-L66) ):

```solidity
66:     IPermit2 private _permit2;
```

- *UniswapSettlement.sol* ( [13-13](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L13-L13), [14-14](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L14-L14) ):

```solidity
13:     ISwapRouter private immutable _swapRouter;

14:     IQuoterV2 private immutable _quoterV2;
```

- *SupplyToken.sol* ( [8-8](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L8-L8) ):

```solidity
8:     address immutable _controller;
```

</details>

### [N-48] Missing event when a state variables is set in constructor

The initial states set in a constructor are important and should be recorded in the event.

There is 1 instance:

- *BaseMarket.sol* ( [23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L23) ):

```solidity
23:         whitelistFiller = _whitelistFiller;
```

### [N-49] Empty bytes check is missing

Passing empty bytes to a function can cause unexpected behavior, such as certain operations failing, producing incorrect results, or wasting gas. It is recommended to check that all byte parameters are not empty.

<details>
<summary>There are 17 instances (click to show):</summary>

- *PredyPool.sol* ( [251-255](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L251-L255), [265-269](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L265-L269), [313-317](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L313-L317) ):

```solidity
/// @audit settlementData
251:     function reallocate(uint256 pairId, bytes memory settlementData)
252:         external
253:         nonReentrant
254:         returns (bool relocationOccurred)
255:     {

/// @audit settlementData
265:     function trade(TradeParams memory tradeParams, bytes memory settlementData)
266:         external
267:         nonReentrant
268:         returns (TradeResult memory tradeResult)
269:     {

/// @audit settlementData
313:     function execLiquidationCall(uint256 vaultId, uint256 closeRatio, bytes memory settlementData)
314:         external
315:         nonReentrant
316:         returns (TradeResult memory tradeResult)
317:     {
```

- *BaseMarket.sol* ( [28-33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L28-L33) ):

```solidity
/// @audit settlementData
28:     function predySettlementCallback(
29:         address quoteToken,
30:         address baseToken,
31:         bytes memory settlementData,
32:         int256 baseAmountDelta
33:     ) external onlyPredyPool {
```

- *BaseMarketUpgradable.sol* ( [49-54](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L49-L54) ):

```solidity
/// @audit settlementData
49:     function predySettlementCallback(
50:         address quoteToken,
51:         address baseToken,
52:         bytes memory settlementData,
53:         int256 baseAmountDelta
54:     ) external onlyPredyPool {
```

- *Trade.sol* ( [32-36](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol#L32-L36) ):

```solidity
/// @audit settlementData
32:     function trade(
33:         GlobalDataLibrary.GlobalData storage globalData,
34:         IPredyPool.TradeParams memory tradeParams,
35:         bytes memory settlementData
36:     ) external returns (IPredyPool.TradeResult memory tradeResult) {
```

- *LiquidationLogic.sol* ( [39-44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L39-L44) ):

```solidity
/// @audit settlementData
39:     function liquidate(
40:         uint256 vaultId,
41:         uint256 closeRatio,
42:         GlobalDataLibrary.GlobalData storage globalData,
43:         bytes memory settlementData
44:     ) external returns (IPredyPool.TradeResult memory tradeResult) {
```

- *ReallocationLogic.sol* ( [27-30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReallocationLogic.sol#L27-L30) ):

```solidity
/// @audit settlementData
27:     function reallocate(GlobalDataLibrary.GlobalData storage globalData, uint256 pairId, bytes memory settlementData)
28:         external
29:         returns (bool isRangeChanged)
30:     {
```

- *TradeLogic.sol* ( [29-33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/TradeLogic.sol#L29-L33) ):

```solidity
/// @audit settlementData
29:     function trade(
30:         GlobalDataLibrary.GlobalData storage globalData,
31:         IPredyPool.TradeParams memory tradeParams,
32:         bytes memory settlementData
33:     ) external returns (IPredyPool.TradeResult memory tradeResult) {
```

- *GammaTradeMarketL2.sol* ( [42-46](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol#L42-L46), [73-73](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol#L73-L73) ):

```solidity
/// @audit sig
42:     function executeTradeL2(GammaOrderL2 memory order, bytes memory sig, SettlementParamsV3 memory settlementParams)
43:         external
44:         nonReentrant
45:         returns (IPredyPool.TradeResult memory tradeResult)
46:     {

/// @audit sig
73:     function modifyAutoHedgeAndClose(GammaModifyOrderL2 memory order, bytes memory sig) external {
```

- *GammaTradeMarketWrapper.sol* ( [12-15](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketWrapper.sol#L12-L15) ):

```solidity
/// @audit sig
12:     function executeTrade(GammaOrder memory gammaOrder, bytes memory sig, SettlementParamsV3 memory settlementParams)
13:         external
14:         returns (IPredyPool.TradeResult memory tradeResult)
15:     {
```

- *PerpMarket.sol* ( [28-33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarket.sol#L28-L33) ):

```solidity
/// @audit sig
28:     function executeOrderV3L2(
29:         PerpOrderV3L2 memory compressedOrder,
30:         bytes memory sig,
31:         SettlementParamsV3 memory settlementParams,
32:         uint64 orderId
33:     ) external nonReentrant returns (IPredyPool.TradeResult memory) {
```

- *UniswapSettlement.sol* ( [22-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L22-L29), [38-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L38-L45), [58-58](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L58-L58), [62-62](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L62-L62) ):

```solidity
/// @audit data
22:     function swapExactIn(
23:         address,
24:         address baseToken,
25:         bytes memory data,
26:         uint256 amountIn,
27:         uint256 amountOutMinimum,
28:         address recipient
29:     ) external override returns (uint256 amountOut) {

/// @audit data
38:     function swapExactOut(
39:         address quoteToken,
40:         address,
41:         bytes memory data,
42:         uint256 amountOut,
43:         uint256 amountInMaximum,
44:         address recipient
45:     ) external override returns (uint256 amountIn) {

/// @audit data
58:     function quoteSwapExactIn(bytes memory data, uint256 amountIn) external override returns (uint256 amountOut) {

/// @audit data
62:     function quoteSwapExactOut(bytes memory data, uint256 amountOut) external override returns (uint256 amountIn) {
```

</details>

### [N-50] Don't define functions with the same name in a contract

In Solidity, while function overriding allows for functions with the same name to coexist, it is advisable to avoid this practice to enhance code readability and maintainability. Having multiple functions with the same name, even with different parameters or in inherited contracts, can cause confusion and increase the likelihood of errors during development, testing, and debugging. Using distinct and descriptive function names not only clarifies the purpose and behavior of each function, but also helps prevent unintended function calls or incorrect overriding. By adopting a clear and consistent naming convention, developers can create more comprehensible and maintainable smart contracts.

There are 2 instances:

- *BaseMarket.sol* ( [63](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L63) ):

```solidity
/// @audit Different function with same name found on line 55
63:     function _getSettlementData(IFillerMarket.SettlementParams memory settlementParams, address filler)
```

- *PositionCalculator.sol* ( [186](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L186) ):

```solidity
/// @audit Different function with same name found on line 117
186:     function calculateMinValue(uint256 _sqrtPrice, PositionParams memory _positionParams, uint256 _riskRatio)
```

### [N-51] Multiple mappings with same keys can be combined into a single struct mapping for readability

Well-organized data structures make code reviews easier, which may lead to fewer bugs. Consider combining related mappings into mappings to structs, so it's clear what data is related.

There are 2 instances:

- *PredyPool.sol* ( [38-38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L38-L38), [40-40](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L40-L40) ):

```solidity
38:     mapping(address => bool) public allowedUniswapPools;

40:     mapping(address trader => mapping(uint256 pairId => bool)) public allowedTraders;
```

### [N-52] Missing event for critical changes

Events should be emitted when critical changes are made to the contracts.

There are 2 instances:

- *BaseMarket.sol* ( [84-86](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L84-L86), [92-94](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L92-L94) ):

```solidity
84:     function updateWhitelistFiller(address newWhitelistFiller) external onlyOwner {
85:         whitelistFiller = newWhitelistFiller;
86:     }

92:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyOwner {
93:         _whiteListedSettlements[settlementContractAddress] = isEnabled;
94:     }
```

### [N-53] Non-assembly method available

There are some automated tools that will flag a project as having higher complexity if there is inline-assembly, so it's best to avoid using it where it's not necessary. In addition, most assembly methods can be replaced by non-assembly methods, for example:
- `assembly{ g := gas() }` => `uint256 g = gasleft()`
- `assembly{ id := chainid() }` => `uint256 id = block.chainid`
- `assembly { r := mulmod(a, b, d) }` => `uint256 m = mulmod(x, y, k)`
- `assembly { size := extcodesize() }` => `uint256 size = address(a).code.length`
- etc.

There are 5 instances:

- *BaseMarket.sol* ( [118-118](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L118-L118) ):

```solidity
118:             revert(add(32, data), mload(data))
```

- *BaseMarketUpgradable.sol* ( [166-166](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L166-L166) ):

```solidity
166:             revert(add(32, data), mload(data))
```

- *UniHelper.sol* ( [80-80](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L80-L80) ):

```solidity
80:                 revert(add(32, errMsg), mload(errMsg))
```

- *ReaderLogic.sol* ( [60-60](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L60-L60), [68-68](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol#L68-L68) ):

```solidity
60:             revert(add(32, data), mload(data))

68:             revert(add(32, data), mload(data))
```

### [N-54] Consider adding emergency-stop functionality

Adding a way to quickly halt protocol functionality in an emergency, rather than having to pause individual contracts one-by-one, will make in-progress hack mitigation faster and much less stressful.

<details>
<summary>There are 10 instances (click to show):</summary>

- *PredyPool.sol* ( [28-28](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L28-L28) ):

```solidity
28: contract PredyPool is IPredyPool, IUniswapV3MintCallback, Initializable, ReentrancyGuardUpgradeable {
```

- *PriceFeed.sol* ( [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L9), [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L29) ):

```solidity
9: contract PriceFeedFactory {

29: contract PriceFeed {
```

- *GammaTradeMarket.sol* ( [24-24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L24-L24) ):

```solidity
24: contract GammaTradeMarket is IFillerMarket, BaseMarketUpgradable, ReentrancyGuardUpgradeable {
```

- *GammaTradeMarketL2.sol* ( [40-40](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol#L40-L40) ):

```solidity
40: contract GammaTradeMarketL2 is GammaTradeMarket {
```

- *GammaTradeMarketWrapper.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketWrapper.sol#L10-L10) ):

```solidity
10: contract GammaTradeMarketWrapper is GammaTradeMarketL2 {
```

- *PerpMarket.sol* ( [27-27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarket.sol#L27-L27) ):

```solidity
27: contract PerpMarket is PerpMarketV1 {
```

- *PerpMarketV1.sol* ( [29-29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L29-L29) ):

```solidity
29: contract PerpMarketV1 is BaseMarketUpgradable, ReentrancyGuardUpgradeable {
```

- *UniswapSettlement.sol* ( [10-10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L10-L10) ):

```solidity
10: contract UniswapSettlement is ISettlement {
```

- *SupplyToken.sol* ( [7-7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L7-L7) ):

```solidity
7: contract SupplyToken is ERC20, ISupplyToken {
```

</details>

### [N-55] Avoid the use of sensitive terms

Use [alternative variants](https://www.zdnet.com/article/mysql-drops-master-slave-and-blacklist-whitelist-terminology/), e.g. allowlist/denylist instead of whitelist/blacklist.

<details>
<summary>There are 40 instances (click to show):</summary>

- *BaseMarket.sol* ( [11](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L11), [17](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L17), [19](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L19), [23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L23), [36](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L36), [81](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L81), [84](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L84), [85](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L85), [89](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L89), [92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L92), [93](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol#L93) ):

```solidity
11:     address public whitelistFiller;

17:     mapping(address settlementContractAddress => bool) internal _whiteListedSettlements;

19:     constructor(IPredyPool predyPool, address _whitelistFiller, address quoterAddress)

23:         whitelistFiller = _whitelistFiller;

36:         SettlementCallbackLib.validate(_whiteListedSettlements, settlementParams);

81:      * @notice Updates the whitelist filler address

84:     function updateWhitelistFiller(address newWhitelistFiller) external onlyOwner {

85:         whitelistFiller = newWhitelistFiller;

89:      * @notice Updates the whitelist settlement address

92:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyOwner {

93:         _whiteListedSettlements[settlementContractAddress] = isEnabled;
```

- *BaseMarketUpgradable.sol* ( [23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L23), [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L29), [32](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L32), [38](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L38), [44](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L44), [57](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L57), [125](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L125), [128](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L128), [129](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L129), [137](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L137), [140](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L140), [141](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol#L141) ):

```solidity
23:     address public whitelistFiller;

29:     mapping(address settlementContractAddress => bool) internal _whiteListedSettlements;

32:         if (msg.sender != whitelistFiller) revert CallerIsNotFiller();

38:     function __BaseMarket_init(IPredyPool predyPool, address _whitelistFiller, address quoterAddress)

44:         whitelistFiller = _whitelistFiller;

57:         SettlementCallbackLib.validate(_whiteListedSettlements, settlementParams);

125:      * @notice Updates the whitelist filler address

128:     function updateWhitelistFiller(address newWhitelistFiller) external onlyFiller {

129:         whitelistFiller = newWhitelistFiller;

137:      * @notice Updates the whitelist settlement address

140:     function updateWhitelistSettlement(address settlementContractAddress, bool isEnabled) external onlyFiller {

141:         _whiteListedSettlements[settlementContractAddress] = isEnabled;
```

- *SettlementCallbackLib.sol* ( [30](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L30), [34](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L34), [36](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol#L36) ):

```solidity
30:         mapping(address settlementContractAddress => bool) storage _whiteListedSettlements,

34:             settlementParams.contractAddress != address(0) && !_whiteListedSettlements[settlementParams.contractAddress]

36:             revert IFillerMarket.SettlementContractIsNotWhitelisted();
```

- *GammaTradeMarket.sol* ( [69](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L69), [74](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L74), [179](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L179), [180](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L180) ):

```solidity
69:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)

74:         __BaseMarket_init(predyPool, whitelistFiller, quoterAddress);

179:             // only whitelisted filler can open position

180:             if (msg.sender != whitelistFiller) {
```

- *PerpMarketV1.sol* ( [92](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L92), [97](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L97), [201](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L201), [202](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L202) ):

```solidity
92:     function initialize(IPredyPool predyPool, address permit2Address, address whitelistFiller, address quoterAddress)

97:         __BaseMarket_init(predyPool, whitelistFiller, quoterAddress);

201:             // only whitelisted filler can open position

202:             if (msg.sender != whitelistFiller) {
```

</details>

### [N-56] Use the Modern Upgradeable Contract Paradigm

Modern smart contract development often employs upgradeable contract structures, utilizing proxy patterns like OpenZeppelin’s Upgradeable Contracts. This paradigm separates logic and state, allowing developers to amend and enhance the contract's functionality without altering its state or the deployed contract address. Transitioning to this approach enhances long-term maintainability.
Resolution: Adopt a well-established proxy pattern for upgradeability, ensuring proper initialization and employing transparent proxies to mitigate potential risks. Embrace comprehensive testing and audit practices, particularly when updating contract logic, to ensure state consistency and security are preserved across upgrades. This ensures your contract remains robust and adaptable to future requirements.

There are 3 instances:

- *PriceFeed.sol* ( [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L29) ):

```solidity
29: contract PriceFeed {
```

- *UniswapSettlement.sol* ( [10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol#L10) ):

```solidity
10: contract UniswapSettlement is ISettlement {
```

- *SupplyToken.sol* ( [7](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol#L7) ):

```solidity
7: contract SupplyToken is ERC20, ISupplyToken {
```

### [N-57] Large or complicated code bases should implement invariant tests

This includes: large code bases, or code with lots of inline-assembly, complicated math, or complicated interactions between multiple contracts.
Invariant fuzzers such as Echidna require the test writer to come up with invariants which should not be violated under any circumstances, and the fuzzer tests various inputs and function calls to ensure that the invariants always hold.
Even code with 100% code coverage can still have bugs due to the order of the operations a user performs, and invariant fuzzers may help significantly.

There is 1 instance:

- Global finding

### [N-58] The default value is manually set when it is declared

In instances where a new variable is defined, there is no need to set it to it's default value.

There are 5 instances:

- *LiquidationLogic.sol* ( [87-87](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol#L87-L87) ):

```solidity
87:         uint256 sentMarginAmount = 0;
```

- *ArrayLib.sol* ( [23-23](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/ArrayLib.sol#L23-L23) ):

```solidity
23:         for (uint256 i = 0; i < items.length; i++) {
```

- *GammaTradeMarket.sol* ( [366-366](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L366-L366) ):

```solidity
366:         for (uint64 i = 0; i < userPositionIDs.length; i++) {
```

- *L2GammaDecoder.sol* ( [65-65](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol#L65-L65) ):

```solidity
65:         uint32 isEnabledUint = 0;
```

- *PerpMarketV1.sol* ( [117-117](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L117-L117) ):

```solidity
117:             uint256 cost = 0;
```

### [N-59] Contracts should have all `public`/`external` functions exposed by `interface`s

All `external`/`public` functions should extend an `interface`. This is useful to ensure that the whole API is extracted and can be more easily integrated by other projects.

<details>
<summary>There are 8 instances (click to show):</summary>

- *PredyPool.sol* ( [28](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol#L28) ):

```solidity
28: contract PredyPool is IPredyPool, IUniswapV3MintCallback, Initializable, ReentrancyGuardUpgradeable {
```

- *PriceFeed.sol* ( [9](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L9), [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol#L29) ):

```solidity
9: contract PriceFeedFactory {

29: contract PriceFeed {
```

- *GammaTradeMarket.sol* ( [24](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol#L24) ):

```solidity
24: contract GammaTradeMarket is IFillerMarket, BaseMarketUpgradable, ReentrancyGuardUpgradeable {
```

- *GammaTradeMarketL2.sol* ( [40](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol#L40) ):

```solidity
40: contract GammaTradeMarketL2 is GammaTradeMarket {
```

- *GammaTradeMarketWrapper.sol* ( [10](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketWrapper.sol#L10) ):

```solidity
10: contract GammaTradeMarketWrapper is GammaTradeMarketL2 {
```

- *PerpMarket.sol* ( [27](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarket.sol#L27) ):

```solidity
27: contract PerpMarket is PerpMarketV1 {
```

- *PerpMarketV1.sol* ( [29](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol#L29) ):

```solidity
29: contract PerpMarketV1 is BaseMarketUpgradable, ReentrancyGuardUpgradeable {
```

</details>

### [N-60] Consider adding formal verification proofs

Formal verification is the act of proving or disproving the correctness of intended algorithms underlying a system with respect to a certain formal specification/property/invariant, using formal methods of mathematics.

Some tools that are currently available to perform these tests on smart contracts are [SMTChecker](https://docs.soliditylang.org/en/latest/smtchecker.html) and [Certora Prover](https://www.certora.com/).

<details>
<summary>There are 55 instances (click to show):</summary>

- [*PredyPool.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PredyPool.sol)

- [*PriceFeed.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/PriceFeed.sol)

- [*BaseHookCallback.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallback.sol)

- [*BaseHookCallbackUpgradable.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseHookCallbackUpgradable.sol)

- [*BaseMarket.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarket.sol)

- [*BaseMarketUpgradable.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/BaseMarketUpgradable.sol)

- [*SettlementCallbackLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/base/SettlementCallbackLib.sol)

- [*ApplyInterestLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ApplyInterestLib.sol)

- [*Constants.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Constants.sol)

- [*DataType.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/DataType.sol)

- [*InterestRateModel.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/InterestRateModel.sol)

- [*PairLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PairLib.sol)

- [*Perp.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Perp.sol)

- [*PerpFee.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol)

- [*PositionCalculator.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol)

- [*PremiumCurveModel.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PremiumCurveModel.sol)

- [*Reallocation.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Reallocation.sol)

- [*ScaledAsset.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/ScaledAsset.sol)

- [*SlippageLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/SlippageLib.sol)

- [*Trade.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/Trade.sol)

- [*UniHelper.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol)

- [*VaultLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/VaultLib.sol)

- [*AddPairLogic.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/AddPairLogic.sol)

- [*LiquidationLogic.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/LiquidationLogic.sol)

- [*ReaderLogic.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReaderLogic.sol)

- [*ReallocationLogic.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReallocationLogic.sol)

- [*SupplyLogic.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/SupplyLogic.sol)

- [*TradeLogic.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/TradeLogic.sol)

- [*Bps.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Bps.sol)

- [*LPMath.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/LPMath.sol)

- [*Math.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/math/Math.sol)

- [*DecayLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/DecayLib.sol)

- [*OrderInfoLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/OrderInfoLib.sol)

- [*Permit2Lib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/Permit2Lib.sol)

- [*ResolvedOrder.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/orders/ResolvedOrder.sol)

- [*L2Decoder.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/L2Decoder.sol)

- [*ArrayLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/ArrayLib.sol)

- [*GammaOrder.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaOrder.sol)

- [*GammaTradeMarket.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarket.sol)

- [*GammaTradeMarketL2.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketL2.sol)

- [*GammaTradeMarketLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketLib.sol)

- [*GammaTradeMarketWrapper.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/GammaTradeMarketWrapper.sol)

- [*L2GammaDecoder.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/gamma/L2GammaDecoder.sol)

- [*PerpMarket.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarket.sol)

- [*PerpMarketLib.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketLib.sol)

- [*PerpMarketV1.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpMarketV1.sol)

- [*PerpOrder.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrder.sol)

- [*PerpOrderV3.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/markets/perp/PerpOrderV3.sol)

- [*UniswapSettlement.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/settlements/UniswapSettlement.sol)

- [*SupplyToken.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/tokenization/SupplyToken.sol)

- [*GlobalData.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/GlobalData.sol)

- [*LockData.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/types/LockData.sol)

- [*AggregatorV3Interface.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/vendors/AggregatorV3Interface.sol)

- [*IPyth.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/vendors/IPyth.sol)

- [*IUniswapV3PoolOracle.sol*](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/vendors/IUniswapV3PoolOracle.sol)

</details>

### [N-61] Use scopes sparingly

The use of scoped blocks, denoted by `{}` without a preceding control structure like `if`, `for`, etc., allows for the creation of isolated scopes within a function. While this can be useful for managing memory and preventing naming conflicts, it should be used sparingly. Excessive use of these scope blocks can obscure the code's logic flow and make it more difficult to understand, impeding code maintainability. As a best practice, only employ scoped blocks when necessary for memory management or to avoid clear naming conflicts. Otherwise, aim for clarity and simplicity in your code structure for optimal readability and maintainability.

<details>
<summary>There are 7 instances (click to show):</summary>

- *PerpFee.sol* ( [24-25](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L24-L25), [32-33](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PerpFee.sol#L32-L33) ):

```solidity
24:         {
25:             (int256 rebalanceInterestBase, int256 rebalanceInterestQuote) = computeRebalanceInterest(

32:         {
33:             (int256 feeUnderlying, int256 feeStable) = computePremium(assetStatus, userStatus.sqrtPerp);
```

- *PositionCalculator.sol* ( [196-197](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L196-L197), [203-204](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/PositionCalculator.sol#L203-L204) ):

```solidity
196:         {
197:             int256 v = calculateValue(upperPrice, _positionParams);

203:         {
204:             int256 v = calculateValue(lowerPrice, _positionParams);
```

- *UniHelper.sol* ( [114-115](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L114-L115), [131-132](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/UniHelper.sol#L131-L132) ):

```solidity
114:             {
115:                 (,, uint256 lowerFeeGrowthOutside0X128, uint256 lowerFeeGrowthOutside1X128,,,,) =

131:             {
132:                 (,, uint256 upperFeeGrowthOutside0X128, uint256 upperFeeGrowthOutside1X128,,,,) =
```

- *ReallocationLogic.sol* ( [44-45](https://github.com/code-423n4/2024-05-predy/blob/a9246db5f874a91fb71c296aac6a66902289306a/./src/libraries/logic/ReallocationLogic.sol#L44-L45) ):

```solidity
44:         {
45:             int256 deltaPositionBase;
```

</details>
