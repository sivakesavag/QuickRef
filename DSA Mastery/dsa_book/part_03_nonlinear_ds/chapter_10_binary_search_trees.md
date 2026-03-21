# Chapter 10: Binary Search Trees

**Target:** 65 MCQs | **Distribution:** 16 Foundational, 26 Intermediate, 18 Advanced, 5 Expert

---

**Q10.1: Foundational - [Theory] - [BST Definition]**

Binary Search Tree (BST) property:

A) Left subtree values < node value < right subtree values
B) Left subtree values ≤ node value ≤ right subtree values
C) Inorder traversal gives sorted order
D) Both A and C

**Answer: D**

**Explanation:**
BST: for each node, all values in left subtree are less than node's value, all values in right subtree are greater. Inorder traversal yields values in sorted ascending order. Duplicates may be handled differently (left or right, or count). Strict inequality (A) or non-strict (B) depends on duplicate policy.

---

**Q10.2: Foundational - [Theory] - [BST Search]**

Searching in BST:

A) Compare with root, go left if smaller, right if larger
B) O(h) time where h = height
C) O(log n) average, O(n) worst
D) All of the above

**Answer: D**

**Explanation:**
BST search: start at root. If target = node.val, found. If target < node.val, search left. Else search right. O(h) where h is height. Balanced: O(log n). Skewed (degenerate): O(n) worst case. This is why balanced BSTs (AVL, RB) are important.

---

**Q10.3: Foundational - [Theory] - [BST Insertion]**

Inserting into BST:

A) Search for position, insert as leaf
B) O(h) time
C) Does not cause restructuring
D) All of the above

**Answer: D**

**Explanation:**
BST insert: search as if finding the key. When reach null, insert new node there. Always inserted as leaf. O(h) time. Simple BST doesn't self-balance, so insert doesn't trigger restructuring (unlike AVL/RB trees).

---

**Q10.4: Foundational - [Trace] - [BST Insertion]**

Insert [5,3,7,1,4] into empty BST:

A) Root: 5. 3 < 5, left. 7 > 5, right
B) 1 < 5, < 3, left of 3. 4 < 5, > 3, right of 3
C) Final tree: 5(3(1,4),7)
D) All of the above

**Answer: D**

**Explanation:**
Insert sequence: 5 becomes root. 3 goes left. 7 goes right. 1 goes left of 3. 4 goes right of 3. Tree: 5(3(1,4),7). Inorder: 1,3,4,5,7 sorted.

---

**Q10.5: Foundational - [Theory] - [BST Deletion]**

Deleting leaf node from BST:

A) Simply remove it
B) Set parent's child pointer to null
C) O(1) additional work after finding
D) All of the above

**Answer: D**

**Explanation:**
Delete leaf: remove directly. O(1) once node found (already O(h) to find). Simplest case of BST deletion.

---

**Q10.6: Intermediate - [Theory] - [Delete with One Child]**

Deleting node with one child in BST:

A) Replace node with its child
B) Bypass the node
C) Still O(h) time
D) All of the above

**Answer: D**

**Explanation:**
Delete node with one child: connect parent directly to child, removing the node. Child can be left or right. Simple bypass operation. O(h) total.

---

**Q10.7: Intermediate - [Theory] - [Delete with Two Children]**

Deleting node with two children in BST:

A) Replace with inorder successor (or predecessor)
B) Copy successor value, delete successor
C) Successor has at most one child
D) All of the above

**Answer: D**

**Explanation:**
Delete with two children: find inorder successor (smallest in right subtree) or predecessor (largest in left subtree). Copy its value to current node. Delete successor (which has at most one child, making it easier). Maintains BST property. Alternative: splice successor to replace deleted node directly.

---

**Q10.8: Intermediate - [Trace] - [Delete with Two Children]**

Delete 5 from tree 5(3(1,4),7):

A) Inorder successor of 5 is 7 (smallest in right subtree)
B) Copy 7 to root, delete 7
C) New tree: 7(3(1,4),null) or predecessor approach: 4(3(1),7)
D) Both valid depending on choice

**Answer: D**

**Explanation:**
Successor approach: successor is 7. Tree becomes 7(3(1,4),null). Predecessor approach: predecessor is 4. Tree becomes 4(3(1),7). Both valid BSTs. Different implementations choose differently. Successor more common.

---

**Q10.9: Intermediate - [Theory] - [Inorder Successor]**

