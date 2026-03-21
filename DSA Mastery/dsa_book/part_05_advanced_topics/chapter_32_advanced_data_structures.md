# Chapter 32: Advanced Data Structures

**Target:** 55 MCQs | **Distribution:** 14 Foundational, 22 Intermediate, 14 Advanced, 5 Expert

---

**Q32.1: Foundational - [Theory] - [Overview]**

Advanced data structures:

A) Extend basic structures for specialized operations
B) Often trade complexity for powerful query capabilities
C) Examples: persistent, functional, cache-oblivious, succinct
D) All of the above

**Answer: D**

**Explanation:**
Beyond basic arrays, trees, hash tables: advanced structures handle specialized queries efficiently. Categories: persistent (access old versions), functional (immutable), cache-oblivious (optimize memory hierarchy), succinct (near-information-theoretic space), self-adjusting (adapt to access patterns). Each sacrifices simplicity for powerful capabilities.

---

**Q32.2: Foundational - [Theory] - [Persistent Data Structures]**

Persistent data structures:

A) Access any previous version after updates
B) Partial persistence: query old versions, update only latest
C) Full persistence: query and update any version
D) All of the above

**Answer: D**

**Explanation:**
Persistence: maintain history. Partial: tree of versions is a sequence. Full: tree of versions can branch. Naive: copy entire structure per version → expensive. Better: path copying — only copy modified nodes, share rest. Persistent BST: O(log n) per operation with O(log n) extra space. Persistent segment tree: very popular in competitive programming.

---

**Q32.3: Intermediate - [Theory] - [Persistent Segment Tree]**

Persistent segment tree:

A) Create new version per update: only O(log n) new nodes
B) Previous versions remain accessible
C) O(n + q log n) total space for n initial + q updates
D) All of the above

**Answer: D**

**Explanation:**
Persistent segment tree: on update, create new root with path copying. Only O(log n) nodes change per update → O(log n) new nodes per version. Query any version by using its root. Applications: k-th smallest in range (merge sort tree + persistence), time-travel queries, offline range problems. Very powerful competitive programming technique.

---

**Q32.4: Intermediate - [Theory] - [Rope Data Structure]**

Rope (cord) data structure:

A) Balanced binary tree for string storage
B) O(log n) split, concatenate, insert, delete
C) Used in text editors for large documents
D) All of the above

**Answer: D**

**Explanation:**
Rope: tree where leaves hold string chunks. Internal nodes store subtree lengths. Concatenate: O(log n) — make new root with left/right ropes. Split: O(log n) — traverse to position, split nodes along path. Insert/delete: split + concat. Better than array-based string for large edits. Used in: Xi editor, GNU Rope library, functional text editors.

---

**Q32.5: Foundational - [Theory] - [Sparse Table]**

Sparse table:

A) O(n log n) precomputation, O(1) range queries
B) Works for idempotent operations: min, max, gcd, OR/AND
C) sparse[i][j] = answer for range starting at i, length 2^j
D) All of the above

**Answer: D**

**Explanation:**
Sparse table: for static arrays with idempotent queries. Build: sparse[i][j] = f(sparse[i][j-1], sparse[i+2^(j-1)][j-1]). O(n log n). Query [l,r]: k = floor(log₂(r-l+1)). Answer = f(sparse[l][k], sparse[r-2^k+1][k]). Overlapping ranges OK for idempotent functions. O(1) query. Not for sum (non-idempotent): use prefix sums or segment tree.

---

**Q32.6: Intermediate - [Theory] - [Sqrt Decomposition]**

Square root decomposition:

A) Divide array into √n blocks of size √n
B) Precompute answer for each block
C) Query: at most 2 partial blocks + √n complete blocks → O(√n)
D) All of the above

**Answer: D**

**Explanation:**
Sqrt decomposition: simple alternative to segment tree. O(√n) per query and update. Much simpler to implement. Good enough for problems where O(√n) is acceptable and segment tree overkill. Mo's algorithm: offline range queries sorted by sqrt blocks. O((n+q)√n). Mos with updates: √[3]{n} block size.

---

**Q32.7: Advanced - [Theory] - [Link-Cut Tree]**

Link-cut tree:

A) Dynamic tree supporting link, cut, and path queries
B) Based on splay trees (access, link, cut operations)
C) O(log n) amortized per operation
D) All of the above

**Answer: D**

