# Chapter 26: String Algorithms

**Target:** 65 MCQs | **Distribution:** 16 Foundational, 26 Intermediate, 16 Advanced, 7 Expert

---

**Q26.1: Foundational - [Theory] - [String Matching Overview]**

String matching problem:

A) Find all occurrences of pattern P in text T
B) Naive: O(n×m) — slide pattern and compare
C) Better algorithms: KMP, Rabin-Karp, Boyer-Moore
D) All of the above

**Answer: D**

**Explanation:**
String matching: given text T (length n) and pattern P (length m), find all positions where P occurs in T. Naive: try every starting position, compare character by character. O((n-m+1)×m) worst case. Better: preprocess pattern to avoid redundant comparisons. KMP O(n+m), Rabin-Karp O(n+m) expected, Boyer-Moore O(n/m) best.

---

**Q26.2: Foundational - [Theory] - [KMP Algorithm]**

Knuth-Morris-Pratt (KMP):

A) Precompute failure/prefix function for pattern
B) Never re-examine text characters — pointer only moves forward
C) O(n + m) time, O(m) space
D) All of the above

**Answer: D**

**Explanation:**
KMP: key insight — when mismatch occurs, use already-matched prefix information to skip ahead. Failure function π[i]: length of longest proper prefix of P[0..i] that is also a suffix. On mismatch at position j in pattern: jump to π[j-1], not back to 0. Text pointer never decrements. O(n+m). Preprocessing O(m).

---

**Q26.3: Foundational - [Trace] - [KMP Failure Function]**

Compute failure function for P = "ABABAC":

A) π[0]=0 (by definition)
B) π[1]=0 (B≠A), π[2]=1 (AB→A matches), π[3]=2 (ABA→AB matches)
C) π[4]=3 (ABAB→ABA matches), π[5]=0 (ABABAC, C≠B)
D) π = [0, 0, 1, 2, 3, 0]

**Answer: D**

**Explanation:**
Build π incrementally. π[0]=0 always. For i=1: compare P[1]=B with P[0]=A: mismatch → 0. i=2: P[2]=A matches P[0]=A → 1. i=3: P[3]=B matches P[1]=B → 2. i=4: P[4]=A matches P[2]=A → 3. i=5: P[5]=C vs P[3]=B: mismatch. Fall back: π[2]=1. P[5]=C vs P[1]=B: mismatch. π[0]=0. P[5]=C vs P[0]=A: mismatch → 0.

---

**Q26.4: Foundational - [Theory] - [Rabin-Karp Algorithm]**

Rabin-Karp:

A) Hash-based pattern matching
B) Rolling hash: update hash in O(1) as window slides
C) O(n + m) expected, O(nm) worst (hash collisions)
D) All of the above

**Answer: D**

**Explanation:**
Rabin-Karp: compute hash of pattern and rolling hash of each window. If hashes match: verify character by character (avoid false positives). Rolling hash: h(s[i+1..i+m]) = (h(s[i..i+m-1]) - s[i]×d^(m-1)) × d + s[i+m]. O(1) per slide. Expected O(n+m). Worst case (all collisions): O(nm). Excellent for multi-pattern matching.

---

**Q26.5: Intermediate - [Theory] - [Boyer-Moore Algorithm]**

Boyer-Moore:

A) Compare pattern right to left
B) Bad character rule: skip based on mismatched character
C) Good suffix rule: skip based on matched suffix
D) O(n/m) best case — sublinear!

**Answer: D**

**Explanation:**
Boyer-Moore: start comparison from right end of pattern. Bad character: if mismatch at position j with text char c, shift pattern to align c (or past it if not in pattern). Good suffix: if suffix matched, shift to next occurrence of that suffix in pattern. Best case: Θ(n/m) when alphabet is large. Worst case: O(nm) without good suffix, O(n) with.

---

**Q26.6: Intermediate - [Theory] - [Z-Algorithm]**

Z-algorithm:

A) Z[i] = length of longest substring starting at i that matches prefix
B) Compute all Z-values in O(n) time
C) String matching: concatenate P$T, find Z[i] = m
D) All of the above

**Answer: D**

