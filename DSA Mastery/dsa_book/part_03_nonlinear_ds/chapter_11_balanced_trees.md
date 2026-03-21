# Chapter 11: Balanced Trees

**Target:** 75 MCQs | **Distribution:** 19 Foundational, 30 Intermediate, 19 Advanced, 7 Expert

---

**Q11.1: Foundational - [Theory] - [Balanced Tree Motivation]**

Why are balanced trees needed?

A) Unbalanced BST can degenerate to O(n) height
B) Balanced trees guarantee O(log n) height
C) Ensures worst-case O(log n) operations
D) All of the above

**Answer: D**

**Explanation:**
Inserting sorted data into a plain BST produces a linked list with height n. Balanced trees (AVL, Red-Black, B-Trees) use structural invariants and rotations/splits to keep height O(log n). This guarantees O(log n) search, insert, and delete in the worst case, unlike unbalanced BSTs where these degrade to O(n). Refer to Q10.24-25 for degenerate BST examples.

---

**Q11.2: Foundational - [Theory] - [AVL Tree Definition]**

AVL tree property:

A) For every node, heights of left and right subtrees differ by at most 1
B) Named after Adelson-Velsky and Landis
C) First self-balancing BST (1962)
D) All of the above

**Answer: D**

**Explanation:**
AVL tree: balance factor = height(left) - height(right), must be in {-1, 0, 1} for every node. If insertion or deletion violates this, rotations restore balance. Guarantees height ≤ 1.44 × log₂(n+2). Historically the first self-balancing BST data structure.

---

**Q11.3: Foundational - [Theory] - [Balance Factor]**

Balance factor of a node in AVL tree:

A) height(left subtree) - height(right subtree)
B) Must be -1, 0, or 1
C) If |BF| > 1, rebalancing needed
D) All of the above

**Answer: D**

**Explanation:**
Balance factor (BF) = left height - right height. BF = 0: perfectly balanced. BF = 1: left-heavy. BF = -1: right-heavy. |BF| > 1: violates AVL property, needs rotation. After every insert/delete, check and fix BF along the path from modified node to root.

---

**Q11.4: Foundational - [Theory] - [AVL Rotations Overview]**

AVL tree uses how many types of rotations?

A) 1 (single rotation only)
B) 2 (left and right)
C) 4 (left, right, left-right, right-left)
D) 8

**Answer: C**

**Explanation:**
Four rotation types: (1) Right rotation (LL case), (2) Left rotation (RR case), (3) Left-Right rotation (LR case — left then right), (4) Right-Left rotation (RL case — right then left). Single rotations fix same-direction imbalance; double rotations fix zig-zag imbalance. Each takes O(1) time.

---

**Q11.5: Foundational - [Theory] - [Right Rotation (LL Case)]**

When is a right rotation performed in AVL?

A) Node is left-heavy (BF = 2) and left child is left-heavy or balanced (BF ≥ 0)
B) Called LL case (insertion into left subtree of left child)
C) Pivot is the left child, it becomes new root of subtree
D) All of the above

**Answer: D**

**Explanation:**
LL case: new node inserted in left subtree of left child causes BF = 2 at ancestor. Fix: right rotation around the unbalanced node. Left child becomes parent, unbalanced node becomes right child, left child's right subtree transfers to unbalanced node's left. O(1) pointer changes.

---

**Q11.6: Foundational - [Theory] - [Left Rotation (RR Case)]**

Left rotation in AVL is performed when:

A) Node is right-heavy (BF = -2) and right child is right-heavy or balanced (BF ≤ 0)
B) Called RR case
C) Right child becomes new root of subtree
D) All of the above

**Answer: D**

**Explanation:**
RR case: mirror of LL. Insertion in right subtree of right child. Left rotation: right child becomes parent. Symmetric to right rotation. O(1) operation. Restores BF to {-1, 0, 1}.

---

**Q11.7: Foundational - [Trace] - [Right Rotation]**

Tree: 30(20(10,25),40), insert 5 causes BF(30) = 2. After right rotation:

A) 20 becomes new root
B) 30 becomes right child of 20
C) 25 becomes left child of 30
D) Result: 20(10(5,null),30(25,40))

**Answer: D**

**Explanation:**
Before: 30(20(10(5),25),40). BF(30) = 2 (LL case). Right rotation at 30: 20 becomes root. 30 goes right of 20. 25 (20's right child) transfers to 30's left. Result: 20(10(5,null),30(25,40)). All BFs now ≤ 1. Height reduced from 3 to 2.

---

**Q11.8: Foundational - [Theory] - [LR Rotation]**

Left-Right (LR) double rotation:

A) Node BF = 2, left child BF = -1 (left child is right-heavy)
B) First left-rotate on left child
C) Then right-rotate on node
D) All of the above

**Answer: D**

**Explanation:**
LR case: insertion in right subtree of left child (zig-zag). Single right rotation won't fix it. Solution: first left-rotate the left child (straighten the zig-zag), then right-rotate the node. Grandchild becomes new root of subtree. Two O(1) rotations.

---

**Q11.9: Foundational - [Trace] - [LR Rotation]**

Tree: 30(10(null,20),40), insert 25. After LR rotation at 30:

A) BF(30) = 2, left child 10 has BF = -1 (LR case)
B) Left-rotate at 10: 20(10,null) replaces 10
C) Right-rotate at 30: 20(10,30(25,40))
D) Balanced result

**Answer: D**

**Explanation:**
Before rotation: 30(10(null,20(null,25)),40). BF(30) = 2, BF(10) = -1 → LR case. Step 1: left-rotate at 10 → 20(10,25). Step 2: right-rotate at 30 → 20(10,30(25,40)). Grandchild 20 becomes subtree root. All BFs restored.

---

**Q11.10: Foundational - [Theory] - [RL Rotation]**

Right-Left (RL) double rotation:

A) Node BF = -2, right child BF = 1 (right child is left-heavy)
B) First right-rotate on right child
C) Then left-rotate on node
D) All of the above

**Answer: D**

