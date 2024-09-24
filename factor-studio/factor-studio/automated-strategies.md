# Automated Strategies

## Overview

Factor Studio comes packaged with [Gelato Web3 Functions](https://docs.gelato.network/web3-services/web3-functions) enabling you to define time-based triggers for your strategies. Execute your strategy at a specified time or recurrently execute your strategy at configured intervals.

* **Time Based Triggers:** Automatically trigger your strategy at a specified time to take advantage of varying market conditions in the future.
* **Periodic Triggers:** Execute your strategy at specified intervals to regularly adjust your position’s liquidity allocations.
* **Rule Based Triggers:** Pair this with the IF Conditional Building Block and automatically trigger your strategy whenever your target condition is reached.

{% embed url="https://www.gelato.network/web3-functions" %}

## Automating Your Strategies

You can easily add time-based triggers to any of your mix-and-match strategies via the Factor Studio interface. Automation triggers are specified at a per strategy level enabling you to chain as many [Factor Building Blocks](../../factor-building-blocks/factor-building-blocks.md) into a single automated strategy, By pairing recurring triggers with the IF Conditional Building Block, your strategies can be automatically executed only when the market conditions are suitable.

Strategy automation is fully on-chain thereby ensuring the reliability of strategy execution. Due to this design, you will first have to prefund your strategy with the required gas tokens for the transaction. Your strategy will not be executed if there is insufficient gas in the strategy contract.

Reduce your manual overheads and take advantage of market conditions by automating your strategies on Factor Studio.
