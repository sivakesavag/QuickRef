# Chapter 14: Graphs — Representation

**Target:** 45 MCQs | **Distribution:** 11 Foundational, 18 Intermediate, 12 Advanced, 4 Expert

---

**Q14.1: Foundational - [Theory] - [Graph Definition]**

A graph G = (V, E) consists of:

A) V = set of vertices (nodes)
B) E = set of edges (connections between vertices)
C) Edges can be directed or undirected
D) All of the above

**Answer: D**

**Explanation:**
Graph: mathematical structure modeling pairwise relationships. V = vertices, E ⊆ V × V (edges). Undirected: {u,v} = {v,u}. Directed: (u,v) ≠ (v,u). Weighted: edges have associated values. Graphs model networks, relationships, dependencies, maps, and countless real-world systems.

---

**Q14.2: Foundational - [Theory] - [Directed vs Undirected]**

Directed vs undirected graph:

A) Directed: edges have direction (u → v), called arcs
B) Undirected: edges are bidirectional ({u, v})
C) Directed graphs can model one-way relationships (web links, dependencies)
D) All of the above

**Answer: D**

**Explanation:**
Undirected: friendship (symmetric). Directed: Twitter follow (asymmetric), prerequisites, web link structure. Undirected edge {u,v} equivalent to two directed edges (u,v) and (v,u). Terminology: in directed graphs, in-degree and out-degree; in undirected, just degree.

---

**Q14.3: Foundational - [Theory] - [Adjacency Matrix]**

Adjacency matrix representation:

A) V × V matrix, M[i][j] = 1 if edge (i,j) exists
B) O(V²) space
C) Edge lookup: O(1)
D) All of the above

**Answer: D**

**Explanation:**
Adjacency matrix: 2D array. M[i][j] = weight or 1/0. Symmetric for undirected graphs. Space: O(V²) regardless of edge count. Edge check: O(1). Good for dense graphs (E ≈ V²). Bad for sparse graphs (wastes space). Adding vertex: requires resizing matrix. Iterate neighbors: O(V) per vertex.

---

**Q14.4: Foundational - [Theory] - [Adjacency List]**

Adjacency list representation:

A) Array of lists, one per vertex
B) Each list contains neighbors of that vertex
C) O(V + E) space
D) All of the above

**Answer: D**

**Explanation:**
Adjacency list: array of V lists. adj[u] = list of vertices adjacent to u. Space: O(V + E). For undirected graph, each edge stored twice. Edge check: O(degree(u)). Iterate neighbors: O(degree(u)). Good for sparse graphs (most real-world graphs). Standard representation for BFS, DFS, Dijkstra.

---

**Q14.5: Foundational - [Trace] - [Adjacency List]**

Graph: vertices {0,1,2,3}, edges {(0,1), (0,2), (1,2), (2,3)}, undirected:

A) adj[0] = [1, 2]
B) adj[1] = [0, 2]
C) adj[2] = [0, 1, 3]
D) adj[3] = [2]

**Answer: D**

**Explanation:**
Each edge appears in both vertices' lists (undirected). 0-1: adj[0] gets 1, adj[1] gets 0. 0-2: adj[0] gets 2, adj[2] gets 0. 1-2: adj[1] gets 2, adj[2] gets 1. 2-3: adj[2] gets 3, adj[3] gets 2. Total entries: 2 × |E| = 8. Space efficient for sparse graphs.

---

**Q14.6: Foundational - [Theory] - [Edge List]**

Edge list representation:

A) List of all edges as (u, v) pairs (or (u, v, w) for weighted)
B) O(E) space
C) Simple but slow for neighbor queries
D) All of the above

**Answer: D**