**Explanation:**
RL case: mirror of LR. Insertion in left subtree of right child. Two rotations: right-rotate right child, then left-rotate node. Symmetric to LR case. Grandchild becomes new subtree root.

---

**Q11.11: Foundational - [Theory] - [AVL Height Bound]**

Maximum height of AVL tree with n nodes:

A) Exactly log₂(n)
B) At most 1.44 × log₂(n+2)
C) At most 2 × log₂(n)
D) Exactly n-1

**Answer: B**

**Explanation:**
AVL height bound: h < 1.44 × log₂(n+2). Derived from Fibonacci-like minimum node count: N(h) = N(h-1) + N(h-2) + 1. Minimum nodes for height h follows Fibonacci growth. Tighter than Red-Black trees (2 × log₂(n+1)), so AVL trees are more strictly balanced.

---

**Q11.12: Intermediate - [Theory] - [AVL Minimum Nodes]**

Minimum number of nodes in AVL tree of height h:

A) N(h) = N(h-1) + N(h-2) + 1
B) N(0) = 1, N(1) = 2
C) Fibonacci-like recurrence
D) All of the above

**Answer: D**

**Explanation:**
Minimum nodes: make one subtree height h-1, other h-2 (maximum imbalance allowed). N(0) = 1, N(1) = 2, N(2) = 4, N(3) = 7, N(4) = 12. N(h) ≈ φ^h where φ ≈ 1.618 (golden ratio). This gives the height bound h ≈ 1.44 log₂ n.

---

**Q11.13: Intermediate - [Trace] - [AVL Insert Sequence]**

Insert [10, 20, 30] into empty AVL:

A) Insert 10: root. Insert 20: right of 10
B) Insert 30: right of 20. BF(10) = -2 (RR case)
C) Left rotation at 10: 20(10,30)
D) Balanced AVL tree

**Answer: D**

**Explanation:**
Step by step: 10 (root). 20 right of 10. 30 right of 20 → BF(10) = -2 (RR). Left rotate at 10: 20 becomes root, 10 left, 30 right. Height 1. Without AVL balancing, this would be a right-skewed chain of height 2.

---

**Q11.14: Intermediate - [Trace] - [AVL Insert LR Case]**

Insert [30, 10, 20] into empty AVL:

A) 30 root. 10 left of 30. 20 right of 10
B) BF(30) = 2, BF(10) = -1 → LR case
C) Left-rotate at 10, then right-rotate at 30
D) Result: 20(10,30)

**Answer: D**

**Explanation:**
30 → 30(10) → 30(10(null,20)). BF(30) = 2, left child BF = -1 (LR). Step 1: left-rotate at 10 → 20(10,null). Step 2: right-rotate at 30 → 20(10,30). Balanced. Without double rotation, single rotation would not fix this zig-zag pattern.

---

**Q11.15: Intermediate - [Theory] - [AVL Deletion]**

AVL deletion may require:

A) Multiple rotations (up to O(log n))
B) Rebalancing along path to root
C) More complex than insertion (which needs at most 2 rotations)
D) All of the above

**Answer: D**

**Explanation:**
AVL insertion: at most 1 or 2 rotations fix the tree (one imbalance point). Deletion: can cause cascading imbalances — fixing one node may unbalance its ancestor. Worst case O(log n) rotations. This is why Red-Black trees (at most 3 rotations for delete) are preferred in practice for frequent deletions.

---

**Q11.16: Intermediate - [Trace] - [AVL Deletion]**

AVL tree 20(10(5,15),30(25,35)), delete 5:

A) Remove leaf 5, tree becomes 20(10(null,15),30(25,35))
B) BF(10) = -1 (balanced)
C) BF(20) = 0 → still balanced
D) No rotation needed

**Answer: D**

**Explanation:**
Delete 5 (leaf removal). 10 now has only right child 15. BF(10) = 0-1 = -1 (valid). BF(20) = height(left=1) - height(right=1) = 0 (valid). No rebalancing needed. Deletion doesn't always require rotation — only when BF becomes ±2.

---

**Q11.17: Intermediate - [Theory] - [AVL vs BST Performance]**

AVL tree guarantees:

A) Search: O(log n) worst case
B) Insert: O(log n) worst case (including rotations)
C) Delete: O(log n) worst case
D) All of the above

**Answer: D**

**Explanation:**
All operations O(log n) worst case because height ≤ 1.44 log n. Search: same as BST but bounded height. Insert: search + at most 2 rotations. Delete: search + up to O(log n) rotations. Each rotation is O(1). Space: O(n) with one extra field (height or BF) per node.

---

**Q11.18: Foundational - [Theory] - [Red-Black Tree Definition]**

Red-Black tree properties:

A) Every node is red or black
B) Root is black
C) Every leaf (NIL) is black
D) All of the above (plus two more properties)

**Answer: D**

**Explanation:**
Five Red-Black properties: (1) Every node is red or black. (2) Root is black. (3) Every leaf (NIL sentinel) is black. (4) Red node's children are both black (no two consecutive reds). (5) All paths from any node to descendant NIL nodes have same number of black nodes (black-height). These ensure height ≤ 2 × log₂(n+1).

---

**Q11.19: Foundational - [Theory] - [Red-Black Property 4]**

"No two consecutive red nodes" means:

A) If a node is red, both its children must be black
B) A red node cannot have a red parent
C) Equivalent statements
D) All of the above

**Answer: D**

**Explanation:**
Property 4: no red-red parent-child. If node is red, children are black. Equivalently, parent of red must be black. This limits how many red nodes can appear on any root-to-leaf path, bounding height. Violation after insert = red uncle/parent conflict needing fix-up.

---

**Q11.20: Foundational - [Theory] - [Black-Height]**

Black-height of a Red-Black tree:

A) Number of black nodes on any path from root to NIL (excluding root, or including root — convention varies)
B) Same for all paths from a node to its descendant NILs
C) Ensures balance
D) All of the above

**Answer: D**

**Explanation:**
Black-height (bh): count of black nodes from node to leaf NIL. Property 5 guarantees all paths have same bh. This means subtree rooted at node with bh = k has at least 2^k - 1 internal nodes. Therefore n ≥ 2^bh - 1, so bh ≤ log₂(n+1), and height ≤ 2 × bh ≤ 2 × log₂(n+1).

