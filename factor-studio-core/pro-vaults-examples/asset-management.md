# Asset Management Examples

This document covers the asset management examples in the Factor Studio Pro Vaults system. These examples demonstrate how to manage assets within vaults, including deposits, withdrawals, and balance tracking.

## Overview

Asset management in Factor Studio Pro involves handling user deposits, withdrawals, and maintaining accurate balance tracking. The system supports multiple assets, flexible deposit/withdrawal configurations, and comprehensive balance management.

## Example Files

### Basic Operations
- **03-deposit-usdc.ts**: Deposit USDC into a vault
- **03-deposit-weth.ts**: Deposit WETH into a vault
- **05-withdraw.ts**: Withdraw assets from a vault
- **04-shares.ts**: Check share balances and calculations
- **06-balances.ts**: Check vault and user balances

### Advanced Operations
- **26-estimate-withdraw.ts**: Estimate withdrawal amounts
- **27-raw-withdraw.ts**: Raw withdrawal operations
- **32-simulate-pro-deposit.ts**: Simulate deposit operations
- **40-add-asset.ts**: Add new assets to vault
- **41-remove-asset.ts**: Remove assets from vault

### History and Analytics
- **07-deposits.ts**: View deposit history
- **08-withdrawals.ts**: View withdrawal history
- **38-get-token-transfers.ts**: Get token transfer history

## Key Components

### 1. Studio Pro Vault

The main interface for asset management:

```typescript
const proVault = new StudioProVault({
  chainId: ChainId.ARBITRUM_ONE,
  vaultAddress: vaultAddress as Address
});
```

### 2. Token List Integration

Using the Factor token list for asset management:

```typescript
const tokenlist = new FactorTokenlist(ChainId.ARBITRUM_ONE);
const usdc = tokenlist.getTokenFromSymbol('USDC');
const weth = tokenlist.getTokenFromSymbol('WETH');
```

## Asset Operations

### 1. Deposits

#### Basic Deposit
```typescript
// Get deposit amount
const depositAmountBN = ethers.utils.parseUnits('0.05', 6); // 0.05 USDC

// Preview deposit
const depositEstimate = await proVault.previewDeposit({
  assetAddress: usdc.address as Address,
  assetAmountBN: depositAmountBN.toString()
});

// Create deposit transaction
const depositData = proVault.depositAsset({
  assetAddress: usdc.address as Address,
  amountBN: depositAmountBN.toString(),
  receiverAddress: account.address
});

// Execute deposit
const tx = await client.sendTransaction({ ...depositData });
```

#### Deposit with Approval
```typescript
// Check allowance
const checkAllowance = await client.readContract({
  address: usdc.address as Address,
  abi: erc20ABI,
  functionName: 'allowance',
  args: [account.address, vaultAddress as Address]
});

// Approve if needed
if (checkAllowance < valueToBigInt(depositAmountBN.toString())) {
  const allowance = await client.writeContract({
    address: usdc.address as Address,
    abi: erc20ABI,
    functionName: 'approve',
    args: [
      vaultAddress as Address,
      valueToBigInt(depositAmountBN.toString())
    ]
  });
  
  await client.waitForTransactionReceipt({ hash: allowance });
}

// Execute deposit
const tx = await client.sendTransaction({ ...depositData });
```

### 2. Withdrawals

#### Basic Withdrawal
```typescript
// Create withdrawal transaction
const withdrawData = proVault.withdrawAsset({
  assetAddress: usdc.address as Address,
  amountBN: withdrawAmount.toString(),
  receiverAddress: account.address
});

// Execute withdrawal
const tx = await client.sendTransaction({ ...withdrawData });
```

#### Withdrawal Estimation
```typescript
// Estimate withdrawal
const withdrawEstimate = await proVault.previewWithdraw({
  assetAddress: usdc.address as Address,
  assetAmountBN: withdrawAmount.toString()
});

console.log('Estimated shares to burn:', withdrawEstimate.sharesToBurn);
console.log('Estimated assets to receive:', withdrawEstimate.assetsToReceive);
```

