# Chapter 34: System Design & Distributed Systems

**Target:** 35 MCQs | **Distribution:** 9 Foundational, 14 Intermediate, 9 Advanced, 3 Expert

---

**Q34.1: Foundational - [Theory] - [CAP Theorem]**

The CAP theorem states that a distributed system can guarantee at most two of three properties. What are they?

A) Caching, Authentication, Performance
B) Consistency, Availability, Partition tolerance
C) Concurrency, Atomicity, Persistence
D) Compression, Aggregation, Parallelism

**Answer: B**

**Explanation:**
CAP (Brewer, 2000): Consistency (all nodes see same data), Availability (every request gets a response), Partition tolerance (system works despite network partitions). Since network partitions are inevitable in distributed systems, you must choose: CP (strong consistency, may be unavailable during partition — e.g., HBase, ZooKeeper) or AP (available but may serve stale data — e.g., Cassandra, DynamoDB).

---

**Q34.2: Foundational - [Theory] - [Consistent Hashing]**

In consistent hashing, when a new server is added to the ring, approximately what fraction of keys need to be remapped?

A) All keys
B) About 1/n (where n is the number of servers)
C) About n/2
D) None

**Answer: B**

**Explanation:**
Consistent hashing: servers and keys mapped to a ring. Each key assigned to the next server clockwise. Adding a server: only keys between the new server and its predecessor need to move — approximately K/n keys (K = total keys, n = servers). Regular hash (mod n): adding a server changes almost ALL key assignments. Virtual nodes improve balance further. Used in DynamoDB, Cassandra, CDNs.

---

**Q34.3: Intermediate - [Theory] - [Load Balancing]**

Which load balancing algorithm is most appropriate when servers have different processing capacities?

A) Round robin
B) Weighted round robin
C) Random
D) Least connections

**Answer: B**

**Explanation:**
Weighted round robin: assign weight proportional to each server's capacity. A server with weight 3 gets 3× more requests than weight 1. Simple round robin treats all servers equally — overloads weaker servers. Random is simple but unpredictable. Least connections adapts to current load but doesn't account for server capacity differences. Weighted algorithms explicitly handle heterogeneous hardware.

---

**Q34.4: Intermediate - [Theory] - [Sharding Strategy]**

Range-based sharding (e.g., A-M on shard 1, N-Z on shard 2) has what major disadvantage?

A) It doesn't support range queries
B) Hot spots — some ranges may receive disproportionately more traffic
C) It requires more network bandwidth
D) It can only handle numeric keys

**Answer: B**

**Explanation:**
Range sharding: sequential keys go to same shard. Pro: range queries are efficient (single shard). Con: uneven data/traffic distribution. If keys are timestamps: latest shard gets ALL writes (hot spot). If names: some letters more common than others. Hash-based sharding: distributes evenly but destroys key ordering (range queries span all shards). Hybrid approaches: hash-range or compound sharding keys balance both concerns.

---

**Q34.5: Foundational - [Theory] - [Caching]**

In a cache-aside (lazy loading) pattern, what happens on a cache miss?

A) The request fails and returns an error
B) The application reads from the database, then populates the cache
C) The cache automatically fetches from the database
D) The request is retried indefinitely

**Answer: B**

**Explanation:**
Cache-aside: application checks cache first. Miss: app reads from DB, stores result in cache, returns data. Hit: return cached data directly. Application manages cache explicitly. Alternatives: read-through (cache fetches from DB automatically), write-through (write to cache and DB simultaneously), write-behind (write to cache, async DB update). Cache-aside is simplest and most common (Redis + app code).

---

**Q34.6: Intermediate - [Theory] - [Consensus Algorithms]**

What problem does Raft/Paxos solve in distributed systems?

A) Load balancing across servers
B) Agreeing on a single value/leader even when some nodes fail
C) Encrypting communication between nodes
D) Compressing replicated data

**Answer: B**

