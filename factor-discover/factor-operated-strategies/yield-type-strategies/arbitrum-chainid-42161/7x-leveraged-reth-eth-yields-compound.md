# 7x Leveraged rETH:ETH Yields - Compound

{% hint style="success" %}
Visit Discover to deposit into this strategy and automate your yields!

:arrow\_right: [Strategy Link](https://pro.factor.fi/strategies/0x1DEe0BCf8C5Ea25bf6F4a50D8458A532B592bD06)
{% endhint %}

{% hint style="info" %}
Visit Studio to copy/fork and tweak this strategy!

:arrow\_right: [Strategy Builder Link](https://studio.factor.fi/?hash=0xdbe8f35df5f8376525ca9a908f457a9d4b8c0206f83593d072bbbfa007134d14)
{% endhint %}

## Description

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption><p><a href="https://studio.factor.fi/?hash=0xdbe8f35df5f8376525ca9a908f457a9d4b8c0206f83593d072bbbfa007134d14">https://studio.factor.fi/?hash=0xdbe8f35df5f8376525ca9a908f457a9d4b8c0206f83593d072bbbfa007134d14</a></p></figcaption></figure>

This vault creates 7x leveraged rETH:ETH position that earns 1x rETH liquid staking yields plus an additional 6x interest differential between rETH yields and WETH borrow costs.

Deposited rETH is supplied to Compound enabling the strategy to borrow WETH which is then swapped for more rETH. This process is repeated to get up to 7x leverage which provides a 5% liquidation buffer.

\+ rETH liquid staking yields

\+ COMP borrow rewards

\- ETH borrow interest

## Strategy

{% tabs %}
{% tab title="Main strategy" %}
1. Flash loan 6x the deposited $rETH amount
2. Lend all $rETH - Compound
3. Borrow $ETH to cover flash loan
4. Swap borrowed $ETH → $rETH
{% endtab %}

{% tab title="Exit Strategy" %}
1. Flash loan $ETH
2. Repay $ETH debt - Compound
3. Withdraw $rETH collateral - Compound
4. Swap $rETH → $ETH
{% endtab %}
{% endtabs %}

## Protocol Parameters

{% tabs %}
{% tab title="Compound" %}
* [0.64%](https://app.compound.finance/markets/weth-arb) COMP Borrow Rewards
* [\~2.1%](https://app.compound.finance/markets/weth-arb) WETH Borrow Interest
* [90%](https://app.compound.finance/markets/weth-arb) rETH Max LTV
{% endtab %}

{% tab title="Rocket Pool" %}
* [\~2.64%](https://rocketpool.net/) rETH Liquid Staking Yields
{% endtab %}

{% tab title="OpenOcean" %}
* 0.1% Max Slippage Config
{% endtab %}
{% endtabs %}

## Strategy Performance Conditions

{% tabs %}
{% tab title="Profit" %}
* rETH continuously increases in value vs WETH.
* WETH borrow cost is less than rETH liquid staking yields plus COMP rewards
{% endtab %}

{% tab title="Loss" %}
* rETH depegs from ETH.
* rETH liquid staking yields falls below WETH borrow costs.
{% endtab %}
{% endtabs %}

## Calculation Template

{% hint style="success" %}
**Create Your Own Strategies!**

Create a copy of the sheet below and tweak it to create your own personalized strategy.
{% endhint %}

{% embed url="https://docs.google.com/spreadsheets/d/1U9BOVhKlBRGiFNLfUZ-iSgZ--4X6zcQtGrwyL0VBmfQ/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/1U9BOVhKlBRGiFNLfUZ-iSgZ--4X6zcQtGrwyL0VBmfQ/edit?usp=sharing](https://docs.google.com/spreadsheets/d/1U9BOVhKlBRGiFNLfUZ-iSgZ--4X6zcQtGrwyL0VBmfQ/edit?usp=sharing)
{% endembed %}

## Estimated Returns

{% embed url="https://docs.google.com/spreadsheets/d/13qmV6QWLkjo2T-f2s4P_HHsQuw4LU-XeY-0Qz7lHJ5U/edit?usp=sharing" %}
[https://docs.google.com/spreadsheets/d/13qmV6QWLkjo2T-f2s4P\_HHsQuw4LU-XeY-0Qz7lHJ5U/edit?usp=sharing](https://docs.google.com/spreadsheets/d/13qmV6QWLkjo2T-f2s4P_HHsQuw4LU-XeY-0Qz7lHJ5U/edit?usp=sharing)
{% endembed %}
