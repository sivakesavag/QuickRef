# Chapter 42: Comprehensive Review & Mixed Problems

**Target:** 30 MCQs | **Distribution:** 8 Foundational, 12 Intermediate, 7 Advanced, 3 Expert

This chapter draws from ALL parts of the book, mixing topics to test integrated understanding.

---

**Q42.1: Foundational - [Theory] - [Data Structure Selection]**

You need O(1) average insertion AND O(1) average lookup by key. Which data structure is best?

A) Balanced BST
B) Hash table
C) Sorted array
D) Linked list

**Answer: B**

**Explanation:**
Hash table: O(1) average insert, O(1) average lookup (with good hash function and load factor). BST: O(log n) both. Sorted array: O(log n) search but O(n) insertion (shifting). Linked list: O(1) insert (prepend) but O(n) lookup. Hash table is the only structure with O(1) average for both operations. Trade-off: no ordering (can't do range queries), worst case O(n) with bad hash.

---

**Q42.2: Foundational - [Complexity] - [Recurrence Relations]**

T(n) = 2T(n/2) + n. What is T(n)?

A) O(n)
B) O(n log n)
C) O(n²)
D) O(log n)

**Answer: B**

**Explanation:**
Master Theorem Case 2: a=2, b=2, f(n)=n. log_b(a) = log₂ 2 = 1. f(n) = n = Θ(n^1) = Θ(n^(log_b a)). Case 2: T(n) = Θ(n log n). This is the recurrence for merge sort: divide into 2 halves (2T(n/2)), merge in O(n). Also applies to many divide-and-conquer algorithms with balanced splits and linear combination.

---

**Q42.3: Intermediate - [Theory] - [Graph Representation]**

For a sparse graph with V=10,000 nodes and E=50,000 edges, which representation is more memory-efficient?

A) Adjacency matrix: O(V²) = 10⁸ entries
B) Adjacency list: O(V + E) = 60,000 entries
C) Both use the same space
D) Edge list: O(E) = 50,000 entries

**Answer: B**

**Explanation:**
Adjacency matrix: V² = 10⁸ entries (mostly zeros for sparse graph — 99.9% empty). Adjacency list: V + 2E = 110,000 pointers/entries. Edge list (D): even more compact but slower for neighbor lookup. For sparse graphs (E << V²): adjacency list saves orders of magnitude of space. For dense graphs (E ≈ V²): matrix is fine and has O(1) edge lookup. Most real-world graphs are sparse → adjacency list preferred.

---

**Q42.4: Intermediate - [Trace] - [Stack Operations]**

Given operations: push(3), push(7), push(1), pop(), push(5), pop(), pop(). What is the final stack state (bottom to top)?

A) [3]
B) [3, 7]
C) [3, 5]
D) [7]

**Answer: A**

**Explanation:**
push(3): [3]. push(7): [3,7]. push(1): [3,7,1]. pop() → removes 1: [3,7]. push(5): [3,7,5]. pop() → removes 5: [3,7]. pop() → removes 7: [3]. Final stack: [3]. LIFO: each pop removes the most recently pushed element. Three pushes, three pops = net one element remaining.

---

**Q42.5: Intermediate - [Complexity] - [Nested Loops]**

```
for i in range(n):
    for j in range(i, n):
        process(i, j)
```

How many times is `process` called?

A) n
B) n²
C) n(n+1)/2
D) n log n

**Answer: C**

**Explanation:**
Outer loop: i from 0 to n-1. Inner loop: j from i to n-1, so n-i iterations. Total: Σ(n-i) for i=0..n-1 = n + (n-1) + ... + 1 = n(n+1)/2. This is O(n²) but exactly half of n² (upper triangle of n×n matrix). Common pattern in algorithms comparing all pairs (but only once each). Examples: bubble sort comparisons, checking all pairs in array.

---

**Q42.6: Advanced - [Theory] - [Algorithm Design Paradigms]**

Which problem is best solved by dynamic programming rather than greedy?

A) Activity selection (maximum non-overlapping intervals)
B) 0/1 Knapsack (items with weights and values)
C) Minimum spanning tree
D) Huffman coding

**Answer: B**

