# Public Strategy Creation

{% hint style="info" %}
**Strategy Canvas**

All Factor Studio strategies will be created via the same canvas. This guide focuses on the creation of public strategies.&#x20;

If you want to create a private strategy, you can view the [Private Strategy Creation user guide](../../studio/user-guide/private-strategy-creation.md).
{% endhint %}

## Step 1: Mix-and-match Strategies

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Kickstart your strategy creation journey by visiting [Studio](https://studio.factor.fi/) and selecting:

* **Building Blocks:** Select various DeFi building blocks from the Block Picker to add them to the canvas.
* **Templates:** Jumpstart your strategy creation with our preset templates which you can extend upon.

## Step 2: Configure Strategy Parameters

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Upon selecting a block, you will see 2 tabs on your canvas:

* **Main strategy:** This is the strategy that will be executed by the strategy manager.
* **Exit strategy:** This enables the vault to automatically withdraw utilized funds in case the vault balance is insufficient to cover the Depositor requested withdrawal amount.

The "Main strategy" tab will be automatically populated with your selected block. You can expand each block to set their corresponding parameters.

Upon finalizing the params, you can click on the canvas to close the block and view the Strategy Details on the right.

{% hint style="warning" %}
**Exit Strategy**

It is highly recommended that you configure an Exit Strategy as anyone can deposit into your public vault. This ensures that Depositors are always able to withdraw their own funds without intervention from the strategy manager.

View our [Exit Strategy guide](create-an-exit-strategy.md) for more details.
{% endhint %}

## Step 3: Test Your Strategy

<figure><img src="../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

To ensure your strategy executes as intended, you can test your strategy. This will simulate the execution of your strategy and provide you with the corresponding results.

You can view any execution errors by following the notification to the Tenderly logs.

## Step 4: Configure Deployment

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once your strategy has passed the test, you can deploy your strategy vault by clicking the "Configure Deployment" button at the bottom of the page.&#x20;

As this is a public strategy, you will just need to **use the "Deploy only"** option as deposits will be received via Discover.

This is an on-chain transaction which deploys your strategy vault for you. The strategy vault will manage the strategy funds and execution.

## Step 5: Make Your Strategy Public

All strategies will be initially deployed as Private strategies which can then be converted into Public strategies. This allows for any modifications and internal testing prior to public deposits.

View the [Making Your Strategy Public](making-your-strategy-public.md) guide once you're ready to launch your strategy.
