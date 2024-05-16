# 🪙 FCTR Token

## Overview

The FactorDAO (FCTR) token promotes the sustainability of the Factor ecosystem by incentivizing genuine community governance which shapes the protocol's development and trajectory. Implemented as an [ERC20](https://docs.openzeppelin.com/contracts/5.x/erc20) token on Arbitrum, FCTR plays an essential role in governing the Factor platform through the FactorDAO and facilitating its various operations.

By staking FCTR, Factorians are able to vote on FactorDAO governance processes as well as influence the distribution of platform revenue via [Factor Scale](../factor-scale/). In return for securing the Factor ecosystem, FCTR stakers also earn a share of the protocol's revenue.

{% hint style="success" %}
**Factor Ethos**

Factor operates based on principles of fairness, community involvement, and sustainable development. These core values are mirrored in our tokenomics model, which has been carefully designed to emphasize the equitable distribution of the majority of $FCTR tokens directly to our community. This approach empowers our community members to actively participate in governing our protocol, ensuring their central role in decision-making processes.

With over 80% of the FCTR supply allocated to the community, we emphasize our trust in the collective wisdom and decision-making capabilities of an active community. We firmly believe that this strategy will drive DeFi innovation to unprecedented levels and nurture a collaborative ecosystem.
{% endhint %}

### At A Glance

<table><thead><tr><th width="253">FCTR Token Details</th><th>Value</th></tr></thead><tbody><tr><td>Name</td><td>FactorDAO</td></tr><tr><td>Symbol</td><td>FCTR</td></tr><tr><td>Token Launch Chain</td><td><a href="https://docs.arbitrum.io/for-devs/gentle-introduction-dapps">Arbitrum One</a> (ChainID: 42161)</td></tr><tr><td>Token Standard</td><td>ERC20 (<a href="https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/master/contracts/token/ERC20/ERC20Upgradeable.sol">Upgradeable</a>)</td></tr><tr><td>Decimals</td><td>18</td></tr><tr><td>Total Supply</td><td>100,000,000</td></tr><tr><td>Max Supply</td><td>100,000,000</td></tr><tr><td>Token Generation Event</td><td>Feb-19-2023 09:27:37 PM +UTC (<a href="https://arbiscan.io/tx/0x4e0d6223254b490d072e93f5a9f27cc446d391142dceb6656bc9374510b448ae">Tx Hash</a>)</td></tr><tr><td>Contract Address (Proxy)</td><td><a href="https://arbiscan.io/address/0x6dd963c510c2d2f09d5eddb48ede45fed063eb36"><code>0x6dd963c510c2d2f09d5eddb48ede45fed063eb36</code></a></td></tr></tbody></table>

## Tokenomics

Factor implements a gauge voting system that **allocates greater voting weight for FCTR tokens which have been vested for longer periods**. This aligns platform decentralized governance with long term economic incentives. To ensure the growth and evolution of a resilient platform via an actively involved community, the Factor ecosystem consists of 3 tokens:

* **FCTR:** The main token of the Factor platform which represents total platform value.  FCTR tokens can be traded on any ERC20 compatible DEXs.
* **veFCTR:** Users receive veFCTR in return for staking FCTR. Each veFCTR represents a vote which can be allocated to influence various governance proposals.
* **esFCTR:** The esFCTR token represents vested or locked rewards on the Factor platform. esFCTR is non-transferable and can be converted to FCTR after the 90-day vesting period.

{% hint style="info" %}
**Token Contract Addresses**

The relevant contracts for each of the tokens can be found on the [Contract Addresses](contract-addresses.md) page.
{% endhint %}

Each of the tokens above plays a vital role in securing the Factor ecosystem through permissionless and democratic means. Factor **enforces a maximum supply cap of 100,000,000 FCTR tokens** thereby ensuring no inflationary mechanisms nor any circumstances that could introduce unsustainable tokenomics. Factorians always maintain full ownership over their tokens and have the freedom to utilize the underlying value of the tokens however they see fit.

### FCTR