**Explanation:**
0/1 Knapsack: greedy (by value/weight ratio) fails because you can't take fractions. Must consider all inclusion/exclusion combinations → DP. Activity selection: greedy (earliest finish first) works optimally. MST: greedy (Kruskal/Prim). Huffman coding: greedy (merge two least frequent). Key test: if locally optimal choice doesn't guarantee globally optimal → need DP. Knapsack counterexample: items {(weight=3,value=4), (2,3), (2,3)}, capacity=4.

---

**Q42.7: Foundational - [Theory] - [Tree Traversal]**

Which tree traversal visits nodes in sorted order for a Binary Search Tree?

A) Pre-order (root, left, right)
B) In-order (left, root, right)
C) Post-order (left, right, root)
D) Level-order (BFS)

**Answer: B**

**Explanation:**
BST property: left subtree keys < root < right subtree keys. In-order: visit left (all smaller), root, right (all larger) → sorted order. Pre-order: root first — useful for serialization/reconstruction. Post-order: root last — useful for deletion (children before parent). Level-order: breadth-first — useful for finding depth. Only in-order exploits the BST ordering property to produce sorted output.

---

**Q42.8: Intermediate - [Theory] - [Shortest Path Algorithm Selection]**

For shortest paths from a single source in a graph with negative edge weights but no negative cycles, which algorithm should you use?

A) Dijkstra's algorithm
B) Bellman-Ford algorithm
C) Floyd-Warshall algorithm
D) BFS

**Answer: B**

**Explanation:**
Dijkstra: FAILS with negative weights (greedy assumption violated — finalized distance may not be optimal). BFS: only for unweighted graphs. Floyd-Warshall: all-pairs, O(V³), overkill for single-source. Bellman-Ford: O(VE), handles negative weights correctly by relaxing all edges V-1 times. Detects negative cycles (if V-th iteration still improves). Correct choice for negative-weight single-source shortest paths.

---

**Q42.9: Foundational - [Theory] - [Hashing Collision Resolution]**

In open addressing with linear probing, what causes performance degradation?

A) Hash table being too large
B) Primary clustering — contiguous occupied slots forming long chains
C) Too few elements in the table
D) Using prime-sized tables

**Answer: B**

**Explanation:**
Linear probing: collision → check next slot, then next, etc. Clusters form: full slots attract more collisions (new elements hash near cluster → extend it). Cluster length grows super-linearly. At load factor 0.75: average probe count ~2.5 (acceptable). At 0.9: ~5.5 (degraded). At 0.99: ~50 (terrible). Fixes: double hashing (different step sizes), Robin Hood hashing (swap with shorter probe distance), or keep load factor ≤ 0.7.

---

**Q42.10: Advanced - [Theory] - [Amortized Analysis]**

Dynamic array (ArrayList) doubling has O(1) amortized insertion cost. What does "amortized" mean here?

A) Each individual insertion takes O(1) time
B) The average cost per insertion is O(1) when spread over n insertions, even though some individual insertions cost O(n)
C) The worst-case insertion is O(1)
D) Only the first insertion is O(1)

**Answer: B**

**Explanation:**
Amortized: total cost / number of operations. n insertions: most are O(1) (append). Occasional resize: copy all elements O(n). With doubling: resizes at sizes 1, 2, 4, 8, ..., n. Total copy cost: 1+2+4+...+n = 2n-1 = O(n). Average: O(n)/n = O(1) per insertion. Key: "amortized O(1)" ≠ "worst-case O(1)." Any single insertion might cost O(n), but averaged over n operations, the cost per operation is O(1).

---

**Q42.11: Intermediate - [Theory] - [NP-Completeness]**

A problem is NP-complete if:

A) It can be solved in polynomial time
B) It is in NP and every problem in NP can be reduced to it in polynomial time
C) It has no solution
D) It requires exponential space

**Answer: B**

**Explanation:**
NP: verifiable in polynomial time (given a solution, check if correct quickly). NP-hard: every NP problem reduces to it (at least as hard as anything in NP). NP-complete: NP-hard AND in NP. Examples: SAT, 3-SAT, Vertex Cover, Hamiltonian Path, TSP decision. If ANY NP-complete problem has polynomial solution → P=NP (all NP problems become polynomial). Cook-Levin theorem proved SAT is NP-complete.

---

**Q42.12: Foundational - [Theory] - [When to Use Which Structure]**

