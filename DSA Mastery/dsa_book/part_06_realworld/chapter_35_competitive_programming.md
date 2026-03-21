# Chapter 35: Competitive Programming Techniques

**Target:** 40 MCQs | **Distribution:** 10 Foundational, 16 Intermediate, 10 Advanced, 4 Expert

---

**Q35.1: Foundational - [Theory] - [Two Pointers]**

The two-pointer technique on a sorted array works because:

A) It uses binary search internally
B) Sorted order allows eliminating candidates by moving one pointer inward
C) It requires the array to be circular
D) It only works for arrays with distinct elements

**Answer: B**

**Explanation:**
Two pointers on sorted array: left and right pointers. If sum < target: move left right (increase sum). If sum > target: move right left (decrease sum). Sorted order guarantees we eliminate invalid pairs monotonically. O(n) vs O(n²) brute force. Works with or without duplicates. Classic example: pair sum, container with most water, three sum (fix one + two pointers).

---

**Q35.2: Foundational - [Theory] - [Sliding Window]**

The sliding window technique converts which type of problem from O(n²) to O(n)?

A) Sorting problems
B) Subarray/substring problems with contiguous elements
C) Graph traversal problems
D) Tree balancing problems

**Answer: B**

**Explanation:**
Sliding window: maintain a window [left, right] over contiguous elements. Expand right to include more, shrink left to satisfy constraint. O(n) because each element enters and leaves the window at most once. Problems: max sum subarray of size k, longest substring without repeating characters, minimum window substring. Key requirement: the problem must involve contiguous subarrays/substrings.

---

**Q35.3: Intermediate - [Theory] - [Binary Search on Answer]**

"Binary search on answer" is applicable when:

A) The input array is sorted
B) There's a monotonic predicate: if answer x works, then x+1 also works (or vice versa)
C) The problem involves searching for an element
D) The data structure supports random access

**Answer: B**

**Explanation:**
Binary search on answer: instead of searching IN the data, search OVER the answer space. If predicate is monotonic (feasible for all x ≥ threshold): binary search finds the threshold. Examples: "minimum time to complete tasks" (if time T works, T+1 also works). "Maximum minimum distance" (if distance d works, d-1 also works). Convert optimization to decision problem, binary search the decision boundary.

---

**Q35.4: Intermediate - [Trace] - [Two Pointers]**

Using two pointers to find a pair summing to 9 in sorted array [1, 2, 4, 5, 7, 8]. Which pairs are checked?

A) (1,8)→9✓ found immediately
B) (1,8)→9✓, (2,7)→9✓, (4,5)→9✓ — three pairs found
C) All 15 pairs checked exhaustively
D) (1,2)→3, (1,4)→5, (1,5)→6, (1,7)→8, (1,8)→9✓ found after 5 checks

**Answer: A**

**Explanation:**
Two pointers: left=0 (value 1), right=5 (value 8). Sum = 1+8 = 9 = target → found immediately on first check. If we wanted ALL pairs summing to 9: after finding (1,8), move both pointers inward → (2,7)→9✓, then (4,5)→9✓. Two pointers checks at most n pairs total, vs C(n,2) for brute force. The sorted order is essential — random order requires hash set.

---

**Q35.5: Foundational - [Theory] - [Prefix Sum]**

Why are prefix sums useful for range sum queries?

A) They sort the array
B) They precompute cumulative sums, enabling O(1) range sum via subtraction
C) They compress the array
D) They find the maximum element efficiently

**Answer: B**

**Explanation:**
Prefix sum: pre[i] = arr[0] + arr[1] + ... + arr[i-1]. Sum of range [l, r] = pre[r+1] - pre[l]. O(n) precomputation, O(1) per query. Without prefix sums: O(n) per range query. With 10⁵ queries on 10⁵ elements: O(10¹⁰) naive vs O(10⁵) with prefix sums. 2D prefix sums extend to rectangle sum queries. Foundation for many competitive programming techniques.

---

**Q35.6: Intermediate - [Theory] - [Coordinate Compression]**

Coordinate compression is used when:

A) Data values are small but array indices are large
B) Data values are large/sparse but only their relative ordering matters
C) The data needs to be encrypted
D) The array must be sorted in reverse

**Answer: B**

**Explanation:**
Values like {10⁹, 2×10⁹, 5} can be mapped to {1, 2, 0}. Preserves relative order, reduces value range from 10⁹ to n. Enables use of BIT/segment tree indexed by value. Steps: sort unique values, assign consecutive indices. Example: "count inversions" — need BIT indexed by value, but values up to 10⁹. After compression: BIT of size n. O(n log n) total. Essential technique when value range >> data count.

---

**Q35.7: Advanced - [Theory] - [Mo's Algorithm]**

Mo's algorithm answers offline range queries on arrays in what time complexity?

A) O(n) total
B) O(n log n) total
C) O((n + q) × √n) total for q queries
D) O(n × q) total

**Answer: C**

