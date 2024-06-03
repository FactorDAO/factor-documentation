# Emission Multiplier Calculations

## Overview

The [Factor Scale](./) emissions multiplier ensures that users that contribute the most network security (i.e. economic security through staked [FCTR](../fctr-token/#fctr)) also receive the most rewards for staking their liquidity into various strategies. By assigning a weight to the user's staked liquidity, the emission multiplier rewards users holding more [veFCTR](../fctr-token/#vefctr) with a greater share of the strategy's allocated rewards.

### TLDR

* The higher the proportion of veFCTR supply held, the larger the share of strategy emission rewards.
* The maximum emissions multiplier is achieved when the proportion of veFCTR supply held by the user approaches the proportion of strategy staked liquidity (i.e.  $$veFCTR\%$$ approaches $$StakedLiq\%$$).
* When $$veFCTR\%$$ is greater than $$StakedLiq\%$$, the rate of multiplier decay is slower than if $$veFCTR\%$$ is lower than $$StakedLiq\%$$.

<details>

<summary>Emission Multiplier Flow</summary>

1. User stakes [FCTR](../fctr-token/#fctr) to receive an amount of [veFCTR](../fctr-token/#vefctr) depending on staked duration (up to 1FCTR:1veFCTR for max stake duration).
2. User provides liquidity to the target strategy which is eligible for [Factor Scale](./) emissions.
3. User stakes the liquidity position in order to be eligible for rewards.
4. With the [veFCTR](../fctr-token/#vefctr) obtained in 1, user votes for their target strategy on [Factor Scale](./).
5. When the voting period for the epoch ends, the total emissions allocated for the epoch is distributed in proportion to the number of votes that the strategy receives. (i.e. if strategy receives 10% of total votes for that epoch, it receives 10% of emissions).
6. For each strategy, the allocated emissions amount is then distributed over the course of the epoch according to the gauge weighted liquidity provided by LPs  who have staked their liquidity in the strategy.

</details>

## Weighted Liquidity Formulas

At it's core, the emissions multiplier ensures fairer distribution of emission rewards by constantly comparing:

* Proportion of staked liquidity the user contributes to a specific strategy:

$$
stakedLiq\% = \frac{stakedLiq_{user}}{stakedLiq_{pool}}
$$

{% hint style="info" %}
**Staked Liquidity Amount & Leverage**

As Factor enables users to increase their capital exposure via [Leverage](../../getting-started/strategy-explainers/leverage.md) strategies, the $$stakedLiquidity$$ amount also takes into account the leveraged portion by utilizing the debt portion of the user's position. That is, $$stakedLiquidity$$ for leveraged positions tracks the debt value.
{% endhint %}

* Proportion of [veFCTR](../fctr-token/#vefctr) supply held by the user:

$$
veFCTR\% = \frac{veFCTR_{user}}{veFCTR_{supply}}
$$

In general, the larger the proportion of [veFCTR](../fctr-token/#vefctr) supply held, the larger the emissions multiplier.

### Weighted Liquidity

By applying a [veFCTR](../fctr-token/#vefctr) holding weight to the staked liquidity provided by the user, it enables [veFCTR](../fctr-token/#vefctr) holders to access up to 2.5x the emissions for their staked liquidity. The weighted liquidity for a user is calculated based on the following formula:

$$
min \biggl( (0.4 \times stakedLiq_{user}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{user}}{veFCTR_{supply}}) , stakedLiq_{user} \biggl)
$$

The above formula is used to calculate the $$weightedLiq$$ for every depositor in the strategy, including those who do not have [veFCTR](../fctr-token/#vefctr) staked. The [esFCTR](../fctr-token/#esfctr) emissions allocated to the pool for that epoch is then linearly streamed throughout the epoch based on the proportion of the strategy's $$weightedLiquidity$$ that the user holds at that point in time.

Based on the above formula, there are a few critical points to take note of:

* The maximum emissions multiplier of 2.5x occurs when the $$StakedLiq\%$$approaches the $$veFCTR\%$$
* When $$veFCTR\%$$ is greater than $$StakedLiq\%$$, the rate of multiplier decay is significantly slower than if $$veFCTR\%$$ is lower than $$StakedLiq\%$$

Put simply, the weighted liquidity formulas prioritizes distributing emissions towards users with larger $$veFCTR\%$$ (i.e. users who have staked more FCTR for longer periods). **For the same absolute  % difference, your emissions multiplier will be much higher if your** $$veFCTR\%$$ **is greater than** $$StakedLiq\%$$**.** To achieve the max multiplier, your $$veFCTR\%$$ should be closer to $$StakedLiq\%$$.

## Example

{% tabs %}
{% tab title="Baseline" %}
**Users**

* Alice provides 100 staked liquidity but does not hold any veFCTR
* Bloxy provides 100 staked liquidity and holds 50veFCTR

**Conditions**

* Assume no other users in the strategy hence $$stakedLiq_{pool} = stakedLiq_{Alice} + stakedLiq_{Bloxy} = 200$$
* Total veFCTR supply (including Bloxy): 500veFCTR
* Emission rewards allocated to strategy: 1,000 esFCTR

**Alice's Weighted Supply**

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times stakedLiq_{Alice}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Alice}}{veFCTR_{supply}}) , stakedLiq_{Alice} \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times 100) + (0.6 \times 200 \times \frac{0}{500}) , 100 \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( 40 , 100 \biggl) = 40
$$

**Bloxy's Weighted Supply**

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times stakedLiq_{Bloxy}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Bloxy}}{veFCTR_{supply}}) , stakedLiq_{Bloxy} \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times 100) + (0.6 \times 200 \times \frac{50}{500}) , 100 \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( 40 + 12 , 100 \biggl) = min \biggl( 52 , 100 \biggl) = 52
$$

