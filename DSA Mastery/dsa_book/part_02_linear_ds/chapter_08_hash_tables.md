# Chapter 8: Hash Tables

**Target:** 75 MCQs | **Distribution:** 18 Foundational, 30 Intermediate, 20 Advanced, 7 Expert

---

**Q8.1: Foundational - [Theory] - [Hash Table Basics]**

A hash table provides:

A) Sorted order of elements
B) Average O(1) insert, delete, and search
C) O(log n) guaranteed operations
D) Sequential access only

**Answer: B**

**Explanation:**
Hash table: key-value storage with hash function mapping keys to indices. Average case O(1) for insert, delete, lookup. Worst case O(n) with collisions. No ordering guaranteed. Contrast with balanced trees (O(log n), sorted), arrays (O(1) index, O(n) search). Hash tables are the most commonly used data structure for associative arrays.

---

**Q8.2: Foundational - [Theory] - [Hash Function]**

A hash function:

A) Maps keys to array indices
B) Should distribute keys uniformly
C) Should be deterministic (same key → same hash)
D) All of the above

**Answer: D**

**Explanation:**
Hash function h(key) → index. Properties: (1) Deterministic: h(k) always same for same k. (2) Uniform: distributes keys evenly across table to minimize collisions. (3) Fast: O(1) computation. (4) Minimizes collisions: different keys should have different hashes. Good hash functions critical for performance.

---

**Q8.3: Foundational - [Theory] - [Collision]**

A collision occurs when:

A) Two different keys hash to same index
B) Two hash tables conflict
C) Hash function returns error
D) Table is empty

**Answer: A**

**Explanation:**
Collision: h(k₁) = h(k₂) for k₁ ≠ k₂. Inevitable by pigeonhole principle when keys > slots. Collision resolution strategies: chaining (store multiple items at index), open addressing (probe for empty slot). Load factor α = n/m (items/slots) affects collision probability.

---

**Q8.4: Foundational - [Theory] - [Collision Resolution]**

Common collision resolution methods:

A) Chaining and open addressing
B) Linear probing and quadratic probing
C) Double hashing
D) All of the above

**Answer: D**

**Explanation:**
Chaining: each bucket stores linked list of collided items. Open addressing: all items in table, probe sequence finds empty slot. Linear probing: try h(k), h(k)+1, h(k)+2... Quadratic: try h(k), h(k)+1², h(k)+2²... Double hashing: try h(k), h(k)+h₂(k), h(k)+2×h₂(k)...

---

**Q8.5: Foundational - [Complexity] - [Chaining]**

Separate chaining with n items in m buckets:

A) Worst case O(n) search
B) Average case O(1 + α) where α = n/m
C) Insert is O(1)
D) All of the above

**Answer: D**

**Explanation:**
Chaining: linked list per bucket. Worst: all items in one bucket, O(n) search. Average: assuming uniform hashing, chain length = α = n/m. Search: O(1) hash + O(α) traverse. Insert: O(1) add to head. α = load factor, typically kept ≤ 1 for chaining.

---

**Q8.6: Intermediate - [Theory] - [Load Factor]**

Load factor α = n/m:

A) Higher α means more collisions
B) Typically kept below 0.75 for open addressing
C) Resizing occurs when α exceeds threshold
D) All of the above

**Answer: D**

**Explanation:**
Load factor measures table fullness. Higher α → more collisions → worse performance. Open addressing: α < 1 required. Typical thresholds: 0.75 for Java HashMap, 0.9 for Python dict. When exceeded: resize (rehash) to larger table, O(n) but amortized O(1).

---

**Q8.7: Intermediate - [Theory] - [Resizing]**

Hash table resizing:

A) Create new larger table (typically 2× size)
B) Rehash all items to new table
C) Amortized O(1) operations
D) All of the above

**Answer: D**

**Explanation:**
Resize when load factor exceeds threshold. New size usually 2× (keeps hash computations simple). Rehash: for each item, compute new hash, insert. O(n) time. Expensive but infrequent—amortized analysis shows average O(1).

---

**Q8.8: Intermediate - [Theory] - [Linear Probing]**

Linear probing: collision resolution probes:

A) h(k), h(k)+1, h(k)+2, ... (mod m)
B) Simple but suffers from primary clustering
C) Good cache locality
D) All of the above

**Answer: D**

**Explanation:**
Linear probing: sequential search for empty slot. Simple, good cache locality (consecutive accesses). Problem: primary clustering—occupied slots cluster together, increasing probe length. Analysis: successful search average (1 + 1/(1-α))/2, unsuccessful (1 + 1/(1-α)²)/2.

---

**Q8.9: Intermediate - [Theory] - [Quadratic Probing]**

Quadratic probing:

A) h(k,i) = (h'(k) + c₁i + c₂i²) mod m
B) Reduces primary clustering
C) May not find empty slot even if one exists
D) All of the above

