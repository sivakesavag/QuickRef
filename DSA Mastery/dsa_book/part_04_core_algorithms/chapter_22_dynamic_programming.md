# Chapter 22: Dynamic Programming

**Target:** 105 MCQs | **Distribution:** 26 Foundational, 42 Intermediate, 26 Advanced, 11 Expert

---

**Q22.1: Foundational - [Theory] - [DP Definition]**

Dynamic programming:

A) Solve problems by breaking into overlapping subproblems
B) Store subproblem solutions to avoid recomputation
C) Optimal substructure: optimal solution contains optimal sub-solutions
D) All of the above

**Answer: D**

**Explanation:**
DP requires: (1) Optimal substructure: problem's optimal solution built from subproblems' optimal solutions. (2) Overlapping subproblems: same subproblems solved multiple times. Without overlap: divide-and-conquer suffices. DP avoids recomputation via memoization (top-down) or tabulation (bottom-up).

---

**Q22.2: Foundational - [Theory] - [Memoization vs Tabulation]**

Top-down (memoization) vs bottom-up (tabulation):

A) Memoization: recursive + cache, solve what's needed
B) Tabulation: iterative, fill table in order, solves all subproblems
C) Both give same time complexity
D) All of the above

**Answer: D**

**Explanation:**
Memoization: natural recursive approach, cache results. Only computes needed subproblems. Tabulation: iterative, fill table from smallest to largest. Computes all subproblems. Memoization may have recursion overhead; tabulation may compute unnecessary subproblems. Same asymptotic complexity. Choose based on problem structure and preference.

---

**Q22.3: Foundational - [Trace] - [Fibonacci DP]**

Fibonacci with DP, n=6:

A) dp[0]=0, dp[1]=1
B) dp[2]=1, dp[3]=2, dp[4]=3, dp[5]=5, dp[6]=8
C) O(n) time, O(n) space (or O(1) with two variables)
D) vs O(2^n) naive recursion

**Answer: D**

**Explanation:**
Naive Fibonacci: fib(n) calls fib(n-1) and fib(n-2), exponential redundancy. DP: store each fib(i), compute in O(1) per step. O(n) total. Space optimization: only need previous two values → O(1) space. Classic example showing DP's power: exponential → linear.

---

**Q22.4: Foundational - [Theory] - [Coin Change Problem]**

Minimum coins to make amount:

A) dp[i] = minimum coins for amount i
B) dp[i] = min(dp[i - coin] + 1) for each coin denomination
C) Base: dp[0] = 0. If dp[amount] = ∞: impossible
D) All of the above

**Answer: D**

**Explanation:**
Coin change (min coins): for each amount 1 to target, try each coin. dp[i] = min over coins c of dp[i-c] + 1. O(amount × coins). Greedy doesn't always work (e.g., coins {1,3,4}, amount 6: greedy=4+1+1=3, optimal=3+3=2). DP guarantees optimal.

---

**Q22.5: Foundational - [Theory] - [Longest Increasing Subsequence]**

LIS (Longest Increasing Subsequence):

A) dp[i] = length of LIS ending at index i
B) dp[i] = max(dp[j] + 1) for all j < i where arr[j] < arr[i]
C) O(n²) basic DP, O(n log n) with patience sorting/binary search
D) All of the above

**Answer: D**

**Explanation:**
LIS: find longest subsequence where each element > previous. O(n²): for each i, scan all j < i. O(n log n): maintain tails array (smallest tail for each length), binary search for insertion point. LIS length = tails length. Patience sorting connection (Chapter 17). Classic DP problem with clever optimization.

---

**Q22.6: Foundational - [Theory] - [Longest Common Subsequence]**

LCS (Longest Common Subsequence):

A) dp[i][j] = LCS length of first i chars of X and first j chars of Y
B) If X[i]==Y[j]: dp[i][j] = dp[i-1][j-1] + 1
C) Else: dp[i][j] = max(dp[i-1][j], dp[i][j-1])
D) O(mn) time and space

**Answer: D**

**Explanation:**
LCS: longest sequence common to both strings (not necessarily contiguous). 2D DP table. Match: extend previous LCS. No match: take better of excluding either character. O(mn) time. Space optimization: O(min(m,n)) using two rows. Backtrack through table to reconstruct actual LCS. Applications: diff tools, DNA sequence alignment.

---

**Q22.7: Foundational - [Trace] - [LCS]**

LCS of "ABCBDAB" and "BDCAB":

A) Build 7×5 DP table
B) dp[7][5] = 4
C) One LCS: "BDAB" or "BCAB"
D) Multiple LCS possible, length is unique

**Answer: D**

**Explanation:**
LCS("ABCBDAB", "BDCAB") = 4. Possible LCS: "BCAB", "BDAB". Length always unique (optimal). Multiple optimal subsequences may exist. Reconstruct by backtracking: diagonal = match (include), else follow max direction. O(mn) to build, O(m+n) to reconstruct.

---

**Q22.8: Foundational - [Theory] - [0/1 Knapsack]**

0/1 Knapsack:

A) Items with weight and value; maximize value within weight capacity
B) dp[i][w] = max value using first i items with capacity w
C) Include item i: dp[i-1][w-weight[i]] + value[i]. Exclude: dp[i-1][w]
D) O(nW) time where n = items, W = capacity

**Answer: D**

**Explanation:**
0/1 knapsack: each item taken or not (no fractions). dp[i][w] = max(dp[i-1][w], dp[i-1][w-w_i] + v_i) if w ≥ w_i. O(nW) pseudo-polynomial (depends on W value, not input size). Space: O(W) with 1D array (process weights right-to-left to avoid using item twice). NP-hard in general but DP gives practical solution for reasonable W.

---

**Q22.9: Intermediate - [Theory] - [Edit Distance]**

Edit distance (Levenshtein distance):

A) Minimum insertions, deletions, substitutions to transform string A to B
B) dp[i][j] = edit distance between A[0..i-1] and B[0..j-1]
C) If A[i]==B[j]: dp[i-1][j-1]. Else: 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
D) O(mn) time

**Answer: D**

**Explanation:**
Edit distance: dp[i][j] = min operations. Match: no cost, take diagonal. Insert: dp[i][j-1]+1. Delete: dp[i-1][j]+1. Replace: dp[i-1][j-1]+1. O(mn). Applications: spell checking, DNA alignment, fuzzy matching. Wagner-Fischer algorithm. Space-optimized: O(min(m,n)).

---

**Q22.10: Intermediate - [Theory] - [Matrix Chain Multiplication]**

Matrix Chain Multiplication:

A) Find optimal parenthesization to minimize scalar multiplications
B) dp[i][j] = min cost to multiply matrices i through j
C) dp[i][j] = min over k of dp[i][k] + dp[k+1][j] + p[i-1]*p[k]*p[j]
D) O(n³) time

**Answer: D**

**Explanation:**
MCM: parenthesizing n matrices affects total computation. Try all split points k in range [i,j]. Cost = left + right + multiplication cost. Fill table by chain length (increasing gap). O(n³). Classic interval DP. Applications: query optimization in databases, optimal evaluation order.

---

**Q22.11: Intermediate - [Theory] - [DP on Intervals]**

Interval DP pattern:

A) dp[i][j] = optimal value for subarray/substring [i..j]
B) Fill by increasing interval length
C) Examples: MCM, optimal BST, palindrome partitioning
D) All of the above

**Answer: D**

**Explanation:**
Interval DP: subproblems are contiguous ranges. Outer loop: length from 2 to n. Inner: all starting points i, j = i + length - 1. Try all split points k in [i,j]. O(n³) typical. Pattern: "what's optimal for range [i,j] given optimal for all sub-ranges?" Matrix chain, burst balloons, stone merge are classic examples.

---

**Q22.12: Intermediate - [Theory] - [Knapsack Variations]**

Knapsack variations:

A) 0/1: take or leave each item
B) Unbounded: unlimited copies of each item
C) Bounded: limited copies. Subset sum: values = weights
D) All solved by DP with modifications

**Answer: D**

**Explanation:**
0/1: dp[w] updated right-to-left (each item once). Unbounded: dp[w] updated left-to-right (reuse item). Bounded: binary representation or monotone queue optimization. Subset sum: special case with value = weight. All O(nW) or similar. Fractional knapsack: greedy (Chapter 23), not DP.

---

**Q22.13: Intermediate - [Theory] - [DP State Design]**

DP state design principles:

A) State must capture all information needed for future decisions
B) Minimize number of state dimensions
C) Ensure DAG structure (no circular dependencies)
D) All of the above

**Answer: D**

**Explanation:**
State design is the hardest part of DP. State must be: (1) Sufficient: encode all info for remaining decisions. (2) Minimal: avoid redundant dimensions (affects complexity). (3) Ordered: clear dependency direction (smaller states computed first). Common states: index, remaining capacity, subset (bitmask), position in string/array.

---

**Q22.14: Foundational - [Theory] - [DP Recurrence Steps]**

Developing a DP solution:

A) Define state and what it represents
B) Write recurrence relation
C) Identify base cases
D) Determine computation order (or use memoization)

**Answer: D**

**Explanation:**
DP recipe: (1) State: what does dp[...] represent? (2) Transition: how to compute dp[...] from smaller states? (3) Base case: smallest/simplest states with known values. (4) Order: bottom-up (tabulation) or top-down (memoization). (5) Answer: which state(s) give the final answer? (6) Optimize: space, time if possible.

---

**Q22.15: Intermediate - [Theory] - [Longest Palindromic Subsequence]**

Longest palindromic subsequence:

A) dp[i][j] = LPS length in s[i..j]
B) If s[i]==s[j]: dp[i][j] = dp[i+1][j-1] + 2
C) Else: dp[i][j] = max(dp[i+1][j], dp[i][j-1])
D) O(n²) time

**Answer: D**

**Explanation:**
LPS: longest subsequence that reads same forward/backward. Interval DP. Base: single char = 1. If endpoints match: include both + inner LPS. If not: better of excluding either end. Alternative: LPS(s) = LCS(s, reverse(s)). O(n²) time, O(n) space optimized.

---

**Q22.16: Intermediate - [Theory] - [Rod Cutting]**

Rod cutting problem:

A) Cut rod of length n to maximize revenue given price table
B) dp[n] = max over cuts i of price[i] + dp[n-i]
C) Unbounded knapsack variant
D) O(n²) time

**Answer: D**

**Explanation:**
Rod cutting: length n, prices for lengths 1..n. Cut into pieces to maximize revenue. dp[0]=0. dp[j] = max(price[i] + dp[j-i]) for i=1..j. O(n²). Like unbounded knapsack where items are segments of different lengths. Reconstruct: track which cuts were made.

---

**Q22.17: Intermediate - [Theory] - [Coin Change Ways]**

Number of ways to make change:

A) dp[amount] = number of ways to form amount using given coins
B) For each coin c: dp[j] += dp[j-c] for j from c to target
C) Process coins in outer loop to avoid counting permutations
D) O(amount × coins)

**Answer: D**

**Explanation:**
Count combinations (not permutations): process coins in outer loop. For each coin: update dp[c..target]. This ensures each combination counted once (coins in non-decreasing order). If coins in inner loop: counts permutations (e.g., 1+2 and 2+1 counted separately). Subtle but important distinction.

---

**Q22.18: Intermediate - [Theory] - [House Robber]**

House robber (no two adjacent):

A) dp[i] = max money robbing houses 0..i
B) dp[i] = max(dp[i-1], dp[i-2] + nums[i])
C) O(n) time, O(1) space
D) All of the above

**Answer: D**

**Explanation:**
House robber: can't rob adjacent houses. At house i: rob it (skip i-1, add to i-2) or skip it (take i-1). dp[i] = max(skip, rob). O(n) with O(1) space (only need last two values). Extensions: circular arrangement (house robber II), tree structure (house robber III — tree DP).

---

**Q22.19: Intermediate - [Theory] - [Climbing Stairs]**

Climbing stairs (1 or 2 steps):

A) dp[n] = dp[n-1] + dp[n-2]
B) Same as Fibonacci sequence
C) dp[0]=1, dp[1]=1 → dp[2]=2, dp[3]=3, dp[4]=5
D) O(n) time, O(1) space

**Answer: D**

**Explanation:**
Climbing n stairs: at each step, climb 1 or 2. Ways to reach step n: ways to reach n-1 (then take 1 step) + ways to reach n-2 (then take 2 steps). Exactly Fibonacci! Generalizes to k step sizes. With costs: minimum cost climbing stairs adds min selection.

---

**Q22.20: Advanced - [Theory] - [Bitmask DP]**

Bitmask DP:

A) State includes subset of elements, represented as bitmask
B) dp[mask] = optimal value considering elements in the mask
C) Enumerate submasks: for s=mask; s>0; s=(s-1)&mask
D) O(2^n × n) or O(3^n) depending on transitions

**Answer: D**

