# Chapter 39: External Memory Algorithms

**Target:** 25 MCQs | **Distribution:** 6 Foundational, 10 Intermediate, 6 Advanced, 3 Expert

---

**Q39.1: Foundational - [Theory] - [External Memory Model]**

The external memory (I/O) model measures algorithm efficiency by:

A) CPU instruction count
B) Number of disk block transfers (I/Os) between disk and memory
C) Total RAM usage
D) Number of comparison operations

**Answer: B**

**Explanation:**
External memory model (Aggarwal & Vitter, 1988): memory holds M elements, disk organized in blocks of B elements. Cost = number of block transfers. Scanning n elements: O(n/B) I/Os. Sorting: O((n/B) log_{M/B}(n/B)) I/Os. Internal algorithms ignore I/O — a cache miss can be 100-1000× slower than a cache hit. For large data: I/O complexity dominates running time, not CPU comparisons.

---

**Q39.2: Foundational - [Theory] - [Sequential vs Random Access]**

Why is sequential disk access dramatically faster than random access?

A) Sequential access uses more RAM
B) HDDs avoid seek time; SSDs exploit internal parallelism and prefetching
C) Random access uses more electricity
D) Sequential access skips error checking

**Answer: B**

**Explanation:**
HDD: random access = seek (move head, ~5-10ms) + rotation (~2-4ms). Sequential: head already positioned, just read consecutive sectors. ~100× faster. SSD: no mechanical parts, but sequential still ~2-4× faster due to: (1) Large internal page sizes (4-16KB), (2) Prefetch/read-ahead, (3) Parallel channels better utilized. External memory algorithms minimize random I/O by accessing data in large sequential blocks.

---

**Q39.3: Intermediate - [Complexity] - [External Sorting]**

External merge sort of n elements with memory M and block size B requires how many I/Os?

A) O(n)
B) O(n/B)
C) O((n/B) × log_{M/B}(n/B))
D) O(n × log n)

**Answer: C**

**Explanation:**
Phase 1: create ⌈n/M⌉ sorted runs, each of size M. Reads/writes each element once: O(n/B) I/Os. Phase 2: (M/B - 1)-way merge (one buffer per run + one output buffer). Each merge pass: O(n/B) I/Os. Number of passes: log_{M/B}(n/M). Total: O((n/B) × log_{M/B}(n/B)). Compare to internal sort O(n log n): the /B factor (blocking) and log base M/B (many-way merge) dramatically reduce I/Os.

---

**Q39.4: Foundational - [Theory] - [B-Tree in External Memory]**

B-Trees are the standard external memory search structure because:

A) They have the smallest binary tree height
B) Each node matches one disk block, minimizing I/O per search
C) They only work on SSDs
D) They don't need any memory

**Answer: B**

**Explanation:**
B-Tree: node size = disk block (typically 4-16KB). With fanout f ≈ B: tree height = O(log_B n). Each level = one I/O. For n = 10⁹, B = 1000: height ≈ 3. Three I/Os for any search. Binary tree: height log₂(10⁹) ≈ 30 I/Os — 10× worse. B-Tree's high fanout directly exploits block transfer. This is why virtually all disk-based databases use B-Trees (or B+ Trees) as their primary index.

---

**Q39.5: Intermediate - [Theory] - [Replacement Selection]**

Replacement selection during external sort run generation can create runs larger than memory because:

A) It compresses the data
B) It uses a heap to continuously output the minimum while reading new elements into freed space
C) It uses multiple disks simultaneously
D) It skips duplicate elements

**Answer: B**

**Explanation:**
Replacement selection: maintain min-heap of M elements. Extract min (write to current run), read next element from input. If new element ≥ last output: insert into heap (extends current run). If smaller: mark for next run. Average run size: ~2M (twice memory). Longer runs = fewer merge passes. But: modern CPUs favor quicksort-based partitioning (better cache use) over replacement selection, despite shorter runs (~M not ~2M).

---

**Q39.6: Intermediate - [Theory] - [Double Buffering]**

