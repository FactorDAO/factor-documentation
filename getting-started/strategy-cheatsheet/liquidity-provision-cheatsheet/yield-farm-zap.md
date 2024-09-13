# Yield Farm Zap

## Overview

<figure><img src="../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

[Zap into any liquidity pool](liquidity-pool-zap.md) and immediately stake your liquidity to start earning yield farming rewards. Earn additional rewards or incentives for committing liquidity long term to staking protocols. The [LP Management Building Block](../../../factor-building-blocks/lp-management/) also supports management of concentrated liquidity positions in addition to the standard AMM implementation.

Your tokens are immediately swapped at the best available rates and staked to earn yield farming rewards.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* Select the token to swap from based on the target pool. If the target pool tokens are different from your current token, you will have to add an additional [Swap Building Block ](../../../factor-building-blocks/swap/)to acquire all the pool tokens.
* Input token amount. The ratio of tokens required will be dependent on your target pool as well as the price range which you are providing liquidity to.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lp-management/"><strong>Provide Liquidity</strong></a></summary>

* Select the target pool.
* Add the required ratio of tokens.

</details>

<details>

<summary><a href="../../../governance/fctr-token/staking-and-governance.md"><strong>Stake</strong></a></summary>

* Stake your liquidity position.

</details>