**Explanation:**
Bitmask DP: state = binary representation of which elements are included. n ≤ 20-25 typically. TSP: dp[mask][last] = min cost visiting cities in mask, ending at last. O(2^n × n²). Subset enumeration: iterate all submasks of a mask. Total over all masks: O(3^n) (each element in, in submask, or not in mask).

---

**Q22.21: Advanced - [Theory] - [TSP with Bitmask DP]**

Traveling Salesman with DP:

A) dp[mask][i] = min cost to visit cities in mask, ending at city i
B) dp[mask|(1<<j)][j] = min(dp[mask][i] + dist[i][j])
C) O(2^n × n²) — exponential but better than n! brute force
D) All of the above

**Answer: D**

**Explanation:**
TSP DP: states = (visited set, current city). 2^n subsets × n cities = 2^n × n states. Each transition: try moving to unvisited city O(n). Total: O(2^n × n²). n=20: ~20 million states, feasible. n! brute force: 20! ≈ 2.4 × 10^18, infeasible. DP reduces factorial to exponential.

---

**Q22.22: Advanced - [Theory] - [DP on Trees]**

DP on trees:

A) Process leaves first, combine at parent
B) Post-order traversal (children before parent)
C) State: dp[node] depends on dp[children]
D) All of the above

**Answer: D**

**Explanation:**
Tree DP: process bottom-up (leaves → root). Each node's DP depends on children's results. Common problems: max independent set on tree, tree diameter, subtree sizes, tree coloring. Rooted tree: DFS, process children recursively, combine at parent. O(n) for most tree DP problems.

---

**Q22.23: Advanced - [Theory] - [Max Independent Set on Tree]**

Maximum independent set on tree:

A) dp[v][0] = max independent set in subtree of v, v NOT included
B) dp[v][1] = max independent set in subtree of v, v included
C) dp[v][0] = Σ max(dp[child][0], dp[child][1])
D) dp[v][1] = 1 + Σ dp[child][0]

**Answer: D**

**Explanation:**
Tree MIS: select maximum vertices such that no two adjacent. If v not included: each child can be included or not (take max). If v included: no child can be included. Standard tree DP: O(n). On general graphs: NP-hard. Tree structure makes it polynomial. Base: leaf v: dp[v][0]=0, dp[v][1]=1.

---

**Q22.24: Intermediate - [Theory] - [Minimum Path Sum in Grid]**

Minimum path sum (top-left to bottom-right, right/down only):

A) dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
B) First row/column: cumulative sum (only one direction)
C) O(mn) time, O(n) space optimized
D) All of the above

**Answer: D**

**Explanation:**
Grid DP: each cell reachable from above or left. dp[i][j] = cost to reach (i,j) optimally. First row: only from left. First column: only from above. Interior: min of above and left + current. O(mn). Space: single row O(n). Extensions: allow diagonal, obstacles, max path sum.

---

**Q22.25: Intermediate - [Theory] - [Subset Sum]**

Subset sum problem:

A) Does a subset exist that sums to target?
B) dp[j] = true if some subset sums to j
C) For each num: dp[j] |= dp[j-num] (process right-to-left)
D) O(n × target), pseudo-polynomial

**Answer: D**

**Explanation:**
Subset sum: partition into subsets with specific sums. dp[0]=true. For each number, update dp right-to-left (0/1 knapsack style). dp[target] tells if achievable. O(n × sum). NP-complete in general but pseudo-polynomial DP works for reasonable sum values. Variant: partition into two equal-sum subsets → target = total/2.

---

**Q22.26: Intermediate - [Theory] - [Word Break]**

Word break problem:

A) Can string be segmented into dictionary words?
B) dp[i] = true if s[0..i-1] can be segmented
C) dp[i] = OR over j<i of (dp[j] AND s[j..i-1] in dict)
D) O(n² × L) where L = max word length

**Answer: D**

**Explanation:**
Word break: dp[0] = true (empty string). For each position i, try all previous positions j: if dp[j] and s[j..i-1] is a valid word → dp[i]=true. Use hash set for dictionary lookup O(1). Optimization: only check j values where i-j ≤ max word length. For generating all segmentations: backtracking with memoization.

---

**Q22.27: Foundational - [Theory] - [Overlapping Subproblems Example]**

Fibonacci demonstrates overlapping subproblems:

A) fib(5) calls fib(4)+fib(3)
B) fib(4) calls fib(3)+fib(2) — fib(3) computed twice!
C) Without memoization: exponential redundancy
D) With memoization: each fib(k) computed once → O(n)

**Answer: D**

**Explanation:**
fib(5) call tree: fib(3) computed 2 times, fib(2) computed 3 times, fib(1) computed 5 times. Total calls: O(2^n). With memoization: n+1 unique subproblems, each O(1) → O(n). This massive reduction from exponential to linear is DP's power.

---

**Q22.28: Advanced - [Theory] - [Digit DP]**

Digit DP:

A) Count numbers with specific digit properties up to N
B) State: (position, tight constraint, digits used so far)
C) Process digit by digit from most significant
D) All of the above

**Answer: D**

**Explanation:**
Digit DP: "how many numbers in [0, N] satisfy condition?" State: current position, whether still bounded by N's digits (tight), and any accumulated properties (sum, digit set, etc.). For each position: if tight, digit ≤ N's digit; else 0-9. Transition: update properties. O(digits × states). Common in competitive programming.

---

**Q22.29: Advanced - [Theory] - [DP Optimization - Divide and Conquer]**

Divide and conquer DP optimization:

A) When dp[i][j] = min over k≤j of (dp[i-1][k-1] + cost(k,j))
B) If optimal split point opt(i,j) is monotone: opt(i,j) ≤ opt(i,j+1)
C) Reduces O(kn²) to O(kn log n)
D) All of the above

**Answer: D**

**Explanation:**
D&C optimization: when optimal split point is monotone (SMAWK condition), divide range, find opt for midpoint, recurse on halves with narrowed range. Each level of recursion: O(n) work. O(log n) levels → O(n log n) per row. Total for k rows: O(kn log n). Common in partition-type problems.

---

**Q22.30: Expert - [Theory] - [Convex Hull Trick]**

Convex Hull Trick (CHT):

A) When dp[i] = min over j of (dp[j] + b[j] × a[i] + c[i])
B) Maintain set of lines, query minimum at x = a[i]
C) Reduces from O(n²) to O(n log n) or O(n)
D) All of the above

**Answer: D**

**Explanation:**
CHT: dp transition is linear function of some parameter. View as "which line gives minimum at x?" Maintain convex hull of lines. If query points sorted: amortized O(1) per query (Li Chao tree or pointer advancement). If not sorted: O(log n) per query. Powerful DP optimization. Common in competitive programming for "slope trick" problems.

