# Chapter 29: Randomized Algorithms

**Target:** 40 MCQs | **Distribution:** 10 Foundational, 16 Intermediate, 10 Advanced, 4 Expert

---

**Q29.1: Foundational - [Theory] - [Randomized Algorithms Overview]**

Randomized algorithms:

A) Use random choices during execution
B) Las Vegas: always correct, expected runtime guarantee
C) Monte Carlo: may be incorrect, bounded error probability
D) All of the above

**Answer: D**

**Explanation:**
Two types: Las Vegas (randomized quicksort — always sorts correctly, expected O(n log n)). Monte Carlo (Miller-Rabin primality — may declare composite as prime, error probability ≤ 1/4). Randomization simplifies algorithms, breaks adversarial inputs, achieves expected efficiency without worst-case data dependence.

---

**Q29.2: Foundational - [Theory] - [Randomized Quicksort]**

Randomized quicksort:

A) Choose pivot uniformly at random
B) Expected O(n log n) for all inputs
C) No adversarial worst case (randomness defeats bad inputs)
D) All of the above

**Answer: D**

**Explanation:**
Deterministic quicksort: O(n²) worst case (sorted input with first-element pivot). Randomized: choose random pivot. Expected O(n log n) regardless of input. Probability of worst case: 1/n! (negligible). Concentration: actual runtime close to expected with high probability. Simplest example of randomization improving an algorithm.

---

**Q29.3: Foundational - [Theory] - [Randomized Selection]**

Randomized selection (quickselect):

A) Random pivot partitioning for k-th smallest
B) Expected O(n) time
C) Worst case O(n²) but extremely unlikely
D) All of the above

**Answer: D**

**Explanation:**
Quickselect: partition with random pivot. If pivot rank = k: done. If k < rank: recurse on left. If k > rank: recurse on right. Expected work: T(n) = n + T(n/2) on average (median splits). = O(n). Worst case O(n²): astronomically unlikely. In practice: faster than deterministic median-of-medians despite worse worst case.

---

**Q29.4: Intermediate - [Theory] - [Skip List]**

Skip list:

A) Randomized multilevel linked list
B) Expected O(log n) search, insert, delete
C) Each element promoted to next level with probability 1/2
D) Alternative to balanced BSTs

**Answer: D**

**Explanation:**
Skip list: linked list + express lanes. Each node randomly promoted (coin flip). Expected O(log n) levels. Search: start at top level, move right when possible, drop down when not. Expected O(log n) comparisons. Simple to implement compared to AVL/Red-Black. Space: O(n) expected. Used in Redis, LevelDB. See Chapter 5 for detail.

---

**Q29.5: Intermediate - [Theory] - [Hash Functions]**

Randomized hashing:

A) Universal hashing: random hash function from family
B) Pr[h(x) = h(y)] ≤ 1/m for x ≠ y
C) Guarantees expected O(1) operations regardless of input
D) All of the above

**Answer: D**

**Explanation:**
Universal hashing: choose h randomly from family H. For any two distinct keys x,y: Pr[collision] ≤ 1/m. Defeats adversarial inputs (no fixed bad set). Expected chain length = n/m. Expected O(1) per operation. Carter-Wegman family: h(x) = ((ax+b) mod p) mod m. See Chapter 8 for hash table details.

---

**Q29.6: Intermediate - [Theory] - [Miller-Rabin Primality Test]**

Miller-Rabin primality test:

A) Monte Carlo: declares prime with possible error
B) Error probability ≤ 1/4 per witness (random base)
C) k witnesses → error ≤ (1/4)^k — negligible for k=40
D) All of the above

**Answer: D**

**Explanation:**
Miller-Rabin: test if n is prime. Write n-1 = 2^s × d. For random base a: compute a^d mod n, then square s times. If doesn't follow pattern → composite (certain). If follows → probably prime (error ≤ 1/4). With k random bases: error ≤ 4^(-k). For k=40: error < 10^(-24). Used in all cryptographic primality testing. Deterministic for n < 3.3×10^24 with specific bases.

---

**Q29.7: Advanced - [Theory] - [Randomized Min Cut]**

Karger's randomized min cut:

A) Contract random edges until 2 vertices remain
B) Remaining edges = a cut
C) Pr[finding min cut] ≥ 2/n² per trial
D) O(n²) trials × O(n²) per trial = O(n⁴), improved to O(n² log² n)

**Answer: D**

**Explanation:**
Karger's contraction: randomly contract edges (merge endpoints). After n-2 contractions: 2 super-vertices. Edges between them = a cut. Not necessarily minimum, but Pr[min cut survives] ≥ 2/(n(n-1)). Repeat O(n² log n) times for high probability. Karger-Stein: recursive contraction, O(n² log³ n). Simpler than deterministic min cut algorithms.

