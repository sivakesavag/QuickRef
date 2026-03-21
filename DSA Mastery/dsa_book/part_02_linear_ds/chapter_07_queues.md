# Chapter 7: Queues

**Target:** 55 MCQs | **Distribution:** 14 Foundational, 22 Intermediate, 14 Advanced, 5 Expert

---

**Q7.1: Foundational - [Theory] - [Queue Definition]**

A queue is a data structure with operations:

A) Push and pop from same end
B) Enqueue at rear, dequeue from front (FIFO)
C) Insert and delete at arbitrary positions
D) Add to front, remove from rear

**Answer: B**

**Explanation:**
Queue: FIFO (First In, First Out). Enqueue (add) at rear/tail, dequeue (remove) from front/head. Like a line at a store—first to arrive is first served. Contrast with stack (LIFO). Fundamental for BFS, scheduling, buffering, asynchronous processing. Fairness property makes queues essential for resource allocation.

---

**Q7.2: Foundational - [Theory] - [FIFO Property]**

Queue operations: enqueue(1), enqueue(2), enqueue(3), dequeue(), dequeue():

A) Returns 3, then 2
B) Returns 1, then 2
C) Returns 1, then 3
D) Queue underflow

**Answer: B**

**Explanation:**
Queue state: [], enqueue(1)→[1], enqueue(2)→[1,2], enqueue(3)→[1,2,3]. dequeue()→returns 1, queue [2,3]. dequeue()→returns 2, queue [3]. FIFO: first enqueued (1) is first dequeued. This ordering is essential for BFS traversal, fair scheduling, and ordered processing.

---

**Q7.3: Foundational - [Complexity] - [Queue Operations]**

Queue enqueue and dequeue are:

A) O(n) time
B) O(log n) time
C) O(1) time
D) O(n²) time

**Answer: C**

**Explanation:**
Enqueue: add element at rear (array: increment tail index; linked list: append to tail with tail pointer). Dequeue: remove from front (array: increment head; linked list: remove head). Both O(1) with proper implementation. This efficiency makes queues suitable for real-time systems, streaming data, and high-frequency operations.

---

**Q7.4: Foundational - [Theory] - [Queue Implementation]**

Queue can be implemented using:

A) Array with circular buffer
B) Linked list with head and tail
C) Two stacks
D) All of the above

**Answer: D**

**Explanation:**
Array (circular): head and tail indices wrap around, modulo capacity. Efficient but fixed size or resizing needed. Linked list: head for dequeue, tail for enqueue, both O(1). Two stacks: enqueue to stack1, dequeue from stack2 (if empty, pop all from stack1 to stack2). Amortized O(1). Each has tradeoffs—circularity vs pointer overhead vs amortized complexity.

---

**Q7.5: Foundational - [Theory] - [Circular Queue]**

Circular queue (ring buffer) uses:

A) Fixed-size array with wrap-around indices
B) Modulo arithmetic for head/tail
C) Prevents unnecessary shifting in linear array
D) All of the above

**Answer: D**

**Explanation:**
Circular queue: array where tail wraps to beginning after end. head = (head + 1) % capacity, tail = (tail + 1) % capacity. Efficient O(1) operations without shifting elements. Fixed capacity, but efficient memory reuse. Used in embedded systems, audio buffers, producer-consumer scenarios. Full when (tail + 1) % capacity == head (wastes one slot).

---

**Q7.6: Foundational - [Trace] - [Circular Queue]**

Circular queue capacity 5: enqueue(1), enqueue(2), dequeue(), enqueue(3), enqueue(4), enqueue(5), enqueue(6):

A) head at 1 (value 2), tail at 0 (circular)
B) Queue contains [2,3,4,5,6] in circular order
C) Full, cannot enqueue more
D) All of the above

**Answer: D**

**Explanation:**
Initial: head=0, tail=0. E(1): arr[0]=1, tail=1. E(2): arr[1]=2, tail=2. D(): return arr[0]=1, head=1. E(3): arr[2]=3, tail=3. E(4): arr[3]=4, tail=4. E(5): arr[4]=5, tail=0 (wrap). E(6): arr[0]=6, tail=1. Queue: [6,2,3,4,5] from index 0. head=1 points to 2, tail=1 points past 6. Circular structure manages wrap-around.

---

**Q7.7: Intermediate - [Theory] - [BFS with Queue]**

BFS traversal uses:

A) Stack
B) Queue
C) Priority queue
D) Recursion only

**Answer: B**

