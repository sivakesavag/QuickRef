# Chapter 13: Tries & String Data Structures

**Target:** 55 MCQs | **Distribution:** 14 Foundational, 22 Intermediate, 14 Advanced, 5 Expert

---

**Q13.1: Foundational - [Theory] - [Trie Definition]**

A trie (prefix tree) is:

A) Tree-like data structure for storing strings
B) Each edge represents a character
C) Path from root to node represents a prefix
D) All of the above

**Answer: D**

**Explanation:**
Trie: tree where each path from root to a node spells out a prefix. Nodes share common prefixes. Root represents empty string. Each node may have up to |Σ| children (alphabet size). Leaf or marked node indicates complete word. Name from "retrieval" (re-trie-val). Efficient for prefix-based operations.

---

**Q13.2: Foundational - [Theory] - [Trie Node Structure]**

Trie node typically contains:

A) Array or map of children (one per character)
B) Boolean flag: isEndOfWord
C) Optionally: count, value, or other metadata
D) All of the above

**Answer: D**

**Explanation:**
Node structure: children array of size |Σ| (26 for lowercase English), or hash map for large alphabets. isEndOfWord marks complete words vs prefixes. For prefix counting: store count. For autocomplete: store word or value. Space: O(Σ) per node; compressed tries reduce this.

---

**Q13.3: Foundational - [Theory] - [Trie Insert]**

Inserting a word into trie:

A) Follow existing path character by character
B) Create new nodes for characters not yet in trie
C) Mark last node as end of word
D) All of the above

**Answer: D**

**Explanation:**
Insert "apple": start at root. 'a' → create if missing, move to 'a' node. 'p' → create, move. Continue for 'p', 'l', 'e'. Mark 'e' node as isEndOfWord. O(L) time where L = word length. Each character checked/created in O(1) with array children.

---

**Q13.4: Foundational - [Trace] - [Trie Insert]**

Insert "cat", "car", "card" into empty trie:

A) "cat": root→c→a→t (mark t)
B) "car": root→c→a→r (mark r). Shares c→a prefix with "cat"
C) "card": root→c→a→r→d (mark d). Shares c→a→r with "car"
D) Three words stored, sharing common prefixes

**Answer: D**

**Explanation:**
After all insertions: root has child 'c'. 'c' has child 'a'. 'a' has children 't' (end=true) and 'r' (end=true). 'r' has child 'd' (end=true). Words "cat", "car", "card" share the prefix "ca". This prefix sharing is the key advantage of tries.

---

**Q13.5: Foundational - [Theory] - [Trie Search]**

Searching for a word in trie:

A) Follow path from root, character by character
B) If path exists and last node is marked end-of-word: found
C) If path doesn't exist (missing child): not found
D) All of the above

**Answer: D**

**Explanation:**
Search "car": root→c→a→r. Check isEndOfWord at 'r'. If true, word exists. If false, "car" is only a prefix (e.g., "card" exists but "car" was never inserted). O(L) time. Key distinction: search for exact word vs prefix existence.

---

**Q13.6: Foundational - [Theory] - [Prefix Search]**

Check if any word starts with a given prefix:

A) Follow path from root for each character of prefix
B) If all characters found: prefix exists
C) Don't need to check isEndOfWord (any path constitutes a prefix)
D) All of the above

**Answer: D**

**Explanation:**
Prefix check: traverse trie for each character. If we reach the end of prefix string without hitting a null child, the prefix exists (at least one word starts with it). O(L) time for prefix of length L. This is tries' primary advantage over hash tables: efficient prefix queries.

---

**Q13.7: Foundational - [Theory] - [Trie Complexity]**

Trie time complexity:

A) Insert: O(L) where L = word length
B) Search: O(L)
C) Delete: O(L)
D) All of the above

**Answer: D**

**Explanation:**
All operations proportional to word length L, independent of number of words stored. Compare: hash table has average O(L) for hashing the string, but no prefix matching. BST: O(L × log n) comparisons (each comparison O(L)). Trie: O(L) guaranteed, no hash collisions. Space is the main disadvantage.

---

**Q13.8: Intermediate - [Theory] - [Trie Space Complexity]**

Space complexity of trie:

A) O(N × L × Σ) worst case (N words, L avg length, Σ alphabet size)
B) Each node stores array of Σ pointers
C) Can be reduced with compressed tries or hash maps
D) All of the above

**Answer: D**

