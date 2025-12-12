# Machine Learning Beginner Level Assignments (1-155)

> **Level**: Beginner | **Total Assignments**: 155 | **Focus**: ML Fundamentals, Supervised Learning Basics, Mathematical Foundations

## Summary

| Section | Topic | Questions |
|---------|-------|-----------|
| A | Mathematical Foundations | 30 |
| B | Data Preprocessing & Feature Engineering | 30 |
| C | Linear Regression | 25 |
| D | Logistic Regression & Classification | 25 |
| E | k-Nearest Neighbors | 20 |
| F | Evaluation Metrics & Validation | 25 |
| **Total** | | **155** |

---

## Section A: Mathematical Foundations (A1-A30)

### A1: Vector Operations from Scratch
**Domain**: Math/ML | **Difficulty**: ★☆☆☆☆ | **Time**: 30 min
**Implementation**: From Scratch

**Problem**: Implement a Vector class supporting addition, subtraction, scalar multiplication, dot product, and magnitude calculation. These operations form the backbone of all ML algorithms, from computing distances to gradient updates.

**Mathematical Foundation**: 
- Dot product: a·b = Σ(aᵢ × bᵢ)
- Magnitude: ||v|| = √(Σvᵢ²)

**Expected Deliverables**:
- Vector class with all operations
- Unit tests for each operation

**Test Cases**:
1. `[1,2,3] + [4,5,6]` → `[5,7,9]`
2. `[1,2,3] · [4,5,6]` → `32`
3. `||[3,4]||` → `5.0`

**Hints**: Use list comprehensions; magnitude is just the square root of the dot product with itself.

**Skills**: Linear algebra, OOP, numerical computing

---

### A2: Matrix Operations from Scratch
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: From Scratch

**Problem**: Build a Matrix class with addition, subtraction, scalar multiplication, matrix multiplication, and transpose. Matrix operations are essential for transforming data, solving linear systems, and implementing neural networks.

**Mathematical Foundation**:
- Matrix multiplication: Cᵢⱼ = Σₖ(Aᵢₖ × Bₖⱼ)
- Transpose: Aᵀᵢⱼ = Aⱼᵢ

**Expected Deliverables**:
- Matrix class with dimension validation
- Transpose and multiplication methods

**Test Cases**:
1. `[[1,2],[3,4]] × [[5,6],[7,8]]` → `[[19,22],[43,50]]`
2. `[[1,2,3],[4,5,6]]ᵀ` → `[[1,4],[2,5],[3,6]]`

**Hints**: Check dimension compatibility before multiplication (m×n) × (n×p) = (m×p).

**Skills**: Matrix algebra, nested loops, input validation

---

### A3: NumPy Vector and Matrix Basics
**Domain**: Math/ML | **Difficulty**: ★☆☆☆☆ | **Time**: 25 min
**Implementation**: Libraries (NumPy)

**Problem**: Recreate A1 and A2 operations using NumPy. Compare performance between your from-scratch implementation and NumPy on large arrays (10000+ elements). Understand why vectorized operations are crucial for ML.

**Expected Deliverables**:
- NumPy equivalents of all operations
- Performance comparison table
- Explanation of broadcasting

**Test Cases**:
1. Time comparison for 10000-element vector dot product
2. Verify NumPy results match from-scratch results

**Hints**: Use `np.dot()`, `@` operator, `.T` for transpose. Use `%timeit` for benchmarking.

**Skills**: NumPy basics, vectorization, performance profiling

---

### A4: Eigenvalue and Eigenvector Computation
**Domain**: Math/ML | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Both

**Problem**: Understand eigenvalues and eigenvectors conceptually, then use NumPy to compute them. Create visualizations showing how eigenvectors represent the principal directions of a transformation. This is fundamental for PCA and understanding data variance.

**Mathematical Foundation**:
- Av = λv where λ is eigenvalue, v is eigenvector
- Characteristic polynomial: det(A - λI) = 0

**Dataset**: Create 2D synthetic data with clear directional variance

**Expected Deliverables**:
- Visualization of eigenvectors on transformed data
- Explanation of eigenvalue magnitude meaning

**Test Cases**:
1. `[[2,1],[1,2]]` eigenvalues → `[3, 1]`
2. Verify Av = λv relationship

**Hints**: Use `np.linalg.eig()`. Larger eigenvalues indicate directions of greater variance.

**Skills**: Linear algebra, data visualization, NumPy linalg

---

### A5: Matrix Inverse and Determinant
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Implement 2x2 matrix inverse from scratch, then use NumPy for larger matrices. Understand when matrices are invertible (non-zero determinant) and why this matters for solving linear systems in ML (e.g., normal equation for linear regression).

**Mathematical Foundation**:
- 2×2 inverse: A⁻¹ = (1/det(A)) × [[d,-b],[-c,a]]
- det([[a,b],[c,d]]) = ad - bc

**Expected Deliverables**:
- From-scratch 2x2 inverse function
- Singular matrix detection
- Connection to linear regression normal equation

**Test Cases**:
1. `[[4,7],[2,6]]` inverse → `[[0.6,-0.7],[-0.2,0.4]]`
2. `[[1,2],[2,4]]` → Singular (no inverse)

**Hints**: Check determinant before inverting. Use `np.linalg.inv()` for larger matrices.

**Skills**: Matrix algebra, error handling, numerical stability

---

### A6: Linear System Solver
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Solve systems of linear equations Ax = b using matrix inverse and NumPy's solver. This directly applies to finding optimal weights in linear regression via the normal equation: θ = (XᵀX)⁻¹Xᵀy.

**Mathematical Foundation**:
- Solution: x = A⁻¹b
- Normal equation: θ = (XᵀX)⁻¹Xᵀy

**Expected Deliverables**:
- Solver using inverse method
- Solver using `np.linalg.solve()`
- Performance and stability comparison

**Test Cases**:
1. `2x + y = 5, x + 3y = 6` → `x=1.8, y=1.4`

**Hints**: `np.linalg.solve()` is more numerically stable than computing inverse explicitly.

**Skills**: Linear algebra applications, numerical methods

---

### A7: Derivative Computation
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: From Scratch

**Problem**: Implement numerical differentiation using the definition of derivative. Compute derivatives of common ML functions: x², eˣ, log(x), sigmoid. Compare numerical results with analytical derivatives.

**Mathematical Foundation**:
- f'(x) ≈ (f(x+h) - f(x-h)) / 2h (central difference)
- Sigmoid derivative: σ(x)(1-σ(x))

**Expected Deliverables**:
- Numerical derivative function
- Comparison table with analytical derivatives
- Error analysis for different h values

**Test Cases**:
1. d/dx(x²) at x=3 → 6
2. d/dx(eˣ) at x=0 → 1
3. Sigmoid derivative at x=0 → 0.25

**Hints**: Use h=1e-5 for good accuracy. Central difference is more accurate than forward difference.

**Skills**: Calculus, numerical methods, function composition

---

### A8: Gradient Computation
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: From Scratch

**Problem**: Extend derivative computation to gradients (partial derivatives). Compute gradients for functions of multiple variables like f(x,y) = x² + y², which is essential for optimizing ML loss functions.

**Mathematical Foundation**:
- Gradient: ∇f = [∂f/∂x₁, ∂f/∂x₂, ..., ∂f/∂xₙ]
- Points in direction of steepest increase

**Expected Deliverables**:
- Gradient computation function
- Visualization of gradient vectors on contour plot

**Test Cases**:
1. ∇(x² + y²) at (1,1) → [2, 2]
2. ∇(x²y + y³) at (2,3) → [12, 31]

**Hints**: Compute partial derivative by varying one variable while fixing others.

**Skills**: Multivariable calculus, visualization

---

### A9: Chain Rule Implementation
**Domain**: Math/ML | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Implement the chain rule for composite functions. This is the mathematical foundation of backpropagation in neural networks. Compute derivatives of nested functions like sigmoid(wx + b).

**Mathematical Foundation**:
- Chain rule: d/dx[f(g(x))] = f'(g(x)) × g'(x)
- For sigmoid(wx+b): σ'(wx+b) × w

**Expected Deliverables**:
- Composite function derivative calculator
- Step-by-step breakdown of each derivative
- Verification against numerical derivatives

**Test Cases**:
1. d/dx[sin(x²)] at x=1 → 2cos(1)
2. d/dx[sigmoid(2x+1)] at x=0

**Hints**: Break complex functions into simple components and multiply derivatives.

**Skills**: Chain rule, function decomposition, backpropagation foundation

---

### A10: Gradient Descent Visualization
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: From Scratch

**Problem**: Implement gradient descent to find the minimum of f(x,y) = x² + y². Create an animated visualization showing the optimization path from different starting points. This builds intuition for how ML models learn.

**Mathematical Foundation**:
- Update rule: θ = θ - α∇f(θ)
- α is learning rate

**Expected Deliverables**:
- Gradient descent optimizer
- Animated path visualization
- Convergence analysis for different learning rates

**Test Cases**:
1. Minimum of x² + y² → (0, 0)
2. Compare paths with α=0.1, 0.5, 1.5

**Hints**: Too large learning rate causes oscillation; too small is slow. Use matplotlib animation.

**Skills**: Optimization, visualization, learning rate intuition

---

### A11: Mean, Variance, and Standard Deviation
**Domain**: Statistics/ML | **Difficulty**: ★☆☆☆☆ | **Time**: 25 min
**Implementation**: Both

**Problem**: Implement mean, variance, and standard deviation from scratch for both population and sample. These statistics are fundamental for data normalization, feature scaling, and understanding data distributions.

**Mathematical Foundation**:
- Mean: μ = (1/n)Σxᵢ
- Variance: σ² = (1/n)Σ(xᵢ - μ)²
- Sample variance uses (n-1) for Bessel's correction

**Expected Deliverables**:
- From-scratch implementations
- NumPy verification
- Explanation of population vs sample variance

**Test Cases**:
1. `[2,4,4,4,5,5,7,9]` mean → 5, var → 4
2. Compare sample vs population variance

**Hints**: Use `np.mean()`, `np.var(ddof=0)` for population, `ddof=1` for sample.

**Skills**: Descriptive statistics, NumPy

---

### A12: Probability Distributions Exploration
**Domain**: Statistics/ML | **Difficulty**: ★★☆☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Explore and visualize key probability distributions used in ML: Normal (Gaussian), Uniform, Bernoulli, Binomial, Poisson. Understand when each distribution applies and how to sample from them.

**Expected Deliverables**:
- PDF/PMF plots for each distribution
- Random sampling demonstrations
- Real-world examples for each distribution

**Test Cases**:
1. Normal(μ=0, σ=1) → ~68% within [-1,1]
2. Binomial(n=10, p=0.5) mode → 5

**Hints**: Use `scipy.stats` for distributions. `rvs()` for sampling, `pdf()`/`pmf()` for probability.

**Skills**: Probability theory, scipy.stats, visualization

---

### A13: Bayes' Theorem Calculator
**Domain**: Statistics/ML | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: From Scratch

**Problem**: Implement Bayes' theorem and solve classic problems: disease testing, spam classification probability. Understanding Bayesian reasoning is essential for Naive Bayes classifiers and probabilistic ML models.

**Mathematical Foundation**:
- P(A|B) = P(B|A) × P(A) / P(B)
- P(B) = P(B|A)P(A) + P(B|¬A)P(¬A)

**Expected Deliverables**:
- Bayes calculator function
- Disease test problem solution with explanation
- Sensitivity to prior probabilities analysis

**Test Cases**:
1. Disease test: P(disease)=1%, sensitivity=99%, specificity=95% → P(disease|positive)?
2. Spam: P(spam)=30%, P("free"|spam)=80%, P("free"|¬spam)=10%

**Hints**: The base rate (prior) dramatically affects posterior probability.

**Skills**: Bayesian reasoning, probability calculations

---

### A14: Covariance and Correlation
**Domain**: Statistics/ML | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Compute covariance and Pearson correlation coefficient from scratch. Create a covariance matrix for multivariate data. These measure relationships between features and are essential for PCA and feature selection.

**Mathematical Foundation**:
- Cov(X,Y) = E[(X-μₓ)(Y-μᵧ)]
- Correlation: r = Cov(X,Y) / (σₓσᵧ)

**Dataset**: Use iris dataset or create correlated synthetic data

**Expected Deliverables**:
- Covariance and correlation functions
- Covariance matrix heatmap
- Interpretation of correlation values

**Test Cases**:
1. Perfect positive correlation → r = 1
2. Perfect negative correlation → r = -1
3. No correlation → r ≈ 0

**Hints**: Correlation is covariance normalized to [-1, 1]. Use `np.cov()`, `np.corrcoef()`.

**Skills**: Statistical relationships, feature analysis, visualization

---

### A15: Hypothesis Testing Basics
**Domain**: Statistics/ML | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Both

**Problem**: Implement t-test and understand p-values, significance levels, and Type I/II errors. Apply to A/B testing scenarios common in ML model comparison and feature significance.

**Mathematical Foundation**:
- t = (x̄ - μ₀) / (s/√n)
- p-value: probability of observing results at least as extreme

**Expected Deliverables**:
- One-sample and two-sample t-test implementations
- p-value interpretation guide
- A/B test scenario analysis

**Test Cases**:
1. Compare two model accuracy distributions
2. Test if feature mean differs from zero

**Hints**: Use `scipy.stats.ttest_ind()` for verification. α=0.05 is common threshold.

**Skills**: Inferential statistics, hypothesis testing, A/B testing

---

### A16: Central Limit Theorem Demonstration
**Domain**: Statistics/ML | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Demonstrate the Central Limit Theorem by sampling from non-normal distributions and showing that sample means become normally distributed. This justifies many statistical assumptions in ML.

**Expected Deliverables**:
- Sampling from uniform, exponential, binomial distributions
- Visualization of sample mean distributions
- Convergence analysis for different sample sizes

**Test Cases**:
1. Uniform[0,1] sample means → Normal as n increases
2. Show normality with n=5, 30, 100