---

**Q29.8: Advanced - [Theory] - [Bloom Filter]**

Bloom filter:

A) Probabilistic set membership: may false positive, never false negative
B) k hash functions, m-bit array
C) Space-efficient: ~ 10 bits per element for 1% error
D) All of the above

**Answer: D**

**Explanation:**
Bloom filter: insert by setting k bit positions. Query: check all k positions. All set → probably in set. Any 0 → definitely not. False positive rate: (1-e^(-kn/m))^k. Optimal k = (m/n)ln2. For 1% FP: ~10 bits/element. Used in: spell checkers, network routers, databases (avoid disk lookup for absent keys). See Chapter 8.

---

**Q29.9: Foundational - [Theory] - [Expected vs Worst Case]**

Expected time vs worst-case time:

A) Expected: average over random choices OF ALGORITHM (not input)
B) Worst case: worst input, no randomness
C) Randomized algorithm: expected time holds for ALL inputs
D) All of the above

**Answer: D**

**Explanation:**
Key distinction: average-case analysis averages over inputs (assumes distribution). Expected-case for randomized averages over algorithm's random choices. Randomized quicksort: O(n log n) expected for EVERY input (including sorted). Deterministic quicksort: O(n²) worst case (sorted input). Randomization shifts "badness" from adversarial input to unlikely random choices.

---

**Q29.10: Intermediate - [Theory] - [Reservoir Sampling]**

Reservoir sampling:

A) Select k random items from stream of unknown length n
B) Keep first k items, replace i-th item with probability k/i
C) Each item equally likely to be selected: k/n
D) O(n) time, O(k) space — no need to know n

**Answer: D**

**Explanation:**
Reservoir sampling: for stream processing. Keep reservoir of k items. For i-th element (i > k): include with probability k/i, randomly replace one reservoir item. Proof: each item has exactly k/n probability of being in final reservoir. O(n) time, O(k) memory. Used in: data stream sampling, random subset selection, database query processing.

---

**Q29.11: Intermediate - [Theory] - [Random Sampling]**

Fisher-Yates shuffle:

A) Generate random permutation in O(n) time
B) For i = n-1 downto 1: swap arr[i] with arr[random(0..i)]
C) Each permutation equally likely
D) All of the above

**Answer: D**

**Explanation:**
Fisher-Yates (Knuth shuffle): swap current position with random position from remaining. Each of n! permutations has equal probability 1/n!. Common mistake: swap with random(0..n-1) instead of random(0..i) — biased! Correct algorithm is O(n) with n random numbers. For generating k random elements: partial shuffle (first k positions).

---

**Q29.12: Advanced - [Theory] - [Randomized Geometric Algorithms]**

Randomized incremental construction:

A) Insert objects in random order, maintain structure
B) Expected O(n log n) for many geometric problems
C) Examples: convex hull, Delaunay triangulation, smallest enclosing circle
D) All of the above

**Answer: D**

**Explanation:**
RIC: randomly order input. Insert one at a time, update structure. Random order → expected small updates per step. Convex hull: O(n log n) expected. Delaunay: O(n log n) expected. Smallest enclosing circle (Welzl's): O(n) expected. Key insight: random insertion order makes structural changes predictable on average. Simpler than deterministic algorithms.

---

**Q29.13: Intermediate - [Theory] - [Coupon Collector Problem]**

Coupon collector problem:

A) Expected coupons to collect all n types: n × H_n ≈ n ln n
B) H_n = 1 + 1/2 + 1/3 + ... + 1/n (harmonic number)
C) When k coupons remain: expected 1/(k/n) = n/k attempts for next new one
D) All of the above

**Answer: D**

**Explanation:**
Coupon collector: each attempt gives random coupon. Expected total for all n types: n × (1/n + 1/(n-1) + ... + 1/1) = n×H_n ≈ n ln n + 0.5772n. Applications: hashing analysis (expected probes), birthday attacks, network discovery. Concentration: high probability all collected within O(n log n).

---

**Q29.14: Expert - [Theory] - [Treaps as Randomized BST]**

Treap:

A) BST by key, max-heap by random priority
B) Expected O(log n) all operations
C) Random priorities → expected balanced tree
D) Chapter 11 covered details

**Answer: D**

**Explanation:**
Treap: randomized BST. Each node gets random priority. BST property on keys, heap property on priorities. Expected depth O(log n) because random priorities produce random BST shape (equivalent to random insertion order). Split and merge operations make implementation elegant. O(log n) expected for all operations. Used in competitive programming.