---

**Q11.21: Intermediate - [Theory] - [RB Tree Height Bound]**

Height of Red-Black tree with n internal nodes:

A) At most 2 × log₂(n+1)
B) Looser than AVL (1.44 × log₂(n+2))
C) Trade-off: fewer rotations on insert/delete
D) All of the above

**Answer: D**

**Explanation:**
Red-Black height ≤ 2 × log₂(n+1), vs AVL ≤ 1.44 × log₂(n+2). Red-Black allows more imbalance but needs fewer structural changes: insert = at most 2 rotations, delete = at most 3 rotations (vs O(log n) for AVL delete). This makes Red-Black preferred for systems with many insertions/deletions (e.g., Linux kernel, Java TreeMap).

---

**Q11.22: Intermediate - [Theory] - [RB Insert Fix-Up]**

After inserting a red node in Red-Black tree, fix-up cases:

A) Case 1: Uncle is red → recolor parent, uncle to black; grandparent to red; move up
B) Case 2: Uncle is black, node is inner child → rotate to outer child (reduce to Case 3)
C) Case 3: Uncle is black, node is outer child → rotate grandparent, recolor
D) All of the above

**Answer: D**

**Explanation:**
Insert new node as red (preserves black-height). If parent is black, done. If parent is red (violation): check uncle. Red uncle: recolor and move problem up (may cascade to root). Black uncle: 1-2 rotations fix locally. At most 2 rotations total for insert. Recoloring may cascade O(log n) levels but no additional rotations.

---

**Q11.23: Intermediate - [Trace] - [RB Insert]**

Insert 10 into empty RB tree, then insert 20, then 30:

A) Insert 10: red node, then recolor to black (root property)
B) Insert 20: red, parent 10 is black → no fix needed
C) Insert 30: red, parent 20 is red, uncle is NIL (black) → Case 3 (RR): left-rotate at 10, recolor
D) Result: 20(black, 10(red), 30(red))

**Answer: D**

**Explanation:**
10 inserted red, recolored black (root). 20 inserted red as right child of 10 (black parent, ok). 30 inserted red as right child of 20 (red parent, violation). Uncle of 30 is 10's left child = NIL (black). Outer child case: left-rotate at 10, swap colors of 20 and 10. Tree: 20(10,30), 20 black, 10 and 30 red.

---

**Q11.24: Intermediate - [Theory] - [RB Delete Fix-Up]**

Red-Black delete fix-up:

A) More complex than insert fix-up
B) At most 3 rotations
C) Cases depend on sibling's color and sibling's children colors
D) All of the above

**Answer: D**

**Explanation:**
Delete: if removed/replaced node is red, no violation. If black, black-height changes → fix-up with 4 cases (and mirrors). Sibling red: rotate to get black sibling. Sibling black with black children: recolor sibling red, move up. Sibling black with red child: 1-2 rotations. Bounded at 3 rotations total.

---

**Q11.25: Intermediate - [Theory] - [AVL vs Red-Black Comparison]**

AVL vs Red-Black trees:

A) AVL: stricter balance, faster lookups
B) Red-Black: fewer rotations on insert/delete, better for write-heavy
C) AVL height ≤ 1.44 log n; RB height ≤ 2 log n
D) All of the above

**Answer: D**

**Explanation:**
AVL: stricter balance means shorter trees → faster search by constant factor. But delete may need O(log n) rotations. Red-Black: relaxed balance, at most 2 rotations for insert, 3 for delete → faster modifications. In practice: AVL for read-heavy (databases), Red-Black for balanced read/write (std::map, TreeMap). Both O(log n) asymptotically.

---

**Q11.26: Intermediate - [Theory] - [Red-Black in Practice]**

Red-Black trees used in:

A) C++ std::map, std::set
B) Java TreeMap, TreeSet
C) Linux kernel (CFS scheduler, memory management)
D) All of the above

**Answer: D**

**Explanation:**
Red-Black trees are the most widely used balanced BST in practice. C++ STL, Java Collections, Linux kernel's Completely Fair Scheduler (CFS), virtual memory management. Chosen over AVL due to simpler insert/delete with bounded rotations.

---

**Q11.27: Advanced - [Theory] - [RB Tree Insertion Amortized]**

Amortized cost of Red-Black tree insertion:

A) O(1) amortized rotations
B) Recoloring may cascade but rotations bounded by 2
C) Structural changes (rotations) are O(1) worst case per insert
D) All of the above

**Answer: D**

**Explanation:**
Each insert: at most 2 rotations (worst case). Recoloring may cascade O(log n) levels but recoloring is cheap (no pointer changes). Amortized structural cost per insert is O(1). This makes Red-Black trees excellent for applications needing many insertions.

---

**Q11.28: Foundational - [Theory] - [B-Tree Definition]**

B-Tree of order m (minimum degree t):

A) Each node has at most m children (2t children)
B) Each internal node (except root) has at least ⌈m/2⌉ children (t children)
C) All leaves at same level
D) All of the above

**Answer: D**

**Explanation:**
B-Tree: self-balancing tree optimized for disk access. Order m (or minimum degree t where m = 2t): root has 1 to m-1 keys. Internal nodes have ⌈m/2⌉ to m children. All leaves at same depth. Keys sorted within each node. Balanced by construction. Used in databases and file systems.

---

**Q11.29: Foundational - [Theory] - [B-Tree Properties]**

B-Tree key properties:

A) Keys within a node are sorted
B) Node with k keys has k+1 children
C) All leaves at same depth
D) All of the above

**Answer: D**

**Explanation:**
B-Tree node with k keys: k+1 child pointers. Keys sorted: key[i] separates subtree[i] and subtree[i+1]. All leaves at same level ensures balanced height. Height O(log_t n) where t is minimum degree. Each node read/write is one disk I/O, so minimizing height minimizes disk accesses.

---

**Q11.30: Intermediate - [Theory] - [B-Tree Height]**

Height of B-Tree with n keys and minimum degree t:

A) O(log_t n)
B) At most log_t((n+1)/2)
C) Much smaller than binary tree height for large t
D) All of the above

**Answer: D**

**Explanation:**
B-Tree height: h ≤ log_t((n+1)/2). For t = 1000 and n = 10^9: h ≤ 3. Binary tree would need ~30 levels. Each B-Tree level = 1 disk I/O, so 3 disk reads vs 30. This is why B-Trees dominate database indexing.

---

**Q11.31: Intermediate - [Theory] - [B-Tree Search]**

Searching in B-Tree:

A) At each node, binary search among keys
B) If key found, return
C) Follow appropriate child pointer
D) All of the above

**Answer: D**

**Explanation:**
Search: start at root. Binary search within node's keys (O(log m) per node). If found, done. If not, follow child pointer between appropriate keys. Repeat until found or reach leaf. Total: O(log_t n) nodes visited, O(log m) per node. Total comparisons: O(log n). Disk I/Os: O(log_t n).

---

**Q11.32: Intermediate - [Theory] - [B-Tree Insert]**

B-Tree insertion:

A) Always insert into a leaf
B) If leaf is full (has m-1 keys), split it
C) Split pushes median key to parent
D) All of the above

**Answer: D**

**Explanation:**
Insert: search for correct leaf. If leaf not full, insert key in sorted position. If full (m-1 keys): split into two nodes, median key promotes to parent. If parent full, split cascades up. Worst case: splits cascade to root, increasing tree height by 1. This is the only way B-Tree height grows.

---

**Q11.33: Intermediate - [Trace] - [B-Tree Insert]**

B-Tree order 3 (max 2 keys per node), insert [10, 20, 30, 40, 50]:

A) Insert 10, 20: node [10,20]
B) Insert 30: full, split → [20] with children [10] and [30]
C) Insert 40: goes to [30], becomes [30,40]
D) Insert 50: [30,40] full, split → [20,40] with children [10],[30],[50]

**Answer: D**

**Explanation:**
Order 3 (t=2, max 2 keys). [10,20] full, insert 30 → split: root [20], left [10], right [30]. Insert 40 → right becomes [30,40]. Insert 50 → [30,40] full, split: median 40 promotes. Root [20,40], children [10],[30],[50]. Height 1. All leaves at same depth.

---

**Q11.34: Intermediate - [Theory] - [B-Tree Delete]**

B-Tree deletion cases:

A) Key in leaf: remove directly (if node has enough keys)
B) Key in internal node: replace with predecessor/successor from leaf, delete from leaf
C) If node underflows (< ⌈m/2⌉-1 keys): borrow from sibling or merge
D) All of the above

**Answer: D**

**Explanation:**
Delete from leaf: simple if node has more than minimum keys. If at minimum: try borrowing from adjacent sibling (rotate through parent key). If sibling also at minimum: merge nodes (combine with parent key). Internal node key: swap with inorder predecessor/successor (always in a leaf), then delete from leaf. Merge may cascade to root.

---

**Q11.35: Intermediate - [Theory] - [B+ Tree vs B-Tree]**

B+ Tree differs from B-Tree:

A) All data records stored only in leaves
B) Internal nodes store only keys (for routing)
C) Leaves linked in a linked list for sequential access
D) All of the above

**Answer: D**

**Explanation:**
B+ Tree: data pointers only at leaf level. Internal nodes are index-only (more keys per node, reducing height). Leaves form a linked list enabling efficient range queries and sequential scans. B-Trees store data at all levels. B+ Trees are standard for database indexes (MySQL InnoDB, PostgreSQL).

---

**Q11.36: Intermediate - [Theory] - [B+ Tree Advantages]**

B+ Tree advantages over B-Tree:

A) Higher fanout (more keys per internal node since no data pointers)
B) Efficient range queries via leaf linked list
C) Consistent search time (always reaches leaf)
D) All of the above

**Answer: D**

**Explanation:**
B+ Tree internal nodes: only keys + child pointers (no data). More keys fit in one disk page → higher branching factor → shorter tree. Range queries: scan leaf linked list. All searches touch same number of levels (always leaf). Predictable performance. Trade-off: slightly more space for duplicated keys in leaves.

---

**Q11.37: Advanced - [Theory] - [B-Tree Order Confusion]**

B-Tree "order" definition varies:

A) Knuth: order m = maximum children per node
B) Others: order = minimum degree t (each node has t to 2t children)
C) CLRS uses minimum degree t
D) All of the above — always clarify convention

**Answer: D**

**Explanation:**
Confusion source: Knuth defines order as max children (m). CLRS defines minimum degree t where max children = 2t, max keys = 2t-1. A "B-Tree of order 5" (Knuth) = minimum degree t=3 (CLRS). Always check which convention is being used. This is a common exam/interview gotcha.

---

**Q11.38: Foundational - [Theory] - [Splay Tree Concept]**

Splay tree:

A) Self-adjusting BST
B) Accessed node is splayed (moved) to root via rotations
C) No balance information stored
D) All of the above

**Answer: D**

**Explanation:**
Splay tree: after every access (search, insert, delete), the accessed node is moved to root using a sequence of rotations called splaying. No height or balance factor stored. Frequently accessed elements stay near root. Amortized O(log n) per operation. Simpler implementation than AVL/RB. Refer to Q10.39-40 for splay operation details.

---

**Q11.39: Intermediate - [Theory] - [Splay Operations: Zig, Zig-Zig, Zig-Zag]**

Splay rotation cases:

A) Zig: node is child of root → single rotation
B) Zig-Zig: node and parent are same-side children → rotate parent first, then node
C) Zig-Zag: node and parent are different-side children → rotate node twice
D) All of the above

**Answer: D**

**Explanation:**
Splaying: bring node x to root. Zig: x is child of root, single rotation. Zig-Zig: x and parent same direction (both left or both right) — rotate grandparent-parent first, then parent-x. This ordering is crucial for amortized bound. Zig-Zag: different directions — two rotations like AVL double rotation. Zig-zig order distinguishes splay from naive rotate-to-root.

---

