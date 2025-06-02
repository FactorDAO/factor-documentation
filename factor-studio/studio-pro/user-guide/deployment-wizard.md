# Deployment WIzard

## Overview

Studio Pro comes equipped with a deployment wizard that simplifies strategy configuration. As anyone can create any strategy with Factor Studio, the deployment wizard allows easy configuration of:

* Strategy Metadata: Name, description, logo, symbol, etc.
* Vault Security: Contract upgradeability, withdraw cooldowns, timelocks, etc.
* Fees: Fee amounts and receiver.
* Deposit Safeguards: Price deviaiton limits, max debt ratio, TVL caps, etc.
* Integrations: Tokens, protocols, markets, etc.

## Public Strategies For All

### Step 1:  Open the wizard

<figure><img src="../../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

The public strategy helper can be accessed via clicking on the "Deploy" button on the top right of the Strategy Canvas.

This will kickstart your strategy publishing process.

### Step 2: Vault Info

<figure><img src="../../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

You will first have to give your strategy publicly viewable data that will make your strategy easily identifiable and understandable:

* **Vault Name:** This is the name of your strategy which will be displayed to Depositors. You should use a name which will help Depositors identify and contextualize your vault.
* **Vault Symbol:** A string that uniquely identifies your vault. Duplicate vault symbols are allowed but it is recommended to make your vault symbol unique to allow easy identification by Depositors.
* **Vault Logo:** A `png` graphic file which will be displayed on your vault's Discover page.
* **Vault Description:** A short description of the strategy that helps Depositors understand where is the yield coming from.

### Step 3: Security Info

<figure><img src="../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

The security configurations specifies certain operational limitations that help safeguard your Depositor's funds:

* **Vault Owner:** The address of the strategy manager (who has the ability to execute the strategy). This is automatically set to the connected wallet.
* **Denominator:** The token against which the strategy value will be baselined.

{% hint style="info" %}
**Price Baseline**

The price baseline configuration pulls live pricing data from the selected oracle. This price is used in various strategy calculations such as strategy TVL as well as strategy safeguards.
{% endhint %}

* **Upgradeable Vault:** Check this option if you want to upgrade the vault configurations in the future.
* **Upgrade Timelock:** The duration of time since the last vault upgrade before the strategy can be upgraded again.
* **Withdraw Cooldown:** By specifying a cooldown, this limits the negative impact of short term liquidity on your strategy (which includes potential flash loan attacks).

### Step 4: Fees Configuration

<figure><img src="../../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

The fees configuration allows you to specify the different types of fees which will be incurred by Depositors of your strategy:

* **Deposit Fee:** Charged at the point of deposit based on the deposit amount.
* **Withdrawal Fee:** Charged at the point of withdrawal based on the withdrawal amount.
* **Management Fee:** An annual fee that is manually triggered by the Strategy Manager (together with performance fee collection). Fee amount is calculated based on the fees accrued since last fee collection execution.
* **Performance Fee:** A fee that is charged based on the strategy profit whenever strategy TVL hits an all time high. Manually triggered by the Strategy Manager (together with management fee collection).&#x20;
* **Fee Receiver Address:** The address that will receive the fees. The fee receiver can be different from the vault owner.

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

### Step 5: Deposit Safeguards

<figure><img src="../../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

The deposit safeguards provides configurable limits that protects vault deposits:

* **24H Price Deviation Limit:** Blocks the execution of any strategy that would result in the strategy TVL deviating by more than the specified percentage.
* **Max Debt Ratio:** Blocks the execution of any strategy that would result in the total value of all strategy debt being higher than the specified percentage of strategy assets.
* **Vault TVL Cap:** The USD value of the vault TVL after which no further deposits will be allowed.
* **Executable Vault:** Whether the vault's "main strategy" can be executed when a Depositor triggers a deposit.
* **Public Strategy:** Allows anyone to deposit into the strategy if toggled on. If not, you can whitelist allowed depositor addresses.

