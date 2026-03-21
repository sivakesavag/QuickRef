# Chapter 40: Streaming Algorithms

**Target:** 25 MCQs | **Distribution:** 6 Foundational, 10 Intermediate, 6 Advanced, 3 Expert

---

**Q40.1: Foundational - [Theory] - [Streaming Model]**

The streaming model requires algorithms to process data with:

A) Unlimited memory and multiple passes
B) Limited memory (sub-linear in input size) and typically one pass
C) No memory at all
D) Random access to all elements

**Answer: B**

**Explanation:**
Streaming: data arrives sequentially, too large to store entirely. Algorithm uses O(polylog n) or O(n^ε) memory. Typically single pass (or few passes). Must produce answer from this limited state. Examples: network traffic monitoring (billions of packets), sensor data, log analysis. Trade-off: exact answers often impossible in sub-linear space → approximation or randomization required.

---

**Q40.2: Foundational - [Theory] - [Count-Min Sketch]**

A Count-Min Sketch estimates element frequencies by:

A) Storing exact counts in a hash table
B) Using d hash functions mapping to d arrays of w counters, querying minimum across arrays
C) Sampling random elements
D) Sorting the stream

**Answer: B**

**Explanation:**
Count-Min Sketch: d hash functions, w counters per row (d×w matrix). Insert(x): increment counter at h_i(x) for each row i. Query(x): return min(counters at h_i(x)). Always overestimates (hash collisions only add). Error: with w=⌈e/ε⌉, d=⌈ln(1/δ)⌉: estimate ≤ true_count + ε×||stream||₁ with probability 1-δ. Space: O((1/ε)×log(1/δ)). Used in network monitoring, NLP frequency estimation.

---

**Q40.3: Intermediate - [Theory] - [HyperLogLog]**

HyperLogLog counts approximate distinct elements using what statistical observation?

A) Elements with rare values appear less frequently
B) The maximum number of leading zeros in hashed values indicates the log of the number of distinct elements
C) Distinct elements always hash to different buckets
D) Counting is impossible in streaming

**Answer: B**

**Explanation:**
Hash each element to uniform random bits. If n distinct elements: expected max leading zeros ≈ log₂ n. HyperLogLog splits hash into two parts: first p bits = bucket index (m=2^p buckets), remaining bits → track max leading zeros per bucket. Estimate: harmonic mean across buckets with bias correction. 12KB (16384 buckets × 6 bits) → ~0.8% error for any n. Redis PFCOUNT: exactly this algorithm. Space-independent of n.

---

**Q40.4: Foundational - [Theory] - [Bloom Filter]**

A Bloom filter can produce:

A) Both false positives and false negatives
B) False positives but never false negatives
C) False negatives but never false positives
D) Neither false positives nor false negatives

**Answer: B**

**Explanation:**
Bloom filter: k hash functions, m-bit array. Insert: set k bit positions. Query: check k positions. If all set: "maybe present" (could be false positive from other elements setting those bits). If any unset: "definitely not present" (never false negative — insert always sets required bits). Optimal k = (m/n) ln 2. With m=10n, k=7: ~0.8% false positive rate. Can't delete elements (unsetting bit may affect other elements).

---

**Q40.5: Intermediate - [Complexity] - [Bloom Filter Space]**

A Bloom filter with desired false positive rate p for n elements needs approximately how many bits?

A) O(n)
B) O(-n × ln(p) / (ln 2)²) ≈ O(n × log(1/p))
C) O(n²)
D) O(log n)

**Answer: B**

**Explanation:**
Optimal Bloom filter: m = -n × ln(p) / (ln 2)² bits. For p = 1%: ~9.6 bits per element. For p = 0.1%: ~14.4 bits per element. Optimal k = -log₂(p) ≈ 6.6 for 1%. Space is proportional to n (number of elements) and log(1/p) (precision). Independent of the size of elements themselves. A million URLs need ~1.2MB at 1% false positive — remarkably compact.

