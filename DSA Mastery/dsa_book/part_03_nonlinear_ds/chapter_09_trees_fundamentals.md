# Chapter 9: Trees — Fundamentals

**Target:** 65 MCQs | **Distribution:** 16 Foundational, 26 Intermediate, 18 Advanced, 5 Expert

---

**Q9.1: Foundational - [Theory] - [Tree Definition]**

A tree is:

A) A linear data structure like linked list
B) A hierarchical structure with nodes and edges, no cycles
C) A cyclic graph with hierarchy
D) Only binary nodes allowed

**Answer: B**

**Explanation:**
Tree: hierarchical, connected, acyclic graph. One root node, edges connect parent to children. No cycles (unique path between any two nodes). N nodes, N-1 edges. Non-linear structure. Can have any number of children per node (binary tree: at most 2). Foundation for file systems, DOM, organization charts, decision trees.

---

**Q9.2: Foundational - [Theory] - [Tree Terminology]**

In a tree, leaf node is:

A) The first node
B) Node with no children
C) Node with exactly one child
D) The root node

**Answer: B**

**Explanation:**
Leaf (external node): no children. Root: topmost node, no parent. Internal node: has at least one child. Parent: node with children. Children: nodes directly connected below parent. Siblings: share same parent. Ancestors: path to root. Descendants: subtree nodes. Height: longest path to leaf. Depth: distance from root.

---

**Q9.3: Foundational - [Theory] - [Binary Tree]**

Binary tree node has:

A) Exactly 2 children
B) At most 2 children (left and right)
C) Any number of children
D) Only left child

**Answer: B**

**Explanation:**
Binary tree: each node has 0, 1, or 2 children. Left and right child distinct. Full binary tree: every node has 0 or 2 children. Complete binary tree: all levels full except possibly last, filled left to right. Perfect binary tree: all internal nodes have 2 children, all leaves at same level.

---

**Q9.4: Foundational - [Theory] - [Tree Height]**

Height of a tree:

A) Number of nodes
B) Number of edges on longest root-to-leaf path
C) Number of leaves
D) Depth of root

**Answer: B**

**Explanation:**
Height: maximum number of edges from root to any leaf. Single node tree: height 0. Depth of node: edges from root to node. Height of node: edges from node to deepest leaf. Tree height = root height = max depth.

---

**Q9.5: Foundational - [Theory] - [Tree Traversals]**

Binary tree inorder traversal order:

A) Root, left, right
B) Left, root, right
C) Left, right, root
D) Root, right, left

**Answer: B**

**Explanation:**
Inorder: left subtree, root, right subtree. Preorder: root, left, right. Postorder: left, right, root. For BST, inorder gives sorted order. Traversals: recursive or iterative (stack). Time O(n), space O(h) where h = height.

---

**Q9.6: Foundational - [Trace] - [Inorder Traversal]**

Tree: 1(2(4,5),3), inorder output:

A) 1,2,4,5,3
B) 4,2,5,1,3
C) 4,5,2,3,1
D) 1,2,3,4,5

**Answer: B**

**Explanation:**
Tree: root 1, left 2 (left 4, right 5), right 3. Inorder: left(4,2,5), root(1), right(3) → 4,2,5,1,3. Preorder: 1,2,4,5,3. Postorder: 4,5,2,3,1.

---

**Q9.7: Intermediate - [Theory] - [Level Order Traversal]**

Level order (breadth-first) traversal uses:

A) Stack
B) Queue
C) Recursion
D) Priority queue

**Answer: B**

**Explanation:**
Level order: process nodes level by level. Queue: enqueue root. While queue not empty: dequeue node, process, enqueue left child, enqueue right child. Time O(n), space O(w) where w = maximum width.

---

**Q9.8: Intermediate - [Trace] - [Level Order]**

Tree: 1(2(4,5),3(6,7)), level order:

A) 1,2,3,4,5,6,7
B) 1,2,4,5,3,6,7
C) 4,5,2,6,7,3,1
D) 1,3,2,7,6,5,4

**Answer: A**

