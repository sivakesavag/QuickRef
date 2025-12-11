# Python Advanced Level Assignments (1-160)

> **Level**: Advanced | **Prerequisites**: Intermediate Level | **Focus**: Advanced Python, ML, Automation

---

## Section A: Decorators & Advanced Functions (A1-A20)

### A1: Simple Decorator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Create decorator that logs function entry and exit.

**Output**: Logs function name, args, return value

**Skills**: Decorator basics, functools.wraps

---

### A2: Decorator with Arguments
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create parameterized decorator for retry logic.

**Usage**: `@retry(max_attempts=3, delay=1.0)`

**Skills**: Decorator factories

---

### A3: Timing Decorator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Measure function execution time.

**Features**: Log to console, return timing in result

**Skills**: time module, decorator wrapping

---

### A4: Memoization Decorator
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement caching decorator with TTL.

**Features**: Cache expiration, size limit

**Skills**: Caching patterns, closures

---

### A5: Access Control Decorator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Role-based access control decorator.

**Usage**: `@requires_role('admin')`

**Skills**: Authorization patterns

---

### A6: Validation Decorator
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Validate function arguments with schema.

**Usage**: `@validate(arg_types={'x': int, 'y': str})`

**Skills**: Type checking, inspect module

---

### A7: Rate Limiter Decorator
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Limit function calls per time period.

**Features**: Configurable limit and window

**Skills**: Time tracking, thread safety

---

### A8: Deprecation Decorator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Warn when deprecated function is called.

**Features**: Custom message, version info

**Skills**: warnings module

---

### A9: Debug Decorator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Enable/disable debugging output.

**Features**: Environment-based, verbose levels

**Skills**: Conditional decorator

---

### A10: Decorator Stacking
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 40 min

**Problem**: Correctly stack multiple decorators.

**Focus**: Order of execution, preserving metadata

**Skills**: Multiple decorators

---

### A11: Class Decorator
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Create decorator that modifies class behavior.

**Examples**: @dataclass alternative, @singleton, @register

**Skills**: Class decorators

---

### A12: Method Decorators
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 40 min

**Problem**: Decorate methods, handle self properly.

**Skills**: Method decoration, descriptor protocol

---

### A13: Async Decorator
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Create decorator for async functions.

**Skills**: async/await in decorators

---

### A14: Property Factory
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Create property decorator with validation.

**Usage**: `@validated_property(type=int, min=0, max=100)`

**Skills**: Property descriptors

---

### A15: Context-Aware Decorator
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Decorator that behaves differently in different contexts.

**Skills**: Context detection, adaptive behavior

---

### A16: Recursive Function Decorator
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Track and limit recursion depth.

**Features**: Depth logging, max depth enforcement

**Skills**: Recursion tracking

---

### A17: Plugin System
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 60 min

**Problem**: Build plugin registration system using decorators.

**Features**: Register, discover, load plugins

**Skills**: Plugin architecture

---

### A18: Benchmark Suite
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Build benchmarking framework with decorators.

**Features**: Multiple runs, statistics, comparison

**Skills**: Performance measurement

---

### A19: Dependency Injection
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 60 min

**Problem**: Implement DI container with decorators.

**Features**: Constructor injection, singleton scope

**Skills**: DI pattern

---

### A20: Decorator Introspection
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Inspect and document decorated functions.

**Skills**: inspect module, decorator metadata

---

## Section B: Generators & Iterators (B1-B15)

### B1: Basic Generator
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Create generator for Fibonacci sequence.

**Skills**: yield, generator basics

---

### B2: Generator Expression
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 25 min

**Problem**: Convert list comprehensions to generators.

**Focus**: Memory efficiency comparison

**Skills**: Generator expressions

---

### B3: File Line Generator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Read large files lazily.

**Skills**: File generators, memory efficiency

---

### B4: Infinite Generators
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create infinite sequence generators.

**Examples**: Counter, cycle, repeat with variations

**Skills**: Infinite sequences

---

### B5: Generator Pipeline
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Chain generators for data processing.

**Pipeline**: Read → Filter → Transform → Aggregate

**Skills**: Pipeline pattern

---

### B6: Two-Way Generators
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Use send() for bidirectional communication.

**Skills**: Generator coroutines

---

### B7: Generator Delegation
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 40 min

**Problem**: Use yield from for sub-generators.

**Skills**: yield from, delegation

---

### B8: Custom Iterator Class
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement __iter__ and __next__.

**Skills**: Iterator protocol

