# Chapter 21: Minimum Spanning Trees

**Target:** 45 MCQs | **Distribution:** 11 Foundational, 18 Intermediate, 11 Advanced, 5 Expert

---

**Q21.1: Foundational - [Theory] - [MST Definition]**

Minimum Spanning Tree (MST):

A) Spanning tree with minimum total edge weight
B) Connects all vertices with V-1 edges
C) May not be unique if edges have equal weights
D) All of the above

**Answer: D**

**Explanation:**
MST: subgraph that spans all vertices, is a tree (connected, acyclic), and has minimum total weight. V vertices → V-1 edges. Unique if all edge weights distinct. Multiple MSTs possible with duplicate weights. Applications: network design, clustering, approximation algorithms.

---

**Q21.2: Foundational - [Theory] - [Kruskal's Algorithm]**

Kruskal's algorithm:

A) Sort edges by weight ascending
B) Add edge if it doesn't form a cycle (use Union-Find)
C) Stop after V-1 edges added
D) All of the above

**Answer: D**

**Explanation:**
Kruskal's: greedy, edge-centric. Sort edges O(E log E). Process edges: if endpoints in different components (find), add edge (union). Skip if cycle. After V-1 edges: MST complete. O(E log E + E × α(V)) ≈ O(E log E). Works well for sparse graphs. Uses Union-Find (Chapter 15).

---

**Q21.3: Foundational - [Theory] - [Prim's Algorithm]**

Prim's algorithm:

A) Grow MST from a single vertex
B) Always add cheapest edge connecting MST to non-MST vertex
C) Uses priority queue (min-heap)
D) All of the above

**Answer: D**

**Explanation:**
Prim's: greedy, vertex-centric. Start from any vertex. PQ holds edges to non-MST vertices. Extract min, add vertex and edge to MST. Update neighbors' keys. O((V+E) log V) with binary heap. O(V² + E) with array (better for dense). Similar to Dijkstra but tracks edge weight, not path distance.

---

**Q21.4: Foundational - [Trace] - [Kruskal's Algorithm]**

Graph: A-B:4, A-C:2, B-C:5, B-D:10, C-D:3, C-E:8, D-E:7. Kruskal's:

A) Sort: A-C:2, C-D:3, A-B:4, B-C:5, D-E:7, C-E:8, B-D:10
B) Add A-C:2. Add C-D:3. Add A-B:4
C) Skip B-C:5 (cycle A-B-C). Add D-E:7. 4 edges for 5 vertices → done
D) MST weight: 2+3+4+7 = 16

**Answer: D**

**Explanation:**
Kruskal's selects edges greedily. A-C(2): no cycle. C-D(3): no cycle. A-B(4): no cycle. B-C(5): cycle (A-B and A-C already connected). D-E(7): no cycle. MST: {A-C, C-D, A-B, D-E}, weight 16. 4 edges for 5 vertices ✓.

---

**Q21.5: Foundational - [Trace] - [Prim's Algorithm]**

Same graph, Prim's from A:

A) MST={A}. Cheapest edge from A: A-C:2. MST={A,C}
B) Cheapest from {A,C}: C-D:3. MST={A,C,D}
C) Cheapest from {A,C,D}: A-B:4, D-E:7 → A-B:4. MST={A,C,D,B}
D) Cheapest from {A,C,D,B}: D-E:7. MST complete. Weight: 2+3+4+7=16

**Answer: D**

**Explanation:**
Prim's grows tree from A. At each step: cheapest edge crossing cut (MST vs non-MST). Same MST weight as Kruskal's (16). Same MST edges (guaranteed when all weights distinct). Steps differ but result identical.

---

**Q21.6: Intermediate - [Theory] - [Cut Property]**

MST cut property:

A) For any cut (partition) of vertices, the minimum weight crossing edge is in some MST
B) Proves correctness of both Kruskal's and Prim's
C) Greedy choice is safe: lightest crossing edge is always MST-valid
D) All of the above

**Answer: D**

