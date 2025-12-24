# Public Strategy Creation

## Step 1: Mix-and-match Strategies

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Kickstart your strategy creation journey by visiting [Studio](https://studio.factor.fi/) and selecting:

* [**Building Blocks**](/broken/pages/qNiXKjtPcqNVNXaG59w6)**:** Select various DeFi building blocks from the Block Picker to add them to the canvas:
  * [Swap](../../../factor-building-blocks/swap/): Instantly swap between any ERC20 token via integrated aggregators and DEXs.
  * [Lend](../../../factor-building-blocks/lend.md): Supply your token to various lending markets to earn lending interest.
  * [Borrow](../../../factor-building-blocks/borrow.md): Borrow against tokens supplied to various lending markets to get additional capital.
  * [Flash Loan](../../../factor-building-blocks/flash-loan/): Instant access to uncollateralized loans to create leverage or take advantage of short term market movements.
  * [Create LP](../../../factor-building-blocks/lp-management/): Provide liquidity to various DEXs to earn market making fees.
  * Claim Rewards: Claim accrued liquidity rewards across all the protocols used in your strategy.
* **Templates:** Jumpstart your strategy creation with our preset templates which you can extend upon.

## Step 2: Configure Strategy Parameters

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

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

## Step 3: Test Your Strategy \[WIP]

{% hint style="info" %}
**Strategy Simulation**

Factor Studio's testing environment is currently being upgraded to support gasless testing of the strategy.

You can still deploy strategies by skipping the testing stage. If you're unsure of the feasibility of your strategy, feel free to drop a message on Discord and we will be happy to help.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (5) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

To ensure your strategy executes as intended, you can test your strategy. This will simulate the execution of your strategy and provide you with the corresponding results.

You can view any execution errors by following the notification to the Tenderly logs.

## Step 4: Configure Deployment

<figure><img src="../../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

Once your strategy has passed the test, you can deploy your strategy vault by clicking the "Deploy" button at the top right of the canvas.&#x20;

As this is a public strategy, you will just need to deploy the strategy as deposits will be received via Discover.

View the [Deployment Wizard](deployment-wizard.md) guide once you're ready to launch your strategy.