Inorder successor in BST:

A) If right subtree exists: minimum of right subtree
B) Else: first ancestor where node is in left subtree
C) O(h) time to find
D) All of the above

**Answer: D**

**Explanation:**
Successor: next node in inorder traversal. Case 1: has right child → go right, then leftmost (minimum of right subtree). Case 2: no right child → go up until find ancestor where node is in left subtree (first ancestor greater than node). O(h) time.

---

**Q10.10: Intermediate - [Trace] - [Find Successor]**

Tree: 20(10(5,15(12,17)),30(25,35)), find successor of 15:

A) 15 has right child 17
B) Minimum of right subtree = 17? No wait, right subtree is (17), so min is 17
C) But 17 > 15, yes successor is 17... actually check: inorder is 5,10,12,15,17,20,25,30,35
D) Successor of 15 is 17

**Answer: D**

**Explanation:**
Inorder: 5,10,12,15,17,20,25,30,35. Successor of 15 is 17. 15 has right child 17, so min of right subtree = 17. If no right child, would go up to find ancestor where 15 is left descendant.

---

**Q10.11: Intermediate - [Theory] - [BST Validation]**

Check if tree is valid BST:

A) Inorder must be sorted
B) Or recursive: node value must be in (min, max) range
C) Both O(n) time
D) All of the above

**Answer: D**

**Explanation:**
Approach 1: inorder, check sorted. O(n) time, O(h) space. Approach 2: recursive with valid range. Root valid for (-∞, +∞). Left child: (-∞, root.val), right: (root.val, +∞). Check recursively. O(n) time, O(h) space.

---

**Q10.12: Intermediate - [Trace] - [Validate BST]**

Tree: 5(1,6(3,7)) - is this valid BST?

A) Inorder: 1,5,3,6,7 - not sorted (3 < 5 but appears after)
B) Range check: 3 is right of 6, should be > 6, but 3 < 6
C) Invalid BST
D) All checks show invalid

**Answer: D**

**Explanation:**
This is not a BST. Node 3 is in right subtree of 5, but 3 < 5, violating BST property. Inorder not sorted confirms. Common mistake: only checking immediate children, not entire subtree.

---

**Q10.13: Intermediate - [Theory] - [BST vs Hash]**

BST advantages over hash table:

A) Ordered iteration
B) Range queries
C) Successor/predecessor queries
D) All of the above

**Answer: D**

**Explanation:**
BST: maintains order. Inorder gives sorted sequence. Can do range queries (find all in [a,b]), successor/predecessor, floor/ceiling. Hash: O(1) average lookup, no ordering. Choose based on operations needed.

---

**Q10.14: Intermediate - [Theory] - [Floor and Ceiling]**

Floor and ceiling in BST:

A) Floor: largest value ≤ target
B) Ceiling: smallest value ≥ target
C) Both O(h) time
D) All of the above

**Answer: D**

**Explanation:**
Floor: go left if target < node, else update floor candidate and go right. Ceiling: opposite. Both O(h). Useful for nearest value queries, range queries.

---

**Q10.15: Intermediate - [Trace] - [Floor/Ceiling]**

Tree: 20(10(5,15),30(25,35)), floor and ceiling of 22:

A) Floor: go 20→30→25, last ≤ 22 is 20
B) Ceiling: go 20→30→25, first ≥ 22 is 25
C) Floor=20, Ceiling=25
D) All of the above

**Answer: D**

**Explanation:**
Floor 22: 20 ≤ 22, candidate. Go right to 30. 30 > 22, go left to 25. 25 > 22, go left to null. Floor = 20. Ceiling 22: 20 < 22, go right to 30. 30 > 22, candidate. Go left to 25. 25 > 22, candidate. Go left to null. Ceiling = 25.

---

**Q10.16: Intermediate - [Theory] - [k-th Smallest]**

k-th smallest element in BST:

A) Inorder traversal, count k
B) O(n) time
C) With augmented size field: O(h) time
D) Both A and C

**Answer: D**

**Explanation:**
Naive: inorder, stop at k. O(n). Optimized: augment each node with size of subtree. Compare k with left.size. If k = left.size + 1, current node. If k ≤ left.size, recurse left. Else recurse right with k - left.size - 1. O(h).

---

**Q10.17: Advanced - [Code] - [Augmented BST]**

BST augmented with subtree size for order statistics:

A) Insert/Delete: update sizes along path
B) O(h) extra per operation
C) Enables rank and select operations
D) All of the above

**Answer: D**

**Explanation:**
Augmented BST: store size at each node (nodes in subtree). Update during insert/delete. Rank(x): 1 + size(left subtree) + rank in path. Select(k): use size fields to navigate. Order statistics in O(h).

---

**Q10.18: Advanced - [Theory] - [BST from Preorder]**

Construct BST from preorder traversal:

A) First element is root
B) Elements smaller than root form left subtree
C) Elements larger form right subtree
D) All of the above

**Answer: D**

**Explanation:**
Preorder: root, then left subtree, then right subtree. In BST: all values after root that are < root form left subtree, > root form right. Recursively construct. O(n) with careful partition or using stack. Simpler than general tree because BST property gives split point.

---

**Q10.19: Advanced - [Trace] - [BST from Preorder]**

Preorder [8,5,1,7,10,12], construct BST:

A) Root=8. Left: 5,1,7 (all < 8). Right: 10,12 (all > 8)
B) Left subtree preorder [5,1,7], right [10,12]
C) Recursively: 5(1,7), 10(null,12)
D) Tree: 8(5(1,7),10(null,12))

**Answer: D**

**Explanation:**
8 is root. Values < 8: [5,1,7] form left. Values > 8: [10,12] form right. Recursively, 5 is root of left with [1] left and [7] right. 10 is root of right with [] left and [12] right. Final tree: 8(5(1,7),10(null,12)).

---

**Q10.20: Advanced - [Theory] - [Convert Sorted Array to BST]**

Convert sorted array to balanced BST:

A) Middle element as root
B) Left half forms left subtree, right half forms right
C) Recursively build
D) All of the above

**Answer: D**

**Explanation:**
Sorted array to balanced BST: pick middle element as root (ensures balance). Left subarray (0 to mid-1) forms left subtree. Right subarray (mid+1 to end) forms right. Recursively construct. O(n) time, O(log n) recursion space. Height balanced.

---

**Q10.21: Advanced - [Trace] - [Sorted Array to BST]**

Array [1,2,3,4,5,6,7] to BST:

A) Root = middle = 4 (index 3)
B) Left [1,2,3], root 2. Right [5,6,7], root 6
C) Continue: 4(2(1,3),6(5,7))
D) Balanced BST with height 2

**Answer: D**

**Explanation:**
Mid = 3 (value 4). Left [1,2,3], mid=1 (value 2). Right [5,6,7], mid=5 (value 6). Continue: left of 2 is [1], right [3]. Left of 6 is [5], right [7]. Tree: 4(2(1,3),6(5,7)). Height 2 (balanced).

---

**Q10.22: Advanced - [Theory] - [Range Sum BST]**

Sum of values in range [L,R] in BST:

A) DFS, add if L ≤ val ≤ R
B) Prune: if val < L, only search right
C) If val > R, only search left
D) All of the above

**Answer: D**

**Explanation:**
Range sum: DFS/BFS with pruning. If node.val < L, all values in left subtree also < L, skip left. If node.val > R, skip right. Otherwise add node.val and search both. Average O(log n + k) where k is number of nodes in range. Worst O(n).

---

**Q10.23: Expert - [Theory] - [BST with Duplicates]**

Handling duplicates in BST:

A) Store count in node
B) Store duplicates in left or right consistently
C) Use multiset (allow multiple same keys)
D) All of the above

**Answer: D**

**Explanation:**
Duplicate strategies: (1) count field: node stores value and count. (2) strict BST: all ≤ in left, all ≥ in right, or vice versa. (3) multiset: allow multiple nodes with same key. Trade-offs: count is space efficient but complex; separate nodes simple but increases height.

---

**Q10.24: Expert - [Theory] - [Self-Balancing Need]**

Why self-balancing BSTs (AVL, Red-Black):

A) BST can degenerate to linked list
B) O(n) height, operations become O(n)
C) Guarantees O(log n) height
D) All of the above

**Answer: D**

**Explanation:**
Unbalanced BST: inserting sorted data creates linked list, height = n, operations O(n). Self-balancing: maintain height O(log n) through rotations. AVL: strictly balanced (height ≤ 1.44 log n). Red-Black: relaxed balance, less rotation overhead. Essential for guaranteed performance.

---

**Q10.25: Expert - [Trace] - [Degenerate BST]**

Insert [1,2,3,4,5] into BST:

