# Retrieval-Augmented Generation (RAG)

## What is RAG?

RAG is an architecture that **enhances LLM outputs by retrieving relevant external knowledge** at inference time, rather than relying solely on the model's parametric memory. It decouples *knowledge* (stored in a retrieval corpus) from *reasoning* (performed by the LLM).

> **Core Idea**: Query → Retrieve relevant documents → Augment the prompt with retrieved context → Generate answer.

---

## Why RAG?

| Problem with vanilla LLMs | How RAG solves it |
|---|---|
| Knowledge cutoff (stale training data) | Retrieves from up-to-date external sources |
| Hallucinations / fabricated facts | Grounds responses in retrieved evidence |
| No access to private/domain data | Connects to proprietary knowledge bases |
| Expensive to retrain for new knowledge | Update the corpus instead of retraining |

---

## Architecture

```
┌──────────┐    ┌───────────────┐    ┌──────────────┐    ┌────────────┐
│  Query   │───▶│   Retriever   │───▶│   Augmented   │───▶│  Generator │
│          │    │ (search docs) │    │    Prompt      │    │   (LLM)    │
└──────────┘    └───────────────┘    └──────────────┘    └────────────┘
                       │
                ┌──────┴──────┐
                │  Knowledge  │
                │    Base     │
                │(vector DB / │
                │  index)     │
                └─────────────┘
```

### Key Components

1. **Indexing Pipeline** — Offline, one-time (or periodic) process:
   - **Document Loading**: Ingest raw data (PDFs, HTML, DBs, APIs).
   - **Chunking**: Split documents into manageable chunks (fixed-size, semantic, recursive).
   - **Embedding**: Convert chunks into dense vectors using an embedding model (e.g., `text-embedding-3-small`).
   - **Storage**: Store vectors + metadata in a vector database (Pinecone, Weaviate, Chroma, FAISS).

2. **Retrieval** — At query time:
   - Embed the user query with the same embedding model.
   - Perform **similarity search** (cosine similarity, dot product, or ANN) against the vector store.
   - Return top-k most relevant chunks.

3. **Generation** — Feed retrieved chunks + original query into the LLM as context.

---

## Retrieval Strategies

| Strategy | Description |
|---|---|
| **Dense Retrieval** | Embed query & docs into same vector space; use ANN search (FAISS, HNSW) |
| **Sparse Retrieval** | Traditional keyword-based (BM25, TF-IDF) |
| **Hybrid Retrieval** | Combine dense + sparse (e.g., reciprocal rank fusion) |
| **Re-ranking** | Use a cross-encoder to re-score top-k results for higher precision |
| **Multi-query** | LLM generates multiple query variants → retrieve for each → merge results |
| **HyDE** | LLM generates a hypothetical answer → use it as the retrieval query |

---

## Chunking Strategies

- **Fixed-size**: Split by token/character count with overlap (simple but may break context).
- **Recursive**: Split by separators (`\n\n` → `\n` → `. ` → ` `) hierarchically.
- **Semantic**: Use embedding similarity to detect natural breakpoints.
- **Document-aware**: Respect structure (headings, sections, paragraphs).

**Chunk size trade-off**: Smaller chunks → more precise retrieval but less context; larger chunks → more context but noisier retrieval.

---

## Advanced RAG Patterns

| Pattern | Description |
|---|---|
| **Naive RAG** | Basic retrieve → generate pipeline |
| **Advanced RAG** | Adds pre-retrieval (query rewriting) and post-retrieval (re-ranking, filtering) steps |
| **Modular RAG** | Flexible, composable modules (routing, query transformation, iterative retrieval) |
| **Agentic RAG** | LLM agent decides *when* and *what* to retrieve; can do multi-step retrieval |
| **Graph RAG** | Uses knowledge graphs for structured, relational retrieval |
| **Self-RAG** | Model self-reflects on whether retrieval is needed and if retrieved docs are relevant |
| **CRAG** | Corrective RAG — evaluates retrieval quality and falls back to web search if poor |

---

## Evaluation Metrics

- **Retrieval Quality**: Precision@k, Recall@k, MRR, NDCG.
- **Generation Quality**: Faithfulness (grounded in retrieved docs), Answer Relevancy, Context Relevancy.
- **Frameworks**: RAGAS, TruLens, LangSmith.

---

## RAG vs Fine-Tuning

| Dimension | RAG | Fine-Tuning |
|---|---|---|
| Knowledge update | Swap/update corpus (cheap) | Retrain model (expensive) |
| Traceability | Can cite source documents | No source attribution |
| Latency | Higher (retrieval step) | Lower (single forward pass) |
| Best for | Factual Q&A, dynamic knowledge | Style, format, domain adaptation |

> **Rule of thumb**: Use RAG for *knowledge*, fine-tuning for *behavior*. Combine both for best results.

---

## Common Pitfalls

- Poor chunking leading to loss of context or irrelevant retrieval.
- Embedding model mismatch between indexing and query time.
- Not using re-ranking (top-k from ANN is approximate, not optimal).
- Ignoring metadata filtering (dates, categories) for precision.
- Context window overflow when stuffing too many chunks.
