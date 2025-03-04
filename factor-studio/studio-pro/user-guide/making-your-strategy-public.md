# Making Your Strategy Public

## Overview

Studio Pro enables any strategy to be made public with ease via an intuitive helper. All Studio created strategies will be initially deployed as Private strategies which can then be converted into Public strategies. This allows for any modifications and internal testing prior to public deposits.

## Public Strategies For All

### Step 1:  Open the helper

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

The public strategy helper can be accessed via clicking on the "Private" button on the top right of the Strategy Canvas.

This will kikcstart your strategy publishing process.

### Step 2: Vault Info

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

You will first have to give your strategy a publicly viewable name and symbol.

* **Vault Name:** This is the name of your strategy which will be displayed to Depositors. You should use a name which will help Depositors identify and contextualize your vault.
* **Vault Symbol:** A string of up to 6 characters that uniquely identifies your vault.

### Step 3: Security Info

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

The security configurations specifies certain operational limitations that help safeguard your Depositor's funds:

* **Vault Owner:** The address of the strategy manager (who has the ability to execute the strategy).
* **Upgradeable Strategies:** Uncheck this option if the "Main strategy" for the vault will not be changed in the future.
* **Upgrade Timelock:** The duration of time since the last strategy upgrade before the strategy can be upgraded again.
* **24H Price Deviation Limit:** Blocks the execution of any strategy that would result in the strategy TVL deviating by more than the specified percentage.
* **Max Debt Ratio:** Blocks the execution of any strategy that would result in the total value of all strategy debt being higher than the specified percentage of strategy assets.

### Step 4: Vault Configurations

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

The vault configurations limits Depositor actions:

* **Depositor Whitelist:** Addresses which can deposit into the strategy. Leave this empty if you are not restricting who can deposit into your strategy.
* **Withdraw Cooldown:** By specifying a cooldown, this limits the negative impact of short term liquidity on your strategy (which includes potential flash loan attacks).
* **Vault TVL Cap:** The USD value of the vault TVL after which no further deposits will be allowed.
* **Primary Strategy (**_**coming soon**_**):** Toggle this to allow the Depositor to execute the specified strategy or limit strategy execution to just the manager.

### Step 5: Fees Configuration

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

The fees configuration allows you to specify the different types of fees which will be incurred by Depositors of your strategy:

* **Deposit Fee:** Charged at the point of deposit based on the deposit amount.
* **Withdrawal Fee:** Charged at the point of withdrawal based on the withdrawal amount.
* **Management Fee:** An annual fee that is manually triggered by the Strategy Manager (together with performance fee collection). Fee amount is calculated based on the fees accrued since last fee collection execution.
* **Performance Fee:** A fee that is charged based on the strategy profit whenever strategy TVL hits an all time high. Manually triggered by the Strategy Manager (together with management fee collection).&#x20;

{% hint style="info" %}
**Claiming of Management & Performance Fees**

Both Management & Performance fees will require manual claiming by the Manager. While this functionality is available at the contract level, Factor is working towards enabling this via the UI.

The fees collected are determined when the Manager triggers the claim and is dependent on the vault's liquidity at that point in time.
{% endhint %}

{% hint style="info" %}
**Factor Platform Fees**

To fund the continued platform operations for publicly created strategies, Factor charges a 20% platform fee on any fees collected by the Strategy Manager.

These fees accrue to the [FactorDAO Protocol Rewards](../../../governance/factordao/factordao-multisig-addresses.md) address.
{% endhint %}

### Step 6: Integrations Configuration

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

The integrations page allows you to specify what tokens your strategy can interact with.&#x20;

* **Denominator:** The token against which the strategy value will be baselined.
* **Strategy Asset Tokens:** The allowable list of tokens that can be held as assets by the strategy.

{% hint style="info" %}
**Asset Tokens**

Please note that if you strategy is lending the tokens to vairious money markets (e.g. Aave, Compound, Silo), you will also need to add the relevant liquidity tokens that represent token supply on such protocols (e.g. aArbWETH, cWETHv3, sWETH-Silo).
{% endhint %}

* **Strategy Debt Tokens:** The allowable list of debt tokens that can be held by the strategy. Each lending protocol has a different token representing debt which must be added to enable borrows against said protocol.
* **Deposit Tokens:** The list of tokens that can be deposited into the strategy.
* **Withdrawal Tokens:** The list of tokens that are returned on withdrawal.
* **Incentive Tokens:** Whitelist of tokens that can be distributed as incentives via [Factor Boost](../../../governance/factor-boost/).

{% hint style="info" %}
**Price Baseline**

The price baseline configuration pulls live pricing data from the selected oracle. This price is used in various strategy calculations such as strategy TVL as well as strategy safeguards.
{% endhint %}

### Step 7: Review Your Strategy

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

You will be able to review your strategy summary on the final page.

Once you're happy with all the configurations, you can proceed to publish your strategy by checking the box and selecting the publishing button. This is an multi-step on-chain tx that requires gas.

### Step 8: Share Your Strategy

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

That's it! Your strategy is now public and can be accessed directly via Discover.&#x20;

You strategy will always be accessible via the link above. To reach a wider audience, your strategy will be automatically listed on Discover if it meets the criteria below:

{% hint style="info" %}
**Community Curated Strategies**

To safeguard users and highlight only the most relevant user created strategies, [Factor Discover](broken-reference) only lists strategies which meet any of the following criteria:

* Strategy TVL ≥USD 10,000
* Strategy receives ≥10,000 [veFCTR](../../../governance/fctr-token/#vefctr) votes via [Factor Scale](../../../governance/factor-scale/)
* Strategy holds ≥10,000 [FCTR](../../../governance/fctr-token/#fctr)
{% endhint %}