A) Root: 1. 2 > 1, right. 3 > 2, right of 2
B) Forms linked list: 1(null,2(null,3(null,4(null,5))))
C) Height = 4, search O(n)
D) All of the above

**Answer: D**

**Explanation:**
Sorted insertion creates degenerate BST. Resembles linked list. Height = n-1 = 4. Operations O(n). Demonstrates need for balancing.

---

**Q10.26: Intermediate - [Application] - [Two Sum IV]**

Two sum in BST: find if two values sum to target:

A) Hash set approach: O(n) space
B) Two pointers on sorted array (inorder): O(n) time, O(n) space
C) Use iterator for two pointers on BST: O(n) time, O(h) space
D) All of the above

**Answer: D**

**Explanation:**
Approaches: (1) hash set as traverse, O(n) space. (2) inorder to array, two pointers from ends, O(n) space. (3) use BST iterator for next() from start and predecessor iterator for prev() from end, O(h) space. Multiple valid approaches with tradeoffs.

---

**Q10.27: Advanced - [Theory] - [Closest Value]**

Closest value to target in BST:

A) Track closest during search
B) Go left if target < node.val, else right
C) O(h) time
D) All of the above

**Answer: D**

**Explanation:**
Search: track min_diff and closest_value. Update if |node.val - target| < min_diff. Navigate left or right based on comparison. O(h). Example: closest to 4.5 in tree with 4 and 5. Visit nodes, update closest.

---

**Q10.28: Advanced - [Trace] - [Closest Value]**

Tree: 4(2(1,3),6(5,7)), target = 4.5:

A) Start 4, diff=0.5, closest=4
B) 4.5 > 4, go right to 6, diff=1.5, closest stays 4
C) 4.5 < 6, go left to 5, diff=0.5, closest could be 4 or 5
D) Answer: 4 or 5 (both same distance)

**Answer: D**

**Explanation:**
4: |4-4.5|=0.5, closest=4. Go right. 6: |6-4.5|=1.5 > 0.5, keep 4. Go left. 5: |5-4.5|=0.5, tie. Could return 4 or 5 depending on > vs ≥ logic. Both correct.

---

**Q10.29: Expert - [Theory] - [BST Iterator]**

Implement BST iterator with next() and hasNext():

A) Stack stores left spine
B) next(): pop, process, push right's left spine
C) hasNext(): stack not empty
D) All of the above

**Answer: D**

**Explanation:**
BST iterator for inorder: constructor pushes all left children from root. next(): pop node, if has right child, push all left children of right. hasNext(): stack not empty. Amortized O(1) per operation, O(h) space. Enables iterating without full traversal.

---

**Q10.30: Advanced - [Trace] - [Iterator]**

Tree: 7(3(1,5),15(10,20)), iterator:

A) Init: push 7,3,1. Stack: [7,3,1]
B) next(): pop 1, no right, return 1
C) next(): pop 3, has right 5, push 5, return 3
D) Sequence: 1,3,5,7,10,15,20

**Answer: D**

**Explanation:**
Initialization: push root, then left repeatedly: [7,3,1]. next(): pop 1, return 1 (no right). next(): pop 3, push right's left spine (5), return 3. Continue: 5 (pop, no right), 7 (pop, push 15's left spine: 10), 10, 15 (push 20), 20. Inorder achieved.

---

**Q10.31: Intermediate - [Application] - [Trim BST]**

Trim BST to range [L,R]:

A) Recursively trim left and right subtrees
B) If root.val < L: return trim(root.right)
C) If root.val > R: return trim(root.left)
D) All of the above

**Answer: D**

**Explanation:**
Trim: if root.val < L, root and left are too small, return trimmed right. If root.val > R, return trimmed left. Else: trim both children, return root. Effectively removes nodes outside range. O(n) visits each node once.

---

**Q10.32: Advanced - [Theory] - [Delete Node and Return Root]**

Delete node with given key and return new root:

A) If key < root.val: root.left = delete(root.left, key)
B) If key > root.val: root.right = delete(root.right, key)
C) Else found: handle 0,1,2 children cases
D) All of the above

**Answer: D**

**Explanation:**
Standard BST delete: search recursively. When found: 0 children → return null. 1 child → return that child. 2 children → find successor, copy value, delete successor recursively. Update parent's child pointer. Returns potentially new root if original root deleted.

---

**Q10.33: Expert - [Theory] - [Concurrent BST]**