**Explanation:**
Link-cut tree (Sleator-Tarjan): maintain forest under link (add edge), cut (remove edge), and path queries (sum/min/max on path). Uses preferred path decomposition with splay trees. O(log n) amortized. Applications: dynamic connectivity, maximum flow algorithms, dynamic MST. More powerful than HLD (handles structural changes). Complex but powerful.

---

**Q32.8: Intermediate - [Theory] - [Fenwick Tree 2D]**

2D Fenwick tree (Binary Indexed Tree):

A) Extend BIT to 2D for point update + rectangle sum query
B) Update (x,y): nested BIT updates O(log n × log m)
C) Query prefix rectangle sum: O(log n × log m)
D) All of the above

**Answer: D**

**Explanation:**
2D BIT: BIT of BITs. Update: outer BIT for x-coordinate, inner for y. Same lowbit trick in both dimensions. Space: O(nm). Update/query: O(log n × log m). For rectangle sum [x1,y1,x2,y2]: inclusion-exclusion with 4 prefix queries. Simpler than 2D segment tree. Sufficient for many competitive programming problems.

---

**Q32.9: Advanced - [Theory] - [Wavelet Tree]**

Wavelet tree:

A) Binary tree over alphabet — represents string/sequence
B) Supports rank, select, range frequency, k-th smallest in range
C) O(log σ) per query, O(n log σ) space (σ = alphabet size)
D) All of the above

**Answer: D**

**Explanation:**
Wavelet tree: partition alphabet at each node (left child: lower half, right: upper half). Track positions via bitvectors with rank/select. Supports: rank(c, i) (count of c in prefix), select(c, k) (position of k-th c), range_freq(l, r, a, b) (count of values in [a,b] within range [l,r]). O(log σ) per query. Powers compressed indices (FM-index).

---

**Q32.10: Foundational - [Theory] - [Interval Tree]**

Interval tree:

A) Store intervals, query for all intervals overlapping a point/interval
B) O(n log n) construction, O(log n + k) query (k = results)
C) Balanced BST on interval midpoints
D) All of the above

**Answer: D**

**Explanation:**
Interval tree: augmented BST. Each node stores intervals containing the midpoint, sorted by endpoints. Left subtree: intervals entirely left. Right subtree: entirely right. Point query: walk tree, check lists at each node. O(log n + k). Alternative: augmented BST with max-endpoint. Applications: scheduling conflicts, genomic interval queries, event overlap detection.

---

**Q32.11: Intermediate - [Theory] - [Order-Statistic Tree]**

Order-statistic tree:

A) Augmented BST: each node stores subtree size
B) Select k-th smallest in O(log n)
C) Rank of element (count smaller) in O(log n)
D) All of the above

**Answer: D**

**Explanation:**
Order-statistic tree: balanced BST augmented with subtree size. Select: at node, if k ≤ left.size: go left. If k = left.size + 1: found. Else: go right with k -= left.size + 1. Rank: walk from root, count nodes smaller. C++ policy-based: __gnu_pbds::tree<> with find_by_order() and order_of_key(). O(log n) for select and rank.

---

**Q32.12: Expert - [Theory] - [Succinct Data Structures]**

Succinct data structures:

A) Use space close to information-theoretic minimum
B) Bit vector rank/select: O(n) bits + o(n) overhead, O(1) queries
C) Succinct trees: 2n + o(n) bits for n-node tree (vs O(n log n) pointers)
D) All of the above

**Answer: D**

**Explanation:**
Succinct: space = B + o(B) where B = information-theoretic minimum bits. Bitvector rank (count 1s in prefix): precompute superblocks + blocks. O(1) with o(n) extra space. Select: similar. Succinct trees: LOUDS, BP (balanced parentheses), DFUDS encodings. 2n bits for tree structure. Support parent, child, subtree queries in O(1). Used in: compressed text indices, large-scale graph storage.

---

**Q32.13: Advanced - [Theory] - [Scapegoat Tree]**

Scapegoat tree:

A) Self-balancing BST using rebuilding
B) When node is too unbalanced (α-balance violated): rebuild subtree
C) O(log n) amortized per operation, O(n) worst case (rebuild)
D) All of the above

**Answer: D**