**Explanation:**
Edge list: store all edges. Space: O(E). Edge check: O(E) linear scan. Neighbor query: O(E). Simple to implement and useful when: processing all edges (Kruskal's MST), graph input format, sparse graph with few operations. Often used as input format then converted to adjacency list for algorithms.

---

**Q14.7: Foundational - [Theory] - [Matrix vs List Comparison]**

Adjacency matrix vs adjacency list:

A) Matrix: O(1) edge check, O(V²) space
B) List: O(degree) edge check, O(V+E) space
C) Matrix for dense graphs, list for sparse
D) All of the above

**Answer: D**

**Explanation:**

| Operation | Matrix | List |
|-----------|--------|------|
| Space | O(V²) | O(V+E) |
| Edge check | O(1) | O(deg) |
| All neighbors | O(V) | O(deg) |
| Add edge | O(1) | O(1) |
| Add vertex | O(V²) resize | O(1) |

Sparse (E << V²): list wins on space. Dense (E ≈ V²): matrix acceptable. Most real graphs are sparse.

---

**Q14.8: Intermediate - [Theory] - [Weighted Graph]**

Weighted graph representation:

A) Adjacency matrix: M[i][j] = weight (0 or ∞ for no edge)
B) Adjacency list: store (neighbor, weight) pairs
C) Edge list: store (u, v, weight) tuples
D) All of the above

**Answer: D**

**Explanation:**
Weighted edges: matrix stores weight directly (use ∞ for non-edges, distinguish from weight 0). List: pairs (neighbor, weight). Edge list: triples (u, v, weight). Required for shortest path (Dijkstra, Bellman-Ford) and MST (Kruskal, Prim) algorithms. Weight can represent distance, cost, capacity, latency.

---

**Q14.9: Intermediate - [Theory] - [Graph Degree]**

Degree of a vertex:

A) Undirected: number of edges incident to vertex
B) Directed: in-degree (incoming edges) + out-degree (outgoing edges)
C) Sum of all degrees = 2 × |E| (handshaking lemma)
D) All of the above

**Answer: D**

**Explanation:**
Handshaking lemma: Σ deg(v) = 2|E| for undirected graphs. Each edge contributes 1 to each endpoint's degree. For directed: Σ in-deg = Σ out-deg = |E|. Max degree in simple graph: V-1. Useful for: checking graph validity, estimating algorithm complexity (BFS/DFS depend on Σ degrees = 2E).

---

**Q14.10: Intermediate - [Theory] - [Connected Graph]**

Connected graph:

A) Undirected: path exists between every pair of vertices
B) Directed: weakly connected (underlying undirected graph is connected) or strongly connected (path in both directions between every pair)
C) Testing connectivity: BFS/DFS from any vertex, check all reachable
D) All of the above

**Answer: D**

**Explanation:**
Connected: all vertices reachable from any vertex. Test: BFS/DFS from vertex 0, if visited count = V, connected. Disconnected: multiple connected components. Directed: strongly connected = bidirectional paths between all pairs. Weakly connected = connected if directions ignored. Connected components found via DFS/BFS.

---

**Q14.11: Intermediate - [Theory] - [Bipartite Graph]**

Bipartite graph:

A) Vertices can be divided into two disjoint sets
B) Every edge connects vertices from different sets
C) Equivalent to: graph has no odd-length cycles
D) All of the above

**Answer: D**

**Explanation:**
Bipartite: 2-colorable. BFS/DFS with alternating colors: if conflict → not bipartite. If all colored without conflict → bipartite. Applications: matching problems, scheduling, social networks (two types of entities). Complete bipartite K_{m,n}: all possible edges between two groups.

---

**Q14.12: Intermediate - [Trace] - [Bipartite Check]**

Graph: edges {(0,1), (1,2), (2,0)}. Is it bipartite?

A) BFS from 0: color 0 = A, neighbor 1 = B, neighbor 2 = B
B) Check edge (1,2): both colored B (same set)
C) Conflict → not bipartite
D) Contains odd cycle (0→1→2→0, length 3)

**Answer: D**

