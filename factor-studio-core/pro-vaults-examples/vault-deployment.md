# Vault Deployment Examples

This document covers the vault deployment examples in the Factor Studio Pro Vaults system. These examples demonstrate how to deploy vaults with different configurations and parameters.

## Overview

Vault deployment in Factor Studio Pro involves creating a new vault instance with specific configuration parameters. The deployment process uses the `StudioProFactory` to create vaults with predefined settings for assets, adapters, fees, and risk management.

## Example Files

### 01-deploy-vault-v0.ts through 01-deploy-vault-v9.ts

These files demonstrate different vault deployment configurations, each with unique parameters and use cases.

## Key Components

### 1. Deployment Configuration

Each deployment example follows a similar pattern:

```typescript
function getDeploymentConfig(): StudioProFactoryDeployVaultParams {
  const initialDeposit = '1600'; // 1600 wei minimum deposit

  // Get contract addresses for the chain and environment
  const {
    factor_openocean_adapter_pro,
    factor_aave_adapter_pro,
    factor_flashloan_balancer_adapter_pro,
    factor_chainlink_accounting_adapter_pro,
    // ... other adapters
  } = getContractAddressesForChainOrThrow(chainId, 'testing');

  // Configure adapters
  const managerAdapters = [factor_aave_adapter_pro];
  const ownerAdapters = [factor_boost_adapter_pro];
  const withdrawAdapters = [factor_transfer_adapter_pro];

  return {
    initialDepositBN: initialDeposit.toString(),
    name: 'Vault Name',
    symbol: 'VAULT',
    configParams: {
      // Configuration parameters
    },
    feeParams: {
      // Fee parameters
    }
  };
}
```

### 2. Configuration Parameters

#### Basic Configuration
- **name**: Human-readable vault name
- **symbol**: Vault token symbol
- **initialDepositBN**: Minimum initial deposit amount

#### Asset Configuration
- **assetDenominatorAddress**: Base asset for calculations (usually USDC)
- **assetDenominatorAccountingAddress**: Oracle for base asset pricing
- **initialAssetAddresses**: Assets the vault can hold
- **initialDepositAssetAddresses**: Assets users can deposit
- **initialWithdrawAssetAddresses**: Assets users can withdraw
- **initialDebtAddresses**: Assets the vault can borrow

#### Adapter Configuration
- **initialManagerAdapters**: Adapters that can execute strategies
- **initialOwnerAdapters**: Adapters that can modify vault configuration
- **initialWithdrawAdapters**: Adapters that can process withdrawals

#### Risk Management
- **maxCapBN**: Maximum total value the vault can hold
- **maxDebtRatioBN**: Maximum debt-to-asset ratio
- **cumulativePriceDeviationAllowanceBpsBN**: Maximum price deviation allowance

#### Security Settings
- **upgradeTimelockBN**: Time delay for upgrades
- **cooldownTimeBN**: Cooldown period between operations
- **upgradeable**: Whether the vault can be upgraded

### 3. Fee Configuration

```typescript
feeParams: {
  feeReceiver: '0x...',                    // Address to receive fees
  depositFeeBN: '0.001',                   // 0.1% deposit fee
  withdrawFeeBN: '0.001',                  // 0.1% withdrawal fee
  performanceFeeBN: '0.1',                 // 10% performance fee
  managementFeeBN: '0.001'                 // 0.1% management fee
}
```

## Deployment Process

### 1. Environment Setup

```typescript
const privateKey = process.env.PRIVATE_KEY?.replace('0x', '');
const alchemyApiKey = process.env.ALCHEMY_API_KEY;
const account = privateKeyToAccount(`0x${privateKey}`);

const client = createWalletClient({
  account,
  chain: arbitrum,
  transport: http(`https://arb-mainnet.g.alchemy.com/v2/${alchemyApiKey}`)
}).extend(publicActions);
```

### 2. Factory Initialization

```typescript
const proFactory = new StudioProFactory({
  chainId: ChainId.ARBITRUM_ONE,
  environment: 'testing'
});
```

### 3. Token Approval

```typescript
// Approve the factory to spend tokens for initial deposit
const allowance = await client.writeContract({
  address: usdc,
  abi: erc20ABI,
  functionName: 'approve',
  args: [
    factor_studio_pro_factory as Address,
    valueToBigInt(MAX_UINT_256.toString())
  ]
});
```

### 4. Vault Deployment

```typescript
const deploymentConfig = getDeploymentConfig();
const txData = proFactory.deployVault(deploymentConfig);
const hash = await client.sendTransaction(txData);
const receipt = await client.waitForTransactionReceipt({ hash });

// Extract vault address from receipt
const vaultAddress = proFactory.decodeDeployVaultEventFromReceipt(receipt).vault;
```

## Example Configurations

### Basic Vault (v0)
- **Assets**: WETH, USDC
- **Adapters**: Compound V3, Transfer, Refund
- **Use Case**: Simple asset management

### Leverage Vault (v1)
- **Assets**: WETH, aWETH, vDebtUSDC
- **Adapters**: Aave, OpenOcean, Flash Loan
- **Use Case**: Leveraged ETH positions

### Trading Vault (v2)
- **Assets**: USDC, WBTC, WETH
- **Adapters**: Uniswap, Chainlink
- **Use Case**: Multi-asset trading

### LP Vault (v3)
- **Assets**: WETH, USDC
- **Adapters**: Uniswap V3 LP
- **Use Case**: Liquidity provision

### Yield Vault (v4)
- **Assets**: WETH, USDC
- **Adapters**: Pendle, Silo
- **Use Case**: Yield farming

## Best Practices

### 1. Configuration Validation
- Validate all addresses before deployment
- Check adapter compatibility
- Verify asset configurations
- Test with small amounts first

### 2. Security Considerations
- Use appropriate timelock periods
- Set reasonable cooldown times
- Implement proper access controls
- Consider upgrade paths

### 3. Fee Structure
- Set competitive fee rates
- Consider market conditions
- Balance profitability with user adoption
- Monitor fee collection

### 4. Risk Management
- Set appropriate debt ratios
- Implement price deviation limits
- Consider market volatility
- Plan for emergency scenarios

## Common Issues and Solutions

### 1. Insufficient Gas
- Increase gas limit
- Check gas price
- Optimize transaction size

### 2. Invalid Configuration
- Validate all parameters
- Check adapter addresses
- Verify asset configurations

### 3. Approval Issues
- Ensure proper token approvals
- Check allowance amounts
- Verify factory address

### 4. Deployment Failures
- Check contract addresses
- Verify environment settings
- Review error messages

## Testing and Validation

### 1. Pre-deployment Testing
- Validate configuration parameters
- Test with simulation tools
- Check adapter compatibility
- Verify asset configurations

### 2. Post-deployment Validation
- Verify vault address
- Check initial configuration
- Test basic operations
- Validate fee structure

### 3. Integration Testing
- Test deposit/withdrawal flows
- Verify strategy execution
- Check fee collection
- Validate access controls

## Monitoring and Maintenance

### 1. Deployment Monitoring
- Track deployment transactions
- Monitor gas usage
- Check for errors
- Verify configuration

### 2. Ongoing Maintenance
- Monitor vault performance
- Update configurations as needed
- Manage fee structures
- Handle upgrades

### 3. User Support
- Provide clear documentation
- Monitor user interactions
- Handle support requests
- Maintain uptime

## Resources

- [Studio Pro Factory API](./api-reference.md#studio-pro-factory)
- [Vault Configuration Guide](./vault-configuration.md)
- [Adapter Documentation](./adapter-documentation.md)
- [Risk Management Guide](./risk-management.md)