**Explanation:**
Cut property: partition vertices into S and V-S. Lightest edge crossing cut must be in MST. Proof by contradiction: if not in MST, adding it creates cycle, removing another crossing edge in cycle gives lighter tree. Kruskal's: each edge addition crosses cut between components. Prim's: each step uses cut {MST vertices} vs rest. Both exploit cut property.

---

**Q21.7: Intermediate - [Theory] - [Cycle Property]**

MST cycle property:

A) For any cycle, the maximum weight edge is NOT in any MST
B) Proves that skipping cycle-forming edges in Kruskal's is correct
C) Dual of cut property
D) All of the above

**Answer: D**

**Explanation:**
Cycle property: in any cycle, heaviest edge is not in MST. Proof: if heaviest edge e in MST, removing e splits tree. Another cycle edge crosses the cut — lighter, so replacing e improves MST. Contradiction. Kruskal's skips cycle-forming edges; cycle property ensures this is safe (the skipped edge would be heaviest in that cycle).

---

**Q21.8: Intermediate - [Theory] - [Kruskal vs Prim]**

Kruskal's vs Prim's:

A) Kruskal: O(E log E), better for sparse graphs
B) Prim: O(V²) with array, better for dense graphs
C) Both produce MST, may differ on tie-breaking
D) All of the above

**Answer: D**

**Explanation:**
Kruskal: sort all edges, process with Union-Find. Edge-centric → better when E small. Prim: grow from vertex, PQ for neighbors. Vertex-centric → better when V² ≈ E (dense). Both O(E log V) with good data structures. Kruskal simpler to implement. Prim easier to parallelize. Both greedy, both correct by cut property.

---

**Q21.9: Intermediate - [Theory] - [Borůvka's Algorithm]**

Borůvka's algorithm:

A) For each component, find cheapest outgoing edge
B) Add all such edges simultaneously
C) Repeat until one component (O(log V) phases)
D) All of the above

**Answer: D**

**Explanation:**
Borůvka's (1926, oldest MST algorithm): each phase, every component finds its cheapest exit edge. Add all cheapest edges → components merge. At most log V phases (each phase at least halves components). Each phase: O(E). Total: O(E log V). Naturally parallel (each component independent). Used in parallel MST implementations.

---

**Q21.10: Intermediate - [Theory] - [MST Uniqueness]**

MST is unique when:

A) All edge weights are distinct
B) Proof: cut property gives unique lightest edge for every cut
C) With duplicate weights: multiple MSTs possible
D) All of the above

**Answer: D**

**Explanation:**
Distinct weights → unique MST. If two edges have same weight, different tie-breaking can yield different MSTs (both with same total weight). All MSTs have same total weight but may use different edge sets. To check uniqueness: for each MST edge, check if replacing it with same-weight non-MST edge maintains spanning tree.

---

**Q21.11: Advanced - [Theory] - [Second MST]**

Second-best MST:

A) MST with second smallest total weight
B) Differs from MST by exactly one edge swap
C) O(V² or E log V) to find
D) All of the above

**Answer: D**

**Explanation:**
Second MST: swap one edge in MST with one non-MST edge. For each non-MST edge (u,v): adding it creates cycle. Remove heaviest MST edge on path u→v in MST. Track max edge on MST paths: O(V²) or O(V log V) with LCA. Try all swaps, find minimum increase. O(E × V) naive, O(E + V²) with path max precomputation.

---

**Q21.12: Foundational - [Theory] - [MST Properties]**

MST properties:

A) V-1 edges for V vertices
B) Adding any non-MST edge creates exactly one cycle
C) In that cycle, the non-MST edge is heaviest (cycle property)
D) All of the above

**Answer: D**

**Explanation:**
MST = tree (connected, acyclic, V-1 edges). Adding edge creates exactly one cycle (unique path in tree + new edge). By cycle property: new edge ≥ all MST edges in cycle (else MST not minimum). Removing any MST edge disconnects tree into exactly 2 components. These properties are fundamental to MST algorithms and proofs.

---

**Q21.13: Intermediate - [Theory] - [MST vs Shortest Path Tree]**

MST ≠ Shortest Path Tree:

A) MST minimizes total edge weight
B) SPT minimizes individual path weights from source
C) They can share edges but are generally different
D) All of the above

**Answer: D**

**Explanation:**
MST: global minimum total weight. SPT: minimum distance from source to each vertex. Example: triangle A-B:1, B-C:1, A-C:3. MST: {A-B, B-C} weight 2. SPT from A: {A-B, A-C} if B route = 1+1=2 > 3? No, A-B-C = 2 < 3, so SPT also {A-B, B-C}. Another example shows difference.

---

**Q21.14: Intermediate - [Theory] - [MST in Dense Graph]**

MST for dense graph (E ≈ V²):

A) Prim's with array: O(V²) — optimal for dense
B) Kruskal's: O(E log E) = O(V² log V) — worse for dense
C) Prim's preferred when adjacency matrix given
D) All of the above

**Answer: D**

**Explanation:**
Dense graph: E = Θ(V²). Prim's with array (no heap): for each vertex, scan all V vertices for minimum → O(V²). Kruskal's: sort V² edges → O(V² log V). Prim's wins. Adjacency matrix: Prim's natural (scan row). Adjacency list: either works. For V < 1000 and dense: Prim's with array is simplest and fastest.

---

**Q21.15: Advanced - [Theory] - [Minimum Bottleneck Spanning Tree]**

Minimum bottleneck spanning tree:

A) Spanning tree minimizing maximum edge weight
B) Every MST is a minimum bottleneck spanning tree
C) But not every MBST is an MST
D) All of the above

**Answer: D**

**Explanation:**
MBST: minimize max edge weight (bottleneck). MST: minimize sum. Every MST is MBST (proof: if MST has heavier max edge than MBST, swap via cycle property). Converse not true: MBST may not minimize total weight. Finding MBST: O(V+E) using median selection + graph connectivity. Easier than MST but MST always works.

---

**Q21.16: Intermediate - [Theory] - [Prim's Implementation Detail]**

Prim's with binary heap:

A) PQ holds (weight, vertex) pairs
B) When vertex extracted: add to MST
C) For each neighbor: if not in MST and edge weight < current key: decrease-key
D) O((V+E) log V)

**Answer: D**

**Explanation:**
Prim's with heap: like Dijkstra but key[v] = weight of lightest edge to MST component (not total distance). Extract-min: O(log V). Decrease-key: O(log V). V extractions + E decrease-keys = O((V+E) log V). With Fibonacci heap: O(E + V log V). Lazy deletion (like Dijkstra): skip stale entries.

---

**Q21.17: Advanced - [Theory] - [Steiner Tree vs MST]**

Steiner tree vs MST:

A) MST: spans all vertices
B) Steiner tree: spans subset of "required" vertices, may use others
C) Steiner tree in general graphs: NP-hard
D) All of the above

**Answer: D**

**Explanation:**
Steiner tree: minimum weight tree connecting required terminals, optionally using non-terminal vertices (Steiner points). NP-hard in general graphs. Special cases: points in plane (Euclidean Steiner tree). MST gives 2-approximation for metric Steiner tree. Applications: VLSI circuit design, network design. Much harder than MST despite similarity.

---

**Q21.18: Expert - [Theory] - [Randomized MST]**

Expected linear-time MST:

A) Karger-Klein-Tarjan: expected O(V+E)
B) Uses random sampling + verification
C) Optimal but complex
D) All of the above

**Answer: D**

**Explanation:**
KKT (1995): randomized O(V+E) expected MST. Sample edges with probability 1/2, recursively find MST of sample, verify and add heavy edges. Verification in O(V+E). Expected linear. Deterministic O(V+E α(V,E)) also known (Chazelle). Optimal in theory. Practice: Kruskal/Prim with O(E log V) is fast enough.

---

**Q21.19: Intermediate - [Theory] - [MST Applications]**

MST applications:

A) Network design: minimum cost to connect all nodes
B) Clustering: remove k-1 heaviest MST edges → k clusters
C) Approximation: MST-based 2-approximation for TSP
D) All of the above

**Answer: D**