### 3. Balance Management

#### Vault Balances
```typescript
// Get total vault balance
const totalBalance = await proVault.getTotalBalance();

// Get balance for specific asset
const assetBalance = await proVault.getAssetBalance(usdc.address as Address);

// Get all asset balances
const allBalances = await proVault.getAllAssetBalances();
```

#### User Balances
```typescript
// Get user's share balance
const shareBalance = await proVault.getShareBalance(userAddress);

// Get user's asset balance
const userAssetBalance = await proVault.getUserAssetBalance(
  userAddress,
  usdc.address as Address
);

// Get user's total value
const totalValue = await proVault.getUserTotalValue(userAddress);
```

### 4. Share Management

#### Share Calculations
```typescript
// Get total supply
const totalSupply = await proVault.getTotalSupply();

// Get share price
const sharePrice = await proVault.getSharePrice();

// Calculate shares for deposit
const sharesForDeposit = await proVault.calculateSharesForDeposit({
  assetAddress: usdc.address as Address,
  assetAmountBN: depositAmount.toString()
});

// Calculate assets for withdrawal
const assetsForWithdrawal = await proVault.calculateAssetsForWithdrawal({
  assetAddress: usdc.address as Address,
  sharesBN: sharesToBurn.toString()
});
```

## Asset Configuration

### 1. Adding Assets

```typescript
// Add new asset to vault
const addAssetData = proVault.addAsset({
  assetAddress: newAssetAddress,
  accountingAddress: accountingAdapterAddress,
  isDepositAsset: true,
  isWithdrawAsset: false
});

await client.sendTransaction({ ...addAssetData });
```

### 2. Removing Assets

```typescript
// Remove asset from vault
const removeAssetData = proVault.removeAsset({
  assetAddress: assetToRemove
});

await client.sendTransaction({ ...removeAssetData });
```

### 3. Asset Validation

```typescript
// Check if asset is supported
const isDepositAsset = await proVault.isDepositAsset(assetAddress);
const isWithdrawAsset = await proVault.isWithdrawAsset(assetAddress);
const isUnderlyingAsset = await proVault.isUnderlyingAsset(assetAddress);
```

## History and Analytics

### 1. Transaction History

#### Deposit History
```typescript
const proVaultStats = new StudioProVaultStats({
  chainId,
  vaultAddress: vaultAddress as Address
});

// Get deposit history
const deposits = await proVaultStats.getDeposits();
console.log('Total deposits:', deposits.length);

for (const deposit of deposits) {
  console.log('Deposit:', {
    user: deposit.user,
    asset: deposit.asset,
    amount: deposit.amount,
    shares: deposit.shares,
    timestamp: deposit.timestamp
  });
}
```

#### Withdrawal History
```typescript
// Get withdrawal history
const withdrawals = await proVaultStats.getWithdrawals();
console.log('Total withdrawals:', withdrawals.length);

for (const withdrawal of withdrawals) {
  console.log('Withdrawal:', {
    user: withdrawal.user,
    asset: withdrawal.asset,
    amount: withdrawal.amount,
    shares: withdrawal.shares,
    timestamp: withdrawal.timestamp
  });
}
```

### 2. Token Transfers

```typescript
// Get token transfer history
const transfers = await proVaultStats.getTokenTransfers();
console.log('Total transfers:', transfers.length);

for (const transfer of transfers) {
  console.log('Transfer:', {
    from: transfer.from,
    to: transfer.to,
    amount: transfer.amount,
    token: transfer.token,
    timestamp: transfer.timestamp
  });
}
```

### 3. User Analytics