**Explanation:**
Consensus: getting N distributed nodes to agree on a value/order despite failures. Raft: elects leader, leader replicates log to followers. Majority (quorum) must acknowledge. If leader fails: new election. Paxos: more general, harder to understand. Both tolerate up to ⌊(n-1)/2⌋ failures (majority survives). Used in: etcd (Raft), ZooKeeper (ZAB, Paxos-like), Google Spanner. Foundation of strongly consistent distributed systems.

---

**Q34.7: Advanced - [Theory] - [CRDTs]**

Conflict-free Replicated Data Types (CRDTs) achieve eventual consistency without coordination by:

A) Locking all replicas before writes
B) Designing data structures where all concurrent operations commute (order doesn't matter)
C) Using a single master node
D) Discarding conflicting writes

**Answer: B**

**Explanation:**
CRDTs: mathematically designed so concurrent updates always converge to the same state regardless of order received. G-Counter: each node has its own counter, merge = take max per node. G-Set: add-only set, merge = union. LWW-Register: last write wins by timestamp. No coordination needed → available under partition (AP). Trade-off: limited data types, can't do arbitrary operations. Used in Redis CRDT, Riak, collaborative editing.

---

**Q34.8: Foundational - [Theory] - [Replication]**

What is the primary purpose of data replication in distributed systems?

A) To reduce storage costs
B) To improve fault tolerance and read performance
C) To enforce schema constraints
D) To compress data

**Answer: B**

**Explanation:**
Replication: copies of data on multiple nodes. Benefits: (1) Fault tolerance: if one node dies, others have the data. (2) Read scalability: read from any replica (distribute read load). (3) Lower latency: replicas geographically closer to users. Trade-off: consistency — how quickly do all replicas reflect a write? Synchronous: strong consistency, slower writes. Asynchronous: faster writes, eventual consistency.

---

**Q34.9: Intermediate - [Theory] - [Rate Limiting]**

The token bucket algorithm for rate limiting works by:

A) Counting requests and blocking when count exceeds threshold
B) Adding tokens at a fixed rate and consuming one token per request; denying when empty
C) Queuing all requests and processing them one at a time
D) Randomly accepting or rejecting requests

**Answer: B**

**Explanation:**
Token bucket: bucket holds tokens, filled at rate r, max capacity b. Each request consumes one token. No tokens = request denied (or queued). Allows bursts up to b requests, sustains r requests/second long-term. Alternative: leaky bucket (smooth output rate, no bursts). Sliding window: count requests in time window. Token bucket is most common: used in API gateways, nginx, AWS API Gateway.

---

**Q34.10: Advanced - [Theory] - [HyperLogLog]**

HyperLogLog counts distinct elements using approximately how much memory for 1 billion elements with ~2% error?

A) 1 GB (store all elements)
B) 100 MB (compressed set)
C) ~12 KB (using probabilistic counting)
D) ~1 byte

**Answer: C**

**Explanation:**
HyperLogLog: ~12KB for 16384 registers (6 bits each). Counts distinct elements with standard error 1.04/√m ≈ 0.81% for m=16384. Stores NO actual elements — only max leading zeros per bucket from hashed values. For 1 billion distinct elements: same 12KB. Redis PFCOUNT: uses this exact implementation. Space savings: exact count of 1B elements would need ~1-8GB. HyperLogLog: constant ~12KB regardless of cardinality.

---

**Q34.11: Intermediate - [Theory] - [Merkle Trees]**

Merkle trees are used in distributed systems to:

A) Sort data across nodes
B) Efficiently detect which data blocks differ between replicas
C) Encrypt all communications
D) Schedule tasks across workers

**Answer: B**

**Explanation:**
Merkle tree: binary tree of hashes. Leaves = hashes of data blocks. Internal nodes = hash of children. Root hash summarizes all data. To compare two replicas: compare root hashes. If different: compare children recursively, narrowing to specific differing blocks. Only O(log n) hash comparisons to find differences vs O(n) full scan. Used in: Cassandra anti-entropy repair, Git, Bitcoin, IPFS.

---

**Q34.12: Foundational - [Theory] - [CDN]**

Content Delivery Networks (CDNs) improve performance primarily through:

A) Compressing all data to reduce size
B) Caching content at edge servers geographically close to users
C) Using faster CPUs at data centers
D) Rewriting application code for optimization

**Answer: B**

**Explanation:**
CDN: network of edge servers worldwide. Static content (images, CSS, JS, video) cached at edge closest to user. Reduces latency (shorter network path) and origin server load. DNS-based routing directs users to nearest edge. Cache invalidation: TTL-based or explicit purge. Providers: CloudFlare, Akamai, AWS CloudFront. Physical distance = network latency → serving from nearby edge dramatically improves user experience.

---

**Q34.13: Intermediate - [Theory] - [Message Queue]**

What data structure underlies most message queue systems (Kafka, RabbitMQ)?

A) Hash table
B) Append-only log (for Kafka) or queue data structure
C) Binary search tree
D) Graph

**Answer: B**

**Explanation:**
Kafka: append-only commit log. Messages written sequentially, consumers track offset. Very fast sequential I/O. Retention-based: messages kept for configurable time, not deleted on consumption. RabbitMQ: traditional queue — message delivered to consumer and acknowledged (deleted). Both decouple producers from consumers. Kafka's log structure enables replay, multiple consumer groups, and high throughput.

---

**Q34.14: Advanced - [Theory] - [Quorum]**

In a system with N=5 replicas, what are the minimum values for write quorum (W) and read quorum (R) to guarantee strong consistency?

A) W=1, R=1
B) W=3, R=3
C) W=5, R=5
D) W=2, R=2

**Answer: B**

**Explanation:**
Strong consistency requires W + R > N, ensuring every read sees the latest write (read and write quorums overlap). With N=5: W=3, R=3 → W+R=6 > 5 ✓. W=2, R=2 → W+R=4 < 5 ✗ (reads might miss latest write). Other valid combos: W=4,R=2 or W=2,R=4. Higher W = slower writes, more durable. Higher R = slower reads. W=R=3 is the balanced choice.

---

**Q34.15: Intermediate - [Theory] - [Bloom Filter in Distributed Systems]**

In a distributed system, Bloom filters help reduce:

A) The CPU usage for computations
B) Unnecessary network requests by pre-filtering queries that will return empty results
C) The size of stored data
D) The number of replicas needed

**Answer: B**

**Explanation:**
Bloom filter: each node maintains a Bloom filter for its data. Query arrives: check Bloom filter first. If says "not present": definitely not here → don't query this node (save network I/O). If says "maybe present": query the node. False positives cause occasional unnecessary queries but false negatives never occur. Bigtable, Cassandra, HBase all use Bloom filters per SSTable to avoid unnecessary disk/network reads.

---

**Q34.16: Foundational - [Theory] - [Horizontal vs Vertical Scaling]**

Horizontal scaling means:

A) Adding more powerful hardware (CPU, RAM) to existing servers
B) Adding more servers to distribute the load
C) Optimizing the code to run faster
D) Using a faster programming language

**Answer: B**

**Explanation:**
Horizontal (scale out): add more machines. Advantages: near-unlimited scaling, fault tolerance (one machine down, others continue). Challenge: data distribution, consistency. Vertical (scale up): bigger/faster single machine. Advantages: simpler architecture, no distributed complexity. Limits: hardware ceiling, single point of failure. Modern systems: horizontal scaling with sharding and replication (e.g., Cassandra, Kafka clusters).

---

**Q34.17: Expert - [Theory] - [Vector Clocks]**

Vector clocks in distributed systems solve what problem that Lamport timestamps cannot?

A) Ordering events chronologically
B) Detecting concurrent events (events that cannot be causally ordered)
C) Counting the total number of events
D) Encrypting event timestamps

**Answer: B**

**Explanation:**
Lamport timestamps: if a→b then L(a) < L(b). But L(a) < L(b) does NOT imply a→b (could be concurrent). Vector clocks: each process maintains a vector of counters. VC(a) < VC(b) implies a→b. If neither VC(a) < VC(b) nor VC(b) < VC(a): events are concurrent (no causal relationship). Used for conflict detection in DynamoDB, Riak. Trade-off: O(n) space per event for n processes.

