# Conditional Strategies

## Overview

React in real time to market changes by equipping your automated strategies on Factor with conditional if-else logic. The IF Conditional Building Block enables you to specify strategy flows based on pre-defined conditions. The conditions are checked against a reliable data oracle during execution to ensure the reliability of your drag-and-drop strategy on the Factor Studio.

* **Conditional Execution:** Respond to market conditions in real time as your strategy executes alternative flows based on your pre-set conditions.
* **Rule Based Triggers:** Pair this with [Factor Studio Automation](automated-strategies.md) and automatically trigger your strategy whenever your target condition is reached.

## Rule Based Strategies

The IF Conditional Building Block supplements the core DeFi Building Blocks enabling you to add rule-based flows to your strategy that is checked during strategy execution. This means you can pre-define any number of conditions for your strategy to follow thereby giving you fine grained control over how your strategy is executed no matter the market conditions.

Conditions are checked against data from [Chainlink](https://chain.link/) to ensure the security and reliability of the checks. The IF Conditional Building Block supports checking data for the following data types:

* Token
* Protocol (🚧)
* Position (🚧)
* Yield (🚧)
* Custom (🚧)

By chaining together various DeFi primitives with conditional logic, Factor Building Blocks allows anyone to create complex multi-protocol strategies with no coding knowledge required. You can drag-and-drop strategies from across DeFi into a single transaction and automatically execute it based on various market conditions.

Additionally, Factor Studio also enables time-based automations whereby you can trigger strategy execution at a specified time or recurrently execute your strategy at specified intervals.

## Things To Note

* **Strategy Execution Sequence:** Your strategy will be executed sequentially based on the the order of your selected building blocks (i.e. top to bottom based on the Strategy Builder UI). As such, any IF Conditionals will also follow this sequence.
* **Gas Costs:** As the strategy will be checked on execution, the checking of conditionals will still consume gas. If the condition is not met, the strategy will skip ahead to the next building block after the IF Conditional block thereby not incurring gas on the part of strategy defined within the IF Conditional block.
* **Strategy Termination:** All strategies will be executed in full with any remaining strategy after conditional blocks being executed until the final block in your strategy. Please use opposing IF Conditional blocks if your strategy flows might result in token reuse.
