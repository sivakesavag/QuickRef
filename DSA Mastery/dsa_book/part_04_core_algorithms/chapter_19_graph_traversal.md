# Chapter 19: Graph Traversal

**Target:** 55 MCQs | **Distribution:** 14 Foundational, 22 Intermediate, 14 Advanced, 5 Expert

---

**Q19.1: Foundational - [Theory] - [BFS Overview]**

Breadth-First Search (BFS):

A) Explore all neighbors before going deeper
B) Uses a queue (FIFO)
C) O(V + E) time with adjacency list
D) All of the above

**Answer: D**

**Explanation:**
BFS: level-by-level exploration. Start from source, visit all distance-1 nodes, then distance-2, etc. Queue ensures FIFO order. Each vertex and edge processed once. O(V+E). Finds shortest path in unweighted graphs. Space: O(V) for visited array + queue.

---

**Q19.2: Foundational - [Theory] - [DFS Overview]**

Depth-First Search (DFS):

A) Explore as deep as possible, then backtrack
B) Uses stack (explicit or recursion call stack)
C) O(V + E) time with adjacency list
D) All of the above

**Answer: D**

**Explanation:**
DFS: go deep along one path until stuck, then backtrack. Recursive: natural call stack. Iterative: explicit stack. O(V+E): each vertex/edge visited once. Space: O(V) for visited + O(V) stack (worst case). Used for: cycle detection, topological sort, connected components, articulation points.

---

**Q19.3: Foundational - [Trace] - [BFS Traversal]**

BFS from vertex 0. Graph: 0-1, 0-2, 1-3, 2-3, 3-4:

A) Queue: [0]. Visit 0. Enqueue 1,2. Queue: [1,2]
B) Visit 1. Enqueue 3. Queue: [2,3]. Visit 2. 3 already queued. Queue: [3]
C) Visit 3. Enqueue 4. Queue: [4]. Visit 4. Queue empty
D) BFS order: 0, 1, 2, 3, 4. Level 0:{0}, Level 1:{1,2}, Level 2:{3}, Level 3:{4}

**Answer: D**

**Explanation:**
BFS from 0: neighbors 1,2 (level 1). From 1: neighbor 3 (level 2). From 2: neighbor 3 (already visited). From 3: neighbor 4 (level 3). Each vertex visited once. Shortest distances: d[0]=0, d[1]=1, d[2]=1, d[3]=2, d[4]=3.

---

**Q19.4: Foundational - [Trace] - [DFS Traversal]**

DFS from vertex 0. Graph: 0-1, 0-2, 1-3, 2-3, 3-4:

A) Visit 0 → neighbor 1 → neighbor 3 → neighbor 4 (dead end)
B) Backtrack to 3 → neighbor 2 (via 3-2? if exists). Actually 2-3 exists
C) Backtrack to 0 → neighbor 2 (already visited via 3? depends on edge order)
D) DFS order depends on neighbor processing order, one possibility: 0,1,3,2,4

**Answer: D**

**Explanation:**
DFS is order-dependent. Processing neighbors in order: from 0→1→3→2→4 or 0→1→3→4 (backtrack)→2. From 0: visit 1. From 1: visit 3. From 3: visit 2 and 4. One valid order: 0,1,3,2,4. Another: 0,1,3,4,2. Both correct DFS orderings.

---

**Q19.5: Foundational - [Theory] - [BFS Shortest Path]**

BFS finds shortest path in:

A) Unweighted graphs: minimum number of edges
B) Does NOT work for weighted graphs (use Dijkstra)
C) Shortest path tree: parent array records path
D) All of the above

**Answer: D**

**Explanation:**
BFS: discovers vertices in order of distance from source. First time a vertex is reached = shortest distance. Parent tracking: parent[v] = u when v discovered via u. Reconstruct path: follow parent pointers from destination to source. Only works for unweighted (or unit weight). For weighted: Dijkstra (Chapter 20).

---

**Q19.6: Foundational - [Theory] - [Connected Components]**

Finding connected components (undirected graph):

A) BFS or DFS from each unvisited vertex
B) Each traversal discovers one component
C) O(V + E) total
D) All of the above

**Answer: D**

