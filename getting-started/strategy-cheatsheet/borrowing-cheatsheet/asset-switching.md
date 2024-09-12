# Asset Switching

## Overview

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Switch the lending provider or collateral token underlying your borrow position in a single transaction. This strategy provides you with the opportunity to benefit from higher supply interest across lending markets or the relative price increase of the new collateral token. This strategy assumes you have an existing borrow position.

By utilizing a [flash loan](../../../factor-building-blocks/flash-loan/concepts/flash-loan.md), you can easily asset switch without having to source the required capital to repay your initial loan. Depending on the flash loan token available, you might need to add additional swap blocks to account in differences between tokens that are flash loaned, repaid, and borrowed. Your tokens are immediately swapped at the best available rates ensuring minimal slippage when asset switching.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/flash-loan/"><strong>Flash Loan</strong></a></summary>

* Flash loan the debt token to be repaid in full.
* If there is no flash loan market for your debt token, you will need to add a [Swap Building Block](../../../factor-building-blocks/swap/) and flash loan the value of your debt to be swapped.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Repay</strong></a></summary>

* Repay the full amount of debt owed.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Withdraw</strong></a></summary>

* Withdraw all of your collateral token from the lending pool.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/"><strong>Swap</strong></a></summary>

* Exchange all of your withdrawn collateral token for the new target collateral token.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend all of the newly swapped collateral tokens to the target lending market.
* The tokens which you can borrow will be determined by the underlying lending market.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Select the new debt token.
* Input a borrow amount which deducts the accrued interest from previous position and includes an additional buffer for any price fluctuations.
* If your flash loan token differs from the new debt token, add an additional [Swap Building Block](../../../factor-building-blocks/swap/) to exchange borrowed tokens for flash loan tokens.

</details>