**Explanation:**
Z-array: Z[i] = length of longest string starting at position i that is also a prefix of the string. Z[0] = n (by convention, or undefined). Computed in O(n) using Z-box [L,R]. For pattern matching: S = P + "$" + T. Any Z[i] = |P| indicates a match. O(n+m). Simpler than KMP for some implementations.

---

**Q26.7: Intermediate - [Theory] - [Suffix Array]**

Suffix array:

A) Sorted array of all suffixes' starting indices
B) Binary search for pattern: O(m log n)
C) Construction: O(n) or O(n log n) or O(n log² n)
D) All of the above

**Answer: D**

**Explanation:**
Suffix array: sort all n suffixes lexicographically, store starting indices. Pattern search: binary search, compare prefix. O(m log n) per query. Construction: naive O(n² log n). DC3/Skew: O(n). SA-IS: O(n) practical. O(n log² n) with rank-doubling is competitive and simpler. Space: O(n) integers vs suffix tree's O(n) but larger constants.

---

**Q26.8: Intermediate - [Theory] - [LCP Array]**

LCP (Longest Common Prefix) array:

A) LCP[i] = length of common prefix between suffix i and suffix i-1 in sorted order
B) Constructed in O(n) from suffix array (Kasai's algorithm)
C) Used for: counting distinct substrings, longest repeated substring
D) All of the above

**Answer: D**

**Explanation:**
LCP array augments suffix array. LCP[i] = length of common prefix between SA[i] and SA[i-1]. Kasai's: O(n) using the observation that LCP values decrease by at most 1 when moving in text order. Distinct substrings = n(n+1)/2 - Σ LCP[i]. Longest repeated substring = max(LCP). Powerful combined with suffix array.

---

**Q26.9: Intermediate - [Theory] - [Suffix Tree]**

Suffix tree:

A) Compressed trie of all suffixes
B) Ukkonen's algorithm: O(n) online construction
C) Applications: pattern matching, longest repeated substring, LCS of two strings
D) All of the above

**Answer: D**

**Explanation:**
Suffix tree: every suffix represented as root-to-leaf path. Compressed: chains of single-child nodes collapsed into one edge with substring label. O(n) nodes and edges. Ukkonen's: online O(n). Pattern matching: traverse tree in O(m) — very fast. Applications: substring queries, repeated patterns, biological sequence analysis. Space-heavy: suffix arrays often preferred.

---

**Q26.10: Foundational - [Theory] - [Naive String Matching]**

Naive (brute force) string matching:

A) Try pattern at every position in text
B) At each position: compare character by character
C) O((n-m+1) × m) worst case
D) Works well in practice for short patterns and large alphabets

**Answer: D**

**Explanation:**
Naive: outer loop over text positions (n-m+1), inner loop comparing m characters. Worst: "AAAA...A" with "AAA...AB" — nearly full comparison at every position. In practice: large alphabets (English text) cause early mismatches → fast average. Simple, no preprocessing. Used when pattern is very short or simplicity preferred.

---

**Q26.11: Intermediate - [Theory] - [Aho-Corasick Algorithm]**

Aho-Corasick:

A) Multi-pattern matching: find all occurrences of k patterns in text
B) Build trie of patterns + failure links (like KMP on trie)
C) O(n + m + z) where z = total matches, m = total pattern length
D) All of the above

**Answer: D**

**Explanation:**
Aho-Corasick: generalization of KMP to multiple patterns. Build trie of all patterns. Add failure links (like KMP's failure function but on trie). Process text: traverse trie, follow failure links on mismatch. Dictionary links: point to pattern endings reachable via failure links. O(n + Σ|patterns| + output_count). Used in: intrusion detection, content filtering, bioinformatics.

---

**Q26.12: Foundational - [Theory] - [Rolling Hash Detail]**

Polynomial rolling hash:

A) h(s) = s[0]×d^(m-1) + s[1]×d^(m-2) + ... + s[m-1] mod q
B) Roll: remove leading char, add trailing char, O(1)
C) d = base (e.g., 31 or 131), q = large prime
D) All of the above

**Answer: D**