**Explanation:**
Components: iterate all vertices. If unvisited: start BFS/DFS, mark all reachable vertices as same component. Count components = number of traversals started. O(V+E) total (each vertex/edge processed once across all traversals). Alternative: Union-Find (Chapter 15) for dynamic connectivity.

---

**Q19.7: Intermediate - [Theory] - [DFS Timestamps]**

DFS discovery and finish times:

A) discovery[v]: when v is first visited (pre-order)
B) finish[v]: when v's subtree is fully explored (post-order)
C) Useful for: classifying edges, topological sort
D) All of the above

**Answer: D**

**Explanation:**
DFS timestamps: global timer incremented on discover and finish. discovery[v] < discovery[w] < finish[w] < finish[v] means w is descendant of v. Parenthesis property: [disc[v], fin[v]] either contains [disc[w], fin[w]] (ancestor) or is disjoint (no relation). Foundation for edge classification and advanced DFS applications.

---

**Q19.8: Intermediate - [Theory] - [Edge Classification]**

DFS edge types in directed graph:

A) Tree edge: discovers new vertex
B) Back edge: to ancestor → indicates cycle
C) Forward edge: to descendant (not tree edge). Cross edge: to neither ancestor nor descendant
D) All of the above

**Answer: D**

**Explanation:**
Edge (u,v) classification: Tree: v undiscovered. Back: v discovered but not finished (ancestor in DFS tree). Forward: disc[u] < disc[v] and v finished. Cross: disc[u] > disc[v] and v finished. Cycle exists ⟺ back edge exists. In undirected graphs: only tree and back edges (no forward/cross).

---

**Q19.9: Intermediate - [Theory] - [Cycle Detection - Directed]**

Cycle detection in directed graph:

A) DFS with three states: white (unvisited), gray (in progress), black (finished)
B) Back edge (to gray node) indicates cycle
C) O(V + E)
D) All of the above

**Answer: D**

**Explanation:**
Three-color DFS: white=unvisited, gray=discovered but not finished (on recursion stack), black=finished. If DFS reaches a gray node: back edge → cycle. If only reaches white/black: no cycle from this path. O(V+E). Alternative: topological sort — if it can't process all vertices, cycle exists (Kahn's algorithm).

---

**Q19.10: Intermediate - [Theory] - [Cycle Detection - Undirected]**

Cycle detection in undirected graph:

A) DFS: if neighbor is visited AND not parent → cycle
B) BFS: if neighbor is visited AND not parent → cycle
C) Union-Find: if find(u) == find(v) for edge (u,v) → cycle
D) All are valid approaches

**Answer: D**

**Explanation:**
Undirected cycle: DFS finds back edge to non-parent visited vertex. Must track parent to avoid false positive on the edge we came from. BFS: similarly check non-parent visited neighbor. Union-Find: adding edge between same-component vertices creates cycle. All O(V+E). DFS is most common approach.

---

**Q19.11: Intermediate - [Theory] - [Topological Sort - Kahn's]**

Kahn's algorithm (BFS-based topological sort):

A) Compute in-degree of all vertices
B) Enqueue vertices with in-degree 0
C) Process: dequeue, add to result, reduce neighbors' in-degrees, enqueue new 0-degree
D) All of the above

**Answer: D**

**Explanation:**
Kahn's: BFS-like. Queue holds vertices with no incoming edges. Remove vertex, add to sorted order, reduce in-degrees of neighbors. New 0-degree vertices enqueued. If all vertices processed: valid topological order. If not: cycle exists (remaining vertices all have incoming edges). O(V+E).

---

**Q19.12: Intermediate - [Trace] - [Topological Sort]**

DAG: 5→2, 5→0, 4→0, 4→1, 2→3, 3→1. Kahn's:

A) In-degrees: 0:2, 1:2, 2:1, 3:1, 4:0, 5:0. Queue: [4,5]
B) Process 4: reduce 0,1. In-degrees: 0:1, 1:1. Process 5: reduce 2,0. 0:0→enqueue. 2:0→enqueue
C) Process 0. Process 2: reduce 3. 3:0→enqueue. Process 3: reduce 1. 1:0→enqueue. Process 1
D) One valid topological order: [4, 5, 0, 2, 3, 1]

**Answer: D**

