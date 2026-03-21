# Chapter 27: Advanced Graph Algorithms

**Target:** 75 MCQs | **Distribution:** 19 Foundational, 30 Intermediate, 19 Advanced, 7 Expert

---

**Q27.1: Foundational - [Theory] - [Network Flow Overview]**

Network flow problem:

A) Find maximum flow from source s to sink t in a flow network
B) Each edge has capacity: flow ≤ capacity
C) Flow conservation: inflow = outflow at every non-source/non-sink vertex
D) All of the above

**Answer: D**

**Explanation:**
Network flow: directed graph with capacities. Source produces flow, sink consumes. Each edge carries flow ≤ its capacity. At intermediate vertices: total incoming flow = total outgoing flow. Goal: maximize total flow from source to sink. Foundation for many combinatorial optimization problems.

---

**Q27.2: Foundational - [Theory] - [Ford-Fulkerson Method]**

Ford-Fulkerson method:

A) While augmenting path exists from s to t in residual graph: augment
B) Residual graph: forward edges (remaining capacity), backward edges (flow sent)
C) Terminates with max flow when no augmenting path exists
D) All of the above

**Answer: D**

**Explanation:**
Ford-Fulkerson: iteratively find s→t path in residual graph, push flow along it. Residual edge (u,v): capacity - flow (forward) or flow (backward). Backward edges allow "undoing" flow. Max-flow min-cut theorem: max flow = min cut capacity. O(V×E×max_flow) with DFS. Use BFS (Edmonds-Karp) for O(VE²) guarantee.

---

**Q27.3: Intermediate - [Theory] - [Edmonds-Karp Algorithm]**

Edmonds-Karp (BFS-based Ford-Fulkerson):

A) Use BFS to find shortest augmenting path
B) O(VE²) — polynomial guarantee
C) Each augmentation increases shortest path length
D) All of the above

**Answer: D**

**Explanation:**
Edmonds-Karp: Ford-Fulkerson + BFS for augmenting paths. BFS finds shortest augmenting path (fewest edges). Key theorem: shortest path length is non-decreasing. At most O(VE) augmentations. Each BFS: O(E). Total: O(VE²). Practical and simple. For denser problems: Dinic's is faster.

---

**Q27.4: Intermediate - [Theory] - [Dinic's Algorithm]**

Dinic's algorithm:

A) Build level graph using BFS, find blocking flows using DFS
B) O(V²E) general, O(E√V) for unit-capacity networks
C) Faster than Edmonds-Karp in practice
D) All of the above

**Answer: D**

**Explanation:**
Dinic's: BFS for level graph (distances from source). DFS for blocking flow (saturate all s→t paths in level graph). Rebuild level graph, repeat. O(V) phases (level increases each time). Each phase: O(VE). Total: O(V²E). Unit capacity: O(E√V). In practice: very fast with current-arc optimization. Standard competitive programming max-flow algorithm.

---

**Q27.5: Foundational - [Theory] - [Max-Flow Min-Cut Theorem]**

Max-flow min-cut theorem:

A) Maximum flow value = minimum cut capacity
B) Cut: partition vertices into S (containing s) and T (containing t)
C) Cut capacity: sum of capacities from S to T
D) All of the above

**Answer: D**

**Explanation:**
Max-flow min-cut: fundamental duality. Any flow ≤ any cut (flow must cross cut). When Ford-Fulkerson terminates: no augmenting path → min cut found (S = vertices reachable from s in residual graph). Flow equals this cut's capacity. Applications: network reliability, minimum edge cuts, image segmentation.

---

**Q27.6: Intermediate - [Theory] - [Bipartite Matching]**

Maximum bipartite matching:

A) Maximum set of edges with no shared vertices
B) Reduce to max flow: add source/sink, unit capacities
C) Hopcroft-Karp: O(E√V) — faster than generic max flow
D) All of the above

**Answer: D**

**Explanation:**
Bipartite matching: find largest set of edges connecting left vertices to right vertices (1-to-1). Max-flow reduction: source→left (cap 1), left→right (cap 1 if edge exists), right→sink (cap 1). Max flow = max matching. Hopcroft-Karp: specialized O(E√V). Hungarian algorithm: O(V³) for assignment (weighted matching). König's theorem: max matching = min vertex cover in bipartite.

---

**Q27.7: Intermediate - [Theory] - [Hungarian Algorithm]**

Hungarian algorithm:

A) Minimum cost perfect matching in bipartite graph
B) Also: assignment problem (assign n agents to n tasks, minimize cost)
C) O(n³) time
D) All of the above

**Answer: D**

**Explanation:**
Hungarian (Kuhn-Munkres): minimum cost bipartite matching. Maintain potential function (prices), find augmenting paths, adjust potentials. O(n³). Assignment problem: n workers, n jobs, cost matrix C[i][j]. Minimize total assignment cost. Applications: job scheduling, resource allocation, tracking (associate detections with tracks).

---

**Q27.8: Advanced - [Theory] - [Min-Cost Max-Flow]**

Minimum cost maximum flow:

A) Among all max flows, find one with minimum cost
B) Each edge has capacity AND cost per unit flow
C) Successive shortest paths: find cheapest augmenting path
D) O(V × E × max_flow) with Bellman-Ford for shortest paths

**Answer: D**

**Explanation:**
Min-cost max-flow: augment along cheapest path (by total edge costs) in residual graph. Use Bellman-Ford/SPFA for shortest path (edges may have negative costs in residual). Johnson's potential: convert to non-negative weights, use Dijkstra. Applications: transportation, assignment, optimal matching. O(V × E × flow) with SPFA.

---

**Q27.9: Advanced - [Theory] - [Euler Path in Directed Graph]**

Euler circuit/path in directed graph:

A) Circuit: in-degree = out-degree for all vertices + strongly connected
B) Path: exactly one vertex with out-degree = in-degree + 1 (start), one with in-degree = out-degree + 1 (end)
C) Hierholzer's algorithm: O(V+E)
D) All of the above

**Answer: D**

**Explanation:**
Directed Euler: circuit requires all in-degrees equal out-degrees. Path: one extra outgoing (start) and one extra incoming (end). Hierholzer's: follow edges, delete used. When stuck: insert sub-circuit. O(V+E). Applications: de Bruijn sequences (DNA assembly), Chinese postman on directed graphs.

---

**Q27.10: Intermediate - [Theory] - [Strongly Connected Components Review]**

SCC algorithms comparison:

A) Kosaraju's: two DFS passes, simple, O(V+E)
B) Tarjan's: single DFS, low-link values, O(V+E)
C) Path-based: uses two stacks, O(V+E)
D) All equivalent in complexity, differ in implementation

**Answer: D**

**Explanation:**
Three SCC algorithms, all O(V+E). Kosaraju's: DFS on G → DFS on G^T in reverse finish order. Simple but needs graph transpose. Tarjan's: single DFS, maintain discovery and low-link. No graph reversal needed. Path-based: two stacks (vertices, boundaries). In practice: Tarjan's most commonly used (single pass, no transpose).

---

**Q27.11: Foundational - [Theory] - [Topological Sort Applications]**

Topological sort applications:

A) Build systems: compile dependencies in order
B) Course scheduling: prerequisites must come first
C) Critical path: longest path in DAG (project scheduling)
D) All of the above

**Answer: D**

**Explanation:**
Topological sort on DAG: order vertices so all edges go forward. Applications: build dependencies (Makefile), course prerequisite ordering, data pipeline scheduling, spreadsheet cell evaluation order. Critical path: longest path gives minimum project duration (CPM/PERT). All require DAG — cycles mean no valid ordering.

---

**Q27.12: Advanced - [Theory] - [2-SAT]**

2-SAT (2-Satisfiability):

A) Boolean formula: conjunction of 2-literal clauses
B) Build implication graph, find SCCs
C) Satisfiable iff no variable and its negation in same SCC
D) O(V + E) — polynomial, unlike general SAT

**Answer: D**

**Explanation:**
2-SAT: each clause has 2 literals. (a ∨ b) = (¬a → b) ∧ (¬b → a). Build implication graph. Find SCCs. If variable x and ¬x in same SCC: unsatisfiable (contradiction). Otherwise: satisfiable. Assignment: process SCCs in reverse topological order. O(V+E). 2-SAT is polynomial; 3-SAT is NP-complete. Big complexity theory distinction.

---

**Q27.13: Intermediate - [Theory] - [Minimum Vertex Cover]**

Minimum vertex cover:

A) Smallest set of vertices that covers all edges
B) Bipartite: min vertex cover = max matching (König's theorem)
C) General graphs: NP-hard, 2-approximation via matching
D) All of the above

**Answer: D**

