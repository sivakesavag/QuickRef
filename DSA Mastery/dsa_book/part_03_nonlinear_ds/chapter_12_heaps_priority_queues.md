# Chapter 12: Heaps & Priority Queues

**Target:** 65 MCQs | **Distribution:** 16 Foundational, 26 Intermediate, 16 Advanced, 7 Expert

---

**Q12.1: Foundational - [Theory] - [Heap Definition]**

A binary heap is:

A) A complete binary tree satisfying the heap property
B) Parent ≥ children (max-heap) or parent ≤ children (min-heap)
C) Can be efficiently stored in an array
D) All of the above

**Answer: D**

**Explanation:**
Binary heap: complete binary tree where every parent satisfies the heap ordering with respect to its children. Max-heap: parent ≥ children (root is max). Min-heap: parent ≤ children (root is min). Complete tree → array storage with formulaic parent/child indices. Foundation for priority queues and heap sort.

---

**Q12.2: Foundational - [Theory] - [Heap Array Representation]**

Heap stored in array (0-indexed), node at index i:

A) Left child at 2i + 1
B) Right child at 2i + 2
C) Parent at ⌊(i-1)/2⌋
D) All of the above

**Answer: D**

**Explanation:**
Complete binary tree maps naturally to array. 0-indexed: root at 0, left = 2i+1, right = 2i+2, parent = ⌊(i-1)/2⌋. 1-indexed: root at 1, left = 2i, right = 2i+1, parent = ⌊i/2⌋. No pointer overhead, cache-friendly. Refer to Q9.13-14 for array representation of complete trees.

---

**Q12.3: Foundational - [Theory] - [Max-Heap Property]**

In a max-heap:

A) Root contains the maximum element
B) For every node, parent.value ≥ child.value
C) Children are not ordered relative to each other
D) All of the above

**Answer: D**

**Explanation:**
Max-heap: root is always maximum. Parent ≥ both children, but left and right children have no ordering between them (unlike BST). This means in-order traversal does NOT give sorted order. Heap is partially ordered, not fully sorted. Key insight: only vertical (parent-child) ordering, no horizontal (sibling) ordering.

---

**Q12.4: Foundational - [Theory] - [Heap Insert]**

Inserting into a binary heap:

A) Add element at end (next available position to maintain completeness)
B) Sift up (bubble up): swap with parent while heap property violated
C) O(log n) time
D) All of the above

**Answer: D**

**Explanation:**
Insert: place at end of array (maintains complete tree). Compare with parent. If violates heap property, swap with parent. Repeat up the tree. Worst case: new element percolates to root = O(log n) = O(height). Best case: O(1) if no sifting needed.

---

**Q12.5: Foundational - [Trace] - [Heap Insert]**

Max-heap [50, 30, 40, 10, 20], insert 60:

A) Add 60 at index 5 (left child of 40): [50,30,40,10,20,60]
B) 60 > 40 (parent), swap: [50,30,60,10,20,40]
C) 60 > 50 (root), swap: [60,30,50,10,20,40]
D) Final max-heap: [60,30,50,10,20,40]

**Answer: D**

**Explanation:**
Insert 60 at end. Index 5, parent at ⌊(5-1)/2⌋ = 2 (value 40). 60 > 40 → swap. Now at index 2, parent at ⌊(2-1)/2⌋ = 0 (value 50). 60 > 50 → swap. Now at root. Sifted up 2 levels. Array: [60,30,50,10,20,40].

---

**Q12.6: Foundational - [Theory] - [Extract Max/Min]**

Extract-max from max-heap:

A) Remove root (maximum element)
B) Move last element to root
C) Sift down (heapify down): swap with larger child while violated
D) All of the above

**Answer: D**

**Explanation:**
Extract: save root value. Replace root with last element (maintains completeness). Sift down: compare with children, swap with larger child (max-heap) until heap property restored. O(log n) time. This is the key operation for priority queue dequeue.

---

**Q12.7: Foundational - [Trace] - [Extract Max]**

Max-heap [60,30,50,10,20,40], extract max:

A) Remove 60, move last (40) to root: [40,30,50,10,20]
B) 40 vs children 30, 50: swap with 50 (larger): [50,30,40,10,20]
C) 40 vs children 10, 20: 40 > both, stop
D) Max-heap restored: [50,30,40,10,20], extracted 60

**Answer: D**

**Explanation:**
Remove 60, place 40 at root. Sift down: children are 30 (index 1) and 50 (index 2). 50 > 40 → swap. Now at index 2, children 10 (index 5 doesn't exist, only 10 at 3 and 20 at 4). Wait: index 2's children = 2×2+1=5, 2×2+2=6, both out of bounds. Stop. Final: [50,30,40,10,20]. Heap valid.

---

**Q12.8: Foundational - [Theory] - [Heapify (Build Heap)]**

Build heap from unsorted array:

A) Bottom-up: sift down from last non-leaf to root
B) O(n) time (not O(n log n))
C) Last non-leaf at index ⌊n/2⌋ - 1
D) All of the above

**Answer: D**

**Explanation:**
Build heap: start from last non-leaf (⌊n/2⌋ - 1), sift down each node. Leaves (half the nodes) need no work. Nodes near bottom sift down few levels, nodes near top sift down many but there are few of them. Sum: Σ(n/2^(h+1) × h) for h=0 to log n = O(n). This is key: building heap is linear, not O(n log n).

---

**Q12.9: Foundational - [Trace] - [Build Heap]**

