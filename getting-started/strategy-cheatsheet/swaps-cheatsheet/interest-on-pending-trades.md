# Interest On Pending Trades

## Overview

<figure><img src="../../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Earn supply interest on your allocated trade funds while waiting for your target price to be reached.

This strategy requires that you first have a lending position in the token that you're trading from. By lending tokens allocated to the trade, your otherwise idle tokens will be earning supply interest until the market reaches your trigger price.

Upon your target price being reached, your tokens are immediately withdrawn and the initial loan amount is immediately swapped at optimal market rates. By specifying a swap amount that is equal to the initial lending amount, any interest earned will then accrue to the strategy for the duration of the wait period.

## Potential Alpha

* **Earn Short Term Lending Interest:** Earn additional yields on otherwise idle reserved tokens while waiting for your target price to be hit.
* **Buy Low, Sell High:** Automatically trade at your desired price and earn from any token appreciation.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/lend.md">Lend</a></summary>

* Lend all tokens to trade from to the lending protocol.

</details>

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

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Withdraw</strong></a></summary>

* Withdraw all tokens in the lending pool (interest would have accrued automatically).

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Select the tokens to swap
  * Token purchases: Input token is the token to swap from and output token is the target token.
  * Token sales: Input token is the token to sell and output token is the token to receive.
* Choose an input token amount that is equal to the initial lending amount. Remaining interest remains in the strategy.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>