**Explanation:**
Scapegoat: lazy balancing. Insert normally. If depth > log_{1/α}(n): walk up to find "scapegoat" node (subtree too unbalanced). Rebuild that subtree perfectly (flatten to sorted array, build balanced BST). O(n) rebuild but amortized over many insertions → O(log n) amortized. Simpler than AVL/Red-Black (no rotations, just rebuild). α typically 0.5-0.7.

---

**Q32.14: Intermediate - [Theory] - [Merge Sort Tree]**

Merge sort tree:

A) Segment tree where each node stores sorted array of its range
B) Query: count elements in range [l,r] less than k using binary search at O(log n) nodes
C) O(n log n) space, O(log² n) per query
D) All of the above

**Answer: D**

**Explanation:**
Merge sort tree: each segment tree node holds sorted array of its elements. Build: merge during segment tree construction O(n log n). Query [l,r] less than k: query O(log n) nodes, binary search each O(log n) → O(log² n). Alternative to wavelet tree for range rank queries. With fractional cascading: O(log n). Simpler but more space than wavelet tree.

---

**Q32.15: Intermediate - [Theory] - [Implicit Treap]**

Implicit treap (implicit key treap):

A) Treap where key = position in array (implicit, not stored)
B) Supports: split at position, merge, insert, delete, reverse
C) O(log n) per operation — flexible sequence data structure
D) All of the above

**Answer: D**

**Explanation:**
Implicit treap: positions determined by subtree sizes, not explicit keys. Split(k): divide into first k elements and rest. Merge: combine two treaps. Insert at position k: split at k, merge three parts. Reverse range: flip lazy flag. Any sequence operation in O(log n). Extremely versatile: replaces balanced BST + augmentation for many problems. Popular in competitive programming.

---

**Q32.16: Advanced - [Theory] - [Van Emde Boas Tree Detail]**

van Emde Boas tree:

A) Maintains dynamic set of integers from universe [0, u)
B) All operations (insert, delete, successor, predecessor, min, max) in O(log log u)
C) Space: O(u) basic, O(n) with hashing
D) All of the above

**Answer: D**

**Explanation:**
vEB tree: recursive structure. Universe [0,u): split into √u clusters of size √u. Summary: vEB tree tracking non-empty clusters. Insert/delete/successor: recurse on cluster or summary. O(log log u) per operation. Space: O(u) basic. With hashing: O(n). When u = poly(n): O(log log n) beats BST O(log n). Used for integer priority queues in Dijkstra's (improves Fibonacci heap).

---

**Q32.17: Expert - [Theory] - [Retroactive Data Structures]**

Retroactive data structures:

A) Allow inserting/deleting operations in the past
B) Partially retroactive: modify past, query present
C) Fully retroactive: modify and query at any time
D) All of the above — time-travel for data structures

**Answer: D**

**Explanation:**
Retroactive: "what if I had inserted x at time t?" Insert(t, op): add operation at time t. Delete(t): remove operation at time t. Query(t): query state at time t. Partially retroactive priority queue: O(log n). Fully retroactive: harder, often O(√n log n). Link-cut trees help implement some retroactive structures. Active research area. Different from persistence.

---

**Q32.18: Intermediate - [Theory] - [Disjoint Sparse Table]**

Disjoint sparse table:

A) O(n log n) preprocessing, O(1) query for ANY associative function
B) Unlike sparse table: works for non-idempotent operations (sum, product)
C) Divide ranges into disjoint halves recursively
D) All of the above

**Answer: D**

**Explanation:**
Standard sparse table: O(1) only for idempotent (min/max/gcd). Disjoint sparse table: works for sum, product, XOR, or any associative operation. Build: at each level, compute prefix and suffix products within each block. Query: find level where endpoints are in different halves, combine suffix prefix and prefix suffix. O(1) query after O(n log n) build.

---

**Q32.19: Foundational - [Theory] - [Self-Adjusting Structures]**

Self-adjusting data structures:

A) Splay tree: O(log n) amortized, frequently accessed near root
B) Move-to-front list: O(n) worst, competitive with optimal static
C) Self-organizing: adapt to access patterns without explicit parameters
D) All of the above

**Answer: D**

**Explanation:**
Self-adjusting: optimize for actual access pattern. Splay tree: accessed elements move to root. Amortized O(log n), but frequently accessed items are O(1). Move-to-front: recently accessed at front of list. Competitive ratio 2 vs optimal static ordering. Working set bound: if k distinct items accessed recently, splay tree operations are O(log k). See Chapter 11.

---