**Explanation:**
Multiple valid orderings: [4,5,0,2,3,1], [5,4,2,0,3,1], [4,5,2,0,3,1], etc. All satisfy: every edge goes from earlier to later in ordering. 5 must come before 2 and 0. 4 must come before 0 and 1. 2 before 3. 3 before 1.

---

**Q19.13: Intermediate - [Theory] - [Topological Sort - DFS]**

DFS-based topological sort:

A) Run DFS, record vertices in reverse finish order
B) When vertex finishes (all descendants processed), push to front
C) Reverse of post-order gives topological order
D) All of the above

**Answer: D**

**Explanation:**
DFS topological sort: when a vertex finishes (all outgoing edges explored), add to stack/front of list. The last vertex to finish has no dependencies → goes first. Reverse post-order = topological order. If back edge found → cycle → no topological order. Same O(V+E) as Kahn's.

---

**Q19.14: Intermediate - [Theory] - [BFS Level Order]**

BFS for level-order processing:

A) Process all vertices at distance d before distance d+1
B) Track level: increment when all vertices of current level processed
C) Applications: shortest path, minimum operations, level-order tree traversal
D) All of the above

**Answer: D**

**Explanation:**
Level processing: track level boundaries. Method 1: process queue size at each level (snapshot size). Method 2: use two queues or sentinel. Level = distance from source. Each level processed in order. Applications: word ladder (BFS on word graph), maze shortest path, social network degree of separation.

---

**Q19.15: Intermediate - [Theory] - [Bipartite Check via BFS]**

Check bipartiteness using BFS:

A) Color source with color A
B) Color all neighbors with color B, their neighbors with A, etc.
C) If conflict (neighbor has same color): not bipartite
D) All of the above

**Answer: D**

**Explanation:**
2-coloring via BFS: color start A. Queue neighbors as B. Continue alternating. If a neighbor is already colored and color matches current → conflict → odd cycle → not bipartite. All vertices colored without conflict → bipartite. O(V+E). DFS works too (alternating colors during recursion).

---

**Q19.16: Intermediate - [Theory] - [0-1 BFS]**

0-1 BFS (edges with weight 0 or 1):

A) Use deque instead of queue
B) Weight-0 edge: add to front. Weight-1 edge: add to back
C) O(V + E) — like BFS but for 0/1 weighted graphs
D) All of the above

**Answer: D**

**Explanation:**
0-1 BFS: modified BFS for graphs with edge weights 0 or 1. Deque: 0-weight neighbors added to front (process immediately, same distance), 1-weight to back (next distance). Correct shortest paths without full Dijkstra overhead. O(V+E) vs Dijkstra's O((V+E) log V). Common in competitive programming.

---

**Q19.17: Advanced - [Theory] - [Strongly Connected Components]**

Strongly connected components (SCC) of directed graph:

A) Every vertex in SCC reachable from every other vertex in SCC
B) Kosaraju's: two DFS passes (one on G, one on G^T)
C) Tarjan's: single DFS with low-link values
D) All of the above

**Answer: D**

**Explanation:**
SCC: maximal subgraph where all pairs mutually reachable. Kosaraju's: DFS on G (record finish order), DFS on G^T (in reverse finish order → each DFS discovers one SCC). Tarjan's: single DFS, track discovery time and low-link (earliest reachable ancestor). Both O(V+E). Condensation: collapse SCCs → DAG.

---

**Q19.18: Advanced - [Trace] - [Kosaraju's Algorithm]**

Graph: 0→1, 1→2, 2→0, 1→3, 3→4, 4→3. Kosaraju's:

A) DFS on G: finish order (one possibility): [0,2,1,3,4] → stack: [4,3,1,2,0]
B) Transpose G^T: 1→0, 2→1, 0→2, 3→1, 4→3, 3→4
C) DFS on G^T in stack order: 4→3→4 (SCC {3,4}), 1→0→2→1 (SCC {0,1,2})
D) SCCs: {0,1,2} and {3,4}

**Answer: D**

**Explanation:**
First DFS finish order captures dependency. Transpose reverses reachability. Second DFS in reverse finish order: each new start discovers one SCC. {0,1,2}: cycle 0→1→2→0. {3,4}: cycle 3→4→3. Condensation DAG: {0,1,2}→{3,4}.

---

