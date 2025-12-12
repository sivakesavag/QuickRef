# Machine Learning Curriculum - Topics Overview

> **Total Assignments**: 620 | **Levels**: 4 | **Duration**: Beginner to Expert

## Quick Navigation

| Level | File | Assignments | Focus |
|-------|------|-------------|-------|
| Beginner | [ml_assign_beginner.md](ml_assign_beginner.md) | 155 | Foundations & Core Algorithms |
| Intermediate | [ml_assign_intermediate.md](ml_assign_intermediate.md) | 155 | Classical ML & Unsupervised Learning |
| Advanced | [ml_assign_advanced.md](ml_assign_advanced.md) | 155 | Deep Learning, NLP, Time Series |
| Expert | [ml_assign_expert.md](ml_assign_expert.md) | 155 | Transformers, LLMs, MLOps, RL |

---

## Beginner Level Topics (155 Assignments)

### Section A: Mathematical Foundations (30)
- Linear algebra: vectors, matrices, operations, eigenvalues
- Calculus: derivatives, gradients, partial derivatives
- Probability: distributions, Bayes theorem, expectations
- Statistics: mean, variance, correlation, hypothesis testing
- Numerical computing with NumPy

### Section B: Data Preprocessing & Feature Engineering (30)
- Data loading, exploration, and cleaning
- Missing value handling strategies
- Outlier detection and treatment
- Feature scaling: normalization, standardization
- Encoding categorical variables (one-hot, label, ordinal)
- Feature creation and transformation

### Section C: Linear Regression (25)
- Simple and multiple linear regression
- Gradient descent from scratch
- Closed-form solution (normal equation)
- Polynomial regression
- Regularization: Ridge, Lasso, ElasticNet
- Model assumptions and diagnostics

### Section D: Logistic Regression & Classification (25)
- Binary and multiclass classification
- Sigmoid function and log loss
- Decision boundaries
- Regularized logistic regression
- Class imbalance handling

### Section E: k-Nearest Neighbors (20)
- Distance metrics (Euclidean, Manhattan, Minkowski)
- KNN classification and regression
- Choosing optimal k
- Weighted KNN
- Curse of dimensionality

### Section F: Evaluation Metrics & Validation (25)
- Train/test/validation splits
- Cross-validation (k-fold, stratified, leave-one-out)
- Classification: accuracy, precision, recall, F1, AUC-ROC
- Regression: MSE, RMSE, MAE, R²
- Confusion matrix analysis
- Bias-variance tradeoff

---

## Intermediate Level Topics (155 Assignments)

### Section A: Decision Trees & Tree-Based Methods (25)
- Decision tree algorithms (CART, ID3, C4.5)
- Splitting criteria (Gini, entropy, information gain)
- Pruning strategies
- Feature importance
- Tree visualization

### Section B: Support Vector Machines (22)
- Linear SVM and maximum margin
- Soft margin and C parameter
- Kernel trick (RBF, polynomial)
- SVM for regression (SVR)
- Multi-class SVM strategies

### Section C: Naive Bayes & Probabilistic Models (22)
- Bayes theorem application
- Gaussian, Multinomial, Bernoulli Naive Bayes
- Text classification with Naive Bayes
- Laplace smoothing
- Probabilistic predictions

### Section D: Ensemble Methods (25)
- Bagging and bootstrap aggregation
- Random Forests
- Boosting (AdaBoost, Gradient Boosting)
- XGBoost, LightGBM, CatBoost
- Stacking and blending
- Voting classifiers

### Section E: Clustering Algorithms (28)
- K-Means and K-Means++
- Hierarchical clustering (agglomerative, divisive)
- DBSCAN and density-based methods
- Gaussian Mixture Models (GMM)
- Cluster evaluation (silhouette, Davies-Bouldin)
- Clustering for customer segmentation

### Section F: Dimensionality Reduction (20)
- Principal Component Analysis (PCA)
- Explained variance and component selection
- t-SNE for visualization
- UMAP
- Feature selection methods
- Truncated SVD for sparse data

### Section G: Model Optimization & Hyperparameter Tuning (13)
- Grid search and random search
- Bayesian optimization (Optuna, Hyperopt)
- Cross-validation strategies for tuning
- Early stopping
- Learning curves

---

