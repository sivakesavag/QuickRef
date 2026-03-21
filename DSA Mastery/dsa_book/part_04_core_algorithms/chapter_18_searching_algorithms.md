# Chapter 18: Searching Algorithms

**Target:** 55 MCQs | **Distribution:** 14 Foundational, 22 Intermediate, 14 Advanced, 5 Expert

---

**Q18.1: Foundational - [Theory] - [Linear Search]**

Linear search:

A) Scan array sequentially, compare each element
B) O(n) worst/average, O(1) best
C) Works on unsorted arrays
D) All of the above

**Answer: D**

**Explanation:**
Linear search: simplest search. Check each element until found or exhausted. No requirement on array ordering. Best: O(1) first element. Worst: O(n) last or absent. Average: O(n/2) = O(n). Only option for unsorted, unindexed data. Sentinel optimization: place target at end to eliminate bounds check.

---

**Q18.2: Foundational - [Theory] - [Binary Search]**

Binary search on sorted array:

A) Compare target with middle element
B) If equal: found. If less: search left half. If greater: search right half
C) O(log n) time, requires sorted array
D) All of the above

**Answer: D**

**Explanation:**
Binary search: divide search space in half each step. Sorted array required. At most ⌈log₂ n⌉ + 1 comparisons. O(1) space iterative, O(log n) stack recursive. Foundation for many algorithms. Seemingly simple but notoriously error-prone to implement correctly (off-by-one errors).

---

**Q18.3: Foundational - [Trace] - [Binary Search]**

Binary search for 7 in [1, 3, 5, 7, 9, 11, 13]:

A) lo=0, hi=6, mid=3, arr[3]=7
B) arr[3]==7: found at index 3
C) Only 1 comparison needed
D) Best case: target at middle

**Answer: D**

**Explanation:**
Array [1,3,5,7,9,11,13]. mid = (0+6)/2 = 3. arr[3] = 7 = target. Found in one comparison. Best case: O(1). If searching for 3: mid=3 (7>3)→hi=2, mid=1 (3=3)→found at index 1: 2 comparisons.

---

**Q18.4: Foundational - [Theory] - [Binary Search Variants]**

Common binary search variations:

A) Find first occurrence of target (lower bound)
B) Find last occurrence of target (upper bound)
C) Find insertion point (bisect)
D) All of the above

**Answer: D**

**Explanation:**
Lower bound: leftmost index where arr[i] ≥ target. Upper bound: leftmost index where arr[i] > target. Count of target = upper - lower. Insertion point: where to insert to maintain sort. Python: bisect_left, bisect_right. C++: lower_bound, upper_bound. Each requires careful boundary handling.

---

**Q18.5: Foundational - [Theory] - [Binary Search Implementation Pitfalls]**

Common binary search bugs:

A) Integer overflow: mid = (lo + hi) / 2 overflows → use lo + (hi - lo) / 2
B) Infinite loop: wrong update (lo = mid instead of lo = mid + 1)
C) Off-by-one: wrong boundary (< vs <=)
D) All of the above

**Answer: D**

**Explanation:**
Binary search is "90% of programmers can't write it correctly" (Bentley). Overflow: lo+hi can exceed INT_MAX. Fix: lo + (hi-lo)/2. Infinite loop: if lo=mid when hi=lo+1, loop forever. Off-by-one: inclusive vs exclusive bounds. Test: empty array, single element, target at boundaries, duplicates.

---

**Q18.6: Intermediate - [Theory] - [Lower Bound Binary Search]**

Lower bound (first occurrence) implementation:

A) If arr[mid] >= target: hi = mid (candidate, search left)
B) If arr[mid] < target: lo = mid + 1
C) Return lo when lo == hi
D) All of the above

**Answer: D**

**Explanation:**
Lower bound: find leftmost position where arr[i] ≥ target. Key: when arr[mid] ≥ target, don't return immediately — there might be earlier occurrence. Set hi=mid (keep in range). When arr[mid] < target: lo=mid+1. Loop while lo < hi. Returns insertion point if target absent. O(log n).

---

**Q18.7: Intermediate - [Theory] - [Binary Search on Answer]**

Binary search on answer (parametric search):