**Hints**: Create 1000+ samples of size n, compute means, plot histogram.

**Skills**: Statistical theory, simulation, visualization

---

### A17: Euclidean and Manhattan Distance
**Domain**: Math/ML | **Difficulty**: ★☆☆☆☆ | **Time**: 25 min
**Implementation**: Both

**Problem**: Implement Euclidean (L2) and Manhattan (L1) distance metrics from scratch. These are the foundation of k-NN, clustering, and similarity-based algorithms.

**Mathematical Foundation**:
- Euclidean: d = √(Σ(xᵢ - yᵢ)²)
- Manhattan: d = Σ|xᵢ - yᵢ|

**Expected Deliverables**:
- Distance functions for n-dimensional vectors
- Visualization of distance contours in 2D
- When to use each metric

**Test Cases**:
1. Euclidean: `[0,0]` to `[3,4]` → 5
2. Manhattan: `[0,0]` to `[3,4]` → 7

**Hints**: Euclidean measures "as the crow flies"; Manhattan measures "city block" distance.

**Skills**: Distance metrics, geometry

---

### A18: Cosine Similarity and Distance
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Both

**Problem**: Implement cosine similarity for comparing vectors by angle rather than magnitude. This is crucial for text/document similarity where vector length shouldn't affect comparison.

**Mathematical Foundation**:
- Cosine similarity: cos(θ) = (A·B) / (||A|| × ||B||)
- Cosine distance: 1 - cosine similarity

**Expected Deliverables**:
- Cosine similarity function
- Comparison with Euclidean distance
- Document similarity example

**Test Cases**:
1. `[1,0]` and `[0,1]` → similarity = 0 (perpendicular)
2. `[1,1]` and `[2,2]` → similarity = 1 (same direction)

**Hints**: Normalize vectors first, then dot product equals cosine similarity.

**Skills**: Vector similarity, NLP foundations

---

### A19: Minkowski Distance Generalization
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: From Scratch

**Problem**: Implement generalized Minkowski distance that includes Euclidean (p=2), Manhattan (p=1), and Chebyshev (p=∞) as special cases. Understand how parameter p affects distance behavior.

**Mathematical Foundation**:
- Minkowski: d = (Σ|xᵢ - yᵢ|ᵖ)^(1/p)
- p=1: Manhattan, p=2: Euclidean, p→∞: Chebyshev (max)

**Expected Deliverables**:
- Generalized Minkowski function
- Visualization of unit circles for different p values
- Use case recommendations

**Test Cases**:
1. Verify p=1 matches Manhattan
2. Verify p=2 matches Euclidean
3. p=∞ should equal max(|xᵢ - yᵢ|)

**Hints**: For p=∞, use `max()` instead of the formula.

**Skills**: Distance metrics, mathematical generalization

---

### A20: K-Nearest Neighbors Distance Selection
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Compare k-NN performance using different distance metrics on various datasets. Determine which metric works best for different data types (continuous, binary, mixed).

**Dataset**: Iris (continuous), MNIST subset (binary), synthetic mixed

**Expected Deliverables**:
- k-NN accuracy comparison table
- Visualization of decision boundaries
- Metric selection guidelines

**Evaluation Criteria**: Accuracy with different distance metrics

**Hints**: Use `sklearn.neighbors.KNeighborsClassifier(metric=...)`. Consider feature scaling effects.

**Skills**: Distance metrics in practice, sklearn

---

### A21: Sampling Techniques
**Domain**: Statistics/ML | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Implement random sampling, stratified sampling, and systematic sampling. Proper sampling ensures representative train/test splits and is crucial for unbiased model evaluation.

**Expected Deliverables**:
- Sampling functions for each technique
- Comparison of class distributions
- Demonstration on imbalanced dataset

**Test Cases**:
1. Stratified split preserves class ratios
2. Random split may skew class ratios

**Hints**: Use `sklearn.model_selection.train_test_split(stratify=...)` for stratified splitting.

**Skills**: Sampling theory, data splitting

---

### A22: Confidence Intervals
**Domain**: Statistics/ML | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Calculate confidence intervals for means and proportions. Apply to ML model performance metrics to understand the uncertainty in accuracy estimates.

**Mathematical Foundation**:
- CI = x̄ ± z*(σ/√n)
- 95% CI uses z* = 1.96

**Expected Deliverables**:
- Confidence interval calculator
- Model accuracy confidence intervals
- Sample size vs CI width analysis

**Test Cases**:
1. 95% CI for accuracy = 0.85, n = 100
2. How n affects CI width

**Hints**: Larger samples give narrower confidence intervals.

**Skills**: Statistical inference, model evaluation uncertainty

---

### A23: Maximum Likelihood Estimation Concept
**Domain**: Statistics/ML | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Understand and implement Maximum Likelihood Estimation for simple distributions (Bernoulli, Gaussian). MLE is the foundation of how many ML algorithms learn optimal parameters.

**Mathematical Foundation**:
- Likelihood: L(θ|data) = ∏P(xᵢ|θ)
- Log-likelihood: ℓ(θ) = Σlog P(xᵢ|θ)
- MLE: argmax_θ ℓ(θ)

**Expected Deliverables**:
- MLE for Bernoulli (coin flip) parameter
- MLE for Gaussian mean and variance
- Visualization of likelihood function

**Test Cases**:
1. Coin: 7 heads, 3 tails → MLE p = 0.7
2. Normal data → MLE μ = sample mean

**Hints**: Take derivative of log-likelihood, set to zero, solve for θ.

**Skills**: Statistical estimation, optimization foundations

---

### A24: Information Theory - Entropy
**Domain**: Math/ML | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: From Scratch

**Problem**: Implement Shannon entropy and understand its meaning as "uncertainty" or "information content." Entropy is used in decision tree splitting criteria and compression algorithms.

**Mathematical Foundation**:
- Entropy: H(X) = -Σ p(x) log₂ p(x)
- Maximum entropy for uniform distribution

**Expected Deliverables**:
- Entropy calculator
- Entropy of different probability distributions
- Connection to decision tree information gain

**Test Cases**:
1. Fair coin: H = 1 bit
2. Biased coin (p=0.9): H < 1 bit
3. Certain outcome (p=1): H = 0

**Hints**: Handle p=0 specially (0 × log(0) = 0 by convention).

**Skills**: Information theory, decision tree foundations

---

### A25: Cross-Entropy and KL Divergence
**Domain**: Math/ML | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Implement cross-entropy and KL divergence. Cross-entropy is the most common loss function for classification; KL divergence measures how one distribution differs from another.

**Mathematical Foundation**:
- Cross-entropy: H(p,q) = -Σ p(x) log q(x)
- KL divergence: D_KL(p||q) = Σ p(x) log(p(x)/q(x))
- H(p,q) = H(p) + D_KL(p||q)

**Expected Deliverables**:
- Cross-entropy loss function
- KL divergence calculator
- Connection to classification loss

**Test Cases**:
1. True: [1,0,0], Pred: [0.9,0.05,0.05] → low cross-entropy
2. True: [1,0,0], Pred: [0.1,0.45,0.45] → high cross-entropy

**Hints**: Cross-entropy penalizes confident wrong predictions heavily.

**Skills**: Loss functions, classification metrics

---

### A26: Softmax Function
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: From Scratch

**Problem**: Implement softmax function that converts raw scores to probabilities. Handle numerical stability issues with the log-sum-exp trick. Softmax is essential for multi-class classification.

**Mathematical Foundation**:
- softmax(zᵢ) = exp(zᵢ) / Σexp(zⱼ)
- Stable: subtract max(z) before exp

**Expected Deliverables**:
- Numerically stable softmax
- Gradient of softmax (for backprop)
- Visualization of softmax output

**Test Cases**:
1. `[1,2,3]` → `[0.09, 0.24, 0.67]`
2. `[1000,1001,1002]` shouldn't overflow

**Hints**: Without stability trick, large values cause overflow.

**Skills**: Activation functions, numerical stability

---

### A27: Log-Sum-Exp Trick
**Domain**: Math/ML | **Difficulty**: ★★☆☆☆ | **Time**: 25 min
**Implementation**: From Scratch

**Problem**: Implement the log-sum-exp trick for numerically stable computation. This technique is essential when working with probabilities in log space.

**Mathematical Foundation**:
- log(Σexp(xᵢ)) = max(x) + log(Σexp(xᵢ - max(x)))

**Expected Deliverables**:
- Stable log-sum-exp function
- Comparison of naive vs stable implementation
- Application to softmax denominator

**Test Cases**:
1. `[1000, 1001, 1002]` should give correct result without overflow
2. `[-1000, -999, -998]` should work without underflow

**Hints**: Always subtract max before exponentiating, add it back after.

**Skills**: Numerical stability, logarithmic computation

---

### A28: Normal Equation Derivation
**Domain**: Math/ML | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Derive and implement the normal equation for linear regression. Understand when to use normal equation vs gradient descent based on feature count and dataset size.

**Mathematical Foundation**:
- Loss: J(θ) = ||Xθ - y||²
- Normal equation: θ = (XᵀX)⁻¹Xᵀy

**Expected Deliverables**:
- Mathematical derivation walkthrough
- Implementation with NumPy
- Comparison with sklearn LinearRegression
- Complexity analysis: O(n³) for matrix inverse

**Test Cases**:
1. Simple linear: y = 2x + 1 → θ = [1, 2]
2. Match sklearn results

**Hints**: Normal equation is faster for small n (features < 10000), but doesn't scale.

**Skills**: Linear algebra application, regression theory

---

### A29: Convexity and Local Minima
**Domain**: Math/ML | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Visualize convex vs non-convex functions. Demonstrate that gradient descent converges to global minimum for convex functions but may get stuck in local minima for non-convex functions.

**Expected Deliverables**:
- Plots of convex (MSE) vs non-convex functions
- Gradient descent on both function types
- Multiple starting points showing different convergence

**Test Cases**:
1. MSE loss: always converges to same minimum
2. Non-convex: different start → different end

**Hints**: Linear/logistic regression losses are convex; neural network losses are not.

**Skills**: Optimization theory, visualization

---

### A30: Jacobian and Hessian Introduction
**Domain**: Math/ML | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Both

