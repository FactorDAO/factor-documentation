# Yield Aggregators

## Overview

Yield Aggregators (a.k.a. Yield Vaults) automate the compounding of LP rewards to maximize potential yield while socializing the costs of interacting with DEX smart contracts. Yield Aggregators increases the potential yield generated from liquidity pool trading fees and [Yield Farms](yield-farming.md) by auto-compounding the accrued rewards on a periodic basis. This ensures more optimal returns via greater capital efficiency while minimizing the manual overhead and gas costs required for liquidity management.

Prior to the creation of Yield Aggregators, LPs had to manually claim their rewards on a per position basis which would then be reinvested into the pool. This meant incurring a gas cost for each claim and add liquidity transaction which could significantly cut into a LP's profit depending on their liquidity size. Moreover, in cases where Yield Farm tokens differed from the pool tokens, an additional swap was required before the value of the farming rewards could be reinvested. Critically, in most AMMs and Yield Farms, LP rewards usually laid dormant (i.e. not actively generating yield) until it was claimed and reinvested.

Through automating the rewards claiming process, Yield Aggregators generated the following benefits:

* Increased capital efficiency and yields
* Reduced exposure to reward tokens as hold time was significantly slashed
* Reduced liquidity management transaction fees

## How It Works

To qualify for a Yield Aggregator, LPs must first deposit liquidity into an underlying liquidity pool to receive a LP token. The LP token represents the LP's share of the liquidity pool and enables the LP token holder to manage the position. Using the LP token, LPs can then delegate their liquidity share to the Yield Aggregator contract. The contract defines the yield strategy and manages the LP's liquidity and auto-compounds rewards for the LP.

Of note, Yield Aggregators are able to handle multiple positions that are created on the underlying liquidity pool. This means that multiple LPs could stake their positions in the Yield Aggregator contract whereby operational costs could be socialized.

Users are also able to withdraw their assets, along with their accrued yield, from the Yield Aggregator according to their needs and timing.
