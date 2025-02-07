---
id: <leave blank -- will be assigned by reviewers>
title: Empirical Study of Transaction Revert and MEV on L2s
team: Daniel Marzec, Fahim Ahmed
created: 2025-02-06
---

# Transaction Revert and MEV on L2s

As Ethereum rollups gain adoption, the dynamics of Maximum Extractable Value (MEV) on Layer-2 (L2) blockchains are evolving, creating new challenges and opportunities for arbitrageurs, liquidators, and sequencers. While L2 mempools are often encrypted and operate on a first-come, first-served basis, low gas fees make mempool spamming an attractive MEV extraction strategy.
In this research, we analyze the effectiveness of spam-based MEV strategies using empirical data from major rollups and DeFi protocols. Additionally, we evaluate how these strategies can be optimized with the revert protection mechanisms.

## Background and Problem Statement
The evolution of MEV extraction has undergone significant transformations, beginning with Ethereum’s early days. The introduction of MEV Boost mechanisms, followed by Proposer-Builder Separation (PBS), tranformed how MEV was captured on Ethereum, and now, with the rise of rollups, layer-2 (L2) blockchains, history appears to be repeating itself.

Rollups are gaining traction, reshaping transaction execution and settlement dynamics. However, MEV remains an inherent challenge, leading to what is often described as the MEV trilemma—where avoiding MEV extraction entirely is impossible.
The Dencun upgrade resulted in a significant reduction in gas fees on L2 and a surge in the transaction revert rate, indicating the ongoing evolution of MEV strategies. Although initially blob transactions were relatively inexpensive, their rising costs could pose new challenges for rollup scalability and MEV extraction strategies.

Looking ahead, major developments such as Unichain with the proposed sequencer-builder separation, MEV tax and revert protection mechanisms could introduce new paradigms for MEV extraction on L2s. 

This research explores these developments, analyzing the reverted transaction on L2s with the goal to attribute them to the MEV extraction strategies. In particular, the research questions are:
1) How do reverted transactions correlate with different MEV strategies/taxonomy, such as atomic and non-atomic arbitrage, liquidations, and other forms of extraction? What patterns can be identified in user behavior related to reverted transactions?
2) What is the scale of spam-based MEV extraction on Ethereum rollups, based on empirical analysis of reverted transactions? How does spam-based MEV profitability compare across different L2 solutions and DeFi protocols?
3)  What is can be the impact of revert protection on these MEV strategies, rollup economics, and L1 consensus mechanisms, particularly in relation to blob pricing?

## Plan and Deliverables
This study analyzes reverted transaction data and swap data from major Ethereum rollups, including Arbitrum, Base, and Optimism (optimistic rollups), as well as ZKsync Era (a ZK-rollup).

The dataset is sourced from blockchain archive nodes provided by [to be decided]~\cite{x}. The analyzed swaps, transactions, and block ranges are detailed in Table~\ref{tab:dataset}. Using event logs from the \emph{Swap} method, historical spot prices and liquidity levels within liquidity pools are recalculated. For Uniswap~v3, the spot price after a swap is extracted from the \textit{sqrtPriceX96} field in the event logs. Market data for the ETH-USDC exchange rate on centralized exchanges (CEXs) is obtained from Binance APIs~\cite{Binance_API}.  
To analyze MEV-related strategies, we employ a matching approach that links failed transactions to subsequent successful ones. When a transaction succeeds, event logs from Uniswap, Aave or other DeFi protocols can be accessed, allowing for the extraction of exact parameters and the calculation of the profitability of the executed strategy. The process for each rollup follows these steps:

1) Identify all reverted transactions and group them by destination address.
2) Determine the most frequently used destination addresses, such as Uniswap pools and Aave pools.
3) Identify the primary senders of these transactions.
4) Locate successful transactions originating from the same senders within the relevant DeFi pools and extract the corresponding event logs (as event logs are not available for reverted transactions).
5) Assess the profitability of the identified strategy, determining whether the transactions are linked to MEV extraction.

Timeline:

- Month 1: Data Gatering and Parsin
- Month 2: Data anaysis, analysis per protocols
- Month 1-2: Writing the findings

Delivaratbles:
Python lirbary that explorts this
Flashbots article
Academic papers (to be submited to one of the peer-reviwed conferences)

## References
- Adams, H., Toda, M., Karys, A., Wan, X., Gretzke, D., Zhong, E., Wong, Z., Marzec, D., Miller, R., Hasu, & Floersch, K., & Robinson, D. (2024). Unichain Whitepaper. https://docs.unichain.org/whitepaper.pdf
- Zhu, B. Z., Wan, X., Moallemi, C. C., Robinson, D., & Bachu, B. (2024). Quantifying the Value of Revert Protection. arXiv. https://arxiv.org/abs/2410.19106
- Flaashbots Post (2024). It’s time to talk about L2 MEV. https://collective.flashbots.net/t/it-s-time-to-talk-about-l2-mev/3593/1
- Flashbots Dune Dashboard. Multichain Transaction Reverts. https://dune.com/flashbots/multichain-transaction-reverts
