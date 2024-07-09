# Table of contents

* [🏭 Introduction to Factor](README.md)

## Getting Started

* [🕹️ Quickstart](getting-started/quickstart.md)
* [🔗 Supported Protocols](getting-started/supported-protocols.md)
* [🧠 Strategy Explainers](getting-started/strategy-explainers/README.md)
  * [Leverage](getting-started/strategy-explainers/leverage/README.md)
    * [Leverage Performance Modelling](getting-started/strategy-explainers/leverage/leverage-performance-modelling.md)
    * [Leverage Long Simulation](getting-started/strategy-explainers/leverage/leverage-long-simulation.md)
    * [Leverage Short Simulation](getting-started/strategy-explainers/leverage/leverage-short-simulation.md)
  * [Yield](getting-started/strategy-explainers/yield/README.md)
    * [Yield Performance Modelling](getting-started/strategy-explainers/yield/yield-performance-modelling.md)
  * [PT Strategies](getting-started/strategy-explainers/pt-strategies/README.md)
    * [Leverage Long PT Simulation](getting-started/strategy-explainers/pt-strategies/leverage-long-pt-simulation.md)
* [📖 Glossary](getting-started/glossary.md)

## Factor Discover

* [🔍 Factor Discover](factor-discover/factor-discover/README.md)
  * [Leverage User Guides](factor-discover/factor-discover/leverage-user-guides/README.md)
    * [Create A Leveraged Position](factor-discover/factor-discover/leverage-user-guides/create-a-leveraged-position.md)
    * [Adjust Position Leverage](factor-discover/factor-discover/leverage-user-guides/adjust-position-leverage.md)
    * [Add Collateral To Position](factor-discover/factor-discover/leverage-user-guides/add-collateral-to-position.md)
    * [Withdraw Collateral From Position](factor-discover/factor-discover/leverage-user-guides/withdraw-collateral-from-position.md)
    * [Repay Position Debt](factor-discover/factor-discover/leverage-user-guides/repay-position-debt.md)
  * [Yield User Guides](factor-discover/factor-discover/yield-user-guides/README.md)
    * [Auto-compound Your Yields](factor-discover/factor-discover/yield-user-guides/auto-compound-your-yields.md)
  * [PT User Guides](factor-discover/factor-discover/pt-user-guides/README.md)
    * [Redeem Your PT](factor-discover/factor-discover/pt-user-guides/redeem-your-pt.md)
  * [APY Calculations](factor-discover/factor-discover/apy-calculations.md)

## Factor Studio

* [🎨 Factor Studio](factor-studio/factor-studio.md)
* [🏠 Studio](factor-studio/studio.md)
* [👥 Studio Pro](factor-studio/studio-pro.md)
* [🏗️ Strategy Builder](factor-studio/strategy-builder.md)
* [📜 Studio Contracts](factor-studio/studio-contracts/README.md)
  * [Leverage](factor-studio/studio-contracts/leverage/README.md)
    * [FactorLeverageDescriptor.sol](factor-studio/studio-contracts/leverage/factorleveragedescriptor.sol.md)
    * [FactorLeverageVault.sol](factor-studio/studio-contracts/leverage/factorleveragevault.sol.md)
    * [WrapperFactorLeverageVault.sol](factor-studio/studio-contracts/leverage/wrapperfactorleveragevault.sol.md)
  * [LP Management](factor-studio/studio-contracts/lp-management/README.md)
    * [FactorLPVault.sol](factor-studio/studio-contracts/lp-management/factorlpvault.sol.md)
    * [FactorLPDescriptor.sol](factor-studio/studio-contracts/lp-management/factorlpdescriptor.sol.md)

## Factor SDK

* [📦 Factor SDK](factor-sdk/factor-sdk.md)
* [↔️ REST APIs](factor-sdk/rest-apis/README.md)
  * [Utility APIs](factor-sdk/rest-apis/utility-apis/README.md)
    * [Pricing](factor-sdk/rest-apis/utility-apis/pricing.md)
    * [Stats](factor-sdk/rest-apis/utility-apis/stats.md)

