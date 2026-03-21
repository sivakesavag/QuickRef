# Chapter 37: Concurrency & Parallel Algorithms

**Target:** 25 MCQs | **Distribution:** 6 Foundational, 10 Intermediate, 6 Advanced, 3 Expert

---

**Q37.1: Foundational - [Theory] - [Thread Safety]**

A data structure is "thread-safe" when:

A) It can only be accessed by one thread
B) It behaves correctly when accessed by multiple threads concurrently
C) It uses no memory
D) It runs faster with more threads

**Answer: B**

**Explanation:**
Thread-safe: concurrent access produces correct results without data corruption. Techniques: mutexes (exclusive access), read-write locks (many readers or one writer), lock-free algorithms (CAS operations), immutable data (no modification needed). Non-thread-safe: concurrent modifications can corrupt internal state (e.g., two threads resizing a hash table simultaneously). Java ConcurrentHashMap: thread-safe. Python dict: not thread-safe for concurrent writes.

---

**Q37.2: Foundational - [Theory] - [Race Condition]**

A race condition occurs when:

A) Two programs compete for the fastest execution
B) The correctness of output depends on unpredictable timing of thread execution
C) A thread runs faster than expected
D) Too many threads are created

**Answer: B**

**Explanation:**
Race condition: result depends on scheduling order. Classic example: two threads incrementing counter. Read-modify-write is not atomic: both read 5, both write 6 (lost update). Expected: 7. Actual: 6. Fix: make increment atomic (mutex, atomic instruction, lock-free CAS). Race conditions are notoriously hard to debug because they're timing-dependent — may only appear under high load or specific scheduling.

---

**Q37.3: Intermediate - [Theory] - [Lock-Free vs Wait-Free]**

What is the difference between lock-free and wait-free algorithms?

A) Lock-free is always faster
B) Lock-free guarantees system-wide progress; wait-free guarantees per-thread progress
C) They are the same concept
D) Wait-free uses more locks

**Answer: B**

**Explanation:**
Lock-free: at least ONE thread makes progress in any execution (no global deadlock, but individual threads may starve). Wait-free: EVERY thread completes in bounded steps (no starvation). Wait-free is strictly stronger: every wait-free algorithm is lock-free, not vice versa. Lock-free: CAS retry loops (a thread may retry indefinitely under contention). Wait-free: harder to design, often uses helping mechanisms. Examples: lock-free queue (Michael-Scott), wait-free register (Herlihy).

---

**Q37.4: Foundational - [Theory] - [Mutex vs Semaphore]**

A mutex differs from a semaphore in that:

A) A mutex has binary state (locked/unlocked) and ownership; a semaphore is a counter
B) A semaphore is always binary
C) A mutex allows multiple threads simultaneously
D) They are functionally identical

**Answer: A**

**Explanation:**
Mutex: binary lock, owned by the locking thread (only owner can unlock). Protects critical sections. Semaphore: counter initialized to N. sem_wait() decrements (blocks if 0), sem_post() increments. N=1: binary semaphore (like mutex but without ownership — any thread can post). N>1: allows N simultaneous accessors. Use case: mutex for mutual exclusion, semaphore for resource counting (e.g., connection pool of size N).

---

**Q37.5: Intermediate - [Theory] - [CAS Operation]**

Compare-and-Swap (CAS) is the foundation of lock-free programming because:

A) It locks all threads except one
B) It atomically reads, compares, and conditionally writes in a single hardware instruction
C) It is faster than any lock
D) It eliminates the need for memory

**Answer: B**

**Explanation:**
CAS(addr, expected, new): atomically: if *addr == expected, set *addr = new, return true. Else return false (value changed by another thread). Single hardware instruction → atomic without locks. Lock-free pattern: read value, compute new value, CAS to install. If CAS fails (another thread changed it): retry. ABA problem: value changes A→B→A, CAS doesn't detect intermediate change. Fix: tagged pointers or hazard pointers.

---

**Q37.6: Advanced - [Theory] - [ABA Problem]**

