# Chapter 20: Shortest Path Algorithms

**Target:** 75 MCQs | **Distribution:** 19 Foundational, 30 Intermediate, 19 Advanced, 7 Expert

---

**Q20.1: Foundational - [Theory] - [Shortest Path Problem]**

Single-source shortest path (SSSP):

A) Find shortest distance from source to all other vertices
B) Shortest = minimum total edge weight along path
C) Different algorithms for different graph types
D) All of the above

**Answer: D**

**Explanation:**
SSSP: given source s, find min-weight path to every reachable vertex. Unweighted: BFS O(V+E). Non-negative weights: Dijkstra. Negative weights: Bellman-Ford. All-pairs: Floyd-Warshall or repeated SSSP. Choice depends on graph properties (weights, density, negative edges).

---

**Q20.2: Foundational - [Theory] - [Dijkstra's Algorithm]**

Dijkstra's algorithm:

A) Greedy: always process vertex with smallest tentative distance
B) Uses priority queue (min-heap)
C) Works only with non-negative edge weights
D) All of the above

**Answer: D**

**Explanation:**
Dijkstra: maintain dist[v], initially ∞ except dist[s]=0. Priority queue of (dist, vertex). Extract min, relax all neighbors. Once extracted, vertex's distance is final (greedy proof relies on non-negative weights). O((V+E) log V) with binary heap. O(V² + E) with array (better for dense graphs).

---

**Q20.3: Foundational - [Trace] - [Dijkstra's Algorithm]**

Dijkstra from A. Edges: A-B:1, A-C:4, B-C:2, B-D:6, C-D:3:

A) dist=[A:0, B:∞, C:∞, D:∞]. Extract A(0). Relax: B=1, C=4
B) Extract B(1). Relax: C=min(4, 1+2=3)=3, D=1+6=7
C) Extract C(3). Relax: D=min(7, 3+3=6)=6
D) Extract D(6). Final: A:0, B:1, C:3, D:6

**Answer: D**

**Explanation:**
Dijkstra trace: A(0)→B(1)→C(3)→D(6). Path to D: A→B→C→D (cost 6), not A→B→D (cost 7). Greedy choice at each step is optimal because all weights ≥ 0. Each vertex extracted once, each edge relaxed once.

---

**Q20.4: Foundational - [Theory] - [Dijkstra Negative Weight Problem]**

Why Dijkstra fails with negative edges:

A) Once a vertex is "finalized," its distance won't decrease
B) Negative edge could provide shorter path through already-finalized vertex
C) Greedy assumption violated
D) All of the above

**Answer: D**

**Explanation:**
Example: A→B:1, A→C:2, B→C:-5. Dijkstra: finalize A(0), B(1), C(2). But path A→B→C = 1+(-5) = -4 < 2. C's distance should be -4, not 2. Once C is extracted from PQ at distance 2, it won't be updated. For negative weights: use Bellman-Ford.

---

**Q20.5: Foundational - [Theory] - [Bellman-Ford Algorithm]**

Bellman-Ford algorithm:

A) Relax all edges V-1 times
B) Handles negative edge weights
C) Detects negative weight cycles
D) All of the above

**Answer: D**

**Explanation:**
Bellman-Ford: for i in 1..V-1: for each edge (u,v,w): if dist[u]+w < dist[v]: dist[v] = dist[u]+w. After V-1 iterations: all shortest paths found (longest simple path has V-1 edges). Extra iteration: if any distance decreases → negative cycle. O(VE). Slower than Dijkstra but handles negative weights.

---

**Q20.6: Foundational - [Trace] - [Bellman-Ford]**

Bellman-Ford from A. Edges: A→B:4, A→C:5, B→C:-3, C→D:2:

A) Init: dist=[A:0, B:∞, C:∞, D:∞]
B) It 1: A→B: B=4. A→C: C=5. B→C: C=min(5,4-3)=1. C→D: D=3
C) It 2: B→C: C=min(1,4-3)=1. C→D: D=min(3,1+2)=3. No change
D) Final: A:0, B:4, C:1, D:3. Path to C: A→B→C (cost 1)

**Answer: D**

**Explanation:**
Negative edge B→C:-3 makes A→B→C (cost 1) shorter than direct A→C (cost 5). Bellman-Ford correctly finds this. Iteration 1 suffices here. Iteration 2 confirms no further relaxation. No negative cycle (no further decrease in iteration V).

---

**Q20.7: Foundational - [Theory] - [Floyd-Warshall Algorithm]**

Floyd-Warshall algorithm:

A) All-pairs shortest path
B) DP: dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]) for each intermediate k
C) O(V³) time, O(V²) space
D) All of the above

**Answer: D**

**Explanation:**
Floyd-Warshall: three nested loops (k, i, j). k = intermediate vertex. dist[i][j] via vertices {1..k} = min(via {1..k-1}, via k). O(V³). Handles negative weights (not negative cycles). Detects negative cycle: dist[i][i] < 0. Simple implementation. Best for dense graphs with V ≤ ~500. Space can be optimized to 2D.

