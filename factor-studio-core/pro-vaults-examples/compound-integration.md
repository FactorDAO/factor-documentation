# Compound V3 Integration Examples

This document covers the Compound V3 integration examples in the Factor Studio Pro Vaults system. These examples demonstrate how to integrate with Compound V3 for lending and borrowing operations.

## Overview

Compound V3 integration allows vaults to interact with Compound's lending protocol for supply, borrow, and reward operations. The integration provides access to Compound's markets and enables sophisticated lending strategies.

## Example Files

### Core Integration Examples
- **00-deploy-vault.ts**: Deploy vault with Compound V3 integration
- **01-add-market-asset.ts**: Add market assets to vault
- **01-add-market-debt.ts**: Add market debt to vault
- **01-add-market-ua.ts**: Add market underlying assets to vault

### Operations
- **02-borrow-usdc.ts**: Borrow USDC from Compound
- **03-supply-all-weth.ts**: Supply all WETH to Compound
- **04-supply-all-usdc.ts**: Supply all USDC to Compound
- **05-withdraw-all-usdc.ts**: Withdraw all USDC from Compound

### Analytics
- **06-get-user-info.ts**: Get user information from Compound
- **07-claim-rewards.ts**: Claim rewards from Compound

## Key Components

### 1. Compound V3 Adapter

The Compound V3 adapter provides the interface for interacting with Compound markets:

```typescript
const sb = new StrategyBuilder({
  chainId: ChainId.ARBITRUM_ONE,
  isProAdapter: true,
  environment: 'testing'
});

// Access Compound V3 adapter
const compoundAdapter = sb.adapter.compoundV3;
```

### 2. Market Configuration

Compound V3 markets need to be configured with specific parameters:

```typescript
// Market addresses for Arbitrum
const USDC_MARKET = '0x9c4ec768c28520B50860ea7a15bd7213a9fF58bf';
const WETH_MARKET = '0x9c4ec768c28520B50860ea7a15bd7213a9fF58bf';

// Asset addresses
const USDC = '0xaf88d065e77c8cc2239327c5edb3a432268e5831';
const WETH = '0x82af49447d8a07e3bd95bd0d56f35241523fbab1';
```

## Market Operations

### 1. Adding Market Assets

#### Add Market Asset
```typescript
// Add market asset to vault
const addMarketAssetData = proVault.addMarketAsset({
  marketAddress: USDC_MARKET,
  assetAddress: USDC,
  accountingAddress: compoundAccountingAdapter
});

await client.sendTransaction({ ...addMarketAssetData });
```

#### Add Market Debt
```typescript
// Add market debt to vault
const addMarketDebtData = proVault.addMarketDebt({
  marketAddress: USDC_MARKET,
  debtAddress: USDC,
  accountingAddress: compoundAccountingAdapter
});

await client.sendTransaction({ ...addMarketDebtData });
```

#### Add Market Underlying Asset
```typescript
// Add market underlying asset to vault
const addMarketUAData = proVault.addMarketUA({
  marketAddress: USDC_MARKET,
  underlyingAssetAddress: USDC,
  accountingAddress: compoundAccountingAdapter
});

await client.sendTransaction({ ...addMarketUAData });
```

### 2. Supply Operations

#### Supply WETH to Compound
```typescript
// Get WETH balance
const wethBalance = await client.readContract({
  address: WETH,
  abi: erc20ABI,
  functionName: 'balanceOf',
  args: [vaultAddress]
});

// Supply all WETH to Compound
const supplyData = sb.adapter.compoundV3.supplyBN({
  marketAddress: WETH_MARKET,
  assetAddress: WETH,
  amountBN: wethBalance.toString()
});

const executeData = proVault.executeByManager([supplyData]);
await client.sendTransaction({ ...executeData });
```

#### Supply USDC to Compound
```typescript
// Get USDC balance
const usdcBalance = await client.readContract({
  address: USDC,
  abi: erc20ABI,
  functionName: 'balanceOf',
  args: [vaultAddress]
});

// Supply all USDC to Compound
const supplyData = sb.adapter.compoundV3.supplyBN({
  marketAddress: USDC_MARKET,
  assetAddress: USDC,
  amountBN: usdcBalance.toString()
});

const executeData = proVault.executeByManager([supplyData]);
await client.sendTransaction({ ...executeData });
```

