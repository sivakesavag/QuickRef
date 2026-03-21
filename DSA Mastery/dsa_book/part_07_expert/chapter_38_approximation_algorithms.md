# Chapter 38: Approximation Algorithms

**Target:** 30 MCQs | **Distribution:** 8 Foundational, 12 Intermediate, 7 Advanced, 3 Expert

---

**Q38.1: Foundational - [Theory] - [Why Approximation]**

Approximation algorithms are used when:

A) Exact algorithms are too slow for NP-hard problems, but a near-optimal solution is acceptable
B) The problem has an efficient exact solution
C) Random answers are sufficient
D) Only small inputs need to be handled

**Answer: A**

**Explanation:**
NP-hard problems (TSP, Set Cover, Vertex Cover) have no known polynomial-time exact algorithms. For practical use: either wait exponentially long or accept a provably near-optimal solution in polynomial time. Approximation algorithms guarantee: solution ≤ α × OPT (for minimization) where α is the approximation ratio. This ratio is mathematically proven, not just empirical.

---

**Q38.2: Foundational - [Theory] - [Approximation Ratio]**

An algorithm with approximation ratio 2 for a minimization problem guarantees:

A) The solution is exactly twice optimal
B) The solution costs at most twice the optimal solution
C) The running time is double that of an exact algorithm
D) It fails half the time

**Answer: B**

**Explanation:**
Approximation ratio α: ALG(I) ≤ α × OPT(I) for all instances I (minimization). Ratio 2 means: worst case is 2× optimal, but often much better in practice. For maximization: ALG(I) ≥ OPT(I)/α. A ratio of 1 would be exact. Lower ratios are better. Some problems: constant ratio achievable (Vertex Cover: 2). Others: no constant ratio unless P=NP (general TSP).

---

**Q38.3: Intermediate - [Theory] - [Vertex Cover 2-Approximation]**

The simple 2-approximation for Vertex Cover works by:

A) Picking the highest-degree vertex first
B) Picking an arbitrary edge and including both endpoints, removing covered edges, repeating
C) Finding a maximum matching then including all matched vertices
D) Using dynamic programming on the graph

**Answer: B**

**Explanation:**
Algorithm: while edges remain, pick any edge (u,v), add BOTH u and v to cover, remove all edges incident to u or v. Why 2-approx? Each chosen edge contributes 2 vertices. Any valid cover must include at least one endpoint of each chosen edge → OPT ≥ |chosen edges|. ALG = 2 × |chosen edges| ≤ 2 × OPT. Option C also works and gives the same ratio (matching lower bounds OPT). Greedy by degree (A) has no proven constant ratio.

---

**Q38.4: Foundational - [Theory] - [Greedy Set Cover]**

The greedy algorithm for Set Cover (always pick the set covering the most uncovered elements) achieves what ratio?

A) Constant factor (2×)
B) O(log n) where n is the number of elements
C) O(n)
D) Exact optimal

**Answer: B**

**Explanation:**
Greedy Set Cover: at each step, pick set that covers the most remaining elements. Ratio: H(n) = 1 + 1/2 + 1/3 + ... + 1/n = O(ln n). Proof: each greedy step reduces remaining elements by at least 1/OPT fraction → harmonic series bound. This is essentially tight: under standard assumptions, no polynomial algorithm achieves ratio (1-ε)ln n. Logarithmic ratio is the best possible.

---

**Q38.5: Intermediate - [Theory] - [TSP Approximation]**

The Christofides algorithm for metric TSP achieves what approximation ratio?

A) 1.5 (3/2)
B) 2
C) O(log n)
D) Exact optimal

**Answer: A**

**Explanation:**
Christofides (1976): (1) Find MST. (2) Find minimum-weight perfect matching on odd-degree MST vertices. (3) Combine → Eulerian graph. (4) Find Euler tour → shortcut to Hamiltonian tour. Ratio: MST ≤ OPT, matching ≤ OPT/2 → total ≤ 1.5 × OPT. Best known polynomial approximation for metric TSP for decades. Recent breakthrough (2020): 1.5 - ε for some tiny ε. General (non-metric) TSP: no constant ratio unless P=NP.