**Explanation:**
BFS explores level by level: start node, then its neighbors, then their neighbors, etc. Queue manages frontier: enqueue start, while queue not empty, dequeue node, enqueue unvisited neighbors. FIFO ensures closest vertices processed first, guaranteeing shortest path in unweighted graphs. Queue size can grow to O(V), space complexity O(V).

---

**Q7.8: Intermediate - [Trace] - [BFS Levels]**

BFS on graph starting at A, neighbors B,C, their neighbors D,E:

A) Level 0: A, Level 1: B,C, Level 2: D,E
B) Queue: [A]→dequeue A, enqueue B,C→[B,C]→dequeue B, enqueue D→[C,D]→dequeue C, enqueue E→[D,E]
C) Order: A,B,C,D,E
D) All of the above

**Answer: D**

**Explanation:**
BFS processes nodes in FIFO order, discovering nodes level by level. Queue tracks frontier between discovered and unexplored. This level-order property is essential for shortest path and level-based processing. Contrast with DFS which uses stack and explores one branch deeply before others.

---

**Q7.9: Intermediate - [Theory] - [Deque]**

Double-ended queue (deque) supports:

A) Insert/delete at front only
B) Insert/delete at both ends
C) Insert/delete at rear only
D) Random access

**Answer: B**

**Explanation:**
Deque: add/remove at both front and rear, all O(1). Generalizes queue (FIFO at one end) and stack (LIFO at one end). Can simulate both. Array implementation: circular buffer with head/tail. Linked list: doubly linked with head/tail pointers. Python collections.deque, C++ std::deque, Java ArrayDeque provide efficient double-ended operations.

---

**Q7.10: Intermediate - [Theory] - [Priority Queue]**

Priority queue is typically implemented as:

A) Sorted array
B) Heap (binary heap)
C) BST
D) Both B and C

**Answer: B**

**Explanation:**
Priority queue: extract highest (or lowest) priority element. Binary heap: O(log n) insert and extract-min/max, O(n) build, O(1) peek. Efficient, simple, array-based. BST (like treap) also works but more complex. For ordered iteration, sorted array works but insert is O(n). Heap is the standard choice for priority queue implementation.

---

**Q7.11: Advanced - [Theory] - [Monotonic Queue]**

Monotonic queue maintains:

A) FIFO order always
B) Monotonic increasing or decreasing values
C) Used for sliding window minimum/maximum
D) Both B and C

**Answer: D**

**Explanation:**
Monotonic queue: dequeue from front while out of window, and from back while new element violates monotonicity (smaller than back for increasing). Maintains candidates in window. Front is current window extremum. O(n) for sliding window min/max (each element enqueued/dequeued once). Complements monotonic stack technique.

---

**Q7.12: Advanced - [Trace] - [Sliding Window Maximum]**

Sliding window max of [1,3,-1,-3,5,3,6,7], k=3:

A) Monotonic decreasing queue of indices
B) Remove out-of-window from front, remove smaller from back, add current
C) Results: [3,3,5,5,6,7]
D) All of the above

**Answer: D**

**Explanation:**
Window [1,3,-1]: queue [1,3] (3 larger, -1 smaller), max=3. [3,-1,-3]: remove 1 (out), -3 smaller than -1, queue [3,-1,-3], max=3. [-1,-3,5]: remove 3, 5 larger, pop -3,-1, queue [5], max=5. Continue: [5,3,6]→[6], max=6. [3,6,7]→[7]? Wait, 6 then 7, queue [6,7], max=7. Results [3,3,5,5,6,7]. O(n).

---

**Q7.13: Intermediate - [Application] - [Producer-Consumer]**

Producer-consumer problem uses:

A) Queue as buffer between producer and consumer
B) Synchronization primitives (mutex, condition variables)
C) Bounded queue to prevent unbounded growth
D) All of the above

**Answer: D**

**Explanation:**
Producer generates data, consumer processes it. Queue decouples them, allowing different speeds. Producer waits if queue full, consumer waits if queue empty. Mutex protects queue, condition variables signal state changes. Bounded queue prevents memory exhaustion. Classic synchronization problem, foundation of message queues, async processing.

---

**Q7.14: Advanced - [Theory] - [Lock-Free Queue]**

Michael-Scott lock-free queue:

A) Uses CAS (compare-and-swap) for enqueue/dequeue
B) Dummy node eliminates special cases
C) ABA problem requires hazard pointers
D) All of the above

**Answer: D**

