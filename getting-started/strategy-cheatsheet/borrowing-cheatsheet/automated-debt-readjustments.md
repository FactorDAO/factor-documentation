# Automated Debt Readjustments

## Overview

<figure><img src="../../../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

Prevent your borrow positions from being forced liquidated by automatically repaying a portion of accrued debt whenever your position approaches the [liquidation threshold](../../glossary.md#liquidation-price). By utilizing a flash loan for debt repayment, you do not need to set aside reserved capital and can easily pay down your debt through partial sales of your collateral.

This strategy requires an existing borrow position to be opened whereupon your automated strategy will monitor the position's health.&#x20;

## Potential Alpha

* **Automated Liquidation Protection:** Reduce the likelihood of your position being forced liquidated by selling some asset token to reduce the debt burden.
* **No Upfront Capital Required:** With flash loans, your otherwise idle tokens reserved for repayment can be freed for other yield generating activities, maximizing your capital efficiency.

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

{% hint style="info" %}
[**Automated Strategy**](../../../factor-studio/factor-studio/automated-strategies.md)

This is an automated strategy whereby you can configure a time-based one-time/recurring trigger for your strategy.&#x20;
{% endhint %}

<details>

<summary><a href="../../../factor-studio/factor-studio/conditional-strategies.md">IF Conditional</a></summary>

* This condition will be checked each time this strategy is executed by the automation feature.
* Specify your target price where your position becomes at risk of being undercollateralized (i.e. collateral value < debt value). Remember to leave a buffer in cases of extreme volatility.

</details>

<details>

<summary><a href="../../../factor-building-blocks/flash-loan/"><strong>Flash Loan</strong></a></summary>

* Flash loan the debt token to be partially repaid. The amount to loan will be dependent on the target [health factor](../../glossary.md#health-factor) after adjustments.
* If there is no flash loan market for your debt token, you will need to add a Swap Building Block and flash loan the value of your debt to be swapped.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Repay</strong></a></summary>

* Repay a portion of your debt position.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Withdraw</strong></a></summary>

* Withdraw the value of your flash loan from your collateral.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Swap the withdrawn collateral for the flash loan token.
* The flash loan debt is automatically credited from your strategy.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
