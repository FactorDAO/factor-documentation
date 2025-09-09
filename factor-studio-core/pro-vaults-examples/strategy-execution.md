# Strategy Execution Examples

This document covers the strategy execution examples in the Factor Studio Pro Vaults system. These examples demonstrate how to execute various DeFi strategies using the vault's manager privileges.

## Overview

Strategy execution in Factor Studio Pro involves using the `StrategyBuilder` to encode complex DeFi operations and executing them through the vault's manager system. Only designated managers can execute strategies, providing security and control over vault operations.

## Example Files

### Core Execution Examples
- **10-execute.ts**: Basic strategy execution
- **15-execute-public-strategy.ts**: Public strategy execution
- **31-execute-swap.ts**: Swap execution
- **34-uniswap-lp.ts**: Uniswap V3 liquidity provision
- **35-camleot-lp.ts**: Camelot liquidity provision

### Strategy Management
- **12-add-deposit-strategy.ts**: Add deposit strategies
- **12-add-deposit-strategy-v2.ts**: Add deposit strategies (v2)
- **14-add-public-strategy.ts**: Add public strategies
- **13-deposit-execute.ts**: Deposit and execute in one transaction

## Key Components

### 1. Strategy Builder

The `StrategyBuilder` is the core component for encoding strategies:

```typescript
const sbEncoder = new StrategyBuilder({
  chainId: ChainId.ARBITRUM_ONE,
  isProAdapter: true,
  environment: 'testing'
});
```

### 2. Strategy Execution

Strategies are executed through the vault's manager system:

```typescript
const proVault = new StudioProVault({
  chainId,
  vaultAddress: vaultAddress as Address
});

const executeData = proVault.executeByManager([strategyData]);
const tx = await client.sendTransaction({ ...executeData });
```

## Strategy Types

### 1. Swap Strategies

#### Uniswap V2/V3 Swaps
```typescript
// Exact input single swap
const swapData = sbEncoder.adapter.uniswap.exactInputSingleAll({
  tokenInAddress: usdc.address,
  tokenOutAddress: weth.address
});

// Exact output single swap
const swapData = sbEncoder.adapter.uniswap.exactOutputSingleAll({
  tokenInAddress: usdc.address,
  tokenOutAddress: weth.address,
  amountOutBN: amount.toString()
});
```

#### OpenOcean Swaps
```typescript
const swapData = sbEncoder.adapter.openocean.swap({
  tokenInAddress: usdc.address,
  tokenOutAddress: weth.address,
  amountInBN: amount.toString()
});
```

### 2. Lending Strategies

#### Aave Lending
```typescript
// Supply assets to Aave
const supplyData = sbEncoder.adapter.aave.supplyBN({
  assetAddress: weth,
  amountBN: amount.toString()
});

// Borrow assets from Aave
const borrowData = sbEncoder.adapter.aave.borrowBN({
  debtAddress: usdc,
  amountBN: amount.toString()
});

// Repay borrowed assets
const repayData = sbEncoder.adapter.aave.repayBN({
  debtAddress: usdc,
  amountBN: amount.toString()
});
```

#### Compound V3 Lending
```typescript
// Supply to Compound V3
const supplyData = sbEncoder.adapter.compoundV3.supplyBN({
  assetAddress: weth,
  amountBN: amount.toString()
});

// Borrow from Compound V3
const borrowData = sbEncoder.adapter.compoundV3.borrowBN({
  debtAddress: usdc,
  amountBN: amount.toString()
});
```

### 3. Liquidity Provision Strategies

#### Uniswap V3 LP
```typescript
// Create LP position
const createPositionData = sbEncoder.adapter.uniswapV3Lp.createPosition({
  token0: {
    tokenAddress: weth.address as Address,
    amountBN: amountInWeth.toString(),
    amountMinBN: 0
  },
  token1: {
    tokenAddress: usdc.address as Address,
    amountBN: amountInUSDC.toString(),
    amountMinBN: 0
  },
  fee: 3000,
  tickLower: -199800,
  tickUpper: -198060
});

// Increase liquidity
const increaseLiquidityData = sbEncoder.adapter.uniswapV3Lp.increaseLiquidity({
  tokenId: positionId,
  amount0BN: amount0.toString(),
  amount1BN: amount1.toString()
});

// Decrease liquidity
const decreaseLiquidityData = sbEncoder.adapter.uniswapV3Lp.decreaseLiquidity({
  tokenId: positionId,
  liquidityBN: liquidity.toString()
});
```

#### Camelot LP
```typescript
// Add liquidity to Camelot
const addLiquidityData = sbEncoder.adapter.camelot.addLiquidity({
  tokenA: weth.address,
  tokenB: usdc.address,
  amountADesiredBN: amountA.toString(),
  amountBDesiredBN: amountB.toString()
});
```

