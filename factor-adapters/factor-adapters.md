# 🔌 Factor Adapters

## Overview

Factor Adapters enables [Factor Studio](../solutions/factor-studio.md) to securely and permissionlessly interact with external DeFi protocols on-chain. Factor Adapters generalizes core financial operations by implementing protocol-specific smart contracts that interface directly with external protocol smart contracts. The adapter smart contracts forms the base of the composability layer which Factor is building.

By abstracting protocol-specific code across various financial segments, Factor Adapters enables multiple financial functions to be combined into a single multi-step transaction via the [Strategy Builder](../solutions/strategy-builder.md). Consequently, users can drag-and-drop strategy Building Blocks in a simple interface with the Strategy Builder handling the batching of the required protocol-specific adapters.

All Adapter smart contracts are audited to ensure the correct handling and safety of user funds when integrating with external protocols.