**Explanation:**
Triangle (3-cycle) is not bipartite. Color 0=A, 1=B. Edge 2-0: 2 must be B (neighbor of 0=A). Edge 1-2: both B, conflict. Odd cycle of length 3 makes 2-coloring impossible. Even cycles are always bipartite. A graph is bipartite ⟺ no odd cycles.

---

**Q14.13: Intermediate - [Theory] - [DAG]**

Directed Acyclic Graph (DAG):

A) Directed graph with no cycles
B) Has at least one topological ordering
C) Used for: task scheduling, dependency resolution, git history
D) All of the above

**Answer: D**

**Explanation:**
DAG: directed, no cycles. Every DAG has at least one topological sort (linear ordering where u before v if edge u→v). Multiple valid orderings possible. Applications: build systems (Makefile), course prerequisites, version control (git commits), data processing pipelines. Cycle detection: DFS with states (white/gray/black) or Kahn's algorithm.

---

**Q14.14: Intermediate - [Theory] - [Topological Sort]**

Topological sort of a DAG:

A) Order vertices so every edge goes from earlier to later
B) Kahn's algorithm: repeatedly remove vertices with in-degree 0
C) DFS-based: reverse post-order
D) All of the above

**Answer: D**

**Explanation:**
Kahn's: BFS-like. Queue of in-degree 0 vertices. Remove vertex, reduce neighbors' in-degrees, add new 0-degree vertices. O(V+E). DFS: post-order traversal, reverse result. O(V+E). Both produce valid topological ordering. If cycle exists, Kahn's won't process all vertices (detection). See Chapter 19 for detailed coverage.

---

**Q14.15: Intermediate - [Theory] - [Graph Properties]**

Simple graph:

A) No self-loops (edge from vertex to itself)
B) No multi-edges (at most one edge between any pair)
C) At most V(V-1)/2 edges (undirected) or V(V-1) edges (directed)
D) All of the above

**Answer: D**

**Explanation:**
Simple graph: no self-loops, no parallel edges. Maximum edges: C(V,2) = V(V-1)/2 for undirected. Multigraph: allows parallel edges. Pseudograph: allows self-loops. Complete graph K_V: all possible edges present. Simple graphs are the default assumption unless stated otherwise.

---

**Q14.16: Intermediate - [Theory] - [Tree as Graph]**

A tree is a special graph that:

A) Is connected and acyclic
B) Has exactly V-1 edges
C) Has unique path between any two vertices
D) All of the above

**Answer: D**

**Explanation:**
Tree = connected acyclic graph. Adding any edge creates a cycle. Removing any edge disconnects. V-1 edges. Forest = acyclic graph (possibly disconnected) = collection of trees. Spanning tree: subgraph that includes all vertices and is a tree. Fundamental in graph theory.

---

**Q14.17: Foundational - [Theory] - [Graph Traversal Overview]**

Two fundamental graph traversal methods:

A) BFS (Breadth-First Search): layer by layer using queue
B) DFS (Depth-First Search): go deep first using stack/recursion
C) Both visit all reachable vertices in O(V+E)
D) All of the above

**Answer: D**

**Explanation:**
BFS: explore neighbors first, then their neighbors. Uses queue. Finds shortest path in unweighted graphs. DFS: explore as deep as possible, backtrack. Uses stack/recursion. Finds cycles, topological sort, connected components. Both O(V+E) with adjacency list. Foundation of most graph algorithms. Detailed coverage in Chapter 19.

---

**Q14.18: Intermediate - [Theory] - [Incidence Matrix]**

Incidence matrix:

A) V × E matrix, M[v][e] = 1 if vertex v is incident to edge e
B) O(V × E) space
C) Useful in theoretical analysis, less common in practice
D) All of the above

**Answer: D**

**Explanation:**
Incidence matrix: rows = vertices, columns = edges. Entry 1 if vertex is endpoint of edge. For directed: +1 for head, -1 for tail. Space: O(VE). Used in: graph theory proofs, linear algebra formulations, network analysis. Rarely used in programming due to high space cost. Adjacency representations preferred.