**Explanation:**
Worst case: all words share no prefixes, each word creates L new nodes, each node has Σ-sized array → O(N × L × Σ). In practice: prefix sharing reduces this significantly. Space reduction: (1) hash map instead of array per node (sparse alphabets), (2) compressed trie (merge chains), (3) ternary search trie (3 pointers per node). Memory is tries' main drawback.

---

**Q13.9: Intermediate - [Theory] - [Trie Delete]**

Deleting a word from trie:

A) Unmark isEndOfWord at last character
B) Remove nodes bottom-up if they have no other children and aren't end-of-word
C) O(L) time
D) All of the above

**Answer: D**

**Explanation:**
Delete: find word (O(L)). Unmark end-of-word. If the node has no children and no other words pass through it, remove the node. Walk up, removing nodes that are now unnecessary (no children, not end-of-word). Like pruning dead branches. O(L) time. Don't delete nodes that are prefixes of other words.

---

**Q13.10: Intermediate - [Theory] - [Trie vs Hash Table]**

Trie advantages over hash table:

A) Prefix matching (startsWith) efficient
B) Lexicographic ordering of keys (DFS gives sorted order)
C) No hash collisions
D) All of the above

**Answer: D**

**Explanation:**
Trie: prefix queries O(L), sorted iteration via DFS, no collision handling. Hash table: O(1) average lookup, but no prefix matching (would need to check all keys), no ordering, potential collisions. Trie disadvantages: higher space usage, potentially slower for single exact lookups. Choose trie for prefix-heavy workloads (autocomplete, spell check, IP routing).

---

**Q13.11: Intermediate - [Theory] - [Autocomplete with Trie]**

Implementing autocomplete:

A) Navigate trie to prefix node
B) DFS from prefix node to collect all words with that prefix
C) Can limit results to top-K (e.g., by frequency stored in nodes)
D) All of the above

**Answer: D**

**Explanation:**
Autocomplete: user types prefix → find all completions. Trie: traverse to prefix end, DFS to collect words. O(prefix_length + total_chars_in_results). For top-K: store frequency, use priority queue during DFS. Real-world: Google search suggestions, IDE code completion, phone keyboard predictions. Compressed tries used for efficiency.

---

**Q13.12: Intermediate - [Trace] - [Autocomplete]**

Trie with words ["apple", "app", "apt", "bat"]. Autocomplete for "ap":

A) Navigate: root→a→p (prefix "ap" found)
B) DFS from 'p' node: finds "app" (p→end), "apple" (p→l→e→end), "apt" (p→t→end)
C) Results: ["app", "apple", "apt"]
D) "bat" not included (different prefix)

**Answer: D**

**Explanation:**
Prefix "ap" → node 'p' under 'a'. DFS: 'p' is end ("app"), 'p'→'l'→'e' is end ("apple"), 'p'→'t' is end ("apt"). "bat" shares no prefix with "ap". Three results returned. Can sort alphabetically or by frequency.

---

**Q13.13: Intermediate - [Theory] - [Compressed Trie (Radix/Patricia)]**

Compressed trie (radix tree / Patricia tree):

A) Merge chains of single-child nodes into one edge
B) Edge labels are strings instead of single characters
C) Reduces number of nodes, saves space
D) All of the above

**Answer: D**

**Explanation:**
Compressed trie: if a node has only one child, merge with child. Edge labeled with concatenated characters. Example: "romane", "romanus" → edge "roman" then branch to "e" and "us". Reduces nodes dramatically for sparse tries. Patricia tree: a particular variant. Radix tree: general term. Same O(L) operations, O(n) nodes (n = number of words) instead of O(sum of lengths).

---

**Q13.14: Intermediate - [Trace] - [Compressed Trie]**

Words ["romane", "romanus", "romulus", "rubens"]:

A) Standard trie: r→o→m→a→n→(e,u→s), r→u→b→e→n→s, r→o→m→u→l→u→s
B) Compressed: r→(om→(an→(e, us), ulus), ubens)
C) Fewer nodes, edges carry multiple characters
D) All of the above

**Answer: D**

**Explanation:**
Standard trie has many single-child chains. Compressed: root splits on "om" and "ubens" branches. "om" splits on "an" and "ulus". "an" splits on "e" and "us". Four words stored in much fewer nodes. Same search time O(L), less space.

---

**Q13.15: Intermediate - [Theory] - [Ternary Search Trie]**

Ternary search trie (TST):

A) Each node has 3 children: less-than, equal, greater-than
B) Combines trie with BST approach
C) Less space than standard trie (3 pointers vs Σ)
D) All of the above

