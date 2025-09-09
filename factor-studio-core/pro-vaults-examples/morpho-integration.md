# Morpho Integration Examples

This document covers the Morpho integration examples in the Factor Studio Pro Vaults system. These examples demonstrate how to integrate with Morpho's lending protocol for supply, borrow, collateral management, and reward operations.

## Overview

Morpho integration allows vaults to interact with Morpho's lending protocol for sophisticated lending and borrowing operations. The integration provides access to Morpho's markets and enables advanced lending strategies with collateral management and reward claiming.

## Example Files

### Core Integration Examples
- **00-add-market.ts**: Add Morpho market to vault configuration
- **01-supply-collateral.ts**: Supply collateral to Morpho markets
- **01-supply-collateral-all.ts**: Supply all available collateral
- **02-withdraw-collateral.ts**: Withdraw collateral from Morpho markets
- **02-withdraw-collateral-all.ts**: Withdraw all collateral
- **02-withdraw-collateral-%.ts**: Withdraw percentage of collateral

### Lending Operations
- **03-borrow.ts**: Borrow assets from Morpho markets
- **04-supply.ts**: Supply assets to Morpho markets
- **04-supply-all.ts**: Supply all available assets
- **05-withdraw.ts**: Withdraw supplied assets
- **05-withdraw-all.ts**: Withdraw all supplied assets

### Debt Management
- **06-repay.ts**: Repay borrowed assets
- **06-repay-all.ts**: Repay all borrowed assets

### Reward Management
- **07-claim-rewards.ts**: Claim rewards from Morpho markets

## Key Components

### 1. Morpho Adapter

The Morpho adapter provides the interface for interacting with Morpho markets:

```typescript
const sb = new StrategyBuilder({
  chainId: ChainId.BASE,
  isProAdapter: true,
  environment: 'testing'
});

// Access Morpho adapter
const morphoAdapter = sb.adapter.morpho;
```

### 2. Market Configuration

Morpho markets are identified by unique market IDs:

```typescript
// Example market ID for Base network
const MARKET_ID = '0x8793cf302b8ffd655ab97bd1c695dbd967807e8367a65cb2f4edaf1380ba1bda';
```

## Market Operations

### 1. Adding Markets

#### Add Market to Vault
```typescript
// Add Morpho market to vault configuration
const addMarketData = sb.adapter.morpho.addMarketToAssetAndDebt({
  marketId: MARKET_ID
});

const executeData = proVault.executeByManager([addMarketData]);
await client.sendTransaction({ ...executeData });
```

### 2. Collateral Management

#### Supply Collateral
```typescript
// Supply specific amount of collateral
const supplyCollateralData = sb.adapter.morpho.supplyCollateralBN({
  marketId: MARKET_ID,
  amountBN: parseUnits('0.1', 18).toString() // 0.1 tokens
});

const executeData = proVault.executeByManager([supplyCollateralData]);
await client.sendTransaction({ ...executeData });
```

#### Supply All Collateral
```typescript
// Supply all available collateral
const supplyAllCollateralData = sb.adapter.morpho.supplyCollateralAll({
  marketId: MARKET_ID
});

const executeData = proVault.executeByManager([supplyAllCollateralData]);
await client.sendTransaction({ ...executeData });
```

#### Withdraw Collateral
```typescript
// Withdraw specific amount of collateral
const withdrawCollateralData = sb.adapter.morpho.withdrawCollateralBN({
  marketId: MARKET_ID,
  amountBN: parseUnits('0.05', 18).toString() // 0.05 tokens
});

const executeData = proVault.executeByManager([withdrawCollateralData]);
await client.sendTransaction({ ...executeData });
```

#### Withdraw All Collateral
```typescript
// Withdraw all collateral
const withdrawAllCollateralData = sb.adapter.morpho.withdrawCollateralAll({
  marketId: MARKET_ID
});

const executeData = proVault.executeByManager([withdrawAllCollateralData]);
await client.sendTransaction({ ...executeData });
```

#### Withdraw Percentage of Collateral
```typescript
// Withdraw percentage of collateral
const withdrawCollateralPercentData = sb.adapter.morpho.withdrawCollateralPercent({
  marketId: MARKET_ID,
  percentBN: parseUnits('50', 18).toString() // 50%
});

const executeData = proVault.executeByManager([withdrawCollateralPercentData]);
await client.sendTransaction({ ...executeData });
```

### 3. Lending Operations

#### Supply Assets
```typescript
// Supply specific amount of assets
const supplyData = sb.adapter.morpho.supplyBN({
  marketId: MARKET_ID,
  amountBN: parseUnits('100', 6).toString() // 100 tokens
});

const executeData = proVault.executeByManager([supplyData]);
await client.sendTransaction({ ...executeData });
```

#### Supply All Assets
```typescript
// Supply all available assets
const supplyAllData = sb.adapter.morpho.supplyAll({
  marketId: MARKET_ID
});

const executeData = proVault.executeByManager([supplyAllData]);
await client.sendTransaction({ ...executeData });
```

#### Withdraw Assets
```typescript
// Withdraw specific amount of supplied assets
const withdrawData = sb.adapter.morpho.withdrawBN({
  marketId: MARKET_ID,
  amountBN: parseUnits('50', 6).toString() // 50 tokens
});

const executeData = proVault.executeByManager([withdrawData]);
await client.sendTransaction({ ...executeData });
```

#### Withdraw All Assets
```typescript
// Withdraw all supplied assets
const withdrawAllData = sb.adapter.morpho.withdrawAll({
  marketId: MARKET_ID
});

const executeData = proVault.executeByManager([withdrawAllData]);
await client.sendTransaction({ ...executeData });
```

