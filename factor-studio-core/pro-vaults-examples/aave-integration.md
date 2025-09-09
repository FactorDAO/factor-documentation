# Aave Integration Examples

This document covers the Aave integration examples in the Factor Studio Pro Vaults system. These examples demonstrate how to integrate with Aave's lending protocol for supply, borrow, and advanced lending strategies.

## Overview

Aave integration allows vaults to interact with Aave's lending protocol for sophisticated lending and borrowing operations. The integration provides access to Aave's markets and enables advanced lending strategies with collateral management, flash loans, and yield optimization.

## Example Files

### Core Integration Examples
- **01-deploy-vault.ts**: Deploy vault with Aave integration configuration
- **02-set-deposit-strategy.ts**: Set up deposit strategies for automatic execution
- **03-deposit-usdc-and-execute.ts**: Deposit assets and execute strategies in one transaction
- **04-withdraw-from-aave.ts**: Withdraw assets from Aave markets

## Key Components

### 1. Aave Adapter

The Aave adapter provides the interface for interacting with Aave markets:

```typescript
const sb = new StrategyBuilder({
  chainId: ChainId.BASE,
  isProAdapter: true,
  environment: 'testing'
});

// Access Aave adapter
const aaveAdapter = sb.adapter.aave;
```

### 2. Token Configuration

Aave integration requires proper token configuration including aTokens and debt tokens:

```typescript
const tokens = new FactorTokenlist(ChainId.BASE);
const weth = tokens.getTokenFromSymbol('WETH');
const usdc = tokens.getTokenFromSymbol('USDC');
const cbbtc = tokens.getTokenFromSymbol('cbBTC');
const cbeth = tokens.getTokenFromSymbol('cbETH');

// Get Aave-specific tokens
const wethAave = tokens.getDebtToken(weth.address, Protocols.AAVE) as AaveToken;
const usdcAave = tokens.getDebtToken(usdc.address, Protocols.AAVE) as AaveToken;
const cbBTCaave = tokens.getDebtToken(cbbtc.address, Protocols.AAVE) as AaveToken;
const cbethAave = tokens.getDebtToken(cbeth.address, Protocols.AAVE) as AaveToken;
```

## Vault Deployment with Aave Integration

### 1. Deployment Configuration

```typescript
async function getDeploymentConfig(): Promise<StudioProFactoryDeployVaultParams> {
  const initialDeposit = '1600'; // 1600 wei

  const {
    factor_openocean_adapter_pro,
    factor_aave_adapter_pro,
    factor_chainlink_accounting_adapter_pro,
    factor_aave_accounting_adapter_pro,
    factor_flashloan_balancer_adapter_pro,
  } = getContractAddressesForChainOrThrow(chainId, environment);

  const managerAdapters = [
    factor_aave_adapter_pro,
    factor_openocean_adapter_pro,
    factor_flashloan_balancer_adapter_pro,
  ];

  const ownerAdapters = [];
  const withdrawAdapters = [
    factor_aave_adapter_pro,
    factor_openocean_adapter_pro,
    factor_flashloan_balancer_adapter_pro,
  ];

  return {
    initialDepositBN: initialDeposit.toString(),
    name: 'Simple AAVE Lend & Borrow',
    symbol: 'TVAAVEv1',
    configParams: {
      assetDenominatorAddress: usdc.address,
      assetDenominatorAccountingAddress: factor_chainlink_accounting_adapter_pro,
      upgradeTimelockBN: ONE_DAY_IN_SECONDS * 2,
      cooldownTimeBN: ONE_SECOND,
      upgradeable: true,
      initialAssetAddresses: [
        usdc.address,
        weth.address,
        cbeth.address,
        usdcAave.aToken,
        cbethAave.aToken,
      ],
      initialDepositAssetAddresses: [usdc.address],
      initialWithdrawAssetAddresses: [usdc.address],
      initialAssetAccountingAddresses: [
        factor_chainlink_accounting_adapter_pro,
        factor_chainlink_accounting_adapter_pro,
        factor_chainlink_accounting_adapter_pro,
        factor_aave_accounting_adapter_pro,
        factor_aave_accounting_adapter_pro,
      ],
      initialDebtAddresses: [wethAave.variableDebtToken],
      initialDebtAccountingAddresses: [factor_aave_accounting_adapter_pro],
      initialManagerAdapters: managerAdapters,
      initialOwnerAdapters: ownerAdapters,
      initialWithdrawAdapters: withdrawAdapters,
      maxCapBN: MAX_UINT_256,
      maxDebtRatioBN: 1e18,
      cumulativePriceDeviationAllowanceBpsBN: 10_000,
    },
    feeParams: {
      feeReceiver,
      depositFeeBN: '0',
      withdrawFeeBN: '0',
      performanceFeeBN: '0',
      managementFeeBN: '0',
    },
  };
}
```