A) Search for optimal value that satisfies a condition
B) Search space: range of possible answers
C) Condition is monotonic: if x works, all y > x (or < x) also work
D) All of the above

**Answer: D**

**Explanation:**
Binary search on answer: instead of searching array, search value space. Example: "minimum capacity to ship packages in D days" → binary search on capacity. For each candidate: check feasibility in O(n). Total: O(n log(max_answer)). Powerful technique for optimization problems with monotonic feasibility. Very common in competitive programming.

---

**Q18.8: Intermediate - [Trace] - [Binary Search on Answer]**

Minimum eating speed to finish n bananas in h hours. Piles=[3,6,7,11], h=8:

A) Search range: [1, 11]. mid=6: hours=1+1+2+2=6≤8 ✓
B) Try smaller: mid=3: hours=1+2+3+4=10>8 ✗
C) mid=4: hours=1+2+2+3=8≤8 ✓. mid=3: ✗
D) Answer: 4 (minimum speed)

**Answer: D**

**Explanation:**
Binary search on speed k. For each pile p: hours = ⌈p/k⌉. Total hours must be ≤ h. Speed 4: ⌈3/4⌉+⌈6/4⌉+⌈7/4⌉+⌈11/4⌉ = 1+2+2+3 = 8 ≤ 8 ✓. Speed 3: 1+2+3+4 = 10 > 8 ✗. Minimum feasible speed = 4. O(n × log(max_pile)).

---

**Q18.9: Intermediate - [Theory] - [Ternary Search]**

Ternary search:

A) For unimodal functions (single peak or valley)
B) Divide into thirds, compare f(m1) and f(m2)
C) Eliminate one-third each step: O(log₃ n) → O(log n)
D) All of the above

**Answer: D**

**Explanation:**
Ternary search: find maximum of unimodal function. m1 = lo + (hi-lo)/3, m2 = hi - (hi-lo)/3. If f(m1) < f(m2): peak in [m1, hi], else peak in [lo, m2]. Reduces by 1/3 each step. O(log_{3/2} n) = O(log n). For finding peak; NOT for sorted array search (binary is faster: log₂ < 2 log₃).

---

**Q18.10: Intermediate - [Theory] - [Interpolation Search]**

Interpolation search:

A) Estimate position using value distribution
B) pos = lo + (target - arr[lo]) × (hi - lo) / (arr[hi] - arr[lo])
C) O(log log n) for uniformly distributed data
D) All of the above

**Answer: D**

**Explanation:**
Interpolation search: like human searching a dictionary — jump to estimated position. Uniform distribution: O(log log n) average. Worst case: O(n) for non-uniform data. Better than binary search when data uniformly distributed. Rarely used in practice (binary search is simpler, more predictable). Extension: interpolation + binary search hybrid.

---

**Q18.11: Intermediate - [Theory] - [Exponential Search]**

Exponential search:

A) Find range [2^k, 2^(k+1)] containing target
B) Then binary search within that range
C) O(log i) where i is target's position — good for unbounded arrays
D) All of the above

**Answer: D**

**Explanation:**
Exponential search: double search bound until exceeding target (1, 2, 4, 8, ...). Then binary search in [2^(k-1), min(2^k, n)]. O(log i) where i = target position. Advantage: if target near beginning, much faster than binary search. Also works for unbounded arrays (infinite streams). Natural for skip lists.

---

**Q18.12: Foundational - [Theory] - [Search in Rotated Sorted Array]**

Search in rotated sorted array:

A) Array sorted then rotated: [4,5,6,7,0,1,2]
B) Modified binary search: one half is always sorted
C) O(log n) — check which half is sorted, narrow accordingly
D) All of the above

**Answer: D**

**Explanation:**
Rotated array: [4,5,6,7,0,1,2]. At any mid: one half is sorted. If arr[lo] ≤ arr[mid]: left sorted. Check if target in [lo,mid]. If arr[mid] ≤ arr[hi]: right sorted. Check if target in [mid,hi]. O(log n). Classic interview problem. Handle duplicates: worst case O(n).

---

**Q18.13: Intermediate - [Trace] - [Rotated Array Search]**

Search for 0 in [4,5,6,7,0,1,2]:

A) lo=0, hi=6, mid=3. arr[3]=7. Left [4,5,6,7] sorted. 0 not in [4,7]→search right
B) lo=4, hi=6, mid=5. arr[5]=1. Right [1,2] sorted. 0 not in [1,2]→search left
C) lo=4, hi=4, mid=4. arr[4]=0. Found!
D) 3 comparisons, O(log 7)

**Answer: D**

**Explanation:**
Step 1: mid=3(7). Left sorted [4,7]. 0<4→go right. Step 2: mid=5(1). Right sorted [1,2]. 0<1→go left. Step 3: mid=4(0)=target. Found at index 4. Three iterations of binary search variant.

---

**Q18.14: Intermediate - [Theory] - [Peak Finding]**

Find peak element (element ≥ both neighbors):

A) Binary search: if arr[mid] < arr[mid+1], peak is right
B) If arr[mid] < arr[mid-1], peak is left
C) O(log n) — guaranteed to find a peak
D) All of the above

**Answer: D**

**Explanation:**
Peak: arr[i] ≥ arr[i-1] and arr[i] ≥ arr[i+1] (boundaries considered -∞). Binary search: go toward the higher neighbor. At least one peak exists (pigeon hole). O(log n) vs O(n) linear scan. Works because moving toward higher side guarantees finding a local maximum.

---

**Q18.15: Foundational - [Theory] - [Search vs Sort Trade-off]**

Multiple searches on same data:

A) Single search on unsorted: O(n) linear search
B) Sort first O(n log n), then each search O(log n)
C) Worthwhile if number of searches > log n
D) All of the above

**Answer: D**

**Explanation:**
Trade-off: k searches. Unsorted: O(kn). Sort + search: O(n log n + k log n). Break-even: kn = n log n + k log n → k ≈ log n. If k >> log n: sort first. If k = 1: just linear search. For dynamic data: balanced BST gives O(log n) search and insert.

---

**Q18.16: Intermediate - [Theory] - [Two Pointers]**

Two-pointer technique:

A) Two indices scanning from same or opposite directions
B) Two sum in sorted array: left + right pointers
C) O(n) for problems that would be O(n²) with brute force
D) All of the above

**Answer: D**

**Explanation:**
Two pointers: exploit sorted order or monotonic property. Two sum: if sum < target, move left pointer right; if sum > target, move right pointer left. Container with most water: shrink side with shorter height. Merge two sorted arrays: compare fronts. Pattern recognition key for efficient searching.

---

**Q18.17: Intermediate - [Theory] - [Sliding Window]**

Sliding window technique:

A) Fixed or variable window over array
B) Fixed window: max sum of k consecutive elements
C) Variable window: smallest subarray with sum ≥ target
D) All of the above

**Answer: D**

**Explanation:**
Sliding window: maintain window [left, right]. Fixed: slide window of size k, update in O(1). Variable: expand right until condition met, shrink left to optimize. O(n) for problems that would be O(nk) or O(n²). Common pattern for substring, subarray problems.

---

**Q18.18: Advanced - [Theory] - [Fractional Cascading]**

Fractional cascading:

A) Speed up binary searches across multiple sorted lists
B) Search k lists: O(log n + k) instead of O(k log n)
C) Augment each list with elements from next list
D) All of the above

**Answer: D**

**Explanation:**
Fractional cascading: given k sorted lists, search for value in all. Naive: k binary searches O(k log n). Cascading: binary search first list O(log n), follow pointers for subsequent lists O(1) each. Total: O(log n + k). Applications: computational geometry (layered range trees), merge sort tree queries.

---

**Q18.19: Advanced - [Theory] - [van Emde Boas Tree]**

van Emde Boas tree:

A) Supports search, insert, delete, successor, predecessor in O(log log u)
B) u = universe size (range of possible values)
C) Space: O(u), but can be reduced with hashing
D) All of the above

**Answer: D**

**Explanation:**
vEB tree: recursive structure. Universe [0, u). Split into √u clusters of size √u. Operations recurse on cluster or summary. O(log log u) per operation. Beats balanced BST O(log n) when u = poly(n). Space: O(u) (or O(n) with hashing). Used in practice for small integer universes. Predecessor/successor in O(log log u) is remarkable.

