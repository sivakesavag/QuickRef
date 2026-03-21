# Chapter 28: Computational Geometry

**Target:** 45 MCQs | **Distribution:** 11 Foundational, 18 Intermediate, 11 Advanced, 5 Expert

---

**Q28.1: Foundational - [Theory] - [Computational Geometry Overview]**

Computational geometry:

A) Algorithms for geometric problems (points, lines, polygons)
B) Applications: computer graphics, GIS, robotics, CAD
C) Key problems: convex hull, line intersection, nearest neighbor
D) All of the above

**Answer: D**

**Explanation:**
Computational geometry: study of algorithms for problems stated in geometric terms. Points, line segments, polygons, circles in 2D/3D. Applications everywhere: GPS routing, collision detection, 3D rendering, VLSI design. Core techniques: sweep line, divide and conquer, randomized incremental, duality.

---

**Q28.2: Foundational - [Theory] - [Convex Hull]**

Convex hull:

A) Smallest convex polygon containing all points
B) "Rubber band" around points
C) O(n log n) algorithms: Graham scan, Andrew's monotone chain
D) All of the above

**Answer: D**

**Explanation:**
Convex hull: boundary of smallest convex set containing all points. 2D: convex polygon. Algorithms: Graham scan (sort by polar angle, stack-based O(n log n)), Andrew's monotone chain (sort by x, build upper/lower hulls O(n log n)), Jarvis march (gift wrapping O(nh)). Lower bound: Ω(n log n) by reduction from sorting.

---

**Q28.3: Foundational - [Trace] - [Graham Scan]**

Graham scan for points (0,0), (1,0), (2,1), (1,3), (0,2), (0.5,0.5):

A) Find bottom-left: (0,0). Sort by polar angle from (0,0)
B) Sorted: (1,0), (2,1), (1,3), (0,2), (0.5,0.5) [approximate]
C) Push points, check cross product for left turn
D) Hull: (0,0), (1,0), (2,1), (1,3), (0,2). Point (0.5,0.5) is interior

**Answer: D**

**Explanation:**
Graham scan: sort by polar angle. Process in order. At each point: while top two stack points make right turn with new point → pop. Push new point. Cross product determines turn direction. (0.5,0.5) is inside the hull (detected and removed during scan). Final hull has 5 vertices.

---

**Q28.4: Intermediate - [Theory] - [Line Segment Intersection]**

Line segment intersection:

A) Shamos-Hoey: detect if any two segments intersect O(n log n)
B) Bentley-Ottmann: find all intersections O((n+k) log n), k = intersections
C) Sweep line algorithm: process events (endpoints) left to right
D) All of the above

**Answer: D**

**Explanation:**
Sweep line: vertical line sweeps left to right. Events: segment starts/ends, intersections. Active segments maintained in balanced BST (sorted by y at sweep line). Only adjacent pairs in sweep line structure can be new intersection candidates. Shamos-Hoey: detect any intersection. Bentley-Ottmann: report all k intersections. Without sweep line: O(n²) checking all pairs.

---

**Q28.5: Intermediate - [Theory] - [Point in Polygon]**

Point-in-polygon test:

A) Ray casting: count crossings of ray from point — odd = inside
B) Winding number: count winds around point — nonzero = inside
C) Both work for simple polygons; winding number also handles complex polygons
D) All of the above

**Answer: D**

**Explanation:**
Ray casting: cast horizontal ray from point, count edge crossings. Odd: inside. Even: outside. O(n) per query. Edge cases: ray through vertex or along edge. Winding number: sum signed angles — more robust for self-intersecting polygons. For convex polygon: O(log n) using binary search on edges.

---

**Q28.6: Foundational - [Theory] - [Cross Product]**

Cross product for orientation:

A) cross(P,Q,R) = (Q-P) × (R-P) = (Qx-Px)(Ry-Py) - (Qy-Py)(Rx-Px)
B) Positive: counterclockwise turn (left)
C) Negative: clockwise turn (right). Zero: collinear
D) All of the above — fundamental geometric primitive

**Answer: D**

**Explanation:**
Cross product: determines orientation of three points. Foundation of almost all computational geometry algorithms. Convex hull: detect turns. Segment intersection: opposite orientations means crossing. Area of triangle: |cross|/2. Polygon area: sum of cross products / 2. O(1) computation. Use integer arithmetic (long long) when possible to avoid floating-point issues.

---

**Q28.7: Intermediate - [Theory] - [Voronoi Diagram]**

Voronoi diagram:

A) Partition space into regions closest to each point (site)
B) Fortune's algorithm: O(n log n) sweep line construction
C) Dual of Delaunay triangulation
D) All of the above

**Answer: D**

