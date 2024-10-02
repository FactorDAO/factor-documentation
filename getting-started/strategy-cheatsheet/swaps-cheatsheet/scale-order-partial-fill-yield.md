# Scale Order Partial Fill Yield

## Overview

<figure><img src="../../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Pseudo Scale Orders**

By adding single-sided concentrated liquidity, your position functions as a automated DCA into/out of a token while earning AMM trading fees. See [Automated Scale Order](automated-scale-order.md) for more info.
{% endhint %}

Lock in your scale order partial fills and earn supply interest on your newly acquired tokens while waiting for your remaining scale order to fill.&#x20;

This strategy requires an existing concentrated liquidity position whose price range covers the current market price (i.e. single-sided liquidity has been partially converted to double-sided liquidity).

## Potential Alpha

* **Lock In Trades:** By removing your desired token from the position and narrowing your new position price range, you ensure that the tokens can no longer be automatically traded by the AMM therefore acting as profit taking or stop loss confirmations.
* **Partial Fill Yield:** Earn a supply interest on your newly acquired tokens by depositing into a lending pool to earn yield without any impermanent loss risks.
* **Gradually Buy At Lower Prices:** Purchase tokens along a smooth price curve starting from your start price to your specified end price.
* **Gradually Sell At Higher Prices:** Sell tokens along a smooth price curve starting from your start price to your specified end price.
* **Earn From Market Spreads:** Earn additional trading fees from short term volatility within your selected range.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-studio/studio-contracts/lp-management/"><strong>Remove Liquidity</strong></a></summary>

* Remove all liquidity from existing position.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Deposit the token you were trading to into the target lending pool.

</details>

<details>

<summary><a href="../../../factor-studio/studio-contracts/lp-management/"><strong>Provide Liquidity</strong></a></summary>

* You will now be left with the remaining tokens left to trade from which can then be added to a new single sided liquidity position.
* Create a new position with a narrower range. The price range adjustment will depend on the direction of trade:
  * Buy: Min price will remain the same as the initial position's min price. Max price will decrease by the proportion of tokens already bought.
  * Sell: Min price will increase by the proportion of tokens already sold. Max price will remain the same as the initial position's max price.

</details>
