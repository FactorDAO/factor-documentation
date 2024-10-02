# Leverage Trade

## Overview

<figure><img src="../../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

Create leveraged long or short strategies giving you greater exposure to potential upside and enabling downside speculation. This strategy enables users to benefit from the differences between the cost of borrowing and the expected profit generated from the borrowed liquidity.

{% hint style="info" %}
[**Leverage Strategy Explainer**](../../strategy-explainers/leverage/)
{% endhint %}

## Potential Alpha

* **Multiply Your Gains:** Get access to more liquidity thereby increasing your capital efficiency through leverage.
* **Offset Borrowing Costs:** Collateralize tokens with higher supply interest and you can even cover your borrow costs plus more.
* **Amplify Native Yields:** Take advantage of tokens with native yield as your collateral value rises relative to your debt value.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/flash-loan/"><strong>Flash Loan</strong></a></summary>

* Create a flash loan for the asset token.
  * Longs: Asset token is the token which you are bullish on.
  * Shorts: Asset token is a stable token with debt being the token you are bearish on.
* The amount that you can flash loan will be dependent on the maximum collateralization ratio for your selected lending pool (i.e. $$\text{collatRatio}=\frac{value_\text{flashLoan}}{value_\text{initiaclCollateral}+value_\text{flashLoan}}$$ ).
* If there is no existing flash loan market for either your asset token, you will have to add an additional [Swap Building Block](../../../factor-building-blocks/swap/) per below.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* This is an optional block in the case where there is no flash loan market for your asset token.
* Swap the flash loaned token for your target asset token.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Add the newly acquired asset tokens to the target lending pool as collateral.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Borrow the flash loan debt amount.
* If the debt and flash loan token differs, you will need to add an additional swap step per below.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Swap the debt token for the flash loan token.
* The flash loan debt will be automatically deducted from your strategy.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>