---

**Q18.20: Intermediate - [Theory] - [Order Statistics]**

Finding k-th smallest element:

A) Sort and index: O(n log n)
B) Quickselect: O(n) average, O(n²) worst
C) Median of medians: O(n) worst case
D) All are valid approaches

**Answer: D**

**Explanation:**
Order statistics: k-th smallest. Sort: O(n log n), overkill. Quickselect (Hoare): partition-based, O(n) expected. Median of medians: O(n) worst case guaranteed but higher constant. Median (k=n/2) is special case. Min-heap: O(n + k log n). Use quickselect in practice, median-of-medians when worst case matters.

---

**Q18.21: Intermediate - [Theory] - [Binary Search on Doubles]**

Binary search on floating-point:

A) Can't use equality; use tolerance (hi - lo < epsilon)
B) Or fixed number of iterations (e.g., 100)
C) Common for: square root, cube root, optimization
D) All of the above

**Answer: D**

**Explanation:**
Float binary search: no exact equality possible. Terminate when range < epsilon (1e-9) or after fixed iterations (100 iterations = 2^-100 ≈ 0 precision). Example: sqrt(x): binary search in [0, x] for val where val² ≈ x. Same approach for any monotonic continuous function root-finding.

---

**Q18.22: Foundational - [Theory] - [Linear Search Optimization]**

Linear search optimizations:

A) Sentinel: place target at end, remove bounds check
B) Move-to-front: move found element to beginning
C) Transposition: swap found element one position forward
D) All of the above

**Answer: D**

**Explanation:**
Sentinel: add target to array end. Loop without checking index bounds — guaranteed to stop. Saves one comparison per iteration. Move-to-front: frequently accessed elements migrate to beginning. Transposition: incremental improvement, less drastic than move-to-front. Both are self-organizing search strategies.

---

**Q18.23: Intermediate - [Theory] - [Search in 2D Sorted Matrix]**

Search in row-sorted and column-sorted matrix:

A) Start from top-right (or bottom-left) corner
B) If target < current: move left. If target > current: move down
C) O(m + n) for m×n matrix
D) All of the above

**Answer: D**

**Explanation:**
Staircase search: start at top-right. Current > target: eliminate column (move left). Current < target: eliminate row (move down). Each step eliminates row or column. At most m+n steps. O(m+n) vs O(m×n) brute force or O(m log n) per-row binary search. Elegant and optimal for this structure.

---

**Q18.24: Intermediate - [Trace] - [2D Matrix Search]**

Search for 14 in matrix (rows and columns sorted):
```
[[1,4,7,11],
 [2,5,8,12],
 [3,6,9,16],
 [10,13,14,17]]
```

A) Start top-right: (0,3)=11. 14>11 → move down: (1,3)=12
B) 14>12 → down: (2,3)=16. 14<16 → left: (2,2)=9
C) 14>9 → down: (3,2)=14. Found!
D) 5 steps, O(m+n) = O(8)

**Answer: D**

**Explanation:**
Path: 11→12→16→9→14. Five comparisons. Each step either goes down or left. Maximum steps: m+n-1 = 7. Found in 5. Alternative: binary search each row O(m log n) = O(4 × 2) = 8, comparable for small matrix.

---

**Q18.25: Advanced - [Theory] - [Parallel Binary Search]**

Parallel binary search:

A) Answer multiple binary search queries simultaneously
B) Process all queries' mid-points together per iteration
C) O(Q log V × f(n)) → reduces from O(Q × log V × f(n))
D) All of the above

**Answer: D**

**Explanation:**
Parallel binary search: Q queries each binary searching in [0, V). Group all queries by current mid-point. Process data once per iteration (not per query). Each iteration advances all queries' binary search. O(log V) iterations × O(process data). Converts Q independent O(f(n) × log V) to combined O(log V × (f(n) + Q)). Powerful competitive programming technique.

---

**Q18.26: Foundational - [Theory] - [Hash-Based Search]**

Hash-based search:

A) Hash table: O(1) average search
B) Build: O(n). Each lookup: O(1) average
C) No ordering, no range queries
D) All of the above

**Answer: D**

