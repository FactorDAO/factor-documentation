# Factor Studio Pro Vaults Examples

This directory contains comprehensive examples demonstrating how to use the Factor Studio Pro Vaults system. These examples cover everything from basic vault deployment to advanced strategy execution and management.

## Overview

Factor Studio Pro Vaults are public strategies that anyone can deposit into and withdraw from. They provide a sophisticated framework for building and managing DeFi strategies with advanced features like:

- **Public Access**: Anyone can deposit and withdraw
- **Manager Execution**: Only designated managers can execute strategies
- **Owner Controls**: Vault owners can modify configurations
- **Fee Management**: Configurable deposit, withdrawal, performance, and management fees
- **Risk Management**: Built-in risk controls and validation
- **Multi-Asset Support**: Support for multiple assets and debt positions

## Example Categories

### 1. Environment Setup and Discovery
- **00-check-environment.ts**: Check adapter status and environment configuration
- **00-get-all-vaults.ts**: Discover all deployed vaults and owned vaults

### 2. Vault Deployment
- **01-deploy-vault-v0.ts** through **01-deploy-vault-v9.ts**: Various vault deployment configurations
- **02-get-vault.ts**: Retrieve comprehensive vault information

### 3. Basic Operations
- **03-deposit-usdc.ts**: Deposit USDC into a vault
- **03-deposit-weth.ts**: Deposit WETH into a vault
- **04-shares.ts**: Check share balances and calculations
- **05-withdraw.ts**: Withdraw assets from a vault
- **06-balances.ts**: Check vault and user balances
- **07-deposits.ts**: View deposit history
- **08-withdrawals.ts**: View withdrawal history

### 4. Strategy Management
- **09-add-manager.ts**: Add new managers to a vault
- **10-execute.ts**: Execute strategies using manager privileges
- **11-executions.ts**: View execution history
- **12-add-deposit-strategy.ts**: Add deposit strategies
- **12-add-deposit-strategy-v2.ts**: Add deposit strategies (v2)
- **13-deposit-execute.ts**: Deposit and execute in one transaction
- **14-add-public-strategy.ts**: Add public strategies
- **15-execute-public-strategy.ts**: Execute public strategies

### 5. Boost and Rewards
- **16-add-boost-whitelist.ts**: Add addresses to boost whitelist
- **17-add-boost-funds.ts**: Add funds to boost rewards
- **18-redeem-boost.ts**: Redeem boost rewards
- **19-get-rewards-data.ts**: Get comprehensive rewards data
- **30-get-whitelisted-bribe.ts**: Get whitelisted bribe information
- **33-get-boosted-vaults.ts**: Get boosted vaults
- **36-get-bribe-rewards.ts**: Get bribe rewards

### 6. Governance and Management
- **20-owner-vaults.ts**: Get vaults owned by an address
- **21-get-vote-summary.ts**: Get voting summary
- **22-enable-whistelist.ts**: Enable whitelist functionality
- **23-get-fee-collected.ts**: Get collected fees
- **39-charge-performance-fee.ts**: Charge performance fees
- **46-simulate-charge-fee.ts**: Simulate fee charging

### 7. Strategy Validation and Testing
- **24-validate-strategy.ts**: Validate strategy configuration
- **24-validate-strategy-static.ts**: Static strategy validation
- **25-adapters-and-tokens.ts**: Get adapters and token information
- **26-estimate-withdraw.ts**: Estimate withdrawal amounts
- **27-raw-withdraw.ts**: Raw withdrawal operations
- **28-simulate-pro-vault.ts**: Simulate vault operations
- **29-get-all-vaults-with-metrics.ts**: Get all vaults with metrics
- **31-execute-swap.ts**: Execute swap operations
- **32-simulate-pro-deposit.ts**: Simulate deposit operations
- **37-get-single-vault-metrics.ts**: Get single vault metrics
- **38-get-token-transfers.ts**: Get token transfer history
- **40-add-asset.ts**: Add new assets to vault
- **41-remove-asset.ts**: Remove assets from vault
- **42-filter-cached-vaults.ts**: Filter cached vault data

### 8. Liquidity Provision Strategies
- **34-uniswap-lp.ts**: Uniswap V3 liquidity provision
- **35-camleot-lp.ts**: Camelot liquidity provision

### 9. Analytics and Monitoring
- **37-get-single-vault-metrics.ts**: Get detailed vault metrics
- **38-get-token-transfers.ts**: Get token transfer history
- **45-get-holders.ts**: Get vault token holders

