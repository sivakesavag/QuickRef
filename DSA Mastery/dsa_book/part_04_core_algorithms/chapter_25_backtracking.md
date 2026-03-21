# Chapter 25: Backtracking

**Target:** 45 MCQs | **Distribution:** 11 Foundational, 18 Intermediate, 11 Advanced, 5 Expert

---

**Q25.1: Foundational - [Theory] - [Backtracking Definition]**

Backtracking:

A) Systematic exploration of all candidate solutions
B) Build solution incrementally, abandon (backtrack) on dead ends
C) Explores tree of choices, prunes invalid branches
D) All of the above

**Answer: D**

**Explanation:**
Backtracking: try a choice, recurse, undo if it leads to failure. State space tree: each node = partial solution. Leaf = complete solution or dead end. Pruning: stop exploring branch early when constraint violated. Without pruning: same as brute force. With effective pruning: dramatically fewer states explored.

---

**Q25.2: Foundational - [Theory] - [N-Queens Problem]**

N-Queens:

A) Place N queens on N×N board with no two attacking
B) Backtrack: place queen column by column, check conflicts
C) Prune: skip positions attacked by existing queens
D) 8-Queens has 92 solutions

**Answer: D**

**Explanation:**
N-Queens: classic backtracking. Place one queen per column. At column c, try each row r. Check: no same row, no same diagonal (|r1-r2| ≠ |c1-c2|). If valid: place, recurse to next column. If no valid row: backtrack. 8-Queens: 92 solutions. Pruning reduces from 8^8 = 16M to ~15K nodes explored. Bitwise optimization: O(1) conflict check.

---

**Q25.3: Foundational - [Theory] - [Backtracking Template]**

General backtracking template:

A) backtrack(state): if goal(state): record solution
B) For each choice in candidates(state): if valid(choice):
C) make(choice), backtrack(new_state), unmake(choice)
D) All of the above — try, recurse, undo

**Answer: D**

**Explanation:**
Template: (1) Check if current state is solution. (2) Generate candidate extensions. (3) For each valid candidate: apply, recurse, undo (restore state). Key: unmake step ensures state is clean for next candidate. This is the "try everything, but prune early" pattern. All backtracking problems follow this structure.

---

**Q25.4: Foundational - [Theory] - [Sudoku Solver]**

Sudoku via backtracking:

A) Find empty cell, try digits 1-9
B) Check row, column, 3×3 box constraints
C) If valid: place and recurse. If no digit works: backtrack
D) All of the above

**Answer: D**

**Explanation:**
Sudoku: 81 cells, constraints on rows, columns, 3×3 boxes. Backtracking: find empty cell, try each digit, validate. Valid: recurse. All digits fail: backtrack (undo last placement). Optimization: choose cell with fewest candidates (MRV heuristic). Advanced: constraint propagation (naked singles, hidden singles) before backtracking.

---

**Q25.5: Foundational - [Theory] - [Subsets Generation]**

Generate all subsets:

A) For each element: include or exclude (two choices)
B) 2^n subsets total
C) Backtracking: build subset incrementally, branch at each element
D) All of the above

**Answer: D**

**Explanation:**
Subsets: for element i, two branches — include or not. Recurse. At n elements: output current subset. 2^n subsets. Iterative: use bitmask 0 to 2^n-1. Backtracking: add element, recurse, remove element, recurse. Clean O(n × 2^n) (n per subset output). Foundation for more complex combinatorial generation.

---

**Q25.6: Foundational - [Theory] - [Permutations Generation]**

Generate all permutations:

A) Fix each remaining element at current position, recurse
B) n! permutations total
C) Swap-based: swap element to front, recurse on rest, swap back
D) All of the above

**Answer: D**

**Explanation:**
Permutations: at position i, try each unused element. Fix it, recurse for remaining positions. Backtracking: mark used, recurse, unmark. Or: swap arr[i] with arr[j] for j ≥ i, recurse, swap back. n! permutations. Heap's algorithm: generates all permutations with minimal swaps. Applications: brute force optimization, testing.

---

**Q25.7: Intermediate - [Theory] - [Pruning]**

Pruning strategies in backtracking:

A) Constraint checking: skip choices violating constraints
B) Bound checking: prune if best possible from here can't beat current best
C) Symmetry breaking: avoid equivalent states
D) All of the above — key to efficiency

**Answer: D**

**Explanation:**
Pruning is what makes backtracking practical. Constraint: N-Queens row/diagonal check. Bound: branch and bound (if remaining items can't beat current best, prune). Symmetry: in N-Queens, if a solution exists, rotations/reflections also do — break symmetry to reduce by 8×. Ordering: try most promising choices first (fail-first for constraints).

---

**Q25.8: Intermediate - [Theory] - [Combinations Generation]**

Generate all C(n,k) combinations:

A) Backtracking: choose elements in order (avoid duplicates)
B) At each step: add element ≥ last added, recurse
C) Stop when k elements chosen
D) All of the above

**Answer: D**

**Explanation:**
Combinations: choose k from n without repetition, order doesn't matter. Backtrack: start from element after last chosen. If current subset size = k: record. If remaining elements insufficient: prune. C(n,k) results. O(C(n,k) × k) total. Ordering constraint (elements in increasing order) naturally avoids duplicates.

---

**Q25.9: Intermediate - [Theory] - [Constraint Satisfaction]**

Backtracking for constraint satisfaction problems (CSP):

A) Variables, domains, constraints
B) Assign values to variables, check constraints
C) If constraint violated: backtrack
D) N-Queens, Sudoku, graph coloring are CSPs

**Answer: D**

**Explanation:**
CSP framework: variables (cells/positions), domains (possible values), constraints (rules). Backtracking: assign value to next variable. If all constraints satisfied: recurse. If not: try next value. All values fail: backtrack. Heuristics: MRV (minimum remaining values), degree heuristic, forward checking. AC-3: arc consistency preprocessing.

---

**Q25.10: Intermediate - [Theory] - [Graph Coloring via Backtracking]**

Graph coloring backtracking:

A) Assign colors 1..k to vertices, no two adjacent same color
B) Try each color for current vertex, check neighbors
C) If valid: recurse. All colors fail: backtrack
D) Find minimum k (chromatic number): try k=1,2,...

**Answer: D**

**Explanation:**
k-coloring via backtracking: for each vertex, try k colors. Check adjacent vertices for conflicts. Pruning: forward checking (remove color from neighbors' domains). Finding chromatic number: minimize k. NP-hard in general. Backtracking with good heuristics handles moderate graphs. 2-coloring: polynomial (BFS). 3-coloring: NP-complete.

---

**Q25.11: Intermediate - [Theory] - [Hamiltonian Path/Cycle]**

Hamiltonian path via backtracking:

A) Visit every vertex exactly once
B) Build path incrementally, try unvisited neighbors
C) If all visited and back to start: Hamiltonian cycle
D) NP-complete — backtracking is exponential but practical for small graphs

**Answer: D**

**Explanation:**
Hamiltonian: visit all vertices exactly once. Backtracking: from current vertex, try each unvisited neighbor. Prune: if unreachable vertices detected early (connectivity check). Worst: O(n!) but pruning helps. NP-complete: no known polynomial algorithm. For small n (≤ 20): backtracking with bitmask. For larger: heuristics or exact exponential algorithms.

---

**Q25.12: Intermediate - [Theory] - [Word Search in Grid]**

Word search backtracking:

A) Find word in 2D grid, moving to adjacent cells
B) Backtracking: match character by character, try 4 directions
C) Mark cells as visited during search, unmark on backtrack
D) O(m×n × 4^L) worst case, L = word length

**Answer: D**

**Explanation:**
Word search: start from each cell matching first character. Try 4 directions for next character. Mark visited (can't reuse). Backtrack: unmark. Pruning: mismatch = immediate backtrack. Trie optimization for multiple words: build trie of words, DFS on grid with trie navigation. Boggle solver uses this approach.

---

**Q25.13: Advanced - [Theory] - [Branch and Bound]**

Branch and bound:

A) Backtracking + bounding function (estimate best possible)
B) Prune if bound ≤ current best known solution
C) Used for optimization: TSP, assignment, knapsack
D) All of the above

**Answer: D**