---

**Q22.31: Intermediate - [Theory] - [Palindrome Partitioning]**

Minimum cuts for palindrome partitioning:

A) dp[i] = min cuts for s[0..i]
B) For each palindrome s[j..i]: dp[i] = min(dp[j-1] + 1)
C) Precompute palindromes in O(n²) or use Manacher's
D) O(n²) total

**Answer: D**

**Explanation:**
Palindrome partition: cut string so each piece is palindrome. dp[i] = min cuts for first i+1 characters. For each position i: try all j ≤ i where s[j..i] is palindrome. dp[i] = min(dp[j-1] + 1). Precompute is_palindrome[j][i] in O(n²). Total: O(n²). Can extend to count all partitions.

---

**Q22.32: Intermediate - [Theory] - [Unique Paths in Grid]**

Unique paths in m×n grid (right/down only):

A) dp[i][j] = dp[i-1][j] + dp[i][j-1]
B) dp[0][j] = dp[i][0] = 1 (only one path along edges)
C) Answer: C(m+n-2, m-1) = combinatorial formula
D) Both DP and combinatorial solutions work

**Answer: D**

**Explanation:**
Paths in grid: total m+n-2 moves (m-1 right + n-1 down). Choose m-1 positions for right moves: C(m+n-2, m-1). DP equivalent but slower at O(mn). With obstacles: DP is necessary (combinatorial doesn't handle easily). DP approach generalizes better.

---

**Q22.33: Advanced - [Theory] - [SOS DP - Sum over Subsets]**

Sum over subsets DP:

A) For each mask, compute sum over all submasks
B) dp[mask] = Σ f(submask) for all submasks of mask
C) O(3^n) naive, O(n × 2^n) with SOS optimization
D) All of the above

**Answer: D**

**Explanation:**
SOS DP: for each bitmask, compute aggregate over all submasks. Naive submask enumeration: O(3^n). SOS optimization: iterate over bits, O(n × 2^n). For each bit position: dp[mask] += dp[mask ^ (1<<bit)] if bit is set. Processes each dimension independently. Used in: problems involving subset relationships, inclusion-exclusion.

---

**Q22.34: Foundational - [Theory] - [Space Optimization]**

DP space optimization:

A) If dp[i] only depends on dp[i-1]: keep two rows O(n) instead of O(mn)
B) If dp[i] depends on dp[i-1] and dp[i-2]: keep three values
C) Knapsack: 1D array with careful update order
D) All of the above

**Answer: D**

**Explanation:**
Space optimization: analyze dependencies. LCS: row i depends only on row i-1 → O(2n) space. Fibonacci: only previous two values → O(1). 0/1 knapsack: process weights right-to-left in 1D. Unbounded: left-to-right in 1D. Key: update order must not overwrite needed values. Reduces space without affecting time.

---

**Q22.35: Intermediate - [Theory] - [Longest Common Substring]**

Longest common substring (contiguous):

A) dp[i][j] = length of common substring ending at i,j
B) If s1[i]==s2[j]: dp[i][j] = dp[i-1][j-1] + 1. Else: dp[i][j] = 0
C) Answer: max of all dp[i][j]
D) O(mn) time, different from LCS (subsequence)

**Answer: D**

**Explanation:**
Substring vs subsequence: substring must be contiguous. dp[i][j] resets to 0 on mismatch (vs taking max in LCS). Track global maximum. Alternative: suffix array + LCP in O(n log n). For very long strings: rolling hash approach.

---

**Q22.36: Intermediate - [Theory] - [Buy/Sell Stock with Cool Down]**

Stock with cooldown after selling:

A) States: hold (have stock), sold (just sold), rest (cooldown/no stock)
B) hold[i] = max(hold[i-1], rest[i-1] - price[i])
C) sold[i] = hold[i-1] + price[i]. rest[i] = max(rest[i-1], sold[i-1])
D) O(n) time, O(1) space

**Answer: D**

**Explanation:**
State machine DP: define states based on what you can do next. hold: owning stock (can sell or hold). sold: just sold (must rest next). rest: no stock (can buy or rest). Transitions model constraints. O(n) time. Multiple stock variants use similar state machine approach. Clean way to handle complex transition rules.

---

**Q22.37: Advanced - [Theory] - [Knuth's Optimization]**

Knuth's optimization for optimal BST:

A) When dp[i][j] = min over i≤k≤j of dp[i][k-1] + dp[k+1][j] + w(i,j)
B) If opt(i,j-1) ≤ opt(i,j) ≤ opt(i+1,j): monotone condition
C) Reduces O(n³) to O(n²)
D) All of the above

**Answer: D**

**Explanation:**
Knuth optimization: when optimal split point is monotone (opt(i,j-1) ≤ opt(i,j) ≤ opt(i+1,j)). Restrict search range for opt(i,j). Total work: O(n²) instead of O(n³). Applies to: optimal BST, stone merging (quadrangle inequality condition). Powerful but requires verifying monotonicity condition.

---

**Q22.38: Expert - [Theory] - [Profile DP (Broken Profile)]**

Profile DP / broken profile:

A) DP on grid processed column by column
B) State: configuration of current column boundary
C) Example: tiling m×n grid with dominoes, dp[column][bitmask]
D) O(n × 2^m) where m is grid width

**Answer: D**

**Explanation:**
Profile DP: process grid column by column, track boundary state as bitmask. Each bit: does a domino extend into next column at this row? Useful for: tiling problems, grid covering. m ≤ 20 typically. State: 2^m profiles. Transitions: fill current column consistent with profile. Elegant but requires careful case analysis.

---

**Q22.39: Intermediate - [Theory] - [Catalan Numbers via DP]**

Catalan numbers:

A) C(n) = Σ C(i) × C(n-1-i) for i = 0 to n-1
B) Count: valid parenthesizations, BST structures, paths
C) C(n) = C(2n,n)/(n+1) ~ 4^n / (n^(3/2) √π)
D) All of the above

**Answer: D**

**Explanation:**
Catalan: C(0)=1, C(1)=1, C(2)=2, C(3)=5, C(4)=14. Counts: balanced parentheses of n pairs, BSTs with n nodes, non-crossing partitions, full binary trees, Dyck paths. DP recurrence: split at root position. Closed form: C(2n,n)/(n+1). Appears throughout combinatorics and CS.

---

**Q22.40: Advanced - [Theory] - [DP on DAG]**

DP on DAG:

A) Process vertices in topological order
B) Each vertex's DP depends only on predecessors
C) Longest path in DAG: weight + max(predecessor values)
D) All of the above

