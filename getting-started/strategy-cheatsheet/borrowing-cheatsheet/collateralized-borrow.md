# Collateralized Borrow

## Overview

<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

Borrow against your collateralized tokens in a single transaction. You earn supply interest on the token lent while being charged a borrow interest on the token borrowed. Collateralized borrows enable you to source more liquidity for your strategy while maintaining full exposure to your collateral.

The maximum amount that you can borrow is determined by the [collateralization ratio](../../glossary.md#collateralisation-ratio) of the underlying lending pool. Please pay attention to the [health factor](../../glossary.md#health-factor) of your position when borrowing to ensure that you do not lose funds through forced liquidations. Your position can be liquidated if the value of your debt exceeds the collateral value.

## Potential Alpha

* **Access More Capital:** Get access to more liquidity while maintaining full exposure to your asset token plus added supply interest.
* **Benefit From Price Divergence:** Lend a bullish token and borrow stables or lend stables and borrow a bearish token to reduce your debt burden.

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

## Example

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