**Answer: D**

**Explanation:**
Quadratic: probe sequence spreads out. Reduces primary clustering but secondary clustering remains. Problem: may cycle without finding empty slot even if table not full. Table size should be prime, and α < 0.5 for guaranteed insertion.

---

**Q8.10: Advanced - [Theory] - [Double Hashing]**

Double hashing:

A) h(k,i) = (h₁(k) + i × h₂(k)) mod m
B) Uses two hash functions
C) Best open addressing: less clustering
D) All of the above

**Answer: D**

**Explanation:**
Double hashing: probe sequence depends on key via second hash. h₂(k) must be ≠ 0, relatively prime to table size. Different keys have different step sizes, eliminating clustering. Best open addressing method theoretically.

---

**Q8.11: Intermediate - [Trace] - [Linear Probing]**

Table size 7, insert 10, 20, 30 with h(k)=k%7:

A) 10%7=3, slot 3: [_,_,_,10,_,_,_]
B) 20%7=6, slot 6: [_,_,_,10,_,_,20]
C) 30%7=2, slot 2: [_,_,30,10,_,_,20]
D) No collisions

**Answer: D**

**Explanation:**
h(10)=3, h(20)=6, h(30)=2. All different, no probing needed. Shows uniform distribution when no collisions.

---

**Q8.12: Advanced - [Trace] - [Double Hashing]**

Table size 7, h₁(k)=k%7, h₂(k)=1+(k%6), insert 10, 24:

A) h₁(10)=3, insert at 3
B) h₁(24)=3, collision. h₂(24)=1. Probe: 3+1=4
C) Insert 24 at 4
D) Probes: 1 for 10, 2 for 24

**Answer: D**

**Explanation:**
10: h₁=3, empty, insert. 24: h₁=3 occupied, h₂=1+(24%6)=1, probe (3+1)%7=4, empty, insert. Different step sizes reduce clustering vs linear probing.

---

**Q8.13: Intermediate - [Theory] - [HashMap vs HashSet]**

HashMap vs HashSet:

A) HashMap stores key-value pairs
B) HashSet stores only keys (no duplicates)
C) HashSet typically backed by HashMap
D) All of the above

**Answer: D**

**Explanation:**
HashMap: dictionary, key→value. HashSet: set of unique elements. Java's HashSet backed by HashMap (dummy values). Operations: HashMap put/get/remove, HashSet add/remove/contains. Both O(1) average.

---

**Q8.14: Intermediate - [Theory] - [String Hashing]**

Rolling hash for string "abc":

A) hash = (((a)×26 + b)×26 + c)
B) Enables O(1) substring hash with precomputation
C) Used in Rabin-Karp string matching
D) All of the above

**Answer: D**

**Explanation:**
Polynomial rolling hash: H(s) = Σ s[i] × b^(n-1-i). Precompute powers of b and prefix hashes for O(1) substring hash. Used in Rabin-Karp, duplicate detection. Choose large prime mod to reduce collisions.

---

**Q8.15: Advanced - [Theory] - [Consistent Hashing]**

Consistent hashing for distributed caching:

A) Hash servers and keys to same ring
B) Key maps to next server clockwise
C) Adding/removing server affects only adjacent keys
D) All of the above

**Answer: D**

**Explanation:**
Consistent hashing: hash both servers and keys to points on a ring. Key assigned to first server clockwise. Adding/removing server: only keys between previous and new server move. Virtual nodes improve distribution. Used in memcached, DynamoDB, CDN load balancing.

---

**Q8.16: Advanced - [Trace] - [Consistent Hashing]**

Ring with servers A(20), B(50), C(80), keys hash to 10, 30, 60, 90:

A) Key 10 → A (next clockwise from 10 is 20-A)
B) Key 30 → B (next from 30 is 50-B)
C) Key 60 → C, Key 90 → A (wraps around)
D) All correct

**Answer: D**

**Explanation:**
Consistent hash ring: keys assigned to next server clockwise. 10→A(20), 30→B(50), 60→C(80), 90→A(20 wrapping). If B removed: 30 now goes to C. Only key 30 moves. Minimal disruption on topology changes.

---

**Q8.17: Advanced - [Theory] - [Cuckoo Hashing]**

Cuckoo hashing:

A) Two (or more) hash tables
B) Each key in one of two positions: h₁(key) or h₂(key)
C) Displacement chain may need rehash
D) All of the above

**Answer: D**

**Explanation:**
Cuckoo: two tables (or two hash functions). Insert: try h₁, if occupied, evict resident, insert it at alternate location, continue. May cycle—if so, rehash. Lookup: check both positions, O(1) worst case. Space-efficient, fast lookups.

---

**Q8.18: Expert - [Trace] - [Cuckoo Insertion]**

h₁(x)=x%5, h₂(x)=x%7, insert 10, 20:

A) h₁(10)=0, insert T1[0]=10
B) h₁(20)=0, occupied. h₂(20)=6, T2[6]=20
C) Insert succeeds without displacement
D) All of the above

**Answer: D**

**Explanation:**
10: h₁=0, T1 empty, insert. 20: h₁=0 occupied, h₂=6, T2 empty, insert. No displacement needed. When both positions occupied, displacement chain begins.

---

**Q8.19: Advanced - [Theory] - [Robin Hood Hashing]**

Robin Hood hashing:

A) Variation of linear probing
B) Steal from "rich" (far from home) to give to "poor"
C) Reduces variance in probe lengths
D) All of the above

**Answer: D**

**Explanation:**
Robin Hood: when inserting, if existing item is farther from home, swap them. Reduces variance in probe distances. Lookup: find key or empty slot with probe distance less than current's.

---

**Q8.20: Advanced - [Theory] - [Perfect Hashing]**

Perfect hashing:

A) No collisions for static set of keys
B) Two-level: first hash to bucket, second hash within bucket
C) O(1) worst case lookup
D) All of the above

**Answer: D**

**Explanation:**
Perfect hashing: guaranteed O(1) worst case, no collisions. Static: keys known in advance. FKS scheme: first level hashes to buckets. Each bucket has own hash function. Size of bucket's table = size² to guarantee no collisions. Space O(n), construction O(n).

---

**Q8.21: Expert - [Theory] - [Universal Hashing]**

Universal hash family:

A) For random h from family, P(h(x)=h(y)) ≤ 1/m for x≠y
B) Guarantees expected O(1) regardless of input
C) Prevents worst-case attack
D) All of the above

**Answer: D**

**Explanation:**
Universal hashing: family of hash functions where collision probability is low for any distinct keys. Choose random function from family. Prevents collision attacks where adversary crafts keys all hashing to same bucket. Important for security (hash tables in network services).

---

**Q8.22: Expert - [Theory] - [Hash Flooding Attack]**

Hash flooding attack:

A) Adversary sends keys with same hash
B) Causes O(n) lookup per operation
C) Denial of service on hash-based systems
D) All of the above

**Answer: D**

**Explanation:**
Attack: knowing hash function, adversary sends many colliding keys. All hash to same bucket, chain length n, O(n) per operation. Defenses: universal hashing, randomized seeds, SipHash (cryptographic hash for short inputs).

---

**Q8.23: Intermediate - [Application] - [Two Sum]**

Two sum: find indices where nums[i] + nums[j] = target:

A) Hash map: value→index
B) For each num, check if target-num in map
C) O(n) time, O(n) space
D) All of the above

**Answer: D**

**Explanation:**
Hash map approach: for each nums[i], check if (target - nums[i]) in map. If yes, return indices. Else add nums[i] to map. Single pass, O(n). Classic interview problem demonstrating hash map for O(1) lookups.

---

**Q8.24: Intermediate - [Application] - [Anagram Check]**

Check if two strings are anagrams:

A) Sort and compare: O(n log n)
B) Count characters with hash map: O(n)
C) Compare frequency arrays: O(n) with O(1) space for fixed alphabet
D) Both B and C

**Answer: D**

**Explanation:**
Hash map: count character frequencies for both strings, compare. O(n) time, O(k) space for k unique characters. For lowercase English (26 letters), fixed array [26] works, O(1) space.

---

**Q8.25: Intermediate - [Application] - [First Unique Character]**

First non-repeating character in string:

A) Hash map: count occurrences
B) Second pass: find first with count 1
C) O(n) time, O(k) space
D) All of the above

**Answer: D**

**Explanation:**
Two passes: first count all characters, second find first with count 1. Hash map or array for fixed alphabet. O(n) time, O(k) space where k = alphabet size.

---

**Q8.26: Advanced - [Theory] - [LRU Cache with HashMap]**

LRU cache O(1) operations:

A) HashMap: key→node reference
B) Doubly linked list: order by recency
C) On access: move to front. On eviction: remove from back
D) All of the above

**Answer: D**

**Explanation:**
Hash map gives O(1) lookup. List gives O(1) order update and eviction. Combined: O(1) get and put. get: hash to node, move to front. put: if exists update, else add to front. If capacity exceeded, remove tail.

---

**Q8.27: Advanced - [Trace] - [LRU Operations]**

LRU capacity 2: put(1,1), put(2,2), get(1), put(3,3), get(2):

A) put(1), put(2): [1,2]
B) get(1): 1→front, [2,1]. put(3): evict 2, [1,3]
C) get(2): not found, return -1
D) All correct

**Answer: D**

**Explanation:**
Trace: After initial puts: list [1,2]. get(1): move to front, [2,1]. put(3): capacity full, evict 2 (back), [1,3]. get(2): 2 was evicted, not found. Demonstrates LRU semantics.

---

**Q8.28: Expert - [Theory] - [LFU Cache]**