**Emissions Distribution**

$$
esFCTR_{Alice} = esFCTR_{pool} \times \frac{weightedSupply_{Alice}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Alice} = 1,000 \times \frac{40}{40+52} = 1,000 \times 0.435 = 435 esFCTR
$$

$$
esFCTR_{Bloxy} = esFCTR_{pool} \times \frac{weightedSupply_{Bloxy}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Bloxy} = 1,000 \times \frac{52}{40+52} = 1,000 \times 0.565 = 565 esFCTR
$$
{% endtab %}

{% tab title="Max Multiplier" %}
{% hint style="info" %}
This example builds upon the [Baseline](emission-multiplier-calculations.md#baseline) example. Changes to calculations are highlighted in **bold**.
{% endhint %}

**Users**

* Alice provides 100 staked liquidity but does not hold any veFCTR
* Bloxy provides 10 staked liquidity and holds 50veFCTR (50% -> 10% of stakedLiquidity)

**Conditions**

* Assume no other users in the strategy hence $$stakedLiq_{pool} = stakedLiq_{Alice} + stakedLiq_{Bloxy} = \textbf{110}$$
* Total veFCTR supply (including Bloxy): 500veFCTR
* Emission rewards allocated to strategy: 1,000 esFCTR

**Alice's Weighted Supply**

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times stakedLiq_{Alice}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Alice}}{veFCTR_{supply}}) , stakedLiq_{Alice} \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times 100) + (0.6 \times \textbf{110} \times \frac{0}{500}) , 100 \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( 40 , 100 \biggl) = 40
$$

**Bloxy's Weighted Supply**

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times stakedLiq_{Bloxy}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Bloxy}}{veFCTR_{supply}}) , stakedLiq_{Bloxy} \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times \textbf{10}) + (0.6 \times \textbf{110} \times \frac{50}{500}) , 10 \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( 4 + \textbf{6.6} , \textbf{10} \biggl) = min \biggl(\textbf{10.6} , \textbf{10} \biggl) = \textbf{10}
$$

