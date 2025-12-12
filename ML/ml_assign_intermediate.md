# Machine Learning Intermediate Level Assignments (1-155)

> **Level**: Intermediate | **Total Assignments**: 155 | **Prerequisites**: Beginner Level | **Focus**: Advanced Algorithms, Model Optimization, Unsupervised Learning

## Summary

| Section | Topic | Questions |
|---------|-------|-----------|
| A | Decision Trees & Tree-Based Methods | 25 |
| B | Support Vector Machines | 22 |
| C | Naive Bayes & Probabilistic Models | 22 |
| D | Ensemble Methods Basics | 25 |
| E | Clustering Algorithms | 28 |
| F | Dimensionality Reduction | 20 |
| G | Model Optimization & Hyperparameter Tuning | 13 |
| **Total** | | **155** |

---

## Section A: Decision Trees & Tree-Based Methods (A1-A25)

### A1: Decision Tree Classifier from Scratch
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 75 min
**Implementation**: From Scratch

**Problem**: Implement a decision tree classifier using recursive splitting with information gain (entropy) as the splitting criterion. Build the tree structure, implement prediction by traversing nodes, and visualize the resulting tree.

**Mathematical Foundation**:
- Entropy: H(S) = -Σ pᵢ log₂(pᵢ)
- Information Gain: IG(S, A) = H(S) - Σ (|Sᵥ|/|S|) × H(Sᵥ)

**Dataset**: Iris or synthetic classification data

**Expected Deliverables**:
- DecisionTreeClassifier class with fit() and predict()
- Recursive splitting logic
- Tree structure visualization

**Test Cases**:
1. Perfect split on linearly separable data
2. Match sklearn DecisionTreeClassifier results
3. Visualize tree structure

**Hints**: Use recursion for tree building. Stop when pure node or max depth reached.

**Skills**: Decision tree internals, recursive algorithms, entropy

---

### A2: Gini Impurity vs Entropy
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Implement Gini impurity and compare with entropy as splitting criteria. Understand the subtle differences: Gini is computationally faster, entropy tends to produce more balanced trees.

**Mathematical Foundation**:
- Gini: G(S) = 1 - Σ pᵢ²
- Both range from 0 (pure) to max at uniform distribution

**Expected Deliverables**:
- Gini impurity calculation
- Comparison of trees with Gini vs entropy
- Performance and structure differences

**Test Cases**:
1. Compare split choices on same data
2. Tree depth differences
3. Classification accuracy comparison

**Hints**: Use `criterion='gini'` vs `'entropy'` in sklearn. Gini is default.

**Skills**: Splitting criteria, impurity measures

---

### A3: Decision Tree for Regression
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: From Scratch

**Problem**: Implement a decision tree regressor that uses variance reduction as the splitting criterion and predicts the mean of leaf node samples. Understand how the same tree structure applies to both tasks.

**Mathematical Foundation**:
- Variance reduction: Var(S) - Σ (|Sᵥ|/|S|) × Var(Sᵥ)
- Prediction: mean of samples in leaf

**Expected Deliverables**:
- DecisionTreeRegressor from scratch
- Variance-based splitting
- Piecewise constant predictions visualization

**Test Cases**:
1. Fit non-linear data (sine wave)
2. Match sklearn DecisionTreeRegressor
3. Show staircase predictions

**Hints**: Same tree structure as classifier, just different split criterion and prediction method.

**Skills**: Regression trees, variance reduction

---

### A4: Tree Pruning Techniques
**Domain**: Classification/Regression | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Implement pre-pruning (early stopping) and understand post-pruning (cost-complexity pruning). Control tree complexity to prevent overfitting without losing predictive power.

**Mathematical Foundation**:
- Cost-complexity: Rα(T) = R(T) + α|T|
- Higher α = simpler trees

**Expected Deliverables**:
- Pre-pruning with max_depth, min_samples_split
- Cost-complexity pruning with ccp_alpha
- Optimal complexity selection via CV

**Test Cases**:
1. Unpruned tree overfits
2. Find optimal ccp_alpha
3. Compare pruned vs unpruned generalization

**Hints**: Use `ccp_alpha` parameter. Plot alpha vs tree size and accuracy.

**Skills**: Pruning, regularization for trees

---

### A5: Feature Importance in Trees
**Domain**: Interpretation | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Calculate and interpret feature importance based on impurity decrease. Understand limitations of this importance measure and when it can be misleading.

**Expected Deliverables**:
- Feature importance extraction
- Visualization (bar plot)
- Comparison with permutation importance

**Test Cases**:
1. Identify most important features
2. Show bias toward high-cardinality features
3. Compare with permutation importance

**Hints**: Use `.feature_importances_`. High-cardinality features get inflated importance.

**Skills**: Feature importance, model interpretation

---

### A6: Decision Boundary Visualization
**Domain**: Visualization | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Visualize decision tree boundaries showing the axis-aligned rectangular regions. Understand why trees create "staircase" boundaries and cannot capture diagonal separations efficiently.

**Expected Deliverables**:
- 2D decision boundary plot
- Effect of max_depth on boundaries
- Comparison with logistic regression boundaries

**Test Cases**:
1. Show rectangular decision regions
2. Increase depth = more complex boundaries
3. Struggle with diagonal separation

**Hints**: Create meshgrid, predict on all points. Trees always create axis-parallel splits.

**Skills**: Visualization, understanding tree limitations

---

### A7: Handling Missing Values in Trees
**Domain**: Data Handling | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Understand how decision trees can handle missing values natively (surrogate splits) or through preprocessing. Compare strategies for missing value handling.

**Expected Deliverables**:
- Imputation before tree fitting
- Trees with native missing handling (XGBoost, LightGBM)
- Performance comparison

**Test Cases**:
1. Compare imputation vs native handling
2. Performance on data with 20% missing
3. Which approach is more robust

**Hints**: sklearn trees don't handle missing natively; use imputation or gradient boosting libraries.

**Skills**: Missing data handling, tree algorithms

---

### A8: Categorical Features in Trees
**Domain**: Data Handling | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Handle categorical features in decision trees using encoding or native support. Understand how trees can split on categorical features optimally.

**Expected Deliverables**:
- One-hot encoding approach
- Ordinal encoding for trees
- Native categorical handling (CatBoost)

**Test Cases**:
1. Compare encoding strategies
2. Performance on high-cardinality categoricals
3. Interpretability of encoded trees

**Hints**: Trees can handle ordinal encoding well. One-hot creates many binary splits.

**Skills**: Categorical encoding for trees

---

### A9: CART Algorithm Deep Dive
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Conceptual + Code

**Problem**: Understand the CART (Classification and Regression Trees) algorithm in detail: binary splits, greedy optimization, and the search for optimal split points.

**Mathematical Foundation**:
- Binary splits only
- Greedy search over features and thresholds
- O(n × m × log n) complexity

**Expected Deliverables**:
- CART algorithm explanation
- Comparison with ID3, C4.5
- Computational complexity analysis

**Test Cases**:
1. Trace through CART on small dataset
2. Count number of split evaluations
3. Compare with other tree algorithms

**Hints**: CART is binary; ID3/C4.5 can have multi-way splits.

**Skills**: Algorithm understanding, tree variants

---

### A10: ID3 and C4.5 Algorithms
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: From Scratch (simplified)

**Problem**: Implement simplified versions of ID3 and understand C4.5 improvements: handling continuous attributes, missing values, and gain ratio to avoid high-cardinality bias.

**Mathematical Foundation**:
- Gain Ratio = Information Gain / Split Information
- Split Info = -Σ (|Sᵥ|/|S|) log₂(|Sᵥ|/|S|)

**Expected Deliverables**:
- ID3 implementation for categorical features
- Gain ratio calculation
- Understanding of C4.5 improvements

**Test Cases**:
1. ID3 on categorical dataset
2. Show gain ratio reduces high-cardinality bias
3. Compare with CART

**Hints**: ID3 only handles categorical; C4.5 adds continuous splitting.

**Skills**: Classic tree algorithms, historical context

---

### A11: Decision Tree Instability
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Demonstrate that decision trees have high variance: small changes in data lead to completely different trees. This motivates ensemble methods.

**Expected Deliverables**:
- Train trees on bootstrap samples
- Show structure variation
- Quantify prediction variance

**Test Cases**:
1. Remove one sample, tree changes dramatically
2. Bootstrap samples give very different trees
3. High variance, low bias demonstration

**Hints**: This instability is why Random Forests work so well (variance reduction).

**Skills**: Understanding tree variance, motivation for ensembles

---

### A12: Multi-Output Decision Trees
**Domain**: Regression/Classification | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use decision trees for multi-output prediction where each sample has multiple target variables. Single tree predicts all outputs simultaneously.

**Expected Deliverables**:
- Multi-output classification
- Multi-output regression
- When to use vs separate models

**Test Cases**:
1. Predict multiple related targets
2. Compare with separate trees per target
3. Computational advantage

**Hints**: Use sklearn DecisionTree with multi-dimensional y. Good when outputs are related.

**Skills**: Multi-output learning

---

### A13: Extremely Randomized Trees (Extra Trees)
**Domain**: Classification/Regression | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Understand Extra Trees which randomize split thresholds in addition to feature subsets. This adds more randomness than Random Forests, potentially reducing variance further.

**Expected Deliverables**:
- ExtraTreesClassifier/Regressor usage
- Comparison with Random Forest
- When Extra Trees outperforms

**Test Cases**:
1. Compare accuracy with Random Forest
2. Training time comparison
3. Variance comparison

**Hints**: Use `ExtraTreesClassifier`. Faster training due to no optimal threshold search.

**Skills**: Extra Trees, randomized algorithms

---

### A14: Decision Tree Interpretability
**Domain**: Interpretation | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Extract and present decision rules from trees in human-readable format. Create decision path explanations for individual predictions.

**Expected Deliverables**:
- Tree visualization (graphviz)
- Rule extraction
- Decision path for specific predictions

**Test Cases**:
1. Export tree as rules
2. Explain specific prediction path
3. Create business-friendly rules

**Hints**: Use `export_text` and `export_graphviz`. Trees are inherently interpretable.

**Skills**: Model interpretation, rule extraction

---

### A15: Monotonic Constraints in Trees
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply monotonic constraints where certain features should always have positive or negative relationship with target (e.g., higher income → higher credit limit).

**Expected Deliverables**:
- Monotonic constraint specification
- Comparison with unconstrained tree
- When constraints improve model

**Test Cases**:
1. Enforce monotonic relationship
2. Compare predictions at feature boundaries
3. Business rule enforcement

**Hints**: Use `monotone_cst` in HistGradientBoosting or LightGBM. Not available in basic sklearn trees.

**Skills**: Constrained optimization, domain knowledge integration

---

### A16: Handling Imbalanced Data with Trees
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply class weights and sampling techniques to improve decision tree performance on imbalanced datasets. Trees naturally find majority class splits.

**Expected Deliverables**:
- Class weight application
- Comparison with resampling
- Threshold adjustment for trees

**Test Cases**:
1. Baseline on imbalanced data
2. With class_weight='balanced'
3. Combined with pruning

**Hints**: Use `class_weight` parameter. Trees can overfit minority class without pruning.

**Skills**: Imbalanced classification with trees

---

### A17: Tree Ensemble Preparations
**Domain**: Theory | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Conceptual

**Problem**: Understand the theoretical foundation for tree ensembles: bootstrap aggregating (bagging), random subspace method, and how combining weak learners creates strong learners.

