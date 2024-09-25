# Borrow

## Overview

The [Borrow Building Block](../../../factor-building-blocks/borrow.md) functions as an automation and composability layer between the borrow request and multiple integrated lending protocols. With the Borrow Building Block, strategies can source more liquidity for amplified gains via an endless variety of multi-token strategies.

## Actions

{% hint style="info" %}
You will need to collateralize assets via the Lending Building Block before you can initiate a collatarallized borrow from the underlying markets.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

1. **Debt Token:** Select the token to borrow by searching via token symbol or name. Tokens borrowed will be charged a dynamic borrow interest.
2. **Lending Amount:** The number of debt tokens to borrow from the selected lending market. The number of tokens available to borrow will be dependent on the value of your collateral as well as the [collateralization ratio](../../../getting-started/glossary.md#collateralisation-ratio) of your selected market.
3. **Protocol:** Select the underlying lending protocol to borrow from.
4. **Lending Market:** Select a lending market which you have previously provided collateral to.