**Q19.19: Advanced - [Theory] - [Tarjan's SCC Algorithm]**

Tarjan's SCC algorithm:

A) Maintain disc[v] and low[v] for each vertex
B) low[v] = minimum disc reachable from subtree of v
C) If low[v] == disc[v]: v is root of an SCC
D) All of the above

**Answer: D**

**Explanation:**
Tarjan's: single DFS. disc[v] = discovery time. low[v] = min disc reachable via DFS subtree (through back edges). If low[v] == disc[v]: no vertex in v's subtree reaches above v → v is SCC root. Pop stack until v to extract SCC. O(V+E). Elegant single-pass algorithm.

---

**Q19.20: Advanced - [Theory] - [Articulation Points]**

Articulation point (cut vertex):

A) Vertex whose removal disconnects the graph
B) DFS: vertex u is AP if child v has low[v] ≥ disc[u]
C) Root is AP if it has ≥ 2 DFS children
D) All of the above

**Answer: D**

**Explanation:**
Articulation point: removing it increases number of connected components. DFS-based: if low[v] ≥ disc[u] (no back edge from v's subtree bypasses u), u is AP. Root special case: AP iff ≥ 2 children in DFS tree (removal splits DFS tree). O(V+E). Applications: network reliability, infrastructure vulnerability.

---

**Q19.21: Advanced - [Theory] - [Bridges]**

Bridge (cut edge):

A) Edge whose removal disconnects the graph
B) DFS: edge (u,v) is bridge if low[v] > disc[u]
C) Strict inequality (no back edge from v's subtree reaches u or above)
D) All of the above

**Answer: D**

**Explanation:**
Bridge: removing edge (u,v) disconnects graph. Condition: low[v] > disc[u] (vs ≥ for articulation point). No back edge from v's subtree reaches u or any ancestor of u. If low[v] = disc[u]: back edge reaches u, so removing (u,v) doesn't disconnect. O(V+E). Applications: network reliability analysis.

---

**Q19.22: Intermediate - [Theory] - [Multi-Source BFS]**

Multi-source BFS:

A) Start BFS from multiple sources simultaneously
B) Initialize queue with all source vertices
C) Each cell gets distance to nearest source
D) All of the above

**Answer: D**

**Explanation:**
Multi-source BFS: enqueue all sources at distance 0. BFS as normal. Each vertex gets shortest distance to any source. O(V+E). Applications: "01 matrix" (distance to nearest 0), rotting oranges (spread from all rotten simultaneously), nearest exit from fire. Clean technique for "nearest to any of multiple points."

---

**Q19.23: Intermediate - [Theory] - [Bidirectional BFS]**

Bidirectional BFS:

A) BFS from both source and target simultaneously
B) Alternate expanding from each side
C) When frontiers meet: shortest path found
D) All of the above

**Answer: D**

**Explanation:**
Bidirectional BFS: expand from source and target alternately. When a vertex appears in both visited sets: path found. If branching factor b and depth d: O(b^(d/2) + b^(d/2)) vs O(b^d). Exponential speedup. Works when target is known and edges are reversible. Common for word ladder, puzzle shortest path.

---

**Q19.24: Foundational - [Theory] - [DFS vs BFS Comparison]**

DFS vs BFS:

A) BFS: shortest path (unweighted), level-order, uses queue
B) DFS: cycle detection, topological sort, SCC, uses stack
C) Both O(V+E), both find all reachable vertices
D) All of the above

**Answer: D**

**Explanation:**
BFS: breadth exploration, queue, shortest path. DFS: depth exploration, stack/recursion, path properties. Choose based on problem: shortest path → BFS. Cycle/topo sort → DFS. Connected components → either. In practice, DFS is simpler to implement recursively; BFS requires explicit queue.

---

**Q19.25: Intermediate - [Theory] - [Iterative DFS vs Recursive]**

Iterative DFS vs recursive DFS:

A) Recursive: simple, but limited by stack depth
B) Iterative: explicit stack, handles large graphs
C) Iterative may visit nodes in different order (depends on push order)
D) All of the above

**Answer: D**

**Explanation:**
Recursive DFS: clean code, stack overflow risk for large graphs (n > 10^5 in some languages). Iterative: explicit stack, no overflow. Subtlety: recursive processes neighbors in order; iterative with stack processes in reverse (LIFO). For identical order: push neighbors in reverse. Pre/post-order timestamps require additional bookkeeping in iterative.