LFU (least frequently used) cache:

A) Track access frequency per key
B) Evict minimum frequency, tie-break by recency
C) Can use hash map + multiple doubly linked lists
D) All of the above

**Answer: D**

**Explanation:**
LFU evicts least frequently accessed. Ties broken by LRU. Data structure: hash map key→(value, frequency, node). Multiple doubly linked lists: one per frequency. Min frequency tracked. O(1) operations.

---

**Q8.29: Advanced - [Theory] - [Trie vs Hash]**

When to use Trie over Hash:

A) Prefix searches (auto-complete)
B) Ordered iteration
C) Space efficiency with common prefixes
D) All of the above

**Answer: D**

**Explanation:**
Trie (prefix tree): tree where path spells key. Enables prefix searches, longest prefix match, ordered iteration. Hash: O(1) exact match, no ordering. Trie time: O(key length) vs O(1) hash.

---

**Q8.30: Intermediate - [Application] - [Group Anagrams]**

Group anagrams together:

A) Hash each word: sorted string as key
B) Map key→list of anagrams
C) O(n × k log k) where k = word length
D) All of the above

**Answer: D**

**Explanation:**
Key insight: anagrams sorted become same string. "eat", "tea" → "aet". Hash map: key="aet", value=["eat","tea","ate"]. O(n × k log k) for sorting each word. Alternative: count array as key O(n × k).

---

**Q8.31: Advanced - [Theory] - [Bloom Filter]**

Bloom filter:

A) Probabilistic data structure for set membership
B) May have false positives, no false negatives
C) Multiple hash functions, bit array
D) All of the above

**Answer: D**

**Explanation:**
Bloom filter: bit array of m bits, k hash functions. Insert: set bits h₁(x), h₂(x), ..., hₖ(x). Query: check if all bits set. If all set: probably in set (may be false positive). If any bit 0: definitely not in set. Space-efficient: ~10 bits per element for 1% false positive.

---

**Q8.32: Advanced - [Trace] - [Bloom Filter]**

Bloom filter m=10 bits, k=2, insert "a", "b":

A) h₁(a)=2, h₂(a)=5: set bits 2, 5
B) h₁(b)=5, h₂(b)=8: set bits 5, 8
C) Query "a": bits 2,5 set → yes (true positive)
D) Query "c" with h₁=2, h₂=8: false positive possible

**Answer: D**

**Explanation:**
Insert a: bits {2,5} = 1. Insert b: bits {5,8} = 1. Query a: check {2,5}, both 1 → yes. Query c with h₁=2, h₂=8: bits {2,8}, both 1 → yes! But c never inserted. False positive because 2 set by a, 8 by b.

---

**Q8.33: Expert - [Theory] - [Count-Min Sketch]**

Count-Min sketch for frequency estimation:

A) 2D array: d rows × w columns
B) d hash functions, update all rows
C) Query returns minimum count across rows
D) All of the above

**Answer: D**

**Explanation:**
Count-Min sketch: d × w counter table. Update(x): for each row i, increment cms[i][hᵢ(x)]. Query(x): return minᵢ cms[i][hᵢ(x)]. Returns count + overestimate (due to hash collisions). Used in network monitoring, streaming analytics.

---

**Q8.34: Intermediate - [Application] - [Longest Substring Without Repeating]**

Longest substring without repeating characters:

A) Sliding window with hash set
B) Expand right, contract left when duplicate found
C) O(n) time
D) All of the above

**Answer: D**

**Explanation:**
Sliding window: expand right pointer, add to hash set. If char in set, contract left until char removed. Track max window size. Hash set provides O(1) membership check. O(n) time as each pointer moves at most n steps.

---

**Q8.35: Advanced - [Theory] - [Hash Map Iteration Order]**

Hash map iteration order:

A) Not guaranteed (hash based)
B) May change between runs (hash randomization)
C) LinkedHashMap preserves insertion order
D) All of the above

**Answer: D**

**Explanation:**
Standard hash map: iteration order arbitrary. Hash randomization makes order unpredictable across runs. LinkedHashMap maintains insertion or access order. Never rely on hash map order.

---

**Q8.36: Intermediate - [Application] - [Subarray Sum Equals K]**

Subarray sum equals k: count subarrays with sum k:

A) Hash map: prefix sum → frequency
B) For each prefix, check if prefix - k exists
C) O(n) time
D) All of the above

**Answer: D**

**Explanation:**
Prefix sum approach: sum[i..j] = prefix[j+1] - prefix[i]. For each prefix p, need count of prefixes equal to p - k. Hash map stores prefix frequencies seen so far. O(n) time, O(n) space.

---

**Q8.37: Advanced - [Theory] - [ConcurrentHashMap]**

Java's ConcurrentHashMap:

A) Segmented: multiple locks on segments
B) Lock-free reads (volatile)
C) JDK 8+: single array with CAS and synchronized on first node
D) All of the above