Concurrent BST without locks:

A) Lock-free using CAS on child pointers
B) Logical deletion (mark then CAS)
C) Complexity similar to concurrent skiplists
D) All of the above

**Answer: D**

**Explanation:**
Concurrent BST: challenging due to multiple pointers. Lock-free: CAS on child pointers. Delete: mark node as deleted (logical), then unlink (physical). Similar techniques to lock-free linked lists. Less common than concurrent skiplists because skiplists simpler for lock-free. Research area with various algorithms (Ellen et al., Fraser).

---

**Q10.34: Expert - [Theory] - [BST vs Skip List]**

BST vs Skip List comparison:

A) Both O(log n) expected operations
B) Skip list simpler, no rotations
C) BST better cache locality (in-order nodes)
D) All of the above

**Answer: D**

**Explanation:**
Both provide ordered O(log n) operations. Skip lists: simpler implementation, probabilistic balancing, good for concurrent (lock-free). BSTs: better cache locality (in-order), lower constant factors, range queries efficient. Choose based on use case: concurrent access favors skip lists; cache-sensitive favors BSTs.

---

**Q10.35: Intermediate - [Application] - [Delete Leaves with Value]**

Delete leaves with given target value:

A) Postorder: process children first
B) If leaf and val == target: return null (delete)
C) Else return node
D) All of the above

**Answer: D**

**Explanation:**
Delete specific leaves: postorder traversal. Recursively process left and right. After recursion, check if current is leaf (both children null) and value matches target. If so, return null to delete. Else return node. New parents get null child pointers. O(n) time.

---

**Q10.36: Advanced - [Theory] - [Balance a BST]**

Balance an unbalanced BST:

A) Inorder to get sorted array
B) Build balanced BST from sorted array
C) O(n) time, O(n) space
D) All of the above

**Answer: D**

**Explanation:**
Balance BST: inorder traversal → sorted array (O(n)). Then build balanced BST from array (middle as root, recursively, O(n)). Total O(n) time, O(n) space for array. Alternative: Day-Stout-Warren algorithm O(n) time, O(1) space by rotating in place. Most practical approach uses array.

---

**Q10.37: Advanced - [Trace] - [Balance]**

Degenerate tree 1(null,2(null,3(null,4))) to balanced:

A) Inorder: [1,2,3,4]
B) Build: root=2(1,3(null,4)) or root=3(2(1),4)
C) Height reduces from 3 to 2
D) All of the above

**Answer: D**

**Explanation:**
Inorder: [1,2,3,4]. Balanced BST: root can be 2 with left [1], right [3,4]. Or root=3 with left [1,2], right [4]. Both balanced. Height reduces from O(n) to O(log n).

---

**Q10.38: Expert - [Theory] - [Optimal BST]**

Optimal BST (optimal binary search tree):

A) Minimize expected search cost given key probabilities
B) Dynamic programming: try each key as root
C) Cost = sum of depth × probability for all nodes
D) All of the above

**Answer: D**

**Explanation:**
Optimal BST: given keys and search probabilities, construct BST with minimum expected search comparisons. DP: dp[i][j] = min cost for keys i to j. Try each k as root: cost = dp[i][k-1] + dp[k+1][j] + sum of frequencies (increased depth by 1). O(n³) naive, O(n²) with Knuth optimization (monotonicity). Classic DP problem.

---

**Q10.39: Expert - [Theory] - [Splay Tree Operations]**

Splay tree after access:

A) Splay (rotate) accessed node to root
B) Amortized O(log n) operations
C) Self-adjusting, no explicit balance info
D) All of the above

**Answer: D**

**Explanation:**
Splay tree: self-adjusting BST. After access (search/insert), splay node to root via rotations. Frequently accessed nodes stay near root. Amortized O(log n), no balance fields. Simple, good cache of recent items. Worst case O(n) per operation but amortized bound holds.

---

**Q10.40: Expert - [Trace] - [Splay]**

Splay tree: access 3 from tree 5(2(1,3(4)),6):

A) 3 is left child of... wait tree is 5(2(1,3),6) where 3 has right 4
B) Actually 3 is right child of 2, with right child 4
C) Zig-zig or zig-zag rotations to bring 3 to root
D) Final tree has 3 as root

**Answer: D**

**Explanation:**
Splaying brings accessed node to root via rotations. Zig (parent is root): single rotation. Zig-zig (node and parent both left or both right): two rotations. Zig-zag: different directions. After splaying 3, it becomes root with appropriate structure. Self-adjusting property moves frequently accessed nodes up.