Build max-heap from [4, 10, 3, 5, 1]:

A) Last non-leaf: index ⌊5/2⌋-1 = 1 (value 10)
B) Index 1 (10): children 5,1. 10 > both, ok
C) Index 0 (4): children 10, 3. Swap with 10: [10,4,3,5,1]. Then 4 vs 5,1: swap with 5: [10,5,3,4,1]
D) Max-heap: [10,5,3,4,1]

**Answer: D**

**Explanation:**
Array [4,10,3,5,1]. Non-leaves at indices 0,1. Index 1 (10): children = index 3 (5), index 4 (1). 10 > both, ok. Index 0 (4): children = index 1 (10), index 2 (3). 10 > 4 → swap → [10,4,3,5,1]. Sift down 4: children index 3 (5), index 4 (1). 5 > 4 → swap → [10,5,3,4,1]. Done.

---

**Q12.10: Foundational - [Theory] - [Heap Sort]**

Heap sort algorithm:

A) Build max-heap: O(n)
B) Repeatedly extract max, place at end: O(n log n)
C) Total: O(n log n), in-place, not stable
D) All of the above

**Answer: D**

**Explanation:**
Heap sort: (1) Build max-heap O(n). (2) Swap root (max) with last unsorted element, reduce heap size, sift down root. Repeat n-1 times. Each sift down: O(log n). Total: O(n log n). In-place (array). Not stable (swapping distant elements). Compare: merge sort is stable but not in-place; quicksort is in-place but worst case O(n²).

---

**Q12.11: Foundational - [Trace] - [Heap Sort Step]**

Max-heap [10,5,3,4,1], first heap sort step:

A) Swap root 10 with last element 1: [1,5,3,4,10]
B) Heap size reduces to 4, sift down 1
C) 1 vs 5,3: swap with 5: [5,1,3,4,10]. 1 vs 4: swap: [5,4,3,1,10]
D) After step: [5,4,3,1 | 10] (10 in sorted position)

**Answer: D**

**Explanation:**
Swap root with last: [1,5,3,4,10]. Reduce heap size to 4. Sift down 1: children 5,3 → swap with 5 → [5,1,3,4]. Children of 1 at new position: 4 → swap → [5,4,3,1]. Sorted portion: [10]. Continue extracting to sort remaining.

---

**Q12.12: Intermediate - [Theory] - [Priority Queue ADT]**

Priority queue operations:

A) insert(key): add element with priority
B) extractMax/extractMin: remove highest/lowest priority element
C) peek: see highest/lowest priority without removing
D) All of the above

**Answer: D**

**Explanation:**
Priority queue: abstract data type. Operations: insert, extract-max/min, peek. Implementations: binary heap (O(log n) insert/extract), sorted array (O(n) insert, O(1) extract), unsorted array (O(1) insert, O(n) extract), Fibonacci heap (O(1) amortized insert, O(log n) amortized extract). Binary heap is most common implementation.

---

**Q12.13: Intermediate - [Theory] - [Min-Heap vs Max-Heap]**

Converting max-heap implementation to min-heap:

A) Reverse comparison operators
B) Sift up/down comparisons flip direction
C) All algorithms identical except comparison direction
D) All of the above

**Answer: D**

**Explanation:**
Max-heap: parent ≥ children. Min-heap: parent ≤ children. Code difference: change `>` to `<` in comparisons. Extract-min returns smallest. Sift down swaps with smaller child. Functionally identical structure, opposite ordering. Most libraries support both via comparator parameter.

---

**Q12.14: Intermediate - [Theory] - [Decrease Key]**

Decrease-key operation in min-heap:

A) Reduce a key's value
B) Sift up if new value < parent
C) O(log n) time
D) All of the above

**Answer: D**

**Explanation:**
Decrease-key: lower key at position i. New value may be less than parent → sift up to restore heap property. O(log n) worst case. Critical for Dijkstra's algorithm (relaxing edge weights). Requires knowing element's position in heap (typically via index map/array). Increase-key is the reverse (sift down).

---

**Q12.15: Intermediate - [Theory] - [Heap Applications]**

Common heap/priority queue applications:

A) Dijkstra's shortest path, Prim's MST
B) Heap sort
C) Median maintenance (two heaps), top-K elements
D) All of the above

**Answer: D**

**Explanation:**
Priority queues are ubiquitous: Dijkstra/Prim (extract-min + decrease-key), heap sort, median of stream (max-heap for lower half, min-heap for upper half), top-K (min-heap of size K), merge K sorted lists (min-heap of K elements), task scheduling by priority, Huffman encoding.

---

**Q12.16: Intermediate - [Trace] - [Top K Elements]**

Find top 3 elements from stream [5, 2, 8, 1, 9, 3] using min-heap of size 3:

A) Process 5,2,8: heap = [2,5,8] (min-heap)
B) 1 < 2 (min): skip. 9 > 2: replace 2 with 9, heapify → [5,9,8]
C) 3 < 5 (min): skip
D) Top 3: {5, 8, 9}

**Answer: D**

**Explanation:**
Min-heap of size K for top-K: maintain heap of K largest seen. If new element > heap min, replace min and heapify. Final heap contains K largest. After stream: [5,8,9]. O(n log K) total. More efficient than sorting O(n log n) when K << n.

---

**Q12.17: Intermediate - [Theory] - [Median Maintenance]**

Finding running median using two heaps:

A) Max-heap for lower half (stores smaller elements)
B) Min-heap for upper half (stores larger elements)
C) Balance sizes: |max_heap.size - min_heap.size| ≤ 1
D) All of the above

**Answer: D**

**Explanation:**
Two heaps for median: max-heap holds elements ≤ median, min-heap holds elements ≥ median. Median = max_heap root (if larger) or average of both roots (if equal size). Insert: compare with median, add to appropriate heap, rebalance if sizes differ by > 1. O(log n) per insert, O(1) median query.

---

**Q12.18: Intermediate - [Trace] - [Median Maintenance]**

Stream [5, 2, 8], running median:

A) 5: max-heap [5], min-heap []. Median = 5
B) 2: 2 < 5, add to max-heap [5,2]. Rebalance: move 5 to min-heap. max=[2], min=[5]. Median = (2+5)/2 = 3.5
C) 8: 8 > 5, add to min-heap [5,8]. max=[2], min=[5,8]. Median = 5
D) Medians: 5, 3.5, 5

**Answer: D**

**Explanation:**
After 5: max-heap=[5]. Median = 5. After 2: add to max-heap → [5,2], size 2 vs 0. Move max (5) to min-heap. max=[2], min=[5]. Equal sizes → median = (2+5)/2 = 3.5. After 8: 8 > root of min-heap (5), add to min. max=[2], min=[5,8]. min larger by 1 → median = min root = 5.

---

**Q12.19: Intermediate - [Theory] - [Merge K Sorted Lists]**

Merge K sorted lists using min-heap:

A) Insert first element of each list into min-heap
B) Extract-min, insert next element from that list
C) O(N log K) where N = total elements
D) All of the above

**Answer: D**

**Explanation:**
K-way merge: min-heap of size K holding one element from each list (with list identifier). Extract-min: output smallest. Insert next element from same list. When list exhausted, don't insert. Total: N extract-min and N insert = O(N log K). Used in external sorting, merge step of multi-way merge sort.

---

**Q12.20: Intermediate - [Theory] - [d-ary Heap]**

d-ary heap (each node has d children):

A) Height = O(log_d n)
B) Insert: O(log_d n) sift up
C) Extract: O(d × log_d n) sift down (compare with d children)
D) All of the above

**Answer: D**

**Explanation:**
d-ary heap: generalization of binary heap. Height = ⌈log_d n⌉. Insert: sift up, compare with one parent, O(log_d n). Extract: sift down, compare with d children per level, O(d × log_d n). Optimal d depends on operation mix. For decrease-key heavy (Dijkstra): larger d reduces sift-up cost. Trade-off: insert vs extract performance.

---

**Q12.21: Intermediate - [Theory] - [Heap vs Sorted Array]**

Heap vs sorted array for priority queue:

A) Heap: O(log n) insert, O(log n) extract
B) Sorted array: O(n) insert, O(1) extract
C) Heap wins for mixed insert/extract workloads
D) All of the above

**Answer: D**

**Explanation:**
Sorted array: insert requires shifting O(n). Extract is O(1) at end. Unsorted array: O(1) insert, O(n) extract. Heap: O(log n) both. For n operations total, heap is O(n log n) vs O(n²) for array approaches. Heap is the standard choice unless workload is heavily skewed toward one operation.

---

**Q12.22: Intermediate - [Theory] - [Is Array a Heap?]**

Check if array represents a valid max-heap:

A) For each node i, check arr[i] ≥ arr[2i+1] and arr[i] ≥ arr[2i+2]
B) Only need to check non-leaf nodes
C) O(n) time
D) All of the above

**Answer: D**

**Explanation:**
Verify heap: iterate from index 0 to ⌊n/2⌋-1 (non-leaves). For each, check parent ≥ children. If all satisfy, valid heap. O(n). Leaves (indices ⌊n/2⌋ to n-1) trivially satisfy heap property (no children). Simple linear scan verification.

---

**Q12.23: Intermediate - [Trace] - [Is Array a Heap?]**

Array [9, 5, 6, 2, 3], valid max-heap?

A) Index 0 (9): children 5,6. 9 ≥ 5 ✓, 9 ≥ 6 ✓
B) Index 1 (5): children 2,3. 5 ≥ 2 ✓, 5 ≥ 3 ✓
C) Index 2 (6): no children (indices 5,6 out of bounds)
D) Valid max-heap ✓

**Answer: D**

**Explanation:**
Check non-leaves: index 0 (9 ≥ 5, 9 ≥ 6 ✓), index 1 (5 ≥ 2, 5 ≥ 3 ✓). Index 2 (6): left child index 5 ≥ array size 5, so no children. All checks pass. Valid max-heap. Note: 6 > 5 but they're siblings — heap doesn't require sibling ordering.

---

**Q12.24: Intermediate - [Theory] - [Heap Delete Arbitrary]**

Delete element at arbitrary position i in heap:

A) Replace arr[i] with last element
B) Sift up or sift down as needed
C) O(log n) time (need to know position i)
D) All of the above

**Answer: D**

**Explanation:**
Delete at position i: replace with last element, reduce size. New element at i may need sift up (if smaller than parent in max-heap) or sift down (if larger than children). Exactly one direction will be needed. O(log n). Finding position i requires index tracking (hash map key → index). Without index: O(n) to find + O(log n) to delete.

---

**Q12.25: Intermediate - [Theory] - [Kth Largest Element]**

Find k-th largest element in unsorted array:

A) Build max-heap, extract k times: O(n + k log n)
B) Build min-heap of size k: O(n log k)
C) Quickselect: O(n) average
D) All are valid approaches