---

**Q19.26: Intermediate - [Theory] - [DFS on Grid]**

DFS/BFS on 2D grid:

A) Grid cells as vertices, 4 (or 8) neighbors as edges
B) "Number of islands": DFS/BFS from each unvisited land cell
C) Mark visited to avoid revisiting
D) All of the above

**Answer: D**

**Explanation:**
Grid graph: cell (r,c) connects to (r±1,c) and (r,c±1). Boundaries: check 0 ≤ r < rows, 0 ≤ c < cols. Islands: count connected components of '1' cells. BFS/DFS from each unvisited '1', mark all connected as visited. O(rows × cols). Flood fill: same technique (paint connected region).

---

**Q19.27: Advanced - [Theory] - [Euler Tour/Path]**

Euler path and circuit:

A) Euler path: traverse every edge exactly once
B) Euler circuit: path that returns to start
C) Undirected: circuit exists iff all vertices have even degree and graph is connected
D) All of the above

**Answer: D**

**Explanation:**
Euler circuit: all vertices even degree + connected. Euler path (not circuit): exactly 2 vertices with odd degree. Directed: circuit iff in-degree = out-degree for all + strongly connected. Hierholzer's algorithm: O(V+E) construction. Applications: Chinese postman problem, DNA sequence assembly, route planning.

---

**Q19.28: Advanced - [Theory] - [Hierholzer's Algorithm]**

Hierholzer's algorithm for Euler circuit:

A) Start at any vertex, follow edges, removing as used
B) When stuck (no unused edges from current): backtrack, insert into circuit
C) O(V + E) — each edge processed once
D) All of the above

**Answer: D**

**Explanation:**
Hierholzer's: DFS, delete edges as traversed. When stuck: current vertex added to circuit. Continue from last vertex with unused edges. Stack-based: push vertices, when no neighbors, pop to circuit. Result in reverse order. O(V+E). More efficient than Fleury's algorithm (which is O(E²)).

---

**Q19.29: Foundational - [Theory] - [BFS Space Complexity]**

BFS space complexity:

A) O(V) for visited array
B) Queue can hold O(V) vertices in worst case
C) Total: O(V)
D) All of the above

**Answer: D**

**Explanation:**
BFS space: visited array O(V) + queue. Queue worst case: all vertices at same level. Complete binary tree: bottom level has n/2 nodes. Complete graph: first expansion queues V-1. So queue: O(V). Total BFS space: O(V). DFS: O(V) visited + O(V) stack (depth). Both O(V) but BFS typically uses more queue space than DFS uses stack.

---

**Q19.30: Expert - [Theory] - [Iterative Deepening DFS]**

Iterative Deepening DFS (IDDFS):

A) DFS with increasing depth limits: 1, 2, 3, ...
B) Combines BFS's shortest-path guarantee with DFS's space efficiency
C) O(b^d) time (same as BFS), O(d) space (same as DFS)
D) All of the above

**Answer: D**

**Explanation:**
IDDFS: depth-limited DFS, increment limit until solution found. Redundant work: level d visited O(d) times total. But since most nodes are at deepest level, overhead is only O(b/(b-1)) ≈ constant factor. Space: O(d) stack only. Best of both: optimal shortest path + linear space. Used in game AI (chess, etc.).

---

**Q19.31: Intermediate - [Theory] - [Shortest Path in Unweighted Graph]**

Shortest path reconstruction from BFS:

A) Maintain parent[v] = vertex that discovered v
B) Reconstruct: follow parent from destination to source
C) Reverse path gives source → destination
D) All of the above

**Answer: D**

**Explanation:**
BFS parent tracking: when vertex v discovered from u, set parent[v] = u. Path: start at destination, follow parent pointers to source. Reverse for source→dest. Path length = number of edges. Multiple shortest paths possible (BFS tree is not unique). Modification: store all parents for all shortest paths.

---

**Q19.32: Intermediate - [Theory] - [Graph Coloring via BFS/DFS]**

Graph coloring via BFS/DFS:

A) Assign colors to vertices so no two adjacent share a color
B) Bipartite check = 2-coloring (BFS/DFS)
C) General k-coloring: NP-complete for k ≥ 3
D) All of the above

**Answer: D**