**Emissions Distribution**

$$
esFCTR_{Alice} = esFCTR_{pool} \times \frac{weightedSupply_{Alice}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Alice} = 1,000 \times \frac{40}{40+\textbf{10}} = 1,000 \times \textbf{0.8} = \textbf{800} esFCTR
$$

$$
esFCTR_{Bloxy} = esFCTR_{pool} \times \frac{weightedSupply_{Bloxy}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Alice} = 1,000 \times \frac{\textbf{10}}{40+\textbf{10}} = 1,000 \times \textbf{0.2} = \textbf{200} esFCTR
$$

**Observations**

* **Change:** Bloxy reduces staked liquidity proportion to match veFCTR supply proportion.
* **Result:** Based on the new staked liquidity, Bloxy receives \~2.2x the esFCTR. Note that the capital efficiency as Bloxy's staked liquidity is reduced. Bloxy could have also chosen to acquire more veFCTR to get a higher multiplier. The maximum multiplier is also dependent on the strategy's liquidity as well as ttotal veFCTR supply.
{% endtab %}

{% tab title="Larger veFCTR %" %}
{% hint style="info" %}
This example builds upon the [Baseline](emission-multiplier-calculations.md#baseline) example. Changes to calculations are highlighted in **bold**.
{% endhint %}

**Users**

* Alice provides 100 staked liquidity but does not hold any veFCTR
* Bloxy provides 100 staked liquidity and holds **150veFCTR** (100 more than baseline -> 25% vs 10% of veFCTR supply)

**Conditions**

* Assume no other users in the strategy hence $$stakedLiq_{pool} = stakedLiq_{Alice} + stakedLiq_{Bloxy} = 200$$
* Total veFCTR supply (including Bloxy): **600veFCTR**
* Emission rewards allocated to strategy: 1,000 esFCTR

**Alice's Weighted Supply**

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times stakedLiq_{Alice}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Alice}}{veFCTR_{supply}}) , stakedLiq_{Alice} \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times 100) + (0.6 \times 200 \times \frac{0}{\textbf{600}}) , 100 \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( 40 , 100 \biggl) = 40
$$

**Bloxy's Weighted Supply**

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times stakedLiq_{Bloxy}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Bloxy}}{veFCTR_{supply}}) , stakedLiq_{Bloxy} \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times 100) + (0.6 \times \textbf{200} \times \frac{\textbf{150}}{\textbf{600}}) , 100 \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( 40 + \textbf{30} , 100 \biggl) = min \biggl( \textbf{70} , 100 \biggl) = \textbf{70}
$$

**Emissions Distribution**

$$
esFCTR_{Alice} = esFCTR_{pool} \times \frac{weightedSupply_{Alice}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Alice} = 1,000 \times \frac{40}{40+\textbf{70}} = 1,000 \times \textbf{0.364} = \textbf{364} esFCTR
$$

$$
esFCTR_{Bloxy} = esFCTR_{pool} \times \frac{weightedSupply_{Bloxy}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Bloxy} = 1,000 \times \frac{\textbf{70}}{40+\textbf{70}} = 1,000 \times \textbf{0.636}= \textbf{636} esFCTR
$$

**Observations**

* **Change:** Bloxy holds an additional 15% of veFCTR supply.
* **Result:** Bloxy gets an additional 136esFCTR which is a 1.27x multiplier.
{% endtab %}

{% tab title="Larger StakedLiquidity %" %}
{% hint style="info" %}
This example builds upon the [Baseline](emission-multiplier-calculations.md#baseline) example. Changes to calculations are highlighted in **bold**.
{% endhint %}

**Users**

* Alice provides 100 staked liquidity but does not hold any veFCTR
* Bloxy provides 200 staked liquidity and holds 50veFCTR

**Conditions**

* Assume no other users in the strategy hence $$stakedLiq_{pool} = stakedLiq_{Alice} + stakedLiq_{Bloxy} = \textbf{300}$$
* Total veFCTR supply (including Bloxy): 500veFCTR
* Emission rewards allocated to strategy: 1,000 esFCTR

**Alice's Weighted Supply**

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times stakedLiq_{Alice}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Alice}}{veFCTR_{supply}}) , stakedLiq_{Alice} \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times 100) + (0.6 \times \textbf{300} \times \frac{0}{500}) , 100 \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( 40 , 100 \biggl) = 40
$$

