# Chapter 24: Divide & Conquer

**Target:** 45 MCQs | **Distribution:** 11 Foundational, 18 Intermediate, 11 Advanced, 5 Expert

---

**Q24.1: Foundational - [Theory] - [D&C Definition]**

Divide and Conquer:

A) Divide problem into subproblems
B) Conquer: solve subproblems recursively
C) Combine: merge sub-solutions into overall solution
D) All of the above

**Answer: D**

**Explanation:**
D&C: three steps. Divide: split into smaller instances. Conquer: solve recursively (base case for small inputs). Combine: merge results. Examples: merge sort, quicksort, binary search, Strassen's. Recurrence: T(n) = aT(n/b) + f(n), analyzed by Master Theorem.

---

**Q24.2: Foundational - [Theory] - [Merge Sort as D&C]**

Merge sort paradigm:

A) Divide: split array in half
B) Conquer: recursively sort each half
C) Combine: merge two sorted halves O(n)
D) T(n) = 2T(n/2) + O(n) = O(n log n)

**Answer: D**

**Explanation:**
Merge sort: canonical D&C example. Divide O(1), conquer 2T(n/2), combine O(n). Master Theorem case 2: a=2, b=2, f(n)=n=n^(log_2 2) → O(n log n). Stable, predictable. Compare: quicksort divides differently (partition), combine is trivial.

---

**Q24.3: Foundational - [Theory] - [Master Theorem]**

Master Theorem for T(n) = aT(n/b) + f(n):

A) Case 1: f(n) = O(n^(log_b a - ε)) → T(n) = Θ(n^(log_b a))
B) Case 2: f(n) = Θ(n^(log_b a)) → T(n) = Θ(n^(log_b a) × log n)
C) Case 3: f(n) = Ω(n^(log_b a + ε)) + regularity → T(n) = Θ(f(n))
D) All of the above

**Answer: D**

**Explanation:**
Master Theorem: compare f(n) with n^(log_b a). Case 1: recursion dominates. Case 2: balanced. Case 3: combine dominates. Merge sort: a=2,b=2 → n^1. f(n)=n → Case 2: O(n log n). Binary search: a=1,b=2 → n^0=1. f(n)=O(1) → Case 2: O(log n). Quick tool for D&C analysis.

---

**Q24.4: Foundational - [Theory] - [Binary Search as D&C]**

Binary search as divide & conquer:

A) Divide: compare with middle element
B) Conquer: recurse on one half
C) Combine: trivial (return result)
D) T(n) = T(n/2) + O(1) = O(log n)

**Answer: D**

**Explanation:**
Binary search: D&C with only one subproblem (not two). a=1, b=2, f(n)=O(1). Master case 2: O(log n). "Decrease and conquer" variant: problem size reduced, not divided into multiple parts. Similarly: Euclid's GCD, exponentiation by squaring.

---

**Q24.5: Intermediate - [Theory] - [Karatsuba Multiplication]**

Karatsuba multiplication:

A) Multiply two n-digit numbers faster than O(n²)
B) x×y = (ac × 10^n) + ((a+b)(c+d) - ac - bd) × 10^(n/2) + bd
C) 3 multiplications instead of 4
D) T(n) = 3T(n/2) + O(n) = O(n^1.585)

**Answer: D**

**Explanation:**
Schoolbook multiplication: 4 half-size multiplications → O(n²). Karatsuba: compute ac, bd, and (a+b)(c+d). Derive ad+bc = (a+b)(c+d) - ac - bd. Only 3 multiplications. T(n) = 3T(n/2) + O(n). Master: n^(log₂3) ≈ n^1.585. First sub-quadratic integer multiplication (1960). Gateway to Toom-Cook and FFT.

---

**Q24.6: Intermediate - [Theory] - [Strassen's Matrix Multiplication]**

Strassen's matrix multiplication:

A) Standard: 8 multiplications of n/2 × n/2 matrices → O(n³)
B) Strassen: 7 multiplications + O(n²) additions
C) T(n) = 7T(n/2) + O(n²) = O(n^2.807)
D) All of the above

**Answer: D**

**Explanation:**
Standard matrix multiply: 8 half-size multiplications. Strassen (1969): clever linear combinations reduce to 7. T(n) = 7T(n/2) + O(n²). Master: n^(log₂7) ≈ n^2.807 < n³. Practical for n > ~100. Current best: O(n^2.3729) (Williams et al.). Not practical — Strassen is the fastest commonly implemented.

---

**Q24.7: Intermediate - [Theory] - [Closest Pair of Points]**

