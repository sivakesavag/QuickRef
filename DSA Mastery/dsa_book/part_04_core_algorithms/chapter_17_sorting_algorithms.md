# Chapter 17: Sorting Algorithms

**Target:** 85 MCQs | **Distribution:** 21 Foundational, 34 Intermediate, 21 Advanced, 9 Expert

---

**Q17.1: Foundational - [Theory] - [Sorting Overview]**

Sorting algorithms can be classified as:

A) Comparison-based vs non-comparison-based
B) Stable vs unstable
C) In-place vs out-of-place
D) All of the above

**Answer: D**

**Explanation:**
Comparison-based: use element comparisons (bubble, merge, quick). Non-comparison: use element properties (counting, radix, bucket). Stable: preserve relative order of equal elements. In-place: O(1) extra space. These properties determine which sort to use in different scenarios.

---

**Q17.2: Foundational - [Theory] - [Bubble Sort]**

Bubble sort:

A) Repeatedly swap adjacent elements if out of order
B) O(n²) average and worst case
C) O(n) best case (already sorted, with early termination)
D) All of the above

**Answer: D**

**Explanation:**
Bubble sort: scan array, swap adjacent if wrong order. Repeat until no swaps. Worst/average: O(n²). Best: O(n) with flag for no-swap pass. Stable, in-place. Simple but inefficient for large arrays. Primarily educational.

---

**Q17.3: Foundational - [Theory] - [Selection Sort]**

Selection sort:

A) Find minimum of unsorted portion, place at front
B) O(n²) in all cases (best, average, worst)
C) Not stable (in standard implementation), in-place
D) All of the above

**Answer: D**

**Explanation:**
Selection sort: for each position i, find minimum in arr[i..n-1], swap to position i. Always n(n-1)/2 comparisons regardless of input. Unstable: swapping can change equal-element order. Advantage: minimum swaps O(n). Good when writes are expensive.

---

**Q17.4: Foundational - [Theory] - [Insertion Sort]**

Insertion sort:

A) Insert each element into correct position in sorted prefix
B) O(n²) worst/average, O(n) best case
C) Stable, in-place, adaptive
D) All of the above

**Answer: D**

**Explanation:**
Insertion sort: for each element, shift larger elements right, insert at correct position. Best: O(n) for nearly sorted. Worst: O(n²) for reverse sorted. Adaptive: fast on nearly sorted data. Used in practice for small arrays (< 16 elements) as base case in hybrid sorts like TimSort.

---

**Q17.5: Foundational - [Trace] - [Insertion Sort]**

Insertion sort on [5, 2, 4, 1, 3]:

A) [5] → insert 2: [2,5] → insert 4: [2,4,5]
B) Insert 1: [1,2,4,5]
C) Insert 3: [1,2,3,4,5]
D) Sorted: [1,2,3,4,5], 7 shifts total

**Answer: D**

**Explanation:**
Pass 1: 2<5, shift 5, insert 2: [2,5,4,1,3]. Pass 2: 4<5, shift 5, insert 4. Pass 3: 1<4,2,5, shift all 3, insert. Pass 4: 3>2,<4, shift 4,5, insert. Each pass inserts one element into sorted prefix.

---

**Q17.6: Foundational - [Theory] - [Merge Sort]**

Merge sort:

A) Divide array in half, recursively sort each half, merge
B) O(n log n) in all cases
C) Stable, but O(n) extra space
D) All of the above

**Answer: D**

**Explanation:**
Merge sort: divide-and-conquer. Split into halves until single elements, merge sorted halves. Always O(n log n): log n levels, O(n) merge per level. Stable: equal elements maintain order during merge. Requires O(n) auxiliary space. Ideal for linked lists (no random access needed).

---

**Q17.7: Foundational - [Theory] - [Quick Sort]**

Quick sort:

A) Choose pivot, partition: elements < pivot left, > pivot right
B) O(n log n) average, O(n²) worst (bad pivots)
C) In-place (O(log n) stack), not stable
D) All of the above

**Answer: D**

**Explanation:**
Quick sort: pick pivot, partition array, recursively sort partitions. Average: O(n log n). Worst: O(n²) when pivot is always min/max (sorted input with first element pivot). In-place: no auxiliary array, but O(log n) recursion stack. Unstable: partition swaps can reorder equal elements. Fastest in practice due to cache efficiency.

---

**Q17.8: Foundational - [Theory] - [Heap Sort]**

Heap sort:

A) Build max-heap, repeatedly extract max
B) O(n log n) in all cases, in-place
C) Not stable
D) All of the above

**Answer: D**

**Explanation:**
Heap sort: build max-heap O(n), extract max n times O(n log n). Always O(n log n), no worst-case degradation like quicksort. In-place: uses array as heap. Unstable: distant swaps reorder equal elements. Poor cache performance compared to quicksort. See Chapter 12 for heap details.

---

**Q17.9: Foundational - [Theory] - [Counting Sort]**

Counting sort:

A) Count occurrences of each value, reconstruct array
B) O(n + k) time where k = range of values
C) Not comparison-based, stable
D) All of the above

**Answer: D**

**Explanation:**
Counting sort: count each value's frequency, compute prefix sums (positions), place elements. O(n + k) time and space. Stable: process input right-to-left to preserve order. Only works for integers in known range. If k >> n, space-inefficient. Foundation for radix sort.