### 4. Yield Farming Strategies

#### Pendle Yield Farming
```typescript
// Supply to Pendle
const supplyData = sbEncoder.adapter.pendle.supplyBN({
  assetAddress: wsteth,
  amountBN: amount.toString()
});

// Claim rewards
const claimData = sbEncoder.adapter.pendle.claimRewards({
  assetAddress: wsteth
});
```

#### Silo Yield Farming
```typescript
// Supply to Silo
const supplyData = sbEncoder.adapter.silo.supplyBN({
  assetAddress: weth,
  amountBN: amount.toString()
});
```

### 5. Flash Loan Strategies

#### Balancer Flash Loans
```typescript
const flashLoanData = sbEncoder.adapter.flashloanBalancer.flashLoan({
  assetAddress: usdc,
  amountBN: amount.toString(),
  callbackData: callbackData
});
```

## Execution Patterns

### 1. Single Strategy Execution

```typescript
// Encode single strategy
const strategyData = sbEncoder.adapter.uniswap.exactInputSingleAll({
  tokenInAddress: usdc.address,
  tokenOutAddress: weth.address
});

// Execute strategy
const executeData = proVault.executeByManager([strategyData]);
await client.sendTransaction(executeData);
```

### 2. Multi-Strategy Execution

```typescript
// Encode multiple strategies
const strategies = [
  sbEncoder.adapter.aave.supplyBN({
    assetAddress: weth,
    amountBN: amount.toString()
  }),
  sbEncoder.adapter.uniswap.exactInputSingleAll({
    tokenInAddress: usdc.address,
    tokenOutAddress: weth.address
  })
];

// Execute multiple strategies
const executeData = proVault.executeByManager(strategies);
await client.sendTransaction(executeData);
```

### 3. Conditional Strategy Execution

```typescript
// Check conditions before execution
const vaultBalance = await proVault.getBalance();
if (vaultBalance > minimumBalance) {
  const strategyData = sbEncoder.adapter.uniswap.exactInputSingleAll({
    tokenInAddress: usdc.address,
    tokenOutAddress: weth.address
  });
  
  const executeData = proVault.executeByManager([strategyData]);
  await client.sendTransaction(executeData);
}
```

## Strategy Validation

### 1. Pre-execution Validation

```typescript
// Validate strategy before execution
const isValid = await proVault.validateStrategy(strategyData);
if (!isValid) {
  throw new Error('Invalid strategy');
}
```

### 2. Simulation

```typescript
// Simulate strategy execution
const simulationResult = await sb.simulateWithOverrides(
  executeData.data,
  funds,
  vaultAddress as Address
);
```

## Best Practices

### 1. Strategy Design
- Keep strategies simple and focused
- Use appropriate slippage protection
- Implement proper error handling
- Consider gas optimization

### 2. Risk Management
- Validate inputs before execution
- Use appropriate amounts
- Implement stop-loss mechanisms
- Monitor execution results

### 3. Gas Optimization
- Batch operations when possible
- Use efficient routing
- Optimize transaction size
- Consider gas price fluctuations

### 4. Security
- Validate all inputs
- Use proper access controls
- Implement emergency stops
- Monitor for suspicious activity

## Common Issues and Solutions

### 1. Insufficient Liquidity
- Check available liquidity
- Use alternative routes
- Implement fallback strategies
- Monitor market conditions

### 2. Slippage Issues
- Set appropriate slippage tolerance
- Use limit orders when possible
- Monitor price movements
- Implement dynamic slippage

### 3. Gas Estimation
- Check gas limits
- Optimize transaction size
- Use gas estimation tools
- Consider gas price optimization

### 4. Execution Failures
- Check strategy validity
- Verify adapter addresses
- Validate asset configurations
- Review error messages

## Monitoring and Analytics

### 1. Execution Monitoring
- Track execution success rates
- Monitor gas usage
- Analyze performance metrics
- Check for errors

### 2. Performance Analytics
- Measure strategy performance
- Track profit/loss
- Analyze risk metrics
- Compare with benchmarks

### 3. User Analytics
- Monitor user interactions
- Track deposit/withdrawal patterns
- Analyze user behavior
- Optimize user experience

## Testing and Validation

### 1. Unit Testing
- Test individual strategies
- Validate encoding/decoding
- Check error handling
- Verify calculations

### 2. Integration Testing
- Test with real vaults
- Validate execution flows
- Check adapter interactions
- Verify results

### 3. Simulation Testing
- Use simulation tools
- Test with different market conditions
- Validate risk parameters
- Check edge cases

## Resources

- [Strategy Builder API](./api-reference.md#strategy-builder)
- [Adapter Documentation](./adapter-documentation.md)
- [Vault Management Guide](./vault-management.md)
- [Risk Management Guide](./risk-management.md)