Double buffering in external memory algorithms improves performance by:

A) Using two copies of the data for redundancy
B) Overlapping I/O with computation — one buffer processes while the other loads
C) Doubling the block size
D) Using twice the memory for the sort

**Answer: B**

**Explanation:**
Without double buffering: read block → process → read next block (CPU idle during I/O). With double buffering: two buffers, alternate. While processing buffer 1, load into buffer 2. When done: swap. CPU and disk work simultaneously. Hides I/O latency. Generalizes to k-buffering (k buffers in pipeline). Essential for achieving peak I/O throughput. Uses 2× memory for buffers but eliminates I/O wait time.

---

**Q39.7: Advanced - [Theory] - [Cache-Oblivious Model]**

Cache-oblivious algorithms are significant because:

A) They use no cache at all
B) They achieve optimal I/O performance without knowing cache size or block size
C) They are simpler than cache-aware algorithms
D) They only work on specific hardware

**Answer: B**

**Explanation:**
Cache-oblivious: algorithm doesn't know M (cache size) or B (block size), yet achieves asymptotically optimal I/O for ANY M and B. Works across the ENTIRE memory hierarchy simultaneously (L1, L2, L3, RAM, disk). Key technique: recursive divide-and-conquer that naturally creates sub-problems fitting any cache. van Emde Boas layout for trees, funnel sort for sorting. Elegant theoretical framework with practical impact.

---

**Q39.8: Intermediate - [Theory] - [Buffer Tree]**

A buffer tree improves B-Tree insertion throughput by:

A) Making the tree shorter
B) Collecting updates in buffers at internal nodes, flushing when full
C) Removing the tree structure entirely
D) Using linked lists instead of arrays in nodes

**Answer: B**

**Explanation:**
Buffer tree (Arge, 1995): each internal node has a buffer of size B. Insertions go to root buffer. When buffer fills: flush to appropriate children. Each flush: O(1) I/Os amortized (flush entire buffer in one I/O). Amortized insertion: O((1/B) × log_M/B(n/B)) I/Os — a 1/B factor better than standard B-Tree's O(log_B n). Trade-off: queries may need to check buffers along path. Precursor to LSM Trees and fractal trees.

---

**Q39.9: Foundational - [Theory] - [External Memory Scanning]**

Scanning n elements stored on disk (reading each once) costs:

A) O(n) I/Os
B) O(n/B) I/Os
C) O(n × B) I/Os
D) O(1) I/Os

**Answer: B**

**Explanation:**
Each I/O transfers one block of B elements. n elements in n/B blocks. Sequential scan: read all blocks once = O(n/B) I/Os. This is the minimum possible I/O for reading all data. Example: n = 10⁹, B = 1000 (block holds 1000 elements): 10⁶ I/Os vs 10⁹ element-by-element reads. The "factor of B" savings from blocked access is the fundamental reason external memory algorithms matter.

---

**Q39.10: Advanced - [Theory] - [External Memory Graph Algorithms]**

BFS on a graph stored on disk has I/O complexity:

A) O(V + E) I/Os (same as internal)
B) It depends on the graph structure — O((V + E/B) × log(V/B)) with best known algorithms
C) O(1) I/Os
D) Always O(V × E) I/Os

**Answer: B**

**Explanation:**
External BFS is much harder than internal BFS. Adjacency list scan: O(V + sort(E)) I/Os with known techniques. But vertices discovered in arbitrary order → random access to adjacency lists. Best algorithms (Munagala-Ranade, Mehlhorn-Meyer): O(V + sort(E)) I/Os for undirected. Directed: even harder. Graph algorithms on disk lack the sequential access patterns that make sorting efficient externally. Active research area.

---

**Q39.11: Intermediate - [Theory] - [External Hashing]**

Extendible hashing handles growing data on disk by:

A) Rehashing all elements when the table is full
B) Splitting only the overflowing bucket, using a directory that grows incrementally
C) Creating a new hash function each time
D) Storing all data in a single file

**Answer: B**