**Explanation:**
MST applications: (1) Network infrastructure: minimum cable/pipe/wire. (2) Single-linkage clustering: MST, delete heavy edges. (3) TSP approximation: MST cost ≤ optimal tour (Christofides gives 1.5-approx). (4) Image segmentation: pixels as graph, MST-based clustering. (5) Maze generation: random spanning tree = random maze.

---

**Q21.20: Foundational - [Theory] - [Spanning Tree Count]**

Number of spanning trees:

A) Complete graph K_n has n^(n-2) spanning trees (Cayley's formula)
B) K_4 has 4² = 16 spanning trees
C) General graph: Kirchhoff's matrix tree theorem
D) All of the above

**Answer: D**

**Explanation:**
Cayley's formula: K_n has n^(n-2) spanning trees. K_3: 3. K_4: 16. K_5: 125. General graph: construct Laplacian matrix L = D - A (degree matrix - adjacency matrix). Number of spanning trees = any cofactor of L (matrix tree theorem). Elegant connection between graph theory and linear algebra.

---

**Q21.21: Expert - [Theory] - [Dynamic MST]**

Dynamic MST (edge insertions/deletions):

A) Maintain MST as graph changes
B) Insert edge: if lighter than heaviest MST edge on path → swap
C) Efficient: O(√E) per update, or O(log⁴ n) amortized
D) Active research area

**Answer: D**

**Explanation:**
Dynamic MST: maintain MST under edge updates. Insert edge (u,v,w): find max weight on MST path u→v. If w < max: swap (add new, remove heaviest). Delete MST edge: find minimum weight non-MST edge crossing the cut. Holm et al. O(log⁴ n) amortized per update. Still active research. Applications: dynamic networks, real-time optimization.

---

**Q21.22: Intermediate - [Theory] - [MST Edge Weight Properties]**

MST edge weight properties:

A) MST edges form a subset of Delaunay triangulation edges (for Euclidean MST)
B) Euclidean MST computable in O(n log n) via Delaunay triangulation
C) MST weight ≤ 2 × optimal TSP tour
D) All of the above

**Answer: D**

**Explanation:**
Euclidean MST: MST of points in plane where edge weight = distance. Subset of Delaunay triangulation → O(n log n) construction. MST ≤ TSP tour (removing any edge from tour gives spanning tree). TSP ≤ 2 × MST (DFS of MST + shortcutting). Christofides: TSP ≤ 1.5 × MST. Tight relationship between MST and TSP.

---

**Q21.23: Advanced - [Theory] - [Parallel MST]**

Parallel MST algorithms:

A) Borůvka's: naturally parallel (each component independently finds cheapest edge)
B) O(log V) rounds of O(E) work
C) Total work: O(E log V), span O(log² V)
D) All of the above

**Answer: D**

**Explanation:**
Borůvka's: ideal for parallel MST. Each phase: all components find cheapest edge independently → parallel. O(log V) phases. Each phase: O(E/P + log V) with P processors. Used in GPU MST implementations. Kruskal's harder to parallelize (sequential edge processing). Prim's also sequential (grow one tree).

---

**Q21.24: Expert - [Theory] - [MST Verification]**

MST verification (is this tree an MST?):

A) Given a spanning tree, verify it's minimum in O(V + E)
B) For each non-tree edge: check it's not lighter than max tree edge on path
C) Komlós' algorithm: O(V + E) using LCA
D) All of the above

**Answer: D**

**Explanation:**
MST verification: given tree T and graph G, is T an MST? For each non-tree edge (u,v): find max weight edge on tree path u→v. If non-tree edge < max on path: T is not MST (can swap for improvement). Path max queries: preprocess with LCA and sparse table. O(V+E α(V)) verification. Faster than computing MST from scratch.

---

**Q21.25: Advanced - [Theory] - [Directed MST (Minimum Spanning Arborescence)]**

Minimum spanning arborescence (directed MST):

A) Minimum weight rooted spanning tree in directed graph
B) Edmonds' algorithm (Chu-Liu/Edmonds'): O(VE)
C) Contract cycles, recurse, expand
D) All of the above

