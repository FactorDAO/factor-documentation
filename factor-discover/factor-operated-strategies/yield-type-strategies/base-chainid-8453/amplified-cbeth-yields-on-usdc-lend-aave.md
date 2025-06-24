# Amplified cbETH Yields On USDC Lend - Aave

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Deposit Link](https://pro.factor.fi/strategies/0x4A3de8A60A853f0436E0fA38c0FDcF0b8035E525)
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:arrow\_right: [Strategy Builder Link](https://studio.factor.fi/?hash=0xa383182aa4e1feece921d7e65ff0ce55476964a4bc27398772abb084291e696a)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/Amplified cbETH Yields On USDC Lend.jpeg" alt=""><figcaption></figcaption></figure>

The vault deposits USDC into Aave to earn lending interest.

By collateralizing the USDC deposit, the vault is able to borrow ETH with a 20% liquidation buffer.

Borrowed ETH is swapped for cbETH to create a 3.5x leveraged cbETH:ETH position on Aave that earns amplified interest differentials between cbETH liquid staking yields and ETH borrow costs.

\+ USDC supply interest

\+ cbETH liquid staking yields

\- ETH borrow interest

## Strategy

<figure><img src="../../../../.gitbook/assets/image (79).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0xa383182aa4e1feece921d7e65ff0ce55476964a4bc27398772abb084291e696a">https://studio.factor.fi/?hash=0xa383182aa4e1feece921d7e65ff0ce55476964a4bc27398772abb084291e696a</a></p></figcaption></figure>

{% tabs %}
{% tab title="Main strategy" %}
1. Lend $USDC - Aave
2. Borrow $ETH
   1. 62.5% deposit for 20% buffer against LTV
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
* [\~5.77%](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3) USDC Supply Interest
* [\~2.43%](https://app.aave.com/reserve-overview/?underlyingAsset=0x4200000000000000000000000000000000000006\&marketName=proto_base_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Max LTV
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

{% embed url="https://docs.google.com/spreadsheets/d/1GZy-aRVCG_MRxJjphwMAaxYQy4AkJdzvMRp9-CEKNMc/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1GZy-aRVCG\_MRxJjphwMAaxYQy4AkJdzvMRp9-CEKNMc/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1GZy-aRVCG_MRxJjphwMAaxYQy4AkJdzvMRp9-CEKNMc/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1BTVCYVrNmHfY61-6pyZoF-FXr57eXcIekdEuUcG98mc/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1BTVCYVrNmHfY61-6pyZoF-FXr57eXcIekdEuUcG98mc/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1BTVCYVrNmHfY61-6pyZoF-FXr57eXcIekdEuUcG98mc/edit?usp=sharing)
{% endembed %}