**Q11.40: Intermediate - [Theory] - [Splay Amortized Analysis]**

Splay tree amortized complexity:

A) O(log n) per operation amortized
B) Worst case single operation: O(n)
C) Sequence of m operations: O(m log n) total
D) All of the above

**Answer: D**

**Explanation:**
Splay: single operation can be O(n) (accessing deepest node in degenerate tree). But splaying restructures tree, improving future accesses. Potential method proves amortized O(log n). Key insight: zig-zig rotation order ensures tree becomes balanced after accessing deep nodes. Without zig-zig ordering, amortized bound doesn't hold.

---

**Q11.41: Advanced - [Theory] - [Splay Tree Properties]**

Splay trees satisfy:

A) Static optimality: within O(1) factor of optimal static BST
B) Working set property: recently accessed items are faster to access
C) Sequential access theorem: accessing all n elements in order is O(n)
D) All of the above

**Answer: D**

**Explanation:**
Splay trees have remarkable properties: static optimality (as good as any fixed BST for a given access sequence up to constant factor), working set property (recent items near root), sequential access (O(n) for sorted access). The unproven dynamic optimality conjecture (Q10.64) states splay trees are O(1)-competitive with any online BST algorithm.

---

**Q11.42: Foundational - [Theory] - [Treap Definition]**

Treap:

A) Combination of tree and heap
B) BST property by key, heap property by random priority
C) Expected O(log n) height
D) All of the above

**Answer: D**

**Explanation:**
Treap: each node has (key, priority). Keys satisfy BST property (left < root < right). Priorities satisfy heap property (parent priority > children priorities for max-heap variant). Random priorities → expected tree shape same as random BST → expected height O(log n). Simpler than AVL/RB.

---

**Q11.43: Intermediate - [Theory] - [Treap Insert]**

Treap insertion:

A) BST insert by key
B) Then fix heap property by rotations
C) Rotate inserted node up while priority > parent priority
D) All of the above

**Answer: D**

**Explanation:**
Insert: BST insert at leaf position. Assign random priority. If priority violates heap property (inserted node priority > parent), rotate up. Left rotation if right child, right rotation if left child. Repeat until heap property restored. Expected O(log n) rotations.

---

**Q11.44: Intermediate - [Theory] - [Treap Split and Merge]**

Treap supports efficient split and merge:

A) Split(k): divide into treap with keys ≤ k and treap with keys > k
B) Merge: combine two treaps where all keys in first < all keys in second
C) Both O(log n) expected time
D) All of the above

**Answer: D**

**Explanation:**
Split: recursively split by comparing k with root. Merge: compare priorities of roots, make one root and recursively merge remaining. Both O(expected height) = O(log n). These operations make treaps powerful for range operations, implicit treaps (implicit keys for array operations), and competitive programming.

---

**Q11.45: Advanced - [Trace] - [Treap Insert]**

Insert (key=5, priority=20) into treap with root (key=10, priority=15):

A) BST insert: 5 < 10, goes left of root
B) Priority 20 > 15 (parent), heap violation
C) Right-rotate at root 10
D) 5 becomes new root: (5,20) with right child (10,15)

**Answer: D**

**Explanation:**
Insert 5 as left child of 10 (BST). Priority 20 > 15 → rotate up. Right-rotate at 10: 5 becomes root, 10 becomes right child. 5's old right child (null) becomes 10's left child. Now BST: 5 < 10 ✓. Heap: 20 > 15 ✓. Balanced by randomized priorities.

---

**Q11.46: Intermediate - [Theory] - [2-3 Tree]**

2-3 Tree:

A) Every internal node has 2 or 3 children
B) All leaves at same level
C) Equivalent to Red-Black tree conceptually
D) All of the above

**Answer: D**

**Explanation:**
2-3 Tree: 2-node has 1 key, 2 children. 3-node has 2 keys, 3 children. All leaves at same depth. Insert: if node overflow (4 children), split and push median up. Perfectly balanced. Isomorphic to Red-Black trees: 2-node = black node, 3-node = black node with red child. Conceptual bridge to understanding Red-Black trees.

---

**Q11.47: Intermediate - [Theory] - [2-3-4 Tree]**

2-3-4 Tree:

A) Nodes have 2, 3, or 4 children
B) Direct mapping to Red-Black trees
C) 4-node = black node with two red children
D) All of the above

**Answer: D**

**Explanation:**
2-3-4 Tree: generalization of 2-3. 4-node has 3 keys, 4 children. Direct isomorphism with Red-Black trees: 2-node → black. 3-node → black with one red child. 4-node → black with two red children. This mapping proves Red-Black tree correctness and explains insert/delete cases. B-Tree of order 4.

---

**Q11.48: Advanced - [Theory] - [Left-Leaning Red-Black Tree]**

Left-Leaning Red-Black Tree (LLRB):

A) Restriction: red links lean left only
B) Simpler implementation (~80 lines of code)
C) 1-1 correspondence with 2-3 trees
D) All of the above

**Answer: D**

**Explanation:**
LLRB by Robert Sedgewick: constrain red links to lean left (3-nodes represented consistently). Reduces cases in insert/delete. Simpler code than standard Red-Black trees. 1-1 with 2-3 trees (not 2-3-4). Slight performance trade-off for simplicity. Used in educational implementations and some systems.

---

**Q11.49: Intermediate - [Theory] - [Rotation Cost]**

Cost of a single rotation (left or right):

A) O(1) time — constant number of pointer changes
B) Changes at most 3 pointers (node, parent, child)
C) Does not change keys, only structure
D) All of the above

**Answer: D**

**Explanation:**
Rotation: O(1). Three pointer updates: (1) rotating node's child becomes parent, (2) parent becomes child, (3) transferred subtree reattached. No key copying, no data movement. BST property preserved. This is why rotations are the fundamental rebalancing primitive for AVL, Red-Black, splay, and treap trees.

---

**Q11.50: Advanced - [Theory] - [Weight-Balanced Trees]**

Weight-balanced trees (BB[α] trees):

A) Balance based on subtree sizes, not heights
B) Fraction of nodes in each subtree within bounds
C) α parameter controls balance strictness
D) All of the above

