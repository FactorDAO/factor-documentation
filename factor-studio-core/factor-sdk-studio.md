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