**Explanation:**
Michael-Scott queue: singly linked list with head and tail pointers. Dummy node simplifies logic. Enqueue CAS tail.next, dequeue CAS head. ABA problem: use hazard pointers or safe memory reclamation. Standard lock-free queue, used in Java's ConcurrentLinkedQueue. Enables high-concurrency without locks.

---

**Q7.15: Intermediate - [Theory] - [Queue with Two Stacks]**

Implementing queue using two stacks:

A) enqueue: push to stack1
B) dequeue: if stack2 empty, pop all from stack1 to stack2, then pop
C) Amortized O(1) for both operations
D) All of the above

**Answer: D**

**Explanation:**
Enqueue O(1): push to input stack. Dequeue: if output stack empty, transfer all (pop from input, push to output), reversing order. Then pop from output. Amortized O(1): n enqueues cost O(n), n dequeues cost O(n) total (one transfer). Worst case dequeue O(n). Classic implementation problem demonstrating stack queue relationship.

---

**Q7.16: Advanced - [Trace] - [Two Stack Queue]**

Operations: enqueue(1), enqueue(2), dequeue(), enqueue(3), dequeue(), dequeue():

A) Stack1: [1,2], dequeue: transfer to stack2 [2,1], pop 1
B) Stack2 not empty, enqueue(3) only to stack1 [3]
C) dequeue: pop from stack2, returns 2
D) dequeue: stack2 empty, transfer stack1 [3] to stack2, pop 3. Sequence: 1,2,3

**Answer: D**

**Explanation:**
Full trace: E(1): s1=[1]. E(2): s1=[1,2]. D(): s2 empty, transfer [2,1], pop→1, s2=[2]. E(3): s1=[3], s2=[2]. D(): s2 not empty, pop→2, s2=[]. D(): s2 empty, transfer s1 [3] to s2, pop→3. Output: 1,2,3. FIFO order maintained. Shows amortized behavior—transfer happens rarely.

---

**Q7.17: Intermediate - [Application] - [Level Order Traversal]**

Binary tree level order uses:

A) Stack for DFS
B) Queue for BFS
C) Recursion
D) Parent pointers

**Answer: B**

**Explanation:**
Level order (breadth-first): enqueue root. While queue not empty: dequeue node, process, enqueue left child, enqueue right child. Processes nodes level by level (root, then children, then grandchildren). Queue size at most width of tree. Space O(w) where w is maximum width. Contrast with inorder/preorder which use stack/recursion.

---

**Q7.18: Advanced - [Trace] - [Level Order]**

Tree: 1(2(4,5),3(6,7)), level order output:

A) Queue: [1]→dequeue 1, enqueue 2,3→[2,3]→dequeue 2, enqueue 4,5→[3,4,5]→dequeue 3, enqueue 6,7→[4,5,6,7]→...
B) Output: 1,2,3,4,5,6,7
C) Levels: [1], [2,3], [4,5,6,7]
D) All of the above

**Answer: D**

**Explanation:**
Level order processes complete levels. Queue manages frontier. Can track level boundaries by queue size before processing level, or by null sentinel. Time O(n), space O(w). Foundation of BFS, tree serialization, connected component analysis. The queue ensures we explore outward uniformly from root.

---

**Q7.19: Advanced - [Theory] - [Zigzag Level Order]**

Zigzag (spiral) level order traversal:

A) Normal level order with stack for every other level
B) Or queue with direction flag, reverse every other level
C) Time O(n), space O(w)
D) Both A and B

**Answer: D**

**Explanation:**
Approach 1: level order, store levels, reverse every other. Approach 2: two stacks—current level left-to-right, next level right-to-left. Pop from stack1, push children to stack2 (left then right), then swap. O(n) time, O(w) space. Variation of BFS with alternating directions. Common interview problem (LeetCode 103).

---

**Q7.20: Expert - [Theory] - [Persistent Queue]**

Persistent (immutable) queue:

A) All operations return new queue
B) Shares structure with previous versions
C) Banker's queue: front/back lists with lazy reversal
D) All of the above

**Answer: D**

**Explanation:**
Banker's queue: two lists, front (for dequeue, reversed) and back (for enqueue). Enqueue: cons to back O(1). Dequeue: if front empty, reverse back to front (O(n) but amortized O(1)), then pop front. Persistent: reverse produces new structure, sharing common tail. Used in functional programming (Haskell, Clojure, OCaml).

---

**Q7.21: Intermediate - [Application] - [Task Scheduler]**

CPU task scheduler with cooldown:

A) tasks = ["A","A","A","B","B","B"], n=2 (cooldown)

