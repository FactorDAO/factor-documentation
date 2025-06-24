# Delta Neutral ETH With cbETH & USDC Yields

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Deposit Link](https://pro.factor.fi/strategies/0x42B5b7B5b0B33ce41bF19d1609aacB0f006D613a)
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:arrow\_right: [Strategy Builder Link](https://studio.factor.fi/?hash=0x2a8e47f3bbe733a5d49aa613d8b81dcf7caf11fb8213db2796055075de49dd22)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/image (78).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0x2a8e47f3bbe733a5d49aa613d8b81dcf7caf11fb8213db2796055075de49dd22">https://studio.factor.fi/?hash=0x2a8e47f3bbe733a5d49aa613d8b81dcf7caf11fb8213db2796055075de49dd22</a></p></figcaption></figure>

By combining 2 opposing Long and Short positions, this strategy earns yields while maintaining its value throughout short term market volatility. A fall in ETH’s price is covered by a short ETH position and vice versa.

Half of the USDC deposited is used to create a 2x USDC/ETH Short position with a 20% liquidation buffer. This earns 1x USDC lending interest (on initial deposit amount) with a 0.5x ETH borrow position. If ETH price drops relative to USDC, the debt owed decreases and vice versa.

To offset the risks of increasing debt on the USDC/ETH short position, the remaining USDC deposited is swapped for cbETH. The upside exposure of holding cbETH cancels out the downside exposure of the ETH debt from the above short USDC/ETH position. Additionally, cbETH continues to earn liquid staking yields which historically has been above the ETH borrow interest.

\+ USDC Supply Interest

\+ cbETH Liquid Staking Yields

\- ETH Borrow Interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Create 2x USDC/ETH Short
   1. Flash loan 2x of 50% $USDC balance
   2. Lend 50% initial $USDC + flash loaned $USDC amount
   3. Borrow $ETH to cover flash loan
   4. Swap $ETH → $USDC
2. Swap 50% $USDC deposit for $cbETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Close remaining debt
2. Swap all to withdraw token
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
* [\~5.68%](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3) USDC Supply Interest
* [\~2.58%](https://app.aave.com/reserve-overview/?underlyingAsset=0x4200000000000000000000000000000000000006\&marketName=proto_base_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3) USDC Max LTV
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0x2ae3f1ec7f1f5012cfeab0185bfc7aa3cf0dec22\&marketName=proto_base_v3) cbETH Max LTV
{% endtab %}

{% tab title="Coinbase" %}
* [\~3.1%](https://www.coinbase.com/en-gb/earn/staking/coinbase-wrapped-staked-eth) cbETH Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* USDC supply interest and cbETH liquid staking yields are greater than WETH borrow costs.
* cbETH price continuously increases relative to WETH.&#x20;
{% endtab %}

{% tab title="Loss" %}
* Long term WETH borrow costs is greater than USDC supply interest and cbETH liquid staking yields.
* cbETH depegs from ETH.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1u86xqxLthHIBSp0flGGG-FqgCqW3qk5nEc_apkyhZI0/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1u86xqxLthHIBSp0flGGG-FqgCqW3qk5nEc\_apkyhZI0/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1u86xqxLthHIBSp0flGGG-FqgCqW3qk5nEc_apkyhZI0/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1wekMatG1ZiGnJmoyz89oWqMUK3cPsukVHF8n7FgTQvE/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1wekMatG1ZiGnJmoyz89oWqMUK3cPsukVHF8n7FgTQvE/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1wekMatG1ZiGnJmoyz89oWqMUK3cPsukVHF8n7FgTQvE/edit?usp=sharing)
{% endembed %}