### Step 6: Integrations Configuration

<figure><img src="../../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

The integrations page allows you to specify what tokens, protocols, and markets your strategy can interact with.&#x20;

* **Scale Multichain Whitelist:** Allows [Factor Scale](../../../governance/factor-scale/) emission rewards to be distributed to your vault depositors.
* **Close Debt:** If the protocol is supported, it enables Depositor's to trigger liquidation of utilized tokens in underlying protocols for the purpose of immediate withdrawals.
* **Exit Swap All:** Allows Depositor's to swap all the vault's underlying tokens into their selected Withdrawal Token when withdrawing.
* **Strategy Asset Tokens:** The allowable list of tokens that can be handled as assets by the strategy. You will need to include every token that is utilized in the strategy.

{% hint style="info" %}
**Asset Tokens (Aave)**

Please note that if you strategy is lending tokens Aave, you will also need to add the relevant liquidity tokens that represent token supply on such protocols (e.g. aArbWETH, aBasUSDC, etc.). This is because protocols like Aave issue lending receipt tokens that represents deposits.
{% endhint %}

* **Strategy Debt Tokens:** The allowable list of debt tokens that can be held by the strategy. Each lending protocol has a different token representing debt which must be added to enable borrows against said protocol.

{% hint style="info" %}
**Debt Tokens (Aave)**

Borrowing from Aave requires that the derived debt token (i.e. variableDebtToken) is whitelisted as a debt token. This is because Aave issues borrow receipt tokens that represents debt borrowed.
{% endhint %}

* **Deposit Tokens:** The list of tokens that can be deposited into the strategy. You will need to include the denominator token as part of the [ERC4626](https://docs.openzeppelin.com/contracts/4.x/erc4626) specification for smart contract vaults.
* **Withdrawal Tokens:** The list of tokens that are returned on withdrawal. You will need to include the denominator token as part of the [ERC4626](https://docs.openzeppelin.com/contracts/4.x/erc4626) specification for smart contract vaults.

{% hint style="success" %}
**Deposit/Withdrawal Tokens On Discover**

Factor allows Managers to select which tokens can be selected by Depositors via Discover. This sidesteps the ERC4626 limitations by introducing additional controls on the Factor UI but users can still interact directly with the underlying vault contract.

![](<../../../.gitbook/assets/image (71).png>)
{% endhint %}

* **Incentive Tokens:** Whitelist of tokens that can be distributed as incentives via [Factor Boost](../../../governance/factor-boost/).
* **Protocol Markets:** The markets which can be used by this strategy.

{% hint style="info" %}
**Lending Markets (Compound)**

If you're lending/borrowing from Compound markets, you will need to whitelist the underlying markets by selecting the asset and debt being used on each market. Compound tracks user balances internally hence whitelisting is done at the market level.
{% endhint %}

### Step 7: Review Your Strategy

<figure><img src="../../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Upon completing the wizard, you will be able to view a summary of your strategy.

Once you're happy with all the configurations, you can proceed to publish your strategy by clicking the "Deploy" button. This is an multi-step on-chain tx that requires gas.

### Step 8: Share Your Strategy

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

That's it! Your strategy is now public and can be accessed directly via Discover.&#x20;

You strategy will always be accessible via the link above. To reach a wider audience, your strategy will be automatically listed on Discover if it meets the criteria below:

{% hint style="info" %}
**Community Curated Strategies**

To safeguard users and highlight only the most relevant user created strategies, [Factor Discover](broken-reference) only lists strategies which meet any of the following criteria:

* Strategy TVL ≥USD 10,000
* Strategy receives ≥10,000 [veFCTR](../../../governance/fctr-token/#vefctr) votes via [Factor Scale](../../../governance/factor-scale/)
* Strategy holds ≥10,000 [FCTR](../../../governance/fctr-token/#fctr)
{% endhint %}
