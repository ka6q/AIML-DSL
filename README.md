# AIML-DSL

## Transpiler enables Federated Polyglot AI/ML - Low Latency at World-Wide Scale.

One of the requirements of AI/ML online fraud detection is to be able to return scores within 10 to 30ms per transaction, with very tight P99 distributions. The workload is a given fraction of the total transaction traffic (For example, credit-card networks are engineered for 24,000 transactions per sec total).

The challenge is further complicated by the fact that many ML models require computation of Features over large windows of time, eg. aggregates over as much as 90 days. Transaction logs over such large windows can approach petabyte scale. This makes both CPU time and RAM for in-memory databases unaffordable. Further, unlike the approach in Google's "Tail at Scale"[1], fintech transactions are not idempotent, and serialization matters; hence computations cannot be hedged to control latency tail.

A better solution would process transactions with lower latency, and also enable updating ML models in weeks instead of months. This can help reduce enumeration attacks which are responsible for more than $1.1 billion annually in fraud losses globally.[2]

Therefore some form of extreme optimization is essential; we need to somehow blend together inexpensive high-throughput batch pre-computation with low-latency real-time computation, and orchestrate this combination such that it is both data-parallel and computataion-parallel.

One traditional workaround is a cop-out which reduces model quality, where real-time aggregates are computed only over the most recent hour or few, in a main-memory database, eg. Redis. Separate batch jobs provide uncorrelated long term aggregates over weeks. This has numerous problems: (1) Time-discontinuities between batch and real-time clusters cause some transactions to be missed by ML, (2) Inability to synthesize long-term and short-term Features together result in AI/ML missing insights about fraud, (3) Overlapping GroupBy's mean sharding is not easily scalable, hot-spots are common.

Not coincidentally, perpetrators of credit-card fraud3 exploit these very gaps. We need better solutions: better AI/ML platform which can deploy GenAI or traditional ML models to low-latency production and do so with very short update cycles, and with 100% guaranteed correctness.

[1] [The Tail at Scale, Jeffrey Dean, Luiz Andr, Communications of the ACM, 56 (2013), pp. 74-80](https://dl.acm.org/doi/10.1145/2408776.2408794)

[2] [Visa Announces Generative AI-Powered Fraud Solution to Combat Account Attacks](https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.20661.html)

