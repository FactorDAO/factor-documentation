# Amplified wstETH Yields On USDC Lend - Aave

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Deposit Link](https://pro.factor.fi/strategies/0x4a05c725fda5b3b700839f4552be3513ced37f39)
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:arrow\_right: [Strategy Builder Link](https://studio.factor.fi/?hash=0x3daac7c10909d7184cc0cb3e1cdd8f1cf8c601eb9437d69aa7d1b1e84a35f979)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/image (61).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0x3daac7c10909d7184cc0cb3e1cdd8f1cf8c601eb9437d69aa7d1b1e84a35f979">https://studio.factor.fi/?hash=0x3daac7c10909d7184cc0cb3e1cdd8f1cf8c601eb9437d69aa7d1b1e84a35f979</a></p></figcaption></figure>

The vault deposits USDC into Aave to earn lending interest.

By collateralizing the USDC deposit, the vault is able to borrow ETH with a 20% liquidation buffer.

Borrowed ETH is swapped for wstETH to create a leveraged wstETH/ETH position on Aave that earns amplified interest differentials between wstETH liquid staking yields and ETH borrow costs.

\+ USDC supply interest

\+ wstETH liquid staking yields

\- ETH borrow interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend $USDC - Aave
2. Borrow $ETH
   1. 62.5% deposit for 20% buffer against LTV
3. Flash loan 2.5x the borrowed $ETH amount
   1. 5% buffer from LTV
4. Swap all $ETH → $wstETH
5. Lend all $wstETH - Aave
6. Borrow $ETH to cover flash loan
{% endtab %}

{% tab title="Exit Strategy" %}
1. Flash loan $ETH
2. Repay $ETH debt - Aave
3. Withdraw $wstETH collateral - Aave
4. Swap $wstETH → $ETH
5. Repay $ETH debt - Aave
6. Withdraw $USDC collateral - Aave
7. Withdraw $USDC
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Exit Strategy**

Factor Discover also enables Depositors to permissionlessly withdraw from any strategy at anytime via an Exit Strategy.

Visit our [Exit Strategy explainer](../../../../factor-studio/studio-pro/exit-strategy.md) to see how Factor Studio strategies can maximize returns while ensuring truly permissionless withdrawals.
{% endhint %}

## Protocol Parameters

{% tabs %}
{% tab title="Aave" %}
* [\~2.94%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Supply Interest
* [\~2.34%](https://app.aave.com/reserve-overview/?underlyingAsset=0x82af49447d8a07e3bd95bd0d56f35241523fbab1\&marketName=proto_arbitrum_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Max LTV
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0x5979d7b546e38e414f7e9822514be443a4800529\&marketName=proto_arbitrum_v3) wstETH Max LTV
{% endtab %}

{% tab title="Lido" %}
* [\~2.9%](https://stake.lido.fi/) wstETH Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* wstETH continuously increases in value vs WETH.
* WETH borrow cost is less than wstETH liquid staking yields across Aave
* USDC supply interest is greater than the interest differentials between wstETH yield and WETH borrow.
{% endtab %}

{% tab title="Loss" %}
* wstETH depegs from ETH.
* wstETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1AqQt0Uk2gzOYYnJi4ijrFbvjwjsGMm0ywrlMGOdHilY/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1AqQt0Uk2gzOYYnJi4ijrFbvjwjsGMm0ywrlMGOdHilY/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1AqQt0Uk2gzOYYnJi4ijrFbvjwjsGMm0ywrlMGOdHilY/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1FzCCMzjcbHUpzxBq635VNuOmdd1tJBY8GLbfa4R4lMk/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1FzCCMzjcbHUpzxBq635VNuOmdd1tJBY8GLbfa4R4lMk/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1FzCCMzjcbHUpzxBq635VNuOmdd1tJBY8GLbfa4R4lMk/edit?usp=sharing)
{% endembed %}
