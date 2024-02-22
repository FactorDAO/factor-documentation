# 🔀 Swap

## Overview

The Swap Building Block enables users to conveniently access deeper and more efficient liquidity for their specific trading requirements through smart trade routing and automated conditional swaps. Through routing the trades via various integrated AMM DEXs and DEX Aggregators, the Swap Building Block is able to objectively discover more capital efficient liquidity sources thereby ensuring favourable swap rates while encouraging greater market stability.

The Swap Building Block supports more advanced orders offering users the flexibility when creating strategies:

* **Market Orders:** Instantly swap at favourable rates as the order is executed upon strategy execution.
* **Conditional Market Orders (a.k.a Conditional Swaps):** Set your preferred price threshold and your market order will be triggered when the market matches your selected price.
* **Stop Loss Market Orders (a.k.a Stop Loss Swaps):** Cap your losses by setting a price threshold below the current market price and your trade is immediately executed when the market price matches your Stop Loss price.
* **Profit Taking Market Orders (a.k.a Profit Taking Swaps):** Secure your profits by setting a price threshold above the current market price and your trade is immediately executed when the market price matches your Profit Taking price.

The Swap Building Block functions as an automation and optimization layer between the incoming swap request and the multiple integrated liquidity protocols. With the Swap Building Block, strategies can easily swap between any ERC20 token thereby creating endless possibilities for multi-token strategies.

<details>

<summary>Related Concepts</summary>

* [Market Orders](concepts/market-orders.md)
* [DEX Aggregators](concepts/dex-aggregators.md)

</details>

## Features

* **Swap At Superior Rates:** By aggregating liquidity across multiple liquidity sources, the Swap Building Block is able to uncover more capital efficient liquidity for a swap.
* **Smart Trade Routing:** Specify your swap parameters and the Swap Building Block automatically optimizes the swap route for better rates.
* **Automated Conditional Swaps:** Create predefined triggers for your swap and the Swap Building Block automatically executes the transaction when the corresponding market conditions are met.

## Integrations

Factor has integrated with leading yield farming protocols, offering a broad spectrum of possibilities for your strategies.

* [OpenOcean](https://openocean.finance/)
* [Trader Joe](https://www.traderjoexyz.com/)
* [Uniswap V3](https://uniswap.org/)
* [Vela Exchange](https://www.vela.exchange/)

Visit our [**Discover**](https://app.factor.fi/discover) page to see the latest swap strategies.

{% hint style="success" %}
**Don't Limit Your Strategies To Just Swaps**

[Factor Studio](../../factor-studio/factor-studio.md) enables different [Building Blocks](../factor-building-blocks.md) to be mixed-and-matched thereby facilitating multi-step strategies which span across the whole DeFi ecosystem.

Please refer to [Supported Protocols](../../getting-started/supported-protocols.md) to view the full list of DeFi protocols which have been integrated with Factor Studio.
{% endhint %}
