# Security

## Overview

As a platform that enables the permissionless creation, sharing, and management of DeFi strategies in a pseudonymous environment, there are multiple facets when it comes to security. In addition to technical security (i.e. expected and secure execution of intended code), there is also the need to account for the economic security of any token deposited into public strategies.

While all [Factor Studio](broken-reference) vaults are non-custodial, there is still an element of trust required when a Strategy Manager is provided the reigns to manage deposits of meaningful value. Put simply, although Managers don't directly own the deposited tokens, they can still trade against their own depositors by utilizing the value of the deposits.

{% hint style="info" %}
**Exit Strategy**

Factor Discover also enables Depositors to permissionlessly withdraw from any strategy at anytime via an Exit Strategy.

Visit our [Exit Strategy explainer](exit-strategy.md) to see how Factor Studio strategies can maximize returns while ensuring truely permissionless withdrawals.
{% endhint %}

## Security Measures

{% hint style="success" %}
All Factor contracts are audited by Peckshield/Sourcehat with additional real-time monitoring provided by Chainalysis.&#x20;

Visit our [security section](../../security/security.md) for more info.
{% endhint %}

To protect Depositors from malicious Strategy Managers while still allowing Managers the strategy flexibility, Factor Studio requires Managers to set constraints on their own strategies. These constraints can then be viewed by Depositors prior to depositing.

All constraints are enforced on-chain which provides even greater security guarantees as the parameters are checked during execution itself. These constraints are fixed with the initial deployment of the public strategy.

The list of constraints are provided below:

<table><thead><tr><th width="240">Constraints</th><th>Purpose</th></tr></thead><tbody><tr><td>Upgradeable Vaults</td><td>Determines if the vault logic is immutable or can be upgraded in the future.</td></tr><tr><td>Upgrade Timelock</td><td>Vault upgrades can only be implemented after the timeout period has passed. Provides time for Depositors to remove liquidity.</td></tr><tr><td>Token Whitelist</td><td>Only allows the strategy to handle whitelisted tokens thereby blocking the transfer of value to potentially suspicious or unexpected tokens.</td></tr><tr><td>Adapter Whitelist</td><td>The adapter enables seamless transfer of liquidity between protocols. By requiring an adapter whitelist, this limits any strategy executed on the vault to only use the protocols which have been whitelisted at deployment.</td></tr><tr><td>24H Price Deviation Limit</td><td>Blocks strategy execution by the Manager if it results in the vault value going below the cumulative 24H limit.</td></tr><tr><td>Max Debt Ratio</td><td>Blocks strategy execution by the Manager if it results in the vault's asset:debt ratio falling below the specified limit.</td></tr><tr><td>Withdraw Cooldown</td><td>Sets a time limit between deposit and withdrawal to protect the vault from short term liquidity and malicious flash loan attacks.</td></tr><tr><td>Vault TVL Cap</td><td>Sets a USD maximum cap above which no further deposits are allowed. This allows Managers to manage the capital efficiency of their vault relative to market opportunities. Additionally, protects against any large volume attacks.</td></tr></tbody></table>

All these safety constraints are configured by the Manager on Studio when making the strategy public. View the [Manager user guides](../../factor-discover/factor-discover/public-strategies-user-guides/) for more information on the end-to-end Public Strategy creation flow.