**Explanation:**
Rolling hash: treat string as base-d number mod q. Roll window: h_new = (h_old - s[i]×d^(m-1)) × d + s[i+m] mod q. O(1) per position. Choose d and q carefully: d > alphabet size, q = large prime (10^9+7 or 10^9+9). Double hashing (two different q values) reduces collision probability to ~1/q².

---

**Q26.13: Intermediate - [Theory] - [Manacher's Algorithm]**

Manacher's algorithm:

A) Find all palindromic substrings in O(n)
B) Uses symmetry: palindrome within palindrome reuses information
C) Finds longest palindromic substring as a byproduct
D) All of the above

**Answer: D**

**Explanation:**
Manacher's: for each center, compute palindrome radius. Key: if position i is within a known palindrome centered at c with right boundary r: mirror position 2c-i already computed. Use its radius as starting point. Only extend when reaching beyond r. Amortized O(n). Handles odd and even length palindromes (insert separators: "#a#b#a#").

---

**Q26.14: Advanced - [Theory] - [Suffix Automaton]**

Suffix automaton (DAWG):

A) Minimal DFA accepting all suffixes of a string
B) O(n) states and transitions
C) Applications: count distinct substrings, shortest non-occurring string
D) All of the above

**Answer: D**

**Explanation:**
Suffix automaton: directed acyclic word graph (DAWG). Each state represents an equivalence class of right extensions. At most 2n states, 3n transitions. Built online in O(n). Count distinct substrings: sum of (len[v] - len[link[v]]) over all states. Can answer substring queries, find shortest absent word, count occurrences. Most compact representation of all substrings.

---

**Q26.15: Intermediate - [Theory] - [String Hashing Applications]**

String hashing applications:

A) Substring equality check in O(1) with prefix hashes
B) Longest common substring via binary search + hashing
C) Palindrome check on substrings in O(1)
D) All of the above

**Answer: D**

**Explanation:**
Prefix hashing: h[i] = hash of s[0..i]. Substring hash s[l..r] = (h[r] - h[l-1] × d^(r-l+1)) mod q. Compare any two substrings in O(1). LCS: binary search on length + hash all substrings of that length. O(n log n). Palindrome: compare hash of s[l..r] with hash of reversed s[l..r] (precompute reverse prefix hashes). Powerful O(1) string queries.

---

**Q26.16: Advanced - [Theory] - [Burrows-Wheeler Transform]**

Burrows-Wheeler Transform (BWT):

A) Permutation of string that groups similar characters
B) Construct: sort rotations, take last column
C) Reversible: original string recoverable from BWT
D) Foundation of bzip2 compression and FM-index

**Answer: D**

**Explanation:**
BWT: form matrix of all rotations, sort lexicographically, take last column. BWT tends to have runs of same character → compressible with run-length encoding + Huffman. Reverse: LF-mapping reconstructs original. FM-index: compressed full-text index using BWT. O(m) pattern search with O(n) space (compressed). Used in bioinformatics (BWA, Bowtie aligners).

---

**Q26.17: Advanced - [Theory] - [Palindromic Tree (Eertree)]**

Palindromic tree (eertree):

A) Contains all distinct palindromic substrings
B) At most n+2 nodes for string of length n
C) Built online in O(n)
D) All of the above

**Answer: D**

**Explanation:**
Eertree: each node represents a distinct palindromic substring. Two root nodes: length -1 (imaginary) and 0 (empty). Suffix links: like KMP failure function for palindromes. Online construction: O(n) amortized. Counts: distinct palindromes ≤ n+1 (surprisingly few). Applications: count palindromic substrings, find longest palindromic prefix/suffix.

---

**Q26.18: Intermediate - [Theory] - [Longest Repeated Substring]**

Longest repeated substring:

A) Suffix array + LCP: max LCP value
B) Suffix tree: deepest internal node
C) Binary search + hashing: O(n log n)
D) All valid approaches

**Answer: D**

**Explanation:**
Longest repeated substring: appears ≥ 2 times. Suffix array: adjacent suffixes in sorted order with longest LCP are the answer. O(n) with LCP array. Suffix tree: deepest internal node's path label (internal node = branching = ≥ 2 suffixes below). Binary search + hashing: check if repeated substring of length L exists → O(n log n).

---

**Q26.19: Advanced - [Theory] - [Lyndon Factorization]**