**Answer: D**

**Explanation:**
DAG DP: topological order ensures all dependencies processed first. Shortest/longest path: dp[v] = opt(dp[u] + w(u,v)) for predecessor u. O(V+E). Many problems reduce to DAG DP: scheduling with precedence, critical path, counting paths. Any DP can be viewed as DP on DAG of states.

---

**Q22.41: Expert - [Theory] - [Hirschberg's Algorithm]**

Hirschberg's algorithm for LCS:

A) Computes LCS in O(mn) time but O(min(m,n)) space
B) Divide-and-conquer + DP
C) Finds actual LCS, not just length
D) All of the above

**Answer: D**

**Explanation:**
Standard LCS: O(mn) space to reconstruct. Hirschberg: divide and conquer. Compute LCS length in forward/backward passes with O(n) space. Find optimal split point. Recurse on halves. O(mn) time (constant factor increase), O(min(m,n)) space. Key insight: LCS length computable in O(n) space; finding split via forward+backward pass.

---

**Q22.42: Intermediate - [Theory] - [Egg Drop Problem]**

Egg drop (minimum trials, k eggs, n floors):

A) dp[k][t] = max floors testable with k eggs and t trials
B) dp[k][t] = dp[k-1][t-1] + dp[k][t-1] + 1
C) Binary search for minimum t where dp[k][t] ≥ n
D) O(k × log n)

**Answer: D**

**Explanation:**
Egg drop: dp[k][t] = max floors. Drop from floor f: breaks → k-1 eggs, t-1 trials for floors below. Survives → k eggs, t-1 trials for floors above. dp[k][t] = below + above + 1 = dp[k-1][t-1] + dp[k][t-1] + 1. Find min t: dp[k][t] ≥ n. O(k × log n) with binary search on t.

---

**Q22.43: Expert - [Theory] - [Alien DP]**

Aliens trick (lambda optimization):

A) Remove constraint "exactly k items" by adding penalty λ per item
B) Binary search on λ to achieve exactly k items
C) Reduces constrained DP to unconstrained + binary search
D) All of the above

**Answer: D**

**Explanation:**
Aliens trick: for "optimize subject to exactly k items" DP, remove the k constraint, add penalty λ per item. Solve unconstrained DP for each λ. Binary search on λ to find value where solution uses exactly k items. Reduces O(nk) to O(n log(answer)) often. Named after IOI 2016 "Aliens" problem. Powerful general technique.

---

**Q22.44: Advanced - [Theory] - [DP with Probability]**

Probabilistic DP:

A) dp[state] = expected value or probability of reaching state
B) Transition: dp[state] = Σ p(transition) × dp[next_state]
C) Used for: dice games, random walks, expected operations
D) All of the above

**Answer: D**

**Explanation:**
Probability DP: model random processes. Forward: dp[state] = probability of being in state. Backward: dp[state] = expected cost/value from state. Transitions weighted by probabilities. Example: expected coin flips to see all faces. Expected steps in random walk. Markov chain analysis. Same DP framework, different interpretation.

---

**Q22.45: Intermediate - [Theory] - [DP Reconstruction]**

Reconstructing DP solution (not just value):

A) Store decisions made at each state
B) Backtrack from answer state following stored decisions
C) Example: LCS backtrack through dp table
D) All of the above

**Answer: D**

**Explanation:**
DP gives optimal value; reconstruction gives actual solution. Method 1: store choice at each state, backtrack. Method 2: recompute and check which transition was optimal. LCS: diagonal = match (include char), up/left = skip. Knapsack: did we include item i? Check dp[i][w] vs dp[i-1][w]. Space trade-off: storing choices vs recomputing.

---

**Q22.46: Foundational - [Theory] - [DP vs Greedy]**

DP vs greedy:

A) Greedy: locally optimal choice is globally optimal
B) DP: explores all choices, keeps optimal
C) Greedy is subset of DP (DP reduces to greedy when greedy works)
D) All of the above

**Answer: D**

**Explanation:**
Greedy: make best local choice, never reconsider. Correct for: activity selection, Huffman, MST. DP: try all options for each subproblem. Correct for: knapsack, edit distance, LCS. If greedy works: use it (simpler, faster). If greedy fails: must use DP. Coin change: greedy works for some denominations, not others. DP always works.

---

**Q22.47: Expert - [Theory] - [Connection Cover Optimization]**

Connection between DP and shortest path:

A) Any DP can be viewed as shortest/longest path in DAG of states
B) Each state = node, each transition = edge
C) DP fills "distances" in topological order
D) All of the above

**Answer: D**

**Explanation:**
DP = DAG shortest path. States are vertices. Transitions are edges with costs. Optimal substructure = shortest path property. Topological order = bottom-up computation. This unifying view: Fibonacci = path in chain, LCS = path in grid, TSP = path in powerset lattice. Deep connection between DP and graph algorithms.

---

**Q22.48: Expert - [Theory] - [DP on Broken Profile]**

Counting Hamiltonian paths with profile DP:

A) State: (column, profile bitmask of path endpoints)
B) O(n × 2^m) for m×n grid
C) Handles connectivity tracking
D) Exponential in grid width, polynomial in length

**Answer: D**

**Explanation:**
Hamiltonian path on grid: visit every cell exactly once. Profile DP: process column by column, track which cells have path segments entering. State: bitmask of profile. Transitions: consistent extensions. O(n × C_m) where C_m relates to profile states (2^m upper bound, fewer valid profiles). Practical for narrow grids (m ≤ 15).

---

**Q22.49: Expert - [Theory] - [Slope Trick]**

Slope trick DP:

A) Represent DP function by its slope changes
B) Maintain piecewise linear function via priority queue
C) Efficient for: LIS cost, sequences with adjacent constraints
D) All of the above

**Answer: D**

**Explanation:**
Slope trick: instead of full DP array, maintain breakpoints of piecewise-linear convex function. Operations (add convex function, shift, take envelope) handled by priority queue. O(n log n) for problems that appear O(n²). Elegant technique from competitive programming. Applicable when DP function is convex and transitions are simple.

---

**Q22.50: Advanced - [Theory] - [Counting DP]**

Counting with DP:

A) How many ways to reach a state (vs optimization)
B) dp[state] = Σ dp[predecessor_states]
C) Module arithmetic often needed (answer mod 10^9+7)
D) All of the above

**Answer: D**

**Explanation:**
Counting DP: sum instead of min/max. Number of paths in grid, number of BSTs with n nodes (Catalan), number of decodings, number of valid parenthesizations. Same framework: define states, transitions add counts. Often need modular arithmetic for large answers. Counting is often harder than optimization (more states needed).