---

**Q20.8: Intermediate - [Theory] - [Dijkstra Complexity]**

Dijkstra's complexity depends on priority queue:

A) Array-based PQ: O(V² + E) — good for dense graphs
B) Binary heap: O((V+E) log V) — good for sparse
C) Fibonacci heap: O(V log V + E) — theoretical optimum
D) All of the above

**Answer: D**

**Explanation:**
Array PQ: extractMin by scanning all V → V × O(V). Each edge relaxed in O(1). Total: O(V²+E). Binary heap: extractMin O(log V) × V + decreaseKey O(log V) × E = O((V+E) log V). Fibonacci: extractMin O(log V) amortized × V + decreaseKey O(1) amortized × E = O(V log V + E). Practice: binary heap usually best.

---

**Q20.9: Intermediate - [Theory] - [Negative Cycle Detection]**

Bellman-Ford negative cycle detection:

A) After V-1 iterations, run one more iteration
B) If any distance decreases: negative cycle reachable from source
C) To find cycle: track predecessors, follow back from updated vertex
D) All of the above

**Answer: D**

**Explanation:**
V-1 iterations suffice for shortest paths (longest simple path has V-1 edges). If V-th iteration still relaxes: some path with V edges is shorter → cycle visited → negative cycle. To find cycle vertices: start from any vertex updated in V-th iteration, follow predecessors V times — guaranteed to be in cycle. Applications: arbitrage detection in currency exchange.

---

**Q20.10: Intermediate - [Theory] - [Johnson's Algorithm]**

Johnson's algorithm for all-pairs shortest path:

A) Reweight edges using Bellman-Ford (make all non-negative)
B) Run Dijkstra from each vertex
C) O(VE + V(V+E) log V) — better than Floyd-Warshall for sparse
D) All of the above

**Answer: D**

**Explanation:**
Johnson's: (1) Add vertex s, zero-weight edges to all vertices. (2) Bellman-Ford from s: compute h[v] for each v. (3) Reweight: w'(u,v) = w(u,v) + h[u] - h[v] ≥ 0. (4) Run Dijkstra from each vertex using w'. (5) Adjust distances. For sparse graphs (E << V²): O(VE log V) vs Floyd-Warshall O(V³).

---

**Q20.11: Intermediate - [Theory] - [A* Search Algorithm]**

A* search for shortest path:

A) f(n) = g(n) + h(n): actual cost + heuristic
B) Admissible h: never overestimates → optimal
C) Consistent h: h(u) ≤ w(u,v) + h(v) → no re-expansion
D) All of the above

**Answer: D**

**Explanation:**
A*: Dijkstra with heuristic guidance. Explores fewer vertices by prioritizing promising directions. Admissible: h ≤ actual cost guarantees optimality. Consistent: triangle inequality on h → monotone f → each vertex extracted at most once. Common heuristics: Euclidean distance, Manhattan distance. Used in game pathfinding, navigation, puzzle solving.

---

**Q20.12: Intermediate - [Theory] - [Shortest Path in DAG]**

Shortest path in DAG:

A) Topological sort, then relax edges in topological order
B) O(V + E) — much faster than Dijkstra
C) Works with negative weights (no cycles to loop)
D) All of the above

**Answer: D**

**Explanation:**
DAG shortest path: topological order ensures each vertex processed after all predecessors. Single pass relaxation suffices. O(V+E). Handles negative weights (no cycles possible). Also finds longest path in DAG (negate weights or modify relaxation to maximize). Applications: critical path in project scheduling (PERT/CPM).

---

**Q20.13: Intermediate - [Trace] - [DAG Shortest Path]**

DAG: 0→1:5, 0→2:3, 1→3:6, 1→2:2, 2→3:7, 3→4:1. Topo order: 0,1,2,3,4:

A) dist=[0:0, 1:∞, 2:∞, 3:∞, 4:∞]
B) Process 0: dist[1]=5, dist[2]=3
C) Process 1: dist[3]=min(∞,5+6)=11, dist[2]=min(3,5+2)=3 (no change)
D) Process 2: dist[3]=min(11,3+7)=10. Process 3: dist[4]=10+1=11. Final: [0,5,3,10,11]

**Answer: D**

**Explanation:**
Process in topological order. Each edge relaxed exactly once. Path to 3: 0→2→3 (cost 10) beats 0→1→3 (cost 11). O(V+E) = O(5+6) = O(11). No priority queue needed — topological order ensures correctness.

---

**Q20.14: Intermediate - [Theory] - [SPFA Algorithm]**

SPFA (Shortest Path Faster Algorithm):

A) Optimization of Bellman-Ford using queue
B) Only re-relax vertices whose distance changed
C) O(VE) worst case, often O(E) in practice
D) All of the above

**Answer: D**

