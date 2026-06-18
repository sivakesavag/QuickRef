# Knowledge Distillation

## What is Knowledge Distillation?

Knowledge distillation is a model compression technique where a **smaller "student" model is trained to mimic the behavior of a larger, more capable "teacher" model**. The student learns from the teacher's soft probability distributions (soft labels) rather than just hard ground-truth labels.

> **Core Idea**: Large teacher model → transfers "dark knowledge" → compact student model that retains most of the teacher's performance.

---

## Why Distillation?

| Benefit | Description |
|---|---|
| **Model compression** | Deploy smaller models with similar accuracy |
| **Faster inference** | Fewer parameters → lower latency |
| **Lower cost** | Reduced compute, memory, and energy at inference |
| **Edge deployment** | Enable deployment on mobile, IoT, and embedded devices |
| **API cost reduction** | Replace expensive API calls (GPT-4) with a local distilled model |

---

## How It Works

### The Hinton Framework (2015)

The student is trained on a **weighted combination** of two losses:

$$\mathcal{L} = \alpha \cdot \mathcal{L}_{\text{hard}} + (1 - \alpha) \cdot T^2 \cdot \mathcal{L}_{\text{soft}}$$

Where:
- $\mathcal{L}_{\text{hard}}$: Standard cross-entropy with ground-truth labels.
- $\mathcal{L}_{\text{soft}}$: KL divergence between teacher and student soft distributions.
- $T$ (Temperature): Softens probability distributions. Higher T → softer, more informative distributions.
- $\alpha$: Balances hard vs soft loss (typically 0.1–0.5 for hard label weight).

### Temperature Scaling

```
Standard softmax:     p_i = exp(z_i) / Σ exp(z_j)
Softened softmax:     p_i = exp(z_i / T) / Σ exp(z_j / T)
```

- **T = 1**: Standard (peaked) distribution.
- **T > 1**: Softer distribution — reveals inter-class relationships (the "dark knowledge").
- **T → ∞**: Uniform distribution.

> **Dark knowledge**: A teacher trained on cats vs dogs might output [0.9, 0.05, 0.03, 0.02] for [cat, lynx, dog, car]. The soft probabilities reveal that "lynx" is more similar to "cat" than "car" is — information lost in hard labels.

---

## Types of Distillation

### By Knowledge Source

| Type | What is Transferred | Method |
|---|---|---|
| **Response-based** | Final output logits/probabilities | KL divergence on soft labels |
| **Feature-based** | Intermediate layer representations | MSE between teacher & student hidden states |
| **Relation-based** | Relationships between data points or layers | Similarity matrices, attention maps |

### By Architecture

| Type | Description |
|---|---|
| **Offline Distillation** | Teacher is pre-trained and frozen; student trains on teacher outputs |
| **Online Distillation** | Teacher and student train simultaneously; can be peer-to-peer |
| **Self-Distillation** | Model distills knowledge from its own deeper layers to shallower ones |

---

## LLM Distillation

For large language models, distillation takes specialized forms:

### 1. Logit-Based Distillation
- Student matches the teacher's output token-level probability distribution.
- Requires access to teacher logits (white-box).
- Most faithful transfer but needs teacher internals.

### 2. Black-Box / Data-Augmented Distillation
- Teacher generates synthetic training data (instruction-response pairs).
- Student is fine-tuned (SFT) on this synthetic data.
- No access to teacher weights needed — works with API-only models.
- Examples: Alpaca (GPT-3.5 → LLaMA), Vicuna, Orca.

### 3. Chain-of-Thought Distillation
- Teacher generates step-by-step reasoning traces.
- Student learns to replicate the reasoning process, not just the final answer.
- Significantly improves student reasoning capabilities.

### 4. Progressive Distillation
- Distill iteratively through intermediate-sized models.
- Teacher → Medium model → Small model (each stage transfers knowledge).

---

## Distillation Pipeline

```
1. Train / Select Teacher
   └── Large, high-accuracy model (or API model)

2. Generate Teacher Outputs
   ├── Run teacher on training data
   ├── Collect soft logits (white-box) or generated responses (black-box)
   └── Optionally generate CoT reasoning traces

3. Design Student Architecture
   ├── Fewer layers, smaller hidden dim, fewer attention heads
   └── Can be different architecture family

4. Train Student
   ├── Optimize combined hard + soft loss
   ├── Use temperature T = 2–20 for softening
   └── Monitor validation performance vs teacher

5. Evaluate
   ├── Compare student vs teacher on benchmarks
   ├── Measure compression ratio and speedup
   └── Verify no critical capability loss
```

---

## Key Hyperparameters

| Parameter | Typical Range | Effect |
|---|---|---|
| Temperature (T) | 2–20 | Higher = softer distributions, more dark knowledge |
| Alpha (α) | 0.1–0.5 | Weight of hard label loss |
| Student size | 1/4× to 1/10× teacher | Trade-off between compression and accuracy |
| Learning rate | 1e-4 to 1e-3 | Student training LR |

---

## Notable Examples

| Student | Teacher | Method |
|---|---|---|
| DistilBERT | BERT | Feature + response distillation (40% smaller, 60% faster, 97% perf) |
| TinyBERT | BERT | Two-stage: general + task-specific distillation |
| Alpaca 7B | GPT-3.5 | Black-box: SFT on 52K GPT-generated instructions |
| Orca | GPT-4 | CoT distillation with explanation traces |
| Gemma | Gemini | Distilled from larger Gemini family |
| Phi-series | Web data + GPT-4 | Textbook-quality synthetic data distillation |

---

## Common Pitfalls

- **Capacity gap**: If the student is too small, it cannot absorb the teacher's knowledge. Use progressive distillation.
- **Temperature too low**: Fails to capture inter-class relationships. Start with T=4 and tune.
- **Ignoring hard labels**: Soft labels alone may not ground the student well. Use both losses.
- **Data mismatch**: Student should be trained on data similar to deployment distribution.
- **Legal/licensing issues**: Distilling from proprietary APIs (e.g., GPT-4) may violate terms of service.
