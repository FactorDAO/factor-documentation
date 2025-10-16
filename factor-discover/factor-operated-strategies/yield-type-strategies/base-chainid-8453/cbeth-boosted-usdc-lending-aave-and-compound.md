# cbETH Boosted USDC Lending - Aave & Compound

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:inbox\_tray: Strategy Deposit Link
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:tools: Strategy Builder Link
{% endhint %}

## Description

This strategy earns blended USDC and ETH yields by taking advantage of differences in Aave and Compound.

By depositing USDC into Aave, this strategy earns 1x the Aave USDC lending interest. This also allows the strategy to borrow WETH against the USDC collateral with a 20% buffer.&#x20;

Borrowed WETH from Aave is swapped for cbETH earning the interest differentials between cbETH liquid staking yields and Aave WETH borrow interest.

The cbETH is then used to create a 8.2x leveraged cbETH:ETH position (2.5% liquidation buffer) which earns an additional 7.2x interest differential between cbETH liquid staking yields and Compound WETH borrow interest. The total WETH borrowed on Compound also earns additional COMP borrow rewards.

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* cbETH continuously increases in value vs WETH.
* WETH borrow cost is less than cbETH liquid staking yields across Aave and Compound (including COMP rewards).
* USDC supply interest is greater than the interest differentials between cbETH yield and WETH borrow.
{% endtab %}

{% tab title="Loss" %}
* cbETH depegs from ETH.
* cbETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Where Does The Yields Come From?

## Comparisons

## Factor Studio Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend $USDC - Aave
2. Borrow $ETH
   1. 62.5% deposit for 20% buffer against LTV
3. Swap borrowed $ETH → $cbETH
4. Flash loan 7.2x the borrowed $cbETH amount
   1. 2.5% buffer from LTV
5. Lend all $cbETH - Compound
6. Borrow $ETH&#x20;
7. Swap $ETH to $cbETH to cover flash loan
{% endtab %}

{% tab title="Exit Strategy" %}
1. Flash loan $ETH
2. Repay $ETH debt - Compound
3. Withdraw $cbETH collateral - Compound
4. Swap $cbETH → $ETH
5. Repay $ETH debt - Aave
6. Withdraw $USDC collateral - Aave
7. Withdraw $USDC
{% endtab %}
{% endtabs %}

## Protocol Parameters

{% tabs %}
{% tab title="Aave" %}
* [\~5.86%](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3) USDC Supply Interest
* [\~2.28%](https://app.aave.com/reserve-overview/?underlyingAsset=0x4200000000000000000000000000000000000006\&marketName=proto_base_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3) USDC Max LTV
{% endtab %}

{% tab title="Compound" %}
* [\~2.36%](https://app.compound.finance/markets/weth-basemainnet) WETH Borrow
* [\~0.30%](https://app.compound.finance/markets/weth-arb) COMP Borrow Rewards
{% endtab %}

{% tab title="Coinbase" %}
* [\~3.27%](https://www.coinbase.com/en-gb/earn/staking/coinbase-wrapped-staked-eth) cbETH Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1QkVZ5UDyhseZYfkbifIQ02EmeId4QNvaoNrirZE8vQ4/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1QkVZ5UDyhseZYfkbifIQ02EmeId4QNvaoNrirZE8vQ4/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1QkVZ5UDyhseZYfkbifIQ02EmeId4QNvaoNrirZE8vQ4/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1RjV85lCCneej7R3vJM8LL6aS5iPYYo2fbbQR9khO69E/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1RjV85lCCneej7R3vJM8LL6aS5iPYYo2fbbQR9khO69E/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1RjV85lCCneej7R3vJM8LL6aS5iPYYo2fbbQR9khO69E/edit?usp=sharing)
{% endembed %}