Lyndon factorization (Duval's algorithm):

A) Decompose string into Lyndon words w1 ≥ w2 ≥ ... ≥ wk (lexicographically)
B) Lyndon word: strictly smaller than all its rotations
C) O(n) time, O(1) space
D) All of the above

**Answer: D**

**Explanation:**
Lyndon word: lexicographically smallest rotation of itself (primitive + smallest). Chen-Fox-Lyndon theorem: unique factorization into non-increasing Lyndon words. Duval's algorithm: O(n) in-place. Applications: minimum rotation of string, Booth's algorithm for lexicographically smallest rotation. Elegant connection between string theory and combinatorics.

---

**Q26.20: Foundational - [Theory] - [String Comparison]**

Comparing algorithms for single-pattern matching:

A) Naive: O(nm), no preprocessing, simple
B) KMP: O(n+m), character-by-character, no backtracking
C) Boyer-Moore: O(n/m) best, right-to-left, practical fastest
D) Rabin-Karp: O(n+m) expected, hash-based, good for multi-pattern

**Answer: D**

**Explanation:**
Algorithm choice depends on use case:

| Algorithm | Preprocess | Search | Best For |
|-----------|-----------|--------|----------|
| Naive | O(1) | O(nm) | Short patterns |
| KMP | O(m) | O(n) | Streaming/guaranteed |
| Boyer-Moore | O(m+σ) | O(n/m)–O(n) | Large alphabet, practical |
| Rabin-Karp | O(m) | O(n) avg | Multiple patterns |

---

**Q26.21: Intermediate - [Theory] - [Minimum Rotation]**

Lexicographically smallest rotation:

A) Booth's algorithm: O(n) time, O(n) space
B) Duval-based: O(n) time, O(1) space
C) Important for: canonical form of cyclic strings
D) All of the above

**Answer: D**

**Explanation:**
Smallest rotation: given s, find rotation r such that s[r..]+s[..r-1] is lexicographically smallest. Booth's: modified failure function on concatenated string s+s. O(n). Duval's approach: Lyndon factorization of s+s gives minimum rotation. Applications: canonical form for cyclic molecules (chemistry), necklace problems, isomorphism of cyclic strings.

---

**Q26.22: Foundational - [Theory] - [String Distance Metrics]**

String distance metrics:

A) Hamming distance: same length, count mismatched positions
B) Edit distance: insertions, deletions, substitutions (Chapter 22)
C) Longest common subsequence distance: n + m - 2×LCS
D) All of the above

**Answer: D**

**Explanation:**
Hamming: only for equal-length strings, O(n). Edit (Levenshtein): most general, O(nm) DP. LCS distance: edit distance restricted to insert+delete only. Jaccard distance: set-based (for token comparison). Jaro-Winkler: for short strings (names). Choose metric based on application: spell checking, DNA alignment, record linkage.

---

**Q26.23: Advanced - [Theory] - [Suffix Array Construction Algorithms]**

Suffix array construction algorithms:

A) Naive: sort suffixes O(n² log n)
B) Prefix doubling: O(n log² n) or O(n log n) with radix sort
C) DC3/Skew, SA-IS: O(n) linear time
D) All of the above

**Answer: D**

**Explanation:**
Construction spectrum: Naive O(n² log n): sort suffixes as strings. Prefix doubling: sort by first 1, 2, 4, ... characters. O(log n) rounds × O(n log n) sort = O(n log² n). With radix sort: O(n log n). DC3 (Kärkkäinen-Sanders): O(n) but complex. SA-IS (Nong et al.): O(n), practical, and elegant. SA-IS is the preferred O(n) algorithm in practice.

---

**Q26.24: Expert - [Theory] - [Compressed String Indices]**

Compressed string indices:

A) FM-index: BWT-based, count occurrences in O(m), locate in O(m + occ × log n)
B) Compressed suffix array: O(n/log n) space
C) Wavelet tree: supports rank/select queries on strings
D) All of the above

**Answer: D**

**Explanation:**
FM-index: BWT + rank queries. Count pattern occurrences without storing original text. O(m) counting, O(m + occ × log^ε n) locating. Space: O(n × H_k) where H_k = k-th order empirical entropy. Wavelet tree: represent BWT, support rank/select in O(log σ). State-of-art for compressed text indexing. Powers modern bioinformatics tools.

