# Factor SDK Studio

The Factor SDK Studio (`@factordao/sdk-studio`) is an advanced TypeScript SDK designed specifically for strategy builders and developers who want to create sophisticated DeFi strategies using the Factor infrastructure. This package provides high-level abstractions and comprehensive integration with the Factor ecosystem.

## Package Information

- **Package Name**: `@factordao/sdk-studio`
- **Version**: 2.0.54
- **License**: MIT
- **Main Entry Point**: `dist/cjs/index.js`

## Architecture Overview

The Factor SDK Studio builds upon the core Factor Contracts to provide specialized tools for strategy development. It follows a modular architecture with clear separation of concerns:

### Core Modules

#### 1. Private Strategy Builder (`src/strategy-builder/`)
Programmatic strategy construction tools that allow developers to build complex DeFi strategies using a modular approach for private strategies, anyone beside the owner can't execute the strategy.

**Key Components:**
- **Strategy Builder**: Core strategy construction engine
- **Strategy Builder Vault**: Vault management for strategy execution
- **Strategy Builder Stats**: Performance metrics and analytics
- **Strategy Builder Metrics**: Detailed performance measurements

#### 2. Adapter System (`src/adapter/`)
Comprehensive adapter system for integrating with various DeFi protocols and services.

**Adapter Categories:**
- **DEX Adapters**: Uniswap, Camelot, TraderJoe integrations
- **Lending Adapters**: Aave, Compound, Euler integrations
- **Yield Adapters**: Pendle, Silo, Tender integrations
- **LP Adapters**: Liquidity provision strategies
- **Leverage Adapters**: Leveraged position management
- **Flash Loan Adapters**: Flash loan integrations
- **Perpetual Adapters**: GMX, Vela perpetual integrations
- **Policy Adapters**: Risk management and validation
- **Utility Adapters**: Helper functions and utilities
- **Validation Adapters**: Input validation and security

#### 3. Studio Pro (`src/studio-pro/`)
Advanced features for professional strategy developers and institutional users for public strategies, anyone can deposit and withdraw from the strategy.

**Studio Pro Features:**
- **Studio Pro Factory**: Advanced vault deployment and management
- **Studio Pro Vault**: Enhanced vault functionality
- **Studio Pro Stats**: Advanced analytics and reporting
- **Resolver Modules**: Data resolution and processing

#### 4. Boost Integration (`src/boost/`)
Integration with Factor's reward and incentive mechanisms.

#### 5. Scale Integration (`src/scale/`)
Integration with Factor's governance and token staking systems.

## Configuration and Deployment

### Environment Configuration
The SDK Studio supports multiple environments:

- **Testing**: Development and testing environment
- **Staging**: Pre-production environment
- **Production**: Production environment

### Chain Support
Currently supported chains:
- **Arbitrum One**: Full support
- **Base**: Full support
- **Berachain**: Full support (coming soon)
- **Sonic**: Full support (coming soon)

### Contract Addresses
The address book is available in the `src/common/address/{chain}` folder, there's a file for each chain and each environment.

## Pro Vaults Examples

The Factor SDK Studio includes comprehensive examples in the `pro-vaults-examples/` directory that demonstrate real-world usage of the Studio Pro system. These examples provide practical implementations of various DeFi strategies and vault management operations.

### Example Documentation

- **[Pro Vaults Examples Overview](pro-vaults-examples/README.md)**: Complete overview of all available examples and their purposes
- **[Vault Deployment Examples](pro-vaults-examples/vault-deployment.md)**: Step-by-step guide to deploying vaults with different configurations
- **[Strategy Execution Examples](pro-vaults-examples/strategy-execution.md)**: Comprehensive examples of executing DeFi strategies using the Strategy Builder
- **[Asset Management Examples](pro-vaults-examples/asset-management.md)**: Managing deposits, withdrawals, and balance tracking within vaults
- **[Compound V3 Integration](pro-vaults-examples/compound-integration.md)**: Specialized examples for Compound V3 lending and borrowing operations

### Key Example Categories

#### 1. **Vault Deployment** (10+ examples)
- Basic vault deployment configurations
- Advanced vault setups with multiple assets
- Different adapter configurations
- Fee structure examples

#### 2. **Strategy Execution** (15+ examples)
- Swap strategies (Uniswap, OpenOcean)
- Lending strategies (Aave, Compound)
- Liquidity provision (Uniswap V3, Camelot)
- Yield farming strategies
- Flash loan implementations

#### 3. **Asset Management** (10+ examples)
- Deposit and withdrawal operations
- Balance tracking and analytics
- Share calculations
- Asset configuration management

#### 4. **Advanced Features** (10+ examples)
- Boost and reward management
- Governance operations
- Strategy validation and testing
- Analytics and monitoring

### Getting Started with Examples

1. **Review the Overview**: Start with the [Pro Vaults Examples README](pro-vaults-examples/README.md) to understand the structure
2. **Environment Setup**: Configure your development environment following the setup guides
3. **Deploy Your First Vault**: Use the [Vault Deployment Examples](pro-vaults-examples/vault-deployment.md) to deploy a test vault
4. **Execute Strategies**: Learn strategy execution with the [Strategy Execution Examples](pro-vaults-examples/strategy-execution.md)
5. **Manage Assets**: Understand asset management with the [Asset Management Examples](pro-vaults-examples/asset-management.md)

### Example Use Cases

- **Yield Farming**: Deploy vaults that automatically farm yield from multiple protocols
- **Leverage Trading**: Create leveraged positions using Aave and other lending protocols
- **Liquidity Provision**: Provide liquidity to DEXs and earn trading fees
- **Arbitrage**: Execute arbitrage strategies across different DEXs
- **Portfolio Management**: Manage multi-asset portfolios with automated rebalancing

## Dependencies

### Core Dependencies
- `@factordao/contracts`: Factor smart contracts
- `@factordao/sdk`: Core Factor SDK
- `@factordao/tokenlist`: Token list management
- `@uniswap/sdk`: Uniswap integration
- `@uniswap/v3-sdk`: Uniswap V3 integration
- `ethers`: Ethereum interaction library
- `viem`: Modern Ethereum library
- `bignumber.js`: Big number handling
- `dayjs`: Date manipulation
- `axios`: HTTP client
- `graphql-request`: GraphQL client

### Development Dependencies
- `hardhat`: Development framework
- `typescript`: Type safety
- `eslint`: Code linting
- `prettier`: Code formatting
- `mocha`: Testing framework
- `chai`: Assertion library

## Contributing

1. Fork the repository
2. Create a feature branch
3. Implement your changes with tests
4. Ensure all tests pass
5. Submit a pull request

## License

This package is licensed under the MIT License.