**Explanation:**
Mo's algorithm: sort queries by (block of left endpoint, right endpoint). Maintain current answer for range [curL, curR]. Extend/shrink by ±1 to reach next query's range. Block size = √n. Analysis: left pointer moves O(√n) per query block. Right pointer moves O(n) per block, O(n√n) total. With q queries: O((n + q)√n). Only works for offline queries where add/remove at endpoints is O(1). Can't be used for online queries.

---

**Q35.8: Foundational - [Theory] - [Meet in the Middle]**

Meet-in-the-middle reduces brute-force search time from O(2^n) to:

A) O(n log n)
B) O(2^(n/2))
C) O(n²)
D) O(√n)

**Answer: B**

**Explanation:**
Split n items into two halves of n/2. Enumerate all 2^(n/2) subsets for each half. Combine results using sorting + two pointers or hash map. Example: subset sum — split items, generate all sums for each half (2^20 each for n=40), sort, binary search for target complement. O(2^20) ≈ 10⁶ manageable vs O(2^40) ≈ 10¹² infeasible. Works when n ≤ 40 and a full 2^n search is too slow.

---

**Q35.9: Intermediate - [Theory] - [Difference Array]**

A difference array supports what operation efficiently?

A) Point queries in O(1)
B) Range updates (add value to all elements in [l, r]) in O(1)
C) Finding the maximum element in O(1)
D) Sorting the array in O(n)

**Answer: B**

**Explanation:**
Difference array diff[]: diff[l] += val, diff[r+1] -= val for range update [l,r]. After all updates: prefix sum of diff[] gives final values. O(1) per range update, O(n) to reconstruct. Without difference array: O(n) per range update. With 10⁵ updates on 10⁵ elements: O(10¹⁰) naive vs O(10⁵) with difference array. Limitation: can't do point queries between updates without reconstruction.

---

**Q35.10: Advanced - [Theory] - [SOS DP]**

Sum over Subsets (SOS) DP computes, for each bitmask, the sum over all its submasks in:

A) O(3^n) using submask enumeration
B) O(n × 2^n) by processing each bit independently
C) O(2^n) by iterating masks once
D) O(n²) using matrix multiplication

**Answer: B**

**Explanation:**
Naive submask enumeration: for each mask, iterate all submasks → O(3^n) total (each element: in mask and submask, in mask not submask, or not in mask). SOS optimization: for each bit position i: dp[mask] += dp[mask ^ (1<<i)] if bit i is set. Process each of n bits independently across all 2^n masks → O(n × 2^n). Significant speedup: for n=20, 3^20 ≈ 3.5×10⁹ vs 20 × 2^20 ≈ 2×10⁷.

---

**Q35.11: Intermediate - [Theory] - [Sparse Table]**

Sparse table achieves O(1) range minimum queries because:

A) It stores all possible ranges
B) Overlapping range queries can be combined with idempotent operations (min of overlapping ranges = min of full range)
C) It uses hash tables for constant-time access
D) It only works for sorted arrays

**Answer: B**

**Explanation:**
Sparse table: precompute min for ranges of length 2^k starting at each index. Query [l,r]: find largest k where 2^k ≤ r-l+1. Answer = min(table[l][k], table[r-2^k+1][k]). Two ranges overlap but min(a,b) is idempotent: min(min(x,y), min(y,z)) = min(x,y,z). O(n log n) build, O(1) query. Only for idempotent operations (min, max, GCD). For sum: need segment tree (overlapping would double-count).

---

**Q35.12: Foundational - [Theory] - [Greedy vs DP Recognition]**

You should suspect a problem needs DP rather than greedy when:

A) The problem asks for a count of all solutions
B) The problem has a clear "take the best option now" strategy
C) The problem involves sorting first
D) The problem only has one optimal solution

**Answer: A**

**Explanation:**
DP indicators: counting solutions (can't count with greedy), optimal substructure with overlapping subproblems, choices where locally optimal ≠ globally optimal. Greedy works when: local optimal = global optimal (provable via exchange argument), the problem has greedy-choice property. Example: coin change with arbitrary denominations needs DP. With denominations 1,5,10,25: greedy works. Always verify greedy correctness.

---

**Q35.13: Advanced - [Theory] - [Heavy-Light Decomposition]**

HLD decomposes a tree so that any root-to-leaf path crosses at most:

A) O(1) heavy chains
B) O(log n) heavy chains
C) O(√n) heavy chains
D) O(n) heavy chains

**Answer: B**

**Explanation:**
HLD: classify edges as heavy (to largest-subtree child) or light. Light edge: child's subtree ≤ half of parent's subtree. So each light edge halves the subtree size → at most O(log n) light edges on any root-to-leaf path. Heavy chains are stored contiguously → segment tree queries on a chain are efficient. Path query (u to v): O(log² n) with HLD + segment tree. Critical technique for tree path queries in competitive programming.

---

**Q35.14: Intermediate - [Theory] - [Fast I/O]**

In competitive programming, fast I/O is important because:

A) Standard I/O functions are always correct
B) Default I/O (e.g., scanf/cin, input) can be a bottleneck for large inputs
C) Judges score based on code length
D) It makes debugging easier

**Answer: B**