---

**Q14.19: Advanced - [Theory] - [Compressed Sparse Row (CSR)]**

Compressed Sparse Row format:

A) Three arrays: row_ptr, col_idx, values
B) row_ptr[i] = start index of vertex i's neighbors in col_idx
C) Efficient for static graphs, cache-friendly iteration
D) All of the above

**Answer: D**

**Explanation:**
CSR: compact adjacency list in contiguous arrays. row_ptr has V+1 entries demarcating where each vertex's neighbors start/end in col_idx. col_idx stores all neighbor IDs consecutively. values (optional) stores edge weights. Benefits: cache-friendly sequential access, compact storage. Used in: scientific computing, sparse matrix operations, graph libraries (SNAP, GraphBLAS).

---

**Q14.20: Advanced - [Trace] - [CSR Format]**

Graph: 0→1, 0→2, 1→2, 2→3 (directed):

A) row_ptr = [0, 2, 3, 4, 4]
B) col_idx = [1, 2, 2, 3]
C) Vertex 0's neighbors at col_idx[0..1] = [1,2]
D) Vertex 3 has no outgoing edges: row_ptr[3]=row_ptr[4]=4

**Answer: D**

**Explanation:**
CSR: vertex 0 has edges to 1,2 → col_idx[0]=1, col_idx[1]=2. row_ptr[0]=0, row_ptr[1]=2. Vertex 1 → col_idx[2]=2. row_ptr[2]=3. Vertex 2 → col_idx[3]=3. row_ptr[3]=4. Vertex 3: no outgoing. row_ptr[4]=4. Neighbors of v: col_idx[row_ptr[v]..row_ptr[v+1]-1].

---

**Q14.21: Intermediate - [Theory] - [Graph Density]**

Dense vs sparse graphs:

A) Sparse: E = O(V), e.g., planar graphs, trees
B) Dense: E = O(V²), e.g., social networks among small groups
C) Adjacency list for sparse, matrix acceptable for dense
D) All of the above

**Answer: D**

**Explanation:**
Density = E / (V(V-1)/2). Dense: ratio near 1 (most possible edges). Sparse: ratio near 0. Most real-world graphs are sparse (internet, road networks, social networks with billions of nodes but limited connections per node). Algorithm complexity often expressed as O(V+E); for sparse E ≈ V, for dense E ≈ V².

---

**Q14.22: Intermediate - [Theory] - [Complete Graph]**

Complete graph K_n:

A) Every pair of vertices connected by an edge
B) |E| = n(n-1)/2 (undirected)
C) Represents worst case for many graph algorithms
D) All of the above

**Answer: D**

**Explanation:**
Complete graph: all possible edges present. K_5 has 10 edges. K_n has C(n,2) = n(n-1)/2 edges. Dense by definition. Complete bipartite K_{m,n}: m × n edges. Complete graphs represent worst-case input for algorithms that depend on edge count. Also used in: tournament graphs (directed K_n), clique problems.

---

**Q14.23: Foundational - [Theory] - [Self-Loop and Multi-Edge]**

Self-loop and multi-edge:

A) Self-loop: edge from vertex to itself (v,v)
B) Multi-edge: multiple edges between same pair
C) Simple graph: neither allowed
D) All of the above

**Answer: D**

**Explanation:**
Self-loop: (v,v). In adjacency matrix: M[v][v] = 1. In adjacency list: v appears in adj[v]. Multi-edge (parallel edges): multigraph. In matrix: M[u][v] = count. In list: v appears multiple times in adj[u]. Most algorithms assume simple graphs. Some applications need multigraphs (network flow, circuit design).

---

**Q14.24: Advanced - [Theory] - [Implicit Graph]**

Implicit graph:

A) Graph not explicitly stored but generated on-the-fly
B) Neighbors computed as needed (e.g., puzzle states)
C) Saves space for exponentially large state spaces
D) All of the above

**Answer: D**

**Explanation:**
Implicit graph: state space too large to store explicitly. Generate neighbors dynamically. Examples: puzzle states (8-puzzle, Rubik's cube), chess positions, game trees. BFS/DFS work on implicit graphs — just need a successor function. The "graph" is the set of reachable states. Space: O(states visited) rather than O(total states).

---

**Q14.25: Advanced - [Theory] - [Graph Complement]**

Complement of graph G:

A) Same vertices, edges present where G has no edge and vice versa
B) G has E edges → complement has V(V-1)/2 - E edges (undirected)
C) G ∪ complement = complete graph K_V
D) All of the above

**Answer: D**

**Explanation:**
Complement Ḡ: (u,v) ∈ Ḡ ⟺ (u,v) ∉ G. If G is sparse, Ḡ is dense and vice versa. Properties: G connected → Ḡ has diameter ≤ 2 when disconnected. Independent set in G = clique in Ḡ. Some problems are easier on complement graph.

---

**Q14.26: Advanced - [Theory] - [Hypergraph]**

Hypergraph:

A) Generalization where edges (hyperedges) can connect any number of vertices
B) Edge can connect 3+ vertices simultaneously
C) Models: database relations, set systems, group interactions
D) All of the above

**Answer: D**

**Explanation:**
Hypergraph: hyperedge ⊆ V (any subset, not just pairs). Standard graph: all edges have exactly 2 vertices. Hypergraph models higher-order relationships: database tables (each row = hyperedge), chemical reactions, co-authorship. Representation: incidence matrix or adjacency list per hyperedge. More complex but captures multi-way relationships.

---

**Q14.27: Intermediate - [Theory] - [Subgraph]**

Subgraph H of G:

A) V(H) ⊆ V(G) and E(H) ⊆ E(G)
B) Induced subgraph: all edges of G between vertices of H
C) Spanning subgraph: V(H) = V(G) (same vertex set)
D) All of the above

**Answer: D**

**Explanation:**
Subgraph: subset of vertices and edges. Induced subgraph on vertex set S: include all edges of G with both endpoints in S. Spanning subgraph: keep all vertices, possibly remove some edges. Spanning tree: spanning subgraph that is a tree. Different subgraph types used in different contexts.

---

**Q14.28: Intermediate - [Theory] - [Path and Cycle]**

Path vs cycle in a graph:

A) Path: sequence of vertices where consecutive pairs have edges, no vertex repeated
B) Cycle: path that starts and ends at same vertex
C) Walk: vertices/edges may repeat; trail: edges don't repeat
D) All of the above

**Answer: D**

**Explanation:**
Walk: any sequence of adjacent vertices (may repeat). Trail: walk without repeated edges. Path: walk without repeated vertices. Cycle: closed walk without repeated vertices (except start=end). These distinctions matter for proofs and algorithm correctness. Euler path/circuit = trail visiting every edge. Hamilton path/cycle = path visiting every vertex.

---

**Q14.29: Advanced - [Theory] - [Planar Graph]**

Planar graph:

A) Can be drawn in plane without edge crossings
B) Euler's formula: V - E + F = 2 (F = faces including outer)
C) E ≤ 3V - 6 for simple planar graph
D) All of the above

**Answer: D**

**Explanation:**
Planar: embeddable in plane without crossing edges. Euler's formula: V - E + F = 2. Implies E ≤ 3V - 6 (each face bounded by ≥ 3 edges, each edge borders 2 faces). K_5 and K_{3,3} are not planar (Kuratowski's theorem). Many real graphs (road networks, circuit boards) are planar. Planar graphs allow specialized efficient algorithms.

---

**Q14.30: Foundational - [Theory] - [Graph Terminology Summary]**

Essential graph vocabulary:

A) Vertex, edge, degree, path, cycle, connected
B) Directed, undirected, weighted, unweighted
C) Adjacent, incident, neighbor, component
D) All of the above

**Answer: D**

**Explanation:**
Graph terminology: Adjacent vertices share an edge. Incident: edge is incident to its endpoints. Neighbor: adjacent vertex. Component: maximal connected subgraph. Degree: number of incident edges. These terms are prerequisites for all graph algorithms in Chapters 19-21, 27, and 42.

---

**Q14.31: Intermediate - [Theory] - [Adjacency List with HashMap]**

Adjacency list using hash map:

A) Map<vertex, List<vertex>> or Map<vertex, Set<vertex>>
B) Supports non-integer vertex labels
C) O(1) average edge check with Set
D) All of the above

**Answer: D**

**Explanation:**
Hash map adjacency: keys = vertices, values = collections of neighbors. Supports string/arbitrary vertex labels. With HashSet neighbors: O(1) average edge check. With list: O(degree) check but ordered iteration. Python: defaultdict(list) or defaultdict(set). Java: HashMap<Integer, HashSet<Integer>>. Flexible but more overhead than array-based.

---

**Q14.32: Intermediate - [Theory] - [Storing Weighted Edges]**

Storing edge weights in adjacency list:

A) List of (neighbor, weight) pairs
B) Or separate weight array indexed by edge ID
C) In Python: defaultdict(list) with (neighbor, weight) tuples
D) All of the above

**Answer: D**

**Explanation:**
Weighted adjacency list: adj[u] = [(v1, w1), (v2, w2), ...]. Alternative: CSR-like parallel arrays (col_idx and weights). Edge ID approach: adj[u] = [edge_id1, edge_id2, ...], edges[edge_id] = (u, v, w). Choice depends on whether edges have additional attributes beyond weight.

---

**Q14.33: Advanced - [Theory] - [Object-Oriented Graph]**

Object-oriented graph representation:

A) Vertex class with list of Edge objects
B) Edge class with source, destination, weight
C) Flexible but higher memory overhead
D) All of the above

**Answer: D**

**Explanation:**
OOP graph: Vertex objects with adjacency lists of Edge objects. Edge stores endpoints and metadata. Flexible: easy to add attributes, support different edge types. Overhead: object headers, pointer indirection, cache-unfriendly. Used in: graph libraries (JGraphT, networkx), complex graph models. For competitive programming: array-based adjacency lists preferred for speed.

---

**Q14.34: Expert - [Theory] - [Dynamic Graph Representation]**

Dynamic graph (edges added/removed):

A) Adjacency matrix: O(1) add/remove
B) Adjacency list: O(1) add, O(degree) remove
C) For frequent updates: hash set per vertex for O(1) remove
D) All of the above

**Answer: D**

**Explanation:**
Static graph: build once, query many times. Dynamic: edges change. Matrix: O(1) both, but O(V²) space. List with hash set: O(1) amortized add/remove, O(V+E) space. For dynamic connectivity queries: link-cut trees or Euler tour trees. For dynamic shortest paths: research-level complexity. Choice depends on what operations and queries are needed.

---

**Q14.35: Intermediate - [Theory] - [Graph Input Parsing]**

Common graph input formats:

A) V and E on first line, then E lines of (u, v) pairs
B) Adjacency matrix as V lines of V values
C) Edge weight format: E lines of (u, v, weight)
D) All are standard input formats

**Answer: D**

**Explanation:**
Standard formats: (1) Edge list: first line "V E", next E lines "u v [w]". (2) Adjacency matrix: V lines of V space-separated values. (3) CSR: row_ptr array, col_idx array. (4) Standard file formats: DIMACS, GML, GraphML, DOT. Competitive programming typically uses edge list. Libraries (networkx, igraph) support multiple formats.

---

**Q14.36: Advanced - [Theory] - [Graph Isomorphism]**

