# Parallel Aggregation, Concurrency, and Economic Concept in the Terra Dourada Architecture

## 1) Specialized Mini-Rollups

- Each data type has its own **mini-rollup**: **user, transaction, vote, etc.**
- Each mini-rollup processes **independent batches** of its data type.
- **Competitive Provers:** Multiple provers compete in parallel to process the same batch; the **first to submit a valid proof wins**.
- Provers who **fail or do not arrive on time** are moved to the **end of the queue** and can try again.
- This competition **reduces latency**, increasing the **throughput** of mini-rollups.

**💡 Economy and Energy Efficiency:**
- Specialized computers for mini-rollups consume **significantly less energy** than traditional Bitcoin miners (e.g., **500–1000W vs. 5000–10000W** for a powerful miner).
- **Smaller and cheaper machines** can participate, making the ecosystem more **accessible and democratic**, allowing ordinary users to act as provers.
- This reduces **hardware and energy costs**, strengthening the system’s **sustainability**.

---

## 2) Synchronization and Sequencing

- An **orchestration smart contract** ensures that all mini-rollups in the same dataset (e.g., **user + vote + transaction**) are **collected in the same sequence** before being aggregated by the **main zk-rollup**.
- This ensures that consumer contracts receive the data in the **correct order**.

---

## 3) Main zk-Rollup with Continuous Pipeline

- The **main zk-rollup** aggregates the results of all finalized mini-rollups.
- Like mini-rollups, the aggregation can have **competitive provers**, allowing multiple provers to attempt generating the **final ZK proof** for the batch.
- The **first prover to submit a valid proof finalizes the aggregated batch**.
- While the ZK proof of the current batch is being verified (which may take a few seconds), **another prover can already start aggregating the next set of mini-rollups**, keeping the pipeline **continuously active**.

---

## 4) Model Benefits

- **Maximum Throughput:** Parallel mini-rollups + concurrency in the main zk-rollup keeps the network **constantly busy**.
- **Reduced Latency:** Multiple competitive provers lower the **average time** to complete each batch.
- **Security and Robustness:** Dynamic queue + **slashing** ensures that failing provers do not compromise sequencing.
- **Guaranteed Sequence:** The **synchronization smart contract** ensures data is delivered to the main zk-rollup and consumer contracts in the correct order.
- **Accessibility and Economy:** Low hardware cost and energy consumption make the ecosystem **democratic**, allowing any user to participate as a prover, creating a **more inclusive and sustainable network**.

---

## 5) Visual Summary (Concept)

- **Specialized mini-rollups** processing batches in parallel → **competitive provers & energy-efficient**.
- **Smart contract** synchronizes the collection of all mini-rollups in a set.
- **Main zk-rollup** aggregates the set → **prover competition for final proof submission**.
- **Continuous pipeline** → While the ZK proof is being verified, the **next batch starts aggregation**.