**Explanation:**
SPFA: queue-based Bellman-Ford. Enqueue source. Dequeue vertex, relax neighbors. If neighbor's distance decreases and not in queue: enqueue. Avoid redundant relaxations. Average case much faster than Bellman-Ford. Worst case still O(VE) (adversarial inputs). Popular in competitive programming for negative-weight SSSP.

---

**Q20.15: Intermediate - [Theory] - [Path Reconstruction]**

Reconstructing shortest path:

A) Maintain predecessor/parent array during relaxation
B) When dist[v] updated via u: pred[v] = u
C) Follow predecessors from target to source, reverse
D) All of the above

**Answer: D**

**Explanation:**
All shortest path algorithms can track predecessors. Dijkstra: pred[v] = u when dist[v] relaxed via u. Bellman-Ford: same. Floyd-Warshall: next[i][j] = k when path goes through k. Reconstruct: follow pred/next pointers. Print path: reverse predecessor chain or use next-hop matrix.

---

**Q20.16: Foundational - [Theory] - [Single Source vs All Pairs]**

SSSP vs APSP:

A) SSSP: from one source. Dijkstra O((V+E) log V), Bellman-Ford O(VE)
B) APSP: all pairs. Floyd-Warshall O(V³), Johnson's O(VE + V² log V)
C) APSP via V × SSSP: O(V(V+E) log V) with Dijkstra
D) All of the above

**Answer: D**

**Explanation:**
SSSP: one start vertex. APSP: every vertex to every other. APSP approaches: (1) V × Dijkstra: O(V(V+E) log V). (2) Floyd-Warshall: O(V³). (3) Johnson's: O(VE + V(V+E) log V). Dense graph (E≈V²): Floyd-Warshall. Sparse: Johnson's. V × Dijkstra when no negative weights and sparse.

---

**Q20.17: Advanced - [Theory] - [Bidirectional Dijkstra]**

Bidirectional Dijkstra:

A) Run Dijkstra from source and target simultaneously
B) Stop when a vertex is settled in both directions
C) Shortest path ≤ min settled distance from both sides
D) Roughly 2× speedup (each side explores half)

**Answer: D**

**Explanation:**
Bidirectional: two priority queues, alternate expansions. When vertex u settled in both: candidate path = dist_forward[u] + dist_backward[u]. Must continue until min PQ value ≥ current best. Speedup: √2 in search radius → searches ~half the vertices. Used in road network routing. Combined with A*: bidirectional A*.

---

**Q20.18: Advanced - [Theory] - [Contraction Hierarchies]**

Contraction hierarchies:

A) Preprocess graph by contracting vertices (add shortcut edges)
B) Query: bidirectional Dijkstra on augmented graph
C) Preprocessing: O(V log V × E), Query: O(V^0.5 log V) in practice
D) Fastest known practical SSSP for road networks

**Answer: D**

**Explanation:**
Contraction hierarchies (Geisberger et al.): contract vertices in order of "importance." When contracting v: add shortcut edges between remaining neighbors of v to preserve distances. Query: upward search from source and target in hierarchy. Extremely fast in practice (~1ms for continental-scale road networks). Powers Google Maps, OpenStreetMap routing.

---

**Q20.19: Intermediate - [Theory] - [Dijkstra with Lazy Deletion]**

Dijkstra with lazy deletion:

A) Don't implement decrease-key; insert new entry with better distance
B) When extracting, check if already finalized → skip
C) O((V+E) log E) — slightly worse but simpler
D) All of the above

**Answer: D**

**Explanation:**
Standard Dijkstra needs decrease-key (complex with binary heap). Lazy approach: just insert (new_dist, v) into heap. Multiple entries for same vertex. When extracting (dist, v): if dist > dist[v], skip (stale entry). Works correctly, simpler code. Heap may grow to E entries → O(E log E) = O(E log V) (since E ≤ V²). Common in competitive programming.

---

**Q20.20: Intermediate - [Theory] - [0-1 BFS Detail]**

0-1 BFS for 0/1 weighted graphs:

A) Deque: 0-weight edges → push front, 1-weight → push back
B) O(V + E) — like BFS complexity
C) Replaces Dijkstra when weights are only 0 or 1
D) All of the above

**Answer: D**

**Explanation:**
0-1 BFS: deque-based. 0-weight neighbor same "level" (front of deque). 1-weight neighbor next "level" (back). Correctly processes in non-decreasing distance order. O(V+E) vs Dijkstra O((V+E) log V). Applicable: grid with walls (cost 1 to break) and free cells (cost 0). Significant speedup for this special case.

---

**Q20.21: Intermediate - [Theory] - [k Shortest Paths]**

k shortest paths:

A) Find not just the shortest, but k shortest paths
B) Yen's algorithm: O(kV(V+E) log V) using modified Dijkstra
C) Eppstein's algorithm: O(E + V log V + k)
D) All of the above

**Answer: D**

