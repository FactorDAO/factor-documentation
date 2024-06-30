# PT Strategies

{% hint style="info" %}
**Pendle Yield Tokenization**

PT Strategies refer to DeFi strategies which utilize [Pendle's Principal Token](https://docs.pendle.finance/ProtocolMechanics/YieldTokenization/PT) (i.e. PT). Through splitting yield-bearing assets into various tokens, Pendle enables users to earn a fixed yield by holding Principal Tokens till maturity or speculate on the variable yields through trading Yield Tokens.

Please visit [Pendle Docs](https://docs.pendle.finance/Introduction) for further info on the yield tokenization mechanics.
{% endhint %}

## PT Overview

Pendle's [Principal Token](https://docs.pendle.finance/ProtocolMechanics/YieldTokenization/PT) (PT) enables users to earn a fixed yield by holding the newly acquired PT until the stated maturity date. This means that instead of worrying about changes in yield over time, users can lock in fixed returns at a specified future date by holding PT. **The fixed return is represented as a discount on PT** (i.e. locked in at acquisition) which enables holders to claim the accounting asset at a 1:1 ratio on the maturity date.

The example below provides an intuitive understanding of PT returns for different yield token types:

{% tabs %}
{% tab title="Interest-Bearing" %}
_Yields from interest-bearing assets are realized as an increase in the **value** of the token._

1. Bloxy has 1 [weETH](https://etherfi.gitbook.io/etherfi/ether.fi-whitepaper/eth-re-staking) which represents 1 restaked ETH that is earning both Ethereum Mainnet PoS rewards and ETH restaking yields.
2. At the beginning of the year (i.e. 01JAN2023) Bloxy exchanges 1 weETH for 1.1 PT-weETH-01JAN2024 which matures at the beginning of the next year (i.e. 01JAN2024).
3. By holding 1.1 PT-weETH-01JAN2024 until maturity (i.e. 1 Jan 2024), Bloxy is able to redeem 1.1 ETH worth of PT-weETH at the stated date.
{% endtab %}

{% tab title="Rebasing" %}
_Yields from rebasing tokens are realized as an increase in the total **number** of tokens held._

1. Bloxy has 1 [stETH](https://help.lido.fi/en/articles/5230610-what-is-steth) which represents a share of ETH that is staked via Lido (i.e. staked ETH and staking rewards).
2. At the beginning of the year (i.e. 01JAN2023) Bloxy exchanges 1 stETH for 1.1 PT-stETH-01JAN2024 which matures at the beginning of the next year (i.e. 01JAN2024).
3. By holding until maturity (i.e. 1 Jan 2024), Bloxy is able to redeem 1.1 PT-stETH-01JAN2024 for 1.1 stETH at the stated date.
{% endtab %}
{% endtabs %}

The discounted PT in step 2 above comes about due to:

* **Opportunity Costs:** To get the indicated returns at the point of exchanging TKN for PT-TKN, users must hold PT until maturity.&#x20;
* **Price Of Certainty:** PT holders are selling their claim to any upside in yields whereby the yields accrued by the underlying asset are still liable to change as it is traded on the open market.

In effect, PT holders are going short (i.e. bearish) on the yield portion of the yield-bearing asset. In other words, **PT holders expect that the amount of yield generated until maturity will be less than the discount received when exchanging TKN for PT-TKN**.&#x20;

If 1 PT-TKN enables you to claim 1.1TKN at the maturity date, exchanging your TKN for PT-TKN means that you expect the total yield accrued during the maturity period to be less than 0.1TKN. Additionally, you can hold PT-TKN to ensure that you get a fixed 0.1TKN return at maturity and not have to worry about yield fluctuations for that period.

{% hint style="success" %}
**Get Started With PT Strategies!**

You can visit our [PT User Guides](../../../solutions/studio-discover/pt-user-guides/) if you would like to get started with amplified PT yields.
{% endhint %}

## PT Strategies

Strategies utilizing PT takes advantage of the fixed income nature of PT whereby the value of a PT-TKN is always approaching that of its accounting asset at maturity date. To see why this is the case, remember that PT-TKN can be redeemed 1:1 for the accounting asset (i.e. TKN) on maturity.&#x20;

The above means that the PT-TKN discount declines towards zero on maturity as the yield portion of the yield-bearing asset (i.e. YT) becomes increasingly insignificant. In other words, **the shorter the time to maturity, the less time there is for yield to accrue hence the lower the PT discount**. This is why PT with longer maturity periods are able to command higher fixed APYs (in addition to having a longer holding period).

It is critical to note that TKN to PT-TKN swaps can also happen in reverse as Pendle provides a [market](https://app.pendle.finance/trade/markets) for trading of all the tokenized yield equivalents. Consequently, the price of TKN:PT-TKN is dependent on the current market conditions (i.e. do yield traders believe that the yield accrued by TKN until the maturity date is more or less than the current discount).

{% hint style="info" %}
**PT Fixed APYs**

As a PT holder that has no intention to trade, the most important thing to note is that **the expected fixed return from holding PT is only realized as real returns on the maturity date**. While PT can be traded, it does not accrue any yield and only allows redemption of the accounting asset on maturity.

Consequently, **the expected returns is "locked in" based on when TKN was swapped for PT-TKN**.
{% endhint %}

### PT Leverage Strategies

By lending PT-TKN and borrowing TKN (i.e. Long PT), the fixed income nature of PT ensures that **the value of the collateral (i.e. PT-TKN) is always increasing relative to debt (i.e. TKN)**. Barring any black swan events, this ensures that the position never becomes undercollateralized.

The additional TKNs borrowed can then be swapped for more PT-TKN and supplied to the lending pool thereby increasing exposure to the PT's fixed returns on maturity (i.e. you are holding more PT based on the initial portfolio value). This process can be repeated with the fixed returns being "locked in" with each TKN to PT-TKN swap.

{% hint style="success" %}
**Leverage Strategies Explained**

Please view our [Leverage Strategy Explainer](../leverage/) if you would like a deeper dive into the design of the standard leverage strategy.
{% endhint %}

To ensure a sustainable lending and borrowing market, lending pools specify both a Supply APY and Borrow APY. PT-TKN supplied will earn a Supply APY while TKN borrowed will incur a Borrow APY. As a PT leverage strategy depositor, the Borrow APY is the cost of maintaining your leveraged exposure to PT-TKN.&#x20;

**As PT returns are only realized on maturity, any changes to your leveraged position before the maturity date will have varying effects based on the market conditions.** For example, removing your leverage results in your PT-TKNs being sold at the current market price which can be either higher if yields have been increasing since you initially acquired PT or less if yields have been decreasing.

Due to the inherent complexity with managing PT strategies, it is recommended that the PT leveraged position be held until maturity to realize the fixed returns. Leveraged PT strategies are profitable as long as the Fixed APY at which you acquired PT is greater than the average Borrow APY during the maturity period.

{% hint style="warning" %}
**Look Out For:**

* [x] Fixed returns are only realized on maturity.
* [x] Your expected returns are fixed at the point of leverage creation.
* [x] Borrowing costs can change throughout the maturity period.
* [x] Changes to your position will sell your existing position on the open market (i.e. profit/loss is dependent on the market).
* [x] Position adjustments will result in PT being acquired at the current market fixed APY.
{% endhint %}

### PT Yield Strategies

Auto-compounding strategies take advantage of yield farming rewards which are provided to PT holders. To incentivize adoption of PT, protocols will provide additional rewards which are external to PT performance. This includes the claiming of governance tokens as well as liquidity incentive tokens.

{% hint style="success" %}
**Yield Strategies Explained**

Please view our [Yield Strategy Explainer](../) if you would like a deeper dive into how yields can be auto-compounded.
{% endhint %}

PT yield strategies forego any trading risks and instead enable you to grow your initial PT holdings by regularly harvesting all accrued rewards and swapping for more PT. By automating this harvest and swap routine, your rewards can be compounded as you gain incrementally more PT with each cycle.

Auto-compounding immediately swaps all available rewards for PT at each execution cycle hence the amount of PT acquired will be dependent on the market conditions. Critically, **as PT rewards are only realized at maturity, each subsequent PT swap will have gradually less discount as it gets closer to maturity**. Put simply, your newly acquire PT fixed returns will generally reduce with every compounding cycle.

PT yield strategies are a good way to increase your fixed returns without any downside risks as compared to just holding your initial PT amount. Moreover, by consistently swapping your accrued reward tokens for PT, you reduce your reward token exposure risks due to the reduced reward token holding times.

{% hint style="warning" %}
**Look Out For:**

* [x] Decrementing fixed returns for PT with every subsequent auto-compound cycle.
* [x] Changes in the price of reward tokens relative to PT.
{% endhint %}
