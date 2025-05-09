# ⚖️ Factor Scale

## Overview

{% hint style="success" %}
**Factor Scale Rewards**

Factor allocates up to 100,000 [FCTR](../fctr-token/#fctr) per epoch (weekly) based on completed TVL milestones. The [FCTR](../fctr-token/#fctr) tokens for Scale rewards are sourced from the [Ecosystem Incentives  ](../fctr-token/initial-distribution.md#ecosystem-incentives-20.8)portion allotted during [FCTR](../fctr-token/#fctr) initial distribution.
{% endhint %}

Factor Scale enables [veFCTR](../fctr-token/#vefctr) holders to vote on the distribution of weekly gauge rewards to different community curated vaults created on Factor. To incentivize greater user engagement and deeper liquidity, the allocated [FCTR](../fctr-token/) tokens are distributed per epoch (i.e weekly) to Strategy Depositors as gauge rewards. [veFCTR](../fctr-token/#vefctr)  holders participate in a weighted voting mechanism that takes place weekly to determine the distribution of gauge rewards.&#x20;

Factor Scale therefore democratizes the allocation of protocol rewards via allowing [veFCTR](../fctr-token/#vefctr) holders to direct protocol emissions through community voting. Rewards distributed by Scale are vested as [esFCTR](../fctr-token/#esfctr), which can be converted to [FCTR](../fctr-token/#fctr) at a 1:1 ratio over a 90-day vesting period.&#x20;

{% hint style="info" %}
**Don't See Your Vault?**

To streamline the voting process and prevent any rewards abuse, Factor Scale displays a community curated list of eligible vaults. Vault eligibility is determined either through a [FactorDAO](../factordao/) vote or via individual strategy reviews by the Factor team.

As Factor Scale matures, more scalable and efficient solutions will be implemented to ensure even more equitable rewards distribution. As we build towards this future, please email [info@factor.fi](mailto:info@factor.fi) if you would like to submit your vault for Factor Scale eligibility review (e.g.\[SCALE WHITELIST]).
{% endhint %}

## FCTR Emission Milestones

To ensure equitable distribution of emissions, Factor Scale implements TVL milestones whereby every subsequent TVL target achieved unlocks more [FCTR](../fctr-token/#fctr) rewards in the next epoch. Weekly emission rewards start at 25,000 [FCTR](../fctr-token/#fctr) with depositors progressively unlocking up to 100,000 [FCTR](../fctr-token/#fctr).

TVL milestones are calculated based on the moving average of the total TVL across all Factor vaults during the specified emissions epoch. This reduces the impact of short term spikes and minimizes rewards misappropriation.&#x20;

## Voting Process

To be eligible to vote on Scale rewards distribution, users must first stake [FCTR](../fctr-token/#fctr) to receive [veFCTR](../fctr-token/#vefctr) which represents a single vote (i.e. 1 [veFCTR](../fctr-token/#vefctr): 1 vote). [veFCTR](../fctr-token/#vefctr) holders are then able to vote for multiple strategies by allocating a percentage of their total [veFCTR](../fctr-token/#vefctr) holdings towards various vaults. In order to qualify for emission rewards, users must also stake their vault position(s).&#x20;

{% hint style="info" %}
**Emissions Multiplier**

An emissions multiplier of up to 2.5x is applied to each [veFCTR](../fctr-token/#vefctr) voter based on their [FCTR](../fctr-token/#fctr) staking duration, relative [veFCTR](../fctr-token/#vefctr) holdings, and strategy deposit amount. The emissions multiplier does not decay and remains the same for the period that the underlying [FCTR](../fctr-token/#fctr) is [staked](../factordao/user-guides/stake-fctr.md).
{% endhint %}

Voting occurs per epoch (weekly) whereby [veFCTR](../fctr-token/#vefctr) holders will have a 7-day window to vote on their preferred vaults. This encourages greater participation by allowing ample time for votes to be cast and aggregated on-chain. Votes are automatically carried over to the next epoch unless modified by the user. Following the voting window, an on-chain snapshot of the votes is taken whereupon Scale rewards are distributed based on voting results.

{% hint style="info" %}
**Votes Finalization Per Epoch (i.e. On-chain Snapshot)**

To ensure transparency, the results of the vote must be broadcasted upon completion of an epoch to enable the calculation of rewards. Factor Scale automates this process via exposing a "Finalize Epoch" which is called via [Gelato automation](https://docs.gelato.network/web3-services/web3-functions).

As a fail safe, the "Finalize Epoch" function can also be manually triggered via the Factor Scale UI after an epoch has been completed. This ensures that the Factor community will still be able to trigger the distribution of Scale rewards in exceptional circumstances.&#x20;
{% endhint %}

Every step, from voting to reward distribution, is transparent and aligns with the community’s sentiment.

{% hint style="success" %}
**Emissions Multiplier Calculations**

Please visit the [Emissions Multiplier Calculations](emission-multiplier-calculations/) page if you would like to find out more about how emissions are distributed in favor of veFCTR holders.
{% endhint %}

## **How to use Factor Scale?**

1. **Stake FCTR for** [**veFCTR**](../fctr-token/#vefctr)**:** Begin by staking your [FCTR](../fctr-token/#fctr) tokens to obtain [veFCTR](../fctr-token/#vefctr), granting you voting rights in the Factor Scale system.
2. **Stake Vault Position:** Stake your vault position (i.e. contributed liquidity) to qualify for emission rewards.
3. **Voting on the Dashboard:** Participate in voting via the [Scale dashboard](https://pro.factor.fi/governance/scale) to influence the allocation of Scale rewards.
4. **Track and Adapt:** Monitor the impact of your votes on reward distribution, and the impact of Scale rewards on strategy APYs.