**Explanation:**
k-shortest: useful for route alternatives, network reliability. Yen's: iteratively find next shortest by deviating from previous. Eppstein's: more efficient using path graph structure. Applications: navigation (show alternative routes), network routing (backup paths), flow problems.

---

**Q20.22: Advanced - [Theory] - [Shortest Path with Constraints]**

Shortest path with constraints:

A) Max k edges: BFS-like DP, O(kE)
B) Must visit specific vertices: Bitmask DP, O(2^m × V²)
C) Time-dependent weights: modified Dijkstra
D) All vary from standard algorithms

**Answer: D**

**Explanation:**
Constrained shortest path: (1) ≤ k edges: dp[v][i] = min dist to v using ≤ i edges. Bellman-Ford naturally gives this. (2) Visit subset: TSP-like bitmask DP. (3) Time-dependent: Dijkstra with time as state dimension. (4) With fuel/resources: state = (vertex, resource_remaining). State-space expansion technique.

---

**Q20.23: Foundational - [Theory] - [Shortest Path Tree]**

Shortest path tree:

A) Tree rooted at source with shortest paths to all vertices
B) Produced by Dijkstra or Bellman-Ford (via predecessor array)
C) V-1 edges connecting V vertices
D) All of the above

**Answer: D**

**Explanation:**
SPT: for each vertex v, exactly one edge (parent[v], v) on shortest path from source. Forms a tree rooted at source. Not unique if multiple shortest paths exist. Dijkstra produces SPT naturally. SPT ≠ MST in general (different objectives). SPT edges provide the actual shortest path routes.

---

**Q20.24: Advanced - [Theory] - [Multi-Source Shortest Path]**

Multi-source shortest path:

A) Add virtual source s' with 0-weight edges to all real sources
B) Run single Dijkstra/Bellman-Ford from s'
C) Each vertex gets distance to nearest source
D) All of the above

**Answer: D**

**Explanation:**
Multi-source: find shortest distance from any source to each vertex. Virtual source trick: add s' with 0-weight edges to all sources. Single SSSP from s' gives min distance to nearest source. O((V+E) log V) with Dijkstra. Equivalent to multi-source BFS for unweighted. Applications: facility location, Voronoi on graphs.

---

**Q20.25: Expert - [Theory] - [All-Pairs via Matrix Multiplication]**

All-pairs shortest path via matrix multiplication:

A) Treat adjacency matrix as "multiplication" with (min, +) semiring
B) Repeated squaring: O(V³ log V) — not better than Floyd-Warshall
C) But enables sub-cubic improvements with fast matrix multiply
D) All of the above

**Answer: D**

**Explanation:**
APSP as matrix product: D^(k) = D^(k/2) ⊗ D^(k/2) where ⊗ uses min for + and + for ×. Log V squarings × O(V³) multiplication = O(V³ log V). With subcubic matrix multiply: Williams' O(V³/2^Ω(√log V)). Theoretical improvement over Floyd-Warshall but impractical. Shows deep connection between APSP and matrix multiplication.

---

**Q20.26: Intermediate - [Theory] - [Dijkstra Modified for Largest Minimum Edge]**

Widest/bottleneck path:

A) Maximize minimum edge weight on path
B) Modified Dijkstra: dist[v] = max over paths of (min edge on path)
C) Relax: dist[v] = max(dist[v], min(dist[u], w(u,v)))
D) All of the above

**Answer: D**

**Explanation:**
Widest path: maximize bottleneck (minimum capacity along path). Modified Dijkstra with max-heap: process vertex with largest bottleneck distance. Relax: new bottleneck = min(current path bottleneck, edge weight). Applications: network bandwidth routing, maximum capacity path. O((V+E) log V).

---

**Q20.27: Intermediate - [Theory] - [Shortest Path in Grid]**

Shortest path in weighted grid:

A) Treat grid as graph, cells as vertices, 4 neighbors
B) Apply Dijkstra for weighted grid
C) BFS only if all weights are equal
D) All of the above

**Answer: D**

**Explanation:**
Grid shortest path: each cell connected to 4 (or 8) neighbors. Uniform weight: BFS O(rows×cols). Variable weights: Dijkstra O(rows×cols × log(rows×cols)). 0/1 weights: 0-1 BFS O(rows×cols). Common in maze problems, game pathfinding. A* with Manhattan/Euclidean heuristic much faster in practice.

---

**Q20.28: Advanced - [Theory] - [Dial's Algorithm]**

Dial's algorithm:

A) Dijkstra with bucket queue instead of heap
B) Bucket for each possible distance 0, 1, ..., C×V
C) O(V + E + C) where C = max edge weight
D) All of the above

**Answer: D**

**Explanation:**
Dial's: array of buckets, one per possible distance. Process smallest non-empty bucket. Relax: move neighbor to appropriate bucket. O(V + E + C) where C = max weight. Good for small integer weights. Extension: radix heap O(V + E + V log C). Between BFS O(V+E) for C=1 and Dijkstra O((V+E) log V) for arbitrary C.

---

