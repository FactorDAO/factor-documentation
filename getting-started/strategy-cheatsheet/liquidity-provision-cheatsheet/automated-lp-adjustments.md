# Automated LP Adjustments

## Overview

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Automatically adjust your AMM LP position according to market conditions to continue earning trading fees or dynamically adjust spreads. The [LP Management Building Block](../../../factor-building-blocks/lp-management/) also supports management of concentrated liquidity positions in addition to the standard AMM implementation.

This strategy requires an existing LP position to be opened. If your market conditions are met, all of the liquidity from your existing LP position is withdrawn and a new position is opened with varying parameters and token ratios. LP position parameters can be defined based on your market making goals, whether it's to adjust token ratios, liquidity price ranges, or even liquidity pool fee tiers.

For any adjustments of token ratios to meet LP deposit requirements, your tokens are swapped at the best available rates and immediately added to the new LP position to generate fees.

## Potential Alpha

* **Non Stop Yields:** Automate position adjustments to ensure that your position is always in range and earning trading fees and any liquidity incentives.
* **Minimize Risks & Overheads:** Reduce the amount of time required to create a position while simultaneously eliminating any market volatility risks during the position adjustment process.

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
* Specify your target market condition for when to adjust your LP position.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lp-management/"><strong>Withdraw Liquidity</strong></a></summary>

* Remove all liquidity from the existing LP position.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Depending on the parameters of your new position, swap between pool tokens to get the ratio of tokens required.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lp-management/"><strong>Create LP</strong></a></summary>

* Create a concentrated liquidity position for the token pair.
* Select the target pool.
* Adjust the price range to provide liquidity to.
* Add the required ratio of tokens.

</details>