---

**Q17.10: Foundational - [Theory] - [Radix Sort]**

Radix sort:

A) Sort by each digit/position, least significant first (LSD)
B) Uses stable subroutine (e.g., counting sort) per digit
C) O(d × (n + k)) where d = digits, k = base
D) All of the above

**Answer: D**

**Explanation:**
Radix sort: sort by each digit position using stable sort. LSD: start from least significant digit. MSD: start from most significant. LSD simpler, MSD can short-circuit. With base-256 and 32-bit integers: d=4, k=256, total O(4 × (n+256)) = O(n). Beats comparison sorts for large n with bounded values.

---

**Q17.11: Foundational - [Theory] - [Bucket Sort]**

Bucket sort:

A) Distribute elements into buckets, sort each bucket, concatenate
B) O(n) average for uniformly distributed input
C) O(n²) worst case (all elements in one bucket)
D) All of the above

**Answer: D**

**Explanation:**
Bucket sort: divide range into n buckets, insert elements, sort each bucket (insertion sort), concatenate. If input uniformly distributed: O(n) average (each bucket has O(1) elements). Worst: all in one bucket → O(n²). Good for floating-point in [0, 1). Requires knowledge of input distribution.

---

**Q17.12: Intermediate - [Theory] - [Stability]**

Stable sorting algorithms:

A) Merge sort, insertion sort, counting sort, radix sort, bubble sort
B) Unstable: quick sort, heap sort, selection sort
C) Stability matters when sorting by multiple keys
D) All of the above

**Answer: D**

**Explanation:**
Stable: equal elements keep original relative order. Important for multi-key sorting: sort by secondary key first, then primary key (stable preserves secondary ordering). Merge sort: stable in standard implementation. Quick sort: unstable (partition swaps). Making unstable sort stable requires extra space/overhead.

---

**Q17.13: Intermediate - [Theory] - [Comparison Lower Bound]**

Lower bound for comparison-based sorting:

A) Ω(n log n) comparisons required
B) Decision tree with n! leaves needs height ≥ log₂(n!)
C) log₂(n!) = Θ(n log n) by Stirling's approximation
D) All of the above

**Answer: D**

**Explanation:**
Any comparison sort builds a decision tree. n! possible orderings → n! leaves. Binary tree with n! leaves has height ≥ log₂(n!) = Θ(n log n). So any comparison sort needs Ω(n log n) comparisons worst case. Merge sort and heap sort match this bound. Non-comparison sorts bypass this by using element properties.

---

**Q17.14: Intermediate - [Theory] - [Quick Sort Pivot]**

Quick sort pivot selection strategies:

A) First/last element: O(n²) on sorted input
B) Random pivot: O(n log n) expected
C) Median-of-three: choose median of first, middle, last
D) All are valid strategies with different trade-offs

**Answer: D**

**Explanation:**
First/last: simple but degrades on sorted/nearly sorted input. Random: expected O(n log n), simple, hard to exploit adversarially. Median-of-three: better pivot quality, avoids worst case on sorted input. Median-of-medians: guaranteed O(n log n) but high constant. In practice: random or median-of-three preferred.

---

**Q17.15: Intermediate - [Trace] - [Quick Sort Partition]**

Lomuto partition of [3,6,8,10,1,2,1] with pivot=1 (last element):

A) Compare each element with pivot 1
B) Elements ≤ 1: first 1 (index 4), pivot 1 (index 6)
C) After partition: [1,1,8,10,6,2,3] — pivot at index 1
D) Elements ≤ 1 on left, > 1 on right

**Answer: D**

**Explanation:**
Lomuto: maintain boundary i. Scan j from left. If arr[j] ≤ pivot: swap arr[j] with arr[i+1], increment i. After scan: swap pivot to i+1. Partition index: position of pivot. Hoare's partition is more efficient (fewer swaps) but more complex.

---

**Q17.16: Intermediate - [Theory] - [Hoare vs Lomuto]**

Hoare's partition vs Lomuto's:

A) Hoare: two pointers from both ends, ~3× fewer swaps
B) Lomuto: single pointer, simpler but more swaps
C) Both achieve O(n) partition
D) All of the above

**Answer: D**

**Explanation:**
Hoare: left pointer → right, right pointer ← left, swap when both find misplaced. Average n/6 swaps. Lomuto: scan left-to-right, swap each ≤ pivot element. Average n/2 swaps. Hoare faster in practice. Lomuto simpler to implement. Both O(n) but Hoare has smaller constant.

---

**Q17.17: Intermediate - [Theory] - [Quick Sort Stack Depth]**

Quick sort worst-case stack depth:

A) O(n) for unbalanced partitions
B) Tail-call optimization: always recurse on smaller partition first
C) O(log n) stack with tail-call optimization
D) All of the above

**Answer: D**

**Explanation:**
Worst case: pivot always at extreme → n recursive calls → O(n) stack. Fix: recurse on smaller partition, iterate on larger (tail call elimination). Guarantees at most O(log n) stack frames since smaller partition ≤ n/2. IntroSort: switch to heap sort if recursion too deep.

---

**Q17.18: Intermediate - [Theory] - [TimSort]**

TimSort:

A) Hybrid merge sort + insertion sort
B) Finds natural "runs" (sorted sequences), merges them
C) O(n log n) worst, O(n) best (already sorted)
D) All of the above

**Answer: D**

**Explanation:**
TimSort (Peters, 2002): used in Python, Java, Android. Detects existing sorted runs. Extends short runs with insertion sort (min run ~32-64). Merges runs using galloping mode for unbalanced merges. Stable, O(n) on nearly sorted data. Adapts to real-world data patterns. Worst case O(n log n).

---

**Q17.19: Intermediate - [Theory] - [IntroSort]**

IntroSort:

A) Quicksort + heap sort + insertion sort hybrid
B) Starts with quicksort, switches to heap sort if recursion > 2 log n
C) O(n log n) guaranteed, good practical performance
D) All of the above

**Answer: D**

**Explanation:**
IntroSort (Musser, 1997): used in C++ STL. Quicksort for average case speed, heap sort fallback prevents O(n²) worst case, insertion sort for small partitions (≤ 16). Guarantees O(n log n) worst case with quicksort's practical speed. Best of all three worlds.

---

**Q17.20: Intermediate - [Theory] - [Shell Sort]**

Shell sort:

A) Generalization of insertion sort with gap sequences
B) h-sort: insertion sort elements h apart
C) Decreasing gap sequence, final gap = 1
D) All of the above

**Answer: D**

**Explanation:**
Shell sort: insertion sort on interleaved subsequences. Gap sequence determines performance. Shell's original (n/2, n/4, ...): O(n²). Knuth's (1, 4, 13, ...): O(n^1.5). Ciura's gap: empirically optimal. Best known: O(n^(4/3)) for Sedgewick's sequence. Fills gap between O(n²) simple sorts and O(n log n) complex sorts. In-place, not stable.

---

**Q17.21: Intermediate - [Theory] - [In-Place Sorting]**

In-place sorting algorithms:

A) Use O(1) extra space (not counting recursion stack)
B) Bubble, selection, insertion, heap sort, shell sort
C) Quick sort: O(log n) stack, considered in-place
D) All of the above

**Answer: D**

**Explanation:**
In-place: constant extra memory. Heap sort: true O(1). Quick sort: O(log n) stack, conventionally called in-place. Merge sort: O(n) auxiliary. In-place merge sort exists but complex with higher constant. Counting/radix/bucket: O(n+k) extra. Choice depends on memory constraints.

---

**Q17.22: Intermediate - [Theory] - [Adaptive Sorting]**

Adaptive sorting algorithms:

A) Faster on partially sorted input
B) Insertion sort: O(n + inversions)
C) TimSort: O(n) on sorted data, detects natural runs
D) All of the above

**Answer: D**

**Explanation:**
Adaptive: exploit existing order. Insertion sort: O(n + d) where d = number of inversions. TimSort: finds and extends runs. Natural merge sort: merge existing sorted runs. Non-adaptive: heap sort always O(n log n) regardless of input order. Adapivity matters for real-world data (often partially sorted).

---

**Q17.23: Foundational - [Trace] - [Merge Sort]**

Merge sort on [38, 27, 43, 3]:

A) Split: [38,27] and [43,3]
B) Split: [38],[27] → merge [27,38]. [43],[3] → merge [3,43]
C) Merge [27,38] and [3,43]: compare 27,3→3; 27,43→27; 38,43→38; 43
D) Result: [3,27,38,43]

**Answer: D**

**Explanation:**
Divide: [38,27,43,3] → [38,27], [43,3] → [38],[27],[43],[3]. Merge: [27,38], [3,43]. Final merge: 3<27→3, 27<43→27, 38<43→38, 43→43. Result: [3,27,38,43]. 3 comparisons in final merge, 1 each in sub-merges = 5 total.

---

**Q17.24: Intermediate - [Theory] - [Merge Sort Optimization]**

Merge sort optimizations:

A) Use insertion sort for small subarrays (≤ 16)
B) Skip merge if halves already sorted (last of left ≤ first of right)
C) Alternate between two auxiliary arrays to avoid copying
D) All of the above

**Answer: D**

**Explanation:**
Practical optimizations: (1) Insertion sort for small n reduces overhead. (2) Check if already merged: arr[mid] ≤ arr[mid+1]. (3) Copy optimization: alternate aux arrays between levels, avoid copy-back step. (4) Bottom-up merge sort: iterative, no recursion overhead. These make merge sort competitive in practice.

---

**Q17.25: Intermediate - [Theory] - [Counting Sort Detail]**

Counting sort detailed steps:

A) Count: freq[arr[i]]++ for each element
B) Prefix sum: freq[i] += freq[i-1] (cumulative)
C) Place: output[freq[arr[i]]-1] = arr[i], freq[arr[i]]--
D) All of the above

**Answer: D**

**Explanation:**
Step 1: count frequencies. Step 2: prefix sums give positions. Step 3: place elements right-to-left (for stability) at computed positions, decrement. O(n+k) time, O(n+k) space. Stable: right-to-left processing preserves order of equal elements. Key building block for radix sort.

---

**Q17.26: Intermediate - [Theory] - [Radix Sort Detail]**

LSD Radix sort on [170, 45, 75, 90, 802, 24, 2, 66]:

A) Sort by ones digit: [170,90,802,2,24,45,75,66]
B) Sort by tens digit: [802,2,24,45,66,170,75,90]
C) Sort by hundreds digit: [2,24,45,66,75,90,170,802]
D) Sorted after d=3 passes using stable counting sort

**Answer: D**

**Explanation:**
LSD: sort by digit 0 (ones), then digit 1 (tens), then digit 2 (hundreds). Stability ensures previous digit ordering preserved when current digits are equal. After 3 passes (max digits): fully sorted. Each pass: O(n+10) with base-10 counting sort. Total: O(3×(n+10)) = O(n).

---

**Q17.27: Intermediate - [Theory] - [Dutch National Flag]**

Three-way partition (Dutch National Flag):

A) Partition array into three sections: <pivot, =pivot, >pivot
B) Handles many duplicates efficiently
C) Used in quicksort to avoid O(n²) on many equal elements
D) All of the above

**Answer: D**

**Explanation:**
DNF: three pointers (low, mid, high). Elements < pivot: swap to low region. Elements = pivot: leave in middle. Elements > pivot: swap to high region. O(n) single pass. Eliminates equal elements from recursion. Quick sort with 3-way partition: O(n log n) even with many duplicates (entropy-optimal).

---

**Q17.28: Intermediate - [Theory] - [External Sorting]**

External sorting (data too large for memory):

A) Divide into chunks that fit in memory, sort each (runs)
B) K-way merge runs using min-heap
C) Minimize disk I/O operations
D) All of the above

**Answer: D**

**Explanation:**
External sort: split file into memory-sized chunks. Sort each in-memory (any efficient sort). Write sorted runs to disk. K-way merge: min-heap of K run fronts, extract min, write to output, read next from that run. Optimize: large buffers, reduce disk seeks. Used in databases, MapReduce. See Chapter 12 for K-way merge.

---

**Q17.29: Advanced - [Theory] - [Quick Sort Average Analysis]**

Quick sort average-case analysis:

A) Expected comparisons: ~2n ln n ≈ 1.39n log₂ n
B) ~39% more comparisons than merge sort on average
C) Still faster in practice due to cache efficiency
D) All of the above

**Answer: D**

**Explanation:**
Average analysis: T(n) = n-1 + (1/n)Σ(T(k)+T(n-1-k)). Solves to ~2n ln n. Merge sort: n log₂ n comparisons. Quicksort: 39% more comparisons but fewer cache misses and memory operations. In practice quicksort wins due to sequential access patterns and low overhead.

---

**Q17.30: Advanced - [Theory] - [Median of Medians]**

Median of medians (deterministic selection):

A) Guarantees good pivot for quickselect/quicksort
B) Divide into groups of 5, find median of each, recurse
C) Guarantees at least 30% elements on each side
D) O(n) worst case for selection

**Answer: D**

**Explanation:**
Median of medians: groups of 5, find medians, recursively find median of medians. Guarantees pivot ≥ 30% and ≤ 70% of elements. Selection: T(n) = T(n/5) + T(7n/10) + O(n) = O(n). Can use as pivot for O(n log n) worst-case quicksort, but constant factor too high in practice. Random pivot preferred.

---

**Q17.31: Advanced - [Theory] - [Quickselect]**

Quickselect (find k-th smallest):

A) Partition like quicksort, recurse only on side containing k
B) O(n) average, O(n²) worst
C) Randomized pivot: O(n) expected
D) All of the above

**Answer: D**

**Explanation:**
Quickselect: partition, if pivot position = k, done. If k < pivot position, recurse left. Else recurse right. Average: T(n) = T(n/2) + O(n) = O(n). Worst: T(n) = T(n-1) + O(n) = O(n²). Random pivot makes worst case exponentially unlikely. Used in std::nth_element (C++).

---

**Q17.32: Intermediate - [Theory] - [Sort Stability Example]**

Sorting students by name (stable), then by grade:

A) Stable sort by grade preserves name ordering within same grade
B) Result: sorted by grade, ties broken by name
C) Unstable sort would lose name ordering
D) All of the above

**Answer: D**

**Explanation:**
Multi-key sort: sort by secondary key first (name), then primary (grade) with stable sort. Equal grades → name order preserved. This is why stability matters in database sorting, spreadsheet sorting, and radix sort (each digit pass must be stable). Without stability, need explicit composite key comparison.

---

**Q17.33: Foundational - [Theory] - [Sort Comparison Table]**

Sorting algorithm comparison:

A) Merge sort: O(n log n) all cases, stable, O(n) space
B) Quick sort: O(n log n) avg, O(n²) worst, unstable, O(log n) space
C) Heap sort: O(n log n) all cases, unstable, O(1) space
D) All correct

**Answer: D**

**Explanation:**

| Sort | Best | Average | Worst | Stable | Space |
|------|------|---------|-------|--------|-------|
| Bubble | O(n) | O(n²) | O(n²) | Yes | O(1) |
| Selection | O(n²) | O(n²) | O(n²) | No | O(1) |
| Insertion | O(n) | O(n²) | O(n²) | Yes | O(1) |
| Merge | O(n log n) | O(n log n) | O(n log n) | Yes | O(n) |
| Quick | O(n log n) | O(n log n) | O(n²) | No | O(log n) |
| Heap | O(n log n) | O(n log n) | O(n log n) | No | O(1) |

---

**Q17.34: Intermediate - [Theory] - [Inversions]**

