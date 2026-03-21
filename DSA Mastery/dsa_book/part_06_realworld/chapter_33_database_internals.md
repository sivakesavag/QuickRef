# Chapter 33: Database Internals & DSA

**Target:** 40 MCQs | **Distribution:** 10 Foundational, 16 Intermediate, 10 Advanced, 4 Expert

---

**Q33.1: Foundational - [Theory] - [B-Tree Purpose]**

Why are B-Trees used as the primary index structure in most relational databases?

A) They minimize CPU cache misses during sorts
B) They minimize disk I/O by storing many keys per node (matching disk block size)
C) They provide O(1) lookup time
D) They automatically compress data

**Answer: B**

**Explanation:**
B-Trees are designed for disk-based storage. Each node = one disk block (typically 4-16KB). High branching factor (hundreds of keys per node) → tree height of 3-4 for billions of records. Each level = one disk I/O. With root cached, a lookup needs only 2-3 disk reads. Hash indexes give O(1) but can't do range queries. B-Trees balance lookup speed with range query support.

---

**Q33.2: Foundational - [Theory] - [B+ Tree vs B-Tree]**

What is the key structural difference between a B-Tree and a B+ Tree?

A) B+ Trees store all data in leaf nodes only, with leaves linked in a list
B) B-Trees have higher branching factor
C) B+ Trees don't support range queries
D) B-Trees use less disk space

**Answer: A**

**Explanation:**
B+ Tree: internal nodes store only keys (routing), ALL data records live in leaf nodes. Leaves are linked as a doubly-linked list. Advantages: (1) Internal nodes are smaller → higher fanout → shorter tree, (2) Range queries: follow leaf links sequentially, (3) All leaves at same depth. B-Trees store data at every level — saves space if data is small but loses the leaf-chain range scan advantage.

---

**Q33.3: Intermediate - [Complexity] - [B-Tree Operations]**

For a B-Tree of order m with n keys, what is the height and search complexity?

A) Height O(log₂ n), search O(log₂ n)
B) Height O(log_m n), search O(m × log_m n)
C) Height O(n), search O(n)
D) Height O(log_m n), search O(log_m n)

**Answer: B**

**Explanation:**
B-Tree height: O(log_m n) where m = order (max children per node). At each node, binary search among up to m-1 keys: O(log m). Total comparisons: O(log m × log_m n) = O(log n). But in terms of DISK I/Os: O(log_m n) — one I/O per level. Since m is large (≈256-1024), log_m(10⁹) ≈ 3. The O(m × log_m n) accounts for scanning within each node (linear scan often used in practice since nodes fit in cache).

---

**Q33.4: Foundational - [Theory] - [LSM Tree Motivation]**

LSM Trees (Log-Structured Merge) are preferred over B-Trees when:

A) Read performance is the top priority
B) Write-heavy workloads dominate (high insert/update throughput)
C) The data fits entirely in memory
D) Only point queries are needed

**Answer: B**

**Explanation:**
LSM Trees batch writes in an in-memory buffer (memtable), then flush as sorted runs to disk. Writes are sequential → much faster than B-Tree's random I/O updates. Trade-off: reads may check multiple levels. Used in: Cassandra, RocksDB, LevelDB, HBase. B-Trees are better for read-heavy workloads. LSM Trees sacrifice some read speed for dramatically better write throughput.

---

**Q33.5: Intermediate - [Theory] - [LSM Compaction]**

What is the purpose of compaction in an LSM Tree?

A) To compress data and save disk space
B) To merge sorted runs, eliminating duplicates and maintaining read performance
C) To defragment memory
D) To rebuild the in-memory index

**Answer: B**

**Explanation:**
Without compaction, reads degrade: must check all levels for a key. Compaction merges sorted runs at one level into a larger sorted run at the next. Eliminates deleted entries (tombstones), merges updates (keep latest), and reduces number of files to check. Two strategies: leveled (RocksDB default, better reads) and tiered (Cassandra, better writes). Trade-off: compaction uses I/O bandwidth.

---

**Q33.6: Intermediate - [Theory] - [Hash Index]**

What is the main limitation of hash indexes in databases?

A) They have O(n) lookup time
B) They cannot support range queries or ordered scans
C) They require more disk space than B-Trees
D) They cannot handle concurrent access

**Answer: B**