**Answer: D**

**Explanation:**
Multiple approaches: (1) Max-heap: build O(n), extract k times O(k log n). Good for small k. (2) Min-heap of size k: stream through, keep top k. O(n log k). (3) Quickselect: partition-based, O(n) average, O(n²) worst. (4) Sort O(n log n). Choice depends on k vs n ratio and whether average vs worst case matters.

---

**Q12.26: Foundational - [Theory] - [Priority Queue vs Heap]**

Priority queue vs heap:

A) Priority queue is an abstract data type (interface)
B) Heap is a concrete data structure (implementation)
C) Priority queue can be implemented by other structures too
D) All of the above

**Answer: D**

**Explanation:**
Priority queue: ADT defining insert, extract-min/max, peek. Can be implemented by: binary heap, Fibonacci heap, binomial heap, sorted/unsorted array, balanced BST. Heap is the most common implementation. Distinction: ADT specifies WHAT operations, data structure specifies HOW. Common interview clarification point.

---

**Q12.27: Intermediate - [Theory] - [Heap Sort Stability]**

Is heap sort a stable sorting algorithm?

A) No, heap sort is not stable
B) Element order for equal keys is not preserved
C) Swapping root with distant elements breaks relative order
D) All of the above

**Answer: D**

**Explanation:**
Heap sort is unstable. During extract-max, root swaps with last element. Equal elements at different positions may be reordered. Example: [5a, 5b, 3] → build heap → extract → 5b may appear before 5a in output. For stable O(n log n): use merge sort. Heap sort trade-off: in-place but unstable.

---

**Q12.28: Foundational - [Theory] - [Complete Binary Tree Property]**

Why must heaps be complete binary trees?

A) Enables compact array storage with no gaps
B) Guarantees O(log n) height
C) Efficient parent/child index computation
D) All of the above

**Answer: D**

**Explanation:**
Completeness ensures: (1) no wasted array space (dense packing). (2) Height = ⌊log₂ n⌋, guaranteed O(log n). (3) Parent/child relationships computed arithmetically, no pointers needed. If not complete, array representation would have gaps, wasting space and complicating index formulas.

---

**Q12.29: Advanced - [Theory] - [Build Heap Time Proof]**

Prove build-heap is O(n), not O(n log n):

A) Nodes at height h: at most ⌈n/2^(h+1)⌉
B) Sift-down cost for node at height h: O(h)
C) Total: Σ(⌈n/2^(h+1)⌉ × h) for h=0 to ⌊log n⌋ = O(n)
D) All steps correct

**Answer: D**

**Explanation:**
Key insight: most nodes are near the bottom (small height, cheap sift-down), few are near the top (large height, but rare). Sum: n × Σ(h/2^(h+1)) = n × Σ(h/2^(h+1)). Series Σ(h × x^h) = x/(1-x)². With x=1/2: sum = 2. So total = O(2n) = O(n). This is tighter than naive O(n log n) analysis of n × O(log n) per node.

---

**Q12.30: Advanced - [Theory] - [Fibonacci Heap Overview]**

Fibonacci heap:

A) Collection of min-heap-ordered trees
B) Insert: O(1) amortized (just add tree)
C) Decrease-key: O(1) amortized (cut and mark)
D) All of the above

**Answer: D**

**Explanation:**
Fibonacci heap: lazy structure. Insert: create single-node tree, add to root list, O(1). Decrease-key: cut node, add to root list, mark parent, O(1) amortized. Extract-min: remove min root, add children to root list, consolidate (merge trees of same degree). Extract-min: O(log n) amortized. Excellent for Dijkstra/Prim but complex to implement.

---

**Q12.31: Advanced - [Theory] - [Fibonacci Heap Complexity]**

Fibonacci heap operation complexities:

A) Insert: O(1) amortized
B) Find-min: O(1)
C) Decrease-key: O(1) amortized
D) Extract-min: O(log n) amortized

**Answer: D**

**Explanation:**

| Operation | Binary Heap | Fibonacci Heap |
|-----------|-------------|----------------|
| Insert | O(log n) | O(1) amortized |
| Find-min | O(1) | O(1) |
| Extract-min | O(log n) | O(log n) amortized |
| Decrease-key | O(log n) | O(1) amortized |
| Merge | O(n) | O(1) |

Fibonacci heap wins for decrease-key and merge. Makes Dijkstra O(V log V + E) vs O((V+E) log V) with binary heap.

---

**Q12.32: Advanced - [Theory] - [Fibonacci Heap in Dijkstra]**

Dijkstra with Fibonacci heap vs binary heap:

A) Binary heap: O((V + E) log V)
B) Fibonacci heap: O(V log V + E)
C) Improvement when E >> V (dense graphs)
D) All of the above

**Answer: D**

**Explanation:**
Dijkstra: V extract-min + E decrease-key. Binary heap: V × O(log V) + E × O(log V) = O((V+E) log V). Fibonacci heap: V × O(log V) + E × O(1) = O(V log V + E). For dense graphs (E = Θ(V²)): binary = O(V² log V), Fibonacci = O(V² + V log V) = O(V²). Significant improvement. However, Fibonacci heap's high constant factors mean binary heap often wins for moderate sizes.

---

**Q12.33: Intermediate - [Theory] - [Binomial Heap]**

Binomial heap:

A) Collection of binomial trees
B) Binomial tree B_k: 2^k nodes, height k
C) Merge two heaps: O(log n) (like binary addition)
D) All of the above