## Factor Building Blocks

* [🧱 Factor Building Blocks](factor-building-blocks/factor-building-blocks.md)
* [🔄 Leverage](factor-building-blocks/leverage/README.md)
  * [Concepts](factor-building-blocks/leverage/concepts/README.md)
    * [Collateralized Lending & Borrowing](factor-building-blocks/leverage/concepts/collateralized-lending-and-borrowing.md)
    * [Looping](factor-building-blocks/leverage/concepts/looping.md)
  * [Leverage Dev Guides](factor-building-blocks/leverage/leverage-dev-guides/README.md)
    * [Create Leveraged Position](factor-building-blocks/leverage/leverage-dev-guides/create-leveraged-position.md)
    * [Add Leverage To Position](factor-building-blocks/leverage/leverage-dev-guides/add-leverage-to-position.md)
  * [Strategy Contracts](factor-building-blocks/leverage/strategy-contracts/README.md)
    * [AAVEV3LeverageStrategy.sol](factor-building-blocks/leverage/strategy-contracts/aavev3leveragestrategy.sol.md)
    * [CompoundLeverageStrategy.sol](factor-building-blocks/leverage/strategy-contracts/compoundleveragestrategy.sol.md)
    * [LodeStarLeverageStrategy.sol](factor-building-blocks/leverage/strategy-contracts/lodestarleveragestrategy.sol.md)
    * [RadiantLeverageStrategy.sol](factor-building-blocks/leverage/strategy-contracts/radiantleveragestrategy.sol.md)
    * [SiloLeverageStrategy.sol](factor-building-blocks/leverage/strategy-contracts/siloleveragestrategy.sol.md)
    * [SiloYieldTokenStrategy.sol](factor-building-blocks/leverage/strategy-contracts/siloyieldtokenstrategy.sol.md)
    * [TenderLeverageStrategy.sol](factor-building-blocks/leverage/strategy-contracts/tenderleveragestrategy.sol.md)
  * [FAQ - Leverage Building Block](factor-building-blocks/leverage/faq-leverage-building-block.md)
* [💸 Yield](factor-building-blocks/yield/README.md)
  * [Concepts](factor-building-blocks/yield/concepts/README.md)
    * [Yield Farming](factor-building-blocks/yield/concepts/yield-farming.md)
    * [Yield Aggregators](factor-building-blocks/yield/concepts/yield-aggregators.md)
  * [⚡ Zap](factor-building-blocks/yield/zap.md)
* [🌊 LP Management](factor-building-blocks/lp-management/README.md)
  * [Concepts](factor-building-blocks/lp-management/concepts/README.md)
    * [Automated Market Maker](factor-building-blocks/lp-management/concepts/automated-market-maker.md)
    * [Concentrated Liquidity](factor-building-blocks/lp-management/concepts/concentrated-liquidity.md)
* [🔀 Swap](factor-building-blocks/swap/README.md)
  * [Concepts](factor-building-blocks/swap/concepts/README.md)
    * [Market Orders](factor-building-blocks/swap/concepts/market-orders.md)
    * [DEX Aggregators](factor-building-blocks/swap/concepts/dex-aggregators.md)
* [🪄 Flash Loan](factor-building-blocks/flash-loan/README.md)
  * [Concepts](factor-building-blocks/flash-loan/concepts/README.md)
    * [Uncollateralized Lending & Borrowing](factor-building-blocks/flash-loan/concepts/uncollateralized-lending-and-borrowing.md)
    * [Flash Loan](factor-building-blocks/flash-loan/concepts/flash-loan.md)

## Factor Adapters

* [🔌 Factor Adapters](factor-adapters/factor-adapters.md)
* [📜 Adapter Contracts](factor-adapters/adapter-contracts/README.md)
  * [Leverage](factor-adapters/adapter-contracts/leverage.md)
  * [Yield](factor-adapters/adapter-contracts/yield.md)
  * [Swap](factor-adapters/adapter-contracts/swap.md)
  * [Flash Loan](factor-adapters/adapter-contracts/flash-loan.md)