**Explanation:**
Hash indexes provide O(1) average point lookups — faster than B-Trees for exact key matches. But hash functions destroy key ordering: WHERE id = 5 is fast, but WHERE id BETWEEN 5 AND 100 requires scanning ALL buckets. B-Trees maintain sorted order → range scans follow leaf pointers. Most databases (PostgreSQL, MySQL) use B-Trees as default because range queries are common. Hash indexes are niche.

---

**Q33.7: Foundational - [Theory] - [MVCC]**

Multi-Version Concurrency Control (MVCC) allows:

A) Readers to never block writers (and vice versa)
B) Only one transaction at a time
C) Automatic data replication
D) Faster disk writes

**Answer: A**

**Explanation:**
MVCC: each write creates a new version of the row rather than overwriting. Readers see a consistent snapshot (old version) while writers create new versions. No reader-writer locks needed. Used in PostgreSQL, MySQL/InnoDB, Oracle. Trade-off: storage overhead (multiple versions), vacuum/garbage collection needed to reclaim old versions. Enables high concurrency without read locks.

---

**Q33.8: Advanced - [Theory] - [WAL Purpose]**

Write-Ahead Logging (WAL) ensures database durability by:

A) Writing all changes to a sequential log BEFORE modifying data pages
B) Keeping a backup copy of the entire database
C) Using RAID storage for redundancy
D) Compressing data before writing

**Answer: A**

**Explanation:**
WAL: every modification logged sequentially before the actual data page is updated. On crash: replay the log to recover committed transactions. Sequential writes are fast (append-only). Data pages can be written lazily (checkpointing). If crash occurs between log write and data write: log replay fixes everything. Foundation of ARIES recovery protocol. Used in virtually all databases (PostgreSQL pg_wal, MySQL redo log).

---

**Q33.9: Intermediate - [Theory] - [Join Algorithms]**

For joining two large tables where neither is indexed, which join algorithm is typically most efficient?

A) Nested loop join
B) Hash join
C) Sort-merge join
D) Cross join

**Answer: B**

**Explanation:**
Hash join: build hash table on smaller table, probe with larger table. O(n + m) if hash table fits in memory. Nested loop: O(n × m) — too slow for large tables. Sort-merge: O(n log n + m log m) — good when data is already sorted or when output needs ordering. Hash join is the default for equi-joins in modern databases (PostgreSQL, Oracle). If no index and no pre-sorting, hash join wins.

---

**Q33.10: Advanced - [Theory] - [Nested Loop vs Hash Join]**

When would a nested loop join outperform hash join?

A) When both tables are very large
B) When the inner table has an index on the join column and is small
C) When the join condition uses inequality (>, <)
D) When the tables have no indexes

**Answer: B**

**Explanation:**
Index nested loop join: for each row in outer table, use index to find matching inner rows. If inner table is small and indexed: O(n × log m) with index lookups. With n=1000 and m=10M indexed: 1000 × 4 I/Os = 4000 I/Os. Hash join: must hash all 10M rows. So indexed NLJ wins when outer is small and inner is indexed. For inequality joins (C), only NLJ or sort-merge work — hash join can't handle non-equality.

---

**Q33.11: Intermediate - [Theory] - [Bitmap Index]**

Bitmap indexes are most effective for:

A) High-cardinality columns (many distinct values like email addresses)
B) Low-cardinality columns (few distinct values like gender, status, boolean flags)
C) Primary key columns
D) Foreign key columns with frequent updates

**Answer: B**

**Explanation:**
Bitmap index: one bit-vector per distinct value. For gender (M/F): two bit-vectors of n bits each. Query WHERE gender='M': scan one bit-vector. AND/OR operations: bitwise operations on vectors — extremely fast. Low cardinality: few bit-vectors, efficient. High cardinality (email): one vector per email → n vectors of n bits = n² space, terrible. Also bad for frequent updates (must update all affected bits).

---

**Q33.12: Foundational - [Theory] - [Clustered vs Non-Clustered Index]**

A clustered index determines:

A) Which columns are indexed
B) The physical storage order of rows on disk
C) The compression algorithm used
D) The replication factor

**Answer: B**

**Explanation:**
Clustered index: rows stored on disk in index order. Only one per table (can't sort data two ways physically). Range scans are very fast (sequential disk reads). Non-clustered (secondary) index: separate structure pointing to data locations. Multiple secondary indexes per table. Primary key is usually the clustered index. In InnoDB, the clustered index IS the table (index-organized table).

---

**Q33.13: Advanced - [Theory] - [Bloom Filter in LSM]**

How do Bloom filters help LSM Tree read performance?

A) They compress the data stored in SSTables
B) They quickly determine if a key is definitely NOT in an SSTable, avoiding unnecessary disk reads
C) They sort the keys within each level
D) They cache frequently accessed values