### 2. Strategy Validation

```typescript
const proFactory = new StudioProFactory({
  chainId,
  environment,
});

const validated = await proFactory.validateStrategy({
  managerAdapters: deploymentConfig.configParams.initialManagerAdapters as Address[],
  ownerAdapters: deploymentConfig.configParams.initialOwnerAdapters as Address[],
  withdrawAdapters: deploymentConfig.configParams.initialWithdrawAdapters as Address[],
  assetAddresses: deploymentConfig.configParams.initialAssetAddresses as Address[],
  depositAssetAddresses: deploymentConfig.configParams.initialDepositAssetAddresses as Address[],
  withdrawAssetAddresses: deploymentConfig.configParams.initialWithdrawAssetAddresses as Address[],
  assetAccountingAddresses: deploymentConfig.configParams.initialAssetAccountingAddresses as Address[],
  debtAddresses: deploymentConfig.configParams.initialDebtAddresses as Address[],
  debtAccountingAddresses: deploymentConfig.configParams.initialDebtAccountingAddresses as Address[],
});

if (!validated.isValid) {
  throw new Error('Invalid strategy configuration');
}
```

### 3. Vault Deployment

```typescript
const deploymentConfig = await getDeploymentConfig();
const proFactory = new StudioProFactory({
  chainId,
  environment,
});

// Approve factory for initial deposit
const allowance = await client.writeContract({
  address: usdc.address as Address,
  abi: erc20ABI,
  functionName: 'approve',
  args: [
    factor_studio_pro_factory as Address,
    valueToBigInt(MAX_UINT_256.toString()),
  ],
});

await client.waitForTransactionReceipt({ hash: allowance });

// Deploy vault
const txData = proFactory.deployVault(deploymentConfig);
const hash = await client.sendTransaction({
  ...txData,
  gas: 8000000n,
});

const receipt = await client.waitForTransactionReceipt({ hash });
console.log('Vault deployed at:', receipt.contractAddress);
```

## Strategy Configuration

### 1. Setting Deposit Strategies

```typescript
const sbEncoder = new StrategyBuilder({
  chainId,
  isProAdapter: true,
  environment: 'testing',
});

// Configure deposit strategy
sbEncoder.adapter.aave.supplyAll({
  assetAddress: usdc.address as Address,
});

sbEncoder.adapter.aave.borrowBN({
  debtAddress: weth.address as Address,
  amountBN: parseEther('0.00003').toString(),
});

const blocks = sbEncoder.getTransactions();
console.log('Strategy blocks:', blocks);

// Set deposit strategy
const executeData = proVault.setDepositStrategy(blocks);
await client.sendTransaction({ ...executeData });
```

### 2. Deposit and Execute Strategy

```typescript
// Deposit assets and execute strategy in one transaction
const depositAmountBN = ethers.utils.parseUnits('1.5', 6); // 1.5 USDC
const assetAddress = usdc.address as Address;
const receiverAddress = account.address;

// Preview deposit
const depositEstimate = await proVault.previewDeposit({
  assetAddress,
  assetAmountBN: depositAmountBN.toString(),
});

// Create deposit and execute transaction
const depositData = proVault.depositAssetAndExecute({
  assetAddress,
  amountBN: depositAmountBN.toString(),
  receiverAddress,
});

// Check and approve allowance
const checkAllowance = await client.readContract({
  address: usdc.address as Address,
  abi: erc20ABI,
  functionName: 'allowance',
  args: [account.address, vaultAddress as Address],
});

if (checkAllowance < valueToBigInt(depositAmountBN.toString())) {
  const allowance = await client.writeContract({
    address: assetAddress,
    abi: erc20ABI,
    functionName: 'approve',
    args: [
      vaultAddress as Address,
      valueToBigInt(depositAmountBN.toString()),
    ],
  });
  
  await client.waitForTransactionReceipt({ hash: allowance });
}

// Execute deposit and strategy
const tx = await client.sendTransaction({
  ...depositData,
  gas: 3000000,
});

const receipt = await client.waitForTransactionReceipt({ hash: tx });
```

## Aave Operations

### 1. Supply Operations

#### Supply All Assets
```typescript
// Supply all available assets to Aave
const supplyAllData = sb.adapter.aave.supplyAll({
  assetAddress: usdc.address as Address
});

const executeData = proVault.executeByManager([supplyAllData]);
await client.sendTransaction({ ...executeData });
```

#### Supply Specific Amount
```typescript
// Supply specific amount to Aave
const supplyData = sb.adapter.aave.supplyBN({
  assetAddress: usdc.address as Address,
  amountBN: parseUnits('100', 6).toString() // 100 USDC
});

const executeData = proVault.executeByManager([supplyData]);
await client.sendTransaction({ ...executeData });
```

