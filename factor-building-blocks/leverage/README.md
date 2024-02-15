# 🔄 Leverage

## Overview

Factor Leverage Building Block facilitates advanced [collateralized lending and borrowing](concepts/collateralized-lending-and-borrowing.md) management across multiple DeFi lending protocols. By codifying the convoluted lending processes, the Leverage Building Block provides a simple interface enabling lenders to quickly manage their positions in accordance with market dynamics.

The Leverage Building Block currently supports the following operations:

* Create Lending Position
* Withdraw Lending Position
* Create Borrow Position
* Repay Borrowed Position
* Refinance Position

With integrations across multiple lending protocols, lenders are free to choose between their preferred protocols, tokens, and strategies without worrying about specific protocol differences. The Leverage Building Block allows lenders to easily access more liquidity while offsetting the opportunity costs of [HODL](https://www.investopedia.com/terms/h/hodl.asp)ing their favourite tokens.

<details>

<summary>Related Concepts</summary>

* [Collateralized Lending](concepts/collateralized-lending-and-borrowing.md)
* [Looping](concepts/looping.md)

</details>

## Features

* **Access More Liquidity:** Maintain exposure to collateralized assets while maximizing capital efficiency by borrowing tokens against your lending position.
* [**One-Click Looping**](concepts/looping.md#one-click-looping)**:** Choose your desired leverage multiplier and the Leverage Building Block handles the complex process of depositing, borrowing, and looping.
* **Collateral And Debt Asset Switching:** Easily replace your collateral or borrowed token with an alternate token in a single transaction.
* **Effortless Refinancing:** Compare lending terms across multiple protocols and seamlessly migrate your leveraged position to take advantage of market conditions.
* **Liquidation Safeguards:** Immediate liquidations risks are minimized through customizable parameters that enable risk management flexibility.
* **Real Time Updates:** The Leverage Building Block provides real time data for crucial position metrics such as Loan-To-Value (LTV), liquidation factors, as well as health factors.

## Integrations

Factor has integrated with leading lending protocols, offering a broad spectrum of possibilities for your strategies.

* [Aave](https://aave.com/)
* [Lodestar Finance](https://www.lodestarfinance.io/)
* [Tender.Fi](https://www.tender.fi/)

Visit our [**Discover**](https://app.factor.fi/discover) page to see the latest leverage strategies.

{% hint style="success" %}
**Don't Limit Your Strategies To Just Leverage**

[Factor Studio](../../factor-studio/factor-studio.md) enables different [Building Blocks](../factor-building-blocks.md) to be mixed-and-matched thereby facilitating multi-step strategies which span across the whole DeFi ecosystem.

Please refer to [Supported Protocols](../../getting-started/supported-protocols.md) to view the full list of DeFi protocols which have been integrated with Factor Studio.
{% endhint %}

## Next Steps

{% tabs %}
{% tab title="Users" %}
* [Take Out A Loan](user-guides/take-out-a-loan.md)
* [Manage Your Loan](user-guides/manage-your-loan.md)
* [Refinance Your Loan](user-guides/refinance-your-loan.md)
{% endtab %}

{% tab title="Strategy Builders" %}
{% hint style="info" %}
:construction: This section is under construction. Stay tuned for exciting updates coming real soon!
{% endhint %}
{% endtab %}
{% endtabs %}