**Answer: D**

**Explanation:**
ConcurrentHashMap: JDK 7 had segments, JDK 8 uses single array with CAS for empty bins, synchronized on first node. Lock-free get. Better concurrency than Hashtable (synchronized methods).

---

**Q8.38: Expert - [Theory] - [Hopscotch Hashing]**

Hopscotch hashing:

A) Open addressing with bounded probe sequence
B) Neighbourhood of size H around home position
C) Item in neighbourhood or displaced within H
D) All of the above

**Answer: D**

**Explanation:**
Hopscotch: each item in neighbourhood of size H from home. Insert: if home empty, place there. Else find empty within H, swap items to make room. Bitmap per bucket tracks which neighbourhood slots occupied. O(1) lookup.

---

**Q8.39: Advanced - [Theory] - [Hopscotch vs Cuckoo]**

Hopscotch vs Cuckoo hashing:

A) Both use multiple hash functions
B) Hopscotch: bounded neighbourhood, Cuckoo: unbounded chains
C) Hopscotch lookup checks H consecutive slots
D) All of the above

**Answer: D**

**Explanation:**
Both use multiple locations per key. Hopscotch: bounded probe length (H), guaranteed lookup time by checking H consecutive slots. Cuckoo: eviction chains potentially unbounded. Hopscotch simpler implementation, no rehash needed usually.

---

**Q8.40: Expert - [Theory] - [Quotient Filter]**

Quotient filter (compact hash table):

A) Compact alternative to Bloom filter with deletion
B) Stores fingerprints (hash quotients) with metadata
C) Supports insert, delete, query
D) All of the above

**Answer: D**

**Explanation:**
Quotient filter: hash → quotient (index) and remainder (fingerprint). Store fingerprints in slots with run/bucket metadata. Supports deletion (unlike Bloom filter). ~10% space overhead. Used in databases (LevelDB, RocksDB).

---

**Q8.41: Intermediate - [Application] - [Intersection of Two Arrays]**

Intersection of two arrays:

A) Sort both, two pointers: O(n log n + m log m)
B) Hash set of first, check second: O(n + m)
C) If one array much smaller, hash smaller
D) All of the above

**Answer: D**

**Explanation:**
Approach 1: sort, two pointers. Approach 2: hash set. Approach 3: hash smaller for space efficiency. Hash set usually simplest and fastest for unsorted.

---

**Q8.42: Advanced - [Theory] - [External Hashing]**

External memory hash table:

A) Hash to buckets stored on disk
B) Buckets overflow to chained pages
C) Extendible hashing: directory doubles
D) All of the above

**Answer: D**

**Explanation:**
External hashing: hash to bucket, buckets on disk pages. Extendible hashing: directory of bucket pointers. When bucket overflows, split (if local depth = global depth, double directory). Used in databases.

---

**Q8.43: Expert - [Theory] - [Extendible Hashing]**

Extendible hashing directory doubling:

A) Global depth increases
B) Split bucket, redistribute based on additional hash bit
C) Directory doubles when local depth = global depth
D) All of the above

**Answer: D**

**Explanation:**
Extendible: hash prefix determines bucket. When bucket full, if local < global, split (redistribute, increase local). If local = global, double directory (global++), then split. Amortized O(1) insert. Used in database systems.

---

**Q8.44: Intermediate - [Application] - [Copy List with Random Pointer]**

Deep copy list with random pointer:

A) Hash map old→new nodes
B) First pass: create copies, second pass: set next/random
C) O(n) time, O(n) space
D) All of the above

**Answer: D**

**Explanation:**
Hash approach: traverse old list, create copy nodes, store mapping old→new. Second pass: set next and random using map. O(n) time and space. Alternative O(1) space: interleave copies, set random, then separate.

---

**Q8.45: Advanced - [Theory] - [Hash Join]**

Database hash join:

A) Build hash table on smaller relation
B) Probe with larger relation
C) O(n + m) average
D) All of the above

**Answer: D**

**Explanation:**
Hash join: build hash table on smaller relation, then scan larger relation, hash probe to find matches. O(n + m) vs sort-merge O(n log n + m log m). Used when tables unsorted.

---

**Q8.46: Advanced - [Application] - [Word Pattern]**

Word pattern "abba" matches "dog cat cat dog":

A) Bijection between pattern letters and words
B) Hash map: letter→word and word→letter
C) Check consistency both directions
D) All of the above

**Answer: D**

**Explanation:**
Bijection required: each letter maps to one word, each word to one letter. Two hash maps or one map + set. O(n) time. Hash tables naturally handle bijection verification.

---

**Q8.47: Expert - [Theory] - [Minimal Perfect Hashing]**

Minimal perfect hash function:

A) Maps n keys to n consecutive integers (0..n-1)
B) No collisions, no wasted space
C) Static: all keys known in advance
D) All of the above

