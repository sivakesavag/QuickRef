# Quantization

## What is Quantization?

Quantization is a model compression technique that **reduces the numerical precision** of a model's weights (and optionally activations) from higher-precision formats (e.g., FP32, FP16) to lower-precision formats (e.g., INT8, INT4). This shrinks model size, reduces memory footprint, and accelerates inference.

> **Core Idea**: Represent 32-bit floating-point numbers using fewer bits with minimal accuracy loss.

---

## Why Quantize?

| Benefit | Impact |
|---|---|
| **Smaller model size** | FP16 → INT4 = ~4× size reduction |
| **Lower memory usage** | Fit larger models on smaller GPUs |
| **Faster inference** | Integer ops are faster than floating-point on most hardware |
| **Reduced power consumption** | Critical for edge/mobile deployment |
| **Lower cost** | Serve models on cheaper hardware |

**Example**: LLaMA 70B in FP16 ≈ 140 GB → INT4 ≈ 35 GB (fits on a single 48GB GPU).

---

## Number Formats

| Format | Bits | Range | Use Case |
|---|---|---|---|
| FP32 | 32 | ±3.4 × 10³⁸ | Training (standard) |
| BF16 | 16 | ±3.4 × 10³⁸ (lower precision) | Training (modern GPUs) |
| FP16 | 16 | ±65,504 | Inference, mixed-precision training |
| FP8 (E4M3/E5M2) | 8 | Varies | Training & inference on latest GPUs |
| INT8 | 8 | -128 to 127 | Quantized inference |
| INT4 | 4 | -8 to 7 | Aggressive quantization |
| NF4 | 4 | Non-uniform (normal dist.) | QLoRA-specific format |
| Binary/Ternary | 1–2 | {-1, 0, 1} | Extreme compression (research) |

---

## Quantization Math

### Linear (Uniform) Quantization

Map a floating-point range to a fixed set of integer values:

$$x_q = \text{round}\left(\frac{x}{s}\right) + z$$

$$x_{dequant} = s \cdot (x_q - z)$$

Where:
- $s$ = **scale**: `(x_max - x_min) / (2^b - 1)` (maps float range to int range)
- $z$ = **zero-point**: ensures 0.0 maps exactly to an integer
- $b$ = number of bits

### Symmetric vs Asymmetric

| Type | Zero-Point | Range | Use Case |
|---|---|---|---|
| **Symmetric** | z = 0 | [-max, +max] | Weights (centered around 0) |
| **Asymmetric** | z ≠ 0 | [min, max] | Activations (often skewed) |

### Granularity

| Level | Description | Trade-off |
|---|---|---|
| **Per-tensor** | One scale/zero-point for entire tensor | Fastest, least accurate |
| **Per-channel** | One scale/zero-point per output channel | Good balance (standard for INT8) |
| **Per-group** | One scale per group of elements (e.g., 128) | Better accuracy, used in INT4 (GPTQ, AWQ) |
| **Per-element** | Individual scale per weight | Maximum accuracy, maximum overhead |

---

## Quantization Methods

### Post-Training Quantization (PTQ)
Quantize **after training is complete**. No retraining needed.

| Method | Description |
|---|---|
| **Dynamic Quantization** | Weights quantized offline; activations quantized on-the-fly at inference |
| **Static Quantization** | Both weights and activations quantized offline using a calibration dataset |
| **Weight-Only Quantization** | Only quantize weights; keep activations in FP16 (most common for LLMs) |

### Quantization-Aware Training (QAT)
Simulate quantization **during training** using fake quantization nodes. Model learns to be robust to quantization noise.

- **Straight-Through Estimator (STE)**: Approximate gradients through the non-differentiable rounding operation.
- Higher accuracy than PTQ but requires full training pipeline.

---

## LLM Quantization Methods

| Method | Type | Bits | Key Idea |
|---|---|---|---|
| **GPTQ** | PTQ (weight-only) | 2–8 | Layer-wise quantization using approximate second-order information (Hessian) |
| **AWQ** | PTQ (weight-only) | 4 | Protect salient weight channels (identified by activation magnitude) |
| **GGUF** (llama.cpp) | PTQ (weight-only) | 2–8 | CPU-optimized quantization format with mixed precision per layer |
| **bitsandbytes** | PTQ (weight-only) | 4, 8 | NF4 / INT8 quantization, integrated with HuggingFace |
| **SmoothQuant** | PTQ (W8A8) | 8 | Migrate quantization difficulty from activations to weights via channel-wise scaling |
| **QuIP#** | PTQ (weight-only) | 2–4 | Incoherence-processed quantization for extreme compression |
| **HQQ** | PTQ (weight-only) | 2–4 | Half-Quadratic Quantization, no calibration data needed |
| **AQLM** | PTQ (weight-only) | 2 | Additive quantization with learned codebooks |
| **QAT** | Training-time | 4–8 | Quantization-aware fine-tuning |

---

## Practical Comparison

| Method | Calibration Data? | Speed | Accuracy (INT4) | GPU Required? |
|---|---|---|---|---|
| **GPTQ** | Yes (128–1024 samples) | Minutes | ★★★★ | Yes |
| **AWQ** | Yes (small set) | Minutes | ★★★★★ | Yes |
| **GGUF** | No | Fast | ★★★ | No (CPU) |
| **bitsandbytes** | No | Instant (on-load) | ★★★ | Yes |
| **SmoothQuant** | Yes | Fast | ★★★★ (INT8) | Yes |

---

## Mixed-Precision Quantization

Not all layers are equally sensitive to quantization:

- **Attention layers**: More sensitive → use higher precision (INT8 or FP16).
- **FFN layers**: More robust → can use INT4.
- **First/last layers**: Often kept at higher precision.
- **Embedding layers**: Usually kept in FP16.

Many modern methods (GGUF, AWQ) automatically assign different precision per layer.

---

## Quantization Pipeline

```
1. Select Model & Target Precision
   └── Balance: model size vs accuracy vs hardware constraints

2. Choose Method
   ├── No calibration data? → bitsandbytes, HQQ, GGUF
   ├── Have calibration data? → GPTQ, AWQ, SmoothQuant
   └── Can retrain? → QAT (best accuracy)

3. Calibrate (if applicable)
   ├── Use 128–1024 representative samples
   └── Samples should reflect deployment distribution

4. Quantize
   ├── Apply chosen method
   └── Save quantized model

5. Evaluate
   ├── Perplexity on held-out data
   ├── Task-specific benchmarks
   └── Compare against FP16 baseline

6. Benchmark Inference
   ├── Throughput (tokens/sec)
   ├── Latency (time to first token)
   └── Memory footprint
```

---

## Rules of Thumb

- **INT8**: Nearly lossless for most models. Safe default.
- **INT4**: 1–3% accuracy drop typical. Good for deployment.
- **INT3/INT2**: Significant accuracy loss. Only for very large models (70B+).
- **Weight-only quantization**: Best for LLMs (activations are harder to quantize due to outliers).
- **Larger models quantize better**: A 70B model at INT4 often outperforms a 7B model at FP16.

---

## Common Pitfalls

- **Activation outliers**: A few extreme activation values can ruin quantization. Use SmoothQuant or outlier-aware methods.
- **Evaluating only perplexity**: Perplexity may look fine while task-specific performance degrades. Evaluate on downstream tasks.
- **Ignoring hardware**: INT4 is only faster than FP16 if your hardware has INT4 compute kernels (e.g., NVIDIA Ada/Hopper).
- **Calibration data mismatch**: Calibration data should match deployment distribution.
- **Over-quantizing small models**: Models < 3B parameters are very sensitive to quantization below INT8.