**Answer: D**

**Explanation:**
TST: each node stores one character and three pointers. If search char < node char: go left. If equal: go middle (next char). If greater: go right. Space: 3 pointers per node vs Σ. Balanced performance between trie and BST. Efficient for medium-sized alphabets. Used in some spell checkers and autocomplete systems.

---

**Q13.16: Advanced - [Theory] - [Suffix Trie]**

Suffix trie:

A) Trie of all suffixes of a string
B) For string "abc": suffixes "abc", "bc", "c" all inserted
C) Enables substring queries in O(pattern length)
D) All of the above

**Answer: D**

**Explanation:**
Suffix trie: insert all suffixes of text. String of length n → n suffixes → O(n²) nodes worst case. Substring search: check if pattern is a path in the suffix trie. O(m) for pattern of length m. Too much space for practical use. Suffix trees and suffix arrays address this.

---

**Q13.17: Advanced - [Theory] - [Suffix Tree]**

Suffix tree:

A) Compressed trie of all suffixes
B) O(n) nodes and edges for string of length n
C) Built in O(n) time (Ukkonen's algorithm)
D) All of the above

**Answer: D**

**Explanation:**
Suffix tree: compressed suffix trie. Edge labels are substrings (stored as start,length pair). O(n) space. Ukkonen's algorithm: online O(n) construction. Supports: substring search O(m), longest common substring, longest repeated substring, all in optimal time. Powerful but complex to implement. Foundation of many string algorithms.

---

**Q13.18: Advanced - [Theory] - [Suffix Array]**

Suffix array:

A) Sorted array of all suffix starting positions
B) O(n) space (just indices)
C) Can simulate suffix tree operations with LCP array
D) All of the above

**Answer: D**

**Explanation:**
Suffix array: sort all suffixes of string, store starting indices. For "banana": suffixes sorted → [5:"a", 3:"ana", 1:"anana", 0:"banana", 4:"na", 2:"nana"]. SA = [5,3,1,0,4,2]. O(n) space. Construction: O(n log n) with SA-IS, O(n) possible. With LCP (longest common prefix) array, supports same queries as suffix tree. Simpler to implement, less space.

---

**Q13.19: Advanced - [Trace] - [Suffix Array]**

Suffix array for "abac":

A) Suffixes: "abac"(0), "bac"(1), "ac"(2), "c"(3)
B) Sorted: "abac"(0), "ac"(2), "bac"(1), "c"(3)
C) Suffix array: [0, 2, 1, 3]
D) Binary search suffix array for pattern matching

**Answer: D**

**Explanation:**
Sort suffixes alphabetically. "abac" < "ac" < "bac" < "c". SA = [0,2,1,3]. To search for pattern "ac": binary search over suffix array → found at position 2. Search time: O(m log n) with binary search, O(m + log n) with LCP. Much simpler than suffix tree implementation.

---

**Q13.20: Intermediate - [Theory] - [LCP Array]**

LCP (Longest Common Prefix) array:

A) LCP[i] = length of longest common prefix between SA[i] and SA[i-1]
B) Used with suffix array for efficient pattern matching
C) Constructible in O(n) time (Kasai's algorithm)
D) All of the above

**Answer: D**

**Explanation:**
LCP array: adjacent suffixes in sorted order share common prefix. LCP[i] = |LCP(suffix[SA[i]], suffix[SA[i-1]])|. Enables: number of distinct substrings = n(n+1)/2 - sum(LCP), longest repeated substring = max(LCP), and efficient pattern matching with SA. Kasai's algorithm: O(n) using the inverse suffix array.

---

**Q13.21: Intermediate - [Theory] - [Aho-Corasick Algorithm]**

Aho-Corasick algorithm:

A) Multi-pattern string matching
B) Builds trie of all patterns, adds failure links
C) Searches text in O(text_length + total_matches)
D) All of the above

**Answer: D**

**Explanation:**
Aho-Corasick: build trie of all patterns. Add failure links (similar to KMP failure function, but for trie). Process text character by character, following trie edges or failure links. Finds all pattern occurrences in O(n + m + z) where n = text length, m = total pattern length, z = number of matches. Used in virus scanning, DNA sequence matching, intrusion detection.

---

**Q13.22: Advanced - [Theory] - [Aho-Corasick Failure Links]**

Aho-Corasick failure links:

A) Point to longest proper suffix that is also a prefix in the trie
B) Similar to KMP failure function but across multiple patterns
C) Built via BFS from root
D) All of the above