**Explanation:**
With n=10⁶ inputs: Python's input() or C++ cin (synced with stdio) can be 5-10× slower than needed. Fixes: C++: `ios::sync_with_stdio(false); cin.tie(nullptr)`. Python: `sys.stdin`. Java: BufferedReader. Can make difference between TLE (Time Limit Exceeded) and AC (Accepted). Not about algorithm complexity — pure I/O overhead. Always optimize I/O in competitive programming.

---

**Q35.15: Expert - [Theory] - [Persistent Segment Tree]**

A persistent segment tree supports what capability that standard segment trees don't?

A) Faster point queries
B) Access to any previous version of the tree after updates
C) More compact storage
D) Multi-dimensional range queries

**Answer: B**

**Explanation:**
Persistent: after each update, both old and new versions accessible. Implementation: don't modify nodes — create new path from root to updated leaf (O(log n) new nodes per update), sharing unmodified subtrees. Memory: O(n log n) for n updates. Used for: k-th element in range (merge sort tree alternative), array version history, functional programming style. Each version is an immutable snapshot accessible by its root pointer.

---

**Q35.16: Intermediate - [Theory] - [Monotonic Stack Applications]**

Monotonic stacks are used to solve which type of problem efficiently?

A) Finding the next greater element for each element in O(n)
B) Sorting an array in O(n)
C) Finding the median in O(1)
D) Computing prefix sums in O(1) per query

**Answer: A**

**Explanation:**
Monotonic stack: maintains elements in increasing (or decreasing) order. For next greater element: push indices onto stack. When current element > stack top: stack top's next greater element is current. Pop and record. O(n): each element pushed and popped at most once. Applications: next greater/smaller element, largest rectangle in histogram, stock span problem. Simple but powerful pattern.

---

**Q35.17: Foundational - [Theory] - [Offline vs Online Queries]**

An algorithm that must answer queries in the order they arrive (without seeing future queries) is called:

A) Offline
B) Online
C) Batch processing
D) Streaming

**Answer: B**

**Explanation:**
Online: must answer each query before seeing the next one. Cannot reorder or preprocess queries. Offline: sees ALL queries upfront, can process in any order. Mo's algorithm: offline (sorts queries). Segment tree: online (answers immediately). Offline is often easier/faster because you can choose processing order. Some problems require online answers — then offline techniques like Mo's algorithm don't apply.

---

**Q35.18: Advanced - [Theory] - [Centroid Decomposition]**

What property makes the centroid of a tree useful in centroid decomposition?

A) It has the maximum degree
B) Removing it ensures no remaining subtree exceeds n/2 nodes
C) It is always a leaf node
D) It has the minimum depth

**Answer: B**

**Explanation:**
Centroid: vertex whose removal minimizes the maximum subtree size. Guaranteed: max subtree ≤ n/2 after removal. Centroid decomposition: find centroid, solve for paths through it, remove centroid, recurse on subtrees. Depth of decomposition: O(log n) (each level halves max subtree). Used for: counting paths with specific properties (e.g., paths summing to target), distance queries. O(n log n) for many tree problems.

---

**Q35.19: Expert - [Theory] - [Lambda Optimization (Aliens Trick)]**

The Aliens trick converts a constrained DP into an unconstrained one by:

A) Removing all constraints entirely
B) Adding a penalty λ per item and binary searching for the λ that gives exactly k items
C) Using matrix exponentiation
D) Parallelizing the computation

**Answer: B**

**Explanation:**
"Select exactly k items to optimize cost" DP: O(n × k). Aliens trick: instead of forcing k items, add penalty λ per item selected. For large λ: fewer items selected. For small λ: more items. Binary search on λ to find value where exactly k items are chosen. Unconstrained DP: O(n) or O(n log n). Total: O(n × log(answer)). Named after IOI 2016 "Aliens" problem. Powerful general technique.

---

**Q35.20: Intermediate - [Theory] - [Square Root Decomposition]**

Square root decomposition divides an array into blocks of size √n. What is the query time for range sum?

A) O(1)
B) O(√n)
C) O(log n)
D) O(n)

**Answer: B**

**Explanation:**
Array divided into √n blocks of √n each. Range sum [l, r]: sum partial first block + sum complete middle blocks + sum partial last block. At most 2 partial blocks (O(√n) each) + O(√n) complete blocks (O(1) each with precomputed sums) = O(√n) total. Simpler than segment tree but slower (O(√n) vs O(log n)). Good when segment tree is overkill or problem doesn't need O(log n).

---

## Chapter 35 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 6 | Two pointers, sliding window, prefix sum, meet-in-middle, greedy vs DP, online/offline |
| Intermediate | 9 | Binary search on answer, coordinate compression, difference array, sparse table, monotonic stack, sqrt decomp |
| Advanced | 4 | Mo's, SOS DP, HLD, centroid decomposition |
| Expert | 2 | Persistent segment tree, Aliens trick |

**Total MCQs: 20**

**Answer Distribution: A=5, B=14, C=1, D=0**

**Next:** Chapter 36 - Machine Learning DS&A