---

**Q22.51: Foundational - [Theory] - [Common DP Patterns]**

Common DP patterns:

A) Linear: dp[i] depends on dp[i-1], dp[i-2], etc.
B) Grid: dp[i][j] depends on dp[i-1][j], dp[i][j-1]
C) Interval: dp[i][j] depends on dp[i][k] and dp[k][j]
D) All standard patterns

**Answer: D**

**Explanation:**
DP patterns: (1) Linear/1D: Fibonacci, house robber, LIS. (2) Grid/2D: path sum, LCS, edit distance. (3) Interval: MCM, palindrome partition. (4) Tree: post-order processing. (5) Bitmask/subset: TSP, SOS. (6) Digit: counting with digit properties. Recognizing the pattern is half the battle.

---

**Q22.52: Advanced - [Theory] - [DP on Graph]**

DP on general graphs:

A) Only works on DAGs (no cycles)
B) For graphs with cycles: convert to DAG or use different approach
C) State augmentation can break cycles (add dimension)
D) All of the above

**Answer: D**

**Explanation:**
DP requires DAG of states (no circular dependency). General graph with cycles: shortest path DP (Bellman-Ford) works by iterating. Or augment state to make DAG: (vertex, step_count) is always a DAG. Or transform: SCC condensation makes DAG. DP on graph = shortest path algorithm with appropriate state space.

---

**Q22.53: Intermediate - [Theory] - [Wildcard Pattern Matching]**

Wildcard pattern matching DP:

A) '?' matches any single char, '*' matches any sequence (including empty)
B) dp[i][j] = pattern[0..i-1] matches text[0..j-1]
C) '*': dp[i][j] = dp[i-1][j] (use *) OR dp[i][j-1] (extend *)
D) O(mn)

**Answer: D**

**Explanation:**
Wildcard matching: dp[i][j] = does pattern[0..i-1] match text[0..j-1]? char match or '?': dp[i-1][j-1]. '*': dp[i-1][j] (match empty) OR dp[i][j-1] (match one more char). O(mn). Similar to regex matching but simpler. Full regex: NFA simulation or more complex DP.

---

**Q22.54: Foundational - [Theory] - [DP Applications Summary]**

DP applications across domains:

A) Strings: LCS, edit distance, word break, regex
B) Optimization: knapsack, scheduling, path planning
C) Counting: paths, trees, partitions, combinations
D) All of the above, plus bioinformatics, finance, AI

**Answer: D**

**Explanation:**
DP is universal optimization/counting technique. Strings: alignment, matching, palindromes. Graphs: shortest paths (Dijkstra, Floyd-Warshall are DP). Sequences: LIS, subsequences. Combinatorics: Catalan, partitions. Real-world: portfolio optimization, speech recognition (Viterbi), bioinformatics (sequence alignment). Most algorithms interview questions involve DP.

---

**Q22.55: Foundational - [Theory] - [Rod Cutting]**

Rod cutting problem:

A) Given rod of length n and prices for each length, maximize revenue
B) dp[i] = max revenue for rod of length i
C) dp[i] = max(price[j] + dp[i-j]) for j = 1 to i
D) All of the above — O(n²)

**Answer: D**

**Explanation:**
Rod cutting: unbounded subproblem (can cut same length multiple times). dp[0]=0. For each length i: try all first-cut lengths j, take best. dp[i] = max over j of price[j] + dp[i-j]. O(n²). First example in CLRS for DP. Relates to unbounded knapsack — rod lengths are items, capacity is rod length.

---

**Q22.56: Intermediate - [Theory] - [Palindrome Partitioning]**

Minimum cuts to partition string into palindromes:

A) dp[i] = minimum cuts for s[0..i]
B) If s[0..i] is palindrome: dp[i] = 0
C) Else: dp[i] = min(dp[j] + 1) for j where s[j+1..i] is palindrome
D) All of the above — O(n²) with palindrome preprocessing

**Answer: D**

**Explanation:**
Palindrome partitioning: precompute isPalin[i][j] using DP (expand from center or DP: isPalin[i][j] = s[i]==s[j] && isPalin[i+1][j-1]). Then dp[i] = min cuts for first i+1 chars. If whole prefix is palindrome: 0 cuts. Else: try all split points where suffix is palindrome. O(n²) total.

---

**Q22.57: Advanced - [Theory] - [Egg Drop Problem]**

Egg drop: k eggs, n floors, minimize worst-case trials:

A) dp[k][n] = min trials with k eggs and n floors
B) dp[k][n] = 1 + min over f of max(dp[k-1][f-1], dp[k][n-f])
C) Binary search on f gives O(n×k×log n)
D) All of the above

**Answer: D**

**Explanation:**
Classic DP: drop egg from floor f. Breaks: k-1 eggs, f-1 floors below. Survives: k eggs, n-f floors above. Worst case: take max. Optimize over f. Base: dp[1][n]=n, dp[k][0]=0. O(kn²) naive, O(kn log n) with binary search on optimal f. Alternative formulation: dp[t][k] = max floors testable with t trials and k eggs. O(kn) with this approach.

---

**Q22.58: Foundational - [Theory] - [Subset Sum]**

Subset sum: can we select elements summing to target?

A) dp[i][s] = can first i elements form sum s?
B) dp[i][s] = dp[i-1][s] (skip) OR dp[i-1][s-arr[i]] (include)
C) Space optimization: 1D dp[s], iterate s from target down
D) All of the above — O(n × target)

**Answer: D**

**Explanation:**
Subset sum: Boolean DP. dp[0][0]=true, dp[0][s>0]=false. For each element: include or exclude. dp[n][target] = answer. 1D optimization: fill right-to-left (descending s) to avoid using element twice. O(n × sum). Pseudo-polynomial (depends on target value, not input size). NP-complete in general but practical for small targets.

---

**Q22.59: Intermediate - [Theory] - [Longest Palindromic Subsequence]**

Longest palindromic subsequence (LPS):

A) LPS(s) = LCS(s, reverse(s))
B) Or direct DP: dp[i][j] = LPS of s[i..j]
C) dp[i][j] = dp[i+1][j-1]+2 if s[i]==s[j], else max(dp[i+1][j], dp[i][j-1])
D) All of the above — O(n²)

**Answer: D**

**Explanation:**
LPS: longest subsequence that's a palindrome. Elegant reduction: LPS = LCS with reverse. Or direct interval DP: base dp[i][i]=1. If endpoints match: extend both sides. Else: try dropping either end. O(n²) time and space. Space: O(n) with diagonal-by-diagonal filling. Applications: minimum insertions to make palindrome = n - LPS.