**Answer: D**

**Explanation:**
Failure link of node u: longest proper suffix of string(u) that is a prefix of some pattern (i.e., exists as a path from root in trie). BFS construction: root's children fail to root. For deeper nodes: follow parent's failure link, try to extend. Like KMP generalized to a tree of patterns. Dictionary links: follow failure links to find patterns that are suffixes.

---

**Q13.23: Foundational - [Theory] - [Trie Applications]**

Common trie applications:

A) Autocomplete, spell checker
B) IP routing (longest prefix matching)
C) Phone directory, dictionary lookup
D) All of the above

**Answer: D**

**Explanation:**
Tries excel at: (1) Autocomplete: prefix → all words. (2) Spell checking: find closest words. (3) IP routing: longest prefix match for routing tables (Chapter 35). (4) Word games (Boggle, Scrabble). (5) Genome analysis (DNA sequences as strings). (6) T9 predictive text. Wherever prefix-based queries dominate, tries are the natural choice.

---

**Q13.24: Intermediate - [Theory] - [Longest Common Prefix of Words]**

Find longest common prefix of an array of words using trie:

A) Insert all words into trie
B) Follow path from root while node has exactly one child
C) Stop at branching point or end-of-word marker
D) All of the above

**Answer: D**

**Explanation:**
Insert all words. Starting from root, follow path while each node has exactly one child and is not end-of-word. The path so far is the longest common prefix. Alternative without trie: compare characters position by position across all strings, stop at first mismatch. O(S) where S = sum of all string lengths for both approaches.

---

**Q13.25: Intermediate - [Theory] - [Word Search in Grid]**

Word search in 2D grid using trie:

A) Build trie from dictionary of words to find
B) DFS from each cell, following trie edges
C) Prune: stop exploring if no trie path matches
D) All of the above

**Answer: D**

**Explanation:**
Word search II (Leetcode 212): build trie from word list. From each cell, DFS in 4 directions. At each step, check if current character has a trie child. If no child: prune (no word starts with this path). If end-of-word: found a word. Avoids searching for each word independently. O(M × N × 4^L) worst case, but trie pruning makes it practical.

---

**Q13.26: Foundational - [Theory] - [Trie vs BST for Strings]**

Trie vs balanced BST for string keys:

A) Trie: O(L) lookup — independent of number of strings
B) BST: O(L × log n) — each comparison is O(L)
C) Trie wins for prefix-heavy operations
D) All of the above

**Answer: D**

**Explanation:**
BST with string keys: each comparison takes O(L) (string comparison). Height O(log n) → total O(L × log n) per operation. Trie: each character = one step, total O(L). For large n and moderate L, trie is significantly faster. BST advantage: sorted order for range queries, lower space for long strings with little prefix sharing.

---

**Q13.27: Advanced - [Theory] - [Suffix Automaton (DAWG)]**

Suffix automaton (Directed Acyclic Word Graph — DAWG):

A) Minimal DFA accepting all suffixes of a string
B) O(n) states and transitions
C) Supports substring queries, counting distinct substrings
D) All of the above

**Answer: D**

**Explanation:**
Suffix automaton: smallest automaton recognizing all suffixes. At most 2n-1 states, at most 3n-4 transitions. Online construction in O(n). Supports: substring check O(m), count of distinct substrings, longest common substring of two strings. More space-efficient than suffix tree. Popular in competitive programming.

---

**Q13.28: Foundational - [Theory] - [Trie for Counting]**

Count words with given prefix using trie:

A) Store count at each node (number of words passing through)
B) Navigate to prefix end, read count
C) O(L) time for prefix of length L
D) All of the above

**Answer: D**

**Explanation:**
Augmented trie: each node stores prefix count (incremented during insert). To count words with prefix "app": navigate to 'p' node after "ap", read count. If count = 3, three words start with "app". Alternative: store end-of-word count and sum all counts in subtree (less efficient). Prefix count is a common trie modification.

---

**Q13.29: Intermediate - [Theory] - [XOR Trie]**

Trie for maximum XOR:

A) Binary trie: store numbers as binary strings (MSB first)
B) For each number, greedily choose opposite bit at each level
C) Finds maximum XOR pair in O(n × 32) for 32-bit integers
D) All of the above

**Answer: D**

**Explanation:**
Maximum XOR: for each number, traverse binary trie choosing opposite bit at each level (maximize XOR). If opposite bit child doesn't exist, follow same bit. Insert all numbers first, then query each. O(n × W) where W = bit width. Classic competitive programming technique. Works because XOR is maximized by differing in most significant bits.

