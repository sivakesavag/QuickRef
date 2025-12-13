# Machine Learning & Deep Learning Comparative Notes
## Comprehensive Guide for Interview Preparation & Quick Revision

---

# Table of Contents
1. [Algorithm Comparisons](#1-algorithm-comparisons)
2. [Deep Learning Architecture Comparisons](#2-deep-learning-architecture-comparisons)
3. [Training and Optimization Comparisons](#3-training-and-optimization-comparisons)
4. [Activation Function Comparisons](#4-activation-function-comparisons)
5. [Evaluation Metric Comparisons](#5-evaluation-metric-comparisons)
6. [Model Complexity Comparisons](#6-model-complexity-comparisons)
7. [Data Handling Comparisons](#7-data-handling-comparisons)
8. [Problem Type Comparisons](#8-problem-type-comparisons)
9. [Framework and Library Comparisons](#9-framework-and-library-comparisons)
10. [Deep Learning Concept Comparisons](#10-deep-learning-concept-comparisons)
11. [Advanced Technique Comparisons](#11-advanced-technique-comparisons)
12. [Deployment and Production Comparisons](#12-deployment-and-production-comparisons)

---

# 1. Algorithm Comparisons

## 1.1 Classification vs Regression

| Aspect | Classification | Regression |
|--------|---------------|------------|
| **Output Type** | Discrete categories/classes | Continuous numerical values |
| **Goal** | Predict class membership | Predict quantity |
| **Loss Functions** | Cross-entropy, Hinge loss | MSE, MAE, Huber |
| **Evaluation Metrics** | Accuracy, F1, AUC-ROC | R², RMSE, MAE |
| **Examples** | Spam detection, Disease diagnosis | House price prediction, Temperature forecasting |

### Key Differences
- **Decision Boundary**: Classification creates boundaries; Regression fits a continuous function
- **Probability Output**: Classification can output probabilities per class; Regression outputs single value
- **Threshold Dependency**: Classification often requires threshold tuning; Regression doesn't

### When to Use
```
Classification: When answer is "which category?"
├── Binary: Yes/No, Spam/Not-Spam
└── Multi-class: Cat/Dog/Bird, Sentiment (Positive/Negative/Neutral)

Regression: When answer is "how much/many?"
├── Price prediction
├── Demand forecasting
└── Age estimation
```

---

## 1.2 Linear vs Logistic Regression

| Aspect | Linear Regression | Logistic Regression |
|--------|------------------|---------------------|
| **Problem Type** | Regression | Classification |
| **Output Range** | (-∞, +∞) | [0, 1] probability |
| **Function** | y = wx + b | σ(wx + b) = 1/(1+e^-(wx+b)) |
| **Loss Function** | MSE: Σ(y - ŷ)² | Binary Cross-Entropy: -Σ[y·log(ŷ) + (1-y)·log(1-ŷ)] |
| **Assumptions** | Linear relationship, Homoscedasticity | Linear decision boundary in feature space |

### Mathematical Formulation
```
Linear Regression:
  ŷ = Σ(wᵢxᵢ) + b
  Loss = (1/n)Σ(yᵢ - ŷᵢ)²

Logistic Regression:
  z = Σ(wᵢxᵢ) + b
  ŷ = σ(z) = 1/(1 + e^(-z))
  Loss = -(1/n)Σ[yᵢ·log(ŷᵢ) + (1-yᵢ)·log(1-ŷᵢ)]
```

### Decision Guide
```
Use Linear Regression when:
├── Target is continuous
├── Relationship appears linear
└── Need interpretable coefficients

Use Logistic Regression when:
├── Target is binary/categorical
├── Need probability estimates
└── Want simple, interpretable classifier
```

---

## 1.3 Decision Trees vs Random Forest vs Gradient Boosting

| Aspect | Decision Tree | Random Forest | Gradient Boosting |
|--------|--------------|---------------|-------------------|
| **Ensemble Type** | Single model | Bagging (parallel) | Boosting (sequential) |
| **Bias-Variance** | Low bias, High variance | Low bias, Medium variance | Low bias, Low variance |
| **Training Speed** | Fast | Medium (parallelizable) | Slow (sequential) |
| **Overfitting Risk** | High | Low | Medium (needs tuning) |
| **Interpretability** | High | Medium | Low |
| **Hyperparameters** | Few | Medium | Many |

### Architecture Comparison
```
Decision Tree:        Random Forest:           Gradient Boosting:
     [Root]           [Tree1][Tree2][Tree3]    Tree1 → Tree2 → Tree3
      / \                  ↓    ↓    ↓              ↓       ↓
   [L]  [R]              [Vote/Average]         [Add residuals]
   / \   / \                   ↓                      ↓
 [...] [...]             [Final Prediction]     [Final Prediction]
```

### Key Mechanisms

**Random Forest:**
- Bootstrap sampling (with replacement)
- Random feature subset at each split
- Majority vote (classification) or average (regression)
- Reduces variance through averaging

**Gradient Boosting:**
- Sequential tree building
- Each tree corrects predecessor's errors
- Fits to negative gradient of loss function
- Learning rate controls contribution

### Performance Comparison

| Dataset Size | Decision Tree | Random Forest | Gradient Boosting |
|-------------|---------------|---------------|-------------------|
| Small (<1K) | Good | Overfits | Best |
| Medium (1K-100K) | Overfits | Good | Best |
| Large (>100K) | Overfits | Good | Best (but slow) |

### When to Use
```
Decision Tree:
├── Need interpretability (explain decisions)
├── Quick baseline model
└── Small datasets with clear patterns

Random Forest:
├── Robust general-purpose classifier
├── Handle missing values well
├── Parallel training needed
└── Feature importance analysis

Gradient Boosting:
├── Maximum predictive accuracy needed
├── Structured/tabular data
├── Competition/production models
└── Have time for hyperparameter tuning
```

---

## 1.4 SVM vs Neural Networks

| Aspect | SVM | Neural Networks |
|--------|-----|-----------------|
| **Best For** | Small-medium structured data | Large unstructured data |
| **Feature Engineering** | Required | Learns features automatically |
| **Kernel Trick** | Yes (implicit high-dim mapping) | No (explicit layers) |
| **Interpretability** | Support vectors identifiable | Black box |
| **Training Data Need** | Works with less data | Needs large datasets |
| **Hyperparameters** | C, kernel, gamma | Architecture, LR, layers, etc. |
| **Training Time** | O(n²) to O(n³) | Depends on architecture |

### Mathematical Core
```
SVM Objective:
  Minimize: (1/2)||w||² + C·Σξᵢ
  Subject to: yᵢ(w·xᵢ + b) ≥ 1 - ξᵢ

Neural Network:
  Forward: ŷ = f(W₃·f(W₂·f(W₁·x + b₁) + b₂) + b₃)
  Backward: ∂L/∂W = chain rule through layers
```

### When to Use
```
SVM:
├── Small to medium datasets (<100K samples)
├── High-dimensional sparse data (text)
├── Clear margin of separation exists
└── Limited computational resources

Neural Networks:
├── Large datasets available
├── Images, audio, text, sequences
├── Complex non-linear patterns
└── Sufficient compute (GPU/TPU)
```

---

## 1.5 K-Means vs Hierarchical Clustering vs DBSCAN

| Aspect | K-Means | Hierarchical | DBSCAN |
|--------|---------|--------------|--------|
| **Cluster Shape** | Spherical | Any (based on linkage) | Arbitrary |
| **K Required** | Yes (upfront) | No (cut dendrogram) | No |
| **Scalability** | O(nkt) - Good | O(n²) or O(n³) - Poor | O(n log n) with indexing |
| **Noise Handling** | Poor | Poor | Excellent |
| **Deterministic** | No (init dependent) | Yes | Yes |

### Algorithm Mechanisms
```
K-Means:
1. Initialize K centroids randomly
2. Assign points to nearest centroid
3. Update centroids as cluster means
4. Repeat until convergence

Hierarchical (Agglomerative):
1. Start: each point is a cluster
2. Merge closest pair of clusters
3. Repeat until single cluster
4. Cut dendrogram at desired level

DBSCAN:
1. For each point, find ε-neighborhood
2. If ≥ minPts neighbors → core point
3. Connect core points within ε
4. Assign border points to clusters
5. Mark remaining as noise
```

### Hyperparameters

| Algorithm | Parameters | Selection Method |
|-----------|------------|------------------|
| K-Means | K (clusters) | Elbow method, Silhouette |
| Hierarchical | Linkage type, Cut height | Dendrogram inspection |
| DBSCAN | ε (radius), minPts | k-distance graph |

### When to Use
```
K-Means:
├── Known number of clusters
├── Spherical, equal-sized clusters
├── Large datasets
└── Fast results needed

Hierarchical:
├── Need cluster hierarchy visualization
├── Unknown number of clusters
├── Small to medium datasets
└── Domain requires taxonomy

DBSCAN:
├── Unknown number of clusters
├── Irregular cluster shapes
├── Dataset contains noise/outliers
└── Density-based grouping makes sense
```

---

## 1.6 PCA vs t-SNE vs UMAP

| Aspect | PCA | t-SNE | UMAP |
|--------|-----|-------|------|
| **Type** | Linear | Non-linear | Non-linear |
| **Preserves** | Global variance | Local structure | Local + some global |
| **Scalability** | O(min(n³, p³)) | O(n²) | O(n log n) |
| **Deterministic** | Yes | No | No |
| **New Point Projection** | Yes | No (recompute) | Yes (with transform) |
| **Interpretability** | High (loadings) | Low | Low |

### Mathematical Basis
```
PCA:
  Maximize variance: max ||Xw||²
  Subject to: ||w|| = 1
  Solution: Eigenvectors of X^TX

t-SNE:
  Minimize KL divergence between:
  - pᵢⱼ: Gaussian similarities in high-dim
  - qᵢⱼ: t-distribution similarities in low-dim

UMAP:
  Based on manifold theory and topology
  - Constructs fuzzy simplicial complex
  - Optimizes cross-entropy between high/low dim graphs
```

### Comparison Results
```
Visualization Quality:
├── PCA: Shows major variance directions, misses non-linear structure
├── t-SNE: Excellent cluster separation, can distort distances
└── UMAP: Good clusters, better preserved global structure

Speed (10K points):
├── PCA: ~1 second
├── t-SNE: ~1-5 minutes
└── UMAP: ~10-30 seconds
```

### When to Use
```
PCA:
├── Need interpretable components
├── Linear relationships dominate
├── Preprocessing for other algorithms
├── Large datasets requiring speed
└── Need to project new points

t-SNE:
├── Visualization only (2D/3D)
├── Small-medium datasets (<50K)
├── Focus on local cluster structure
└── Publication-quality figures

UMAP:
├── Large dataset visualization
├── Need to preserve more global structure
├── Downstream clustering needed
└── Require new point projection
```

---

## 1.7 Naive Bayes vs Logistic Regression

| Aspect | Naive Bayes | Logistic Regression |
|--------|-------------|---------------------|
| **Approach** | Generative (P(X|Y)) | Discriminative (P(Y|X)) |
| **Independence Assumption** | Yes (strong) | No |
| **Training** | Count-based, very fast | Iterative optimization |
| **Performance (small data)** | Often better | May overfit |
| **Performance (large data)** | Plateaus | Continues improving |
| **Calibration** | Often poor | Generally good |

### Mathematical Formulation
```
Naive Bayes:
  P(Y|X) ∝ P(Y) · ∏P(Xᵢ|Y)
  Predict: argmax_y P(y) · ∏P(xᵢ|y)

Logistic Regression:
  P(Y=1|X) = σ(w^T x + b)
  Trained by maximizing likelihood
```

### When to Use
```
Naive Bayes:
├── Text classification (spam, sentiment)
├── Very high-dimensional sparse data
├── Limited training data
├── Need very fast training/inference
└── Features are reasonably independent

Logistic Regression:
├── Features are correlated
├── Need well-calibrated probabilities
├── Enough training data available
├── Want interpretable coefficients
└── Need regularization (L1/L2)
```

---

## 1.8 Bagging vs Boosting vs Stacking

| Aspect | Bagging | Boosting | Stacking |
|--------|---------|----------|----------|
| **Training** | Parallel | Sequential | Two-stage |
| **Base Learners** | Homogeneous | Homogeneous | Heterogeneous |
| **Sampling** | Bootstrap (with replacement) | Weighted / Residual-based | K-fold predictions |
| **Focus** | Reduce variance | Reduce bias | Combine strengths |
| **Overfitting Risk** | Low | Medium-High | Medium |

### Architecture
```
Bagging:
  Data → [Bootstrap Sample 1] → Model1 ─┐
       → [Bootstrap Sample 2] → Model2 ─┼→ Average/Vote → Prediction
       → [Bootstrap Sample N] → ModelN ─┘

Boosting:
  Data → Model1 → Residuals → Model2 → Residuals → Model3 → Sum → Prediction
         (weak)   (fit to)    (weak)   (fit to)    (weak)

Stacking:
  Level 0: [Model1, Model2, Model3] → Predictions
  Level 1: Meta-learner(Predictions) → Final Prediction
```

### When to Use
```
Bagging:
├── High-variance base learners (trees)
├── Parallel training resources available
├── Want robust, stable predictions
└── Example: Random Forest

Boosting:
├── Need maximum accuracy
├── Structured/tabular data
├── Have time for tuning
└── Example: XGBoost, LightGBM

Stacking:
├── Competition scenarios
├── Have diverse strong models
├── Computational budget available
└── Want to leverage different model strengths
```

---

## 1.9 XGBoost vs LightGBM vs CatBoost

| Aspect | XGBoost | LightGBM | CatBoost |
|--------|---------|----------|----------|
| **Tree Growth** | Level-wise | Leaf-wise | Level-wise (symmetric) |
| **Speed** | Fast | Fastest | Medium |
| **Memory** | Medium | Low | High |
| **Categorical Handling** | Manual encoding | Native (but limited) | Native (best) |
| **GPU Support** | Yes | Yes | Yes (best) |
| **Overfitting Control** | Good | Needs care | Excellent |

### Tree Growth Strategies
```
Level-wise (XGBoost):        Leaf-wise (LightGBM):
       [1]                          [1]
      /   \                        /   \
    [2]   [3]                    [2]   [3]
   / \   / \                    /
 [4][5][6][7]                 [4]
                              /
Grows all leaves           [5] ← Grows best leaf
at same level              

Symmetric (CatBoost):
       [1]
      /   \
    [2]   [2]  ← Same split condition
   / \   / \
 [3][4][3][4]
```

### Performance Comparison

| Dataset Characteristic | Best Choice |
|-----------------------|-------------|
| Large dataset (>1M rows) | LightGBM |
| Many categorical features | CatBoost |
| Small dataset | CatBoost (less overfitting) |
| Fastest training needed | LightGBM |
| GPU training | CatBoost |
| General purpose | XGBoost |

### Key Hyperparameters

| XGBoost | LightGBM | CatBoost |
|---------|----------|----------|
| max_depth | num_leaves | depth |
| learning_rate | learning_rate | learning_rate |
| n_estimators | n_estimators | iterations |
| subsample | bagging_fraction | subsample |
| colsample_bytree | feature_fraction | rsm |
| reg_alpha, reg_lambda | lambda_l1, lambda_l2 | l2_leaf_reg |

---

## 1.10 RNN vs LSTM vs GRU vs Transformers

| Aspect | RNN | LSTM | GRU | Transformer |
|--------|-----|------|-----|-------------|
| **Memory** | Short-term | Long-term | Long-term | Attention-based |
| **Vanishing Gradient** | Severe | Mitigated | Mitigated | None |
| **Parameters** | Fewest | Most | Medium | Varies |
| **Parallelization** | No | No | No | Yes |
| **Long-range Dependencies** | Poor | Good | Good | Best |

### Architecture Details
```
RNN Cell:
  hₜ = tanh(Wₓₕxₜ + Wₕₕhₜ₋₁ + b)

LSTM Cell (3 gates):
  fₜ = σ(Wf·[hₜ₋₁, xₜ] + bf)     # Forget gate
  iₜ = σ(Wi·[hₜ₋₁, xₜ] + bi)     # Input gate
  oₜ = σ(Wo·[hₜ₋₁, xₜ] + bo)     # Output gate
  c̃ₜ = tanh(Wc·[hₜ₋₁, xₜ] + bc)  # Candidate
  cₜ = fₜ⊙cₜ₋₁ + iₜ⊙c̃ₜ          # Cell state
  hₜ = oₜ⊙tanh(cₜ)               # Hidden state

GRU Cell (2 gates):
  zₜ = σ(Wz·[hₜ₋₁, xₜ])          # Update gate
  rₜ = σ(Wr·[hₜ₋₁, xₜ])          # Reset gate
  h̃ₜ = tanh(W·[rₜ⊙hₜ₋₁, xₜ])    # Candidate
  hₜ = (1-zₜ)⊙hₜ₋₁ + zₜ⊙h̃ₜ       # Output

Transformer:
  Attention(Q,K,V) = softmax(QK^T/√dₖ)V
  Multi-Head: Concat(head₁,...,headₕ)Wᴼ
```

### When to Use
```
RNN:
├── Simple sequences, short dependencies
├── Resource-constrained environments
└── Teaching/learning purposes

LSTM:
├── Long sequences with dependencies
├── Time series forecasting
├── Speech recognition
└── When forget mechanism is needed

GRU:
├── Similar to LSTM tasks
├── Need faster training
├── Smaller datasets
└── Mobile/edge deployment

Transformer:
├── Very long sequences
├── NLP tasks (translation, QA)
├── Parallel training needed
├── Large compute budget available
```

---

## 1.11 CNN Architectures Comparison

| Architecture | Year | Depth | Parameters | Top-5 Error (ImageNet) | Key Innovation |
|-------------|------|-------|------------|----------------------|----------------|
| VGG-16 | 2014 | 16 | 138M | 7.3% | Uniform 3×3 convolutions |
| ResNet-50 | 2015 | 50 | 25M | 3.6% | Skip connections |
| Inception-v3 | 2015 | 48 | 24M | 3.5% | Multi-scale filters |
| EfficientNet-B0 | 2019 | 237 | 5.3M | 2.5% | Compound scaling |

### Architectural Patterns
```
VGG Block:
  Conv3x3 → ReLU → Conv3x3 → ReLU → MaxPool

ResNet Block:
  Input ─→ Conv → BN → ReLU → Conv → BN → (+) → ReLU
    └──────────────────────────────────┘

Inception Module:
        ┌→ 1×1 Conv ─────────────────┐
  Input ├→ 1×1 Conv → 3×3 Conv ──────┼→ Concat
        ├→ 1×1 Conv → 5×5 Conv ──────┤
        └→ MaxPool → 1×1 Conv ───────┘

EfficientNet (Compound Scaling):
  Depth: d = α^φ
  Width: w = β^φ  
  Resolution: r = γ^φ
  where α·β²·γ² ≈ 2
```

### When to Use
```
VGG:
├── Simple baseline
├── Transfer learning (pretrained features)
└── When interpretability of layers matters

ResNet:
├── Very deep networks needed
├── General-purpose image tasks
├── Available as backbone for detection/segmentation
└── Standard choice for most vision tasks

Inception:
├── Multi-scale features important
├── Object detection at different sizes
└── Computational efficiency needed

EfficientNet:
├── State-of-the-art accuracy needed
├── Resource-efficient deployment
├── Mobile/edge applications
└── Best accuracy-efficiency trade-off
```

---

# 2. Deep Learning Architecture Comparisons

## 2.1 Feedforward vs Recurrent vs Convolutional Networks

| Aspect | Feedforward (MLP) | Recurrent (RNN) | Convolutional (CNN) |
|--------|-------------------|-----------------|---------------------|
| **Data Type** | Tabular, fixed-size | Sequential, variable-length | Grid-structured (images, audio) |
| **Connection Pattern** | Fully connected | Temporal connections | Local receptive fields |
| **Parameter Sharing** | None | Across time steps | Across spatial positions |
| **Memory** | Stateless | Has hidden state | Stateless (per layer) |
| **Translation Invariance** | No | Time-invariant | Spatially invariant |

### Architecture Diagrams
```
Feedforward:             Recurrent:              Convolutional:
  [Input]                 x₁→x₂→x₃              [Image Grid]
     ↓                     ↓  ↓  ↓                  ↓
  [Dense]                 h₁→h₂→h₃              [Conv+Pool]
     ↓                        ↓                    ↓
  [Dense]                 [Output]              [Conv+Pool]
     ↓                                              ↓
  [Output]                                      [Flatten→Dense]
```

### When to Use
```
Feedforward (MLP):
├── Tabular/structured data
├── Fixed-size input features
├── Simple classification/regression
└── As final layers in other architectures

Recurrent (RNN/LSTM/GRU):
├── Time series, sequences
├── Text processing
├── Speech recognition
└── Variable-length inputs

Convolutional (CNN):
├── Images, video frames
├── Audio spectrograms
├── Any grid-structured data
└── When spatial hierarchies matter
```

---

## 2.2 LSTM vs GRU (Detailed Gate Comparison)

| Aspect | LSTM | GRU |
|--------|------|-----|
| **Gates** | 3 (forget, input, output) | 2 (reset, update) |
| **States** | 2 (cell state, hidden state) | 1 (hidden state) |
| **Parameters** | 4 × (n² + nm + n) | 3 × (n² + nm + n) |
| **Training Speed** | Slower | ~30% faster |
| **Memory Usage** | Higher | Lower |
| **Long Dependencies** | Slightly better | Good |

### Gate Mechanisms Compared
```
LSTM Gates:
┌─────────────────────────────────────────────────────────────┐
│  Forget Gate: fₜ = σ(Wf·[hₜ₋₁, xₜ] + bf)                   │
│  → Decides what to discard from cell state                  │
│                                                             │
│  Input Gate: iₜ = σ(Wi·[hₜ₋₁, xₜ] + bi)                    │
│  → Decides what new information to store                    │
│                                                             │
│  Output Gate: oₜ = σ(Wo·[hₜ₋₁, xₜ] + bo)                   │
│  → Decides what to output                                   │
└─────────────────────────────────────────────────────────────┘

GRU Gates:
┌─────────────────────────────────────────────────────────────┐
│  Reset Gate: rₜ = σ(Wr·[hₜ₋₁, xₜ])                         │
│  → Controls how much past info to forget                    │
│                                                             │
│  Update Gate: zₜ = σ(Wz·[hₜ₋₁, xₜ])                        │
│  → Controls balance between old and new info                │
│  (Combines forget + input gate functionality)               │
└─────────────────────────────────────────────────────────────┘
```

### Performance Guidelines
```
Choose LSTM when:
├── Very long sequences (>500 steps)
├── Need explicit memory control
├── Complex temporal patterns
└── Output gating is important

Choose GRU when:
├── Moderate sequence lengths
├── Faster training needed
├── Limited compute resources
├── Similar performance, fewer parameters
└── Default choice for experimentation
```

---

## 2.3 RNN vs Transformer Architectures

| Aspect | RNN | Transformer |
|--------|-----|-------------|
| **Attention** | Implicit through hidden state | Explicit self-attention |
| **Parallelization** | Sequential only | Fully parallel |
| **Complexity** | O(n) sequential steps | O(n²) attention, O(1) depth |
| **Long-range** | Limited (vanishing gradient) | Excellent (direct paths) |
| **Position** | Implicit (order of processing) | Explicit (positional encoding) |
| **Memory** | O(1) for hidden state | O(n²) for attention |

### Architecture Comparison
```
RNN Processing:
  x₁ → [RNN] → h₁
         ↓
  x₂ → [RNN] → h₂
         ↓
  x₃ → [RNN] → h₃ → Output
  
  (Sequential, information bottleneck through hidden state)

Transformer Processing:
  [x₁, x₂, x₃] + [PE₁, PE₂, PE₃]
         ↓
  [Self-Attention Layer]  ← All positions see all positions
         ↓
  [Feed-Forward Layer]
         ↓
  [Output₁, Output₂, Output₃]
  
  (Parallel, direct connections between all positions)
```

### When to Choose
```
RNN (LSTM/GRU):
├── Limited compute/memory
├── Streaming data (online processing)
├── Very long sequences (memory efficient)
├── Embedded/mobile deployment
└── When positional ordering is central

Transformer:
├── Sufficient GPU memory
├── Need best accuracy
├── Parallel training important
├── NLP tasks (translation, summarization)
├── Long-range dependencies critical
└── Pre-trained models available
```

---

## 2.4 GANs vs VAEs for Generation

| Aspect | GAN | VAE |
|--------|-----|-----|
| **Training** | Adversarial (min-max game) | Direct likelihood optimization |
| **Output Quality** | Sharp, realistic | Slightly blurry |
| **Mode Collapse** | Common problem | Rare |
| **Training Stability** | Difficult | Stable |
| **Latent Space** | Unstructured | Structured, interpretable |
| **Likelihood** | Implicit (no density estimate) | Explicit (ELBO) |

### Architecture
```
GAN:
  z ~ N(0,1) → [Generator] → fake_image
                              ↓
  real_image ──────────→ [Discriminator] → real/fake
  
  Loss: min_G max_D E[log D(x)] + E[log(1-D(G(z)))]

VAE:
  x → [Encoder] → μ, σ → z = μ + σ·ε → [Decoder] → x̂
  
  Loss: Reconstruction + KL Divergence
      = E[log p(x|z)] - KL(q(z|x) || p(z))
```

### Trade-offs
```
Sample Quality:
├── GAN: Higher fidelity, sharper details
└── VAE: Smoother, sometimes blurry

Diversity:
├── GAN: May have mode collapse (limited diversity)
└── VAE: Better coverage of data distribution

Controllability:
├── GAN: Less control over latent space
└── VAE: Smooth, interpolatable latent space

Training:
├── GAN: Requires careful balancing G vs D
└── VAE: Standard backpropagation, more stable
```

### When to Use
```
GAN:
├── Photo-realistic image generation
├── Super-resolution
├── Style transfer
├── When quality > diversity
└── Data augmentation

VAE:
├── Representation learning
├── Anomaly detection
├── Data compression
├── When interpretable latent space needed
├── More stable training preferred
```

---

## 2.5 BERT vs GPT vs T5

| Aspect | BERT | GPT | T5 |
|--------|------|-----|-----|
| **Architecture** | Encoder-only | Decoder-only | Encoder-Decoder |
| **Pre-training** | Masked LM + NSP | Causal LM | Text-to-Text |
| **Bidirectional** | Yes | No (left-to-right) | Encoder: Yes, Decoder: No |
| **Best For** | Understanding | Generation | Both |
| **Fine-tuning** | Add task head | Prompt-based | Unified format |

### Architecture Diagrams
```
BERT (Encoder-only):
  [CLS] + tokens → [Transformer Encoder] → Contextualized embeddings
                                                    ↓
                                            [Task-specific head]

GPT (Decoder-only):
  tokens → [Masked Transformer Decoder] → next_token prediction
                        ↓
                 [Autoregressive generation]

T5 (Encoder-Decoder):
  input_text → [Encoder] → representations → [Decoder] → output_text
  "translate: Hello" ────────────────────→ "Hola"
```

### Pre-training Objectives
```
BERT:
├── Masked Language Model (MLM): Predict [MASK] tokens
└── Next Sentence Prediction (NSP): Is sentence B after A?

GPT:
└── Causal Language Model: Predict next token given previous

T5:
└── Span Corruption: Replace spans with sentinel tokens, predict
```

### Task Suitability

| Task | BERT | GPT | T5 |
|------|------|-----|-----|
| Classification | ★★★ | ★★ | ★★★ |
| NER/Tagging | ★★★ | ★ | ★★★ |
| Question Answering | ★★★ | ★★ | ★★★ |
| Text Generation | ★ | ★★★ | ★★★ |
| Translation | ★ | ★★ | ★★★ |
| Summarization | ★★ | ★★★ | ★★★ |

---

## 2.6 Segmentation Architectures: U-Net vs SegNet vs Mask R-CNN

| Aspect | U-Net | SegNet | Mask R-CNN |
|--------|-------|--------|------------|
| **Type** | Semantic | Semantic | Instance |
| **Architecture** | Encoder-Decoder + Skip | Encoder-Decoder | Detection + Mask branch |
| **Skip Connections** | Feature concatenation | Pooling indices | From FPN |
| **Speed** | Fast | Fast | Slower |
| **Instance Separation** | No | No | Yes |

### Architecture Patterns
```
U-Net:
  Encoder           Decoder
  [───512───]──────[───512───]  (skip connection)
      ↓                ↑
  [──256──]────────[──256──]
      ↓                ↑
  [─128─]──────────[─128─]
      ↓                ↑
      └───[Bottleneck]───┘

SegNet:
  Encoder           Decoder
  [Conv+Pool]      [Unpool+Conv]
       ↓                ↑
   (Store pooling indices for precise upsampling)

Mask R-CNN:
  Image → [Backbone+FPN] → [RPN] → [RoIAlign] → ┬→ [Box Head] → Boxes
                                                ├→ [Class Head] → Labels
                                                └→ [Mask Head] → Masks
```

### When to Use
```
U-Net:
├── Medical image segmentation
├── Biomedical applications
├── Limited training data
├── Need for precise boundaries
└── Semantic segmentation (all of one class)

SegNet:
├── Scene understanding
├── Road segmentation
├── When memory efficiency matters
└── Real-time applications

Mask R-CNN:
├── Instance segmentation (separate each object)
├── When need object detection + masks
├── COCO-style benchmarks
├── Panoptic segmentation base
```

---

## 2.7 Object Detection: YOLO vs R-CNN Family vs SSD

| Aspect | YOLO | Faster R-CNN | SSD |
|--------|------|--------------|-----|
| **Approach** | One-stage | Two-stage | One-stage |
| **Speed** | Fastest (45-155 FPS) | Slow (5-7 FPS) | Fast (46 FPS) |
| **Accuracy** | Good | Best | Good |
| **Small Objects** | Weak | Strong | Moderate |
| **Real-time** | Yes | No | Yes |

### Architecture Overview
```
YOLO (You Only Look Once):
  Image → [Single CNN] → Grid × (Boxes + Confidence + Classes)
  └── One forward pass, division into grid cells

Faster R-CNN (Two-stage):
  Image → [Backbone] → [RPN] → Proposals → [RoI Pooling] → [Heads] → Detections
  └── Stage 1: Region proposals
  └── Stage 2: Classification + Refinement

SSD (Single Shot Detector):
  Image → [Multi-scale feature maps] → [Predictions at each scale]
  └── Combines different resolution features
```

### Speed vs Accuracy Trade-off
```
Accuracy (mAP)
    ↑
    │    ★ Faster R-CNN
    │       
    │  ★ YOLOv4    ★ SSD512
    │  ★ YOLOv5
    │    ★ SSD300
    │         ★ YOLOv3
    │
    └──────────────────────→ Speed (FPS)
```

### When to Use
```
YOLO (v5/v7/v8):
├── Real-time applications
├── Video processing
├── Edge deployment
├── When speed is critical
└── Good balance for most use cases

Faster R-CNN:
├── Maximum accuracy needed
├── Small object detection critical
├── Offline processing acceptable
├── Research/benchmarking
└── When have compute resources

SSD:
├── Good speed-accuracy balance
├── Multi-scale detection important
├── Real-time with decent accuracy
└── Mobile deployment (MobileNet-SSD)
```

---

## 2.8 Normalization: Batch vs Layer vs Instance Normalization

| Aspect | Batch Norm | Layer Norm | Instance Norm |
|--------|------------|------------|---------------|
| **Normalize Over** | Batch dimension | Feature dimension | Spatial dimensions |
| **Batch Dependency** | Yes | No | No |
| **Best For** | CNNs | RNNs, Transformers | Style transfer |
| **Small Batch** | Poor | Good | Good |
| **Inference** | Uses running stats | Same as training | Same as training |

### Normalization Dimensions
```
Input Shape: [N, C, H, W] (Batch, Channels, Height, Width)

Batch Norm:     Normalize over [N, H, W] for each channel
                Calculate mean/var across batch & spatial dims

Layer Norm:     Normalize over [C, H, W] for each sample
                Calculate mean/var across all features per sample

Instance Norm:  Normalize over [H, W] for each channel of each sample
                Calculate mean/var per channel per sample

Group Norm:     Normalize over [G, H, W] where channels split into groups
                Middle ground between Layer and Instance
```

### Mathematical Formulation
```
All follow: y = γ · (x - μ) / √(σ² + ε) + β

Difference is in computing μ and σ:

Batch Norm:    μ, σ = mean/std over (N, H, W)
Layer Norm:    μ, σ = mean/std over (C, H, W)  
Instance Norm: μ, σ = mean/std over (H, W)
Group Norm:    μ, σ = mean/std over (C/G, H, W)
```

### When to Use
```
Batch Normalization:
├── CNNs for classification
├── Large batch sizes (≥32)
├── When batch statistics are reliable
└── Standard choice for ResNet, VGG, etc.

Layer Normalization:
├── Transformers (attention layers)
├── RNNs/LSTMs
├── Small batch sizes
├── When batch-independence needed
└── NLP models

Instance Normalization:
├── Style transfer
├── Image generation
├── When per-image normalization needed
└── BN alternative in GANs

Group Normalization:
├── Object detection, segmentation
├── Very small batches
├── When BN fails due to batch size
└── GPU memory constrained
```

---

# 3. Training and Optimization Comparisons

## 3.1 SGD vs Adam vs RMSprop vs AdaGrad vs Muon

| Optimizer | Learning Rate | Momentum | Adaptive LR | Memory | Best For |
|-----------|---------------|----------|-------------|--------|----------|
| **SGD** | Fixed | Optional | No | O(1) | Convex, large-scale |
| **SGD+Momentum** | Fixed | Yes | No | O(n) | Deep networks |
| **AdaGrad** | Per-parameter | No | Yes (↓) | O(n) | Sparse data |
| **RMSprop** | Per-parameter | No | Yes | O(n) | RNNs, non-stationary |
| **Adam** | Per-parameter | Yes | Yes | O(2n) | General default |
| **AdamW** | Per-parameter | Yes | Yes | O(2n) | Transformers |
| **Muon** | Per-parameter | Yes | No | O(n) | LLM pretraining |

### Update Rules
```
SGD:
  θ = θ - η·∇L

SGD + Momentum:
  v = βv + ∇L
  θ = θ - η·v

AdaGrad:
  G = G + (∇L)²
  θ = θ - η·∇L/√(G + ε)

RMSprop:
  G = βG + (1-β)(∇L)²
  θ = θ - η·∇L/√(G + ε)

Adam:
  m = β₁m + (1-β₁)∇L           # First moment
  v = β₂v + (1-β₂)(∇L)²        # Second moment
  m̂ = m/(1-β₁ᵗ)                # Bias correction
  v̂ = v/(1-β₂ᵗ)
  θ = θ - η·m̂/√(v̂ + ε)

Muon:
  Uses orthogonalized momentum
  Better for large language models
  Lower memory than Adam
```

### Hyperparameters

| Optimizer | Key Parameters | Typical Values |
|-----------|---------------|----------------|
| SGD | lr, momentum | 0.1, 0.9 |
| Adam | lr, β₁, β₂, ε | 0.001, 0.9, 0.999, 1e-8 |
| RMSprop | lr, α, ε | 0.001, 0.99, 1e-8 |
| AdamW | + weight_decay | 0.01 |

### When to Use
```
SGD + Momentum:
├── Final fine-tuning (often best generalization)
├── Computer vision (ResNets)
├── When have time to tune learning rate schedule
└── Large-scale distributed training

Adam/AdamW:
├── Default starting point
├── Transformers and NLP
├── Fast prototyping
├── Works well out-of-box
└── AdamW for weight decay regularization

RMSprop:
├── Recurrent networks
├── Non-stationary objectives
├── Reinforcement learning
└── When Adam shows instability

Muon:
├── Large language model pretraining
├── Memory-constrained training
├── Alternative to Adam for LLMs
└── Research/experimental settings
```

---

## 3.2 Batch vs Mini-batch vs Stochastic Gradient Descent

| Aspect | Batch GD | Mini-batch GD | Stochastic GD |
|--------|----------|---------------|---------------|
| **Samples per Update** | All N | B (e.g., 32-512) | 1 |
| **Updates per Epoch** | 1 | N/B | N |
| **Gradient Noise** | None | Low | High |
| **Convergence** | Smooth, slow | Balanced | Noisy, fast |
| **Memory** | O(N) | O(B) | O(1) |
| **GPU Utilization** | Efficient | Most efficient | Inefficient |

### Visualization
```
Loss Landscape:

Batch GD:        Mini-batch GD:    Stochastic GD:
   ↓                 ↘                  ↙↘
   ↓                 ↘↙                ↘↙
   ↓               ↘                 ↙↘↙
   ●               ●                   ●
(smooth)       (slight noise)    (very noisy)
```

### Trade-offs
```
Convergence Speed:
├── Batch: Slow per epoch, guaranteed direction
├── Mini-batch: Fast, good GPU utilization
└── Stochastic: Fastest initial progress, noisy

Generalization:
├── Batch: May overfit, settles in sharp minima
├── Mini-batch: Good regularization from noise
└── Stochastic: Best regularization, finds flat minima

Practical Recommendation:
└── Mini-batch with size 32-256 is almost always best
```

---

## 3.3 L1 vs L2 vs Elastic Net Regularization

| Aspect | L1 (Lasso) | L2 (Ridge) | Elastic Net |
|--------|------------|------------|-------------|
| **Penalty** | λΣ|wᵢ| | λΣwᵢ² | λ₁Σ|wᵢ| + λ₂Σwᵢ² |
| **Effect on Weights** | Sparse (zeros out) | Shrinks uniformly | Both |
| **Feature Selection** | Yes | No | Partial |
| **Correlated Features** | Picks one arbitrarily | Keeps both | Handles well |
| **Computational** | Harder (non-smooth) | Easier | Medium |

### Mathematical Formulation
```
L1 Regularization (Lasso):
  Loss = L_original + λ·Σ|wᵢ|
  Gradient: λ·sign(w)
  
L2 Regularization (Ridge):
  Loss = L_original + λ·Σwᵢ²
  Gradient: 2λ·w
  
Elastic Net:
  Loss = L_original + λ₁·Σ|wᵢ| + λ₂·Σwᵢ²
  
Weight Decay (in optimizer):
  w = w - η·(∇L + λ·w)
  Equivalent to L2 for SGD, different for Adam
```

### When to Use
```
L1 (Lasso):
├── Feature selection needed
├── Expect sparse solutions
├── Many irrelevant features
└── Interpretability important

L2 (Ridge):
├── All features likely relevant
├── Prevent large weights
├── More stable optimization
└── Default regularization choice

Elastic Net:
├── High-dimensional data
├── Correlated feature groups
├── Want sparsity + stability
└── Uncertain about feature importance
```

---

## 3.4 Dropout vs Early Stopping vs Data Augmentation

| Technique | Type | When Applied | Effect |
|-----------|------|--------------|--------|
| **Dropout** | Regularization | Training (per batch) | Ensemble effect |
| **Early Stopping** | Regularization | End of epoch | Limits capacity |
| **Data Augmentation** | Data manipulation | Input preprocessing | Increases diversity |

### Mechanisms
```
Dropout:
  Training: x̃ = x · mask / (1-p)  where mask ~ Bernoulli(1-p)
  Inference: No change (or multiply by 1-p if no scaling)
  
  Effect: Each forward pass uses different sub-network
          Approximately trains ensemble of 2ⁿ networks

Early Stopping:
  Monitor validation loss
  If val_loss doesn't improve for 'patience' epochs → stop
  Restore best weights
  
  Effect: Implicit regularization, limits effective capacity

Data Augmentation:
  Apply random transformations to input
  Examples: rotation, flip, crop, color jitter, mixup
  
  Effect: Artificially increases training data diversity
```

### Comparison
```
Computational Cost:
├── Dropout: Minimal (mask operations)
├── Early Stopping: None (just monitoring)
└── Data Augmentation: Can be significant (transforms)

Hyperparameters:
├── Dropout: p (drop probability, typically 0.2-0.5)
├── Early Stopping: patience (epochs to wait)
└── Data Augmentation: Transform types and magnitudes

Combination:
└── All three are commonly used together!
    Dropout + Early Stopping + Data Augmentation
```

### When to Use
```
Dropout:
├── Large networks with overfitting risk
├── Fully connected layers (higher p ~0.5)
├── After conv layers (lower p ~0.2)
└── NOT with Batch Normalization (usually)

Early Stopping:
├── Always (virtually no downside)
├── When training is expensive
├── As automatic regularization
└── Combine with learning rate reduction

Data Augmentation:
├── Limited training data
├── Image/audio data
├── When domain knowledge suggests invariances
└── Heavy augmentation for small datasets
```

---

## 3.5 Xavier vs He vs LeCun Initialization

| Method | Formula | Best For | Activation |
|--------|---------|----------|------------|
| **Xavier/Glorot** | W ~ N(0, 2/(n_in + n_out)) | Sigmoid, Tanh | Symmetric |
| **He/Kaiming** | W ~ N(0, 2/n_in) | ReLU, Leaky ReLU | Asymmetric |
| **LeCun** | W ~ N(0, 1/n_in) | SELU | Self-normalizing |

### Mathematical Derivation
```
Goal: Maintain variance of activations across layers

Xavier (Glorot):
  Var(W) = 2 / (fan_in + fan_out)
  Uniform: W ~ U[-√(6/(n_in+n_out)), √(6/(n_in+n_out))]
  Normal:  W ~ N(0, 2/(n_in + n_out))
  
He (Kaiming):
  Var(W) = 2 / fan_in
  Accounts for ReLU zeroing out half the distribution
  Normal:  W ~ N(0, 2/n_in)
  
LeCun:
  Var(W) = 1 / fan_in
  Designed for SELU activation
  Normal:  W ~ N(0, 1/n_in)
```

### Decision Guide
```
Activation Function → Initialization:
├── Sigmoid, Tanh → Xavier
├── ReLU → He
├── Leaky ReLU → He (with adjustment for slope)
├── SELU → LeCun
└── Linear → Xavier or He
```

---

## 3.6 Loss Functions: Cross-entropy vs Hinge vs Focal

| Loss | Formula | Best For | Output Layer |
|------|---------|----------|--------------|
| **Cross-entropy** | -Σyᵢlog(ŷᵢ) | Classification | Softmax |
| **Binary CE** | -[y·log(ŷ) + (1-y)·log(1-ŷ)] | Binary classification | Sigmoid |
| **Hinge** | max(0, 1 - y·ŷ) | SVM, margins | Raw scores |
| **Focal** | -(1-ŷ)^γ·y·log(ŷ) | Imbalanced data | Softmax |

### Comparison
```
Cross-Entropy:
  L = -Σyᵢlog(ŷᵢ)
  Properties:
  - Probabilistic interpretation
  - Well-calibrated probabilities
  - Standard choice for classification

Hinge Loss:
  L = max(0, 1 - y·f(x))  where y ∈ {-1, 1}
  Properties:
  - Margin-based
  - Not differentiable at 1
  - SVM objective

Focal Loss:
  L = -(1-pₜ)^γ · log(pₜ)
  Properties:
  - Down-weights easy examples
  - γ controls focusing (γ=2 typical)
  - For class imbalance in detection
```

### When to Use
```
Cross-Entropy:
├── Standard classification
├── Multi-class problems
├── When probabilities matter
└── Well-balanced datasets

Hinge Loss:
├── SVM-style classifiers
├── When margin important
├── Binary classification
└── Less common in deep learning

Focal Loss:
├── Object detection (many background examples)
├── Severe class imbalance
├── RetinaNet and similar architectures
└── When easy negatives dominate
```

---

# 4. Activation Function Comparisons

## 4.1 Comprehensive Activation Comparison

| Activation | Formula | Range | Gradient | Pros | Cons |
|------------|---------|-------|----------|------|------|
| **Sigmoid** | 1/(1+e⁻ˣ) | (0, 1) | σ(1-σ) | Probability output | Vanishing gradient |
| **Tanh** | (eˣ-e⁻ˣ)/(eˣ+e⁻ˣ) | (-1, 1) | 1-tanh² | Zero-centered | Vanishing gradient |
| **ReLU** | max(0, x) | [0, ∞) | 0 or 1 | Fast, no vanish | Dead neurons |
| **Leaky ReLU** | max(αx, x) | (-∞, ∞) | α or 1 | No dead neurons | α is hyperparameter |
| **ELU** | x if x>0, α(eˣ-1) else | (-α, ∞) | 1 or α·eˣ | Smooth, robust | Expensive exp() |
| **Swish** | x·σ(x) | (-∞, ∞) | Smooth | Self-gated, smooth | Computationally heavier |
| **GELU** | x·Φ(x) | (-∞, ∞) | Smooth | Used in Transformers | Complex formula |

### Visual Comparison
```
      │                          │                          │
   1  │    ┌─────── Sigmoid      │────────┐ Tanh           │        ╱ ReLU
      │   ╱                      │        │                │       ╱
   0  ├──┼──────────────        ─┼────────┼──              ├──────╱──────
      │                          │        │                │ dead ╱
  -1  │                          │────────┘                │     ╱
      └──────────────────        └──────────────           └──────────────
```

### Gradient Flow Analysis
```
Vanishing Gradient Problem:

Layer:      1      2      3      4      5
Sigmoid:   0.25 × 0.25 × 0.25 × 0.25 × 0.25 = 0.001
           (max gradient is 0.25)
           
Tanh:      Same issue (max gradient ~1 at 0, diminishes)

ReLU:      1    × 1    × 1    × 1    × 1    = 1
           (gradient is either 0 or 1)
           But: 0 × anything = 0 (dead neuron)
```

---

## 4.2 When to Use Each Activation

### Decision Tree
```
Choosing Activation Function:
│
├── Output Layer?
│   ├── Binary Classification → Sigmoid
│   ├── Multi-class Classification → Softmax
│   ├── Regression (bounded) → Sigmoid/Tanh
│   └── Regression (unbounded) → Linear (none)
│
└── Hidden Layers?
    ├── Default choice → ReLU
    ├── Dying ReLU problem? → Leaky ReLU or ELU
    ├── Need smooth gradients? → Swish or GELU
    ├── Transformer architecture? → GELU
    ├── Need self-normalization? → SELU (with LeCun init)
    └── Very deep network? → ReLU with proper init
```

### Layer-Specific Recommendations
```
CNN Hidden Layers:
└── ReLU (most common), Leaky ReLU

RNN/LSTM Gates:
└── Sigmoid (gates), Tanh (candidate states)

Transformer:
└── GELU (attention) or Swish

GAN Generator:
└── ReLU or Leaky ReLU (hidden), Tanh (output)

GAN Discriminator:
└── Leaky ReLU (hidden), Sigmoid or none (output)
```

---

## 4.3 Gradient Flow and Vanishing/Exploding Gradients

### Problem Summary
```
Vanishing Gradients:
├── Cause: Repeated multiplication of small gradients (<1)
├── Affected: Sigmoid, Tanh (saturating activations)
├── Symptoms: Early layers don't learn, loss plateaus
└── Solutions: ReLU family, skip connections, proper init

Exploding Gradients:
├── Cause: Repeated multiplication of large gradients (>1)
├── Affected: Any activation with unconstrained output
├── Symptoms: NaN values, loss shoots up
└── Solutions: Gradient clipping, batch normalization
```

### Mitigation Strategies by Activation

| Strategy | Vanishing | Exploding |
|----------|-----------|-----------|
| Use ReLU | ✓ | Neutral |
| Skip Connections (ResNet) | ✓ | Neutral |
| Batch Normalization | ✓ | ✓ |
| Gradient Clipping | - | ✓ |
| Proper Initialization | ✓ | ✓ |
| Layer Normalization | ✓ | ✓ |
| Careful LR scheduling | ✓ | ✓ |

### ReLU Variants Comparison

| Variant | Dead Neuron Problem | Smoothness | Computation |
|---------|--------------------:|:-----------|:------------|
| ReLU | Yes | Not smooth at 0 | Fastest |
| Leaky ReLU | No (α gradient) | Not smooth at 0 | Fast |
| PReLU | No (learned α) | Not smooth at 0 | Fast + params |
| ELU | No | Smooth | exp() needed |
| SELU | No | Smooth | exp() needed |
| Swish | No | Smooth | sigmoid needed |
| GELU | No | Smooth | Complex |

---

# 5. Evaluation Metric Comparisons

## 5.1 Accuracy vs Precision vs Recall vs F1-Score

| Metric | Formula | Focus | Best When |
|--------|---------|-------|-----------|
| **Accuracy** | (TP+TN)/(TP+TN+FP+FN) | Overall correctness | Balanced classes |
| **Precision** | TP/(TP+FP) | Positive predictions | Cost of FP high |
| **Recall** | TP/(TP+FN) | Actual positives | Cost of FN high |
| **F1-Score** | 2·(P·R)/(P+R) | Balance P & R | Imbalanced data |

### Confusion Matrix Reference
```
                    Predicted
                  Pos     Neg
             ┌────────┬────────┐
Actual  Pos  │   TP   │   FN   │  ← Recall = TP/(TP+FN)
             ├────────┼────────┤
        Neg  │   FP   │   TN   │
             └────────┴────────┘
                  ↓
           Precision = TP/(TP+FP)
```

### Trade-offs Visualization
```
Precision-Recall Trade-off:

High Threshold (conservative predictions):
├── ↑ Precision (fewer false positives)
└── ↓ Recall (more false negatives)

Low Threshold (liberal predictions):
├── ↓ Precision (more false positives)
└── ↑ Recall (fewer false negatives)
```

### When to Use
```
Accuracy:
├── Balanced classes
├── Equal cost of errors
└── Quick baseline metric

Precision:
├── Spam detection (don't mark good emails as spam)
├── Fraud detection (don't block legitimate transactions)
├── Recommender systems (quality of recommendations)
└── When FP is costly

Recall (Sensitivity):
├── Disease diagnosis (catch all sick patients)
├── Fraud detection (catch all fraud, even if some false alarms)
├── Search engines (return all relevant results)
└── When FN is costly

F1-Score:
├── Imbalanced datasets
├── Need single metric balancing P & R
├── When both FP and FN matter
└── Information retrieval
```

---

## 5.2 ROC-AUC vs PR-AUC

| Metric | X-Axis | Y-Axis | Best When |
|--------|--------|--------|-----------|
| **ROC-AUC** | FPR | TPR (Recall) | Balanced classes |
| **PR-AUC** | Recall | Precision | Imbalanced classes |

### Curve Interpretation
```
ROC Curve:
  TPR │    ┌──────
      │   ╱
      │  ╱
      │ ╱  Area = AUC
      │╱
      └────────────
             FPR
  
  - Area of 0.5 = random classifier
  - Area of 1.0 = perfect classifier
  - Insensitive to class imbalance

PR Curve:
  Prec│
      │\
      │ \
      │  \  Area = AP
      │   \___
      └────────────
           Recall
           
  - Baseline = proportion of positive class
  - Very sensitive to imbalance
  - Better for rare events
```

### When to Use
```
ROC-AUC:
├── Balanced datasets
├── Comparing classifiers across thresholds
├── When TN rate matters (class 0 predictions)
└── Standard reporting metric

PR-AUC (Average Precision):
├── Highly imbalanced datasets (<5% positive)
├── Rare event detection
├── When TN doesn't matter
├── Information retrieval
└── Medical diagnosis, fraud detection
```

### Common Misconception
```
⚠️ High ROC-AUC doesn't mean good performance on imbalanced data!

Example (1% positive class):
- Classifier: predict everything negative
- Accuracy: 99%
- ROC-AUC: ~0.5 (random)
- PR-AUC: ~0.01 (terrible, correctly reflects)

→ Always use PR-AUC for imbalanced problems
```

---

## 5.3 Regression Metrics: MSE vs MAE vs RMSE vs MAPE vs Huber

| Metric | Formula | Outlier Sensitivity | Interpretation |
|--------|---------|--------------------:|:---------------|
| **MSE** | (1/n)Σ(y-ŷ)² | High | Squared error |
| **RMSE** | √MSE | High | Same scale as y |
| **MAE** | (1/n)Σ|y-ŷ| | Low | Absolute error |
| **MAPE** | (100/n)Σ|(y-ŷ)/y| | Medium | Percentage error |
| **Huber** | Quadratic near 0, linear far | Medium | Robust MSE |

### Mathematical Details
```
MSE:   L = (1/n)Σ(yᵢ - ŷᵢ)²
       - Penalizes large errors more (squared)
       - Differentiable everywhere
       
RMSE:  L = √[(1/n)Σ(yᵢ - ŷᵢ)²]
       - Same scale as target
       - Most commonly reported
       
MAE:   L = (1/n)Σ|yᵢ - ŷᵢ|
       - Equal penalty at all scales
       - Not differentiable at 0
       
MAPE:  L = (100/n)Σ|(yᵢ - ŷᵢ)/yᵢ|
       - Percentage-based
       - Undefined when y = 0
       
Huber: L = { 0.5(y-ŷ)²        if |y-ŷ| ≤ δ
           { δ|y-ŷ| - 0.5δ²   if |y-ŷ| > δ
       - Best of both MSE and MAE
```

### When to Use
```
MSE/RMSE:
├── Most common default
├── When outliers are important signal
├── Differentiable optimization
├── Report RMSE for interpretability

MAE:
├── Outliers should be downweighted
├── Robust predictions needed
├── When median prediction preferred
└── Financial forecasting

MAPE:
├── Business contexts (% error intuitive)
├── When understanding relative error matters
├── Avoid when target can be near zero
└── Demand forecasting

Huber:
├── Want MSE benefits with outlier robustness
├── δ controls transition point
└── Regression with noisy data
```

---

## 5.4 Micro vs Macro vs Weighted Averaging

| Averaging | Calculation | Effect | Best When |
|-----------|-------------|--------|-----------|
| **Micro** | Global TP, FP, FN | Dominated by majority | All samples equal |
| **Macro** | Average of per-class | Equal weight to classes | Classes equally important |
| **Weighted** | Size-weighted average | Accounts for imbalance | Proportionally weight classes |

### Example Calculation
```
3-class problem:
Class A: 100 samples, precision = 0.90
Class B: 50 samples,  precision = 0.80
Class C: 10 samples,  precision = 0.60

Micro-precision:
  = total_TP / (total_TP + total_FP)
  = global calculation across all classes
  
Macro-precision:
  = (0.90 + 0.80 + 0.60) / 3 = 0.767
  = simple average (each class counts equally)
  
Weighted-precision:
  = (100×0.90 + 50×0.80 + 10×0.60) / 160
  = (90 + 40 + 6) / 160 = 0.85
  = size-weighted average
```

### When to Use
```
Micro:
├── Large imbalanced datasets
├── When overall accuracy matters
├── Multi-label classification
└── Same as accuracy for single-label

Macro:
├── When all classes equally important
├── Regardless of class size
├── Penalizes poor performance on minority classes
└── Class-balanced evaluation

Weighted:
├── Account for class imbalance
├── Business impact proportional to class size
├── More realistic overall assessment
└── Default for sklearn reports
```

---

## 5.5 Cohen's Kappa vs Matthews Correlation Coefficient

| Metric | Range | Accounts For | Best For |
|--------|-------|--------------|----------|
| **Cohen's Kappa** | [-1, 1] | Chance agreement | Inter-rater reliability |
| **MCC** | [-1, 1] | All quadrants | Imbalanced binary classification |

### Mathematical Formulas
```
Cohen's Kappa:
  κ = (p₀ - pₑ) / (1 - pₑ)
  
  p₀ = observed agreement (accuracy)
  pₑ = expected chance agreement
  
  Interpretation:
  < 0    : Less than chance
  0-0.2  : Slight
  0.2-0.4: Fair
  0.4-0.6: Moderate
  0.6-0.8: Substantial
  0.8-1.0: Almost perfect

Matthews Correlation Coefficient:
  MCC = (TP·TN - FP·FN) / √[(TP+FP)(TP+FN)(TN+FP)(TN+FN)]
  
  Interpretation:
  -1 : Perfect disagreement
   0 : Random prediction
  +1 : Perfect prediction
```

### When to Use
```
Cohen's Kappa:
├── Comparing human annotators
├── When chance agreement matters
├── Multi-class classification
├── Medical diagnosis agreement
└── Crowdsourcing quality control

MCC:
├── Imbalanced binary classification
├── More informative than accuracy/F1
├── When all quadrants matter equally
├── Preferred for bioinformatics
└── Captures full confusion matrix info
```

### Key Insight
```
⚠️ Why MCC is often better than F1:

F1 ignores True Negatives (TN)
MCC uses all four quadrants: TP, TN, FP, FN

Example:
- 99% negative class
- Classifier predicts all negative
- F1 = 0 (correctly shows failure)
- But F1 ignores the 99% TN

MCC properly accounts for this imbalance
and gives a more balanced picture.
```

---

# 6. Model Complexity Comparisons

## 6.1 Parametric vs Non-parametric Models

| Aspect | Parametric | Non-parametric |
|--------|------------|----------------|
| **Parameters** | Fixed number | Grows with data |
| **Assumptions** | Strong (distribution) | Weak |
| **Training** | Estimate parameters | Store data |
| **Flexibility** | Lower | Higher |
| **Overfitting Risk** | Lower | Higher |
| **Inference Speed** | Fast | Slow (often) |

### Examples
```
Parametric:
├── Linear Regression (w, b)
├── Logistic Regression
├── Naive Bayes
├── Neural Networks (fixed architecture)
└── LDA

Non-parametric:
├── K-Nearest Neighbors
├── Decision Trees (can grow with data)
├── Kernel SVM
├── Random Forests
└── Gaussian Processes
```

### Trade-offs
```
Data Requirements:
├── Parametric: Works with less data if assumptions hold
└── Non-parametric: Needs more data, but fewer assumptions

Interpretability:
├── Parametric: Often easier to interpret (coefficients)
└── Non-parametric: Can be complex (except trees)

Scalability:
├── Parametric: Typically better scaling
└── Non-parametric: May struggle with large datasets
```

---

## 6.2 Generative vs Discriminative Models

| Aspect | Generative | Discriminative |
|--------|------------|----------------|
| **Models** | P(X, Y) = P(X|Y)·P(Y) | P(Y|X) directly |
| **Generation** | Can generate new X | Cannot generate |
| **Training** | Often faster | Often more accurate |
| **Missing Data** | Handles well | May struggle |
| **Assumptions** | Strong (data distribution) | Weaker |

### Examples
```
Generative Models:
├── Naive Bayes
├── Gaussian Mixture Models
├── Hidden Markov Models
├── VAEs, GANs
├── LDA (topic models)
└── Language Models (GPT)

Discriminative Models:
├── Logistic Regression
├── SVM
├── Decision Trees
├── Neural Networks (classifiers)
├── CRFs
└── BERT (classification)
```

### When to Use
```
Generative:
├── Need to generate new samples
├── Missing data is common
├── Want interpretable components
├── Semi-supervised learning
└── Anomaly detection

Discriminative:
├── Classification accuracy is primary
├── Large labeled dataset available
├── Complex decision boundaries needed
└── Computational efficiency important
```

---

## 6.3 Online vs Batch Learning

| Aspect | Online | Batch |
|--------|--------|-------|
| **Data Processing** | One at a time | All at once |
| **Memory** | O(1) - O(model) | O(n) for data |
| **Adaptation** | Continuous | Requires retraining |
| **Convergence** | Noisier | More stable |
| **Use Case** | Streaming data | Static datasets |

### Algorithm Support
```
Online Learning (supports incremental):
├── Stochastic Gradient Descent
├── Perceptron
├── Online Random Forest
├── Vowpal Wabbit algorithms
└── Reinforcement learning

Batch Learning:
├── Standard gradient descent
├── Most sklearn models
├── Tree ensembles (standard)
└── Most deep learning (in practice uses mini-batch)

Mini-batch (Hybrid):
├── Deep learning standard
├── Gets benefits of both
└── Most common in practice
```

### When to Use
```
Online Learning:
├── Data doesn't fit in memory
├── Streaming real-time data
├── Concept drift (distribution changes)
├── Continuous learning systems
└── Recommendation systems

Batch Learning:
├── Static historical datasets
├── Need reproducible results
├── Have compute for full passes
└── Most training scenarios
```

---

## 6.4 Eager vs Lazy Learning

| Aspect | Eager | Lazy |
|--------|-------|------|
| **Training Time** | High (builds model) | None |
| **Prediction Time** | Fast | Slow (compute at query) |
| **Storage** | Model parameters | All training data |
| **Generalization** | Global model | Local approximation |

### Examples
```
Eager Learning:
├── Decision Trees (build once)
├── Neural Networks
├── SVM
├── Naive Bayes
└── Most ML algorithms

Lazy Learning:
├── K-Nearest Neighbors
├── Locally Weighted Regression
├── Case-Based Reasoning
└── Lazy Decision Trees
```

### Trade-offs
```
Eager:
├── ✓ Fast prediction
├── ✓ Compact model
├── ✗ Can't easily add new data
└── ✗ May miss local patterns

Lazy:
├── ✓ Adapts to local structure
├── ✓ Easy to add new data
├── ✗ Slow prediction
└── ✗ High storage requirements
```

---

## 6.5 Instance-based vs Model-based Learning

| Aspect | Instance-based | Model-based |
|--------|----------------|-------------|
| **Storage** | Training instances | Parameters/structure |
| **Prediction** | Compare to stored instances | Apply learned function |
| **Adaptation** | Add/remove instances | Retrain model |
| **Interpretability** | Examples-based explanation | Model-based explanation |

### Examples and Use Cases
```
Instance-based:
├── K-Nearest Neighbors
├── Case-Based Reasoning
├── RBF Networks (hybrid)
├── Memory Networks
└── Few-shot learning (prototype networks)

Model-based:
├── Linear/Logistic Regression
├── Neural Networks
├── Decision Trees
├── SVM
└── Most ML algorithms
```

### When to Choose
```
Instance-based:
├── Explanations via similar cases important
├── Few training examples
├── Distribution may change (just update examples)
└── k-NN style problems

Model-based:
├── Need efficient predictions
├── Large datasets
├── Want generalizable patterns
└── Production deployment
```

---

# 7. Data Handling Comparisons

## 7.1 Train-Test Split vs Cross-Validation vs Time Series Split

| Method | Data Usage | Variance | Best For |
|--------|------------|----------|----------|
| **Train-Test Split** | Single split | High | Large datasets, quick eval |
| **K-Fold CV** | K splits, rotate test | Lower | Small-medium datasets |
| **Stratified K-Fold** | K splits, preserve class ratio | Lower | Imbalanced classification |
| **Time Series Split** | Temporal order preserved | Low | Sequential/temporal data |

### Visualization
```
Train-Test Split (80/20):
[========== Train ===========][== Test ==]

5-Fold Cross-Validation:
Fold 1: [Test][====== Train ======]
Fold 2: [Train][Test][=== Train ===]
Fold 3: [= Train =][Test][= Train =]
Fold 4: [=== Train ===][Test][Train]
Fold 5: [====== Train ======][Test]

Time Series Split:
Fold 1: [Train][Test]
Fold 2: [== Train ==][Test]
Fold 3: [==== Train ====][Test]
Fold 4: [====== Train ======][Test]
         ↑ Always uses past data
```

### When to Use
```
Train-Test Split:
├── Very large datasets (>1M samples)
├── Quick prototyping
├── When training is expensive
└── Final model evaluation

K-Fold Cross-Validation:
├── Small to medium datasets
├── Want stable performance estimate
├── Hyperparameter tuning
└── Model selection

Stratified K-Fold:
├── Imbalanced classification
├── Preserve class distribution
└── Standard for classification

Time Series Split:
├── Temporal/sequential data
├── Avoid data leakage from future
├── Financial, weather, sales data
└── When order matters
```

### Common Pitfalls
```
⚠️ Data Leakage Issues:

1. Shuffling time series data
   ✗ Random split on stock prices
   ✓ Use time series split

2. Preprocessing before split
   ✗ StandardScaler.fit(all_data)
   ✓ Fit only on training fold

3. Feature selection leakage
   ✗ Select features on full data
   ✓ Select features within CV loop
```

---

## 7.2 Undersampling vs Oversampling vs SMOTE vs Class Weights

| Method | Approach | Data Size | Risk |
|--------|----------|-----------|------|
| **Undersampling** | Remove majority samples | Decreases | Lose information |
| **Oversampling** | Duplicate minority samples | Increases | Overfitting |
| **SMOTE** | Generate synthetic minority | Increases | Noise amplification |
| **Class Weights** | Weight loss function | Same | None |

### How Each Works
```
Original Data (10:1 imbalance):
Majority: ○○○○○○○○○○ (100)
Minority: ●          (10)

Undersampling:
Majority: ○          (10) ← Random subset
Minority: ●          (10)

Oversampling:
Majority: ○○○○○○○○○○ (100)
Minority: ●●●●●●●●●● (100) ← Duplicates

SMOTE (Synthetic Minority Oversampling):
Majority: ○○○○○○○○○○ (100)
Minority: ●★★★★★★★★● (100) ← Synthetic points

Class Weights:
Loss = Σ wᵢ · L(yᵢ, ŷᵢ)
w_minority = n_total / (n_classes × n_minority)
```

### When to Use
```
Undersampling:
├── Large dataset with many majority samples
├── Majority class has redundancy
├── RandomUnderSampler, NearMiss
└── Combine with ensemble (EasyEnsemble)

Oversampling:
├── Very small minority class
├── Simple approach needed
├── RandomOverSampler
└── Often combined with undersampling

SMOTE:
├── Classification problems
├── Continuous features
├── Moderate imbalance (2:1 to 10:1)
├── Variants: SMOTE-NC (categorical), BorderlineSMOTE
└── Apply only to training data!

Class Weights:
├── When want to keep all data
├── Most algorithms support it
├── class_weight='balanced' in sklearn
└── Focal Loss for severe imbalance
```

### Important Notes
```
⚠️ Critical Rules:

1. Apply resampling ONLY to training data
   ✗ SMOTE on full data, then split
   ✓ Split first, then SMOTE training set

2. For SMOTE:
   - Works best with numeric features
   - Can amplify noise
   - Combine with Tomek Links or ENN

3. Ensemble of balanced subsets often best
   - BalancedRandomForestClassifier
   - EasyEnsembleClassifier
```

---

## 7.3 Encoding: One-Hot vs Label vs Target vs Embedding

| Method | Output | Cardinality | Use With |
|--------|--------|-------------|----------|
| **One-Hot** | Binary columns | Low (<50) | Linear, Tree models |
| **Label** | Integer | Any | Tree models |
| **Target** | Continuous | High | Linear, NN |
| **Embedding** | Dense vectors | Very high | Neural Networks |

### How Each Works
```
Original: ['cat', 'dog', 'bird', 'cat', 'bird']

One-Hot Encoding:
   cat  dog  bird
   [1,   0,   0]
   [0,   1,   0]
   [0,   0,   1]
   [1,   0,   0]
   [0,   0,   1]

Label Encoding:
   [0, 1, 2, 0, 2]

Target Encoding (for y=[0,1,0,1,0]):
   cat  → mean(y where cat)  = 0.5
   dog  → mean(y where dog)  = 1.0
   bird → mean(y where bird) = 0.0
   [0.5, 1.0, 0.0, 0.5, 0.0]

Embedding (learned 2D):
   cat  → [0.3, 0.8]
   dog  → [0.9, 0.1]
   bird → [0.5, 0.5]
```

### When to Use
```
One-Hot:
├── Low cardinality (<50 categories)
├── No ordinal relationship
├── Tree-based models (works well)
├── Linear models (required)
└── Interpretability needed

Label Encoding:
├── Ordinal features (low/medium/high)
├── Tree-based models (can handle)
├── Reduces dimensionality
└── ✗ Avoid for linear models (implies order)

Target Encoding:
├── High cardinality features
├── Strong category-target relationship
├── Use cross-validation to avoid leakage!
├── Smoothing for rare categories
└── CatBoost uses this internally

Embedding:
├── Very high cardinality (users, products)
├── Neural networks
├── Learn semantic relationships
├── NLP (word embeddings)
└── Recommender systems
```

---

## 7.4 Scaling: Min-Max vs Standardization vs Robust

| Method | Formula | Range | Outlier Sensitivity |
|--------|---------|-------|--------------------:|
| **Min-Max** | (x-min)/(max-min) | [0, 1] | High |
| **Standard (Z-score)** | (x-μ)/σ | ~[-3, 3] | Medium |
| **Robust** | (x-median)/IQR | Unbounded | Low |

### Mathematical Details
```
Min-Max Scaling:
  x' = (x - x_min) / (x_max - x_min)
  - Bounded to [0, 1]
  - Outliers compress range
  - Preserves zero entries

Standard Scaling (Z-score):
  x' = (x - μ) / σ
  - Mean = 0, Std = 1
  - Unbounded range
  - Assumes roughly normal

Robust Scaling:
  x' = (x - median) / (Q75 - Q25)
  - Uses median & IQR
  - Ignores outliers
  - Good for skewed data
```

### Visual Comparison
```
Original with outlier:
[1, 2, 3, 4, 5, 100]

Min-Max: [0, 0.01, 0.02, 0.03, 0.04, 1.0]
         ↑ Compressed by outlier

Standard: [-0.45, -0.42, -0.39, -0.36, -0.33, 2.56]
          ↑ Mean=0, but outlier still affects

Robust:   [-0.5, -0.25, 0, 0.25, 0.5, 32.3]
          ↑ Main distribution preserved
```

### When to Use
```
Min-Max Scaling:
├── Neural networks (bounded activations)
├── Image data (pixel values)
├── K-means clustering
├── When [0,1] range required
└── No significant outliers

Standardization (Z-score):
├── Most algorithms (default choice)
├── SVM, Logistic Regression
├── PCA, LDA
├── Gradient descent optimization
└── Reasonably normal distribution

Robust Scaling:
├── Data contains outliers
├── Don't want to remove outliers
├── Skewed distributions
└── More stable feature ranges
```

### Important Notes
```
⚠️ Scaling Best Practices:

1. Fit scaler on TRAINING data only
   scaler.fit(X_train)
   X_train_scaled = scaler.transform(X_train)
   X_test_scaled = scaler.transform(X_test)

2. Some algorithms don't need scaling:
   - Tree-based (Random Forest, XGBoost)
   - Naive Bayes

3. Always scale when using:
   - Distance-based (KNN, SVM, K-means)
   - Gradient descent (Neural Networks)
   - Regularization (Lasso, Ridge)
```

---

## 7.5 Feature Selection vs Feature Extraction

| Aspect | Feature Selection | Feature Extraction |
|--------|-------------------|-------------------|
| **Method** | Choose subset | Create new features |
| **Original Features** | Kept | Transformed |
| **Interpretability** | High | Lower |
| **Information** | Some discarded | Compressed |

### Methods Overview
```
Feature Selection:
├── Filter Methods (statistical)
│   ├── Variance Threshold
│   ├── Correlation
│   ├── Chi-square
│   └── Mutual Information
├── Wrapper Methods (model-based)
│   ├── Forward Selection
│   ├── Backward Elimination
│   └── Recursive Feature Elimination (RFE)
└── Embedded Methods (during training)
    ├── L1 Regularization (Lasso)
    ├── Tree Feature Importance
    └── ElasticNet

Feature Extraction:
├── Linear
│   ├── PCA (Principal Component Analysis)
│   ├── LDA (Linear Discriminant Analysis)
│   └── SVD (Singular Value Decomposition)
├── Non-linear
│   ├── t-SNE
│   ├── UMAP
│   ├── Autoencoders
│   └── Kernel PCA
└── Domain-specific
    ├── CNN features (images)
    ├── Word embeddings (text)
    └── Fourier transforms (signals)
```

### When to Use
```
Feature Selection:
├── Interpretability is important
├── Want to understand which features matter
├── Reduce overfitting (fewer features)
├── Speed up training
└── Curse of dimensionality

Feature Extraction:
├── High-dimensional data
├── Correlated features
├── Want compressed representation
├── Visualization (t-SNE, UMAP)
├── Preprocessing for ML pipeline
└── Transfer learning (CNN features)
```

---

# 8. Problem Type Comparisons

## 8.1 Classification vs Regression vs Clustering

| Aspect | Classification | Regression | Clustering |
|--------|---------------|------------|------------|
| **Output** | Discrete classes | Continuous values | Group assignments |
| **Supervision** | Supervised | Supervised | Unsupervised |
| **Goal** | Predict category | Predict quantity | Find structure |
| **Examples** | Spam detection | Price prediction | Customer segments |

### Decision Guide
```
What type of problem?

Target variable exists?
├── Yes → Is target categorical?
│         ├── Yes → Classification
│         └── No → Regression
└── No → Clustering (or other unsupervised)

Target type details:
├── Binary (0/1) → Binary Classification
├── Multiple classes → Multi-class Classification
├── Multiple labels per sample → Multi-label Classification
├── Continuous → Regression
└── No target → Clustering, Dimensionality Reduction
```

### Algorithm Mapping

| Problem | Common Algorithms |
|---------|------------------|
| Classification | Logistic Regression, SVM, Random Forest, Neural Networks |
| Regression | Linear Regression, XGBoost, Neural Networks |
| Clustering | K-Means, DBSCAN, Hierarchical, GMM |

---

## 8.2 Learning Paradigms: Supervised vs Unsupervised vs Semi-supervised vs RL

| Paradigm | Labels | Goal | Examples |
|----------|--------|------|----------|
| **Supervised** | All labeled | Predict labels | Classification, Regression |
| **Unsupervised** | None | Find patterns | Clustering, Dim reduction |
| **Semi-supervised** | Some labeled | Use both | Label propagation |
| **Reinforcement** | Rewards | Maximize reward | Game playing, Robotics |

### Visual Comparison
```
Supervised:
  Input → [Model] → Output
    ↑                  ↑
  (X, y)            Compare with y, update

Unsupervised:
  Input → [Model] → Structure (no labels!)
    ↑
  (X only)

Semi-supervised:
  Input → [Model] → Output
    ↑
  (X_labeled, y) + (X_unlabeled)
  Use unlabeled to improve

Reinforcement Learning:
  State → [Agent] → Action → Environment → Reward
    ↑___________________________|
         (learn to maximize reward)
```

### When to Use
```
Supervised Learning:
├── Have labeled data
├── Clear input-output relationship
├── Most common in practice
└── Classification, Regression

Unsupervised Learning:
├── No labels available
├── Exploratory data analysis
├── Customer segmentation
├── Anomaly detection
└── Dimensionality reduction

Semi-supervised Learning:
├── Some labels, lots of unlabeled data
├── Labeling is expensive
├── Medical imaging
├── NLP with limited annotations
└── Pseudo-labeling, self-training

Reinforcement Learning:
├── Sequential decision making
├── Game playing (AlphaGo)
├── Robotics, control
├── Recommendation systems
└── When reward signal available
```

---

## 8.3 Single-label vs Multi-label vs Multi-class Classification

| Type | Classes per Sample | Example |
|------|-------------------|---------|
| **Binary** | 1 of 2 | Spam vs Not-Spam |
| **Multi-class** | 1 of N | Cat vs Dog vs Bird |
| **Multi-label** | Multiple of N | Movie genres |

### Visual Example
```
Binary:
  Sample → [Spam] or [Not Spam]
           (exactly one)

Multi-class:
  Sample → [Cat] or [Dog] or [Bird]
           (exactly one)

Multi-label:
  Sample → [Action] + [Comedy] + [Romance]
           (zero or more)
           
  Movie "The Hangover" → [Comedy: 1, Action: 0, Drama: 0, Romance: 1]
```

### Implementation Differences

| Aspect | Multi-class | Multi-label |
|--------|-------------|-------------|
| Output layer | Softmax (sums to 1) | Sigmoid (per class) |
| Loss | Categorical CE | Binary CE (per label) |
| Prediction | argmax | threshold per label |
| Metrics | Accuracy, F1-macro | Hamming loss, Sample F1 |

### Code Pattern
```python
# Multi-class
output = softmax(logits)  # [0.1, 0.7, 0.2] sums to 1
prediction = argmax(output)  # 1 (Dog)

# Multi-label
output = sigmoid(logits)  # [0.8, 0.3, 0.9] independent
prediction = output > 0.5  # [1, 0, 1] (Action, Romance)
```

---

## 8.4 Binary vs Multiclass Classification Approaches

| Approach | Description | Use Case |
|----------|-------------|----------|
| **Native Multiclass** | Single model, N outputs | Softmax, Decision Trees |
| **One-vs-Rest (OvR)** | N binary classifiers | SVM, Logistic Regression |
| **One-vs-One (OvO)** | N(N-1)/2 classifiers | SVM (some implementations) |

### How Each Works
```
3-class problem: A, B, C

Native Multiclass:
  Single model → [P(A), P(B), P(C)]
  Decision Trees, Neural Networks, Naive Bayes

One-vs-Rest (OvR):
  Classifier 1: A vs (B, C)
  Classifier 2: B vs (A, C)
  Classifier 3: C vs (A, B)
  → Pick class with highest score

One-vs-One (OvO):
  Classifier 1: A vs B
  Classifier 2: A vs C
  Classifier 3: B vs C
  → Voting: each classifier votes for winner
```

### Comparison

| Aspect | OvR | OvO |
|--------|-----|-----|
| Number of classifiers | N | N(N-1)/2 |
| Training time | Lower | Higher |
| Each classifier | Imbalanced | Balanced |
| Prediction time | O(N) | O(N²) |

### When to Use
```
Native Multiclass:
├── Algorithm supports it (Trees, NN)
├── Most efficient
└── Default choice when available

One-vs-Rest:
├── Binary classifier only (SVM, LR)
├── sklearn default for these
├── Good for many classes
└── N classifiers

One-vs-One:
├── Certain SVM implementations
├── Better for imbalanced classes
├── More classifiers but smaller training sets
└── N(N-1)/2 classifiers
```

---

# 9. Framework and Library Comparisons

## 9.1 TensorFlow vs PyTorch vs JAX

| Aspect | TensorFlow | PyTorch | JAX |
|--------|------------|---------|-----|
| **Paradigm** | Graph-based (eager available) | Eager by default | Functional + JIT |
| **API Style** | Keras (high-level) | Pythonic | NumPy-like |
| **Debugging** | Harder (graph mode) | Easy (Python debugger) | Medium |
| **Production** | TF Serving, TFLite | TorchServe, ONNX | XLA, TPU-native |
| **Community** | Industry, Google | Research, Meta | Research, advanced |
| **Learning Curve** | Medium | Lower | Higher |

### Strengths and Weaknesses
```
TensorFlow:
├── ✓ Production pipelines (TF Serving, TFLite)
├── ✓ Keras for quick prototyping
├── ✓ TensorBoard visualization
├── ✓ Wide deployment options
├── ✗ Complex API (TF 1.x legacy)
└── ✗ Less flexible than PyTorch

PyTorch:
├── ✓ Pythonic and intuitive
├── ✓ Dynamic computation graph
├── ✓ Easy debugging
├── ✓ Strong research community
├── ✗ Production deployment evolving
└── ✗ Less mature mobile support

JAX:
├── ✓ Fastest transformations (jit, vmap, grad)
├── ✓ Pure functional approach
├── ✓ Best for TPUs
├── ✓ Cutting-edge research
├── ✗ Steepest learning curve
└── ✗ Smaller ecosystem
```

### When to Use
```
TensorFlow:
├── Production ML systems
├── Mobile/edge deployment (TFLite)
├── Google Cloud integration
├── Established enterprise projects
└── Need TensorBoard

PyTorch:
├── Research and experimentation
├── NLP and computer vision research
├── Quick prototyping
├── Learning deep learning
└── Default choice for most new projects

JAX:
├── Cutting-edge research
├── Need advanced autodiff (higher-order)
├── TPU-first development
├── When need vmap, pmap
└── Scientific computing with ML
```

---

## 9.2 Keras vs PyTorch Lightning

| Aspect | Keras (TF) | PyTorch Lightning |
|--------|------------|-------------------|
| **Backend** | TensorFlow | PyTorch |
| **Abstraction Level** | Very high | Medium-high |
| **Flexibility** | Limited | High |
| **Boilerplate Reduction** | Maximum | Significant |
| **Custom Loops** | Harder | Easy |

### Code Comparison
```python
# Keras
model = keras.Sequential([
    keras.layers.Dense(128, activation='relu'),
    keras.layers.Dense(10, activation='softmax')
])
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy')
model.fit(X_train, y_train, epochs=10)

# PyTorch Lightning
class Model(pl.LightningModule):
    def __init__(self):
        super().__init__()
        self.layer1 = nn.Linear(784, 128)
        self.layer2 = nn.Linear(128, 10)
    
    def forward(self, x):
        return F.softmax(self.layer2(F.relu(self.layer1(x))))
    
    def training_step(self, batch, batch_idx):
        x, y = batch
        loss = F.cross_entropy(self(x), y)
        return loss
```

### When to Use
```
Keras:
├── Quick prototyping
├── Standard architectures
├── Teaching/learning
├── When TensorFlow ecosystem needed
└── Simple projects

PyTorch Lightning:
├── Research with reproducibility
├── Complex training loops
├── Multi-GPU training
├── Custom architectures
└── Want PyTorch flexibility + structure
```

---

## 9.3 scikit-learn vs XGBoost vs LightGBM

| Aspect | scikit-learn | XGBoost | LightGBM |
|--------|-------------|---------|----------|
| **Focus** | General ML | Gradient Boosting | Gradient Boosting |
| **Speed** | Moderate | Fast | Fastest |
| **Algorithms** | Many | Tree-based | Tree-based |
| **GPU Support** | Limited | Yes | Yes |
| **API Style** | fit/predict | fit/predict | fit/predict |

### Coverage
```
scikit-learn covers:
├── Preprocessing (scaling, encoding)
├── Linear models
├── Tree-based models (basic)
├── SVM, KNN, Naive Bayes
├── Clustering (K-means, DBSCAN)
├── Dimensionality reduction (PCA, t-SNE)
├── Model selection (CV, GridSearch)
└── Metrics

XGBoost/LightGBM specialize in:
├── Gradient boosted trees
├── Handling missing values
├── Regularization
├── Feature importance
└── Competition-winning performance
```

### When to Use
```
scikit-learn:
├── Learning ML fundamentals
├── Quick baselines
├── Preprocessing pipelines
├── Non-tree-based algorithms
├── Standard ML tasks
└── Prototyping

XGBoost:
├── Tabular data competitions
├── When need GPU training
├── General gradient boosting
└── Wide compatibility

LightGBM:
├── Large datasets
├── Fastest training needed
├── Memory efficiency important
├── Many categorical features
└── Default for most tabular tasks
```

---

## 9.4 Pandas vs Polars vs Dask

| Aspect | Pandas | Polars | Dask |
|--------|--------|--------|------|
| **Language** | Python/C | Rust | Python |
| **Single Machine** | Yes | Yes | Optional |
| **Distributed** | No | Limited | Yes |
| **Speed** | Baseline | 10-100x faster | Comparable |
| **Memory** | High | Lower | Lazy eval |
| **API** | Standard | Similar + Lazy | Familiar |

### Performance Characteristics
```
Pandas:
├── In-memory only
├── Single-threaded (mostly)
├── Copying on many operations
└── Limited by RAM

Polars:
├── Multi-threaded by default
├── Lazy evaluation option
├── Zero-copy where possible
├── Apache Arrow backend
└── Rust performance

Dask:
├── Parallel Pandas
├── Distributed across cluster
├── Lazy evaluation
├── Familiar API
└── Out-of-core processing
```

### When to Use
```
Pandas:
├── Small datasets (<1GB)
├── Quick analysis
├── Wide ecosystem compatibility
├── Most tutorials/examples
└── Interactive exploration

Polars:
├── Medium-large datasets (1-100GB)
├── Performance critical
├── Single machine
├── Modern workflows
└── When Pandas too slow

Dask:
├── Very large datasets (>100GB)
├── Distributed computing needed
├── Parallel processing
├── Cluster environments
└── Want Pandas-like API at scale
```

---

## 9.5 Matplotlib vs Seaborn vs Plotly

| Aspect | Matplotlib | Seaborn | Plotly |
|--------|------------|---------|--------|
| **Level** | Low-level | High-level | High-level |
| **Interactive** | Static | Static | Interactive |
| **Customization** | Maximum | Good | Good |
| **Learning Curve** | Higher | Lower | Medium |
| **Output** | PNG, PDF | PNG, PDF | HTML, Web |

### Strengths
```
Matplotlib:
├── Full control over every element
├── Publication-quality figures
├── Extensive documentation
├── Base for other libraries
└── Any visualization possible

Seaborn:
├── Statistical visualizations
├── Beautiful defaults
├── Pandas integration
├── Complex plots in one line
└── Built-in themes

Plotly:
├── Interactive by default
├── Dashboards (Dash)
├── Web-native
├── 3D visualizations
└── Hover information
```

### When to Use
```
Matplotlib:
├── Publication figures
├── Custom/complex layouts
├── When need precise control
├── Base for custom visualizations
└── Animation

Seaborn:
├── Statistical analysis
├── Quick EDA
├── Distribution plots
├── Correlation heatmaps
├── Pair plots
└── Default for data science

Plotly:
├── Interactive dashboards
├── Web applications
├── 3D visualizations
├── Geographical plots
├── Presentations
└── When users need to explore data
```

---

# 10. Deep Learning Concept Comparisons

## 10.1 Transfer Learning vs Fine-tuning vs Training from Scratch

| Approach | Pretrained | New Data | Compute | Best When |
|----------|-----------|----------|---------|-----------|
| **From Scratch** | No | All | High | Large dataset, unique domain |
| **Transfer (Frozen)** | Yes, frozen | Small | Low | Similar domain, small data |
| **Fine-tuning** | Yes, trainable | Medium | Medium | Similar domain, more data |

### Visualization
```
Training from Scratch:
  Random Weights → Train all → Task-specific model
  (requires lots of data and compute)

Transfer Learning (Feature Extraction):
  Pretrained → [Frozen Backbone] → [New Head] → Train head only
  (use pretrained as fixed feature extractor)

Fine-tuning:
  Pretrained → [Trainable Backbone] → [New Head] → Train all
  (often with lower LR for backbone)
```

### Implementation Pattern
```python
# From Scratch
model = MyModel()
train(model, data)  # Full training

# Transfer Learning (Frozen)
backbone = load_pretrained("resnet50")
for param in backbone.parameters():
    param.requires_grad = False
model = nn.Sequential(backbone, nn.Linear(2048, num_classes))
train(model, data)  # Only trains Linear layer

# Fine-tuning
backbone = load_pretrained("resnet50")
model = nn.Sequential(backbone, nn.Linear(2048, num_classes))
optimizer = Adam([
    {'params': backbone.parameters(), 'lr': 1e-5},  # Lower LR
    {'params': model[-1].parameters(), 'lr': 1e-3}  # Higher LR
])
train(model, data)
```

### Decision Guide
```
How much data do you have?
├── Very little (<1000) → Transfer Learning (frozen)
├── Medium (1000-10000) → Fine-tuning
└── Large (>100000) → Consider from scratch

How similar is your domain?
├── Very similar → Transfer works well
├── Somewhat similar → Fine-tune heavily
└── Very different → May need from scratch
```

---

## 10.2 Pre-training vs Multi-task Learning

| Aspect | Pre-training | Multi-task |
|--------|-------------|------------|
| **When** | Before downstream | Simultaneously |
| **Tasks** | Usually one | Multiple |
| **Data Sharing** | Sequential | Concurrent |
| **Goal** | Learn representations | Learn shared + task-specific |

### Architecture
```
Pre-training:
  Phase 1: [Encoder] ← Train on pretext task (MLM, next token)
  Phase 2: [Encoder] + [Task Head] ← Fine-tune on downstream

Multi-task Learning:
                        ┌→ [Task Head A] → Output A
  Input → [Shared Encoder] ┼→ [Task Head B] → Output B
                        └→ [Task Head C] → Output C
  (trained jointly on all tasks)
```

### When to Use
```
Pre-training:
├── Have large unlabeled corpus
├── Downstream tasks benefit from representations
├── BERT, GPT, image pretraining
├── Foundation model development
└── When single task is final goal

Multi-task Learning:
├── Related tasks with shared structure
├── Limited data per task
├── Want to regularize via task diversity
├── NLU (NER + POS + parsing)
└── When multiple tasks are deployment goals
```

---

## 10.3 Attention: Self-Attention vs Cross-Attention

| Type | Query | Key/Value | Used In |
|------|-------|-----------|---------|
| **Self-Attention** | Same sequence | Same sequence | BERT, GPT (within) |
| **Cross-Attention** | Target sequence | Source sequence | Transformer decoder |

### Mechanism
```
Self-Attention (e.g., in encoder):
  Input: X = [x₁, x₂, x₃]
  Q, K, V all come from X
  
  Each position attends to all positions:
  x₁ → attends to [x₁, x₂, x₃]
  x₂ → attends to [x₁, x₂, x₃]
  x₃ → attends to [x₁, x₂, x₃]

Cross-Attention (e.g., in decoder):
  Query: from decoder (target)
  Key, Value: from encoder (source)
  
  Decoder position attends to encoder:
  y₁ → attends to [x₁, x₂, x₃] (encoder output)
  y₂ → attends to [x₁, x₂, x₃]
```

### Applications
```
Self-Attention:
├── BERT encoder (bidirectional)
├── GPT decoder (masked/causal)
├── Vision Transformer (patches attend to patches)
└── Understanding context within sequence

Cross-Attention:
├── Transformer decoder attending to encoder
├── Translation (target attends to source)
├── Image captioning (text attends to image)
├── Multimodal fusion
└── Any encoder-decoder architecture
```

---

## 10.4 Encoder-only vs Decoder-only vs Encoder-Decoder

| Architecture | Examples | Pre-training | Best For |
|-------------|----------|--------------|----------|
| **Encoder-only** | BERT, RoBERTa | MLM | Understanding |
| **Decoder-only** | GPT, LLaMA | Causal LM | Generation |
| **Encoder-Decoder** | T5, BART | Various | Sequence-to-sequence |

### Architecture Diagrams
```
Encoder-only (BERT):
  [CLS] The cat [MASK] → [Encoder] → [Contextualized repr]
                                           ↓
                                    [Classification head]
  (Bidirectional, good for understanding)

Decoder-only (GPT):
  The cat sat → [Decoder] → on
  The cat sat on → [Decoder] → the
  (Left-to-right only, good for generation)

Encoder-Decoder (T5):
  "translate: Hello" → [Encoder] → [Decoder] → "Hola"
  (Encoder: bidirectional, Decoder: causal)
```

### When to Use
```
Encoder-only (BERT-style):
├── Text classification
├── Named entity recognition
├── Sentence embeddings
├── Question answering (extractive)
└── When understanding > generation

Decoder-only (GPT-style):
├── Text generation
├── Chatbots, dialogue
├── Code generation
├── Few-shot learning
└── When generation is primary

Encoder-Decoder (T5-style):
├── Translation
├── Summarization
├── Question answering (generative)
├── Text-to-text tasks
└── When input and output are different
```

---

## 10.5 Feature Extraction: Convolution vs Pooling vs Attention

| Operation | Purpose | Learnable | Locality |
|-----------|---------|-----------|----------|
| **Convolution** | Extract features | Yes (kernels) | Local |
| **Pooling** | Downsample, invariance | No | Local |
| **Attention** | Weighted aggregation | Yes (QKV) | Global |

### How Each Works
```
Convolution:
  [Input Image] → [3x3 kernel slides] → [Feature Map]
  Learns local patterns (edges, textures)
  Parameters: kernel weights

Pooling:
  [2x2 region] → max(values) or mean(values)
  Reduces spatial dimensions
  No learnable parameters

Attention:
  [All positions] → weighted sum based on relevance
  Global relationships
  Learns Query, Key, Value projections
```

### Comparison
```
                Local → ← Global
                  ↓         ↓
Convolution ━━━━━━━━━━●
Pooling     ━━━━━━━━━━●
Attention   ━━━━━━━━━━━━━━━━━━━●

Computational cost:
├── Convolution: O(k²·c·n)  Linear in input
├── Pooling: O(n)           Very cheap
└── Attention: O(n²)        Quadratic (costly for long)
```

### Modern Trends
```
Vision:
├── Traditional: Conv → Pool → Conv → Pool → FC
├── ResNet: Conv + Skip connections
├── ViT: Attention (patches as tokens)
└── Hybrid: Conv for early, Attention for later

NLP:
├── Pre-Transformer: Conv1D, RNN + Attention
├── Transformer: All attention
└── Efficient: Linear attention, sparse attention
```

---

# 11. Advanced Technique Comparisons

## 11.1 Data Augmentation vs Synthetic Data Generation

| Aspect | Data Augmentation | Synthetic Data Generation |
|--------|-------------------|---------------------------|
| **Source** | Transform real data | Generate from scratch |
| **Fidelity** | Close to original | Variable quality |
| **Diversity** | Limited by transforms | Potentially unlimited |
| **Methods** | Geometric, color, noise | GANs, VAEs, Diffusion |
| **Privacy** | May leak original | Can preserve privacy |

### Methods Comparison
```
Data Augmentation:
├── Image: Flip, rotate, crop, color jitter
├── Text: Back-translation, synonym replacement
├── Audio: Time stretch, pitch shift, noise
├── Tabular: SMOTE (borderline synthetic)
└── Advanced: MixUp, CutMix, AutoAugment

Synthetic Data Generation:
├── GANs: Photo-realistic images
├── VAEs: Diverse samples, latent control
├── Diffusion: State-of-the-art images
├── LLMs: Synthetic text data
└── Simulation: 3D rendered images, physics
```

### When to Use
```
Data Augmentation:
├── First approach for limited data
├── Know domain-relevant invariances
├── Training time augmentation
├── Low computational cost
└── Always combine with other techniques

Synthetic Data Generation:
├── Privacy-critical applications (healthcare)
├── Rare event simulation
├── Testing edge cases
├── Unlimited training data needed
└── When real data is expensive to collect
```

---

## 11.2 Ensemble Methods vs Single Models

| Aspect | Single Model | Ensemble |
|--------|-------------|----------|
| **Complexity** | Lower | Higher |
| **Interpretability** | Better | Harder |
| **Accuracy** | Good | Better |
| **Training Cost** | Lower | Higher |
| **Inference Cost** | Lower | Higher |
| **Variance** | Higher | Lower |

### Ensemble Types
```
Homogeneous Ensembles:
├── Bagging: Random Forest (parallel trees)
├── Boosting: XGBoost (sequential trees)
└── Same algorithm, different data/weights

Heterogeneous Ensembles:
├── Stacking: Multiple models + meta-learner
├── Voting: Average predictions from different models
└── Different algorithms combined
```

### Performance Gains
```
Typical accuracy improvements:
├── Single model: Baseline
├── Bagging: +1-3% (reduces variance)
├── Boosting: +3-5% (reduces bias)
└── Stacking: +1-2% (on top of best single)

Diminishing returns:
├── 2-3 models: Most of the gain
├── 5-10 models: Marginal improvement
└── >10 models: Rarely worth it
```

### When to Use
```
Single Model Preferred:
├── Real-time inference critical
├── Model interpretability needed
├── Limited compute resources
├── Prototyping/development
└── When single model is "good enough"

Ensemble Preferred:
├── Competitions (maximize accuracy)
├── High-stakes production systems
├── Reducing prediction variance
├── Have compute budget
└── Combining diverse models
```

---

## 11.3 Model Compression: Distillation vs Pruning vs Quantization

| Technique | What It Does | Size Reduction | Speed Gain | Accuracy Loss |
|-----------|-------------|----------------|------------|---------------|
| **Distillation** | Teacher-Student | New model | Variable | Low |
| **Pruning** | Remove weights/neurons | 50-90% | 2-10x | Low-Medium |
| **Quantization** | Reduce precision | 2-4x | 2-4x | Very Low |

### How Each Works
```
Knowledge Distillation:
  Large Teacher → [Soft Labels] → Train Small Student
  
  Loss = α·CE(student, hard_labels) + (1-α)·KL(student_soft, teacher_soft)
  
  The student learns "why" not just "what"

Pruning:
  Original Network → Remove unimportant weights → Sparse Network
  
  Methods:
  ├── Magnitude pruning (smallest weights)
  ├── Structured pruning (entire filters/neurons)
  └── Lottery ticket (find winning sub-network)

Quantization:
  Float32 (4 bytes) → Int8 (1 byte) or lower
  
  Types:
  ├── Post-training: Quantize after training
  └── Quantization-aware: Train with quantization
```

### Comparison
```
                 Size ↓    Speed ↑    Accuracy
Distillation    ━━━━━━━━   ●○○○○     ●●●●●
Pruning         ━━━━━━━━   ●●●○○     ●●●○○
Quantization    ━━━━●      ●●●●●     ●●●●○

Combined:
Distillation + Pruning + Quantization = Maximum compression
```

### When to Use
```
Distillation:
├── Want smaller architecture
├── Have compute for training
├── Teacher model available
└── Mobile/edge deployment

Pruning:
├── Large pretrained model
├── Sparsity support in hardware
├── Want to keep architecture class
└── Research on efficient networks

Quantization:
├── Fastest implementation
├── Hardware supports INT8
├── Minimal accuracy loss acceptable
├── Production deployment
└── Almost always worth trying
```

---

## 11.4 Learning Paradigms: Centralized vs Federated vs Distributed

| Aspect | Centralized | Federated | Distributed |
|--------|------------|-----------|-------------|
| **Data Location** | Central server | Edge devices | Sharded across nodes |
| **Privacy** | Low (data moves) | High (data stays) | Medium |
| **Communication** | High (all data) | Medium (gradients) | High (sync needed) |
| **Compute** | Central | Edge + Central | Distributed |

### Architecture
```
Centralized Learning:
  All Data → [Central Server] → Train → Model
  
  Simple, but:
  - Privacy concerns
  - Data transfer costs
  - Single point of failure

Federated Learning:
  Device 1: Local data → Local model
  Device 2: Local data → Local model  → [Aggregate] → Global model
  Device N: Local data → Local model
  
  Data never leaves device

Distributed Learning:
  Data Shard 1 → Worker 1 ─┐
  Data Shard 2 → Worker 2 ─┼→ [Parameter Server] → Sync
  Data Shard 3 → Worker 3 ─┘
  
  Scale to massive datasets
```

### When to Use
```
Centralized:
├── Data can be collected centrally
├── Privacy not a concern
├── Standard ML/DL training
└── Most common approach

Federated:
├── Privacy-critical (healthcare, finance)
├── Data on edge devices (phones)
├── Regulatory requirements (GDPR)
├── Google Keyboard, Apple ML
└── When data can't leave devices

Distributed:
├── Dataset too large for one machine
├── Need to speed up training
├── Large model training (LLMs)
├── Data parallelism, Model parallelism
└── When have cluster resources
```

---

## 11.5 Few-shot vs Zero-shot vs One-shot Learning

| Paradigm | Training Examples | Description |
|----------|-------------------|-------------|
| **Zero-shot** | 0 | Learn without any examples |
| **One-shot** | 1 | Learn from single example |
| **Few-shot** | 2-10 | Learn from handful of examples |

### Mechanisms
```
Zero-shot Learning:
  Transfer knowledge from seen to unseen classes
  
  Example: "This is a zebra" (never seen zebra)
  Uses: Knows horse + knows stripes → infers zebra
  
  Methods: CLIP, GPT-3 prompting, attribute-based

One-shot Learning:
  Learn from exactly one example per class
  
  Example: Given one face photo, recognize that person
  
  Methods: Siamese networks, Matching networks

Few-shot Learning:
  Learn from K examples (K typically 1-10)
  
  Example: 5-shot 5-way classification
  5 classes, 5 examples each → classify new sample
  
  Methods: Prototypical networks, MAML, Matching networks
```

### Method Comparison
```
                      Zero    One    Few
Data needed:           0       1     2-10
Accuracy:            Lower   Medium  Higher
Generalization:      Best   Medium  Lower (to new tasks)
Difficulty:         Hardest  Hard   Easier
```

### When to Use
```
Zero-shot:
├── No labeled data for target task
├── Large pretrained model available
├── Target classes describable in text
├── CLIP, GPT-style models
└── Rapid prototyping

One-shot:
├── Exactly one example per class
├── Face verification (is this the same person?)
├── Signature verification
└── When more examples impossible

Few-shot:
├── Very limited labeled data (2-10)
├── Many tasks with few examples each
├── Meta-learning scenarios
├── Personalization
└── Low-resource languages/domains
```

---

# 12. Deployment and Production Comparisons

## 12.1 Batch Inference vs Real-time Inference

| Aspect | Batch Inference | Real-time Inference |
|--------|-----------------|---------------------|
| **Latency** | Minutes-hours | Milliseconds |
| **Throughput** | High (bulk) | Per-request |
| **Scheduling** | Periodic | On-demand |
| **Resource Usage** | Burst | Steady |
| **Error Handling** | Retry bulk | Graceful fallback |

### Architecture
```
Batch Inference:
  [Data Lake] → [Batch Job] → [Model] → [Output Store]
               (scheduled, e.g., nightly)
               
  Examples:
  - Recommendation scores for all users
  - Credit scoring for portfolio
  - Report generation

Real-time Inference:
  [Request] → [API Gateway] → [Model Server] → [Response]
              (synchronous, <100ms)
              
  Examples:
  - Search ranking
  - Fraud detection
  - Chatbots
```

### When to Use
```
Batch Inference:
├── Results can be precomputed
├── Latency not critical
├── Large-scale scoring needed
├── Cost optimization (spot instances)
└── Periodic predictions (daily, weekly)

Real-time Inference:
├── User-facing applications
├── Time-sensitive decisions
├── Interactive features
├── Personalization
└── Fraud/anomaly detection
```

---

## 12.2 Model Serving: Flask vs FastAPI vs TensorFlow Serving

| Aspect | Flask | FastAPI | TF Serving |
|--------|-------|---------|------------|
| **Type** | Web framework | Web framework | ML-specific |
| **Performance** | Low-Medium | High | Very High |
| **Async** | Limited | Native | Native |
| **ML Features** | None | None | Built-in |
| **Complexity** | Simple | Medium | Medium-High |

### Use Cases
```
Flask:
├── Prototyping
├── Simple endpoints
├── Internal tools
├── When team knows Flask
└── Quick deployment

FastAPI:
├── Production APIs
├── Need async/performance
├── API documentation
├── Type validation
└── Modern Python deployment

TensorFlow Serving:
├── High-throughput TF models
├── Model versioning needed
├── Batching optimization
├── GPU inference
└── Enterprise TF deployments
```

### Code Comparison
```python
# Flask
from flask import Flask, request
app = Flask(__name__)
@app.route('/predict', methods=['POST'])
def predict():
    data = request.json
    result = model.predict(data['input'])
    return {'prediction': result}

# FastAPI
from fastapi import FastAPI
app = FastAPI()
@app.post('/predict')
async def predict(data: InputSchema):
    result = await model.predict_async(data.input)
    return {'prediction': result}

# TensorFlow Serving (gRPC)
# Deploy model to TF Serving, then:
stub = prediction_service_pb2_grpc.PredictionServiceStub(channel)
request = predict_pb2.PredictRequest()
request.model_spec.name = 'my_model'
response = stub.Predict(request)
```

### Decision Guide
```
Prototyping / Small scale:
└── Flask

Production API (< 1000 QPS):
└── FastAPI

High-throughput TensorFlow:
└── TensorFlow Serving

PyTorch / General:
├── TorchServe
└── Triton Inference Server

Kubernetes deployment:
├── Seldon Core
└── KServe
```

---

## 12.3 Cloud Platforms: AWS SageMaker vs Azure ML vs Google Vertex AI

| Aspect | AWS SageMaker | Azure ML | Vertex AI |
|--------|--------------|----------|-----------|
| **Ecosystem** | AWS | Microsoft | Google Cloud |
| **AutoML** | Autopilot | AutoML | AutoML |
| **Notebooks** | Studio | Azure Notebooks | Workbench |
| **MLOps** | Pipelines | Pipelines | Pipelines |
| **Strength** | Maturity | Enterprise | AI/Research |

### Feature Comparison
```
AWS SageMaker:
├── Mature, feature-rich
├── Tight S3/EC2 integration
├── Built-in algorithms
├── Ground Truth (labeling)
├── Feature Store
└── Good for: Enterprise AWS shops

Azure ML:
├── Office 365 integration
├── Azure DevOps integration
├── Responsible AI dashboard
├── Designer (visual ML)
├── Enterprise security
└── Good for: Microsoft shops

Vertex AI:
├── TPU access
├── TensorFlow ecosystem
├── BigQuery integration
├── Matching Engine (similarity)
├── Model Garden (pretrained)
└── Good for: Research, Google-first
```

### When to Use
```
AWS SageMaker:
├── Already on AWS
├── Need mature MLOps
├── Enterprise features
├── Wide framework support
└── Large ecosystem of integrations

Azure ML:
├── Already on Azure
├── Microsoft stack
├── Enterprise compliance critical
├── .NET / C# teams
└── Power BI integration

Vertex AI:
├── Already on GCP
├── TensorFlow preference
├── Need TPUs
├── BigQuery-centric workflows
├── Research/cutting-edge focus
└── Gemini/PaLM access
```

---

## 12.4 Hardware: CPU vs GPU vs TPU

| Aspect | CPU | GPU | TPU |
|--------|-----|-----|-----|
| **Architecture** | General purpose | Parallel cores | Matrix-optimized |
| **Parallelism** | 8-64 cores | 1000s of cores | Systolic array |
| **Training Speed** | Baseline | 10-100x | 100-200x |
| **Cost** | Lowest | Medium-High | High |
| **Availability** | Everywhere | Common | Google Cloud |

### Performance Characteristics
```
CPU:
├── Sequential operations
├── Complex logic
├── Small batch inference
├── Data preprocessing
└── Not for training large models

GPU (NVIDIA):
├── Parallel matrix operations
├── Training and inference
├── Widely available
├── CUDA ecosystem
└── Standard for deep learning

TPU:
├── Google-designed for ML
├── Optimized for TensorFlow/JAX
├── Massive batch sizes
├── High bandwidth memory
└── Best for large-scale training
```

### Cost-Performance Trade-offs
```
Training Time (example: BERT-base):
├── CPU (16 cores): ~2 weeks
├── GPU (V100): ~4 days
├── 8x GPUs: ~12 hours
├── TPU v3-8: ~1.5 hours
└── TPU pod: minutes

Cost Efficiency (rough):
├── Small models: CPU often fine
├── Medium models: GPU best $/perf
└── Large models: TPU most efficient
```

### When to Use
```
CPU:
├── Inference for small models
├── Batch processing
├── Preprocessing pipelines
├── Development/debugging
└── When GPU unavailable

GPU:
├── Training most deep learning
├── Real-time inference
├── Computer vision, NLP
├── Flexible deployment
└── Default for DL

TPU:
├── Large-scale training
├── TensorFlow/JAX models
├── Research (TPU Research Cloud)
├── Massive batch sizes beneficial
└── When max speed critical
```

---

# Quick Reference Cheatsheet

## Algorithm Selection Flowchart
```
Start: What's your problem?
│
├─ Supervised?
│  ├─ Target continuous? → Regression
│  │  ├─ Linear relationship? → Linear Regression
│  │  ├─ Complex/trees? → XGBoost, Random Forest
│  │  └─ Very complex? → Neural Network
│  │
│  └─ Target categorical? → Classification
│     ├─ Binary? → Logistic Regression, XGBoost, SVM
│     ├─ Multi-class? → Random Forest, XGBoost, NN
│     └─ Need probabilities? → Calibrated classifiers
│
├─ Unsupervised?
│  ├─ Find groups? → Clustering
│  │  ├─ Know K? → K-Means
│  │  ├─ Arbitrary shapes? → DBSCAN
│  │  └─ Hierarchical? → Agglomerative
│  │
│  └─ Reduce dimensions? → PCA, t-SNE, UMAP
│
└─ Reinforcement?
   └─ Sequential decisions → RL (DQN, PPO, A3C)
```

## Metric Selection Matrix
```
Classification:
├─ Balanced? → Accuracy, F1-macro
├─ Imbalanced? → PR-AUC, F1-weighted, MCC
├─ Cost-sensitive? → Custom threshold + Precision/Recall
└─ Ranking? → ROC-AUC

Regression:
├─ Outliers matter? → MSE, RMSE
├─ Robust needed? → MAE, Huber
├─ Relative error? → MAPE
└─ R² for explained variance
```

## Deep Learning Architecture Guide
```
Data Type:
├─ Tabular → MLP, XGBoost (often better)
├─ Images → CNN (ResNet, EfficientNet)
├─ Sequences → Transformer, LSTM
├─ Text → Transformer (BERT, GPT)
├─ Audio → CNN on spectrograms, Wav2Vec
└─ Graphs → GNN (GCN, GAT)

Task:
├─ Classification → Softmax output
├─ Detection → YOLO, Faster R-CNN
├─ Segmentation → U-Net, Mask R-CNN
├─ Generation → GAN, VAE, Diffusion
└─ Translation → Encoder-Decoder
```

---

*End of ML/DL Comparative Notes*

---
