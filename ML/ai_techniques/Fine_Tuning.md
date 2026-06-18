# Fine-Tuning

## What is Fine-Tuning?

Fine-tuning is the process of **taking a pre-trained model and further training it on a smaller, task-specific dataset** to adapt its behavior, style, or domain knowledge. It modifies the model's weights to specialize its capabilities.

> **Core Idea**: Pre-trained general model + domain-specific data → specialized model.

---

## Why Fine-Tune?

| Scenario | Why Fine-Tuning Helps |
|---|---|
| Domain adaptation | Teach medical, legal, or financial terminology and reasoning |
| Output style/format | Enforce consistent JSON, XML, or structured responses |
| Task specialization | Optimize for classification, summarization, code generation, etc. |
| Cost optimization | A fine-tuned smaller model can match a larger model's performance at lower cost |
| Latency reduction | Smaller fine-tuned model → faster inference |
| Behavior alignment | RLHF / DPO to align model with human preferences |

---

## Fine-Tuning Approaches

### Full Fine-Tuning
- Update **all** model parameters.
- Highest capacity to learn but most expensive.
- Risk of **catastrophic forgetting** (losing pre-trained knowledge).
- Requires significant GPU memory (full model + optimizer states + gradients).

### Parameter-Efficient Fine-Tuning (PEFT)
Update only a **small subset** of parameters. Dramatically reduces compute and memory.

| Method | How it Works | Trainable Params |
|---|---|---|
| **LoRA** | Inject low-rank decomposition matrices (A×B) into attention layers | ~0.1–1% |
| **QLoRA** | LoRA on a 4-bit quantized base model (NF4 + double quantization) | ~0.1–1% |
| **Adapter Layers** | Insert small trainable bottleneck layers between frozen transformer blocks | ~1–5% |
| **Prefix Tuning** | Prepend trainable continuous vectors to the key/value pairs in attention | ~0.1% |
| **Prompt Tuning** | Prepend trainable soft tokens to the input embedding | ~0.01% |
| **IA³** | Learn element-wise rescaling vectors for keys, values, and FFN activations | ~0.01% |

> **LoRA** is the most widely used PEFT method due to its simplicity and strong performance.

### LoRA in Detail

```
Original:    h = W · x           (W is frozen, shape d×d)
LoRA:        h = W · x + (B·A) · x   (A: d×r, B: r×d, r << d)
```

- **Rank `r`**: Controls capacity (typical: 8–64). Higher r = more expressive but more params.
- **Alpha `α`**: Scaling factor. The LoRA output is scaled by `α/r`.
- **Target modules**: Usually applied to `q_proj`, `v_proj` in attention. Can extend to `k_proj`, `o_proj`, and FFN layers.
- At inference, LoRA weights can be **merged** back into the base model (zero overhead).

---

## Fine-Tuning Pipeline

```
1. Data Preparation
   ├── Collect task-specific data
   ├── Format into instruction/completion pairs
   ├── Clean, deduplicate, balance classes
   └── Split: train / validation / test

2. Choose Base Model
   ├── Match model size to task complexity & budget
   └── Consider: Llama, Mistral, Gemma, Phi, Qwen

3. Configure Training
   ├── Learning rate: 1e-5 to 5e-5 (full FT), 1e-4 to 3e-4 (LoRA)
   ├── Epochs: 1–5 (watch for overfitting)
   ├── Batch size: as large as memory allows
   ├── Warmup steps: 5–10% of total steps
   └── Weight decay: 0.01–0.1

4. Train & Monitor
   ├── Track loss curves (train & val)
   ├── Early stopping on validation loss
   └── Save checkpoints

5. Evaluate
   ├── Task-specific metrics (accuracy, F1, BLEU, ROUGE)
   ├── Human evaluation for generative tasks
   └── Compare against base model baseline
```

---

## Data Formats

### Instruction Tuning (Supervised Fine-Tuning / SFT)
```json
{
  "instruction": "Summarize the following article in 3 bullet points.",
  "input": "The European Central Bank announced...",
  "output": "• ECB raised rates by 25bps\n• Inflation remains above target\n• Markets reacted positively"
}
```

### Chat Format
```json
{
  "messages": [
    {"role": "system", "content": "You are a helpful coding assistant."},
    {"role": "user", "content": "Write a Python function to reverse a string."},
    {"role": "assistant", "content": "def reverse(s): return s[::-1]"}
  ]
}
```

### Preference Data (for RLHF/DPO)
```json
{
  "prompt": "Explain quantum computing simply.",
  "chosen": "Quantum computing uses qubits that can be 0 and 1 simultaneously...",
  "rejected": "Quantum computing is a type of computing that uses quantum mechanics..."
}
```

---

## Alignment Fine-Tuning

| Method | Description |
|---|---|
| **SFT** | Supervised fine-tuning on curated instruction-response pairs |
| **RLHF** | Train a reward model on human preferences → optimize policy with PPO |
| **DPO** | Direct Preference Optimization — skip the reward model, optimize directly on preference pairs |
| **ORPO** | Odds Ratio Preference Optimization — combines SFT and alignment in one step |
| **KTO** | Kahneman-Tversky Optimization — uses binary (good/bad) feedback instead of pairwise comparisons |

**Typical pipeline**: Pre-training → SFT → Alignment (RLHF/DPO)

---

## Tools & Frameworks

| Tool | Purpose |
|---|---|
| **Hugging Face Transformers + PEFT** | Standard library for PEFT methods |
| **TRL** | Training library for SFT, RLHF, DPO |
| **Axolotl** | Streamlined fine-tuning config framework |
| **Unsloth** | 2x faster LoRA/QLoRA training with 60% less memory |
| **LLaMA-Factory** | Unified fine-tuning framework with 100+ models |
| **OpenAI Fine-tuning API** | Managed fine-tuning for GPT models |

---

## Common Pitfalls

- **Too little data**: < 100 examples often insufficient; aim for 500–10,000+ high-quality examples.
- **Overfitting**: Model memorizes training data. Use validation loss, dropout, and early stopping.
- **Catastrophic forgetting**: Full fine-tuning can degrade general capabilities. PEFT methods mitigate this.
- **Data quality > quantity**: Noisy or contradictory data hurts more than small data.
- **Wrong learning rate**: Too high → divergence; too low → no learning. Use a learning rate finder.
- **Ignoring evaluation**: Always compare against the base model to confirm improvement.
