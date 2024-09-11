# Conditional Market Order

## Overview

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Swap your tokens at the market price only if your target price is reached during transaction execution.&#x20;

Your tokens are immediately swapped at the best available prices as the selected protocol dynamically reroutes your trade to more capital efficient sources.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-studio/factor-studio/conditional-strategies.md">IF Conditional</a></summary>

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