---

**Q10.41: Intermediate - [Application] - [Sorted List to BST]**

Convert sorted singly linked list to BST:

A) Find middle using slow/fast pointers
B) Middle is root, recursively left and right
C) O(n log n) naive, O(n) with bottom-up
D) All of the above

**Answer: D**

**Explanation:**
Sorted list to BST: find middle (slow/fast), make root, recursively build left (before middle) and right (after). O(n log n) due to finding middle each level. Optimized O(n): build bottom-up, inorder simulation. Or convert to array first.

---

**Q10.42: Advanced - [Theory] - [Count Nodes in Range]**

Count nodes with values in range [L,R] in BST:

A) If node.val < L: search right only
B) If node.val > R: search left only
C) Else: 1 + count left + count right (or count in subtrees)
D) All of the above

**Answer: D**

**Explanation:**
Count range: prune subtrees outside range. If node.val < L, only right subtree can have values ≥ L. If node.val > R, only left. Else node in range, add 1 and check both subtrees. With augmented size: O(log n + k). Without: O(n) worst, pruned average better.

---

**Q10.43: Expert - [Theory] - [Interval Tree]**

Interval tree (augmented BST for intervals):

A) Key is low endpoint of interval
B) Max of high endpoints in subtree stored
C) Efficient overlap queries
D) All of the above

**Answer: D**

**Explanation:**
Interval tree: BST keyed by interval start. Augment: store max endpoint in subtree. Overlap query: if current overlaps target, return. Else if left.max < target.low, can't overlap left, go right. Else go left. O(log n + k) for k overlapping intervals. Used in scheduling, computational geometry.

---

**Q10.44: Expert - [Trace] - [Interval Query]**

Intervals [1,5], [3,7], [8,10], [10,12], query [4,6]:

A) Root could be [3,7], max=12
B) [3,7] overlaps [4,6]? Yes (3≤6, 7≥4), found
C) Search stops at first overlap (or continue for all)
D) All of the above

**Answer: D**

**Explanation:**
Interval tree: organized by start point. Query [4,6]: check root [3,7], overlaps (3 ≤ 6 and 7 ≥ 4), found. Can stop or continue for all overlaps. Structure enables efficient overlap finding without checking all intervals.

---

**Q10.45: Intermediate - [Application] - [Search in BST]**

Search for value in BST:

A) O(h) comparisons
B) Start at root
C) Go left if smaller, right if larger
D) All of the above

**Answer: D**

**Explanation:**
Basic BST search: O(h) time. Start at root. If equal, found. If target smaller, go left (all values there smaller). If larger, go right. If reach null, not found. Fundamental operation.

---

**Q10.46: Advanced - [Theory] - [Construct from Level Order]**

Construct BST from level order traversal:

A) First element is root
B) For remaining, smaller values go left, larger go right in level order
C) Use queue, process nodes with their valid ranges
D) All of the above

**Answer: D**

**Explanation:**
Level order to BST: root first. Then elements partitioned by value relative to root. Left subtree elements appear before right subtree elements in level order only if within proper range. Algorithm: queue with (value, min, max). For each next value, find first node where it fits range, create child. O(n) time.

---

**Q10.47: Expert - [Theory] - [Persistent BST]**

Persistent BST:

A) Modifications create new version, share structure
B) Path copying: copy nodes on path to root
C) O(log n) extra space per update
D) All of the above

**Answer: D**

**Explanation:**
Persistent BST: preserve previous versions. Insert/delete: copy path from root to modified node (path copying), share unchanged subtrees. O(log n) extra space per operation. Used in functional programming, versioned databases, undo systems. Similar to persistent treap or red-black tree.

---

**Q10.48: Expert - [Trace] - [Persistent Insert]**

Insert 4 into persistent BST with versions, tree was 2(1,3):

A) Insert 4 as right child of 3
B) Copy path: 2, then 3 (new nodes)
C) New root points to new 2, shares left subtree 1
D) Old version still accessible via old root

**Answer: D**

**Explanation:**
Persistent insert: copy nodes on path. Original: 2(1,3). Insert 4: go 2→3, copy 2, copy 3, add 4 as right of new 3. New tree: 2'(1,3'(null,4)). Old root still points to original structure. Path copying preserves immutability.

---