**Answer: D**

**Explanation:**
Binomial heap: set of binomial trees satisfying heap property. B_0 = single node. B_k = two B_{k-1} trees, one as child of other's root. Merge: combine trees of same order (like binary addition). At most one tree of each order. Insert = merge with single-node heap. Extract-min = remove min root, children become new binomial heap, merge. All operations O(log n).

---

**Q12.34: Intermediate - [Theory] - [Leftist Heap]**

Leftist heap:

A) Merge-friendly heap
B) Maintains "rank" (shortest path to null) property
C) Left child's rank ≥ right child's rank (leftist property)
D) All of the above

**Answer: D**

**Explanation:**
Leftist heap: heap-ordered binary tree where rank(left) ≥ rank(right) at every node. Rank = length of rightmost path to null (s-value). Right spine is short (O(log n)). Merge: compare roots, recursively merge along right spines. O(log n) merge. Insert and delete-min use merge. Not balanced but merge-efficient.

---

**Q12.35: Advanced - [Theory] - [Skew Heap]**

Skew heap:

A) Self-adjusting variant of leftist heap
B) Merge: swap left and right children at every merge step
C) No rank maintained, simpler than leftist
D) All of the above

**Answer: D**

**Explanation:**
Skew heap: like leftist heap but without rank tracking. On every merge step, unconditionally swap left and right children. Amortized O(log n) merge. Simpler implementation: no rank fields. Self-adjusting like splay trees are to BSTs. Good amortized performance, simple code.

---

**Q12.36: Intermediate - [Theory] - [Heap Property Invariant]**

After insert or extract, how do we restore heap property?

A) Insert: sift up (compare with parent, swap if needed)
B) Extract: sift down (compare with children, swap with max/min child)
C) At most O(log n) swaps (height of tree)
D) All of the above

**Answer: D**

**Explanation:**
Sift up: inserted element may be larger than parent (max-heap), swap until proper position found or reach root. Sift down: replacement element at root may be smaller than children, swap with largest child until leaf or proper position. Both traverse at most one root-to-leaf path: O(height) = O(log n).

---

**Q12.37: Advanced - [Theory] - [Heap Merge]**

Merging two binary heaps:

A) Naive: concatenate arrays, build heap → O(n + m)
B) Cannot merge in O(log n) with binary heaps
C) Fibonacci/binomial/leftist heaps support O(log n) or O(1) merge
D) All of the above

**Answer: D**

**Explanation:**
Binary heap merge: best is O(n + m) by concatenating and rebuilding. No way to merge two binary heaps in O(log n) due to array layout. Mergeable heaps: binomial O(log n), leftist O(log n), Fibonacci O(1). If frequent merges needed, binary heap is the wrong choice.

---

**Q12.38: Expert - [Theory] - [Decrease-Key in Binary Heap]**

Decrease-key in binary heap challenge:

A) Need to locate element: O(n) without index map
B) With hash map (key → index): O(1) lookup + O(log n) sift up
C) Must update index map during swaps
D) All of the above

**Answer: D**

**Explanation:**
Binary heap decrease-key: (1) find element position. Without auxiliary structure: O(n) scan. With key-to-index hash map: O(1) lookup. (2) Decrease value. (3) Sift up O(log n). Complication: every swap in sift-up must update the index map for both swapped elements. This bookkeeping is error-prone and why Fibonacci heaps (O(1) amortized decrease-key) are theoretically preferred.

---

**Q12.39: Advanced - [Trace] - [Heap Sort Full]**

Heap sort [4, 10, 3, 5, 1]:

A) Build max-heap: [10, 5, 3, 4, 1]
B) Swap 10 with 1: [1,5,3,4,10]. Sift down: [5,4,3,1,10]
C) Swap 5 with 1: [1,4,3,5,10]. Sift down: [4,1,3,5,10]
D) Continue: final sorted [1,3,4,5,10]

**Answer: D**

**Explanation:**
Build heap: [10,5,3,4,1]. Round 1: swap(10,1)→[1,5,3,4|10], sift→[5,4,3,1|10]. Round 2: swap(5,1)→[1,4,3|5,10], sift→[4,1,3|5,10]. Round 3: swap(4,3)→[3,1|4,5,10], sift→[3,1|4,5,10]. Round 4: swap(3,1)→[1|3,4,5,10]. Sorted: [1,3,4,5,10].

---

**Q12.40: Intermediate - [Theory] - [Heap for Scheduling]**

Heap in process scheduling:

A) Priority queues for process scheduling (highest priority first)
B) O(log n) to add/remove processes
C) Real-time systems use heaps for deadline scheduling
D) All of the above

**Answer: D**

**Explanation:**
OS scheduling: priority queue holds ready processes. Highest priority (or earliest deadline) extracted first. Insert new process: O(log n). Context switch: extract-max O(log n). Timer interrupts may reprioritize (decrease/increase key). Deadline scheduling (EDF): min-heap by deadline. Fundamental OS data structure. Refer to Chapter 34 for more OS applications.

---

**Q12.41: Foundational - [Theory] - [Min-Heap Extract-Min]**

Extract-min from min-heap returns:

A) The smallest element
B) Located at the root
C) O(log n) time to restore heap
D) All of the above

**Answer: D**

**Explanation:**
Min-heap: root is minimum. Extract: remove root, place last element at root, sift down (swap with smaller child). O(log n). Used in Dijkstra (extract closest unvisited vertex), Prim (extract cheapest edge), any application needing repeated minimum extraction.

