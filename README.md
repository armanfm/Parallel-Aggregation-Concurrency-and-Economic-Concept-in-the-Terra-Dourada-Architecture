# Terra Dourada Architecture: Parallel Aggregation, Concurrency, and Reference Semaphore

**1) Specialized Mini-Rollups**

- Each data type has its own mini-rollup: user, transaction, vote, etc.
- Each mini-rollup processes independent batches of its data type.
- **Competitive Provers**: multiple provers compete in parallel to process the same batch; the first to submit a valid proof wins.
- Provers that fail or miss the deadline are moved to the end of the queue and can try again.

**This competition reduces latency and increases throughput of mini-rollups.**

**Economy and Energy Efficiency**:
- Specialized mini-rollup computers consume much less energy than traditional Bitcoin miners (e.g., 500–1000W vs. 5000–10000W for a powerful miner).
- Simpler, cheaper machines can participate, making the ecosystem more accessible and democratic.
- This reduces hardware and energy costs, enhancing the system’s sustainability.

**2) Synchronization and Sequencing via Reference Semaphore**

- A **smart contract acts as a reference semaphore**, not as a micro-managing controller.
- Provers submit their batch commits to the semaphore.
- It **does not collect** or **guarantee order** directly; it only publishes a batchId that everyone agrees to use as a sequence reference.
- The order **emerges naturally** from consensus around the reference semaphore.
- The semaphore can signal (via events) that a batchId has received commits from all expected mini-rollups, but it is up to the zk-rollup principal prover to decide whether to act on that signal.

**3) Main zk-Rollup with Continuous Pipeline**

- The main zk-rollup aggregates results from all mini-rollups of the finalized set.
- **Competitive provers** also apply here, attempting to generate the final ZK proof of the batch.
- The first prover to submit a valid proof finalizes the aggregated batch.
- While the ZK proof of the current batch is being verified (which may take a few seconds), another prover can start aggregating the next set of mini-rollups, keeping the pipeline continuously active.

**4) Model Benefits**

- **Maximum Throughput**: parallel mini-rollups + concurrency in the main zk-rollup keeps the network fully utilized.
- **Reduced Latency**: multiple competing provers decrease the average time to complete each batch.
- **Security and Robustness**: dynamic queue + slashing ensures failing provers do not compromise the sequence.
- **Guaranteed Sequence**: the reference semaphore ensures data is delivered to the main zk-rollup and consuming contracts in the correct order.
- **Accessibility and Economy**: low hardware and energy costs make the ecosystem democratic, allowing anyone to participate as a prover, creating a more inclusive and sustainable network.

**5) Visual Summary (Concept)**

- Specialized mini-rollups processing batches in parallel → competitive and energy-efficient provers.
- Smart contract **acts as a reference semaphore** to synchronize all mini-rollups of a set.
- Main zk-rollup aggregates the set → prover competition for final proof submission.
- Continuous pipeline → while a ZK proof is being verified, the next batch can already begin aggregation.