**Answer: B**

**Explanation:**
LSM read: must check each level's SSTable for the key. Without Bloom filters: read from each level's SSTable = multiple disk I/Os. With Bloom filter per SSTable: check filter first (in memory). If filter says "not present": skip that SSTable entirely (no false negatives). False positive rate ~1% with proper sizing. 10 levels without Bloom: 10 I/Os. With Bloom: ~1.1 I/Os expected. Massive read improvement.

---

**Q33.14: Intermediate - [Theory] - [Query Optimization]**

What does a database query optimizer primarily try to minimize?

A) The amount of SQL code
B) The estimated cost of the query execution plan (usually I/O and CPU)
C) The number of tables referenced
D) The length of column names

**Answer: B**

**Explanation:**
Query optimizer: takes SQL query, considers many possible execution plans (different join orders, access methods, join algorithms), estimates cost of each using table statistics (row count, column cardinality, index availability), and picks cheapest plan. Cost model includes: disk I/Os, CPU comparisons, network transfer. Can choose hash join vs NLJ, index scan vs table scan, join order. This is why EXPLAIN is important for debugging performance.

---

**Q33.15: Expert - [Theory] - [B-Tree Concurrency]**

The latch-crabbing technique for concurrent B-Tree access works by:

A) Locking the entire tree during any modification
B) Acquiring latches top-down, releasing parent's latch once child is confirmed safe (won't split/merge)
C) Using optimistic concurrency without any locks
D) Partitioning the tree among threads

**Answer: B**

**Explanation:**
Latch crabbing (lock coupling): traverse tree acquiring latch on each node. Once child node is "safe" (not full for inserts, not half-empty for deletes), release parent's latch. Only keeps latches on nodes that might change. Key insight: most operations only modify leaf nodes → upper nodes rarely need exclusive locks. Optimistic variants: assume no splits, retry if wrong. Bw-Tree (used in SQL Server Hekaton): lock-free using CAS.

---

**Q33.16: Intermediate - [Complexity] - [Sort-Merge Join]**

Sort-merge join has what time complexity?

A) O(n + m) always
B) O(n × m) always
C) O(n log n + m log m) for unsorted inputs, O(n + m) for pre-sorted
D) O(log n × log m)

**Answer: C**

**Explanation:**
Sort-merge join: (1) Sort both tables by join key: O(n log n + m log m). (2) Merge scan: two pointers advance through sorted data: O(n + m). Total: dominated by sort step. If tables already sorted (clustered index on join column): skip sort → O(n + m). This is why sort-merge join is optimal when data arrives pre-sorted or when the result needs ordering (ORDER BY on join column).

---

**Q33.17: Foundational - [Theory] - [Index Selection]**

You have a query: `SELECT * FROM orders WHERE customer_id = 5 AND status = 'shipped'`. What index would be most helpful?

A) Index on (status) only
B) Index on (customer_id) only
C) Composite index on (customer_id, status)
D) No index needed

**Answer: C**

**Explanation:**
Composite index on (customer_id, status): directly narrows to matching rows using both conditions — most selective. Index on customer_id only: finds all orders for customer 5, then filters by status (less efficient if customer has many orders). Index on status only: 'shipped' may match many rows across all customers. Composite index follows the "leftmost prefix" rule: can also serve queries filtering only by customer_id.

---

**Q33.18: Advanced - [Theory] - [ARIES Recovery]**

The ARIES recovery protocol uses three phases:

A) Backup, Restore, Verify
B) Analysis, Redo, Undo
C) Lock, Process, Unlock
D) Parse, Optimize, Execute

**Answer: B**

**Explanation:**
ARIES (Algorithm for Recovery and Isolation Exploiting Semantics): (1) Analysis: scan WAL from last checkpoint, determine dirty pages and active transactions at crash time. (2) Redo: replay ALL logged changes (even for uncommitted transactions) to restore exact pre-crash state. (3) Undo: roll back uncommitted transactions by applying compensating log records (CLRs). "Redo history, undo losers." Gold standard for database recovery.

---

**Q33.19: Intermediate - [Theory] - [Covering Index]**

A "covering index" is beneficial because:

A) It covers all tables in the database
B) It includes all columns needed by the query, avoiding table row lookups
C) It covers all possible queries
D) It covers the primary key only

**Answer: B**