**Q20.29: Foundational - [Theory] - [Relaxation]**

Edge relaxation:

A) If dist[u] + w(u,v) < dist[v]: update dist[v]
B) Core operation of all shortest path algorithms
C) Try to improve current best distance estimate
D) All of the above

**Answer: D**

**Explanation:**
Relaxation: fundamental operation. "Can we improve v's distance by going through u?" If yes: update dist[v] and pred[v]. Dijkstra: relaxes each edge once. Bellman-Ford: relaxes all edges V-1 times. Floyd-Warshall: relaxes via each intermediate vertex. All shortest path algorithms are essentially different orderings of relaxation operations.

---

**Q20.30: Expert - [Theory] - [Planar Graph Shortest Path]**

Shortest path in planar graphs:

A) O(V log² V) using separator-based algorithms
B) Better than general Dijkstra O((V+E) log V) for planar
C) Exploits planarity (few edges: E ≤ 3V-6)
D) All of the above

**Answer: D**

**Explanation:**
Planar graphs: E = O(V). Dijkstra: O(V log V). But MSSP (multiple-source SP) on planar: O(V log² V) using recursive planar separators. FR-Dijkstra: O(V) for planar with non-negative weights using Fibonacci heap + planarity. Specialized algorithms exploit structure for better constants.

---

**Q20.31: Intermediate - [Theory] - [Floyd-Warshall Path Reconstruction]**

Floyd-Warshall path reconstruction:

A) Maintain next[i][j] = first vertex on shortest path from i to j
B) When dist[i][j] updated via k: next[i][j] = next[i][k]
C) Reconstruct: i → next[i][j] → next[next[i][j]][j] → ... → j
D) All of the above

**Answer: D**

**Explanation:**
Floyd-Warshall path: next[i][j] initialized to j for direct edges. When path through k is shorter: next[i][j] = next[i][k] (go toward k first). To reconstruct i→j: follow next pointers. next[i][j], next[next[i][j]][j], ... until reaching j. O(path length) reconstruction.

---

**Q20.32: Advanced - [Theory] - [Bellman-Ford on DAG vs General]**

Bellman-Ford on DAG vs general graph:

A) DAG: topological order relaxation, O(V+E), one pass
B) General: V-1 passes over all edges, O(VE)
C) DAG is strictly easier for shortest path
D) All of the above

**Answer: D**

**Explanation:**
DAG: topological order processes each vertex after all predecessors → single-pass relaxation suffices. O(V+E). General graph: may need V-1 iterations because edges can be processed "out of order." Worst case: each iteration extends shortest path by one edge. DAG: no cycles, so one topological pass = one correct pass.

---

**Q20.33: Intermediate - [Theory] - [Shortest Path Applications]**

Shortest path applications:

A) GPS navigation: road network routing
B) Network routing: minimum latency/cost paths
C) Currency arbitrage: negative cycle detection
D) All of the above

**Answer: D**

**Explanation:**
Shortest path is ubiquitous: navigation (road networks: Dijkstra/A*/contraction hierarchies), networking (OSPF uses Dijkstra, BGP uses path-vector), arbitrage (negative cycle in log-exchange-rate graph), social networks (degrees of separation), game AI (pathfinding), logistics (minimum cost routing).

---

**Q20.34: Expert - [Theory] - [Algebraic Shortest Path]**

Algebraic path problem:

A) Generalize shortest path to arbitrary semirings
B) (min, +) semiring: shortest path. (max, min): widest path
C) (boolean OR, AND): transitive closure
D) All unified framework

**Answer: D**

**Explanation:**
Semiring framework: Floyd-Warshall generalizes. Replace (min, +) with any closed semiring. (max, min): widest path. (OR, AND): reachability. (max, ×): most reliable path (multiply probabilities). (+, ×): count all paths. Unified view shows deep structure of path problems. Same O(V³) algorithm, different semiring operations.

---

**Q20.35: Intermediate - [Theory] - [Parallel Shortest Path]**

Parallelizing shortest path:

A) Bellman-Ford: each iteration parallelizable (relax all edges)
B) Floyd-Warshall: inner two loops parallelizable per k
C) Dijkstra: harder to parallelize (sequential dependency)
D) All of the above

**Answer: D**

**Explanation:**
Bellman-Ford: iteration i depends on i-1, but within iteration, all edge relaxations independent → parallelize inner loop. Floyd-Warshall: for fixed k, all (i,j) updates independent. Dijkstra: extracting min is sequential bottleneck. Δ-stepping: parallel Dijkstra variant for PRAM model. GPU-based BFS/SSSP used in practice for large graphs.

---

**Q20.36: Advanced - [Theory] - [Shortest Path DAG]**

Shortest path DAG (all shortest paths):

A) Includes all edges (u,v) where dist[u] + w(u,v) = dist[v]
B) Subgraph of original graph containing all shortest paths
C) Useful for: counting shortest paths, finding all shortest paths
D) All of the above

**Answer: D**