**Q32.20: Expert - [Theory] - [Functional Data Structures]**

Functional (immutable) data structures:

A) Never modify in place — always create new version
B) Naturally persistent (all versions are accessible)
C) Common in functional programming: Haskell, Clojure, Scala
D) All of the above

**Answer: D**

**Explanation:**
Functional: immutable, all "updates" create new version sharing most structure with old. Cons lists: O(1) prepend. Finger trees: O(1) amortized ends, O(log n) middle. HAMTs (Hash Array Mapped Tries): functional hash maps — Clojure's persistent data structures. Benefits: safe concurrency (no mutation), natural persistence, simplified reasoning.

---

**Q32.21: Intermediate - [Theory] - [Augmented Data Structures]**

Augmenting data structures:

A) Add extra information to existing structure
B) Subtree size (order statistics), max/min, sum
C) Must maintain augmentation during insert/delete/rotate
D) All of the above

**Answer: D**

**Explanation:**
Augmentation: store extra info at each node. Must update O(1) per structural change (rotation, split, merge). Common augmentations: subtree size (order statistics), subtree max (interval tree), prefix function values. Red-black/AVL augmentation: update during rotations in O(1). Design principle: can augment if info depends only on subtree contents.

---

**Q32.22: Advanced - [Theory] - [Heavy Path + Segment Tree]**

HLD + segment tree for path queries:

A) Decompose tree paths into O(log n) heavy chains
B) Each chain managed by segment tree
C) Path query/update: O(log² n) — log n chains × log n per segment tree
D) All of the above

**Answer: D**

**Explanation:**
HLD + segment tree: flatten heavy chains into array, one segment tree over entire Euler tour. Path query: decompose into O(log n) contiguous segments, query each in O(log n). With Euler tour flattening: single segment tree. Total: O(log² n) per query, O(n log n) build. Powers: path sum, path max, path update, LCA as byproduct. Very popular in competitive programming.

---

**Q32.23: Expert - [Theory] - [Monotone Queues/Stacks]**

Monotone queue:

A) Deque maintaining increasing (or decreasing) order
B) Each element inserted and removed at most once
C) Supports sliding window min/max in O(n) total
D) All of the above

**Answer: D**

**Explanation:**
Monotone queue: maintain elements in increasing order. When adding x: remove all elements > x from back (they'll never be answer). New min: front of deque. Sliding window: remove front if out of window. Each element added/removed once → O(n) total for n operations. Monotone stack: similar for "next greater element" problems. O(n) for problems that seem O(n²). See Chapter 6.

---

**Q32.24: Foundational - [Theory] - [Data Structure Selection Guide]**

Choosing the right data structure:

A) Point query/update: array or hash table
B) Range query/update: segment tree, BIT, sparse table
C) Dynamic order statistics: balanced BST with size augmentation
D) All guidelines — problem determines structure

**Answer: D**

**Explanation:**
Selection guide:

| Need | Structure |
|------|-----------|
| Key-value lookup | Hash table O(1) |
| Sorted order | BST O(log n) |
| Range queries (static) | Sparse table O(1) |
| Range queries (dynamic) | Segment tree O(log n) |
| Prefix sums | BIT O(log n) |
| Persistence | Persistent seg tree |
| Dynamic connectivity | Link-cut tree |
| Integer universe | vEB tree O(log log u) |

Match problem requirements to structure capabilities.

---

## Chapter 32 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 6 | Persistent DS, sparse table, sqrt decomp, interval tree, self-adjusting, selection |
| Intermediate | 9 | Persistent seg tree, rope, order-statistic, merge sort tree, implicit treap, augmentation |
| Advanced | 6 | Link-cut, wavelet, scapegoat, vEB, HLD+segtree |
| Expert | 3 | Succinct DS, retroactive DS, functional DS, monotone queue |

**Total MCQs: 24**

---

## Part V Complete Summary

| Chapter | Topic | MCQs |
|---------|-------|------|
| 26 | String Algorithms | 35 |
| 27 | Advanced Graph Algorithms | 25 |
| 28 | Computational Geometry | 20 |
| 29 | Randomized Algorithms | 20 |
| 30 | Bit Manipulation | 35 |
| 31 | Number Theory & Math | 30 |
| 32 | Advanced Data Structures | 24 |
| **Part V Total** | | **189** |

**Next:** Part VI - DSA in Real-World Applications (Chapter 33)