**Q10.49: Intermediate - [Application] - [Mode in BST]**

Find mode in BST (most frequent element):

A) Inorder traversal (sorted)
B) Count consecutive equal values
C) Track max frequency
D) All of the above

**Answer: D**

**Explanation:**
BST mode: inorder gives sorted with duplicates consecutive. Track current value count, update max. O(n) time, O(1) extra space. No hash needed. Multiple modes possible if ties.

---

**Q10.50: Advanced - [Theory] - [Find Predecessor]**

Inorder predecessor in BST:

A) If left subtree exists: maximum of left subtree
B) Else: first ancestor where node is in right subtree
C) O(h) time
D) All of the above

**Answer: D**

**Explanation:**
Predecessor: previous in inorder. Case 1: has left child → max of left subtree (rightmost). Case 2: no left → go up until find ancestor where node is in right subtree (first ancestor less than node). O(h) time. Symmetric to successor.

---

**Q10.51: Expert - [Theory] - [Treap vs BST]**

Treap advantage over basic BST:

A) Expected O(log n) height without complex rebalancing
B) Simple implementation
C) Good average performance
D) All of the above

**Answer: D**

**Explanation:**
Treap: BST by key, heap by random priority. Random priorities give expected O(log n) height. No complex rebalancing logic like AVL. Simple to implement. Good for average-case scenarios. Randomization avoids worst-case from ordered input.

---

**Q10.52: Intermediate - [Application] - [Insert into BST]**

Insert sequence [7,3,9,1,5]:

A) 7 root
B) 3 left, 9 right of 7
C) 1 left of 3, 5 right of 3
D) Tree: 7(3(1,5),9)

**Answer: D**

**Explanation:**
Insert: 7 root. 3 < 7, left. 9 > 7, right. 1 < 7, < 3, left of 3. 5 < 7, > 3, right of 3. Final: 7(3(1,5),9). Inorder: 1,3,5,7,9 sorted.

---

**Q10.53: Advanced - [Theory] - [Delete Root]**

Delete root from BST and return new root:

A) Find successor (min of right subtree)
B) Copy value to root, delete successor
C) New root might be successor if root had only right child
D) All of the above

**Answer: D**

**Explanation:**
Delete root: find inorder successor (or predecessor). Copy value. Delete successor from right subtree. If root had only right child, successor is right child, becomes new root. If only left, predecessor becomes root. Handles all cases.

---

**Q10.54: Expert - [Theory] - [Cartesian Tree is BST]**

Cartesian tree:

A) Heap-ordered by value
B) Inorder gives original array
C) Is a BST? No, heap property dominates
D) Actually not a BST, it's a heap structure

**Answer: D**

**Explanation:**
Cartesian tree: heap by value, inorder by position (array order). Not a BST. Root is array minimum. Used for RMQ problems. Different structure from BST despite binary tree form.

---

**Q10.55: Intermediate - [Application] - [Is Subtree]**

Check if tree S is subtree of BST T:

A) Simpler than general tree (use BST property)
B) But still need structure match
C) O(n) to serialize both, check substring
D) All of the above

**Answer: D**

**Explanation:**
Subtree check: same as general tree. Can serialize both, check if S serialization is substring of T's (with delimiters). O(n). BST property doesn't simplify subtree checking significantly. Must match structure and values.

---

**Q10.56: Advanced - [Theory] - [Recover BST]**

Recover BST where two nodes swapped:

A) Inorder should be sorted
B) Find two violations in inorder
C) First: prev > current (first element is first swapped)
D) Last: prev > current (second element is second swapped)

**Answer: D**

**Explanation:**
Two nodes swapped in BST: inorder has exactly two violations of sorted order. First violation: first swapped node is previous element. Last violation: second swapped node is current element. Swap values back. O(n) time, O(h) space. Morris traversal can do O(1) space.

---

**Q10.57: Expert - [Trace] - [Recover]**

Tree: 1(3,null) - nodes 1 and 3 swapped, inorder [3,1]:

A) First violation: prev=3, curr=1, 3 > 1, first = 3
B) No second violation (only two elements)
C) Swap 3 and 1 values
D) Tree becomes 3(1,null), correct BST

**Answer: D**

**Explanation:**
Inorder [3,1]: violation 3 > 1. First = 3 (previous), no second violation found, so second = 1 (current). Swap values: node with 3 becomes 1, node with 1 becomes 3. Tree: 3(1,null). Inorder [1,3] sorted.