## Advanced Level Topics (155 Assignments)

### Section A: Advanced Feature Engineering (25)
- Target encoding with smoothing
- Feature hashing
- Entity embeddings
- Weight of Evidence (WoE)
- Geographical and temporal features
- Automated feature generation

### Section B: Natural Language Processing (28)
- Text preprocessing and tokenization
- Bag-of-Words and TF-IDF
- Word embeddings (Word2Vec, GloVe)
- Sentiment analysis
- Named Entity Recognition (NER)
- Topic modeling (LDA)
- Text classification and sequence labeling
- BERT and transformer-based NLP

### Section C: Time Series Analysis (25)
- Time series decomposition
- Stationarity testing (ADF, KPSS)
- ARIMA and SARIMA models
- Prophet forecasting
- Feature engineering for time series
- LSTM for sequences
- Anomaly detection in time series

### Section D: Deep Learning Fundamentals (30)
- Perceptron and MLP from scratch
- Activation functions
- Backpropagation
- Optimizers (SGD, Adam, RMSprop)
- Regularization (dropout, batch norm)
- CNNs and image classification
- RNNs, LSTM, GRU
- Transfer learning
- PyTorch and TensorFlow basics

### Section E: Model Interpretability & Explainability (22)
- Feature importance methods
- SHAP values
- LIME explanations
- Partial dependence plots (PDP)
- Counterfactual explanations
- Fairness and bias detection
- Model documentation

### Section F: Anomaly Detection (25)
- Statistical methods (z-score, IQR)
- Isolation Forest
- Local Outlier Factor (LOF)
- One-Class SVM
- Autoencoder-based detection
- Time series anomalies
- Fraud detection systems

---

## Expert Level Topics (155 Assignments)

### Section A: Transformers & Attention Mechanisms (25)
- Self-attention from scratch
- Multi-head attention
- Positional encoding (sinusoidal, RoPE)
- Transformer encoder and decoder
- BERT architecture
- GPT architecture
- Vision Transformers (ViT)
- Efficient attention (Flash Attention)
- Model compression (distillation, quantization, pruning)
- Parameter-efficient fine-tuning (LoRA, adapters)

### Section B: Large Language Models & Applications (28)
- LLM API usage and prompt engineering
- Chain-of-thought reasoning
- Retrieval Augmented Generation (RAG)
- Vector databases (FAISS, Chroma, Pinecone)
- LLM fine-tuning and instruction tuning
- RLHF and DPO concepts
- LLM agents and tool use
- Multi-agent systems
- Guardrails and safety
- Local LLM deployment

### Section C: MLOps & Production Systems (30)
- ML pipeline design
- Feature stores (Feast)
- Experiment tracking (MLflow, W&B)
- Model registry and versioning
- Containerization (Docker)
- Kubernetes for ML
- CI/CD for ML
- Model monitoring and drift detection
- A/B testing for models
- Distributed training
- Edge deployment

### Section D: Reinforcement Learning (25)
- MDP and Bellman equations
- Q-Learning and SARSA
- Deep Q-Networks (DQN)
- Policy gradients (REINFORCE)
- Actor-Critic methods (A2C, PPO, SAC)
- Multi-armed bandits
- Imitation learning
- Multi-agent RL
- Safe RL

### Section E: Advanced Research Techniques (22)
- Reading and reproducing research papers
- Ablation studies
- Neural Architecture Search (NAS)
- Meta-learning (MAML)
- Continual learning
- Self-supervised learning
- Diffusion models
- Graph Neural Networks
- Causal inference
- Federated learning

### Section F: Capstone Projects & System Design (25)
- End-to-end ML systems
- Recommendation engines
- Search and retrieval systems
- Fraud detection pipelines
- Computer vision pipelines
- NLP processing systems
- Real-time ML systems
- AutoML platforms
- System design interview preparation

---

## Learning Path Recommendation

```
Beginner (4-6 weeks)
    ↓
Intermediate (4-6 weeks)
    ↓
Advanced (6-8 weeks)
    ↓
Expert (8-12 weeks)
```

**Total Estimated Time**: 22-32 weeks for complete mastery

---

## Supporting Resources

- **Cheatsheet**: [ml_cheatsheet.md](ml_cheatsheet.md) - Comprehensive reference for solving assignments