**Expected Deliverables**:
- Bias-variance decomposition for ensembles
- Bootstrap sampling explanation
- Why averaging reduces variance

**Test Cases**:
1. Variance of single tree vs average
2. Effect of tree correlation on variance reduction
3. Theoretical variance reduction formula

**Hints**: Variance of average of n uncorrelated variables is 1/n of individual variance.

**Skills**: Ensemble theory, variance reduction

---

### A18: Decision Trees for Feature Selection
**Domain**: Feature Engineering | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use tree-based feature importance for feature selection. Compare with other selection methods and understand when tree importance is misleading.

**Expected Deliverables**:
- Feature selection using tree importance
- Recursive Feature Elimination with trees
- Comparison with filter methods

**Test Cases**:
1. Select top 10 features by importance
2. Re-train with selected features
3. Compare accuracy before/after selection

**Hints**: Tree importance is fast but biased. Permutation importance is more reliable.

**Skills**: Feature selection, tree-based methods

---

### A19: Oblique Decision Trees
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Understand oblique trees that can make splits on linear combinations of features, not just single features. These can capture diagonal boundaries with fewer splits.

**Expected Deliverables**:
- Oblique tree concept explanation
- Implementation using sklearn or specialized library
- Comparison with axis-aligned trees

**Test Cases**:
1. Diagonal separation problem
2. Compare tree depth needed
3. Interpretability tradeoff

**Hints**: Standard sklearn doesn't support oblique trees. Use specialized implementations.

**Skills**: Advanced tree variants

---

### A20: Decision Tree Regression Visualization
**Domain**: Visualization | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Visualize decision tree regression predictions showing the piecewise constant approximation. Demonstrate underfitting with shallow trees and overfitting with deep trees.

**Expected Deliverables**:
- 1D regression tree visualization
- 2D surface plot for two features
- Depth effect visualization

**Test Cases**:
1. Fit sine wave with different depths
2. Show staircase approximation
3. Optimal depth selection

**Hints**: Trees create step functions. More depth = finer steps but risk overfitting.

**Skills**: Regression visualization, depth selection

---

### A21: Tree Model Comparison
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Compare decision trees with linear models, k-NN, and Naive Bayes on various datasets. Understand when trees excel (non-linear relationships, feature interactions).

**Expected Deliverables**:
- Performance comparison table
- Dataset characteristics analysis
- Algorithm selection guidelines

**Test Cases**:
1. Linear data: trees vs logistic regression
2. Complex interaction data: trees advantage
3. High-dimensional sparse: trees disadvantage

**Hints**: Trees excel with interactions and non-linearity but struggle with sparse high-d data.

**Skills**: Algorithm comparison, model selection

---

### A22: Decision Tree Computational Efficiency
**Domain**: Theory | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Conceptual + Benchmarks

**Problem**: Analyze time and space complexity of decision tree training and prediction. Understand why trees are fast to train and predict compared to many other algorithms.

**Expected Deliverables**:
- Training complexity analysis
- Prediction complexity analysis
- Benchmark results on varying data sizes

**Test Cases**:
1. Training time vs n and d
2. Prediction time vs tree depth
3. Memory usage analysis

**Hints**: Training is O(n × m × log n), prediction is O(depth).

**Skills**: Algorithm complexity, performance profiling

---

### A23: Decision Tree Real-World Project
**Domain**: End-to-End | **Difficulty**: ★★★☆☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Complete decision tree project with preprocessing, hyperparameter tuning, pruning, and interpretation. Create business-ready decision rules.

**Dataset**: Bank Marketing, Titanic, or Customer Churn

**Expected Deliverables**:
- Complete pipeline
- Hyperparameter optimization (depth, min_samples)
- Extract and present decision rules
- Business interpretation

**Evaluation Criteria**: Accuracy/F1, interpretability, business value

**Test Cases**:
1. Beat baseline significantly
2. Interpretable rules extracted
3. Handle categorical and missing data

**Hints**: Focus on interpretability. Trees are valued for explainability.

**Skills**: End-to-end project, business communication

---

### A24: Comparing Tree Libraries
**Domain**: Practical | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Compare decision tree implementations across libraries: sklearn, LightGBM single tree, CatBoost single tree. Understand API differences and feature support.

**Expected Deliverables**:
- API comparison
- Feature support comparison
- Performance benchmarks

**Test Cases**:
1. Same hyperparameters across libraries
2. Categorical handling differences
3. Missing value handling

**Hints**: HistGradientBoosting is faster sklearn tree implementation for large datasets.

**Skills**: Library comparison, practical ML

---

### A25: Decision Tree Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Comprehensive decision tree analysis: implement from scratch, compare with sklearn, analyze interpretability vs accuracy tradeoff, and create production-ready pipeline.

**Dataset**: Choose complex real-world dataset

**Expected Deliverables**:
- From-scratch implementation validation
- Optimal hyperparameters via CV
- Comprehensive interpretation
- Production pipeline
- Documentation and presentation

**Evaluation Criteria**: 
- Technical correctness
- Interpretation quality
- Production readiness

**Test Cases**:
1. From-scratch matches sklearn
2. Optimal depth/pruning found
3. Clear, actionable rules

**Hints**: Document tree construction step by step. Show value of interpretability.

**Skills**: Complete mastery of decision trees

---

## Section B: Support Vector Machines (B1-B22)

### B1: Linear SVM from Scratch
**Domain**: Classification | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: From Scratch

**Problem**: Implement a linear Support Vector Machine using gradient descent on the hinge loss. Find the maximum-margin hyperplane that separates classes with the largest gap.

**Mathematical Foundation**:
- Hinge loss: max(0, 1 - y(wᵀx + b))
- Objective: min 1/2||w||² + C Σ max(0, 1 - yᵢ(wᵀxᵢ + b))

**Dataset**: Synthetic linearly separable data

**Expected Deliverables**:
- LinearSVM class with fit() and predict()
- Margin visualization
- Support vector identification

**Test Cases**:
1. Find separating hyperplane
2. Identify support vectors
3. Match sklearn LinearSVC (approximately)

**Hints**: Use sub-gradient descent for hinge loss. Support vectors are points on or within margin.

**Skills**: SVM fundamentals, margin maximization, optimization

---

### B2: Soft Margin SVM
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Understand soft margin SVM that allows some misclassifications via slack variables. Control the bias-variance tradeoff with the C parameter.

**Mathematical Foundation**:
- Slack variables ξᵢ for margin violations
- C controls penalty for violations
- Large C = hard margin, Small C = soft margin

**Expected Deliverables**:
- C parameter effect visualization
- Decision boundary changes with C
- Optimal C selection via CV

**Test Cases**:
1. C=0.01 vs C=100 comparison
2. Optimal C on noisy data
3. Overfitting with large C

**Hints**: Use `C` parameter in sklearn SVC. Start with default C=1.

**Skills**: Soft margin, regularization in SVM

---

### B3: Kernel Trick Concept
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Conceptual + Code

**Problem**: Understand the kernel trick that computes inner products in high-dimensional space without explicit transformation. This enables non-linear decision boundaries efficiently.

**Mathematical Foundation**:
- K(x, x') = φ(x)ᵀφ(x')
- Compute in high-d without transforming

**Expected Deliverables**:
- Kernel function examples
- Why kernel trick is efficient
- Feature space dimension examples

**Test Cases**:
1. Polynomial kernel implicit dimension
2. RBF kernel infinite dimensions
3. Computational savings demonstration