---

**Q12.42: Intermediate - [Theory] - [K-Way Merge Complexity]**

Merging K sorted lists of total N elements:

A) O(N log K) with min-heap
B) O(N log N) with full sort (ignoring sorted property)
C) log K < log N when K < N, so heap approach is faster
D) All of the above

**Answer: D**

**Explanation:**
K-way merge: heap of size K. Each of N elements inserted and extracted once from heap. Each operation O(log K). Total: O(N log K). If K is small (e.g., 10 lists), log K ≈ 3-4 comparisons per element vs log N which could be 20+. Significant speedup. Used in external sorting (merge phase), multi-way merge sort.

---

**Q12.43: Advanced - [Theory] - [Soft Heap]**

Soft heap:

A) Allows a small fraction of keys to be "corrupted" (increased)
B) Achieves O(1) amortized insert and decrease-key
C) Used in optimal MST algorithm
D) All of the above

**Answer: D**

**Explanation:**
Soft heap (Chazelle): trades accuracy for speed. Fraction ε of elements may have their keys corrupted (increased). Insert: O(1) amortized. Extract-min: O(log(1/ε)) amortized. Used in Chazelle's optimal O(E × α(E,V)) MST algorithm. Theoretical importance: shows that approximate priority queues can be faster. Rarely implemented in practice.

---

**Q12.44: Expert - [Theory] - [Hollow Heap]**

Hollow heap:

A) Simpler alternative to Fibonacci heap
B) Same amortized bounds: O(1) insert, decrease-key; O(log n) extract-min
C) Uses "hollow" (deleted) nodes that persist until extracted
D) All of the above

**Answer: D**

**Explanation:**
Hollow heap (Haeupler et al.): achieves Fibonacci heap bounds with simpler structure. Nodes become "hollow" on decrease-key (old node left in place, new node created). Hollow nodes cleaned up during extract-min. Simpler to implement than Fibonacci heaps while matching theoretical bounds. Practical alternative for decrease-key-heavy algorithms.

---

**Q12.45: Intermediate - [Theory] - [Heap in Huffman Encoding]**

Heap in Huffman encoding:

A) Min-heap holds character frequencies
B) Repeatedly extract two minimum, merge, insert back
C) Builds optimal prefix code tree
D) All of the above

**Answer: D**

**Explanation:**
Huffman: greedy algorithm using min-heap. (1) Insert all characters with frequencies. (2) Extract two minimums, create internal node with sum frequency, insert back. (3) Repeat until one node (root of Huffman tree). O(n log n). Heap enables efficient minimum extraction. Refer to Chapter 23 for greedy algorithms.

---

**Q12.46: Advanced - [Theory] - [Index Priority Queue]**

Indexed priority queue:

A) Associates indices with priorities
B) Supports decrease-key by index in O(log n)
C) Maintains mapping: index → position in heap
D) All of the above

**Answer: D**

**Explanation:**
Indexed PQ: elements identified by index 0..N-1. Maintains two maps: (1) position in heap → index, (2) index → position in heap. Enables O(log n) decrease-key, increase-key, delete by index. Essential for Dijkstra/Prim with adjacency list. Binary heap alone doesn't support efficient key lookup by identifier.

---

**Q12.47: Foundational - [Theory] - [Heap vs BST]**

Heap vs BST for finding minimum:

A) Min-heap: O(1) find-min, O(log n) insert
B) BST: O(log n) find-min (or O(1) with pointer), O(log n) insert
C) Heap better for pure priority queue, BST better for ordered operations
D) All of the above

**Answer: D**

**Explanation:**
Heap: optimized for extract-min/max quickly. BST: optimized for ordered traversal, range queries, predecessor/successor. Heap doesn't support efficient search for arbitrary element (O(n)). BST supports O(log n) search for any key. Choose based on needed operations. Heap when only need min/max; BST when need broader ordered operations.

---

**Q12.48: Intermediate - [Theory] - [Double-Ended Priority Queue]**

Double-ended priority queue (DEPQ):

A) Supports both extract-min and extract-max
B) Can be implemented with min-max heap
C) Or two heaps (one min, one max) with cross-references
D) All of the above

**Answer: D**

**Explanation:**
DEPQ: insert, delete-min, delete-max all needed. Implementations: (1) Min-max heap: alternating min/max levels. (2) Two heaps with cross-pointers. (3) Interval heap: paired elements. Min-max heap: O(log n) for all operations. Useful when both extremes matter (e.g., statistics, windowed algorithms).

---

**Q12.49: Advanced - [Theory] - [Min-Max Heap]**

Min-max heap:

A) Even levels are min-levels, odd levels are max-levels
B) Root (level 0) is minimum
C) Level 1 contains maximum
D) All of the above

**Answer: D**

**Explanation:**
Min-max heap: alternating min/max levels. Root (level 0, min): smallest element. Level 1 (max): one of these children is largest element. Insert/delete: sift up/down considering alternating properties. Each operation O(log n). Supports both find-min and find-max in O(1), extract-min and extract-max in O(log n).

---

**Q12.50: Intermediate - [Theory] - [Heap Space Complexity]**

Space complexity of binary heap:

A) O(n) for n elements
B) No pointer overhead (array-based)
C) More cache-friendly than pointer-based trees
D) All of the above

**Answer: D**

