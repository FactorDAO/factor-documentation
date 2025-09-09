# Factor Contracts

The Factor Contracts package (`@factordao/contracts`) contains all the smart contracts that power the Factor protocol ecosystem. This package provides the foundational infrastructure for DeFi strategy execution, asset management, and protocol governance.

## Package Information

- **Package Name**: `@factordao/contracts`
- **Version**: 2.0.54
- **License**: MIT
- **Main Entry Point**: `dist/cjs/src/index.js`

## Architecture Overview

The Factor protocol uses a modular, adapter-based architecture that allows for flexible integration with various DeFi protocols. The contracts are organized into several key categories:

### Core Components

#### 1. Adapters (`contracts/adapters/`)
Protocol-specific integrations that abstract away the complexity of interacting with different DeFi protocols.

**Adapter Categories:**
- **DEX Adapters** (`dex/`): Uniswap, Camelot, TraderJoe integrations
- **Lending Adapters** (`lending/`): Aave, Compound, Euler integrations  
- **Yield Adapters** (`yields/`): Pendle, Silo, Tender integrations
- **LP Adapters** (`lp/`): Liquidity provision strategies
- **Leverage Adapters** (`leverage/`): Leveraged position management
- **Flash Loan Adapters** (`fl/`): Flash loan integrations
- **Perpetual Adapters** (`perp/`): GMX, Vela perpetual integrations
- **Policy Adapters** (`policy/`): Risk management and validation
- **Utility Adapters** (`utils/`): Helper functions and utilities
- **Validation Adapters** (`validation/`): Input validation and security

#### 2. Strategies (`contracts/strategies/`)
Pre-built DeFi strategies that combine multiple adapters to create sophisticated investment strategies.

**Strategy Types:**
- **Single Strategies** (`single/`): Simple, single-protocol strategies
- **Multi Strategies** (`multi/`): Multi-protocol strategies
- **Leverage Strategies** (`leverage/`): Leveraged position strategies
- **LP Strategies** (`lp/`): Liquidity provision strategies
- **Batchable Strategies** (`batchable/`): Strategies that can be executed in batches

#### 3. Vaults (`contracts/vaults/`)
Asset management containers that hold user funds and execute strategies.

**Vault Types:**
- **Single Vaults** (`single/`): Single-strategy vaults
- **Multi Vaults** (`multi/`): Multi-strategy vaults
- **Genesis Vaults** (`genesis/`): Initial protocol vaults
- **Batchable Vaults** (`batchable/`): Vaults supporting batch operations
- **Base Vaults** (`base/`): Base vault implementations

#### 4. Governance (`contracts/scale/`, `contracts/boost/`, `contracts/bribe/`)
Token governance, voting, and reward mechanisms.

**Governance Components:**
- **Factor Scale** (`scale/`): Token staking and governance
- **Factor Boost** (`boost/`): Reward and incentive mechanisms
- **Factor Bribe** (`bribe/`): Bribe and incentive distribution
- **Voting Escrow** (`scale/voting-escrow/`): Token locking and voting power

#### 5. Cross-Chain (`contracts/crosschain/`)
Multi-chain communication infrastructure for cross-chain operations.

#### 6. Studio (`contracts/studio/`)
Strategy builder and studio-specific contracts for advanced strategy development.

## Supported Protocols

The Factor protocol integrates with a wide range of DeFi protocols:

### DEX Protocols
- Uniswap V2/V3
- Camelot
- TraderJoe
- Balancer
- Curve

### Lending Protocols
- Aave V2/V3
- Compound
- Euler
- Radiant
- Silo

### Yield Protocols
- Pendle
- Tender
- Plutus
- Umami
- Lodestar

### Perpetual Protocols
- GMX
- Vela
- Lyra

### Other Protocols
- Gelato (Automation)
- LayerZero (Cross-chain)
- OpenZeppelin (Security)

## Development Tools

### Build System
- **Hardhat**: Primary development framework
- **Forge**: Advanced testing and deployment
- **TypeScript**: Type-safe contract interactions
- **Wagmi**: Contract ABI generation

### Testing Framework
- **Forge Test**: Solidity testing
- **Hardhat Test**: JavaScript/TypeScript testing
- **Coverage**: Test coverage analysis
- **Gas Reporter**: Gas usage analysis

### Deployment
- **Hardhat Deploy**: Contract deployment management
- **Tenderly**: Contract verification and monitoring
- **Docker**: Containerized deployment

## Network Support

The contracts support deployment on multiple networks:

- **Arbitrum**
- **Base**
- **Optimism**
- **Berachain**
- **Sonic**

## Dependencies

### Core Dependencies
- `@openzeppelin/contracts`: Security and standard implementations
- `@uniswap/v3-core`: Uniswap V3 integration
- `@uniswap/v3-periphery`: Uniswap V3 periphery contracts
- `@cryptoalgebra/core`: Algebra DEX integration

### Development Dependencies
- `hardhat`: Development framework
- `ethers`: Ethereum interaction library
- `typescript`: Type safety
- `prettier`: Code formatting
- `solhint`: Solidity linting

## Contributing

1. Fork the repository
2. Create a feature branch
3. Implement your changes with tests
4. Ensure all tests pass
5. Submit a pull request

## License

This package is licensed under the MIT License.
