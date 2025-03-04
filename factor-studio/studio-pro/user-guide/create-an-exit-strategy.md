# Create An Exit Strategy

## Overview

While all Studio Pro created vaults are non-custodial, the complexity of removing funds from an active strategy might be prohibitive for Depositors. Given that anyone can deposit into public strategies created via Studio Pro, the Exit Strategy functions as a safeguard for depositors to access their funds.&#x20;

As such, while not mandatory, Factor strongly suggests that your public strategy is deployed with a proper exit strategy. This will allay any Depositor fears whenever they have a need to liquidate their holdings.

The exit strategy will be triggered whenever the vault's available balance is insufficient to cover the requested withdrawal amount.

{% hint style="info" %}
View our [Exit Strategy conceptual overview](../exit-strategy.md) for more info.
{% endhint %}

## Configuring An Exit Strategy

{% hint style="info" %}
**Main Strategy**

Please refer to the [Public Strategy Creation](public-strategy-creation.md) guide if you require a step-by-step guide to drag-and-dropping your strategy.
{% endhint %}

### Step 1: Navigate to exit strategy tab

<figure><img src="../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Once a strategy canvas has been populated with a block, you will be able to see the "Exit strategy" tab.

You can toggle between the "Main strategy" and "Exit Strategy" by clicking on the tab.

### Step 2: Create an exit strategy

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

The "Exit strategy" creation process is exactly the same as the "[Main strategy](public-strategy-creation.md)" and will generally be in the opposite direction.

Exit strategies will be tailored to the specific strategy being implemented by the vault. That is, when executed, the exit strategy removes liquidity from the active strategy for withdrawals.

The example below shows a simple borrow strategy and its corresponding exit strategy:

{% tabs %}
{% tab title="Main strategy" %}
1. Lend 100 $USDC on Aave
2. Borrow 50 $USDT
{% endtab %}

{% tab title="Exit strategy" %}
1. Flash loan $USDT debt amount from Balancer
2. Repay $USDT debt on Aave
3. Withdraw $USDC collateral
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Exit strategy amounts**

To facilitate easy withdrawal of funds, the token amounts per exit strategy will be automatically calculated based on the withdrawal amount requested by the Depositor.
{% endhint %}

### Step 3: Test your exit strategy

<figure><img src="../../../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

To ensure your strategy executes as intended, you can test your strategy. This will simulate the execution of your strategy and provide you with the corresponding results.

You can view any execution errors by following the notification to the Tenderly logs.

Once your exit strategy has passed the test, it will be deployed together with the "Main strategy".
