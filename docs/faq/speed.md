# Speed

## Maximum throughput

Current zkSync transaction throughput has been benchmarked to reach 300 TPS (transactions per second). This number will grow to 1000 TPS as soon as Ethereum Berlin network upgrade is activated, which includes BLS12-381 elliptic curve precompile and enables larger zkSync blocks.

At the same time we are working on fully integrating the [RedShift](https://eprint.iacr.org/2019/1400) support into the bellman prover (expected completion in Q3 2020). Once this is done (regardless of the Berlin upgrade status), the only bottleneck for zkSync scalability will be Ethereum's block size capacity which zkSync uses to publish its state ∆ updates. Current benchmarks of the gas consumption suggest the upper bound of 3500 TPS with RedShift.

It should be noted that zkSync node infrastructure has been benchmarked to support >7000 TPS.

## Transaction finality

Transactions in **zkSync** reach the finality of Ethereum once the SNARK proof of zkSync block is generated accepted by the smart contract. The proof time generation is expected to be ~10 min, i.e. after 10 minutes, the zkSync transaction is as final as any L1 Ethereum tx included in the same Ethereum block as the zkSync verification tx.

In contrast, fraud-based scaling solutions (e.g. optimistic rollup) require at least 2 weeks of lockout period to operate more or less securely, which results in 2 weeks objective<sup>\*</sup> tx finality time.

It should be added that Matter Labs and other companies in the ZKP space are constantly working on improving the prover efficiency, which will result in lower finality times (potentially down to under 1 min).

<span class="footnote"><sup>*</sup> Subjective finality time can be shorter for optimistic rollup users who validate every tx themselves, but this would defeat the purpose of optimistic rollup as a scaling solution.</span>

## Instant confirmations

- Instant promise in the UI for now (to be backed by security bond)
- Finality on ETH mainnet after the ZKP is generated and mined on ethereum (~10-15 min)
- explain block filling timeout (timeout of 15 min)
- in the future we will add instant confirmations with guarantee (check out zkSync intro)

## What if Ethereum is congested?

Periodically, extrordinary events lead to very high levels of congestion on the Ethereum network (notable examples are [Cryptokitties crisis](https://media.consensys.net/the-inside-story-of-the-cryptokitties-congestion-crisis-499b35d119cc) or the [Shanghai DOS attack](https://blog.ethereum.org/2016/09/22/ethereum-network-currently-undergoing-dos-attack/)). During such peak load times, gas prices skyrocket and it might become prohibitatively expensive to move crypto assets, rendering some services unoperational or preventing arbitrage opportunities.

Moreover, some systems can generally fail in the extreme circumstances, leading to cascading failures (the recent [DeFi Black Thursday](https://forklog.media/black-thursday-for-defi-wounds-to-lick-and-lessons-to-learn/) is an excellent example). This is especially worrisome for fraud-proof-based scaling solutions (payment channels, optimistic rollups), because there is a risk that their automated security bots won't be able to get their fraud-proof transactions mined in case of an attack during high-congestion, thus jeopardizing the security of all assets under control of such systems. What makes the problem for these systems worse, you can never know until the situation occurs (just like [it happened](https://medium.com/dragonfly-research/daos-ex-machina-an-in-depth-timeline-of-makers-recent-crisis-66d2ae39dd65) for Maker's liquidation bot).

In contrast, **zkSync** is positioned exceptionally well to thrive in a high-congestion environment.

First and foremost, a congested network (just like as a targeted DOS attack) can never create any threat to assets in zkSync. Any movement of funds within or to outside of zkSync requires a zero-knowledge proof of validity, and it's simply unaffected by the transactability on L1 in any way.

Second, the normal operation of **zkSync** is also unlikely to be disrupted, even for smaller amounts. The operators node is configured to automatically increase the gas price to over-the-average level in order to get zkSync blocks mined with high priority. Since the on-chain costs per transaction are ~1/100th of the cost of corresponsing plain transaction on the L1, zkSync users will be least affected.