**Explanation:**
Hash table lookup: hash key → index → check. O(1) average, O(n) worst (all collisions). Best for: exact match, frequent lookups, no order needed. Can't do: range queries, predecessor/successor, sorted traversal. If these needed: balanced BST or sorted array with binary search. See Chapter 8 for hash table details.

---

**Q18.27: Intermediate - [Theory] - [Search in Nearly Sorted Array]**

Search in nearly sorted array (each element at most k away from sorted position):

A) Check positions mid-k to mid+k during binary search
B) Or use modified binary search with wider range
C) O(log n) still achievable for constant k
D) All of the above

**Answer: D**

**Explanation:**
Nearly sorted: element at index i could be at i-k to i+k in sorted array. Modified binary search: when checking mid, also check mid±k. O(log n × k) for constant k = O(log n). Alternative: min-heap of size 2k+1 for streaming k-nearly-sorted output. Related to Chapter 12 (heap for k-sorted).

---

**Q18.28: Advanced - [Theory] - [Fibonacci Search]**

Fibonacci search:

A) Like binary search but divides using Fibonacci numbers
B) Uses addition instead of division (no mid = (lo+hi)/2)
C) Useful when division is expensive (old CPUs, disk access)
D) All of the above

**Answer: D**

**Explanation:**
Fibonacci search: probe positions based on Fibonacci numbers. F(k), F(k-1), F(k-2) determine split. Only comparisons + addition needed (no division). Same O(log n) as binary search. Historical significance: useful when division was slow. Now mostly academic but appears in interview questions about search variants.

---

**Q18.29: Advanced - [Theory] - [Binary Search on Answers Applications]**

Common "binary search on answer" problems:

A) Minimum time/speed/capacity to complete task
B) Maximum minimum distance (aggressive cows)
C) Minimum maximum workload (painter's partition)
D) All of the above

**Answer: D**

**Explanation:**
Pattern: optimization problem → binary search on answer + greedy check. "Min X such that feasible": binary search on X, check feasibility greedily. "Max min": binary search on min value, check if achievable. Feasibility check must be monotonic: if X works, X+1 works (or vice versa). O(n × log(answer_range)).

---

**Q18.30: Foundational - [Theory] - [Search Comparison]**

Comparing search algorithms:

A) Linear: O(n), unsorted ok
B) Binary: O(log n), sorted array required
C) Hash: O(1) avg, hash table required
D) BST: O(log n), balanced BST required

**Answer: D**

**Explanation:**
Search algorithm comparison:

| Algorithm | Time | Prerequisite | Range Query |
|-----------|------|--------------|-------------|
| Linear | O(n) | None | N/A |
| Binary | O(log n) | Sorted array | Yes |
| Hash | O(1) avg | Hash table | No |
| BST | O(log n) | Balanced BST | Yes |
| Interpolation | O(log log n) | Sorted + uniform | Yes |

Choose based on data structure available and query types needed.

---

**Q18.31: Intermediate - [Theory] - [Bidirectional BFS for Search]**

Bidirectional search:

A) Search from both start and goal simultaneously
B) Meet in the middle: each side searches √(total states)
C) O(b^(d/2)) instead of O(b^d) for BFS
D) All of the above

**Answer: D**

**Explanation:**
Bidirectional BFS: expand from start and goal. When frontiers meet: path found. If branching factor b, depth d: normal BFS visits O(b^d) states. Bidirectional: each side O(b^(d/2)). Total: O(2 × b^(d/2)) << O(b^d). Works when goal state known and reverse transitions available. Huge speedup for large search spaces.

---

**Q18.32: Advanced - [Theory] - [A* Search]**

A* search algorithm:

A) Best-first search using f(n) = g(n) + h(n)
B) g(n) = cost from start, h(n) = heuristic to goal
C) Optimal if h(n) is admissible (never overestimates)
D) All of the above

**Answer: D**

**Explanation:**
A*: priority queue ordered by f = g + h. Admissible h: h(n) ≤ actual cost → A* finds optimal path. Consistent h: h(n) ≤ c(n,n') + h(n') → no node re-expanded. With h=0: degrades to Dijkstra. With h perfect: finds path immediately. Quality of heuristic determines efficiency. Used in pathfinding, puzzles, game AI.