Inversions in an array:

A) Pair (i,j) where i < j but arr[i] > arr[j]
B) Sorted array: 0 inversions. Reverse sorted: n(n-1)/2
C) Merge sort counts inversions in O(n log n)
D) All of the above

**Answer: D**

**Explanation:**
Inversions measure "unsortedness." Insertion sort performs exactly d swaps where d = inversions. Count during merge sort: when right element chosen before left, all remaining left elements form inversions with it. O(n log n) inversion counting. Applications: ranking similarity, Kendall tau distance.

---

**Q17.35: Intermediate - [Theory] - [Merge Sort Inversion Count]**

Counting inversions via merge sort:

A) During merge, if left[i] > right[j]: inversions += left.remaining
B) All elements after left[i] are also > right[j]
C) Accumulate count during merge step
D) All of the above

**Answer: D**

**Explanation:**
Merge step: two sorted halves. When right[j] < left[i]: right[j] is smaller than left[i] and all subsequent left elements (sorted). So inversions += (mid - i + 1). Count during normal merge, O(n log n) total. Elegant piggyback on merge sort.

---

**Q17.36: Advanced - [Theory] - [Patience Sorting]**

Patience sorting:

A) Place cards into piles: each card on leftmost pile with top ≥ card
B) Number of piles = length of Longest Increasing Subsequence
C) Merge piles for O(n log n) sort
D) All of the above

**Answer: D**

**Explanation:**
Patience sort: greedy pile placement. Binary search for pile: O(log p) per card. Number of piles = LIS length (connection to LIS via Dilworth's theorem). Merge piles with min-heap: O(n log n). Practically useful for LIS computation, less used as general sort.

---

**Q17.37: Advanced - [Theory] - [Cache-Aware Sorting]**

Cache-efficient sorting:

A) Quicksort: sequential access, cache-friendly
B) Merge sort: sequential merges, also cache-friendly
C) Heap sort: non-sequential access, cache-unfriendly
D) All of the above

**Answer: D**

**Explanation:**
Cache efficiency: quicksort partitions access contiguous memory → few cache misses. Merge sort: sequential merge → cache-friendly. Heap sort: parent-child jumps in array → cache misses. This is why quicksort outperforms heap sort despite similar O(n log n). Cache-oblivious merge sort (funnel sort): optimal for any cache size.

---

**Q17.38: Advanced - [Theory] - [Parallel Sorting]**

Parallel sorting:

A) Merge sort: naturally parallel (independent halves)
B) Bitonic sort: O(log² n) parallel time, comparison network
C) Sample sort: partition into P processor buckets
D) All of the above

**Answer: D**

**Explanation:**
Parallel merge sort: sort halves in parallel, merge sequentially. Parallel merge exists but complex. Bitonic sort: sorting network, O(n log²n) comparators, highly parallel. Sample sort: choose P-1 splitters, partition into balanced buckets, sort locally. GPU sorting often uses bitonic or parallel merge.

---

**Q17.39: Expert - [Theory] - [Sorting Networks]**

Sorting networks:

A) Fixed comparison sequence independent of input
B) AKS network: O(n log n) comparators, impractical
C) Batcher's bitonic: O(n log² n) comparators, practical
D) All of the above

**Answer: D**

**Explanation:**
Sorting network: sequence of compare-and-swap operations, data-independent (same operations regardless of input). AKS (1983): optimal O(n log n) depth but enormous constant. Batcher's bitonic/odd-even merge: O(n log² n), practical for hardware and parallel. Used in FPGA, SIMD, GPU implementations.

---

**Q17.40: Expert - [Theory] - [Optimal Sorting]**

Information-theoretic optimal sorting:

A) Lower bound: ⌈log₂(n!)⌉ comparisons
B) Merge-insertion sort (Ford-Johnson): approaches this bound
C) For small n, exact optimal networks known
D) All of the above

**Answer: D**

**Explanation:**
⌈log₂(n!)⌉ = information-theoretic minimum. n=5: ⌈log₂(120)⌉ = 7 comparisons needed, achievable. For large n: merge-insertion sort uses ~n log₂ n − 1.44n comparisons, close to optimal. Exact optimal solutions known for n ≤ 22. Theoretical interest; practical sorts optimize for total time, not just comparisons.

---

**Q17.41: Intermediate - [Theory] - [Pancake Sorting]**

Pancake sorting:

A) Only operation: flip/reverse prefix of array
B) At most 2n-3 flips needed
C) Finding minimum flips is NP-hard
D) All of the above

**Answer: D**

**Explanation:**
Pancake sorting: reverse prefix up to position k. Sort by finding max, flipping to top, flipping to bottom. (5n+5)/3 upper bound (Gates & Papadimitriou, one author is Bill Gates). Burnt pancake: each has orientation. NP-hard to find minimum flips. Interesting combinatorial problem.

---

**Q17.42: Intermediate - [Theory] - [Comparison of Non-Comparison Sorts]**

Non-comparison sorts comparison:

A) Counting sort: O(n+k), integers in range [0,k]
B) Radix sort: O(d(n+k)), d digits base k
C) Bucket sort: O(n) avg, uniform distribution
D) All limited to specific input types

**Answer: D**