**Explanation:**
Covering index: contains all columns the query needs (SELECT list + WHERE + ORDER BY). Database can answer the query entirely from the index without fetching the actual table row (no "table lookup" or "bookmark lookup"). Example: INDEX on (customer_id, order_date, total) covers `SELECT order_date, total WHERE customer_id = 5`. Reduces I/O significantly. Also called "index-only scan."

---

**Q33.20: Expert - [Theory] - [Fractal Tree Index]**

How does a fractal tree index (used in TokuDB) differ from a standard B-Tree?

A) It uses hash functions instead of comparisons
B) It buffers writes at internal nodes, batching them for more efficient I/O
C) It stores data only in root nodes
D) It doesn't support range queries

**Answer: B**

**Explanation:**
Fractal tree: similar to B-Tree but each internal node has a message buffer. Writes go to root buffer, propagated down during flushes. Amortizes write I/O: O(log(N/B)/B) per insert vs B-Tree's O(log_B N). Much better write throughput on disk. Same read performance as B-Tree. Conceptually similar to buffer trees from external memory algorithms. TokuDB (now Percona): implemented this for MySQL. Trade-off: more complex implementation.

---

**Q33.21: Intermediate - [Theory] - [Page Replacement]**

Database buffer pools typically use which page replacement policy?

A) Random replacement
B) LRU or clock (approximation of LRU)
C) FIFO only
D) Always keep the most recently loaded page

**Answer: B**

**Explanation:**
Buffer pool: cache of disk pages in memory. When full, must evict a page. LRU (Least Recently Used): evict page not accessed for longest time. Works well for most access patterns. Clock algorithm: approximation of LRU with lower overhead (circular buffer with "referenced" bits). Some databases also use LRU-K (consider K-th most recent access) to handle sequential scan pollution. PostgreSQL uses clock algorithm.

---

**Q33.22: Foundational - [Theory] - [Transaction ACID]**

Which ACID property ensures that a committed transaction's changes survive system crashes?

A) Atomicity
B) Consistency
C) Isolation
D) Durability

**Answer: D**

**Explanation:**
Durability: once committed, changes are permanent even if the system crashes immediately after. Implemented via WAL — changes logged to durable storage before acknowledging commit. Atomicity: all-or-nothing. Consistency: database remains in valid state. Isolation: concurrent transactions don't interfere. Durability is specifically about surviving failures, guaranteed by write-ahead logging and checkpointing.

---

**Q33.23: Intermediate - [Theory] - [Index Scan vs Table Scan]**

When does the query optimizer choose a full table scan over using an available index?

A) Never — indexes are always faster
B) When the query returns a large fraction of the rows (high selectivity)
C) When the table has fewer than 10 rows
D) When the index is a composite index

**Answer: B**

**Explanation:**
Index scan: for each matching index entry, follow pointer to fetch row from table (random I/O). If query matches 50% of rows: 500K random I/Os (for 1M table) is WORSE than sequential table scan (few thousand sequential I/Os). Rule of thumb: index scan wins when selectivity < 5-15% of rows. Optimizer uses statistics to estimate selectivity and chooses accordingly. This is why high-cardinality columns benefit most from indexes.

---

**Q33.24: Advanced - [Theory] - [Write Amplification]**

Write amplification in LSM Trees refers to:

A) Amplifying the signal strength of writes to storage
B) Each logical write causing multiple physical writes due to repeated compaction
C) Writing data to multiple replicas simultaneously
D) Increasing the buffer size to accumulate more writes

**Answer: B**

**Explanation:**
In LSM Trees, a single inserted key-value pair may be written to disk multiple times: once when flushed from memtable, then again during each level of compaction (L0→L1, L1→L2, etc.). With T size ratio and L levels: write amplification ≈ T × L. For RocksDB with T=10, L=5: each byte written ~50 times total. SSDs have limited write endurance, so write amplification directly impacts hardware lifetime. Tuning T trades read vs write amplification.

---

**Q33.25: Expert - [Theory] - [Bw-Tree]**

The Bw-Tree (used in SQL Server Hekaton) achieves lock-free operations using:

A) Global locks with fine granularity
B) Delta records and compare-and-swap (CAS) on a mapping table
C) Pessimistic two-phase locking
D) Software transactional memory

**Answer: B**

**Explanation:**
Bw-Tree: latch-free B-Tree variant. Instead of in-place updates, append "delta records" to a page. Mapping table maps logical page IDs to physical pointers. Updates: CAS on mapping table entry to prepend delta. Consolidate deltas when chain gets long. No locks needed — all updates are atomic CAS. Designed for modern multi-core CPUs where lock contention is a bottleneck. Used in Azure SQL, SQL Server.

