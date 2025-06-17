# Private Strategy Creation

{% hint style="info" %}
**Strategy Canvas**

All Factor Studio strategies will be created via the same canvas. This guide focuses on the creation of private strategies.

If you want to create a public strategy, you can view the [Public Strategy Creation user guide](../../studio-pro/user-guide/public-strategy-creation.md).
{% endhint %}

## Step 1: Mix-and-match Strategies

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Kickstart your strategy creation journey by visiting [Studio](https://studio.factor.fi/) and selecting:

* **Building Blocks:** Select various DeFi building blocks from the Block Picker to add them to the canvas.
* **Templates:** Jumpstart your strategy creation with our preset templates which you can extend upon.

## Step 2: Configure Strategy Parameters

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

You can then set the parameters for each block in the canvas.

Upon finalizing the params, you can click on the canvas to close the block and view the Strategy Details on the right.

## Step 3: Test Your Strategy

<figure><img src="../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

To ensure your strategy executes as intended, you can test your strategy. This will simulate the execution of your strategy and provide you with the corresponding results.

## Step 4: Configure Deployment

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once your strategy has passed the test, you can deploy your strategy vault by clicking the "Configure Deployment" button at the bottom of the page.&#x20;

This is an on-chain transaction which deploys your strategy vault for you. The strategy vault will manage the strategy funds and execution.

## Step 5: Fund Your Strategy

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Upon deploying your strategy, you will be able to view the contract address under the Strategy Details.

You can then proceed to fund your strategy with the required strategy tokens.

## Step 6: Execute Your Strategy

<figure><img src="../../../.gitbook/assets/image (7) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once all the tests have passed and you are happy with your strategy, you can execute your strategy with a single click in the top right.
