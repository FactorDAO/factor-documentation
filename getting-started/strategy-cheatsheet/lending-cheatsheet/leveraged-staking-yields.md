# Leveraged Staking Yields

## Overview

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Gain leveraged staking yield exposure by borrowing against your staking tokens. By borrowing base tokens against your yield-bearing tokens, you get safe access to leveraged staking yields.

## Potential Alpha

* **Staking Yield Amplification:** Earn multiple of your initial staking token yield amount as long as the average staking yield is greater than the incurred debt.
* **Decreasing Debt Burden:** Lend yield bearing staking tokens and borrow base tokens to open a position where collateral value is always rising relative to debt.
* **Earn Additional Interest:** In addition from your staking token growing in value, you will also receive lending pool supply interest by charging borrowers of your tokens a borrow interest.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/flash-loan/"><strong>Flash Loan</strong></a></summary>

* Flash loan an intermediary token.
* The amount that you can flash loan will be dependent on the maximum collateralization ratio for your selected lending pool (i.e. $$\text{collatRatio}=\frac{value_\text{flashLoan}}{value_\text{initiaclCollateral}+value_\text{flashLoan}}$$ ).&#x20;

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Swap the flash loaned token for staking tokens.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend all available staking tokens to the target lending market.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Borrow the flash loan debt amount denominated in underlying token. This ensures that your asset value is always increasing relative to debt.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Swap the acquired debt tokens for the flash loan token.
* The flash loan debt will be automatically deducted from your strategy.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>