### 10. Compound Protocol Integration
- **compound/**: Specialized examples for Compound V3 integration
  - **00-deploy-vault.ts**: Deploy vault with Compound integration
  - **01-add-market-asset.ts**: Add market assets
  - **01-add-market-debt.ts**: Add market debt
  - **01-add-market-ua.ts**: Add market underlying assets
  - **02-borrow-usdc.ts**: Borrow USDC from Compound
  - **03-supply-all-weth.ts**: Supply all WETH to Compound
  - **04-supply-all-usdc.ts**: Supply all USDC to Compound
  - **05-withdraw-all-usdc.ts**: Withdraw all USDC from Compound
  - **06-get-user-info.ts**: Get user information from Compound
  - **07-claim-rewards.ts**: Claim rewards from Compound

## Key Concepts

### Vault Types
1. **Public Vaults**: Anyone can deposit and withdraw
2. **Private Vaults**: Only whitelisted addresses can interact
3. **Manager Vaults**: Only designated managers can execute strategies

### Adapter Types
1. **Manager Adapters**: Can execute strategies
2. **Owner Adapters**: Can modify vault configuration
3. **Withdraw Adapters**: Can process withdrawals

### Asset Types
1. **Deposit Assets**: Assets that can be deposited
2. **Withdraw Assets**: Assets that can be withdrawn
3. **Underlying Assets**: Assets held by the vault
4. **Debt Assets**: Borrowed assets

### Fee Structure
1. **Deposit Fee**: Fee charged on deposits
2. **Withdrawal Fee**: Fee charged on withdrawals
3. **Performance Fee**: Fee charged on profits
4. **Management Fee**: Ongoing management fee

## Usage Patterns

### 1. Vault Deployment Pattern
```typescript
// 1. Configure deployment parameters
const config = getDeploymentConfig();

// 2. Deploy vault using factory
const factory = new StudioProFactory({ chainId, environment });
const txData = factory.deployVault(config);

// 3. Execute deployment
const hash = await client.sendTransaction(txData);
const receipt = await client.waitForTransactionReceipt({ hash });
```

### 2. Strategy Execution Pattern
```typescript
// 1. Create strategy builder
const sb = new StrategyBuilder({ chainId, isProAdapter: true });

// 2. Encode strategy
const strategyData = sb.adapter.uniswap.exactInputSingleAll({
  tokenInAddress: usdc.address,
  tokenOutAddress: weth.address
});

// 3. Execute via vault
const vault = new StudioProVault({ chainId, vaultAddress });
const executeData = vault.executeByManager([strategyData]);
await client.sendTransaction(executeData);
```

### 3. Asset Management Pattern
```typescript
// 1. Check balances
const balances = await vault.getBalances();

// 2. Deposit assets
const depositData = vault.depositAsset({
  assetAddress: usdc.address,
  amountBN: amount.toString(),
  receiverAddress: userAddress
});

// 3. Withdraw assets
const withdrawData = vault.withdrawAsset({
  assetAddress: usdc.address,
  amountBN: amount.toString(),
  receiverAddress: userAddress
});
```

## Best Practices

### 1. Security
- Always validate strategy configurations before deployment
- Use proper access controls for managers and owners
- Implement risk management parameters
- Test strategies thoroughly before mainnet deployment

### 2. Gas Optimization
- Batch operations when possible
- Use appropriate fee structures
- Optimize strategy execution order
- Consider gas costs in strategy design

### 3. User Experience
- Provide clear deposit/withdrawal interfaces
- Implement proper error handling
- Use consistent fee structures
- Provide comprehensive analytics

### 4. Monitoring
- Track vault performance metrics
- Monitor execution history
- Analyze user behavior
- Implement alerting for critical events

## Environment Setup

### Required Environment Variables
```bash
PRIVATE_KEY=0x...          # Private key for transactions
ALCHEMY_API_KEY=...        # Alchemy API key for RPC
PRO_VAULT_ADDRESS=0x...    # Vault address for testing
```

### Network Configuration
- **Chain ID**: 42161 (Arbitrum One)
- **Environment**: testing/production
- **RPC URL**: https://arb-mainnet.g.alchemy.com/v2/{API_KEY}

## Testing Strategy

### 1. Local Testing
- Use testing environment
- Deploy test vaults
- Execute test strategies
- Validate results

### 2. Simulation
- Use simulation tools
- Test with different market conditions
- Validate risk parameters
- Check gas usage

### 3. Production Deployment
- Deploy to production environment
- Monitor initial performance
- Adjust parameters as needed
- Scale operations

## Common Use Cases

### 1. Yield Farming
- Deploy vault with yield farming strategy
- Users deposit assets
- Manager executes yield farming
- Users withdraw with rewards

### 2. Liquidity Provision
- Deploy vault with LP strategy
- Users deposit multiple assets
- Manager provides liquidity
- Users withdraw with fees

### 3. Leveraged Trading
- Deploy vault with leverage strategy
- Users deposit collateral
- Manager opens leveraged positions
- Users withdraw with profits

### 4. Arbitrage
- Deploy vault with arbitrage strategy
- Users deposit assets
- Manager executes arbitrage
- Users withdraw with profits

## Troubleshooting

### Common Issues
1. **Insufficient Allowance**: Ensure proper token approvals
2. **Invalid Strategy**: Validate strategy configuration
3. **Gas Estimation**: Check gas limits and prices
4. **Access Control**: Verify manager/owner permissions

### Debug Tools
- Use simulation tools for testing
- Check transaction receipts
- Monitor vault events
- Analyze execution logs

## Contributing

When adding new examples:
1. Follow the naming convention
2. Include comprehensive comments
3. Test thoroughly
4. Document any special requirements
5. Update this README

## Resources

- [Factor Documentation](https://docs.factor.fi)
