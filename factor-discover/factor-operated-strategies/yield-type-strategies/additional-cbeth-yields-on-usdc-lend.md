# Additional cbETH Yields On USDC Lend

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: Strategy Link
{% endhint %}

## Description

This strategy earns USDC lending interest on Aave and borrows ETH to generate additional cbETH liquid staking yields.

By swapping borrowed ETH for cbETH, this strategy earns the the difference between cbETH liquid staking yields and ETH borrow interest. Liquid staking yields accrues natively to the liquid staked token and is reflected in cbETH price always appreciating against ETH.

\+ USDC Lending Interest

\+ cbETH Liquid Staking Yields

\- ETH Borrow Interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend all $USDC - Aave
2. Borrow $WETH
   1. 62.5% of collateral value for 20% buffer
3. Swap $WETH → $cbETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Swap $cbETH → $WETH
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
* [\~5.7% ](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3)USDC Supply Interest
* [\~2.5%](https://app.aave.com/reserve-overview/?underlyingAsset=0x4200000000000000000000000000000000000006\&marketName=proto_base_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3) USDC Max LTV
{% endtab %}

{% tab title="Coinbase" %}
* [\~3.1%](https://www.coinbase.com/en-gb/earn/staking/coinbase-wrapped-staked-eth) rETH Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* cbETH continuously increases in value vs WETH.
* WETH borrow cost is less than cbETH liquid staking yields.
* USDC supply interest is greater than the interest differentials between cbETH yield and WETH borrow.
{% endtab %}

{% tab title="Loss" %}
* cbETH depegs from ETH.
* cbETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1TLfW0SncYQVlGB5zGZYFP0QLhhWrgI9GsOQl_UC_v6c/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1TLfW0SncYQVlGB5zGZYFP0QLhhWrgI9GsOQl\_UC\_v6c/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1TLfW0SncYQVlGB5zGZYFP0QLhhWrgI9GsOQl_UC_v6c/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1HQixpwzumoEXx8lB-2CI0YBMEUsV-VP_EG_A7O29vmM/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1HQixpwzumoEXx8lB-2CI0YBMEUsV-VP\_EG\_A7O29vmM/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1HQixpwzumoEXx8lB-2CI0YBMEUsV-VP_EG_A7O29vmM/edit?usp=sharing)
{% endembed %}
