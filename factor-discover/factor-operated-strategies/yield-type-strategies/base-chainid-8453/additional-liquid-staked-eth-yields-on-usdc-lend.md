# Additional Liquid Staked ETH Yields On USDC Lend

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Link](https://pro.factor.fi/strategies/0x5F25Ba28239E59a8a835521aba067f06462Ee345)
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:arrow\_right: [Strategy Builder Link](https://studio.factor.fi/?hash=0x2b26a8bf684f160582c14a78293fe2ca16003d6d982864171d735cba3f749978)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/image (77).png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0x2b26a8bf684f160582c14a78293fe2ca16003d6d982864171d735cba3f749978">https://studio.factor.fi/?hash=0x2b26a8bf684f160582c14a78293fe2ca16003d6d982864171d735cba3f749978</a></p></figcaption></figure>

This strategy earns USDC lending interest on Aave and borrows ETH to generate additional ETH liquid staking yields.

By swapping borrowed ETH for cbETH & wstETH, this strategy earns the the difference between cbETH/wstETH liquid staking yields and ETH borrow interest. Liquid staking yields accrues natively to the liquid staked token and is reflected in cbETH/wstETH price always appreciating against ETH.

\+ USDC Lending Interest

\+ cbETH Liquid Staking Yields

\+ wstETH Liquid Staking Yields

\- ETH Borrow Interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Lend all $USDC - Aave
2. Borrow $WETH
   1. 62.5% of collateral value for 20% buffer
3. Swap 50% $WETH → $cbETH
4. Swap 50% $WETH → $wstETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Swap $cbETH → $WETH
2. Swap $wstETH → $WETH
3. Repay $WETH debt - Aave
4. Withdraw $USDC collateral
5. Close remaining debt
6. Swap all to withdraw token
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Exit Strategy**

Factor Discover also enables Depositors to permissionlessly withdraw from any strategy at anytime via an Exit Strategy.

Visit our [Exit Strategy explainer](../../../../factor-studio/studio-pro/exit-strategy.md) to see how Factor Studio strategies can maximize returns while ensuring truly permissionless withdrawals.
{% endhint %}

## Protocol Parameters

{% tabs %}
{% tab title="Aave" %}
* [\~5.69%](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3) USDC Supply Interest
* [\~2.43%](https://app.aave.com/reserve-overview/?underlyingAsset=0x4200000000000000000000000000000000000006\&marketName=proto_base_v3) WETH Borrow Interest
* [75%](https://app.aave.com/reserve-overview/?underlyingAsset=0x833589fcd6edb6e08f4c7c32d4f71b54bda02913\&marketName=proto_base_v3) USDC Max LTV
{% endtab %}

{% tab title="Coinbase" %}
* [\~2.8%](https://www.coinbase.com/en-gb/earn/staking/coinbase-wrapped-staked-eth) cbETH Liquid Staking Yields
{% endtab %}

{% tab title="Lido" %}
* [\~2.8%](https://lido.fi/) Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* cbETH/wstETH continuously increases in value vs WETH.
* WETH borrow cost is less than cbETH/wstETH liquid staking yields.
* USDC supply interest is greater than the interest differentials between cbETH/wstETH yield and WETH borrow.
{% endtab %}

{% tab title="Loss" %}
* cbETH/wstETH depegs from ETH.
* cbETH/wstETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1ocolNRjOGwBULsJEOs5vKbk61K_krQ7yajVNYI9yLB4/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1ocolNRjOGwBULsJEOs5vKbk61K\_krQ7yajVNYI9yLB4/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1ocolNRjOGwBULsJEOs5vKbk61K_krQ7yajVNYI9yLB4/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/1lBNZxx69FLLQjuli6oLYUw6KpMdNTup_jii67r0zGyI/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1lBNZxx69FLLQjuli6oLYUw6KpMdNTup\_jii67r0zGyI/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1lBNZxx69FLLQjuli6oLYUw6KpMdNTup_jii67r0zGyI/edit?usp=sharing)
{% endembed %}