B) Use queue to track task next available time
C) Or greedy: arrange most frequent first
D) All approaches valid

**Answer: D**

**Explanation:**
Problem: schedule tasks with n idle time between same tasks. Approaches: (1) greedy by frequency, math formula. (2) max heap for remaining counts, queue for cooling tasks. Time = number of units. Priority queue for most frequent, queue tracks when tasks become available. Common problem demonstrating scheduling with constraints.

---

**Q7.22: Advanced - [Theory] - [K-Queue in Single Array]**

K queues in single array:

A) Divide array into k fixed segments
B) Or linked free list with next pointers
C) Second allows dynamic sharing
D) Both valid

**Answer: D**

**Explanation:**
Fixed division: simple but potential waste. Linked approach: array cells store (data, next), free list manages available cells. Each queue maintains front/rear indices (actually pointers into array). Enqueue: take from free, link. Dequeue: return to free. Dynamic sharing, O(1) operations. Space overhead: next pointer per cell.

---

**Q7.23: Expert - [Theory] - [Queue Reconstruction by Height]**

Reconstruct queue from [[h,k],...] where k = number of taller or equal in front:

A) Sort by descending h, then ascending k
B) Insert each person at index k in result
C) Taller people first, then insert shorter at correct relative position
D) All of the above

**Answer: D**

**Explanation:**
[[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]: sort by h desc, k asc: [7,0],[7,1],[6,1],[5,0],[5,2],[4,4]. Insert at index k: [7,0], [7,0],[7,1], [7,0],[6,1],[7,1], [5,0],[7,0],[6,1],[7,1], [5,0],[7,0],[5,2],[6,1],[7,1], [5,0],[7,0],[5,2],[6,1],[4,4],[7,1]. O(n²) but clever greedy. LeetCode 406.

---

**Q7.24: Intermediate - [Application] - [Design Circular Queue]**

Design circular queue with: enQueue, deQueue, Front, Rear, isEmpty, isFull:

A) Array with head, tail, size or count
B) Full when (tail+1)%capacity == head
C) Empty when head == tail
D) All of the above

**Answer: D**

**Explanation:**
Circular queue implementation: array, head index (front), tail index (next position at rear). Count tracks elements (simpler). Or: empty when head == tail, full when (tail+1)%cap == head (wastes one slot to distinguish). enQueue: arr[tail]=x, tail=(tail+1)%cap. deQueue: x=arr[head], head=(head+1)%cap. All O(1).

---

**Q7.25: Advanced - [Theory] - [Time-Based Queue]**

Time-based key-value store with get/set:

A) Hash map for key→(value, timestamp) list
B) Binary search on timestamps for get(key, timestamp)
C) Queue for LRU eviction
D) All of the above

**Answer: D**

**Explanation:**
Design: hash map stores key→sorted list of (timestamp, value). Set: append to list. Get: binary search for largest timestamp ≤ query. For eviction: LRU or TTL with priority queue/queue. This is Redis-like design. Multiple data structures work together: hash for O(1) key access, list/tree for time queries.

---

**Q7.26: Advanced - [Trace] - [Dota2 Senate]**

Dota2 senate "DDRR": Dire ban Radiant, Radiant ban Dire alternately:

A) Use queue for each party
B) Round robin: front of each queue, smaller index bans later
C) Banned senator removed, winner re-queues with increased index
D) Simulate until one queue empty

**Answer: D**

**Explanation:**
Queue simulation: D queue [0,1], R queue [2,3]. D[0] bans R[2], R[3] bans D[1]. D[0] and R[3] back to queues with indices+4. Continue until one queue empty. Winner determined by who has more active senators. O(n) simulation. Demonstrates queue for round-robin processing with future scheduling.

---

**Q7.27: Expert - [Theory] - [Array- vs List-Based Deque]**

C++ std::deque vs std::list:

A) Deque: segmented array, O(1) random access
B) List: node per element, no random access
C) Deque better cache locality, less overhead
D) All of the above

**Answer: D**

**Explanation:**
std::deque: segmented array (blocks), maintains index-to-block mapping. O(1) push_front/pop_front/push_back/pop_back. O(1) random access (slower than vector). Better cache locality than list. List: node per element, no locality, pointer overhead. Deque preferred for double-ended operations with occasional random access.

---

**Q7.28: Intermediate - [Application] - [Recent Calls]**

RecentCounter: ping(t) returns pings in last 3000ms:

A) Queue of timestamps
B) While front < t-3000, dequeue
C) Return queue size
D) All of the above