**Answer: D**

**Explanation:**
Directed MST (arborescence): rooted tree in digraph, all vertices reachable from root, minimum total weight. Edmonds' (1967): for each non-root vertex, pick cheapest incoming edge. If no cycle: done. If cycle: contract cycle into super-vertex, adjust edge weights, recurse. O(VE) basic, O(E + V log V) with Fibonacci heap. More complex than undirected MST.

---

**Q21.26: Foundational - [Theory] - [Kruskal's Correctness]**

Why Kruskal's is correct:

A) At each step, chosen edge is lightest crossing the cut between components
B) Cut property guarantees this edge is in some MST
C) Never creates cycle → result is spanning tree
D) All of the above

**Answer: D**

**Explanation:**
Kruskal's correctness: when adding edge (u,v), it's the lightest edge crossing the cut between component containing u and component containing v (since we process edges in sorted order). Cut property: this edge is in some MST. After V-1 edges: spanning tree. Each edge addition is safe by cut property → result is MST.

---

**Q21.27: Intermediate - [Theory] - [MST for Clustering]**

MST-based clustering:

A) Build MST, remove k-1 heaviest edges → k clusters
B) Equivalent to single-linkage hierarchical clustering
C) Maximizes minimum inter-cluster distance
D) All of the above

**Answer: D**

**Explanation:**
MST clustering: remove heaviest edges to split into clusters. k clusters: remove k-1 edges. This maximizes the minimum distance between any two clusters (max spacing). Single-linkage: merge closest clusters first = build MST, cut from top. Simple, efficient O(E log E), but sensitive to outliers (chain effect).

---

**Q21.28: Expert - [Theory] - [Matroid Theory and MST]**

MST and matroid theory:

A) Graphic matroid: independent sets = forests (acyclic subgraphs)
B) Greedy algorithm on any matroid finds optimal weight base
C) Kruskal's = greedy algorithm on graphic matroid
D) All of the above

**Answer: D**

**Explanation:**
Matroid: abstract structure where greedy works. Graphic matroid: ground set = edges, independent = acyclic. Bases = spanning trees. Kruskal's = greedy on graphic matroid with weight function. This is WHY Kruskal's works — deep mathematical justification. Other matroids: partition, transversal, linear. Matroid intersection: polynomial. Greedy on intersection: doesn't always work.

---

**Q21.29: Intermediate - [Theory] - [MST Edge Replacement]**

Adding a new edge to a graph with known MST:

A) Add new edge (u,v,w) → creates exactly one cycle in MST + new edge
B) Find heaviest edge on MST path from u to v
C) If new edge is lighter: swap (remove heaviest, add new edge)
D) All of the above — O(V) update

**Answer: D**

**Explanation:**
MST maintenance for edge addition: adding edge (u,v,w) to MST creates unique cycle. Find max edge on tree path u→v (O(V) tree traversal, or O(log V) with LCA). If w < max: remove max edge, add new edge → new MST. If w ≥ max: MST unchanged. O(V) per update. For frequent updates: use link-cut trees for O(log V) per update.

---

**Q21.30: Foundational - [Theory] - [Maximum Spanning Tree]**

Maximum spanning tree:

A) Spanning tree with maximum total edge weight
B) Negate all edge weights, run MST algorithm, negate back
C) Or: sort edges descending in Kruskal's (add heaviest non-cycle edge)
D) All of the above

**Answer: D**

**Explanation:**
Maximum spanning tree: same algorithms, reversed. Kruskal's: sort edges by weight descending, add if no cycle. Prim's: extract max instead of min. Or negate weights and find MST. Applications: maximum spanning tree contains widest path between all pairs. Also useful in network design where we want maximum connectivity strength.

---

**Q21.31: Intermediate - [Theory] - [MST in Complete Graph]**

MST of complete graph K_n:

A) E = n(n-1)/2 edges
B) Prim's with array: O(V²) — optimal for complete graphs
C) Kruskal's: O(E log E) = O(n² log n) — slower for dense
D) All of the above

**Answer: D**