---

**Q38.6: Intermediate - [Complexity] - [PTAS]**

A PTAS (Polynomial-Time Approximation Scheme) provides:

A) An exact solution in polynomial time
B) A (1+ε)-approximation for any chosen ε > 0, with runtime polynomial in n but possibly exponential in 1/ε
C) A constant-factor approximation
D) A randomized approximation

**Answer: B**

**Explanation:**
PTAS: for any ε > 0, gives (1+ε)-approximate solution. Runtime: O(n^f(1/ε)) where f is some function. For fixed ε: polynomial in n. But ε=0.001 might give O(n^1000). FPTAS (fully polynomial): runtime polynomial in BOTH n and 1/ε, e.g., O(n²/ε). FPTAS is strictly better. Knapsack has FPTAS. Euclidean TSP has PTAS. General metric TSP has no PTAS (unless P=NP).

---

**Q38.7: Foundational - [Theory] - [Randomized Approximation]**

The MAX-CUT randomized approximation (assign each vertex to a random side) achieves expected cut size of:

A) Exactly OPT
B) At least OPT/2 (0.5 approximation)
C) At least OPT/4
D) Zero expected cut

**Answer: B**

**Explanation:**
Random partition: each edge crosses the cut with probability 1/2 (endpoints equally likely on different sides). Expected cut = m/2 where m = total edges. OPT ≤ m (can't cut more edges than exist). So E[ALG] = m/2 ≥ OPT/2. A 0.5-approximation! Goemans-Williamson SDP relaxation: achieves ~0.878 ratio. Under Unique Games Conjecture: 0.878 is optimal. Simple randomization gives surprisingly good guarantees.

---

**Q38.8: Intermediate - [Theory] - [LP Relaxation]**

Linear programming relaxation is used in approximation algorithms by:

A) Solving the exact integer program
B) Relaxing integer constraints to continuous, solving, then rounding
C) Ignoring the objective function
D) Adding random constraints

**Answer: B**

**Explanation:**
Many optimization problems: express as Integer LP (variables ∈ {0,1}). NP-hard to solve. Relaxation: allow variables in [0,1]. Solve LP in polynomial time (simplex/interior point). LP optimal ≤ ILP optimal (for minimization). Round fractional solution to integer. Rounding quality determines approximation ratio. Set Cover: randomized rounding gives O(log n). Vertex Cover: round x_v ≥ 0.5 to 1, gives 2-approximation.

---

**Q38.9: Advanced - [Theory] - [Inapproximability]**

What does it mean when a problem is "APX-hard"?

A) It has a polynomial-time exact algorithm
B) No PTAS exists for it unless P = NP
C) It can be approximated to any ratio
D) It requires exponential space

**Answer: B**

**Explanation:**
APX: class of problems with constant-factor polynomial approximation. APX-hard: at least as hard as everything in APX. If an APX-hard problem had a PTAS: all APX problems would too → would imply P = NP. Examples: metric TSP is APX-hard (no PTAS), MAX-3SAT is APX-hard. Contrast: Euclidean TSP has PTAS (not APX-hard). Inapproximability results tell us when to stop searching for better ratios.

---

**Q38.10: Intermediate - [Theory] - [Knapsack FPTAS]**

The FPTAS for 0/1 Knapsack works by:

A) Using a different objective function
B) Scaling and rounding profit values to reduce the DP table size
C) Removing the least valuable items
D) Using greedy instead of DP

**Answer: B**

**Explanation:**
Exact DP: O(n × P_max) where P_max = max profit. Pseudo-polynomial. FPTAS: scale profits by dividing by K = ε × P_max / n, round down. New DP: O(n × n/ε) = O(n²/ε) — polynomial in both n and 1/ε. Error from rounding: each item loses at most K profit → total loss ≤ n × K = ε × P_max ≤ ε × OPT. So ALG ≥ (1-ε) × OPT. Trade accuracy (ε) for speed.

---

**Q38.11: Foundational - [Theory] - [Load Balancing]**

The greedy load balancing algorithm (assign each job to the least-loaded machine) achieves what approximation ratio for makespan minimization?

