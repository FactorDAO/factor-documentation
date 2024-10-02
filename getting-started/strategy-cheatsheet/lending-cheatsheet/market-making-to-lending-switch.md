# Market Making To Lending Switch

## Overview

<figure><img src="../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Migrate from market making to lending markets in a single transaction and start earning leding interest immediately without IL risks.

If you want to maintain exposure to both tokens but believe there is a high chance that impermanent loss might become permanent for your target time period, you can migrate to lending instead and earn yields while eliminating IL risks completely.

Alternatively, if market spreads are negligible for your target time period, you might stand to earn more yields by lending your tokens instead of continuing to market make.

## Potential Alpha

* **Lending Market Outperformance:** Earn more yields if the average supply interest across both tokens is consistently above the trading fees from depositing into an AMM.
* **HODL With Yield:** Eliminate impermanent loss risks while still earning supply interest on your holdings. HODL with yield.
* **Maximize Supply Interest:** Not a single second is wasted as your tokens are immediately added to the target lending pools to earn interest.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-studio/studio-contracts/lp-management/"><strong>Remove Liquidity</strong></a></summary>

* Remove all liquidity from existing position.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend one of the tokens (`tokenA`/`token0`) to a selected lending pool.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend the other token (`tokenB`/`token1`) to a selected lending pool.

</details>
