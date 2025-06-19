# Diversified USDC Lending Yields - Aave & Compound

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:inbox\_tray:  [Strategy Link](https://pro.factor.fi/strategies/0xCAbb63CFEe43eDE977a01955D1c3742000baddae)
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:tools:  [Strategy Builder Link](https://studio.factor.fi/?hash=0x3419064c42ad1868dcd1f07e760a1b2435bc98646e760f1a2b8bf32e3aa34b7b)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/image (63).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0x3419064c42ad1868dcd1f07e760a1b2435bc98646e760f1a2b8bf32e3aa34b7b">https://studio.factor.fi/?hash=0x3419064c42ad1868dcd1f07e760a1b2435bc98646e760f1a2b8bf32e3aa34b7b</a></p></figcaption></figure>

This strategy earns diversified USDC lending interest on both Aave and Compound.

By lending USDC evenly across Aave and Compound, this strategy captures lending interest from across  two major USDC lending markets. By lending USDC on Compound, this strategy also accrues COMP liquidity rewards.

Lending market risks are split between Aave and Compound, minimizing any adverse market conditions to just half the strategy value.&#x20;

\+ USDC Lending Interest (Aave)

\+ USDC Lending Interest (COmpound)

\+ COMP Lending Rewards

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend 50% $USDC on Aave
2. Lend 50% $USDC on Compound USDC market (cUSDCv3)
{% endtab %}

{% tab title="Exit Strategy" %}
1. Withdraw $USDC from Aave
2. Withdraw $USDC from Compound
{% endtab %}
{% endtabs %}

## Protocol Parameters

{% tabs %}
{% tab title="Aave" %}
* [\~5.11%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Supply Interest
{% endtab %}

{% tab title="Compound" %}
* [\~3.18%](https://app.compound.finance/markets/usdc-arb) USDC Supply Interest
* [\~1.05%](https://app.compound.finance/markets/usdc-arb) COMP rewards
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* USDC lending interest from both Aave and Compound
{% endtab %}

{% tab title="Loss" %}
* USDC depeg resulting in loss of capital value
* Loss from lending market risk is halved through splitting lending across Aave and Compound
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/14BiAX3FCa8UnnzlOmLAw6iBHr1yEk46Qq0Bfl_BJQAo/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/14BiAX3FCa8UnnzlOmLAw6iBHr1yEk46Qq0Bfl\_BJQAo/edit?usp=sharing](https://docs.google.com/spreadsheets/d/14BiAX3FCa8UnnzlOmLAw6iBHr1yEk46Qq0Bfl_BJQAo/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1xz99b4B1I18Nt0ZPPfkbiUT9ESC6uFF8SCGrqir4lLg/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1xz99b4B1I18Nt0ZPPfkbiUT9ESC6uFF8SCGrqir4lLg/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1xz99b4B1I18Nt0ZPPfkbiUT9ESC6uFF8SCGrqir4lLg/edit?usp=sharing)
{% endembed %}
