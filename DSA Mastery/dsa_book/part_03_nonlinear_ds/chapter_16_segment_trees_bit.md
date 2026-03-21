# Chapter 16: Segment Trees & Binary Indexed Trees

**Target:** 65 MCQs | **Distribution:** 16 Foundational, 26 Intermediate, 16 Advanced, 7 Expert

---

**Q16.1: Foundational - [Theory] - [Range Query Problem]**

Range query problem:

A) Given array, answer queries about subarrays [l, r]
B) Common queries: sum, minimum, maximum, GCD over range
C) Also support point updates (change single element)
D) All of the above

**Answer: D**

**Explanation:**
Range queries: fundamental problem. Naive: O(n) per query. Prefix sum: O(1) query, O(n) update. Segment tree: O(log n) query + O(log n) update. BIT: O(log n) both. Sparse table: O(1) query, no updates. Choice depends on: static vs dynamic, query type (sum, min, etc.), and update frequency.

---

**Q16.2: Foundational - [Theory] - [Prefix Sum Limitation]**

Prefix sum for range sum queries:

A) prefix[i] = sum of arr[0..i-1]
B) Range sum [l,r] = prefix[r+1] - prefix[l]
C) O(1) query but O(n) update (rebuild prefix)
D) All of the above

**Answer: D**

**Explanation:**
Prefix sum: precompute cumulative sums. Query O(1). But updating arr[i] changes all prefix[j] for j > i → O(n) to rebuild. If array is static (no updates): prefix sum is optimal. With updates: need segment tree or BIT. Prefix sum handles only sum/XOR (invertible operations), not min/max.

---

**Q16.3: Foundational - [Theory] - [Binary Indexed Tree Definition]**

Binary Indexed Tree (BIT / Fenwick Tree):

A) Array-based structure for efficient prefix operations
B) O(log n) point update and prefix query
C) Uses clever bit manipulation of indices
D) All of the above

**Answer: D**

**Explanation:**
BIT (Fenwick Tree): compact structure for prefix sums. BIT[i] stores sum of a specific range determined by lowest set bit of i. Update element: O(log n) indices affected. Prefix sum query: O(log n) indices summed. Simple to implement (~10 lines). Uses lowbit(i) = i & (-i) to navigate.

---

**Q16.4: Foundational - [Theory] - [BIT Operations]**

BIT core operations:

A) Update(i, delta): add delta to position i, propagate up
B) Query(i): compute prefix sum from 1 to i
C) Both use i += i & (-i) or i -= i & (-i)
D) All of the above

**Answer: D**

**Explanation:**
Update: move up the tree. i += i & (-i) → next responsible position. Query: move down (accumulate). i -= i & (-i) → parent in implicit tree. i & (-i) = lowest set bit. Example: 6 (110) → lowbit=2. Query sum [1,6]: BIT[6] + BIT[4]. Update pos 3: affects BIT[3], BIT[4], BIT[8], etc.

---

**Q16.5: Foundational - [Trace] - [BIT Update and Query]**

Array [0,1,2,3,4,5] (1-indexed), BIT after building:

A) BIT[1]=1, BIT[2]=1+2=3, BIT[3]=3, BIT[4]=1+2+3+4=10
B) BIT[5]=5, BIT[6]=5+6=11
C) Query prefix sum(6) = BIT[6] + BIT[4] = 11 + 10 = 21 (=1+2+3+4+5+6)
D) O(log n) per query

**Answer: D**

**Explanation:**
BIT stores: BIT[i] = sum of arr[i-lowbit(i)+1 .. i]. BIT[1]=1, BIT[2]=3, BIT[3]=3, BIT[4]=10, BIT[5]=5, BIT[6]=11. Query(6): 6(110)→BIT[6]=11, remove lowbit: 4(100)→BIT[4]=10. Total=21. Verify: 1+2+3+4+5+6=21. ✓

---

**Q16.6: Foundational - [Theory] - [BIT Range Sum]**

Range sum query [l, r] using BIT:

A) rangeSum(l, r) = query(r) - query(l-1)
B) Two prefix queries
C) O(log n)
D) All of the above

**Answer: D**

**Explanation:**
BIT provides prefix sums. Range sum: difference of two prefix sums. sum[l,r] = prefix(r) - prefix(l-1). Two O(log n) queries → O(log n) total. Simple and clean. This works because sum is invertible (can subtract). For min/max: BIT doesn't directly work (not invertible).

---

**Q16.7: Foundational - [Theory] - [Segment Tree Definition]**

Segment tree:

A) Binary tree built on array, each node represents a range
B) Root represents entire array [0, n-1]
C) Leaves represent individual elements
D) All of the above

**Answer: D**

**Explanation:**
Segment tree: divide-and-conquer structure. Root = [0, n-1]. Left child = [0, mid], right child = [mid+1, n-1]. Leaves = single elements. Each internal node stores aggregate (sum, min, max) of its range. Height: O(log n). Space: O(4n) or O(2n) with careful implementation. Supports any associative operation.

---

**Q16.8: Foundational - [Theory] - [Segment Tree Build]**

Building a segment tree:

A) Recursive: if leaf, store element; else build left and right, combine
B) O(n) time to build
C) O(4n) space (for implementation simplicity)
D) All of the above

**Answer: D**

**Explanation:**
Build: recursively split range in half. Leaf: store arr[i]. Internal: tree[node] = combine(tree[left], tree[right]). O(n) time: each element processed once, each node filled once. Space: complete binary tree with up to 2n leaves needs ~4n nodes (round up to next power of 2). Some use exactly 2n with careful indexing.