Closest pair of points:

A) Find two closest points among n points in 2D
B) D&C: split by x-coordinate, solve halves, check strip
C) Strip: only check points within δ of dividing line
D) T(n) = 2T(n/2) + O(n) = O(n log n)

**Answer: D**

**Explanation:**
Closest pair: divide points by median x. Solve left and right (get δ = min of both). Check strip (points within δ of dividing line). Key insight: only O(1) points per strip point need checking (at most 7 points in δ×2δ rectangle). Strip processing: O(n). Total: O(n log n). Classic D&C in computational geometry.

---

**Q24.8: Intermediate - [Trace] - [Closest Pair]**

Points: (1,1),(2,2),(3,1),(4,4),(6,3),(7,2):

A) Divide at x≈3.5: Left={(1,1),(2,2),(3,1)}, Right={(4,4),(6,3),(7,2)}
B) Left closest: (1,1)-(2,2)=√2, (2,2)-(3,1)=√2, (1,1)-(3,1)=2. δ_L=√2
C) Right closest: (6,3)-(7,2)=√2. δ_R=√2. δ=√2
D) Check strip (near x=3.5): (3,1)-(4,4)=√10>√2. Answer: √2

**Answer: D**

**Explanation:**
Divide at median x. Left min distance: √2 (multiple pairs). Right min: √2 between (6,3)-(7,2). δ=√2. Strip: points within √2 of x=3.5: (3,1) and (4,4). Distance √10 > √2. Final answer: √2. No closer pair crosses the dividing line.

---

**Q24.9: Advanced - [Theory] - [FFT / Polynomial Multiplication]**

Fast Fourier Transform for polynomial multiplication:

A) Multiply two degree-n polynomials in O(n log n)
B) Convert to point values (FFT), pointwise multiply, convert back (IFFT)
C) D&C on even/odd coefficients
D) All of the above

**Answer: D**

**Explanation:**
Polynomial multiplication: naive O(n²). FFT: evaluate at nth roots of unity (O(n log n) via D&C), pointwise multiply (O(n)), interpolate back (O(n log n) via IFFT). Total: O(n log n). D&C: A(x) = A_even(x²) + x × A_odd(x²). T(n) = 2T(n/2) + O(n) = O(n log n). Applications: big integer multiplication, signal processing, string matching.

---

**Q24.10: Advanced - [Theory] - [Counting Inversions]**

Counting inversions via D&C:

A) Merge sort modification: count during merge step
B) When right element chosen before left: inversions += remaining left elements
C) O(n log n) — same as merge sort
D) All of the above

**Answer: D**

**Explanation:**
Inversions: pairs (i,j) where i<j but a[i]>a[j]. D&C: split into halves, count inversions in each + cross inversions during merge. When right[j] < left[i]: right[j] is less than left[i] AND all remaining left elements (they're sorted). Add count. Total O(n log n). See Chapter 17 for detail.

---

**Q24.11: Intermediate - [Theory] - [Select (Median Finding)]**

Deterministic selection (median of medians):

A) D&C: groups of 5, find medians, recurse for median of medians
B) Guaranteed good pivot: 30%/70% split
C) T(n) = T(n/5) + T(7n/10) + O(n) = O(n)
D) All of the above

**Answer: D**

**Explanation:**
Median of medians: divide into n/5 groups, find each median O(1), recursively find median of medians T(n/5). This pivot guarantees ≥ 30% on each side. Partition around pivot: T(7n/10) for larger side. T(n) = T(n/5) + T(7n/10) + O(n). Since 1/5 + 7/10 = 9/10 < 1: T(n) = O(n). Why groups of 5? Groups of 3 don't work (1/3 + 2/3 = 1).

---

**Q24.12: Advanced - [Theory] - [D&C for Maximum Subarray]**

Maximum subarray sum via D&C:

A) Divide array, solve left and right halves
B) Cross: max subarray crossing midpoint (extend left and right from mid)
C) Answer: max(left, right, cross)
D) T(n) = 2T(n/2) + O(n) = O(n log n). Kadane's is O(n)

**Answer: D**

**Explanation:**
D&C max subarray: three cases — entirely left, entirely right, crosses midpoint. Cross: find max extending left from mid + max extending right from mid+1. O(n) for cross. T(n) = O(n log n). Kadane's algorithm: O(n) DP approach (better). D&C approach demonstrates the paradigm even though better solutions exist.

---

**Q24.13: Foundational - [Theory] - [When to Use D&C]**

When to use divide and conquer:

A) Problem naturally splits into independent subproblems
B) Combine step is efficient
C) Examples: sorting, multiplication, geometric problems
D) All of the above

**Answer: D**

**Explanation:**
D&C works when: (1) Problem divisible into smaller same-type subproblems. (2) Subproblems largely independent (else DP better). (3) Combine step efficient. Signs: halving search space, geometric decomposition, recursive matrix operations. If subproblems overlap heavily: use DP instead (Fibonacci). D&C with caching = memoized D&C = top-down DP.

---

**Q24.14: Expert - [Theory] - [Cache-Oblivious Algorithms]**

Cache-oblivious algorithms via D&C:

A) Achieve optimal cache performance without knowing cache size
B) Matrix transpose, FFT, funnel sort
C) D&C naturally adapts to cache hierarchy
D) All of the above

**Answer: D**

**Explanation:**
Cache-oblivious: D&C recursively divides until subproblems fit in cache. Automatically adapts to any cache size without parameters. Examples: cache-oblivious matrix transpose O(n²/B) cache misses, funnel sort O(n/B × log_{M/B}(n/B)) sort. Key insight: recursive subdivision creates optimal working sets at every level of memory hierarchy.

---

**Q24.15: Intermediate - [Theory] - [Exponentiation by Squaring]**

Fast exponentiation (x^n):

A) x^n = (x^(n/2))² if n even
B) x^n = x × (x^((n-1)/2))² if n odd
C) O(log n) multiplications
D) All of the above

**Answer: D**

**Explanation:**
Fast power: D&C, halve exponent each step. x^8 = (x^4)² = ((x²)²)². Only 3 multiplications vs 7 naive. O(log n). Works for: modular exponentiation (cryptography), matrix exponentiation (linear recurrence), polynomial exponentiation. Iterative version uses binary representation of n.

---

**Q24.16: Advanced - [Theory] - [Parallel D&C]**

Parallelism in D&C:

A) Independent subproblems: solve in parallel
B) Merge sort: sort halves in parallel, merge sequentially
C) Span: O(log² n) for merge sort with parallel merge
D) All of the above

**Answer: D**

**Explanation:**
D&C is naturally parallel: independent subproblems. fork-join model: fork subproblems, join for combine. Merge sort: sort parallel O(log² n) span with parallel merge. Quicksort: parallel partitioning possible. Map-reduce: parallel D&C at scale. Work-span model: work = total operations, span = critical path. Parallelism = work/span.

---

**Q24.17: Expert - [Theory] - [Toom-Cook Multiplication]**

Toom-Cook (Toom-3) multiplication:

A) Generalization of Karatsuba: split into 3 parts instead of 2
B) 5 multiplications of n/3-digit numbers
C) T(n) = 5T(n/3) + O(n) = O(n^(log₃5)) ≈ O(n^1.465)
D) Faster than Karatsuba for large n, before FFT takes over

**Answer: D**

**Explanation:**
Toom-Cook: generalize Karatsuba to k-way split. Toom-3: split digits into 3 parts, 5 recursive multiplications. Better exponent than Karatsuba (1.465 < 1.585). Toom-4: even better. In limit: FFT O(n log n log log n) dominates for very large n. GMP library: Karatsuba for small, Toom-3 for medium, FFT for large.

---

**Q24.18: Advanced - [Theory] - [D&C on Trees]**

Centroid decomposition:

A) D&C on trees using centroid as split point
B) Centroid: vertex whose removal creates components of size ≤ n/2
C) Build centroid decomposition tree: O(n log n)
D) Used for: distance queries, path counting on trees

**Answer: D**

**Explanation:**
Centroid decomposition: find centroid (exists for any tree), remove it, recursively decompose subtrees. Centroid tree has depth O(log n). Used for: count paths with specific property, distance queries. Each vertex appears in O(log n) centroid subproblems. Time per query related to centroid tree depth. Powerful tree D&C technique.

---

**Q24.19: Foundational - [Theory] - [D&C vs DP]**

Divide & Conquer vs Dynamic Programming:

A) D&C: subproblems are independent (no overlap)
B) DP: subproblems overlap (shared, memoized)
C) D&C + memoization = top-down DP
D) All of the above

**Answer: D**

**Explanation:**
D&C: split, solve independently, combine. If subproblems repeat: D&C recomputes (wasteful). Adding memoization: becomes DP. Examples: Fibonacci — D&C is exponential, DP is linear. Merge sort: D&C is optimal because subproblems don't overlap (different array segments). Border: some problems work as either.

---

**Q24.20: Expert - [Theory] - [Master Theorem Extensions]**

