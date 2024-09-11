# Collateralized Borrow Zap

## Overview

<figure><img src="../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Use any token to enter a lending market and take out a collateralized loan in a single transaction. Collateralized borrows enable you to source more liquidity for your strategy while maintaining full exposure to your collateral.

Your tokens are immediately swapped at the best available rates and added to the lending pool to earn supply interest. By collateralizing the asset lent, you can also take out a loan which incurs a borrow interest.

The maximum amount that you can borrow is determined by the [collateralization ratio](../../glossary.md#collateralisation-ratio) of the underlying lending pool. Please pay attention to the [health factor](../../glossary.md#health-factor) of your position when borrowing to ensure that you do not lose funds through forced liquidations. Your position can be liquidated if the value of your debt exceeds the collateral value.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Select the token to swap from.
* Input the token amount.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend the output tokens from the swap to the target lending market.
* The tokens which you can borrow will be determined by the underlying lending market.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Select the token to borrow.
* Input a borrow amount which includes a buffer for any price fluctuations.

</details>