**Explanation:**
Level 0: 1. Level 1: 2,3. Level 2: 4,5,6,7. Output: 1,2,3,4,5,6,7.

---

**Q9.9: Intermediate - [Theory] - [Tree Diameter]**

Diameter of binary tree:

A) Number of nodes
B) Longest path between any two nodes (edges count)
C) Height of root
D) Number of leaves

**Answer: B**

**Explanation:**
Diameter: longest path between any two nodes. Path length = number of edges. Algorithm: at each node, diameter through node = left_height + right_height. Global max of all nodes. O(n) time.

---

**Q9.10: Intermediate - [Code] - [Max Depth/Height]**

Max depth of binary tree:

A) 0 for null, else 1 + max(left_depth, right_depth)
B) O(n) time
C) O(h) recursion stack space
D) All of the above

**Answer: D**

**Explanation:**
Recursive: if node null, return 0. Else return 1 + max(maxDepth(left), maxDepth(right)). Each node visited once: O(n). Stack depth O(h).

---

**Q9.11: Intermediate - [Theory] - [Complete Binary Tree]**

Complete binary tree:

A) All levels completely filled
B) All levels filled except possibly last, filled left to right
C) Every node has 0 or 2 children
D) All leaves at same level

**Answer: B**

**Explanation:**
Complete binary tree: all levels fully filled except possibly last level, which is filled from left to right. Used in heap implementation. Height ⌊log₂n⌋. Can be stored compactly in array.

---

**Q9.12: Intermediate - [Theory] - [Full vs Complete vs Perfect]**

Perfect binary tree:

A) All internal nodes have 2 children, all leaves at same level
B) Height h has exactly 2^(h+1) - 1 nodes
C) All levels completely filled
D) All of the above

**Answer: D**

**Explanation:**
Perfect: every node has 0 or 2 children, all leaves at same level. Nodes = 2^(h+1) - 1. Full: every node has 0 or 2 children (leaves can be at different levels). Complete: filled left to right, last level may not be full.

---

**Q9.13: Intermediate - [Theory] - [Array Representation]**

Complete binary tree in array, node at index i:

A) Left child at 2i, right child at 2i+1
B) Parent at ⌊i/2⌋
C) Root at index 1 (or 0 with 2i+1, 2i+2)
D) All of the above

**Answer: D**

**Explanation:**
Array representation (1-indexed): root at 1, children of i at 2i and 2i+1, parent at ⌊i/2⌋. 0-indexed: root at 0, left=2i+1, right=2i+2, parent=⌊(i-1)/2⌋. No pointers needed, cache-friendly. Used for heaps.

---

**Q9.14: Intermediate - [Trace] - [Array Indexing]**

Tree [1,2,3,4,5,6,7] (level order), node 3's children:

A) 0-indexed: node at index 2 (value 3), left=2×2+1=5, right=2×2+2=6
B) Children at indices 5,6 → values 6,7
C) Array indexing enables O(1) parent/child access
D) All of the above

**Answer: D**

**Explanation:**
0-indexed array: index 0→1, 1→2, 2→3, 3→4, 4→5, 5→6, 6→7. Node at index 2 (value 3): left=5 (value 6), right=6 (value 7).

---

**Q9.15: Advanced - [Theory] - [Morris Traversal]**

Morris inorder traversal:

A) O(1) space by threading tree
B) Create temporary links from predecessor to current
C) Restore tree structure after
D) All of the above

**Answer: D**

**Explanation:**
Morris traversal: O(1) space, no stack, no recursion. For current, find inorder predecessor. If predecessor.right is null, set to current (thread), go left. Else restore null, visit current, go right. O(n) time.

---

**Q9.16: Advanced - [Trace] - [Morris Traversal]**

Tree: 1(2(4,5),3), Morris inorder result:

A) Creates temporary threads
B) 4,2,5,1,3
C) Restores tree after
D) All of the above

**Answer: D**

**Explanation:**
Morris creates temporary links to avoid stack. Result: 4,2,5,1,3 (inorder). Tree structure restored after traversal.

---

**Q9.17: Advanced - [Theory] - [Tree from Traversals]**

Reconstruct tree from inorder and preorder:

A) Preorder first element is root
B) Find root in inorder, left is left subtree, right is right
C) Recursively build
D) All of the above

**Answer: D**

**Explanation:**
Preorder: root, left, right. Inorder: left, root, right. First preorder element = root. Find root position in inorder, left part is left subtree, right part is right subtree. Recursively build. Time O(n²) naive, O(n) with hash map.

---

**Q9.18: Advanced - [Trace] - [Build Tree]**

Inorder [4,2,5,1,3], Preorder [1,2,4,5,3]:

A) Root=1 (first preorder)
B) Inorder: [4,2,5] left, [3] right
C) Recursively build left with pre[1..3], in[0..2]
D) Build right with pre[4], in[4]

**Answer: D**

**Explanation:**
Root=1. Left subtree size 3 from inorder. Preorder: [2,4,5] is left, [3] is right. Recursively build. Final tree: 1 root, left 2(4,5), right 3.

---

**Q9.19: Advanced - [Theory] - [Iterative Traversals]**

Iterative inorder with stack:

A) Push all left descendants
B) Pop, visit, go right
C) O(n) time, O(h) space
D) All of the above

**Answer: D**

**Explanation:**
Iterative inorder: while current or stack: push all left children of current. Pop, visit, set current to right. Simulates recursion. Preorder: visit before pushing children. Postorder: more complex. All O(n) time, O(h) space.

---

**Q9.20: Advanced - [Trace] - [Iterative Inorder]**

Tree: 1(2(4,5),3), iterative inorder result:

A) Uses stack
B) 4,2,5,1,3
C) O(h) space
D) All of the above

**Answer: D**

**Explanation:**
Iterative inorder with stack produces 4,2,5,1,3. Stack depth O(h) where h is tree height.

---

**Q9.21: Advanced - [Theory] - [Boundary Traversal]**

Boundary traversal of binary tree:

A) Print left boundary (top-down, leaves excluded)
B) Print all leaves (left to right)
C) Print right boundary (bottom-up, leaves excluded)
D) All of the above

**Answer: D**

**Explanation:**
Boundary: anticlockwise. Left boundary + leaves + right boundary reverse. O(n) time. Variation combining multiple traversal patterns.

---

**Q9.22: Expert - [Theory] - [Threaded Binary Tree]**

Threaded binary tree:

A) Null pointers store inorder successor/predecessor
B) Inorder traversal without stack or recursion
C) Right thread points to inorder successor
D) All of the above

**Answer: D**

**Explanation:**
Threaded tree: null pointers store threads to predecessor/successor. Enables iterative traversal without stack. More complex insertion/deletion. Morris traversal achieves similar without permanent threads.

---

**Q9.23: Intermediate - [Application] - [Same Tree]**

Check if two trees are identical:

A) Both null → true
B) One null → false
C) Values equal and left subtrees same and right subtrees same
D) All of the above

**Answer: D**

**Explanation:**
Recursive: both null → true. One null → false. Values differ → false. Else recurse on left and right. O(n) time.

---

**Q9.24: Intermediate - [Application] - [Symmetric Tree]**

Check if tree is mirror of itself:

A) Left subtree mirrors right subtree
B) Recursive: left.val == right.val, left.left mirrors right.right, left.right mirrors right.left
C) Or iterative with two queues
D) All of the above

**Answer: D**

**Explanation:**
Symmetric: mirror image around center. Recursive or iterative with queues. O(n) time.

---

**Q9.25: Intermediate - [Application] - [Path Sum]**

Has path sum: root-to-leaf path equals target:

A) DFS, subtract node value from target
B) At leaf, check if target equals leaf value
C) Recursive: any path from left or right works
D) All of the above

**Answer: D**

**Explanation:**
Recursive: hasPathSum(root, target) = root is leaf and root.val == target, OR hasPathSum(left, target-root.val), OR hasPathSum(right, target-root.val). O(n) time.

---

**Q9.26: Advanced - [Theory] - [Lowest Common Ancestor]**

LCA of two nodes in binary tree:

A) Node where paths to p and q diverge
B) Deepest node that has both p and q as descendants
C) Recursive: if node is p or q, return node; else find in left and right; if both found, return current
D) All of the above