---

**Q40.6: Intermediate - [Theory] - [Reservoir Sampling]**

Reservoir sampling maintains a uniform random sample of k elements from a stream of unknown length by:

A) Keeping the first k elements
B) For element i (i > k): replacing a random reservoir element with probability k/i
C) Keeping the last k elements
D) Sampling every n/k-th element

**Answer: B**

**Explanation:**
Algorithm: fill reservoir with first k elements. For each subsequent element i: generate random r in [1, i]. If r ≤ k: replace reservoir[r] with element i. Proof: each element has probability k/n of being in final sample (where n = stream length). Works without knowing n in advance! O(k) memory, one pass. Applications: random sampling from database query results, log sampling, A/B testing on streams.

---

**Q40.7: Advanced - [Theory] - [Flajolet-Martin Algorithm]**

The Flajolet-Martin algorithm estimates distinct elements by tracking:

A) The exact count of each element
B) The maximum number of trailing zeros in hash values
C) The minimum hash value
D) The average hash value

**Answer: B**

**Explanation:**
Flajolet-Martin: hash each element, track R = max trailing zeros across all hashes. Estimate: 2^R. Intuition: with n distinct elements, ~n/2 hash to even (0 trailing zeros), ~n/4 hash to ≡0 mod 4 (2 trailing zeros), etc. Expect R ≈ log₂ n. High variance → use multiple hash functions, take median or mean. HyperLogLog improves this with stochastic averaging across many "registers." FM was the foundational algorithm for probabilistic cardinality estimation.

---

**Q40.8: Intermediate - [Theory] - [Misra-Gries Algorithm]**

The Misra-Gries algorithm finds frequent elements (appearing > n/k times) using:

A) Exact frequency counts for all elements
B) k-1 counters that are decremented in groups when no matching counter exists
C) Sorting the stream in memory
D) Random sampling

**Answer: B**

**Explanation:**
Misra-Gries: maintain at most k-1 (element, counter) pairs. New element: if present, increment. If not and space available: add with count 1. If not and full: decrement ALL counters by 1, remove zeros. Guarantee: any element with frequency > n/k survived (may have reduced count). Second pass (or approximate count) verifies. O(k) space. Deterministic. Boyer-Moore voting: special case k=2 (majority element). Foundation of heavy hitter detection.

---

**Q40.9: Foundational - [Theory] - [Majority Element]**

Boyer-Moore voting algorithm finds a majority element (appearing > n/2 times) using:

A) A hash table of all element counts
B) O(1) space: one candidate and one counter
C) Sorting the array first
D) Binary search

**Answer: B**

**Explanation:**
Boyer-Moore: maintain candidate and count (init: first element, count=1). For each subsequent element: if equals candidate: count++. Else: count--. If count=0: candidate = current, count=1. If majority element exists: it survives (more increments than decrements). Final candidate must be verified with a second pass. O(n) time, O(1) space. Elegant example of streaming with constant memory.

---

**Q40.10: Advanced - [Theory] - [Turnstile Model]**

The "turnstile" streaming model differs from the "cash register" model in that:

A) Only insertions are allowed
B) Both insertions and deletions are allowed (element frequencies can decrease)
C) Elements arrive in sorted order
D) Multiple passes are required

**Answer: B**

**Explanation:**
Cash register model: elements only inserted (frequencies non-decreasing). Simpler. Turnstile model: elements can be inserted AND deleted (frequencies can increase/decrease, but must stay non-negative). More general — models database updates, stock transactions. Count-Min Sketch works in both (though accuracy differs). Some algorithms only work in cash register model. Turnstile is strictly harder → stronger lower bounds.

---

**Q40.11: Intermediate - [Theory] - [Moment Estimation]**

The k-th frequency moment F_k of a stream is defined as:

A) The k-th largest frequency
B) Σ(f_i^k) where f_i is the frequency of element i
C) The total number of elements divided by k
D) The k most frequent elements