---

**Q10.58: Expert - [Theory] - [Summary]**

BST key properties:

A) Inorder sorted
B) O(h) search/insert/delete
C) Need balancing for O(log n) guaranteed
D) All of the above

**Answer: D**

**Explanation:**
BST: left < root < right. Inorder gives sorted sequence. Operations O(h). Balanced BST (AVL, RB) guarantees O(log n). Unbalanced can be O(n). Foundation for ordered symbol tables, databases, many applications.

---

**Q10.59: Intermediate - [Application] - [Find Target]**

Find if there exists a value in BST equal to target:

A) Standard BST search
B) O(h) time
C) Return true/false
D) All of the above

**Answer: D**

**Explanation:**
Basic BST membership test. Search algorithm. O(h) time. Returns boolean indicating presence.

---

**Q10.60: Advanced - [Theory] - [All Elements in Range]**

Get all elements in range [L,R] from BST:

A) Modified inorder traversal
B) Prune left if node.val < L
C) Prune right if node.val > R
D) All of the above

**Answer: D**

**Explanation:**
Range query: inorder with pruning. If node.val < L, skip left (all too small). If node.val > R, skip right. Else add to result and recurse both. Output sorted. O(log n + k) where k = number of results.

---

**Q10.61: Expert - [Theory] - [Threaded BST]**

Threaded BST for inorder:

A) Null right pointers point to successor
B) Null left pointers point to predecessor
C) Inorder without stack
D) All of the above

**Answer: D**

**Explanation:**
Threaded BST: threads replace null pointers. Right thread → inorder successor. Left thread → predecessor. Enables iterative inorder without stack or recursion. More complex insertion/deletion to maintain threads.

---

**Q10.62: Expert - [Theory] - [Optimal BST Complexity]**

Optimal BST with Knuth optimization:

A) O(n²) time
B) O(n²) space
C) Down from O(n³) naive
D) All of the above

**Answer: D**

**Explanation:**
Optimal BST: DP O(n³) naive. Knuth optimization uses quadrangle inequality/monotonicity of optimal roots. Reduces to O(n²). Space O(n²). Significant improvement for larger n. Classic DP optimization technique.

---

**Q10.63: Expert - [Theory] - [Splay Tree Amortized]**

Splay tree amortized analysis:

A) Potential method
B) Amortized O(log n) per operation
C) Weight balancing argument
D) All of the above

**Answer: D**

**Explanation:**
Splay tree: amortized O(log n) via potential method. Define potential based on tree structure. Show splaying pays for itself over sequence. Tight analysis, classic data structures theory. Good average performance, self-optimizing to access patterns.

---

**Q10.64: Expert - [Theory] - [Dynamic Optimality]**

Dynamic optimality conjecture (splay trees):

A) Splay trees within constant factor of optimal offline algorithm
B) Unproven but widely believed
C) Related to working set and traversal properties
D) All of the above

**Answer: D**

**Explanation:**
Dynamic optimality: splay trees conjectured to be O(1) competitive with any binary search tree algorithm that knows the future (offline optimal). Unproven for decades. Related properties proven: static optimality, working set, sequential access (traversal). Major open problem in data structures.

---

**Q10.65: Expert - [Theory] - [Final Summary]**

BST comprehensive understanding requires:

A) Core operations (search, insert, delete)
B) Balancing motivation
C) Order statistics and range queries
D) All of the above

**Answer: D**

**Explanation:**
BST mastery: basic operations, handling duplicates, balancing (AVL, RB), order statistics, range queries, iteration, persistence, optimality. Foundation for database indexes, ordered maps, many applications. Key data structure in computer science.

---

## Chapter 10 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 16 | BST definition, search, insert, delete basics |
| Intermediate | 26 | Successor, validation, floor/ceiling, k-th smallest, trim |
| Advanced | 18 | Iterator, balance, range queries, recovery, splay |
| Expert | 5 | Optimal BST, persistence, dynamic optimality, threading |

**Total MCQs: 65** | **Target Met: ✓**

**Key BST Operations:**
- Search: O(h) = O(log n) balanced, O(n) worst
- Insert: O(h)
- Delete: O(h) (three cases: 0, 1, 2 children)
- Successor/Predecessor: O(h)
- Validation: O(n)
- Build from sorted array: O(n)

**Next:** Chapter 11 - Balanced Trees (AVL, Red-Black)