**Answer: D**

**Explanation:**
Minimal perfect hash: bijection from keys to [0,n-1], no gaps, no collisions. Static construction. Used for read-only dictionaries, perfect hash for keywords in compilers. Space-efficient: ~2-3 bits per key.

---

**Q8.48: Expert - [Theory] - [Hashing in Distributed Systems]**

Consistent hashing variants:

A) Rendezvous hashing: highest hash wins
B) Jump consistent hash: minimal memory
C) Maglev hashing: load balancing
D) All of the above

**Answer: D**

**Explanation:**
Rendezvous: compute hash(key, server) for each server, choose max. Jump consistent: O(1) memory, O(log n) computation. Maglev: Google, fast lookup table for consistent hashing with load balancing. Critical for distributed caching and load balancing.

---

**Q8.49: Intermediate - [Application] - [Isomorphic Strings]**

Check if strings isomorphic:

A) Character mapping must be bijective
B) Hash map for char→char both directions
C) Pattern matching with two maps
D) All of the above

**Answer: D**

**Explanation:**
Isomorphic: one-to-one character correspondence. Map s[i]→t[i], check consistency. Also check t[i]→s[i]. Use two hash maps or one map + set. O(n) time.

---

**Q8.50: Advanced - [Trace] - [Fraction to Recurring Decimal]**

Convert fraction to decimal: hash map tracks remainders:

A) Long division: quotient digit, remainder × 10
B) Hash map: remainder→position in result
C) When remainder repeats, insert '(' at previous position
D) All of the above

**Answer: D**

**Explanation:**
1/6: 1÷6, quotient 0, remainder 1. 10÷6, quotient 1, remainder 4. 40÷6, quotient 6, remainder 4. Remainder 4 repeats! Hash map had 4→position 2. Result: 0.1(6). Hash map detects cycle start for recurring decimal.

---

**Q8.51: Expert - [Theory] - [SipHash]**

SipHash for short inputs:

A) Cryptographic hash function
B) Prevents hash flooding attacks
C) Used in Python, Ruby, Rust hash tables
D) All of the above

**Answer: D**

**Explanation:**
SipHash: pseudorandom function, fast, secure against hash flooding. Secret key makes collisions unpredictable. Python 3.3+, Ruby, Rust use SipHash. Prevents DoS via hash collisions.

---

**Q8.52: Expert - [Theory] - [Swiss Table]**

Swiss table (Google's hash map):

A) Open addressing with SIMD
B) Metadata byte per slot (empty/deleted/full)
C) Parallel check of 16 slots with one instruction
D) All of the above

**Answer: D**

**Explanation:**
Swiss table (absl::flat_hash_map): open addressing, metadata byte per slot. SIMD (SSE2) checks 16 slots in parallel. Robin Hood hashing. Compact, fast, cache-friendly. Modern hash table design optimized for current hardware.

---

**Q8.53: Intermediate - [Application] - [Happy Number]**

Happy number: repeatedly sum square of digits, eventually 1:

A) Hash set to detect cycle
B) If cycle without 1, not happy
C) Floyd's cycle detection also works
D) All of the above

**Answer: D**

**Explanation:**
Process: 19 → 82 → 68 → 100 → 1 → happy. Unhappy numbers enter cycle (4 → 16 → 37 → 58 → 89 → 145 → 42 → 20 → 4). Hash set detects cycle. Floyd's tortoise-hare also works (O(1) space).

---

**Q8.54: Advanced - [Theory] - [Identity HashCode]**

System.identityHashCode:

A) Default hashCode from Object
B) Based on memory address or synthetic value
C) Not overridden, unique per object
D) All of the above

**Answer: D**

**Explanation:**
Java's Object.hashCode(): native implementation, often memory address. identityHashCode returns this even if hashCode overridden. Used for identity-based collections (IdentityHashMap). Distinct from logical equality.

---

**Q8.55: Advanced - [Application] - [Contains Duplicate II]**

Contains duplicate within k distance:

A) Hash map: value→last index
B) For each num, check if in map and index diff ≤ k
C) O(n) time, O(min(n,k)) space
D) All of the above

**Answer: D**

**Explanation:**
Hash map tracks last seen index. For nums[i], if in map and i - map[nums[i]] ≤ k, return true. Update map[nums[i]] = i. Space O(min(n,k)) by maintaining sliding window of indices.

---

**Q8.56: Expert - [Theory] - [Hash Table Security]**

SipHash for short inputs:

A) Cryptographic hash function
B) Prevents hash flooding attacks
C) Used in Python, Ruby, Rust hash tables
D) All of the above

**Answer: D**

**Explanation:**
SipHash: pseudorandom function, fast, secure against hash flooding. Secret key makes collisions unpredictable to attacker. Python 3.3+, Ruby, Rust use SipHash-2-4 or similar. Prevents DoS via hash collisions.

---