You need to maintain a collection supporting: insert, delete, and find-minimum — all efficiently. Best data structure?

A) Sorted array
B) Hash table
C) Min-heap (priority queue)
D) Stack

**Answer: C**

**Explanation:**
Min-heap: insert O(log n), delete-min O(log n), find-min O(1). Perfect for this combination. Sorted array: insert O(n) (shifting). Hash table: no efficient find-min (would need O(n) scan). Stack: only accesses top element. If you also need arbitrary delete: consider balanced BST O(log n) for all three. Fibonacci heap: O(1) amortized insert, O(log n) amortized delete-min. Choose based on exact operation mix.

---

**Q42.13: Advanced - [Theory] - [Reduction]**

To prove problem X is NP-hard, you should:

A) Reduce X to a known NP-hard problem
B) Reduce a known NP-hard problem to X
C) Show X has exponential running time
D) Show X is in P

**Answer: B**

**Explanation:**
Direction matters! Reduce KNOWN hard problem → X. This shows: "X is at least as hard as the known problem." If known-hard ≤_p X: solving X would solve the known-hard problem, so X must also be hard. Common mistake: reducing X to known-hard only shows "X is at most as hard as known-hard" (not useful for proving hardness). Example: reduce 3-SAT to Vertex Cover to prove Vertex Cover is NP-hard.

---

**Q42.14: Intermediate - [Complexity] - [Algorithm Comparison]**

For finding the k-th largest element in an unsorted array of n elements, which approach is most efficient on average?

A) Sort the array O(n log n), then index
B) Use a min-heap of size k, scan all elements: O(n log k)
C) Quickselect: O(n) average
D) Check all elements k times: O(nk)

**Answer: C**

**Explanation:**
Quickselect: partition (like quicksort), recurse only on the side containing position k. Average: T(n) = T(n/2) + O(n) = O(n). Best average case. Heap O(n log k): good when k is small but has logarithmic factor. Full sort O(n log n): more work than needed. O(nk): brute force, worst for large k. Median-of-medians gives O(n) worst case but with larger constant. In practice: Quickselect with random pivot is fastest.

---

**Q42.15: Intermediate - [Theory] - [Graph Cycle Detection]**

Which algorithm detects cycles in a directed graph?

A) Union-Find
B) DFS with coloring (white/gray/black) — a back edge indicates a cycle
C) BFS only
D) Prim's algorithm

**Answer: B**

**Explanation:**
DFS coloring: white = unvisited, gray = in current DFS path, black = fully processed. If DFS reaches a gray node: back edge → cycle found. Union-Find detects cycles in undirected graphs (not directed — unioning directed endpoints can miss direction). BFS: can detect cycles in undirected (if visited node found that isn't parent) but not straightforward for directed. Kahn's algorithm (topological sort): also detects directed cycles (if sort doesn't include all nodes).

---

**Q42.16: Foundational - [Theory] - [Stable Sort Importance]**

When sorting database records by multiple fields, stability is important because:

A) Stable sorts are always faster
B) Stable sort preserves the relative order of records with equal keys from previous sorts
C) Unstable sorts produce incorrect results
D) Stability reduces memory usage

**Answer: B**

**Explanation:**
Multi-key sort: sort by secondary key first, then by primary with stable sort. Stability ensures secondary ordering is preserved within equal primary keys. Example: sort students by name (stable), then by grade → students with same grade remain sorted by name. Without stability: secondary ordering lost. Unstable sort still produces correctly sorted output by primary key — but loses the secondary ordering (not "incorrect" but less useful).

---

**Q42.17: Advanced - [Theory] - [Trade-offs Across Chapters]**

B-Trees (Ch33), Skip Lists (Ch36), and Red-Black Trees (Ch10) all support O(log n) search. What makes B-Trees uniquely suited for databases?

A) B-Trees are simpler to implement
B) B-Trees match disk block size with high fanout, minimizing I/O operations
C) B-Trees have faster CPU performance
D) B-Trees use less memory

**Answer: B**