**Bloxy's Weighted Supply**

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times stakedLiq_{Bloxy}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Bloxy}}{veFCTR_{supply}}) , stakedLiq_{Bloxy} \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times \textbf{200}) + (0.6 \times \textbf{300} \times \frac{50}{500}) , \textbf{200} \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( \textbf{80} + \textbf{18} , \textbf{200} \biggl) = min \biggl( \textbf{98} , \textbf{200} \biggl) = \textbf{98}
$$

**Emissions Distribution**

$$
esFCTR_{Alice} = esFCTR_{pool} \times \frac{weightedSupply_{Alice}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Alice} = 1,000 \times \frac{40}{40+\textbf{98}} = 1,000 \times \textbf{0.290} = \textbf{290} esFCTR
$$

$$
esFCTR_{Bloxy} = esFCTR_{pool} \times \frac{weightedSupply_{Bloxy}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Bloxy} = 1,000 \times \frac{\textbf{98}}{40+\textbf{98}} = 1,000 \times \textbf{0.710} = \textbf{710} esFCTR
$$

**Observations**

* **Change:** Bloxy stakes an additional 100 liquidity and now owns 66% of strategy staked liquidity.
* **Result:** Bloxy gets an additional 210esFCTR which is a 1.42x multiplier.
{% endtab %}

{% tab title="Increased veFCTR Supply" %}
{% hint style="info" %}
This example builds upon the [Baseline](emission-multiplier-calculations.md#baseline) example. Changes to calculations are highlighted in **bold**.
{% endhint %}

**Users**

* Alice provides 100 staked liquidity but does not hold any veFCTR
* Bloxy provides 100 staked liquidity and holds 50veFCTR
* Charles stakes FCTR to increase the veFCTR supply by 250veFCTR but does not provide liquidity nor vote on Scale (i.e. pure increase in veFCTR supply)

**Conditions**

* Assume no other users in the strategy hence $$stakedLiq_{pool} = stakedLiq_{Alice} + stakedLiq_{Bloxy} = 200$$
* Total veFCTR supply: **750**veFCTR
* Emission rewards allocated to strategy: 1,000 esFCTR

**Alice's Weighted Supply**

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times stakedLiq_{Alice}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Alice}}{veFCTR_{supply}}) , stakedLiq_{Alice} \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times 100) + (0.6 \times 200 \times \frac{0}{\textbf{750}}) , 100 \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( 40 , 100 \biggl) = 40
$$

**Bloxy's Weighted Supply**

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times stakedLiq_{Bloxy}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Bloxy}}{veFCTR_{supply}}) , stakedLiq_{Bloxy} \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times 100) + (0.6 \times 200 \times \frac{50}{\textbf{750}}) , 100 \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( 40 + \textbf{8} , 100 \biggl) = min \biggl( \textbf{48} , 100 \biggl) = \textbf{48}
$$

**Emissions Distribution**

$$
esFCTR_{Alice} = esFCTR_{pool} \times \frac{weightedSupply_{Alice}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Alice} = 1,000 \times \frac{40}{40+\textbf{48}} = 1,000 \times \textbf{0.455} = \textbf{455} esFCTR
$$

$$
esFCTR_{Bloxy} = esFCTR_{pool} \times \frac{weightedSupply_{Bloxy}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Bloxy} = 1,000 \times \frac{\textbf{48}}{40+\textbf{48}} = 1,000 \times \textbf{0.545} = \textbf{545} esFCTR
$$

