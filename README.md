# Thor Galactica

<div align="center">
  <img src=".github/project-logo.png" alt="Thor Galactica Logo" width="200">
</div>

Welcome to **Thor Galactica** – the central repository for all artifacts, information, and documentation related to the Galactica hardfork for VeChain Thor.

## Overview

The **Galactica hardfork** marks a significant milestone in VeChain's evolution, introducing several critical improvements to the protocol:

- **Dynamic Fee Market (VIP-251)**: Replacing the fixed-fee model with a dynamic fee market inspired by Ethereum's EIP-1559
- **Typed Transactions (VIP-252)**: A new standardized transaction envelope format for better transaction management inspired by Ethereum's EIP-2718
- **EVM Upgrade (VIP-242)**: Aligning with Ethereum's Shanghai EVM capabilities for greater compatibility
- **Extension Contract v3 (VIP-250)**: Enhanced functions for developers to simplify contract execution

## Documentation

For comprehensive information about Galactica, check out:

- **[Galactica branch](https://github.com/vechain/thor/tree/release/galactica)**: Thor Galactica release branch
- **[VIPs](.github/vip.md)**: VeChain Improvement Proposals implemented in Galactica
- **[Genesis Instructions](.github/genesis.md)**: Step-by-step guide to generate genesis files

## [New API Endpoints](.github/docs/README.md#endpoints)

- `fees/history`: Retrieve information about block base fees, gas used ratios, and rewards
- `fees/priority`: Get recommended priority fee values for transactions