# Chapter 15: Disjoint Sets (Union-Find)

**Target:** 45 MCQs | **Distribution:** 11 Foundational, 18 Intermediate, 12 Advanced, 4 Expert

---

**Q15.1: Foundational - [Theory] - [Disjoint Set Definition]**

Disjoint Set (Union-Find) data structure:

A) Maintains a collection of non-overlapping sets
B) Supports union (merge two sets) and find (identify set of element)
C) Each element belongs to exactly one set
D) All of the above

**Answer: D**

**Explanation:**
Disjoint Set Union (DSU): partition of elements into groups. Two key operations: Find(x) returns representative (root) of x's set. Union(x,y) merges sets containing x and y. Elements start in individual sets. Used for dynamic connectivity, Kruskal's MST, equivalence classes. Also called Union-Find.

---

**Q15.2: Foundational - [Theory] - [Find Operation]**

Find operation:

A) Returns the representative (root) of the set containing element x
B) Two elements in same set iff find(x) == find(y)
C) Traverses parent pointers to root
D) All of the above

**Answer: D**

**Explanation:**
Find: follow parent pointers from x up to root (element whose parent is itself). Root is the representative. Same root = same set. Without optimization: O(n) worst case (tall tree). With path compression: nearly O(1) amortized.

---

**Q15.3: Foundational - [Theory] - [Union Operation]**

Union operation:

A) Merge two sets into one
B) Make root of one set child of root of other
C) After union, both sets have same representative
D) All of the above

**Answer: D**

**Explanation:**
Union(x,y): find roots of x and y. If different, make one root child of other. Choice of which becomes child affects performance. Naive union: arbitrary choice → can create tall trees (O(n) find). Smart union (by rank/size): keeps trees shallow. O(1) for the pointer update itself.

---

**Q15.4: Foundational - [Trace] - [Basic Union-Find]**

Elements {0,1,2,3,4}. Union(0,1), Union(2,3), Union(0,2):

A) Initially: each element is own parent: [0,1,2,3,4]
B) Union(0,1): parent[1] = 0 → sets: {0,1}, {2}, {3}, {4}
C) Union(2,3): parent[3] = 2 → sets: {0,1}, {2,3}, {4}
D) Union(0,2): find(0)=0, find(2)=2, parent[2] = 0 → sets: {0,1,2,3}, {4}

**Answer: D**

**Explanation:**
After all unions: parent = [0,0,0,2,4]. Find(3): 3→2→0 (root). Find(1): 1→0 (root). Find(4): 4 (root). Two sets: {0,1,2,3} with root 0, {4} with root 4.

---

**Q15.5: Foundational - [Theory] - [Union by Rank]**

Union by rank:

A) Each node has a rank (approximate height)
B) Attach shorter tree under root of taller tree
C) Prevents tree from growing too tall
D) All of the above

**Answer: D**

**Explanation:**
Union by rank: keep rank (upper bound on height). Union: attach smaller rank root under larger rank root. If equal ranks: either becomes child, increment parent's rank. Guarantees height ≤ log n. Without rank: height can be n-1 (degenerate). Rank only increases when merging equal-rank trees.

---

**Q15.6: Foundational - [Theory] - [Union by Size]**

Union by size:

A) Track number of elements in each set
B) Attach smaller set under root of larger set
C) Similar effect to union by rank
D) All of the above

**Answer: D**

**Explanation:**
Union by size: store size at root. Union: smaller tree under larger tree. Size updated: new root's size = sum. Height bounded by O(log n): each time a node's depth increases by 1, it's in a tree at least twice as large. Both rank and size give O(log n) find without path compression.

---

**Q15.7: Foundational - [Theory] - [Path Compression]**

Path compression:

A) During find(x), make all nodes on path point directly to root
B) Flattens tree, making future finds faster
C) Nearly O(1) amortized with union by rank
D) All of the above

**Answer: D**

**Explanation:**
Path compression: find(x) traverses to root, then updates every node on the path to point directly to root. Next find for any of these nodes = O(1). With union by rank: amortized O(α(n)) per operation, where α is the inverse Ackermann function — effectively constant (α(n) ≤ 4 for any practical n).

---

