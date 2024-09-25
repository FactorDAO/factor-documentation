# Lend

## Overview

The [Lend Building Block](../../../factor-building-blocks/lend.md) functions as an automation and composability layer between the deposit request and multiple integrated lending protocols. With the Lend Building Block, strategies can easily generate yield while simultaneously increasing the capital efficiency for an endless variety of multi-token strategies.

## Actions

<figure><img src="../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

1. **Lend All:** Based on the lending market selected, Studio will lend all of the relevant tokens in the vault to the market if this option is selected.
2. **Asset Token:** Select the token to lend by searching via token symbol or name. This is the token that will earn supply interest and can be collateralized to enable borrowing.
3. **Lending Amount:** The number of asset tokens to be supplied to the selected lending market.
4. **Protocol:** Select the underlying lending protocol to which your assets will be supplied to.
5. **Lending Market:** Lending protocols may implement isolated lending markets which limits risk exposure by combining various token combinations. Each market will have their own allowable tokens and rates.