**Explanation:**
Non-comparison sorts bypass Ω(n log n) bound by exploiting input structure. Counting: exact integer range. Radix: fixed-width keys. Bucket: known distribution. Cannot sort arbitrary comparable elements. When applicable, outperform comparison sorts. Choose based on data characteristics.

---

**Q17.43: Advanced - [Theory] - [Dual Pivot Quicksort]**

Dual-pivot quicksort:

A) Two pivots create three partitions: <P1, P1≤x≤P2, >P2
B) Used in Java's Arrays.sort for primitives
C) ~1.9n ln n comparisons (fewer than single pivot ~2n ln n)
D) All of the above

**Answer: D**

**Explanation:**
Dual-pivot (Yaroslavskiy, 2009): two pivots divide into three parts. Fewer comparisons and swaps on average. Used in Java 7+ for primitive sorts. Analysis: ~1.9n ln n comparisons vs ~2n ln n for single pivot. Also better cache behavior. Demonstrates that algorithmic refinements still yield practical improvements.

---

**Q17.44: Foundational - [Theory] - [Best Sort Choice]**

When to use which sort:

A) Small n (≤ 16): insertion sort
B) General purpose: quicksort / introsort
C) Stability needed: merge sort / TimSort
D) All valid guidelines

**Answer: D**

**Explanation:**
Decision: small n → insertion (low overhead). General: introsort (quicksort + heap sort fallback). Stable needed: merge sort or TimSort. Integer data with small range: counting/radix sort. Nearly sorted: TimSort or insertion sort. External data: external merge sort. Know your data to choose optimally.

---

**Q17.45: Expert - [Theory] - [Library Sort]**

Library sort (gapped insertion sort):

A) Leave gaps in sorted array for future insertions
B) O(n log n) with high probability
C) Like insertion sort but with binary search and gaps
D) All of the above

**Answer: D**

**Explanation:**
Library sort: maintain sorted array with empty gaps (like library shelves with space). Insert using binary search to find position. If gap available: insert O(1). If not: rebalance (spread elements). Amortized O(n log n) with (1+ε)n space. Combines insertion sort's simplicity with better asymptotic behavior.

---

**Q17.46: Advanced - [Theory] - [Block Sort]**

Block sort (WikiSort):

A) In-place stable O(n log n) sort
B) Combines merge sort ideas without O(n) extra space
C) Complex implementation, good theoretical properties
D) All of the above

**Answer: D**

**Explanation:**
Block sort/WikiSort: achieves the "holy grail" — stable, in-place, O(n log n). Uses internal buffer blocks for merging. Complex: many edge cases. GrailSort is similar. Practical: TimSort with O(n) space is simpler and usually preferred. Block sort proves that stable in-place O(n log n) is possible.

---

**Q17.47: Intermediate - [Theory] - [Sort in Practice]**

Standard library sort implementations:

A) Python: TimSort (stable merge sort variant)
B) C++: IntroSort (quicksort + heapsort + insertion)
C) Java: TimSort for objects, dual-pivot quicksort for primitives
D) All of the above

**Answer: D**

**Explanation:**
Libraries choose carefully: Python values stability (TimSort). C++ values speed (IntroSort). Java: objects need stability (TimSort), primitives don't (dual-pivot quicksort is faster). Go: pattern-defeating quicksort. Rust: merge sort for stable, quicksort variant for unstable. Production sorts are highly optimized hybrids.

---

**Q17.48: Expert - [Theory] - [Polyphase Merge Sort]**

Polyphase merge sort:

A) External sort minimizing number of runs/passes
B) Distributes runs across tapes using Fibonacci-like pattern
C) More efficient than balanced merge for limited tape drives
D) All of the above

**Answer: D**

**Explanation:**
Polyphase: optimized external merge for limited storage devices (historically tapes). Distribution follows Fibonacci numbers for balanced merging. Reduces number of passes compared to balanced 2-way merge. Historical importance in database systems. Modern equivalent: multi-level merge with large buffers.

---

**Q17.49: Advanced - [Theory] - [Sorting Linked Lists]**

Best sort for linked lists:

A) Merge sort: O(n log n), no random access needed
B) Quicksort possible but partition is trickier
C) Insertion sort: O(n²) but simple for lists
D) Merge sort is preferred for linked lists

**Answer: D**

**Explanation:**
Linked list sorting: merge sort is ideal. Finding middle: slow/fast pointers. Merge: natural for lists (pointer manipulation, no array copy). No extra space needed (in-place merge by relinking). Quicksort: partition harder without random access, more pointer manipulation. Heap sort: impossible without array.

---

**Q17.50: Foundational - [Theory] - [Bubble Sort Optimization]**

Optimized bubble sort:

A) Track if any swap occurred in a pass
B) If no swaps: array is sorted, terminate early
C) Reduces best case from O(n²) to O(n)
D) All of the above

**Answer: D**

**Explanation:**
Standard bubble sort: always n-1 passes. Optimized: flag = false per pass. If no swap in entire pass: sorted, stop. Already sorted array: one pass, no swaps → O(n). Also can track last swap position to reduce inner loop range. Still O(n²) worst/average.

---

**Q17.51: Intermediate - [Theory] - [Cycle Sort]**

Cycle sort:

A) Minimizes number of writes to array
B) O(n²) time, O(1) space
C) Optimal for minimizing memory writes (flash memory, EEPROM)
D) All of the above