### 3. Borrow Operations

#### Borrow USDC from Compound
```typescript
// Borrow USDC from Compound
const borrowData = sb.adapter.compoundV3.borrowBN({
  marketAddress: USDC_MARKET,
  debtAddress: USDC,
  amountBN: borrowAmount.toString()
});

const executeData = proVault.executeByManager([borrowData]);
await client.sendTransaction({ ...executeData });
```

#### Repay USDC to Compound
```typescript
// Repay USDC to Compound
const repayData = sb.adapter.compoundV3.repayBN({
  marketAddress: USDC_MARKET,
  debtAddress: USDC,
  amountBN: repayAmount.toString()
});

const executeData = proVault.executeByManager([repayData]);
await client.sendTransaction({ ...executeData });
```

### 4. Withdrawal Operations

#### Withdraw USDC from Compound
```typescript
// Get USDC balance in Compound
const compoundBalance = await client.readContract({
  address: USDC,
  abi: erc20ABI,
  functionName: 'balanceOf',
  args: [vaultAddress]
});

// Withdraw all USDC from Compound
const withdrawData = sb.adapter.compoundV3.withdrawBN({
  marketAddress: USDC_MARKET,
  assetAddress: USDC,
  amountBN: compoundBalance.toString()
});

const executeData = proVault.executeByManager([withdrawData]);
await client.sendTransaction({ ...executeData });
```

## User Information and Analytics

### 1. Get User Information

```typescript
// Get user information from Compound
const userInfo = await proVault.getCompoundUserInfo({
  marketAddress: USDC_MARKET,
  userAddress: userAddress
});

console.log('User Info:', {
  supplyBalance: userInfo.supplyBalance,
  borrowBalance: userInfo.borrowBalance,
  collateralValue: userInfo.collateralValue,
  borrowValue: userInfo.borrowValue,
  healthFactor: userInfo.healthFactor
});
```

### 2. Market Information

```typescript
// Get market information
const marketInfo = await proVault.getCompoundMarketInfo({
  marketAddress: USDC_MARKET
});

console.log('Market Info:', {
  totalSupply: marketInfo.totalSupply,
  totalBorrow: marketInfo.totalBorrow,
  supplyRate: marketInfo.supplyRate,
  borrowRate: marketInfo.borrowRate,
  utilizationRate: marketInfo.utilizationRate
});
```

### 3. Reward Information

```typescript
// Get reward information
const rewardInfo = await proVault.getCompoundRewardInfo({
  marketAddress: USDC_MARKET,
  userAddress: userAddress
});

console.log('Reward Info:', {
  claimableRewards: rewardInfo.claimableRewards,
  rewardToken: rewardInfo.rewardToken,
  rewardRate: rewardInfo.rewardRate
});
```

## Reward Management

### 1. Claim Rewards

```typescript
// Claim rewards from Compound
const claimRewardsData = sb.adapter.compoundV3.claimRewards({
  marketAddress: USDC_MARKET
});

const executeData = proVault.executeByManager([claimRewardsData]);
await client.sendTransaction({ ...executeData });
```

### 2. Check Claimable Rewards

```typescript
// Check claimable rewards
const claimableRewards = await proVault.getClaimableRewards({
  marketAddress: USDC_MARKET,
  userAddress: userAddress
});

console.log('Claimable Rewards:', claimableRewards);
```

## Advanced Strategies

### 1. Leverage Strategy