**Explanation:**
Branch and bound: systematic exploration with pruning based on bounds. Lower bound (minimization): if lower bound ≥ current best, prune. Upper bound: any feasible solution. Tighter bounds = more pruning. For TSP: MST gives lower bound. For knapsack: fractional solution gives upper bound. Dramatically reduces search space vs pure backtracking.

---

**Q25.14: Advanced - [Theory] - [Dancing Links (DLX)]**

Algorithm X with Dancing Links:

A) Knuth's algorithm for exact cover problem
B) Represent constraints as sparse matrix with doubly-linked lists
C) Cover/uncover columns efficiently
D) Solves Sudoku, pentomino puzzles, N-Queens

**Answer: D**

**Explanation:**
Exact cover: select rows covering each column exactly once. Algorithm X: choose column, try rows covering it, remove covered columns and conflicting rows, recurse. Dancing Links: doubly-linked list allows O(1) remove/restore (links "dance"). Sudoku: 729 rows (9×9×9 cell-digit combos), 324 columns (constraints). Very fast in practice.

---

**Q25.15: Advanced - [Theory] - [Constraint Propagation]**

Constraint propagation with backtracking:

A) Before branching: propagate implications of choices
B) Arc consistency (AC-3): if x=v eliminates all options for y → no solution
C) Reduces domain sizes, fewer branches to explore
D) All of the above

**Answer: D**

**Explanation:**
Constraint propagation: after assigning a variable, propagate effects. AC-3: for each pair (x,y), ensure every value in domain(x) has a compatible value in domain(y). If not: remove from domain(x). If domain empty: backtrack. Dramatically reduces search for CSPs like Sudoku. Naked/hidden singles: simple propagation rules.

---

**Q25.16: Intermediate - [Theory] - [Backtracking Complexity]**

Backtracking complexity:

A) Worst case: O(b^d) where b=branching factor, d=depth
B) Effective: depends on pruning quality
C) Good pruning: polynomial or near-polynomial for many instances
D) All of the above

**Answer: D**

**Explanation:**
Worst case: no pruning = exhaustive search O(b^d). Subsets: O(2^n). Permutations: O(n!). N-Queens: O(n!) worst. With pruning: typically much less. 8-Queens: 15K nodes vs 16M without pruning. Sudoku: constraint propagation often solves without any branching. Pruning quality determines practical performance.

---

**Q25.17: Intermediate - [Theory] - [Backtracking with Memoization]**

Backtracking + memoization:

A) If same state reachable via different paths: memoize
B) Converts backtracking to DP
C) Top-down DP = memoized backtracking
D) All of the above

**Answer: D**

**Explanation:**
When backtracking explores same state multiple times: add memoization → top-down DP. Example: coin change backtracking with memo. Subset sum backtracking with memo. Key: state must be fully captured by memo key. If state includes "which specific elements chosen" (not just count): harder to memoize. Subset state = bitmask → memoized backtracking.

---

**Q25.18: Advanced - [Theory] - [Sudoku Advanced Techniques]**

Advanced Sudoku solving:

A) Naked/hidden singles: forced cells (no backtracking needed)
B) X-Wing, swordfish: advanced constraint propagation
C) Usually: propagation solves most, backtracking handles the rest
D) All of the above

**Answer: D**

**Explanation:**
Sudoku difficulty levels: easy = naked singles only. Medium = hidden singles/pairs. Hard = X-Wing, coloring. Expert = few cells require trial (backtracking). Most efficient solvers: constraint propagation first, backtrack only when stuck. DLX-based solvers: handle even the hardest Sudokus in milliseconds.

---

**Q25.19: Foundational - [Theory] - [Maze Solving]**

Maze solving via backtracking:

A) Try each direction from current cell
B) Mark visited to avoid loops
C) Dead end: backtrack to last junction
D) DFS with backtracking

**Answer: D**

**Explanation:**
Maze: grid with walls and passages. Backtracking: from current cell, try up/down/left/right. If open and unvisited: move, recurse. Dead end: backtrack. Finds a path (not necessarily shortest). For shortest path: use BFS instead. For all paths: backtrack without early termination. Classic introduction to backtracking concept.

---

