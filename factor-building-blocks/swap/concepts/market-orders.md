# Market Orders

## Overview

A Market Order is an instruction to trade an asset at the best available price given current market conditions. Market Orders prioritizes settlement immediacy in favor of price predictability. This is because market conditions are constantly changing as buyers and sellers continuously adjusts their expectations based on the latest available data. As such, where immediate trades are required, the final settlement price of the trade can only be known after trade execution.

Market Orders are exposed to slippage risks whereby the expected price and executed price for an order can differ depending on the market conditions. As there is always a certain amount of time between order placement and order execution, there is a possibility that market conditions might have changed during this short interval. By extension, slippage risks are also higher during periods of relative market volatility whereby asset prices tend to change more rapidly.

The extent of slippage for a Market Order is dependent on the available liquidity for the particular swap pair. Commonly traded tokens will usually have greater market depth as market makers are able to profit from the constant trade volume being generated. On the other hand, there is a higher liquidity premium for exotic token swaps as there are less opportunities for market makers to earn a profit from arbitrageurs.

Market Orders enable instant trade execution at the expense of price predictability. Traders can minimize their Market Order risks by utilizing [DEX Aggregators](dex-aggregators.md) which have been integrated with the Swap Building Block.