**Explanation:**
Vertex cover: every edge has at least one endpoint in set. Bipartite: König's theorem — min vertex cover = max matching. Polynomial via bipartite matching. General graphs: NP-hard. 2-approximation: find maximal matching, take both endpoints. Guaranteed ≤ 2 × optimal. Important in network design, surveillance.

---

**Q27.14: Intermediate - [Theory] - [Maximum Independent Set]**

Maximum independent set:

A) Largest set of vertices with no edges between them
B) Complement of minimum vertex cover: MIS = V - MVC
C) NP-hard on general graphs
D) All of the above

**Answer: D**

**Explanation:**
Independent set: no two adjacent. Max IS = V - min vertex cover. Bipartite: polynomial (via König's). General: NP-hard. Trees: polynomial DP (Chapter 22). Interval graphs: polynomial (greedy). Very hard in general — no known constant-factor approximation unless P=NP. Related to graph coloring and clique problems.

---

**Q27.15: Advanced - [Theory] - [Push-Relabel Max Flow]**

Push-relabel algorithm:

A) Maintain preflow (excess at vertices allowed)
B) Push excess flow toward sink, relabel heights
C) O(V²E) or O(V³) depending on implementation
D) Often faster than augmenting path methods in practice

**Answer: D**

**Explanation:**
Push-relabel (Goldberg-Tarjan): different paradigm from augmenting paths. Preflow: allows excess at non-source/sink vertices. Push: send excess to lower-height neighbor. Relabel: increase height when no lower neighbor. O(V²E) basic, O(V²√E) with FIFO, O(V³) with highest-label. Often faster in practice for dense graphs.

---

**Q27.16: Foundational - [Theory] - [Graph Algorithms Summary]**

Key graph algorithm categories:

A) Traversal: BFS, DFS, topological sort
B) Shortest path: Dijkstra, Bellman-Ford, Floyd-Warshall
C) Flow: Ford-Fulkerson, max-matching, min-cut
D) All fundamental graph algorithm families

**Answer: D**

**Explanation:**
Graph algorithms span: traversal (Ch 19), shortest path (Ch 20), MST (Ch 21), flow/matching (this chapter), coloring, planarity, decomposition. Each family has specialized algorithms exploiting specific structure. Understanding which family a problem belongs to is key to solving it. Many problems reduce to known graph algorithm families.

---

**Q27.17: Expert - [Theory] - [Gomory-Hu Tree]**

Gomory-Hu tree:

A) Compact representation of all-pairs max flow in undirected graph
B) Only V-1 max flow computations needed (not V²)
C) Tree edge weights = max flow between endpoints
D) All of the above

**Answer: D**

**Explanation:**
Gomory-Hu: minimum cut tree encoding all V(V-1)/2 pairwise min-cuts. Built with V-1 max-flow computations (not V² — remarkable reduction). Tree edge (u,v) with weight w: min cut between u and v has value w. Min cut between any pair: minimum edge weight on tree path between them. Powerful structural result.

---

**Q27.18: Intermediate - [Theory] - [Network Flow Applications]**

Max flow applications:

A) Bipartite matching, image segmentation
B) Airline scheduling, baseball elimination
C) Project selection with dependencies
D) All of the above

**Answer: D**

**Explanation:**
Max flow solves surprisingly many problems: bipartite matching (unit capacities), circulation problems, project selection (min cut = optimal profit boundary), airline crew scheduling, sports elimination (can team X still win?), image segmentation (foreground/background), edge-disjoint paths (max flow = number of disjoint paths). Powerful modeling tool.

---

**Q27.19: Expert - [Theory] - [Planar Graph Algorithms]**

Algorithms exploiting planarity:

A) Max flow in planar graphs: O(V log V) using shortest path duality
B) Planar separator theorem: O(√n) separator exists
C) Many NP-hard problems become tractable or have better approximations on planar graphs
D) All of the above

**Answer: D**

**Explanation:**
Planar graphs (embeddable without crossings): E ≤ 3V-6, sparse. Max flow: dual of shortest path in planar dual graph, O(V log V). Separator: O(√n) vertices split graph into balanced parts → divide-and-conquer algorithms. Independent set: PTAS. Coloring: always 4-colorable. Many problems have polynomial algorithms on planar graphs that are NP-hard in general.

---

**Q27.20: Advanced - [Theory] - [Heavy-Light Decomposition]**

Heavy-light decomposition (HLD):