**Q8.57: Expert - [Theory] - [Swiss Table]**

Swiss table (Google's hash map):

A) Open addressing with SIMD
B) Metadata byte per slot (empty/deleted/full)
C) Parallel check of 16 slots with one instruction
D) All of the above

**Answer: D**

**Explanation:**
Swiss table (absl::flat_hash_map): open addressing, metadata byte per slot indicates state. SIMD (SSE2) checks 16 slots in parallel for match. Robin Hood hashing for better cache behavior. Compact, fast, cache-friendly. Modern hash table design optimized for current hardware (cache lines, SIMD).

---

**Q8.58: Intermediate - [Application] - [Top K Frequent]**

Top K frequent elements:

A) Hash map: count frequencies O(n)
B) Min heap of size k: O(n log k)
C) Or quickselect on frequencies: O(n) average
D) All of the above

**Answer: D**

**Explanation:**
Hash for frequencies. Then: (1) heap of size k, O(n log k). (2) quickselect for k-th largest, then collect top k, O(n) average. (3) bucket sort by frequency if range small. Hash table enables frequency counting, then various methods for top-k extraction.

---

**Q8.59: Advanced - [Theory] - [Ordered Statistics in Hash]**

Order statistics in hash tables:

A) Standard hash: O(n) to find k-th element
B) Tree-based hash (LinkedHashMap) can maintain order
C) Order statistic tree: O(log n) operations
D) All of the above

**Answer: D**

**Explanation:**
Standard hash tables don't support order statistics efficiently. Tree-based: O(log n) ordered operations. Order statistic tree: augment tree with subtree sizes. For hash-based, need hybrid or accept O(n) scan.

---

**Q8.60: Expert - [Theory] - [Thread-Local Hash]**

Thread-local hash tables:

A) Each thread has own hash table
B) No synchronization needed for reads/writes
C) Merge at checkpoints or on demand
D) All of the above

**Answer: D**

**Explanation:**
Thread-local: avoid synchronization overhead. Each thread owns hash table. Writes local, reads may check local then global. Merge strategy for shared view. Used in high-performance systems: databases, game engines.

---

**Q8.61: Intermediate - [Application] - [Jewels and Stones]**

Count jewels in stones:

A) Hash set of jewels
B) Count stones in set
C) O(jewels + stones)
D) All of the above

**Answer: D**

**Explanation:**
Hash set for O(1) membership. Count stones present in jewel set. O(J + S) time. Bitset for small alphabets. Demonstrates basic hash set usage for membership testing.

---

**Q8.62: Advanced - [Theory] - [Python Dictionary Evolution]**

Python dictionary (3.6+):

A) Compact dict: entries array + index array
B) Preserves insertion order
C) Faster iteration, better cache locality
D) All of the above

**Answer: D**

**Explanation:**
Python 3.6: new dict implementation. Entries stored in dense array (insertion order). Sparse index array maps hash to entry index. Preserves order. Better cache locality for iteration. Smaller memory.

---

**Q8.63: Expert - [Theory] - [Frozen Hash]**

Frozen/immutable hash table:

A) No modifications after creation
B) Can be shared safely across threads
C) Can be used as dict key or set element
D) All of the above

**Answer: D**

**Explanation:**
Immutable/frozen hash tables: thread-safe by construction, cacheable, hashable themselves (can be keys). Building new version shares structure with old (path copying). Important for functional programming and concurrent systems.

---

**Q8.64: Advanced - [Application] - [4Sum II]**

Four arrays, count tuples where A[i]+B[j]+C[k]+D[l]=0:

A) O(n⁴) brute force
B) Hash map of A+B sums, check -(C+D) in map: O(n²)
C) O(n²) time, O(n²) space
D) Both B and C

**Answer: D**

**Explanation:**
Meet-in-the-middle: hash all n² sums from A+B. For each of n² C+D pairs, check if negative exists in hash. O(n²) total. Classic technique reducing complexity from 4D to 2D+2D.

---

**Q8.65: Expert - [Theory] - [SIMD Hash]**

SIMD-accelerated hash lookups:

A) Check multiple buckets in parallel
B) Swiss table uses SSE2 for 16-way parallel
C) Reduces branch misprediction
D) All of the above

**Answer: D**

**Explanation:**
SIMD: process 128 or 256 bits at once. Hash: load metadata for 16 buckets, compare with target in one instruction. No branches, no misprediction penalty. Swiss table, F14 (Facebook) use this.

---

**Q8.66: Intermediate - [Application] - [Bulls and Cows]**

Bulls and Cows game:

A) Bulls: correct digit in correct position
B) Cows: correct digit in wrong position
C) Hash map count unmatched digits
D) All of the above

**Answer: D**

**Explanation:**
Algorithm: scan for bulls first (match position), decrement counts. Then scan for cows: if not bull and char in map with count > 0, increment cows, decrement count. Hash map tracks available digits. O(n) time.