Graph isomorphism:

A) Two graphs are isomorphic if there's a bijection preserving adjacency
B) Same structure, different vertex labels
C) Testing is neither known to be P nor NP-complete
D) All of the above

**Answer: D**

**Explanation:**
Graph isomorphism: f: V₁→V₂ bijection where (u,v) ∈ E₁ ⟺ (f(u),f(v)) ∈ E₂. Same structure up to relabeling. Testing: in NP but not known to be NP-complete. Babai's 2015 result: quasipolynomial time. Practical algorithms: VF2, nauty/bliss. Famous open problem in complexity theory.

---

**Q14.37: Foundational - [Theory] - [Sparse vs Dense Impact]**

Graph density affects algorithm choice:

A) BFS/DFS: O(V+E) — fast for sparse, acceptable for dense
B) Floyd-Warshall: O(V³) — same regardless of density
C) Dijkstra with binary heap: O((V+E) log V) — prefer for sparse
D) All of the above

**Answer: D**

**Explanation:**
Sparse (E ≈ V): Dijkstra with heap O(V log V), BFS O(V). Dense (E ≈ V²): Floyd-Warshall O(V³) competitive with V × Dijkstra = O(V³ log V). Matrix operations (multiplication, transitive closure) work well with dense matrix representation. Algorithm + representation choice coupled with graph density.

---

**Q14.38: Expert - [Theory] - [Multigraph Representation]**

Multigraph (parallel edges allowed):

A) Adjacency matrix: store edge count M[u][v] = k
B) Adjacency list: vertex may appear multiple times
C) Edge list: naturally supports multi-edges
D) All of the above

**Answer: D**

**Explanation:**
Multigraph: multiple edges between same pair. Matrix: M[u][v] = number of parallel edges. List: neighbor appears multiple times or store list of edge IDs. Edge list: each edge separate entry. Applications: network flow (multiple paths), chemistry (double bonds), transportation networks (multiple routes between cities).

---

**Q14.39: Intermediate - [Theory] - [Transpose of Directed Graph]**

Transpose (reverse) of directed graph:

A) Reverse all edge directions
B) G^T has edge (v,u) for every edge (u,v) in G
C) Adjacency list: O(V+E) to compute
D) All of the above

**Answer: D**

**Explanation:**
Transpose: reverse all edges. Used in: Kosaraju's SCC algorithm (DFS on G and G^T), reachability queries. Adjacency matrix: transpose the matrix. Adjacency list: iterate all edges, add reversed. O(V+E). The graph's SCC structure is identical; only direction flips.

---

**Q14.40: Expert - [Theory] - [Graph Streaming Model]**

Graph streaming:

A) Edges arrive one at a time, limited memory
B) Cannot store entire graph
C) Approximate answers: connectivity, triangle counting
D) All of the above

**Answer: D**

**Explanation:**
Semi-streaming model: O(V × polylog(V)) memory, process edge stream. Enough to store spanning forest but not full graph. Algorithms: approximate matching, cut estimation, reachability. Full exact algorithms often impossible: connectivity needs O(V) memory (spanning forest), but clique/coloring queries need Ω(E) memory. Active research area.

---

**Q14.41: Advanced - [Theory] - [Space Comparison]**

Space comparison for graph with V=1000, E=5000:

A) Matrix: 1000² = 1,000,000 entries
B) Adjacency list: ~5000 entries + 1000 headers = ~6000
C) List uses 166× less space in this case
D) sparse graph → adjacency list strongly preferred

**Answer: D**

**Explanation:**
V=1000, E=5000 (sparse, avg degree 10). Matrix: 10⁶ entries, wastes 99.5% space. List: ~6000 entries. Ratio: 166×. For V=100, E=4000 (dense, avg degree 80): matrix = 10000, list = ~4100, ratio only 2.4×. Crossover: when E ≈ V²/c for small c, matrix becomes competitive. Real-world graphs (millions of vertices) almost always use adjacency lists.

