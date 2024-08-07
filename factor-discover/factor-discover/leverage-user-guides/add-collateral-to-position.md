# Add Collateral To Position

## Introduction

You can easily add collateral to your leveraged position via the position management dashboard. By adding more collateral to the position, you are ensuring that the position does not become undercollateralized and therefore reduces the position's liquidation risks.&#x20;

{% hint style="info" %}
**Position Leverage Multiplier**

Note that the adding of collateral only increases the position's collateral amount. Consequently, the position's leverage multiplier is reduced accordingly with the position's [Health Factor](../../../getting-started/glossary.md#health-factor) also seeing a corresponding increase.
{% endhint %}

{% hint style="success" %}
**Leverage Strategy Explainers**

Please refer to the [Leverage Strategy Explainer](../../../getting-started/strategy-explainers/leverage/) if you would like to understand the leverage process and how Factor streamlines the management of leveraged positions.
{% endhint %}

## Increase Your Position's Collateral

{% hint style="info" %}
**Leverage Fees**

Factor charges a small transaction-based fee that supports the development of the Factor ecosystem. 50% of the protocol's ongoing revenue is [shared with veFCTR ](../../../governance/fctr-token/faq-tokenomics.md#vefctr)holders to encourage greater community governance.

The schedule of fees can be viewed [here](../../../governance/factordao/platform-fees.md#fee-structure).
{% endhint %}

## Increase Your Position's Collateral

### Step 1: Navigate to the target position

You can access your position via your personalized [dashboard](https://app.factor.fi/strategies/dashboard).

<figure><img src="../../../.gitbook/assets/UG_Leverage_Guide_Adjust_1.png" alt=""><figcaption><p>Discover overview</p></figcaption></figure>

Upon clicking the "Expand" button, you can then select the target position. Note that the following page displays all the positions created for a particular strategy.

<figure><img src="../../../.gitbook/assets/UG_Leverage_Guide_Adjust_2.png" alt=""><figcaption><p>Select a position</p></figcaption></figure>

### Step 2: Select the amount of collateral to add

Once on the position management dashboard, you can then select the "Add Collateral" tab specify the additional amount of <mark style="color:green;">asset</mark> token to be added to the position.

<figure><img src="../../../.gitbook/assets/UG_Leverage_Add_1.png" alt=""><figcaption><p>Input the amount of additional collateral</p></figcaption></figure>

### Step 3: Approve additional collateral amount

To add additional collateral to the position, the strategy contract will require authorization to debit the <mark style="color:green;">asset</mark> token from your wallet. You will be prompted to sign an approval request if further spending allowance is required by the strategy contract.

### Step 4: Confirm the collateral addition

With an additional collateral amount selected, you can execute the changes by selecting the "Add Collateral" button. This will require a signature via the connected wallet as Factor updates the position's configurations and executes the multi-step process on the underlying protocols.

<figure><img src="../../../.gitbook/assets/UG_Leverage_Add_2.png" alt=""><figcaption><p>Add collateral to the position</p></figcaption></figure>

### Step 5: View new collateral amount

<figure><img src="../../../.gitbook/assets/UG_Leverage_Add_3.png" alt=""><figcaption><p>Updated position metrics</p></figcaption></figure>

Once the collateral addition has been executed, notice that the position's key metrics have been adjusted according to the additional <mark style="color:green;">asset</mark> token added as collateral.

* **Net Value:** Increases by the USD value of the additional collateral.
* **Collateral Value:** Increases by the USD value of the additional collateral.
* [**Health Factor**](../../../getting-started/glossary.md#health-factor)**:** Increases as the collateral value increases relative to debt value (which is unchanged).
* **Liquidation Price:** For this long position, the liquidation price decreases as the position's leverage decreases.
* **Leverage Multiplier:** Viewable on the "Change Leverage" tab, the position's leverage decreases as there are more <mark style="color:green;">asset</mark> tokens collateralizing the same amount of debt.