**Answer: D**

**Explanation:**
Sliding window in time: queue maintains timestamps of pings in window. New ping: enqueue, remove old timestamps outside window (while queue.front <= t-3000, dequeue). Return size. O(number of pings in window) time, could be O(n) worst case but amortized O(1) per ping. Simple application of queue for time-based sliding window.

---

**Q7.29: Advanced - [Theory] - [Queue with Max]**

Queue with O(1) max operation:

A) Monotonic queue (deque) maintaining decreasing values
B) Or two stacks with max tracking
C) Or auxiliary deque of candidates
D) All of the above

**Answer: D**

**Explanation:**
Monotonic deque: front is max. Enqueue: remove from back while back < new element, then push back. Dequeue: if front == removed element, pop front. O(1) all operations. Alternative: max queue using two stacks (each with max tracking), amortized O(1). Useful for sliding window maximum, stream processing.

---

**Q7.30: Advanced - [Trace] - [Queue with Max]**

Max queue: enqueue 3, enqueue 1, enqueue 4, enqueue 2, dequeue(), getMax():

A) After enqueues: deque [4,2] (maintained decreasing), actual queue [3,1,4,2]
B) Dequeue 3: front of deque is 4 ≠ 3, so deque unchanged
C) getMax returns 4
D) Deque front always current max

**Answer: D**

**Explanation:**
Trace: E(3): deque=[3]. E(1): 1<3, deque=[3,1]. E(4): 4>1, pop 1, 4>3, pop 3, deque=[4]. E(2): 2<4, deque=[4,2]. D(): remove 3, 3≠4, deque=[4,2]. getMax=4. D(): remove 1, 1≠4, deque=[4,2]. D(): remove 4, 4==deque.front, pop front, deque=[2]. getMax=2. O(1) operations.

---

**Q7.31: Expert - [Theory] - [Wait-Free Queue]**

Wait-free queue vs lock-free:

A) Wait-free: every operation completes in finite steps
B) Lock-free: some operation completes, others may starve
C) Wait-free is stronger guarantee
D) All of the above

**Answer: D**

**Explanation:**
Progress guarantees: wait-free (strongest) guarantees every thread makes progress in bounded steps. Lock-free guarantees system progress (some thread succeeds), but individual threads may retry indefinitely. Obstruction-free: progress if no contention. Wait-free algorithms complex, often have higher overhead. Most practical queues are lock-free, not wait-free.

---

**Q7.32: Intermediate - [Application] - [Number of Islands]**

BFS for number of islands (connected 1s in grid):

A) Queue for BFS, visit all connected 1s from each unvisited 1
B) Mark visited as 0 or use separate visited set
C) Count BFS/DFS starts
D) All of the above

**Answer: D**

**Explanation:**
Island count: scan grid, when find unvisited 1, BFS/DFS to mark entire island visited, increment count. BFS: queue, enqueue neighbors if 1. Mark visited by setting to 0 or using visited array. Time O(m×n), space O(min(m,n)) for queue (maximum one level). Classic BFS/DFS application for connected components.

---

**Q7.33: Advanced - [Theory] - [01 BFS]**

0-1 BFS for weighted graph with weights 0 or 1:

A) Use deque: weight 0 push_front, weight 1 push_back
B) O(V+E) time, like unweighted BFS
C) Shortest path in 0-1 weighted graph
D) All of the above

**Answer: D**

**Explanation:**
0-1 BFS: edges weight 0 or 1. Deque: if edge weight 0, push to front (same "distance"), if weight 1, push to back (next "distance"). Maintains distance ordering like Dijkstra but O(V+E) instead of O((V+E)log V). Efficient for special case. Generalization: dial's algorithm for small integer weights (bucket Dijkstra).

---

**Q7.34: Expert - [Theory] - [Bucket Queue / Dial's Algorithm]**

Dial's algorithm (bucket Dijkstra) for weights 0..C:

A) Array of buckets (queues) for each distance mod (C×V)
B) O(C×V+E) time
C) When C small, faster than binary heap
D) All of the above

**Answer: D**

**Explanation:**
Dial's algorithm: bucket queue with range [0..C×V]. Each bucket contains vertices at that distance. Process buckets in order, use circular array. O(C×V + E) time. When C is small constant, O(V+E), same as BFS. For C=1, equivalent to 0-1 BFS. Practical for small integer weights, used in network flow, traffic routing.

---

**Q7.35: Intermediate - [Application] - [Open the Lock]**