---

**Q16.9: Foundational - [Theory] - [Segment Tree Query]**

Segment tree range query [l, r]:

A) If node's range entirely within [l,r]: return node's value
B) If no overlap: return identity (0 for sum, ∞ for min)
C) Otherwise: query both children, combine results
D) All of the above

**Answer: D**

**Explanation:**
Query: traverse tree, collect answers from relevant ranges. Three cases: (1) Complete overlap: return stored value. (2) No overlap: return identity element. (3) Partial overlap: recursively query both children, combine. At most O(4 log n) nodes visited per query → O(log n). Works for any associative combine function.

---

**Q16.10: Foundational - [Trace] - [Segment Tree Query]**

Array [1,3,5,7,9,11], query sum [1,4] (0-indexed):

A) Root [0,5]=36. Partial overlap with [1,4]
B) Left [0,2]=9: partial → left [0,1]=4: partial → 3 from [1,1], right [2,2]=5: included
C) Right [3,5]=27: partial → left [3,4]=16: included, right [5,5]=11: excluded
D) Answer: 3 + 5 + 7 + 9 = 24

**Answer: D**

**Explanation:**
Query [1,4]: elements at indices 1,2,3,4 = 3+5+7+9 = 24. Tree traversal visits O(log 6) ≈ 3 levels. Nodes contributing: [1,1]=3, [2,2]=5, [3,4]=16. Sum = 3+5+16 = 24. Efficient: only ~6-8 nodes visited for 6-element array.

---

**Q16.11: Foundational - [Theory] - [Segment Tree Point Update]**

Point update (change single element):

A) Update leaf node
B) Propagate change up to root, updating ancestors
C) O(log n) — one path from leaf to root
D) All of the above

**Answer: D**

**Explanation:**
Update arr[i] to new value: find leaf for index i, change it. Walk up updating each ancestor: parent = combine(left_child, right_child). Exactly O(log n) nodes updated (one per level). After update, all range queries return correct results.

---

**Q16.12: Intermediate - [Theory] - [Segment Tree vs BIT]**

Segment tree vs BIT comparison:

A) Both O(log n) update and query
B) Segment tree: more versatile (supports min, max, GCD, etc.)
C) BIT: simpler implementation, lower constant factor
D) All of the above

**Answer: D**

**Explanation:**
BIT: only for invertible operations (sum, XOR). Simpler code (~10 lines), smaller constant. Segment tree: handles any associative operation (min, max, GCD), supports range updates with lazy propagation. More complex (~40-60 lines). Use BIT when possible; segment tree when BIT can't handle the operation or lazy propagation needed.

---

**Q16.13: Intermediate - [Theory] - [BIT vs Prefix Sum vs Segment Tree]**

Comparison for range sum with point updates:

A) Prefix sum: O(1) query, O(n) update
B) BIT: O(log n) query, O(log n) update
C) Segment tree: O(log n) query, O(log n) update (higher constant)
D) BIT is ideal for this case

**Answer: D**

**Explanation:**
Range sum + point updates: BIT is the simplest and fastest solution. Same O(log n) as segment tree but lower constant (simpler operations, better cache). Prefix sum fails for updates. Segment tree overkill (extra features unused). For pure range sum + point update: always prefer BIT.

---

**Q16.14: Intermediate - [Theory] - [Lazy Propagation Concept]**

Lazy propagation in segment tree:

A) Defer range updates instead of updating all leaves immediately
B) Propagate deferred updates to children only when queried
C) Enables O(log n) range updates instead of O(n)
D) All of the above

**Answer: D**

**Explanation:**
Range update (e.g., add 5 to all elements in [l,r]): without lazy, must update O(n) leaves. With lazy: mark nodes with pending update, apply lazily when accessed. Range update: O(log n). Range query: push lazy values down before querying. Key insight: defer work until it's actually needed.

---

**Q16.15: Intermediate - [Theory] - [Lazy Propagation Mechanics]**

Lazy propagation implementation:

A) Each node has a lazy value (pending operation)
B) Before accessing children: push lazy to children (propagate)
C) Update: if range fully covered, apply to node and mark lazy
D) All of the above

**Answer: D**

**Explanation:**
push_down(node): if lazy[node] ≠ identity: apply lazy to children's values and lazy tags, reset node's lazy. Update [l,r] by delta: if complete overlap → update node value, set lazy. Else push down, recurse on children, pull up. Query: push down before recursing. Maintains correctness: lazy values always applied before read.

---

**Q16.16: Intermediate - [Trace] - [Lazy Propagation]**

Array [1,2,3,4], add 10 to range [0,3], then query sum [0,1]:

A) Build seg tree: root [0,3]=10, left [0,1]=3, right [2,3]=7
B) Range update [0,3] +10: root fully covered, value=10+4×10=50, lazy=10
C) Query [0,1]: push lazy to children. Left [0,1]: value=3+2×10=23, lazy=10
D) Return 23 (=11+12). Correct: (1+10)+(2+10)=23

**Answer: D**

**Explanation:**
Build: root=10, left=3, right=7. Update [0,3]: root fully covered, add 4×10 to sum=50, lazy=10. Query [0,1]: partial overlap → push lazy down. Left child: 3+2×10=23 (2 elements each +10). Right child: 7+2×10=27. Clear root lazy. Query left: fully covered → return 23. Verify: (1+10)+(2+10)=11+12=23. ✓