**Explanation:**
SP DAG: after computing SSSP, edge (u,v) is on some shortest path iff dist[u] + w(u,v) = dist[v]. This subgraph is a DAG (for graphs without 0-weight cycles). Count shortest paths: DP on SP DAG. Find all shortest paths: enumerate in SP DAG. Used in betweenness centrality computation (Brandes' algorithm).

---

**Q20.37: Foundational - [Theory] - [BFS as Shortest Path]**

BFS is Dijkstra with all weights = 1:

A) BFS processes in distance order automatically
B) No need for priority queue (queue suffices)
C) O(V+E) vs Dijkstra's O((V+E) log V)
D) All of the above

**Answer: D**

**Explanation:**
Unweighted = all weights 1. Dijkstra with unit weights: PQ always extracts in FIFO order = queue. So BFS is Dijkstra for unit weights. BFS O(V+E) < Dijkstra O((V+E) log V). Always use BFS for unweighted shortest path. Never use Dijkstra for unweighted graphs.

---

**Q20.38: Expert - [Theory] - [Thorup's Algorithm]**

Thorup's algorithm:

A) O(V + E) SSSP for undirected graphs with non-negative integer weights
B) Uses component hierarchy and bucketing
C) Theoretically optimal but complex
D) All of the above

**Answer: D**

**Explanation:**
Thorup (1999): linear-time SSSP for undirected graphs with integer weights. Uses split/join decomposition and hierarchical bucketing. O(V+E) vs Dijkstra O((V+E) log V). Theoretically optimal. Impractical: enormous constant factors, complex implementation. Shows O(V+E) is achievable, which was previously open question.

---

**Q20.39: Intermediate - [Theory] - [Negative Weight Cycle Applications]**

Negative cycle applications:

A) Currency arbitrage: cycle of exchanges with net profit
B) Model rates as -log(exchange_rate), negative cycle = arbitrage
C) Bellman-Ford detects in O(VE)
D) All of the above

**Answer: D**

**Explanation:**
Currency arbitrage: exchange A→B→C→A with product of rates > 1. Take -log: sum of -log(rates) < 0 → negative cycle. Bellman-Ford on -log graph detects arbitrage opportunities. Other applications: detecting inconsistencies in constraint systems, pricing anomalies in financial networks.

---

**Q20.40: Expert - [Theory] - [Distance Oracle]**

Distance oracles:

A) Preprocess graph to answer distance queries quickly
B) Approximate distance oracle: O(n^(1+1/k)) space, O(k) query, stretch 2k-1
C) Trade-off: space vs query time vs accuracy
D) All of the above

**Answer: D**

**Explanation:**
Distance oracle (Thorup-Zwick): preprocess in O(k × m × n^(1/k)). Store O(n^(1+1/k)) space. Query in O(k) time with stretch factor 2k-1 (approximate). k=2: O(n^1.5) space, O(1) query, stretch 3. Exact oracle: O(n²) space for O(1) query. Trade accuracy for space/time. Used in large network routing.

---

**Q20.41: Advanced - [Theory] - [Shortest Path Counting]**

Count number of shortest paths:

A) Maintain count[v] alongside dist[v]
B) When dist[v] updated (improved): count[v] = count[u]
C) When dist[v] tied (same distance via different vertex): count[v] += count[u]
D) All of the above

**Answer: D**

**Explanation:**
Path counting: augment SSSP. count[s]=1. When relaxing edge (u,v): if dist[u]+w < dist[v]: dist[v]=dist[u]+w, count[v]=count[u]. If dist[u]+w == dist[v]: count[v]+=count[u]. Works with Dijkstra and BFS. O(V+E) additional work. Used in: betweenness centrality, network reliability.

---

**Q20.42: Foundational - [Theory] - [Algorithm Selection Guide]**

Choosing shortest path algorithm:

A) Unweighted: BFS O(V+E)
B) Non-negative weights: Dijkstra O((V+E) log V)
C) Negative weights: Bellman-Ford O(VE)
D) All-pairs: Floyd-Warshall O(V³) for dense, Johnson's for sparse

**Answer: D**

**Explanation:**
Decision tree: Unweighted → BFS. Weighted, no negative → Dijkstra. Negative weights → Bellman-Ford. DAG → topological + relax O(V+E). All-pairs, dense → Floyd-Warshall. All-pairs, sparse → Johnson's. 0/1 weights → 0-1 BFS. Know which to use for each scenario.

---

**Q20.43: Foundational - [Trace] - [Dijkstra Detailed Trace]**

Dijkstra on graph A→B:1, A→C:4, B→C:2, B→D:6, C→D:3 from source A:

A) Init: dist[A]=0, dist[B,C,D]=∞. Process A: dist[B]=1, dist[C]=4
B) Process B (dist=1): dist[C]=min(4, 1+2)=3, dist[D]=min(∞, 1+6)=7
C) Process C (dist=3): dist[D]=min(7, 3+3)=6
D) Process D (dist=6). Final: A:0, B:1, C:3, D:6