The ABA problem in lock-free algorithms occurs when:

A) A thread reads value A, another changes it to B then back to A, and the first thread's CAS incorrectly succeeds
B) Two threads deadlock
C) Memory is freed twice
D) A priority inversion occurs

**Answer: A**

**Explanation:**
ABA: Thread 1 reads A. Thread 2 changes value A→B→A. Thread 1's CAS(expected=A, new=C) succeeds — thinks nothing changed. But the underlying data may have changed (e.g., node was freed and reused). Dangerous in lock-free data structures with memory reuse. Solutions: tagged pointers (version counter), hazard pointers (defer reuse), epoch-based reclamation. x86 CMPXCHG16B supports 128-bit CAS for tagged pointers.

---

**Q37.7: Intermediate - [Theory] - [Reader-Writer Lock]**

A read-write lock improves performance over a simple mutex when:

A) Writes are more frequent than reads
B) Reads vastly outnumber writes (many concurrent readers allowed)
C) Only one thread exists
D) The critical section is very short

**Answer: B**

**Explanation:**
Read-write lock: multiple readers simultaneously OR one writer exclusively. For read-heavy workloads (e.g., config lookup, cache reads): many threads read concurrently without blocking each other. Writer needs exclusive access, blocking all readers and other writers. If writes are frequent: overhead of RW lock > simple mutex (mode switching cost). Best case: 95%+ reads, rare writes. Java: ReadWriteLock, ReentrantReadWriteLock.

---

**Q37.8: Intermediate - [Theory] - [Parallel Merge Sort]**

Parallel merge sort with p processors achieves what time complexity?

A) O(n/p)
B) O(n log n / p + log² n)
C) O(n log n) regardless of p
D) O(p × n log n)

**Answer: B**

**Explanation:**
Parallel merge sort: divide work among p processors. Sort phase: each processor sorts n/p elements in O((n/p) log(n/p)). Merge phase: parallel merge of sorted runs. With optimal parallel merge: O(n/p × log n + log² n). The log² n term: communication/synchronization overhead from merging. Span (critical path): O(log² n). Work: O(n log n). Speedup: nearly linear for p << n/log n. Amdahl's law limits practical speedup.

---

**Q37.9: Foundational - [Theory] - [Deadlock Conditions]**

Which of the following is NOT one of the four necessary conditions for deadlock?

A) Mutual exclusion
B) Hold and wait
C) Preemption
D) Circular wait

**Answer: C**

**Explanation:**
Four conditions for deadlock (Coffman conditions): (1) Mutual exclusion: resources not shareable. (2) Hold and wait: hold one resource, wait for another. (3) No preemption: resources can't be forcibly taken. (4) Circular wait: circular chain of waiting. "Preemption" (C) is the opposite — it's "NO preemption" that is required. If resources CAN be preempted (forcibly taken), deadlock is prevented. Breaking any one condition prevents deadlock.

---

**Q37.10: Advanced - [Theory] - [Concurrent Hash Map]**

Java's ConcurrentHashMap avoids locking the entire map by:

A) Using a single global lock
B) Using lock striping (partitioning into segments, each with its own lock)
C) Making all operations sequential
D) Copying the entire map on each write

**Answer: B**

**Explanation:**
Lock striping: divide hash table into segments (e.g., 16). Each segment has its own lock. Concurrent access to different segments: no contention. Same segment: serialized. Java 8+: even finer — CAS on individual bins, synchronized only for linked list/tree updates. Read operations: usually lock-free (volatile reads). Throughput scales with number of segments/cores. Go's sync.Map: similar concept with read-optimized path.

---

**Q37.11: Intermediate - [Theory] - [Map-Reduce Pattern]**

The Map-Reduce paradigm for parallel processing consists of:

A) Mapping data to a database then reducing table sizes
B) A map phase (apply function to each element independently) followed by a reduce phase (combine results)
C) Two sequential sorting passes
D) A single parallel scan

**Answer: B**