---

**Q34.18: Advanced - [Theory] - [Gossip Protocol]**

Gossip protocols disseminate information through a cluster in:

A) O(1) time by broadcasting to all nodes simultaneously
B) O(log n) rounds by each node telling random peers
C) O(n) time by sequential forwarding
D) O(n²) time by all-pairs communication

**Answer: B**

**Explanation:**
Gossip: each round, every node tells k random peers any new information. After 1 round: ~k nodes know. After 2: ~k². After log_k(n) rounds: all n nodes know. Robust: works even if some messages lost (redundant paths). Used in: Cassandra (node health), SWIM (failure detection), epidemic protocols. O(n log n) total messages, O(log n) rounds. Self-healing: no central coordinator needed.

---

**Q34.19: Intermediate - [Theory] - [Database Partitioning]**

In a key-value store, hash partitioning assigns keys to partitions using hash(key) mod P. What happens when you add a new partition (P → P+1)?

A) Only a few keys need to move
B) Almost all keys need to be reassigned to different partitions
C) No keys need to move
D) Only the last partition is affected

**Answer: B**

**Explanation:**
hash(key) mod P → hash(key) mod (P+1): different result for most keys. Nearly ALL keys remap to different partitions → massive data migration. This is why consistent hashing was invented — adding a node moves only ~1/P of keys. Fixed mod-based partitioning: only works if P never changes. In practice: either use consistent hashing or over-provision partitions from the start (e.g., Kafka fixed partition count).

---

**Q34.20: Expert - [Theory] - [Linearizability]**

Linearizability is a stronger guarantee than sequential consistency because:

A) It requires less coordination between nodes
B) It requires operations to appear instantaneous at some point between invocation and response
C) It allows operations to be reordered freely
D) It only applies to read operations

**Answer: B**

**Explanation:**
Linearizability: each operation appears to take effect atomically at some point between its start and end (real-time ordering preserved). Sequential consistency: operations appear in SOME sequential order consistent with each process's program order — but not necessarily real-time order. Linearizability respects wall-clock time; sequential consistency doesn't. Linearizability requires more coordination (consensus) → lower performance. Used when correctness requires real-time ordering (locks, leader election).

---

**Q34.21: Intermediate - [Theory] - [Event-Driven Architecture]**

What data structure pattern enables event sourcing?

A) Mutable state table updated in place
B) Append-only event log where current state is derived by replaying events
C) Circular buffer overwriting old events
D) Stack of undo/redo operations

**Answer: B**

**Explanation:**
Event sourcing: store all state changes as immutable events in an ordered log. Current state: replay events from beginning (or from a snapshot). Benefits: complete audit trail, time-travel debugging, event replay for new views. Like a database transaction log AS the primary data store. Kafka naturally supports this pattern. Trade-off: rebuilding state can be slow without periodic snapshots.

---

**Q34.22: Advanced - [Theory] - [Shard Rebalancing]**

When a distributed database needs to rebalance shards across nodes, which approach minimizes data movement?

A) Randomly reassign all shards
B) Move only the minimum number of shards needed to achieve balance
C) Delete and recreate all shards from backup
D) Copy all data to a single node first

**Answer: B**

**Explanation:**
Optimal rebalancing: calculate current vs target shard distribution. Move only shards necessary to equalize load — typically O(n/k) shard moves for k new nodes. Algorithms: min-cost flow, greedy reassignment. During rebalancing: dual-read (check old and new location) until migration complete. CockroachDB, TiDB: automatic range splitting and rebalancing. The goal is minimal disruption during topology changes.

---

## Chapter 34 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 6 | CAP, consistent hashing, caching, replication, CDN, scaling |
| Intermediate | 10 | Load balancing, sharding, consensus, rate limiting, Merkle trees, Bloom, queues |
| Advanced | 4 | CRDTs, quorum, gossip, column store, shard rebalancing |
| Expert | 2 | Vector clocks, linearizability |

**Total MCQs: 22**

**Answer Distribution: A=3, B=16, C=2, D=1**

**Next:** Chapter 35 - Competitive Programming Techniques