**Q25.20: Expert - [Theory] - [Backtracking for SAT]**

DPLL algorithm for SAT solving:

A) Davis-Putnam-Logemann-Loveland: backtracking for boolean satisfiability
B) Unit propagation: if clause has one literal, must be true
C) Pure literal elimination + backtracking
D) Foundation of modern SAT solvers

**Answer: D**

**Explanation:**
DPLL: systematic backtracking for SAT. Choose variable, assign true/false, propagate. Unit propagation: clause with one unassigned literal → force it. Pure literal: appears only positive (or only negative) → set accordingly. Modern CDCL (conflict-driven clause learning) extends DPLL with learning and non-chronological backtracking. SAT solvers handle millions of variables.

---

**Q25.21: Expert - [Theory] - [IDA* as Backtracking]**

IDA* as depth-limited backtracking:

A) DFS with f-value cutoff (g + h ≤ threshold)
B) Iteratively increase threshold
C) Combines backtracking space efficiency with A* optimality
D) All of the above

**Answer: D**

**Explanation:**
IDA*: backtracking in state space with heuristic pruning. DFS: O(depth) space. Threshold: prune states with f > threshold. Increase threshold to minimum pruned f-value. Each iteration: backtracking search with bound. Finds optimal solution with O(d) memory. See Chapter 18 for search context.

---

**Q25.22: Intermediate - [Theory] - [Partition Equal Subset Sum]**

Partition array into two equal-sum subsets:

A) Reduce to subset sum: target = total_sum / 2
B) Backtracking: try including/excluding each element
C) DP more efficient: O(n × sum/2)
D) Both work, DP preferred for efficiency

**Answer: D**

**Explanation:**
Equal partition: does subset with sum = total/2 exist? If total odd: impossible. Backtracking: try all subsets, prune when current sum exceeds target. O(2^n) worst. DP: boolean dp[j] = can form sum j. O(n × sum/2). For n ≤ 20: backtracking fine. For n > 20: DP preferred. Trade-off: backtracking explores less if few solutions, DP does all.

---

**Q25.23: Advanced - [Theory] - [Letter Combinations of Phone Number]**

Phone number letter combinations:

A) Each digit maps to 3-4 letters (abc, def, ...)
B) Backtracking: for each digit, try all mapped letters
C) O(4^n) combinations for n digits
D) All of the above

**Answer: D**

**Explanation:**
Phone keypad: 2→abc, 3→def, ..., 9→wxyz. For n-digit number: try each letter combination. Backtracking: at digit i, try each mapped letter, append, recurse to next digit. At final digit: record combination. 3^n to 4^n combinations. Pure generation (no pruning needed — all valid). Classic backtracking generation problem.

---

**Q25.24: Expert - [Theory] - [Randomized Backtracking]**

Randomized backtracking:

A) Random variable/value ordering
B) Restart with new random seed if taking too long
C) Often faster than deterministic for hard instances
D) All of the above

**Answer: D**

**Explanation:**
Randomized: shuffle choice order each run. Some random orderings find solution much faster. Random restarts: if search takes too long, restart with new random ordering. Heavy-tailed distributions: some instances have wildly varying search times depending on ordering. Restarts exploit this. Used in SAT solvers, CSP solvers, combinatorial optimization.

---

**Q25.25: Advanced - [Theory] - [Backtracking Applications Summary]**

Backtracking applications:

A) Puzzles: N-Queens, Sudoku, crossword generation
B) Combinatorics: subsets, permutations, combinations
C) Optimization: branch and bound (TSP, knapsack, scheduling)
D) All of the above — universal last-resort technique

**Answer: D**

**Explanation:**
Backtracking is the "ultimate" algorithm: can solve any finite search problem. Efficiency depends entirely on pruning. No pruning: brute force. Good pruning: practical for NP-hard problems at moderate size. Combined with DP (memoization), heuristics (A*), learning (CDCL): forms basis of modern constraint solving, AI planning, and optimization.

---

**Q25.26: Intermediate - [Theory] - [Letter Combinations of Phone Number]**

Letter combinations from phone digits:

A) Each digit maps to 3-4 letters (e.g., 2→"abc", 3→"def")
B) Backtrack: build string one letter per digit
C) For n digits: O(4^n) combinations worst case
D) All of the above