```typescript
// Leverage strategy using Compound
const leverageStrategy = [
  // 1. Supply collateral
  sb.adapter.compoundV3.supplyBN({
    marketAddress: WETH_MARKET,
    assetAddress: WETH,
    amountBN: collateralAmount.toString()
  }),
  
  // 2. Borrow against collateral
  sb.adapter.compoundV3.borrowBN({
    marketAddress: USDC_MARKET,
    debtAddress: USDC,
    amountBN: borrowAmount.toString()
  }),
  
  // 3. Swap borrowed USDC for more WETH
  sb.adapter.uniswap.exactInputSingleAll({
    tokenInAddress: USDC,
    tokenOutAddress: WETH,
    amountInBN: borrowAmount.toString()
  }),
  
  // 4. Supply additional WETH
  sb.adapter.compoundV3.supplyBN({
    marketAddress: WETH_MARKET,
    assetAddress: WETH,
    amountBN: additionalAmount.toString()
  })
];

const executeData = proVault.executeByManager(leverageStrategy);
await client.sendTransaction({ ...executeData });
```

### 2. Yield Farming Strategy

```typescript
// Yield farming strategy
const yieldStrategy = [
  // 1. Supply assets to Compound
  sb.adapter.compoundV3.supplyBN({
    marketAddress: USDC_MARKET,
    assetAddress: USDC,
    amountBN: supplyAmount.toString()
  }),
  
  // 2. Claim rewards
  sb.adapter.compoundV3.claimRewards({
    marketAddress: USDC_MARKET
  }),
  
  // 3. Reinvest rewards
  sb.adapter.uniswap.exactInputSingleAll({
    tokenInAddress: rewardToken,
    tokenOutAddress: USDC,
    amountInBN: rewardAmount.toString()
  })
];

const executeData = proVault.executeByManager(yieldStrategy);
await client.sendTransaction({ ...executeData });
```

## Risk Management

### 1. Health Factor Monitoring

```typescript
// Monitor health factor
const healthFactor = await proVault.getHealthFactor({
  marketAddress: USDC_MARKET,
  userAddress: userAddress
});

if (healthFactor < 1.5) {
  console.warn('Health factor is low:', healthFactor);
  // Implement risk management actions
}
```

### 2. Liquidation Risk

```typescript
// Check liquidation risk
const liquidationRisk = await proVault.getLiquidationRisk({
  marketAddress: USDC_MARKET,
  userAddress: userAddress
});

if (liquidationRisk.isAtRisk) {
  console.warn('User is at liquidation risk');
  // Implement protective measures
}
```

### 3. Borrow Limit

```typescript
// Check borrow limit
const borrowLimit = await proVault.getBorrowLimit({
  marketAddress: USDC_MARKET,
  userAddress: userAddress
});

if (borrowLimit.available < requiredAmount) {
  throw new Error('Insufficient borrow capacity');
}
```

## Best Practices

### 1. Market Selection
- Choose markets with good liquidity
- Consider supply and borrow rates
- Monitor market health
- Diversify across markets

### 2. Risk Management
- Monitor health factors
- Set appropriate collateral ratios
- Implement stop-loss mechanisms
- Regular rebalancing

### 3. Gas Optimization
- Batch operations when possible
- Use efficient routing
- Consider gas costs
- Optimize transaction timing

### 4. Monitoring
- Track market conditions
- Monitor user positions
- Analyze performance
- Implement alerts

## Common Issues and Solutions

### 1. Insufficient Collateral
```typescript
// Check collateral before borrowing
const collateralValue = await proVault.getCollateralValue({
  marketAddress: USDC_MARKET,
  userAddress: userAddress
});

if (collateralValue < requiredCollateral) {
  throw new Error('Insufficient collateral');
}
```

### 2. Market Pause
```typescript
// Check if market is paused
const isPaused = await proVault.isMarketPaused({
  marketAddress: USDC_MARKET
});

if (isPaused) {
  throw new Error('Market is paused');
}
```

### 3. Borrow Limit Exceeded
```typescript
// Check borrow limit
const borrowLimit = await proVault.getBorrowLimit({
  marketAddress: USDC_MARKET,
  userAddress: userAddress
});

if (borrowLimit.used + borrowAmount > borrowLimit.max) {
  throw new Error('Borrow limit exceeded');
}
```

## Resources

- [Compound V3 Documentation](https://docs.compound.finance/)
- [Compound V3 Adapter API](./api-reference.md#compound-v3-adapter)
- [Risk Management Guide](./risk-management.md)
- [Market Analytics](./market-analytics.md)