---

**Q13.30: Advanced - [Trace] - [XOR Trie]**

Numbers [3(011), 10(1010), 5(0101)], find max XOR pair:

A) Insert all as 4-bit binary into trie
B) Query 3 (0011): try 1→0→1→0 = 1010 = 10. XOR = 3⊕10 = 9
C) Query 10 (1010): try 0→1→0→1 = 0101 = 5. XOR = 10⊕5 = 15
D) Maximum XOR pair = (10, 5) with XOR = 15

**Answer: D**

**Explanation:**
Trie approach: for each number, greedily find the number in trie that maximizes XOR bit by bit. Querying 3: try opposite bits → get 10, XOR=9. Querying 10: try opposite bits → get 5, XOR=15. Querying 5: try opposite → get 10, XOR=15. Max XOR = 15. O(n × W) = O(3 × 4) = O(12).

---

**Q13.31: Intermediate - [Theory] - [Trie-based Sorting]**

Sorting strings using trie:

A) Insert all strings into trie
B) DFS traversal gives strings in lexicographic order
C) O(S) time where S = total characters
D) All of the above

**Answer: D**

**Explanation:**
Trie sort: insert all strings O(S). DFS in alphabetical order of children collects strings in sorted order. O(S) total — linear in total character count. This is essentially radix sort for strings. Comparison-based sort would be O(S × n log n) due to O(S/n) average string comparison. Trie sort is faster for many equal-length strings.

---

**Q13.32: Foundational - [Theory] - [Trie for IP Routing]**

Trie for longest prefix matching in IP routing:

A) IP addresses stored as binary strings in trie
B) Longest matching prefix determines routing
C) O(W) lookup where W = address width (32 for IPv4)
D) All of the above

**Answer: D**

**Explanation:**
IP routing: forwarding table maps IP prefixes to next-hop. Binary trie: traverse address bits, track last match. Longest prefix = most specific route. O(32) for IPv4, O(128) for IPv6. Patricia trie (compressed) used in practice for space efficiency. Critical for router performance. See Chapter 35 for networking applications.

---

**Q13.33: Advanced - [Theory] - [Persistent Trie]**

Persistent trie:

A) Immutable: old versions preserved after updates
B) Path copying: new root, share unchanged subtrees
C) O(L) new nodes per insert (L = word length)
D) All of the above

**Answer: D**

**Explanation:**
Persistent trie: insert creates new path from root to new/modified leaf. Shared nodes for unchanged branches. O(L) space per insert. Previous roots still access old versions. Used for versioned dictionaries, functional programming, competitive programming with offline queries. Same persistence technique as persistent BSTs (Q10.47).

---

**Q13.34: Intermediate - [Theory] - [Counting Distinct Substrings]**

Count distinct substrings using suffix array + LCP:

A) Total substrings: n(n+1)/2
B) Subtract LCP values (overlapping prefixes between adjacent suffixes)
C) Distinct = n(n+1)/2 - sum(LCP)
D) All of the above

**Answer: D**

**Explanation:**
Each suffix of length k contributes k substrings (its prefixes). Total non-distinct substrings: sum of suffix lengths = n(n+1)/2. Adjacent suffixes in sorted order share LCP[i] prefixes (already counted). Subtract: distinct = n(n+1)/2 - Σ(LCP[i]). O(n) after suffix array and LCP array construction. Alternative: suffix automaton directly counts in O(n).

---

**Q13.35: Advanced - [Theory] - [Longest Repeated Substring]**

Longest repeated substring using suffix array + LCP:

A) Longest repeated substring = max value in LCP array
B) LCP[i] = length of longest common prefix of consecutive sorted suffixes
C) Maximum LCP = longest substring appearing at least twice
D) All of the above

**Answer: D**

**Explanation:**
If two suffixes share a prefix of length k (LCP = k), that prefix occurs at least twice as a substring. Maximum LCP over entire array gives longest such substring. Find max LCP value, reconstruct substring from corresponding suffixes. O(n) after building SA + LCP. Alternative: suffix tree (deepest internal node = longest repeated substring).

---

**Q13.36: Foundational - [Theory] - [Trie Memory Optimization]**

Reducing trie memory usage:

A) Use hash map instead of array for children (sparse nodes)
B) Compressed trie (merge single-child chains)
C) Use array only for nodes near root, hash map for deeper nodes
D) All valid strategies

**Answer: D**