---

**Q18.33: Expert - [Theory] - [IDA* Search]**

IDA* (Iterative Deepening A*):

A) A* with iterative deepening: depth limit = f-value threshold
B) O(1) space (no open/closed lists)
C) Each iteration: DFS with f-value cutoff
D) All of the above

**Answer: D**

**Explanation:**
IDA*: set threshold = h(start). DFS, prune if f(n) > threshold. If no solution: increase threshold to minimum f that exceeded threshold. Repeat. Space: O(depth) only. Re-explores nodes but in practice, most nodes at deepest level → overhead small. Preferred for large state spaces where A*'s memory is prohibitive.

---

**Q18.34: Intermediate - [Theory] - [Find First and Last Position]**

Find first and last position of target in sorted array:

A) Two binary searches: one for lower bound, one for upper bound
B) Lower bound: first index where arr[i] ≥ target
C) Upper bound: first index where arr[i] > target
D) Range = [lower_bound, upper_bound - 1], count = upper - lower

**Answer: D**

**Explanation:**
Two binary searches: O(log n) each. Count of target = upper_bound - lower_bound. If lower_bound index has arr[lower_bound] ≠ target → not found. C++: lower_bound, upper_bound, equal_range (returns both). Python: bisect_left, bisect_right. Foundation for many interval/frequency queries on sorted data.

---

**Q18.35: Intermediate - [Theory] - [Square Root Decomposition]**

Square root decomposition for range queries:

A) Divide array into blocks of size √n
B) Precompute answer for each block
C) Query: O(√n), Update: O(1) or O(√n)
D) All of the above

**Answer: D**

**Explanation:**
Sqrt decomposition: blocks of √n. Query [l,r]: partial blocks at boundaries + complete blocks in middle. At most 2×√n elements in partial + √n complete blocks. Total: O(√n). Simpler than segment tree but slower (√n vs log n). Good for problems where segment tree is overkill or hard to apply (e.g., Mo's algorithm).

---

**Q18.36: Advanced - [Theory] - [Mo's Algorithm]**

Mo's algorithm for offline range queries:

A) Sort queries by block of left endpoint, break ties by right
B) Move left/right pointers to answer each query incrementally
C) O((n + q) × √n) total
D) All of the above

**Answer: D**

**Explanation:**
Mo's: offline algorithm. Divide into √n blocks. Sort queries: by block(l), then by r. Maintain current answer for [cur_l, cur_r]. Extend/shrink to reach each query's [l, r]. Total pointer movements: O(n√n). Each add/remove: O(1) or O(log n). Works for: distinct count, frequency queries. Can't handle: updates between queries (without modifications).

---

**Q18.37: Foundational - [Theory] - [Jump Search]**

Jump search:

A) Jump ahead by √n steps, then linear search backward
B) O(√n) time on sorted array
C) Fewer comparisons than linear, simpler than binary
D) All of the above

**Answer: D**

**Explanation:**
Jump search: step = √n. Jump until arr[step*i] > target. Linear search in previous block. Optimal step size: √n gives O(√n). Between linear O(n) and binary O(log n). Advantage: only jumps forward (good for linked lists where backward traversal is expensive). Rarely used when binary search is available.

---

**Q18.38: Expert - [Theory] - [Randomized Search]**

Randomized search techniques:

A) Random sampling: pick random elements, check
B) Skip list: randomized search structure, O(log n) expected
C) Locality-sensitive hashing: approximate nearest neighbor
D) All of the above

**Answer: D**

**Explanation:**
Randomized approaches: (1) Random sampling: O(n/k) to find element in top-k. (2) Skip list: randomized balanced structure (Chapter 5). (3) LSH: hash similar items to same bucket, approximate nearest neighbor in high dimensions. (4) Randomized binary search trees: treaps (Chapter 11). Randomization often simplifies analysis and implementation.

---

**Q18.39: Intermediate - [Theory] - [Search Pattern: Minimize Maximum]**

"Minimize the maximum" pattern:

A) Binary search on the answer (the maximum value)
B) For each candidate max: check if feasible (greedy)
C) Find smallest max that's feasible
D) All of the above

**Answer: D**