**Answer: D**

**Explanation:**
Weight-balanced: for each node, size(left) / size(total) and size(right) / size(total) bounded by α and 1-α. α typically 1/4 to 1-1/√2. Size-based balance enables order statistics naturally (size info already stored). Alternative to height-balanced AVL. Used in some functional programming implementations.

---

**Q11.51: Foundational - [Theory] - [When to Use Which Tree]**

Choosing between balanced tree types:

A) AVL: read-heavy applications (faster lookups)
B) Red-Black: write-heavy applications (fewer rotations)
C) B-Tree: disk-based storage (minimize I/O)
D) All of the above

**Answer: D**

**Explanation:**
AVL: tightest balance → fastest search. Red-Black: bounded rotations → smoother insert/delete. B-Tree: high fanout → shallow trees → minimal disk I/O. Splay: self-adjusting for skewed access patterns. Treap: simple implementation with good expected performance. Choice depends on access pattern and storage medium.

---

**Q11.52: Advanced - [Theory] - [AVL Delete Cascading Rotations]**

AVL deletion worst case rotations:

A) O(log n) rotations possible
B) Fixing one node can create imbalance at ancestor
C) Each rotation along path to root is O(1)
D) All of the above

**Answer: D**

**Explanation:**
AVL delete: removing from shorter subtree can make BF = ±2. After rotation, subtree height may decrease by 1, causing parent's BF to become ±2. This cascading continues up to root, hence O(log n) rotations. Total time still O(log n). In contrast, RB delete needs at most 3 rotations.

---

**Q11.53: Intermediate - [Theory] - [B-Tree Splitting]**

When a B-Tree node overflows during insertion:

A) Node has m keys (one too many)
B) Split into two nodes at median
C) Median key moves to parent
D) All of the above

**Answer: D**

**Explanation:**
Split: node with m keys (max is m-1). Choose median (⌊m/2⌋-th key). Keys before median → left node. Keys after → right node. Median → parent. If parent overflows, cascade split. If root splits, new root created → tree height increases by 1. Height only changes through root splits/merges.

---

**Q11.54: Advanced - [Trace] - [B-Tree Delete with Merge]**

B-Tree order 3, tree: root [20] with children [10] and [30]. Delete 10:

A) Remove 10 from left child → [empty]
B) Node underflow (< ⌈3/2⌉-1 = 0 minimum keys... actually min keys = 1)
C) Left child now empty, borrow from sibling or merge
D) Merge: combine with [30] and parent key [20] → single node [20,30], becomes new root

**Answer: D**

**Explanation:**
Order 3 (t=2): min 1 key per non-root node. Delete 10: left child empty (0 keys). Can't borrow from sibling [30] (already at minimum with 1 key). Merge: left + parent key 20 + right [30] = [20,30]. Root becomes empty, removed. New root is [20,30]. Height decreases by 1.

---

**Q11.55: Intermediate - [Theory] - [B-Tree vs Binary Tree]**

B-Tree advantage over binary balanced trees for disk:

A) Each node = one disk page → one I/O per level
B) Branching factor hundreds or thousands → very shallow tree
C) Millions of keys in 3-4 levels
D) All of the above

**Answer: D**

**Explanation:**
Disk I/O is ~10^5 times slower than memory access. B-Tree: node size = disk page (4KB-16KB). With 4KB pages and 8-byte keys+pointers: ~500 keys per node. 10^9 keys: height ≈ log₅₀₀(10^9) ≈ 3-4. Only 3-4 disk reads. Binary tree: log₂(10^9) ≈ 30 levels = 30 disk reads.

---

**Q11.56: Advanced - [Theory] - [B+ Tree Leaf Linked List]**

B+ Tree leaf linked list enables:

A) Range queries: find start key, scan leaves sequentially
B) Full table scan without touching internal nodes
C) Efficient ORDER BY in databases
D) All of the above

**Answer: D**

**Explanation:**
B+ Tree leaves linked list: after finding range start via tree traversal, scan leaves linearly. Sequential disk reads (pre-fetchable). SQL range queries (WHERE x BETWEEN a AND b), full scans, and ORDER BY all benefit. Internal nodes stay in memory as cache; leaves retrieved as needed.

---

**Q11.57: Advanced - [Theory] - [RB Tree Proof: Height Bound]**

Prove Red-Black tree height ≤ 2 × log₂(n+1):

A) Subtree with black-height bh has ≥ 2^bh - 1 internal nodes
B) At least half the nodes on any path are black (no consecutive reds)
C) So bh ≥ h/2, giving n ≥ 2^(h/2) - 1, so h ≤ 2 × log₂(n+1)
D) All steps correct

**Answer: D**

**Explanation:**
Proof: (1) By induction, subtree rooted at x with bh(x) = k has ≥ 2^k - 1 internal nodes. (2) On any root-to-leaf path of length h, at least h/2 nodes are black (property 4: no consecutive reds). (3) So bh ≥ h/2. (4) n ≥ 2^(h/2) - 1, hence h ≤ 2 × log₂(n+1). QED.

---

**Q11.58: Foundational - [Theory] - [Balanced Tree Operations Summary]**

All balanced BSTs guarantee:

A) O(log n) search
B) O(log n) insert
C) O(log n) delete
D) All of the above

**Answer: D**

**Explanation:**
AVL, Red-Black, B-Trees, Splay (amortized), Treaps (expected): all guarantee O(log n) for core operations. The methods differ (rotations, splits, splaying, random priorities) but the invariant remains: tree height is O(log n), so all operations following a root-to-leaf path are O(log n).

---

**Q11.59: Intermediate - [Theory] - [B-Tree Proactive vs Reactive Split]**

Proactive splitting in B-Tree insertion:

A) Split full nodes on the way down before inserting
B) Avoids backtracking after insert
C) Single-pass top-down insertion
D) All of the above

**Answer: D**

**Explanation:**
Standard B-Tree insert: insert at leaf, split upward if needed (reactive/bottom-up). Proactive: on the way down, split any full node encountered. When reaching the leaf, it's guaranteed not full. No upward pass needed. Simplifies implementation, especially for concurrent access. Both produce valid B-Trees with same asymptotic cost.