**Explanation:**
2-coloring: polynomial, equivalent to bipartite check. 3-coloring: NP-complete. Greedy coloring: O(V+E) but doesn't guarantee minimum colors. Chromatic number (minimum colors): NP-hard in general. Planar graphs: always 4-colorable (four color theorem). Applications: scheduling, register allocation, map coloring.

---

**Q19.33: Advanced - [Theory] - [DFS Tree Properties]**

DFS tree properties:

A) Every non-tree edge connects an ancestor to a descendant (in undirected graphs)
B) No cross edges in undirected DFS
C) Back edges indicate cycles
D) All of the above

**Answer: D**

**Explanation:**
Undirected DFS: only tree edges and back edges. No forward or cross edges (if such existed, the "cross" vertex would have been discovered earlier). This simplifies undirected graph analysis. Directed DFS: all four edge types possible. This structural property is fundamental to algorithms for bridges, articulation points, biconnected components.

---

**Q19.34: Advanced - [Theory] - [Biconnected Components]**

Biconnected components:

A) Maximal subgraph with no cut vertex (removing any single vertex doesn't disconnect it)
B) Found using DFS + articulation point detection
C) Edge-based decomposition (each edge belongs to exactly one biconnected component)
D) All of the above

**Answer: D**

**Explanation:**
Biconnected: no articulation point → removing any vertex leaves graph connected. 2-edge-connected: no bridge. Found by modifying articulation point algorithm: maintain edge stack, pop component when AP found. Block-cut tree: tree of biconnected components and cut vertices. O(V+E). Applications: robust network design.

---

**Q19.35: Expert - [Theory] - [Lexicographic BFS]**

Lexicographic BFS (Lex-BFS):

A) BFS variant that visits vertices in lexicographic order of neighborhoods
B) Used for: perfect elimination ordering, chordal graph recognition
C) O(V + E) with partition refinement
D) All of the above

**Answer: D**

**Explanation:**
Lex-BFS: vertices ordered so that vertices with "more important" neighbors come first. Produces perfect elimination ordering for chordal graphs. Implementation: partition refinement, O(V+E). Chordal graph recognition: Lex-BFS + verify. Applications: minimum coloring/clique on chordal graphs. Specialized but powerful for graph structure analysis.

---

**Q19.36: Intermediate - [Theory] - [Flood Fill]**

Flood fill algorithm:

A) Start from a cell, change all connected same-color cells
B) BFS or DFS on grid
C) O(rows × cols) — visit each cell at most once
D) All of the above

**Answer: D**

**Explanation:**
Flood fill: paint connected region. Used in: paint bucket tool, image segmentation, mine sweeper (reveal empty cells). DFS: simple recursion. BFS: queue-based. Both equivalent for this purpose. Boundary check + same-color check before processing. Mark as visited before enqueueing (avoid duplicates).

---

**Q19.37: Expert - [Theory] - [DFS Ordering Applications]**

DFS orderings enable:

A) Topological sort: reverse post-order on DAG
B) SCC: Kosaraju's uses post-order; Tarjan's uses low-link
C) Articulation points/bridges: pre-order + low-link
D) All of the above, plus Euler tour for subtree queries

**Answer: D**

**Explanation:**
DFS orderings are versatile: pre-order for discovery, post-order for completion, reverse post-order for topological sort. Euler tour (entry/exit times) flattens tree for range queries (Chapter 16). Low-link values enable bridge/AP/SCC detection. DFS is the Swiss Army knife of graph algorithms.

---

**Q19.38: Foundational - [Theory] - [Visited Array]**

Why track visited vertices in BFS/DFS?

A) Prevent infinite loops (cycles in undirected graphs)
B) Prevent revisiting (unnecessary work)
C) Ensure O(V+E) complexity (each vertex processed once)
D) All of the above

**Answer: D**

**Explanation:**
Without visited tracking: DFS would loop forever on cycles. BFS would re-enqueue visited vertices, potentially O(V×E). Visited ensures each vertex processed once, each edge examined at most twice (once from each endpoint in undirected). Critical for correctness and efficiency. Mark before or when enqueueing (BFS) or when recursing (DFS).

---

**Q19.39: Intermediate - [Theory] - [BFS on Implicit Graph]**

BFS on implicit graph (state-space search):

