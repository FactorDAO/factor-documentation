# Earn Negative Interest

## Overview

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Take out a collateralized loan whenever there is negative interest and get paid to borrow.

This strategy requires that you first have a lending position which can function as the collateral for your borrow. By lending tokens, you also earn any supply interest,

By automating checks for negative borrow interest conditions, your strategy can automatically trigger a borrow whenever borrow rates for your lending market is negative. You can borrow up to the maximum [collateralization ratio](../../glossary.md#collateralisation-ratio) but pay attention to the [health factor](../../glossary.md#health-factor) of your position to avoid forced liquidations.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/lend.md">Lend</a></summary>

* Lend all tokens to the lending protocol.

</details>

{% hint style="info" %}
[**Automated Strategy**](../../../factor-studio/factor-studio/automated-strategies.md)

This is an automated strategy whereby you can configure a time-based one-time/recurring trigger for your strategy.&#x20;
{% endhint %}

<details>

<summary><a href="../../../factor-studio/factor-studio/conditional-strategies.md">IF Conditional</a></summary>

* This condition will be checked each time this strategy is executed by the automation feature.
* Specify the negative borrow interest condition.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Borrow an amount up to the collateralization ratio.

</details>