## Governance

* [🏛️ FactorDAO](governance/factordao/README.md)
  * [Factor Flywheel](governance/factordao/factor-flywheel.md)
  * [User Guides](governance/factordao/user-guides/README.md)
    * [Stake FCTR](governance/factordao/user-guides/stake-fctr.md)
    * [Governance Migration](governance/factordao/user-guides/migrate-from-v1-to-v2.md)
  * [Contracts](governance/factordao/contracts/README.md)
    * [FactorDAO Contract Addresses](governance/factordao/contracts/factordao-contract-addresses.md)
  * [FactorDAO Multisig Addresses](governance/factordao/factordao-multisig-addresses.md)
  * [Platform Fees](governance/factordao/platform-fees.md)
* [🪙 FCTR Token](governance/fctr-token/README.md)
  * [🌿 Staking and Governance](governance/fctr-token/staking-and-governance.md)
  * [🌱 Initial Distribution](governance/fctr-token/initial-distribution.md)
  * [📜 Contract Addresses](governance/fctr-token/contract-addresses.md)
  * [❔ FAQ - Tokenomics](governance/fctr-token/faq-tokenomics.md)
* [⚖️ Factor Scale](governance/factor-scale/README.md)
  * [Arbitrum Foundation LTIPP](governance/factor-scale/arbitrum-foundation-ltipp.md)
  * [Emission Multiplier Calculations](governance/factor-scale/emission-multiplier-calculations.md)
  * [User Guides](governance/factor-scale/user-guides/README.md)
    * [Stake FCTR](https://docs.factor.fi/governance/factordao/user-guides/stake-fctr)
    * [Vote On Emissions Distribution](governance/factor-scale/user-guides/vote-on-emissions-distribution.md)
  * [Contracts](governance/factor-scale/contracts/README.md)
    * [Factor Scale Contract Addresses](governance/factor-scale/contracts/factor-scale-contract-addresses.md)
  * [❔ FAQ - Factor Scale](governance/factor-scale/faq-factor-scale.md)
* [🚀 Factor Boost](governance/factor-boost/README.md)
  * [Contracts](governance/factor-boost/contracts/README.md)
    * [Factor Boost Contract Addresses](governance/factor-boost/contracts/factor-boost-contract-addresses.md)
* [💼 Factor Bribes](governance/factor-bribe/README.md)
  * [Contracts](governance/factor-bribe/contracts/README.md)
    * [Factor Bribes Contracts](governance/factor-bribe/contracts/factor-bribes-contracts.md)

## Security

* [🛡️ Security](security/security.md)
* [📋 Audits](security/audits/README.md)
  * [PeckShield](security/audits/peckshield/README.md)
    * [Leverage Vault Wrapper](security/audits/peckshield/leverage-vault-wrapper.md)
    * [Silo Yield](security/audits/peckshield/silo-yield.md)
    * [Silo Leverage](security/audits/peckshield/silo-leverage.md)
    * [Penpie](security/audits/peckshield/penpie.md)
    * [Factor Boost](security/audits/peckshield/factor-boost.md)
  * [SourceHat](security/audits/sourcehat/README.md)
    * [FactorDAO Vaults](https://sourcehat.com/audits/FactorDAOVaults/)
    * [FCTR & Voting Escrow](https://sourcehat.com/audits/Factor/)

## Reference

* [dApp](https://app.factor.fi/)
* [Official Website](https://factor.fi/)
* [Press Kit](reference/press-kit.md)
* [Partnership Form](https://forms.gle/xAhiB956tePz5vvv5)

## Community

* [Factor Contributors](community/factor-contributors.md)
* [X](https://twitter.com/FactorDAO)
* [Discord](https://discord.gg/factor)
* [Telegram](https://t.me/FactorDAO)
* [Medium](https://medium.com/@FactorDAO)
* [Email Enquiries](mailto:info@factor.fi)