---

### B9: Reversible Iterator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create iterator that can go forward and backward.

**Skills**: __reversed__, custom navigation

---

### B10: Lazy Evaluation
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Implement lazy properties and sequences.

**Skills**: Lazy evaluation patterns

---

### B11: Coroutine Basics
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Create data processing coroutines.

**Pattern**: Consumer pattern with .send()

**Skills**: Coroutine pattern

---

### B12: Iterator Combinators
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Implement custom itertools functions.

**Functions**: Custom takewhile, dropwhile, groupby

**Skills**: Iterator operations

---

### B13: Streaming CSV Processor
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Process large CSV files with generators.

**Features**: Memory-efficient, transformation pipeline

**Skills**: Stream processing

---

### B14: Batch Iterator
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Yield items in configurable batch sizes.

**Skills**: Batching pattern

---

### B15: Generator State Machine
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 60 min

**Problem**: Implement state machine using generators.

**Skills**: State machine pattern

---

## Section C: Context Managers (C1-C12)

### C1: File Context Manager
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Create custom file handler with logging.

**Skills**: __enter__, __exit__

---

### C2: Timer Context Manager
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Measure code block execution time.

**Skills**: Context manager timing

---

### C3: contextlib Decorators
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Use @contextmanager decorator.

**Skills**: contextlib.contextmanager

---

### C4: Database Connection Manager
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Manage database connections with pooling.

**Skills**: Connection management

---

### C5: Transaction Manager
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Implement transaction with commit/rollback.

**Skills**: Transaction pattern

---

### C6: Lock Manager
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Manage threading locks safely.

**Skills**: Thread synchronization

---

### C7: Temporary Directory
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create and cleanup temp directories.

**Skills**: tempfile module, cleanup

---

### C8: Redirect Output
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Redirect stdout/stderr temporarily.

**Skills**: contextlib.redirect_stdout

---

### C9: Suppress Exceptions
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Contextually suppress specific exceptions.

**Skills**: contextlib.suppress

---

### C10: Nested Context Managers
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 40 min

**Problem**: Safely nest multiple context managers.

**Skills**: ExitStack

---

### C11: Async Context Manager
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Create async context manager.

**Skills**: __aenter__, __aexit__

---

### C12: Resource Pool Manager
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 60 min

**Problem**: Build resource pool with reuse and cleanup.

**Skills**: Pool pattern, lifecycle management

---

## Section D: Web Scraping (D1-D18)

### D1: BeautifulSoup Basics
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Parse HTML and extract elements.

**Skills**: BeautifulSoup, find, find_all

---

### D2: CSS Selectors
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Use CSS selectors for element selection.

**Skills**: select, select_one

---

### D3: Attribute Extraction
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Extract links, images, metadata.

**Skills**: Attribute access, href, src

---

### D4: Table Scraping
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Extract tables to DataFrames.

**Skills**: Table parsing, pandas integration

---

### D5: Form Data Extraction
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Extract form fields and values.

**Skills**: Form element parsing

---

### D6: Pagination Handling
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Scrape paginated content.

**Skills**: Page navigation, URL patterns

---

### D7: Request Headers
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Handle User-Agent and headers.

**Skills**: Request headers, anti-bot measures

---

### D8: Session Cookies
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Maintain session state across requests.

**Skills**: Session management

---

### D9: Rate Limiting Scraper
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Implement polite scraping with delays.

**Skills**: Rate limiting, ethics

---

### D10: Error Handling
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 40 min

**Problem**: Handle failures gracefully.

**Skills**: Retry, timeout, error recovery

---

### D11: Selenium Basics
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Automate browser for JavaScript sites.

**Skills**: WebDriver, element location

---

### D12: Wait Strategies
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 40 min

**Problem**: Handle dynamic content loading.

**Skills**: Explicit waits, expected conditions

---

### D13: Form Automation
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Fill and submit forms automatically.

**Skills**: Form interaction, validation

---

### D14: Screenshot Capture
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Capture page screenshots.

**Skills**: Screenshot API, evidence collection

---

### D15: Data Extraction Pipeline
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 75 min

**Problem**: Build complete scraping pipeline.

**Features**: Extract, clean, store, schedule

**Skills**: End-to-end scraping

---

### D16: API Discovery
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Find and use hidden APIs.

**Skills**: Network inspection, API reverse engineering

---

### D17: robots.txt Compliance
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Parse and respect robots.txt.

**Skills**: Ethical scraping

---

