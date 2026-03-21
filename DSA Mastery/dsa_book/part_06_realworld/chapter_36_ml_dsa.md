# Chapter 36: Machine Learning DS&A

**Target:** 25 MCQs | **Distribution:** 6 Foundational, 10 Intermediate, 6 Advanced, 3 Expert

---

**Q36.1: Foundational - [Theory] - [KD-Tree Purpose]**

KD-Trees are primarily used in machine learning for:

A) Sorting training data
B) Efficient nearest neighbor search in multi-dimensional space
C) Training neural networks
D) Text tokenization

**Answer: B**

**Explanation:**
KD-Tree: binary tree partitioning k-dimensional space. At each level, split on one dimension (cycling through dimensions). Nearest neighbor: prune branches that can't contain closer points. Average O(log n) for low dimensions. KNN classifier uses KD-Trees for fast neighbor finding. Degrades in high dimensions (curse of dimensionality) — for d > 20, approximate methods (LSH) preferred.

---

**Q36.2: Foundational - [Theory] - [Gradient Descent]**

Gradient descent is fundamentally:

A) A sorting algorithm
B) An iterative optimization algorithm that follows the negative gradient to find minima
C) A graph traversal algorithm
D) A data compression technique

**Answer: B**

**Explanation:**
Gradient descent: compute gradient (direction of steepest ascent) of loss function, move in opposite direction (steepest descent). Update: θ = θ - α∇L(θ). Repeat until convergence. Variants: batch (full dataset), SGD (single sample), mini-batch (subset). Learning rate α: too large → diverge, too small → slow. Foundation of all neural network training. O(n × d) per epoch for n samples, d features.

---

**Q36.3: Intermediate - [Theory] - [Hash Functions in ML]**

Locality-Sensitive Hashing (LSH) differs from standard hashing in that:

A) It minimizes collisions between all inputs
B) It intentionally causes similar items to hash to the same bucket
C) It produces longer hash values
D) It only works for numeric data

**Answer: B**

**Explanation:**
Standard hashing: minimize collisions (different items → different buckets). LSH: MAXIMIZE collisions for SIMILAR items (nearby points → same bucket). For cosine similarity: random hyperplane LSH. For Jaccard: MinHash LSH. Approximate nearest neighbor: hash query, check items in same bucket. Sub-linear query time. Used in: recommendation systems, duplicate detection, image similarity. Key enabler for billion-scale similarity search.

---

**Q36.4: Intermediate - [Complexity] - [KNN Complexity]**

K-Nearest Neighbors classification with n training samples and d dimensions has what time complexity per query (without any index structure)?

A) O(1)
B) O(log n)
C) O(n × d)
D) O(n²)

**Answer: C**

**Explanation:**
Brute-force KNN: compute distance from query to all n training points. Each distance: O(d) (Euclidean in d dimensions). Total: O(n × d). Then find k smallest: O(n log k) with heap. Dominant: O(n × d). With KD-Tree: O(d × log n) average (low d). With LSH: sub-linear approximate. For d > 20: KD-Tree degrades to O(n × d). High-dimensional KNN is fundamentally expensive.

---

**Q36.5: Foundational - [Theory] - [Decision Tree Splitting]**

Decision trees choose split points by:

A) Random selection
B) Maximizing information gain (or minimizing Gini impurity)
C) Alphabetical ordering of features
D) Using the median value always

**Answer: B**

**Explanation:**
Decision tree: at each node, find feature and threshold that best separates classes. Metrics: information gain (reduction in entropy), Gini impurity (probability of misclassification). For each feature: try all thresholds, compute metric, pick best. Greedy: locally optimal split at each node. O(n × d × log n) per level with sorting. ID3: information gain. CART: Gini impurity. Both produce similar trees in practice.

---

**Q36.6: Intermediate - [Theory] - [Random Forest]**

Random forests reduce overfitting compared to single decision trees by:

A) Using a single deep tree
B) Training many trees on random subsets of data and features, then voting
C) Pruning all trees to depth 1
D) Using neural networks inside each tree

**Answer: B**

**Explanation:**
Random forest (Breiman): ensemble of decision trees. Each tree trained on: bootstrap sample (random rows with replacement) + random subset of features at each split. Individual trees may overfit, but averaging/voting reduces variance. Uncorrelated errors cancel out. Feature randomization ensures tree diversity. O(n × d × T × log n) for T trees. Robust, parallelizable, and hard to overfit — one of the most reliable ML algorithms.

---

**Q36.7: Advanced - [Theory] - [VP-Tree]**