**Explanation:**
B-Tree node = disk block (4-16KB). Fanout ~100-1000. Height: log_B(n) ≈ 3-4 for billions of records = 3-4 disk reads. Red-Black/AVL: fanout 2, height ~log₂(n) ≈ 30 for same data = 30 disk reads. Skip list: randomized, not block-aligned. In memory (no disk I/O): RB-tree and skip list perform comparably to B-Tree. The block-aligned design is specifically optimized for the disk I/O bottleneck.

---

**Q42.18: Intermediate - [Theory] - [Space-Time Trade-offs]**

Which pair correctly demonstrates a space-time trade-off?

A) Hash table (O(n) space, O(1) lookup) vs linear scan (O(1) space, O(n) lookup)
B) Merge sort vs quicksort (same time, same space)
C) BFS vs DFS (same time, same space)
D) Insertion sort vs selection sort (identical algorithms)

**Answer: A**

**Explanation:**
Hash table: uses O(n) extra space but achieves O(1) average lookup. Linear scan: no extra space (O(1)) but O(n) lookup. Classic trade-off: spend memory to save time. Other examples: memoization (cache results, avoid recomputation), precomputation tables, Bloom filters (compact space, allow false positives). Most algorithm design involves navigating space-time trade-offs. Understanding these choices is a core engineering skill.

---

**Q42.19: Expert - [Theory] - [Lower Bounds Across Domains]**

Which statement about lower bounds is INCORRECT?

A) Comparison sorting: Ω(n log n)
B) External sorting: Ω((n/B) × log_{M/B}(n/B)) I/Os
C) Element distinctness: Ω(n log n) in algebraic decision tree model
D) Searching in a sorted array: Ω(n)

**Answer: D**

**Explanation:**
Searching a sorted array: binary search achieves O(log n), and Ω(log n) is the lower bound (not Ω(n)). All other bounds are correct: comparison sorting Ω(n log n) (decision tree), external sorting Ω((n/B) log_{M/B}(n/B)) (I/O model), element distinctness Ω(n log n) (algebraic decision tree — Ben-Or). D is incorrect because it claims Ω(n) aka linear lower bound, when the true lower bound is Ω(log n).

---

**Q42.20: Intermediate - [Theory] - [Choosing Algorithms in Practice]**

Your application needs to process 10⁸ integers finding duplicates. Memory is limited to 100MB. Best approach?

A) Hash set: O(n) time, but needs ~800MB for 10⁸ integers — doesn't fit
B) Sort the array in-place, then scan for adjacent duplicates: O(n log n) time, O(1) extra space
C) Compare all pairs: O(n²) time
D) Binary search each element: O(n log n) but needs sorted data

**Answer: B**

**Explanation:**
10⁸ integers × 8 bytes = 800MB for hash set — exceeds 100MB limit. In-place sort (quicksort/introsort): O(n log n), modifies array in place (O(log n) stack). Then linear scan for adjacent duplicates: O(n). Total: O(n log n) time, O(1) extra space. Alternative: Bloom filter with ~12 bits per element = 150MB — also exceeds limit. External sort if data doesn't fit in RAM. Real-world constraints often eliminate theoretically optimal algorithms.

---

**Q42.21: Expert - [Theory] - [P vs NP Implications]**

If P = NP were proven, which statement would be TRUE?

A) All algorithms would become faster
B) Every problem with a polynomial-time verifier would also have a polynomial-time solver
C) Quantum computers would become unnecessary
D) Sorting would become O(n)

**Answer: B**

**Explanation:**
P = NP means: every problem where solutions can be VERIFIED in polynomial time can also be SOLVED in polynomial time. SAT, TSP, graph coloring — all solvable efficiently. Practical impact: some cryptography broken (but not information-theoretic crypto). A, C, D are wrong: sorting is already in P, quantum computers address different problems, and existing fast algorithms don't change. Note: most computer scientists believe P ≠ NP. A proof of P = NP would be the biggest mathematical result in history.

---

**Q42.22: Advanced - [Theory] - [Cross-Topic Integration]**

A social network needs to answer "what is the shortest path between any two users?" for 10⁹ users. Which approach is feasible?

A) Floyd-Warshall: O(V³) — compute all-pairs once
B) Pre-compute nothing, run BFS on demand for each query
C) Bidirectional BFS from both users, meeting in the middle
D) Store the complete distance matrix

**Answer: C**

