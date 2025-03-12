# Documentation *(work in progress)*

This documentation is a work in progress. It will be updated as new features are added.

With the Galactica hardfork, the following API endpoints and flags are introduced.

## Endpoints

- `fees/history`: Similar to [`eth_feeHistory`](https://docs.metamask.io/services/reference/ethereum/json-rpc-methods/eth_feehistory/), allows you to retrieve the information about a range of block base fees and gas used ratios. 

    _Request parameters_:

    - `blockCount`: Number of blocks to retrieve.
    - `newestBlock`: The highest block number to retrieve, its value is a `revision` following the existing VeChainThor endpoints.

    _Response parameters_:
    The range might not be `newestBlock` - `blockCount` necessarily if the oldest block does not exist/is not included because of the backtrace limit (see flags below for more details about this limit)

    - `oldestBlock`: Oldest block in the requested range. 
    - `baseFees`: Array of block base fees for the requested range
    - `gasUsedRatios`: Array of gas ratios (block gas used divided by the block gas limit) for the requested range

- `fees/priority`: Similar to [`eth_maxPriorityFeePerGas`](https://docs.metamask.io/services/reference/ethereum/json-rpc-methods/eth_maxpriorityfeepergas/), suggests a tip that is enough to be included as the `maxPriorityFeePerGas` value in a transaction so it is included in the closest possible block.

    _Response parameters_:
    - `maxPriorityFeePerGas`: Tip value to be used as the `maxPriorityFeePerGas` in a transaction (also to be considered for `maxFeePerGas` since it is the block base fee + this tip)

## Flags

Blabla

## Run Galactica with Thor Solo

Blabla