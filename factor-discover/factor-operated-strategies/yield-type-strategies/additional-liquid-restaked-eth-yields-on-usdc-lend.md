# Additional Liquid Restaked ETH Yields On USDC Lend

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Link](https://pro.factor.fi/strategies/0x549D2315d99F0c50872DA2E33a2b027514BD7812)
{% endhint %}

## Description

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption><p><a href="https://studio.factor.fi/builder?hash=0x1d711d4ec0159a6f9a678c85517df63805a01970707157e880e2c11b8e5aa282">https://studio.factor.fi/builder?hash=0x1d711d4ec0159a6f9a678c85517df63805a01970707157e880e2c11b8e5aa282</a></p></figcaption></figure>

This strategy earns USDC lending interest on Aave and borrows ETH to generate additional ETH restaking yields.

By swapping borrowed ETH for weETH, ezETH, and rsETH, this strategy earns the the difference between liquid restaking yields and ETH borrow interest. Liquid restaking yields accrues natively to the liquid staked token and is reflected in liquid restaked token price always appreciating against ETH.

\+ USDC Lending Interest

\+ weETH Liquid Staking Yields

\+ ezETH Liquid Staking Yields

\+ rsETH Liquid Staking Yields

\- ETH Borrow Interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend all $USDC - Aave
2. Borrow $WETH
   1. 62.5% of collateral value for 20% buffer
3. Swap 33% $WETH → $weETH
4. Swap 33% $WETH → $ezETH
5. Swap 33% $WETH → $rsETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Swap all $weETH → $WETH
2. Swap all $ezETH → $WETH
3. Swap all $rsETH → $WETH
4. Repay $WETH debt - Aave
5. Withdraw $USDC collateral
6. Close remaining debt
7. Swap all to withdraw token
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

{% tab title="Ether.fi" %}
* [\~3.7%](https://app.ether.fi/weeth) weETH Liquid Staking Yields
{% endtab %}

{% tab title="Renzo" %}
* [\~4.1%](https://app.renzoprotocol.com/restaking) ezETH Liquid Restaking Yields
{% endtab %}

{% tab title="Kelp" %}
* [\~4.1%](https://kerneldao.com/kelp/restake/) rsETH Liquid Restaking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* weETH/ezETH/rsETH continuously increases in value vs WETH.
* WETH borrow cost is less than weETH/ezETH/rsETH liquid restaking yields.
* USDC supply interest is greater than the interest differentials between weETH/ezETH/rsETH yield and WETH borrow.
{% endtab %}

{% tab title="Loss" %}
* weETH/ezETH/rsETH depegs from ETH.
* weETH/ezETH/rsETH liquid restaking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1DPuJzHnpyTe2EfBr10ZehHpcaLQhJq8wH3Ea9kBcr10/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1DPuJzHnpyTe2EfBr10ZehHpcaLQhJq8wH3Ea9kBcr10/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1DPuJzHnpyTe2EfBr10ZehHpcaLQhJq8wH3Ea9kBcr10/edit?usp=sharing)
{% endembed %}