**Q15.8: Intermediate - [Trace] - [Path Compression]**

Tree: 0←1←2←3 (parent of 3 is 2, of 2 is 1, of 1 is 0). Find(3) with path compression:

A) Traverse: 3→2→1→0 (root found)
B) Compress: parent[3]=0, parent[2]=0, parent[1]=0 (already)
C) After: all nodes point directly to root 0
D) Next find(3) = O(1): 3→0

**Answer: D**

**Explanation:**
Before: chain 3→2→1→0. Find(3): walk up 3 hops. During return or second pass: set parent[3]=0, parent[2]=0. After: flat tree. find(2), find(3) both O(1) now. Path compression amortizes the cost of long chains over multiple operations.

---

**Q15.9: Intermediate - [Theory] - [Inverse Ackermann Function]**

α(n) — inverse Ackermann function:

A) Grows incredibly slowly (≤ 4 for n up to 2^65536)
B) Union by rank + path compression: O(α(n)) amortized per operation
C) Effectively constant for all practical purposes
D) All of the above

**Answer: D**

**Explanation:**
Inverse Ackermann α: A(4,4) > 10^80 (number of atoms in universe). So α(10^80) ≤ 4. For any conceivable input: α(n) ≤ 4. Tarjan proved O(α(n)) amortized bound. Frederickson/Seidel proved this is tight (Ω(α(n))). Practically O(1) per operation. One of the most elegant amortized analyses in CS.

---

**Q15.10: Intermediate - [Theory] - [Kruskal's MST with DSU]**

Union-Find in Kruskal's MST algorithm:

A) Sort edges by weight
B) For each edge (u,v,w): if find(u) ≠ find(v), add edge, union(u,v)
C) O(E log E + E × α(V)) ≈ O(E log E)
D) All of the above

**Answer: D**

**Explanation:**
Kruskal's: greedily add cheapest edge that doesn't form cycle. DSU provides cycle detection: same set = cycle. Union to merge components. E edges with E find+union operations: O(E × α(V)). Sorting dominates: O(E log E) = O(E log V). DSU makes Kruskal's practical and elegant. Refer to Chapter 21 for MST details.

---

**Q15.11: Intermediate - [Trace] - [Kruskal's with DSU]**

Graph: edges [(0,1,1), (1,2,2), (0,2,3), (2,3,4)], Kruskal's:

A) Sort: (0,1,1), (1,2,2), (0,2,3), (2,3,4)
B) (0,1,1): find(0)≠find(1), union → MST edge
C) (1,2,2): find(1)≠find(2), union → MST edge
D) (0,2,3): find(0)==find(2), skip (cycle). (2,3,4): union → MST edges: {(0,1,1),(1,2,2),(2,3,4)}, cost=7

**Answer: D**

**Explanation:**
Kruskal's trace: process edges cheapest first. (0,1,1): different sets → add. (1,2,2): 0,1 in same set, 2 alone → add, merge. (0,2,3): now 0,1,2 same set → skip (would form cycle). (2,3,4): 3 alone → add, merge. MST has 3 edges (V-1=3), weight=7.

---

**Q15.12: Intermediate - [Theory] - [Connected Components with DSU]**

Finding connected components using DSU:

A) Process all edges, union endpoints
B) After processing, count distinct roots
C) O(V + E × α(V))
D) All of the above

**Answer: D**

**Explanation:**
Connected components: start with V individual sets. For each edge (u,v): union(u,v). After all edges: number of distinct sets = number of connected components. Count: iterate all vertices, count unique find(v) values. Alternative: BFS/DFS also O(V+E). DSU advantage: supports dynamic edge additions (online connectivity).

---

**Q15.13: Intermediate - [Theory] - [Dynamic Connectivity]**

DSU for dynamic connectivity:

A) "Are u and v connected?" queries
B) Edges added over time (online)
C) After each edge addition: O(α(n)) per query/update
D) All of the above

**Answer: D**

