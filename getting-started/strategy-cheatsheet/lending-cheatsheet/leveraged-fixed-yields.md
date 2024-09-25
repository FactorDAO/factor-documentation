# Leveraged Fixed Yields

## Overview

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Earn amplified fixed yields by lending yield tokens on leverage and pocket the difference between the fixed yields and borrow cost. This strategy takes advantage of the yield markets for yield-bearing tokens whereby users can acquire principal tokens at a discount and hold it until maturity to realize fixed-yields.

Refer to [PT Strategies](../../strategy-explainers/pt-strategies/) for a detailed strategy explainer.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/flash-loan/"><strong>Flash Loan</strong></a></summary>

* Flash loan the debt token.
* The amount that you can flash loan will be dependent on the maximum collateralization ratio for your selected lending pool (i.e. $$\text{collatRatio}=\frac{value_\text{flashLoan}}{value_\text{initiaclCollateral}+value_\text{flashLoan}}$$ ).&#x20;

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Swap the flash loaned token for more of the initial token.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Swap all of the acquired tokens for Principal Tokens.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lp-management/"><strong>Provide Liquidity</strong></a></summary>

* Add Principal Tokens to the `Token:Principal Token` pool&#x20;

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend/"><strong>Lend</strong></a></summary>

* Lend additional LP tokens to the selected lending pool.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Borrow the flash loan debt amount.
* The flash loan debt will be automatically deducted from your strategy.

</details>