---

**Q33.26: Foundational - [Theory] - [Secondary Index]**

What is the main cost of having many secondary indexes on a table?

A) They slow down reads
B) They slow down writes (each insert/update must update all indexes)
C) They increase query complexity
D) They reduce table capacity

**Answer: B**

**Explanation:**
Each secondary index: separate data structure maintained alongside the table. Every INSERT: must add entry to EVERY index. Every UPDATE: may need to update affected indexes. Every DELETE: must remove from all indexes. A table with 5 indexes: insert is ~5× slower than with 0 indexes. Read queries benefit from indexes, but write-heavy workloads suffer. Index selection is a trade-off between read and write performance.

---

**Q33.27: Intermediate - [Theory] - [Consistent Hashing in Databases]**

Consistent hashing in distributed databases helps with:

A) Faster SQL query parsing
B) Minimizing data movement when adding/removing nodes
C) Compressing data more efficiently
D) Sorting data across nodes

**Answer: B**

**Explanation:**
Traditional hash partitioning: hash(key) mod N. Adding a node (N→N+1): almost ALL keys remap → massive data migration. Consistent hashing: keys and nodes on a hash ring. Adding a node: only keys between new node and its predecessor move → ~1/N of data migrates. Used in: DynamoDB, Cassandra, Redis Cluster, memcached. Enables elastic scaling without full reshuffling.

---

**Q33.28: Advanced - [Theory] - [Column Store vs Row Store]**

Column-oriented storage is better than row-oriented for:

A) OLTP workloads (frequent single-row inserts and lookups)
B) OLAP workloads (aggregation queries scanning few columns across many rows)
C) Small tables under 1000 rows
D) Workloads with frequent full-row updates

**Answer: B**

**Explanation:**
Column store: stores each column separately. Query `SELECT AVG(price) FROM sales`: reads ONLY the price column, not all 50 columns. Massive I/O savings for analytical queries. Plus: better compression (similar values together). Row store: all columns of a row together — ideal when reading/writing entire rows (OLTP). Column stores: Parquet, ClickHouse, Redshift, BigQuery. Row stores: PostgreSQL, MySQL, Oracle (traditional).

---

**Q33.29: Intermediate - [Trace] - [B-Tree Insertion]**

Insert key 25 into a B-Tree (order 3, max 2 keys per node) with root [10, 20] and children: [5,7], [12,15], [22,30]. What happens?

A) 25 goes into the rightmost leaf [22,30] with no split needed
B) Key 25 causes [22,30] to overflow → split into [22,25] and [30], promoting 25 to root
C) Key 25 replaces 22 in the leaf
D) Key 25 is added to the root node

**Answer: B**

**Explanation:**
Insert 25: search → rightmost leaf [22,30]. Adding 25: [22,25,30] overflows (max 2 keys). Split: left [22], right [30], promote middle key 25 to parent. Root becomes [10,20,25] — but root max is also 2! Root overflows → split root: left [10], right [25], new root [20]. Height increases by 1. B-Trees grow from the root upward, maintaining balance.

---

**Q33.30: Foundational - [Theory] - [Database Indexing Trade-off]**

What is the fundamental trade-off of database indexing?

A) Speed vs accuracy
B) Faster reads vs slower writes and more storage
C) Security vs performance
D) Simplicity vs functionality

**Answer: B**

**Explanation:**
Indexes speed up SELECT queries (avoid full table scan) but: (1) Slow down INSERT/UPDATE/DELETE (must maintain index), (2) Use additional disk space (index data structures), (3) Need maintenance (rebalancing, vacuuming). The DBA must balance read vs write workload. Over-indexing: writes become bottleneck. Under-indexing: reads scan full tables. Profile actual queries to decide which indexes to create.

---

## Chapter 33 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 8 | B-Tree purpose, B+ Tree, LSM motivation, clustered index, ACID, index trade-offs |
| Intermediate | 13 | Compaction, hash index, join algorithms, bitmap, query optimization, page replacement |
| Advanced | 6 | NLJ vs hash, Bloom in LSM, ARIES, write amplification, column store |
| Expert | 3 | B-Tree concurrency, fractal tree, Bw-Tree |

**Total MCQs: 30**

**Answer Distribution: A=7, B=14, C=6, D=3 (~25% each)**

**Question Types: Theory=26, Trace=1, Complexity=2, Code=0**

**Next:** Chapter 34 - System Design & Distributed Systems
