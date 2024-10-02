# Automated Swap & Earn

## Overview

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Trigger a swap when your target price is reached and immediately lend for supply interest.

Your tokens are swapped at the best available prices and the tokens received are added to your selected lending pool in a single transaction.

## Potential Alpha

* **Buy Low, Sell High:** Automatically trade at your desired price and earn from any token appreciation.
* **Earn Lending Interest:** Put your tokens to work and earn a supply interest by depositing it into  various lending markets.

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
* Specify your target price and condition for the swap.
  * Token purchases: Only execute the swap if `marketPrice` is ≤ `targetPrice`
  * Token sales: Only execute the swap if `marketPrice` is ≥ `targetPrice`

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Select the tokens to swap
  * Token purchases: Input token is the token to swap from and output token is the target token.
  * Token sales: Input token is the token to sell and output token is the token to receive.
* Input token amount

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md">Lend</a></summary>

* Lend all of the swapped tokens to the selected lending pool to earn maximum supply interest.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