**Hints**: K(x,x') for RBF is easy; explicit φ(x) would be infinite-dimensional.

**Skills**: Kernel trick, implicit feature spaces

---

### B4: Polynomial Kernel SVM
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply polynomial kernel for datasets with polynomial decision boundaries. Tune the degree and coef0 parameters for optimal performance.

**Mathematical Foundation**:
- K(x, x') = (γxᵀx' + coef0)^degree

**Expected Deliverables**:
- Polynomial kernel SVM
- Degree selection via CV
- Decision boundary visualization

**Test Cases**:
1. Degree 2 for quadratic boundaries
2. Overfitting with high degree
3. Compare with feature engineering + linear SVM

**Hints**: Use `kernel='poly'`, tune degree and coef0. Higher degree = more complex boundaries.

**Skills**: Polynomial kernel, hyperparameter tuning

---

### B5: RBF Kernel SVM
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply the Radial Basis Function (Gaussian) kernel, the most commonly used kernel. Understand the gamma parameter and its effect on decision boundary smoothness.

**Mathematical Foundation**:
- K(x, x') = exp(-γ||x - x'||²)
- Small γ = smooth boundary, Large γ = complex boundary

**Expected Deliverables**:
- RBF kernel SVM
- Gamma effect visualization
- C and gamma joint optimization

**Test Cases**:
1. Gamma effect on decision boundary
2. GridSearchCV for C and gamma
3. Circle inside circle problem

**Hints**: Use `kernel='rbf'`. Log scale for both C and gamma in grid search.

**Skills**: RBF kernel, two-parameter tuning

---

### B6: SVM Decision Boundary Analysis
**Domain**: Visualization | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Visualize SVM decision boundaries, margins, and support vectors for different kernels. Understand how kernel choice affects boundary shape.

**Expected Deliverables**:
- Decision boundary with margin
- Support vectors highlighted
- Comparison across kernels

**Test Cases**:
1. Linear kernel: straight line
2. RBF kernel: curved boundary
3. Show support vectors are boundary-defining

**Hints**: Use `decision_function` for distance to hyperplane. Contour at 0, ±1.

**Skills**: SVM visualization, understanding margins

---

### B7: SVM for Regression (SVR)
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply Support Vector Regression with epsilon-insensitive loss. Understand the epsilon-tube concept where errors within epsilon are ignored.

**Mathematical Foundation**:
- ε-insensitive loss: max(0, |y - f(x)| - ε)
- Points within tube don't contribute to loss

**Expected Deliverables**:
- SVR with different kernels
- Epsilon parameter effect
- Comparison with other regressors

**Test Cases**:
1. Fit non-linear function
2. Effect of epsilon on model
3. Compare with linear regression

**Hints**: Use `SVR`. Epsilon controls tube width; larger = simpler model.

**Skills**: SVR, epsilon-insensitive regression

---

### B8: One-Class SVM for Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Use One-Class SVM for unsupervised anomaly detection. Learn the boundary of normal data and flag points outside as anomalies.

**Expected Deliverables**:
- OneClassSVM training on normal data
- Anomaly score computation
- Threshold selection for detection

**Test Cases**:
1. Detect artificial outliers
2. Nu parameter effect
3. Compare with Isolation Forest

**Hints**: Use `OneClassSVM`. Nu parameter is upper bound on fraction of outliers.

**Skills**: Anomaly detection, one-class classification

---

### B9: Multi-Class SVM Strategies
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Extend binary SVM to multi-class using One-vs-Rest (OvR) and One-vs-One (OvO) strategies. Understand computational tradeoffs.

**Mathematical Foundation**:
- OvR: K classifiers
- OvO: K(K-1)/2 classifiers

**Expected Deliverables**:
- OvR implementation
- OvO implementation
- Accuracy and speed comparison

**Test Cases**:
1. 10-class problem OvR vs OvO
2. Training time comparison
3. Prediction consistency

**Hints**: sklearn uses OvO by default for SVC. Use `decision_function_shape`.

**Skills**: Multi-class extension, classifier strategies

---

### B10: SVM Feature Scaling Importance
**Domain**: Preprocessing | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Libraries

**Problem**: Demonstrate critical importance of feature scaling for SVM. Without scaling, features with larger magnitudes dominate the kernel computation.

**Expected Deliverables**:
- SVM without scaling
- SVM with scaling
- Performance comparison

**Test Cases**:
1. Dramatic accuracy difference
2. Effect on support vector positions
3. Standard vs MinMax scaling

**Hints**: Always scale for SVM. Use pipeline to prevent data leakage.

**Skills**: Preprocessing for SVM, impact of scaling

---

### B11: SVM Probability Estimates
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Obtain probability estimates from SVM using Platt scaling. Understand that SVM doesn't naturally produce probabilities and calibration is added post-hoc.

**Expected Deliverables**:
- Enable probability estimates
- Calibration quality assessment
- Comparison with logistic regression probabilities

**Test Cases**:
1. Enable probability=True
2. Assess calibration with reliability diagram
3. Training time impact

**Hints**: `probability=True` adds computational cost. Probabilities may not be well-calibrated.

**Skills**: SVM probability estimation, calibration

---

### B12: Kernel Selection Guide
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Develop guidelines for kernel selection based on data characteristics. Create a decision framework for choosing between linear, polynomial, RBF, and custom kernels.

**Expected Deliverables**:
- Kernel comparison framework
- Dataset characteristic mapping
- Performance comparison experiments

**Test Cases**:
1. High-d sparse: linear often best
2. Non-linear low-d: RBF
3. Domain knowledge: custom kernel

**Hints**: Start with RBF for non-linear, linear for high-d text/sparse data.

**Skills**: Kernel selection, practical guidelines

---

### B13: SVM Hyperparameter Tuning
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Efficiently tune SVM hyperparameters (C, gamma, kernel) using grid search and random search. Understand the search space geometry.

**Expected Deliverables**:
- Grid search over log scales
- Random search comparison
- Visualization of parameter space

**Test Cases**:
1. Find optimal C, gamma for RBF
2. Compare grid vs random search
3. Heatmap of CV scores

**Hints**: Use log scale for C and gamma. Start coarse, then refine.

**Skills**: Hyperparameter optimization for SVM

---

### B14: SVM Computational Considerations
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Benchmarks

**Problem**: Understand SVM computational complexity and when to use approximations. Training is O(n²) to O(n³), making large datasets challenging.

**Expected Deliverables**:
- Training time vs n analysis
- Memory requirements
- When to use LinearSVC vs SVC

**Test Cases**:
1. Training time scaling
2. Memory usage with kernel
3. SGDClassifier as alternative

**Hints**: For large n, use LinearSVC, SGDClassifier, or kernel approximations.

**Skills**: Computational complexity, practical scaling

---

### B15: Kernel Approximations
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Use Nyström approximation and Random Fourier Features to approximate kernels, enabling linear SVM on large datasets with non-linear boundaries.

**Mathematical Foundation**:
- Approximate K(x, x') with explicit features
- Linear SVM on transformed features

**Expected Deliverables**:
- Nyström implementation
- Random Fourier Features
- Accuracy vs time tradeoff

**Test Cases**:
1. Compare approximation vs exact kernel
2. Training time speedup
3. Optimal number of components

**Hints**: Use `sklearn.kernel_approximation`. Enables kernel SVM on large data.

**Skills**: Kernel approximations, scaling SVM

---

### B16: Custom Kernel Functions
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Define and use custom kernel functions for domain-specific similarity. Understand Mercer's condition for valid kernels.

**Mathematical Foundation**:
- Valid kernel: Gram matrix is positive semi-definite
- Mercer's theorem requirements

**Expected Deliverables**:
- Custom kernel function
- Integration with sklearn SVC
- Domain-specific kernel example

**Test Cases**:
1. String kernel for text
2. Verify kernel validity
3. Compare with standard kernels

**Hints**: Use `kernel='precomputed'` or callable kernel. Ensure positive definite.

**Skills**: Custom kernels, domain knowledge

---

### B17: SVM vs Logistic Regression
**Domain**: Comparison | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Compare SVM with logistic regression: loss functions, decision boundaries, probability outputs, and when each is preferred.

**Expected Deliverables**:
- Loss function comparison (hinge vs log loss)
- Decision boundary comparison
- Probability calibration comparison

**Test Cases**:
1. Same accuracy, different margins
2. Calibration quality difference
3. When SVM outperforms

**Hints**: Similar performance often; SVM better for max margin, LR for probabilities.

**Skills**: Algorithm comparison, understanding tradeoffs

---

### B18: SVM for Text Classification
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply linear SVM to text classification with TF-IDF features. SVMs are historically very effective for text due to high-dimensional sparse nature.

**Dataset**: 20 Newsgroups or IMDB Reviews

**Expected Deliverables**:
- TF-IDF + LinearSVC pipeline
- Performance on text classification
- Important features analysis

**Test Cases**:
1. Multi-class text classification
2. Compare with Naive Bayes
3. Feature analysis

**Hints**: LinearSVC is faster than SVC for text. TF-IDF vectorization essential.

**Skills**: Text classification with SVM

---

### B19: SVM for Image Classification
**Domain**: Computer Vision | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply SVM to image classification using hand-crafted or learned features. Understand SVM's role before deep learning dominated vision.

**Dataset**: MNIST or CIFAR-10 subset

**Expected Deliverables**:
- HOG/raw pixel features + SVM
- Kernel selection for images
- Performance analysis

**Test Cases**:
1. Raw pixels vs HOG features
2. RBF kernel performance
3. Compare with CNN (acknowledge gap)

**Hints**: Features matter more than kernel for images. SVM was state-of-art pre-deep learning.

**Skills**: Image classification, feature importance

---

### B20: SVM Real-World Project
**Domain**: End-to-End | **Difficulty**: ★★★☆☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Complete SVM project with proper preprocessing, kernel selection, hyperparameter tuning, and visualization of decision boundaries/support vectors.

**Dataset**: Breast Cancer, Wine, or Custom

**Expected Deliverables**:
- Complete preprocessing pipeline
- Kernel selection justification
- Hyperparameter optimization
- Interpretation and visualization

**Evaluation Criteria**: Accuracy, interpretability, proper methodology

**Hints**: Start with scaling. Grid search C and gamma. Visualize if 2D possible.

**Skills**: End-to-end SVM project

---

### B21: Comparing SVM Implementations
**Domain**: Practical | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Compare sklearn SVC, LinearSVC, SGDClassifier with hinge loss, and libsvm-based implementations. Understand performance and feature differences.

**Expected Deliverables**:
- API and feature comparison
- Speed benchmarks
- When to use each

**Test Cases**:
1. Same results across implementations
2. Training time comparison
3. Large-scale performance

**Hints**: LinearSVC is faster LibLinear-based. SGDClassifier scales to huge datasets.

**Skills**: Library comparison, practical SVM

---

### B22: SVM Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Both

**Problem**: Comprehensive SVM analysis: compare with other algorithms, implement from scratch, demonstrate kernel trick power, and create production pipeline.

**Dataset**: Complex multi-class problem

**Expected Deliverables**:
- From-scratch linear SVM
- Kernel comparison (linear, poly, RBF)
- Optimal hyperparameters
- Comparison with trees and k-NN
- Production-ready pipeline

**Evaluation Criteria**: Complete understanding, proper methodology, clean implementation

**Hints**: Show when kernels are necessary. Document support vector analysis.

**Skills**: Complete SVM mastery

---

## Section C: Naive Bayes & Probabilistic Models (C1-C22)

### C1: Gaussian Naive Bayes from Scratch
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: From Scratch

**Problem**: Implement Gaussian Naive Bayes assuming features are normally distributed within each class. This is one of the simplest yet effective classifiers.

**Mathematical Foundation**:
- Bayes: P(y|x) ∝ P(x|y)P(y)
- Naive assumption: P(x|y) = Π P(xⱼ|y)
- Gaussian: P(xⱼ|y) = N(μⱼᵧ, σⱼᵧ)

**Dataset**: Iris or synthetic Gaussian data

**Expected Deliverables**:
- GaussianNB class with fit() and predict()
- Per-class mean and variance estimation
- Posterior probability calculation

**Test Cases**:
1. Match sklearn GaussianNB
2. Probability outputs
3. Handle classes with different variances

**Hints**: Store mean and variance per class per feature. Use log probabilities to avoid underflow.

**Skills**: Naive Bayes fundamentals, probability

---

### C2: Multinomial Naive Bayes from Scratch
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: From Scratch

**Problem**: Implement Multinomial Naive Bayes for count data like text classification. Each feature represents counts (e.g., word frequencies).

**Mathematical Foundation**:
- P(xⱼ|y) = (count of j in class y) / (total count in class y)
- Laplace smoothing: add 1 to counts

**Dataset**: Text data with word counts

**Expected Deliverables**:
- MultinomialNB implementation
- Laplace smoothing handling
- Application to text classification

**Test Cases**:
1. Text classification with counts
2. Effect of smoothing parameter
3. Match sklearn MultinomialNB

**Hints**: Laplace smoothing prevents zero probabilities for unseen words.

**Skills**: Multinomial NB, text classification

---

### C3: Bernoulli Naive Bayes
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Implement Bernoulli Naive Bayes for binary features (presence/absence). Understand when Bernoulli is preferred over Multinomial for text.

**Mathematical Foundation**:
- P(xⱼ|y) = pⱼᵧ if xⱼ=1, (1-pⱼᵧ) if xⱼ=0
- Explicitly models absence

**Expected Deliverables**:
- BernoulliNB implementation
- Comparison with MultinomialNB on text
- When to use each

**Test Cases**:
1. Binary feature classification
2. Text with binary presence/absence
3. Short vs long document performance

**Hints**: Bernoulli considers absence of words; Multinomial doesn't. Better for short texts.

**Skills**: Bernoulli NB, binary features

---

### C4: Categorical Naive Bayes
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Apply Categorical Naive Bayes for datasets with discrete categorical features that aren't counts. Understand encoding and probability estimation.

**Expected Deliverables**:
- CategoricalNB usage
- Handling of categorical features
- Comparison with encoding + GaussianNB

**Test Cases**:
1. Pure categorical dataset
2. Effect of smoothing
3. Compare with one-hot + other NB

**Hints**: Use sklearn CategoricalNB. Features must be category encodings.

**Skills**: Categorical NB, discrete features

---

### C5: Complement Naive Bayes
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply Complement Naive Bayes designed for imbalanced datasets. It uses complement of each class to estimate parameters, reducing bias.

**Expected Deliverables**:
- ComplementNB application
- Comparison with MultinomialNB on imbalanced data
- When CNB outperforms

**Test Cases**:
1. Imbalanced text classification
2. Performance improvement over standard NB
3. Mathematical intuition

**Hints**: Use sklearn ComplementNB. Particularly effective for imbalanced text data.

**Skills**: Complement NB, imbalanced classification

---

### C6: Naive Bayes Assumptions Analysis
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Analyze the naive independence assumption and understand why Naive Bayes works well despite this assumption being rarely true in practice.

**Expected Deliverables**:
- Demonstration of violated independence
- Why NB still works (calibration vs accuracy)
- When assumption violation hurts

**Test Cases**:
1. Show correlated features
2. Accuracy remains good
3. Probabilities may be uncalibrated

**Hints**: NB is often well-calibrated for classification despite poor probability estimates.

**Skills**: Understanding NB limitations

---

### C7: Log Probability for Numerical Stability
**Domain**: Implementation | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: From Scratch

**Problem**: Implement log-probability computation to avoid numerical underflow when multiplying many small probabilities. Essential for any probabilistic model.

**Mathematical Foundation**:
- log(ΠPᵢ) = Σlog(Pᵢ)
- log-sum-exp trick for normalization

**Expected Deliverables**:
- Log-probability Naive Bayes
- Comparison of stable vs unstable
- Log-sum-exp implementation

**Test Cases**:
1. Many features cause underflow
2. Log version remains stable
3. Same predictions, stable computation

**Hints**: Always work in log space for probability products.

**Skills**: Numerical stability, log probabilities

---

### C8: Smoothing Techniques
**Domain**: Theory | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Implement and compare smoothing techniques: Laplace (add-1), Lidstone (add-alpha), and understand their effect on probability estimates.

**Mathematical Foundation**:
- Laplace: (count + 1) / (total + V)
- Lidstone: (count + α) / (total + αV)

**Expected Deliverables**:
- Both smoothing methods
- Effect of alpha parameter
- Optimal alpha selection

**Test Cases**:
1. Zero count handling
2. Alpha effect on estimates
3. Cross-validation for alpha

**Hints**: Use `alpha` parameter in sklearn. Typical values 0.01 to 1.0.

**Skills**: Smoothing, hyperparameter effect

---

### C9: Naive Bayes for Text Classification
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Build complete text classification pipeline with Naive Bayes: preprocessing, vectorization, training, and evaluation. NB is baseline for text.

**Dataset**: 20 Newsgroups, IMDB Reviews, or SMS Spam

**Expected Deliverables**:
- Complete text classification pipeline
- TF-IDF vs Count comparison
- Multi-class text classification

**Test Cases**:
1. Spam classification
2. Topic classification
3. Sentiment analysis

**Hints**: Pipeline: text → vectorizer → NB. Compare count vs TF-IDF.

**Skills**: Text classification, NLP pipelines

---

### C10: Naive Bayes vs Logistic Regression
**Domain**: Comparison | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Compare Naive Bayes (generative) with Logistic Regression (discriminative). Understand theoretical differences and practical performance.

**Expected Deliverables**:
- Generative vs discriminative explanation
- Performance comparison on various data
- When each is preferred

**Test Cases**:
1. Small data: NB often better
2. Large data: LR often better
3. Calibration comparison

**Hints**: NB trains faster, needs less data. LR usually more accurate with enough data.

**Skills**: Generative vs discriminative, model comparison

---

### C11: Prior Probability Effects
**Domain**: Theory | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Understand the effect of prior probabilities on Naive Bayes predictions. Explore class imbalance handling and prior adjustment.

**Mathematical Foundation**:
- P(y|x) ∝ P(x|y)P(y)
- Priors affect decision boundary

**Expected Deliverables**:
- Prior estimation methods
- Manual prior adjustment
- Effect on imbalanced data

**Test Cases**:
1. Balanced vs class-proportion priors
2. Uniform priors effect
3. Custom priors for domain knowledge

**Hints**: Use `priors` parameter in GaussianNB. Priors handle class imbalance.

**Skills**: Prior probabilities, Bayesian reasoning

---

### C12: Feature Independence Testing
**Domain**: Analysis | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Test feature independence assumption using correlation analysis, mutual information, and chi-square tests. Understand when NB will struggle.

**Expected Deliverables**:
- Correlation matrix analysis
- Mutual information between features
- Impact on NB performance

**Test Cases**:
1. Identify correlated features
2. NB performance with correlated features
3. Feature selection for NB

**Hints**: High correlation → violated assumption. May still work but probabilities unreliable.

**Skills**: Independence testing, assumption validation

---

### C13: Naive Bayes Feature Importance
**Domain**: Interpretation | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Extract and interpret feature importance from Naive Bayes models. Understand likelihood ratios and their interpretation.

**Expected Deliverables**:
- Feature log-likelihood extraction
- Most predictive features per class
- Likelihood ratio interpretation

**Test Cases**:
1. Top words for spam vs ham
2. Features distinguishing classes
3. Visualization of importances

**Hints**: Compare log P(feature|class=1) vs log P(feature|class=0).

**Skills**: NB interpretation, feature analysis

---

### C14: Semi-Supervised Naive Bayes
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries/Custom

**Problem**: Apply Naive Bayes in semi-supervised setting using EM algorithm. Use unlabeled data to improve estimates when labeled data is scarce.

**Expected Deliverables**:
- EM for semi-supervised NB
- Comparison with supervised-only
- When semi-supervised helps

**Test Cases**:
1. 10% labeled, 90% unlabeled
2. Improvement over labeled-only
3. When unlabeled data hurts

**Hints**: EM alternates E-step (predict labels) and M-step (update parameters).

**Skills**: Semi-supervised learning, EM algorithm

---

### C15: Incremental/Online Naive Bayes
**Domain**: Advanced | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Use partial_fit for incremental learning when data doesn't fit in memory or arrives as a stream. Update model with batches.

**Expected Deliverables**:
- Streaming NB implementation
- Compare with batch training
- Handling class distribution changes

**Test Cases**:
1. Train on streaming data
2. Same result as batch (approximately)
3. Concept drift handling

**Hints**: Use `partial_fit` method. Specify classes upfront.

**Skills**: Online learning, streaming ML

---

### C16: Bayesian Networks Introduction
**Domain**: Probabilistic Models | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Understand Bayesian Networks as generalization of Naive Bayes that allows specified dependencies. Build simple BN for structured inference.

**Expected Deliverables**:
- BN concept explanation
- Simple BN construction
- Comparison with Naive Bayes

**Test Cases**:
1. Model with specified dependencies
2. Inference on BN
3. When BN outperforms NB

**Hints**: Use pgmpy or pomegranate libraries. BN generalizes conditional independence.

**Skills**: Bayesian Networks, probabilistic graphical models

---

### C17: Naive Bayes Probability Calibration
**Domain**: Advanced | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Calibrate Naive Bayes probability outputs which are often extreme (near 0 or 1). Apply calibration methods for reliable probabilities.

**Expected Deliverables**:
- Reliability diagram before calibration
- Platt/Isotonic calibration
- Improvement in calibration

**Test Cases**:
1. Show extreme probability outputs
2. Calibration improvement
3. When calibration matters

**Hints**: NB probabilities are often overconfident. Use CalibratedClassifierCV.

**Skills**: Probability calibration, reliable predictions

---

### C18: Mixed Feature Types
**Domain**: Practical | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Handle datasets with mixed feature types (continuous, categorical, binary) by combining appropriate Naive Bayes variants or preprocessing.

**Expected Deliverables**:
- Strategy for mixed features
- Combined NB approach
- Preprocessing alternatives

**Test Cases**:
1. Continuous + categorical data
2. Compare approaches
3. Best practice guidelines

**Hints**: Discretize continuous for CategoricalNB, or use separate NB models and combine.

**Skills**: Mixed data handling, practical NB

---

### C19: Naive Bayes for Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Use Naive Bayes probability outputs for anomaly detection. Low probability under normal class indicates anomaly.

**Expected Deliverables**:
- Probability-based anomaly scoring
- Threshold selection
- Comparison with other methods

**Test Cases**:
1. Score outliers as low probability
2. ROC for anomaly detection
3. Compare with One-Class SVM

**Hints**: Train on normal class, use predict_proba for anomaly scores.

**Skills**: Anomaly detection, probability as score

---

### C20: Naive Bayes Real-World Project
**Domain**: End-to-End | **Difficulty**: ★★★☆☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Complete Naive Bayes project for text classification with preprocessing, variant comparison, tuning, and interpretation.

**Dataset**: Product Reviews, News Categorization, or Custom

**Expected Deliverables**:
- Complete text pipeline
- NB variant comparison
- Feature analysis
- Business insights from features

**Evaluation Criteria**: Accuracy, interpretability, practical value

**Hints**: Focus on interpretability. Analyze most predictive words.

**Skills**: End-to-end NB project

---

### C21: Comparing Probabilistic Models
**Domain**: Comparison | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Compare Naive Bayes with other probabilistic approaches: LDA, QDA, Logistic Regression. Understand model assumptions and tradeoffs.

**Expected Deliverables**:
- Model assumption comparison
- Performance on various data types
- Decision boundary comparison

**Test Cases**:
1. NB vs LDA on Gaussian data
2. NB vs LR on text
3. Calibration comparison

**Hints**: LDA/QDA have different covariance assumptions than GaussianNB.

**Skills**: Probabilistic model comparison

---

### C22: Naive Bayes Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Both

**Problem**: Comprehensive Naive Bayes analysis: implement from scratch, compare variants, analyze assumptions, and create interpretable production model.

**Dataset**: Multi-domain comparison

**Expected Deliverables**:
- From-scratch implementation
- All variants comparison
- Assumption analysis
- Calibration assessment
- Production pipeline
- Interpretation report

**Evaluation Criteria**: Complete understanding, proper analysis, production quality

**Hints**: Show when NB excels (text) and struggles (correlated features).

**Skills**: Complete NB mastery

---

## Section D: Ensemble Methods Basics (D1-D25)

### D1: Bootstrap Aggregating (Bagging) from Scratch
**Domain**: Ensemble | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: From Scratch

**Problem**: Implement bagging from scratch: create multiple bootstrap samples, train base models on each, and aggregate predictions by voting (classification) or averaging (regression).

**Mathematical Foundation**:
- Bootstrap: sample n items with replacement
- Variance reduction: Var(avg) = Var(single)/n (for uncorrelated)

**Expected Deliverables**:
- BaggingClassifier from scratch
- Bootstrap sampling implementation
- Aggregation methods

**Test Cases**:
1. Match sklearn BaggingClassifier
2. Show variance reduction
3. Out-of-bag samples identification

**Hints**: Each bootstrap sample has ~63.2% unique samples.

**Skills**: Bagging fundamentals, variance reduction

---

### D2: Random Forest from Scratch
**Domain**: Ensemble | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: From Scratch

**Problem**: Implement Random Forest: bagging + random feature subsets at each split. This double randomization reduces correlation between trees, maximizing variance reduction.

**Mathematical Foundation**:
- Feature subset size: sqrt(m) for classification, m/3 for regression
- Correlation reduction → better variance reduction

**Expected Deliverables**:
- RandomForestClassifier from scratch
- Random feature selection at splits
- Feature importance calculation

**Test Cases**:
1. Compare with sklearn RandomForestClassifier
2. Effect of max_features
3. Improvement over single tree

**Hints**: Max_features is the key difference from bagging.

**Skills**: Random Forest internals, feature randomization

---

### D3: Out-of-Bag (OOB) Evaluation
**Domain**: Ensemble | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use out-of-bag samples for model evaluation without separate validation set. Each sample is OOB for ~36.8% of trees, providing free validation.

**Expected Deliverables**:
- OOB score calculation
- Comparison with cross-validation
- When OOB is sufficient

**Test Cases**:
1. Enable oob_score=True
2. Compare OOB vs CV estimates
3. OOB for hyperparameter selection

**Hints**: Use `oob_score=True`. OOB is a reasonable estimate but slightly pessimistic.

**Skills**: OOB evaluation, model validation

---

### D4: Random Forest Feature Importance
**Domain**: Interpretation | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Extract and interpret feature importance from Random Forest using impurity decrease and permutation importance. Understand when each is appropriate.

**Expected Deliverables**:
- Impurity-based importance
- Permutation importance comparison
- Importance visualization

**Test Cases**:
1. Rank features by importance
2. Compare impurity vs permutation
3. Bias in impurity importance

**Hints**: Impurity importance is biased toward high-cardinality. Use permutation for reliable ranking.

**Skills**: Feature importance, model interpretation

---

### D5: Random Forest Hyperparameter Tuning
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Tune key Random Forest hyperparameters: n_estimators, max_features, max_depth, min_samples_split. Understand which matter most.

**Expected Deliverables**:
- Hyperparameter importance analysis
- Grid/Random search implementation
- Learning curves for n_estimators

**Test Cases**:
1. n_estimators effect (diminishing returns)
2. max_features optimization
3. Depth vs minimum samples

**Hints**: More trees rarely hurts. Max_features and max_depth are most important.

**Skills**: RF tuning, hyperparameter importance

---

### D6: Gradient Boosting Concept
**Domain**: Ensemble | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Conceptual + Libraries

**Problem**: Understand gradient boosting: sequentially fit trees to residuals (negative gradients). Each tree corrects errors of the ensemble so far.

**Mathematical Foundation**:
- Fit tree to negative gradient of loss
- F_m(x) = F_{m-1}(x) + η × h_m(x)
- Learning rate η controls contribution

**Expected Deliverables**:
- GB algorithm explanation
- Manual residual fitting demonstration
- Comparison with bagging

**Test Cases**:
1. Show residual reduction per iteration
2. Effect of learning rate
3. Comparison with Random Forest

**Hints**: Lower learning rate + more trees = better generalization usually.

**Skills**: Gradient boosting concept, sequential learning

---

### D7: Gradient Boosting for Regression
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply gradient boosting regression for continuous targets. Tune n_estimators, learning_rate, and max_depth for optimal performance.

**Expected Deliverables**:
- GradientBoostingRegressor usage
- Learning curve (error vs n_estimators)
- Optimal hyperparameters

**Test Cases**:
1. Fit complex non-linear function
2. Compare with Random Forest regression
3. Find optimal stopping

**Hints**: Watch for overfitting with many estimators. Use early stopping.

**Skills**: GB regression, hyperparameter tuning

---

### D8: Gradient Boosting for Classification
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply gradient boosting classification with log-loss. Understand how boosting optimizes this probabilistic objective.

**Expected Deliverables**:
- GradientBoostingClassifier usage
- Probability outputs
- Multi-class extension

**Test Cases**:
1. Binary classification
2. Multi-class classification
3. Probability calibration

**Hints**: Uses log-loss (deviance) by default. Probabilities are usually well-calibrated.

**Skills**: GB classification, probabilistic boosting

---

### D9: AdaBoost Algorithm
**Domain**: Ensemble | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Both

**Problem**: Implement AdaBoost: reweight samples to focus on previously misclassified examples. Weak learners are combined with weighted voting.

**Mathematical Foundation**:
- Sample weights increased for misclassified
- Classifier weight α_t = 0.5 × log((1-ε)/ε)
- Final: sign(Σ α_t × h_t(x))

**Expected Deliverables**:
- AdaBoost from scratch (simplified)
- Sample weight evolution visualization
- Comparison with sklearn

**Test Cases**:
1. Weight increase for hard examples
2. Combined classifier performance
3. Sensitivity to outliers

**Hints**: AdaBoost is sensitive to noisy data and outliers.

**Skills**: AdaBoost internals, sample weighting

---

### D10: XGBoost Introduction
**Domain**: Ensemble | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Use XGBoost library for gradient boosting with regularization, handling missing values, and parallel training. Understand key improvements over sklearn GB.

**Expected Deliverables**:
- XGBoost installation and usage
- Regularization parameters (lambda, alpha)
- Missing value handling

**Test Cases**:
1. Compare XGBoost vs sklearn GB accuracy/speed
2. Effect of regularization
3. Native missing value handling

**Hints**: XGBoost adds L1/L2 regularization to tree structure. Faster than sklearn.

**Skills**: XGBoost basics, regularized boosting

---

### D11: LightGBM Introduction
**Domain**: Ensemble | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Use LightGBM for faster gradient boosting with leaf-wise growth and histogram-based splitting. Ideal for large datasets.

**Expected Deliverables**:
- LightGBM installation and usage
- Leaf-wise vs level-wise comparison
- Categorical feature native handling

**Test Cases**:
1. Speed comparison with XGBoost
2. Categorical feature handling
3. Large dataset performance

**Hints**: LightGBM grows leaf-wise (can overfit more but faster).

**Skills**: LightGBM basics, histogram-based methods

---

### D12: CatBoost Introduction
**Domain**: Ensemble | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Use CatBoost for gradient boosting with native categorical feature handling using ordered target encoding.

**Expected Deliverables**:
- CatBoost usage
- Categorical feature handling
- Comparison with other boosting libraries

**Test Cases**:
1. Compare with one-hot + XGBoost
2. Handle many categorical features
3. Training speed comparison

**Hints**: CatBoost handles categoricals without preprocessing. Often best out-of-box.

**Skills**: CatBoost, categorical handling

---

### D13: Comparing Boosting Libraries
**Domain**: Comparison | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Compare XGBoost, LightGBM, CatBoost, and sklearn GradientBoosting on multiple datasets. Create selection guidelines.

**Expected Deliverables**:
- Accuracy comparison
- Training time comparison
- Feature support matrix

**Test Cases**:
1. Performance on numeric data
2. Performance on categorical data
3. Large-scale performance

**Hints**: All perform similarly; CatBoost for categoricals, LightGBM for speed.

**Skills**: Library comparison, practical selection

---

### D14: Early Stopping in Boosting
**Domain**: Optimization | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Implement early stopping to prevent overfitting and save computation. Stop when validation performance stops improving.

**Expected Deliverables**:
- Early stopping implementation
- Choosing patience/rounds
- Comparison with fixed n_estimators

**Test Cases**:
1. Detect optimal stopping point
2. Effect of patience parameter
3. Generalization improvement

**Hints**: Use `early_stopping_rounds` in XGBoost/LightGBM.

**Skills**: Early stopping, overfitting prevention

---

### D15: Learning Rate and Number of Trees Tradeoff
**Domain**: Theory | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Understand the learning rate and n_estimators tradeoff. Lower learning rate with more trees often gives better generalization.

**Expected Deliverables**:
- Learning rate effect demonstration
- Optimal combination finding
- Computational cost analysis

**Test Cases**:
1. η=0.1 vs η=0.01 with more trees
2. Show accuracy vs computation tradeoff
3. Diminishing returns analysis

**Hints**: Lower learning rate = more trees needed but often better. Use early stopping.

**Skills**: Learning rate tuning, boosting tradeoffs

---

### D16: Stacking Ensemble
**Domain**: Ensemble | **Difficulty**: ★★★★☆ | **Time**: 65 min
**Implementation**: Libraries

**Problem**: Implement stacking: train multiple base models, then train a meta-model on their predictions. This can capture complementary information.

**Mathematical Foundation**:
- Level 0: base models
- Level 1: meta-model on base predictions
- Use CV predictions to avoid leakage

**Expected Deliverables**:
- StackingClassifier/Regressor usage
- Cross-validated stacking
- Meta-model selection

**Test Cases**:
1. Stack diverse models
2. Compare with single best model
3. Avoid overfitting through CV

**Hints**: Use diverse base models. Simple meta-model often best.

**Skills**: Stacking, meta-learning

---

### D17: Voting Ensemble
**Domain**: Ensemble | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Combine multiple models using voting (hard or soft). Simple but effective way to combine diverse classifiers.

**Expected Deliverables**:
- VotingClassifier (hard and soft)
- Weighted voting
- VotingRegressor for regression

**Test Cases**:
1. Hard voting (majority)
2. Soft voting (average probabilities)
3. Weighted voting improvement

**Hints**: Soft voting usually better. Weights can be learned.

**Skills**: Voting ensembles, simple combining

---

### D18: Blending vs Stacking
**Domain**: Ensemble | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Compare blending (holdout-based) with stacking (CV-based). Understand tradeoffs in simplicity vs data efficiency.

**Expected Deliverables**:
- Blending implementation
- Comparison with stacking
- When each is preferred

**Test Cases**:
1. Blending on holdout set
2. Stacking with cross-validation
3. Performance comparison

**Hints**: Blending is simpler but wastes data. Stacking is more complex but uses all data.

**Skills**: Blending, ensemble comparison

---

### D19: Ensemble Diversity
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Understand why diverse base models lead to better ensembles. Measure diversity and correlation between models.

**Expected Deliverables**:
- Diversity measures
- Correlation between model predictions
- Effect of diversity on ensemble performance

**Test Cases**:
1. Ensemble of similar models vs diverse
2. Measure prediction correlation
3. Diversity-accuracy tradeoff

**Hints**: Diverse models make different errors. Maximum diversity doesn't always help.

**Skills**: Ensemble theory, diversity

---

### D20: Handling Imbalanced Data with Ensembles
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply specialized ensemble techniques for imbalanced data: BalancedRandomForest, EasyEnsemble, RUSBoost.

**Expected Deliverables**:
- BalancedRandomForest usage
- Comparison with standard RF on imbalanced data
- When each method is preferred

**Test Cases**:
1. Imbalanced classification improvement
2. Compare different techniques
3. Threshold optimization

**Hints**: Use `imblearn` for balanced ensembles.

**Skills**: Imbalanced ensembles

---

### D21: Ensemble for Uncertainty Estimation
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Use ensemble disagreement for uncertainty estimation. When trees disagree, prediction is uncertain.

**Expected Deliverables**:
- Prediction variance calculation
- Confidence estimation
- Uncertainty visualization

**Test Cases**:
1. High uncertainty at decision boundaries
2. Low uncertainty in dense regions
3. Uncertainty calibration

**Hints**: For RF: look at individual tree predictions. High variance = uncertainty.

**Skills**: Uncertainty estimation, ensemble analysis

---

### D22: Ensemble Real-World Project
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete ensemble project comparing bagging, boosting, and stacking on real dataset. Find optimal ensemble strategy.

**Dataset**: Credit Default, Medical Diagnosis, or Kaggle Competition

**Expected Deliverables**:
- Multiple ensemble methods comparison
- Hyperparameter optimization
- Feature importance analysis
- Final ensemble selection

**Evaluation Criteria**: Best performance, interpretation, reproducibility

**Hints**: Often XGBoost/LightGBM wins. Try stacking top models.

**Skills**: End-to-end ensemble project

---

### D23: Ensemble for Regression
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply ensemble methods to regression: RandomForestRegressor, GradientBoostingRegressor, stacking. Compare with linear baselines.

**Expected Deliverables**:
- RF regression
- GB regression
- Stacking regressors

**Test Cases**:
1. Compare on non-linear data
2. Residual analysis
3. When ensembles help most

**Hints**: Ensembles excel for non-linear data with interactions.

**Skills**: Regression ensembles

---

### D24: Kaggle-Style Ensemble Strategies
**Domain**: Competition | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Learn competition ensemble strategies: diverse model generation, cross-validated predictions, weighted averaging, hill climbing.

**Expected Deliverables**:
- Multiple model generation
- Optimal weight finding
- Submission blending

**Test Cases**:
1. Generate diverse predictions
2. Find optimal weights via CV
3. Improvement from ensembling

**Hints**: Small improvements matter in competitions. Diverse models are key.

**Skills**: Competition strategies, advanced ensembling

---

### D25: Ensemble Methods Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Both

**Problem**: Comprehensive ensemble analysis: implement bagging from scratch, compare all major ensemble types, create production-ready ensemble pipeline.

**Expected Deliverables**:
- From-scratch implementations
- Comprehensive comparison
- Feature importance analysis
- Production pipeline
- Documentation

**Evaluation Criteria**: Understanding, methodology, production quality

**Hints**: Demonstrate understanding of when each method excels.

**Skills**: Complete ensemble mastery

---

## Section E: Clustering Algorithms (E1-E28)

### E1: K-Means from Scratch
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: From Scratch

**Problem**: Implement K-Means clustering: random initialization, assign points to nearest centroid, update centroids, iterate until convergence.

**Mathematical Foundation**:
- Minimize WCSS: Σᵢ Σⱼ ||xⱼ - μᵢ||²
- Assignment: arg min ||x - μₖ||
- Update: μₖ = (1/|Cₖ|) Σ xⱼ

**Expected Deliverables**:
- KMeans class with fit() and predict()
- Convergence tracking
- Cluster visualization

**Test Cases**:
1. Match sklearn KMeans results
2. Show convergence
3. Handle empty clusters

**Hints**: Initialize with K++ for better results. Track inertia decrease.

**Skills**: K-Means fundamentals, clustering basics

---

### E2: K-Means++ Initialization
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: From Scratch

**Problem**: Implement K-Means++ initialization that spreads initial centroids. This leads to faster convergence and better solutions.

**Mathematical Foundation**:
- First centroid: random
- Next: probability ∝ distance² to nearest centroid

**Expected Deliverables**:
- K-Means++ initialization
- Comparison with random initialization
- WCSS improvement

**Test Cases**:
1. Spread initial centroids
2. Faster convergence than random
3. Better final WCSS

**Hints**: Use distance-weighted probability. sklearn uses K-Means++ by default.

**Skills**: K-Means++, smart initialization

---

### E3: Elbow Method for K Selection
**Domain**: Clustering | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Use the elbow method to select optimal number of clusters. Plot WCSS vs K and find the "elbow" where improvement diminishes.

**Expected Deliverables**:
- WCSS vs K plot
- Elbow identification
- Limitations of method

**Test Cases**:
1. Clear elbow identification
2. Ambiguous cases handling
3. Comparison with true K

**Hints**: Elbow is subjective. Consider silhouette score as alternative.

**Skills**: Cluster number selection, model evaluation

---

### E4: Silhouette Score Analysis
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Calculate silhouette score measuring cluster quality: how similar points are to own cluster vs nearest cluster. Use for K selection.

**Mathematical Foundation**:
- a: mean intra-cluster distance
- b: mean nearest-cluster distance
- s = (b - a) / max(a, b)

**Expected Deliverables**:
- Silhouette score calculation
- Per-sample silhouette visualization
- K selection using silhouette

**Test Cases**:
1. Silhouette score for different K
2. Identify poorly clustered points
3. Compare with elbow method

**Hints**: Use `sklearn.metrics.silhouette_score` and `silhouette_samples`.

**Skills**: Silhouette analysis, cluster evaluation

---

### E5: K-Means Limitations and Solutions
**Domain**: Theory | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Understand K-Means limitations: spherical assumption, sensitivity to scale, initialization sensitivity, equal cluster sizes. Apply solutions.

**Expected Deliverables**:
- Demonstration of each limitation
- Solutions for each issue
- When K-Means fails badly

**Test Cases**:
1. Non-spherical clusters
2. Different cluster sizes
3. Different densities

**Hints**: K-Means assumes spherical, equal-size clusters. Other algorithms handle these cases.

**Skills**: K-Means limitations, algorithm selection

---

### E6: Hierarchical Clustering - Agglomerative
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Implement agglomerative (bottom-up) hierarchical clustering. Start with n clusters, merge closest pairs until reaching desired K or single cluster.

**Mathematical Foundation**:
- Linkage: single, complete, average, Ward
- Dendrogram shows merge history

**Expected Deliverables**:
- AgglomerativeClustering usage
- Dendrogram visualization
- Cutting at different levels

**Test Cases**:
1. Build dendrogram
2. Cut at different heights
3. Compare linkage methods

**Hints**: Ward linkage often works best. Dendogram helps choose K.

**Skills**: Hierarchical clustering, dendrogram analysis

---

### E7: Linkage Methods Comparison
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Compare linkage methods: single (chaining), complete (max), average, Ward (variance). Different linkages suit different cluster shapes.

**Expected Deliverables**:
- All linkage methods comparison
- Cluster shape effect
- Best practice guidelines

**Test Cases**:
1. Single linkage chaining effect
2. Complete linkage on elongated clusters
3. Ward on spherical clusters

**Hints**: Single can chain; complete creates compact clusters; Ward minimizes variance.

**Skills**: Linkage selection, clustering behavior

---

### E8: DBSCAN Clustering
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply DBSCAN density-based clustering that finds arbitrarily shaped clusters and marks low-density points as noise. No need to specify K.

**Mathematical Foundation**:
- Core points: ≥ min_samples within eps
- Border points: within eps of core point
- Noise: neither core nor border

**Expected Deliverables**:
- DBSCAN usage
- eps and min_samples selection
- Noise point identification

**Test Cases**:
1. Non-spherical cluster detection
2. Outlier detection
3. Varying density handling

**Hints**: Use k-distance graph to select eps. min_samples ≥ d+1 is common.

**Skills**: Density-based clustering, DBSCAN

---

### E9: HDBSCAN Clustering
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply HDBSCAN that doesn't require eps parameter and handles varying densities. Often the best choice for unknown cluster structure.

**Expected Deliverables**:
- HDBSCAN usage
- Comparison with DBSCAN
- Cluster probability extraction

**Test Cases**:
1. Automatic parameter selection
2. Varying density clusters
3. Outlier identification

**Hints**: HDBSCAN needs only min_cluster_size. Generally more robust than DBSCAN.

**Skills**: HDBSCAN, robust clustering

---

### E10: Gaussian Mixture Models
**Domain**: Clustering | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Apply Gaussian Mixture Models for soft clustering with probabilistic cluster assignments. Each cluster is a Gaussian, fit using EM algorithm.

**Mathematical Foundation**:
- Mixture: P(x) = Σ πₖ N(x|μₖ, Σₖ)
- Soft assignments: P(k|x)
- EM: E-step assigns, M-step updates

**Expected Deliverables**:
- GaussianMixture usage
- Soft cluster assignments
- Model selection (AIC, BIC)

**Test Cases**:
1. Soft assignments for overlapping clusters
2. Different covariance types
3. K selection using BIC

**Hints**: Use 'full' covariance for general clusters. Select K using BIC.

**Skills**: GMM, soft clustering, EM algorithm

---

### E11: Mini-Batch K-Means
**Domain**: Clustering | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Use Mini-Batch K-Means for large datasets. Approximates K-Means using mini-batches, trading some accuracy for speed.

**Expected Deliverables**:
- MiniBatchKMeans usage
- Speed comparison with K-Means
- Accuracy tradeoff

**Test Cases**:
1. Speed on large dataset
2. Accuracy comparison
3. Batch size effect

**Hints**: Use for large datasets (>10K samples). Similar results, much faster.

**Skills**: Scalable clustering

---

### E12: Spectral Clustering
**Domain**: Clustering | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply spectral clustering that uses eigenvalues of similarity matrix. Can find clusters that K-Means cannot (e.g., concentric circles).

**Mathematical Foundation**:
- Construct similarity graph
- Compute graph Laplacian
- Use eigenvectors for embedding
- K-Means on embedding

**Expected Deliverables**:
- SpectralClustering usage
- Concentric circles example
- Similarity graph construction

**Test Cases**:
1. Cluster moons dataset
2. Cluster concentric circles
3. Compare with K-Means

**Hints**: Works well for non-convex clusters. Computationally expensive.

**Skills**: Spectral methods, graph-based clustering

---

### E13: Mean Shift Clustering
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply Mean Shift clustering that finds modes of kernel density estimate. No need to specify K; bandwidth controls cluster size.

**Expected Deliverables**:
- MeanShift usage
- Bandwidth selection
- Mode finding demonstration

**Test Cases**:
1. Automatic K discovery
2. Bandwidth effect
3. Comparison with K-Means

**Hints**: Bandwidth is the key parameter. Estimate using sklearn function.

**Skills**: Mean Shift, mode finding

---

### E14: OPTICS Clustering
**Domain**: Clustering | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply OPTICS that creates an ordering of points based on density, from which clusters can be extracted at different density levels.

**Expected Deliverables**:
- OPTICS usage
- Reachability plot
- Cluster extraction at different levels

**Test Cases**:
1. Extract hierarchical clusters
2. Reachability plot interpretation
3. Comparison with DBSCAN

**Hints**: OPTICS creates ordering; clusters extracted from reachability plot.

**Skills**: OPTICS, hierarchical density clustering

---

### E15: Clustering Validation Metrics
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply external (when labels available) and internal validation metrics for clustering. Compare ARI, NMI, silhouette, Calinski-Harabasz, Davies-Bouldin.

**Expected Deliverables**:
- External metrics (ARI, NMI) when labels known
- Internal metrics (silhouette, CH, DB) without labels
- Metric selection guidelines

**Test Cases**:
1. ARI, NMI on labeled data
2. Internal metrics comparison
3. Correlation between metrics

**Hints**: ARI, NMI require ground truth. Silhouette, CH, DB don't.

**Skills**: Clustering evaluation, metrics

---

### E16: Clustering for Customer Segmentation
**Domain**: Application | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Apply clustering to segment customers based on behavior. Create interpretable segments with business value.

**Dataset**: Retail/E-commerce customer data

**Expected Deliverables**:
- Customer feature engineering
- Clustering with multiple algorithms
- Segment interpretation
- Business recommendations

**Test Cases**:
1. Identify distinct segments
2. Profile each segment
3. Actionable insights

**Hints**: Scale features. Try multiple algorithms. Focus on interpretability.

**Skills**: Business application, customer segmentation

---

### E17: Image Segmentation with Clustering
**Domain**: Computer Vision | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Use clustering for image segmentation: cluster pixels by color/position to create regions. Classic computer vision application.

**Expected Deliverables**:
- K-Means on image pixels
- Color quantization
- Region-based segmentation

**Test Cases**:
1. Reduce image colors (quantization)
2. Segment into regions
3. Effect of K on segmentation

**Hints**: Combine color and position features. Normalize appropriately.

**Skills**: Image clustering, segmentation

---

### E18: Clustering for Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Use clustering for anomaly detection: points far from cluster centers or in their own small clusters are anomalies.

**Expected Deliverables**:
- Distance-based anomaly scoring
- Small cluster detection
- Comparison with dedicated methods

**Test Cases**:
1. Detect outliers as far from centers
2. DBSCAN noise points as anomalies
3. Compare with Isolation Forest

**Hints**: K-Means distance to centroid, DBSCAN noise points, small GMM clusters.

**Skills**: Clustering-based anomaly detection

---

### E19: Text Clustering
**Domain**: NLP | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Cluster documents or texts using TF-IDF vectorization and appropriate clustering algorithms. Topic discovery without labels.

**Dataset**: News articles or document collection

**Expected Deliverables**:
- TF-IDF vectorization
- Document clustering
- Cluster topic interpretation

**Test Cases**:
1. Cluster news articles
2. Identify topic per cluster
3. Top terms per cluster

**Hints**: TF-IDF or embeddings as features. Try K-Means and hierarchical.

**Skills**: Text clustering, topic discovery

---

### E20: Semi-Supervised Clustering
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Incorporate partial labels or constraints (must-link, cannot-link) into clustering. Combine supervision with unsupervised discovery.

**Expected Deliverables**:
- Constraint-based clustering
- Label propagation approach
- Improvement from partial labels

**Test Cases**:
1. Must-link constraints
2. Cannot-link constraints
3. Improvement over unsupervised

**Hints**: Use label propagation or constrained K-Means variants.

**Skills**: Semi-supervised clustering, constrained clustering

---

### E21: Clustering High-Dimensional Data
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Handle clustering challenges in high dimensions: curse of dimensionality, all points equidistant. Apply dimensionality reduction before clustering.

**Expected Deliverables**:
- Demonstrate distance concentration
- PCA/UMAP before clustering
- Subspace clustering concepts

**Test Cases**:
1. Clustering fails in high-d
2. PCA + K-Means improvement
3. UMAP + clustering

**Hints**: Always reduce dimensionality for high-d clustering. UMAP preserves local structure.

**Skills**: High-dimensional clustering, dimensionality reduction

---

### E22: Time Series Clustering
**Domain**: Time Series | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Cluster time series using appropriate distance metrics (DTW) or feature extraction. Find similar patterns in temporal data.

**Expected Deliverables**:
- DTW distance metric
- Feature-based clustering
- Shape-based similarity

**Test Cases**:
1. Cluster similar time series shapes
2. Compare DTW vs Euclidean
3. tslearn library usage

**Hints**: Use tslearn library. DTW handles time warping.

**Skills**: Time series clustering, DTW

---

### E23: Consensus Clustering
**Domain**: Advanced | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries/Custom

**Problem**: Combine multiple clustering results to get robust final clusters. Ensemble clustering that reduces sensitivity to parameter choices.

**Expected Deliverables**:
- Multiple clustering runs
- Consensus matrix construction
- Final cluster extraction

**Test Cases**:
1. Combine K-Means with different K
2. Combine different algorithms
3. Stability assessment

**Hints**: Run clustering many times, build co-association matrix, cluster that.

**Skills**: Ensemble clustering, robust clustering

---

### E24: Online/Streaming Clustering
**Domain**: Advanced | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Cluster streaming data that doesn't fit in memory or arrives continuously. Update clusters incrementally.

**Expected Deliverables**:
- Mini-batch approach
- Birch algorithm
- Online GMM concepts

**Test Cases**:
1. Cluster data stream
2. Handle concept drift
3. Memory efficiency

**Hints**: Use Birch for streaming. Incremental updates without full recomputation.

**Skills**: Streaming clustering, online algorithms

---

### E25: Cluster Interpretation and Profiling
**Domain**: Interpretation | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Interpret clusters by profiling: compare means, identify distinguishing features, create human-readable characterizations.

**Expected Deliverables**:
- Cluster means comparison
- Statistical tests for differences
- Visualization (radar, parallel coordinates)
- Business-friendly descriptions

**Test Cases**:
1. Profile each cluster
2. Identify key differentiators
3. Create cluster names

**Hints**: Compare cluster means to global mean. Use statistical tests.

**Skills**: Cluster interpretation, profiling

---

### E26: Comparing Clustering Algorithms
**Domain**: Comparison | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Systematically compare clustering algorithms on diverse datasets. Create selection guidelines based on data characteristics.

**Expected Deliverables**:
- Multiple algorithms on multiple datasets
- Performance comparison
- Selection decision tree

**Test Cases**:
1. Spherical clusters → K-Means
2. Arbitrary shapes → DBSCAN
3. Gaussian overlapping → GMM

**Hints**: No single best algorithm. matches their strengths to data characteristics.

**Skills**: Algorithm comparison, selection

---

### E27: Clustering Real-World Project
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete clustering project: preprocessing, algorithm selection, validation, interpretation, and business application.

**Dataset**: Customer, Product, or Market data

**Expected Deliverables**:
- Complete preprocessing
- Multiple algorithm comparison
- Optimal K selection
- Cluster profiling
- Business recommendations

**Hints**: Focus on interpretation. Clusters are only useful if actionable.

**Skills**: End-to-end clustering project

---

### E28: Clustering Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Both

**Problem**: Comprehensive clustering analysis: implement K-Means from scratch, compare all major algorithms, create production clustering pipeline.

**Expected Deliverables**:
- From-scratch implementations
- Algorithm comparison
- Validation metrics analysis
- Interpretation framework
- Production pipeline

**Evaluation Criteria**: Understanding, methodology, practical value

**Hints**: Demonstrate when each algorithm is appropriate.

**Skills**: Complete clustering mastery

---

## Section F: Dimensionality Reduction (F1-F20)

### F1: PCA from Scratch
**Domain**: Dimensionality Reduction | **Difficulty**: ★★★★☆ | **Time**: 75 min
**Implementation**: From Scratch

**Problem**: Implement PCA from scratch: center data, compute covariance matrix, find eigenvectors, project onto top-k principal components.

**Mathematical Foundation**:
- Center: X̄ = X - mean(X)
- Covariance: C = X̄ᵀX̄ / (n-1)
- Eigendecomposition: C = VΛVᵀ
- Project: Z = X̄V_k

**Expected Deliverables**:
- PCA class with fit() and transform()
- Explained variance calculation
- Reconstruction error

**Test Cases**:
1. Match sklearn PCA results
2. Verify orthogonality of components
3. Reconstruction from components

**Hints**: Use SVD for numerical stability. Eigenvectors of covariance = right singular vectors.

**Skills**: PCA fundamentals, linear algebra

---

### F2: Explained Variance Analysis
**Domain**: Dimensionality Reduction | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Analyze explained variance to choose number of components. Use cumulative explained variance ratio to find minimum dimensions for target information retention.

**Expected Deliverables**:
- Explained variance ratio plot
- Cumulative variance plot
- Components for 95% variance

**Test Cases**:
1. Find min components for 95% variance
2. Scree plot interpretation
3. Compare with intrinsic dimensionality

**Hints**: Plot cumulative variance. Find elbow or target threshold.

**Skills**: Variance analysis, component selection

---

### F3: PCA for Visualization
**Domain**: Visualization | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Use PCA to reduce high-dimensional data to 2D or 3D for visualization. Understand limitations of linear projection.

**Expected Deliverables**:
- 2D PCA visualization
- 3D PCA visualization
- Color by class labels

**Test Cases**:
1. Visualize high-d dataset
2. Show separation of classes
3. Interpret component axes

**Hints**: Color points by labels. First two components capture most variance but may not be most discriminative.

**Skills**: PCA visualization, exploration

---

### F4: PCA for Preprocessing
**Domain**: Preprocessing | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use PCA for preprocessing: noise reduction, decorrelation, and dimensionality reduction before other algorithms.

**Expected Deliverables**:
- PCA + classifier pipeline
- Optimal component selection via CV
- Performance comparison

**Test Cases**:
1. Noise reduction effect
2. Decorrelation demonstration
3. Speedup from dimensionality reduction

**Hints**: Use truncated PCA (fewer components than features) for regularization effect.

**Skills**: PCA preprocessing, noise reduction

---

### F5: Kernel PCA
**Domain**: Dimensionality Reduction | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply kernel PCA for non-linear dimensionality reduction. Project to non-linear manifold using kernel trick.

**Mathematical Foundation**:
- Apply kernel trick to PCA
- Eigendecomposition on kernel matrix
- RBF kernel most common

**Expected Deliverables**:
- KernelPCA with different kernels
- Non-linear pattern visualization
- Comparison with linear PCA

**Test Cases**:
1. Swiss roll unwrapping
2. Kernel selection effect
3. Compare with linear PCA

**Hints**: RBF kernel most versatile. Grid search gamma.

**Skills**: Kernel methods, non-linear reduction

---

### F6: t-SNE for Visualization
**Domain**: Visualization | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply t-SNE for high-quality 2D/3D visualization that preserves local structure. Understand perplexity and interpret results correctly.

**Mathematical Foundation**:
- Minimize KL divergence between high-d and low-d similarities
- Student-t distribution in low-d (heavier tails)

**Expected Deliverables**:
- t-SNE visualization
- Perplexity effect analysis
- Common misinterpretations

**Test Cases**:
1. Visualize MNIST digits
2. Effect of perplexity
3. Run multiple times (stochastic)

**Hints**: t-SNE distances don't mean anything. Cluster sizes don't mean anything. Only structure matters.

**Skills**: t-SNE, visualization best practices

---

### F7: UMAP for Visualization
**Domain**: Visualization | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply UMAP as faster alternative to t-SNE that better preserves global structure. Often the best choice for visualization.

**Expected Deliverables**:
- UMAP visualization
- n_neighbors and min_dist effects
- Comparison with t-SNE

**Test Cases**:
1. Faster than t-SNE
2. Better global structure
3. Hyperparameter effects

**Hints**: UMAP is usually better than t-SNE: faster, better global structure, more parameters.

**Skills**: UMAP, modern visualization

---

### F8: LDA for Dimensionality Reduction
**Domain**: Supervised Reduction | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply Linear Discriminant Analysis as supervised dimensionality reduction. Maximize class separation while reducing dimensions.

**Mathematical Foundation**:
- Maximize between-class scatter / within-class scatter
- At most (n_classes - 1) components

**Expected Deliverables**:
- LDA for dimensionality reduction
- Comparison with PCA
- Classification after LDA

**Test Cases**:
1. LDA reduces to n_classes-1 dimensions
2. Compare with PCA for classification
3. LDA + classifier pipeline

**Hints**: LDA is supervised; uses labels. Better for classification than PCA often.

**Skills**: LDA, supervised reduction

---

### F9: Factor Analysis
**Domain**: Dimensionality Reduction | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply Factor Analysis to discover latent factors explaining correlations. Generative model unlike PCA.

**Mathematical Foundation**:
- Model: X = Wh + μ + ε
- Latent factors h explain correlations

**Expected Deliverables**:
- FactorAnalysis fitting
- Loading interpretation
- Comparison with PCA

**Test Cases**:
1. Find latent factors
2. Interpret loadings
3. Model selection (n_components)

**Hints**: Factor Analysis assumes noise is different per feature; PCA assumes same.

**Skills**: Factor Analysis, latent variable models

---

### F10: Independent Component Analysis
**Domain**: Signal Processing | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Apply ICA for blind source separation. Separate mixed signals into independent components (e.g., cocktail party problem).

**Mathematical Foundation**:
- Find maximally independent components
- Non-Gaussian sources
- FastICA algorithm

**Expected Deliverables**:
- ICA on mixed signals
- Blind source separation demo
- Comparison with PCA

**Test Cases**:
1. Separate mixed signals
2. Independence vs uncorrelation
3. Image to independent components

**Hints**: ICA finds independent components; PCA finds uncorrelated. Independence is stronger.

**Skills**: ICA, blind source separation

---

### F11: Sparse PCA
**Domain**: Dimensionality Reduction | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply Sparse PCA to get interpretable components with few non-zero loadings. Trade some variance for interpretability.

**Expected Deliverables**:
- SparsePCA usage
- Interpretable components
- Tradeoff with explained variance

**Test Cases**:
1. Sparse loadings visualization
2. Comparison with PCA
3. Sparsity level tuning

**Hints**: Sparse components are easier to interpret. Useful when features have meaning.

**Skills**: Sparse PCA, interpretable reduction

---

### F12: Truncated SVD
**Domain**: Dimensionality Reduction | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Use Truncated SVD for sparse matrices (e.g., TF-IDF) where PCA would fail. Equivalent to PCA but works on sparse data.

**Expected Deliverables**:
- TruncatedSVD on sparse matrix
- Text data application (LSA)
- Comparison with dense PCA

**Test Cases**:
1. Apply to TF-IDF matrix
2. Latent Semantic Analysis
3. Memory efficiency

**Hints**: Use for sparse data (text). Doesn't center data; handles sparse efficiently.

**Skills**: TruncatedSVD, sparse matrices, LSA

---

### F13: Random Projection
**Domain**: Dimensionality Reduction | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use Random Projection for fast, approximate dimensionality reduction. Johnson-Lindenstrauss lemma guarantees distance preservation.

**Mathematical Foundation**:
- Random matrix R with appropriate properties
- Z = XR preserves distances approximately

**Expected Deliverables**:
- GaussianRandomProjection
- SparseRandomProjection
- Distance preservation verification

**Test Cases**:
1. Speed comparison with PCA
2. Distance preservation check
3. Minimum dimensions for preservation

**Hints**: Much faster than PCA. Good for preprocessing before clustering.

**Skills**: Random projection, fast reduction

---

### F14: Feature Selection vs Extraction
**Domain**: Theory | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Compare feature selection (keep original features) with feature extraction (create new features). Understand tradeoffs.

**Expected Deliverables**:
- Feature selection methods
- Feature extraction methods
- When to use each

**Test Cases**:
1. Interpretability with selection
2. Better representation with extraction
3. Noise handling comparison

**Hints**: Selection keeps interpretability; extraction can find better representations.

**Skills**: Selection vs extraction, method choice

---

### F15: Manifold Learning Methods
**Domain**: Dimensionality Reduction | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Compare manifold learning: Isomap, LLE, Spectral Embedding. Discover non-linear manifolds in data.

**Expected Deliverables**:
- Isomap on Swiss roll
- LLE application
- Comparison of methods

**Test Cases**:
1. Swiss roll unrolling
2. Compare methods on same data
3. When manifold learning helps

**Hints**: These find geodesic distances on manifolds. Good for manifold-structured data.

**Skills**: Manifold learning, non-linear methods

---

### F16: Autoencoders for Dimensionality Reduction
**Domain**: Deep Learning | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Use autoencoders (neural networks) for non-linear dimensionality reduction. Encoder learns compressed representation.

**Expected Deliverables**:
- Simple autoencoder implementation
- Latent space visualization
- Comparison with PCA

**Test Cases**:
1. Reduce to low dimensions
2. Visualize latent space
3. Reconstruction quality

**Hints**: Bottleneck layer size = latent dimensions. Can capture non-linear relationships.

**Skills**: Autoencoders, deep dimensionality reduction

---

### F17: Dimensionality Reduction for Preprocessing Pipeline
**Domain**: Preprocessing | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Integrate dimensionality reduction into preprocessing pipelines. Handle CV correctly to avoid data leakage.

**Expected Deliverables**:
- Pipeline with PCA + classifier
- Cross-validation setup
- Hyperparameter tuning for reduction

**Test Cases**:
1. Correct CV avoiding leakage
2. Tune n_components in pipeline
3. Compare with full-feature model

**Hints**: Fit reduction only on training data. Use Pipeline for correct CV.

**Skills**: Pipeline construction, proper CV

---

### F18: Visualization Best Practices
**Domain**: Visualization | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Learn best practices for dimensionality reduction visualization. Understand what can and cannot be interpreted.

**Expected Deliverables**:
- Proper visualization techniques
- Common misinterpretations
- Choosing reduction method

**Test Cases**:
1. t-SNE misinterpretation examples
2. What distances mean
3. When to use which method

**Hints**: Don't interpret cluster sizes or distances in t-SNE. Run multiple times.

**Skills**: Visualization interpretation, best practices

---

### F19: Dimensionality Reduction Comparison
**Domain**: Comparison | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Systematically compare dimensionality reduction methods on various datasets. Create selection guidelines.

**Expected Deliverables**:
- Multiple methods on multiple datasets
- Preservation metrics (trust, continuity)
- Selection decision tree

**Test Cases**:
1. Linear vs non-linear data
2. Speed comparison
3. Downstream task performance

**Hints**: PCA for linear preprocessing; UMAP for visualization; LDA for classification.

**Skills**: Method comparison, selection

---

### F20: Dimensionality Reduction Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: Both

**Problem**: Comprehensive dimensionality reduction analysis: PCA from scratch, method comparison, visualization, and preprocessing pipeline.

**Expected Deliverables**:
- From-scratch PCA
- Method comparison
- Visualization gallery
- Preprocessing pipeline
- Best practice documentation

**Evaluation Criteria**: Understanding, methodology, practical application

**Hints**: Demonstrate understanding of when each method is appropriate.

**Skills**: Complete dimensionality reduction mastery

---

## Section G: Model Optimization & Hyperparameter Tuning (G1-G13)

### G1: Grid Search Deep Dive
**Domain**: Optimization | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Master GridSearchCV: define search space, choose scoring metric, parallelize computation, extract results.

**Expected Deliverables**:
- Complete GridSearchCV usage
- Result analysis (best params, CV results)
- Visualization of search space

**Test Cases**:
1. 2D parameter grid search
2. Extract and analyze all results
3. Visualize hyperparameter performance

**Hints**: Use refit=True to get best model. Access cv_results_ for all scores.

**Skills**: Grid search mastery

---

### G2: Random Search and Scalability
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply RandomizedSearchCV for efficient search over large spaces. Understand when random beats grid search.

**Expected Deliverables**:
- RandomizedSearchCV usage
- Distribution definitions
- Comparison with grid search efficiency

**Test Cases**:
1. Large parameter space
2. Continuous parameter distributions
3. Budget allocation comparison

**Hints**: Random search often finds same quality in fewer iterations.

**Skills**: Random search, efficient optimization

---

### G3: Bayesian Optimization
**Domain**: Optimization | **Difficulty**: ★★★★☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Apply Bayesian optimization using Optuna or Hyperopt. Use surrogate model to guide search efficiently.

**Expected Deliverables**:
- Optuna optimization
- Acquisition function understanding
- Comparison with random search

**Test Cases**:
1. Optimize complex function
2. Show sample efficiency
3. Visualization of optimization

**Hints**: Install Optuna. Define objective function. Uses TPE by default.

**Skills**: Bayesian optimization, modern tuning

---

### G4: Successive Halving and Hyperband
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply Successive Halving and Hyperband for fast hyperparameter tuning. Early-stop poor configurations.

**Expected Deliverables**:
- HalvingGridSearchCV usage
- HalvingRandomSearchCV
- Speedup analysis

**Test Cases**:
1. Compare with exhaustive grid search
2. Early stopping effect
3. Final result quality

**Hints**: sklearn >= 0.24 has Halving searches. Good for expensive models.

**Skills**: Efficient tuning, early stopping

---

### G5: Cross-Validation Strategies for Tuning
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Choose appropriate CV strategy for hyperparameter tuning: k-fold, stratified, grouped, time series.

**Expected Deliverables**:
- Custom CV for different data types
- GroupKFold for grouped data
- TimeSeriesSplit for temporal

**Test Cases**:
1. Stratified for imbalanced
2. Group k-fold for grouped samples
3. Time series split for temporal

**Hints**: Match CV strategy to data structure to avoid leakage.

**Skills**: CV strategies, proper evaluation

---

### G6: Multi-Metric Optimization
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Optimize for multiple metrics simultaneously. Handle tradeoffs and choose based on business requirements.

**Expected Deliverables**:
- Multiple scoring in search
- Refit based on preferred metric
- Pareto-optimal solutions

**Test Cases**:
1. Optimize accuracy and F1
2. Precision-recall tradeoff
3. Business metric incorporation

**Hints**: Use scoring parameter with dict. Set refit to preferred metric.

**Skills**: Multi-objective optimization

---

### G7: Pipeline Hyperparameter Tuning
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Tune hyperparameters of complete pipeline including preprocessing steps. Proper scoping of parameter names.

**Expected Deliverables**:
- Pipeline construction
- Nested parameter naming
- Full pipeline optimization

**Test Cases**:
1. Tune both preprocessor and model
2. Name parameters correctly (step__param)
3. Compare different pipelines

**Hints**: Use double underscore: 'classifier__C' for pipeline parameters.

**Skills**: Pipeline tuning, proper scoping

---

### G8: Custom Scoring Functions
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Create custom scoring functions for business-specific metrics. Integrate with sklearn search.

**Expected Deliverables**:
- Custom scorer definition
- make_scorer usage
- Business metric integration

**Test Cases**:
1. Custom cost-based metric
2. Weighted metric
3. Integration with GridSearchCV

**Hints**: Use make_scorer(). Handle greater_is_better correctly.

**Skills**: Custom metrics, business alignment

---

### G9: Automated Machine Learning (AutoML) Introduction
**Domain**: AutoML | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Explore AutoML tools that automate model selection and tuning: auto-sklearn, TPOT. Understand benefits and limitations.

**Expected Deliverables**:
- Auto-sklearn basic usage
- TPOT exploration
- When to use AutoML

**Test Cases**:
1. Auto model selection
2. Auto feature engineering
3. Compare with manual tuning

**Hints**: AutoML is good for baselines. May over-search for competitions.

**Skills**: AutoML tools, automated ML

---

### G10: Search Space Design
**Domain**: Optimization | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Design effective search spaces: ranges, scales (log vs linear), dependencies between parameters.

**Expected Deliverables**:
- Parameter range selection
- Log vs linear scale choice
- Conditional parameters

**Test Cases**:
1. Log scale for regularization
2. Linear for integers
3. Conditional search space

**Hints**: Regularization params usually log scale. Learning rate log scale.

**Skills**: Search space design

---

### G11: Early Stopping Strategies
**Domain**: Optimization | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Implement early stopping for iterative algorithms to save computation and prevent overfitting.

**Expected Deliverables**:
- Early stopping in boosting
- Patience parameter selection
- Validation monitoring

**Test Cases**:
1. Find optimal stopping point
2. Save computation
3. Generalization improvement

**Hints**: Use validation set for monitoring. Patience controls stopping.

**Skills**: Early stopping, efficient training

---

### G12: Hyperparameter Sensitivity Analysis
**Domain**: Analysis | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Analyze sensitivity of model performance to hyperparameters. Identify which parameters matter most.

**Expected Deliverables**:
- Sensitivity plots
- Important vs unimportant parameters
- Robustness analysis

**Test Cases**:
1. Vary one parameter, fix others
2. Interaction effects
3. Stable regions identification

**Hints**: Some parameters matter more than others. Focus tuning on important ones.

**Skills**: Sensitivity analysis, efficient tuning

---

### G13: Model Optimization Capstone
**Domain**: End-to-End | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Complete optimization project: search space design, method selection, analysis, and final model selection.

**Expected Deliverables**:
- Search space design
- Multiple optimization methods
- Result analysis
- Best model selection
- Documentation

**Evaluation Criteria**: Methodology, efficiency, final results

**Hints**: Compare methods on same budget. Document all choices.

**Skills**: Complete optimization mastery

---