**Explanation:**
V = 10⁹. Floyd-Warshall O(V³) = 10²⁷ — impossible. Distance matrix: V² = 10¹⁸ entries — can't store. BFS from source: explores potentially billions of nodes per query — too slow. Bidirectional BFS: explore from BOTH endpoints simultaneously. In social networks ("six degrees"): meets in ~3 hops from each side. Explores O(k³) where k = average branching factor, meeting in O(√V) nodes explored. Facebook uses this with approximations.

---

**Q42.23: Foundational - [Theory] - [Recursion vs Iteration]**

Every recursive algorithm can be converted to an iterative one because:

A) Recursion is always faster
B) The system call stack can be replaced by an explicit stack data structure
C) Iteration uses recursion internally
D) They use different hardware

**Answer: B**

**Explanation:**
Recursion uses the system call stack to save state (local variables, return address) at each recursive call. An explicit stack data structure can simulate this: push state when "recursing," pop when "returning." Tail recursion: can be converted to a simple loop (no stack needed). DFS: recursive → use explicit stack. Tree traversals: Morris traversal eliminates even the explicit stack using threaded trees. Iterative versions often use less memory.

---

**Q42.24: Intermediate - [Theory] - [Distributed Algorithm Choice]**

For a distributed cache needing eventual consistency, very high availability, and partition tolerance, which DS/algorithm combination fits?

A) B-Tree with two-phase locking (strong consistency)
B) Consistent hashing + CRDTs + gossip protocol (AP system)
C) Single-server red-black tree (no distribution)
D) Paxos consensus on every operation (strong consistency, lower availability)

**Answer: B**

**Explanation:**
Requirements: eventual consistency + high availability + partition tolerance = AP choice (CAP theorem). Consistent hashing: distribute keys across nodes, minimal reshuffling on node changes. CRDTs: conflict-free data types that converge without coordination. Gossip: disseminate updates probabilistically, O(log n) convergence. This is essentially the architecture of Cassandra, Riak, DynamoDB. Strong consistency (A, D) sacrifices availability during partitions — wrong trade-off for this requirement.

---

**Q42.25: Expert - [Theory] - [Algorithm Design Meta-Principles]**

The single most important principle in algorithm design is:

A) Always use the most complex algorithm available
B) Reduce the problem to a known solved problem or paradigm
C) Optimize for the worst case only
D) Always choose O(n) algorithms

**Answer: B**

**Explanation:**
Core principle: recognize the structure of your problem and map it to known solutions. "Is this a shortest path problem?" → Dijkstra/BFS. "Does it have optimal substructure + overlapping subproblems?" → DP. "Can I eliminate half the search space?" → Binary search / D&C. "Is a greedy choice always optimal?" → Greedy. Most "new" problems are variations of known patterns. Learning the paradigms (DP, greedy, D&C, graph algorithms, reductions) is more valuable than memorizing individual algorithms.

---

## Chapter 42 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 7 | Data structure selection, recurrence, tree traversal, hashing, recursion vs iteration |
| Intermediate | 10 | Graph representation, stack trace, nested loops, shortest path, NP-completeness, cycle detection, stability, practical constraints |
| Advanced | 5 | Amortized analysis, reductions, cross-topic integration, trade-offs, B-Tree comparison |
| Expert | 3 | Lower bounds, P vs NP, algorithm design meta-principles |

**Total MCQs: 25**

**Answer Distribution: A=3, B=17, C=4, D=1**

**Question Types: Theory=20, Trace=1, Complexity=3, Code=1**

---

## End of Part VII — Expert-Level & Rare Scenarios

**Part VII Total: 105 MCQs across 5 chapters**

| Chapter | MCQs | Topics |
|---------|-------|--------|
| 38. Approximation Algorithms | 20 | Ratios, vertex cover, TSP, PTAS/FPTAS, LP/SDP relaxation, inapproximability |
| 39. External Memory | 20 | I/O model, external sort, B-Tree, cache-oblivious, buffer trees, lower bounds |
| 40. Streaming Algorithms | 20 | Sketches, Bloom filters, HyperLogLog, sampling, frequency moments |
| 41. Quantum Computing | 20 | Qubits, Grover, Shor, QFT, error correction, post-quantum |
| 42. Comprehensive Review | 25 | Cross-topic integration, paradigm selection, practical trade-offs |