**Explanation:**
Voronoi: for each site, region of points closer to it than any other site. Applications: nearest facility, rainfall estimation, cell tower coverage. Fortune's sweep line: O(n log n). Properties: each Voronoi vertex is equidistant to 3 sites. Delaunay triangulation = dual graph. Contains nearest neighbor information.

---

**Q28.8: Advanced - [Theory] - [Delaunay Triangulation]**

Delaunay triangulation:

A) Triangulation maximizing minimum angle (avoids thin triangles)
B) No point inside circumcircle of any triangle
C) Dual of Voronoi diagram
D) All of the above — O(n log n) construction

**Answer: D**

**Explanation:**
Delaunay: "the nicest" triangulation. Empty circumcircle property: no other point lies inside circumcircle of any Delaunay triangle. Maximizes minimum angle → avoids slivers. Contains MST edges (Euclidean MST ⊂ Delaunay). Construction: incremental insertion O(n log n), divide and conquer O(n log n). Applications: terrain modeling, mesh generation, FEM.

---

**Q28.9: Intermediate - [Theory] - [Closest Pair Review]**

Closest pair of points:

A) Divide and conquer: O(n log n) — split, solve halves, check strip
B) Randomized: O(n) expected using grid hashing
C) Strip check: only O(1) points per δ×2δ box
D) All of the above

**Answer: D**

**Explanation:**
Closest pair: covered in Chapter 24 (D&C). Strip property: after solving halves (minimum δ), strip of width 2δ around dividing line. Each δ×2δ box has ≤ constant points (packing argument). O(n log n) deterministic. Randomized: insert points randomly, maintain grid with cell size δ. Expected O(n). In practice: both very fast.

---

**Q28.10: Advanced - [Theory] - [Convex Hull Trick (Geometric)]**

Convex hull for optimization:

A) Half-plane intersection: convex polygon in O(n log n)
B) Point-line duality: many problems transform
C) Applications: linear programming in 2D, smallest enclosing circle
D) Geometric optimization via convex hull

**Answer: D**

**Explanation:**
Convex hull has optimization applications beyond DP (Chapter 22). Half-plane intersection: intersect n half-planes in O(n log n) → convex polygon or empty. Point-line duality: point (a,b) ↔ line y=ax-b. Transforms upper envelope of lines to convex hull of points. Smallest enclosing circle: Welzl's randomized O(n). LP in 2D: O(n) randomized.

---

**Q28.11: Foundational - [Theory] - [Polygon Area]**

Area of simple polygon:

A) Shoelace formula: A = ½|Σ(x_i × y_{i+1} - x_{i+1} × y_i)|
B) Sum of signed areas of triangles from origin
C) O(n) computation
D) All of the above

**Answer: D**

**Explanation:**
Shoelace formula: sum cross products of consecutive vertices. Signed area: positive for counterclockwise, negative for clockwise. Works for any simple polygon (convex or concave). O(n). Extension: polygon centroid, moment of inertia. Related: Pick's theorem for integer coordinates: A = I + B/2 - 1 (I=interior, B=boundary lattice points).

---

**Q28.12: Expert - [Theory] - [Sweep Line Paradigm]**

Sweep line technique:

A) Scan geometric space with a line (usually vertical, moving left→right)
B) Maintain active structure (BST, priority queue) of relevant objects
C) Process events (insertions, deletions, intersections)
D) Reduces 2D to 1D + event processing

**Answer: D**

**Explanation:**
Sweep line: fundamental CG paradigm. Active structure: objects crossed by sweep line, ordered by y. Events: object starts/ends, intersections. Examples: segment intersection, Voronoi diagram, rectangle union area. Reduces 2D problem to 1D structure maintenance. O(n log n) for many problems (log n per event × n events).

---

**Q28.13: Intermediate - [Theory] - [Convex Hull Algorithms Comparison]**

Convex hull algorithms:

A) Graham scan: O(n log n), sort by polar angle
B) Andrew's monotone chain: O(n log n), sort by x, simpler
C) Jarvis march: O(nh), h=hull vertices — output-sensitive
D) All correct with different trade-offs

**Answer: D**

**Explanation:**
Graham: sort + stack. Simple but polar angle sort has edge cases. Andrew: sort by x, build upper+lower hulls separately. Cleaner implementation. Jarvis (gift wrapping): O(nh) where h=hull size. Better when h small (h << n). Chan's algorithm: O(n log h) — optimal output-sensitive. Divide and conquer: O(n log n). Quickhull: O(n log n) expected, O(n²) worst.

---

**Q28.14: Expert - [Theory] - [Range Trees]**

Multi-level range trees:

A) Answer orthogonal range queries in O(log^d n + k)
B) d=2: 2-level range tree with fractional cascading: O(log n + k)
C) O(n log^(d-1) n) space
D) All of the above

**Answer: D**

