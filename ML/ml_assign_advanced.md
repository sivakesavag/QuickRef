# Machine Learning Advanced Level Assignments (1-155)

> **Level**: Advanced | **Total Assignments**: 155 | **Prerequisites**: Intermediate Level | **Focus**: Deep Learning, NLP, Time Series, Model Interpretability, Advanced Techniques

## Summary

| Section | Topic | Questions |
|---------|-------|-----------|
| A | Advanced Feature Engineering | 25 |
| B | Natural Language Processing | 28 |
| C | Time Series Analysis | 25 |
| D | Deep Learning Fundamentals | 30 |
| E | Model Interpretability & Explainability | 22 |
| F | Anomaly Detection | 25 |
| **Total** | | **155** |

---

## Section A: Advanced Feature Engineering (A1-A25)

### A1: Automated Feature Selection
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply multiple automated feature selection methods: filter (variance, correlation, mutual information), wrapper (RFE, forward/backward), and embedded (Lasso, tree importance).

**Expected Deliverables**:
- Filter method implementations
- Recursive Feature Elimination
- Lasso-based selection
- Comparison of methods

**Test Cases**:
1. Reduce features by 50%
2. Compare selection by different methods
3. Performance vs number of features

**Hints**: Start with filter methods (fast), validate with wrapper methods.

**Skills**: Feature selection, dimension reduction

---

### A2: Target Encoding from Scratch
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Implement target encoding for categorical variables with proper handling of overfitting: smoothing, leave-one-out, and cross-validation encoding.

**Mathematical Foundation**:
- Basic: E[y | category]
- Smoothing: (n × mean_category + m × global_mean) / (n + m)

**Expected Deliverables**:
- Basic target encoding
- Smoothing implementation
- CV-based encoding to prevent leakage

**Test Cases**:
1. Handle rare categories
2. Prevent target leakage
3. Compare with one-hot

**Hints**: Use cross-validation to compute encoding for each fold separately.

**Skills**: Target encoding, leakage prevention

---

### A3: Feature Interactions and Polynomials
**Domain**: Feature Engineering | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Create polynomial features and interaction terms systematically. Understand computational explosion and use selection to manage feature count.

**Expected Deliverables**:
- PolynomialFeatures usage
- Interaction-only features
- Selection of useful interactions

**Test Cases**:
1. Degree 2 interactions
2. Feature count growth analysis
3. Select important interactions only

**Hints**: Interaction-only first (fewer features). Use feature selection after.

**Skills**: Polynomial features, interactions

---

### A4: Date and Time Feature Engineering
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Extract comprehensive features from datetime: cyclical encoding, holidays, business days, time since events, seasonality components.

**Expected Deliverables**:
- Cyclical encoding (sin/cos)
- Holiday features
- Time-based aggregations
- Lag features

**Test Cases**:
1. Hour of day cyclical
2. Day of week with holidays
3. Time since last event

**Hints**: Use sin/cos for cyclical features. Consider business context.

**Skills**: Datetime feature engineering

---

### A5: Text Feature Engineering
**Domain**: NLP/Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Extract features from text beyond bag-of-words: TF-IDF ngrams, word embeddings, sentiment, readability, and custom patterns.

**Expected Deliverables**:
- TF-IDF with ngrams
- Word embedding aggregation
- Sentiment and readability
- Regex-based features

**Test Cases**:
1. Extract email domains
2. Count specific patterns
3. Combine text features with tabular

**Hints**: Pre-trained embeddings save time. Word2Vec or GloVe average.

**Skills**: Text feature extraction

---

### A6: Geographical Feature Engineering
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Create features from geographical data: distance calculations, clustering, reverse geocoding, proximity to points of interest.

**Expected Deliverables**:
- Haversine distance
- Geographical clustering
- POI proximity features
- Area/region encoding

**Test Cases**:
1. Distance to center
2. Nearest POI features
3. Geo-cluster assignment

**Hints**: Use geopy for distances. H3 hexagonal grid for clustering.

**Skills**: Geospatial features

---

### A7: Window-Based Feature Engineering
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Create rolling window features for sequential data: aggregations, trends, ratios, and cumulative features over various window sizes.

**Expected Deliverables**:
- Rolling mean, std, min, max
- Expanding window features
- Ratio and difference features
- Multi-window comparison

**Test Cases**:
1. 7-day vs 30-day rolling
2. Trend detection features
3. Anomaly indicators

**Hints**: Multiple window sizes capture different patterns. Pandas rolling is powerful.

**Skills**: Window features, time-based aggregations

---

### A8: Entity Embeddings
**Domain**: Feature Engineering | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Learn low-dimensional embeddings for categorical features using neural networks. These capture semantic relationships between categories.

**Mathematical Foundation**:
- Embedding layer: lookup table of learned vectors
- End-to-end learning with prediction task

**Expected Deliverables**:
- Embedding layer in neural network
- Visualization of learned embeddings
- Transfer to other models

**Test Cases**:
1. Train neural network with embeddings
2. Extract and visualize embeddings
3. Use in gradient boosting

**Hints**: Use TensorFlow/PyTorch embedding layers. Similar items cluster.

**Skills**: Entity embeddings, deep learning for features

---

### A9: Feature Hashing (Hashing Trick)
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Apply feature hashing for memory-efficient encoding of high-cardinality categoricals. Understand collision tradeoffs.

**Mathematical Foundation**:
- Hash function maps categories to fixed buckets
- Signed hashing reduces collision impact

**Expected Deliverables**:
- FeatureHasher usage
- Collision analysis
- Memory comparison with one-hot

**Test Cases**:
1. 1000 categories to 100 dimensions
2. Collision rate analysis
3. Accuracy vs memory tradeoff

**Hints**: More buckets = fewer collisions. 2^20 buckets common for text.

**Skills**: Feature hashing, scalable encoding

---

### A10: Binning and Discretization
**Domain**: Feature Engineering | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Apply various binning strategies: uniform, quantile, k-means clustering, and custom business rules. Understand when binning helps.

**Expected Deliverables**:
- KBinsDiscretizer usage
- Quantile vs uniform comparison
- Custom binning with business logic

**Test Cases**:
1. Compare binning strategies
2. When binning improves trees
3. Information loss analysis

**Hints**: Quantile bins have equal counts. Trees can find optimal splits anyway.

**Skills**: Discretization, binning strategies

---

### A11: Missing Value Features
**Domain**: Feature Engineering | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Create features from missing value patterns: missing indicators, count of missing per row, patterns that predict missingness.

**Expected Deliverables**:
- Missing indicator features
- Missing count features
- Pattern-based features

**Test Cases**:
1. Add missing indicator columns
2. Count missing per sample
3. Missingness predicts target