A) Exact optimal
B) 2 - 1/m (where m = number of machines)
C) O(log n)
D) O(n)

**Answer: B**

**Explanation:**
Greedy (list scheduling, Graham 1966): assign each job to machine with current minimum load. Ratio: (2 - 1/m). Proof: the last-finishing machine's load ≤ average load + max job time. Average ≤ OPT, max job ≤ OPT → ratio ≤ 2 - 1/m. LPT (Longest Processing Time first — sort jobs descending first): ratio 4/3 - 1/(3m). Better but requires sorting. Both are used in practice for job scheduling.

---

**Q38.12: Advanced - [Theory] - [SDP Relaxation]**

Semidefinite Programming (SDP) relaxation gave the breakthrough for which problem?

A) Shortest path
B) MAX-CUT (Goemans-Williamson ~0.878 ratio)
C) Minimum spanning tree
D) Sorting

**Answer: B**

**Explanation:**
Goemans-Williamson (1995): relax MAX-CUT to SDP (unit vectors, maximize expected cut). Solve SDP → vectors on unit sphere. Random hyperplane rounding: expected cut ≥ 0.878 × OPT. Before: best known was 0.5 (random partition). Under Unique Games Conjecture: 0.878 is optimal — can't do better in polynomial time. SDP relaxation is strictly more powerful than LP relaxation for many problems. Landmark result in approximation algorithms.

---

**Q38.13: Intermediate - [Theory] - [Bin Packing]**

First Fit Decreasing (FFD) for bin packing achieves:

A) Exact optimal always
B) At most 11/9 × OPT + 6/9 bins
C) At most 2 × OPT bins
D) O(n) bins regardless of OPT

**Answer: B**

**Explanation:**
Bin packing: pack items of different sizes into minimum bins (capacity 1). FFD: sort items by size descending, place each in first bin with room. Ratio: ≤ 11/9 OPT + 6/9. Very close to optimal! First Fit (no sorting): ≤ 1.7 OPT. Next Fit: ≤ 2 OPT (simplest, worst ratio). Asymptotically: FFD → OPT as OPT → ∞. The 11/9 bound is tight. Used in cloud resource allocation, container packing.

---

**Q38.14: Expert - [Theory] - [Unique Games Conjecture]**

The Unique Games Conjecture (UGC), if true, implies:

A) P = NP
B) Optimal inapproximability bounds for many problems (e.g., MAX-CUT, Vertex Cover)
C) All NP-hard problems are equally hard to approximate
D) Quantum computers can solve NP-hard problems

**Answer: B**

**Explanation:**
UGC (Khot, 2002): it's hard to satisfy more than (1-ε) fraction of constraints in a unique label cover instance. If true: Vertex Cover has no (2-ε)-approximation, MAX-CUT has no (0.878+ε)-approximation, MAX-2SAT has no (0.9401+ε)-approximation — matching known algorithms exactly. Would unify inapproximability theory. Still open (neither proved nor disproved). One of the most important conjectures in theoretical CS.

---

**Q38.15: Intermediate - [Theory] - [Metric vs General TSP]**

Why does metric TSP have constant-factor approximation but general TSP does not?

A) Metric TSP has fewer cities
B) The triangle inequality allows MST-based approximations; without it, no constant ratio is possible
C) General TSP is easier to solve exactly
D) Metric TSP only works in 2D

**Answer: B**

**Explanation:**
Metric TSP: distances satisfy triangle inequality (d(a,c) ≤ d(a,b) + d(b,c)). MST-based algorithms can shortcut without increasing cost too much. General TSP: can set distance to astronomical values for specific edges, making any shortcut arbitrarily bad. Specifically: if you could approximate general TSP within any constant c, you could distinguish Hamiltonian vs non-Hamiltonian graphs → NP-hard. Triangle inequality is the key structural property enabling approximation.

---

**Q38.16: Advanced - [Theory] - [Primal-Dual Method]**

The primal-dual method for approximation algorithms works by:

A) Solving two separate problems and averaging results
B) Simultaneously constructing a feasible primal solution and dual lower bound, using their ratio as proof
C) Using two different algorithms and picking the better result
D) Dividing the problem into two halves