**Answer: B**

**Explanation:**
F_0 = number of distinct elements. F_1 = stream length (total count). F_2 = sum of squared frequencies (measures skew/concentration). Alon-Matias-Szegedy (AMS): estimated F_2 in O(log n + 1/ε²) space, winning the Gödel Prize. F_k for k ≥ 2: O(n^(1-1/k)/ε²) space. Frequency moments capture essential stream statistics: F_2 detects heavy hitters, F_0 counts distinct elements.

---

**Q40.12: Advanced - [Theory] - [CountSketch]**

CountSketch differs from Count-Min Sketch in that:

A) It uses min instead of sum
B) It uses signed (±1) hash functions, enabling unbiased estimates with median aggregation
C) It stores larger counters
D) It doesn't use hash functions

**Answer: B**

**Explanation:**
CountSketch: each element hashed to position AND multiplied by random ±1 sign. Insert(x): counter[h_i(x)] += s_i(x). Query(x): estimate = median_i(counter[h_i(x)] × s_i(x)). The ±1 signs make collisions cancel in expectation (unbiased). Median across d rows reduces variance. Advantages over Count-Min: unbiased estimates, works in turnstile model (negative counts). Count-Min: simpler, always overestimates, better for cash register.

---

**Q40.13: Foundational - [Theory] - [Space Lower Bound]**

Computing the exact median of a stream of n elements requires:

A) O(1) space
B) O(log n) space
C) Ω(n) space
D) O(√n) space

**Answer: C**

**Explanation:**
Exact median: must distinguish among all possible median values. After seeing the entire stream, the median depends on the exact multiset of elements. Communication complexity argument: any streaming algorithm computing exact median needs Ω(n) bits (essentially must remember the entire stream). This is why streaming algorithms for quantiles (including median) are approximate: ε-approximate quantile in O((1/ε) × log n) space.

---

**Q40.14: Intermediate - [Theory] - [Sliding Window]**

Streaming algorithms over sliding windows (only the last W elements count) are harder because:

A) The window is always small
B) Elements must be "removed" when they expire, requiring tracking of old elements
C) Windows can't be implemented on streams
D) All elements have equal weight

**Answer: B**

**Explanation:**
Standard stream: only insertions. Window: old elements expire (implicit deletion). Must "forget" elements outside the window. Bloom filter: can't delete → counting Bloom filter needed. Count-Min: can use decaying counters. Exponential histograms (Datar et al.): maintain approximate counts over windows using O((1/ε) × log² W) space. Sliding window adds significant complexity to most streaming problems.

---

**Q40.15: Expert - [Theory] - [Sketching Lower Bounds]**

The space lower bound for (1±ε)-approximating F_2 (second frequency moment) in a stream is:

A) O(1)
B) Ω(1/ε²) bits
C) Ω(n) bits
D) Ω(n²) bits

**Answer: B**

**Explanation:**
AMS showed F_2 estimable in O(1/ε² × log n) space. Lower bound: Ω(1/ε²) bits proven via communication complexity (indexing problem reduction). Tight up to log factors. For ε = 0.01: need ~10,000 counters/registers. The 1/ε² dependence is universal across many streaming estimation problems — fundamental price of approximate counting. Matches the "variance of estimator" intuition from statistics.

---

**Q40.16: Advanced - [Theory] - [Cuckoo Filter]**

Cuckoo filters improve upon Bloom filters by:

A) Using more memory
B) Supporting deletion and having better space efficiency for low false positive rates
C) Being simpler to implement
D) Not using hash functions

**Answer: B**

**Explanation:**
Cuckoo filter: store fingerprints in a cuckoo hash table. Deletion: remove fingerprint (safe because fingerprints are short hashes). Bloom filters: can't delete (bit shared by multiple elements). Space: for same false positive rate, cuckoo filters use ~30% less space than Bloom when FP rate < 3%. Lookup: check exactly 2 locations (fast). Trade-off: insertion can fail at very high load factors. Used in: network packet filtering, databases.

