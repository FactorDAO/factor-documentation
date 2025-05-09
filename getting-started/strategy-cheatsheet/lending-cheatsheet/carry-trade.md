# Carry Trade

## Overview

<figure><img src="../../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

Pocket the interest difference between two lending markets by creating a carry trade. Carry trade opportunities arise when the interest charged on borrows is lower than the supply interest on another market.

While carry trades can be created between varying token lending markets by swapping the borrowed tokens, this also introduces the risk of token price divergences. Due to generally lower carry trade interest differentials, it is recommended that the borrow and lending token is the same. Note that there might also be price fluctuation risks between the collateralized token and borrow token as well.

## Potential Alpha

* **Earn Yield Differentials:** Pocket the interest difference between various lending markets by borrowing low and lending high.
* **Debt vs Asset Divergence:** Borrow stables and lend out a bullish token to increase your asset to debt ratio. Alternatively lend stables and borrow a bearish token to reduce your debt burden.

## Strategy Building Blocks

{% hint style="success" %}
The building block order mirrors the Factor Studio UI and can be expanded for further strategy details and parameters.
{% endhint %}

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend initial collateral amount to earn supply interest.

</details>

<details>

<summary><a href="../../../factor-building-blocks/borrow.md"><strong>Borrow</strong></a></summary>

* Borrow the token where there is an interest differential between markets.
* Alternatively, borrow token with very low interest.

</details>

<details>

<summary><a href="../../../factor-building-blocks/swap/">Swap</a></summary>

* In cases where the borrow token differs from the target lend token, swap all of the borrowed token for the target token.

</details>

<details>

<summary><a href="../../../factor-building-blocks/lend.md"><strong>Lend</strong></a></summary>

* Lend all of the output tokens from the swap.

</details>

## Example

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