### D18: News Scraper Project
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 120 min

**Problem**: Build multi-source news aggregator.

**Features**: Multiple sites, deduplication, storage

**Skills**: Complete scraping project

---

## Section E: Machine Learning with scikit-learn (E1-E30)

### E1: Dataset Loading
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Load and explore built-in datasets.

**Skills**: sklearn.datasets, data exploration

---

### E2: Train-Test Split
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Split data properly for validation.

**Skills**: train_test_split, stratification

---

### E3: Feature Scaling
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Scale features using different methods.

**Methods**: StandardScaler, MinMaxScaler, RobustScaler

**Skills**: Preprocessing, pipelines

---

### E4: Label Encoding
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Encode categorical variables.

**Methods**: LabelEncoder, OneHotEncoder, OrdinalEncoder

**Skills**: Categorical encoding

---

### E5: Linear Regression
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Build and evaluate linear regression.

**Metrics**: MSE, RMSE, R², MAE

**Skills**: Regression modeling

---

### E6: Polynomial Regression
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Handle non-linear relationships.

**Skills**: PolynomialFeatures, overfitting

---

### E7: Logistic Regression
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Binary classification with logistic regression.

**Skills**: Classification basics

---

### E8: Decision Trees
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Build and visualize decision trees.

**Skills**: DecisionTreeClassifier, visualization

---

### E9: Random Forest
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Ensemble learning with random forests.

**Skills**: RandomForestClassifier, feature importance

---

### E10: Gradient Boosting
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: XGBoost or GradientBoosting modeling.

**Skills**: Boosting, hyperparameter tuning

---

### E11: K-Nearest Neighbors
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: KNN for classification and regression.

**Skills**: KNeighborsClassifier, distance metrics

---

### E12: Support Vector Machines
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: SVM with different kernels.

**Skills**: SVC, kernel tricks

---

### E13: Naive Bayes
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Text classification with Naive Bayes.

**Skills**: MultinomialNB, GaussianNB

---

### E14: K-Means Clustering
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Unsupervised clustering.

**Skills**: KMeans, elbow method, silhouette

---

### E15: Hierarchical Clustering
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Agglomerative clustering.

**Skills**: Dendrograms, linkage methods

---

### E16: DBSCAN
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Density-based clustering.

**Skills**: DBSCAN, noise handling

---

### E17: PCA
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Dimensionality reduction with PCA.

**Skills**: PCA, explained variance

---

### E18: Cross-Validation
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Proper model validation.

**Methods**: KFold, StratifiedKFold, cross_val_score

**Skills**: Validation strategies

---

### E19: Hyperparameter Tuning
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Optimize model hyperparameters.

**Methods**: GridSearchCV, RandomizedSearchCV

**Skills**: Hyperparameter optimization

---

### E20: Model Pipelines
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Build end-to-end ML pipelines.

**Skills**: Pipeline, ColumnTransformer

---

### E21: Confusion Matrix
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Evaluate classification with confusion matrix.

**Skills**: Metrics, precision, recall, F1

---

### E22: ROC Curves
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Plot and interpret ROC curves.

**Skills**: ROC, AUC, threshold tuning

---

### E23: Feature Selection
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Select best features.

**Methods**: SelectKBest, RFE, feature importance

**Skills**: Feature selection

---

### E24: Handling Imbalanced Data
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Deal with class imbalance.

**Methods**: SMOTE, class weights, undersampling

**Skills**: Imbalanced learning

---

### E25: Model Persistence
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Save and load trained models.

**Skills**: joblib, pickle

---

### E26: House Price Prediction
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 90 min

**Problem**: End-to-end regression project.

**Skills**: Complete ML workflow

---

### E27: Customer Churn Prediction
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 90 min

**Problem**: Binary classification project.

**Skills**: Classification, feature engineering

---

### E28: Credit Card Fraud Detection
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 120 min

**Problem**: Anomaly detection with imbalanced data.

**Skills**: Imbalanced learning, anomaly detection

---

### E29: Image Classification
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 90 min

**Problem**: Classify images with traditional ML.

**Skills**: Image features, SVM/RF

---

### E30: ML Model Comparison Framework
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 120 min

**Problem**: Build automated model comparison system.

**Features**: Multiple models, metrics, reporting

**Skills**: ML automation

---

## Section F: Statistical Analysis & EDA (F1-F20)

### F1: Descriptive Statistics
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Compute comprehensive descriptive stats.

**Skills**: scipy.stats, pandas describe

---