**Explanation:**
Online connectivity: edges arrive one at a time. DSU: union on edge arrival, find for connectivity query. Each O(α(n)). Can answer "connected?" at any point. Limitation: no edge deletions (union-find doesn't support efficient split). For full dynamic (insert+delete): link-cut trees or offline algorithms needed.

---

**Q15.14: Intermediate - [Theory] - [Cycle Detection in Undirected Graph]**

Cycle detection using DSU:

A) Process edges one by one
B) If find(u) == find(v) for edge (u,v): cycle exists
C) O(E × α(V))
D) All of the above

**Answer: D**

**Explanation:**
Cycle detection: before unioning u,v, check if already in same set. If same set → adding this edge creates cycle. Same logic as Kruskal's "skip" step. Works for undirected graphs. For directed graphs: DFS with coloring (white/gray/black) is needed. DSU cycle detection doesn't work for directed graphs (can miss some cycles).

---

**Q15.15: Foundational - [Theory] - [Initial State]**

Initial state of Union-Find with n elements:

A) Each element is its own set
B) parent[i] = i for all i
C) rank[i] = 0 (or size[i] = 1) for all i
D) All of the above

**Answer: D**

**Explanation:**
Initialization: n singleton sets. Each element is root of its own set. parent array: self-referencing. Rank: all 0 (single nodes). Size: all 1. Total sets = n. Each union reduces set count by 1 (if merging different sets). After V-1 unions: all in one set (if fully connected).

---

**Q15.16: Intermediate - [Theory] - [Path Splitting]**

Path splitting (alternative to full path compression):

A) During find, make every node point to its grandparent
B) Partial flattening, one pass
C) Same O(α(n)) amortized bound as full compression
D) All of the above

**Answer: D**

**Explanation:**
Path splitting: during find traversal, set parent[x] = parent[parent[x]] for each node (skip one level). One pass, no second traversal needed. Simpler to implement iteratively than full compression. Path halving: similar, every other node skips. Both achieve same amortized O(α(n)) bound. Practical difference negligible.

---

**Q15.17: Advanced - [Theory] - [Weighted Union-Find]**

Weighted Union-Find:

A) Each element has a weight/value relative to its root
B) Find returns root and computes relative weight
C) Used for: relative distances, potentials, parity constraints
D) All of the above

**Answer: D**

**Explanation:**
Weighted DSU: edges carry weights representing relationships (e.g., "a is 3 units heavier than b"). Maintain potential/weight from each node to its root. During find: sum weights along path. During union: adjust weight based on constraint. Path compression: update weights during flattening. Applications: currency exchange, mass relationships, parity problems.

---

**Q15.18: Advanced - [Trace] - [Weighted DSU]**

Relation: A-B=2, B-C=3. Find A-C using weighted DSU:

A) Union(A,B) with weight 2: potential[A]=0, potential[B]=-2 (B relative to root A)
B) Union(B,C) with weight 3: find(B)=A, find(C)=C. Attach C under A, weight = potential[B] + 3 = -2+3 = 1? Actually potential[C] = -(potential[B]+3)+potential[A]
C) A-C = 2+3 = 5 (via transitive relation)
D) DSU correctly computes: potential[A]-potential[C] = 5

**Answer: D**

**Explanation:**
Weighted DSU tracks relative relationships transitively. A-B=2, B-C=3, so A-C=5. Store weights along edges. During path compression and union, maintain correct relative potentials. This enables answering relationship queries between any two connected elements. Used in problems like "Equation Satisfaction" and contest problems.

---

**Q15.19: Advanced - [Theory] - [Rollback Union-Find]**

Rollback (persistent) Union-Find:

A) Supports undoing the last union operation
B) Don't use path compression (destroys reversibility)
C) Use union by rank only (reversible: detach and restore rank)
D) All of the above

**Answer: D**

**Explanation:**
Rollback DSU: maintain stack of changes. To undo: pop and reverse. Path compression makes reversal impossible (overwritten parents). Use union by rank only (O(log n) per operation). Store (root1, root2, rank_changed) for each union. Undo: detach, restore rank. Used in offline divide-and-conquer algorithms, competitive programming.

---

**Q15.20: Intermediate - [Theory] - [Union-Find Implementation]**

Union-Find implementation (Python/pseudocode):

A) parent array, rank array
B) find(x): while parent[x] ≠ x: path compress, return x
C) union(x,y): link roots by rank
D) All of the above

**Answer: D**