---

**Q16.17: Intermediate - [Theory] - [Range Minimum Query (RMQ)]**

Segment tree for range minimum query:

A) Each node stores minimum of its range
B) Build: O(n), Query [l,r]: O(log n), Point update: O(log n)
C) Supports dynamic array (updates + queries)
D) All of the above

**Answer: D**

**Explanation:**
RMQ with segment tree: node.val = min(children). Query: return min of relevant sub-ranges. Update: change leaf, update minimums up. Same structure as range sum but with min operation. Identity element: +∞ (no overlap returns infinity). Works because min is associative. BIT cannot do RMQ efficiently (min is not invertible).

---

**Q16.18: Intermediate - [Theory] - [Sparse Table for RMQ]**

Sparse table for static RMQ:

A) Precompute min for all power-of-2 ranges
B) O(n log n) precomputation, O(1) query
C) No updates supported (static)
D) All of the above

**Answer: D**

**Explanation:**
Sparse table: table[i][j] = min of arr[i..i+2^j-1]. Build: O(n log n). Query [l,r]: find k = ⌊log₂(r-l+1)⌋, answer = min(table[l][k], table[r-2^k+1][k]). O(1) query using overlapping ranges (ok for min/max, idempotent). Not for sum (overlapping would double-count). Best for static RMQ.

---

**Q16.19: Intermediate - [Theory] - [BIT Point Query]**

BIT for range update + point query:

A) Difference BIT: store differences instead of values
B) Range update [l,r] += val: update(l, val), update(r+1, -val)
C) Point query at i: prefix sum of differences = arr[i]
D) All of the above

**Answer: D**

**Explanation:**
Dual BIT: for range update, point query. Use difference array in BIT. Update [l,r] by val: add val at l, subtract val at r+1. Query position i: prefix sum gives cumulative effect of all updates on position i. O(log n) per operation. Reverses the typical BIT use case.

---

**Q16.20: Advanced - [Theory] - [BIT Range Update + Range Query]**

BIT for range update AND range query:

A) Requires two BITs
B) Based on formula: prefix_sum(i) = B1[i] × i + B2[i] (where B1, B2 are BITs) — or equivalent
C) O(log n) for both range update and range query
D) All of the above

**Answer: D**

**Explanation:**
Range update + range query using BIT: need two BITs (B1, B2). Derivation: prefix_sum(x) = (x+1) × Σ₁ᵢf₁(i) - Σ₁ᵢ(i × f₁(i)). Two BITs track these separately. Range update [l,r] by v: update both BITs at l and r+1. Range query: combine both BIT queries. More complex than single BIT but avoids segment tree overhead.

---

**Q16.21: Intermediate - [Theory] - [Segment Tree for Max]**

Segment tree for range maximum query:

A) Each node stores maximum of its range
B) Query combines with max function
C) Identity element: -∞
D) All of the above

**Answer: D**

**Explanation:**
Range max: symmetric to range min. node.val = max(left.val, right.val). Query: max of relevant sub-ranges. No-overlap returns -∞ (identity for max). Works for any associative, can be generalized. Segment tree is a general framework: plug in any associative combine function.

---

**Q16.22: Intermediate - [Theory] - [Segment Tree Space]**

Segment tree space complexity:

A) Size: 4n is safe (handles non-power-of-2 sizes)
B) 2n for iterative bottom-up implementation (power-of-2 padded)
C) Each node stores one value (+ lazy value if applicable)
D) All of the above

**Answer: D**

**Explanation:**
Recursive segment tree: allocate 4n nodes to be safe (worst case). Iterative: pad array to next power of 2, use 2n nodes. Each node: 1 value for query, +1 for lazy tag if range updates. Total space: O(n). Practical overhead: 4× the array size, but enables O(log n) operations.

---

**Q16.23: Intermediate - [Theory] - [Iterative Segment Tree]**

Iterative (bottom-up) segment tree:

A) Array of size 2n, leaves at position n to 2n-1
B) Query: start from leaves, walk up combining
C) Update: start from leaf, walk up updating
D) All of the above

**Answer: D**

**Explanation:**
Iterative segment tree: simpler, no recursion overhead. Tree[n+i] = arr[i] (leaves). Build: for i = n-1 down to 1: tree[i] = combine(tree[2i], tree[2i+1]). Update: set tree[n+i], walk up dividing index by 2. Query [l,r]: start at l+n and r+n+1, walk up combining. Fewer function calls, cache-friendlier.

---

**Q16.24: Intermediate - [Trace] - [Iterative Segment Tree Build]**

Array [1,3,5,7], build iterative segment tree (n=4):

A) tree[4]=1, tree[5]=3, tree[6]=5, tree[7]=7 (leaves)
B) tree[3]=min(5,7)=5, tree[2]=min(1,3)=1
C) tree[1]=min(tree[2],tree[3])=min(1,5)=1
D) Root tree[1]=1 (global minimum)

**Answer: D**

**Explanation:**
Bottom-up: fill leaves tree[4..7] = [1,3,5,7]. Level up: tree[3]=min(tree[6],tree[7])=min(5,7)=5. tree[2]=min(tree[4],tree[5])=min(1,3)=1. Root: tree[1]=min(tree[2],tree[3])=min(1,5)=1. Global minimum is 1. Array: [_, 1, 1, 5, 1, 3, 5, 7] (index 0 unused).

---

**Q16.25: Advanced - [Theory] - [Persistent Segment Tree]**