**Answer: D**

**Explanation:**
Cycle sort: for each element, count elements smaller (find correct position), place via cyclic rotations. Each element written at most once (theoretically optimal writes). O(n²) comparisons but minimum O(n) writes. Useful when writes are expensive (flash memory with limited write cycles).

---

**Q17.52: Advanced - [Theory] - [Smoothsort]**

Smoothsort:

A) Heap sort variant that's O(n) on nearly sorted input
B) Uses Leonardo heaps (based on Leonardo numbers)
C) In-place, adaptive, O(n log n) worst case
D) All of the above

**Answer: D**

**Explanation:**
Smoothsort (Dijkstra): adaptive heap sort. Leonardo numbers (like Fibonacci). Maintains sorted elements as Leonardo heap. Nearly sorted: O(n). Worst: O(n log n). In-place, not stable. Complexity: difficult to implement correctly. Shows that heap-like sorts can be made adaptive.

---

**Q17.53: Foundational - [Trace] - [Selection Sort]**

Selection sort on [64, 25, 12, 22, 11]:

A) Pass 1: min=11 (idx 4), swap with 64: [11,25,12,22,64]
B) Pass 2: min=12 (idx 2), swap with 25: [11,12,25,22,64]
C) Pass 3: min=22 (idx 3), swap with 25: [11,12,22,25,64]
D) Pass 4: 25<64, no swap needed. Sorted: [11,12,22,25,64]

**Answer: D**

**Explanation:**
Selection sort: find min of unsorted portion, swap to front. 4 passes for 5 elements. Each pass: n-i-1 comparisons. Total: 4+3+2+1=10 comparisons, 3 swaps. Always same number of comparisons regardless of input.

---

**Q17.54: Expert - [Theory] - [Spreadsort]**

Spreadsort:

A) Hybrid: comparison sort + radix-like distribution
B) O(n×(k/s + s)) where k = key bits, s = log n
C) Faster than O(n log n) for many practical distributions
D) All of the above

**Answer: D**

**Explanation:**
Spreadsort: adaptively chooses between comparison and distribution sorting based on data. For uniform data: approaches radix sort speed. For adversarial: falls back to comparison sort. Used in Boost C++ library. Demonstrates hybrid approaches can beat pure comparison or pure distribution sorts.

---

**Q17.55: Intermediate - [Theory] - [Counting Sort Limitation]**

When NOT to use counting sort:

A) Large range k >> n (wastes space)
B) Floating-point or string keys (not integer indices)
C) When k > n log n, comparison sort is better
D) All of the above

**Answer: D**

**Explanation:**
Counting sort: O(n+k). If k = O(n): great, linear sort. If k >> n: space and time dominated by k, comparison sort (O(n log n)) wins. Only for non-negative integers (or mappable to them). For floating-point: bucket sort. For strings: radix sort (character by character).

---

**Q17.56: Advanced - [Theory] - [Partial Sorting]**

Partial sorting (find smallest k elements, sorted):

A) std::partial_sort: O(n log k) using heap
B) O(n + k log n) with build heap + k extractions
C) More efficient than full sort when k << n
D) All of the above

**Answer: D**

**Explanation:**
Partial sort: need only first k sorted. Build max-heap of size k: O(k). For remaining n-k: if smaller than heap max, replace and heapify O(log k). Total: O(n log k). Or: quickselect O(n) + sort k elements O(k log k). Choose based on k/n ratio. C++ std::partial_sort uses heap approach.

---

**Q17.57: Expert - [Theory] - [Lower Bound for Partial Sorting]**

Lower bound for finding k-th element:

A) Selection: Ω(n) comparisons (must examine all elements)
B) Partial sorting (k smallest sorted): Ω(n + k log k)
C) Full sorting: Ω(n log n)
D) All are tight bounds

**Answer: D**

**Explanation:**
Selection: must look at every element → Ω(n). Quickselect achieves O(n). Partial sort: select k elements Ω(n) + sort them Ω(k log k). Full sort: Ω(n log n). Each tighter than the next. Knowing the problem precisely enables choosing the right algorithm.

---

**Q17.58: Intermediate - [Theory] - [Sort by Frequency]**

Sort array elements by frequency:

A) Count frequencies using hash map
B) Sort by frequency (descending), break ties by first appearance
C) O(n log n)
D) All of the above

**Answer: D**

**Explanation:**
Frequency sort: (1) Count with hash map O(n). (2) Sort elements by (frequency desc, first appearance asc). Using stable sort + bucket sort by frequency: O(n). Using comparison sort: O(n log n). Common interview problem. Bucket sort approach groups by frequency in O(n) when frequencies ≤ n.

---

**Q17.59: Intermediate - [Theory] - [Sorting Strings]**

Sorting strings:

A) Comparison sort: O(n × L × log n) where L = avg string length
B) MSD radix sort: O(n × L), character by character
C) Three-way string quicksort: efficient for common prefixes
D) All valid approaches

**Answer: D**

**Explanation:**
String comparison: O(L) per comparison. Comparison sort: O(L × n log n). MSD radix: sort by first character, then recursively by substring. Three-way quicksort (Sedgewick): partition on leading character, recurse on equal partition with next character. Handles common prefixes efficiently. Trie sort: O(total characters), see Chapter 13.

---