### F2: Distribution Analysis
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Identify and visualize distributions.

**Skills**: Histograms, distribution fitting

---

### F3: Correlation Analysis
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Calculate and visualize correlations.

**Methods**: Pearson, Spearman, Kendall

**Skills**: Correlation analysis

---

### F4: Hypothesis Testing Basics
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Perform t-tests and interpret results.

**Skills**: scipy.stats, p-values

---

### F5: ANOVA
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Compare means across groups.

**Skills**: One-way ANOVA, post-hoc tests

---

### F6: Chi-Square Test
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Test categorical relationships.

**Skills**: chi2_contingency, independence

---

### F7: Normality Tests
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Test distribution normality.

**Methods**: Shapiro-Wilk, K-S test

**Skills**: Normality testing

---

### F8: Outlier Detection
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Detect and handle outliers.

**Methods**: IQR, Z-score, isolation forest

**Skills**: Outlier analysis

---

### F9: Missing Data Analysis
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Analyze and impute missing data.

**Methods**: MCAR, MAR, MNAR analysis

**Skills**: Missing data handling

---

### F10: EDA Report Generator
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Automated EDA report.

**Features**: Stats, distributions, correlations

**Skills**: Automated EDA

---

### F11: Time Series EDA
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Analyze time series patterns.

**Skills**: Trends, seasonality, autocorrelation

---

### F12: Multivariate Analysis
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Analyze multivariate relationships.

**Skills**: PCA for EDA, factor analysis

---

### F13: Bootstrap Confidence Intervals
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Compute CIs using bootstrap.

**Skills**: Bootstrap resampling

---

### F14: Power Analysis
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Calculate sample size and power.

**Skills**: Effect size, power calculation

---

### F15: Multiple Testing Correction
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Handle multiple comparisons.

**Methods**: Bonferroni, FDR

**Skills**: Multiple testing

---

### F16: Regression Diagnostics
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Check regression assumptions.

**Skills**: Residual analysis, heteroscedasticity

---

### F17: AB Test Calculator
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Statistical significance calculator.

**Skills**: AB testing, conversion rates

---

### F18: Survey Data Analysis
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 70 min

**Problem**: Analyze Likert scale data.

**Skills**: Ordinal data analysis

---

### F19: Cohort Analysis
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 70 min

**Problem**: Analyze user cohorts over time.

**Skills**: Cohort analysis, retention

---

### F20: Complete EDA Project
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 150 min

**Problem**: Full exploratory analysis project.

**Dataset**: Real-world dataset
**Deliverable**: EDA notebook with insights

**Skills**: End-to-end EDA

---

## Section G: Multithreading & Multiprocessing (G1-G15)

### G1: Threading Basics
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create and run threads.

**Skills**: threading module, Thread class

---

### G2: Thread Synchronization
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 45 min

**Problem**: Use locks for shared data.

**Skills**: Lock, RLock, Semaphore

---

### G3: Thread Pool
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Process tasks with thread pool.

**Skills**: ThreadPoolExecutor

---

### G4: Producer-Consumer
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Implement producer-consumer pattern.

**Skills**: Queue, threading

---

### G5: Process Basics
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Create and run processes.

**Skills**: multiprocessing module

---

### G6: Process Pool
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Parallel processing with pool.

**Skills**: ProcessPoolExecutor

---

### G7: Inter-Process Communication
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Share data between processes.

**Skills**: Queue, Pipe, Manager

---

### G8: Map-Reduce Pattern
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Implement map-reduce with multiprocessing.

**Skills**: Parallel patterns

---

### G9: Parallel File Processing
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Process multiple files concurrently.

**Skills**: File I/O parallelization

---

### G10: Thread-Safe Data Structures
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Create thread-safe collections.

**Skills**: Thread safety patterns

---

### G11: Deadlock Prevention
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 55 min

**Problem**: Detect and prevent deadlocks.

**Skills**: Deadlock avoidance

---

### G12: Parallel Web Requests
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Make concurrent HTTP requests.

**Skills**: I/O-bound parallelism

---

### G13: Concurrent Data Loader
**Domain**: Data Science | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Load large datasets in parallel.

**Skills**: Parallel data loading

---

### G14: Progress Tracking
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Track progress in parallel tasks.

**Skills**: tqdm, progress reporting

---

### G15: Parallel ML Training
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 90 min

**Problem**: Parallelize model training.

**Skills**: Parallel ML, n_jobs

---

## Section H: CLI Tools & Automation (H1-H15)