A) Decompose tree into chains for efficient path queries
B) Each root-to-leaf path crosses O(log n) chains
C) Combined with segment tree: O(log² n) per path query
D) All of the above

**Answer: D**

**Explanation:**
HLD: classify each edge as heavy (to largest subtree child) or light. Heavy edges form chains. Any root-to-leaf path: at most O(log n) light edges (each halves subtree size). Path query: decompose into O(log n) chain segments, query each with segment tree. Total: O(log² n). With Euler tour + segment tree: O(log n). Powers tree path operations.

---

**Q27.21: Advanced - [Theory] - [LCA Algorithms]**

Lowest Common Ancestor algorithms:

A) Naive: climb both paths, O(n) per query
B) Binary lifting: O(n log n) preprocessing, O(log n) per query
C) Euler tour + sparse table: O(n) preprocessing, O(1) per query
D) All valid approaches with different trade-offs

**Answer: D**

**Explanation:**
LCA: lowest ancestor common to two nodes. Binary lifting: store 2^k-th ancestors. Jump in powers of 2. O(n log n) space/preprocess. O(log n) query. Euler tour + RMQ: flatten tree, LCA = minimum depth in Euler tour between nodes. Sparse table: O(1) RMQ. O(n) preprocess, O(1) query. Farach-Colton-Bender: O(n) preprocess, O(1) query, optimal.

---

**Q27.22: Intermediate - [Theory] - [Flow Decomposition]**

Flow decomposition theorem:

A) Any flow can be decomposed into at most E path flows and cycle flows
B) Path flow: s→t path with positive flow
C) Cycle flow: directed cycle with positive flow
D) All of the above

**Answer: D**

**Explanation:**
Flow decomposition: every feasible flow decomposes into ≤ E unit components (paths s→t and cycles). Algorithm: find s→t path with positive flow (greedy), subtract min flow on path. Repeat. Then find positive cycles. At most E iterations. Useful for: understanding flow structure, constructing actual routing from abstract flow.

---

**Q27.23: Expert - [Theory] - [Feedback Arc/Vertex Set]**

Feedback arc set / feedback vertex set:

A) FAS: minimum edges to remove to make DAG
B) FVS: minimum vertices to remove to make DAG
C) Both NP-hard on general directed graphs
D) All of the above

**Answer: D**

**Explanation:**
Feedback arc set: make graph acyclic by removing minimum edges. FVS: remove minimum vertices. Both NP-hard. FAS on tournaments: polynomial. FVS on undirected: 2-approximation. Applications: breaking deadlocks, ordering with minimum constraint violations, compiler optimization (breaking cycles in control flow).

---

**Q27.24: Intermediate - [Theory] - [Tree Diameter]**

Finding tree diameter:

A) Two BFS/DFS: from any vertex find farthest, then from that find farthest
B) Distance between two farthest vertices = diameter
C) O(V) time
D) All of the above

**Answer: D**

**Explanation:**
Tree diameter: longest path. Two-BFS proof: BFS from arbitrary u finds farthest v. BFS from v finds farthest w. dist(v,w) = diameter. Proof: if not, there exists longer path (a,b). But v is farthest from u, and geometric argument shows v must be endpoint of diameter. O(V) — two traversals. Alternative: DFS-based O(V).

---

**Q27.25: Advanced - [Theory] - [Minimum Cut Applications]**

Min cut applications:

A) Network reliability: min edges to disconnect s from t
B) Image segmentation: pixel classification (foreground/background)
C) Surveillance: minimum cameras to monitor all corridors
D) All of the above

**Answer: D**

**Explanation:**
Min cut = max flow (duality). Network reliability: min cut capacity = flow → how resilient. Image segmentation: pixels as nodes, edge weights = similarity. Source = foreground seeds, sink = background seeds. Min cut separates optimally. Minimum cuts also solve: edge connectivity (min cut over all pairs), vertex connectivity (transform to edge connectivity).

---

## Chapter 27 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | Network flow, Ford-Fulkerson, max-flow min-cut, topological sort apps |
| Intermediate | 10 | Edmonds-Karp, Dinic's, bipartite matching, Hungarian, SCC, HLD, LCA |
| Advanced | 7 | Min-cost flow, push-relabel, 2-SAT, Euler path, flow decomposition |
| Expert | 3 | Gomory-Hu tree, planar algorithms, feedback sets |

**Total MCQs: 25**

**Next:** Chapter 28 - Computational Geometry
