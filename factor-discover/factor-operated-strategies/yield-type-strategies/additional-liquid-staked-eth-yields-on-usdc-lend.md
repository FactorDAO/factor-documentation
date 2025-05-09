# Additional Liquid Staked ETH Yields On USDC Lend

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Link](https://pro.factor.fi/strategies/0xfe67342abc06e69b4d319ef6b298b135cff596cc)
{% endhint %}

## Description

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0x203b3da5bb64d3119528042d367a214d8778eca0821dc91d9d285bbaf47c9a87">https://studio.factor.fi/?hash=0x203b3da5bb64d3119528042d367a214d8778eca0821dc91d9d285bbaf47c9a87</a></p></figcaption></figure>

This strategy earns USDC lending interest on Aave and borrows ETH to generate additional ETH liquid staking yields.

By swapping borrowed ETH for rETH & wstETH, this strategy earns the the difference between rETH/wstETH liquid staking yields and ETH borrow interest. Liquid staking yields accrues natively to the liquid staked token and is reflected in rETH/wstETH price always appreciating against ETH.

\+ USDC Lending Interest

\+ rETH Liquid Staking Yields

\+ wstETH Liquid Staking Yields

\- ETH Borrow Interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend all $USDC - Aave
2. Borrow $WETH
   1. 62.5% of collateral value for 20% buffer
3. Swap 50% $WETH → $rETH
4. Swap 50% $WETH → $wstETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Swap $rETH → $WETH
2. Swap $wstETH → $WETH
3. Repay $WETH debt - Aave
4. Withdraw $USDC collateral
5. Close remaining debt
6. Swap all to withdraw token
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
* [\~2.7% ](https://rocketpool.net/)rETH Liquid Staking Yields
{% endtab %}

{% tab title="Lido" %}
* [\~2.8%](https://lido.fi/) Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* rETH/wstETH continuously increases in value vs WETH.
* WETH borrow cost is less than rETH/wstETH liquid staking yields.
* USDC supply interest is greater than the interest differentials between rETH/wstETH yield and WETH borrow.
{% endtab %}

{% tab title="Loss" %}
* rETH/wstETH depegs from ETH.
* rETH/wstETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1_vACL35FxqB018yxyZ6FrHixxcVuZ2sWrOLPr3UX0C4/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1\_vACL35FxqB018yxyZ6FrHixxcVuZ2sWrOLPr3UX0C4/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1_vACL35FxqB018yxyZ6FrHixxcVuZ2sWrOLPr3UX0C4/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1Mj0kiPxqtbJeJAC5CSExpDxvEzs4dlUH7Wktwjx4dlk/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1Mj0kiPxqtbJeJAC5CSExpDxvEzs4dlUH7Wktwjx4dlk/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1Mj0kiPxqtbJeJAC5CSExpDxvEzs4dlUH7Wktwjx4dlk/edit?usp=sharing)
{% endembed %}