### H1: Argparse Basics
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Build CLI with argparse.

**Skills**: Arguments, options, help

---

### H2: Subcommands
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Create CLI with subcommands.

**Skills**: Subparsers, git-style CLI

---

### H3: Click Framework
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Build CLI with Click.

**Skills**: click decorators

---

### H4: Interactive CLI
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Build interactive prompt interface.

**Skills**: prompt_toolkit or questionary

---

### H5: Progress Bars
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Add progress indicators.

**Skills**: tqdm, rich

---

### H6: Rich Console Output
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Create beautiful terminal output.

**Skills**: rich library

---

### H7: Configuration Management
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Handle CLI configuration.

**Skills**: Config files, environment

---

### H8: Scheduled Tasks
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: Schedule recurring tasks.

**Skills**: schedule library, cron

---

### H9: File Watch Automation
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 50 min

**Problem**: React to file system changes.

**Skills**: watchdog library

---

### H10: System Automation
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Automate system administration.

**Skills**: subprocess, os, shutil

---

### H11: Email Automation
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Send automated emails.

**Skills**: smtplib, email module

---

### H12: PDF Generation
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Generate PDF reports.

**Skills**: reportlab or fpdf

---

### H13: Excel Automation
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 55 min

**Problem**: Automate Excel operations.

**Skills**: openpyxl automation

---

### H14: Backup System
**Domain**: Scripting | **Difficulty**: ★★★★☆ | **Time**: 60 min

**Problem**: Build automated backup system.

**Features**: Incremental, compression, scheduling

**Skills**: Backup patterns

---

### H15: Complete CLI Application
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 120 min

**Problem**: Build production-ready CLI tool.

**Features**: Subcommands, config, logging, tests

**Skills**: Complete CLI project

---

## Advanced Level Capstone Projects (CAP1-CAP10)

### CAP1: Data Pipeline Framework
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 8 hours

**Description**: Build extensible ETL framework.

**Features**: Sources, transformations, destinations, scheduling

**Skills**: Generators, decorators, OOP

---

### CAP2: Web Scraping Platform
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 8 hours

**Description**: Multi-site scraping platform.

**Features**: Rate limiting, storage, scheduling, monitoring

**Skills**: Scraping, threading, databases

---

### CAP3: ML Experiment Tracker
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 8 hours

**Description**: Track ML experiments.

**Features**: Parameters, metrics, models, comparison

**Skills**: ML, decorators, storage

---

### CAP4: Automated Report Generator
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 6 hours

**Description**: Generate data reports automatically.

**Features**: Templates, charts, PDF/HTML output

**Skills**: Data processing, visualization

---

### CAP5: Task Scheduler System
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 6 hours

**Description**: Build task scheduling system.

**Features**: Cron, dependencies, monitoring

**Skills**: Threading, scheduling, persistence

---

### CAP6: Customer Analytics Platform
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 10 hours

**Description**: Complete customer analytics.

**Features**: Segmentation, CLV, churn, RFM

**Skills**: ML, statistics, visualization

---

### CAP7: Log Aggregation System
**Domain**: Scripting | **Difficulty**: ★★★★★ | **Time**: 6 hours

**Description**: Aggregate and analyze logs.

**Features**: Multiple sources, parsing, alerting

**Skills**: File processing, regex, threading

---

### CAP8: Data Validation Suite
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 6 hours

**Description**: Comprehensive data validation.

**Features**: Schema, rules, reporting, integration

**Skills**: OOP, decorators, pandas

---

### CAP9: Predictive Maintenance System
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 10 hours

**Description**: Predict equipment failures.

**Features**: Sensor data, ML, alerting

**Skills**: Time series, ML, automation

---

### CAP10: Trading Bot Simulator
**Domain**: Data Science | **Difficulty**: ★★★★★ | **Time**: 12 hours

**Description**: Backtest trading strategies.

**Features**: Data feeds, strategies, backtesting

**Skills**: Finance, ML, optimization

---

**Advanced Level Summary**:
- **Total Assignments**: 160
- **Decorators & Functions**: 20 assignments
- **Generators & Iterators**: 15 assignments
- **Context Managers**: 12 assignments
- **Web Scraping**: 18 assignments
- **Machine Learning**: 30 assignments
- **Statistics & EDA**: 20 assignments
- **Parallel Processing**: 15 assignments
- **CLI & Automation**: 15 assignments
- **Capstone Projects**: 10

---

*Continue to Expert Level: `python_assign_expert.md`*
