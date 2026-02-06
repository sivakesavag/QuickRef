# Chapter 25: Machine Learning

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `scikit-learn` basics, Supervised vs Unsupervised, Train/Test Split, Overfitting/Underfitting, Linear Regression, Random Forest, K-Means, Metrics (Accuracy, Precision, Recall, F1), Scaling (`StandardScaler`), Encoding (`OneHotEncoder`), Pipelines.

---

**Q25.1: Basic - [Scikit-Learn Goal]**

`scikit-learn` is primarily used for:

A) Deep Learning (Neural Networks).
B) Classical Machine Learning (Regression, Classification, Clustering) and preprocessing.
C) Web Development.
D) Game Dev.

**Answer: B**

**Explanation:**
While it has simple MLP support, it's best known for cohesive tools for traditional algorithms (SVM, Random Forest, PCA).

---

**Q25.2: Intermediate - [Fit Predict]**

The standard API consistency in scikit-learn means almost all estimators use:

A) `train()` and `test()`.
B) `fit(X, y)` to train, and `predict(X)` to infer.
C) `learn()` and `guess()`.
D) `run()` and `check()`.

**Answer: B**

**Explanation:**
This uniform interface makes swapping algorithms (e.g., LogisticRegression to SVM) incredibly easy.

---

**Q25.3: Advanced - [Train Test Split]**

`train_test_split(X, y, test_size=0.2, random_state=42)`:

A) Splits the data structure in half.
B) Shuffles and splits the dataset, holding out 20% for testing (evaluation) and 80% for training.
C) Duplicates data.
D) Checks for errors.

**Answer: B**

**Explanation:**
Crucial to evaluate how the model generalizes to *unseen* data, preventing creating a model that just memorizes the training set.

---

**Q25.4: Basic - [Supervised Learning]**

In Supervised Learning:

A) The data has no labels (we look for patterns).
B) The data comes with "ground truth" labels (target variable) that the model tries to predict.
C) The computer learns to play games.
D) A supervisor watches the screen.

**Answer: B**

**Explanation:**
Examples: Spam detection (Spam/Not Spam), House Price prediction.

---

**Q25.5: Intermediate - [Overfitting]**

Overfitting occurs when:

A) The model performs poorly on both training and test data.
B) The model fits the training data *too* well (capturing noise), resulting in poor performance on new/test data.
C) The model is too simple.
D) The computer overheats.

**Answer: B**

**Explanation:**
High variance. Solutions: simplify model, regularization, more data.

---

**Q25.6: Advanced - [StandardScaler]**

`StandardScaler` transforms features by:

A) Scaling them to range [0, 1].
B) Subtracting the mean and dividing by the standard deviation (Z-score normalization), resulting in mean=0 and std=1.
C) Multiplying by 100.
D) Converting to integers.

**Answer: B**

**Explanation:**
Essential for algorithms sensitive to distance (SVM, K-Means, KNN) or gradient descent.

---

**Q25.7: Expert - [Pipeline]**

A Scikit-Learn `Pipeline` (`make_pipeline(StandardScaler(), LogisticRegression())`):

A) Connects to the internet.
B) Chains preprocessing steps and a final estimator into a single object that prevents "data leakage" (ensuring scaling parameters are learned from train set only).
C) Is a pipe character `|`.
D) Is mainly for visualization.

**Answer: B**

**Explanation:**
Best practice for production code. Calling `pipeline.fit(X_train, y_train)` automatically fits the scaler on X_train and transforms it before passing to the classifier.

---

**Q25.8: Basic - [Regression vs Classification]**

Regression predicts a ________ value, while Classification predicts a ________ value.

A) Continuous (Price); Discrete (Label).
B) Discrete; Continuous.
C) True; False.
D) Random; Fixed.

**Answer: A**

**Explanation:**
Regression: "Temp is 23.5". Classification: "Is it Hot? Yes/No".

---

**Q25.9: Intermediate - [OneHotEncoder]**

