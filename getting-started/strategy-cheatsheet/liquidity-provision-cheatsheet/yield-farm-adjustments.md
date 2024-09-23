# Yield Farm Adjustments

## Overview

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Maximize your yield farming rewards by adjusting your staked position in a single transaction. With this strategy, your LP position continues to earn staking rewards without missing a single block.&#x20;

This strategy requires an existing staked LP position. You can easily exit your current staked LP position and create a new staked LP position with varying parameters and token ratios. LP position parameters can be defined based on your market making goals, whether it's to adjust token ratios, liquidity price ranges, or even liquidity pool fee tiers.

For any adjustments of token ratios to meet LP deposit requirements, your tokens are immediately swapped at the best available rates and staked to earn yield farming rewards.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/stake.md"><strong>Unstake</strong></a></summary>

* Unstake your existing LP position.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lp-management/"><strong>Withdraw Liquidity</strong></a></summary>

* Remove all liquidity from the existing LP position.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Depending on the parameters of your new position, swap between pool tokens to get the ratio of tokens required.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lp-management/"><strong>Provide Liquidity</strong></a></summary>

* Select the target pool.
* Adjust the price range to provide liquidity to.
* Add the required ratio of tokens.

</details>

<details>

<summary><a href="../../../governance/fctr-token/staking-and-governance.md"><strong>Stake</strong></a></summary>

* Stake your new LP position.

</details>
