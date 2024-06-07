# Platform Fees

### Overview

Factor generates its primary revenue through transaction-based fees across Factor strategy vaults. The platform is designed to balance revenue generation while incentivizing greater governance participation through the redistribution of platform revenues:

* **veFCTR Revenue Share:** 50% of the protocol's ongoing revenue is automatically distributed to veFCTR holders as [USDC](https://arbiscan.io/token/0xaf88d065e77c8cc2239327c5edb3a432268e5831)
* [**Factor Scale**](../factor-scale/)**:** Weekly gauge emissions rewards
* [**Factor Boost**](../factor-boost/)**:** Liquidity incentives for strategy depositors

Platform fees are configurable and can be updated by the vault owner. Vaults which are owned by Factor (the organization) are updated via a multisig.

<details>

<summary>Utility Fees</summary>

Utility fees are levied on standard portfolio management actions and are enforced via Factor's permissionless smart contracts. As you always maintain custody of your tokens, the utility fees functions as a Factor platform usage/convenience fee. Factor combines multiple DeFi primitives into a single transaction thereby saving you time, resources, and the uncertainties that comes with handling multiple transaction manually.

</details>

<details>

<summary>Harvest Fees</summary>

Harvest fees are variable fees that are dependent on the profitability of the strategy. Factor enables the automation of yield compounding as well as various other alpha investment strategies. Through periodic or event based profit taking transactions, Factor locks in and amplifies any profits generated by the automated strategy.

</details>

{% hint style="info" %}
**Factor Fee Receiver Address:** [`0x0fD4643B81F0B58358eF500A06aA4A3F3E0cDE62`](https://arbiscan.io/address/0x0fD4643B81F0B58358eF500A06aA4A3F3E0cDE62)
{% endhint %}

### **Fee Structure**

<details>

<summary>Yield Strategies</summary>

* **Deposit:** 0.2% of deposited amount
* **Withdraw:** 0.2% of withdrawal amount
* **Harvest:** 5% of harvested amount

</details>

<details>

<summary>Leverage Strategies</summary>

* **Add Leverage:** 0.2% of added collateral
* **Remove Leverage:** 0.2% of removed collateral
* **Leverage Adjustments:** 0.2% of adjusted position
* **Debt Refinancing:** 0.2% of the newly created position
* **Asset Switching:** 0.2% of the new asset amount
* **Debt Switching:** 0.2% of the new debt amount
* **Debt Repayments:** 0%
* **Liquidation Fees:** 0%

</details>