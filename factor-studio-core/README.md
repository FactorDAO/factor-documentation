# Factor Studio Core

Factor Studio Core is a comprehensive monorepo containing the core infrastructure for the Factor protocol ecosystem. This repository provides the foundational smart contracts, SDKs, and tooling necessary for building and deploying DeFi strategies on the Factor platform.

## Repository Structure

The repository is organized as a Lerna monorepo with three main packages:

```
factor-studio-core/
├── packages/
│   ├── factor-contracts/     # Smart contracts and Solidity code
│   ├── factor-sdk/          # Core SDK for interacting with Factor protocol
│   └── factor-sdk-studio/   # Studio-specific SDK for strategy building
├── scripts/                 # Build and deployment scripts
└── lerna.json              # Lerna configuration
```

## Packages Overview

### 1. Factor Contracts (`@factordao/contracts`)
The core smart contract package containing all Solidity contracts for the Factor protocol.

**Key Components:**
- **Adapters**: Protocol-specific integrations (DEX, lending, yield farming)
- **Strategies**: Pre-built DeFi strategies (leverage, LP management, yield)
- **Vaults**: Asset management and strategy execution containers
- **Governance**: Token governance, voting, and reward mechanisms
- **Cross-chain**: Multi-chain communication infrastructure

**Version:** 2.0.54

For detailed documentation, see [Factor Contracts Documentation](factor-contracts.md).

### 2. Factor SDK (`@factordao/sdk`) - Legacy strategies
The core TypeScript SDK providing high-level interfaces for interacting with Factor protocol contracts.

**Key Modules:**
- **Leverage**: Leveraged position management
- **LP Management**: Liquidity provision strategies
- **Yield**: Yield farming and optimization
- **Portfolio**: Multi-strategy portfolio management
- **Vault**: Vault interaction and management
- **Boost**: Reward and incentive mechanisms
- **Scale**: Governance and token staking

**Version:** 2.0.54

### 3. Factor SDK Studio (`@factordao/sdk-studio`)
Studio-specific SDK providing advanced tools for strategy builders and developers.

**Key Features:**
- **Strategy Builder**: Private strategies management
- **Adapter System**: Protocol integration framework
- **Block System**: Modular strategy components
- **Studio Pro**: Public strategies management
- **Boost Integration**: Reward and incentive management
- **Scale Integration**: Governance and staking features

**Version:** 2.0.54

For detailed documentation, see [Factor SDK Studio Documentation](factor-sdk-studio.md).

## Getting Started

### Prerequisites
- Node.js (v18+)
- Yarn package manager
- Git with submodule support

### Initial Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/factordao/factor-studio-core.git
   cd factor-studio-core
   ```

2. **Update submodules:**
   ```bash
   bash scripts/update_submodules.sh
   ```

3. **Install dependencies and build all packages:**
   ```bash
   yarn
   ```

### Development Workflow

The repository uses Lerna for monorepo management with the following key commands:

- `yarn build` - Build all packages in dependency order
- `yarn test` - Run tests across all packages
- `yarn clean` - Clean build artifacts from all packages

### Build Order
Packages are built in the following order to respect dependencies:
1. `factor-contracts` - Smart contracts (foundation)
2. `factor-sdk` - Core SDK (depends on contracts)
3. `factor-sdk-studio` - Studio SDK (depends on both contracts and core SDK)

## Supported Networks

The Factor protocol supports multiple blockchain networks including:
- Arbitrum
- Base
- Optimism
- Berachain (coming soon)
- Sonic (coming soon)

## Development Tools

### Testing
- **Hardhat**: Smart contract development and testing
- **Forge**: Advanced Solidity testing framework
- **Mocha/Chai**: TypeScript testing framework

### Code Quality
- **Prettier**: Code formatting
- **ESLint**: Code linting
- **Solhint**: Solidity linting
- **TypeScript**: Type safety

### Deployment
- **Hardhat Deploy**: Contract deployment management
- **Tenderly**: Contract verification and monitoring
- **Docker**: Containerized deployment options

## Pro Vaults Examples

The `pro-vaults-examples/` directory contains comprehensive examples demonstrating how to use the Factor Studio Pro Vaults system. These examples cover everything from basic vault deployment to advanced strategy execution and management.

### Example Categories

- **[Vault Deployment](pro-vaults-examples/vault-deployment.md)**: Complete guide to deploying vaults with different configurations
- **[Strategy Execution](pro-vaults-examples/strategy-execution.md)**: Examples of executing various DeFi strategies using the vault's manager privileges
- **[Asset Management](pro-vaults-examples/asset-management.md)**: Managing deposits, withdrawals, and balance tracking within vaults
- **[Compound Integration](pro-vaults-examples/compound-integration.md)**: Specialized examples for Compound V3 lending and borrowing operations

### Key Features Demonstrated

- **Public Vaults**: Anyone can deposit and withdraw from these strategies
- **Manager Execution**: Only designated managers can execute strategies
- **Multi-Asset Support**: Support for multiple assets and debt positions
- **Advanced Strategies**: Leverage, yield farming, liquidity provision, and more
- **Risk Management**: Built-in risk controls and validation
- **Fee Management**: Configurable deposit, withdrawal, performance, and management fees

### Getting Started with Examples

1. **Environment Setup**: Configure your development environment with required API keys
2. **Vault Deployment**: Deploy your first vault using the deployment examples
3. **Strategy Execution**: Learn to execute strategies using the Strategy Builder
4. **Asset Management**: Understand deposit/withdrawal flows and balance management
5. **Advanced Integration**: Explore protocol-specific integrations like Compound V3

For detailed documentation and code examples, see the [Pro Vaults Examples README](pro-vaults-examples/README.md).

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For questions and support:
- Documentation: [Factor Documentation](https://docs.factor.fi)
- Discord: [Factor Discord](https://discord.gg/factor)
- GitHub Issues: [Create an issue](https://github.com/factordao/factor-studio-core/issues)