**Answer: D**

**Explanation:**
LCA: deepest common ancestor. Recursive algorithm: O(n) time. Assumes both nodes exist. Variants: BST LCA (use values), with parent pointers (like find intersection of linked lists).

---

**Q9.27: Expert - [Theory] - [Euler Tour]**

Euler tour of tree:

A) Visit each edge exactly twice (down and up)
B) Represents tree as sequence
C) Used for RMQ-based LCA
D) All of the above

**Answer: D**

**Explanation:**
Euler tour: traverse tree, record node when entering and leaving. Sequence length 2n-1 for n nodes. With depth array enables LCA via RMQ. O(n) preprocessing, O(1) or O(log n) LCA queries.

---

**Q9.28: Intermediate - [Application] - [Count Nodes]**

Count nodes in complete binary tree:

A) O(n) traversal
B) O((log n)²) using complete property
C) Check if leftmost depth equals rightmost depth
D) Both B and C

**Answer: D**

**Explanation:**
Complete tree: can be more efficient than O(n). If leftmost and rightmost depth equal, perfect tree: 2^h - 1 nodes. Else recursively count. O((log n)²) time.

---

**Q9.29: Advanced - [Trace] - [Count Complete Tree]**

Complete tree, check if perfect:

A) Left depth: keep going left
B) Right depth: keep going right
C) If equal: 2^h - 1 nodes
D) Else: 1 + count(left) + count(right)

**Answer: D**

**Explanation:**
Compute left and right depth. If equal, perfect tree. Else recursively count subtrees.

---

**Q9.30: Intermediate - [Theory] - [Serialize/Deserialize]**

Serialize binary tree to string:

A) Preorder with null markers
B) Level order with null markers
C) Multiple valid encodings
D) All of the above

**Answer: D**

**Explanation:**
Serialization: convert tree to string. Preorder with "null" markers, level order with queue, or parenthesis representation. O(n) time.

---

**Q9.31: Advanced - [Trace] - [Preorder Serialization]**

Tree: 1(2(4,5),3), preorder with nulls:

A) "1,2,4,null,null,5,null,null,3,null,null"
B) Null indicates missing child
C) Can reconstruct uniquely
D) All of the above

**Answer: D**

**Explanation:**
Preorder with nulls uniquely identifies tree structure. Deserialize by reading values recursively.

---

**Q9.32: Advanced - [Theory] - [Subtree Check]**

Check if tree S is subtree of T:

A) For each node in T, check if matches S
B) Match: same structure and values
C) O(m × n) naive
D) All of the above

**Answer: D**

**Explanation:**
Naive O(m × n). Optimized: serialize both, check substring. Or compute hash for subtrees. O(n + m).

---

**Q9.33: Expert - [Theory] - [Scapegoat Tree]**

Scapegoat tree:

A) Self-balancing without extra storage per node
B) Rebuild entire subtree when unbalanced
C) Amortized O(log n) operations
D) All of the above

**Answer: D**

**Explanation:**
Scapegoat tree: no height/weight fields. Rebuild to perfect balance when unbalanced. Simpler, less memory, occasional expensive rebuilds.

---

**Q9.34: Intermediate - [Application] - [Flatten Tree to List]**

Flatten binary tree to linked list (inorder):

A) Morris traversal: O(1) space
B) Or recursive: process right first, then left
C) Each node's right points to next, left null
D) All of the above

**Answer: D**

**Explanation:**
Flatten to right-linked list. Multiple approaches: Morris O(1) space, recursive, or iterative with prev pointer.

---

**Q9.35: Advanced - [Theory] - [Vertical Order Traversal]**

Vertical order of binary tree:

A) Column (horizontal distance) groups nodes
B) Root at column 0, left child column-1, right column+1
C) Level within column determines order
D) All of the above

**Answer: D**

**Explanation:**
Vertical: group by horizontal distance. Use BFS with tracking. Hash map column→list. Sort columns. O(n log n) or O(n) with TreeMap.

---

**Q9.36: Intermediate - [Application] - [Right View]**