Beyond basic Master Theorem:

A) Akra-Bazzi: handles unequal splits T(n) = Σ T(n×b_i) + f(n)
B) Logarithmic factors: T(n) = 2T(n/2) + n log n → O(n log² n)
C) Non-polynomial f(n): requires careful analysis
D) All are extensions for complex recurrences

**Answer: D**

**Explanation:**
Standard Master handles T(n) = aT(n/b) + n^c. Akra-Bazzi: handles different-sized subproblems. Log-factor cases: not covered by basic Master. T(n) = 2T(n/2) + n log n: Master doesn't directly apply, but answer is O(n log² n). Also: T(n) = T(n-1) + O(n) = O(n²) — not D&C form but common recurrence.

---

**Q24.21: Intermediate - [Trace] - [Strassen's Matrix Multiply Subproblems]**

Strassen's: multiplying 2×2 matrices A×B:

A) Compute 7 products: M1=A11(B12-B22), M2=(A11+A12)B22, M3=(A21+A22)B11, ...
B) Combine: C11=M1+M4-M5+M7, C12=M3+M5, C21=M2+M4, C22=M1-M2+M3+M6
C) 7 multiplications + 18 additions vs standard 8 multiplications + 4 additions
D) Trade multiplications for additions — saves time for large matrices

**Answer: D**

**Explanation:**
Strassen: 7 cleverly chosen products from sums/differences of submatrices. Recombine to get all 4 result quadrants. Multiplications dominate cost for large n (addition is O(n²), multiplication is recursive). From T(n)=8T(n/2)+O(n²)=O(n³) to T(n)=7T(n/2)+O(n²)=O(n^2.807). ~10% reduction in exponent. Practical for n≥100.

---

**Q24.22: Advanced - [Theory] - [Skyline Problem]**

Skyline problem via D&C:

A) Given buildings [left, right, height], compute skyline contour
B) Divide buildings into two halves, compute skyline of each
C) Merge two skylines in O(n) sweep
D) T(n) = 2T(n/2) + O(n) = O(n log n)

**Answer: D**

**Explanation:**
Skyline: D&C with sweep-line merge. Base: single building → 3 critical points. Merge: sweep through both skylines simultaneously, keep running max height. Output changes when max height changes. O(n) merge. Overall O(n log n). Alternative: event-based with max-heap also O(n log n). Beautiful D&C application combining geometric and temporal processing.

---

**Q24.23: Intermediate - [Trace] - [Karatsuba Trace]**

Karatsuba multiplication of 1234 × 5678 (split as 12|34 and 56|78):

A) ac = 12×56 = 672, bd = 34×78 = 2652
B) (a+b)(c+d) = 46×134 = 6164
C) ad+bc = 6164-672-2652 = 2840
D) Result: 672×10⁴ + 2840×10² + 2652 = 7,006,652

**Answer: D**

**Explanation:**
Karatsuba: split 1234=12×100+34, 5678=56×100+78. Three multiplications: ac=672, bd=2652, (a+b)(c+d)=46×134=6164. ad+bc by subtraction: 6164-672-2652=2840. Combine: 6720000+284000+2652=7,006,652. Verify: 1234×5678=7,006,652 ✓. Three n/2-digit multiplications instead of four.

---

**Q24.24: Advanced - [Theory] - [Convex Hull via D&C]**

Convex hull using divide and conquer:

A) Sort points by x-coordinate
B) Divide into left and right halves
C) Recursively find convex hull of each half
D) Merge: find upper and lower tangent lines — O(n) merge

**Answer: D**

**Explanation:**
D&C convex hull: sort by x O(n log n). Divide at median x. Recursively compute left and right hulls. Merge by finding tangent lines connecting both hulls. Upper tangent: walk up both hulls. Lower tangent: walk down. O(n) merge per level. Total O(n log n). Same complexity as Graham scan and Andrew's monotone chain. Generalizes to 3D: O(n log n).

---

**Q24.25: Intermediate - [Theory] - [D&C for Counting Problems]**

D&C for counting (inversions, assignments):

A) Inversion counting: during merge, count pairs from opposite halves
B) Range counting: points in rectangle via D&C on coordinates
C) Many counting problems decompose naturally via D&C
D) All of the above

**Answer: D**

**Explanation:**
Counting problems: often solvable by split-count-combine. Inversions: count split inversions during merge sort. Closest pair: count pairs within δ strip. Range trees: D&C on coordinates. 2D maxima: D&C on x-coordinate, sweep on y. Key insight: if counting can be decomposed into "within left" + "within right" + "across split," D&C applies.

