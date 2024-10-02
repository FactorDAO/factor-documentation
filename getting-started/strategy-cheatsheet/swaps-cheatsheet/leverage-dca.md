# Leverage DCA

## Overview

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

Amplify your gains with leveraged trading with gradual buy/sells. This strategy enables users to automatically benefit from the differences between the cost of borrowing and the expected profit generated from the borrowed liquidity.

## Potential Alpha

* **Multiply Your Gains:** Get access to more liquidity thereby increasing your capital efficiency through leverage.
* **Gradually Buy At Lower Prices:** Purchase tokens along a smooth price curve starting from your start price to your specified end price. Every trade covers a larger proportion of your debt.
* **Gradually Sell At Higher Prices:** Sell tokens along a smooth price curve starting from your start price to your specified end price. Every trade covers a larger proportion of your debt.
* **Earn From Market Spreads:** Earn additional trading fees from short term volatility within your selected range.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Longs (upside speculation)
  * Lend the token you are bullish on to the specified lending pool.
* Shorts (downside speculation)
  * Lend stable tokens to the specified lending pool.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Longs (upside speculation)
  * Borrow stables against your collateral.
* Shorts (downside speculation)
  * Borrow the tokens you are bearish on.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Longs (upside speculation)
  * Swap the acquired stables for more bullish tokens.
* Shorts (downside speculation)
  * Swap the acquired debt tokens for more stables.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lp-management/"><strong>Create LP</strong></a></summary>

* Create a single-sided concentrated liquidity position for the token pair.
  * Longs: Add all the bullish token to a range above the current market price.
  * Shorts: Add all the stables to a range below the current market price.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>
