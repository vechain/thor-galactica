# Documentation *(Work in Progress)*

This documentation is a work in progress and will be updated as new features are added.

## Key concepts

| Name | Description |
|------|-------------|
| **MaxFeePerGas** | The maximum total gas price a user is willing to pay for their transaction. |
| **MaxPriorityFeePerGas** | The maximum tip a user is willing to pay validators to prioritize their transaction. |
| **EffectiveGasPrice** | The final gas price charged when the transaction was executed. |
| **EffectivePriorityPrice** | The final tip amount paid to the validator who included the transaction. |
| **BaseFeePerGas** | The minimum gas price required for a transaction to be included in the current block.|


## Methodology

### Before Galactica

The pre-Galactica transaction model implements a fixed gas pricing mechanism with the following characteristics:

1. **Limited Gas Price Range**: Legacy transactions operate within a constrained gas price range
2. **Fixed Validator Tip**: Validators receive a fixed 30% of the total gas fee paid by users
3. **Base Gas Price**: A network parameter (currently set at 1e13 wei) that can be adjusted by the steering committee

### After Galactica

Galactica introduces a more flexible and efficient fee mechanism that supports two transaction types:

#### 1. Legacy Transactions
- Maintains backward compatibility with the original gas price formula:
  ```
  gasPrice = BaseGasPrice * (1 + GasPriceCoef/255)
  ```
- Continues to operate within the established gas price range

#### 2. Dynamic Fee Transactions
- Introduces two new parameters:
  - `maxFeePerGas`: Maximum total fee per gas unit
  - `maxPriorityFeePerGas`: Maximum priority fee (tip) per gas unit
- Both parameters can range from 0 to 2^256 - 1 wei, offering significantly greater flexibility
- Implements EIP-1559 style dynamic fee market mechanism

#### Fee Market Mechanism

1. **Base Fee Adjustment**:
   - Automatically adjusts based on previous block's gas utilization
   - Base fee is completely burned, reducing overall token supply

2. **Transaction Field Mapping**:
   - Both transaction types use `maxFeePerGas` and `maxPriorityFeePerGas`
   - For legacy transactions:
     ```
     maxFeePerGas = gasPrice
     maxPriorityFeePerGas = gasPrice
     ```

3. **Effective Fee Calculation**:
   - Effective Gas Price (amount user pays per gas):
     ```
     Min(block.BaseFee + tx.maxPriorityFeePerGas, tx.maxFeePerGas)
     ```
   - Effective Priority Fee (tip to validator per gas):
     ```
     Min(tx.maxPriorityFeePerGas, tx.maxFeePerGas - block.BaseFee)
     ```
#### Notable Changes

1. **Legacy Transaction Gas Price Constraints**: Legacy transactions are bound by a fixed gas price range of `1e13` to `2 * 1e13 wei`. These transactions may become un-executable during high network activity periods when `block.baseFee` exceeds `2 * 1e13 wei`.

2. **Base Fee Refund Mechanism**: Dynamic fee transactions introduce a refund feature through independent `maxFeePerGas` and `maxPriorityFeePerGas` settings. When `block.baseFee` is less than `tx.maxFeePerGas - tx.maxPriorityFeePerGas`, users receive a refund of `tx.maxFeePerGas - tx.maxPriorityFeePerGas - block.baseFee` per gas unit. Legacy transactions do not support this refund mechanism.

3. **Transaction Pricing Exclusion**: Both transaction types may become un-executable if the user-specified gas price (`tx.maxFeePerGas` for dynamic fee transactions or `tx.gasPriceCoef` for legacy transactions) falls below the current block's base fee.

## Endpoints

- `fees/history`: Similar to [`eth_feeHistory`](https://docs.metamask.io/services/reference/ethereum/json-rpc-methods/eth_feehistory/), this endpoint allows you to retrieve information about a range of block base fees, gas used ratios and reward.

    _Request parameters_:

    - `rewardPercentiles`: The percentiles of the rewards to be returned. Each percentile value must be between 0 and 100 and in ascending order. Values should be comma-separated. *For example: ?rewardPercentiles=25,50,75*
    - `blockCount`: The number of blocks to retrieve.
    - `newestBlock`: The highest block number to retrieve, its value is a `revision` following the existing VeChainThor endpoints.

    _Response parameters_:
    The range might not necessarily be `newestBlock` - `blockCount` if the oldest block does not exist or is not included due to the backtrace limit (see flags below for more details about this limit). `blockCount` can be higher than the backtrace limit, but the response will include only values within the valid range.

    - `oldestBlock`: The oldest block in the requested range.
    - `baseFeePerGas`: An array of block base fees for the requested range.
    - `gasUsedRatio`: An array of gas ratios (block gas used divided by the block gas limit) for the requested range.
    - `reward`: An array of arrays of rewards by the percentiles provided in the request via *rewardPercentiles*. Each inner array contains the reward values for each percentile requested.

- `fees/priority`: Similar to [`eth_maxPriorityFeePerGas`](https://docs.metamask.io/services/reference/ethereum/json-rpc-methods/eth_maxpriorityfeepergas/), this endpoint recommends an optimal tip value to use as `maxPriorityFeePerGas` in a transaction. Setting this recommended tip increases the likelihood of swift block inclusion.

    _Response parameters_:
    - `maxPriorityFeePerGas`: The tip value to be used as the `maxPriorityFeePerGas` in a transaction (also to be considered for `maxFeePerGas` since it is the block base fee plus this tip).

The full definition of the endpoints can be found in [thor.yaml](../../thor/api/doc/thor.yaml).

## Flags

New flags have been introduced to configure the behavior of Galactica. As mentioned in the endpoints, the existing backtrace limit is used by `fees/history`:

- `--api-priority-fees-percentage`: This is a percentage applied to the most recent block base fee (`next`) to suggest a tip for the `fees/priority` endpoint. The default value is 5 (5%).
- `--min-effective-priority-fee`: The minimum effective priority (the minimum between `maxPriorityFeePerGas` and `maxFeePerGas - block base fee`) that can be used in a transaction. The default value is 0, so this flag is optional.
- `--api-backtrace-limit`: The backtrace limit, starting from the `best` block. The default value is 1000.

A full up-to-date description of the flags can be found in the [usage documentation](../../thor/docs/usage.md#command-line-options).

## Run Galactica with Thor Solo

To run Galactica with Thor Solo, follow the instructions [here](../../thor/docs/usage.md#thor-solo).

The only difference will be the location of the binary, which is `thor/bin/thor` from the root folder of this repository. All the flags and endpoints mentioned above apply.
