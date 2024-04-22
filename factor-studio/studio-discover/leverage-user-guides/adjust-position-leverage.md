# Adjust Position Leverage

## Introduction

You can easily adjust the amount of leverage for your position via the position management dashboard. This enables you to either:

* **Increase leverage:** Gain greater exposure to the <mark style="color:green;">asset</mark> token if you believe the value of the <mark style="color:green;">asset</mark> token to <mark style="color:red;">debt</mark> token will increase.
* **Decrease leverage:** Decrease the likelihood of liquidation if you still want to maintain leveraged exposure to <mark style="color:green;">asset</mark> token but believe the value of the <mark style="color:green;">asset</mark> token to <mark style="color:red;">debt</mark> token will decrease in the short term.

With the Factor dApp,  you can adjust your position's leverage in just 2 clicks!

## Change Your Position's Leverage

### Step 1: Navigate to the target position

You can access your position via the [Factor Discover](https://app.factor.fi/discover) overview. For easier access, you can also filter the page by the "My Vaults" quick filter to view your active positions.

<figure><img src="../../../.gitbook/assets/Discover_Leverage_ViewExisting.png" alt=""><figcaption><p>Discover overview</p></figcaption></figure>

Upon clicking the "Manage Position" button, you can then select the target position. Note that the following page displays all the positions created for a particular strategy.

<figure><img src="../../../.gitbook/assets/Discover_Leverage_AdjustSelectPosition.png" alt=""><figcaption><p>Select a position</p></figcaption></figure>

### Step 2: Select the new leverage amount

Once on the position management dashboard, you can then select the "Change Leverage" tab to bring up the leverage picker.&#x20;

<figure><img src="../../../.gitbook/assets/Discover_Leverage_ChangeLeverage.png" alt=""><figcaption><p>Select the new leverage amount</p></figcaption></figure>

The leverage slider will be loaded with the position's current leverage multiplier. By using the slider, you can adjust the position's leverage and also view the projected position metrics in real time.

### Step 3: Confirm leverage adjustment

With a new leverage multiplier selected, you can execute the changes by selecting the "Change Leverage" button. This will require a signature via the connected wallet as Factor updates the position's configurations and executes the multi-step process on the underlying protocols.

### Step 4: View new collateral amount

<figure><img src="../../../.gitbook/assets/Discover_Leverage_ChangeLeverageSuccess.png" alt=""><figcaption><p>Update position metrics</p></figcaption></figure>

Once the collateral addition has been executed, notice that the position's key metrics have been adjusted according to the new leverage multiplier selected:&#x20;

* **Net Value:** No changes as no collateral was added or removed.
* **Collateral Value:** Increases by the value of the additional leverage multiplier selected multiplied by the initial <mark style="color:green;">asset</mark> provided.
* **Debt Value:** Increases by the additional value of debt required to achieve the increased leveraged multiplier.
* **Health Factor:** Decreases as the collateral value decreases relative to debt value (i.e. more leveraged position).
* **Liquidation Price:** For this long position, the liquidation price increases as the position's leverage increases.