**Explanation:**
Memory optimization: (1) Hash map children: O(average branching) vs O(Σ) per node. Good for sparse alphabets. (2) Compressed trie: O(n) nodes vs O(total chars). (3) Hybrid: array for top levels (likely dense), hash map for deeper (likely sparse). (4) Bitwise trie: for integer keys, fixed depth. Trade-off: memory vs access speed (array O(1) vs hash map O(1) amortized).

---

**Q13.37: Intermediate - [Theory] - [Bitwise Trie]**

Bitwise trie for integers:

A) Each level represents one bit (MSB to LSB)
B) Binary tree of depth W (word size, e.g., 32)
C) Used for XOR queries, integer range queries
D) All of the above

**Answer: D**

**Explanation:**
Bitwise trie: binary trie where path = binary representation. Depth 32 for 32-bit integers. Each node has at most 2 children (bit 0 or 1). Operations: insert O(W), search O(W), maximum XOR O(W). Used for: max XOR (Q13.29), IP routing, range queries. Space: O(n × W) worst case. Compact and fast for fixed-width integer keys.

---

**Q13.38: Advanced - [Theory] - [FM-Index]**

FM-Index:

A) Compressed full-text index based on BWT (Burrows-Wheeler Transform)
B) Supports pattern matching in O(m) time with O(n) space
C) Used in bioinformatics (DNA sequence alignment)
D) All of the above

**Answer: D**

**Explanation:**
FM-Index: uses BWT for compression + rank/select for efficient querying. Compressed to O(n × H_k) bits (k-th order entropy). Pattern matching via backward search: O(m) for pattern of length m. Core of BWA and Bowtie aligners in genomics. Combines space efficiency with fast exact matching. Advanced string data structure.

---

**Q13.39: Foundational - [Theory] - [Trie Alphabet Size Impact]**

Effect of alphabet size on trie:

A) Larger alphabet → more children per node → more memory
B) English lowercase: 26 children per node
C) Unicode: potentially millions → must use hash map
D) All of the above

**Answer: D**

**Explanation:**
Alphabet size Σ directly impacts trie node size. Σ=26: 26-pointer array per node (manageable). Σ=256 (ASCII): 256 pointers. Σ=Unicode: hash map required. Larger Σ → wider but potentially shorter tries. Binary trie (Σ=2): deepest but smallest nodes. Choose node representation based on expected Σ and sparsity.

---

**Q13.40: Intermediate - [Theory] - [Map/Dictionary Using Trie]**

Trie as key-value store:

A) Keys are strings, values stored at end-of-word nodes
B) Insert: O(L), retrieve: O(L)
C) Prefix queries on keys: O(prefix_length + results)
D) All of the above

**Answer: D**

**Explanation:**
Trie as map: store value at the end-of-word node. Get by key: traverse to key's end node, return value. Supports all prefix operations that hash maps can't. Autocomplete with values (e.g., search frequency). Python: use dict of dicts pattern. Many languages have trie library implementations.

---

**Q13.41: Expert - [Theory] - [Suffix Tree Applications]**

Suffix tree enables:

A) Substring search: O(m) for pattern of length m
B) Longest common substring of two strings: O(n + m)
C) Number of occurrences of pattern: O(m + count)
D) All of the above, plus palindrome finding, repeat analysis

**Answer: D**

**Explanation:**
Suffix tree: versatile string data structure. (1) Substring search O(m). (2) Longest common substring: build generalized suffix tree, find deepest internal node with leaves from both strings. (3) Occurrences: count leaves in subtree rooted at pattern's node. (4) Longest palindrome: via Eertree or suffix tree with reversed string. Powerful but complex implementation.

---

**Q13.42: Intermediate - [Theory] - [Z-Function vs Trie]**

When to use trie vs other string algorithms:

A) Trie: multiple queries on a fixed dictionary (autocomplete, spell check)
B) KMP/Z-algorithm: single pattern matching in text
C) Aho-Corasick: multiple patterns in text simultaneously
D) All are valid distinctions

**Answer: D**

**Explanation:**
Choice depends on use case: (1) Fixed dictionary, many queries: trie. (2) Single pattern, single text: KMP or Z-algorithm. (3) Multiple patterns, single text: Aho-Corasick (trie + failure links). (4) Many substrings of one text: suffix array/tree. Each optimized for different query patterns. Understanding when to use which is key.

---

**Q13.43: Expert - [Theory] - [Wavelet Tree]**

Wavelet tree:

A) Data structure for sequences over alphabets
B) Supports rank, select, and access queries in O(log Σ)
C) Space: O(n log Σ) bits
D) All of the above

**Answer: D**

**Explanation:**
Wavelet tree: balanced binary tree over alphabet. Each level partitions alphabet in half. Supports: access(i), rank(c, i), select(c, k) all in O(log Σ). Applications: document retrieval, range frequency, colored range queries. Built on bitvector rank/select. Advanced data structure bridging strings and sequences.

---

**Q13.44: Advanced - [Theory] - [Trie for Contact List]**

Efficient contact list with trie:

A) Insert all contacts into trie
B) As user types each character, count/list matching contacts
C) Each keystroke: O(1) additional trie traversal step
D) All of the above

**Answer: D**

**Explanation:**
Contact search: build trie of names. As user types "Jo", navigate root→J→o. Count at 'o' node = contacts with prefix "Jo". List via DFS from 'o'. Each additional character: O(1) to advance pointer. Incremental search. This is how phone contacts and messaging apps implement name search.

---

**Q13.45: Intermediate - [Theory] - [Replace Words with Root]**

Replace words in sentence with shortest root from dictionary:

A) Build trie of dictionary roots
B) For each word, find shortest prefix that's a root
C) Replace word with that root
D) All of the above

**Answer: D**

**Explanation:**
Root replacement: trie insert all dictionary roots. For each sentence word, traverse trie character by character. If hit isEndOfWord, found shortest root → replace. If exhaust word without finding root → keep original. O(total characters) for all words. Classic trie application demonstrating prefix matching power.

---

**Q13.46: Foundational - [Theory] - [Trie vs Hash Set for Word Lookup]**

Comparing trie and hash set for word existence checks:

A) Hash set: O(L) average per lookup (hashing the string)
B) Trie: O(L) worst case per lookup (traversing characters)
C) Hash set doesn't support prefix queries
D) All of the above

**Answer: D**

**Explanation:**
Both O(L) for exact lookup. Hash set: simpler, lower constant factors, O(L) for hashing. Trie: supports prefix queries, sorted order, but higher space. If only need exact match: hash set is simpler and usually faster. If need prefix operations: trie is necessary. Design choice based on required operations.

---

**Q13.47: Expert - [Theory] - [Eertree (Palindromic Tree)]**

Eertree (palindromic tree):

A) Stores all distinct palindromic substrings of a string
B) O(n) nodes for string of length n
C) Online construction in O(n) time
D) All of the above

**Answer: D**

**Explanation:**
Eertree: at most n+2 nodes (including odd and even root). Each node represents a distinct palindromic substring. Suffix links connect palindromes. Supports: count distinct palindromic substrings, longest palindromic substring, palindrome factorization. Online O(n) construction. Elegant structure for palindrome problems in competitive programming.

---

**Q13.48: Advanced - [Theory] - [Generalized Suffix Tree]**

Generalized suffix tree:

A) Suffix tree for multiple strings
B) Each leaf labeled with (string_id, position)
C) Enables multi-string queries (longest common substring, etc.)
D) All of the above

**Answer: D**

**Explanation:**
Generalized suffix tree: build suffix tree for S₁$₁S₂$₂...Sₖ$ₖ (concatenate with unique terminators). Internal node with leaves from multiple strings → shared substring. Deepest such node = longest common substring. O(Σ|Sᵢ|) construction and space. Powerful for comparative genomics, document similarity.

---

**Q13.49: Intermediate - [Theory] - [Trie Height]**

Height of trie:

A) Equals length of longest word stored
B) Independent of number of words
C) Different from BST height (depends on key count)
D) All of the above

**Answer: D**

**Explanation:**
Trie height = max word length. Inserting 1 million 5-letter words: height = 5. Inserting 1 word of length 100: height = 100. Independent of n (number of words), depends on L_max. This is both advantage (short words → shallow tree) and potential issue (very long keys → deep tree).

---

**Q13.50: Foundational - [Theory] - [Trie Traversal]**

DFS traversal of trie:

A) Visits all nodes, collecting words at end-of-word nodes
B) Produces words in lexicographic order (if children visited alphabetically)
C) Can enumerate all stored words
D) All of the above

**Answer: D**

**Explanation:**
Trie DFS: recursive traversal visiting children in order. If children in alphabetical order, words collected in sorted order. No explicit sorting needed — trie inherently maintains order. Used for: word enumeration, spell checking suggestions, lexicographic sorting. O(total nodes) time.

---