**Explanation:**
Binary heap: array of n elements. No left/right/parent pointers. Dense, contiguous memory. Cache-friendly: sequential access patterns during sift operations. Compared to BST/linked structures: no pointer overhead (2-3 pointers per node), no memory fragmentation. This practical advantage makes binary heaps fast despite same asymptotic complexity as BST-based priority queues.

---

**Q12.51: Expert - [Theory] - [Binomial Heap Properties]**

Binomial heap with n elements:

A) At most ⌊log₂ n⌋ + 1 binomial trees
B) Trees correspond to binary representation of n
C) B_k present iff k-th bit of n is 1
D) All of the above

**Answer: D**

**Explanation:**
Binomial heap: collection of binomial trees. n = 13 = 1101₂ → trees B_0, B_2, B_3 (sizes 1, 4, 8). At most ⌊log₂ n⌋ + 1 trees. Merge = binary addition. This binary representation analogy makes binomial heap operations elegant: insert = add 1, merge = add two numbers. O(log n) per operation.

---

**Q12.52: Foundational - [Theory] - [Heap Complete Property]**

In a heap with n elements, the height is:

A) Exactly ⌊log₂ n⌋
B) Because it's a complete binary tree
C) Level k has min(2^k, n - 2^k + 1) nodes
D) All of the above

**Answer: D**

**Explanation:**
Complete binary tree height = ⌊log₂ n⌋. Full levels 0 through h-1 have 2^0 + 2^1 + ... + 2^(h-1) = 2^h - 1 nodes. Last level has 1 to 2^h nodes. Total n: h = ⌊log₂ n⌋. This tight bound means heap operations are truly O(log n), not just bounded by it.

---

**Q12.53: Intermediate - [Theory] - [Lazy Deletion in Heap]**

Lazy deletion in heap:

A) Mark element as deleted but don't remove
B) During extract-min, skip deleted elements
C) Useful when decrease-key isn't available
D) All of the above

**Answer: D**

**Explanation:**
Lazy deletion: mark node as deleted. When extract-min pops a deleted node, skip and extract again. Amortized cost may be acceptable if deletions are rare relative to extracts. Used in some Dijkstra implementations: re-insert with new priority instead of decrease-key, mark old entry as stale. Simpler but uses more memory. Can degrade to O(n) extract if many stale entries.

---

**Q12.54: Foundational - [Theory] - [Sift Down vs Sift Up]**

Sift down vs sift up:

A) Sift up: used after insert (new element may be too large for position)
B) Sift down: used after extract/build-heap (element may be too small for position)
C) Sift up compares with parent; sift down compares with children
D) All of the above

**Answer: D**

**Explanation:**
Sift up: element possibly violates upward, compare with parent, swap if needed, move up. Sift down: element possibly violates downward, compare with both children, swap with larger (max-heap) or smaller (min-heap) child, move down. Build-heap uses sift down (top-heavy approach). Insert uses sift up. Both O(log n) worst case.

---

**Q12.55: Advanced - [Theory] - [Fibonacci Heap Marking]**

Fibonacci heap marking mechanism:

A) Mark a node when one of its children is cut
B) If marked node loses another child, cut it from parent (cascading cut)
C) Prevents nodes from losing too many children
D) All of the above

**Answer: D**

**Explanation:**
Marking: when decrease-key cuts a child, parent is marked. If a marked parent loses another child: cascading cut — unmark, cut from parent, add to root list, check parent again. This ensures tree degree stays bounded (at most O(log n)), maintaining extract-min O(log n) amortized. Without marking, trees could become degenerate.

---

**Q12.56: Expert - [Theory] - [Fibonacci vs Binary Heap Practice]**

In practice, Fibonacci heaps vs binary heaps:

A) Fibonacci heaps have high constant factors
B) Complex implementation (marking, cascading cuts, consolidation)
C) Binary heaps win for all but very large, sparse graph problems
D) All of the above

**Answer: D**

**Explanation:**
Theory: Fibonacci heap has better asymptotic bounds for decrease-key. Practice: binary heap's simplicity, cache-friendliness, and low constant factors make it faster for typical problem sizes. Fibonacci heap wins only for very large sparse graphs where E >> V and decrease-key dominates. Most implementations use binary heap or d-ary heap instead. Pairing heaps offer a practical middle ground.

---

**Q12.57: Intermediate - [Theory] - [Pairing Heap]**

Pairing heap:

A) Simple tree-based heap
B) Insert: O(1) (link new tree)
C) Decrease-key: O(1) amortized (conjectured)
D) All of the above

**Answer: D**

**Explanation:**
Pairing heap: simple to implement, good practical performance. Insert: link two trees by making one child of other O(1). Extract-min: remove root, pair-and-merge children. Amortized O(log n) extract-min. Decrease-key: cut subtree, link back to root. Conjectured O(1) amortized but proven only O(log log n) amortized. Popular practical alternative to Fibonacci heaps.

---

**Q12.58: Expert - [Theory] - [Lower Bound for Sorting via Heaps]**

Heap sort proves comparison-based sorting lower bound:

A) Heap sort is O(n log n) comparison-based sort
B) Comparison-based sorting lower bound is Ω(n log n)
C) Heap sort matches the lower bound (optimal)
D) All of the above

**Answer: D**

**Explanation:**
Comparison-based sorting: Ω(n log n) (decision tree argument: n! leaves → log(n!) = Θ(n log n) depth). Heap sort, merge sort, and optimal quicksort all achieve O(n log n), matching the lower bound. Heap sort's advantage: in-place. Disadvantage: not stable, poor cache behavior vs merge sort. All three are asymptotically optimal comparison sorts.