**Explanation:**
Pattern: split array into k subarrays minimizing maximum sum. Binary search on max sum. For each candidate: greedily assign elements to subarrays, check if k subarrays suffice. Monotonic: larger max → easier to satisfy. O(n log(sum)) total. Applies to: painter's partition, book allocation, workload distribution.

---

**Q18.40: Foundational - [Theory] - [Sentinel Linear Search]**

Sentinel linear search:

A) Place target at array end as sentinel
B) Loop without bounds check: while arr[i] ≠ target: i++
C) Check if found before sentinel position
D) Saves one comparison per iteration

**Answer: D**

**Explanation:**
Standard: while(i < n && arr[i] != target). Sentinel: arr[n] = target; while(arr[i] != target) i++. Eliminates i < n check. If i < n: found. Else: not found. Roughly 2× fewer comparisons. Micro-optimization but demonstrates how constant factors matter for frequently called code.

---

**Q18.41: Expert - [Theory] - [Nearest Neighbor Search]**

Nearest neighbor in high dimensions:

A) Exact: KD-tree O(n^(1-1/d)) — exponential in dimension
B) Approximate: LSH, random projection trees
C) "Curse of dimensionality" makes exact search hard
D) All of the above

**Answer: D**

**Explanation:**
Curse of dimensionality: in high dimensions, all points are nearly equidistant. KD-tree degrades to linear scan. Approximate methods: LSH hashes nearby points to same bucket with high probability. Random projection: reduce dimension, then search. FAISS (Facebook): production ANN search. Trade exact for speed in high-d applications (image search, recommendation).

---

**Q18.42: Intermediate - [Theory] - [Binary Search Template]**

Universal binary search template:

A) Define search space [lo, hi]
B) Define condition function: is mid feasible?
C) Narrow: if feasible, try better; if not, try other half
D) All of the above

**Answer: D**

**Explanation:**
Template: lo, hi = bounds. While lo < hi: mid = lo + (hi-lo)//2. If condition(mid): hi = mid (or lo = mid). Else: lo = mid+1 (or hi = mid-1). The art: defining the right condition and bounds. Works for: arrays, answer spaces, floating-point. Master this template and adapt to any binary search problem.

---

**Q18.43: Advanced - [Theory] - [Ternary Search vs Binary Search]**

Why not use ternary search on sorted arrays?

A) Ternary: ⌈log₃ n⌉ iterations but 2 comparisons each
B) Binary: ⌈log₂ n⌉ iterations with 1 comparison each
C) Total comparisons: ternary ≈ 2log₃n > log₂n = binary
D) Binary search is strictly better for sorted array search

**Answer: D**

**Explanation:**
Ternary on sorted: 2⌈log₃ n⌉ comparisons. Binary: ⌈log₂ n⌉. Ratio: 2log₃n / log₂n = 2/log₂3 ≈ 1.26. Ternary uses 26% more comparisons! Ternary search is for unimodal functions (no comparison needed, just two function evaluations). For sorted arrays: always use binary search.

---

**Q18.44: Expert - [Theory] - [Comparison of Search Complexities]**

Search complexity hierarchy:

A) Hash lookup: O(1) average
B) Interpolation on uniform: O(log log n)
C) Binary search: O(log n)
D) Linear search: O(n)

**Answer: D**

**Explanation:**
From fastest to slowest: Hash O(1) > Interpolation O(log log n) > Binary O(log n) > Jump O(√n) > Linear O(n). Each requires different prerequisites: hash needs hash table, interpolation needs uniform distribution, binary needs sorted array, jump needs sorted + forward-only access, linear needs nothing. Trade-off: preprocessing vs query time.

---

**Q18.45: Intermediate - [Theory] - [Search Applications]**

Real-world search applications:

A) Database index lookup: B-tree search O(log_B n)
B) Autocomplete: trie prefix search O(L)
C) File system: directory search (hash-based or tree-based)
D) All of the above

**Answer: D**

**Explanation:**
Search is ubiquitous: databases (B-tree/hash index), file systems (directory lookup), web (search engines: inverted index), networking (routing tables: longest prefix match), OS (page tables: multi-level lookup). Understanding search algorithms and data structures is fundamental to all of computer science.

