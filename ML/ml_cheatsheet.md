# Machine Learning Cheatsheet

> **Purpose**: Comprehensive reference to help learners solve 620+ ML assignments from Beginner to Expert level.

---

## Table of Contents

1. [Mathematical Foundations](#1-mathematical-foundations)
2. [Data Preprocessing](#2-data-preprocessing)
3. [Supervised Learning](#3-supervised-learning)
4. [Unsupervised Learning](#4-unsupervised-learning)
5. [Ensemble Methods](#5-ensemble-methods)
6. [Model Evaluation](#6-model-evaluation)
7. [Deep Learning](#7-deep-learning)
8. [Natural Language Processing](#8-natural-language-processing)
9. [Time Series](#9-time-series)
10. [Model Interpretability](#10-model-interpretability)
11. [Transformers & LLMs](#11-transformers--llms)
12. [MLOps](#12-mlops)
13. [Reinforcement Learning](#13-reinforcement-learning)
14. [Code Templates](#14-code-templates)

---

## 1. Mathematical Foundations

### Linear Algebra

```python
import numpy as np

# Vector operations
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
dot_product = np.dot(a, b)        # 32
cross_product = np.cross(a, b)    # [-3, 6, -3]
magnitude = np.linalg.norm(a)     # 3.74

# Matrix operations
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
product = A @ B                    # Matrix multiplication
inverse = np.linalg.inv(A)         # Inverse
determinant = np.linalg.det(A)     # -2.0
eigenvalues, eigenvectors = np.linalg.eig(A)
```

**Key Concepts**:
- **Dot product**: `a·b = Σ aᵢbᵢ = |a||b|cos(θ)`
- **Matrix multiplication**: `(AB)ᵢⱼ = Σₖ AᵢₖBₖⱼ`
- **Eigendecomposition**: `Av = λv` (v = eigenvector, λ = eigenvalue)
- **SVD**: `A = UΣVᵀ` (used in PCA, recommendations)

### Calculus & Optimization

```python
# Gradient descent update
theta = theta - learning_rate * gradient

# Chain rule for backpropagation
# ∂L/∂w = ∂L/∂y × ∂y/∂z × ∂z/∂w
```

**Key Formulas**:
- **Gradient**: `∇f = [∂f/∂x₁, ∂f/∂x₂, ..., ∂f/∂xₙ]`
- **Gradient descent**: `θₜ₊₁ = θₜ - η∇J(θₜ)`
- **Learning rate**: Too high → diverge, too low → slow convergence

### Probability & Statistics

```python
import scipy.stats as stats

# Distributions
normal = stats.norm(loc=0, scale=1)
sample = normal.rvs(size=1000)
pdf_value = normal.pdf(0)          # 0.3989
cdf_value = normal.cdf(1.96)       # 0.975

# Statistical tests
t_stat, p_value = stats.ttest_ind(group1, group2)
```

**Key Concepts**:
| Distribution | Use Case | Parameters |
|-------------|----------|------------|
| Normal | Continuous, symmetric | μ (mean), σ (std) |
| Bernoulli | Binary outcome | p (probability) |
| Binomial | Count of successes | n, p |
| Poisson | Count of events | λ (rate) |
| Exponential | Time between events | λ |

**Bayes Theorem**: `P(A|B) = P(B|A)P(A) / P(B)`

---

## 2. Data Preprocessing

### Loading & Exploration

```python
import pandas as pd

# Load data
df = pd.read_csv('data.csv')

# Quick exploration
df.head()                    # First 5 rows
df.info()                    # Data types, non-null counts
df.describe()                # Statistics for numeric columns
df.isnull().sum()            # Missing values per column
df.duplicated().sum()        # Duplicate rows
df['col'].value_counts()     # Frequency counts
```

### Missing Value Handling

```python
# Detection
df.isnull().sum()
df.isnull().mean() * 100     # Percentage missing

# Simple imputation
df['col'].fillna(df['col'].mean(), inplace=True)      # Mean
df['col'].fillna(df['col'].median(), inplace=True)    # Median (robust)
df['col'].fillna(df['col'].mode()[0], inplace=True)   # Mode (categorical)
df.fillna(method='ffill', inplace=True)               # Forward fill

# Advanced imputation
from sklearn.impute import SimpleImputer, KNNImputer
imputer = KNNImputer(n_neighbors=5)
df_imputed = imputer.fit_transform(df)
```

**Strategy Selection**:
| Data Type | Strategy |
|-----------|----------|
| Numerical (symmetric) | Mean |
| Numerical (skewed) | Median |
| Categorical | Mode or separate category |
| Time series | Forward fill / interpolation |
| High missing % (>50%) | Consider dropping |

### Feature Scaling

```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler, RobustScaler

# Standardization (z-score): (x - μ) / σ → mean=0, std=1
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# Normalization (Min-Max): (x - min) / (max - min) → [0, 1]
scaler = MinMaxScaler()
X_normalized = scaler.fit_transform(X)

# Robust scaling (outlier-resistant): (x - median) / IQR
scaler = RobustScaler()
X_robust = scaler.fit_transform(X)
```

**When to use**:
- **StandardScaler**: Linear models, neural networks, PCA
- **MinMaxScaler**: When you need bounded values [0,1]
- **RobustScaler**: Data with outliers
- **No scaling needed**: Tree-based models (RF, XGBoost)

### Encoding Categorical Variables

```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
import pandas as pd

# Label Encoding (ordinal categories)
le = LabelEncoder()
df['encoded'] = le.fit_transform(df['category'])

# One-Hot Encoding (nominal categories)
df_encoded = pd.get_dummies(df, columns=['category'])

# Or with sklearn
ohe = OneHotEncoder(sparse=False, handle_unknown='ignore')
encoded = ohe.fit_transform(df[['category']])

# Target Encoding (for high cardinality)
means = df.groupby('category')['target'].mean()
df['target_encoded'] = df['category'].map(means)
```

**Encoding Selection**:
| Cardinality | Encoding Type |
|-------------|---------------|
| 2 categories | Label or binary |
| 3-10 categories | One-hot |
| 10-100 categories | Target encoding |
| 100+ categories | Feature hashing, embeddings |

### Outlier Detection

```python
import numpy as np

# Z-score method
z_scores = np.abs((df['col'] - df['col'].mean()) / df['col'].std())
outliers = df[z_scores > 3]

# IQR method
Q1, Q3 = df['col'].quantile([0.25, 0.75])
IQR = Q3 - Q1
lower, upper = Q1 - 1.5*IQR, Q3 + 1.5*IQR
outliers = df[(df['col'] < lower) | (df['col'] > upper)]

# Isolation Forest
from sklearn.ensemble import IsolationForest
iso = IsolationForest(contamination=0.1)
outliers = iso.fit_predict(X)  # -1 = outlier
```

---

## 3. Supervised Learning

### Linear Regression

```python
from sklearn.linear_model import LinearRegression, Ridge, Lasso, ElasticNet

# Basic linear regression
model = LinearRegression()
model.fit(X_train, y_train)
predictions = model.predict(X_test)

# With regularization
ridge = Ridge(alpha=1.0)        # L2: minimize ||w||²
lasso = Lasso(alpha=1.0)        # L1: minimize |w|
elastic = ElasticNet(alpha=1.0, l1_ratio=0.5)  # L1 + L2
```

**Key Formulas**:
- **Prediction**: `ŷ = Xw + b`
- **MSE Loss**: `J(w) = (1/n) Σ(yᵢ - ŷᵢ)²`
- **Normal equation**: `w = (XᵀX)⁻¹Xᵀy`
- **Ridge**: `J(w) = MSE + α||w||²`
- **Lasso**: `J(w) = MSE + α|w|` (feature selection)

### Logistic Regression

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(
    C=1.0,                    # Inverse regularization strength
    penalty='l2',             # 'l1', 'l2', 'elasticnet', 'none'
    solver='lbfgs',           # 'liblinear' for small datasets
    max_iter=1000,
    class_weight='balanced'   # Handle imbalanced classes
)
model.fit(X_train, y_train)
proba = model.predict_proba(X_test)[:, 1]  # Probability of class 1
```

**Key Formulas**:
- **Sigmoid**: `σ(z) = 1 / (1 + e⁻ᶻ)`
- **Prediction**: `P(y=1|x) = σ(wᵀx + b)`
- **Log Loss**: `J = -1/n Σ[y log(ŷ) + (1-y)log(1-ŷ)]`

### K-Nearest Neighbors

```python
from sklearn.neighbors import KNeighborsClassifier, KNeighborsRegressor

model = KNeighborsClassifier(
    n_neighbors=5,            # Typically odd number
    weights='distance',       # 'uniform' or 'distance'
    metric='euclidean'        # 'manhattan', 'minkowski'
)
model.fit(X_train, y_train)
```

**Distance Metrics**:
- **Euclidean**: `√(Σ(xᵢ - yᵢ)²)` - default, sensitive to scale
- **Manhattan**: `Σ|xᵢ - yᵢ|` - robust to outliers
- **Minkowski**: `(Σ|xᵢ - yᵢ|ᵖ)^(1/p)` - generalization

**Choosing k**: Use cross-validation, typically √n, odd to avoid ties

### Decision Trees

```python
from sklearn.tree import DecisionTreeClassifier, DecisionTreeRegressor, plot_tree

model = DecisionTreeClassifier(
    criterion='gini',         # 'entropy' for information gain
    max_depth=5,              # Prevent overfitting
    min_samples_split=10,     # Min samples to split
    min_samples_leaf=5,       # Min samples in leaf
    class_weight='balanced'
)
model.fit(X_train, y_train)

# Feature importance
importances = model.feature_importances_

# Visualization
import matplotlib.pyplot as plt
plt.figure(figsize=(20, 10))
plot_tree(model, feature_names=feature_names, filled=True)
```

**Splitting Criteria**:
- **Gini Impurity**: `1 - Σpᵢ²` (probability of misclassification)
- **Entropy**: `-Σpᵢ log₂(pᵢ)` (information content)
- **Information Gain**: `Entropy(parent) - Σ(weighted entropy of children)`

### Support Vector Machines

```python
from sklearn.svm import SVC, SVR

model = SVC(
    C=1.0,                    # Regularization (smaller = more regularization)
    kernel='rbf',             # 'linear', 'poly', 'rbf', 'sigmoid'
    gamma='scale',            # Kernel coefficient
    probability=True          # Enable probability estimates
)
model.fit(X_train, y_train)
```

**Kernels**:
- **Linear**: `K(x, y) = xᵀy` - linearly separable data
- **Polynomial**: `K(x, y) = (γxᵀy + r)^d` - polynomial decision boundary
- **RBF**: `K(x, y) = exp(-γ||x-y||²)` - most common, flexible

### Naive Bayes

```python
from sklearn.naive_bayes import GaussianNB, MultinomialNB, BernoulliNB

# For continuous features (Gaussian distribution)
gnb = GaussianNB()

# For discrete counts (text classification)
mnb = MultinomialNB(alpha=1.0)  # alpha = Laplace smoothing

# For binary features
bnb = BernoulliNB()
```

**Formula**: `P(y|X) = P(X|y)P(y) / P(X)` with independence assumption

---

## 4. Unsupervised Learning

### K-Means Clustering

```python
from sklearn.cluster import KMeans

model = KMeans(
    n_clusters=3,
    init='k-means++',         # Better initialization
    n_init=10,                # Number of runs
    max_iter=300,
    random_state=42
)
clusters = model.fit_predict(X)
centroids = model.cluster_centers_
inertia = model.inertia_      # Sum of squared distances

# Elbow method for choosing k
inertias = []
for k in range(1, 11):
    km = KMeans(n_clusters=k, random_state=42)
    km.fit(X)
    inertias.append(km.inertia_)
```

### Hierarchical Clustering

```python
from sklearn.cluster import AgglomerativeClustering
from scipy.cluster.hierarchy import dendrogram, linkage

# Sklearn
model = AgglomerativeClustering(
    n_clusters=3,
    linkage='ward'            # 'single', 'complete', 'average', 'ward'
)
clusters = model.fit_predict(X)

# Scipy for dendrogram
Z = linkage(X, method='ward')
dendrogram(Z)
```

**Linkage Methods**:
- **Single**: Min distance (chaining problem)
- **Complete**: Max distance (compact clusters)
- **Average**: Mean distance
- **Ward**: Minimize variance increase

### DBSCAN

```python
from sklearn.cluster import DBSCAN

model = DBSCAN(
    eps=0.5,                  # Maximum distance between points
    min_samples=5,            # Minimum points to form cluster
    metric='euclidean'
)
clusters = model.fit_predict(X)
# -1 indicates noise points
```

**When to use**: Unknown number of clusters, non-spherical clusters, outliers

### PCA (Dimensionality Reduction)

```python
from sklearn.decomposition import PCA

# Reduce to n components
pca = PCA(n_components=2)
X_reduced = pca.fit_transform(X)

# Explained variance
explained_variance = pca.explained_variance_ratio_
cumulative = np.cumsum(explained_variance)

# Choose components for 95% variance
pca = PCA(n_components=0.95)
X_reduced = pca.fit_transform(X)
```

### t-SNE & UMAP (Visualization)

```python
from sklearn.manifold import TSNE
import umap

# t-SNE (slow, for visualization only)
tsne = TSNE(n_components=2, perplexity=30, random_state=42)
X_tsne = tsne.fit_transform(X)

# UMAP (faster, preserves global structure)
reducer = umap.UMAP(n_components=2, n_neighbors=15)
X_umap = reducer.fit_transform(X)
```

---

## 5. Ensemble Methods

### Random Forest

```python
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor

model = RandomForestClassifier(
    n_estimators=100,         # Number of trees
    max_depth=10,             # Tree depth
    min_samples_split=5,
    min_samples_leaf=2,
    max_features='sqrt',      # Features per split
    bootstrap=True,           # Sample with replacement
    n_jobs=-1,                # Parallel processing
    random_state=42
)
model.fit(X_train, y_train)

# Feature importance
importances = pd.DataFrame({
    'feature': feature_names,
    'importance': model.feature_importances_
}).sort_values('importance', ascending=False)
```

### Gradient Boosting (XGBoost, LightGBM)

```python
import xgboost as xgb
import lightgbm as lgb

# XGBoost
xgb_model = xgb.XGBClassifier(
    n_estimators=100,
    max_depth=6,
    learning_rate=0.1,
    subsample=0.8,            # Row sampling
    colsample_bytree=0.8,     # Column sampling
    reg_alpha=0,              # L1 regularization
    reg_lambda=1,             # L2 regularization
    use_label_encoder=False,
    eval_metric='logloss'
)

# LightGBM (faster, handles categorical)
lgb_model = lgb.LGBMClassifier(
    n_estimators=100,
    max_depth=-1,             # No limit
    learning_rate=0.1,
    num_leaves=31,
    subsample=0.8,
    colsample_bytree=0.8
)
```

### Stacking

```python
from sklearn.ensemble import StackingClassifier
from sklearn.linear_model import LogisticRegression

estimators = [
    ('rf', RandomForestClassifier(n_estimators=100)),
    ('xgb', xgb.XGBClassifier(n_estimators=100)),
    ('lgb', lgb.LGBMClassifier(n_estimators=100))
]

stacking = StackingClassifier(
    estimators=estimators,
    final_estimator=LogisticRegression(),
    cv=5
)
stacking.fit(X_train, y_train)
```

---

## 6. Model Evaluation

### Classification Metrics

```python
from sklearn.metrics import (
    accuracy_score, precision_score, recall_score, f1_score,
    roc_auc_score, confusion_matrix, classification_report,
    precision_recall_curve, roc_curve
)

# Basic metrics
accuracy = accuracy_score(y_true, y_pred)
precision = precision_score(y_true, y_pred, average='binary')
recall = recall_score(y_true, y_pred, average='binary')
f1 = f1_score(y_true, y_pred, average='binary')
auc = roc_auc_score(y_true, y_proba)

# Confusion matrix
cm = confusion_matrix(y_true, y_pred)
# [[TN, FP],
#  [FN, TP]]

# Full report
print(classification_report(y_true, y_pred))
```

**Metric Formulas**:
| Metric | Formula | Use Case |
|--------|---------|----------|
| Accuracy | (TP+TN)/(TP+TN+FP+FN) | Balanced classes |
| Precision | TP/(TP+FP) | Minimize false positives |
| Recall | TP/(TP+FN) | Minimize false negatives |
| F1 | 2×(P×R)/(P+R) | Balance precision/recall |
| AUC-ROC | Area under ROC curve | Ranking ability |

### Regression Metrics

```python
from sklearn.metrics import (
    mean_squared_error, mean_absolute_error, r2_score,
    mean_absolute_percentage_error
)

mse = mean_squared_error(y_true, y_pred)
rmse = mean_squared_error(y_true, y_pred, squared=False)
mae = mean_absolute_error(y_true, y_pred)
mape = mean_absolute_percentage_error(y_true, y_pred)
r2 = r2_score(y_true, y_pred)
```

### Cross-Validation

```python
from sklearn.model_selection import (
    cross_val_score, KFold, StratifiedKFold, TimeSeriesSplit,
    GridSearchCV, RandomizedSearchCV
)

# Basic cross-validation
scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')

# Stratified K-Fold (for classification)
skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
for train_idx, val_idx in skf.split(X, y):
    X_train, X_val = X[train_idx], X[val_idx]
    y_train, y_val = y[train_idx], y[val_idx]

# Grid Search
param_grid = {'n_estimators': [100, 200], 'max_depth': [5, 10]}
grid_search = GridSearchCV(model, param_grid, cv=5, scoring='accuracy')
grid_search.fit(X, y)
best_params = grid_search.best_params_
```

---

## 7. Deep Learning

### Neural Network Architecture

```python
import torch
import torch.nn as nn

class MLP(nn.Module):
    def __init__(self, input_size, hidden_size, output_size):
        super().__init__()
        self.layers = nn.Sequential(
            nn.Linear(input_size, hidden_size),
            nn.ReLU(),
            nn.Dropout(0.2),
            nn.Linear(hidden_size, hidden_size),
            nn.ReLU(),
            nn.Dropout(0.2),
            nn.Linear(hidden_size, output_size)
        )
    
    def forward(self, x):
        return self.layers(x)
```

### Training Loop

```python
# Setup
model = MLP(input_size, hidden_size, num_classes)
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)

# Training loop
for epoch in range(num_epochs):
    model.train()
    for batch_x, batch_y in train_loader:
        # Forward pass
        outputs = model(batch_x)
        loss = criterion(outputs, batch_y)
        
        # Backward pass
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
    
    # Validation
    model.eval()
    with torch.no_grad():
        val_outputs = model(X_val)
        val_loss = criterion(val_outputs, y_val)
```

### Common Layers

| Layer | Purpose | PyTorch |
|-------|---------|---------|
| Linear | Fully connected | `nn.Linear(in, out)` |
| Conv2d | 2D convolution | `nn.Conv2d(in_ch, out_ch, kernel)` |
| MaxPool2d | Downsampling | `nn.MaxPool2d(kernel)` |
| BatchNorm | Normalize activations | `nn.BatchNorm1d(features)` |
| Dropout | Regularization | `nn.Dropout(p)` |
| LSTM | Sequence modeling | `nn.LSTM(input, hidden)` |

### Activation Functions

| Function | Formula | Use Case |
|----------|---------|----------|
| ReLU | max(0, x) | Default for hidden layers |
| Leaky ReLU | max(0.01x, x) | Prevent dying neurons |
| Sigmoid | 1/(1+e⁻ˣ) | Binary output, gates |
| Tanh | (eˣ-e⁻ˣ)/(eˣ+e⁻ˣ) | RNN hidden states |
| Softmax | eˣⁱ/Σeˣʲ | Multi-class output |
| GELU | x×Φ(x) | Transformers |

### CNN for Images

```python
class CNN(nn.Module):
    def __init__(self, num_classes):
        super().__init__()
        self.features = nn.Sequential(
            nn.Conv2d(3, 32, 3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2),
            nn.Conv2d(32, 64, 3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2),
        )
        self.classifier = nn.Sequential(
            nn.Flatten(),
            nn.Linear(64 * 8 * 8, 256),
            nn.ReLU(),
            nn.Dropout(0.5),
            nn.Linear(256, num_classes)
        )
    
    def forward(self, x):
        x = self.features(x)
        x = self.classifier(x)
        return x
```

### Transfer Learning

```python
import torchvision.models as models

# Load pre-trained model
model = models.resnet50(pretrained=True)

# Freeze base layers
for param in model.parameters():
    param.requires_grad = False

# Replace classifier
model.fc = nn.Linear(model.fc.in_features, num_classes)

# Fine-tune with lower learning rate
optimizer = torch.optim.Adam(model.fc.parameters(), lr=0.001)
```

---

## 8. Natural Language Processing

### Text Preprocessing

```python
import re
import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer

def preprocess_text(text):
    # Lowercase
    text = text.lower()
    # Remove special characters
    text = re.sub(r'[^a-zA-Z\s]', '', text)
    # Tokenize
    tokens = word_tokenize(text)
    # Remove stopwords
    stop_words = set(stopwords.words('english'))
    tokens = [t for t in tokens if t not in stop_words]
    # Lemmatize
    lemmatizer = WordNetLemmatizer()
    tokens = [lemmatizer.lemmatize(t) for t in tokens]
    return ' '.join(tokens)
```

### TF-IDF Vectorization

```python
from sklearn.feature_extraction.text import TfidfVectorizer

vectorizer = TfidfVectorizer(
    max_features=5000,
    min_df=2,                 # Minimum document frequency
    max_df=0.95,              # Maximum document frequency
    ngram_range=(1, 2)        # Unigrams and bigrams
)
X_tfidf = vectorizer.fit_transform(texts)
```

**TF-IDF Formula**: `TF-IDF = TF × log(N/DF)`

### Word Embeddings

```python
from gensim.models import Word2Vec

# Train Word2Vec
model = Word2Vec(
    sentences=tokenized_texts,
    vector_size=100,
    window=5,
    min_count=2,
    workers=4,
    sg=1                      # 1=Skip-gram, 0=CBOW
)

# Get word vector
vector = model.wv['word']

# Similar words
similar = model.wv.most_similar('king', topn=5)
```

### Transformers with HuggingFace

```python
from transformers import AutoTokenizer, AutoModel, pipeline

# Load pre-trained model
tokenizer = AutoTokenizer.from_pretrained('bert-base-uncased')
model = AutoModel.from_pretrained('bert-base-uncased')

# Tokenize
inputs = tokenizer(text, return_tensors='pt', padding=True, truncation=True)

# Get embeddings
with torch.no_grad():
    outputs = model(**inputs)
    embeddings = outputs.last_hidden_state

# Classification pipeline
classifier = pipeline('sentiment-analysis')
result = classifier("I love this product!")
```

---

## 9. Time Series

### Time Series Basics

```python
import pandas as pd

# Create datetime index
df['date'] = pd.to_datetime(df['date'])
df.set_index('date', inplace=True)

# Resampling
daily = df.resample('D').mean()      # Daily
weekly = df.resample('W').sum()      # Weekly
monthly = df.resample('M').last()    # Monthly

# Rolling statistics
rolling_mean = df['value'].rolling(window=7).mean()
rolling_std = df['value'].rolling(window=7).std()

# Lag features
df['lag_1'] = df['value'].shift(1)
df['lag_7'] = df['value'].shift(7)
```

### Stationarity Testing

```python
from statsmodels.tsa.stattools import adfuller, kpss

# ADF test (null: non-stationary)
result = adfuller(series)
print(f'ADF Statistic: {result[0]:.4f}')
print(f'p-value: {result[1]:.4f}')

# Make stationary by differencing
diff_series = series.diff().dropna()
```

### ARIMA/SARIMA

```python
from statsmodels.tsa.arima.model import ARIMA
from statsmodels.tsa.statespace.sarimax import SARIMAX
import pmdarima as pm

# Auto ARIMA
auto_model = pm.auto_arima(
    series,
    seasonal=True,
    m=12,                     # Seasonal period
    suppress_warnings=True
)

# Manual SARIMA
model = SARIMAX(
    series,
    order=(1, 1, 1),          # (p, d, q)
    seasonal_order=(1, 1, 1, 12)  # (P, D, Q, m)
)
results = model.fit()
forecast = results.forecast(steps=12)
```

### Prophet

```python
from prophet import Prophet

# Prepare data (must have 'ds' and 'y' columns)
df_prophet = df.reset_index()
df_prophet.columns = ['ds', 'y']

# Fit model
model = Prophet(
    yearly_seasonality=True,
    weekly_seasonality=True,
    daily_seasonality=False
)
model.fit(df_prophet)

# Forecast
future = model.make_future_dataframe(periods=365)
forecast = model.predict(future)
```

---

## 10. Model Interpretability

### SHAP Values

```python
import shap

# Tree-based models
explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X)

# Summary plot
shap.summary_plot(shap_values, X, feature_names=feature_names)

# Force plot (single prediction)
shap.force_plot(explainer.expected_value, shap_values[0], X.iloc[0])

# Dependence plot
shap.dependence_plot('feature_name', shap_values, X)
```

### Feature Importance

```python
# Tree-based importance
importances = model.feature_importances_

# Permutation importance
from sklearn.inspection import permutation_importance
result = permutation_importance(model, X_test, y_test, n_repeats=10)
importance = result.importances_mean
```

### Partial Dependence Plots

```python
from sklearn.inspection import partial_dependence, PartialDependenceDisplay

# Single feature
PartialDependenceDisplay.from_estimator(model, X, ['feature_name'])

# Multiple features
PartialDependenceDisplay.from_estimator(model, X, ['f1', 'f2', ('f1', 'f2')])
```

---

## 11. Transformers & LLMs

### Attention Mechanism

```python
import torch
import torch.nn.functional as F

def scaled_dot_product_attention(Q, K, V, mask=None):
    d_k = Q.size(-1)
    scores = torch.matmul(Q, K.transpose(-2, -1)) / math.sqrt(d_k)
    if mask is not None:
        scores = scores.masked_fill(mask == 0, -1e9)
    attention_weights = F.softmax(scores, dim=-1)
    output = torch.matmul(attention_weights, V)
    return output, attention_weights
```

### Using LLM APIs

```python
from openai import OpenAI

client = OpenAI(api_key="your-key")

response = client.chat.completions.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Explain machine learning."}
    ],
    temperature=0.7,
    max_tokens=500
)
answer = response.choices[0].message.content
```

### RAG (Retrieval Augmented Generation)

```python
from langchain.embeddings import OpenAIEmbeddings
from langchain.vectorstores import FAISS
from langchain.text_splitter import RecursiveCharacterTextSplitter

# Split documents
splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=200)
chunks = splitter.split_documents(documents)

# Create vector store
embeddings = OpenAIEmbeddings()
vectorstore = FAISS.from_documents(chunks, embeddings)

# Retrieve relevant documents
docs = vectorstore.similarity_search(query, k=5)

# Generate with context
context = "\n".join([doc.page_content for doc in docs])
prompt = f"Context: {context}\n\nQuestion: {query}\n\nAnswer:"
```

### Prompt Engineering

```python
# Few-shot prompting
prompt = """
Classify the sentiment of these reviews:

Review: "Great product, love it!" -> Positive
Review: "Terrible, waste of money" -> Negative
Review: "It's okay, nothing special" -> Neutral

Review: "{user_review}" ->
"""

# Chain-of-thought
prompt = """
Let's solve this step by step:
1. First, identify the key information
2. Then, analyze the relationships
3. Finally, draw a conclusion

Question: {question}
"""
```

---

## 12. MLOps

### Experiment Tracking (MLflow)

```python
import mlflow

mlflow.set_experiment("my_experiment")

with mlflow.start_run():
    # Log parameters
    mlflow.log_param("learning_rate", 0.01)
    mlflow.log_param("n_estimators", 100)
    
    # Train model
    model.fit(X_train, y_train)
    
    # Log metrics
    mlflow.log_metric("accuracy", accuracy)
    mlflow.log_metric("f1_score", f1)
    
    # Log model
    mlflow.sklearn.log_model(model, "model")
```

### Model Deployment (FastAPI)

```python
from fastapi import FastAPI
from pydantic import BaseModel
import joblib

app = FastAPI()

# Load model
model = joblib.load("model.pkl")

class PredictionRequest(BaseModel):
    features: list

@app.post("/predict")
def predict(request: PredictionRequest):
    prediction = model.predict([request.features])
    return {"prediction": prediction.tolist()}
```

### Docker for ML

```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Data Drift Detection

```python
from evidently import ColumnDriftMetric
from evidently.report import Report

report = Report(metrics=[ColumnDriftMetric(column_name='feature')])
report.run(reference_data=train_df, current_data=new_df)
report.show()
```

---

## 13. Reinforcement Learning

### Q-Learning

```python
import numpy as np

class QLearningAgent:
    def __init__(self, n_states, n_actions, lr=0.1, gamma=0.99, epsilon=0.1):
        self.q_table = np.zeros((n_states, n_actions))
        self.lr = lr
        self.gamma = gamma
        self.epsilon = epsilon
    
    def choose_action(self, state):
        if np.random.random() < self.epsilon:
            return np.random.randint(self.q_table.shape[1])
        return np.argmax(self.q_table[state])
    
    def update(self, state, action, reward, next_state, done):
        target = reward + self.gamma * np.max(self.q_table[next_state]) * (1 - done)
        self.q_table[state, action] += self.lr * (target - self.q_table[state, action])
```

### Stable-Baselines3

```python
from stable_baselines3 import PPO, DQN
import gym

# Create environment
env = gym.make('CartPole-v1')

# Train agent
model = PPO('MlpPolicy', env, verbose=1)
model.learn(total_timesteps=10000)

# Evaluate
obs = env.reset()
for _ in range(1000):
    action, _ = model.predict(obs, deterministic=True)
    obs, reward, done, info = env.step(action)
    if done:
        obs = env.reset()
```

---

## 14. Code Templates

### Complete ML Pipeline

```python
import pandas as pd
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report

# 1. Load data
df = pd.read_csv('data.csv')

# 2. Preprocess
X = df.drop('target', axis=1)
y = df['target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# 3. Scale features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# 4. Train model
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train_scaled, y_train)

# 5. Evaluate
cv_scores = cross_val_score(model, X_train_scaled, y_train, cv=5)
print(f"CV Score: {cv_scores.mean():.4f} (+/- {cv_scores.std()*2:.4f})")

y_pred = model.predict(X_test_scaled)
print(classification_report(y_test, y_pred))
```

### Hyperparameter Tuning Template

```python
from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import randint, uniform

param_distributions = {
    'n_estimators': randint(50, 500),
    'max_depth': randint(3, 20),
    'min_samples_split': randint(2, 20),
    'min_samples_leaf': randint(1, 10),
    'max_features': ['sqrt', 'log2', None]
}

search = RandomizedSearchCV(
    RandomForestClassifier(random_state=42),
    param_distributions,
    n_iter=100,
    cv=5,
    scoring='f1',
    n_jobs=-1,
    random_state=42
)
search.fit(X_train, y_train)

print(f"Best parameters: {search.best_params_}")
print(f"Best score: {search.best_score_:.4f}")
```

---

## Quick Reference Tables

### When to Use Which Model

| Problem | First Try | If Doesn't Work |
|---------|-----------|-----------------|
| Binary Classification | Logistic Regression | XGBoost, Random Forest |
| Multi-class | Random Forest | XGBoost, Neural Network |
| Regression | Linear Regression | XGBoost, Gradient Boosting |
| High-dimensional | Lasso, Ridge | Random Forest |
| Text Classification | TF-IDF + Logistic | BERT, Transformers |
| Time Series | ARIMA, Prophet | LSTM, XGBoost with lags |
| Images | CNN (ResNet, VGG) | Vision Transformer |
| Clustering | K-Means | DBSCAN, Hierarchical |
| Anomaly Detection | Isolation Forest | Autoencoder, LOF |

### Hyperparameter Tuning Priorities

| Model | Most Important | Second Priority |
|-------|----------------|-----------------|
| Random Forest | n_estimators, max_depth | min_samples_split |
| XGBoost | learning_rate, n_estimators | max_depth, subsample |
| Neural Network | learning_rate, architecture | batch_size, regularization |
| SVM | C, kernel, gamma | - |
| KNN | n_neighbors, weights | metric |

### Common Mistakes to Avoid

1. **Data leakage**: Fit scaler/encoder on train only
2. **Ignoring class imbalance**: Use stratified split, class weights
3. **Not using cross-validation**: Always use k-fold
4. **Overfitting**: Use regularization, early stopping
5. **Wrong metric**: Classification → F1/AUC, Regression → RMSE/MAE
6. **Not handling missing values**: Impute before modeling
7. **Feature scaling**: Required for distance-based models
8. **Ignoring feature importance**: Interpret your models

---

*This cheatsheet covers the key concepts needed to complete 620+ ML assignments from beginner to expert level.*
