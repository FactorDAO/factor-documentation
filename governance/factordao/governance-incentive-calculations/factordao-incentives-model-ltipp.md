# FactorDAO Incentives Model (LTIPP)

{% embed url="https://docs.google.com/spreadsheets/d/1kSCjsfm-RSiEhkvXZH8HmeszXhmAt4lFwsm71XwpqZk/edit?usp=sharing" fullWidth="true" %}

{% hint style="info" %}
**Try It Out!**

You can change the model parameters by making edits to the [Google Sheets](https://docs.google.com/spreadsheets/d/1iR8e7OmkbC8B8IzJcLUV5tderOvxkrx6h0eaRJeC4D0/edit?usp=sharing).
{% endhint %}

## Usage Overview

* Please update the cells with the thick borders based on our own parameters:
  * **Starting Capital** -> The USD value of tokens that will be utilized on Factor.
  * **Governance Allocation %** -> What percentage of the starting capital is used for staking via the [Factor dapp](https://app.factor.fi/governance).
  * **ARB Price** -> The ARB token price which can be sourced from external sources such as [CoinGecko](https://www.coingecko.com/en/coins/arbitrum) or [CoinMarketCap](https://coinmarketcap.com/currencies/arbitrum/). Due to technical considerations, this value cannot be dynamically updated.
  * **Strategy APY** -> The expected APR for the Factor strategy that will be deposited into via the [Discover page](https://app.factor.fi/discover).
  * **Strategy TVL** -> The TVL of the strategy that will be deposited into. Can be sourced via the [Factor dapp strategy UI](https://app.factor.fi/discover).
  * **Bribed Strategy APR** -> The expected APR for bribing a strategy via the [votes page](https://app.factor.fi/incentives/scale).
* The majority of the other starting parameters are updated via an API call which is triggered on file open. The specifications for the API used can be found [here](../../../factor-sdk/rest-apis/utility-apis/stats.md#factordao-revenues).

## Notes

* The numbers above are approximate and are meant to provide users with an intuitive feel of governance value flows.
* The calculations do not take into account the [emissions multiplier](../../factor-scale/emission-multiplier-calculations.md) to aid with ease of understanding.