`OneHotEncoder` is used to:

A) Encrypt data.
B) Convert categorical features (e.g., "Red", "Blue") into binary vectors (e.g., [1, 0] for "Red", [0, 1] for "Blue") suitable for ML models.
C) Compress images.
D) Sort lists.

**Answer: B**

**Explanation:**
Models generally require numerical input. `OneHotEncoder` avoids implying an order (Red < Blue) that `LabelEncoder` might.

---

**Q25.10: Advanced - [Confusion Matrix]**

A Confusion Matrix shows:

A) Code that is hard to read.
B) A breakdown of True Positives, False Positives, True Negatives, and False Negatives.
C) A plot of errors over time.
D) Memory usage.

**Answer: B**

**Explanation:**
Better than simple "Accuracy" for understanding *how* a model is failing (e.g., is it flagging legitimate email as spam?).

---

**Q25.11: Basic - [Linear Regression]**

Linear Regression tries to fit:

A) A straight line (or plane) that minimizes the sum of squared errors between predictions and actual values.
B) A curved polynomial.
C) A decision tree.
D) A circle.

**Answer: A**

**Explanation:**
The simplest regression algorithm. `y = mx + c`.

---

**Q25.12: Intermediate - [K-Means]**

K-Means is a ________ algorithm.

A) Supervised Classification.
B) Unsupervised Clustering (grouping similar data points without labels).
C) Regression.
D) Reinforcement.

**Answer: B**

**Explanation:**
Finds `k` centroids and assigns points to the nearest cluster.

---

**Q25.13: Advanced - [Random Forest]**

A Random Forest is an "Ensemble" method because:

A) It grows trees randomly.
B) It combines the predictions of many Decision Trees (trained on random subsets of data/features) to improve stability and reduce overfitting.
C) It uses randomness for security.
D) It runs in a forest.

**Answer: B**

**Explanation:**
Bagging (Bootstrap Aggregating) technique. Usually outperforms single decision trees.

---

**Q25.14: Expert - [Cross Validation]**

`cross_val_score(model, X, y, cv=5)`:

A) Splits data into 5 parts, trains on 4 and tests on 1, rotating 5 times to get a robust estimate of model performance.
B) Validates the data types.
C) Checks for viruses.
D) Multiplies the score by 5.

**Answer: A**

**Explanation:**
K-Fold Cross Validation gives a more reliable metric than a single train/test split, especially on small datasets.

---

**Q25.15: Intermediate - [Precision vs Recall]**

High Precision means ________, while High Recall means ________.

A) Few False Positives (Clean results); Few False Negatives (Found everything).
B) Few False Negatives; Few False Positives.
C) Fast; Slow.
D) Accurate; Precise.

**Answer: A**

**Explanation:**
Precision: "Of the spam I flagged, how much was actually spam?". Recall: "Of all the actual spam, how much did I find?".

---

**Q25.16: Basic - [Fit Transform]**

For a Scaler/Preprocessor, `fit_transform(X_train)`:

A) Calculates parameters (mean/std) from X_train AND applies the transformation.
B) Only calculates.
C) Only transforms.
D) Does nothing.

**Answer: A**

**Explanation:**
On test data, you should ONLY call `transform()`, using the mean/std learned from training data.

---

**Q25.17: Advanced - [Imputer]**

`SimpleImputer(strategy='mean')`:

A) Deletes rows.
B) Fills missing values (NaNs) with the mean of the column.
C) Computes mean only.
D) Is a putter in golf.

**Answer: B**

**Explanation:**
Standard way to handle missing data to keep rows usable.

---

**Q25.18: Intermediate - [Logistic Regression]**

Despite the name, Logistic Regression is used for:

A) Regression (Predicting values).
B) Classification (Predicting probabilities of belonging to a class, usually binary).
C) Logic puzzles.
D) Organizing logistics.

**Answer: B**

**Explanation:**
It uses the logistic (sigmoid) function to squash output between 0 and 1.

---