### 2. Borrowing Operations

#### Borrow Assets
```typescript
// Borrow specific amount from Aave
const borrowData = sb.adapter.aave.borrowBN({
  debtAddress: weth.address as Address,
  amountBN: parseEther('0.1').toString() // 0.1 WETH
});

const executeData = proVault.executeByManager([borrowData]);
await client.sendTransaction({ ...executeData });
```

#### Repay Borrowed Assets
```typescript
// Repay borrowed assets
const repayData = sb.adapter.aave.repayBN({
  debtAddress: weth.address as Address,
  amountBN: parseEther('0.05').toString() // 0.05 WETH
});

const executeData = proVault.executeByManager([repayData]);
await client.sendTransaction({ ...executeData });
```

### 3. Withdrawal Operations

#### Withdraw All Assets
```typescript
// Withdraw all supplied assets from Aave
const withdrawAllData = sb.adapter.aave.withdrawAll({
  assetAddress: usdc.address as Address
});

const executeData = proVault.executeByManager([withdrawAllData]);
await client.sendTransaction({ ...executeData });
```

#### Withdraw Specific Amount
```typescript
// Withdraw specific amount from Aave
const withdrawData = sb.adapter.aave.withdrawBN({
  assetAddress: usdc.address as Address,
  amountBN: parseUnits('50', 6).toString() // 50 USDC
});

const executeData = proVault.executeByManager([withdrawData]);
await client.sendTransaction({ ...executeData });
```

## Advanced Strategies

### 1. Leverage Strategy

```typescript
// Leverage strategy using Aave
const leverageStrategy = [
  // 1. Supply collateral
  sb.adapter.aave.supplyBN({
    assetAddress: usdc.address as Address,
    amountBN: collateralAmount.toString()
  }),
  
  // 2. Borrow against collateral
  sb.adapter.aave.borrowBN({
    debtAddress: weth.address as Address,
    amountBN: borrowAmount.toString()
  }),
  
  // 3. Use borrowed funds for additional investments
  sb.adapter.openocean.swap({
    tokenInAddress: weth.address,
    tokenOutAddress: usdc.address,
    amountInBN: borrowAmount.toString()
  }),
  
  // 4. Supply additional USDC
  sb.adapter.aave.supplyAll({
    assetAddress: usdc.address as Address
  })
];

const executeData = proVault.executeByManager(leverageStrategy);
await client.sendTransaction({ ...executeData });
```

### 2. Yield Farming Strategy

```typescript
// Yield farming strategy with Aave
const yieldStrategy = [
  // 1. Supply assets to earn interest
  sb.adapter.aave.supplyAll({
    assetAddress: usdc.address as Address
  }),
  
  // 2. Supply additional assets for higher yield
  sb.adapter.aave.supplyAll({
    assetAddress: cbeth.address as Address
  }),
  
  // 3. Claim rewards (if available)
  sb.adapter.aave.claimRewards({
    assetAddresses: [usdc.address, cbeth.address]
  })
];

const executeData = proVault.executeByManager(yieldStrategy);
await client.sendTransaction({ ...executeData });
```

### 3. Flash Loan Strategy

```typescript
// Flash loan strategy using Balancer
const flashLoanStrategy = [
  // 1. Flash loan assets
  sb.adapter.flashloanBalancer.flashLoan({
    assetAddress: usdc.address as Address,
    amountBN: flashLoanAmount.toString(),
    callbackData: callbackData
  }),
  
  // 2. Use flash loan for arbitrage
  sb.adapter.openocean.swap({
    tokenInAddress: usdc.address,
    tokenOutAddress: weth.address,
    amountInBN: flashLoanAmount.toString()
  }),
  
  // 3. Swap back for profit
  sb.adapter.openocean.swap({
    tokenInAddress: weth.address,
    tokenOutAddress: usdc.address,
    amountInBN: swapAmount.toString()
  })
];

const executeData = proVault.executeByManager(flashLoanStrategy);
await client.sendTransaction({ ...executeData });
```

## Best Practices

### 1. Market Selection
- Choose markets with good liquidity
- Consider supply and borrow rates
- Monitor market health
- Diversify across multiple assets

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

### 4. Strategy Optimization
- Use deposit strategies for automation
- Implement compound strategies
- Monitor and adjust parameters
- Consider market conditions

## Network Support

### Supported Networks
- **Base**: Full support
- **Arbitrum**: Full support
- **Optimism**: Full support (coming soon)
- **Berachain**: Full support (coming soon)
- **Sonic**: Full support (coming soon)

## Resources

- [Aave Documentation](https://docs.aave.com/)
- [Aave Markets](https://app.aave.com/)
- [Aave Adapter API](./api-reference.md#aave-adapter)
- [Risk Management Guide](./risk-management.md)
- [Market Analytics](./market-analytics.md)