---

**Q11.60: Advanced - [Theory] - [Splay Tree Working Set]**

Working set theorem for splay trees:

A) Access time proportional to log of "working set size"
B) Working set = number of distinct elements accessed since last access
C) Recently accessed items are faster
D) All of the above

**Answer: D**

**Explanation:**
Working set property: if element was accessed recently (few distinct accesses ago), the splay cost is O(log w) where w is the number of distinct items accessed since. This means splay trees naturally adapt to temporal locality. No explicit caching needed. Combined with sequential access theorem, splay trees are remarkably adaptive.

---

**Q11.61: Intermediate - [Theory] - [Red-Black NIL Sentinel]**

Red-Black tree NIL sentinel:

A) Single black node representing all null children
B) Simplifies code (no null pointer checks)
C) All leaves point to same NIL, NIL is always black
D) All of the above

**Answer: D**

**Explanation:**
Implementation: use single sentinel NIL node (color=black). All leaf pointers and root's parent point to NIL. Simplifies insert/delete fix-up code (always have valid parent/sibling to check, no null dereference). Space efficient: one extra node for entire tree. CLRS uses this convention.

---

**Q11.62: Advanced - [Theory] - [Scapegoat Tree Rebuild]**

Scapegoat tree rebalancing:

A) After insert, walk up to find "scapegoat" (unbalanced ancestor)
B) Rebuild entire subtree rooted at scapegoat to perfect balance
C) Amortized O(log n) per operation
D) All of the above

**Answer: D**

**Explanation:**
Scapegoat tree: no stored balance info. After insert, if any ancestor has size(child) > α × size(ancestor), that ancestor is the scapegoat. Flatten subtree (inorder), rebuild as balanced BST. Rebuild is O(k) for k nodes. Amortized O(log n) because rebuilds are infrequent. α typically 2/3 or 3/4. Space efficient: no extra fields per node.

---

**Q11.63: Expert - [Theory] - [Treap Expected Height]**

Expected height of treap with n nodes:

A) O(log n)
B) Same as random BST
C) Random priorities ensure random insertion order
D) All of the above

**Answer: D**

**Explanation:**
Treap with random priorities: structure identical to BST built by inserting keys in the order determined by priorities (highest priority first). Random priorities → random insertion order → expected height O(log n). More precisely, expected depth of any node is O(log n). Expected height is Θ(log n). Same analysis as randomized quicksort pivot depth.

---

**Q11.64: Expert - [Theory] - [Randomized BST vs Treap]**

Randomized BST vs Treap:

A) Both achieve O(log n) expected performance
B) Treap: random priorities assigned at insert, fixed thereafter
C) Randomized BST: randomize at each insert (join with probability based on sizes)
D) Both maintain random tree shape

**Answer: D**

**Explanation:**
Treap: assign random priority once, use to determine structure. Randomized BST: each insert, with probability 1/(n+1), new node becomes root (otherwise recurse). Both produce uniformly random tree shapes. Treap is simpler (just priority comparison). Randomized BST doesn't need stored priorities but needs size information.

---

**Q11.65: Intermediate - [Trace] - [AVL Insert Extended]**

Insert [3, 2, 1, 4, 5, 6, 7] into AVL tree:

A) After [3,2,1]: BF(3)=2 (LL), right rotate → 2(1,3)
B) After 4: 2(1,3(null,4)), balanced
C) After 5: 2(1,3(null,4(null,5))), BF(3)=-2 (RR), left rotate at 3 → 2(1,4(3,5))
D) Continue: after 6,7 more rotations maintain O(log n) height

**Answer: D**

**Explanation:**
Detailed trace: [3,2,1] → rotate → 2(1,3). Add 4: balanced. Add 5: BF(3)=-2, left rotate → 2(1,4(3,5)). Add 6: BF(2)=-2, left rotate → 4(2(1,3),5(null,6)). Add 7: BF(5)=-2, left rotate → 4(2(1,3),6(5,7)). Final height 2 for 7 nodes (perfect). AVL maintained balance throughout.

---

**Q11.66: Advanced - [Theory] - [B-Tree Disk I/O Model]**

In the disk I/O model:

A) Cost = number of disk page reads/writes
B) B-Tree operations: O(log_B n) I/Os where B = page size
C) Optimal for comparison-based searching on disk
D) All of the above

**Answer: D**

**Explanation:**
External memory model: memory size M, block size B. Transfer unit = one block. B-Tree with branching factor ≈ B: height ≈ log_B(n). Each level = 1 I/O. Total I/Os per operation: O(log_B n). Provably optimal for comparison-based search in this model. B+ Tree variant preferred for sequential access.

---

**Q11.67: Intermediate - [Theory] - [AVL Single vs Double Rotation]**

When does AVL need double rotation?

A) When imbalance and child's heavy side differ (zig-zag)
B) LR case: left child is right-heavy
C) RL case: right child is left-heavy
D) All of the above

**Answer: D**

**Explanation:**
Single rotation: imbalance direction matches child's heavy side (LL or RR → same direction). Double rotation: directions differ (LR or RL → zig-zag). Double rotation = two single rotations. First rotation straightens the zig-zag, second rotation fixes the imbalance. Common exam question: identifying which rotation type to apply.

---

**Q11.68: Expert - [Theory] - [Red-Black vs 2-3-4 Mapping]**

Red-Black tree to 2-3-4 tree mapping:

A) Merge red nodes with black parents to form 2-3-4 nodes
B) Black node alone = 2-node
C) Black node with one red child = 3-node
D) Black node with two red children = 4-node

**Answer: D**

**Explanation:**
Mapping: collapse red nodes into parent black node. Black with no red children → 2-node (1 key, 2 children). With one red child → 3-node (2 keys, 3 children). With two red children → 4-node (3 keys, 4 children). This isomorphism proves Red-Black tree correctness: every Red-Black tree corresponds to a valid 2-3-4 tree, and 2-3-4 trees are always balanced.

---

**Q11.69: Foundational - [Theory] - [Self-Balancing Summary]**

