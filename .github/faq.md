# Frequently Asked Questions (FAQ)

## Table of Contents
- [Development and Compatibility](#development-and-compatibility)
  - [Connex Compatibility](#will-my-dapp-using-connex-break-after-the-hardfork)
  - [Thor-devkit Compatibility](#will-my-dapp-using-thor-devkit-break-after-the-hardfork)
  - [Dependencies](#where-can-i-check-my-dependencies)
  - [Product Upgrades](#which-products-will-be-upgraded-to-support-galactica)
  - [Version Support](#which-versions-support-galactica)
- [Node Operations](#node-operations)
  - [Local Node Upgrades](#should-i-upgrade-my-local-node-for-running-my-dapp-in-which-circumstances)
  - [Indexer Behavior](#what-is-the-expected-behavior-for-indexers-after-the-hardfork)
- [Wallets and Public Nodes](#wallets-and-public-nodes)
  - [Sync Wallet Compatibility](#can-i-keep-using-sync-and-sync-2)
  - [Public Node Upgrades](#which-public-nodes-will-upgrade-to-galactica)
  - [Node Upgrade Verification](#how-can-i-check-if-a-public-node-is-upgraded)
- [User Funds and Safety](#user-funds-and-safety)
  - [VeWorld Safety](#i-am-using-veworld-should-i-do-anything-to-avoid-losing-money)
- [Technical Differences with Ethereum](#technical-differences-with-ethereum)
  - [Dynamic Fee Implementation](#how-does-vechains-dynamic-fee-implementation-differ-from-ethereums)
- [Bug Reporting](#bug-reporting)
  - [Reporting Issues](#how-could-i-report-bugs)

## Development and Compatibility

### Will my dapp using Connex break after the Hardfork?
No, your dapp will continue to function, but it will not have access to dynamic typed transactions.
Note that Connex is deprecated - we strongly recommend updating your dApp to use the SDK.

### Will my dapp using Thor-devkit break after the Hardfork?
Similar to Connex, we recommend migrating to the SDK for better compatibility and features.

### Where can I check my dependencies?
You should review your dApp's dependencies in your project's package management files.

### Which products will be upgraded to support Galactica?
All VeChain Foundation supported products will be upgraded to support Galactica.

### Which versions support Galactica?
We recommend always using the latest release versions of all products for optimal compatibility.

## Node Operations

### Should I upgrade my local node for running my dapp? In which circumstances?
Yes, upgrading is necessary. All nodes should be updated once the official release is available.
If you are running a node on testnet, please monitor announcements for testnet release candidates.

### What is the expected behavior for indexers after the Hardfork?
Indexers will need to be updated to handle new fields in the block structure and support the new dynamic fee transaction type.

## Wallets and Public Nodes

### Can I keep using Sync and Sync 2?
While these legacy wallets will continue to function, we strongly recommend migrating to VeWorld for the best user experience and latest features.

### Which public nodes will upgrade to Galactica?
All public nodes will be upgraded to support Galactica.

### How can I check if a Public node is upgraded?
You can verify if a node is upgraded by checking its Thorest API version.

## User Funds and Safety

### I am using VeWorld, should I do anything to avoid losing money?
No action is required. Your funds are completely safe.

## Technical Differences with Ethereum

### How does VeChain's dynamic fee implementation differ from Ethereum's?
While both VeChain and Ethereum implement dynamic fee markets, there are some key differences in how they handle gas pricing:

1. **Ethereum's Approach:**
   - Added a new field called `EffectiveGasPrice` to transaction receipts
   - Calculated as: `EffectiveGasPrice = tx.MaxPriorityFeePerGas + Min(tx.MaxFeePerGas - tx.MaxPriorityFeePerGas, BlockHeader.BaseFee)`

2. **VeChain's Approach:**
   - No need for an additional `EffectiveGasPrice` field
   - Can be calculated directly from the receipt: `EffectiveGasPrice = Receipt.Paid / Receipt.GasUsed`
   - This simpler approach maintains backward compatibility while providing the same information

This difference is particularly important for wallet developers and teams working with transaction receipts, as they should use the VeChain-specific calculation method.

## Bug Reporting

### How could I report bugs?
Please report any issues, bugs, or questions in the [Issues Section](https://github.com/vechain/thor-galactica/issues)