**Explanation:**
Extendible hashing: directory maps hash prefixes to buckets. When bucket overflows: split that bucket (double its local depth), update directory entries. Directory may need to double (increase global depth) but no data is rehashed — just pointer updates. Point query: 2 I/Os (directory + bucket). Linear hashing: similar but splits buckets in order, no directory. Both avoid full rehash. Used in some database systems (e.g., IBM DB2 historically).

---

**Q39.12: Expert - [Theory] - [Cache-Oblivious Sorting]**

Funnel sort achieves the optimal external sorting bound cache-obliviously. Its I/O complexity is:

A) O(n log n)
B) O((n/B) × log_{M/B}(n/B)) — matching external merge sort
C) O(n/B)
D) O(n × B)

**Answer: B**

**Explanation:**
Funnel sort (Frigo et al., 1999): recursive merge structure called a "k-merger" (funnel). Merges k sorted lists using a recursive binary merge tree with buffers. Without knowing M or B: achieves O((n/B) log_{M/B}(n/B)) I/Os — matching the optimal external merge sort bound. The recursive structure naturally creates sub-problems fitting any cache level. Landmark result in cache-oblivious algorithm theory.

---

**Q39.13: Intermediate - [Theory] - [van Emde Boas Layout]**

The van Emde Boas tree layout improves cache performance for binary search by:

A) Using a hash table instead of a tree
B) Arranging tree nodes in memory so subtrees of height ~log B are contiguous
C) Sorting the tree nodes by value
D) Using linked lists for tree children

**Answer: B**

**Explanation:**
Standard binary tree: in-order or BFS layout → traversal crosses many cache lines. van Emde Boas layout: recursively split tree at height/2, store top half contiguously, then bottom subtrees contiguously. Search path crosses O(log_B n) cache lines (optimal for any B), without knowing B. Cache-oblivious search in O(log_B n) I/Os vs O(log n) for naive binary tree (each level may = one cache miss).

---

**Q39.14: Foundational - [Theory] - [Memory Hierarchy]**

The memory hierarchy (registers → L1 → L2 → L3 → RAM → SSD → HDD) exists because:

A) Faster memory is more expensive and smaller in capacity
B) All memory types have the same speed
C) Slower memory is less reliable
D) Registers can only hold instructions

**Answer: A**

**Explanation:**
Fundamental trade-off: speed vs cost/size. Registers: fastest (< 1ns), tiny (hundreds of bytes). L1 cache: ~1ns, ~64KB. L2: ~5ns, ~256KB. L3: ~15ns, ~8MB. RAM: ~50-100ns, GBs. SSD: ~100μs, TBs. HDD: ~10ms, TBs. Each level: faster, smaller, more expensive. Algorithms that exploit locality (access nearby data repeatedly before moving on) leverage the hierarchy effectively. This is why cache-efficient algorithms matter.

---

**Q39.15: Advanced - [Theory] - [External Priority Queue]**

An optimal external priority queue supports insert and delete-min in:

A) O(1) I/Os each
B) O((1/B) × log_{M/B}(n/B)) amortized I/Os each
C) O(log n) I/Os each
D) O(n/B) I/Os each

**Answer: B**

**Explanation:**
External priority queue (buffer heap, tournament tree): batches operations in buffers, amortizes I/O cost. Insert/delete-min: O((1/B) log_{M/B}(n/B)) amortized. The 1/B factor: each I/O moves B elements, amortized over B operations. Matches the sorting lower bound (extracting all elements = sorting). Internal heap: O(log n) per operation but each may be a cache miss. External: much fewer I/Os via buffering. Used in external graph algorithms.

---

**Q39.16: Expert - [Theory] - [I/O Lower Bound for Sorting]**

The I/O lower bound for comparison-based sorting of n elements is:

A) Ω(n/B)
B) Ω((n/B) × log_{M/B}(n/B))
C) Ω(n log n)
D) Ω(n²/B²)

**Answer: B**

