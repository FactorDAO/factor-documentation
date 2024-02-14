# Looping

## Overview

Looping enables users to amplify their exposure to a particular token through taking out multiple recursive loans. By taking out a loan against a collateral asset, borrowers are able to access additional liquidity equal to that of their specified collateral ratio. This loan can then be used to purchase more of the collateral asset with the process repeating perpetually.&#x20;

## Example

Alice has USD1,000 worth of ETH and is bullish on ETH. She decides to take out a USDT loan against her ETH so that she can purchase even more ETH. Alice is comfortable with a 50% collateralization ratio.

* Alice deposits her USD1,000 worth of ETH into the lending contract.&#x20;
* Based on a 50% collateralization ratio, Alice is able to borrow an additional 500USDT (assume the value of 1USDT = value of 1USD).
* Alice uses the 500USDT to purchase more ETH which she then takes out a new loan worth USD500.
* Based on a 50% collateralization ratio, Alice is able to borrow an additional 250USDT.

By repeating the above steps, Alice is constantly able to increase her ETH holdings up to a total value that is constrained by her initial collateralization ratio. In the above scenario, if Alice decides to repeat the process ad infinitum, she would have acquired \~USD2,000 (1,000+500+250+125+62.5+...) worth of ETH from an initial deposit worth USD1,000. This results in 2x the leverage if she had just held the initial ETH instead.

The iterative process above is what is known as looping.

## One Click Looping

While looping enabled access to significantly more liquidity, this repetitive process required a significant amount of time and gas to be implemented manually. Moreover, as market conditions could change during the looping process, users were also exposed to significant liquidation risks if they were unable to respond fast enough to the changes. Note that loan refinancing required each step of the looping process to be handled transaction by transaction.

One Click Looping automates the manual looping process by chaining together multiple loan actions into a single transaction. Instead of having to manually confirm each loan, One Click Looping enables users to specify their desired leverage and the code handles the recursive process of creating multiple loan positions. Critically, as this is done in a single transaction, market volatility risks are significantly reduced as users are able to adjust their collateralization ratios quickly and efficiently.