**Hints**: Missingness often has meaning (e.g., didn't answer = not interested).

**Skills**: Missing data as information

---

### A12: Feature Aggregations by Group
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Create aggregate features by grouping: statistics per customer, per category, relative to group. Essential for relational data.

**Expected Deliverables**:
- Group-level statistics
- Rank within group
- Relative to group mean/median

**Test Cases**:
1. Customer historical aggregates
2. Product category statistics
3. Percentile within group

**Hints**: Pandas groupby + transform. Avoid leakage from current row.

**Skills**: Group aggregations, relational features

---

### A13: Frequency Encoding
**Domain**: Feature Engineering | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Encode categories by their frequency in training data. Simple, effective, and robust alternative to one-hot for high-cardinality.

**Expected Deliverables**:
- Frequency encoding implementation
- When frequency predicts target
- Comparison with other encodings

**Test Cases**:
1. Replace category with count
2. Handle unseen categories
3. Normalize vs raw counts

**Hints**: Popular categories might have different patterns. Simple but effective.

**Skills**: Frequency encoding

---

### A14: Weight of Evidence Encoding
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Implement Weight of Evidence encoding for binary classification. Calculate Information Value for feature selection.

**Mathematical Foundation**:
- WoE = ln(% positive / % negative)
- IV = Σ (% pos - % neg) × WoE

**Expected Deliverables**:
- WoE encoding implementation
- Information Value calculation
- Feature selection by IV

**Test Cases**:
1. Calculate WoE per category
2. Rank features by IV
3. Handle edge cases (0 counts)

**Hints**: IV > 0.3 is strong predictive power. Add smoothing for zeros.

**Skills**: WoE, Information Value

---

### A15: Feature Engineering for Trees vs Linear
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Understand different feature engineering needs: trees handle non-linearity but need interaction hints; linear models need explicit transformations.

**Expected Deliverables**:
- Features for linear models
- Features for tree models
- Feature importance comparison

**Test Cases**:
1. Same data, different features per model
2. Performance comparison
3. When manual features help trees

**Hints**: Trees don't need scaling. Linear models benefit from log transforms.

**Skills**: Model-specific features

---

### A16: Outlier-Based Features
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Create features based on outlier detection: distance to center, isolation scores, statistical deviation measures.

**Expected Deliverables**:
- Z-score features
- Isolation Forest scores
- Mahalanobis distance

**Test Cases**:
1. Flag outliers per feature
2. Combined outlier score
3. Use as features not filters

**Hints**: Outlier features can be predictive even if outliers aren't removed.

**Skills**: Outlier-based features

---

### A17: Clustering-Based Features
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Use clustering to create features: cluster assignments, distances to centroids, soft cluster memberships.

**Expected Deliverables**:
- K-Means cluster features
- GMM soft assignments
- Distance to each centroid

**Test Cases**:
1. Add cluster labels as features
2. Distance features to centroids
3. Improve model with cluster features

**Hints**: Cluster on subsets of features. Multiple clusterings with different K.

**Skills**: Clustering for features

---

### A18: Decomposition-Based Features
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Use matrix decomposition to create features: PCA components, NMF factors, SVD for sparse data.

**Expected Deliverables**:
- PCA-based features
- NMF for non-negative data
- TruncatedSVD for sparse

**Test Cases**:
1. Top k PCA components
2. NMF for interpretable factors
3. Combine with original features

**Hints**: Decomposition captures latent patterns. Use alongside original features.

**Skills**: Decomposition features

---

### A19: Target Transformation
**Domain**: Feature Engineering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Transform target variable for better model performance: log, Box-Cox, Yeo-Johnson. Handle skewed distributions.

**Mathematical Foundation**:
- Box-Cox: (y^λ - 1) / λ for λ ≠ 0
- Yeo-Johnson: handles negatives

**Expected Deliverables**:
- Log transformation
- Box-Cox with optimal lambda
- Yeo-Johnson for any data

**Test Cases**:
1. Transform skewed target
2. Find optimal lambda
3. Inverse transform predictions

**Hints**: TransformedTargetRegressor handles transform/inverse automatically.

**Skills**: Target transformation

---

### A20: Feature Store Design
**Domain**: MLOps/Feature Engineering | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Conceptual + Libraries

**Problem**: Design a feature store for reusable feature computation: offline/online serving, versioning, monitoring, and sharing.

**Expected Deliverables**:
- Feature store architecture
- Offline computation pipeline
- Online serving considerations
- Feast or similar tool exploration

**Test Cases**:
1. Define feature groups
2. Compute and store features
3. Retrieve for training and serving

**Hints**: Feast is open-source feature store. Separate compute from serving.

**Skills**: Feature store, MLOps

---

### A21: Feature Generation with Symbolic Regression
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Use genetic programming for automatic feature generation. Discover interpretable mathematical expressions.

**Expected Deliverables**:
- GPLearn symbolic regression
- Discovered expressions analysis
- Use discovered features

**Test Cases**:
1. Evolve feature expressions
2. Interpret discovered formulas
3. Improve model with generated features

**Hints**: Use gplearn library. Can discover non-obvious relationships.

**Skills**: Symbolic regression, genetic programming

---

### A22: Feature Engineering Competition
**Domain**: Practice | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Apply comprehensive feature engineering to a competition dataset. Iterate through feature creation, selection, and validation.

**Dataset**: Kaggle tabular competition data

**Expected Deliverables**:
- Complete feature engineering pipeline
- Feature importance analysis
- Ablation study of features

**Test Cases**:
1. Significant improvement from features
2. Feature importance ranking
3. Feature ablation results

**Hints**: Start simple, add complexity. Always validate with CV.

**Skills**: Competition feature engineering

---

### A23: Feature Engineering for Specific Domains
**Domain**: Domain-Specific | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply domain-specific feature engineering: finance (returns, volatility), retail (RFM), healthcare (clinical scores).

**Expected Deliverables**:
- Domain-specific feature set
- Industry standard calculations
- Business interpretation

**Test Cases**:
1. RFM features for retail
2. Technical indicators for finance
3. Clinical risk scores

**Hints**: Domain knowledge creates the best features. Consult domain experts.

**Skills**: Domain-specific engineering

---

### A24: Feature Pipeline Automation
**Domain**: MLOps | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Create automated feature engineering pipeline: preprocessing, transformation, and feature creation in reproducible pipeline.

**Expected Deliverables**:
- Sklearn Pipeline with ColumnTransformer
- Custom transformers
- Pipeline persistence

**Test Cases**:
1. End-to-end pipeline
2. Pipeline serialization
3. Consistent train/test processing

**Hints**: Use sklearn ColumnTransformer for different column types.

**Skills**: Pipeline automation

---

### A25: Feature Engineering Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete feature engineering project from raw data to production-ready features. Document decisions and create reproducible pipeline.

**Expected Deliverables**:
- Comprehensive feature engineering
- Selection and validation
- Production pipeline
- Documentation

**Evaluation Criteria**: Feature quality, methodology, reproducibility

**Hints**: Focus on business value and interpretability.

**Skills**: Complete feature engineering mastery

---

## Section B: Natural Language Processing (B1-B28)

### B1: Text Preprocessing Pipeline
**Domain**: NLP | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Build comprehensive text preprocessing: lowercasing, punctuation removal, tokenization, stopword removal, lemmatization/stemming.

**Expected Deliverables**:
- Preprocessing pipeline
- Tokenization (word, sentence)
- Stemming vs lemmatization comparison

**Test Cases**:
1. Clean noisy text
2. Handle edge cases (URLs, emails)
3. Compare stemming vs lemmatization

**Hints**: Use NLTK or spaCy. Lemmatization is usually better than stemming.

**Skills**: Text preprocessing

---

### B2: Bag of Words and TF-IDF
**Domain**: NLP | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Implement bag-of-words and TF-IDF vectorization. Understand term frequency, inverse document frequency, and sparse representations.

**Mathematical Foundation**:
- TF: count(term, doc) / len(doc)
- IDF: log(N / df(term))
- TF-IDF: TF × IDF

**Expected Deliverables**:
- CountVectorizer usage
- TfidfVectorizer usage
- Sparse matrix handling

**Test Cases**:
1. Create document-term matrix
2. Compare BoW vs TF-IDF
3. Handle vocabulary size

**Hints**: Set max_features, min_df, max_df to control vocabulary size.

**Skills**: Text vectorization, TF-IDF

---

### B3: N-grams and Skip-grams
**Domain**: NLP | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Understand n-grams (contiguous sequences) and skip-grams (non-contiguous). Use character and word-level n-grams.

**Expected Deliverables**:
- Word unigrams, bigrams, trigrams
- Character n-grams
- Skip-gram concept

**Test Cases**:
1. Extract n-grams from text
2. Character n-grams for typo handling
3. N-gram feature comparison

**Hints**: Bigrams capture phrases. Character n-grams handle misspellings.

**Skills**: N-grams, text features

---

### B4: Word Embeddings - Word2Vec
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Train Word2Vec embeddings and use pre-trained embeddings. Understand Skip-gram vs CBOW architectures.

**Mathematical Foundation**:
- Skip-gram: predict context from word
- CBOW: predict word from context
- Negative sampling for efficiency

**Expected Deliverables**:
- Train Word2Vec with gensim
- Load pre-trained embeddings
- Word similarity and analogy

**Test Cases**:
1. Train on custom corpus
2. king - man + woman = queen
3. Find similar words

**Hints**: Use gensim. Pre-trained embeddings often better for small data.

**Skills**: Word2Vec, word embeddings

---

### B5: Document Embeddings
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Create document-level embeddings from word embeddings: averaging, TF-IDF weighted averaging, Doc2Vec.

**Expected Deliverables**:
- Average word embeddings
- TF-IDF weighted average
- Doc2Vec training

**Test Cases**:
1. Document similarity
2. Compare aggregation methods
3. Document clustering

**Hints**: Weighted average often beats simple average. SIF removal helps.

**Skills**: Document embeddings

---

### B6: Sentiment Analysis
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Build sentiment analysis models: lexicon-based (VADER, TextBlob) and machine learning approaches.

**Expected Deliverables**:
- VADER sentiment scores
- ML-based classifier
- Fine-grained sentiment

**Test Cases**:
1. Classify positive/negative
2. Handle negation
3. Domain-specific sentiment

**Hints**: VADER works well for social media. Fine-tune for domain.

**Skills**: Sentiment analysis

---

### B7: Text Classification
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Build text classification pipeline for multi-class categorization: spam detection, topic classification, intent classification.

**Dataset**: 20 Newsgroups, AGNews, or custom

**Expected Deliverables**:
- Complete classification pipeline
- Multiple algorithm comparison
- Confusion matrix analysis

**Test Cases**:
1. Multi-class accuracy
2. Per-class performance
3. Error analysis

**Hints**: TF-IDF + SVM or LogisticRegression strong baselines.

**Skills**: Text classification

---

### B8: Named Entity Recognition
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply NER to extract entities: persons, organizations, locations, dates. Use spaCy and understand BIO tagging.

**Expected Deliverables**:
- spaCy NER usage
- Entity extraction
- Custom entity patterns

**Test Cases**:
1. Extract standard entities
2. Visualize entities
3. Add custom entity rules

**Hints**: Use spaCy. EntityRuler for custom patterns.

**Skills**: Named Entity Recognition

---

### B9: Topic Modeling - LDA
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Apply Latent Dirichlet Allocation for unsupervised topic discovery. Interpret topics and tune number of topics.

**Mathematical Foundation**:
- Documents = mixture of topics
- Topics = distribution over words
- Dirichlet prior for smoothness

**Expected Deliverables**:
- LDA with gensim or sklearn
- Topic interpretation
- Coherence score for tuning

**Test Cases**:
1. Discover topics in corpus
2. Interpret top words per topic
3. Assign documents to topics

**Hints**: Use coherence score to select number of topics.

**Skills**: Topic modeling, LDA

---

### B10: Text Similarity and Search
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Compute text similarity using various methods: cosine similarity, Jaccard, BM25, semantic similarity with embeddings.

**Expected Deliverables**:
- Cosine similarity implementation
- BM25 ranking
- Semantic similarity with embeddings

**Test Cases**:
1. Document similarity matrix
2. Search/retrieval task
3. Compare similarity methods

**Hints**: Cosine on TF-IDF for lexical. Embeddings for semantic.

**Skills**: Text similarity, information retrieval

---

### B11: Text Summarization
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Apply extractive and abstractive summarization. Use sentence ranking (TextRank) and pre-trained models.

**Expected Deliverables**:
- Extractive summarization (TextRank)
- Abstractive with transformers
- Summary evaluation

**Test Cases**:
1. Summarize news articles
2. Compare extractive vs abstractive
3. ROUGE score evaluation

**Hints**: sumy for extractive. HuggingFace for abstractive.

**Skills**: Text summarization

---

### B12: Language Models Introduction
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Understand language models: n-gram models, neural language models, perplexity evaluation. Foundation for advanced NLP.

**Mathematical Foundation**:
- P(w1, w2, ..., wn) = Π P(wi | w1...wi-1)
- Perplexity: exp(-1/n × Σ log P(wi))

**Expected Deliverables**:
- N-gram language model
- Perplexity calculation
- Text generation

**Test Cases**:
1. Train on corpus
2. Calculate perplexity
3. Generate text

**Hints**: N-gram models are simple but limited. Neural LMs are better.

**Skills**: Language models, perplexity

---

### B13: BERT and Transformers for NLP
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 75 min
**Implementation**: Libraries

**Problem**: Use pre-trained BERT for text classification, NER, and embeddings. Understand fine-tuning vs feature extraction.

**Expected Deliverables**:
- HuggingFace transformers usage
- BERT embeddings extraction
- Fine-tuning for classification

**Test Cases**:
1. Load pre-trained BERT
2. Extract contextualized embeddings
3. Fine-tune on downstream task

**Hints**: Use HuggingFace transformers library. GPU recommended.

**Skills**: BERT, transformers, fine-tuning

---

### B14: Text Augmentation
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply text augmentation techniques: synonym replacement, random insertion/deletion, back-translation, contextual augmentation.

**Expected Deliverables**:
- Multiple augmentation methods
- Augmentation library usage
- Effect on model performance

**Test Cases**:
1. Generate augmented texts
2. Train with augmented data
3. Improvement measurement

**Hints**: nlpaug library for easy augmentation. Don't over-augment.

**Skills**: Text augmentation

---

### B15: Handling Imbalanced Text Data
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Handle class imbalance in text classification: oversampling, undersampling, class weights, focal loss.

**Expected Deliverables**:
- Class weight adjustment
- Text-specific oversampling
- Focal loss for text

**Test Cases**:
1. Improve minority class recall
2. Compare sampling strategies
3. Class-weighted training

**Hints**: SMOTE doesn't work well for text. Use augmentation or class weights.

**Skills**: Imbalanced text classification

---

### B16: Multi-Label Text Classification
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Handle documents with multiple labels: binary relevance, classifier chains, label embedding approaches.

**Expected Deliverables**:
- Binary relevance approach
- Classifier chains
- Multi-label evaluation metrics

**Test Cases**:
1. One vs Rest classification
2. Classifier chains
3. Hamming loss, F1-micro/macro

**Hints**: Use MultiOutputClassifier or ClassifierChain from sklearn.

**Skills**: Multi-label classification

---

### B17: Text Generation
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Generate text using pre-trained models: GPT-2, controlling generation with temperature, top-k, top-p sampling.

**Expected Deliverables**:
- GPT-2 text generation
- Sampling parameter effects
- Controlled generation

**Test Cases**:
1. Generate coherent text
2. Effect of temperature
3. Top-k vs top-p comparison

**Hints**: Use HuggingFace. Temperature controls randomness.

**Skills**: Text generation, sampling

---

### B18: Question Answering
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Build extractive question answering system using BERT-based models. Find answer spans within context.

**Expected Deliverables**:
- QA model usage
- Answer extraction
- Confidence scores

**Test Cases**:
1. Answer questions from context
2. Handle unanswerable questions
3. Evaluate on QA dataset

**Hints**: Use DistilBERT for faster inference. SQuAD for evaluation.

**Skills**: Question answering

---

### B19: Text Clustering
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Cluster documents for topic discovery: TF-IDF + K-Means, embedding-based clustering, hierarchical clustering for dendrograms.

**Expected Deliverables**:
- TF-IDF + K-Means
- Embedding-based clustering
- Cluster interpretation

**Test Cases**:
1. Cluster news articles
2. Visualize clusters (t-SNE)
3. Interpret cluster topics

**Hints**: Reduce dimensions before clustering for better results.

**Skills**: Text clustering

---

### B20: Sequence Labeling
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Build sequence labeling models for NER and POS tagging: CRF, BiLSTM-CRF, transformer-based approaches.

**Expected Deliverables**:
- CRF implementation
- BiLSTM-CRF architecture
- Performance comparison

**Test Cases**:
1. POS tagging
2. Custom NER
3. Sequence-level evaluation

**Hints**: CRF captures label dependencies. sklearn-crfsuite for simple CRF.

**Skills**: Sequence labeling, CRF

---

### B21: Text Data Cleaning
**Domain**: NLP | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Clean real-world text: handle HTML, Unicode, emojis, contractions, common misspellings, and noise.

**Expected Deliverables**:
- HTML/URL removal
- Unicode normalization
- Contraction expansion

**Test Cases**:
1. Clean web-scraped text
2. Handle social media text
3. Preserve meaning while cleaning

**Hints**: ftfy for Unicode. contractions library for expansion.

**Skills**: Text cleaning

---

### B22: Keyword Extraction
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Extract keywords from documents: TF-IDF top terms, TextRank, YAKE, KeyBERT with embeddings.

**Expected Deliverables**:
- Multiple extraction methods
- Keyword ranking
- Phrase extraction

**Test Cases**:
1. Extract from single document
2. Corpus-level keywords
3. Keyphrase vs keyword

**Hints**: KeyBERT uses embeddings, works well. YAKE is unsupervised.

**Skills**: Keyword extraction

---

### B23: Information Extraction
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Extract structured information: relation extraction, event extraction, slot filling from unstructured text.

**Expected Deliverables**:
- Relation extraction
- Simple event extraction
- Template filling

**Test Cases**:
1. Extract person-organization relations
2. Extract date-event pairs
3. Fill structured templates

**Hints**: Use spaCy dependency parsing. Rule-based then ML-based.

**Skills**: Information extraction

---

### B24: Semantic Search
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Build semantic search using dense embeddings: sentence transformers, FAISS for efficient similarity search.

**Expected Deliverables**:
- Sentence-BERT embeddings
- FAISS indexing
- Semantic search demo

**Test Cases**:
1. Index documents
2. Search by meaning not keywords
3. Scale to large corpus

**Hints**: Use sentence-transformers. FAISS for efficient similarity.

**Skills**: Semantic search, vector databases

---

### B25: NLP for Low-Resource Languages
**Domain**: NLP | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Handle languages with limited resources: multilingual models (mBERT, XLM-RoBERTa), cross-lingual transfer.

**Expected Deliverables**:
- Multilingual model usage
- Cross-lingual transfer
- Zero-shot cross-lingual

**Test Cases**:
1. Apply model to new language
2. Cross-lingual classification
3. Performance comparison

**Hints**: mBERT trained on 104 languages. XLM-RoBERTa is stronger.

**Skills**: Multilingual NLP

---

### B26: NLP Pipelines and Deployment
**Domain**: MLOps | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Build production NLP pipeline: preprocessing, model inference, caching, batching for efficiency.

**Expected Deliverables**:
- Efficient NLP pipeline
- Batch processing
- Model serving considerations

**Test Cases**:
1. Process batch of texts
2. Cache embeddings
3. Latency optimization

**Hints**: spaCy pipelines are efficient. Batch embedding computation.

**Skills**: NLP deployment

---

### B27: NLP Real-World Project
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete NLP project: preprocessing, feature engineering, modeling, evaluation on real text dataset.

**Dataset**: Product reviews, news, or social media

**Expected Deliverables**:
- Complete NLP pipeline
- Multiple model comparison
- Error analysis
- Business insights

**Hints**: Start with baselines. Error analysis guides improvements.

**Skills**: End-to-end NLP project

---

### B28: NLP Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Comprehensive NLP project combining multiple tasks: classification, NER, summarization into unified system.

**Expected Deliverables**:
- Multi-task NLP system
- Pipeline integration
- Evaluation across tasks
- Documentation

**Evaluation Criteria**: Completeness, quality, integration

**Hints**: Build modular components that work together.

**Skills**: Complete NLP mastery

---

## Section C: Time Series Analysis (C1-C25)

### C1: Time Series Data Structures
**Domain**: Time Series | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Work with time series in Pandas: datetime indexing, resampling, time zones, period vs timestamp.

**Expected Deliverables**:
- DateTime index operations
- Resampling (upsampling, downsampling)
- Time zone handling

**Test Cases**:
1. Daily to weekly aggregation
2. Forward/backward fill
3. Time zone conversion

**Hints**: pd.to_datetime, resample, tz_localize, tz_convert.

**Skills**: Time series data manipulation

---

### C2: Time Series Visualization
**Domain**: Time Series | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Create effective time series visualizations: line plots, seasonal plots, lag plots, ACF/PACF plots.

**Expected Deliverables**:
- Time series plots
- Seasonal subseries plots
- ACF/PACF visualization

**Test Cases**:
1. Plot with multiple series
2. Highlight trends/seasonality
3. Interactive plots

**Hints**: Plotly for interactive. matplotlib for static. statsmodels for ACF/PACF.

**Skills**: Time series visualization

---

### C3: Decomposition
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Decompose time series into trend, seasonality, and residual components. Compare additive vs multiplicative decomposition.

**Mathematical Foundation**:
- Additive: Y = T + S + R
- Multiplicative: Y = T × S × R

**Expected Deliverables**:
- seasonal_decompose usage
- STL decomposition
- Component analysis

**Test Cases**:
1. Decompose with known seasonality
2. Compare decomposition types
3. Analyze residuals

**Hints**: STL is more robust. Use period parameter correctly.

**Skills**: Time series decomposition

---

### C4: Stationarity Testing
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Test for stationarity using ADF, KPSS, and PP tests. Understand differencing to achieve stationarity.

**Mathematical Foundation**:
- ADF: test for unit root
- KPSS: test for trend stationarity
- Difference until stationary

**Expected Deliverables**:
- ADF and KPSS tests
- Auto-differencing
- Visual stationarity check

**Test Cases**:
1. Detect non-stationary series
2. Apply differencing
3. Verify stationarity after

**Hints**: Use statsmodels adfuller, kpss. Conflicting results = further investigation.

**Skills**: Stationarity testing, differencing

---

### C5: Moving Averages and Smoothing
**Domain**: Time Series | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Apply smoothing techniques: simple moving average, exponential smoothing, Holt-Winters for trend and seasonality.

**Expected Deliverables**:
- SMA and EMA
- Simple exponential smoothing
- Holt-Winters

**Test Cases**:
1. Smooth noisy series
2. Compare smoothing parameters
3. Trend extraction

**Hints**: Use statsmodels ExponentialSmoothing. pandas ewm for EMA.

**Skills**: Time series smoothing

---

### C6: ARIMA Modeling
**Domain**: Time Series | **Difficulty**: ★★★★☆ | **Time**: 70 min
**Implementation**: Libraries

**Problem**: Build ARIMA models: understand AR, I, MA components; select order using ACF/PACF; validate with diagnostics.

**Mathematical Foundation**:
- AR(p): X_t = c + Σ φᵢX_{t-i} + ε_t
- MA(q): X_t = μ + Σ θᵢε_{t-i} + ε_t
- I(d): differencing order

**Expected Deliverables**:
- ARIMA model fitting
- Order selection (p, d, q)
- Residual diagnostics

**Test Cases**:
1. Fit ARIMA to data
2. Use ACF/PACF for order
3. Check residual independence

**Hints**: Use auto_arima from pmdarima. Check AIC for model selection.

**Skills**: ARIMA, Box-Jenkins methodology

---

### C7: Seasonal ARIMA (SARIMA)
**Domain**: Time Series | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Extend ARIMA for seasonality with SARIMA: seasonal differencing and seasonal AR/MA terms.

**Mathematical Foundation**:
- SARIMA(p,d,q)(P,D,Q)m
- Seasonal period m

**Expected Deliverables**:
- SARIMA model fitting
- Seasonal order selection
- Forecast with confidence intervals

**Test Cases**:
1. Model monthly seasonality
2. Weekly pattern forecasting
3. Out-of-sample evaluation

**Hints**: pm.auto_arima with seasonal=True. m=12 for monthly, m=7 for daily.

**Skills**: SARIMA, seasonal forecasting

---

### C8: Prophet for Forecasting
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Use Facebook Prophet for automatic forecasting with trend, seasonality, and holiday effects.

**Expected Deliverables**:
- Prophet model fitting
- Adding holidays
- Uncertainty intervals

**Test Cases**:
1. Forecast with Prophet
2. Add custom seasonality
3. Include holidays

**Hints**: Install with pip install prophet. Great for daily/monthly data with holidays.

**Skills**: Prophet, practical forecasting

---

### C9: Feature Engineering for Time Series
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Create features from time series for ML models: lags, rolling statistics, date features, Fourier terms.

**Expected Deliverables**:
- Lag features
- Rolling window features
- Cyclical encoding for time

**Test Cases**:
1. Create lag 1,7,30 features
2. Rolling mean, std, min, max
3. Sine/cosine for hour

**Hints**: tsfresh for automated feature extraction. Be careful of leakage.

**Skills**: Time series features

---

### C10: ML for Time Series Forecasting
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Apply ML models (XGBoost, LightGBM) to time series with proper feature engineering and cross-validation.

**Expected Deliverables**:
- Feature engineering for ML
- Time-respecting CV
- Comparison with ARIMA

**Test Cases**:
1. Gradient boosting forecast
2. Time series cross-validation
3. Compare with statistical methods

**Hints**: TimeSeriesSplit for CV. Feature engineering is key for ML.

**Skills**: ML for time series

---

### C11: LSTM for Time Series
**Domain**: Deep Learning/Time Series | **Difficulty**: ★★★★☆ | **Time**: 75 min
**Implementation**: Libraries

**Problem**: Build LSTM networks for sequence prediction: univariate and multivariate time series.

**Expected Deliverables**:
- LSTM architecture
- Sequence preparation
- Multi-step forecasting

**Test Cases**:
1. Univariate LSTM
2. Multi-step ahead prediction
3. Compare with ARIMA

**Hints**: Sequence length matters. Normalize inputs. Use early stopping.

**Skills**: LSTM, RNN for time series

---

### C12: Multivariate Time Series
**Domain**: Time Series | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Forecast using multiple related time series: VAR, VARMAX, and multivariate deep learning approaches.

**Expected Deliverables**:
- VAR model
- Feature series for prediction
- Cross-correlation analysis

**Test Cases**:
1. Fit VAR to multiple series
2. Forecast with exogenous variables
3. Granger causality test

**Hints**: VAR for stationary series. VARMAX for exogenous variables.

**Skills**: Multivariate forecasting

---

### C13: Anomaly Detection in Time Series
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Detect anomalies in time series: statistical methods (z-score, IQR), isolation forest on rolling features, autoencoders.

**Expected Deliverables**:
- Statistical anomaly detection
- ML-based detection
- Visualization of anomalies

**Test Cases**:
1. Detect obvious anomalies
2. Handle seasonal anomalies
3. Point vs pattern anomalies

**Hints**: STL decomposition helps identify anomalies in residuals.

**Skills**: Time series anomaly detection

---

### C14: Change Point Detection
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Detect structural changes in time series: PELT algorithm, Bayesian change point detection.

**Expected Deliverables**:
- Change point algorithms
- Multiple change points
- Confidence in detection

**Test Cases**:
1. Detect mean shift
2. Detect variance change
3. Multiple change points

**Hints**: Use ruptures library. PELT is fast. Prophet also detects changepoints.

**Skills**: Change point detection

---

### C15: Forecasting Evaluation Metrics
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Evaluate forecasts: MAE, RMSE, MAPE, SMAPE, MASE. Understand scale-dependent vs independent metrics.

**Mathematical Foundation**:
- MASE = mean(|error|) / mean(|naive forecast error|)
- SMAPE = mean(2|y-ŷ| / (|y|+|ŷ|))

**Expected Deliverables**:
- All major metrics
- Metric selection guidelines
- Baseline comparison (naive)

**Test Cases**:
1. Compare different metrics
2. When MAPE fails
3. MASE interpretation

**Hints**: MASE is scale-independent and symmetric. Use for cross-series comparison.

**Skills**: Forecast evaluation

---

### C16: Backtesting Forecasts
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Properly backtest forecasting models: walk-forward validation, expanding window, sliding window.

**Expected Deliverables**:
- Walk-forward implementation
- Expanding vs sliding window
- Average performance across windows

**Test Cases**:
1. Walk-forward validation
2. Compare window strategies
3. Statistical significance

**Hints**: TimeSeriesSplit does expanding window. Custom for sliding.

**Skills**: Time series cross-validation

---

### C17: Dealing with Missing Data in Time Series
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Handle missing values: forward/backward fill, interpolation, seasonal pattern imputation, model-based imputation.

**Expected Deliverables**:
- Simple imputation methods
- Seasonal imputation
- Comparison of methods

**Test Cases**:
1. Forward fill for recent data
2. Interpolation for gaps
3. Preserve seasonality

**Hints**: Use interpolate(method='time'). fillna(method='ffill').

**Skills**: Time series imputation

---

### C18: Hierarchical Time Series
**Domain**: Time Series | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Forecast hierarchical time series with reconciliation: bottom-up, top-down, optimal reconciliation.

**Expected Deliverables**:
- Hierarchical aggregation
- Reconciliation methods
- Coherent forecasts

**Test Cases**:
1. Product-category-total hierarchy
2. Bottom-up vs top-down
3. Forecast reconciliation

**Hints**: scikit-hts or hts library. MinT for optimal reconciliation.

**Skills**: Hierarchical forecasting

---

### C19: Intermittent Demand Forecasting
**Domain**: Time Series | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Forecast series with many zeros (intermittent demand): Croston's method, SBA, TSB.

**Expected Deliverables**:
- Croston's method
- Comparison with standard methods
- Evaluation metrics for intermittent

**Test Cases**:
1. Forecast sparse series
2. Compare with ARIMA
3. Use appropriate metrics

**Hints**: statsforecast has Croston. Traditional metrics (MAPE) fail.

**Skills**: Intermittent demand forecasting

---

### C20: Time Series Clustering
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Cluster similar time series using DTW distance and shape-based methods.

**Expected Deliverables**:
- DTW distance calculation
- K-Means with DTW
- Shape-based clustering

**Test Cases**:
1. Cluster similar patterns
2. Compare with Euclidean
3. Visualize clustered series

**Hints**: Use tslearn library. DTW handles time warping.

**Skills**: Time series clustering

---

### C21: Uncertainty in Forecasts
**Domain**: Time Series | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Quantify forecast uncertainty: prediction intervals, probabilistic forecasting, conformal prediction.

**Expected Deliverables**:
- Prediction intervals
- Quantile forecasting
- Interval evaluation (coverage)

**Test Cases**:
1. 95% prediction intervals
2. Quantile regression forecasts
3. Evaluate coverage

**Hints**: Prophet gives intervals. Use pinball loss for quantile evaluation.

**Skills**: Probabilistic forecasting

---

### C22: Exogenous Variables in Forecasting
**Domain**: Time Series | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Include external variables in forecasts: ARIMAX, Prophet with regressors, ML with features.

**Expected Deliverables**:
- ARIMAX modeling
- Prophet with regressors
- Future exogenous handling

**Test Cases**:
1. Add weather as exogenous
2. Use promotions for sales
3. Handle missing future values

**Hints**: Future exogenous must be known (or forecasted). Holidays are common.

**Skills**: Exogenous variable modeling

---

### C23: Real-Time Forecasting Systems
**Domain**: MLOps | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Conceptual + Libraries

**Problem**: Design real-time forecasting pipeline: streaming data, online learning, model updating.

**Expected Deliverables**:
- Streaming architecture
- Online model updates
- Forecast serving

**Test Cases**:
1. Process streaming data
2. Update model incrementally
3. Low-latency predictions

**Hints**: River for online learning. Kafka for streaming. Consider batch updates.

**Skills**: Real-time forecasting

---

### C24: Time Series Project
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete time series project: EDA, feature engineering, multiple models, proper evaluation.

**Dataset**: Sales, weather, or financial data

**Expected Deliverables**:
- Complete analysis and modeling
- Multiple model comparison
- Proper backtesting
- Business recommendations

**Hints**: Start with simple baselines. Always use time-respecting CV.

**Skills**: End-to-end time series project

---

### C25: Time Series Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Comprehensive time series project combining forecasting, anomaly detection, and pattern discovery.

**Expected Deliverables**:
- Multi-task time series analysis
- Production-ready models
- Visualization dashboard
- Documentation

**Evaluation Criteria**: Methodology, accuracy, production readiness

**Hints**: Combine statistical and ML methods for robust solution.

**Skills**: Complete time series mastery

---

## Section D: Deep Learning Fundamentals (D1-D30)

### D1: Perceptron from Scratch
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Implement the perceptron algorithm from scratch: understand weights, bias, activation, and perceptron learning rule.

**Mathematical Foundation**:
- Output: f(x) = sign(w·x + b)
- Update: w = w + η(y - ŷ)x

**Expected Deliverables**:
- Perceptron class with fit/predict
- Convergence visualization
- Limitations on XOR problem

**Test Cases**:
1. Linearly separable data
2. Show XOR failure
3. Decision boundary visualization

**Hints**: Perceptron only works for linearly separable data.

**Skills**: Perceptron, neural network foundations

---

### D2: Multi-Layer Perceptron from Scratch
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: From Scratch

**Problem**: Implement a multi-layer perceptron with backpropagation: forward pass, compute loss, backward pass, update weights.

**Mathematical Foundation**:
- Forward: a^l = σ(W^l × a^(l-1) + b^l)
- Backward: δ^l = ((W^(l+1))^T δ^(l+1)) ⊙ σ'(z^l)

**Expected Deliverables**:
- MLP from scratch
- Backpropagation implementation
- XOR problem solution

**Test Cases**:
1. Solve XOR problem
2. Classify non-linear data
3. Compare with sklearn MLPClassifier

**Hints**: Numerical gradient checking validates backprop implementation.

**Skills**: Backpropagation, MLP internals

---

### D3: Activation Functions
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Implement and compare activation functions: sigmoid, tanh, ReLU, Leaky ReLU, ELU, GELU, Swish. Understand vanishing gradients.

**Mathematical Foundation**:
- ReLU: max(0, x)
- Sigmoid: 1 / (1 + e^(-x))
- tanh: (e^x - e^(-x)) / (e^x + e^(-x))

**Expected Deliverables**:
- All activation functions
- Gradient visualization
- Effect on training

**Test Cases**:
1. Vanishing gradient with sigmoid
2. Dead neurons with ReLU
3. Compare training speed

**Hints**: ReLU is usually first choice. GELU for transformers.

**Skills**: Activation functions, gradient flow

---

### D4: Loss Functions for Neural Networks
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Both

**Problem**: Implement and understand loss functions: MSE, MAE, cross-entropy, binary cross-entropy, focal loss.

**Mathematical Foundation**:
- Cross-entropy: -Σ y log(ŷ)
- Focal: -(1-p)^γ log(p)

**Expected Deliverables**:
- Loss function implementations
- Gradient computation
- When to use each

**Test Cases**:
1. MSE for regression
2. Cross-entropy for classification
3. Focal loss for imbalanced

**Hints**: Use softmax + cross-entropy for stable gradients.

**Skills**: Loss functions, optimization objectives

---

### D5: Gradient Descent Variants
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Both

**Problem**: Implement optimization algorithms: SGD, momentum, RMSprop, Adam, AdaGrad. Understand adaptive learning rates.

**Mathematical Foundation**:
- Momentum: v = βv - η∇L; θ = θ + v
- Adam: combines momentum and RMSprop

**Expected Deliverables**:
- All optimizers from scratch
- Convergence visualization
- Comparison on test functions

**Test Cases**:
1. Compare convergence speed
2. Saddle point behavior
3. Optimal learning rate

**Hints**: Adam is good default. SGD with momentum can generalize better.

**Skills**: Optimizers, adaptive learning rates

---

### D6: Weight Initialization
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Understand weight initialization strategies: Xavier/Glorot, He/Kaiming. Proper initialization enables training.

**Mathematical Foundation**:
- Xavier: Var(W) = 2 / (n_in + n_out)
- He: Var(W) = 2 / n_in

**Expected Deliverables**:
- Initialization implementations
- Effect on activation statistics
- Training impact

**Test Cases**:
1. Compare initialization schemes
2. Monitor layer activations
3. Training with different init

**Hints**: He for ReLU, Xavier for tanh/sigmoid.

**Skills**: Weight initialization, training stability

---

### D7: Regularization in Deep Learning
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply regularization techniques: L2 weight decay, dropout, batch normalization, early stopping, data augmentation.

**Expected Deliverables**:
- Dropout implementation
- Batch normalization
- Regularization comparison

**Test Cases**:
1. Overfitting without regularization
2. Improvement with dropout
3. Batch norm training speedup

**Hints**: Dropout at training, not inference. Batch norm after linear, before activation.

**Skills**: Deep learning regularization

---

### D8: Batch Normalization Deep Dive
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Both

**Problem**: Implement batch normalization from scratch. Understand training vs inference behavior, learnable parameters.

**Mathematical Foundation**:
- Normalize: x̂ = (x - μ) / σ
- Scale and shift: y = γx̂ + β

**Expected Deliverables**:
- Batch norm implementation
- Running mean/variance tracking
- Training vs inference

**Test Cases**:
1. Implement batch norm layer
2. Track running statistics
3. Compare train/eval behavior

**Hints**: Track running mean/var for inference using exponential moving average.

**Skills**: Batch normalization internals

---

### D9: Introduction to PyTorch
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Learn PyTorch fundamentals: tensors, autograd, nn.Module, DataLoader, training loop.

**Expected Deliverables**:
- Tensor operations
- Custom nn.Module
- Complete training loop

**Test Cases**:
1. Create simple network
2. Train on MNIST
3. Evaluate and save model

**Hints**: Use GPU if available. DataLoader for batching.

**Skills**: PyTorch basics

---

### D10: Introduction to TensorFlow/Keras
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Learn TensorFlow/Keras: Sequential API, Functional API, custom training loops.

**Expected Deliverables**:
- Sequential model
- Functional API model
- Custom training step

**Test Cases**:
1. Build and train model
2. Use Functional API
3. Custom training loop

**Hints**: Start with Keras high-level API. GradientTape for custom training.

**Skills**: TensorFlow/Keras basics

---

### D11: CNNs from Scratch
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 75 min
**Implementation**: From Scratch

**Problem**: Implement convolutional layer from scratch: understand filters, stride, padding, and the convolution operation.

**Mathematical Foundation**:
- Output: (input - filter + 2×padding) / stride + 1
- Convolution: sliding dot product

**Expected Deliverables**:
- Conv2D implementation
- MaxPool implementation
- Simple CNN

**Test Cases**:
1. Apply convolution to image
2. Verify output dimensions
3. Train simple CNN

**Hints**: Use nested loops for clarity, optimize later. im2col for efficiency.

**Skills**: CNN internals

---

### D12: CNN Architectures
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Study classic CNN architectures: LeNet, AlexNet, VGG, ResNet, Inception. Understand design principles.

**Expected Deliverables**:
- LeNet implementation
- ResNet block implementation
- Architecture comparison

**Test Cases**:
1. Implement LeNet
2. Build ResNet block
3. Compare on CIFAR-10

**Hints**: Skip connections are key to deep networks. Use pre-trained for transfer learning.

**Skills**: CNN architectures

---

### D13: Transfer Learning
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply transfer learning: use pre-trained ImageNet models, fine-tune for new tasks, feature extraction.

**Expected Deliverables**:
- Load pre-trained model
- Feature extraction approach
- Fine-tuning approach

**Test Cases**:
1. Feature extraction
2. Fine-tune last layers
3. Full fine-tune

**Hints**: Freeze early layers. Use lower learning rate for fine-tuning.

**Skills**: Transfer learning

---

### D14: RNN Fundamentals
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Both

**Problem**: Implement vanilla RNN from scratch. Understand hidden state, vanishing gradients, and sequence modeling.

**Mathematical Foundation**:
- h_t = tanh(W_xh × x_t + W_hh × h_{t-1} + b)
- y_t = W_hy × h_t + b_y

**Expected Deliverables**:
- RNN cell implementation
- Sequence processing
- Vanishing gradient demonstration

**Test Cases**:
1. Process sequence
2. Show gradient vanishing
3. Character-level generation

**Hints**: RNNs struggle with long dependencies. Use LSTM/GRU instead.

**Skills**: RNN internals

---

### D15: LSTM and GRU
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Both

**Problem**: Implement LSTM and GRU from scratch. Understand gates, cell state, and how they solve vanishing gradients.

**Mathematical Foundation**:
- LSTM: forget, input, output gates + cell state
- GRU: reset and update gates

**Expected Deliverables**:
- LSTM cell implementation
- GRU cell implementation
- Comparison with vanilla RNN

**Test Cases**:
1. Implement gates
2. Process long sequences
3. Compare with RNN on long-range dependencies

**Hints**: LSTM slightly better for very long dependencies. GRU faster.

**Skills**: LSTM, GRU internals

---

### D16: Sequence-to-Sequence Models
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 70 min
**Implementation**: Libraries

**Problem**: Build encoder-decoder models for translation, summarization. Understand encoding and decoding process.

**Expected Deliverables**:
- Encoder-decoder architecture
- Teacher forcing training
- Beam search decoding

**Test Cases**:
1. Simple translation task
2. Teacher forcing vs autoregressive
3. Beam vs greedy decoding

**Hints**: Teacher forcing during training. Beam search for inference.

**Skills**: Seq2Seq, encoder-decoder

---

### D17: Attention Mechanism
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Both

**Problem**: Implement attention mechanism: understand query, key, value, and how attention improves seq2seq.

**Mathematical Foundation**:
- Attention(Q, K, V) = softmax(QK^T / √d_k)V
- Context = weighted sum of values

**Expected Deliverables**:
- Attention implementation
- Attention visualization
- Seq2Seq with attention

**Test Cases**:
1. Implement scaled dot-product
2. Visualize attention weights
3. Compare with non-attention

**Hints**: Attention allows direct connection to any input position.

**Skills**: Attention mechanism

---

### D18: Transformer Architecture
**Domain**: Deep Learning | **Difficulty**: ★★★★★ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Understand transformer architecture: multi-head attention, positional encoding, encoder-decoder structure.

**Expected Deliverables**:
- Multi-head attention
- Positional encoding
- Transformer block

**Test Cases**:
1. Implement transformer block
2. Train on sequence task
3. Attention patterns analysis

**Hints**: Use existing implementations (HuggingFace). Focus on understanding.

**Skills**: Transformers

---

### D19: Embeddings and Representation Learning
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Learn embedding layers, contrastive learning basics, and how to learn useful representations.

**Expected Deliverables**:
- Embedding layer usage
- Similarity in embedding space
- Visualization of embeddings

**Test Cases**:
1. Train word embeddings
2. Visualize with t-SNE
3. Similarity search

**Hints**: Embedding space should capture semantic similarity.

**Skills**: Representation learning

---

### D20: Generative Models Introduction
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Introduction to generative models: VAEs and GANs. Understand latent space and generation process.

**Expected Deliverables**:
- Simple VAE
- Simple GAN
- Generation samples

**Test Cases**:
1. Generate MNIST digits
2. Latent space interpolation
3. Mode collapse in GAN

**Hints**: VAEs have stable training. GANs can produce sharper images.

**Skills**: Generative models basics

---

### D21: Model Saving and Loading
**Domain**: Deep Learning | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Save and load models properly: weights, architecture, optimizer state, ONNX export.

**Expected Deliverables**:
- Save entire model
- Save/load weights only
- ONNX export

**Test Cases**:
1. Save and reload
2. Resume training
3. Cross-framework export

**Hints**: Save optimizer state for resuming. ONNX for deployment.

**Skills**: Model persistence

---

### D22: GPU Training
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Train models on GPU: data transfer, memory management, multi-GPU training.

**Expected Deliverables**:
- GPU training setup
- Memory optimization
- Multi-GPU basics

**Test Cases**:
1. Move to GPU
2. Monitor GPU memory
3. Speed comparison CPU vs GPU

**Hints**: Use .to(device). Be careful with memory. Clear cache if needed.

**Skills**: GPU training

---

### D23: Mixed Precision Training
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Use mixed precision (FP16) for faster training and reduced memory. Understand loss scaling.

**Expected Deliverables**:
- Mixed precision training
- Speed improvement
- Memory savings

**Test Cases**:
1. Enable mixed precision
2. Measure speedup
3. Verify accuracy maintained

**Hints**: Use AMP (automatic mixed precision). Loss scaling for stability.

**Skills**: Mixed precision training

---

### D24: Learning Rate Scheduling
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply learning rate schedules: step decay, cosine annealing, warmup, one-cycle policy.

**Expected Deliverables**:
- Multiple schedulers
- Warmup implementation
- Performance comparison

**Test Cases**:
1. Step decay schedule
2. Cosine annealing
3. One-cycle training

**Hints**: Warmup helps stability. Cosine annealing often works well.

**Skills**: Learning rate scheduling

---

### D25: Debugging Deep Learning Models
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Debug common deep learning issues: vanishing/exploding gradients, NaN losses, overfitting, underfitting.

**Expected Deliverables**:
- Gradient monitoring
- NaN debugging
- Common issue solutions

**Test Cases**:
1. Detect vanishing gradients
2. Fix exploding gradients
3. Diagnose training issues

**Hints**: Monitor gradient norms. Small learning rate for exploding. Check data for NaN.

**Skills**: DL debugging

---

### D26: Hyperparameter Tuning for DL
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Tune deep learning hyperparameters: learning rate, batch size, architecture, regularization. Use Optuna.

**Expected Deliverables**:
- Learning rate search
- Architecture search
- Optuna integration

**Test Cases**:
1. Find optimal learning rate
2. Compare batch sizes
3. Automated search with Optuna

**Hints**: Learning rate is most important. Use LR finder.

**Skills**: DL hyperparameter tuning

---

### D27: Data Augmentation for Images
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply image augmentation: flips, rotations, color jitter, cutout, mixup, CutMix.

**Expected Deliverables**:
- Standard augmentations
- Advanced (mixup, CutMix)
- Augmentation library usage

**Test Cases**:
1. Basic augmentations
2. MixUp implementation
3. Effect on validation accuracy

**Hints**: Use albumentations or torchvision transforms. Strong augmentation for small data.

**Skills**: Image augmentation

---

### D28: Custom Dataset and DataLoader
**Domain**: Deep Learning | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Create custom datasets for your data: image folders, CSV data, lazy loading, augmentation integration.

**Expected Deliverables**:
- Custom Dataset class
- DataLoader configuration
- Multi-worker loading

**Test Cases**:
1. Custom image dataset
2. Custom tabular dataset
3. Batching and shuffling

**Hints**: Implement __len__ and __getitem__. Use num_workers for speed.

**Skills**: Custom data loading

---

### D29: Deep Learning Project
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete deep learning project: data preparation, model architecture, training, evaluation, deployment preparation.

**Dataset**: Image classification or NLP task

**Expected Deliverables**:
- Complete training pipeline
- Model selection
- Evaluation and analysis
- Deployment-ready model

**Hints**: Start with established architecture. Focus on good training practices.

**Skills**: End-to-end DL project

---

### D30: Deep Learning Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★★ | **Time**: 150 min
**Implementation**: Both

**Problem**: Comprehensive deep learning project: implement key components from scratch, train production-quality model, document thoroughly.

**Expected Deliverables**:
- From-scratch core components
- Optimized training
- Model analysis
- Production pipeline
- Complete documentation

**Evaluation Criteria**: Technical depth, methodology, production readiness

**Hints**: Demonstrate understanding from fundamentals to production.

**Skills**: Complete deep learning mastery

---

## Section E: Model Interpretability & Explainability (E1-E22)

### E1: Feature Importance Methods Overview
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Compare feature importance methods: tree-based, permutation, SHAP, LIME. Understand when each is appropriate.

**Expected Deliverables**:
- Multiple importance methods
- Comparison of rankings
- Method selection guidelines

**Test Cases**:
1. Compare rankings across methods
2. Correlated features handling
3. When methods disagree

**Hints**: Permutation importance is model-agnostic. SHAP provides theory.

**Skills**: Feature importance overview

---

### E2: Permutation Importance
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Implement and apply permutation importance: measure performance drop when feature values are shuffled.

**Mathematical Foundation**:
- Shuffle feature j
- Measure accuracy decrease
- Larger decrease = more important

**Expected Deliverables**:
- Permutation importance from scratch
- sklearn implementation
- Handling correlated features

**Test Cases**:
1. Implement from scratch
2. Compare with tree importance
3. Handle multicollinearity

**Hints**: Use test set for importance. Multiple repetitions for stability.

**Skills**: Permutation importance

---

### E3: SHAP Values Introduction
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Understand SHAP values from game theory: Shapley values fairly attribute prediction to features.

**Mathematical Foundation**:
- Shapley value: fair contribution of each player
- SHAP: efficient approximations for ML

**Expected Deliverables**:
- SHAP library usage
- Summary plots
- Force plots

**Test Cases**:
1. Compute SHAP values
2. Interpret for individual predictions
3. Global feature importance

**Hints**: TreeSHAP is fast for trees. KernelSHAP for any model.

**Skills**: SHAP values

---

### E4: SHAP Deep Dive
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Master SHAP: TreeSHAP, KernelSHAP, DeepSHAP, interaction values, dependence plots.

**Expected Deliverables**:
- Different SHAP explainers
- Interaction analysis
- Dependence plots

**Test Cases**:
1. TreeSHAP for XGBoost
2. KernelSHAP for any model
3. SHAP interactions

**Hints**: TreeSHAP exact and fast for tree models. DeepSHAP for neural networks.

**Skills**: Advanced SHAP

---

### E5: LIME (Local Interpretable Model-agnostic Explanations)
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply LIME for local explanations: fit interpretable model in neighborhood of prediction.

**Mathematical Foundation**:
- Sample around instance
- Fit weighted linear model
- Interpret linear coefficients

**Expected Deliverables**:
- LIME for tabular data
- LIME for text
- LIME for images

**Test Cases**:
1. Explain tabular prediction
2. Explain text classification
3. Explain image classification

**Hints**: Explanations are local, may vary for similar inputs.

**Skills**: LIME explanations

---

### E6: Partial Dependence Plots
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Create partial dependence plots showing marginal effect of features on predictions. Understand 1D and 2D PDPs.

**Mathematical Foundation**:
- PDP: average prediction over all other features
- Shows relationship between feature and prediction

**Expected Deliverables**:
- 1D PDPs
- 2D PDPs (interaction)
- Interpretation guidelines

**Test Cases**:
1. Create 1D PDP
2. Create 2D PDP
3. Compare with feature importance

**Hints**: PDPs assume feature independence. Use ICE for heterogeneity.

**Skills**: Partial dependence

---

### E7: Individual Conditional Expectation (ICE)
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Create ICE plots showing individual prediction changes, revealing heterogeneity hidden in PDPs.

**Expected Deliverables**:
- ICE plot creation
- Comparison with PDP
- Heterogeneity detection

**Test Cases**:
1. ICE for each instance
2. Detect interaction effects
3. Centered ICE (c-ICE)

**Hints**: ICE reveals when PDP is misleading due to interactions.

**Skills**: ICE plots

---

### E8: Accumulated Local Effects (ALE)
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply ALE plots that handle correlated features better than PDPs. Understand the difference in interpretation.

**Expected Deliverables**:
- ALE plot creation
- Comparison with PDP
- When ALE is preferred

**Test Cases**:
1. Create ALE plots
2. Compare with PDP on correlated data
3. Interpret ALE values

**Hints**: ALE preferred for correlated features. PDP can extrapolate unrealistically.

**Skills**: ALE plots

---

### E9: Interpreting Linear Models
**Domain**: Interpretability | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Interpret coefficients of linear and logistic regression: standardization for comparison, confidence intervals.

**Expected Deliverables**:
- Coefficient interpretation
- Standardized coefficients
- Confidence intervals

**Test Cases**:
1. Interpret regression coefficients
2. Odds ratios for logistic
3. Feature importance from coefficients

**Hints**: Standardize features for comparable coefficients. Confidence intervals from standard errors.

**Skills**: Linear model interpretation

---

### E10: Interpreting Tree-Based Models
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Interpret decision trees and forests: feature importance, decision paths, rule extraction.

**Expected Deliverables**:
- Tree visualization
- Rule extraction
- Importance comparison

**Test Cases**:
1. Visualize single tree
2. Extract decision rules
3. Path analysis for prediction

**Hints**: Single trees are interpretable; forests need aggregated importance.

**Skills**: Tree interpretation

---

### E11: Interpreting Neural Networks
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Apply interpretability methods for neural networks: saliency maps, integrated gradients, attention visualization.

**Expected Deliverables**:
- Saliency maps
- Integrated gradients
- Attention visualization

**Test Cases**:
1. Compute saliency
2. Integrated gradients for images
3. Attention weights for NLP

**Hints**: Use Captum for PyTorch. Integrated gradients satisfy axioms.

**Skills**: Neural network interpretability

---

### E12: Counterfactual Explanations
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Generate counterfactual explanations: "What would need to change for a different outcome?"

**Expected Deliverables**:
- Counterfactual generation
- Actionable recourse
- Diversity in counterfactuals

**Test Cases**:
1. Generate counterfactual
2. Ensure actionability
3. Multiple diverse counterfactuals

**Hints**: Use DiCE library. Constrain to actionable features.

**Skills**: Counterfactual explanations

---

### E13: Anchor Rules
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Generate anchor explanations: find sufficient conditions (rules) for a prediction.

**Expected Deliverables**:
- Anchor rule extraction
- Precision and coverage
- Comparison with LIME

**Test Cases**:
1. Extract anchor rules
2. Validate precision
3. Compare with other methods

**Hints**: Anchors are if-then rules with high precision.

**Skills**: Anchor explanations

---

### E14: Global Surrogates
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Train interpretable surrogate model on complex model's predictions to approximate behavior globally.

**Expected Deliverables**:
- Surrogate model training
- Fidelity measurement
- Interpretation of surrogate

**Test Cases**:
1. Train decision tree surrogate
2. Measure fidelity (R²/accuracy)
3. Interpret surrogate rules

**Hints**: Surrogate explains the model, not data. High fidelity required.

**Skills**: Global surrogates

---

### E15: Feature Effects Visualization
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Create comprehensive feature effect visualizations: combining multiple methods for complete picture.

**Expected Deliverables**:
- Multi-plot dashboard
- PDP + ICE combined
- SHAP summary plot

**Test Cases**:
1. Combined visualization
2. Interactive dashboard
3. Communication to stakeholders

**Hints**: Use combination of methods. Visualize for different audiences.

**Skills**: Effect visualization

---

### E16: Fairness and Bias Detection
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Detect bias in ML models: demographic parity, equalized odds, calibration across groups.

**Mathematical Foundation**:
- Demographic parity: P(Ŷ=1|A=0) = P(Ŷ=1|A=1)
- Equal opportunity: P(Ŷ=1|Y=1,A=0) = P(Ŷ=1|Y=1,A=1)

**Expected Deliverables**:
- Fairness metrics computation
- Bias detection
- Mitigation strategies overview

**Test Cases**:
1. Compute fairness metrics
2. Detect disparate impact
3. Compare mitigated model

**Hints**: Use Fairlearn or AIF360. Different fairness definitions conflict.

**Skills**: Fairness, bias detection

---

### E17: Model Cards and Documentation
**Domain**: Interpretability | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Documentation

**Problem**: Create model cards documenting model purpose, limitations, performance across groups, and intended use.

**Expected Deliverables**:
- Model card template
- Performance breakdown
- Limitations documentation

**Test Cases**:
1. Create complete model card
2. Document failure cases
3. Specify usage guidelines

**Hints**: Follow model card format. Be honest about limitations.

**Skills**: Model documentation

---

### E18: Interpretability for Regulatory Compliance
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Conceptual + Libraries

**Problem**: Understand right to explanation (GDPR), adverse action notices (FCRA), and how to comply.

**Expected Deliverables**:
- Regulatory requirements overview
- Compliant documentation
- Audit-ready reports

**Test Cases**:
1. GDPR explanation requirements
2. Adverse action reasons
3. Audit trail creation

**Hints**: Different regulations have different requirements. Consult legal.

**Skills**: Regulatory compliance

---

### E19: Debugging with Interpretability
**Domain**: Interpretability | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Use interpretability tools to debug models: find spurious correlations, data issues, and model errors.

**Expected Deliverables**:
- Error analysis with SHAP
- Spurious correlation detection
- Data issue identification

**Test Cases**:
1. Find unexpected feature effects
2. Detect data leakage
3. Identify model failures

**Hints**: Interpretability is powerful for debugging, not just explaining.

**Skills**: Debugging with interpretability

---

### E20: Interpretability Comparison Study
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Compare all major interpretability methods on same model. Create selection guidelines.

**Expected Deliverables**:
- All methods on same data
- Agreement/disagreement analysis
- Method selection framework

**Test Cases**:
1. Compare feature rankings
2. Where methods agree/disagree
3. Computational cost comparison

**Hints**: Different methods have different assumptions. Use multiple approaches.

**Skills**: Method comparison

---

### E21: Interpretability Project
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Complete interpretability analysis for a model: global and local explanations, stakeholder communication.

**Expected Deliverables**:
- Complete explanation package
- Technical and non-technical reports
- Actionable insights

**Hints**: Different stakeholders need different explanations.

**Skills**: End-to-end interpretability

---

### E22: Interpretability Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Comprehensive interpretability analysis: all major methods, fairness analysis, documentation, presentation to stakeholders.

**Expected Deliverables**:
- All interpretability methods
- Fairness audit
- Model card
- Stakeholder presentation

**Evaluation Criteria**: Completeness, clarity, actionability

**Hints**: Balance technical depth with accessibility.

**Skills**: Complete interpretability mastery

---

## Section F: Anomaly Detection (F1-F25)

### F1: Statistical Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Implement statistical methods: z-score, modified z-score, IQR, Grubbs test. Understand assumptions.

**Mathematical Foundation**:
- Z-score: (x - μ) / σ > threshold
- IQR: x < Q1 - 1.5×IQR or x > Q3 + 1.5×IQR

**Expected Deliverables**:
- Z-score detection
- IQR method
- Comparison on different distributions

**Test Cases**:
1. Detect Gaussian outliers
2. Handle skewed data
3. Multivariate extension

**Hints**: Modified z-score (MAD) more robust. Grubbs for single outlier.

**Skills**: Statistical anomaly detection

---

### F2: Isolation Forest
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply Isolation Forest: isolate anomalies by random partitioning. Anomalies are easier to isolate.

**Mathematical Foundation**:
- Anomaly score based on path length
- Shorter path = more likely anomaly

**Expected Deliverables**:
- Isolation Forest usage
- Contamination parameter tuning
- Anomaly visualization

**Test Cases**:
1. Detect synthetic outliers
2. Tune contamination
3. High-dimensional data

**Hints**: contamination = expected anomaly fraction. Works well high-d.

**Skills**: Isolation Forest

---

### F3: Local Outlier Factor (LOF)
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply LOF that measures local density deviation. Points with much lower density than neighbors are anomalies.

**Mathematical Foundation**:
- Reachability distance
- Local reachability density (LRD)
- LOF = avg(LRD of neighbors) / LRD(point)

**Expected Deliverables**:
- LOF implementation
- k parameter tuning
- Comparison with global methods

**Test Cases**:
1. Detect local anomalies
2. Compare with Isolation Forest
3. Cluster-specific anomalies

**Hints**: LOF is local, can detect anomalies in variable density data.

**Skills**: Local Outlier Factor

---

### F4: One-Class SVM
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply One-Class SVM that learns boundary of normal data. Points outside are anomalies.

**Expected Deliverables**:
- One-Class SVM usage
- Nu parameter tuning
- Kernel selection

**Test Cases**:
1. Train on normal only
2. Detect anomalies
3. Compare with Isolation Forest

**Hints**: Nu = upper bound on fraction of outliers. RBF kernel common.

**Skills**: One-Class SVM

---

### F5: Elliptic Envelope
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Apply Elliptic Envelope assuming Gaussian distribution. Fits Mahalanobis distance threshold.

**Mathematical Foundation**:
- Mahalanobis distance: d = √((x-μ)ᵀΣ⁻¹(x-μ))
- Points with high distance are anomalies

**Expected Deliverables**:
- Elliptic Envelope usage
- Mahalanobis distance
- Comparison with IQR

**Test Cases**:
1. Gaussian data
2. Non-Gaussian comparison
3. Robust covariance estimation

**Hints**: Works well for Gaussian. MinCovDet for robust estimation.

**Skills**: Elliptic Envelope

---

### F6: DBSCAN for Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Use DBSCAN noise points as anomalies. Points not belonging to any cluster are potential anomalies.

**Expected Deliverables**:
- DBSCAN noise detection
- Parameter tuning
- Cluster-aware anomaly detection

**Test Cases**:
1. Identify noise points
2. Tune eps and min_samples
3. Compare with dedicated methods

**Hints**: DBSCAN naturally identifies noise. Combine with other methods.

**Skills**: Density-based anomaly detection

---

### F7: Autoencoder for Anomaly Detection
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Use autoencoder reconstruction error for anomaly detection. High error indicates anomaly.

**Mathematical Foundation**:
- Train to minimize reconstruction error on normal data
- Error = ||x - decoder(encoder(x))||

**Expected Deliverables**:
- Autoencoder training
- Reconstruction error threshold
- Comparison with traditional methods

**Test Cases**:
1. Train on normal data
2. Detect anomalies by error
3. Threshold selection

**Hints**: Train only on normal data. Larger error = more anomalous.

**Skills**: Autoencoder anomaly detection

---

### F8: Variational Autoencoder for Anomalies
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Use VAE likelihood for anomaly scoring. Low likelihood under learned distribution indicates anomaly.

**Expected Deliverables**:
- VAE training
- Likelihood-based scoring
- Comparison with standard autoencoder

**Test Cases**:
1. Train VAE on normal data
2. Score new samples
3. Compare with reconstruction error

**Hints**: VAE provides probabilistic score. ELBO as anomaly score.

**Skills**: VAE anomaly detection

---

### F9: Time Series Anomaly Detection
**Domain**: Time Series | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Detect anomalies in time series: point anomalies, contextual anomalies, collective anomalies.

**Expected Deliverables**:
- Residual-based detection
- Seasonal anomaly handling
- Multiple anomaly types

**Test Cases**:
1. Point anomaly detection
2. Seasonal adjustment
3. Pattern anomalies

**Hints**: STL decomposition helps. Consider context and seasonality.

**Skills**: Time series anomaly detection

---

### F10: Multivariate Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Detect anomalies in multivariate data: relationships between features matter, not just individual values.

**Expected Deliverables**:
- Multivariate methods
- Relationship-based detection
- Visualization in high dimensions

**Test Cases**:
1. Detect relationship anomalies
2. Compare univariate vs multivariate
3. Handle high dimensions

**Hints**: Point normal in each feature can be anomalous in combination.

**Skills**: Multivariate anomaly detection

---

### F11: Fraud Detection System
**Domain**: Application | **Difficulty**: ★★★★☆ | **Time**: 75 min
**Implementation**: Libraries

**Problem**: Build fraud detection system: class imbalance, real-time scoring, false positive management.

**Dataset**: Credit card fraud or synthetic

**Expected Deliverables**:
- Fraud detection model
- Imbalance handling
- Alert prioritization

**Test Cases**:
1. High recall on fraud
2. Manageable false positives
3. Score interpretation

**Hints**: Cost-sensitive learning. Optimize for business metrics.

**Skills**: Fraud detection

---

### F12: Network Intrusion Detection
**Domain**: Application | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Detect network intrusions using ML: feature engineering from network data, real-time detection.

**Dataset**: KDD Cup 99 or UNSW-NB15

**Expected Deliverables**:
- Network feature extraction
- Anomaly model
- Detection evaluation

**Test Cases**:
1. Detect known attacks
2. Detect zero-day (novel) attacks
3. Low false positive rate

**Hints**: Feature engineering is crucial. Combine signature and anomaly detection.

**Skills**: Network anomaly detection

---

### F13: Sensor Data Anomaly Detection
**Domain**: IoT | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Detect anomalies in sensor/IoT data streams: missing values, sensor drift, failure detection.

**Expected Deliverables**:
- Streaming anomaly detection
- Sensor drift detection
- Multiple sensor correlation

**Test Cases**:
1. Detect sensor failures
2. Handle missing data
3. Cross-sensor anomalies

**Hints**: Consider temporal patterns. Use sliding windows.

**Skills**: IoT anomaly detection

---

### F14: Contextual Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Detect contextual anomalies where values are only anomalous in certain contexts (time, location, etc.).

**Expected Deliverables**:
- Context-aware methods
- Segmented detection
- Context feature engineering

**Test Cases**:
1. Time-based context
2. Categorical context
3. Dynamic context

**Hints**: Normal value depends on context. Segment or include context as feature.

**Skills**: Contextual anomalies

---

### F15: Collective Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Detect collective anomalies: sequences of normal points that together form anomaly.

**Expected Deliverables**:
- Sequence anomaly detection
- Pattern-based methods
- Visualization of collective anomalies

**Test Cases**:
1. Detect unusual patterns
2. Sequence classification
3. Temporal pattern anomalies

**Hints**: Individual points may be normal; pattern is anomalous.

**Skills**: Collective anomalies

---

### F16: Semi-Supervised Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Use labeled normal data (and possibly few labeled anomalies) for better detection.

**Expected Deliverables**:
- Train on labeled normal
- Incorporate few anomaly examples
- Comparison with unsupervised

**Test Cases**:
1. Normal-only training
2. Add few anomaly labels
3. Improvement from labels

**Hints**: Even few labeled anomalies can significantly improve detection.

**Skills**: Semi-supervised anomalies

---

### F17: Ensemble Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Combine multiple anomaly detectors for robust detection. Handle score normalization.

**Expected Deliverables**:
- Multiple detectors
- Score normalization
- Ensemble strategies

**Test Cases**:
1. Combine Isolation Forest + LOF
2. Normalize scores
3. Compare with single detector

**Hints**: Different methods catch different anomalies. Normalize scores before combining.

**Skills**: Ensemble anomalies

---

### F18: Anomaly Detection Evaluation
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Evaluate anomaly detection: precision, recall, F1, PR-AUC for imbalanced anomaly detection.

**Expected Deliverables**:
- Appropriate metrics
- PR curve analysis
- Threshold selection

**Test Cases**:
1. Compute all metrics
2. PR-AUC comparison
3. Business-driven threshold

**Hints**: Use PR-AUC for imbalanced. F1 at different thresholds.

**Skills**: Anomaly evaluation

---

### F19: Threshold Selection
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Select optimal anomaly threshold: percentile, contamination, cost-based, dynamic thresholds.

**Expected Deliverables**:
- Multiple threshold strategies
- Dynamic thresholds
- Cost-based selection

**Test Cases**:
1. Fixed percentile
2. Adaptive threshold
3. Cost-sensitive selection

**Hints**: Threshold depends on domain. Use validation data or business costs.

**Skills**: Threshold selection

---

### F20: Explaining Anomalies
**Domain**: Interpretability | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Explain why a point is anomalous: feature contributions, comparison with normal, root cause.

**Expected Deliverables**:
- Feature-level explanation
- Nearest normal comparison
- Anomaly report generation

**Test Cases**:
1. Explain Isolation Forest prediction
2. SHAP for anomaly scores
3. Generate human-readable explanation

**Hints**: SHAP works on anomaly scores. Compare with similar normal points.

**Skills**: Anomaly explanation

---

### F21: Real-Time Anomaly Detection
**Domain**: MLOps | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Deploy anomaly detection for real-time streaming: latency requirements, model updating, alerting.

**Expected Deliverables**:
- Streaming architecture
- Low-latency scoring
- Alert system

**Test Cases**:
1. Score in real-time
2. Handle model updates
3. Alert generation

**Hints**: Pre-computed statistics for speed. River for online learning.

**Skills**: Real-time anomaly detection

---

### F22: Anomaly Detection at Scale
**Domain**: MLOps | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Scale anomaly detection to large datasets: approximate methods, distributed computing, sampling.

**Expected Deliverables**:
- Scalable algorithms
- Sampling strategies
- Performance profiling

**Test Cases**:
1. Handle million-scale data
2. Approximate vs exact
3. Memory efficiency

**Hints**: Isolation Forest scales well. LOF needs approximation.

**Skills**: Scalable anomaly detection

---

### F23: Anomaly Detection Pipeline
**Domain**: MLOps | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Build complete anomaly detection pipeline: preprocessing, detection, explanation, alerting.

**Expected Deliverables**:
- End-to-end pipeline
- Feature preprocessing
- Alert routing

**Test Cases**:
1. Complete pipeline execution
2. Handle new data types
3. Alert prioritization

**Hints**: Modular design. Clear interface between components.

**Skills**: AD pipeline

---

### F24: Anomaly Detection Project
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete anomaly detection project: EDA, method selection, evaluation, deployment preparation.

**Dataset**: Credit card fraud, sensor data, or custom

**Expected Deliverables**:
- Complete analysis
- Method comparison
- Deployment-ready model
- Documentation

**Hints**: Start with simple methods. Evaluate carefully on imbalanced data.

**Skills**: End-to-end AD project

---

### F25: Anomaly Detection Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★★ | **Time**: 150 min
**Implementation**: Libraries

**Problem**: Comprehensive anomaly detection system: multiple methods, real-time capability, explanation, monitoring.

**Expected Deliverables**:
- Multi-method ensemble
- Real-time scoring
- Explainable alerts
- Monitoring dashboard
- Complete documentation

**Evaluation Criteria**: Completeness, robustness, production readiness

**Hints**: Combine multiple approaches for robustness.

**Skills**: Complete anomaly detection mastery

---