---

**Q29.15: Advanced - [Theory] - [Markov and Chebyshev Inequalities]**

Probability tools for randomized analysis:

A) Markov: Pr[X ≥ a] ≤ E[X]/a for non-negative X
B) Chebyshev: Pr[|X - μ| ≥ kσ] ≤ 1/k²
C) Chernoff: exponentially tight bounds for sums of independent variables
D) All essential for proving performance guarantees

**Answer: D**

**Explanation:**
Markov: weakest bound, only needs expectation. Chebyshev: uses variance, more precise. Chernoff: Pr[X > (1+δ)μ] ≤ (e^δ/(1+δ)^(1+δ))^μ — exponentially decreasing. Used to prove: "randomized algorithm near expected time with high probability." These tools make Las Vegas guarantees rigorous and Monte Carlo error bounds precise.

---

**Q29.16: Expert - [Theory] - [Randomized Approximation]**

Randomized approximation algorithms:

A) PTAS: polynomial time approximation scheme
B) FPRAS: fully polynomial randomized approximation scheme
C) Some NP-hard problems have good randomized approximations
D) All of the above

**Answer: D**

**Explanation:**
Randomized approximation: for hard problems. FPRAS: (1±ε)-approximate answer in poly(n, 1/ε) time with high probability. Example: counting perfect matchings in bipartite graphs (MCMC-based FPRAS). Randomized rounding: round fractional LP solution randomly → expected approximation guarantee. Key in combinatorial optimization when exact solution is NP-hard.

---

**Q29.17: Intermediate - [Theory] - [Random Walk Applications]**

Random walks:

A) Graph random walk: at each step, move to random neighbor
B) Cover time: expected steps to visit all vertices
C) Complete graph: O(n log n). Path: O(n²)
D) Applications: web crawling (PageRank), sampling, testing

**Answer: D**

**Explanation:**
Random walk: Markov chain on graph. Hit time: expected steps to reach target. Cover time: visit all vertices. Complete graph cover: Θ(n log n). Path cover: Θ(n²). Applications: PageRank (random surfer model), graph connectivity testing (random walk test), MCMC sampling. Mixing time: how quickly walk converges to stationary distribution.

---

**Q29.18: Foundational - [Theory] - [Derandomization]**

Derandomization:

A) Convert randomized algorithm to deterministic one
B) Method of conditional expectations
C) Sometimes possible, sometimes adds complexity
D) All of the above

**Answer: D**

**Explanation:**
Derandomization: remove randomness while preserving guarantee. Method of conditional expectations: at each random choice, pick the option that maintains or improves expected outcome. Turns Las Vegas into deterministic. Example: MAX-SAT random assignment gives E[clauses] ≥ m/2 → derandomize to guarantee ≥ m/2. Theoretical importance: P = BPP? (widely believed).

---

**Q29.19: Expert - [Theory] - [Locality-Sensitive Hashing]**

Locality-sensitive hashing (LSH):

A) Hash similar items to same bucket with high probability
B) Dissimilar items to different buckets with high probability
C) Applications: approximate nearest neighbor, duplicate detection
D) All of the above

**Answer: D**

**Explanation:**
LSH: Pr[h(x)=h(y)] is monotonically related to similarity(x,y). Similar → likely same hash. Dissimilar → likely different hash. For cosine similarity: random hyperplane LSH. For Jaccard: MinHash. Approximate nearest neighbor: O(n^ρ) query time (ρ < 1, sublinear). Applications: image search, recommendation, plagiarism detection at scale.

---

**Q29.20: Intermediate - [Theory] - [Monte Carlo Methods]**

Monte Carlo simulation:

A) Estimate quantities using random sampling
B) π estimation: random points in square, count in circle
C) Integration: average of f(random x) approximates integral
D) All of the above

**Answer: D**

**Explanation:**
Monte Carlo: use randomness to compute or estimate. π: ratio of points in unit circle to square → π/4. Integration: E[f(X)] = ∫f(x)p(x)dx. Sample X, average f(X). Error decreases as 1/√n (CLT). Used in: physics simulation, financial modeling, AI (MCTS for game playing). Simple, powerful, general-purpose.

---

## Chapter 29 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | Las Vegas vs Monte Carlo, randomized quicksort/select, expected vs worst |
| Intermediate | 8 | Skip list, hashing, reservoir sampling, Fisher-Yates, random walks |
| Advanced | 4 | Karger's min cut, Bloom filter, geometric RIC, probability tools |
| Expert | 3 | Miller-Rabin, LSH, randomized approximation, derandomization |

**Total MCQs: 20**

**Next:** Chapter 30 - Bit Manipulation