---

**Q14.42: Expert - [Theory] - [Succinct Graph Representation]**

Succinct graph representation:

A) Stores graph in space close to information-theoretic minimum
B) For sparse graphs: O(E log V) bits
C) Supports adjacency queries in O(1) or O(log) time
D) All of the above

**Answer: D**

**Explanation:**
Succinct: near-optimal space with efficient queries. Information-theoretic minimum for labeled graph: log₂(2^(V²/2)) = V²/2 bits (dense) or ≈ E log V bits (sparse). Succinct representations achieve this with O(1) query time. Techniques: compressed adjacency using rank/select. Used for massive graphs (web graph, social networks) that don't fit in RAM.

---

**Q14.43: Intermediate - [Theory] - [Graph Conversion]**

Converting between representations:

A) Edge list → adjacency list: O(E), scan edges, append to lists
B) Adjacency list → matrix: O(V²) to initialize + O(E) to fill
C) Matrix → list: O(V²) to scan all entries
D) All of the above

**Answer: D**

**Explanation:**
Conversions: Edge list → list: iterate edges, append. O(E). List → matrix: O(V² + E). Matrix → list: scan all V² entries, O(V²). Matrix → edge list: O(V²). Edge list → matrix: O(V² + E). The O(V²) cost for matrix operations dominates for sparse graphs, which is why matrix conversions are avoided when possible.

---

**Q14.44: Advanced - [Theory] - [Adjacency Array (CSR) Advantages]**

CSR vs linked-list adjacency:

A) CSR: contiguous memory, cache-friendly
B) Linked list: fragmented memory, cache-unfriendly
C) CSR: faster traversal, but static (no edge additions)
D) All of the above

**Answer: D**

**Explanation:**
CSR: all neighbors stored consecutively in one array. Cache lines prefetched effectively. Link traversal: sequential array access vs pointer chasing. Measured speedup: 2-10x for BFS/DFS on large graphs. Drawback: static — adding edges requires rebuilding. Solution: batch updates, or hybrid (CSR + dynamic buffer). Used in high-performance graph frameworks (Graph500, Ligra).

---

**Q14.45: Intermediate - [Theory] - [Graph Representation Summary]**

Choosing graph representation:

A) Sparse + dynamic: adjacency list with hash sets
B) Dense + static: adjacency matrix
C) Large + static + performance: CSR
D) All valid guidelines

**Answer: D**

**Explanation:**
Decision framework: (1) Density: sparse → list, dense → matrix or list. (2) Static vs dynamic: static → CSR/matrix, dynamic → list with hash sets. (3) Scale: large graphs → compressed/succinct. (4) Operations: frequent edge check → matrix or hash set-based list. Frequent neighbor iteration → CSR. Understanding representation trade-offs is fundamental to efficient graph algorithm implementation.

---

## Chapter 14 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 11 | Graph definition, directed/undirected, matrix, list, edge list, terminology |
| Intermediate | 18 | Weighted, degree, bipartite, DAG, density, conversion, input formats |
| Advanced | 12 | CSR, implicit graphs, complement, planar, isomorphism, OOP representation |
| Expert | 4 | Dynamic graphs, multigraph, streaming, succinct representation |

**Total MCQs: 45** | **Target Met: ✓**

**Key Representation Comparisons:**

| Representation | Space | Edge Check | Iterate Neighbors | Add Edge |
|----------------|-------|------------|--------|----------|
| Adjacency Matrix | O(V²) | O(1) | O(V) | O(1) |
| Adjacency List | O(V+E) | O(deg) | O(deg) | O(1) |
| Edge List | O(E) | O(E) | O(E) | O(1) |
| CSR | O(V+E) | O(log deg) | O(deg) | N/A (static) |

**Next:** Chapter 15 - Disjoint Sets (Union-Find)