**Explanation:**
Map: apply function f to each data chunk independently (embarrassingly parallel). Results: key-value pairs. Shuffle: group by key across workers. Reduce: aggregate values per key. Word count: map emits (word, 1) for each word. Reduce sums counts per word. O(n/p) map + O(n/p) reduce ideally. Framework handles distribution, fault tolerance. Hadoop, Spark. Pattern generalizes beyond big data: any scatter-gather computation.

---

**Q37.12: Expert - [Theory] - [Work-Stealing]**

Work-stealing schedulers (like Java ForkJoinPool) achieve load balancing by:

A) Assigning equal work to all threads upfront
B) Having idle threads steal tasks from the tails of busy threads' deques
C) Using a central work queue with a single lock
D) Randomly redistributing all tasks periodically

**Answer: B**

**Explanation:**
Work-stealing: each thread has a double-ended queue (deque). Push/pop own tasks from one end (LIFO — locality). Idle threads steal from the OTHER end (FIFO — steal large tasks). LIFO/FIFO asymmetry: worker's own tasks are recent/local (cache-warm). Stolen tasks are old/large (worth stealing). Achieves dynamic load balancing with minimal synchronization. O(T₁/p + T∞) time for work T₁ and span T∞ with p processors. Provably optimal.

---

**Q37.13: Intermediate - [Theory] - [Volatile vs Atomic]**

In Java/C++, `volatile` alone is insufficient for thread-safe counters because:

A) Volatile prevents all optimizations
B) Volatile ensures visibility but not atomicity of compound operations (read-modify-write)
C) Volatile is slower than locks
D) Volatile only works for boolean variables

**Answer: B**

**Explanation:**
Volatile (Java): guarantees visibility (changes seen by all threads) and prevents reordering. But `counter++` is three operations: read, increment, write. Volatile doesn't make this sequence atomic. Two threads: both read 5, both write 6. Fix: AtomicInteger (uses CAS), or synchronized block. C++ volatile: even weaker — only prevents compiler optimization, no memory ordering guarantees. Use std::atomic<int> instead.

---

**Q37.14: Foundational - [Theory] - [Amdahl's Law]**

Amdahl's Law states that the maximum speedup from parallelization is limited by:

A) The number of processors available
B) The fraction of the program that must remain sequential
C) The memory bandwidth
D) The programming language used

**Answer: B**

**Explanation:**
Amdahl's Law: Speedup = 1 / (s + (1-s)/p) where s = serial fraction, p = processors. As p → ∞: speedup → 1/s. If 5% is serial: max speedup = 20×, regardless of processors. Even with 1000 cores, serial bottleneck dominates. Implication: optimizing the serial portion matters more than adding processors. Gustafson's Law: alternative view — with more processors, solve larger problems (weak scaling).

---

**Q37.15: Advanced - [Theory] - [Memory Ordering]**

In modern CPUs, memory operations may be reordered. Memory barriers (fences) are needed to:

A) Speed up memory access
B) Prevent hardware and compiler from reordering reads/writes across the barrier
C) Allocate more memory
D) Compress data in memory

**Answer: B**

**Explanation:**
CPUs reorder memory operations for performance (store buffers, out-of-order execution). Without barriers: Thread 1 writes x=1 then flag=true. Thread 2 sees flag=true but x=0 (write reordered). Memory barrier (fence): ensures all prior stores are visible before subsequent stores. C++: std::memory_order_acquire, release, seq_cst. x86: strong ordering (most stores visible in order). ARM/Power: weak ordering (explicit barriers required). Critical for lock-free programming correctness.

---

**Q37.16: Advanced - [Theory] - [Lock-Free Queue]**

The Michael-Scott lock-free queue uses what technique for safe memory reclamation?

A) Garbage collection only
B) Hazard pointers or epoch-based reclamation
C) Reference counting alone
D) Stack-based allocation

**Answer: B**