**Q25.19: Basic - [Feature Matrix X]**

In `model.fit(X, y)`, `X` is conventionally:

A) A 1D array of targets.
B) A 2D feature matrix (Rows=Samples, Columns=Features).
C) A generic object.
D) A list of strings.

**Answer: B**

**Explanation:**
Shape is `(n_samples, n_features)`.

---

**Q25.20: Expert - [Hyperparameter Tuning]**

`GridSearchCV` is used to:

A) Search the web for data.
B) Exhaustively try a grid of defined hyperparameters (e.g., `C` in SVM, `max_depth` in Tree) to find the best combination for the model.
C) Visualize the grid.
D) Align the grid.

**Answer: B**

**Explanation:**
Automates the "tuning" process using cross-validation.

---

**Q25.21: Intermediate - [Bias vs Variance]**

High Bias usually leads to ________, while High Variance leads to ________.

A) Overfitting; Underfitting.
B) Underfitting (Model too simple); Overfitting (Model too complex).
C) Nothing; Nothing.
D) Success; Failure.

**Answer: B**

**Explanation:**
The classic Bias-Variance Tradeoff. `LinearRegression` = High Bias. `DecisionTree` (deep) = High Variance.

---

**Q25.22: Basic - [KNN]**

K-Nearest Neighbors (KNN) works by:

A) Trying to find the K closest training points to a new sample and voting on the label.
B) Neural Networks.
C) Drawing lines.
D) Random guessing.

**Answer: A**

**Explanation:**
Lazy learning (instance-based). No training phase per se, just storing data.

---

**Q25.23: Advanced - [Dimensionality Reduction]**

PCA (Principal Component Analysis) is used to:

A) Increase dimensions.
B) Reduce the number of feature dimensions (projecting data to lower dimensional space) while retaining the most variance/information.
C) Sort data.
D) Add noise.

**Answer: B**

**Explanation:**
Useful for visualization (2D/3D) or removing correlated features (Curse of Dimensionality).

---

**Q25.24: Expert - [Stratify]**

In `train_test_split(X, y, stratify=y)`:

A) It splits randomly.
B) It ensures the proportion of classes (e.g., 90% No, 10% Yes) is preserved in both the Train and Test sets.
C) It stratifies rocks.
D) It sorts y.

**Answer: B**

**Explanation:**
Critical for imbalanced datasets (e.g., Fraud detection). Without it, the test set might end up with 0 fraud cases.

---

**Q25.25: Intermediate - [Score]**

`model.score(X_test, y_test)` typically returns:

A) The error rate.
B) The default metric (Accuracy for Classification, R^2 for Regression).
C) The predictions.
D) Nothing.

**Answer: B**

**Explanation:**
Quick way to gauge performance.

---

**Q25.26: Basic - [Target y]**

The `y` variable in `fit(X, y)` represents:

A) The labels / target variable / outcome.
B) The features.
C) The index.
D) The question.

**Answer: A**

**Explanation:**
Convention: X is uppercase (Matrix), y is lowercase (Vector).

---

**Q25.27: Advanced - [Regularization]**

L1 (Lasso) and L2 (Ridge) Regularization are techniques to:

A) Speed up training.
B) Penalize large coefficients in the model to reduce complexity and prevent overfitting.
C) Make the model fit training data better.
D) Add more features.

**Answer: B**

**Explanation:**
L1 can drive coefficients to zero (feature selection). L2 shrinks them.

---

**Q25.28: Expert - [Data Leakage]**

"Data Leakage" happens when:

A) You spill coffee on the server.
B) Information from the testing set (or future) accidentally leaks into the training process (e.g., scaling before splitting), leading to overly optimistic results.
C) You lose data.
D) RAM leaks.

**Answer: B**

**Explanation:**
A cardinal sin in ML. Always split *before* preprocessing.

---

**Q25.29: Intermediate - [Decision Tree decision]**

A Decision Tree makes predictions by:

A) Using a complex equation.
B) Asking a series of if-else questions based on features (splitting nodes) until a leaf node is reached.
C) Randomly guessing.
D) Voting.

**Answer: B**

**Explanation:**
Highly interpretable ("White box" model).

---

**Q25.30: Basic - [Unsupervised Example]**

An example of Unsupervised Learning is:

A) Training a car to drive by showing it videos of driving.
B) Grouping customers into market segments based on purchasing behavior (Clustering).
C) Predicting house prices.
D) Classifying images as cat vs dog.

**Answer: B**

**Explanation:**
No predefined labels ("Segment A", "Segment B"); the algorithms finds the structure itself.

---

**Q25.31: Intermediate - [SVC C parameter]**

In Support Vector Machines (SVC), a large 'C' parameter means:

A) High regularization (Simple boundary, can tolerate misclassifications).
B) Low regularization (Tries hard to classify every training point correctly, even if it means a complex boundary -> risk of overfitting).
C) Speed.
D) Clustering.

**Answer: B**

**Explanation:**
C is the penalty for error. High penalty = Strict training fit.

---

**Q25.32: Advanced - [R Squared]**

The R^2 (Coefficient of Determination) score in regression:

A) Is always greater than 1.
B) Represents the proportion of variance in the dependent variable that is predictable from the independent variables (1.0 = Perfect fit, 0.0 = Model is as good as just predicting the mean).
C) Is the error rate.
D) Is for classification.

**Answer: B**

**Explanation:**
Can be negative if the model is arbitrarily worse than a constant line.

---

**Q25.33: Basic - [K-Fold]**

K-Fold Cross Validation usually sets K to:

A) 1
B) 5 or 10.
C) 1000
D) 0

**Answer: B**

**Explanation:**
Standard trade-off between variance and bias/time.

---

**Q25.34: Expert - [Gradient Boosting]**

Gradient Boosting (e.g., XGBoost, LightGBM) works by:

A) Averaging trees.
B) Sequentially building trees, where each new tree tries to correct the errors (residuals) made by the previous trees.
C) Randomly guessing.
D) Using neural networks.

**Answer: B**

**Explanation:**
Can be very powerful but prone to overfitting if not tuned (learning rate, depth).

---

**Q25.35: Intermediate - [Classification Report]**

`classification_report(y_true, y_pred)` prints:

A) Only accuracy.
B) A text report showing the main classification metrics (precision, recall, f1-score) for each class.
C) The confusion matrix.
D) A graph.

**Answer: B**

**Explanation:**
Essential for multi-class problems to see if one class is struggling.

---

**Q25.36: Advanced - [Silhouette Score]**

Silhouette Score is used to evaluate:

A) Regression models.
B) Clustering quality (How similar an object is to its own cluster compared to other clusters).
C) Classification accuracy.
D) Image sharpness.

**Answer: B**

**Explanation:**
Range is -1 to +1. High value means well-separated clusters.

---

**Q25.37: Basic - [Predict Proba]**

`model.predict_proba(X)` returns:

A) The class label.
B) The probability estimates for each class (e.g., [0.1, 0.9]).
C) The error.
D) The time taken.

**Answer: B**

**Explanation:**
Useful if you want to set a custom threshold (e.g., only flag fraud if prob > 90%).

---

**Q25.38: Intermediate - [MinMaxScaler]**

`MinMaxScaler` scales features to:

A) Mean 0, Variance 1.
B) A given range, usually [0, 1].
C) No range.
D) Integers.

**Answer: B**

**Explanation:**
Preserves the shape of the original distribution but squashes it. Sensitive to outliers.

---

**Q25.39: Advanced - [Imbalanced Data]**

Common techniques to handle highly imbalanced datasets include:

A) Do nothing.
B) Resampling (Oversampling minority class / Undersampling majority class) or using Class Weights (`class_weight='balanced'`).
C) Only looking at accuracy.
D) Deleting the data.

**Answer: B**

**Explanation:**
If 99% of data is negative, a model that always predicts "Negative" has 99% accuracy but is useless.