---

**Q8.67: Advanced - [Theory] - [Robin Hood Variants]**

Backshift deletion in Robin Hood hashing:

A) On delete, shift elements backward if closer to home
B) Maintains probe sequence invariant
C) Improves over tombstone approach
D) All of the above

**Answer: D**

**Explanation:**
Backshift: when deleting, look at next elements. If next element's probe distance > 0, shift it back one slot, continue. Fills holes and maintains invariant. Better than tombstone markers which cause "deleted" clusters.

---

**Q8.68: Expert - [Theory] - [Hash Displace and Compress]**

Hash, displace and compress (CHD):

A) Perfect hashing construction
B) Displace: adjust hash function per bucket
C) Compress: compact representation
D) All of the above

**Answer: D**

**Explanation:**
CHD: build buckets based on first hash. For buckets with multiple items, find displacement (seed) such that second hash has no collisions. Store displacement per bucket. Construction O(n), space ~2.07 bits/key for minimal perfect hashing.

---

**Q8.69: Expert - [Theory] - [Summary]**

Hash table design considerations:

A) Load factor, collision resolution, hash function quality
B) Memory layout, cache performance, resize strategy
C) Concurrency, security, persistence
D) All critical for production systems

**Answer: D**

**Explanation:**
Production hash tables balance: basic design (load factor, probing vs chaining), performance (cache, SIMD, memory), robustness (concurrency, security, resizing). Modern implementations optimize all these.

---

**Q8.70: Intermediate - [Application] - [Randomized Set]**

Insert, remove, getRandom all O(1):

A) Hash map: value→index in array
B) Array: stores values
C) Remove: swap with last, update hash
D) All of the above

**Answer: D**

**Explanation:**
Hybrid structure: array for O(1) random access (getRandom), hash map for O(1) find/remove. Remove: swap target with last element, update hash map for moved element, pop array. O(1) all operations.

---

**Q8.71: Advanced - [Theory] - [Cache-Oblivious Hash]**

Cache-oblivious hash table:

A) Doesn't know cache size
B) Still optimal cache complexity
C) Recursive structure or blocked probing
D) All of the above

**Answer: D**

**Explanation:**
Cache-oblivious algorithms work well for any cache size without tuning. Hash tables: blocked probing, recursive layout. Theoretical interest, some practical applications.

---

**Q8.72: Expert - [Theory] - [Write-Optimized Hash]**

Log-structured hash table:

A) Append-only log for writes
B) In-memory hash maps log offset
C) Periodic compaction
D) All of the above

**Answer: D**

**Explanation:**
Write-optimized for SSD: append-only log (sequential writes), hash index in memory maps key to log offset. Garbage collection compacts. Used in key-value stores (RocksDB, FlashStore, SILT).

---

**Q8.73: Expert - [Theory] - [GPU Hash Table]**

GPU hash tables:

A) Open addressing with warp-level synchronization
B) Cuckoo hashing for deterministic probes
C) Coalesced memory access patterns
D) All of the above

**Answer: D**

**Explanation:**
GPU hash: thousands of threads, warp-level operations. Open addressing with threads in warp probing cooperatively. Cuckoo hashing: fixed probe sequence. Memory access: coalesced (aligned, consecutive) crucial for performance.

---

**Q8.74: Expert - [Theory] - [Learned Hash]**

Learned index structures:

A) Use ML model to predict position
B) CDF model for cumulative distribution
C) Fallback to traditional for errors
D) All of the above

**Answer: D**

**Explanation:**
Learned indexes: train model f(key) ≈ position. For sorted data, model CDF. Predict position, binary search nearby for exact. Can be smaller and faster than B-tree. Emerging research area.

---

**Q8.75: Expert - [Theory] - [Final Summary]**

Hash tables are fundamental because:

A) O(1) average operations enable many algorithms
B) Simple concept, rich design space
C) Ubiquitous in systems and applications
D) All of the above

**Answer: D**

**Explanation:**
Hash tables: from simple concept to rich theory to diverse implementations. Enable O(1) dictionaries, sets, caches. Building blocks for countless algorithms. Understanding from basic chaining to SIMD-optimized concurrent variants is essential.

---

## Chapter 8 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 12 | Basic operations, collision, chaining, open addressing |
| Intermediate | 30 | Linear/quadratic/double hashing, resizing, LRU, two sum |
| Advanced | 22 | Consistent hashing, cuckoo, Robin Hood, Bloom filter, perfect hashing |
| Expert | 11 | Universal hashing, Swiss table, learned indexes, GPU hashing, SipHash |

**Total MCQs: 75** | **Target Met: ✓**

**Key Hash Table Complexities:**
- Average: O(1) insert, delete, lookup
- Worst: O(n) with collisions
- Chaining: O(1 + α) where α = n/m

**Next:** Part III - Non-Linear Data Structures (Chapters 9-16)