**Explanation:**
Lock-free queue: CAS on head (dequeue) and tail (enqueue). Problem: after dequeuing a node, can't immediately free it — other threads may still hold references. Hazard pointers: each thread publishes pointers it's currently accessing. Reclamation only when no thread's hazard pointer references the node. Epoch-based: threads enter/exit epochs, reclaim nodes from two epochs ago. Java: GC handles this. C++: explicit memory reclamation needed — this is the hard part of lock-free programming.

---

**Q37.17: Expert - [Theory] - [Transactional Memory]**

Hardware Transactional Memory (HTM) provides:

A) Persistent storage transactions
B) Optimistic concurrency: execute speculatively, abort and retry on conflict
C) Network transaction processing
D) File system journaling

**Answer: B**

**Explanation:**
HTM (Intel TSX, IBM POWER): execute critical section speculatively without locks. Hardware tracks read/write sets. If no conflicts: commit atomically. If another thread touches same cache line: abort, retry (or fall back to lock). Optimistic: assumes no conflict, fast common case. Pessimistic (locks): pays lock overhead even without contention. HTM best for low-contention critical sections. Challenges: limited read/write set size, false conflicts on same cache line.

---

**Q37.18: Intermediate - [Theory] - [Thread Pool]**

Thread pools improve performance over creating new threads per task because:

A) Threads are never reused
B) Thread creation/destruction overhead is amortized across many tasks
C) Thread pools use less memory per thread
D) Thread pools guarantee FIFO execution

**Answer: B**

**Explanation:**
Thread creation: kernel system call, stack allocation, scheduling setup (~microseconds to milliseconds). For short tasks (microseconds): creation overhead dominates. Thread pool: create N threads once, reuse for many tasks. Tasks submitted to queue, workers pull and execute. Java: ExecutorService, ThreadPoolExecutor. Python: ThreadPoolExecutor. Typical sizing: CPU-bound tasks: N = cores. I/O-bound: N = cores × (1 + wait/service ratio).

---

**Q37.19: Expert - [Theory] - [Parallel Prefix Sum]**

Parallel prefix sum (scan) on n elements with p processors runs in:

A) O(n) work, O(n) span
B) O(n) work, O(log n) span
C) O(n log n) work, O(log n) span
D) O(n/p) work, O(1) span

**Answer: B**

**Explanation:**
Parallel prefix sum (Blelloch scan): two phases. Up-sweep: reduce pairs → O(n) work, O(log n) depth. Down-sweep: distribute partial sums → O(n) work, O(log n) depth. Total: O(n) work, O(log n) span. With p processors: O(n/p + log n) time. Foundation for many parallel algorithms: parallel sort, stream compaction, parallel filter. GPU implementations: core primitive in CUDA (thrust::inclusive_scan).

---

**Q37.20: Intermediate - [Theory] - [Concurrent Data Structure Choice]**

For a producer-consumer pattern with one producer and one consumer, the most efficient data structure is:

A) Locked linked list
B) Lock-free SPSC (Single Producer Single Consumer) ring buffer
C) Global mutex-protected array
D) Per-element locks

**Answer: B**

**Explanation:**
SPSC ring buffer: no locks needed! Producer writes to tail, consumer reads from head. Only contention: head/tail pointers, resolvable with atomic reads/writes (no CAS needed). Zero-copy: both access the buffer directly. Cache-friendly: sequential access pattern. Used in: Linux kernel (kfifo), audio processing, network packet processing. MPMC (multi-producer multi-consumer): more complex, requires CAS or locks. SPSC is the golden case for lock-free design.

---

## Chapter 37 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | Thread safety, race conditions, mutex vs semaphore, deadlock, Amdahl's Law |
| Intermediate | 8 | Lock-free vs wait-free, CAS, RW locks, parallel merge sort, Map-Reduce, volatile, thread pool, SPSC |
| Advanced | 4 | ABA problem, ConcurrentHashMap, memory ordering, lock-free queue |
| Expert | 3 | Work-stealing, transactional memory, parallel prefix sum |

**Total MCQs: 20**

**Answer Distribution: A=3, B=16, C=1, D=0**

**Next:** Part VII - Expert-Level & Rare Scenarios