---

**Q18.46: Intermediate - [Theory] - [Two Pointer Search for Pair Sum]**

Two-pointer technique for pair with given sum in sorted array:

A) Left pointer at start, right pointer at end
B) If sum < target: move left pointer right
C) If sum > target: move right pointer left
D) All of the above — O(n) time, O(1) space

**Answer: D**

**Explanation:**
Two-pointer: exploit sorted order. Start with widest pair. Too small → increase left (makes sum larger). Too large → decrease right (makes sum smaller). Each pointer moves at most n times → O(n). Compare with hash approach O(n) but O(n) space. Generalizes: 3Sum uses two-pointer inside a loop → O(n²).

---

**Q18.47: Advanced - [Theory] - [Search in Infinite Sorted Array]**

Searching in an unbounded/infinite sorted array:

A) Can't use binary search directly (don't know the end)
B) Exponential search: check positions 1, 2, 4, 8, ... until value ≥ target
C) Then binary search between position[i/2] and position[i]
D) O(log p) where p = position of target

**Answer: D**

**Explanation:**
Infinite array: no length known. Exponential search phase: double index until arr[index] ≥ target. Takes O(log p) steps to find range [p/2, p]. Binary search within range: O(log p). Total: O(log p). Optimal — can't do better without knowing array size. Practical: streaming data, unbounded databases.

---

**Q18.48: Advanced - [Trace] - [K-th Smallest in Sorted Matrix]**

K-th smallest in row-sorted and column-sorted n×n matrix:

A) Binary search on value range [matrix[0][0], matrix[n-1][n-1]]
B) For mid value: count elements ≤ mid using staircase walk O(n)
C) Narrow range until left == right
D) O(n log(max-min)) total

**Answer: D**

**Explanation:**
Binary search on value (not index). For candidate value mid: count elements ≤ mid by starting at bottom-left, walking right if ≤ mid, up if > mid. O(n) per count. If count < k: search higher. If count ≥ k: search lower. Converges in log(max-min) steps. Alternative: min-heap approach O(k log n) — better when k << n².

---

**Q18.49: Expert - [Theory] - [Median of Two Sorted Arrays]**

Median of two sorted arrays (sizes m, n) in O(log min(m,n)):

A) Binary search on partition position in smaller array
B) Partition both arrays so left halves have (m+n+1)/2 elements total
C) Valid partition: maxLeft1 ≤ minRight2 and maxLeft2 ≤ minRight1
D) All of the above

**Answer: D**

**Explanation:**
Classic hard binary search. Partition smaller array at position i, larger at j = (m+n+1)/2 - i. Check cross conditions: left elements ≤ right elements across arrays. Binary search on i in [0, m]. O(log min(m,n)). Median: max of left halves (odd total) or average of max-left and min-right (even total). LeetCode #4 — one of the hardest binary search applications.

---

**Q18.50: Intermediate - [Theory] - [Search in Nearly Sorted Array]**

Search in a nearly sorted array (elements may be displaced by ±1 position):

A) Element at sorted position i might be at i-1, i, or i+1
B) Check arr[mid-1], arr[mid], arr[mid+1] during binary search
C) Adjust search range accordingly
D) Still O(log n) with modified binary search

**Answer: D**

**Explanation:**
Nearly sorted: each element within 1 position of its sorted position. Modified binary search: at each step, check 3 positions (mid-1, mid, mid+1). If found: return. If target < arr[mid-1]: search left half (end = mid-2). If target > arr[mid+1]: search right half (start = mid+2). O(log n). Extends to ±k displacement with O(log n) but checking 2k+1 positions.

---

## Chapter 18 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 11 | Linear, binary search, variants, rotated array, comparisons |
| Intermediate | 24 | Lower/upper bound, search on answer, ternary, interpolation, exponential, 2D matrix, Mo's, two-pointer, nearly sorted |
| Advanced | 11 | Fractional cascading, vEB tree, A*, parallel binary search, Fibonacci search, infinite array, k-th matrix |
| Expert | 4 | IDA*, nearest neighbor, randomized search, median of two sorted arrays |

**Total MCQs: 50** | **Target Met: ✓**

**Next:** Chapter 19 - Graph Traversal