**Problem**: Compute Jacobian matrices for vector-valued functions and Hessian matrices for scalar functions. These are used in advanced optimization (Newton's method) and understanding loss surface curvature.

**Mathematical Foundation**:
- Jacobian: Jᵢⱼ = ∂fᵢ/∂xⱼ
- Hessian: Hᵢⱼ = ∂²f/∂xᵢ∂xⱼ

**Expected Deliverables**:
- Numerical Jacobian calculator
- Numerical Hessian calculator
- Visualization of Hessian for 2D function

**Test Cases**:
1. f(x,y) = [x²+y, xy] Jacobian at (1,2)
2. f(x,y) = x² + y² Hessian = [[2,0],[0,2]]

**Hints**: Second derivatives indicate curvature. Positive definite Hessian → local minimum.

**Skills**: Advanced calculus, optimization foundations

---

## Section B: Data Preprocessing & Feature Engineering (B1-B30)

### B1: Loading and Exploring Datasets
**Domain**: Data Prep | **Difficulty**: ★☆☆☆☆ | **Time**: 25 min
**Implementation**: Libraries (Pandas)

**Problem**: Load CSV, Excel, and JSON files using pandas. Perform initial exploration: shape, dtypes, head/tail, describe, info. This is always the first step in any ML project to understand your data.

**Dataset**: Any Kaggle dataset (Titanic, House Prices)

**Expected Deliverables**:
- Loading code for different file formats
- Summary statistics interpretation
- Column-wise data type analysis

**Test Cases**:
1. Load Titanic dataset successfully
2. Identify numeric vs categorical columns
3. Generate statistical summary

**Hints**: Use `pd.read_csv()`, `.info()`, `.describe(include='all')`.

**Skills**: Pandas basics, data exploration

---

### B2: Missing Value Detection and Analysis
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Detect missing values, visualize patterns, and understand missingness mechanisms (MCAR, MAR, MNAR). Missing data is ubiquitous in real-world datasets and handling it properly is critical for model performance.

**Dataset**: Titanic or any dataset with missing values

**Expected Deliverables**:
- Missing value count and percentage per column
- Heatmap visualization of missing patterns
- Missingness mechanism hypothesis

**Test Cases**:
1. Identify columns with >20% missing
2. Detect if missingness correlates with other columns
3. Visualize missing pattern matrix

**Hints**: Use `df.isnull().sum()`, `seaborn.heatmap()`, `missingno` library.

**Skills**: Missing data analysis, visualization

---

### B3: Missing Value Imputation - Simple Methods
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Implement mean, median, mode imputation for numeric and categorical features. Understand when each method is appropriate and the bias each can introduce.

**Mathematical Foundation**:
- Mean: sensitive to outliers
- Median: robust to outliers
- Mode: for categorical data

**Expected Deliverables**:
- Imputation functions from scratch
- sklearn SimpleImputer usage
- Before/after distribution comparison

**Test Cases**:
1. Impute Age column with median
2. Impute Cabin column with mode
3. Compare distributions before/after

**Hints**: Use `sklearn.impute.SimpleImputer`. Always check distribution changes after imputation.

**Skills**: Imputation techniques, sklearn imputers

---

### B4: Missing Value Imputation - Advanced Methods
**Domain**: Data Prep | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Implement KNN imputation and iterative imputation (MICE). These methods use relationships between features to estimate missing values more accurately than simple methods.

**Expected Deliverables**:
- KNN imputer with different k values
- Iterative imputer with different estimators
- Accuracy comparison on artificially missing data

**Test Cases**:
1. KNN imputation with k=3, 5, 10
2. Compare imputation accuracy to ground truth
3. Show when advanced methods outperform simple ones

**Hints**: Use `sklearn.impute.KNNImputer`, `IterativeImputer`. These require scaling features first.

**Skills**: Advanced imputation, sklearn, experimental design

---

### B5: Duplicate Detection and Removal
**Domain**: Data Prep | **Difficulty**: ★☆☆☆☆ | **Time**: 20 min
**Implementation**: Libraries

**Problem**: Detect exact and near-duplicate records. Understand when to remove duplicates vs keep them (data collection process matters). Duplicates can cause data leakage if not handled properly.

**Expected Deliverables**:
- Exact duplicate detection
- Near-duplicate detection (fuzzy matching)
- Duplicate removal strategy

**Test Cases**:
1. Find exact duplicate rows
2. Find duplicates by subset of columns
3. Keep first vs last duplicate handling

**Hints**: Use `df.duplicated()`, `df.drop_duplicates()`. Consider `fuzzywuzzy` for near-duplicates.

**Skills**: Data cleaning, deduplication

---

### B6: Outlier Detection - Statistical Methods
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Detect outliers using Z-score, IQR (Interquartile Range), and modified Z-score methods. Outliers can heavily influence model training, especially for algorithms sensitive to scale.

**Mathematical Foundation**:
- Z-score: z = (x - μ) / σ, outlier if |z| > 3
- IQR: outlier if x < Q1-1.5×IQR or x > Q3+1.5×IQR

**Expected Deliverables**:
- Outlier detection functions for each method
- Visualization with outliers highlighted
- Comparison of methods on skewed vs normal data

**Test Cases**:
1. Detect outliers in normal distribution
2. Compare Z-score vs IQR on skewed data
3. Sensitivity to threshold parameters

**Hints**: IQR is more robust for skewed distributions. Z-score assumes normality.

**Skills**: Statistical outlier detection, visualization

---

### B7: Outlier Treatment Strategies
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Implement strategies for handling outliers: removal, capping (winsorization), transformation, or keeping as separate category. The choice depends on whether outliers are errors or genuine extreme values.

**Expected Deliverables**:
- Removal implementation
- Winsorization at percentiles
- Log/sqrt transformation
- Impact analysis on model performance

**Test Cases**:
1. Cap values at 1st and 99th percentile
2. Compare linear regression with/without outlier treatment
3. Log transform skewed income data

**Hints**: Use `scipy.stats.mstats.winsorize()`. Always investigate why outliers exist before removing.

**Skills**: Outlier treatment, data transformation

---

### B8: Feature Scaling - Standardization
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Both

**Problem**: Implement Z-score standardization (zero mean, unit variance) from scratch. This is essential for distance-based algorithms (k-NN, SVM) and gradient descent optimization.

**Mathematical Foundation**:
- z = (x - μ) / σ
- Results in mean=0, std=1

**Expected Deliverables**:
- StandardScaler from scratch
- sklearn StandardScaler comparison
- Visualization of before/after distributions

**Test Cases**:
1. Standardize features with different scales
2. Verify mean≈0, std≈1 after transformation
3. Handle edge case of zero variance

**Hints**: Fit on training data only, transform both train and test with same parameters.

**Skills**: Feature scaling, sklearn transformers

---

### B9: Feature Scaling - Normalization
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Both

**Problem**: Implement Min-Max normalization (scales to [0,1]) and MaxAbs scaling. Normalization is preferred when data doesn't follow Gaussian distribution and for neural networks.

**Mathematical Foundation**:
- Min-Max: x' = (x - min) / (max - min)
- MaxAbs: x' = x / |max|

**Expected Deliverables**:
- MinMaxScaler from scratch
- Comparison with standardization
- When to use each method

**Test Cases**:
1. Scale features to [0, 1] range
2. Scale to [-1, 1] range
3. Handle new test data outside training range

**Hints**: Min-Max is sensitive to outliers. MaxAbs preserves sparsity.

**Skills**: Normalization techniques, sklearn scalers

---

### B10: Robust Scaling
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 25 min
**Implementation**: Both

**Problem**: Implement RobustScaler using median and IQR for scaling. This method is robust to outliers, making it ideal when your data contains extreme values you want to keep.

**Mathematical Foundation**:
- x' = (x - median) / IQR
- IQR = Q3 - Q1

**Expected Deliverables**:
- RobustScaler from scratch
- Comparison with StandardScaler on outlier-heavy data
- Visualization showing robustness

**Test Cases**:
1. Scale data with outliers
2. Compare to StandardScaler result
3. Show median and IQR are not affected by outliers

**Hints**: Use `sklearn.preprocessing.RobustScaler`. Great for features with many outliers.

**Skills**: Robust statistics, scaling

---

### B11: One-Hot Encoding
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Implement one-hot encoding for categorical variables. Handle unknown categories at prediction time and the dummy variable trap (multicollinearity).

**Expected Deliverables**:
- One-hot encoder from scratch
- pandas get_dummies usage
- sklearn OneHotEncoder with unknown handling
- Drop first strategy for linear models

**Test Cases**:
1. Encode color column: [red, blue, green]
2. Handle unknown category at test time
3. Demonstrate dummy variable trap

**Hints**: Use `drop='first'` for linear models. Handle unknown with `handle_unknown='ignore'`.

**Skills**: Categorical encoding, sklearn preprocessing

---

### B12: Label Encoding and Ordinal Encoding
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Both

**Problem**: Implement label encoding (categories to integers) and ordinal encoding (respects category order). Understand when each is appropriate—ordinal for tree-based models, ordinal features only.

**Expected Deliverables**:
- LabelEncoder from scratch
- OrdinalEncoder with custom order
- When to use vs one-hot encoding

**Test Cases**:
1. Label encode target variable
2. Ordinal encode education: [High School, Bachelor, Master, PhD]
3. Show why arbitrary label encoding can mislead linear models

**Hints**: LabelEncoder is for targets; OrdinalEncoder for features. Tree models handle label encoding fine.

**Skills**: Encoding strategies, tree vs linear model considerations

---

### B13: Target Encoding (Mean Encoding)
**Domain**: Data Prep | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Implement target encoding where categories are replaced by the mean of the target variable. Handle regularization to prevent overfitting on rare categories and proper cross-validation scheme to avoid data leakage.

**Mathematical Foundation**:
- encoded = (n × category_mean + m × global_mean) / (n + m)
- m is smoothing parameter

**Expected Deliverables**:
- Target encoder with smoothing
- Leave-one-out encoding to prevent leakage
- K-fold target encoding

**Test Cases**:
1. Encode city with ~100 categories
2. Compare smoothed vs non-smoothed results
3. Demonstrate data leakage without proper CV

**Hints**: Use `category_encoders.TargetEncoder`. Always encode using cross-validation folds.

**Skills**: Advanced encoding, data leakage prevention

---

### B14: Frequency and Count Encoding
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 25 min
**Implementation**: Both

**Problem**: Implement frequency encoding (replace category with its frequency in dataset) and count encoding. These simple techniques can capture meaningful information about category prevalence.

**Expected Deliverables**:
- Frequency encoder from scratch
- Count encoder implementation
- Comparison with one-hot for high-cardinality features

**Test Cases**:
1. Encode product_id with 1000+ categories
2. Show frequency captures popularity signal
3. Handle categories with same frequency

**Hints**: Frequency encoding is lightweight and works well for tree-based models with high-cardinality features.

**Skills**: Encoding for high-cardinality features

---

### B15: Binary Encoding
**Domain**: Data Prep | **Difficulty**: ★★★☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Implement binary encoding which converts categories to integer, then to binary representation. This is memory-efficient for high-cardinality features: log₂(n) columns vs n columns for one-hot.

**Expected Deliverables**:
- Binary encoder from scratch
- Comparison with one-hot on column count
- Performance comparison on tree vs linear models

**Test Cases**:
1. Encode 100 categories → 7 binary columns
2. Compare memory usage with one-hot
3. Model accuracy comparison

**Hints**: Use `category_encoders.BinaryEncoder`. Good balance between expressiveness and dimensionality.

**Skills**: Efficient encoding, high-cardinality handling

---

### B16: Feature Selection - Filter Methods
**Domain**: Feature Eng | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Implement filter-based feature selection: correlation threshold, variance threshold, chi-square test, mutual information. These methods select features independent of any model.

**Expected Deliverables**:
- Correlation-based selector (remove highly correlated)
- Variance threshold selector
- Chi-square for categorical features
- Mutual information for numeric features

**Test Cases**:
1. Remove features with >0.9 correlation
2. Remove constant/quasi-constant features
3. Select top 10 features by mutual information

**Hints**: Use `sklearn.feature_selection.VarianceThreshold`, `SelectKBest`, `mutual_info_classif`.

**Skills**: Filter feature selection, sklearn selectors

---

### B17: Feature Selection - Wrapper Methods
**Domain**: Feature Eng | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Implement wrapper feature selection: forward selection, backward elimination, and recursive feature elimination (RFE). These methods use model performance to select features.

**Expected Deliverables**:
- Forward selection implementation
- Backward elimination implementation
- RFE with cross-validation

**Test Cases**:
1. Forward select until 10 features
2. RFE to find optimal feature count
3. Compare selected features across methods

**Hints**: Use `sklearn.feature_selection.RFE`, `RFECV`. Wrapper methods are computationally expensive.

**Skills**: Wrapper selection, model-based feature selection

---

### B18: Feature Selection - Embedded Methods
**Domain**: Feature Eng | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Use L1 regularization (Lasso) and tree-based feature importance for embedded feature selection. These methods select features as part of the model training process.

**Expected Deliverables**:
- Lasso for feature selection
- Random Forest feature importances
- SelectFromModel usage
- Comparison across methods

**Test Cases**:
1. Lasso with different alpha values
2. Top 10 features by RF importance
3. Compare with filter/wrapper selections

**Hints**: Use `sklearn.feature_selection.SelectFromModel`. L1 shrinks irrelevant features to exactly zero.

**Skills**: Embedded selection, regularization for selection

---

### B19: Polynomial Feature Generation
**Domain**: Feature Eng | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Generate polynomial features and interaction terms to capture non-linear relationships. Understand degree selection and the curse of dimensionality with high-degree polynomials.

**Expected Deliverables**:
- Polynomial features from scratch
- sklearn PolynomialFeatures
- Impact on linear regression performance

**Test Cases**:
1. Generate x², x³, x₁×x₂ features
2. Show polynomial regression fitting curves
3. Demonstrate overfitting with high degree

**Hints**: Use `sklearn.preprocessing.PolynomialFeatures`. Start with degree=2, cross-validate higher degrees.

**Skills**: Feature creation, polynomial regression

---

### B20: Binning and Discretization
**Domain**: Feature Eng | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Convert continuous variables to categorical using equal-width binning, equal-frequency binning (quantiles), and custom bins. Binning can capture non-linear effects and handle outliers.

**Expected Deliverables**:
- Equal-width binner (N equal intervals)
- Equal-frequency binner (N quantiles)
- Custom bin boundaries
- When binning helps vs hurts

**Test Cases**:
1. Bin age into 5 equal-width groups
2. Bin income into quintiles
3. Compare binned vs continuous for tree model

**Hints**: Use `pd.cut()` for equal-width, `pd.qcut()` for quantiles. Decision trees do implicit binning.

**Skills**: Discretization, pandas cut/qcut

---

### B21: Log and Power Transformations
**Domain**: Feature Eng | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Apply log, square root, and Box-Cox transformations to reduce skewness and make distributions more Gaussian. Many ML algorithms perform better with normally distributed features.

**Mathematical Foundation**:
- Log: y = log(x + 1)
- Box-Cox: requires positive values, finds optimal λ

**Expected Deliverables**:
- Log1p transformation for skewed features
- Box-Cox with scipy
- Skewness before/after comparison

**Test Cases**:
1. Transform right-skewed income data
2. Find optimal Box-Cox lambda
3. Compare model performance with/without transformation

**Hints**: Use `np.log1p()` to handle zeros. `scipy.stats.boxcox()` for Box-Cox transition.

**Skills**: Power transformations, normality

---

### B22: Date and Time Feature Extraction
**Domain**: Feature Eng | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Extract meaningful features from datetime columns: year, month, day, day of week, hour, is_weekend, quarter, days_since_event. Temporal patterns are often highly predictive.

**Dataset**: Any time-stamped dataset (retail sales, web logs)

**Expected Deliverables**:
- Datetime parsing and extraction
- Cyclical encoding for hours/months
- Days since important date feature

**Test Cases**:
1. Extract hour-of-day for sales prediction
2. Create is_holiday binary feature
3. Cyclical encoding: sin/cos for month

**Hints**: Use `pd.to_datetime()`, `.dt` accessor. Cyclical encoding prevents December/January discontinuity.

**Skills**: Temporal features, pandas datetime

---

### B23: Text Feature Extraction Basics
**Domain**: Feature Eng | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Extract basic text features: character count, word count, average word length, punctuation count, uppercase ratio. These simple features can be predictive for text classification.

**Dataset**: IMDB reviews or tweet dataset

**Expected Deliverables**:
- Text statistics extraction
- Sentiment lexicon features
- Correlation with target variable

**Test Cases**:
1. Extract features from product reviews
2. Show which text features correlate with sentiment
3. Combine with bag-of-words features

**Hints**: Use string methods in pandas. Consider `textstat` library for readability scores.

**Skills**: Text preprocessing, feature engineering

---

### B24: Handling Imbalanced Data Detection
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Libraries

**Problem**: Detect and visualize class imbalance in classification datasets. Calculate imbalance ratio and understand its impact on model training and evaluation metrics.

**Dataset**: Credit fraud, churn, or any imbalanced dataset

**Expected Deliverables**:
- Class distribution visualization
- Imbalance ratio calculation
- Impact demonstration on accuracy vs F1

**Test Cases**:
1. Visualize 99:1 fraud vs non-fraud ratio
2. Show accuracy paradox (high accuracy, poor recall)
3. Calculate class weights

**Hints**: A model predicting majority class always gets 99% accuracy on 99:1 data. Focus on minority class metrics.

**Skills**: Imbalance detection, metric selection

---

### B25: Resampling - Undersampling
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Implement random undersampling and Tomek links for handling imbalanced datasets. Undersampling reduces majority class size to balance with minority class.

**Expected Deliverables**:
- Random undersampling
- Tomek links cleaning
- Impact on model performance

**Test Cases**:
1. Undersample to 1:1 ratio
2. Apply Tomek links
3. Compare model F1 scores

**Hints**: Use `imblearn.under_sampling.RandomUnderSampler`, `TomekLinks`. Undersampling loses information.

**Skills**: Undersampling techniques, imbalanced-learn

---

### B26: Resampling - Oversampling
**Domain**: Data Prep | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Implement random oversampling and SMOTE (Synthetic Minority Over-sampling Technique). Oversampling increases minority class size by duplicating or synthesizing new samples.

**Mathematical Foundation**:
- SMOTE: creates synthetic samples along lines connecting minority class neighbors

**Expected Deliverables**:
- Random oversampling
- SMOTE implementation
- Visualization of synthetic samples
- Comparison with undersampling

**Test Cases**:
1. Oversample to 1:1 ratio
2. Visualize SMOTE synthetic points
3. Compare model recall with different ratios

**Hints**: Use `imblearn.over_sampling.SMOTE`. Apply ONLY on training data, never on test set.

**Skills**: Oversampling, SMOTE, data augmentation

---

### B27: Cost-Sensitive Learning
**Domain**: Data Prep | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Apply class weights to penalize misclassification of minority class more heavily. This is often more effective than resampling and doesn't change the data distribution.

**Expected Deliverables**:
- Compute class weights inversely proportional to frequency
- Apply to sklearn classifiers
- Compare with resampling approaches

**Test Cases**:
1. Train with balanced class weights
2. Compare to SMOTE on same dataset
3. Tune class weights as hyperparameter

**Hints**: Use `class_weight='balanced'` in sklearn. Can also use custom {0: 1, 1: 10} weights.

**Skills**: Cost-sensitive learning, class weights

---

### B28: Data Leakage Detection
**Domain**: Data Prep | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Identify and prevent data leakage - when information from outside the training set leaks into the model. Learn common sources: target leakage, train-test contamination, temporal leakage.

**Expected Deliverables**:
- Checklist for data leakage detection
- Examples of each leakage type
- Proper preprocessing pipeline order

**Test Cases**:
1. Identify feature that contains future information
2. Show leakage from fitting scaler on full data
3. Demonstrate temporal leakage in time series

**Hints**: Always fit preprocessors on training data only. Features with perfect or near-perfect correlation with target are suspicious.

**Skills**: Data leakage prevention, proper validation

---

### B29: Pipeline Construction
**Domain**: Data Prep | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Build sklearn Pipelines to chain preprocessing steps and model training. Pipelines ensure all transformations are applied correctly during cross-validation and prevent data leakage.

**Expected Deliverables**:
- Pipeline with multiple preprocessing steps
- ColumnTransformer for different column types
- Integration with cross-validation

**Test Cases**:
1. Pipeline: impute → scale → model
2. Different preprocessing for numeric vs categorical
3. Grid search over pipeline parameters

**Hints**: Use `sklearn.pipeline.Pipeline`, `ColumnTransformer`. Prefix parameter names with step name in GridSearchCV.

**Skills**: sklearn pipelines, proper ML workflow

---

### B30: Feature Store Concepts
**Domain**: Data Prep | **Difficulty**: ★★★☆☆ | **Time**: 35 min
**Implementation**: Conceptual + Libraries

**Problem**: Understand feature store concepts: feature versioning, online/offline serving, feature reuse across models. Build a simple feature store using dictionary/database pattern.

**Expected Deliverables**:
- Simple feature store implementation
- Feature versioning approach
- Documentation of feature definitions

**Test Cases**:
1. Store and retrieve engineered features
2. Version control for feature changes
3. Serve features for real-time prediction

**Hints**: Libraries like Feast provide production feature stores. For learning, a dict-based approach suffices.

**Skills**: Feature management, MLOps foundations

---

## Section C: Linear Regression (C1-C25)

### C1: Simple Linear Regression from Scratch
**Domain**: Regression | **Difficulty**: ★★☆☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Implement simple linear regression (one feature) using the closed-form solution. Calculate slope and intercept, make predictions, and visualize the best-fit line. This is the foundational supervised learning algorithm.

**Mathematical Foundation**:
- Model: y = mx + b
- Slope: m = Σ(xᵢ - x̄)(yᵢ - ȳ) / Σ(xᵢ - x̄)²
- Intercept: b = ȳ - m × x̄

**Dataset**: Create synthetic data or use simple real dataset (e.g., height vs weight)

**Expected Deliverables**:
- LinearRegression class with fit() and predict()
- Visualization of data points and regression line
- Coefficient interpretation

**Test Cases**:
1. Perfect linear data: R² = 1.0
2. Noisy data: Verify coefficients are close to true values
3. Match sklearn LinearRegression results

**Hints**: Use vectorized operations for efficiency. The closed-form solution avoids iteration.

**Skills**: Linear regression fundamentals, closed-form solutions

---

### C2: Gradient Descent for Linear Regression
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: From Scratch

**Problem**: Implement linear regression using batch gradient descent. This iterative approach scales better than the normal equation for large datasets and introduces the optimization paradigm used in neural networks.

**Mathematical Foundation**:
- Loss: J(θ) = (1/2m) Σ(hθ(xᵢ) - yᵢ)²
- Gradient: ∂J/∂θⱼ = (1/m) Σ(hθ(xᵢ) - yᵢ) × xᵢⱼ
- Update: θⱼ := θⱼ - α × ∂J/∂θⱼ

**Expected Deliverables**:
- Gradient descent optimizer
- Learning curve (loss vs iterations)
- Convergence analysis for different learning rates

**Test Cases**:
1. Converge to same solution as closed-form
2. Show divergence with too-large learning rate
3. Plot cost function decreasing over iterations

**Hints**: Feature scaling is crucial for gradient descent convergence. Start with small α.

**Skills**: Gradient descent, optimization, learning curves

---

### C3: Stochastic and Mini-Batch Gradient Descent
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Implement stochastic gradient descent (SGD) and mini-batch gradient descent. Compare convergence speed and stability with batch gradient descent. SGD is essential for training on large datasets.

**Mathematical Foundation**:
- Batch: Use all samples per update
- SGD: Use 1 sample per update
- Mini-batch: Use batch_size samples per update

**Expected Deliverables**:
- SGD and mini-batch implementations
- Comparison of convergence behavior
- Noise in loss curves analysis

**Test Cases**:
1. SGD reaches approximate solution faster
2. Mini-batch balances speed and stability
3. Same final solution (approximately)

**Hints**: Shuffle data each epoch. Mini-batch size of 32-128 is common. Consider learning rate decay.

**Skills**: SGD variants, large-scale optimization

---

### C4: Multiple Linear Regression
**Domain**: Regression | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Extend to multiple features. Implement using matrix operations and compare with sklearn. Interpret coefficients to understand feature importance and direction of effect.

**Mathematical Foundation**:
- Model: y = Xθ where θ = [θ₀, θ₁, ..., θₙ]
- Normal equation: θ = (XᵀX)⁻¹Xᵀy

**Dataset**: Boston Housing or California Housing (scikit-learn)

**Expected Deliverables**:
- Matrix-based implementation
- Coefficient interpretation report
- Handling of intercept term (bias)

**Test Cases**:
1. Match sklearn results
2. Interpret which features increase/decrease target
3. Handle multicollinear features

**Hints**: Add column of ones for intercept. Use `np.linalg.pinv` for stability.

**Skills**: Multiple regression, matrix operations, interpretation

---

### C5: Polynomial Regression
**Domain**: Regression | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Fit non-linear relationships using polynomial features. Demonstrate underfitting (degree=1), good fit, and overfitting (high degree). This illustrates the bias-variance tradeoff.

**Mathematical Foundation**:
- Transform: x → [1, x, x², x³, ...]
- Fit linear regression on transformed features

**Dataset**: Create non-linear synthetic data (e.g., y = x² + noise)

**Expected Deliverables**:
- Polynomial feature generator
- Comparison of degrees 1, 2, 5, 10, 20
- Train vs test error plots

**Test Cases**:
1. Degree 2 fits parabolic data well
2. High degree overfits: low train error, high test error
3. Cross-validation for degree selection

**Hints**: Use `sklearn.preprocessing.PolynomialFeatures`. Watch for coefficient explosion with high degrees.

**Skills**: Polynomial regression, overfitting demonstration

---

### C6: Ridge Regression (L2 Regularization)
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Both

**Problem**: Implement Ridge regression that adds L2 penalty to prevent overfitting. Understand how lambda (alpha) controls regularization strength and shrinks coefficients toward zero.

**Mathematical Foundation**:
- Loss: J(θ) = MSE + λ Σθⱼ²
- Solution: θ = (XᵀX + λI)⁻¹Xᵀy

**Expected Deliverables**:
- Ridge regression from scratch
- Coefficient paths as α varies
- Cross-validation for α selection

**Test Cases**:
1. α=0 recovers ordinary least squares
2. Large α shrinks all coefficients toward zero
3. Select optimal α via cross-validation

**Hints**: Don't regularize the intercept. Use `sklearn.linear_model.Ridge` or `RidgeCV`.

**Skills**: Regularization, Ridge regression, hyperparameter tuning

---

### C7: Lasso Regression (L1 Regularization)
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Both

**Problem**: Implement Lasso regression that adds L1 penalty. Lasso performs feature selection by shrinking some coefficients exactly to zero. Compare sparsity of solutions with Ridge.

**Mathematical Foundation**:
- Loss: J(θ) = MSE + λ Σ|θⱼ|
- No closed-form; requires iterative optimization

**Expected Deliverables**:
- Lasso using coordinate descent or sklearn
- Comparison of Lasso vs Ridge coefficients
- Feature selection demonstration

**Test Cases**:
1. Show Lasso zeros out irrelevant features
2. Compare number of non-zero coefficients vs Ridge
3. When Lasso vs Ridge is preferred

**Hints**: Use `sklearn.linear_model.Lasso`. L1 is harder to optimize than L2 due to non-differentiability at 0.

**Skills**: L1 regularization, feature selection, sparse models

---

### C8: Elastic Net Regression
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Combine L1 and L2 regularization with Elastic Net. This balances Lasso's sparsity with Ridge's grouping effect for correlated features.

**Mathematical Foundation**:
- Loss: J(θ) = MSE + λ₁ Σ|θⱼ| + λ₂ Σθⱼ²
- l1_ratio controls L1 vs L2 balance

**Expected Deliverables**:
- Elastic Net with different l1_ratio values
- Comparison with pure Lasso and Ridge
- When Elastic Net is best choice

**Test Cases**:
1. l1_ratio=1 equals Lasso
2. l1_ratio=0 equals Ridge
3. Groups of correlated features

**Hints**: Use `sklearn.linear_model.ElasticNet`. Good default is l1_ratio=0.5.

**Skills**: Elastic Net, combined regularization

---

### C9: Regularization Path Analysis
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Plot coefficient paths showing how each coefficient changes as regularization strength increases. This visualization helps understand which features are most important and how regularization works.

**Expected Deliverables**:
- Ridge coefficient paths
- Lasso coefficient paths (showing zeros)
- Cross-validation error curves

**Test Cases**:
1. Visualize all coefficient paths on single plot
2. Identify which features are eliminated first
3. Find optimal regularization strength

**Hints**: Use `sklearn.linear_model.lasso_path()` and `ridge_path()`. Log scale for alpha axis.

**Skills**: Regularization visualization, model introspection

---

### C10: Cross-Validation for Model Selection
**Domain**: Regression | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Use k-fold cross-validation to select the best polynomial degree and regularization strength. Understand why test set should never be used for model selection.

**Expected Deliverables**:
- K-fold CV implementation from scratch
- Cross-validation scores for different models
- Learning curves with CV

**Test Cases**:
1. Select optimal polynomial degree
2. Select optimal Ridge alpha
3. Compare train score, CV score, test score

**Hints**: Use `sklearn.model_selection.cross_val_score`. Keep test set truly held out until final evaluation.

**Skills**: Cross-validation, model selection, proper evaluation

---

### C11: Regression on Real Dataset - House Prices
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Build end-to-end linear regression model for house price prediction. Apply all preprocessing techniques, feature engineering, regularization, and proper validation.

**Dataset**: Kaggle House Prices or California Housing

**Expected Deliverables**:
- Complete preprocessing pipeline
- Model comparison (Linear, Ridge, Lasso)
- Feature importance analysis
- Residual analysis

**Evaluation Criteria**: RMSE on validation set

**Test Cases**:
1. Beat naive baseline (mean prediction)
2. Compare regularized vs non-regularized
3. Identify most predictive features

**Hints**: Log-transform skewed target. Create interaction features. Use pipeline for reproducibility.

**Skills**: End-to-end project, regression best practices

---

### C12: Assumptions of Linear Regression
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Check and validate linear regression assumptions: linearity, independence, homoscedasticity, normality of residuals. Understand what happens when assumptions are violated.

**Expected Deliverables**:
- Residual plots for linearity check
- Q-Q plot for normality
- Breusch-Pagan test for homoscedasticity
- Durbin-Watson test for independence

**Test Cases**:
1. Identify non-linear relationship from residuals
2. Detect heteroscedasticity
3. Apply transformations to fix violations

**Hints**: Use `statsmodels` for diagnostic tests. Many assumption violations can be fixed with transformations.

**Skills**: Regression diagnostics, assumption checking

---

### C13: Residual Analysis
**Domain**: Regression | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Analyze residuals to understand model performance and identify patterns the model missed. Residual analysis reveals model weaknesses and data issues.

**Expected Deliverables**:
- Residual vs fitted values plot
- Residual vs each feature plots
- Histogram and Q-Q plot of residuals
- Identification of outliers

**Test Cases**:
1. Random scatter indicates good fit
2. Pattern indicates missing non-linearity
3. Funnel shape indicates heteroscedasticity

**Hints**: Good residuals should look like white noise. Patterns suggest model improvements.

**Skills**: Residual analysis, model diagnostics

---

### C14: Influential Points and Leverage
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Identify influential observations that disproportionately affect the regression line. Calculate leverage and Cook's distance to detect problematic points.

**Mathematical Foundation**:
- Leverage: Hat matrix diagonal hᵢᵢ
- Cook's Distance: measures change in all predictions if point removed

**Expected Deliverables**:
- Leverage calculation
- Cook's distance for each point
- Decision criteria for influential points

**Test Cases**:
1. Identify high-leverage outliers
2. Compare model with/without influential points
3. Decision on keeping vs removing

**Hints**: Use `statsmodels` get_influence(). High leverage + large residual = influential.

**Skills**: Influential point detection, regression diagnostics

---

### C15: Multicollinearity Detection
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Detect and handle multicollinearity when features are highly correlated. Calculate Variance Inflation Factor (VIF) and understand its impact on coefficient stability.

**Mathematical Foundation**:
- VIF = 1 / (1 - R²ⱼ) where R²ⱼ is R² regressing feature j on all others
- VIF > 5 or 10 suggests multicollinearity

**Expected Deliverables**:
- Correlation matrix heatmap
- VIF calculation for each feature
- Strategies to address multicollinearity

**Test Cases**:
1. Create perfectly collinear features
2. Show coefficient instability
3. Fix by removing features or using Ridge

**Hints**: Use `statsmodels.stats.outliers_influence.variance_inflation_factor`. Ridge naturally handles multicollinearity.

**Skills**: Multicollinearity, VIF, feature engineering

---

### C16: Weighted Least Squares
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Implement weighted least squares for heteroscedastic data where error variance differs across observations. Different observations get different weights inversely proportional to their variance.

**Mathematical Foundation**:
- Weighted loss: J = Σ wᵢ(yᵢ - ŷᵢ)²
- Give lower weight to high-variance observations

**Expected Deliverables**:
- WLS implementation from scratch
- Weight selection strategies
- Comparison with OLS on heteroscedastic data

**Test Cases**:
1. Improve predictions on heteroscedastic data
2. Weight by inverse variance
3. Compare standard errors

**Hints**: Use `sklearn.linear_model.LinearRegression(sample_weight=...)` or `statsmodels.WLS`.

**Skills**: Weighted regression, heteroscedasticity

---

### C17: Quantile Regression
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Predict conditional quantiles (e.g., median, 10th, 90th percentile) instead of just the mean. Quantile regression is robust to outliers and provides prediction intervals.

**Expected Deliverables**:
- Median regression (quantile=0.5)
- Multiple quantile predictions (0.1, 0.5, 0.9)
- Prediction interval visualization

**Test Cases**:
1. Median regression is robust to outliers
2. Quantile bands capture distribution
3. Asymmetric distributions

**Hints**: Use `sklearn.linear_model.QuantileRegressor` or `statsmodels.QuantReg`.

**Skills**: Quantile regression, robust regression

---

### C18: Locally Weighted Regression (LOWESS)
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Implement non-parametric locally weighted regression that fits different models in different regions of the data. LOWESS captures local patterns without assuming global linearity.

**Mathematical Foundation**:
- Weight each point by distance to query point
- Fit weighted regression locally
- No single global model

**Expected Deliverables**:
- LOWESS curve fitting
- Bandwidth (span) selection
- Comparison with polynomial regression

**Test Cases**:
1. Fit complex non-linear relationships
2. Effect of bandwidth parameter
3. Overfitting with small bandwidth

**Hints**: Use `statsmodels.nonparametric.lowess`. Larger span = smoother curve.

**Skills**: Non-parametric regression, local methods

---

### C19: Regression with Categorical Features
**Domain**: Regression | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Handle categorical variables in linear regression using one-hot encoding. Interpret coefficients relative to the reference category and understand the dummy variable trap.

**Expected Deliverables**:
- One-hot encoding integration
- Coefficient interpretation per category
- Reference category selection

**Test Cases**:
1. Add color feature (red, blue, green)
2. Interpret each category's effect
3. Combine numeric and categorical

**Hints**: Drop one category to avoid multicollinearity. Coefficients are differences from reference.

**Skills**: Categorical regression, interpretation

---

### C20: Log-Linear and Log-Log Models
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Apply logarithmic transformations to handle multiplicative relationships and interpret coefficients as percentage changes. Common in economics and business applications.

**Mathematical Foundation**:
- Log-linear: log(y) = β₀ + β₁x (β₁ = % change in y per unit x)
- Log-log: log(y) = β₀ + β₁log(x) (β₁ = elasticity)

**Expected Deliverables**:
- Log transformation of target
- Elasticity interpretation
- Back-transformation of predictions

**Test Cases**:
1. Exponential growth data → log-linear
2. Power law data → log-log
3. Interpret price elasticity

**Hints**: For log(y), predictions need to be exponentiated. Consider bias correction.

**Skills**: Log transformations, elasticity interpretation

---

### C21: Regression Confidence and Prediction Intervals
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Calculate confidence intervals for coefficients and prediction intervals for new observations. Understand the difference: CI for the mean prediction vs PI for individual prediction.

**Mathematical Foundation**:
- CI for coefficients: β̂ ± t × SE(β̂)
- PI is wider than CI due to individual variation

**Expected Deliverables**:
- Coefficient confidence intervals
- Prediction interval calculation
- Visualization of CI/PI bands

**Test Cases**:
1. 95% CI contains true coefficient (in simulation)
2. PI captures ~95% of observations
3. Show PI is wider than CI

**Hints**: Use `statsmodels` for full inference. `get_prediction(...)` gives intervals.

**Skills**: Statistical inference, uncertainty quantification

---

### C22: Robust Regression
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use robust regression methods (Huber, RANSAC, Theil-Sen) that are resistant to outliers. Compare with OLS on contaminated data.

**Expected Deliverables**:
- HuberRegressor for mild outliers
- RANSAC for extreme outliers
- Theil-Sen estimator
- Comparison on outlier dataset

**Test Cases**:
1. OLS fails with outliers
2. Robust methods recover true line
3. Compare breakdown points

**Hints**: Use `sklearn.linear_model.HuberRegressor`, `RANSACRegressor`, `TheilSenRegressor`.

**Skills**: Robust statistics, outlier handling

---

### C23: Feature Importance in Linear Models
**Domain**: Regression | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Determine feature importance using standardized coefficients and permutation importance. Raw coefficients are not directly comparable if features have different scales.

**Expected Deliverables**:
- Standardized (beta) coefficients
- Permutation importance calculation
- Feature ranking comparison

**Test Cases**:
1. Standardize then fit vs scale coefficients
2. Permutation importance on test set
3. Compare rankings across methods

**Hints**: Standardize features first for comparable coefficients. Use `sklearn.inspection.permutation_importance`.

**Skills**: Feature importance, model interpretation

---

### C24: Regression Model Comparison
**Domain**: Regression | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Compare multiple regression models using proper metrics and statistical tests. Use nested model comparison (F-test) and information criteria (AIC, BIC).

**Mathematical Foundation**:
- F-test for nested models
- AIC = n×log(SSE/n) + 2k
- BIC = n×log(SSE/n) + k×log(n)

**Expected Deliverables**:
- Model comparison table (R², Adj-R², AIC, BIC)
- Nested model F-test
- Selection based on parsimony

**Test Cases**:
1. Compare linear vs polynomial fit
2. Compare with/without feature groups
3. Use AIC/BIC to prevent overfitting

**Hints**: Use `statsmodels` for statistical tests. Lower AIC/BIC is better.

**Skills**: Model comparison, statistical testing

---

### C25: End-to-End Regression Project
**Domain**: Regression | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete a full regression project from data exploration to model deployment. Document all decisions, handle real-world data issues, and create reproducible pipeline.

**Dataset**: Choose from: Airbnb Prices, Car Prices, Energy Consumption

**Expected Deliverables**:
- EDA notebook with visualizations
- Feature engineering documentation
- Model comparison with validation
- Final model pipeline
- Business insights report

**Evaluation Criteria**: 
- RMSE/MAE on held-out test set
- Code quality and reproducibility
- Insight quality and presentation

**Test Cases**:
1. Beat baseline by significant margin
2. Interpretable feature importance
3. Residuals show no systematic patterns

**Hints**: Spend 50% time on EDA and feature engineering. Document assumptions and decisions.

**Skills**: End-to-end ML project, best practices, documentation

---

## Section D: Logistic Regression & Classification (D1-D25)

### D1: Binary Logistic Regression from Scratch
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: From Scratch

**Problem**: Implement binary logistic regression using gradient descent. Compute probabilities using the sigmoid function and optimize the log-loss (cross-entropy) objective. This is the foundational classification algorithm.

**Mathematical Foundation**:
- Sigmoid: σ(z) = 1 / (1 + e⁻ᶻ)
- Probability: P(y=1|x) = σ(wᵀx + b)
- Loss: J = -(1/m) Σ[yᵢ log(ŷᵢ) + (1-yᵢ) log(1-ŷᵢ)]

**Dataset**: Synthetic 2D classification or Breast Cancer dataset

**Expected Deliverables**:
- LogisticRegression class with fit(), predict(), predict_proba()
- Decision boundary visualization
- Convergence plot (loss vs iterations)

**Test Cases**:
1. Match sklearn LogisticRegression results
2. Probability outputs sum to 1
3. Decision boundary separates classes

**Hints**: Use log-loss, not MSE. Gradient is similar to linear regression but with sigmoid.

**Skills**: Logistic regression fundamentals, gradient descent for classification

---

### D2: Multi-Class Logistic Regression
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Both

**Problem**: Extend to multi-class classification using One-vs-Rest (OvR) and softmax (multinomial) approaches. Understand when each method is appropriate.

**Mathematical Foundation**:
- OvR: Train K binary classifiers
- Softmax: P(y=k|x) = exp(wₖᵀx) / Σexp(wⱼᵀx)

**Dataset**: Iris or MNIST digits

**Expected Deliverables**:
- One-vs-Rest implementation
- Softmax regression implementation
- Comparison of both approaches

**Test Cases**:
1. OvR: K classifiers for K classes
2. Softmax: single model, K outputs
3. Compare accuracy on Iris dataset

**Hints**: Use `multi_class='ovr'` vs `'multinomial'` in sklearn. Softmax is preferable when classes are mutually exclusive.

**Skills**: Multi-class classification, softmax

---

### D3: Sigmoid and Softmax Functions
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: From Scratch

**Problem**: Implement sigmoid and softmax functions with numerical stability. Understand their derivatives for backpropagation and their role in converting scores to probabilities.

**Mathematical Foundation**:
- Sigmoid derivative: σ(z)(1 - σ(z))
- Softmax derivative: Jacobian matrix

**Expected Deliverables**:
- Numerically stable implementations
- Derivative calculations
- Gradient verification

**Test Cases**:
1. Large inputs don't cause overflow
2. Outputs sum to 1 (softmax)
3. Verify derivatives numerically

**Hints**: For sigmoid, use max(0, z) trick. For softmax, subtract max before exp.

**Skills**: Activation functions, numerical stability, derivatives

---

### D4: Cross-Entropy Loss
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: From Scratch

**Problem**: Implement binary and categorical cross-entropy loss functions. Understand why cross-entropy is preferred over MSE for classification and its gradient for optimization.

**Mathematical Foundation**:
- Binary: L = -[y log(p) + (1-y) log(1-p)]
- Categorical: L = -Σ yₖ log(pₖ)

**Expected Deliverables**:
- Cross-entropy loss functions
- Gradient calculations
- Comparison with MSE for classification

**Test Cases**:
1. Perfect prediction: loss = 0
2. Confident wrong prediction: high loss
3. Gradient pushes probabilities toward correct class

**Hints**: Add small epsilon to prevent log(0). Cross-entropy gradient is simpler than MSE for classification.

**Skills**: Loss functions, classification optimization

---

### D5: Regularized Logistic Regression
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Add L1 (Lasso) and L2 (Ridge) regularization to logistic regression. Understand the effect on coefficients and when to use each.

**Mathematical Foundation**:
- L2: J = CrossEntropy + λ Σwⱼ²
- L1: J = CrossEntropy + λ Σ|wⱼ|

**Expected Deliverables**:
- L2 regularized implementation
- L1 for feature selection
- Regularization path visualization

**Test Cases**:
1. Large λ shrinks coefficients
2. L1 produces sparse solutions
3. CV for λ selection

**Hints**: Use `C` parameter in sklearn (C = 1/λ). Larger C = less regularization.

**Skills**: Regularization for classification, hyperparameter tuning

---

### D6: Classification Threshold Selection
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Understand that 0.5 is not always the optimal classification threshold. Learn to select thresholds based on business requirements, class imbalance, and cost considerations.

**Expected Deliverables**:
- Precision-Recall curve with thresholds
- ROC curve with thresholds
- Threshold selection based on F1 or cost

**Test Cases**:
1. Imbalanced data: optimal threshold ≠ 0.5
2. High-recall requirement: lower threshold
3. High-precision requirement: higher threshold

**Hints**: Use `precision_recall_curve()` and `roc_curve()` from sklearn. Plot threshold on curves.

**Skills**: Threshold optimization, business requirements

---

### D7: Confusion Matrix Analysis
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Compute and interpret the confusion matrix for binary and multi-class classification. Extract all related metrics: TP, TN, FP, FN, and derived measures.

**Expected Deliverables**:
- Confusion matrix from scratch
- Heatmap visualization
- Multi-class confusion matrix

**Test Cases**:
1. Perfect classifier: diagonal matrix
2. Calculate metrics from matrix
3. Identify which class is most confused

**Hints**: Use `sklearn.metrics.confusion_matrix`. Rows are actual, columns are predicted (sklearn convention).

**Skills**: Confusion matrix, classification diagnostics

---

### D8: Accuracy, Precision, Recall, F1
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Compute all fundamental classification metrics from scratch. Understand when each metric is most appropriate and the tradeoffs between precision and recall.

**Mathematical Foundation**:
- Precision: TP / (TP + FP)
- Recall: TP / (TP + FN)
- F1: 2 × (P × R) / (P + R)

**Expected Deliverables**:
- All metrics from scratch
- Macro vs micro averaging for multi-class
- When to use each metric

**Test Cases**:
1. Verify against sklearn metrics
2. Compare on imbalanced dataset
3. Show accuracy paradox

**Hints**: Accuracy is misleading for imbalanced data. F1 balances precision and recall.

**Skills**: Classification metrics, evaluation

---

### D9: ROC Curve and AUC
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Compute and interpret ROC (Receiver Operating Characteristic) curve and AUC (Area Under Curve). Understand TPR vs FPR tradeoff across all thresholds.

**Mathematical Foundation**:
- TPR (Recall) = TP / (TP + FN)
- FPR = FP / (FP + TN)
- AUC: probability that model ranks random positive higher than random negative

**Expected Deliverables**:
- ROC curve computation
- AUC calculation (trapezoidal rule)
- Model comparison using ROC

**Test Cases**:
1. Random classifier: AUC = 0.5
2. Perfect classifier: AUC = 1.0
3. Compare multiple models on same ROC plot

**Hints**: Use `sklearn.metrics.roc_curve`, `roc_auc_score`. AUC is threshold-independent.

**Skills**: ROC-AUC, model evaluation

---

### D10: Precision-Recall Curve
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Compute and interpret the Precision-Recall curve. Understand when PR curve is more informative than ROC, especially for imbalanced datasets.

**Mathematical Foundation**:
- Average Precision (AP): area under PR curve
- F1 score: harmonic mean of precision and recall

**Expected Deliverables**:
- PR curve computation
- Average Precision calculation
- Comparison with ROC for imbalanced data

**Test Cases**:
1. High recall achievable only with low precision
2. AP on highly imbalanced data
3. Compare ROC-AUC vs AP on same dataset

**Hints**: Use `precision_recall_curve`, `average_precision_score`. PR curve is preferred for rare positive class.

**Skills**: Precision-Recall analysis, imbalanced evaluation

---

### D11: Log-Loss Evaluation
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Both

**Problem**: Use log-loss (cross-entropy loss) as an evaluation metric that considers prediction confidence. Understand why well-calibrated probabilities result in lower log-loss.

**Mathematical Foundation**:
- Log-loss: -1/n Σ[yᵢ log(pᵢ) + (1-yᵢ) log(1-pᵢ)]

**Expected Deliverables**:
- Log-loss calculation
- Comparison with accuracy
- Calibration impact on log-loss

**Test Cases**:
1. Confident correct predictions: low log-loss
2. Confident wrong predictions: high log-loss (heavily penalized)
3. Uncertain predictions: moderate log-loss

**Hints**: Use `sklearn.metrics.log_loss`. Log-loss rewards well-calibrated probabilities.

**Skills**: Probabilistic evaluation, calibration importance

---

### D12: Probability Calibration
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Calibrate classifier probabilities using Platt scaling and isotonic regression. Understand why some classifiers (like Naive Bayes, SVM) need calibration.

**Expected Deliverables**:
- Reliability diagram (calibration curve)
- Platt scaling implementation
- Isotonic calibration
- Before/after calibration comparison

**Test Cases**:
1. Show poorly calibrated classifier
2. Improve calibration with CalibratedClassifierCV
3. Verify with reliability diagram

**Hints**: Use `sklearn.calibration.CalibratedClassifierCV` and `calibration_curve`.

**Skills**: Probability calibration, reliable predictions

---

### D13: Decision Boundary Visualization
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Visualize decision boundaries for 2D classification problems. Understand how different algorithms create different boundary shapes.

**Expected Deliverables**:
- Contour plot of decision regions
- Probability heatmap
- Comparison of linear vs non-linear boundaries

**Test Cases**:
1. Linear boundary for logistic regression
2. Non-linear boundary for polynomial features
3. Show regularization effect on boundary smoothness

**Hints**: Create meshgrid, predict on all points, use contourf for visualization.

**Skills**: Visualization, model behavior understanding

---

### D14: Classification with Imbalanced Data
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Apply strategies for imbalanced classification: class weights, threshold adjustment, and evaluation with appropriate metrics. Avoid the accuracy trap.

**Dataset**: Credit Card Fraud, Churn, or Medical Diagnosis

**Expected Deliverables**:
- Baseline without addressing imbalance
- Class weight adjustment
- Threshold optimization for F1/recall
- Comprehensive metric report

**Test Cases**:
1. Show accuracy is misleading
2. Improve recall with class weights
3. ROC-AUC vs PR-AUC comparison

**Hints**: Use `class_weight='balanced'`. Focus on minority class metrics.

**Skills**: Imbalanced learning, metric selection

---

### D15: Feature Importance in Logistic Regression
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Interpret logistic regression coefficients as feature importance. Understand odds ratios and the effect of standardization on comparability.

**Mathematical Foundation**:
- Odds ratio: exp(coefficient)
- Standardized coefficients for comparison

**Expected Deliverables**:
- Coefficient interpretation
- Odds ratio calculation
- Standardized coefficient ranking

**Test Cases**:
1. Positive coefficient increases probability
2. Odds ratio interpretation
3. Compare importance across features

**Hints**: Standardize features for comparable coefficients. Use `np.exp(coef)` for odds ratio.

**Skills**: Model interpretation, odds ratios

---

### D16: Classification on Text Data
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 60 min
**Implementation**: Libraries

**Problem**: Apply logistic regression to text classification using bag-of-words or TF-IDF features. Build a spam classifier or sentiment analyzer.

**Dataset**: SMS Spam, IMDB Reviews, or 20 Newsgroups

**Expected Deliverables**:
- Text vectorization (CountVectorizer, TF-IDF)
- Logistic regression pipeline
- Top predictive words analysis

**Test Cases**:
1. Classify spam vs ham
2. Identify most predictive words per class
3. Compare CountVectorizer vs TF-IDF

**Hints**: Use sklearn pipelines. TF-IDF reduces common word dominance.

**Skills**: Text classification, NLP basics

---

### D17: Classification on Tabular Data Project
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Complete end-to-end classification project on tabular data. Apply all preprocessing, handle imbalance, optimize threshold, and report comprehensive metrics.

**Dataset**: Adult Income, Titanic, or Heart Disease

**Expected Deliverables**:
- Data preprocessing pipeline
- Model training and validation
- Threshold optimization
- Comprehensive evaluation report

**Evaluation Criteria**: F1-score, ROC-AUC on test set

**Test Cases**:
1. Beat baseline significantly
2. Handle missing values and categories
3. Interpret feature importance

**Hints**: Use stratified split. Consider class weights. Report multiple metrics.

**Skills**: End-to-end classification project

---

### D18: Binary vs Multi-Label Classification
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Distinguish between multi-class (one label) and multi-label (multiple labels) classification. Implement multi-label classification where each sample can belong to multiple classes.

**Dataset**: Movie genres, document tags

**Expected Deliverables**:
- Problem type identification
- MultiLabelBinarizer usage
- Multi-label metrics (subset accuracy, hamming loss)

**Test Cases**:
1. One movie can have multiple genres
2. Evaluate with hamming loss
3. Per-label vs overall metrics

**Hints**: Use `sklearn.preprocessing.MultiLabelBinarizer`. Each class gets its own binary classifier.

**Skills**: Multi-label classification, appropriate metrics

---

### D19: Cost-Sensitive Classification
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Implement cost-sensitive classification where different types of errors have different costs. Optimize for minimum expected cost rather than accuracy.

**Mathematical Foundation**:
- Expected cost: Σ P(ŷ|x) × Cost(ŷ, y)
- False positive vs false negative costs

**Expected Deliverables**:
- Cost matrix definition
- Threshold selection based on cost
- Cost-sensitive decision making

**Test Cases**:
1. Medical: FN (miss disease) >> FP
2. Spam: FP (miss email) >> FN
3. Optimal threshold changes with cost ratio

**Hints**: Adjust threshold based on cost ratio. Use sample weights for different costs.

**Skills**: Cost-sensitive learning, decision theory

---

### D20: Cross-Validation for Classification
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Both

**Problem**: Apply stratified k-fold cross-validation to ensure class proportions are maintained in each fold. Use cross-validation for model selection and hyperparameter tuning.

**Expected Deliverables**:
- Stratified k-fold from scratch
- Cross-validation score distribution
- Hyperparameter selection with CV

**Test Cases**:
1. Verify class proportions in each fold
2. Compare with random k-fold on imbalanced data
3. Select best regularization strength

**Hints**: Use `StratifiedKFold`, `cross_val_score`. Stratification is crucial for imbalanced data.

**Skills**: Stratified validation, proper model selection

---

### D21: Learning Curves for Classification
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Plot learning curves showing training and validation performance as training set size increases. Diagnose high bias (underfitting) vs high variance (overfitting).

**Expected Deliverables**:
- Learning curve plot
- Diagnosis of bias vs variance
- Recommendations based on curves

**Test Cases**:
1. Underfitting: both scores low and converged
2. Overfitting: gap between train and val
3. Good fit: both scores high and converged

**Hints**: Use `sklearn.model_selection.learning_curve`. More data helps variance, not bias.

**Skills**: Learning curves, debugging models

---

### D22: Hyperparameter Tuning for Classification
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Use grid search and random search to tune logistic regression hyperparameters (C, penalty, solver). Understand the search space and computational tradeoffs.

**Expected Deliverables**:
- GridSearchCV implementation
- RandomizedSearchCV comparison
- Best parameters and validation scores

**Test Cases**:
1. Find optimal C value
2. Compare grid vs random search efficiency
3. Visualize parameter sensitivity

**Hints**: Use `GridSearchCV`, `RandomizedSearchCV`. Log scale for C. Time both approaches.

**Skills**: Hyperparameter tuning, search strategies

---

### D23: Model Persistence and Deployment
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Save trained classification models and preprocessing pipelines. Load and use for predictions on new data. Understand version compatibility issues.

**Expected Deliverables**:
- Save model with joblib/pickle
- Save entire pipeline
- Load and predict on new data

**Test Cases**:
1. Save and load produces same predictions
2. Pipeline includes preprocessing
3. Handle new data with same transformations

**Hints**: Use `joblib.dump` and `joblib.load`. Save entire pipeline, not just model.

**Skills**: Model serialization, deployment basics

---

### D24: Classification Report and Error Analysis
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Generate comprehensive classification reports and perform error analysis. Identify patterns in misclassified samples to improve the model.

**Expected Deliverables**:
- classification_report interpretation
- Analysis of misclassified samples
- Feature patterns in errors
- Improvement recommendations

**Test Cases**:
1. Identify worst-performing class
2. Find common characteristics in errors
3. Suggest feature engineering improvements

**Hints**: Use `classification_report`. Plot misclassified samples. Look for edge cases.

**Skills**: Error analysis, model improvement

---

### D25: Binary Classification Capstone
**Domain**: Classification | **Difficulty**: ★★★★☆ | **Time**: 120 min
**Implementation**: Libraries

**Problem**: Complete a production-quality binary classification project with business context. Include all stages from EDA to deployment-ready pipeline with comprehensive documentation.

**Dataset**: Choose from: Customer Churn, Credit Default, Disease Diagnosis

**Expected Deliverables**:
- Business problem definition
- Comprehensive EDA
- Feature engineering documentation
- Model selection and validation
- Threshold optimization for business goal
- Final pipeline and predictions
- Business insights presentation

**Evaluation Criteria**: 
- Appropriate metric for business problem
- Code quality and reproducibility
- Documentation and presentation

**Test Cases**:
1. Clear improvement over baseline
2. Appropriate handling of imbalance
3. Actionable business insights

**Hints**: Define success metric with business in mind. Document all decisions. Create reproducible pipeline.

**Skills**: End-to-end project, business integration

---

## Section E: k-Nearest Neighbors (E1-E20)

### E1: k-NN Classifier from Scratch
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 50 min
**Implementation**: From Scratch

**Problem**: Implement k-Nearest Neighbors classifier using Euclidean distance. This instance-based learning algorithm stores all training data and makes predictions by finding the k closest training examples.

**Mathematical Foundation**:
- Euclidean distance: d = √(Σ(xᵢ - yᵢ)²)
- Majority voting among k neighbors

**Dataset**: Iris or synthetic 2D classification data

**Expected Deliverables**:
- KNNClassifier class with fit() and predict()
- Distance computation
- Majority voting implementation

**Test Cases**:
1. Match sklearn KNeighborsClassifier results
2. k=1 memorizes training data perfectly
3. Visualize decision boundaries

**Hints**: Use a list to store training data. Sort distances to find k nearest.

**Skills**: k-NN fundamentals, instance-based learning

---

### E2: k-NN Regressor from Scratch
**Domain**: Regression | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: From Scratch

**Problem**: Extend k-NN to regression by predicting the average of k nearest neighbors instead of majority voting. Handle both uniform and distance-weighted averaging.

**Expected Deliverables**:
- KNNRegressor class
- Uniform vs weighted averaging
- Comparison with sklearn

**Test Cases**:
1. k=1 exactly reproduces training targets
2. Larger k produces smoother predictions
3. Distance weighting improves accuracy

**Hints**: For weighted average, use 1/distance as weights. Handle zero distance specially.

**Skills**: k-NN for regression, weighted predictions

---

### E3: Choosing Optimal k Value
**Domain**: Classification/Regression | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Select the optimal k using cross-validation. Understand the bias-variance tradeoff: small k = high variance, large k = high bias. Plot k vs error curve.

**Expected Deliverables**:
- k vs accuracy/error plot
- Cross-validation for k selection
- Elbow point identification

**Test Cases**:
1. k=1 overfits (high train, low test accuracy)
2. Very large k underfits
3. Find optimal k using CV

**Hints**: Try odd k values to avoid ties. Common range is k=1 to √n.

**Skills**: Hyperparameter selection, bias-variance tradeoff

---

### E4: Distance Metrics Comparison
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Compare k-NN performance with different distance metrics: Euclidean, Manhattan, Chebyshev, Minkowski. Understand when each metric is most appropriate.

**Expected Deliverables**:
- k-NN with different metrics
- Accuracy comparison table
- Visualization of distance contours

**Test Cases**:
1. Euclidean vs Manhattan on same data
2. Effect of Minkowski p parameter
3. When Manhattan outperforms Euclidean

**Hints**: Use `metric` parameter in sklearn. Manhattan can be better for high-dimensional sparse data.

**Skills**: Distance metrics, metric selection

---

### E5: Feature Scaling for k-NN
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Demonstrate why feature scaling is critical for k-NN. Without scaling, features with larger magnitudes dominate distance calculations.

**Expected Deliverables**:
- k-NN without scaling
- k-NN with StandardScaler
- k-NN with MinMaxScaler
- Accuracy comparison

**Test Cases**:
1. Show distance dominated by large-scale feature
2. Significant accuracy improvement with scaling
3. StandardScaler vs MinMaxScaler comparison

**Hints**: Always scale features for k-NN. Use pipeline to avoid data leakage.

**Skills**: Feature scaling importance, preprocessing for k-NN

---

### E6: Weighted k-NN
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Implement distance-weighted k-NN where closer neighbors have more influence on the prediction. This often improves performance over uniform weighting.

**Mathematical Foundation**:
- Weight: wᵢ = 1 / dᵢ (or 1 / dᵢ²)
- Weighted vote: Σ wᵢ × I(yᵢ = c) for each class c

**Expected Deliverables**:
- Weighted voting implementation
- Comparison with uniform voting
- Effect on decision boundaries

**Test Cases**:
1. Uniform vs distance weighting accuracy
2. Show smoother boundaries with weighting
3. Handle zero-distance case

**Hints**: Use `weights='distance'` in sklearn. Very close points get very high weight.

**Skills**: Weighted k-NN, improved predictions

---

### E7: k-NN for High-Dimensional Data
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Understand the curse of dimensionality: as dimensions increase, all points become equidistant, making k-NN ineffective. Apply dimensionality reduction before k-NN.

**Expected Deliverables**:
- k-NN accuracy vs dimensionality
- PCA + k-NN pipeline
- Demonstration of distance concentration

**Test Cases**:
1. k-NN performance degrades with random features
2. PCA improves performance on high-d data
3. Show distance variance decreases with d

**Hints**: Curse of dimensionality is fundamental limitation. Use feature selection or PCA.

**Skills**: Curse of dimensionality, dimensionality reduction

---

### E8: Approximate Nearest Neighbors
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: For large datasets, exact k-NN is slow (O(n×d) per query). Use approximate nearest neighbor algorithms (ball tree, KD-tree, LSH) for faster queries.

**Expected Deliverables**:
- Comparison of brute force vs ball/KD tree
- Query time benchmarks
- Accuracy vs speed tradeoff

**Test Cases**:
1. Speed comparison on large dataset
2. Accuracy with approximate methods
3. When to use each algorithm

**Hints**: Use `algorithm` parameter in sklearn: 'ball_tree', 'kd_tree', 'brute'. KD-tree good for low d.

**Skills**: Efficient k-NN, tree-based search

---

### E9: k-NN for Imbalanced Data
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Handle class imbalance in k-NN which inherently favors majority classes in voting. Apply resampling, class weights, or modified voting strategies.

**Expected Deliverables**:
- Baseline k-NN on imbalanced data
- With SMOTE preprocessing
- Weighted voting by class frequency

**Test Cases**:
1. k-NN fails on 95:5 imbalanced data
2. SMOTE improves minority class recall
3. Compare different strategies

**Hints**: Combine with `imblearn`. Consider distance-weighted + class-weighted combination.

**Skills**: Imbalanced k-NN, resampling

---

### E10: k-NN Decision Boundary Visualization
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Visualize k-NN decision boundaries for different k values and distance metrics. Understand how k affects boundary smoothness.

**Expected Deliverables**:
- Decision boundary plots for k=1, 5, 15, 50
- Comparison of different metrics
- Probability contours

**Test Cases**:
1. k=1 creates jagged boundaries
2. Large k creates smooth boundaries
3. Show boundaries match training labels for k=1

**Hints**: Create meshgrid, predict on all points. Use filled contour plots.

**Skills**: Visualization, model behavior

---

### E11: k-NN for Anomaly Detection
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Use k-NN distance to the k-th nearest neighbor as an anomaly score. Points far from their neighbors are likely anomalies.

**Expected Deliverables**:
- k-NN distance anomaly scorer
- Threshold selection for anomalies
- Comparison with other anomaly methods

**Test Cases**:
1. Detect synthetic outliers
2. Compare with Isolation Forest
3. ROC-AUC for anomaly detection

**Hints**: Use `NearestNeighbors` to get distances. Larger distance = more anomalous.

**Skills**: Anomaly detection with k-NN

---

### E12: Local Outlier Factor (LOF)
**Domain**: Anomaly Detection | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Implement Local Outlier Factor which compares local density of a point to its neighbors. Points with lower density than neighbors are outliers.

**Mathematical Foundation**:
- Local reachability density
- LOF = average ratio of neighbor densities to point density

**Expected Deliverables**:
- LOF calculation understanding
- sklearn LOF usage
- Visualization of LOF scores

**Test Cases**:
1. Detect local anomalies (outliers in sparse regions)
2. LOF handles varying density clusters
3. Compare with global outlier detection

**Hints**: Use `sklearn.neighbors.LocalOutlierFactor`. LOF detects local anomalies better than global methods.

**Skills**: Local outlier detection, density-based methods

---

### E13: k-NN for Missing Value Imputation
**Domain**: Data Preprocessing | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use k-NN to impute missing values by finding similar complete samples and using their values. This is often more accurate than mean/median imputation.

**Expected Deliverables**:
- KNNImputer usage
- Comparison with simple imputation
- Effect of k on imputation quality

**Test Cases**:
1. Compare RMSE of imputed values to true values
2. k-NN imputation vs mean imputation
3. Effect of proportion of missing data

**Hints**: Use `sklearn.impute.KNNImputer`. Scale features before imputation.

**Skills**: k-NN imputation, missing data handling

---

### E14: k-NN for Recommender Systems
**Domain**: Recommendation | **Difficulty**: ★★★☆☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Build a simple user-based or item-based collaborative filtering recommender using k-NN. Find similar users/items and recommend based on their preferences.

**Dataset**: MovieLens small or synthetic ratings

**Expected Deliverables**:
- User-user similarity matrix
- k-NN for finding similar users
- Prediction of unseen ratings

**Test Cases**:
1. Find 5 most similar users
2. Predict rating for unseen movie
3. Evaluate with RMSE

**Hints**: Use `NearestNeighbors` on user-item matrix. Handle sparse matrices efficiently.

**Skills**: Collaborative filtering, recommendation basics

---

### E15: k-NN vs Radius-Based Neighbors
**Domain**: Classification | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Compare k-NN (fixed number of neighbors) with radius-based neighbors (all points within radius). Understand when each approach is preferred.

**Expected Deliverables**:
- RadiusNeighborsClassifier usage
- Comparison with KNeighborsClassifier
- Handling of empty neighborhoods

**Test Cases**:
1. Varying density data: radius vs k performance
2. Handle points with no neighbors in radius
3. When radius-based is preferred

**Hints**: Use `RadiusNeighborsClassifier`. Handle outlier_label for empty neighborhoods.

**Skills**: Radius-based methods, neighbor selection strategies

---

### E16: k-NN Time Complexity Analysis
**Domain**: Theory | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Conceptual + Code

**Problem**: Analyze time and space complexity of k-NN. Understand why k-NN is "lazy learning" and the tradeoffs of storing all training data.

**Expected Deliverables**:
- Time complexity analysis (train/predict)
- Space complexity analysis
- Benchmark with varying n and d

**Test Cases**:
1. O(1) training time
2. O(n×d) prediction time (brute force)
3. Show prediction time scaling

**Hints**: k-NN trades fast training for slow prediction. Compare with "eager" learners.

**Skills**: Algorithm analysis, complexity understanding

---

### E17: k-NN with Categorical Features
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Apply k-NN to data with categorical features using appropriate distance metrics (Hamming, Gower) or encoding strategies.

**Expected Deliverables**:
- One-hot encoding approach
- Hamming distance for binary features
- Gower distance for mixed types

**Test Cases**:
1. k-NN on purely categorical data
2. Mixed categorical and numeric features
3. Compare encoding strategies

**Hints**: One-hot encode then use Euclidean. Consider `gower` distance for mixed data.

**Skills**: Categorical distance metrics, mixed data handling

---

### E18: Condensed k-NN and Prototype Selection
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Reduce training set size by keeping only essential prototypes (condensed nearest neighbors) or editing out noisy samples (edited nearest neighbors).

**Expected Deliverables**:
- Condensed NN implementation concept
- Training set size reduction
- Accuracy comparison

**Test Cases**:
1. Reduce training set by 50%+ with minimal accuracy loss
2. Remove noisy samples
3. Speed improvement at prediction time

**Hints**: Keep border points, remove interior points. This is a form of data compression.

**Skills**: Prototype selection, instance reduction

---

### E19: k-NN Ensemble Methods
**Domain**: Classification | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Combine multiple k-NN classifiers using bagging or different distance metrics. Ensemble can improve stability and accuracy.

**Expected Deliverables**:
- Bagging with k-NN
- Multi-metric ensemble
- Accuracy improvement analysis

**Test Cases**:
1. Single k-NN vs bagged k-NN
2. Combine Euclidean and Manhattan k-NN
3. Variance reduction with ensemble

**Hints**: Use `BaggingClassifier` with k-NN base. Multiple metrics can capture different patterns.

**Skills**: k-NN ensembles, variance reduction

---

### E20: k-NN Capstone Project
**Domain**: Classification/Regression | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Complete a comprehensive k-NN project including preprocessing, parameter tuning, feature engineering, and comparison with other algorithms.

**Dataset**: Wine Quality, Digits, or custom dataset

**Expected Deliverables**:
- Data exploration and preprocessing
- Feature scaling and selection
- k and metric optimization
- Performance comparison with logistic regression
- Error analysis and interpretation

**Evaluation Criteria**: Accuracy/RMSE improvement over baseline

**Test Cases**:
1. Beat baseline significantly
2. Justify k and metric choices
3. Compare with parametric models

**Hints**: k-NN can outperform linear models on non-linear problems. Visualize decision boundaries.

**Skills**: End-to-end k-NN project

---

## Section F: Evaluation Metrics & Validation (F1-F25)

### F1: Train-Test Split
**Domain**: Validation | **Difficulty**: ★☆☆☆☆ | **Time**: 25 min
**Implementation**: Both

**Problem**: Implement train-test split from scratch and compare with sklearn. Understand random state for reproducibility, test size selection, and stratification for classification.

**Expected Deliverables**:
- Random split implementation
- Stratified split for classification
- Effect of test size on evaluation variance

**Test Cases**:
1. 80-20 split preserves class ratios (stratified)
2. Random state ensures reproducibility
3. Smaller test sets have higher variance

**Hints**: Use `sklearn.model_selection.train_test_split`. Always set random_state for reproducibility.

**Skills**: Data splitting, reproducibility

---

### F2: K-Fold Cross-Validation from Scratch
**Domain**: Validation | **Difficulty**: ★★☆☆☆ | **Time**: 45 min
**Implementation**: From Scratch

**Problem**: Implement k-fold cross-validation from scratch. Understand how each fold is used for validation exactly once, providing more robust performance estimates than single split.

**Mathematical Foundation**:
- K folds, K iterations
- Each sample in validation exactly once
- Final score = average of K scores

**Expected Deliverables**:
- k-fold generator yielding train/val indices
- Cross-validation score calculation
- Comparison with single split

**Test Cases**:
1. Each sample appears in validation exactly once
2. K=5 gives 5 different train/val splits
3. CV score variance vs single split variance

**Hints**: Shuffle data before splitting. Track which indices go to which fold.

**Skills**: Cross-validation implementation

---

### F3: Stratified K-Fold for Classification
**Domain**: Validation | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Ensure each fold maintains the same class distribution as the full dataset. Critical for imbalanced datasets where random folds might miss minority classes entirely.

**Expected Deliverables**:
- Stratified k-fold implementation
- Class distribution verification in each fold
- Comparison with regular k-fold on imbalanced data

**Test Cases**:
1. Each fold has same class proportions
2. Regular k-fold can have folds missing classes
3. CV scores are more stable with stratification

**Hints**: Use `StratifiedKFold`. Always stratify for classification tasks.

**Skills**: Stratified validation, imbalanced data handling

---

### F4: Leave-One-Out Cross-Validation
**Domain**: Validation | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Libraries

**Problem**: Implement LOOCV where each sample is used as validation once. Understand when LOOCV is appropriate (small datasets) and its computational cost.

**Expected Deliverables**:
- LOOCV implementation
- Comparison with k-fold (k=5, 10)
- Computational cost analysis

**Test Cases**:
1. n iterations for n samples
2. Compare with k-fold on small dataset
3. Show high variance of LOOCV

**Hints**: Use `LeaveOneOut`. LOOCV has high variance due to similar training sets.

**Skills**: LOOCV, small dataset validation

---

### F5: Time Series Split
**Domain**: Validation | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use TimeSeriesSplit for temporal data where future data cannot be used to predict past. Understand why random splits cause data leakage in time series.

**Expected Deliverables**:
- TimeSeriesSplit visualization
- Comparison with random k-fold
- Demonstration of temporal leakage

**Test Cases**:
1. Training always before validation in time
2. Show temporal leakage with random split
3. Gap parameter for realistic evaluation

**Hints**: Use `TimeSeriesSplit`. Consider gap between train and test for realistic forecasting.

**Skills**: Time series validation, avoiding temporal leakage

---

### F6: Nested Cross-Validation
**Domain**: Validation | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Use nested CV where outer loop estimates generalization and inner loop selects hyperparameters. This gives unbiased performance estimates when tuning hyperparameters.

**Expected Deliverables**:
- Nested CV implementation
- Comparison with non-nested CV
- Understanding of bias in simple CV

**Test Cases**:
1. Inner loop selects best hyperparameter
2. Outer loop estimates true performance
3. Non-nested CV is optimistically biased

**Hints**: Use `cross_val_score` with GridSearchCV as estimator. Computationally expensive but unbiased.

**Skills**: Nested CV, unbiased estimation, hyperparameter tuning

---

### F7: Regression Metrics - MSE, RMSE, MAE
**Domain**: Evaluation | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Compute and interpret MSE, RMSE, and MAE. Understand when each is preferred: MSE penalizes large errors more, MAE is robust to outliers, RMSE is in original units.

**Mathematical Foundation**:
- MSE = (1/n) Σ(yᵢ - ŷᵢ)²
- RMSE = √MSE
- MAE = (1/n) Σ|yᵢ - ŷᵢ|

**Expected Deliverables**:
- All metrics from scratch
- Comparison with sklearn metrics
- Interpretation guidelines

**Test Cases**:
1. MSE > MAE² for datasets with outliers
2. RMSE in same units as target
3. Compare robustness to outliers

**Hints**: Use `sklearn.metrics.mean_squared_error`, `mean_absolute_error`. RMSE is most common.

**Skills**: Regression evaluation, metric selection

---

### F8: R-Squared and Adjusted R-Squared
**Domain**: Evaluation | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Both

**Problem**: Calculate R² (coefficient of determination) and adjusted R² from scratch. Understand R² interpretation and why adjusted R² is needed when adding features.

**Mathematical Foundation**:
- R² = 1 - (SS_res / SS_tot)
- Adjusted R² = 1 - [(1-R²)(n-1)/(n-p-1)]

**Expected Deliverables**:
- R² from scratch
- Adjusted R² accounting for feature count
- Negative R² interpretation

**Test Cases**:
1. Perfect predictions: R² = 1
2. Mean predictions: R² = 0
3. Worse than mean: R² < 0

**Hints**: R² can be negative! Adjusted R² penalizes unnecessary features.

**Skills**: R-squared interpretation, model comparison

---

### F9: MAPE and Percentage Errors
**Domain**: Evaluation | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Both

**Problem**: Calculate Mean Absolute Percentage Error (MAPE) and related percentage metrics. Understand limitations with zero values and when percentage errors are preferred.

**Mathematical Foundation**:
- MAPE = (100/n) Σ|(yᵢ - ŷᵢ)/yᵢ|
- Symmetric MAPE for handling negatives

**Expected Deliverables**:
- MAPE implementation
- Handle zero values
- When MAPE is misleading

**Test Cases**:
1. MAPE undefined when y = 0
2. MAPE is scale-independent
3. Asymmetry in over vs under-prediction

**Hints**: Add small epsilon or use symmetric MAPE. MAPE favors under-predictions.

**Skills**: Percentage errors, business-friendly metrics

---

### F10: Custom Loss Functions
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Create custom loss functions for specific business needs. Understand how to weight different types of errors differently (e.g., under-prediction costs more).

**Expected Deliverables**:
- Asymmetric loss function
- Custom scoring function for sklearn
- Integration with GridSearchCV

**Test Cases**:
1. Under-prediction penalty is higher
2. Use custom scorer in cross-validation
3. Model optimizes for business objective

**Hints**: Use `make_scorer` from sklearn. Define loss function, then wrap as scorer.

**Skills**: Custom metrics, business-aligned evaluation

---

### F11: Regression Baseline Models
**Domain**: Evaluation | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Libraries

**Problem**: Establish baseline performance using DummyRegressor strategies: mean, median, constant. Any useful model should significantly beat these baselines.

**Expected Deliverables**:
- Mean baseline (always predict mean)
- Median baseline
- Comparison with trained models

**Test Cases**:
1. Mean baseline R² = 0 by definition
2. Median baseline is robust to outliers
3. Show improvement percentage over baseline

**Hints**: Use `sklearn.dummy.DummyRegressor`. Always report relative improvement over baseline.

**Skills**: Baseline establishment, meaningful comparison

---

### F12: Classification Baseline Models
**Domain**: Evaluation | **Difficulty**: ★★☆☆☆ | **Time**: 30 min
**Implementation**: Libraries

**Problem**: Establish classification baselines using DummyClassifier: most frequent, stratified random, prior probability. Beat these to prove model value.

**Expected Deliverables**:
- Most frequent class baseline
- Stratified random baseline
- Comparison showing model value

**Test Cases**:
1. Most frequent accuracy on 90-10 split = 90%
2. Stratified maintains class proportions
3. Model must significantly beat baseline

**Hints**: Use `sklearn.dummy.DummyClassifier`. On imbalanced data, beating majority class baseline is the minimum.

**Skills**: Classification baselines, model value demonstration

---

### F13: Bias-Variance Tradeoff
**Domain**: Theory/Validation | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Demonstrate and visualize the bias-variance tradeoff. Understand that total error = bias² + variance + noise, and model complexity affects both.

**Expected Deliverables**:
- Visualization of bias and variance vs complexity
- High bias (underfitting) demonstration
- High variance (overfitting) demonstration

**Test Cases**:
1. Simple model: high bias, low variance
2. Complex model: low bias, high variance
3. Optimal complexity minimizes total error

**Hints**: Use polynomial regression with different degrees. Plot train/test error curves.

**Skills**: Bias-variance tradeoff, model selection intuition

---

### F14: Learning Curves
**Domain**: Validation | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Libraries

**Problem**: Plot learning curves showing training and validation performance vs training set size. Diagnose if model needs more data, complexity, or regularization.

**Expected Deliverables**:
- Learning curve plot
- Diagnosis of overfitting/underfitting
- Recommendations for improvement

**Test Cases**:
1. Overfitting: train high, val low, converging slowly
2. Underfitting: both low, converged early
3. Good fit: both high, converged close together

**Hints**: Use `sklearn.model_selection.learning_curve`. More data helps variance, not bias.

**Skills**: Learning curve analysis, model debugging

---

### F15: Validation Curves
**Domain**: Validation | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Plot validation curves showing performance vs hyperparameter value. Find optimal hyperparameter where validation performance is maximized.

**Expected Deliverables**:
- Validation curve plot
- Optimal hyperparameter identification
- Overfitting region visualization

**Test Cases**:
1. Find optimal regularization strength
2. Show overfitting with too-complex model
3. Show underfitting with too-simple model

**Hints**: Use `sklearn.model_selection.validation_curve`. Use log scale for regularization params.

**Skills**: Validation curves, hyperparameter tuning

---

### F16: Statistical Comparison of Models
**Domain**: Evaluation | **Difficulty**: ★★★★☆ | **Time**: 55 min
**Implementation**: Libraries

**Problem**: Statistically compare two or more models using paired t-test, Wilcoxon signed-rank test, or McNemar's test. Determine if performance differences are significant.

**Expected Deliverables**:
- Paired t-test on CV scores
- Confidence interval for performance difference
- Effect size calculation

**Test Cases**:
1. Compare two classifiers on same CV folds
2. Determine if 2% accuracy difference is significant
3. Report p-value and confidence interval

**Hints**: Use `scipy.stats.ttest_rel`. Pair by fold for valid comparison. Consider corrected tests for CV.

**Skills**: Statistical model comparison, significance testing

---

### F17: Model Selection Criteria
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Use information criteria (AIC, BIC) and cross-validation for model selection. Understand when each approach is appropriate and their assumptions.

**Mathematical Foundation**:
- AIC = 2k - 2ln(L)
- BIC = k×ln(n) - 2ln(L)
- Lower is better

**Expected Deliverables**:
- AIC/BIC calculation
- Comparison with CV selection
- When to use each approach

**Test Cases**:
1. BIC favors simpler models than AIC
2. Compare AIC ranking with CV ranking
3. Select optimal polynomial degree

**Hints**: Use `statsmodels` for AIC/BIC. BIC penalizes complexity more with larger n.

**Skills**: Model selection, information criteria

---

### F18: Bootstrap for Confidence Intervals
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: From Scratch

**Problem**: Use bootstrap resampling to estimate confidence intervals for model performance metrics. Understand why bootstrap is useful when analytical CIs are unknown.

**Expected Deliverables**:
- Bootstrap resampling implementation
- Percentile confidence intervals
- BCa corrected intervals

**Test Cases**:
1. 95% CI for accuracy
2. Compare with analytical CI (if available)
3. Bootstrap for difference between models

**Hints**: Sample with replacement. Use 1000+ bootstrap samples. Percentile method is simplest.

**Skills**: Bootstrap, uncertainty quantification

---

### F19: Holdout vs Cross-Validation Analysis
**Domain**: Validation | **Difficulty**: ★★☆☆☆ | **Time**: 35 min
**Implementation**: Libraries

**Problem**: Compare single holdout split with k-fold cross-validation. Understand variance reduction from CV and when holdout is sufficient.

**Expected Deliverables**:
- Multiple holdout splits comparison
- Variance of holdout vs CV estimates
- When each is preferred

**Test Cases**:
1. Holdout variance across random splits
2. CV gives more stable estimates
3. Large datasets: holdout may suffice

**Hints**: Run 100 random holdout splits, compare variance with 5-fold CV. CV is more stable.

**Skills**: Validation strategy selection

---

### F20: Evaluation on Imbalanced Datasets
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Select appropriate metrics for imbalanced classification. Understand why accuracy fails and when to use precision, recall, F1, ROC-AUC, PR-AUC.

**Expected Deliverables**:
- Accuracy paradox demonstration
- Metric comparison on imbalanced data
- Metric selection guidelines

**Test Cases**:
1. 99% accuracy but 0% recall on minority class
2. F1-score captures both precision and recall
3. PR-AUC better than ROC-AUC for highly imbalanced

**Hints**: Always report class-specific metrics. Consider business cost of errors.

**Skills**: Imbalanced evaluation, metric selection

---

### F21: Multi-Class Evaluation Metrics
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 45 min
**Implementation**: Both

**Problem**: Extend binary classification metrics to multi-class: macro, micro, and weighted averaging. Understand which averaging is appropriate for different situations.

**Mathematical Foundation**:
- Macro: unweighted mean of per-class metrics
- Micro: aggregate TP, FP, FN then compute
- Weighted: weighted by class support

**Expected Deliverables**:
- All averaging strategies
- Multi-class confusion matrix
- When to use each strategy

**Test Cases**:
1. Macro treats all classes equally
2. Weighted handles imbalanced classes
3. Compare on 3+ class problem

**Hints**: Use `average` parameter in sklearn metrics. Macro for equal class importance.

**Skills**: Multi-class metrics, averaging strategies

---

### F22: Multi-Output Evaluation
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Evaluate models with multiple output variables. Understand sample-wise vs output-wise averaging and appropriate metrics.

**Expected Deliverables**:
- Multi-output regression evaluation
- Multi-label classification evaluation
- Aggregation strategies

**Test Cases**:
1. Predict multiple targets simultaneously
2. Per-output and aggregate metrics
3. Sample-wise subset accuracy

**Hints**: Some sklearn metrics support `multioutput` parameter. Consider output importance weighting.

**Skills**: Multi-output evaluation

---

### F23: Error Analysis Techniques
**Domain**: Evaluation | **Difficulty**: ★★★☆☆ | **Time**: 50 min
**Implementation**: Libraries

**Problem**: Systematically analyze errors to improve models. Identify patterns in failures: specific subgroups, feature ranges, edge cases.

**Expected Deliverables**:
- Error distribution analysis
- Subgroup performance breakdown
- Feature importance in errors
- Improvement recommendations

**Test Cases**:
1. Identify worst-performing subgroup
2. Find features correlated with errors
3. Suggest targeted improvements

**Hints**: Analyze residuals/errors. Slice data by features to find weak spots.

**Skills**: Error analysis, model improvement

---

### F24: Creating Evaluation Reports
**Domain**: Evaluation | **Difficulty**: ★★☆☆☆ | **Time**: 40 min
**Implementation**: Libraries

**Problem**: Create comprehensive, reproducible evaluation reports including all relevant metrics, visualizations, and interpretations for stakeholder presentation.

**Expected Deliverables**:
- Automated report generation
- Key visualizations (confusion matrix, ROC, PR)
- Business-friendly interpretation

**Test Cases**:
1. Complete report from single function call
2. Export to HTML/PDF
3. Include confidence intervals

**Hints**: Use classification_report, plot functions. Create template for consistent reporting.

**Skills**: Report generation, communication

---

### F25: Evaluation Best Practices Capstone
**Domain**: Evaluation | **Difficulty**: ★★★★☆ | **Time**: 90 min
**Implementation**: Libraries

**Problem**: Apply all evaluation best practices to a complete ML project. Choose appropriate validation strategy, metrics, baselines, and perform proper statistical comparison.

**Dataset**: Choose appropriate classification or regression dataset

**Expected Deliverables**:
- Proper validation strategy justification
- Baseline to beat
- Multiple relevant metrics
- Statistical significance testing
- Comprehensive evaluation report
- Actionable insights

**Evaluation Criteria**: 
- Correct methodology
- Appropriate metric selection
- Clear communication

**Test Cases**:
1. No data leakage in validation
2. Significant improvement over baseline
3. Robust to different random seeds

**Hints**: Follow evaluation checklist. Document all decisions. Consider deployment requirements.

**Skills**: End-to-end evaluation, best practices

---