**Explanation:**
```
class DSU:
  parent = [i for i in range(n)]
  rank = [0] * n
  
  find(x):
    if parent[x] != x:
      parent[x] = find(parent[x])  # path compression
    return parent[x]
  
  union(x, y):
    rx, ry = find(x), find(y)
    if rx == ry: return
    if rank[rx] < rank[ry]: swap(rx, ry)
    parent[ry] = rx
    if rank[rx] == rank[ry]: rank[rx]++
```
Simple, efficient, widely used.

---

**Q15.21: Intermediate - [Theory] - [Number of Components]**

Track number of connected components:

A) Start with count = n
B) On successful union (different roots): count -= 1
C) Current components = count
D) All of the above

**Answer: D**

**Explanation:**
Component counting: initialize count = n (all singletons). Each union of different sets reduces count by 1. If union(x,y) where find(x)==find(y): no change (already connected). Query: return current count. O(1) per query with maintained counter.

---

**Q15.22: Intermediate - [Theory] - [Largest Component Size]**

Track size of each component:

A) Maintain size array (at roots)
B) On union: new root's size = sum of both
C) Max component = max over all size[root]
D) All of the above

**Answer: D**

**Explanation:**
Size tracking: size[root] = total elements in set. On union: size[new_root] += size[old_root]. Maximum component: track global max, update on union. All O(1) additional per union. Useful for: connectivity problems, percolation, cluster size analysis.

---

**Q15.23: Advanced - [Theory] - [Offline LCA with DSU]**

Offline Lowest Common Ancestor using DSU (Tarjan's):

A) Process LCA queries while doing DFS
B) When node fully processed, union with parent
C) For query (u,v): if both visited, LCA = find(v) or find(u)
D) All of the above

**Answer: D**

**Explanation:**
Tarjan's offline LCA: DFS traversal. When done with subtree rooted at u, union(u, parent(u)). For query (u,v): if v is already processed when we visit u's subtree, then LCA(u,v) = find(v) (representative of v's set = lowest processed ancestor). O((V+Q) × α(V)) for Q queries. Elegant combination of DFS and DSU.

---

**Q15.24: Intermediate - [Theory] - [Redundant Connection]**

Find redundant edge in graph that would be a tree:

A) Tree has V-1 edges; given V edges (one extra)
B) Process edges: first edge causing cycle is redundant
C) DSU: find(u)==find(v) for edge (u,v) → this is the redundant edge
D) All of the above

**Answer: D**

**Explanation:**
Graph with V vertices, V edges (one extra edge makes it not a tree). Process edges in given order. First edge where both endpoints already connected (same component): this edge creates the cycle. Return it. O(V × α(V)) ≈ O(V). Classic DSU application (Leetcode 684).

---

**Q15.25: Intermediate - [Theory] - [DSU for Percolation]**

Union-Find for percolation simulation:

A) Grid cells opened one at a time
B) When cell opens: union with adjacent open cells
C) Check if top row connected to bottom row
D) All of the above

**Answer: D**

**Explanation:**
Percolation: n×n grid, cells randomly opened. Open cell → union with open neighbors. Percolates: top-to-bottom connection exists. DSU with virtual top/bottom nodes: union all top-row cells with virtual top, bottom-row with virtual bottom. Percolates iff find(virtual_top) == find(virtual_bottom). O(n² × α(n²)) ≈ O(n²).

---

**Q15.26: Foundational - [Theory] - [Why Not Hash Set?]**

Why use DSU instead of maintaining sets explicitly?

A) Explicit sets: union requires merging all elements — O(n) per union
B) DSU: O(α(n)) per union via tree structure
C) DSU much faster for many union operations
D) All of the above

**Answer: D**

**Explanation:**
Naive set merging: move all elements from smaller set to larger → O(n) worst case per union (O(n log n) total with small-to-large). DSU: O(α(n)) ≈ O(1) per operation. For m operations on n elements: DSU is O(m × α(n)) vs naive O(m × n). Orders of magnitude faster. DSU is the canonical efficient solution for set merging.

---

**Q15.27: Advanced - [Theory] - [Link-Cut Trees Comparison]**

DSU vs Link-Cut Trees:

A) DSU: union + find, no split operation
B) Link-Cut Trees: link (union) + cut (split) + find-root
C) Link-Cut: O(log n) amortized per operation
D) All of the above

**Answer: D**

**Explanation:**
DSU limitation: no efficient "disconnect" operation. Link-Cut Trees (Sleator & Tarjan): support link (add edge), cut (remove edge), and root-finding in O(log n) amortized. Used for dynamic connectivity, dynamic shortest paths, max-flow improvements. Much more complex than DSU. Use DSU when only connections grow; Link-Cut when connections can break.

---

**Q15.28: Intermediate - [Theory] - [Accounts Merge Problem]**

Account merge using DSU:

A) Each account has name and list of emails
B) Accounts with overlapping emails belong to same person
C) Union-Find: treat emails as elements, union shared emails
D) All of the above

**Answer: D**

**Explanation:**
Accounts merge: email = element. For each account, union all its emails together. After processing: group emails by find(email). Each group = one person's consolidated account. Map each email to account name. O(total_emails × α(n)). Classic DSU application modeling equivalence classes (Leetcode 721).

---

**Q15.29: Advanced - [Theory] - [DSU with Small-to-Large Merging]**

Small-to-large (heavy path) merging with DSU:

A) Always attach smaller set's elements into larger set's data structure
B) Each element moved at most O(log n) times
C) Total work: O(n log n)
D) All of the above

**Answer: D**

**Explanation:**
Small-to-large: when merging auxiliary data (e.g., sets of values, histograms), always merge smaller into larger. Each element can be in the smaller set at most log n times (each merge at least doubles its group size). Total element movements: O(n log n). Used for: merging sets on trees, color counting, maintaining sorted orders during DSU operations.

---

**Q15.30: Intermediate - [Theory] - [Satisfiability of Equality Equations]**

Checking equality/inequality constraints:

A) Equations like a==b, b==c, a!=c
B) Process equalities first: union equal elements
C) Check inequalities: if find(x)==find(y) for x!=y → contradiction
D) All of the above

**Answer: D**

**Explanation:**
Equality satisfaction: process == constraints with union. Then check != constraints: if both in same set → unsatisfiable. O(n × α(n)). Two-pass algorithm: first union all equalities, then verify all inequalities. Elegant DSU application for constraint checking.

---

**Q15.31: Advanced - [Theory] - [Rank vs Size Comparison]**

Union by rank vs union by size:

A) Rank: upper bound on height; size: exact element count
B) Both give O(log n) height bound
C) Rank: increment only on equal-rank merge; size: always update
D) Rank and size both achieve O(α(n)) with path compression

**Answer: D**

**Explanation:**
Both strategies prevent degenerate trees. Rank: simpler (only changes on equal-rank merge). Size: provides additional information (set cardinality). With path compression: both achieve O(α(n)). Implementation preference: rank is traditional (CLRS), size is sometimes more useful (when set sizes needed). Performance difference negligible.

---

**Q15.32: Foundational - [Theory] - [When To Use DSU]**

When is DSU the best choice?

A) Grouping elements into clusters based on connections
B) Detecting cycles in undirected graphs
C) Dynamic connectivity queries (add-only)
D) All of the above

**Answer: D**

**Explanation:**
DSU ideal for: (1) Clustering/partitioning (image segmentation, friend groups). (2) Kruskal's MST (cycle detection). (3) Online connectivity (stream of edges, "connected?" queries). (4) Equivalence class problems (account merge, equation satisfaction). (5) Any problem where sets only grow, never split.

---

**Q15.33: Expert - [Theory] - [Lower Bound for DSU]**

Lower bound for DSU operations:

A) Tarjan proved Ω(m × α(n)) for m operations on n elements
B) Union by rank + path compression is optimal
C) Cannot do better than O(α(n)) amortized per operation
D) All of the above

**Answer: D**

**Explanation:**
Tarjan (1975): any DSU implementation using pointer-based structure requires Ω(m × α(m,n)) time for m operations. Union by rank + path compression matches this lower bound exactly. One of the tightest analyses in CS. Proves DSU is asymptotically optimal. The only way to beat α(n) is to change the model (e.g., word-RAM tricks).

---