A VP-Tree (Vantage Point Tree) is preferred over KD-Tree when:

A) The data has low dimensionality
B) The distance metric is non-Euclidean (e.g., edit distance, custom metrics)
C) The data is sorted
D) Only range queries are needed

**Answer: B**

**Explanation:**
KD-Tree: splits on individual dimensions (axis-aligned). Only works with coordinate-based metrics. VP-Tree: splits based on distance from a vantage point. Works with ANY distance metric (even non-metric with modifications). For string similarity (edit distance), molecular structure distances, etc.: VP-Tree is natural. Partitions: points closer vs farther than median distance from vantage. O(log n) search average. Better for general metric spaces.

---

**Q36.8: Intermediate - [Theory] - [ANN Index]**

HNSW (Hierarchical Navigable Small World) graphs provide approximate nearest neighbor search with:

A) O(n) query time
B) O(log n) query time with high recall
C) O(1) query time
D) O(n²) query time

**Answer: B**

**Explanation:**
HNSW: multi-layer graph where upper layers are sparse (for fast coarse navigation) and bottom layer is dense (for accurate local search). Query: start at top layer, greedily move toward query point, descend to lower layers for finer search. O(log n) layers, constant work per layer. Recall > 99% typical. Used in: Pinecone, Milvus, FAISS. State-of-the-art for billion-scale vector similarity search.

---

**Q36.9: Advanced - [Theory] - [Feature Hashing]**

Feature hashing (hashing trick) reduces dimensionality by:

A) Selecting the k most important features
B) Hashing feature names to a fixed-size vector, allowing collisions
C) PCA projection
D) Removing features with low variance

**Answer: B**

**Explanation:**
Feature hashing: hash each feature to an index in fixed-size array (e.g., 2^18). Multiple features may collide (map to same index). Surprisingly works well: collisions act as noise, and with signed hashing (±1 sign function), expected dot product is preserved. Advantages: no dictionary needed, fixed memory, handles streaming/new features. Used in Vowpal Wabbit, spam filtering with millions of text features.

---

**Q36.10: Foundational - [Theory] - [Curse of Dimensionality]**

The curse of dimensionality causes nearest neighbor search to fail in high dimensions because:

A) Hash functions stop working
B) All points become roughly equidistant, making "nearest" meaningless
C) Memory usage decreases
D) Data becomes sorted automatically

**Answer: B**

**Explanation:**
In high dimensions: distance to nearest neighbor approaches distance to farthest neighbor. Ratio → 1 as d → ∞. If all points are roughly equidistant, "nearest" is not meaningful — any point is about as close as any other. KD-Trees degrade to linear scan for d > 20. Solutions: dimensionality reduction (PCA, random projection), approximate methods (LSH), learned embeddings. Fundamental limit of geometric methods in high-d.

---

**Q36.11: Intermediate - [Theory] - [Inverted Index in Search]**

Inverted indexes enable fast text search by:

A) Sorting all documents alphabetically
B) Mapping each term to the list of documents containing it
C) Compressing documents to reduce size
D) Translating queries to a different language

**Answer: B**

**Explanation:**
Inverted index: term → [doc1, doc5, doc12, ...]. Query "machine learning": intersection of postings list for "machine" and "learning". With sorted postings: merge-intersect in O(n+m). With skip pointers: even faster. TF-IDF scoring: rank by term frequency × inverse document frequency. Foundation of: Elasticsearch, Solr, Google Search. O(1) term lookup + O(k) result retrieval for k matching docs.

---

**Q36.12: Expert - [Theory] - [Product Quantization]**

Product quantization for approximate nearest neighbor works by:

A) Sorting vectors by magnitude
B) Splitting vectors into subvectors and quantizing each independently
C) Hashing vectors to binary codes
D) Training a neural network on vectors

**Answer: B**

**Explanation:**
Product quantization: split d-dimensional vector into m sub-vectors of d/m dimensions. For each subspace: train k-means with K centroids (codebook). Encode each sub-vector as its nearest centroid index (log₂K bits). Distance: sum of precomputed sub-distances from lookup table. Memory: m × log₂K bits per vector (vs d × 32 bits). FAISS (Facebook): uses PQ for billion-scale search. 128-d vector: 8 bytes (not 512). ~100× compression with ~1% accuracy loss.

---

**Q36.13: Intermediate - [Theory] - [Trie in NLP]**

Tries are used in NLP autocomplete systems because:

A) They compress text data
B) They enable prefix-based search in O(L) time (L = prefix length)
C) They sort words alphabetically
D) They remove duplicate words

**Answer: B**