A) States generated on-the-fly, not pre-stored
B) Example: word ladder, puzzle states, game tree
C) Track visited states with hash set
D) All of the above

**Answer: D**

**Explanation:**
Implicit graph: state space too large to store. Generate neighbors as needed. BFS finds shortest path in state space. Visited: hash set for arbitrary states. Example: word ladder — states are words, edges connect words differing by one letter. BFS finds minimum transformations. Memory: O(reachable states).

---

**Q19.40: Advanced - [Theory] - [Condensation Graph]**

SCC condensation:

A) Collapse each SCC into single vertex
B) Result is a DAG
C) Topological sort of condensation gives SCC processing order
D) All of the above

**Answer: D**

**Explanation:**
Condensation: replace each SCC with one "super-vertex." Edges between SCCs preserved. Result is always a DAG (if cycle existed between super-vertices, they'd be in the same SCC). Useful for: 2-SAT, reachability queries, computing minimum reaching cost. Process DAG topologically for DP on SCCs.

---

**Q19.41: Expert - [Theory] - [Planarity Testing]**

Planarity testing:

A) Determine if graph can be drawn without edge crossings
B) O(V) algorithm exists (Hopcroft-Tarjan, Boyer-Myrvold)
C) Based on DFS and embedding
D) All of the above

**Answer: D**

**Explanation:**
Planarity: can graph be embedded in plane? Kuratowski's theorem: non-planar iff contains K_5 or K_{3,3} subdivision. Efficient test: DFS-based O(V) algorithms. Hopcroft-Tarjan (1974): first linear algorithm. Boyer-Myrvold (2004): simpler linear algorithm. Fundamental in graph theory with applications in circuit design, geographic mapping.

---

**Q19.42: Foundational - [Theory] - [BFS vs DFS Applications Summary]**

When to use BFS vs DFS:

A) BFS: shortest path, level-order, minimum operations
B) DFS: cycle detection, topological sort, SCC, backtracking
C) Either: connected components, reachability, flood fill
D) All correct guidelines

**Answer: D**

**Explanation:**
BFS ideal for: shortest path in unweighted, level-order traversal, multi-source proximity. DFS ideal for: topological sort, SCC, articulation points, bridges, all paths. Either works for: connectivity, reachability, island counting. Understanding which to apply is key to solving graph problems efficiently.

---

**Q19.43: Intermediate - [Theory] - [Multi-Source BFS]**

Multi-source BFS:

A) Start BFS from multiple source nodes simultaneously
B) Initialize queue with all sources at distance 0
C) Finds shortest distance from nearest source for every node
D) All of the above — O(V + E)

**Answer: D**

**Explanation:**
Multi-source BFS: add all source nodes to queue with distance 0 at start. Process normally. Each node gets shortest distance to its nearest source. Applications: "nearest 0" in binary matrix, "rotten oranges" (spread from all rotten simultaneously). Same complexity as single-source BFS — just multiple starting points.

---

**Q19.44: Intermediate - [Theory] - [Tree Diameter via BFS/DFS]**

Finding tree diameter (longest path):

A) BFS from any node u → find farthest node v
B) BFS from v → find farthest node w → dist(v,w) = diameter
C) Two BFS/DFS traversals suffice
D) All of the above — O(V)

**Answer: D**

**Explanation:**
Tree diameter: longest shortest path between any two nodes. Algorithm: pick any node, BFS/DFS to find farthest. From that node, BFS/DFS again to find farthest. That distance = diameter. Proof: farthest from any node must be an endpoint of the diameter. Two traversals = O(V). Works only for trees (unique paths).

---

**Q19.45: Foundational - [Theory] - [Euler Path and Circuit Detection]**

Euler path/circuit existence:

A) Euler circuit: all vertices have even degree (undirected)
B) Euler path: exactly 0 or 2 vertices have odd degree
C) Graph must be connected (ignoring isolated vertices)
D) All of the above

**Answer: D**

**Explanation:**
Euler circuit (visit every edge exactly once, return to start): all degrees even + connected. Euler path (visit every edge, may end at different vertex): exactly 2 odd-degree vertices (they are endpoints). Finding the path: Hierholzer's algorithm O(E). Directed: in-degree = out-degree for circuit. Distinct from Hamiltonian path (visits every vertex).

