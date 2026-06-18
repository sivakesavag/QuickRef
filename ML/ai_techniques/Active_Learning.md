# Active Learning

## What is Active Learning?

Active learning is a **semi-supervised machine learning paradigm** where the model actively selects the most informative unlabeled data points to be labeled by an oracle (typically a human annotator). Instead of labeling data randomly, the model strategically chooses samples that would **maximize learning per label**, drastically reducing annotation costs.

> **Core Idea**: Start with few labels → model identifies what it's most uncertain about → human labels those → retrain → repeat.

---

## Why Active Learning?

| Problem | How Active Learning Helps |
|---|---|
| Labeling is expensive (medical, legal, specialized domains) | Reduces labels needed by 50–90% for same accuracy |
| Massive unlabeled data available | Prioritizes labeling effort on high-value samples |
| Cold-start with limited labeled data | Builds strong models from minimal initial labels |
| Class imbalance | Can strategically sample rare classes |
| Annotation budget constraints | Maximizes model performance per dollar spent |

---

## Active Learning Loop

```
┌─────────────────────────────────────────────────────┐
│                                                     │
│   ┌──────────┐    ┌─────────────┐    ┌──────────┐  │
│   │ Labeled   │───▶│ Train Model │───▶│  Query   │  │
│   │ Dataset   │    └─────────────┘    │ Strategy │  │
│   └────▲─────┘                        └────┬─────┘  │
│        │                                   │        │
│        │         ┌──────────────┐          │        │
│        └─────────│  Oracle      │◀─────────┘        │
│                  │  (Human      │  Select most      │
│                  │   Annotator) │  informative      │
│                  └──────────────┘  samples           │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### Steps:
1. **Initialize**: Train on a small seed set of labeled data.
2. **Query**: Use a strategy to select the most informative unlabeled samples.
3. **Annotate**: Human oracle labels the selected samples.
4. **Update**: Add newly labeled samples to the training set and retrain.
5. **Repeat** until performance target is met or budget is exhausted.

---

## Query Strategies

### 1. Uncertainty Sampling
Select samples where the model is **least confident** in its prediction.

| Variant | Formula / Approach | Best For |
|---|---|---|
| **Least Confidence** | $x^* = \arg\min_x \max_y P(y \mid x)$ | Simple classification |
| **Margin Sampling** | $x^* = \arg\min_x [P(y_1 \mid x) - P(y_2 \mid x)]$ | When top-2 classes are close |
| **Entropy Sampling** | $x^* = \arg\max_x -\sum_y P(y \mid x) \log P(y \mid x)$ | Multi-class problems |

> **Most popular** due to simplicity. Works well for classification tasks.

### 2. Query-by-Committee (QBC)
Train a **committee of models** (ensemble). Select samples where committee members **disagree** the most.

- **Vote Entropy**: Measure disagreement via entropy of committee votes.
- **KL Divergence**: Measure average divergence between each member's prediction and consensus.
- Committee can be: different architectures, different initializations, dropout-based (MC Dropout).

### 3. Diversity-Based / Representative Sampling
Select samples that are **most representative** of the unlabeled data distribution.

| Method | Description |
|---|---|
| **Core-Set** | Select points that minimize the maximum distance to any unlabeled point (geometric coverage) |
| **Cluster-Based** | Cluster unlabeled data; sample from under-represented clusters |
| **Feature-Space Diversity** | Select samples that maximize diversity in embedding space |

> Avoids the "sampling bias" problem of pure uncertainty sampling.

### 4. Expected Model Change
Select samples that would cause the **greatest change** in model parameters or gradients.

- **Expected Gradient Length (EGL)**: Choose samples with the largest expected gradient norm.
- Computationally expensive but theoretically principled.

### 5. Hybrid / Batch-Mode Strategies
Combine uncertainty + diversity to get the **best of both worlds**.

| Method | Description |
|---|---|
| **BADGE** | Gradient embeddings + k-means++ for diverse uncertain samples |
| **BALD** (Bayesian Active Learning by Disagreement) | Mutual information between predictions and model parameters |
| **BatchBALD** | Extension of BALD optimized for batch selection |
| **Learning Loss** | Train an auxiliary module to predict the loss of unlabeled samples |

---

## Scenarios

| Scenario | Description |
|---|---|
| **Pool-Based** | Large pool of unlabeled data; model queries from this pool (most common) |
| **Stream-Based** | Data arrives one at a time; model decides to label or skip each instance |
| **Membership Query Synthesis** | Model generates new synthetic data points to query the oracle |

---

## Active Learning for Deep Learning

Deep learning introduces unique challenges:

| Challenge | Solution |
|---|---|
| **Uncertainty estimation is hard** | Use MC Dropout, ensembles, or Bayesian approximations |
| **Retraining from scratch is expensive** | Use incremental / warm-start training |
| **Batch selection needed** (not single-sample) | Use batch-mode strategies (BADGE, BatchBALD) |
| **Feature representations change** | Re-embed unlabeled pool after each retraining cycle |

### MC Dropout for Uncertainty
Run inference **T times with dropout enabled**. Variance across runs ≈ model uncertainty.

```python
predictions = [model(x, training=True) for _ in range(T)]  # dropout active
uncertainty = np.var(predictions, axis=0)
```

---

## Active Learning for LLMs

| Approach | Description |
|---|---|
| **Selective annotation** | Use LLM confidence scores to identify hard examples for human labeling |
| **LLM-as-oracle** | Use a powerful LLM (GPT-4) as the annotator instead of humans |
| **Active fine-tuning** | Select the most informative examples for fine-tuning an LLM |
| **Active RAG** | Identify which documents in a corpus most need expert verification |

---

## Evaluation

- **Learning curve**: Plot accuracy vs number of labeled samples. Compare active learning strategy vs random sampling.
- **Area under the learning curve (AULC)**: Single metric summarizing the learning curve.
- **Label efficiency**: How many fewer labels are needed to reach target performance.

---

## Common Pitfalls

- **Cold start**: With very few initial labels, uncertainty estimates are unreliable. Use diversity-based seeding.
- **Sampling bias**: Pure uncertainty sampling can over-sample decision boundaries and ignore data regions. Add diversity.
- **Oracle noise**: Human annotators make mistakes, especially on ambiguous samples (which active learning preferentially selects).
- **Computational overhead**: Re-training + re-scoring the entire pool each cycle can be expensive. Use warm-starting and approximate methods.
- **Stopping criteria**: Know when to stop — diminishing returns on additional labels.
