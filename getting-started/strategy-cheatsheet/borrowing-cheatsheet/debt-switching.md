# Debt Switching

## Overview

<figure><img src="../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

Switch your debt token for an existing loan in a single transaction. This strategy provides you with the opportunity to benefit from lower borrow interest or relative devaluation of the newly borrowed token.

By utilizing a [flash loan](../../../factor-building-blocks/flash-loan/concepts/flash-loan.md),  you can easily switch your debt without having to source the required capital to repay your initial loan. Depending on the flash loan token available, you might need to add additional swap blocks to account in differences between tokens that are flash loaned, repaid, and borrowed. Your tokens are immediately swapped at the best available rates ensuring minimal slippage when switching your debt.

The maximum amount that you can borrow is determined by the [collateralization ratio](../../glossary.md#collateralisation-ratio) of the underlying lending pool. Please pay attention to the [health factor](../../glossary.md#health-factor) of your position when borrowing to ensure that you do not lose funds through forced liquidations. Your position can be liquidated if the value of your debt exceeds the collateral value.

## Potential Alpha

* **Borrow At Lower Rates:** Pay less borrow interest on your existing loans by consistently switching between various debt tokens.
* **Benefit From Price Divergence:** Switch your debt to a more bearish token and reduce your debt burden as debt token price drops.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/flash-loan/"><strong>Flash Loan</strong></a></summary>

* Flash loan the debt token to be repaid in full.
* If there is no flash loan market for your debt token, you will need to add a Swap Building Block and flash loan the value of your debt to be swapped.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Repay</strong></a></summary>

* Repay the full amount of debt owed.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Select the new debt token.
* Input a borrow amount which includes a buffer for any price fluctuations.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* If the new debt token is different from the flash loan token, initiate a swap to exchange all of the newly borrowed tokens for flash loan tokens.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