**Explanation:**
Range tree: multi-level tree for d-dimensional range queries. Level 1: BST on first coordinate. Each node: secondary tree on second coordinate for its subtree. Query: search primary tree O(log n), query secondary trees O(log n) each → O(log² n + k). With fractional cascading: O(log n + k). 3D: O(log² n + k). General: O(log^(d-1) n + k). Space: O(n log^(d-1) n).

---

**Q28.15: Advanced - [Theory] - [KD-Tree]**

KD-tree:

A) Binary tree for k-dimensional points
B) Alternating split dimensions at each level
C) Nearest neighbor: O(log n) expected, O(n^(1-1/k)) worst
D) All of the above

**Answer: D**

**Explanation:**
KD-tree: partition space by alternating dimensions. Level 0: split on x. Level 1: split on y. Level 2: split on z. Repeat. Construction: O(n log n). Nearest neighbor: prune branches where closest possible point in region is farther than current best. O(log n) expected for low dimensions. Degrades for high dimensions (curse of dimensionality). Good for k ≤ 20.

---

**Q28.16: Expert - [Theory] - [Minkowski Sum]**

Minkowski sum:

A) A ⊕ B = {a + b : a ∈ A, b ∈ B}
B) Convex A and convex B: result is convex, O(n + m) to compute
C) Non-convex: O(n²m²) worst case
D) Applications: collision detection, path planning

**Answer: D**

**Explanation:**
Minkowski sum: geometric addition of shapes. Convex polygons: merge sorted edge sequences, O(n+m). Non-convex: decompose into convex parts, compute pairwise, take union. Robot motion planning: robot can reach point p iff p is outside Minkowski sum of obstacle and reflected robot. Collision detection: A and B collide iff origin ∈ A ⊕ (-B).

---

**Q28.17: Intermediate - [Theory] - [Line Sweep for Rectangle Union]**

Area of union of rectangles:

A) Sweep line left to right at x-events
B) At each event: update active y-intervals (segment tree)
C) Area contribution = (x_next - x_curr) × total active y-length
D) O(n log n)

**Answer: D**

**Explanation:**
Rectangle union area: sweep line at x-boundaries. At each x-event: add/remove rectangles' y-intervals. Segment tree tracks total covered length on y-axis. Area between consecutive x-events: width × covered_y_length. O(n log n). Extension: perimeter of rectangle union, count of distinct covered regions. Elegant sweep line + segment tree combination.

---

**Q28.18: Advanced - [Theory] - [Rotating Calipers]**

Rotating calipers:

A) Technique for antipodal pairs on convex polygon
B) Diameter: maximum distance between any two points = antipodal pair
C) O(n) after convex hull computed
D) All of the above

**Answer: D**

**Explanation:**
Rotating calipers: two parallel support lines rotating around convex hull. At each step: one edge aligns with a caliper. Track antipodal pair (one point on each line). Diameter = max distance among O(n) antipodal pairs. Also: width (min distance between parallel support lines), minimum area enclosing rectangle. All O(n) post-hull.

---

**Q28.19: Foundational - [Theory] - [Geometric Primitives]**

Essential geometric primitives:

A) Point, line, segment, ray, polygon
B) Distance: Euclidean √((x₂-x₁)²+(y₂-y₁)²), Manhattan |x₁-x₂|+|y₁-y₂|
C) Orientation test (cross product), intersection test
D) All building blocks for complex algorithms

**Answer: D**

**Explanation:**
Primitives: foundation. Point (x,y). Line: ax+by+c=0 or parametric. Segment: bounded line portion. Ray: half-line. Polygon: ordered vertices. Distance: Euclidean (L2), Manhattan (L1), Chebyshev (L∞). Orientation: cross product sign. Intersection: solve linear systems. All geometric algorithms built from these primitives. Use exact arithmetic when possible.

---

**Q28.20: Expert - [Theory] - [Art Gallery Problem]**

Art gallery problem:

A) Minimum guards to see all of a simple polygon
B) Upper bound: ⌊n/3⌋ guards suffice (Chvátal's theorem)
C) Finding minimum: NP-hard
D) All of the above

**Answer: D**

**Explanation:**
Art gallery: every point of simple n-gon polygon must be visible from some guard. Chvátal (1975): ⌊n/3⌋ guards always suffice. Fisk's proof: 3-color triangulation, take smallest color class. This is tight (comb polygon needs ⌊n/3⌋). Finding minimum: NP-hard. Variants: edge guards, vertex guards, moving guards. Beautiful connection between combinatorics and geometry.

---

## Chapter 28 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | Convex hull, cross product, polygon area, geometric primitives |
| Intermediate | 7 | Line intersection, point-in-polygon, Voronoi, sweep line, convex hull variants |
| Advanced | 5 | Delaunay, KD-tree, Minkowski sum, rotating calipers |
| Expert | 3 | Range trees, sweep paradigm, art gallery problem |

**Total MCQs: 20**

**Next:** Chapter 29 - Randomized Algorithms
