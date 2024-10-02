# Automated Scale Order

## Overview

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Automatically add single-sided concentrated liquidity when your target price is reached and DCA into/out of a token while earning AMM trading fees. All of your tokens are traded against as the market traverses over your selected range in a single direction. Additionally, your position also earns trading fees for any bi-directional trades that occurs within the range.

## Potential Alpha

* **Gradually Buy At Lower Prices:** Purchase tokens along a smooth price curve starting from your start price to your specified end price.
* **Gradually Sell At Higher Prices:** Sell tokens along a smooth price curve starting from your start price to your specified end price.
* **Earn From Market Spreads:** Earn additional trading fees from short term volatility within your selected range.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

{% hint style="info" %}
[**Automated Strategy**](../../../factor-studio/factor-studio/automated-strategies.md)

This is an automated strategy whereby you can configure a time-based one-time/recurring trigger for your strategy.&#x20;
{% endhint %}

<details>

<summary><a href="../../../factor-studio/factor-studio/conditional-strategies.md">IF Conditional</a></summary>

* This condition will be checked each time this strategy is executed by the automation feature.
* Specify your trigger price and condition for when you want to enter the market
  * Token purchases: Only add liquidity if `marketPrice` is ≤ `targetPrice`
  * Token sales: Only add liquidity if `marketPrice` is ≥ `targetPrice`

</details>

<details>

<summary><a href="../../../factor-studio/studio-contracts/lp-management/"><strong>Create LP</strong></a></summary>

* Select the token to add.
  * Token purchases: Token to add is the token to swap from.
  * Token sales: Token to add is the token to sell.
* Select the price range to add liquidity to. The selected price range will have to exclude the current market price. The narrower the range, the more liquidity that gets traded at an in-range price.
* Select the token amount.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>
