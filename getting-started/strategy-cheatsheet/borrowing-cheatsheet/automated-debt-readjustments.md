# Automated Debt Readjustments

## Overview

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Prevent your borrow positions from being forced liquidated by automatically repaying a portion of accrued debt whenever your position approaches the [liquidation threshold](../../glossary.md#liquidation-price).

This strategy requires an existing borrow position to be opened whereupon your automated strategy will monitor the position's health. Note that this automated strategy requires an allocation of repayment funds which will be debited when the repayment condition is met.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend tokens to the target lending market.
* The tokens which you can borrow will be determined by the underlying lending market.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Select the token to borrow.
* Input a borrow amount which includes a buffer for any price fluctuations.

</details>

{% hint style="info" %}
[**Automated Strategy**](../../../factor-studio/factor-studio/automated-strategies.md)

This is an automated strategy whereby you can configure a time-based one-time/recurring trigger for your strategy.&#x20;
{% endhint %}

<details>

<summary><a href="../../../factor-studio/factor-studio/conditional-strategies.md">IF Conditional</a></summary>

* This condition will be checked each time this strategy is executed by the automation feature.
* Specify your target price where your position becomes at risk of being undercollateralized (i.e. collateral value < debt value). Remember to leave a buffer in cases of extreme volatility.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Repay</strong></a></summary>

* Repay a portion of your debt position. This requires the automated strategy to be pre-funded.
* If needed, you can add a [Swap Building Block](../../../factor-building-blocks/swap/) before this block if your debt and allocated tokens differ.

</details>
