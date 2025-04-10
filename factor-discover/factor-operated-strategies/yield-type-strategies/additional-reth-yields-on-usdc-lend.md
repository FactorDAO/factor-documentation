# Additional rETH Yields On USDC Lend

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Link](https://pro.factor.fi/strategies/0x99E11bF7f92b1D486F8D88Bc5F467C695836f8A2)
{% endhint %}

## Description

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0x894ba2383b0e7923446f5df18e38dd450266ebe3e5961a27f79eb86dbaace6e3">https://studio.factor.fi/?hash=0x894ba2383b0e7923446f5df18e38dd450266ebe3e5961a27f79eb86dbaace6e3</a></p></figcaption></figure>

This strategy earns USDC lending interest on Aave and borrows ETH to generate additional ETH liquid staking yields.

By swapping borrowed ETH for rETH, this strategy earns the the difference between rETH liquid staking yields and ETH borrow interest. Liquid staking yields accrues natively to the liquid staked token and is reflected in rETH price always appreciating against ETH.

\+ USDC Lending Interest

\+ rETH Liquid Staking Yields

\- ETH Borrow Interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend all $USDC - Aave
2. Borrow $WETH
   1. 62.5% of collateral value for 20% buffer
3. Swap $WETH → $rETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Swap $rETH → $WETH
2. Repay $WETH debt - Aave
3. Withdraw $USDC collateral
4. Close remaining debt
5. Swap all to withdraw token
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
* [\~2.4%](https://app.aave.com/reserve-overview/?underlyingAsset=0x82af49447d8a07e3bd95bd0d56f35241523fbab1\&marketName=proto_arbitrum_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Max LTV
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
* rETH continuously increases in value vs WETH.
* WETH borrow cost is less than rETH liquid staking yields.
* USDC supply interest is greater than the interest differentials between rETH yield and WETH borrow.
{% endtab %}

{% tab title="Loss" %}
* rETH depegs from ETH.
* rETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1EYxoyRmWFF7O1tLAGpf_dBMqtyTpexfxaEgDQ2TiyDk/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1EYxoyRmWFF7O1tLAGpf\_dBMqtyTpexfxaEgDQ2TiyDk/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1EYxoyRmWFF7O1tLAGpf_dBMqtyTpexfxaEgDQ2TiyDk/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1_SAtMjfsbUuGSxeVfAanTA1XTtWTuH5vvYI9Fu6seY4/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1\_SAtMjfsbUuGSxeVfAanTA1XTtWTuH5vvYI9Fu6seY4/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1_SAtMjfsbUuGSxeVfAanTA1XTtWTuH5vvYI9Fu6seY4/edit?usp=sharing)
{% endembed %}
