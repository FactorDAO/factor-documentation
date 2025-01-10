# Levered USD & ETH Carry

## Overview

By taking advantage of stablecoin inherent neutrality (i.e. all stablecoins are designed to maintain a peg), you can earn interest differentials between `USD` lending markets and `ETH` borrow markets.

`ETH` borrows can be hedged by holding `ETH` which is then swapped for `rETH` to earn additional `ETH` yields. This `rETH` portion can be sold at anytime to cover any potential `ETH` debt.

## Strategy

The strategy consists of 2 positions:

* **Leveraged short `USD`/`ETH`:** By looping `ETH` borrows against `USD` supply, you can earn the difference between `USD` supply interest and `ETH` borrow interest.
* **Leveraged long rETH/ETH:** By looping `ETH` borrows against `rETH` suply, you can earn the difference between `rETH`liquid staking yields and `ETH`borrows.

By combining the two positions above, there is minimal exchange risks as the `ETH`debt is always covered by the `rETH`portion.&#x20;

### Protocol Parameters

{% tabs %}
{% tab title="Aave" %}
* Max LTV for `USD`: 75%
* Average `USD` supply interest: 6-9%
* `ETH` borrow interest: 2.3%
{% endtab %}

{% tab title="Compound" %}
* Max LTV for rETH on ETH market: 90%
* ETH borrow interest: 2.14%
* COMP reward on ETH borrow: 0.51%
{% endtab %}

{% tab title="Rocket Pool" %}
* Liquid staking APR: 2.6%
{% endtab %}
{% endtabs %}

{% hint style="info" %}
For ease of reference, the example below assumes a starting capital of $100 `USD` and an even split between the 2 positions.
{% endhint %}

### Create a 2x leveraged short USD/ETH position

#### **Steps**

1. Flash loan $50 `USD` amount from Balancer
2. Lend $100 `USD` on Aave
3. Borrow $50 `ETH`

#### **Results**

{% tabs %}
{% tab title="Balances" %}
* Collateral: $100 `USD` lent&#x20;
* Debt: $50 `ETH` borrowed (50% LTV)
* Net Collateral: $50 `USD`
{% endtab %}

{% tab title="Interest" %}
* Net on starting capital: 7.85% `USD`
* Net on borrowed amount: 6.7% `USD` (9% `USD` supply - 2.3% `ETH` borrow)
{% endtab %}
{% endtabs %}

### Create a 5.3x leveraged long rETH/ETH position

#### Steps

1. Swap $50 `USD` for `rETH`
2. Flash loan $215 `rETH` (5.3x max lev with 10% buffer) from Balancer
3. Lend $265 rETH on Compound
4. Borrow $215 `ETH`

#### Results

{% tabs %}
{% tab title="Balances" %}
* Collateral: $265 `rETH` lent
* Debt: $215 `ETH` borrowed (81% LTV)
* Net collateral: $50 `rETH`
{% endtab %}

{% tab title="Interest" %}
* Net on starting capital:&#x20;
  * 2.29% `ETH`
  * 1.35% `COMP`
{% endtab %}
{% endtabs %}

### Final result

The net yields for this strategy are as follows:

* 7.85% USD
* 2.29% ETH
* 1.35% COMP

This is a blended \~11.5% yield which is an additional 2.5% yield as compared to just a pure USD lending strategy (i.e. a 24% yield improvement).
