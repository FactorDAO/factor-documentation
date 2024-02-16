# Flash Loan

## Overview

Flash loans enable trustless [uncollateralized lending](uncollateralized-lending-and-borrowing.md) of crypto assets which are created and paid back within a single block. Unlike loans based on a [credit system](uncollateralized-lending-and-borrowing.md#introduction-of-credit), flash loans facilitate instantaneous uncollateralized loans without the lender facing any default risks. This is made possible due to the nature of transaction finality on the blockchain.

Flash loans are usually utilized in the context of a multi-step transaction whereby the loan provides the initial capital required to realize the end-to-end transaction. In other words, flash loans are usually batched together with other trading strategies into a single transaction which is then processed by the network. As such, flash loans are only executed if the end-to-end transaction succeeds else a loan is never initiated in the first place (i.e. atomic execution).

## How It Works

Flash loan protocols create a market for such loans by:

* Incentivizing lenders to deposit their tokens into a smart contract in return for yields generated through flash loan interests
* Letting borrowers initiate a flash loan from the pool with the repayment terms (i.e. interest per block) specified in the smart contract

What follows below is a simplified example from the perspective of the borrower:

1. Borrower identifies an opportunity for arbitrage on ETH/USDC pair. Market A is selling ETH at 2,750USDC while Market B is buying ETH at 2,800USDC.
2. Borrower wants to arbitrage without using their own funds hence decides to use a USDC flash loan. USDC flash loan lenders are charging 0.5% interest.
3. Borrower constructs a transaction with the following steps:
   1. Take out a flash loan for 100,000USDC
   2. Swap 100,000USDC for 36.36ETH on Market A (1ETH:2,750USDC)
   3. Sell the purchased 36.36ETH for 101,818USDC on Market B (1ETH:2,800USDC)
   4. Pay back the flash loan with interest totalling 100,500USDC
   5. Pocket the 1,318USDC  difference between arbitrage profit and flash loan interest (i.e. 1,818USDC - 500USDC)
4. Borrower executes the transaction on the blockchain.
5. The blockchain executes the transaction and checks the validity of each step. If any of the steps in the transaction fails, the whole transaction is failed (i.e. as if it was never executed in the first place)

As blockchain transaction is atomic, lenders do not face any default risk as the loan must be created and repaid in the same block. Consequently, borrowers are also able to access practically unlimited capital as long as their trading strategy proves to be successful.

Note that the above example has been simplified for readability. Strategies involving flash loans will also have to take into account market volatility/liquidity as well as more fine-grained configurations such as slippage, price impact, etc.