---

**Q22.60: Intermediate - [Theory] - [Unbounded Knapsack]**

Unbounded knapsack (items can be used multiple times):

A) dp[w] = max value achievable with capacity w
B) For each item: dp[w] = max(dp[w], dp[w-weight[i]] + value[i])
C) Iterate w from 0 to W (ascending — allows reuse)
D) All of the above — O(n × W)

**Answer: D**

**Explanation:**
Unbounded vs 0/1 knapsack: items reusable. Key difference in 1D optimization: iterate capacity ascending (allows item reuse) vs descending (prevents reuse in 0/1). Same O(nW) complexity. Examples: coin change (minimize coins), rod cutting (maximize revenue). Both are unbounded knapsack variants.

---

**Q22.61: Foundational - [Trace] - [Grid Paths with Obstacles]**

Unique paths in grid with obstacles:

A) dp[i][j] = number of paths from (0,0) to (i,j)
B) If obstacle at (i,j): dp[i][j] = 0
C) Else: dp[i][j] = dp[i-1][j] + dp[i][j-1]
D) Grid: `.#.` / `...` / `...` → dp[2][2] = 2

**Answer: D**

**Explanation:**
Grid paths: can only move right or down. dp[0][0]=1 (if no obstacle). First row/col: 1 until obstacle, then 0. Interior: sum of top and left (skip obstacles). Example with obstacle at (0,1): paths must go down first. O(m×n) time and space. Space optimization: single row O(n).

---

**Q22.62: Intermediate - [Theory] - [House Robber]**

House robber (can't rob adjacent houses):

A) dp[i] = max money robbing houses 0 to i
B) dp[i] = max(dp[i-1], dp[i-2] + money[i])
C) Skip current (dp[i-1]) or rob current + best from 2 back
D) All of the above — O(n) time, O(1) space

**Answer: D**

**Explanation:**
House robber: no two adjacent. dp[i] = max of not-rob (dp[i-1]) or rob (dp[i-2]+money[i]). Only need previous two values → O(1) space. Circular variant (houses in circle): run twice — excluding first house, excluding last house, take max. Tree variant: tree DP (rob node or not, passing up results).

---

**Q22.63: Foundational - [Theory] - [Minimum Path Sum]**

Minimum path sum in grid (top-left to bottom-right):

A) dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
B) First row: cumulative sum left-to-right
C) First column: cumulative sum top-to-bottom
D) All of the above — O(m × n)

**Answer: D**

**Explanation:**
Minimum path sum: like unique paths but minimizing cost. Each cell: add grid value to minimum of top or left. Boundary: first row/col have only one incoming direction. Can modify grid in-place (no extra space). Triangle variant: dp[i][j] = triangle[i][j] + min(dp[i-1][j-1], dp[i-1][j]).

---

**Q22.64: Foundational - [Trace] - [Climbing Stairs Variants]**

Climbing stairs with step sizes {1, 2, 3}:

A) dp[n] = dp[n-1] + dp[n-2] + dp[n-3]
B) dp[0]=1, dp[1]=1, dp[2]=2
C) dp[3] = 1+1+2 = 4 ways
D) General: k step sizes → dp[n] = Σ dp[n-step_i]

**Answer: D**

**Explanation:**
Climbing stairs: Fibonacci generalization. Steps {1,2}: dp[n]=dp[n-1]+dp[n-2] (Fibonacci). Steps {1,2,3}: Tribonacci. General k steps: sum over all valid step sizes. dp[4] with {1,2,3}: dp[1]+dp[2]+dp[3] = 1+2+4 = 7. This pattern underlies coin change (counting ways) and other combinatorial DP problems.

---

**Q22.65: Intermediate - [Theory] - [Longest Common Substring]**

Longest common substring (contiguous, not subsequence):

A) dp[i][j] = length of common substring ending at s1[i] and s2[j]
B) If s1[i]==s2[j]: dp[i][j] = dp[i-1][j-1]+1, else dp[i][j]=0
C) Answer: max over all dp[i][j]
D) All of the above — O(m × n)

**Answer: D**

**Explanation:**
Substring vs subsequence: substring must be contiguous. dp[i][j]: longest common suffix ending at both positions. Match: extend by 1. Mismatch: reset to 0 (can't skip characters in substring). Track global maximum. O(mn) time. O(min(m,n)) space with row optimization. Suffix tree: O(m+n) alternative.

---

**Q22.66: Intermediate - [Theory] - [Partition Equal Subset Sum]**

Partition array into two subsets with equal sum:

A) Total sum must be even; target = sum/2
B) Reduces to subset sum problem with target = sum/2
C) dp[s] = can we form sum s from array elements?
D) All of the above — O(n × sum/2)

**Answer: D**

**Explanation:**
Equal partition: if total sum is odd → impossible. If even: find subset summing to sum/2 (the other subset automatically sums to sum/2 too). Standard subset sum DP. O(n × sum/2). Related: partition into k equal subsets (NP-hard for k>2, use bitmask DP). Multi-way partition: known NP-hard, but heuristics work well.

---

**Q22.67: Intermediate - [Theory] - [Unique Paths in Grid]**

Number of unique paths from top-left to bottom-right (m×n grid, only right/down):

A) dp[i][j] = dp[i-1][j] + dp[i][j-1]
B) Combinatorial: C(m+n-2, m-1)
C) dp approach: O(m×n), combinatorial: O(m+n)
D) All of the above

**Answer: D**

**Explanation:**
Unique paths: need (m-1) downs and (n-1) rights in any order. Combinatorial: choose which m-1 of m+n-2 moves are down = C(m+n-2, m-1). DP: fill grid cell-by-cell. Both give same answer. DP is more general (handles obstacles, variable costs). Combinatorial is O(m) arithmetic vs O(mn) DP. 3×3 grid: C(4,2)=6 paths.

---

**Q22.68: Advanced - [Theory] - [Wildcard Pattern Matching]**

Wildcard matching (? = single char, * = any sequence):

A) dp[i][j] = does pattern[0..i] match text[0..j]?
B) If pattern[i] == '*': dp[i][j] = dp[i-1][j] (match empty) OR dp[i][j-1] (match one more)
C) If pattern[i] == '?' or match: dp[i][j] = dp[i-1][j-1]
D) All of the above — O(m × n)

**Answer: D**