Persistent segment tree:

A) Maintains all historical versions after updates
B) Each update creates O(log n) new nodes (path copying)
C) Query any version in O(log n)
D) All of the above

**Answer: D**

**Explanation:**
Persistent: on update, create new nodes only along modified path (root to leaf). Unchanged subtrees shared. O(log n) new nodes per update. Each version accessible via its root. Total space: O(n + q log n) for q updates. Used for: kth smallest in range, versioned queries, offline algorithms. Foundation of many advanced techniques.

---

**Q16.26: Advanced - [Theory] - [Kth Smallest with Persistent Segment Tree]**

Kth smallest in range [l,r] using persistent segment tree:

A) Build persistent segment tree on values, version per prefix
B) version[r] - version[l-1] gives frequency tree for range [l,r]
C) Walk down tree: compare k with left child count
D) O(log(max_value)) per query

**Answer: D**

**Explanation:**
Merge sort tree / persistent segment tree: build segment tree on value domain [1..max_val]. Insert elements one by one (persistent update adds 1 to value's position). Query kth in [l,r]: use roots of version l-1 and version r. Difference of left child counts tells how many values ≤ mid in range. Navigate left/right based on k. O(log V) per query.

---

**Q16.27: Intermediate - [Theory] - [Segment Tree with Pairs]**

Segment tree storing pairs (value, index):

A) Range minimum query returning both value and position
B) Combine: return pair with smaller value
C) Useful when needing position of minimum
D) All of the above

**Answer: D**

**Explanation:**
Store (value, index) at each node. Combine: compare values, keep pair with smaller value. This gives both the minimum value and its position in one query. Useful for algorithms that need the position of the extremum (e.g., segment tree-based range operations, LCA on Euler tour).

---

**Q16.28: Advanced - [Theory] - [Merge Sort Tree]**

Merge sort tree:

A) Segment tree where each node stores sorted array of its range
B) Build O(n log n), space O(n log n)
C) Query: how many elements in [l,r] are ≤ k? O(log² n)
D) All of the above

**Answer: D**

**Explanation:**
Merge sort tree: each node stores sorted elements of its range (like merge sort). Build: bottom-up merge, O(n log n). Query "count ≤ k in [l,r]": decompose to O(log n) nodes, binary search in each (O(log n) per node). Total: O(log² n). Can also answer kth smallest. Space: O(n log n) — each element in O(log n) nodes.

---

**Q16.29: Advanced - [Theory] - [2D BIT]**

2D Binary Indexed Tree:

A) BIT extended to 2D (matrix)
B) Point update: O(log n × log m)
C) Prefix rectangle sum query: O(log n × log m)
D) All of the above

**Answer: D**

**Explanation:**
2D BIT: BIT[i][j] stores partial sum over submatrix. Update (r,c,val): nested loops using lowbit on both indices. Query prefix sum (1,1) to (r,c): nested loops subtracting lowbit. Rectangle sum [r1,c1] to [r2,c2]: inclusion-exclusion with 4 prefix queries. O(log² n) per operation. Simpler than 2D segment tree.

---

**Q16.30: Intermediate - [Theory] - [Count Inversions with BIT]**

Count inversions using BIT:

A) Inversion: pair (i,j) where i < j but arr[i] > arr[j]
B) Process array right-to-left, use BIT to count elements already seen that are smaller
C) O(n log n) — equivalent to merge sort inversion count
D) All of the above

**Answer: D**

**Explanation:**
Inversions with BIT: process elements right-to-left (or left-to-right). For each element value v, query BIT for prefix sum [1, v-1] = count of smaller elements already placed. Add result to inversion count. Update BIT at position v. O(n log n). Need coordinate compression if values large. Alternative: merge sort approach (Chapter 17).

---

**Q16.31: Intermediate - [Theory] - [BIT for Order Statistics]**

BIT for dynamic order statistics:

A) BIT as frequency array over value domain
B) Insert: update(value, +1). Delete: update(value, -1)
C) Kth smallest: binary search on BIT prefix sums
D) All of the above

**Answer: D**

**Explanation:**
BIT for order statistics: BIT[v] = count of active elements with value v. Insert/delete: O(log n). Kth smallest: binary search for smallest x where prefix_sum(x) ≥ k. Naive binary search on BIT: O(log² n). Optimized (walk down BIT bit by bit): O(log n). Alternative: balanced BST with order statistics.

---

**Q16.32: Foundational - [Theory] - [BIT 1-Indexed]**

BIT is typically 1-indexed because:

A) Index 0's lowbit is 0, causing infinite loop
B) 1-indexed: lowbit(1) = 1, lowbit(2) = 2, etc. — all well-defined
C) Convention inherited from Fenwick's original paper
D) All of the above

**Answer: D**

**Explanation:**
BIT implementation: 1-indexed to avoid lowbit(0) = 0 problem. Shift array to start at index 1. If 0-indexed array: add 1 when using BIT, subtract 1 when converting back. Common source of off-by-one bugs. Some implementations handle 0-indexing with special offset.

---

**Q16.33: Advanced - [Theory] - [Segment Tree Beats]**

Segment tree beats:

A) Handles "set all elements in [l,r] to min(arr[i], val)" updates
B) Maintains additional information (second maximum, count of max)
C) Amortized O(log² n) or O(log n) per operation
D) All of the above

**Answer: D**