---

**Q26.25: Intermediate - [Theory] - [String Matching Automaton]**

String matching automaton:

A) Build DFA that recognizes *T*P (any text followed by pattern)
B) O(m×σ) preprocessing (σ = alphabet size)
C) O(n) matching (single pass through text)
D) All of the above

**Answer: D**

**Explanation:**
DFA approach: states 0..m, transition δ(q, c) = longest prefix of P that is suffix of P[0..q-1]+c. Building DFA: O(m×σ). Matching: scan text, follow transitions, state m = match. O(n) matching, no backtracking. Trade-off: more preprocessing than KMP but simpler matching. KMP achieves same O(n) matching with O(m) preprocessing (σ-independent).

---

**Q26.26: Expert - [Theory] - [Approximate String Matching]**

Approximate string matching:

A) Find pattern in text allowing k errors
B) DP approach: O(nm) — modification of edit distance
C) Bit-parallel: O(nm/w) using word-level parallelism
D) All of the above

**Answer: D**

**Explanation:**
Approximate matching: find substrings of T within edit distance k from P. DP: like edit distance but row 0 initialized to 0 (match can start anywhere). Any dp[m][j] ≤ k = match ending at j. O(nm). Bit-parallel (Myers 1999): pack DP into bitvectors, O(nm/w) where w=64. For k small: O(nk) with Ukkonen's cutoff. Real-world: agrep, fuzzy search.

---

**Q26.27: Foundational - [Theory] - [Pattern Matching Applications]**

String matching applications:

A) Text editors: find/replace
B) Bioinformatics: DNA/protein sequence search
C) Intrusion detection: match known attack signatures
D) All of the above, plus plagiarism detection, search engines

**Answer: D**

**Explanation:**
String matching is everywhere: text search (grep, IDE find), web search (indexing), biology (BLAST, sequence alignment), security (IDS pattern matching), data mining (log analysis), compression (LZ-family uses string matching). Different applications need different algorithms: single pattern (KMP/BM), multiple patterns (Aho-Corasick), approximate (edit distance DP).

---

**Q26.28: Expert - [Theory] - [Tandem Repeats]**

Finding tandem repeats:

A) Substring that is a concatenation of copies of a shorter string
B) Main-Lorentz algorithm: O(n log n) for all tandem repeats
C) Applications: DNA microsatellite detection, compression
D) All of the above

**Answer: D**

**Explanation:**
Tandem repeat: s[i..i+2p-1] where s[i..i+p-1] = s[i+p..i+2p-1]. Finding all: up to O(n log n) tandem repeats exist. Main-Lorentz: divide and conquer, O(n log n). Crochemore's: find all runs (maximal repetitions) in O(n). DNA tandem repeats: important for genetic markers, disease association. Compression: run-length encoding exploits tandem repeats.

---

**Q26.29: Advanced - [Theory] - [Knuth-Morris-Pratt Applications]**

KMP beyond pattern matching:

A) Period of a string: n - π[n-1] (if n % period == 0)
B) All border lengths: follow failure function chain
C) Counting pattern occurrences in text
D) All of the above

**Answer: D**

**Explanation:**
KMP failure function encodes string structure. Period: smallest p where s[i] = s[i+p]. p = n - π[n-1]. If n % p ≠ 0: no exact period but n-π[n-1] is the shortest "quasi-period." All borders (strings that are both prefix and suffix): follow π chain from π[n-1] → π[π[n-1]-1] → ... Powerful structural analysis tool.

---

**Q26.30: Intermediate - [Theory] - [Longest Common Substring]**

Longest common substring of two strings:

A) Suffix array: concatenate with separator, find max LCP between different-string suffixes
B) DP: O(nm) — dp[i][j] = length ending at (i,j) matches
C) Binary search + hashing: O((n+m) log min(n,m))
D) All valid approaches

**Answer: D**