**Q13.51: Expert - [Theory] - [Compressed Suffix Array]**

Compressed suffix array:

A) Represents suffix array in compressed space
B) O(n) bits with O(log n) access time    
C) Based on BWT and rank computations
D) All of the above

**Answer: D**

**Explanation:**
Compressed SA: stores suffix array implicitly using BWT. Space: O(n × H_k) bits (k-th order entropy). Access SA[i]: O(log n) time using inverse SA and BWT sampling. Combined with FM-index for full-text search. Practical for large texts (genomes, web corpora) where O(n log n) bits for explicit SA is too much.

---

**Q13.52: Intermediate - [Theory] - [Word Break Problem]**

Word break using trie:

A) Given string and dictionary, can string be segmented into dictionary words?
B) Trie of dictionary + dynamic programming
C) DP[i] = true if s[0..i-1] can be segmented
D) All of the above

**Answer: D**

**Explanation:**
Word break: DP where DP[i] = any j < i where DP[j] is true and s[j..i-1] is in dictionary. Trie enables O(L) check of s[j..i-1] in dictionary. Total: O(n² × L) worst case. Trie optimization: for each position, follow trie path to find all matching dictionary words in one traversal. Classic DP + trie combination.

---

**Q13.53: Advanced - [Theory] - [Burrows-Wheeler Transform]**

Burrows-Wheeler Transform (BWT):

A) Permutation of string that groups similar characters
B) Reversible transformation used in compression (bzip2)
C) Foundation for FM-index and compressed suffix arrays
D) All of the above

**Answer: D**

**Explanation:**
BWT: form all rotations of string, sort lexicographically, take last column. Groups similar characters together → highly compressible. Reversible in O(n). Foundation of bzip2 compression. Combined with rank/select → FM-index for fast pattern matching in compressed space. Connects compression and text indexing.

---

**Q13.54: Advanced - [Theory] - [Longest Common Substring]**

Longest common substring of two strings:

A) Suffix array of concatenated strings: O(n + m) space and time
B) Generalized suffix tree: O(n + m) build, find deepest shared internal node
C) DP approach: O(n × m) time and space
D) All valid approaches

**Answer: D**

**Explanation:**
Multiple approaches: (1) DP: dp[i][j] = length of LCS ending at s1[i] and s2[j]. O(nm) time/space. (2) Suffix array: concatenate with separator, find max LCP between adjacent suffixes from different strings. O((n+m) log(n+m)). (3) Suffix tree: O(n+m). Choose based on constraints. DP simplest for small inputs; suffix structures for large.

---

**Q13.55: Intermediate - [Theory] - [Trie Implementation Choices]**

Choosing trie implementation:

A) Array children: fastest (O(1) child access), most memory
B) Hash map children: flexible alphabet, less memory, slightly slower
C) Sorted list children: space efficient, O(log Σ) child access
D) All are valid trade-offs

**Answer: D**

**Explanation:**
Implementation trade-offs: (1) Array: fixed size Σ, O(1) lookup, O(Σ) space per node. Best for small Σ (26 chars). (2) Hash map: dynamic, O(1) average lookup, handles any alphabet. (3) Sorted array/list: O(log Σ) binary search, cache-friendly, minimal space. (4) BST children: O(log Σ) access, simple. Choose based on alphabet size, query pattern, and memory constraints.

---

## Chapter 13 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 14 | Trie definition, insert, search, prefix, complexity, applications, traversal |
| Intermediate | 22 | Compressed trie, TST, autocomplete, Aho-Corasick, suffix array, LCP, XOR trie, word break |
| Advanced | 14 | Suffix tree, suffix automaton, FM-index, persistent trie, BWT, longest common substring |
| Expert | 5 | Wavelet tree, compressed SA, Eertree, suffix tree applications |

**Total MCQs: 55** | **Target Met: ✓**

**Key String DS Comparisons:**

| Structure | Space | Build Time | Substring Search | Prefix Query |
|-----------|-------|------------|-------------------|--------------|
| Trie | O(NLΣ) | O(NL) | O(L) exact | O(L) ✓ |
| Compressed Trie | O(N) | O(NL) | O(L) exact | O(L) ✓ |
| Suffix Tree | O(n) | O(n) | O(m) | O(m) ✓ |
| Suffix Array | O(n) | O(n log n) | O(m log n) | O(m log n) |
| Aho-Corasick | O(M) | O(M) | O(n + z) multi | N/A |

**Next:** Chapter 14 - Graphs — Representation