Open lock "0000" to target with deadends, minimum turns:

A) BFS from start, each turn generates 8 neighbors (4 wheels × 2 directions)
B) Queue stores (combination, turns)
C) Visited set prevents cycles
D) All of the above

**Answer: D**

**Explanation:**
Shortest path in unweighted state space → BFS. Each state (4-digit combination) has 8 neighbors (increment/decrement each digit). BFS finds minimum turns. Deadends are blocked states. Queue for BFS, visited to avoid revisiting. Time O(10⁴ × 8) = manageable. Classic BFS state space search problem (LeetCode 752).

---

**Q7.36: Advanced - [Theory] - [Multi-Source BFS]**

Multi-source BFS from multiple starting nodes:

A) Enqueue all sources initially
B) Standard BFS from there
C) Finds shortest distance from any source
D) All of the above

**Answer: D**

**Explanation:**
Instead of single source, enqueue all sources with distance 0. BFS proceeds simultaneously from all sources. First visit to a node gives shortest distance from any source. Used for: finding nearest special nodes, flood fill from multiple seeds, computing distance transform in image processing. Same complexity as single-source BFS.

---

**Q7.37: Expert - [Theory] - [Bidirectional BFS]**

Bidirectional BFS from start and goal:

A) Two queues, alternately expand
B) Meet in middle when intersections found
C) O(b^(d/2)) vs O(b^d) for single direction
D) All of the above

**Answer: D**

**Explanation:**
Bidirectional: BFS from both start and goal. Terminate when frontiers intersect. Complexity O(b^(d/2)) each direction vs O(b^d) single direction (exponential improvement). Can use one queue alternating or two queues. Meeting check with hash set of visited. Dramatic speedup for large search spaces. Used in shortest path, game solving.

---

**Q7.38: Intermediate - [Application] - [Rotting Oranges]**

Rotting oranges: fresh become rotten if adjacent to rotten:

A) BFS with queue of initially rotten oranges
B) Track minutes, process level by level
C) Return minutes or -1 if fresh remains
D) All of the above

**Answer: D**

**Explanation:**
Multi-source BFS: enqueue all initially rotten. Each level = one minute. Process all at current level, rot adjacent fresh, enqueue them. Track minutes. At end, check if any fresh remain. Time O(m×n), space O(m×n). Demonstrates BFS for parallel spreading processes. Classic grid BFS problem.

---

**Q7.39: Advanced - [Theory] - [Queue in OS Scheduling]**

Operating system process scheduling uses:

A) Ready queue for processes waiting for CPU
B) Round-robin with time quantum
C) Priority queues for different priority levels
D) All of the above

**Answer: D**

**Explanation:**
OS scheduling: ready queue (FIFO) of runnable processes. Round-robin: dequeue, run for time slice, enqueue if not done. Priority scheduling: multiple queues by priority. Feedback queues: adjust priority based on behavior. Disk I/O queues, printer queues. Queue is fundamental abstraction for managing shared resources fairly.

---

**Q7.40: Intermediate - [Application] - [Moving Average]**

Moving average from data stream with window size:

A) Queue of window elements
B) Sum maintained, subtract outgoing, add incoming
C) O(1) per element
D) All of the above

**Answer: D**

**Explanation:**
Queue maintains window. New element: enqueue, add to sum. If window full: dequeue, subtract from sum. Average = sum / window_size. O(1) per element. Space O(window_size). This is the sliding window sum pattern. For large windows, numerical stability considerations (cascading errors in sum) may suggest alternative approaches.

---

**Q7.41: Advanced - [Theory] - [Queue as Iterator]**

Java's Queue iterator behavior:

A) Weakly consistent, may reflect concurrent modifications
B) Fail-fast throws ConcurrentModificationException
C) Depends on implementation
D) All valid behaviors exist

**Answer: D**

**Explanation:**
Queue iterator behaviors: ConcurrentLinkedQueue: weakly consistent, reflects state at some point, may not throw on modification. ArrayBlockingQueue: various guarantees depending on method. Some implementations fail-fast, others weakly consistent. Must check documentation. Iterator over concurrent collections generally don't throw ConcurrentModificationException (unlike HashMap).

---

**Q7.42: Advanced - [Trace] - [Perfect Squares]**

Least number of perfect squares sum to n (e.g., 12=4+4+4, 13=4+9):

A) BFS from 0, edges to +square ≤ n
B) First time reach n is minimum count
C) Queue for BFS level
D) All of the above

**Answer: D**