### 4. Borrowing Operations

#### Borrow Assets
```typescript
// Borrow specific amount of assets
const borrowData = sb.adapter.morpho.borrowBN({
  marketId: MARKET_ID,
  amountBN: parseUnits('25', 6).toString() // 25 tokens
});

const executeData = proVault.executeByManager([borrowData]);
await client.sendTransaction({ ...executeData });
```

### 5. Debt Management

#### Repay Borrowed Assets
```typescript
// Repay specific amount of borrowed assets
const repayData = sb.adapter.morpho.repayBN({
  marketId: MARKET_ID,
  amountBN: parseUnits('10', 6).toString() // 10 tokens
});

const executeData = proVault.executeByManager([repayData]);
await client.sendTransaction({ ...executeData });
```

#### Repay All Borrowed Assets
```typescript
// Repay all borrowed assets
const repayAllData = sb.adapter.morpho.repayAll({
  marketId: MARKET_ID
});

const executeData = proVault.executeByManager([repayAllData]);
await client.sendTransaction({ ...executeData });
```

## Reward Management

### 1. Get Available Rewards

```typescript
// Get available rewards for claiming
const availableRewards = await sb.adapter.morpho.getAvailableRewards(
  vaultAddress as Address,
  alchemyApiKey,
  'https://ipfs.io'
);

console.log('Available rewards:', JSON.stringify(availableRewards, null, 2));
```

### 2. Claim Rewards

```typescript
// Claim rewards from Morpho markets
let claimTransactions: SendTransactionParams[] = [];

for (const reward of availableRewards) {
  for (const token of Object.keys(reward.proofs)) {
    const claimable = reward.proofs[token].amount;
    const proof = reward.proofs[token].proof;
    
    console.log('Claiming...', token, claimable, proof);
    
    claimTransactions.push(
      sb.adapter.morpho.claim({
        reward: token,
        claimable,
        proof
      })
    );
  }
}

// Execute all claim transactions
const executeData = proVault.executeByManager(claimTransactions);
await client.sendTransaction({ ...executeData });
```

## Advanced Strategies

### 1. Leverage Strategy

```typescript
// Leverage strategy using Morpho
const leverageStrategy = [
  // 1. Supply collateral
  sb.adapter.morpho.supplyCollateralBN({
    marketId: MARKET_ID,
    amountBN: collateralAmount.toString()
  }),
  
  // 2. Borrow against collateral
  sb.adapter.morpho.borrowBN({
    marketId: MARKET_ID,
    amountBN: borrowAmount.toString()
  }),
  
  // 3. Use borrowed funds for additional investments
  sb.adapter.uniswap.exactInputSingleAll({
    tokenInAddress: borrowedToken,
    tokenOutAddress: investmentToken,
    amountInBN: borrowAmount.toString()
  })
];

const executeData = proVault.executeByManager(leverageStrategy);
await client.sendTransaction({ ...executeData });
```

### 2. Yield Farming Strategy

```typescript
// Yield farming strategy with Morpho
const yieldStrategy = [
  // 1. Supply assets to earn interest
  sb.adapter.morpho.supplyBN({
    marketId: MARKET_ID,
    amountBN: supplyAmount.toString()
  }),
  
  // 2. Supply collateral for additional yield
  sb.adapter.morpho.supplyCollateralBN({
    marketId: MARKET_ID,
    amountBN: collateralAmount.toString()
  }),
  
  // 3. Claim rewards periodically
  ...claimRewardTransactions
];

const executeData = proVault.executeByManager(yieldStrategy);
await client.sendTransaction({ ...executeData });
```

### 3. Risk Management Strategy

```typescript
// Risk management strategy
const riskManagementStrategy = [
  // 1. Check health factor
  // 2. If health factor is low, repay some debt
  sb.adapter.morpho.repayBN({
    marketId: MARKET_ID,
    amountBN: repayAmount.toString()
  }),
  
  // 3. Or withdraw some collateral
  sb.adapter.morpho.withdrawCollateralBN({
    marketId: MARKET_ID,
    amountBN: withdrawAmount.toString()
  })
];

const executeData = proVault.executeByManager(riskManagementStrategy);
await client.sendTransaction({ ...executeData });
```

## Best Practices

### 1. Market Selection
- Choose markets with good liquidity
- Consider supply and borrow rates
- Monitor market health
- Diversify across multiple markets

### 2. Risk Management
- Monitor health factors regularly
- Set appropriate collateral ratios
- Implement stop-loss mechanisms
- Regular rebalancing

### 3. Gas Optimization
- Batch operations when possible
- Use efficient routing
- Consider gas costs
- Optimize transaction timing

### 4. Reward Optimization
- Claim rewards regularly
- Monitor reward rates
- Optimize reward claiming frequency
- Consider gas costs vs rewards

## Network Support

### Supported Networks
- **Base**: Full support
- **Arbitrum**: Full support 
- **Optimism**: Full support (coming soon)
- **Berachain**: Full support (coming soon)
- **Sonic**: Full support (coming soon)

### Market IDs
Market IDs are unique identifiers for each Morpho market. Common market IDs for Base network:

```typescript
// Example market IDs (these are examples, use actual market IDs)
const USDC_MARKET = '0x8793cf302b8ffd655ab97bd1c695dbd967807e8367a65cb2f4edaf1380ba1bda';
const WETH_MARKET = '0x...'; // Replace with actual market ID
const USDB_MARKET = '0x...'; // Replace with actual market ID
```
## Resources

- [Morpho Documentation](https://docs.morpho.org/)
- [Morpho Markets](https://app.morpho.org/)