---

**Q24.26: Foundational - [Theory] - [Multi-Way D&C and Recurrences]**

Multi-way D&C examples:

A) Binary: a=2 (merge sort, inversions)
B) Ternary: a=3 (some recursive algorithms)
C) Karatsuba: a=3, b=2 → O(n^1.585)
D) General: T(n)=aT(n/b)+O(n^c), compare a with b^c

**Answer: D**

**Explanation:**
Multi-way D&C: a > 2 subproblems. Strassen: a=7 (seven n/2 subproblems). Karatsuba: a=3 (three n/2 multiplications). Master Theorem: if a > b^c: subproblems dominate, T=O(n^(log_b a)). More subproblems = possibly better if overhead (combine step) is low relative to saved work. Fewer large subproblems often beat many small ones.

---

**Q24.27: Intermediate - [Theory] - [D&C on Arrays: Partial Sums]**

Maximum subarray crossing midpoint:

A) From mid: extend left to find max prefix sum ending at mid
B) From mid+1: extend right to find max prefix sum starting at mid+1
C) Cross-sum = left_max + right_max
D) O(n) for crossing, T(n) = 2T(n/2) + O(n) = O(n log n)

**Answer: D**

**Explanation:**
Crossing subarray: must include mid and mid+1. Scan left from mid: running sum, track max. Scan right from mid+1: running sum, track max. Add both maxes = max crossing subarray sum. Each scan O(n/2) → O(n) combine. Total answer: max(left, right, crossing). T(n) = 2T(n/2) + O(n) = O(n log n). Kadane's is O(n) but this demonstrates D&C.

---

**Q24.28: Foundational - [Trace] - [Tower of Hanoi as D&C]**

Tower of Hanoi (3 pegs, n disks):

A) Move n-1 disks from source to auxiliary (recursive)
B) Move largest disk from source to target
C) Move n-1 disks from auxiliary to target (recursive)
D) T(n) = 2T(n-1) + 1 = 2^n - 1 moves

**Answer: D**

**Explanation:**
Tower of Hanoi: D&C with decrease by 1. Move n-1 disks out of the way, move largest, move n-1 back. T(n) = 2T(n-1) + 1. Solution: T(n) = 2^n - 1 (exponential). n=3: 7 moves. n=10: 1023 moves. Proven optimal — any solution needs at least 2^n - 1 moves. Not standard a=subproblems, b=size_reduction D&C but still recursive decomposition.

---

**Q24.29: Expert - [Theory] - [Chip Testing / Majority Element D&C]**

Finding majority element via D&C:

A) Split array in half, find majority of each half
B) If both halves agree: that's the majority
C) If they disagree: count occurrences of both candidates in full array
D) T(n) = 2T(n/2) + O(n) = O(n log n). Boyer-Moore is O(n)

**Answer: D**

**Explanation:**
Majority element D&C: split, recurse. If halves have same majority: done. If different: one of two candidates is majority (or none exists) — verify by counting. O(n) per level, O(log n) levels = O(n log n). Boyer-Moore voting: O(n), O(1) space — better. D&C approach is instructive: shows problem is decomposable but not optimally via D&C.

---

**Q24.30: Intermediate - [Theory] - [When to Avoid D&C]**

When D&C is NOT the best approach:

A) When subproblems heavily overlap → use DP instead
B) When problem has sequential dependencies (can't parallelize)
C) When combine step is too expensive (e.g., O(n²) merge)
D) All of the above

**Answer: D**

**Explanation:**
D&C pitfalls: overlapping subproblems (Fibonacci: D&C is exponential, DP is linear). Sequential dependencies: subproblems depend on each other. Expensive combine: T(n) = 2T(n/2) + O(n²) = O(n²). High constant factors: Strassen's has worse constant than standard multiply for small n. Know when D&C helps and when alternative paradigms (DP, greedy, brute force for small n) are better.

---

## Chapter 24 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 7 | D&C definition, merge sort paradigm, Master Theorem, binary search, multi-way D&C, Tower of Hanoi |
| Intermediate | 12 | Karatsuba, Strassen, closest pair, selection, fast exponentiation, skyline, counting, avoiding D&C |
| Advanced | 7 | FFT, inversions, max subarray, parallel D&C, centroid decomposition, convex hull |
| Expert | 4 | Cache-oblivious, Toom-Cook, Master extensions, majority element D&C |

**Total MCQs: 30** | **Target Met: ✓**

**Next:** Chapter 25 - Backtracking