**Explanation:**
Lower bound proof (Aggarwal-Vitter): each I/O reads/writes B elements. After t I/Os, at most M!^(ceil(t×B/M)) orderings distinguishable. Need to distinguish n! orderings. Solving: t = Ω((n/B) × log_{M/B}(n/B)). Scanning lower bound: Ω(n/B). Sorting: strictly harder than scanning (extra log factor). External merge sort matches this bound → optimal. Cache-oblivious funnel sort also matches it without knowing M, B. Tight bound.

---

**Q39.17: Intermediate - [Theory] - [SSD vs HDD Algorithms]**

SSDs change external memory algorithm design because:

A) SSDs are slower than HDDs
B) SSDs have fast random reads but limited write endurance, favoring read-heavy sequential write patterns
C) SSDs have infinite storage
D) SSDs don't support block-level access

**Answer: B**

**Explanation:**
SSD differences from HDD: (1) Random read much faster (~100μs vs ~10ms), narrowing the sequential/random gap. (2) Limited write endurance (NAND cells wear out). (3) Write amplification from flash translation layer. (4) Erase-before-write at block granularity. Implications: read-optimized structures (B-Trees) may be preferred over write-optimized (LSM Trees) for SSDs. Write amplification matters more. Algorithm design must consider asymmetric read/write costs.

---

**Q39.18: Advanced - [Theory] - [External Memory Selection]**

Finding the median of n unsorted elements on disk requires:

A) O(n/B) I/Os (single scan)
B) O((n/B) × log_{M/B}(n/B)) I/Os (sorting)
C) O(n/B) I/Os using external memory median-of-medians
D) O(n²/B) I/Os

**Answer: C**

**Explanation:**
External selection (k-th element): partition-based like quickselect. Scan to partition: O(n/B). With median-of-medians pivot: recurse on ≤ 7n/10 elements. T(n) = T(7n/10) + O(n/B) = O(n/B). No sorting needed! Same as scanning complexity but with larger constant. Compare to internal quickselect O(n). The /B factor from blocked I/O makes external selection surprisingly efficient — same order as just reading the data.

---

**Q39.19: Intermediate - [Theory] - [Disk Striping / RAID]**

RAID (Redundant Array of Independent Disks) improves external algorithm performance by:

A) Making disks larger
B) Parallelizing I/O across multiple disks, increasing bandwidth
C) Compressing data automatically
D) Eliminating the need for RAM

**Answer: B**

**Explanation:**
RAID: spread data across D disks. RAID 0 (striping): consecutive blocks on different disks. Read/write: D parallel I/Os. Effective bandwidth: D × single disk. RAID 1 (mirroring): redundancy, 2× read speed. RAID 5: striping + parity, tolerates 1 disk failure. For external algorithms: effective block size becomes D×B, boosting the "B factor." External merge sort with RAID: O((n/(D×B)) × log_{M/(D×B)}(n/(D×B))) I/Os.

---

**Q39.20: Expert - [Theory] - [Streaming Lower Bounds]**

Any algorithm that determines whether all n elements in a stream are distinct requires:

A) O(1) space
B) O(log n) space
C) Ω(n) space (must remember all elements)
D) O(√n) space

**Answer: C**

**Explanation:**
Distinctness: must detect if any element repeats. Adversary argument: after seeing k distinct elements, the set of "dangerous" elements (that would create a repeat) is exactly those k elements. Must distinguish between 2^k subsets → need k bits to track. After n elements: need Ω(n) bits. Communication complexity lower bound makes this precise. This is why Bloom filters (approximate) and HyperLogLog (approximate counting) are essential — exact streaming distinctness is provably hard.

---

## Chapter 39 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | I/O model, sequential access, B-Tree external, scanning, memory hierarchy |
| Intermediate | 8 | External sort, replacement selection, double buffering, buffer tree, hashing, SSD, RAID |
| Advanced | 4 | Cache-oblivious, external graph BFS, external priority queue, external selection |
| Expert | 3 | Funnel sort, I/O lower bound, streaming lower bound |

**Total MCQs: 20**

**Answer Distribution: A=3, B=13, C=3, D=1**

**Next:** Chapter 40 - Streaming Algorithms
