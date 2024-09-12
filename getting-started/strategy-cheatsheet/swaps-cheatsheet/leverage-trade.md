# Leverage Trade

## Overview

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Create leveraged long or short strategies giving you greater exposure to potential upside and enabling downside speculation. This strategy enables users to benefit from the differences between the cost of borrowing and the expected profit generated from the borrowed liquidity.

{% hint style="info" %}
[**Leverage Strategy Explainer**](../../strategy-explainers/leverage/)
{% endhint %}

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/lend.md">Lend</a></summary>

* Lend all tokens to the lending protocol.
  * Longs: The token lent is the token which you are bullish on.
  * Shorts: The token lent is a stable token which will maintain it's value relative to the debt token which you are bearish on.

</details>

<details>

<summary><a href="../../../factor-building-blocks/flash-loan/"><strong>Flash Loan</strong></a></summary>

* Flash loan the debt token.
* The amount that you can flash loan will be dependent on the maximum collateralization ratio for your selected lending pool (i.e. $$\text{collatRatio}=\frac{value_\text{flashLoan}}{value_\text{initiaclCollateral}+value_\text{flashLoan}}$$ )

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Swap the flash loaned debt token for more asset tokens.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Add the newly acquired asset tokens to the same lending pool to increase the amount of collateral.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Borrow the flash loan debt amount.
* The flash loan debt will be automatically deducted from your strategy.

</details>