**Explanation:**
Trie: tree where each path from root represents a string prefix. Autocomplete "pro": traverse to 'p'→'r'→'o', then enumerate all descendants = all words starting with "pro". O(L) to reach prefix node + O(k) to enumerate k completions. Hash map: can't enumerate by prefix. Sorted array + binary search: O(L × log n). Trie is ideal for prefix queries. Compressed tries (Patricia/radix trees) reduce memory.

---

**Q36.14: Advanced - [Theory] - [Bloom Filter in ML Pipeline]**

In ML data pipelines, Bloom filters are used for:

A) Training models faster
B) De-duplicating training examples efficiently
C) Computing gradients
D) Storing model weights

**Answer: B**

**Explanation:**
Deduplication: before adding a training example, check Bloom filter. If "maybe present": check exact store. If "definitely not present": add to training set and Bloom filter. False positives: occasionally skip a non-duplicate (minor). False negatives: never — ensures no duplicates in final dataset. For web-scale datasets (billions of URLs/documents): exact de-duplication infeasible. Bloom filter: constant space per element, O(1) check.

---

**Q36.15: Foundational - [Theory] - [Priority Queue in ML]**

Priority queues (heaps) are used in which ML algorithm?

A) K-Nearest Neighbors (maintaining k closest points)
B) Linear regression
C) Logistic regression
D) Principal Component Analysis

**Answer: A**

**Explanation:**
KNN: finding k nearest neighbors. Maintain max-heap of size k. For each training point: if distance < heap's max, replace and heapify. After scanning all points: heap contains k closest. O(n log k) total. Without heap: O(n × k) or O(n log n) full sort. Heaps also used in beam search (NLP decoding), Dijkstra's in graph-based ML, and A* search in planning.

---

**Q36.16: Expert - [Theory] - [Ball Tree]**

Ball trees improve over KD-Trees in high dimensions because:

A) They use simpler data structures
B) They use hypersphere partitions that better capture cluster geometry
C) They require less memory
D) They only work in 2D

**Answer: B**

**Explanation:**
KD-Tree: axis-aligned hyperplane splits. In high-d: hyper-rectangles have large volume → poor pruning. Ball tree: partition into hyperspheres (balls). Each node: center point + radius enclosing all descendants. Query: if distance to center - radius > current best, prune entire subtree. Balls tighter than rectangles in high-d → better pruning. Still degrades in very high d, but outperforms KD-Trees for d=20-100. Scikit-learn implements both.

---

**Q36.17: Intermediate - [Theory] - [Skip List in Redis]**

Redis uses skip lists for sorted sets. What advantage do skip lists have over balanced BSTs for this use case?

A) Lower time complexity for all operations
B) Simpler implementation with comparable O(log n) performance and easy range scans
C) Better space efficiency
D) Faster hash table lookups

**Answer: B**

**Explanation:**
Skip list: randomized, O(log n) expected search/insert/delete. Advantages over balanced BST (red-black, AVL): (1) Simpler to implement and debug, (2) Easy range queries (follow linked list at bottom), (3) Lock-free concurrent versions simpler to build, (4) Cache-friendly sequential access in bottom list. Redis choice: skip list + hash map for O(1) by-member lookup + O(log n) by-score access. Practical simplicity wins.

---

**Q36.18: Advanced - [Theory] - [Count-Min Sketch]**

A Count-Min Sketch estimates element frequencies with:

A) Exact counts guaranteed
B) Overestimates (never undercounts), with error decreasing as more hash functions used
C) Exact counts only for elements above a threshold
D) Undercounts only

**Answer: B**

**Explanation:**
Count-Min Sketch: d hash functions, each mapping to a row of w counters. Insert: increment d counters. Query: take minimum of d counters. Always ≥ true count (hash collisions only ADD to counters). Error: ε = e/w with probability 1 - δ = 1 - (1/e)^d. Trade space (d×w) for accuracy. Used in: network traffic monitoring, trending topics, heavy hitter detection. O(d) per query, O(d×w) total space.

---

## Chapter 36 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | KD-Tree, gradient descent, decision trees, curse of dimensionality, priority queue in ML |
| Intermediate | 7 | LSH, KNN complexity, random forest, HNSW, inverted index, trie in NLP, skip list |
| Advanced | 4 | VP-Tree, feature hashing, Bloom in ML, ball tree |
| Expert | 2 | Product quantization, Count-Min Sketch |

**Total MCQs: 18**

**Answer Distribution: A=3, B=14, C=0, D=1**

**Next:** Chapter 37 - Concurrency & Parallel Algorithms