---

**Q19.46: Intermediate - [Theory] - [Iterative DFS with Explicit Stack]**

Converting recursive DFS to iterative:

A) Use explicit stack instead of call stack
B) Push start node, pop and process in loop
C) Push neighbors in reverse order for same visit order
D) All of the above

**Answer: D**

**Explanation:**
Iterative DFS: stack replaces recursion. Push start. While stack not empty: pop node, if not visited: mark visited, process, push unvisited neighbors. Reverse push order to match recursive DFS visit order. Avoids stack overflow on deep graphs. Same O(V+E) complexity. Important for graphs with >10K nodes where recursion depth is limited.

---

**Q19.47: Advanced - [Theory] - [Bidirectional BFS]**

Bidirectional BFS:

A) BFS simultaneously from source and target
B) Meet in the middle — explores O(b^(d/2)) instead of O(b^d)
C) Terminates when frontiers intersect
D) All of the above

**Answer: D**

**Explanation:**
Bidirectional BFS: two simultaneous BFS expansions. Forward from source, backward from target. Stop when a node is discovered by both. If branching factor b and distance d: single BFS visits O(b^d) nodes. Bidirectional: O(2 × b^(d/2)) — exponentially fewer. Optimal for unweighted shortest path when both endpoints known. Used in social network distance queries (Six Degrees).

---

**Q19.48: Intermediate - [Theory] - [Cycle Detection 3-Color DFS]**

Three-color DFS for cycle detection in directed graphs:

A) WHITE: unvisited, GRAY: in current DFS path, BLACK: fully processed
B) Back edge (to GRAY node) indicates cycle
C) Edge to BLACK node: no cycle (already finished)
D) All of the above

**Answer: D**

**Explanation:**
Three-color scheme: WHITE=unvisited, GRAY=being explored (on recursion stack), BLACK=done. Start: all WHITE. Enter node: mark GRAY. Finish node: mark BLACK. If we encounter GRAY neighbor: back edge = cycle! GRAY→BLACK→BLACK: cross/forward edge, no cycle. This precisely identifies directed cycles. Undirected simpler: any visited non-parent = cycle.

---

**Q19.49: Advanced - [Theory] - [Finding All Paths Between Two Nodes]**

Finding all paths from source to target:

A) Use DFS with backtracking
B) Mark node as visited when entering, unmark when backtracking
C) Cannot use BFS (BFS doesn't naturally track paths)
D) All of the above — exponential worst case

**Answer: D**

**Explanation:**
All paths: DFS + backtracking. Visit node, add to current path. At target: record path. Backtrack: remove from path, unvisit. Must unvisit (unlike standard DFS) to allow node reuse in different paths. Worst case: exponential paths (e.g., complete graph). BFS variant possible but requires storing all partial paths — memory-intensive. Practical only for small graphs or few paths.

---

**Q19.50: Intermediate - [Theory] - [Graph Coloring via BFS (m-coloring)]**

Using BFS for graph coloring:

A) BFS assigns colors level by level
B) Greedy: assign smallest available color not used by neighbors
C) BFS ordering gives good (but not optimal) coloring
D) All of the above

**Answer: D**

**Explanation:**
BFS-based greedy coloring: BFS traversal order, assign each node the smallest color not used by already-colored neighbors. Guarantees valid coloring but not necessarily minimum colors. For bipartite: BFS 2-coloring is optimal. General: optimal coloring is NP-hard. BFS greedy: at most Δ+1 colors (Δ = max degree). Often sufficient in practice. Welsh-Powell: degree-ordered greedy is also popular.

---

## Chapter 19 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 11 | BFS/DFS basics, traversal order, shortest path, connected components, visited array, Euler path |
| Intermediate | 23 | Timestamps, edge types, cycles, topological sort, bipartite, 0-1 BFS, grid traversal, multi-source BFS, tree diameter, iterative DFS, 3-color, graph coloring |
| Advanced | 12 | SCC (Kosaraju/Tarjan), articulation points, bridges, Euler tour, biconnected, bidirectional BFS, all paths |
| Expert | 4 | IDDFS, Lex-BFS, planarity testing, DFS ordering applications |

**Total MCQs: 50** | **Target Met: ✓**

**Next:** Chapter 20 - Shortest Path Algorithms
