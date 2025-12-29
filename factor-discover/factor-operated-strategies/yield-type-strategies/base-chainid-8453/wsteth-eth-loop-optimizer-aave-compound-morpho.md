# wstETH:ETH Loop Optimizer - Aave, Compound, Morpho

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:inbox\_tray:  [Strategy Deposit Link](https://pro.factor.fi/strategies/0xea11bc07cca5a11476a30cfaa1db5c6a5e578799)&#x20;
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:tools:  [Strategy Builder Link](https://studio.factor.fi/?hash=0x6ec39d4a8969d92c0e691baccd4ac7d25c61d457f84b475c706f8a1a7b11132c)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/wstETH_ETH Loop Optimizer-Overview.jpg" alt=""><figcaption></figcaption></figure>

This vault optimizes looped wstETH returns by constantly scanning for the lowest ETH borrow rates  across Aave, Compound, & Morpho wstETH:ETH markets.

By repeatedly borrowing WETH against wstETH when the borrow rates are low, the vault is able to multiply the interest differentials (i.e. yield carry). A wstETH:ETH Long position is created with a 2.5% liquidation buffer on the identified market.

Positions are migrated between markets with minimal price impact as only the portion of liquidity relating to the differing max loan-to-value ratios are swapped.

Any earned rewardsa are automatically compounded for more wstETH.

\+ wstETH liquid staking yields

\+ COMP borrow rewards

\- ETH borrow interest

## Strategy

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption><p><a href="https://studio.factor.fi/builder?hash=0xea11bc07cca5a11476a30cfaa1db5c6a5e578799">https://studio.factor.fi/builder?hash=0xea11bc07cca5a11476a30cfaa1db5c6a5e578799</a></p></figcaption></figure>

{% tabs %}
{% tab title="Main strategy" %}
1. Flash loan $WETH up to 16.1x (dependent on market)
2. Swap WETH → wstETH
3. Lend all $wstETH on market with lowest $ETH borrow
4. Borrow $ETH to cover flash loan
{% endtab %}

{% tab title="Exit Strategy" %}
1. Flash loan $ETH
2. Repay $ETH debt&#x20;
3. Withdraw $wstETH collateral
4. Swap $wstETH → $ETH
{% endtab %}

{% tab title="Refinance" %}
1. Flash loan $ETH
2. Repay all $ETH debt on current market
3. Withdraw all $wstETH on current market
4. Lend all $wstETH on target market
5. Borrow $ETH to repay flash loan
{% endtab %}
{% endtabs %}

## Protocol Parameters

{% tabs %}
{% tab title="Aave" %}
* [\~2.05%](https://app.aave.com/reserve-overview/?underlyingAsset=0x4200000000000000000000000000000000000006\&marketName=proto_base_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0xc1cba3fcea344f92d9239c08c0568f6f2f0ee452\&marketName=proto_base_v3) wstETH Max LTV
{% endtab %}

{% tab title="Compound" %}
* [\~0.28%](https://app.compound.finance/markets/weth-basemainnet) COMP Borrow Rewards
* [\~1,87%](https://app.compound.finance/markets/weth-basemainnet) WETH Borrow Interest
* [90%](https://app.compound.finance/markets/weth-arb) cbETH Max LTV
{% endtab %}

{% tab title="Morpho" %}
* [\~1.56%](https://app.aave.com/reserve-overview/?underlyingAsset=0x4200000000000000000000000000000000000006\&marketName=proto_base_v3) WETH Borrow Interest
* [96.5%](https://app.morpho.org/base/borrow?collateralAssetIdsFilter=62ae9a63-0395-4187-bf1b-8964970c262d\&loanAssetIdsFilter=25a68056-3541-4f4a-8b1c-f3dcf383638e) wstETH Max LTV
{% endtab %}

{% tab title="Lido" %}
* [\~2.5%](https://stake.lido.fi/) cbETH Liquid Staking Yield
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

<figure><img src="../../../../.gitbook/assets/wstETH_ETH Loop Optimizer-Risks vs Returns.jpg" alt=""><figcaption></figcaption></figure>

{% tabs %}
{% tab title="Profit" %}
* wstETH continuously increases in value vs WETH.
* WETH borrow cost is less than wstETH liquid staking yields
{% endtab %}

{% tab title="Loss" %}
* wstETH depegs from ETH.
* wstETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1rjcct3uyf9jqAZ8u8tDqNaio_7EZzbkoMFUO2rja1nA/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1rjcct3uyf9jqAZ8u8tDqNaio\_7EZzbkoMFUO2rja1nA/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1rjcct3uyf9jqAZ8u8tDqNaio_7EZzbkoMFUO2rja1nA/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/111hgqzIM5Eb-l8fZAIpEiTpLOUOTF8GkKMNywkomVjA/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/111hgqzIM5Eb-l8fZAIpEiTpLOUOTF8GkKMNywkomVjA/edit?usp=sharing](https://docs.google.com/spreadsheets/d/111hgqzIM5Eb-l8fZAIpEiTpLOUOTF8GkKMNywkomVjA/edit?usp=sharing)
{% endembed %}