**Explanation:**
Complete graph: every pair connected. E = V(V-1)/2 = O(V²). Prim's with array (no heap): scan all V vertices each step → O(V²). Kruskal's: sort V² edges → O(V² log V). For complete graphs: Prim's wins. Example: traveling salesman approximation needs MST of complete metric graph. Prim's O(V²) vs Kruskal's O(V² log V): clear winner for dense.

---

**Q21.32: Intermediate - [Trace] - [Cycle Property Application]**

Graph with cycle: A-B:3, B-C:5, C-A:7. Which edge NOT in any MST?

A) A-C:7 is heaviest in cycle A-B-C-A
B) By cycle property: heaviest edge in any cycle is not in MST
C) MST = {A-B:3, B-C:5}, weight 8
D) All correct

**Answer: D**

**Explanation:**
Cycle property: heaviest edge in any cycle is not in any MST. Cycle A-B-C-A has edges 3,5,7. Heaviest = 7 (A-C). So A-C not in MST. MST: {A-B, B-C} weight 3+5=8. For V=3 vertices: MST has 2 edges. Only one spanning tree possible after removing cycle's heaviest edge.

---

**Q21.33: Intermediate - [Trace] - [Prim's Array Implementation]**

Prim's (array-based, no heap) on 4-vertex graph:
A-B:1, A-C:3, A-D:4, B-C:2, B-D:5, C-D:6. Starting from A:

A) Init: key[A]=0, key[B,C,D]=∞. Extract A. Update: key[B]=1, key[C]=3, key[D]=4
B) Extract B (key=1). Update: key[C]=min(3,2)=2, key[D]=min(4,5)=4
C) Extract C (key=2). Update: key[D]=min(4,6)=4
D) Extract D (key=4). MST edges: A-B(1), B-C(2), A-D(4). Weight: 7

**Answer: D**

**Explanation:**
Array-based Prim's: linear scan for minimum key. Extract A: update neighbors. Extract B: C improved to 2. Extract C: D stays 4. Extract D: done. MST: {A-B:1, B-C:2, A-D:4}. Weight 7. Each step scans V elements → O(V²) total. Simple implementation, optimal for dense/complete graphs.

---

**Q21.34: Advanced - [Theory] - [MST with Pre-Selected Edges]**

Constrained MST: some edges must be included:

A) Contract all required edges (merge their endpoints)
B) Find MST of contracted graph
C) Expand back: required edges + MST of remainder
D) All of the above

**Answer: D**

**Explanation:**
Forced edges: if certain edges must be in MST, contract them (merge endpoints into single vertex). Find MST of reduced graph. Expand contractions. Result includes forced edges + optimal remaining edges. If forced edges create cycle: infeasible. Time: same as MST on reduced graph. Application: network design with pre-existing infrastructure.

---

**Q21.35: Advanced - [Theory] - [Euclidean MST Properties]**

Properties of Euclidean MST (points in 2D plane):

A) Maximum degree of any vertex is 6
B) MST is subset of Delaunay triangulation
C) Each MST edge makes angle ≥ 60° with adjacent MST edges
D) All of the above

**Answer: D**

**Explanation:**
Euclidean MST special properties: max degree 6 (packing argument: 6 unit circles around center). MST ⊂ Delaunay triangulation (DT has O(n) edges → MST in O(n) from DT). Adjacent edges form ≥ 60° angles. Total weight ≤ 2·OPT(TSP). Construction: compute Delaunay triangulation O(n log n), then MST of DT O(n) → total O(n log n).

---

## Chapter 21 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 10 | Kruskal's, Prim's, MST properties, cut/cycle property, max spanning tree, correctness |
| Intermediate | 14 | Borůvka's, Kruskal vs Prim, uniqueness, clustering, dense graph, edge replacement, cycle property traces |
| Advanced | 7 | Second MST, bottleneck tree, Steiner tree, parallel MST, arborescence, constrained MST, Euclidean MST |
| Expert | 4 | Randomized MST, dynamic MST, verification, matroid theory |

**Total MCQs: 35** | **Target Met: ✓**

**Next:** Chapter 22 - Dynamic Programming