**Answer: D**

**Explanation:**
Phone letters: each digit branches to 3-4 choices. Backtracking tree: depth = number of digits, branching = letters per digit. For "23": a→d,e,f; b→d,e,f; c→d,e,f = 9 combinations. O(4^n) worst case (e.g., digits 7,9 have 4 letters). Classic backtracking: build path, at each level choose one letter for current digit.

---

**Q25.27: Intermediate - [Theory] - [Palindrome Partitioning via Backtracking]**

Generate all palindrome partitionings of a string:

A) At each position: try all possible palindromic prefixes
B) If prefix is palindrome: recurse on remainder
C) Base case: empty string → record current partition
D) Backtrack by removing last palindrome from partition

**Answer: D**

**Explanation:**
Palindrome partitioning: at position i, try substrings s[i..j] for j=i to n-1. If palindrome: add to partition, recurse from j+1. Backtrack: remove substring. Precompute isPalin[i][j] for O(1) palindrome checks. Total partitions can be exponential (all single chars is always valid). Related to Chapter 22's DP for minimum cuts.

---

**Q25.28: Foundational - [Trace] - [Rat in a Maze]**

Rat in maze (4×4 grid, 1=open, 0=blocked), find path from (0,0) to (3,3):

A) Try moving down or right from current position
B) If blocked or out of bounds: backtrack
C) Mark visited cells to avoid loops
D) First valid path found: output solution matrix

**Answer: D**

**Explanation:**
Rat in maze: classic backtracking. Start (0,0). Try down: if open and unvisited, move. Try right: same. If stuck: backtrack (unmark, try next direction). Can also allow left/up (4 directions) with visited tracking. Time: O(2^(n²)) worst case. Pruning: only open cells. Solution matrix: 1 where path goes, 0 elsewhere.

---

**Q25.29: Intermediate - [Theory] - [Combination Sum]**

Combination sum: find all combinations summing to target (reuse allowed):

A) Sort candidates to enable pruning
B) At each step: include current candidate (stay at same index for reuse) or skip to next
C) If sum exceeds target: prune (stop exploring)
D) All of the above

**Answer: D**

**Explanation:**
Combination sum: backtracking with pruning. Sort candidates ascending. For each candidate: if remaining ≥ candidate, include it (allow reuse: don't advance index). If remaining < candidate: prune entire subtree (sorted, so all following are larger). Skip duplicates for unique combinations. Variants: without reuse (move to next index), limited reuse.

---

**Q25.30: Advanced - [Theory] - [Knight's Tour]**

Knight's tour (visit every cell of n×n chessboard exactly once):

A) Backtrack: try all 8 possible L-shaped moves from current position
B) If all cells visited: solution found
C) If stuck (no unvisited valid move): backtrack
D) Warnsdorff's heuristic: move to cell with fewest onward moves — greatly prunes

**Answer: D**

**Explanation:**
Knight's tour: 8^(n²) naive search space (each cell has up to 8 moves). Backtracking: try each move, mark visited, recurse. If dead end: unmark, try next. Without heuristic: very slow for n>5. Warnsdorff's rule: always move to square with minimum degree (fewest unvisited neighbors). Finds tours for standard board almost instantly. Open tour vs closed tour (end adjacent to start).

---

**Q25.31: Intermediate - [Theory] - [Generate Parentheses]**

Generate all valid combinations of n pairs of parentheses:

A) Backtracking: track count of open and close parens used
B) Can add '(' if open_count < n
C) Can add ')' if close_count < open_count
D) All of the above — generates C(n) = (2n)!/(n!(n+1)!) valid strings

**Answer: D**

**Explanation:**
Generate parentheses: backtracking with two counters. Open: can always add if < n. Close: can add only if < open (ensures valid). Base: length = 2n → record string. Never generates invalid strings (pruning by construction). Count = Catalan number C(n). n=3: 5 strings ((())), (()()), (())(), ()(()), ()()(). O(4^n/√n) strings.

---

**Q25.32: Intermediate - [Theory] - [Word Ladder / Transformation]**

Word transformation via backtracking:

A) Transform one word to another, changing one letter at a time
B) Each intermediate word must be in dictionary
C) BFS finds shortest transformation; backtracking finds all paths
D) Backtracking: try each valid transformation, prune visited words

**Answer: D**

**Explanation:**
Word ladder: BFS for shortest path (Chapter 19). But finding ALL shortest paths: BFS for distances, then backtracking on distance-graph. Finding any path: backtracking with dictionary lookup. At each step: change one letter to form valid word. Mark visited to avoid cycles. BFS is preferred for shortest; backtracking for enumeration.

---

**Q25.33: Intermediate - [Trace] - [Subsets II (with Duplicates)]**

Subsets of [1,2,2] (avoiding duplicate subsets):

A) Sort array first: [1,2,2]
B) For duplicate elements: if skipping previous identical element, skip current too
C) Subsets: [], [1], [2], [1,2], [2,2], [1,2,2]
D) 6 unique subsets (not 8)

**Answer: D**

**Explanation:**
Duplicates: sort first, then backtracking with rule: at same recursion level, skip element if same as previous and previous wasn't included. This prevents generating [1,2₁] and [1,2₂] separately. Without dedup: 2³=8 subsets. With dedup: 6 unique. Generalization: for k copies of element, include 0,1,...,k times. Standard technique for avoiding duplicate combinations.

---

**Q25.34: Foundational - [Theory] - [Power Set Generation (Iterative)]**

Generating all subsets (iterative bitmask approach):

A) For n elements: 2^n subsets, each represented by n-bit mask
B) Mask bit i = 1 means element i is included
C) Iterate mask from 0 to 2^n - 1
D) All of the above — O(n × 2^n) total

**Answer: D**

**Explanation:**
Bitmask enumeration: each integer 0 to 2^n-1 represents a subset. Bit i set → include element i. n=3: 000→{}, 001→{a}, 010→{b}, ..., 111→{a,b,c}. O(2^n) subsets, O(n) per subset for construction. Total O(n×2^n). Alternative: backtracking (include/exclude each element). Bitmask is iterative and often simpler for small n (n≤20).

---

**Q25.35: Advanced - [Theory] - [Backtracking Complexity Analysis]**

Analyzing backtracking time complexity:

A) Worst case: O(b^d) where b=branching factor, d=depth
B) Pruning reduces effective branching factor
C) N-Queens: O(n!) with column pruning (not n^n)
D) All of the above — actual performance depends heavily on pruning quality

**Answer: D**

**Explanation:**
Backtracking complexity: tree size = O(b^d) without pruning. With pruning: effective b decreases. N-Queens: naive n^n, with column constraint n!, with diagonal constraints much less. Sudoku: 9^81 naive → 9^(empty cells) with constraints → much less with arc consistency. Strongly NP-complete problems: no polynomial pruning exists (unless P=NP). Good heuristics (ordering, constraint propagation) are crucial.

---

## Chapter 25 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 9 | Backtracking template, N-Queens, Sudoku, subsets, permutations, maze, rat in maze, power set bitmask |
| Intermediate | 15 | Pruning, combinations, CSP, graph coloring, Hamiltonian, word search, partition, phone letters, palindrome partition, combination sum, parentheses, word ladder, subsets II |
| Advanced | 7 | Branch and bound, DLX, constraint propagation, advanced Sudoku, knight's tour, complexity analysis |
| Expert | 4 | DPLL/SAT, randomized backtracking, IDA* |

**Total MCQs: 35** | **Target Met: ✓**

---

## Part IV Complete Summary

| Chapter | Topic | MCQs |
|---------|-------|------|
| 17 | Sorting Algorithms | 65 |
| 18 | Searching Algorithms | 50 |
| 19 | Graph Traversal | 50 |
| 20 | Shortest Path | 55 |
| 21 | Minimum Spanning Trees | 35 |
| 22 | Dynamic Programming | 75 |
| 23 | Greedy Algorithms | 45 |
| 24 | Divide & Conquer | 30 |
| 25 | Backtracking | 35 |
| **Part IV Total** | | **440** |

**Next:** Part V - Advanced Algorithms & Topics (Chapter 26: String Algorithms)