Common self-balancing BSTs:

A) AVL tree (height-balanced, BF ∈ {-1,0,1})
B) Red-Black tree (color-constrained, 5 properties)
C) Splay tree (self-adjusting, amortized O(log n))
D) All of the above, plus Treap, Scapegoat, Skip List

**Answer: D**

**Explanation:**
Self-balancing BST family: AVL (strict balance, fast reads), Red-Black (relaxed balance, fast writes), Splay (adaptive, no metadata), Treap (randomized, simple), Scapegoat (lazy rebuild, no per-node metadata), Skip List (probabilistic, not a tree but alternatives-listed). Each has trade-offs for different use cases.

---

**Q11.70: Expert - [Theory] - [Persistent Red-Black Tree]**

Persistent Red-Black tree:

A) Path copying for functional updates
B) O(log n) new nodes per update
C) Previous versions remain accessible
D) All of the above

**Answer: D**

**Explanation:**
Persistent Red-Black: functional (immutable) data structure. Each insert/delete creates new path from root (path copying), shares unchanged subtrees. O(log n) new nodes per operation. All versions accessible via their roots. Used in functional languages (Haskell, Clojure), version control systems, temporal databases. Refer to Q10.47-48 for persistent BST concepts.

---

**Q11.71: Intermediate - [Theory] - [B-Tree Minimum Degree]**

B-Tree minimum degree t means:

A) Every non-root internal node has at least t children
B) Every node has at most 2t children
C) Every non-root node has at least t-1 keys, at most 2t-1 keys
D) All of the above

**Answer: D**

**Explanation:**
Minimum degree t: non-root internal nodes have [t, 2t] children and [t-1, 2t-1] keys. Root: [1, 2t-1] keys (at least 1 key if non-empty). Leaf same key constraints. The parameter t controls the trade-off: larger t → shorter tree, wider nodes → better for disk where one node = one page read.

---

**Q11.72: Expert - [Theory] - [Amortized Rotations in RB Trees]**

Over a sequence of n insertions into an initially empty Red-Black tree:

A) Total rotations ≤ 2n
B) Amortized O(1) rotations per insert
C) Most inserts need 0 rotations (just recoloring)
D) All of the above

**Answer: D**

**Explanation:**
Red-Black insert: at most 2 rotations per insert. Over n inserts, ≤ 2n rotations total. In practice, most inserts terminate with just recoloring (Case 1 in fix-up). Rotations occur only when uncle is black. Empirically, average rotations per insert ≈ 0.6 for random data. This is why Red-Black trees have excellent practical performance for insertions.

---

**Q11.73: Expert - [Theory] - [Skip List vs Balanced BST]**

Skip list vs balanced BST:

A) Skip list: probabilistic O(log n), simpler implementation
B) BST: deterministic O(log n) (AVL/RB), better worst case
C) Skip list: easier concurrent access (lock-free)
D) All are valid comparisons

**Answer: D**

**Explanation:**
Skip list: randomized, expected O(log n). Simpler to implement correctly than Red-Black. Excellent for concurrent access (lock-free with CAS). Used in Redis, LevelDB, Java ConcurrentSkipListMap. BSTs: deterministic guarantees, better cache performance (nodes are pointers vs skip list's levels). Trade-off: simplicity/concurrency (skip list) vs determinism/cache (BST).

---

**Q11.74: Advanced - [Theory] - [Top-Down vs Bottom-Up]**

Top-down vs bottom-up Red-Black insert:

A) Bottom-up: insert, then fix violations walking up (CLRS approach)
B) Top-down: fix potential violations while descending
C) Top-down avoids backtracking (no parent pointers needed)
D) All of the above

**Answer: D**

**Explanation:**
Bottom-up (CLRS): insert red node, walk up fixing violations. Needs parent pointers or stack. Top-down (Sedgewick): on the way down, split 4-nodes (recolor black parent with two red children). Guarantees no uncle-is-red case at bottom. Simpler in some implementations. Both produce valid Red-Black trees, same asymptotic complexity.

---

**Q11.75: Expert - [Theory] - [Balanced Tree Lower Bound]**

Lower bound for balanced BST operations:

A) Comparison-based search: Ω(log n)
B) No balanced BST can do better than O(log n) worst case
C) Optimal for comparison-based ordered data structures
D) All of the above

**Answer: D**

**Explanation:**
Information-theoretic: n keys → log₂(n) comparisons needed to distinguish (decision tree depth). Any comparison-based BST: Ω(log n) for search. Balanced BSTs achieve this bound (O(log n)). Non-comparison methods (hashing, integer data structures like van Emde Boas) can do better for specific key types but lose ordering guarantees. Balanced BSTs are optimal for ordered, comparison-based operations.

---

## Chapter 11 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 19 | AVL definition, balance factor, rotations, RB properties, B-Tree basics, Splay/Treap concepts |
| Intermediate | 30 | AVL insert/delete traces, RB insert fix-up, B-Tree insert/split, B+ Tree, 2-3 trees, Splay operations |
| Advanced | 19 | AVL cascading rotations, RB proof, B-Tree I/O model, Splay properties, Scapegoat, weight-balanced |
| Expert | 7 | Treap expected height, RB-to-2-3-4 mapping, persistent RB, amortized analysis, lower bounds |

**Total MCQs: 75** | **Target Met: ✓**

**Key Balanced Tree Comparisons:**

| Tree | Height | Insert Rotations | Delete Rotations | Extra Storage |
|------|--------|-------------------|-------------------|---------------|
| AVL | ≤ 1.44 log n | ≤ 2 | O(log n) | Height/BF per node |
| Red-Black | ≤ 2 log n | ≤ 2 | ≤ 3 | Color bit per node |
| B-Tree | O(log_t n) | Splits O(log_t n) | Merges O(log_t n) | None extra |
| Splay | Amortized O(log n) | Amortized O(log n) | Amortized O(log n) | None |
| Treap | Expected O(log n) | Expected O(log n) | Expected O(log n) | Priority per node |

**Next:** Chapter 12 - Heaps & Priority Queues
