# ⚖ Factor Scale

## Overview

{% hint style="success" %}
**Factor Scale Rewards**

Factor will allocate up to 100,000 [FCTR](../fctr-token/#fctr) per epoch (weekly) over an initial period of 6 months for Factor Scale. The [FCTR](../fctr-token/#fctr) tokens for Scale rewards are sourced from the [Ecosystem Incentives  ](../fctr-token/initial-distribution.md#ecosystem-incentives-20.8)portion during [FCTR](../fctr-token/#fctr) initial distribution.
{% endhint %}

Factor Scale enables [veFCTR](../fctr-token/#vefctr) holders to vote on the distribution of weekly gauge rewards to different vaults created on Factor. To incentivize greater user engagement and deeper liquidity, FactorDAO has allocated 100,000 [FCTR](../fctr-token/#fctr) per epoch (weekly) that is distributed to strategy Depositors as gauge rewards. [veFCTR](../fctr-token/#vefctr) holders participate in a weighted voting mechanism that takes place weekly to determine the distribution of gauge rewards.&#x20;

Factor Scale therefore democratizes the allocation of protocol rewards via allowing [veFCTR](../fctr-token/#vefctr) holders to direct protocol emissions through community voting. Rewards distributed by Scale are vested as [esFCTR](../fctr-token/#esfctr), which can be converted to [FCTR](../fctr-token/#fctr) at a 1:1 ratio over a 90-day vesting period.&#x20;

## Scale Weight

In addition to the [veFCTR](../fctr-token/#vefctr) emissions multiplier, Factor Scale utilizes a Scale Weight to further ensure the fair and efficient distribution of Scale rewards. Scale Weight measures teh relative contribution of a vault towards the overall value of the Factor ecosystem. The computed Scale Weight score determines the final Scale reward allocation for each vault. To calculate the Scale Weight, Factor Scale takes into account the following considerations:

* **Vault TVL:** The total value locked in a strategy vault
* **Performance Factor:** A measure of vault's relative performance against other vaults. This includes historical and current performance metrics such as APY, yield generation, and risk-adjusted returns.
* **Community Governance:** The proportion of votes which a vault received via Scale voting.

## Voting Process

To be eligible to vote on Scale rewards distribution, users must first stake [FCTR](../fctr-token/#fctr) to receive [veFCTR](../fctr-token/#vefctr) which represents a single vote (i.e. 1 [veFCTR](../fctr-token/#vefctr): 1 vote). [veFCTR](../fctr-token/#vefctr) holders are then able to vote for multiple strategies by allocating a percentage of their total [veFCTR](../fctr-token/#vefctr) holdings towards various vaults. Note that an emissions multiplier is applied to each [veFCTR](../fctr-token/#vefctr) voter based on their staking duration and relative holdings.

Voting occurs per epoch (weekly) whereby [veFCTR](../fctr-token/#vefctr) holders will have a 72 hour window to vote on their preferred vaults. This encourages greater participation by allowing ample time for votes to be cast. Following the voting window, an on-chain snapshot of the votes is taken every Friday at 12pm UTC. Scale rewards are then proportionally distributed based on a vault's calculated Scale Weight.

Every step, from voting to reward distribution, is transparent and aligns with the community’s sentiment.

## **How to use Factor Scale?**

1. **Stake FCTR for** [**veFCTR**](../fctr-token/#vefctr): Begin by staking your [FCTR](../fctr-token/#fctr) tokens to obtain [veFCTR](../fctr-token/#vefctr), granting you voting rights in the Factor Scale system.
2. **Voting on the Dashboard**: Participate in voting via the dapp dashboard to influence the allocation of Scale rewards.
3. **Track and Adapt**: Monitor the impact of your votes on reward distribution, and the impact of Scale rewards on strategy APYs.
