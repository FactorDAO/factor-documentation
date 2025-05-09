# WBTC Base Switch On rETH For ETH & USDC Yields

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Link](https://pro.factor.fi/strategies/0x1D45B72F007cacB78333AB2aC10128562CabC44c)
{% endhint %}

## Description

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0xb53572bd4b8e3a597bfb7589faec5828432da28cfd9e16de9cd93097c7ce35ab">https://studio.factor.fi/?hash=0xb53572bd4b8e3a597bfb7589faec5828432da28cfd9e16de9cd93097c7ce35ab</a></p></figcaption></figure>

An ETH rotation play which earns USD yields on rETH by switching the base asset from USD → WBTC. This strategy profits when ETH outperforms WBTC and is profitable as long as the generated USDC lending interest is greater than rETH to WBTC underperformance.

\+ USDC Lending Interest

\+ rETH Liquid Staking Yields

\+ rETH Lending Interest

\- WBTC Borrow Interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Flash loan $rETH equivalent to 100% USDC value
2. Lend $rETH - Aave
3. Lend $USDC - Aave
4. Borrow $WBTC
   1. 100% of initial $USD value
5. Swap all $WBTC → $rETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Close remaining debt
2. Swap all to withdraw token
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Exit Strategy**

Factor Discover also enables Depositors to permissionlessly withdraw from any strategy at anytime via an Exit Strategy.

Visit our [Exit Strategy explainer](../../../factor-studio/studio-pro/exit-strategy.md) to see how Factor Studio strategies can maximize returns while ensuring truly permissionless withdrawals.
{% endhint %}

## Protocol Parameters

{% tabs %}
{% tab title="Aave" %}
* [\~6%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Supply Interest
* [\~0.02%](https://app.aave.com/reserve-overview/?underlyingAsset=0xec70dcb4a1efa46b8f2d97c310c9c4790ba5ffa8\&marketName=proto_arbitrum_v3) rETH Supply Interest
* [\~0.3%](https://app.aave.com/reserve-overview/?underlyingAsset=0x2f2a2543b76a4166549f7aab2e75bef0aefc5b0f\&marketName=proto_arbitrum_v3) WBTC Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Max LTV
* [69%](https://app.aave.com/reserve-overview/?underlyingAsset=0xec70dcb4a1efa46b8f2d97c310c9c4790ba5ffa8\&marketName=proto_arbitrum_v3) rETH Max LTV
{% endtab %}

{% tab title="Rocket Pool" %}
* [\~2.7%](https://rocketpool.net/) rETH Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* WETH, and by extension rETH, outperforms WBTC for the period of the deposit.
* USDC supply interest and rETH liquid staking yields are greater than WBTC borrow costs.
{% endtab %}

{% tab title="Loss" %}
* WBTC outperforms WETH.
* rETH depegs from ETH.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1FvNDdfvoec_mQCiDzIPjEGrJWM652I1S2fWFMlK83qE/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1FvNDdfvoec\_mQCiDzIPjEGrJWM652I1S2fWFMlK83qE/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1FvNDdfvoec_mQCiDzIPjEGrJWM652I1S2fWFMlK83qE/edit?usp=sharing)
{% endembed %}

## Estimate Returns

The profitability of this strategy depends on the performance of ETH relative to WBTC. Aside from potential trading returns, the strategy also earns a net yield of \~6.7% (as of 06/03/25) that comprises of:

* USDC lending interest
* rETH liquid staking yields
* WBTC borrow costs