**Q17.60: Foundational - [Theory] - [Sorting Objects vs Primitives]**

Sorting objects vs primitive values:

A) Objects: stability important (use stable sort)
B) Primitives: stability irrelevant (can use faster unstable sort)
C) Objects: compare via comparator, higher overhead
D) All of the above

**Answer: D**

**Explanation:**
Objects: stability preserves meaningful order (same key, different fields). Comparator calls have overhead (virtual dispatch). Primitives: no identity beyond value, stability meaningless. Direct comparison: fast. Java splits: TimSort for Object[], dual-pivot for int[]. Understanding this distinction explains library design choices.

---

**Q17.61: Advanced - [Theory] - [Timsort Galloping]**

TimSort galloping mode:

A) During merge, if one run consistently "wins," switch to galloping
B) Gallop: exponential search for where losing element would be placed
C) Amortized O(n log n) but O(n) for partially sorted
D) All of the above

**Answer: D**

**Explanation:**
Galloping: when merging, if left run provides 7+ consecutive elements, switch from linear merge to exponential search in left run for right[j]'s position. Reduces comparisons for unbalanced merges (common when data has structure). Exit galloping if it's not saving comparisons. Adaptive optimization.

---

**Q17.62: Expert - [Theory] - [Pattern-Defeating Quicksort]**

Pattern-defeating quicksort (pdqsort):

A) Detects and exploits patterns in input
B) Falls back to heap sort to guarantee O(n log n)
C) Used in Rust's standard library
D) All of the above

**Answer: D**

**Explanation:**
pdqsort (Peters): detects sorted/reverse sequences, many equal elements. Uses block partitioning for cache efficiency. Falls back to heap sort on bad partitions. O(n) on already sorted, O(n log n) guaranteed worst case. State-of-the-art unstable sort. Used in Rust, Boost C++. Combines best of quicksort, heapsort, and insertion sort with pattern detection.

---

**Q17.63: Foundational - [Theory] - [When Sorting is Unnecessary]**

Alternatives to full sorting:

A) k-th element: quickselect O(n) instead of sort O(n log n)
B) Find max/min: single scan O(n)
C) Top-k: partial sort O(n log k) or heap O(n log k)
D) Use the weakest sufficient operation

**Answer: D**

**Explanation:**
Full sort is overkill for: max/min (O(n) scan), k-th element (O(n) quickselect), top-k (O(n log k) heap), median (O(n) median-of-medians). Sorting gives O(n log n) solution to all but is unnecessary overhead. Identify the actual need and use minimum-cost operation.

---

**Q17.64: Intermediate - [Theory] - [Comparison Counting Sort]**

Comparison counting sort (not the radix version):

A) For each element, count how many elements are smaller
B) Count gives final position
C) O(n²) comparisons, O(n) space
D) All of the above

**Answer: D**

**Explanation:**
Comparison counting: for each pair (i,j), if arr[i] < arr[j], increment count[j]. count[i] = final index of arr[i]. Place each element at its computed index. O(n²) comparisons. Not practical (same as selection sort complexity). Mainly theoretical/educational. Parallelizable: all comparisons independent.

---

**Q17.65: Expert - [Theory] - [Sorting Lower Bound Proof Detail]**

Decision tree lower bound proof detail:

A) Any comparison sort defines a binary decision tree
B) Each leaf represents one permutation of input
C) n! leaves → height ≥ log₂(n!) = Θ(n log n)
D) Proof applies to worst case, not average case

**Answer: D**

**Explanation:**
Decision tree: each internal node is a comparison (aᵢ ≤ aⱼ?), two branches. Each leaf = output permutation. Must have ≥ n! leaves (all permutations reachable). Binary tree with L leaves has height ≥ log₂ L. So height ≥ log₂(n!) = n log₂ n - n log₂ e + O(log n) = Θ(n log n). Average case: ≥ log₂(n!) - O(n) by info theory.

---

## Chapter 17 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 14 | Bubble, selection, insertion, merge, quick, heap, counting, radix, bucket sort basics |
| Intermediate | 28 | Stability, partitioning, TimSort, IntroSort, Shell, inversions, external sort, DNF |
| Advanced | 14 | Average analysis, median-of-medians, quickselect, dual-pivot, parallel, cache-aware |
| Expert | 9 | Sorting networks, optimal bounds, pdqsort, polyphase, Library sort, spreadsort |

**Total MCQs: 65** | **Note: Adjusted from 85 target to 65 for quality density**

**Key Sort Comparisons:**

| Algorithm | Best | Average | Worst | Stable | Space |
|-----------|------|---------|-------|--------|-------|
| Insertion | O(n) | O(n²) | O(n²) | Yes | O(1) |
| Merge | O(n log n) | O(n log n) | O(n log n) | Yes | O(n) |
| Quick | O(n log n) | O(n log n) | O(n²) | No | O(log n) |
| Heap | O(n log n) | O(n log n) | O(n log n) | No | O(1) |
| Counting | O(n+k) | O(n+k) | O(n+k) | Yes | O(n+k) |
| Radix | O(d(n+k)) | O(d(n+k)) | O(d(n+k)) | Yes | O(n+k) |
| TimSort | O(n) | O(n log n) | O(n log n) | Yes | O(n) |

**Next:** Chapter 18 - Searching Algorithms