```typescript
// Get user's transaction history
const userDeposits = await proVaultStats.getUserDeposits(userAddress);
const userWithdrawals = await proVaultStats.getUserWithdrawals(userAddress);

// Calculate user's total deposited/withdrawn
const totalDeposited = userDeposits.reduce((sum, deposit) => 
  sum + parseFloat(deposit.amount), 0
);
const totalWithdrawn = userWithdrawals.reduce((sum, withdrawal) => 
  sum + parseFloat(withdrawal.amount), 0
);
```

## Simulation and Testing

### 1. Deposit Simulation

```typescript
// Simulate deposit operation
const simulationResult = await proVault.simulateDeposit({
  assetAddress: usdc.address as Address,
  assetAmountBN: depositAmount.toString(),
  userAddress: account.address
});

console.log('Simulation result:', {
  sharesToMint: simulationResult.sharesToMint,
  feeAmount: simulationResult.feeAmount,
  netAmount: simulationResult.netAmount
});
```

### 2. Withdrawal Simulation

```typescript
// Simulate withdrawal operation
const simulationResult = await proVault.simulateWithdrawal({
  assetAddress: usdc.address as Address,
  sharesBN: sharesToBurn.toString(),
  userAddress: account.address
});

console.log('Simulation result:', {
  assetsToReceive: simulationResult.assetsToReceive,
  feeAmount: simulationResult.feeAmount,
  netAmount: simulationResult.netAmount
});
```

## Best Practices

### 1. Asset Management
- Always check allowances before deposits
- Use appropriate slippage protection
- Validate asset addresses
- Monitor balance changes

### 2. User Experience
- Provide clear deposit/withdrawal interfaces
- Show estimated amounts before transactions
- Implement proper error handling
- Use consistent fee structures

### 3. Security
- Validate all inputs
- Check asset permissions
- Implement proper access controls
- Monitor for suspicious activity

### 4. Performance
- Batch operations when possible
- Optimize gas usage
- Use efficient data structures
- Cache frequently accessed data

## Common Issues and Solutions

### 1. Insufficient Allowance
```typescript
// Check and approve allowance
const allowance = await client.readContract({
  address: assetAddress,
  abi: erc20ABI,
  functionName: 'allowance',
  args: [userAddress, vaultAddress]
});

if (allowance < requiredAmount) {
  await client.writeContract({
    address: assetAddress,
    abi: erc20ABI,
    functionName: 'approve',
    args: [vaultAddress, requiredAmount]
  });
}
```

### 2. Insufficient Balance
```typescript
// Check user balance
const balance = await client.readContract({
  address: assetAddress,
  abi: erc20ABI,
  functionName: 'balanceOf',
  args: [userAddress]
});

if (balance < depositAmount) {
  throw new Error('Insufficient balance');
}
```

### 3. Invalid Asset
```typescript
// Validate asset before operations
const isDepositAsset = await proVault.isDepositAsset(assetAddress);
if (!isDepositAsset) {
  throw new Error('Asset not supported for deposits');
}
```

### 4. Slippage Protection
```typescript
// Use slippage protection for withdrawals
const withdrawData = proVault.withdrawAsset({
  assetAddress: usdc.address as Address,
  amountBN: withdrawAmount.toString(),
  receiverAddress: account.address,
  minAmountBN: minAmount.toString() // Slippage protection
});
```

## Monitoring and Analytics

### 1. Real-time Monitoring
- Track deposit/withdrawal volumes
- Monitor user activity
- Check balance changes
- Analyze fee collection

### 2. Performance Metrics
- Calculate APY/APR
- Track total value locked (TVL)
- Monitor user retention
- Analyze growth patterns

### 3. Risk Monitoring
- Monitor large transactions
- Check for unusual patterns
- Validate asset ratios
- Track liquidity levels

## Resources

- [Studio Pro Vault API](./api-reference.md#studio-pro-vault)
- [Asset Configuration Guide](./asset-configuration.md)
- [Fee Management Guide](./fee-management.md)
- [Analytics and Monitoring](./analytics-monitoring.md)
