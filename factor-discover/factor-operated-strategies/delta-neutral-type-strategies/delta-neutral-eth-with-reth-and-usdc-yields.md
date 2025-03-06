# Delta Neutral ETH With rETH & USDC Yields

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Link](https://pro.factor.fi/strategies/0x1489426648E9E563d0c70D3381aF5ED5dd5CFB77)
{% endhint %}

## Description

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption><p><a href="https://studio.factor.fi/builder?hash=0xd2e21a69f28fdfa35c61b8308a18bed944f4c87fc8979836b85709881f925928">https://studio.factor.fi/builder?hash=0xd2e21a69f28fdfa35c61b8308a18bed944f4c87fc8979836b85709881f925928</a></p></figcaption></figure>

By combining 2 opposing Long and Short positions, this strategy earns yields while maintaining its value throughout short term market volatility. A fall in ETH’s price is covered by a short ETH position and vice versa.

Half of the USDC deposited is used to create a 2.9x rETH/ETH Long position with a 5% liquidation buffer. This earns 1x rETH yield plus an additional 1.9x interest differential between rETH yield and ETH borrow. This is a ETH long position which earns additional liquid staking yields.

The remaining USDC is used to create a 2x USDC/ETH Short position. This earns 1x USDC supply interest plus an additional 1x interest differential between USDC supply and ETH borrow.

\+ USDC Supply Interest

\+ rETH Liquid Staking Yields

\+ rETH Supply Interest

\- ETH Borrow Interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Create 2x USDC/ETH Short
   1. Flash loan 1x of 50% $USDC balance
   2. Lend 50% initial $USDC + flash loaned $USDC amount
   3. Borrow $ETH to cover flash loan
   4. Swap $ETH → $USDC
2. Create a 2.9x rETH/ETH Long
   1. Flash loan 1.9x of 50% $USDC balance in rETH
   2. Swap initial 50% USDC → rETH
   3. Lend all rETH
   4. Borrow ETH to cover flash loan
   5. Swap ETH → rETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Close remaining debt
2. Swap all to withdraw token
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
* [\~0.02%](https://app.aave.com/reserve-overview/?underlyingAsset=0xec70dcb4a1efa46b8f2d97c310c9c4790ba5ffa8\&marketName=proto_arbitrum_v3) rETH Supply Interest
* [\~2.4%](https://app.aave.com/reserve-overview/?underlyingAsset=0x82af49447d8a07e3bd95bd0d56f35241523fbab1\&marketName=proto_arbitrum_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0xaf88d065e77c8cc2239327c5edb3a432268e5831\&marketName=proto_arbitrum_v3) USDC Max LTV
* [69%](https://app.aave.com/reserve-overview/?underlyingAsset=0xec70dcb4a1efa46b8f2d97c310c9c4790ba5ffa8\&marketName=proto_arbitrum_v3) rETH Max LTV
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
* USDC supply interest and rETH liquid staking yields are greater than WETH borrow costs.
* rETH price continously increases relative to WETH.&#x20;
{% endtab %}

{% tab title="Loss" %}
* Long term WETH borrow costs is greater than USDC supply interest and rETH liquid staking yields.
* rETH depegs from ETH.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1q7QjmHZJHceg6Hw9291LVLXN0N2b_ht06tpsD9CbDzo/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1q7QjmHZJHceg6Hw9291LVLXN0N2b\_ht06tpsD9CbDzo/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1q7QjmHZJHceg6Hw9291LVLXN0N2b_ht06tpsD9CbDzo/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/14X58mVppX6Sa2SlJ5KQ3E8J6iPtxT9xHAtzlylu4X6w/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/14X58mVppX6Sa2SlJ5KQ3E8J6iPtxT9xHAtzlylu4X6w/edit?usp=sharing](https://docs.google.com/spreadsheets/d/14X58mVppX6Sa2SlJ5KQ3E8J6iPtxT9xHAtzlylu4X6w/edit?usp=sharing)
{% endembed %}
