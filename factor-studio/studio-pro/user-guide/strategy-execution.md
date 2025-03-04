# Strategy Execution

## Overview

Strategy execution allows the Strategy Manager to allocate all deposited funds towards the specified strategy. A vault will always consist of two balances:

* **Active Balance:** The amount of liquidity that have been allocated to the strategy (i.e. deposited on various DeFi protocols.
* **Idle Balance:** The tokens that are sitting in the vault contract. All deposits are initially held by the vault contract.

Strategy managers can affect the aforementioned balances based on their strategy execution.

## Executing Your Strategy

### Step 1: Check Strategy Balances&#x20;

{% hint style="info" %}
**Temporary Workaround**

Factor will be implementing balance checks on Studio Pro soon and DeBank usage will only be temporary. We have prioritized the core functions and are consistently striving to make UX improvements whenever possible.
{% endhint %}

You can view the balances for your strategy on DeBank. A link will also be provided via the Studio Pro interface.

### Step 2: Update Strategy Amounts

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Update the amounts to be used during execution based on the balances in Step 1.

{% hint style="info" %}
**Strategy Amounts**

As Studio Pro matures, more convenient percentage selectors will be implemented to enable automated calculation of exact amounts per strategy execution.&#x20;

Currently, Strategy Managers are required to manually input the corresponding amounts based on strategy deposits.
{% endhint %}

### Step 3: Execute The Strategy

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Once you've checked all the amounts, executing the strategy is as easy as clicking the "Execute" button and signing the tx.