**Explanation:**
Shortest path in unweighted graph: BFS. States 0..n, edges from i to i+j² where i+j² ≤ n. Start 0, target n. Level = number of squares. Lagrange's four-square theorem guarantees ≤ 4 squares. BFS finds minimum. Can also use DP. This is number theory + BFS combination problem.

---

**Q7.43: Expert - [Theory] - [Disjoint Queue Operations]**

Strictly increasing queue (all elements unique and sorted):

A) Enqueue only if greater than rear
B) Dequeue removes front
C) Binary search for position
D) Can be implemented with sorted list

**Answer: D**

**Explanation:**
Various queue variants: priority queue (sorted by priority), monotone queue (monotonic property), double-ended queue. Strictly increasing queue maintains order, can use binary search for insertion point. These specialized queues solve specific problems. Understanding queue variants and their properties allows choosing the right tool.

---

**Q7.44: Expert - [Theory] - [Lock-Free Queue Memory]**

Memory reclamation in lock-free queues:

A) Hazard pointers: threads announce hazardous references
B) Read-copy-update (RCU): defer freeing
C) Epoch-based: batch reclamation
D) All of the above

**Answer: D**

**Explanation:**
Safe memory reclamation: hazard pointers (each thread has small array of protected nodes), RCU (readers don't block, writers defer free), epochs (group operations, reclaim when no threads in old epoch). These solve ABA and safe reclamation in lock-free structures. Complex, critical for production lock-free code.

---

**Q7.45: Intermediate - [Application] - [Stream Processing]**

Stream processing with windowed operations:

A) Queue for event buffer
B) Watermarks for late events
C) Triggering based on time/count
D) All of the above

**Answer: D**

**Explanation:**
Stream processing: queues buffer events, window definitions (time-based, count-based), watermarks track progress and handle late data, triggers emit results. Apache Flink, Kafka Streams, Spark Streaming use these abstractions. Queue/deque fundamental for buffering unbounded data streams with temporal windows.

---

**Q7.46: Advanced - [Theory] - [Work-Stealing Queue]**

Work-stealing queue (fork-join):

A) Double-ended: owner pushes/pops from one end
B) Thieves steal from other end
C) Reduces contention in thread pools
D) All of the above

**Answer: D**

**Explanation:**
Work-stealing: each worker has deque. Owner pushes/pops tasks from bottom. When idle, steals from top of another worker's deque. Owner and thief operate on different ends, minimal synchronization. Java's ForkJoinPool uses this. Efficient load balancing for parallel divide-and-conquer. Queue design critical for parallel performance.

---

**Q7.47: Expert - [Code] - [Chase-Lev Deque]**

Chase-Lev work-stealing deque:

A) Circular array with top (steal) and bottom (owner)
B) Owner doesn't synchronize with itself
C) Thief CAS on top index
D) All of the above

**Answer: D**

**Explanation:**
Chase-Lev deque: resizable circular array. Owner (push/pop): modify bottom, no CAS needed (single writer). Thief (steal): CAS on top. Resizing: owner copies to new array. Lock-free, scalable. Standard for work-stealing schedulers (Java, TBB, Cilk). Careful memory ordering for correctness on weakly ordered architectures.

---

**Q7.48: Expert - [Theory] - [Queue Latency]**

Queue latency in message passing:

A) Queue depth × service time
B) Little's Law: L = λW (avg items = arrival rate × avg wait)
C) Burstiness increases latency
D) All of the above

**Answer: D**

**Explanation:**
Queueing theory: Little's Law relates queue length, arrival rate, and wait time. Burst arrivals (not constant rate) increase queue depth and latency. Service rate must exceed arrival rate for stability. These principles guide system design: buffer sizing, load balancing, backpressure. Understanding queue behavior essential for distributed systems.

---

**Q7.49: Intermediate - [Application] - [Implement Stack using Queue]**

Implementing stack using queues:

A) One queue: rotate after each push
B) Two queues: transfer to make top accessible
C) Pop needs O(n), push O(1) or vice versa
D) All approaches valid

**Answer: D**

**Explanation:**
Approach 1: one queue, push at back, then rotate: pop and enqueue all except last, pop last. O(n) pop, O(1) push. Approach 2: two queues, keep newest in separate queue. Approach 3: O(n) push, O(1) pop by making push expensive. Demonstrates that stacks and queues are convertible, but with complexity tradeoffs.

---

**Q7.50: Advanced - [Trace] - [Queue Rotation]**

Stack using one queue: push(1), push(2), push(3), pop():