Launched on Arbitrum in February 2023, FCTR was immediately distributed via a fair launch lasting 4 days on the [Camelot DEX](https://app.camelot.exchange/launchpad/factor/). With 13,394 participating users, the Fair Launch raised 7,578,366USDC whereupon 10% of FCTR total supply was distributed. The remaining FCTR tokens were allocated to ecosystem growth initiatives with linear vesting ending 4 years after the Token Generation Event (i.e. Feb-19-2027 09:27:37 PM +UTC).

{% hint style="info" %}
:seedling: **FCTR Initial Distribution**

More details regarding the initial distribution of FCTR can be found [here](initial-distribution.md).
{% endhint %}

As Factor's main token, the FCTR token democratizes access to value exchange on the Factor platform. **By owning FCTR tokens, users get the right to participate in Factor governance processes while also directly benefitting from ecosystem growth.**

Adhering to the [ERC20](https://docs.openzeppelin.com/contracts/5.x/erc20) token standard, FCTR maintains seamless compatibility with EVM-based smart contract and can be easily traded on any DEX (decentralized exchange). Long-term FCTR holders can then stake FCTR to become eligible to vote on various Factor initiatives. As such, FCTR effectively functions as the gateway for users to participate in the shared ownership of the Factor platform.

{% hint style="success" %}
**Market Data & Analytics**

* **CoinGecko:** [https://www.coingecko.com/en/coins/factordao](https://www.coingecko.com/en/coins/factordao)
* **CoinMarketCap:** [https://coinmarketcap.com/currencies/factor/](https://coinmarketcap.com/currencies/factor/)
{% endhint %}

### veFCTR

veFCTR (vote-escrow FCTR) is a special governance token that enables holders to vote on various FactorDAO governance proposals. **Each veFCTR represents a single vote within the Factor ecosystem.**

veFCTR is minted when FCTR tokens are staked into the FactorDAO governance contract. The ratio of veFCTR minted per FCTR is determined by the staking duration whereby a max lock of 2 years results in the maximum of 1veFCTR:1FCTR. The veFCTR balance is subject to a time-based linear decay which  corresponds to the time left in the staking period for the underlying FCTR.  In short, the longer the FCTR staking period, the more veFCTR allocated.

By staking FCTR tokens for up to a maximum of 2 years, **FCTR stakers are also able increase their emissions multiplier up till a maximum of 2.5x**. In addition to staking duration, the emissions multiplier also rewards veFCTR holders with a larger proportion of holdings as well as their strategy deposit amount. The emissions multiplier does not decay and remains the same for the period that the underlying FCTR is staked.

Put simply, the longer the commitment, the more voting power and rewards (i.e. emissions) the FCTR staker receives. This discourages speculation and instead incentivizes prolonged engagement with the protocol. Critically, the conversion to veFCTR also limits the influence of large token holders (i.e. whales) thereby ensuring a more balanced governance process.

In addition to governance rights, **50% of the protocol's ongoing revenue is automatically distributed to veFCTR holders as** [**USDC**](https://arbiscan.io/token/0xaf88d065e77c8cc2239327c5edb3a432268e5831). This revenue sharing model greatly encourages long term FCTR staking which in turn aligns FCTR holders and Factor ecosystem growth.

{% hint style="info" %}
**Get veFCTR Tokens**&#x20;

When you stake FCTR tokens, they are converted into locked veFCTR. You can stake your FCTR tokens [here](https://app.factor.fi/governance/staking).

More information regarding veFCTR can be found on [Staking and Governance](staking-and-governance.md).
{% endhint %}

<details>

<summary>veFCTR Price Formula</summary>

As veFCTR is minted with every FCTR staking transaction, the total supply of veFCTR is dependent on the staking duration which each staker selects. The longer the FCTR staking period, the more veFCTR is minted for the staker.&#x20;

Given this dynamic, the veFCTR price is a function of the veFCTR total supply whereby veFCTR total supply is always less than FCTR total supply:

$$veFCTR\_Price_{USD}=FCTR\_Price_{USD}\times\frac{FCTR\_Staked}{veFCTR\_Supply}$$

</details>

### esFCTR

The esFCTR (escrowed FCTR) tokens represent rewards that are vested or locked for a certain period within the Factor protocol. [Factor Scale](../factor-scale/) and [Factor Boost](../factor-boost/) rewards are emitted as esFCTR which can then be converted 1:1 to FCTR following a 90 day linear vesting schedule. Users are required to claim the underlying FCTR once the esFCTR vesting period is completed.

esFCTR minimizes short-term speculation as it is programmed to be non-transferable for the duration of the vesting period. As reward beneficiaries remain vested for this duration, there are more incentives for them to continue participating to ensure the future of the protocol.