**Observations**

* **Change:** veFCTR supply increases by 50% resulting in Bloxy only holding 6.67% of veFCTR supply (down from 10%).
* **Result**: Bloxy gets an additional 45esFCTR which is a 1.09x multiplier.
{% endtab %}

{% tab title="Increased Staked Liquidity" %}
{% hint style="info" %}
This example builds upon the [Baseline](emission-multiplier-calculations.md#baseline) example. Changes to calculations are highlighted in **bold**.
{% endhint %}

**Users**

* Alice provides 100 staked liquidity but does not hold any veFCTR
* Bloxy provides 100 staked liquidity and holds 50veFCTR
* Charles provides 100 staked liquidity but does not hold any veFCTR

**Conditions**

* Assume no other users in the strategy hence $$stakedLiq_{pool} = stakedLiq_{Alice} + stakedLiq_{Bloxy} + stakedLiq_{Charles}= \textbf{300}$$
* Total veFCTR supply (including Bloxy): 500veFCTR
* Emission rewards allocated to strategy: 1,000 esFCTR

**Alice's Weighted Supply**

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times stakedLiq_{Alice}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Alice}}{veFCTR_{supply}}) , stakedLiq_{Alice} \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( (0.4 \times 100) + (0.6 \times \textbf{300} \times \frac{0}{500}) , 100 \biggl)
$$

$$
weightedSupply_{Alice} = min \biggl( 40 , 100 \biggl) = 40
$$

**Bloxy's Weighted Supply**

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times stakedLiq_{Bloxy}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Bloxy}}{veFCTR_{supply}}) , stakedLiq_{Bloxy} \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( (0.4 \times 100) + (0.6 \times \textbf{300} \times \frac{50}{500}) , 100 \biggl)
$$

$$
weightedSupply_{Bloxy} = min \biggl( 40 + \textbf{18} , 100 \biggl) = min \biggl( \textbf{58} , 100 \biggl) = \textbf{58}
$$

**Charle's Weighted Supply**

$$
weightedSupply_{Charles} = min \biggl( (0.4 \times stakedLiq_{Charles}) + (0.6 \times stakedLiq_{pool} \times \frac{veFCTR_{Charles}}{veFCTR_{supply}}) , stakedLiq_{Charles} \biggl)
$$

$$
weightedSupply_{Charles} = min \biggl( (0.4 \times 100) + (0.6 \times \textbf{300} \times \frac{0}{500}) , 100 \biggl)
$$

$$
weightedSupply_{Charles} = min \biggl( 40 , 100 \biggl) = 40
$$

**Emissions Distribution**

$$
esFCTR_{Alice} = esFCTR_{pool} \times \frac{weightedSupply_{Alice}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Alice} = 1,000 \times \frac{40}{40+\textbf{58}+\textbf{40}} = 1,000 \times \textbf{0.290} = \textbf{290} esFCTR
$$

$$
esFCTR_{Bloxy} = esFCTR_{pool} \times \frac{weightedSupply_{Bloxy}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Bloxy} = 1,000 \times \frac{\textbf{58}}{40+\textbf{58}+\textbf{40}} = 1,000 \times \textbf{0.420} = \textbf{420} esFCTR
$$

$$
esFCTR_{Charles} = esFCTR_{pool} \times \frac{weightedSupply_{Bloxy}}{weightedSupply_{Pool}}
$$

$$
esFCTR_{Charles} = 1,000 \times \frac{40}{40+\textbf{58}+\textbf{40}} = 1,000 \times \textbf{0.290} = \textbf{290} esFCTR
$$

**Observations**

* **Change:** The strategy's staked liquidity increase by 50% resulting in Bloxy owning 66% of the staked liquidity (compared to 50%).
* **Result:** Bloxy rewards drops by 80esFCTR due to liquidity dilution.
{% endtab %}
{% endtabs %}