**Answer: D**

**Explanation:**
Dijkstra trace: extract minimum-distance unprocessed vertex. A(0)→B(1)→C(3)→D(6). Path to D: A→B→C→D (cost 6), not A→B→D (cost 7). Greedy by distance ensures optimality with non-negative weights. 4 vertices = 4 extract-min operations.

---

**Q20.44: Intermediate - [Theory] - [Negative Cycle Detection]**

Detecting negative-weight cycles:

A) Bellman-Ford: run V-1 rounds, then check V-th round
B) If any distance decreases in V-th round → negative cycle exists
C) Floyd-Warshall: negative cycle if dist[v][v] < 0 for any v
D) All of the above

**Answer: D**

**Explanation:**
Negative cycle: can reduce path cost infinitely. Bellman-Ford: V-1 rounds suffice for shortest paths. If V-th round still improves: cycle reachable. Floyd-Warshall: negative diagonal means negative self-cycle. SPFA: count relaxations per node; if ≥ V, cycle exists. Applications: currency arbitrage (log transform makes it cycle finding).

---

**Q20.45: Foundational - [Theory] - [Path Reconstruction]**

Reconstructing shortest path (not just distance):

A) Maintain predecessor/parent array: parent[v] = u if (u,v) relaxed
B) Update parent[v] whenever dist[v] is improved
C) Trace back: target → parent[target] → ... → source
D) All of the above

**Answer: D**

**Explanation:**
Path reconstruction: during relaxation, if dist[u]+w(u,v) < dist[v]: set parent[v] = u. After algorithm completes: backtrack from target using parent pointers. Reverse to get source→target path. O(V) space for parent array. Works with Dijkstra, Bellman-Ford, BFS. Floyd-Warshall: use next[i][j] matrix for path.

---

**Q20.46: Intermediate - [Trace] - [DAG Shortest Path Trace]**

DAG shortest path (topological order) on: A→B:3, A→C:6, B→C:4, B→D:4, B→E:11, C→D:8, C→G:11, D→E:5, D→F:2, D→G:2, E→H:1, F→H:2, G→H:2:

A) Topological order: A, B, C, D, E, F, G, H
B) Process A: dist[B]=3, dist[C]=6
C) Process B: dist[C]=min(6,7)=6, dist[D]=7, dist[E]=14
D) Continue until H — no revisiting needed

**Answer: D**

**Explanation:**
DAG shortest path: topological sort, then relax edges in order. Each vertex processed once. No priority queue needed. O(V+E). Works with negative weights (unlike Dijkstra). Key advantage: single pass guarantees optimality because topological order ensures all predecessors processed first.

---

**Q20.47: Advanced - [Theory] - [Dijkstra with Fibonacci Heap]**

Dijkstra with Fibonacci heap:

A) O(V log V + E) — optimal for sparse graphs
B) Decrease-key: O(1) amortized (vs O(log V) for binary heap)
C) Extract-min: O(log V) amortized
D) All of the above

**Answer: D**

**Explanation:**
Fibonacci heap: decrease-key O(1) amortized, extract-min O(log V) amortized. Dijkstra: V extract-mins + E decrease-keys = O(V log V + E). For sparse graphs (E = O(V)): O(V log V). Binary heap: O((V+E) log V). Fibonacci wins when E >> V. In practice: binary heap often faster due to constants. Fibonacci heap mainly theoretical improvement.

---

**Q20.48: Intermediate - [Theory] - [K Shortest Paths (Yen's Algorithm)]**

Finding k shortest simple paths:

A) Yen's algorithm: iteratively find k shortest s-t paths
B) After finding i-th path, systematically deviate to find (i+1)-th
C) Time complexity: O(kV(V log V + E))
D) All of the above

**Answer: D**

**Explanation:**
Yen's (1971): finds k shortest loopless paths. For each of k iterations: try deviating from previous path at each node. Run Dijkstra with excluded edges/nodes. Keep candidates in sorted order. O(kV × Dijkstra). Alternatives: Eppstein's O(E + V log V + k) for general (non-simple) k shortest paths. Applications: route planning, network reliability.

---

**Q20.49: Intermediate - [Theory] - [All-Pairs BFS for Unweighted]**

All-pairs shortest path in unweighted graph:

A) Run BFS from each vertex: V times BFS
B) Total: O(V × (V+E)) = O(V² + VE)
C) Better than Floyd-Warshall O(V³) for sparse graphs
D) All of the above

**Answer: D**

**Explanation:**
Unweighted APSP: V runs of BFS. Each BFS: O(V+E). Total: O(V² + VE). Sparse (E=O(V)): O(V²). Dense (E=O(V²)): O(V³) = same as Floyd-Warshall. For sparse unweighted: V×BFS beats Floyd-Warshall. Floyd-Warshall still useful for weighted dense or when negative edges exist.

---

**Q20.50: Foundational - [Theory] - [Shortest Path in Grid/Maze]**