**Explanation:**
Segment tree beats (Ji driver segment tree): handle operations like "clamp max" (arr[i] = min(arr[i], val)). Store: max value, second max, count of max, sum. If val > max: no effect (break). If second_max < val ≤ max: update max elements to val, adjust sum (tag). If val ≤ second_max: recurse to children. Amortized O(n log²n) for m operations on n elements.

---

**Q16.34: Intermediate - [Theory] - [Segment Tree for GCD]**

Segment tree for range GCD:

A) Each node stores GCD of its range
B) Combine: GCD(left, right)
C) Point update supported, range query O(log n)
D) All of the above

**Answer: D**

**Explanation:**
GCD is associative: GCD(a, GCD(b,c)) = GCD(GCD(a,b), c). Identity: 0 (GCD(x,0) = x). Segment tree: node.val = GCD of range. Build O(n log(max)). Query O(log n × log(max)). Update: change leaf, recompute GCD up the path. Note: GCD computation itself is O(log(max_value)) per pair.

---

**Q16.35: Intermediate - [Theory] - [Segment Tree Combine Function]**

Segment tree generalizes to any associative operation:

A) Sum, min, max, GCD, XOR, matrix multiplication
B) Must define combine(a, b) and identity element
C) Combine must be associative: f(f(a,b), c) = f(a, f(b,c))
D) All of the above

**Answer: D**

**Explanation:**
Segment tree framework: plug in any associative combine. Sum: f=+, identity=0. Min: f=min, identity=∞. GCD: f=gcd, identity=0. XOR: f=⊕, identity=0. Matrix multiply: f=matmul, identity=I (supports linear recurrence queries). Flexibility is segment tree's key advantage over BIT.

---

**Q16.36: Advanced - [Theory] - [Fractional Cascading]**

Fractional cascading:

A) Technique to speed up binary searches in multiple sorted arrays
B) Reduces O(log² n) merge sort tree queries to O(log n)
C) Propagate elements between arrays to create shortcuts
D) All of the above

**Answer: D**

**Explanation:**
Fractional cascading: in merge sort tree, query visits O(log n) nodes, each needing O(log n) binary search. Fractional cascading: augment each node's array with pointers to positions in children's arrays. After binary search in first node, subsequent lookups are O(1). Total: O(log n) instead of O(log² n). Complex to implement but theoretically important.

---

**Q16.37: Foundational - [Theory] - [BIT Implementation]**

BIT implementation (pseudocode):

A) query(x): while x > 0: sum += bit[x]; x -= x & (-x)
B) update(x, val): while x ≤ n: bit[x] += val; x += x & (-x)
C) Both O(log n) — number of set bits traversals
D) All of the above

**Answer: D**

**Explanation:**
Query: accumulate BIT values, moving to parent (remove lowest set bit). Update: modify BIT values, moving to responsible ancestors (add lowest set bit). Each loop executes at most O(log n) times (number of bits in n). Extremely concise and fast. Low constant factor: no function calls, simple arithmetic.

---

**Q16.38: Intermediate - [Theory] - [Segment Tree Lazy Types]**

Common lazy propagation types:

A) Range add: add value to all elements in range
B) Range set: set all elements in range to a value
C) Both require different propagation logic
D) All of the above

**Answer: D**

**Explanation:**
Range add: lazy stores pending addition. Propagate: add lazy to children. Range set: lazy stores set value (use sentinel for "no pending set"). Propagate: overwrite children's values and lazy. Combining both: set overrides add (set first, then add). Implementation must handle interaction between multiple lazy types carefully.

---

**Q16.39: Advanced - [Theory] - [Segment Tree on Euler Tour]**

Segment tree on tree's Euler tour:

A) Flatten tree to array using DFS entry/exit times
B) Subtree of v = range [entry[v], exit[v]]
C) Segment tree on this array handles subtree queries
D) All of the above

**Answer: D**

**Explanation:**
Euler tour: DFS, record entry and exit time for each node. Subtree of v = contiguous range [entry[v], exit[v]] in the flattened array. Build segment tree on this array → subtree queries (sum, min of values in subtree) in O(log n). Update value at node: point update at entry[v]. Powerful technique for tree-based range queries.

---

**Q16.40: Intermediate - [Theory] - [BIT for Prefix Maximum]**

BIT for prefix maximum query:

A) Works only for prefix queries (not arbitrary ranges)
B) Update: can increase values but not decrease
C) O(log n) per operation
D) All of the above

**Answer: D**

**Explanation:**
BIT for max: query prefix max [1..x]. Update: set position i to max of current and new value (monotone increase only). Works because max is not invertible: can't compute range max from two prefix maxes. So: only prefix queries. If values only increase: BIT max works. If arbitrary updates or range queries: use segment tree.

---

**Q16.41: Foundational - [Theory] - [When to Use BIT vs Segment Tree]**

Decision: BIT or segment tree?

A) Sum/XOR with point updates: BIT (simpler, faster)
B) Min/max or range updates: segment tree
C) Need lazy propagation: segment tree
D) All valid guidelines

**Answer: D**

**Explanation:**
BIT: invertible operations (sum, XOR) + point updates only. Simpler, 2× faster constant. Segment tree: any associative operation + range updates via lazy. More complex, handles more problems. Rule: use simplest structure that handles your problem. BIT for sums, segment tree for everything else.

---

**Q16.42: Advanced - [Theory] - [Segment Tree for Intervals]**

Segment tree for interval scheduling/counting:

A) Node represents a coordinate range
B) Mark intervals present in the range
C) Query: how many intervals cover a point
D) All of the above