**Answer: B**

**Explanation:**
LP duality: primal (minimize) and dual (maximize). Weak duality: dual ≤ primal (for feasible solutions). Primal-dual: grow dual variables until some constraint becomes tight, use tight constraints to build primal solution. Ratio: primal/dual ≤ α if each step increases primal by ≤ α × dual increase. Gives both the algorithm AND the proof in one framework. Used for: Shortest path (Dijkstra is primal-dual!), Set Cover, network design.

---

**Q38.17: Foundational - [Theory] - [2-OPT for TSP]**

The 2-OPT local search heuristic for TSP works by:

A) Adding 2 cities at a time
B) Iteratively removing 2 edges and reconnecting the tour if it improves the cost
C) Splitting the tour into 2 sub-tours
D) Using 2 threads to search in parallel

**Answer: B**

**Explanation:**
2-OPT: take current tour, try all pairs of edges. Remove both, reconnect the two resulting paths in the only other way possible (reverse one segment). If new tour is shorter: accept. Repeat until no 2-edge swap improves. O(n²) per pass, may need many passes. No worst-case guarantee, but produces good tours in practice. 3-OPT and LKH (Lin-Kernighan) extend to more edges → better quality, higher cost.

---

**Q38.18: Expert - [Theory] - [Streaming Approximation]**

For distinct element counting in a data stream, the best-known algorithm uses:

A) An exact counter requiring O(n) space
B) O(1/ε² + log n) space for (1±ε)-approximation
C) O(n log n) space
D) No approximation is possible in sub-linear space

**Answer: B**

**Explanation:**
Distinct element counting: Flajolet-Martin/HyperLogLog family. Hash each element, track statistics of hash values (max leading zeros). O(1/ε² × log log n + log n) space for (1±ε)-approximation. HyperLogLog: ~12KB for ~1% error regardless of stream size. Exact counting requires Ω(n) space (must remember all distinct elements). Streaming approximation trades space for accuracy — essential for network monitoring, database cardinality estimation.

---

**Q38.19: Advanced - [Theory] - [Facility Location]**

The facility location problem asks for:

A) The shortest path between facilities
B) Where to open facilities to minimize total opening cost plus client-to-facility connection cost
C) How to sort facilities by cost
D) The maximum number of facilities that can be opened

**Answer: B**

**Explanation:**
Facility location: given potential sites (opening costs) and clients (connection costs), minimize total cost = Σ(opening costs of opened facilities) + Σ(connection cost of each client to nearest open facility). NP-hard. LP-rounding: 4-approximation. Primal-dual: 3-approximation. Local search: 1.488+ε-approximation (best known). Applications: warehouse placement, server placement, k-median clustering. Related to k-means and k-median problems.

---

**Q38.20: Intermediate - [Theory] - [Greedy vs Optimal Approximation]**

For the maximum weight independent set problem on general graphs:

A) A 2-approximation exists
B) A PTAS exists
C) No constant-factor approximation is possible unless P = NP
D) The greedy algorithm gives exact solutions

**Answer: C**

**Explanation:**
Maximum Independent Set on general graphs: under standard assumptions, cannot be approximated within n^(1-ε) for any ε > 0. One of the hardest problems to approximate — essentially no useful approximation exists for general graphs. However: on trees → exact O(n) DP. On planar graphs → PTAS. On interval graphs → exact greedy. Graph structure dramatically affects approximability. Shows that inapproximability can be as strong as exact hardness.

---

## Chapter 38 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | Approximation ratios, set cover greedy, MAX-CUT random, load balancing, 2-OPT |
| Intermediate | 8 | Vertex cover, Christofides, PTAS, LP relaxation, FPTAS knapsack, bin packing, metric TSP |
| Advanced | 4 | Inapproximability, SDP, primal-dual, facility location |
| Expert | 3 | UGC, streaming approximation, max independent set hardness |

**Total MCQs: 20**

**Answer Distribution: A=4, B=14, C=1, D=1**

**Next:** Chapter 39 - External Memory Algorithms
