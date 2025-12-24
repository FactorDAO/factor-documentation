# wstETH Boosted USDC Lending - Aave & Compound

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:inbox\_tray: [Strategy Deposit Link](https://pro.factor.fi/strategies/0x8C1f45D2A08c30cB258603378ad5Ac170935F41D)
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:tools: [Strategy Builder Link](https://studio.factor.fi/?hash=0xb0e29413a72a47536193144b412d7a107580d77408cd21aee8a79dd26ad29584)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/wstETH Boosted USDC Lending - Aave &#x26; Compound-Overview.jpg" alt=""><figcaption></figcaption></figure>

This strategy earns blended USDC and ETH yields by taking advantage of differences in Aave and Compound.

By depositing USDC into Aave, this strategy earns 1x the Aave USDC lending interest. This also allows the strategy to borrow WETH against the USDC collateral with a 20% buffer.&#x20;

Borrowed WETH from Aave is swapped for wstETH earning the interest differentials between wstETH liquid staking yields and Aave WETH borrow interest.

The wstETH is then used to create a 7.1x leveraged wstETH:ETH position (2.5% liquidation buffer) which earns an additional 6.1x interest differential between wstETH liquid staking yields and Compound WETH borrow interest. The total WETH borrowed on Compound also earns additional COMP borrow rewards.

## Strategy Performance Conditions

<figure><img src="../../../../.gitbook/assets/wstETH Boosted USDC Lending - Aave &#x26; Compound-Risks vs Returns (1).jpg" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Profit" %}
* wstETH continuously increases in value vs WETH.
* WETH borrow cost is less than wstETH liquid staking yields across Aave and Compound (including COMP rewards).
* USDC supply interest is greater than the interest differentials between wstETH yield and WETH borrow.
{% endtab %}

{% tab title="Loss" %}
* wstETH depegs from ETH.
* wstETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Where Does The Yields Come From?

<figure><img src="../../../../.gitbook/assets/wstETH Boosted USDC Lending - Aave &#x26; Compound-Yield.jpg" alt=""><figcaption></figcaption></figure>

## Comparisons

<figure><img src="../../../../.gitbook/assets/wstETH Boosted USDC Lending - Aave &#x26; Compound-Comparison.jpg" alt=""><figcaption></figcaption></figure>

## Factor Studio Strategy

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption><p><a href="https://studio.factor.fi/builder?hash=0x8c1f45d2a08c30cb258603378ad5ac170935f41d">https://studio.factor.fi/builder?hash=0x8c1f45d2a08c30cb258603378ad5ac170935f41d</a></p></figcaption></figure>

{% tabs %}
{% tab title="Main strategy" %}
1. Lend $USDC - Aave
2. Borrow $ETH
   1. 62.5% deposit for 20% buffer against LTV
3. Swap borrowed $ETH → $wstETH
4. Flash loan 6.1x the borrowed $wstETH amount
   1. 2.5% buffer from LTV
5. Lend all $wstETH - Compound
6. Borrow $ETH&#x20;
7. Swap $ETH to $wstETH to cover flash loan
{% endtab %}

{% tab title="Exit Strategy" %}
1. Flash loan $ETH
2. Repay $ETH debt - Compound
3. Withdraw $wstETH collateral - Compound
4. Swap $wstETH → $ETH
5. Repay $ETH debt - Aave
6. Withdraw $USDC collateral - Aave
7. Withdraw $USDC
{% endtab %}
{% endtabs %}

## Protocol Parameters

{% tabs %}
{% tab title="Aave" %}
* [\~5.11%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Supply Interest
* [\~2.33%](https://app.aave.com/reserve-overview/?underlyingAsset=0x82af49447d8a07e3bd95bd0d56f35241523fbab1\&marketName=proto_arbitrum_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Max LTV
{% endtab %}

{% tab title="Compound" %}
* [\~2.1%](https://app.compound.finance/markets/weth-arb) WETH Borrow
* [\~0.64%](https://app.compound.finance/markets/weth-arb) COMP Borrow Rewards
{% endtab %}

{% tab title="Lido" %}
* [\~3.2%](https://stake.lido.fi/) wstETH Liquid Staking Yields
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

{% embed url="https://docs.google.com/spreadsheets/d/1p_hk69aImsLMgbzjQlY37vjMza9jAwqR4yjd_34WzaY/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1p\_hk69aImsLMgbzjQlY37vjMza9jAwqR4yjd\_34WzaY/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1p_hk69aImsLMgbzjQlY37vjMza9jAwqR4yjd_34WzaY/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1gUzTfwhzOW6iTslSMoJvnkI0KxkiB99hCHxrfBo6dZ8/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1gUzTfwhzOW6iTslSMoJvnkI0KxkiB99hCHxrfBo6dZ8/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1gUzTfwhzOW6iTslSMoJvnkI0KxkiB99hCHxrfBo6dZ8/edit?usp=sharing)
{% endembed %}