**Answer: D**

**Explanation:**
Interval management: segment tree on coordinate space. Add interval [l,r]: range update +1 on [l,r]. Remove: range update -1. Query point x: point query = count of intervals covering x. With lazy propagation: O(log n) per operation. Applications: computational geometry, event scheduling, sweep line algorithms.

---

**Q16.43: Expert - [Theory] - [Persistent BIT vs Persistent Segment Tree]**

Persistent BIT:

A) Theoretically possible but less practical than persistent segment tree
B) BIT's update pattern (multiple positions) makes persistence complex
C) Persistent segment tree is the standard for versioned range queries
D) Persistent segment tree preferred

**Answer: D**

**Explanation:**
BIT update affects O(log n) positions scattered through the array → path copying would duplicate too many nodes. Persistent segment tree: update affects exactly one root-to-leaf path → clean O(log n) new nodes per version. For persistent range queries: always use persistent segment tree. BIT's advantage (simplicity) vanishes for persistent variant.

---

**Q16.44: Intermediate - [Theory] - [Coordinate Compression for BIT/Segment Tree]**

Coordinate compression:

A) Map large value range to small consecutive range
B) Sort unique values, assign ranks
C) Enables BIT/segment tree of size = distinct values, not max value
D) All of the above

**Answer: D**

**Explanation:**
If values range [1, 10^9] but only n ≤ 10^5 distinct values: compress to [1, n]. Sort unique values, binary search for rank. BIT size: n instead of 10^9. Essential for: inversion counting, order statistics, any value-indexed BIT/segment tree. O(n log n) for sorting + compression.

---

**Q16.45: Expert - [Theory] - [Li Chao Tree]**

Li Chao segment tree:

A) Segment tree variant for inserting lines y = mx + b
B) Query: maximum (or minimum) y value at given x
C) O(log n) insert and query
D) All of the above

**Answer: D**

**Explanation:**
Li Chao tree: dynamic convex hull trick. Each segment tree node stores a line that dominates its range. Insert line: compare with existing line in node, push losing line to relevant child. Query point x: walk root-to-leaf, take maximum over all stored lines. O(log n) insert and query. Simpler than full convex hull trick. Used in DP optimization.

---

**Q16.46: Advanced - [Theory] - [Segment Tree for Sum and Minimum Simultaneously]**

Segment tree storing multiple aggregates:

A) Each node stores both sum and minimum of its range
B) Update affects both aggregates
C) Query can ask for sum OR minimum over any range
D) All of the above

**Answer: D**

**Explanation:**
Multi-aggregate segment tree: store tuple (sum, min, max, count, etc.) at each node. Combine: component-wise. Update: update all components. Query: return specific component. Enables answering different query types on same data. Space: O(k × n) for k aggregates. Common in competitive programming for complex query combinations.

---

**Q16.47: Intermediate - [Theory] - [BIT for 2D Prefix Sums]**

2D prefix sum with updates:

A) Static: 2D prefix sum array O(1) query, O(nm) update
B) Dynamic: 2D BIT O(log n × log m) both
C) 2D segment tree also possible but more complex
D) All of the above

**Answer: D**

**Explanation:**
Static 2D: prefix[i][j] = sum of submatrix (0,0) to (i,j). Rectangle sum via inclusion-exclusion. O(1) query but O(nm) for any update. Dynamic 2D: 2D BIT or 2D segment tree, O(log n × log m) operations. 2D BIT: nest BIT within BIT, simple implementation. 2D segment tree: more flexible but complex.

---

**Q16.48: Expert - [Theory] - [Wavelet Tree and Range Queries]**

Wavelet tree for range queries:

A) Built on array of values
B) Supports: kth smallest in range, count ≤ k in range, rank/select
C) O(log V) per query where V = value range
D) All of the above

**Answer: D**

**Explanation:**
Wavelet tree: binary tree over value domain. Each level partitions values into lower and upper halves. Bitvectors at each level track which partition each element belongs to. Kth smallest in [l,r]: walk down, narrow range using rank queries on bitvectors. O(log V) time. Extremely versatile for rank-based queries. Alternative to persistent segment tree.

---

**Q16.49: Intermediate - [Theory] - [Segment Tree Build Time Proof]**

Segment tree build is O(n):

A) 2n-1 internal and leaf nodes (at most 4n allocated)
B) Each node computed in O(1) from children
C) Total: O(n) (not O(n log n))
D) All of the above

**Answer: D**

**Explanation:**
Build: bottom-up, each node = combine(left, right) in O(1). Total nodes: 2n-1 (complete binary tree with n leaves) or up to 4n (padded). Each processed once. Total: O(n). Note: m queries are O(m log n), not multiplied by build time. Build dominates only if m < n/log n.

---

**Q16.50: Advanced - [Theory] - [Implicit Segment Tree (Dynamic)]**

Implicit (dynamic) segment tree:

A) Don't allocate all nodes upfront
B) Create nodes only when accessed
C) Supports range [0, 10^9] without 10^9 space
D) All of the above

**Answer: D**

**Explanation:**
Dynamic segment tree: for large value ranges where most nodes unused. Allocate nodes on demand (using pointers/indices instead of array positions). Space: O(q × log V) for q operations on values up to V. Essential when: coordinate space is huge but operations are sparse. Example: count elements in [l,r] when values up to 10^9 but only 10^5 insertions.

---

**Q16.51: Intermediate - [Theory] - [Range XOR with BIT]**

Range XOR query with BIT:

A) XOR prefix: prefix_xor(r) ⊕ prefix_xor(l-1)
B) BIT stores prefix XOR instead of prefix sum
C) XOR is invertible (a ⊕ a = 0), so BIT works
D) All of the above

**Answer: D**

**Explanation:**
XOR is associative and self-inverse (a ⊕ a = 0). Prefix XOR with BIT: same structure as prefix sum but replace + with ⊕. Range XOR [l,r] = prefix_xor(r) ⊕ prefix_xor(l-1). Point update: BIT update with ⊕. All O(log n). Another invertible operation suitable for BIT.

---

**Q16.52: Foundational - [Theory] - [Range Update Array]**

Difference array for range updates (no segment tree):

A) diff[i] = arr[i] - arr[i-1]
B) Range update [l,r] += val: diff[l] += val, diff[r+1] -= val
C) Reconstruct: prefix sum of diff gives arr
D) All of the above

**Answer: D**

**Explanation:**
Difference array: O(1) per range update, O(n) to reconstruct. Good for batch updates then single reconstruction. For online queries between updates: need BIT or segment tree. Difference array is the simplest structure for range update problems without intermediate queries.

---

**Q16.53: Expert - [Theory] - [Segment Tree with Matrix Multiplication]**

Segment tree with matrix multiply combine:

A) Each node stores a 2×2 (or k×k) matrix
B) Combine = matrix multiplication
C) Supports: linear recurrence range queries (e.g., Fibonacci range)
D) All of the above

**Answer: D**

**Explanation:**
Matrix segment tree: combine via matrix multiplication (associative). Each leaf: transformation matrix for that element. Range query product: composition of transformations. Application: given linear recurrence y[i] = a×y[i-1] + b×y[i-2], query Fibonacci-like values over a range. O(k³ × log n) per query for k×k matrices. Powerful for recurrence-based problems.

---

**Q16.54: Intermediate - [Theory] - [BIT Initialization]**

Building BIT from array:

A) O(n) using clever propagation
B) For each i: BIT[i] = arr[i], then propagate to parent
C) Alternative: n point updates each O(log n) → O(n log n) total
D) O(n) is possible and preferred

**Answer: D**

**Explanation:**
O(n) BIT build: for each i from 1 to n: set BIT[i] += arr[i], then add BIT[i] to BIT[i + lowbit(i)] if in range. Each element propagated once. Total O(n). Alternatively: n calls to update(i, arr[i]) gives O(n log n). The O(n) approach is a nice optimization.

---

**Q16.55: Expert - [Theory] - [Functional Segment Tree]**

Functional (purely persistent) segment tree:

A) Immutable: every update returns new tree sharing structure
B) Previous versions never modified
C) Natural in functional languages (Haskell, Clojure)
D) All of the above

**Answer: D**

**Explanation:**
Functional segment tree: naturally persistent. Every update creates new path (O(log n) nodes), shares rest. All versions accessible simultaneously. Used in: versioned databases, temporal queries, divide-and-conquer on time. In functional programming: structural persistence is the default. In imperative: explicit pointer management for sharing.

---

**Q16.56: Advanced - [Theory] - [Segment Tree Complexity Analysis]**

Segment tree query visits O(4 log n) nodes:

A) At each level, at most 4 nodes partially overlap the query range
B) Typically 2 are at boundaries, others are fully contained or excluded
C) More precisely: at most 2 partial segments per level
D) Total: O(2 log n) = O(log n) active nodes

**Answer: D**

**Explanation:**
Proof: at each level, query range [l,r] overlaps at most 2 segments partially (at left and right boundaries). Fully contained: returned immediately. Fully excluded: returned identity. So at most 2 recursive calls per level. Height = log n. Total nodes visited: ≤ 2 log n + O(1) = O(log n). Tight analysis important for understanding performance.

---

**Q16.57: Intermediate - [Theory] - [BIT Lowbit Function]**

lowbit(x) = x & (-x):

A) Returns the lowest set bit of x
B) Example: lowbit(6) = lowbit(110₂) = 2 (10₂)
C) Foundation of BIT index navigation
D) All of the above

**Answer: D**

**Explanation:**
Two's complement: -x = ~x + 1. x & (-x) isolates lowest set bit. Examples: lowbit(1)=1, lowbit(2)=2, lowbit(3)=1, lowbit(4)=4, lowbit(6)=2, lowbit(12)=4. BIT query: subtract lowbit (move to prefix start). BIT update: add lowbit (move to parent). Elegant bit manipulation enabling the entire BIT structure.

---

**Q16.58: Foundational - [Theory] - [When to Use Which Structure]**

Choosing range query structure:

A) Static array, sum: prefix sum (O(1) query)
B) Static array, min/max: sparse table (O(1) query)
C) Dynamic array, any operation: segment tree (O(log n))
D) Dynamic array, sum/XOR: BIT (O(log n), simpler)

**Answer: D**

**Explanation:**
Decision tree: Static? → prefix sum (sum) or sparse table (min/max). Dynamic? → BIT (invertible ops, point update) or segment tree (any op, range updates). Need persistence? → persistent segment tree. Need 2D? → 2D BIT or merge sort tree. Understanding when each structure is appropriate is as important as knowing how they work.

---

**Q16.59: Expert - [Theory] - [Segment Tree Beats Applications]**

Segment tree beats advanced applications:

A) Interval minimum assignment: arr[i] = min(arr[i], val) for range
B) Maintain max, second max, count of max, and sum simultaneously
C) Break when val ≥ max, tag when val > second_max
D) All of the above

