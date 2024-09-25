# Flash Loan

## Overview

The [Flash Loan Building Block](../../../factor-building-blocks/flash-loan/) functions as an automation and composability layer between the flash loan request and multiple integrated lending protocols. With the Flash Loan Building Block, strategies can easily source the capital required to fund an endless variety of multi-token strategies.

## Actions

<figure><img src="../../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

1. **Debt Token:** Select the token to flash loan by searching via token symbol or name. The tokens available for flash loans are determined by the underlying flash loan protocol. Tokens borrowed will be charged a fixed per block interest.
2. **Borrow Amount:** The number of debt tokens to borrow from the selected flash loan market. This will have to be paid back with interest within the same block.
3. **Protocol:** Select the underlying flash loan protocol to borrow from.
4. **Flash Loan Strategy**: Add additional building blocks to your flash loan that will enable the flash loan to be paid back within the same block.