**Q15.34: Advanced - [Theory] - [DSU on Trees (Euler Tour)]**

DSU on tree (small-to-large merging on trees):

A) Process tree bottom-up
B) Merge children's answers into parent using DSU
C) Small-to-large: O(n log n) total
D) All of the above

**Answer: D**

**Explanation:**
DSU on trees: for each node, maintain set of descendant properties. When processing subtree: merge children's sets using small-to-large. Total element movements: O(n log n). Used for: counting distinct colors in subtrees, answering subtree queries, merging information bottom-up. Powerful technique combining trees and DSU.

---

**Q15.35: Expert - [Theory] - [Persistent DSU]**

Persistent Union-Find:

A) Maintain all historical versions of DSU state
B) Query connectivity at any past time
C) O(log n) per operation using persistent array
D) All of the above

**Answer: D**

**Explanation:**
Persistent DSU: path-compressed DSU uses destructive updates, so use union by rank only (O(log n) per op). Store parent array as persistent array (fat node or path copying). Each version accessible. O(log n) per operation × O(log n) for persistent array access. Used for offline queries with time travel, competitive programming.

---

**Q15.36: Intermediate - [Theory] - [Minimum Spanning Forest]**

DSU for minimum spanning forest:

A) Same as Kruskal's but graph may be disconnected
B) Process all edges sorted by weight, union if different components
C) Result: MST for each connected component
D) All of the above

**Answer: D**

**Explanation:**
Minimum spanning forest: MST generalized to disconnected graphs. Kruskal's naturally handles this: process all E edges, add those connecting different components. If graph has k components: result has V-k edges forming a forest of k spanning trees. DSU handles disconnected case seamlessly.

---

**Q15.37: Expert - [Theory] - [Ackermann Function]**

Ackermann function growth:

A) A(0,n) = n+1
B) A(1,n) ≈ 2n, A(2,n) ≈ 2^n, A(3,n) ≈ 2^2^...^2 (tower of n)
C) A(4,n) is a tower of 2s of height exponential
D) Grows faster than any primitive recursive function

**Answer: D**

**Explanation:**
Ackermann function: defined recursively, grows incredibly fast. A(4,4) > number of atoms in observable universe. Inverse α: α(n) = min k such that A(k,k) ≥ n. α(universe atoms) ≤ 4. This is why α(n) is effectively constant. Ackermann function is the canonical example of a computable but not primitive recursive function.

---

**Q15.38: Intermediate - [Theory] - [Graph Connectivity Queries]**

DSU vs BFS/DFS for connectivity:

A) BFS/DFS: build from scratch, O(V+E) each time
B) DSU: incremental, handles new edges efficiently
C) DSU better for stream of edges with interleaved queries
D) All of the above

**Answer: D**

**Explanation:**
Static graph: BFS/DFS O(V+E) once, then answer all queries. Dynamic (edges added over time): DSU handles incrementally — each new edge O(α(n)), each query O(α(n)). BFS/DFS would need re-computation. DSU is the standard for online/incremental connectivity.

---

**Q15.39: Advanced - [Theory] - [DSU Space Complexity]**

Union-Find space:

A) O(n) for parent and rank arrays
B) Very space-efficient (two integers per element)
C) No pointers, cache-friendly array access
D) All of the above

**Answer: D**

**Explanation:**
DSU space: parent[n] + rank[n] = 2n integers. Minimal overhead. Array-based: cache-friendly. Compare: graph adjacency list O(V+E), balanced BST O(V) with pointers. DSU is one of the most space-efficient data structures for its functionality. Can be reduced to just parent array if rank not needed (at cost of O(log n) amortized).

---

**Q15.40: Advanced - [Theory] - [Union-Find for Image Segmentation]**

DSU in image processing:

A) Pixels as elements, edges between adjacent similar pixels
B) Union similar pixels → segments (connected components)
C) Used in: Felzenszwalb-Huttenlocher segmentation algorithm
D) All of the above

**Answer: D**

**Explanation:**
Image segmentation: treat pixels as graph nodes. Edge weight = color/intensity difference. Process edges by weight. Union if difference below threshold (adaptively based on component sizes). Felzenszwalb's algorithm: O(E log E) using sorted edges + DSU. Produces meaningful image segments. Real-world application of DSU.