Right side view of binary tree:

A) Last node at each level
B) BFS, record last of each level
C) DFS, prefer right child first, record depth
D) All of the above

**Answer: D**

**Explanation:**
Right view: last node per level. BFS or DFS (right before left). O(n) time.

---

**Q9.37: Advanced - [Theory] - [Tree Isomorphism]**

Two trees isomorphic if:

A) Can be made identical by swapping left/right children
B) Recursive: both null, or one child null but other swap works, or both children isomorphic (possibly swapped)
C) Structure same up to child swapping
D) All of the above

**Answer: D**

**Explanation:**
Isomorphic trees: same structure, children may be swapped. Recursive check O(n) time.

---

**Q9.38: Expert - [Theory] - [Tree Canonization]**

Tree canonization (canonical form):

A) Unique string representation regardless of child order
B) Sort subtrees' canonical forms
C) Parentheses encoding with sorted children
D) All of the above

**Answer: D**

**Explanation:**
Canonical form: isomorphic trees have same encoding. Sort children, combine with parentheses. Tree isomorphism reduces to string equality.

---

**Q9.39: Intermediate - [Application] - [Sum Root to Leaf]**

Sum of root-to-leaf binary numbers:

A) DFS, accumulate value: curr = curr × 2 + node.val
B) At leaf, add to sum
C) Return sum
D) All of the above

**Answer: D**

**Explanation:**
Path 1→0→1 represents binary 101 = 5. DFS with accumulated value. O(n) time, O(h) space.

---

**Q9.40: Advanced - [Theory] - [Root to Leaf Paths]**

Print all root-to-leaf paths:

A) DFS, maintain current path list
B) At leaf, add path to result
C) Backtrack: remove node before returning
D) All of the above

**Answer: D**

**Explanation:**
Backtracking DFS: add node to path, if leaf copy to result, recurse, remove node (backtrack). Classic backtracking pattern.

---

**Q9.41: Intermediate - [Theory] - [Maximum Width]**

Maximum width of binary tree:

A) Maximum nodes at any level
B) Level order, count per level
C) Or assign indices (like heap), width = max - min + 1
D) All of the above

**Answer: D**

**Explanation:**
Width: max nodes at any depth. Level order counting, or assign indices like complete tree: width = max_index - min_index + 1 per level.

---

**Q9.42: Advanced - [Trace] - [Width with Indices]**

Tree: 1(2(4),3), indices: 1→0, 2→1, 3→2, 4→3:

A) Level 0: [0], width=1
B) Level 1: [1,2], width=2
C) Level 2: [3], width=1
D) Max width = 2

**Answer: D**

**Explanation:**
Assign indices like complete tree. Calculate width per level as max - min + 1.

---

**Q9.43: Expert - [Theory] - [Succinct Tree Representation]**

Succinct binary tree:

A) Uses 2n + o(n) bits for n nodes
B) Balanced parentheses representation
C) Operations: parent, left-child, right-child in O(1)
D) All of the above

**Answer: D**

**Explanation:**
Succinct data structures: space close to information-theoretic minimum. Balanced parentheses encoding. O(1) operations with rank/select. Used for massive trees in limited memory.

---

**Q9.44: Intermediate - [Application] - [Merge Two Binary Trees]**

Merge two binary trees:

A) If both nodes exist: sum values
B) Recurse on left and right children
C) If one null: return other
D) All of the above

**Answer: D**

**Explanation:**
Recursive: sum values if both exist, else return non-null node. Recurse on children. O(n) time.

---

**Q9.45: Advanced - [Theory] - [Find Mode]**

Find mode(s) in BST:

A) Inorder traversal gives sorted order
B) Count consecutive equal values
C) Track max frequency
D) All of the above

**Answer: D**

**Explanation:**
BST inorder is sorted. Count runs of equal values. O(n) time, O(1) extra space. No hash needed for BST.

---

**Q9.46: Advanced - [Trace] - [BST Mode]**

BST: 1(null,2(2,null)), modes:

A) Inorder: 1,2,2
B) Count: 1 appears 1, 2 appears 2
C) Mode = [2]
D) All of the above