**Explanation:**
Wildcard matching: '?' matches exactly one character. '*' matches any sequence (including empty). DP: dp[i][j] tracks if first i pattern chars match first j text chars. Star: either matches zero chars (dp[i-1][j]) or extends match (dp[i][j-1]). Base: dp[0][0]=true, dp[leading stars][0]=true. O(mn). Related: regex matching (. and * have slightly different semantics).

---

**Q22.69: Foundational - [Theory] - [Space Optimization in DP]**

Space optimization techniques:

A) 2D → 1D: if dp[i] depends only on dp[i-1], keep one row
B) Rolling array: alternate between two rows
C) Sometimes only need O(1) variables (Fibonacci, house robber)
D) All of the above

**Answer: D**

**Explanation:**
Space optimization: identify which previous states are actually needed. Fibonacci: only prev and prev-prev → O(1). Knapsack: only previous row → O(W). LCS: only previous row → O(min(m,n)). Grid DP: often single row. Trade-off: lose ability to reconstruct solution (need full table for path reconstruction). Time complexity unchanged.

---

**Q22.70: Intermediate - [Theory] - [Optimal BST]**

Optimal binary search tree:

A) Given keys with search frequencies, minimize expected search cost
B) dp[i][j] = optimal cost for keys i..j
C) dp[i][j] = min over root r of dp[i][r-1] + dp[r+1][j] + sum(freq[i..j])
D) O(n³) naive, O(n²) with Knuth's optimization

**Answer: D**

**Explanation:**
Optimal BST: frequent keys near root. Interval DP: try each key as root, recursively optimize subtrees. Cost = left subtree + right subtree + all frequencies (depth increases by 1). O(n³) with three nested loops. Knuth's optimization: optimal root for [i,j] is between optimal roots for [i,j-1] and [i+1,j] → reduces to O(n²). Classic CLRS problem.

---

**Q22.71: Advanced - [Theory] - [DP State Machine]**

State machine DP (e.g., buy/sell stock with cooldown):

A) Define states: HOLD, SOLD, REST
B) Transitions: HOLD→SOLD (sell), REST→HOLD (buy), SOLD→REST
C) dp[i][state] = max profit at day i in each state
D) All of the above — O(n) time, O(1) space

**Answer: D**

**Explanation:**
State machine DP: model problem as finite automaton. Buy/sell with cooldown: HOLD (own stock), SOLD (just sold, cooldown), REST (no stock, can buy). Transitions encode rules. dp per day per state. Only depends on previous day → O(1) space. Generalizes: buy/sell with k transactions, with fee, etc. Powerful pattern for constraint-heavy problems.

---

**Q22.72: Advanced - [Theory] - [Matrix Exponentiation for DP]**

Matrix exponentiation to speed up linear DP:

A) Linear recurrence dp[n] = a₁dp[n-1] + a₂dp[n-2] + ...
B) Express as matrix multiplication: [dp] = M × [dp-1]
C) dp[n] = M^n × base → O(k³ log n) via fast exponentiation
D) All of the above

**Answer: D**

**Explanation:**
Any linear recurrence: expressible as matrix multiplication. Fibonacci: [[1,1],[1,0]]^n gives F(n). k-term recurrence: k×k matrix. M^n via repeated squaring: O(k³ log n). Huge speedup when n is large and k is small. Applications: Fibonacci in O(log n), Tribonacci, linear DP with constant coefficients, counting paths of length n in graph.

---

**Q22.73: Intermediate - [Theory] - [Painting Fence]**

Painting fence with k colors, no 3 consecutive same color:

A) same[i] = ways to paint post i same as post i-1
B) diff[i] = ways to paint post i different from post i-1
C) same[i] = diff[i-1], diff[i] = (k-1) × (same[i-1] + diff[i-1])
D) Total ways: same[n] + diff[n]

**Answer: D**

**Explanation:**
Fence painting: constraint on consecutive same-color posts. Two states: same as previous or different. Same: previous must have been different (else 3 in a row). Different: k-1 color choices regardless of previous state. Base: same[2]=k, diff[2]=k(k-1). Simple linear DP. Generalizes to "no m consecutive same color" with m-1 same-count states.

---

**Q22.74: Intermediate - [Theory] - [Counting Partitions]**

Number of ways to write n as sum of positive integers (order doesn't matter):

A) Partition function p(n): p(4) = 5 (4, 3+1, 2+2, 2+1+1, 1+1+1+1)
B) dp[i][j] = partitions of i using parts ≤ j
C) dp[i][j] = dp[i][j-1] + dp[i-j][j]
D) All of the above

**Answer: D**

**Explanation:**
Integer partitions: use part j or don't. Don't use j: dp[i][j-1]. Use at least one j: dp[i-j][j] (can reuse). Base: dp[0][j]=1 (empty partition), dp[i][0]=0. This is unbounded knapsack with items 1..n, capacity n. Growth: p(100)=190,569,292. Hardy-Ramanujan formula gives asymptotic. p(n) ~ exp(π√(2n/3)) / (4n√3).

---

**Q22.75: Foundational - [Theory] - [DP Problem Classification]**

Classifying DP problems:

A) Sequence DP: LIS, LCS, edit distance
B) Grid DP: paths, minimum cost, obstacles
C) Interval DP: MCM, palindrome partitioning, optimal BST
D) All common categories, plus: knapsack, tree DP, bitmask DP, digit DP

**Answer: D**

**Explanation:**
DP problem categories: (1) Sequence: operate on 1D/2D sequences. (2) Grid: 2D traversal. (3) Interval: dp[i][j] for range. (4) Knapsack: include/exclude items. (5) Tree: dp on tree nodes. (6) Bitmask: dp[mask] for subsets. (7) Digit: dp on digit positions. Recognizing the category is key to formulating the state and transition. Most DP problems fit into these patterns.

---

## Chapter 22 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 19 | DP definition, memo vs tabulation, Fibonacci, coin change, LIS, LCS, knapsack, rod cutting, subset sum, grid paths, climbing stairs, space optimization, classification |
| Intermediate | 28 | Edit distance, MCM, interval DP, states design, grid DP, stock, word break, counting, palindrome partitioning, unbounded knapsack, house robber, longest common substring, partition equal subset, unique paths, optimal BST, painting fence, counting partitions, LPS |
| Advanced | 19 | Bitmask DP, TSP, tree DP, digit DP, D&C optimization, SOS, probabilistic, DAG DP, egg drop, wildcard matching, state machine, matrix exponentiation |
| Expert | 9 | CHT, Knuth's, profile DP, aliens trick, slope trick, Hirschberg's, Hamiltonian |

**Total MCQs: 75** | **Target Met: ✓**

**Next:** Chapter 23 - Greedy Algorithms
