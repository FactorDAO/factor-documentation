# Amplified cbETH Yields On cbBTC Lend - Aave

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Link](https://pro.factor.fi/strategies/0xE3aA3021807244104aF88a4026f391C16717e62e)
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:arrow\_right: [Strategy Builder Link](https://studio.factor.fi/?hash=0x99d4d514caca997bf8b60702f213caefdebc3fa58ed0699eb501139ba77ffc3f)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/image (76).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0x99d4d514caca997bf8b60702f213caefdebc3fa58ed0699eb501139ba77ffc3f">https://studio.factor.fi/?hash=0x99d4d514caca997bf8b60702f213caefdebc3fa58ed0699eb501139ba77ffc3f</a></p></figcaption></figure>

The vault collateralizes cbBTC on Aave to earn amplified interest differentials on borrowed ETH.

By collateralizing the cbBTC deposit, the vault is able to borrow ETH with a 20% liquidation buffer while earning a minor cbBTC supply interest.

Borrowed ETH is swapped for cbETH to create a 3.5x leveraged cbETH:ETH position on Aave that earns amplified interest differentials between cbETH liquid staking yields and ETH borrow costs.

\+ cbBTC supply interest

\+ cbETH liquid staking yields

\- ETH borrow interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend $cbBTC - Aave
2. Borrow $ETH
   1. 60.83% deposit for 20% buffer against LTV
3. Flash loan 2.5x the borrowed $ETH amount
   1. 5% buffer from LTV
4. Swap all $ETH → $cbETH
5. Lend all $cbETH - Aave
6. Borrow $ETH to cover flash loan
{% endtab %}

{% tab title="Exit Strategy" %}
1. Flash loan $ETH
2. Repay $ETH debt - Aave
3. Withdraw $cbETH collateral - Aave
4. Swap $cbETH → $ETH
5. Repay $ETH debt - Aave
6. Withdraw $cbBTC collateral - Aave
7. Withdraw $cbBTC
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
* [\~0.21% ](https://app.aave.com/reserve-overview/?underlyingAsset=0xcbb7c0000ab88b473b1f5afd9ef808440eed33bf\&marketName=proto_base_v3)USDC Supply Interest
* [\~2.43%](https://app.aave.com/reserve-overview/?underlyingAsset=0x4200000000000000000000000000000000000006\&marketName=proto_base_v3) WETH Borrow Interest
* [73%](https://app.aave.com/reserve-overview/?underlyingAsset=0xcbb7c0000ab88b473b1f5afd9ef808440eed33bf\&marketName=proto_base_v3) cbBTC Max LTV
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0x5979d7b546e38e414f7e9822514be443a4800529\&marketName=proto_arbitrum_v3) cbETH Max LTV
{% endtab %}

{% tab title="Coinbase" %}
* [\~3.09%](https://www.coinbase.com/en-gb/earn/staking/coinbase-wrapped-staked-eth) cbETH Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* cbETH continuously increases in value vs WETH.
* WETH borrow cost is less than cbETH liquid staking yields across Aave
* cbBTC supply interest is greater than the interest differentials between cbETH yield and WETH borrow.
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

{% embed url="https://docs.google.com/spreadsheets/d/11fCowOqo8Q5hebFpyqdZg7F3_f6dz4z3mc-YUGRLXU8/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/11fCowOqo8Q5hebFpyqdZg7F3\_f6dz4z3mc-YUGRLXU8/edit?usp=sharing](https://docs.google.com/spreadsheets/d/11fCowOqo8Q5hebFpyqdZg7F3_f6dz4z3mc-YUGRLXU8/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1F24QvyHyp58FnN6ZCtfW51fzOza0apK5pRvkJaBLFB4/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1F24QvyHyp58FnN6ZCtfW51fzOza0apK5pRvkJaBLFB4/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1F24QvyHyp58FnN6ZCtfW51fzOza0apK5pRvkJaBLFB4/edit?usp=sharing)
{% endembed %}
