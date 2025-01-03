# Debt Refinancing

## Overview

<figure><img src="../../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

Switch your lending provider to take advantage of favourable borrow rates in a single transaction. This strategy assumes you have an existing borrow position.

By utilizing a [flash loan](../../../factor-building-blocks/flash-loan/concepts/flash-loan.md), you can easily refinance your borrow position without having to source the required capital to repay your initial loan. Depending on the flash loan token available, you might need to add additional swap blocks to account in differences between tokens that are flash loaned, repaid, and borrowed. Your tokens are immediately swapped at the best available rates ensuring minimal slippage when switching lending providers.

## Potential Alpha

* **Borrow At Lower Rates:** Pay less borrow interest on your existing loans by consistently switching loan providers and lending markets.
* **No Upfront Capital Required:** With flash loans, your otherwise idle tokens reserved for repayment can be freed for other yield generating activities, maximizing your capital efficiency.
* **Save Time, Minimize Risks:** By completing the whole process in a single transaction, you not only save yourself time but also reduce your exposure to market volatility risks.

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

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend all of the withdrawn tokens to the target lending market.
* The tokens which you can borrow will be determined by the underlying lending market.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Select the new debt token.
* Input a borrow amount which deducts the accrued interest from previous position and includes an additional buffer for any price fluctuations.
* If your flash loan token differs from the new debt token, add an additional [Swap Building Block](../../../factor-building-blocks/swap/) to exchange borrowed tokens for flash loan tokens.

</details>

## Example

<figure><img src="../../../.gitbook/assets/DebtRefinancing.png" alt=""><figcaption></figcaption></figure>