**Explanation:**
LCS (substring, not subsequence): contiguous common part. Suffix array: concatenate s1+"$"+s2, build SA+LCP. Max LCP between adjacent suffixes from different strings. O(n+m). DP: dp[i][j] = dp[i-1][j-1]+1 if match, 0 otherwise. O(nm). Hashing: binary search on length, check existence with hash set. O((n+m) log n).

---

**Q26.31: Expert - [Theory] - [Online Pattern Matching]**

Online string matching:

A) Characters arrive one at a time, report matches immediately
B) KMP: naturally online (text pointer only moves forward)
C) Suffix automaton: online construction, query at each step
D) All of the above

**Answer: D**

**Explanation:**
Online: process text character by character. KMP: when new char arrives, advance state, report if state = m. O(1) per character. Suffix automaton: add character, update automaton in O(1) amortized. At each step: can query all substrings seen so far. Streaming applications: network monitoring, real-time text analysis, log processing.

---

**Q26.32: Advanced - [Theory] - [Multiple Pattern Matching Comparison]**

Multi-pattern matching approaches:

A) Aho-Corasick: O(n + Σ|P_i| + z), automaton-based
B) Rabin-Karp: O(n × k) with k patterns (expected)
C) Commentz-Walter: Boyer-Moore generalization, sublinear
D) All valid, Aho-Corasick most general

**Answer: D**

**Explanation:**
Multiple patterns: Aho-Corasick builds combined automaton, single scan of text. O(n + m_total + matches). Rabin-Karp: hash each window, check against pattern hash set. O(n × avg_pattern_length). Commentz-Walter: combines Boyer-Moore's right-to-left with trie-based multi-pattern, can skip text portions. Choose based on pattern count, lengths, and alphabet.

---

**Q26.33: Expert - [Theory] - [Sequence Alignment (Bioinformatics)]**

Sequence alignment algorithms:

A) Needleman-Wunsch: global alignment (full-length), O(nm) DP
B) Smith-Waterman: local alignment (best substring pair), O(nm) DP
C) BLAST: heuristic, seed-and-extend, much faster for databases
D) All of the above

**Answer: D**

**Explanation:**
DNA/protein alignment: fundamental bioinformatics operation. Needleman-Wunsch: edit distance variant with gap penalties. Smith-Waterman: same but allow starting/ending anywhere (min value = 0, not negative). Both O(nm). BLAST: seed with exact k-mer matches, extend seeds. Heuristic O(n) per sequence. Searches billion-letter databases in seconds.

---

**Q26.34: Expert - [Theory] - [Regular Expression Matching]**

Regular expression matching:

A) NFA construction from regex: Thompson's algorithm O(m)
B) NFA simulation: O(nm) — processes text with NFA
C) NFA → DFA conversion: exponential worst case (2^m states)
D) All of the above

**Answer: D**

**Explanation:**
Regex matching: build NFA from regex (Thompson's construction, O(m)). Simulate NFA on text: track set of active states, O(nm). Or convert to DFA: O(1) per text char but DFA can have 2^m states. Hybrid: lazy DFA construction (build states on demand, cache). Backtracking regex engines (Perl, Python): can be exponential — catastrophic backtracking. Use Thompson NFA for guaranteed O(nm).

---

**Q26.35: Intermediate - [Theory] - [Anagram/Permutation Search]**

Find all anagram occurrences:

A) Sliding window of pattern length over text
B) Character frequency comparison or hash
C) O(n × σ) with frequency arrays, O(n) with rolling comparison
D) All of the above

**Answer: D**

**Explanation:**
Anagram search: find all windows in text that are permutations of pattern. Frequency approach: maintain character count for window, compare with pattern count. Slide window: add new char, remove old. Compare: O(σ) per position → O(nσ). Optimization: track "matching count" incrementally → O(n).

---

## Chapter 26 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 8 | Naive, KMP, Rabin-Karp, rolling hash, string distances, applications |
| Intermediate | 13 | Boyer-Moore, Z-function, suffix array/tree, LCP, Aho-Corasick, Manacher's |
| Advanced | 8 | Suffix automaton, BWT, palindromic tree, Lyndon, SA construction |
| Expert | 6 | FM-index, approximate match, tandem repeats, regex NFA, BLAST |

**Total MCQs: 35**

**Next:** Chapter 27 - Advanced Graph Algorithms