---

**Q40.17: Intermediate - [Theory] - [Lossy Counting]**

Lossy counting for frequent items in a stream:

A) Counts all elements exactly
B) Guarantees finding all items with frequency ≥ (s-ε)×n while using O((1/ε) × log(εn)) space
C) Only works for numeric data
D) Requires multiple passes

**Answer: B**

**Explanation:**
Lossy counting (Manku-Motwani): divide stream into windows of size 1/ε. At each window boundary: decrement all counts by 1, remove zeros. Elements with true frequency ≥ sn survive with certainty. Some with frequency ≥ (s-ε)n may also survive (no false negatives above threshold). Space: O((1/ε) × log(εn)). Applications: finding trending topics, hot URLs, popular queries. Deterministic, single pass.

---

**Q40.18: Expert - [Theory] - [L_p Sampling]**

L_p sampling from a stream returns element i with probability proportional to |f_i|^p. Why is this useful?

A) It simplifies the stream
B) It enables estimation of F_p, heavy hitters, and other aggregate functions via sampling
C) It sorts the elements by frequency
D) It compresses the stream

**Answer: B**

**Explanation:**
L_p sampler: returns element i with probability ~|f_i|^p / F_p. For p=0: uniform over distinct elements. For p=2: probability proportional to f_i². Applications: (1) F_p estimation via sampling, (2) Finding heavy hitters, (3) Graph stream algorithms (sampling edges by neighborhood size). Implemented using: precision sampling + sketches. O(polylog n) space. Powerful primitive — many streaming algorithms reduce to L_p sampling. Research frontier: optimal space for L_p sampling.

---

**Q40.19: Advanced - [Theory] - [Graph Streaming]**

Computing connectivity of a graph given as a stream of edges requires:

A) O(V) space using union-find
B) O(V + E) space (must store entire graph)
C) O(1) space
D) O(V²) space

**Answer: A**

**Explanation:**
Graph streaming: edges arrive one at a time. Connectivity: maintain union-find (disjoint set). Each edge (u,v): union(u,v). Space: O(V) for parent/rank arrays. Connected components: number of disjoint sets at the end. Works for insertion-only edge streams. For insertion+deletion: much harder — semi-streaming model allows O(V × polylog V) space. Exact connectivity with deletions requires Ω(V × log V) space. Even basic graph problems become hard in streaming.

---

**Q40.20: Expert - [Theory] - [Mergeable Summaries]**

Mergeable sketches (like Count-Min Sketch, HyperLogLog) enable distributed streaming because:

A) They only work on a single machine
B) Partial sketches from different machines can be combined to get a sketch for the union of streams
C) They reduce network latency
D) They eliminate the need for coordination

**Answer: B**

**Explanation:**
Mergeability: sketch(S₁ ∪ S₂) = merge(sketch(S₁), sketch(S₂)). Count-Min: element-wise max (or sum) of counter arrays. HyperLogLog: element-wise max of registers. Bloom filter: bitwise OR. Each machine builds local sketch → send to coordinator → merge → global answer. No need to send raw data. Essential for distributed monitoring (CDN traffic, multi-datacenter analytics). MapReduce-compatible. Space-efficient communication.

---

## Chapter 40 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | Streaming model, Bloom filter, Boyer-Moore, space lower bounds |
| Intermediate | 8 | CMS, HyperLogLog, reservoir sampling, Misra-Gries, frequency moments, sliding window, lossy counting |
| Advanced | 4 | Flajolet-Martin, turnstile model, CountSketch, cuckoo filter, graph streaming |
| Expert | 3 | Sketching lower bounds, L_p sampling, mergeable summaries |

**Total MCQs: 20**

**Answer Distribution: A=3, B=14, C=2, D=1**

**Next:** Chapter 41 - Quantum Computing Basics