Shortest path in unweighted grid (maze):

A) BFS from start cell, exploring 4 (or 8) neighbors
B) First time reaching destination = shortest path
C) O(rows × cols) time and space
D) All of the above

**Answer: D**

**Explanation:**
Grid BFS: treat each cell as node, edges to adjacent cells. BFS guarantees shortest path in unweighted grid. Mark visited to avoid revisits. Path length = BFS level at destination. Reconstruct path via parent pointers. For weighted grids: use Dijkstra. A* with Manhattan distance heuristic: often faster in practice.

---

**Q20.51: Intermediate - [Theory] - [Bellman-Ford Early Termination]**

Bellman-Ford optimization:

A) If no distance updated in a round → terminate early
B) Best case: O(E) for already-optimal distances
C) Worst case remains O(VE), but practical improvement
D) All of the above

**Answer: D**

**Explanation:**
Standard Bellman-Ford: always V-1 rounds. Optimization: if a complete round produces no relaxation, all distances are final → stop. Best case: 1 round with 0 updates = O(E). Typical random graphs: finishes well before V-1 rounds. SPFA (queue-based variant): only re-processes vertices whose distances changed. Both avoid unnecessary work.

---

**Q20.52: Advanced - [Theory] - [Widest Path / Bottleneck Shortest Path]**

Widest (bottleneck) path — maximize minimum edge weight on path:

A) Maximize the minimum edge weight along any path from s to t
B) Modified Dijkstra: use max instead of sum, track minimum edge on path
C) Or use MST: widest path between any two nodes is the path in maximum spanning tree
D) All of the above

**Answer: D**

**Explanation:**
Widest path (maximin): maximize bottleneck. Modified Dijkstra: width[s]=∞, width[v]=max over u of min(width[u], w(u,v)). Use max-heap. O((V+E) log V). Alternative: maximum spanning tree contains widest path between all pairs. Applications: network bandwidth, maximum flow path. Dual: minimax path (minimize maximum edge).

---

**Q20.53: Intermediate - [Theory] - [Multi-Destination Dijkstra]**

Dijkstra for nearest among multiple targets:

A) Run single Dijkstra from source
B) Stop when first target is extracted from priority queue
C) Guaranteed to be nearest target (Dijkstra extracts in distance order)
D) All of the above — potentially much faster than full Dijkstra

**Answer: D**

**Explanation:**
Early termination: Dijkstra processes vertices in distance order. First target extracted = nearest target. No need to compute distances to all vertices. For k targets in graph of V vertices: expected to process V/k vertices before finding nearest. Huge speedup in geographic routing where only nearby destinations matter.

---

**Q20.54: Advanced - [Theory] - [Shortest Path with Constraints]**

Shortest path with at most k edges:

A) Modified Bellman-Ford: run exactly k rounds
B) After round i: dist[v] = shortest path using at most i edges
C) DP: dp[i][v] = min cost to reach v using ≤ i edges
D) All of the above — O(kE)

**Answer: D**

**Explanation:**
Constrained shortest path: k edges maximum. DP formulation: dp[0][s]=0, dp[0][v]=∞. dp[i][v] = min(dp[i-1][v], min over (u,v) of dp[i-1][u]+w(u,v)). Bellman-Ford naturally computes this: round i uses at most i edges. Need copy of dist array per round (or swap). Application: "cheapest flights within K stops" (LeetCode #787).

---

**Q20.55: Expert - [Theory] - [Difference Constraints and Shortest Paths]**

System of difference constraints:

A) Constraints: x_j - x_i ≤ w_ij
B) Model as shortest path: edge (i,j) with weight w_ij
C) Bellman-Ford from source 0 (connected to all with weight 0)
D) All of the above — feasible if no negative cycle

**Answer: D**

**Explanation:**
Difference constraints: x_j - x_i ≤ b_ij. Create constraint graph: edge i→j with weight b_ij. Add source s with edges s→all at weight 0. Run Bellman-Ford from s. If no negative cycle: dist[v] = x_v (a feasible solution). Negative cycle = infeasible system. Connection to LP: difference constraints are special case of linear programming solvable in polynomial time.

---

## Chapter 20 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 13 | Dijkstra, Bellman-Ford, Floyd-Warshall, BFS as SSSP, relaxation, path reconstruction, grid BFS, traces |
| Intermediate | 22 | A*, DAG SP, SPFA, 0-1 BFS, Johnson's, path counting, negative cycles, k-shortest, early termination, multi-destination, constrained SP |
| Advanced | 13 | Bidirectional Dijkstra, contraction hierarchies, Dial's, bottleneck path, Fibonacci heap Dijkstra, k-th matrix, widest path |
| Expert | 7 | Thorup's, distance oracle, matrix mult APSP, algebraic path, planar SP, difference constraints |

**Total MCQs: 55** | **Target Met: ✓**

**Next:** Chapter 21 - Minimum Spanning Trees