---

**Q25.40: Expert - [Kernel Trick]**

In SVM, the "Kernel Trick":

A) Compresses data.
B) Implicitly maps input vectors to a higher-dimensional feature space where they become linearly separable, without actually computing the coordinates.
C) Uses corn.
D) Is slow.

**Answer: B**

**Explanation:**
Allows linear classifiers (SVM) to solve non-linear problems efficiently.

---

**Q25.41: Basic - [Mean Squared Error]**

MSE (Mean Squared Error) is a common loss function for:

A) Classification.
B) Regression.
C) Clustering.
D) Sorting.

**Answer: B**

**Explanation:**
Penalizes large errors more heavily than MAE (Mean Absolute Error).

---

**Q25.42: Intermediate - [Pickle Model]**

To save a trained scikit-learn model to disk for later use:

A) Copy paste code.
B) Use `pickle.dump(model, file)` or `joblib.dump(model, file)`.
C) `model.save()`.
D) `save(model)`.

**Answer: B**

**Explanation:**
`joblib` is often more efficient for objects carrying large numpy arrays.

---

**Q25.43: Advanced - [ROC Curve]**

The ROC (Receiver Operating Characteristic) curve plots:

A) Accuracy vs Time.
B) True Positive Rate (Recall) vs False Positive Rate at defined probability thresholds.
C) Precision vs Recall.
D) Price vs Size.

**Answer: B**

**Explanation:**
AUC (Area Under Curve) summarizes this performance into a single number.

---

**Q25.44: Expert - [Variance Inflation Factor]**

VIF (Variance Inflation Factor) detects:

A) Inflation in economy.
B) Multicollinearity among predictors in regression (when features are highly correlated with each other).
C) Outliers.
D) Missing values.

**Answer: B**

**Explanation:**
High VIF (>5 or 10) indicates a feature is redundant, which destabilizes model coefficients.

---

**Q25.45: Intermediate - [Naive Bayes]**

Naive Bayes is "Naive" because:

A) It is simple.
B) It assumes that all features are independent of each other (given the class label), which is rarely true in real life but often works well.
C) It learns slowly.
D) It doesn't know math.

**Answer: B**

**Explanation:**
Very popular for text classification (Spam filtering) despite the strong assumption.

---

**Q25.46: Basic - [Epoch]**

In iterative training (like Neural Nets or SGD), an "Epoch" is:

A) One second.
B) One full pass of the entire training dataset through the algorithm.
C) One batch.
D) A million years.

**Answer: B**

**Explanation:**
Training usually involves many epochs.

---

**Q25.47: Advanced - [LabelEncoder]**

`LabelEncoder` transforms labels:

A) To One-Hot.
B) To integers (0, 1, 2...).
C) To text.
D) To images.

**Answer: B**

**Explanation:**
Usually used for the Target variable `y`, not features `X` (unless tree-based models), to avoid implying order.

---

**Q25.48: Expert - [T-SNE]**

t-SNE (t-Distributed Stochastic Neighbor Embedding) is mainly used for:

A) Prediction.
B) Visualizing high-dimensional data in 2D or 3D (Manifold learning).
C) Regression.
D) Sorting.

**Answer: B**

**Explanation:**
Great for seeing clusters in complex data (like MNIST digits), but preserving global structure is not guaranteed.

---

**Q25.49: Intermediate - [Elbow Method]**

The "Elbow Method" helps determine:

A) The best depth for a tree.
B) The optimal number of clusters (K) in K-Means.
C) The learning rate.
D) The arm strength.

**Answer: B**

**Explanation:**
You look for the kink in the inertia plot where adding more clusters gives diminishing returns.

---

**Q25.50: Basic - [Python ML Library]**

The most famous Python library for classical machine learning is:

A) NumPy.
B) Pandas.
C) Scikit-Learn.
D) Requests.

**Answer: C**

**Explanation:**
Built on top of NumPy, SciPy, and matplotlib.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