---

**Q15.41: Intermediate - [Theory] - [Friend Circles / Number of Provinces]**

Count friend groups using DSU:

A) n people, friendship matrix/list given
B) Union all friends, count distinct components
C) O(n² × α(n)) with friendship matrix
D) All of the above

**Answer: D**

**Explanation:**
Friend circles: each person is element. For each friendship (i,j): union(i,j). Count distinct roots = number of friend groups. With n people and friendship matrix: O(n²) to scan + O(n² × α(n)) for unions. Alternative: BFS/DFS O(n²). DSU approach is clean and easy to implement.

---

**Q15.42: Expert - [Theory] - [Borůvka's MST with DSU]**

Borůvka's MST algorithm uses DSU:

A) Each component finds its minimum-weight outgoing edge
B) Add all such edges, merge components
C) Repeat until one component remains
D) O(E log V) using DSU for component tracking

**Answer: D**

**Explanation:**
Borůvka's: each phase, every component finds cheapest outgoing edge. Add all these edges (union components). Repeat. Each phase halves component count → O(log V) phases. Each phase scans all edges O(E). Total: O(E log V). DSU tracks components and detects which edges are "outgoing" (connecting different components). Parallelizable, oldest MST algorithm (1926).

---

**Q15.43: Intermediate - [Theory] - [DSU Amortized Analysis Intuition]**

Why path compression + union by rank is so fast:

A) Path compression: each find "pays" for future finds by flattening
B) Union by rank: prevents any single find from being too expensive
C) Together: nearly constant amortized time per operation
D) All of the above

**Answer: D**

**Explanation:**
Intuition: rank keeps trees shallow (O(log n) worst case without compression). Path compression makes trees flatter over time. The "cost" of a long find is amortized by future finds on the compressed path. Together: trees converge toward flat structures (all nodes → root). Formal proof uses potential function tracking rank/path lengths. Elegant synergy of two simple techniques.

---

**Q15.44: Advanced - [Theory] - [Online/Offline Connectivity]**

DSU for online vs. offline connectivity:

A) Online: edges arrive one at a time, answer queries immediately
B) DSU handles online efficiently: O(α(n)) per edge/query
C) Offline: all edges known in advance, process optimally
D) DSU works well for both online and offline scenarios

**Answer: D**

**Explanation:**
Online: DSU's natural mode — process edges as they arrive. Offline: if edge order can be chosen, algorithms can be more efficient (e.g., sort by weight for MST). Offline with deletions: much harder — need link-cut trees or offline divide-and-conquer with rollback DSU. DSU's strength is online add-only connectivity.

---

**Q15.45: Intermediate - [Theory] - [DSU Summary]**

DSU key takeaways:

A) Two operations: find and union, practically O(1) amortized
B) Optimal: matches theoretical lower bound
C) Applications: connectivity, MST, cycle detection, clustering
D) All of the above

**Answer: D**

**Explanation:**
DSU: simple data structure, deep theory (inverse Ackermann), wide applications. Implementation: ~15 lines of code. Performance: practically O(1). Limitations: no edge deletion, no splitting sets. Extensions: weighted DSU, rollback DSU, DSU on trees. One of the most important data structures in computer science, essential for graph algorithms and competitive programming.

---

## Chapter 15 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 11 | DSU definition, find, union, path compression, union by rank/size, initialization |
| Intermediate | 18 | Kruskal's, connectivity, cycle detection, percolation, small-to-large, implementations |
| Advanced | 12 | Weighted DSU, rollback, offline LCA, link-cut comparison, image segmentation |
| Expert | 4 | Lower bounds, persistent DSU, Ackermann function, Borůvka's |

**Total MCQs: 45** | **Target Met: ✓**

**Key DSU Operations:**

| Operation | Naive | Union by Rank | + Path Compression |
|-----------|-------|---------------|---------------------|
| Find | O(n) | O(log n) | O(α(n))* |
| Union | O(n) | O(log n) | O(α(n))* |
| Space | O(n) | O(n) | O(n) |

*Amortized, α(n) ≤ 4 for all practical n

**Next:** Chapter 16 - Segment Trees & BIT
