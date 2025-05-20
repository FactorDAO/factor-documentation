# Amplified rETH Yields On USDC Lend

{% hint style="info" %}
Compound is coming soon! Mix-and-match borrows across multiple lending protocols on Factor Studio!
{% endhint %}

## Description

The vault deposits USDC into Aave to earn lending interest.

By collateralizing the USDC deposit, the vault is able to borrow ETH with a 20% liquidation buffer.

Borrowed ETH is swapped for rETH to create a leveraged rETH/ETH position on Compound that earns amplified interest differentials between rETH liquid staking yields and ETH borrow costs.

\+ USDC supply interest

\+ rETH liquid staking yields

\- ETH borrow interest

\+ COMP rewards on ETH borrow

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend $USDC - Aave
2. Borrow $ETH
   1. 62.5% deposit for 20% buffer against LTV
3. Flash loan 4.5x the borrowed $ETH amount
   1. 10% buffer from LTV
4. Swap all $ETH → $rETH
5. Lend all $rETH - Compound
6. Borrow $ETH to cover flash loan
{% endtab %}

{% tab title="Exit Strategy" %}
1. Flash loan $ETH
2. Repay $ETH debt - Compound
3. Withdraw $rETH collateral - Compound
4. Swap $rETH → $ETH
5. Repay $ETH debt - Aave
6. Withdraw $USDC collateral - Aave
7. Withdraw $USDC
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

{% tab title="Compound" %}
* [\~2.1%](https://app.compound.finance/markets/weth-arb) WETH Borrow
* [\~0.6%](https://app.compound.finance/markets/weth-arb) COMP Borrow Rewards
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
* WETH borrow cost is less than rETH liquid staking yields across Aave and Compound (including COMP rewards).
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

{% embed url="https://docs.google.com/spreadsheets/d/1cqfXsKPZp4DLVuKOmDuCdeJWQykKzT3cRUpBsWIFs9g/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1cqfXsKPZp4DLVuKOmDuCdeJWQykKzT3cRUpBsWIFs9g/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1cqfXsKPZp4DLVuKOmDuCdeJWQykKzT3cRUpBsWIFs9g/edit?usp=sharing)
{% endembed %}