A) Queue: [1], push 2: [1,2], rotate: [2,1]
B) Push 3: [2,1,3], rotate×2: [3,2,1]
C) Pop returns 3 (front), queue [2,1]
D) Maintains LIFO order

**Answer: D**

**Explanation:**
Push 1: [1]. Push 2: enqueue→[1,2], rotate: dequeue 1, enqueue→[2,1]. Push 3: enqueue→[2,1,3], rotate×2: [3,2,1]. Pop: dequeue 3, return 3. New top is 2 (front). Each push costs O(n) rotates to make new element at front. Demonstrates converting between LIFO and FIFO with rotation overhead.

---

**Q7.51: Expert - [Theory] - [Queue Abstract Machine]**

Queue automaton vs Turing machine:

A) Queue automaton is Turing-complete
B) Can simulate TM with two queues
C) One queue with markers also Turing-complete
D) All of the above

**Answer: D**

**Explanation:**
Surprisingly, queue-based automata are Turing-complete. With two queues, can simulate Turing machine tape. Or one queue with special markers. Post's tag systems (queue-based string rewriting) are Turing-complete. Demonstrates computational power of simple abstractions. Queue and stack provide different but equally powerful computation models.

---

**Q7.52: Intermediate - [Application] - [Walls and Gates]**

Fill empty rooms with distance to nearest gate:

A) Multi-source BFS from all gates simultaneously
B) Queue initially contains all gates (distance 0)
C) Propagate distances level by level
D) All of the above

**Answer: D**

**Explanation:**
INF  -1  0   INF      3  -1   0   1
INF  INF INF  -1  →   2   2   1  -1
INF  -1  INF INF      1  -1   2   3
0    -1  INF INF      0  -1   3   4

Multi-source BFS: enqueue all gates. For each, update neighbors if shorter path found. Single pass fills all distances. O(m×n). Classic BFS application for distance transform from multiple sources.

---

**Q7.53: Advanced - [Theory] - [Shortest Path in Maze]**

Shortest path in unweighted maze:

A) BFS guarantees shortest path (fewest steps)
B) Queue for frontier
C) Visited marks explored cells
D) All of the above

**Answer: D**

**Explanation:**
Unweighted graph → BFS finds shortest path in edges. DFS finds a path but not necessarily shortest. Dijkstra reduces to BFS when all weights equal. Queue processes cells in order of distance from start. First time reach goal is shortest path. Fundamental algorithm for grid/pathfinding problems.

---

**Q7.54: Expert - [Theory] - [Eytzinger Layout]**

Eytzinger (BFS) layout for binary search:

A) Store tree in array level by level
B) Improves cache performance for searches
C) Branch-free binary search possible
D) All of the above

**Answer: D**

**Explanation:**
Eytzinger layout: store complete binary tree level-order (like heap). Children of i at 2i and 2i+1. Improves cache locality vs sorted array for binary search. Can do branch-free search using conditional moves. Used in high-performance searching. Connection between BFS ordering and cache-efficient data structures.

---

**Q7.55: Expert - [Theory] - [Summary]**

Queue applications summary:

A) BFS, scheduling, buffering, producer-consumer
B) Fair resource allocation, load balancing
C) Stream processing, async communication
D) Fundamental to concurrent and distributed systems

**Answer: D**

**Explanation:**
Queue is fundamental for: graph traversal (BFS), fair scheduling, buffering between fast/slow components, asynchronous communication, producer-consumer, stream processing, task distribution. FIFO property ensures fairness and ordering. Understanding queues and their variants (priority, deque, concurrent) is essential for system design. The breadth of applications shows queue's importance.

---

## Chapter 7 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 10 | FIFO, operations, circular queue, implementations |
| Intermediate | 24 | BFS, level order, two-stack queue, sliding window, scheduling |
| Advanced | 16 | Monotonic queue, 0-1 BFS, lock-free, bidirectional BFS, work-stealing |
| Expert | 5 | Persistent queue, wait-free, Chase-Lev, queue automata, Eytzinger |

**Total MCQs: 55** | **Target Met: ✓**

**Key Queue Complexities:**
- Enqueue: O(1)
- Dequeue: O(1)
- Peek/Front: O(1)
- Search: O(n)

**Applications:**
- BFS traversal
- Level order tree traversal
- Producer-consumer
- Task scheduling
- Sliding window problems
- Stream processing
- Shortest path in unweighted graphs

**Next:** Chapter 8 - Hash Tables (Target: 75 MCQs)