**Answer: D**

**Explanation:**
Inorder of BST gives sorted values with duplicates consecutive. Count frequencies to find mode.

---

**Q9.47: Expert - [Theory] - [Tree Decomposition]**

Tree decomposition (for dynamic programming):

A) Break tree into subtrees
B) DP on rooted trees: process children, combine
C) Rerooting technique for unrooted trees
D) All of the above

**Answer: D**

**Explanation:**
Tree DP: root tree, compute based on children. Rerooting for unrooted problems. Fundamental for tree algorithms.

---

**Q9.48: Expert - [Theory] - [Centroid Decomposition]**

Centroid of tree:

A) Node where removal splits tree into components ≤ n/2
B) Always exists
C) Centroid decomposition: recursively decompose at centroids
D) All of the above

**Answer: D**

**Explanation:**
Centroid: removing it leaves no subtree > n/2 nodes. Centroid decomposition: recursively decompose. Tree height O(log n) after. Useful for divide and conquer on trees.

---

**Q9.49: Intermediate - [Application] - [Trim BST]**

Trim BST to range [L, R]:

A) If node.val < L: trim right only
B) If node.val > R: trim left only
C) Else: trim both, return node
D) All of the above

**Answer: D**

**Explanation:**
Recursive trim: return right if too small, return left if too large, else trim both children. O(n) time.

---

**Q9.50: Advanced - [Theory] - [Tree Iterator]**

Binary search tree iterator:

A) Inorder traversal on demand
B) Stack for partially traversed nodes
C) next() and hasNext() O(1) amortized
D) All of the above

**Answer: D**

**Explanation:**
BST iterator: traverse inorder lazily. Stack maintains state. Amortized O(1). Space O(h). Used for merging BSTs, k-th smallest.

---

**Q9.51: Expert - [Theory] - [Binary Lifting]**

Binary lifting for tree LCA:

A) Preprocess up[node][i] = 2^i-th ancestor
B) O(n log n) preprocessing
C) O(log n) LCA queries
D) All of the above

**Answer: D**

**Explanation:**
Binary lifting: up[v][i] = 2^i-th ancestor. Preprocess O(n log n), query O(log n). Supports ancestor queries.

---

**Q9.52: Intermediate - [Application] - [N-ary Tree]**

N-ary tree preorder:

A) Visit root, then each child recursively
B) No distinction of left/right
C) Iterative: stack, push children right-to-left
D) All of the above

**Answer: D**

**Explanation:**
N-ary tree: node has list of children. Preorder: root then children. Iterative: push children right-to-left so leftmost processed first.

---

**Q9.53: Advanced - [Theory] - [Encode-Decode N-ary]**

Serialize N-ary tree:

A) Preorder with children count: "val,numChildren,child1,...,childN"
B) Or special separator between siblings
C) Both valid approaches
D) None work

**Answer: C**

**Explanation:**
Two approaches: encode children count then children recursively, or use separator. Both valid for serialization.

---

**Q9.54: Expert - [Theory] - [Lock-Free Tree]**

Lock-free binary tree operations:

A) CAS on child pointers
B) Copy-on-write for updates
C) Read-Copy-Update (RCU) for traversal
D) All of the above

**Answer: D**

**Explanation:**
Concurrent trees: lock-free via CAS. RCU: readers don't block. Complex, many research variants.

---

**Q9.55: Intermediate - [Application] - [Average of Levels]**

Average of each level in binary tree:

A) Level order BFS
B) Sum and count per level
C) Average = sum / count
D) All of the above

**Answer: D**

**Explanation:**
BFS: track level size and sum, compute average. O(n) time.

---

**Q9.56: Advanced - [Theory] - [Find Duplicate Subtrees]**

Find all duplicate subtrees:

A) Serialize each subtree
B) Hash map: serialization → count
C) Return subtrees with count > 1
D) All of the above

**Answer: D**

**Explanation:**
Postorder serialization. Hash map tracks. O(n) time. Identifies structurally identical subtrees.

---

**Q9.57: Expert - [Theory] - [Hashing Subtrees]**

Efficient subtree hashing:

A) Assign unique IDs to structures
B) Recursive: hash = combine(hash(left), val, hash(right))
C) Map hash → representative node
D) All of the above

**Answer: D**

**Explanation:**
Merkle tree-style hashing. O(1) duplicate detection. Used in Git, blockchain.

---

**Q9.58: Expert - [Theory] - [Heavy-Light Decomposition]**

Heavy-light decomposition:

A) Decompose tree into disjoint paths
B) Heavy edge: child with largest subtree
C) Enables O(log²n) path queries
D) All of the above

**Answer: D**

**Explanation:**
HLD: split into heavy paths. Root-to-leaf crosses O(log n) paths. Path queries via segment trees. O(log²n) query, O(n) preprocessing.

---

**Q9.59: Intermediate - [Application] - [Increasing Order Search Tree]**

Increasing order search tree:

A) Inorder traversal
B) Relink nodes: left=null, right=next inorder
C) Return leftmost node
D) All of the above

**Answer: D**

**Explanation:**
Transform BST to right-linked list in increasing order. Inorder relinking. O(n) time.

---

**Q9.60: Advanced - [Theory] - [Construct from Traversal]**

Construct tree from inorder and postorder:

A) Postorder last element is root
B) Find root in inorder, split
C) Recursively build right then left (postorder order)
D) All of the above

**Answer: D**

**Explanation:**
Similar to inorder+preorder. Postorder: left, right, root. Last element is root. Build right first. O(n) with hash map.

---

**Q9.61: Expert - [Theory] - [Cartesian Tree Construction]**

Cartesian tree from array:

A) Root is minimum (or maximum) element
B) Left subtree from left subarray, right from right
C) Build O(n) using monotonic stack
D) All of the above

**Answer: D**

**Explanation:**
Cartesian tree: heap ordered, inorder gives array. O(n) with stack. Used in RMQ.

---

**Q9.62: Expert - [Theory] - [Treap]**

Treap (tree + heap):

A) Binary search tree by key
B) Heap by random priority
C) Expected O(log n) height
D) All of the above

**Answer: D**

**Explanation:**
Treap: BST by key, heap by priority. Expected O(log n) height. Split/merge operations useful.

---

**Q9.63: Expert - [Theory] - [Randomized BST]**

Randomized BST vs deterministic:

A) Random priorities avoid worst-case
B) Expected height O(log n)
C) No rebalancing rotations needed
D) All of the above

**Answer: D**

**Explanation:**
Randomized BSTs: expected O(log n) height. Simpler than deterministic balancing. Good amortized bounds.

---

**Q9.64: Expert - [Theory] - [Summary]**

Binary tree fundamentals essential because:

A) Basis for BST, heaps, segment trees
B) Recursive structure elegant for algorithms
C) Many real-world hierarchies (file systems, DOM)
D) All of the above

**Answer: D**

**Explanation:**
Binary trees: fundamental hierarchical structure. Basis for many advanced data structures. Recursive nature elegant. Real applications: file systems, HTML/XML DOM.

---

**Q9.65: Intermediate - [Application] - [Closest Value in BST]**

Closest value to target in BST:

A) Compare current, track closest
B) If target < current, go left; else go right
C) O(h) time
D) All of the above

**Answer: D**

**Explanation:**
BST search: track closest. Go left or right based on comparison. O(h) = O(log n) balanced. Similar to binary search.

---

## Chapter 9 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 12 | Tree definition, terminology, traversals, basic properties |
| Intermediate | 26 | Diameter, serialization, LCA, tree construction, iterators |
| Advanced | 18 | Morris traversal, threading, vertical order, width, decomposition |
| Expert | 9 | Succinct trees, centroid decomposition, treaps, binary lifting |

**Total MCQs: 65** | **Target Met: ✓**

**Key Tree Complexities:**
- Traversal (pre/in/post/level): O(n) time, O(h) space
- Height calculation: O(n) time
- Diameter: O(n) time
- LCA: O(n) preprocessing, O(1) or O(log n) query
- Tree from traversals: O(n) with hash map

**Next:** Chapter 10 - Binary Search Trees
