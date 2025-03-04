---
description: Supporting Permissionless Vault Withdrawals
---

# Exit Strategy

## Overview

In addition to being non-custodial, true permissionless asset management also means that Depositors should be able to withdraw any amount of their tokens at anytime. This means that Depositors should be able to unwind their vault position without requiring Strategy Manager approval nor having to incur the opportunity costs of waiting.

Instead of having to speculate on when and how much a Depositor will withdraw, Fator Studio enables Managers to specify an exit flow which can be independently executed by the Depositor. This maximizes potential vault returns while simultaneously minimizing any manual overheads and risks.

{% hint style="success" %}
**Vault Composition**

To ensure fairness for all Depositors in a vault,  it is crucial that the vault's token composition (e.g. % of asset tokens, liabilities, etc.) remains the same before and after the withdrawal.

By maintaining the vault's token ratios, this safeguards vault deposits from the action of any single Depositor. In other words, a Depositor should never trade against the vault as this will come at the expense of other Depositors.
{% endhint %}

## Approach

### Permissionless Vault Contracts

The Exit Strategy takes advantage of smart contracts whereby Depositors can also interact directly on-chain with the permissionless vault smart contracts. As long as the vault is able to validate that the caller is the owner of the shares, the Depositor should be able to trigger any action involving his share of the vault.

The delineation between vault Strategy Manager and share owner (i.e. Depositors) allows for permissionless asset management to thrive in a pseudo-anonymous environment where anyone can easily create vaults.

### Vault Specific Exit Strategy

Given that Factor Studio enables any strategy to be created, the Strategy Manager will have the best knowledge on how to unwind active capital allocated towards the strategy (e.g. closing outstanding debt, claiming rewards, token swap directions, etc.). While Depositors should DYOR before depositing, not all Depositors will have the requisite DeFi strategy knowledge to unwind the funds themselves.

For every strategy created, Strategy Managers have the option to configure an Exit Strategy which specifies the general flow required to unwind the position. Depositors are able to view if an Exit Strategy has been configured for the strategy prior to depositing. While Factor strongly recommends configuring an Exit Strategy, this decision is ultimately left to the Strategy Manager allowing them to determine the trust levels and risks specific to their strategy.

### Maintaining Vault Composition

While Strategy Managers are able to specify the exit flow, the amounts for each step can only be known at the point of withdrawal as it requires the Depositor to specify the amount of shares being withdrawn and the vault state at the point of withdrawal request.

Withdrawals via Factor Discover builds on top of the Exit Strategy configured by the Strategy Manager  to generate a withdrawal request which can be easily signed by the Depositor to be executed directly on-chain.&#x20;

The corresponding amounts for each building block in the Exit Strategy is automatically calculated based on the vault's state at the point of the withdrawal request. This includes:

{% tabs %}
{% tab title="Assets" %}
* **Idle Tokens** → Tokens which are sitting in the vault contract and not allocated to an external protocol.
* **Collateral Tokens** →  Tokens that have been deposited into lending protocols to earn supply interest. Can be used to collateralize borrows of tokens in the same market.
* **LP Tokens** → Tokens that represent liquidity locked in an AMM pool to earn market making fees.
* **Staked Tokens** → Tokens that have been deposited into various pool/staking contracts to earn yield or rewards.
* **Reward Tokens** → Tokens which have accrued as rewards for staking/locking liquidity. Requires claiming from the reward protocol.
{% endtab %}

{% tab title="Liabilities" %}
* **Debt Tokens** → Tokens which represent debt obligations to lending markets where tokens were borrowed from
{% endtab %}
{% endtabs %}

Critically, the vault’s **composition of assets and debts should not change before and after a withdraw tx**. Additionally, calculations will also take into account the slippage settings as configured by the Depositor at withdrawal.

### Handling Debt Obligations

In cases where the vault's asset:debt ratio decreases between deposit and withdrawal, there is a risk that the Strategy Manager configured Exit Strategy might be insufficient to cover any outstanding debt obligations corresponding to the shares burned.

To facilitate withdrawals in such cases, Factor Studio also provides a "Close Debt" block which a Strategy Manager can append to the end of their configured Exit Strategy. By checking the expected vault end state against the vault state after the configure Exit Strategy, the "Close Debt" block automatically loops through any remaining debt and repays the debt in full using the underlying collateral.

<details>

<summary><strong>Close Debt High Level Flow</strong></summary>

To maintain the vault's composition when triggered by the Depositor, amount calculations must take into account the vault state at 3 separate points in the process:

1. Before exit strategy → Current state of the vault
2. After Manager configured exit strategy → Expected vault state after successful execution of the Manager portion of the exit strategy
3. After exit strategy → Expected end state of vault after withdrawal

The withdrawal still has outstanding debt if the the output from 2 is insufficient to cover the debt owed in 3. To close the remaining debt, the Close Debt block abstracts the following process to facilitate safe settlement of remaining debt:

1. Loop through all remaining debt tokens
2. For each debt owed, repay the outstanding with the underlying collateral (equalized in USD terms via price oracle)
   1. Flash loan debt token
   2. Repay debt with flash loaned debt tokens
   3. Withdraw the underlying asset
   4. Swap collateral(s) to flash loaned tokens (i.e. same as debt)

The process above ensures that Depositors are still able to permissionlessly withdraw their tokens even when the Manager configured exit strategy fails is no longer applicable if the vault's asset:debt ratio decreases since deposit.

Note that as tokens have to be swapped via an external aggregator, there is also slippage risks involved which will be configured by the Depositor at the point of initiating the withdrawal tx on Discover.

</details>