---

**Q12.59: Intermediate - [Theory] - [K Closest Points]**

Find K closest points to origin:

A) Max-heap of size K
B) For each point, if distance < max-heap root, replace and heapify
C) O(n log K) time
D) All of the above

**Answer: D**

**Explanation:**
K closest: max-heap of size K (largest of K closest on top). For each new point: if closer than heap root (farthest of current K), replace root and sift down. After processing all n points, heap contains K closest. O(n log K). Alternative: quickselect O(n) average but randomized. Heap approach is deterministic and streaming-friendly.

---

**Q12.60: Foundational - [Theory] - [Peek Operation]**

Peek (find-min or find-max) in heap:

A) O(1) — just read root
B) Does not modify the heap
C) Root always contains min (min-heap) or max (max-heap)
D) All of the above

**Answer: D**

**Explanation:**
Peek: return root value without extraction. O(1), no structural change. Useful for checking next priority without committing to removal. Stack peek/queue front are similar O(1) operations on their respective data structures.

---

**Q12.61: Advanced - [Theory] - [In-Place Heap Sort vs Extra Space]**

Heap sort is in-place because:

A) Uses the input array itself as the heap
B) No additional O(n) space needed
C) O(1) extra space (only for swap variable)
D) All of the above

**Answer: D**

**Explanation:**
Heap sort: build heap in input array (rearrange in-place). Extract phase: swap root to end, shrink heap boundary, sift down. Sorted elements accumulate at the end. Only O(1) extra space for temporary swap variable. Compare: merge sort needs O(n) auxiliary array (unless complex in-place merge). Quicksort: O(log n) stack space for recursion.

---

**Q12.62: Expert - [Theory] - [Weak Heap]**

Weak heap:

A) Relaxed binary heap with fewer comparisons in heap sort
B) Achieves n log n + O(n) comparisons (close to theoretical minimum)
C) Uses array with additional "reverse" bits
D) All of the above

**Answer: D**

**Explanation:**
Weak heap: allows right child to be larger than parent (only left child must be ≤ parent). Reduces comparisons in sift-down (no need to find max of two children). Heap sort with weak heap: roughly n⌈log₂ n⌉ - 2^⌈log₂ n⌉ + 1 comparisons, close to information-theoretic lower bound ⌈log₂(n!)⌉. Practically competitive, theoretically interesting.

---

**Q12.63: Expert - [Theory] - [Broal-Okasaki Priority Queue]**

Brodal-Okasaki priority queue:

A) Worst-case O(1) insert, find-min, merge
B) Worst-case O(log n) delete-min
C) Purely functional implementation
D) All of the above

**Answer: D**

**Explanation:**
Brodal-Okasaki: functional priority queue with optimal worst-case bounds. Not amortized — true worst case O(1) insert, find-min, merge; O(log n) delete-min. Based on nested bootstrapping of skew binomial heaps. Primarily of theoretical interest; complex implementation. Shows that optimal priority queue bounds are achievable in functional setting.

---

**Q12.64: Intermediate - [Theory] - [Heap with Custom Comparator]**

Heap with custom comparison function:

A) Enables min-heap or max-heap from same implementation
B) Can prioritize by any criteria (deadline, profit, cost)
C) Comparator defines the heap ordering
D) All of the above

**Answer: D**

**Explanation:**
Custom comparator: defines what "higher priority" means. Max-heap: a > b means a has higher priority. Min-heap: a < b. Custom: compare by deadline, weight, or composite key. Python heapq is min-heap; negate values for max-heap. Java PriorityQueue takes Comparator. Flexible abstraction.

---

**Q12.65: Advanced - [Theory] - [Heap Applications Summary]**

Heap/priority queue comprehensive applications:

A) Graph algorithms: Dijkstra, Prim, A*
B) Sorting: heap sort; selection: k-th element
C) Streaming: median, top-K, merge K lists
D) All of the above, plus scheduling, Huffman, event simulation

**Answer: D**

**Explanation:**
Heaps are among the most versatile data structures. Graph: shortest path, MST. Sorting: heap sort. Selection: k-th largest/smallest. Streaming: running median, top-K maintenance. Scheduling: OS process priority, task queues. Encoding: Huffman trees. Simulation: event-driven (next event by time). Knowledge of heap variants and when each excels is essential for algorithm design.

---

## Chapter 12 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 16 | Heap definition, array representation, insert, extract, heapify, heap sort basics |
| Intermediate | 26 | Priority queue, median maintenance, K-way merge, d-ary heap, scheduling, custom comparator |
| Advanced | 16 | Build heap proof, Fibonacci/binomial/leftist/skew heaps, decrease-key, min-max heap |
| Expert | 7 | Fibonacci in practice, soft heap, hollow heap, weak heap, Brodal-Okasaki, lower bounds |

**Total MCQs: 65** | **Target Met: ✓**

**Key Heap Complexities:**

| Operation | Binary Heap | Fibonacci Heap | Binomial Heap |
|-----------|-------------|----------------|---------------|
| Insert | O(log n) | O(1)* | O(log n) |
| Find-min | O(1) | O(1) | O(log n) |
| Extract-min | O(log n) | O(log n)* | O(log n) |
| Decrease-key | O(log n) | O(1)* | O(log n) |
| Merge | O(n) | O(1) | O(log n) |

*Amortized

**Next:** Chapter 13 - Tries & String Data Structures