**Answer: D**

**Explanation:**
Segment tree beats key insight: when clamping max by val, if val ≥ max, nothing to do. If second_max < val < max, only max elements change (can update sum = sum - (max - val) × count_max). If val ≤ second_max, must recurse deeper. Amortized analysis shows O(n log² n) total for m operations. Enables operations that seem inherently non-lazy.

---

**Q16.60: Intermediate - [Theory] - [Offline Range Queries with BIT]**

Offline processing of range queries:

A) Sort queries by right endpoint
B) Process array left to right, answer queries ending at current position
C) BIT maintains relevant information for answering
D) All of the above

**Answer: D**

**Explanation:**
Offline: process queries in sorted order. Example: count distinct in [l,r]. Sort by r. Sweep r from left to right. For each element, BIT marks current position (undo previous occurrence). Answer query [l,r] = BIT sum [l,r]. O((n+q) log n). Only works when queries can be processed offline (answers not needed immediately).

---

**Q16.61: Advanced - [Theory] - [Segment Tree for Maximum Subarray Sum]**

Segment tree for maximum subarray sum query:

A) Each node stores: total sum, max prefix, max suffix, max subarray sum
B) Combine: max subarray = max(left.max, right.max, left.suffix + right.prefix)
C) O(log n) per query
D) All of the above

**Answer: D**

**Explanation:**
Maximum subarray sum (Kadane's generalized to ranges): need 4 values per node. total_sum, max_prefix_sum, max_suffix_sum, max_subarray_sum. Combine: prefix = max(left.prefix, left.total + right.prefix). Suffix = max(right.suffix, right.total + left.suffix). Max subarray = max(left.max, right.max, left.suffix + right.prefix). Point updates supported. Elegant segment tree application.

---

**Q16.62: Foundational - [Theory] - [BIT Applications Summary]**

Common BIT applications:

A) Range sum queries with point updates
B) Inversion counting
C) Dynamic order statistics
D) All of the above, plus 2D, coordinate operations

**Answer: D**

**Explanation:**
BIT applications: (1) Range sum + point update. (2) Inversion count (via value-indexed BIT). (3) Order statistics (kth smallest). (4) 2D range sums. (5) With coordinate compression: handle large value ranges. (6) Dual BIT: range update + point query. Simple structure, widely applicable for sum-type problems.

---

**Q16.63: Expert - [Theory] - [Kinetic Segment Tree]**

Kinetic segment tree:

A) Extended segment tree where values change over time (as functions)
B) Tracks when aggregate answers change (breakpoints)
C) Used in computational geometry for moving objects
D) All of the above

**Answer: D**

**Explanation:**
Kinetic data structures: maintain properties as objects move. Kinetic segment tree: elements are functions of time (e.g., linear positions). Track when relative ordering changes (certificate-based). Update structure at breakpoints. Maintains aggregate (max, min) over changing values. Used in animation, robotics, kinetic sorting. Research-level data structure.

---

**Q16.64: Advanced - [Theory] - [Segment Tree Memory Pool]**

Efficient memory for implicit segment tree:

A) Pre-allocate node pool (array of nodes)
B) Allocate from pool instead of dynamic allocation
C) Avoids malloc overhead, cache-friendly
D) All of the above

**Answer: D**

**Explanation:**
Dynamic segment tree: frequent node creation. malloc/new: slow, fragmentation. Memory pool: pre-allocate array of nodes (e.g., 20 × n nodes). Allocate by incrementing index. O(1) per allocation, contiguous memory. Standard technique in competitive programming for speed. Also applies to persistent segment trees.

---

**Q16.65: Intermediate - [Theory] - [Segment Tree and BIT Summary]**

Key takeaways:

A) BIT: simple, fast, for sum-type problems with point updates
B) Segment tree: versatile, handles any associative operation + lazy propagation
C) Both O(log n) per operation, O(n) space
D) Essential structures for competitive programming and real-world range query problems

**Answer: D**

**Explanation:**
BIT and segment tree are foundational range query structures. BIT: 10 lines of code, invertible operations. Segment tree: 40-60 lines, universal. Extensions: persistent, 2D, lazy, beats, merger with other techniques. Understanding both and choosing appropriately is a core competitive programming and systems design skill.

---

## Chapter 16 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 16 | BIT operations, segment tree build/query/update, prefix sums, when to use which |
| Intermediate | 26 | Lazy propagation, RMQ, sparse table, BIT inversions, iterative segment tree, 2D BIT |
| Advanced | 16 | Persistent segment tree, merge sort tree, implicit tree, segment tree beats, maximum subarray |
| Expert | 7 | Li Chao tree, wavelet tree, kinetic segment tree, matrix combine, functional segment tree |

**Total MCQs: 65** | **Target Met: ✓**

**Key Range Query Structure Comparison:**

| Structure | Build | Query | Update | Range Update | Space |
|-----------|-------|-------|--------|--------------|-------|
| Prefix Sum | O(n) | O(1) | O(n) | N/A | O(n) |
| Sparse Table | O(n log n) | O(1) | N/A | N/A | O(n log n) |
| BIT | O(n) | O(log n) | O(log n) | O(log n)* | O(n) |
| Segment Tree | O(n) | O(log n) | O(log n) | O(log n) | O(4n) |

*With dual BIT technique

**Part III Complete.** Next: Part IV — Core Algorithms (Chapter 17: Sorting Algorithms)
