---
description: Building DeFi Accessibility Block-By-Block
---

# 🧱 Factor Building Blocks

## Overview

Factor Building Blocks enable the composability of various DeFi strategies by abstracting the operational logic of each segment into its own Building Block. For example, the Leverage Building Block contains all the functions required for users to manage loans across multiple integrated lending protocols. Building Blocks allow users to focus on strategy creation without having to worry about the nitty-gritty details of strategy implementation.

Each Building Block specifies a standard interface that ensures that a user’s intention is consistently and intuitively translated into actionable strategies, regardless of the underlying protocol. For example, a user can just specify a token and token amount and the Leverage Building Block will handle the creation of the position on the selected protocol.

## Building Block Types

To support the creation of multi-step strategies, Factor Building Blocks are divided into 3 block types.

### Action Blocks

Blocks that facilitate actions with an integrated protocol (i.e. lend, swap, etc.). Each Action Block specifies:

* **Input Parameters:** Strategy parameters to be passed into the Building Block that defines how the block will interact with a specified protocol function.
* **Output Data:** Simulated output data that estimates the outcome of a particular Action Block. This functions as the input parameters for a subsequent block and enables Building Blocks to be chained.
* **Transaction Information:** Other related transaction information that enables the user to make an informed decision prior to transaction confirmation.

Action Blocks are further divided into different categories that logically align with the different financial segments:

<table data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="leverage/"><strong>Leverage</strong></a></td><td></td><td></td></tr><tr><td><a href="yield/"><strong>Yield</strong></a></td><td></td><td></td></tr><tr><td><a href="flash-loan/"><strong>Flash Loan</strong></a></td><td></td><td></td></tr><tr><td><a href="swap/"><strong>Swap</strong></a></td><td></td><td></td></tr><tr><td>Liquidity Pool Management</td><td></td><td></td></tr><tr><td>Indices</td><td></td><td></td></tr></tbody></table>

### Conditional Blocks

Blocks that enable conditional logic (i.e. if/else) to be specified as part of the end-to-end strategy. Blocks which are encapsulated by a Conditional Block will only execute whenever a specified condition is met. This enables the creation of more complex strategies which are able to respond to market conditions at the point of transaction execution.

### Suggestion Blocks

In an effort to improve the strategy building experience, Factor has also created Suggestion Blocks which automatically recommends the next block to be added to the strategy. Suggestion Blocks recommends commonly used patterns based on the outputs of the previous block in order to save a Strategy Builder's time.
