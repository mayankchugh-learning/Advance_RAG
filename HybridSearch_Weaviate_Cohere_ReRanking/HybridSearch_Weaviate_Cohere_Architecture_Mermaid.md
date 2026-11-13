# Advanced RAG Ep 02 — Pipeline Architecture
### by Mayank Chugh | IT AI Enthusiast | @itaienthusiast

Diagram for [`HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb`](HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb) (June 2026). It follows that notebook: collection `RAG` embedded with `BAAI/bge-base-en-v1.5`, a custom `WeaviateV4HybridRetriever` at `alpha=0.5`, Cohere `rerank-v3.5`, and `Qwen/Qwen3-8B` in NF4 4-bit.

**Render at:** [mermaid.live](https://mermaid.live) | Notion | GitHub | Medium

---

```mermaid
flowchart TD
  subgraph P1["🔧 Phase 1 — Setup & Index"]
    direction TB
    A([Weaviate Cloud Cluster]) --> B[HF Token + API Keys]
    B --> C["Collection RAG\ntext2vec-huggingface\nBAAI/bge-base-en-v1.5"]
    C --> D["WeaviateV4HybridRetriever\nalpha=0.5"]
  end

  subgraph P2["🔍 Phase 2 — Hybrid Retrieval"]
    direction TB
    E([User Query]) --> F[BM25 Sparse\nKeyword Search]
    E --> G[Dense Embedding\nSemantic Search]
    F --> H["Weaviate Fusion\n(RRF / alpha blend)"]
    G --> H
    H --> I[Top-K Documents]
  end

  subgraph P3["🎯 Phase 3 — Rerank & Generate"]
    direction TB
    J["Cohere rerank-v3.5\nCohereRerank"] --> K[ContextualCompression\nRetriever]
    K --> L["Qwen3-8B\nNF4 4-bit"]
    L --> M([Final Answer])
  end

  P1 --> P2
  D --> H
  I --> J

  classDef setup   fill:#E6F1FB,stroke:#378ADD,color:#042C53
  classDef retrieve fill:#EAF3DE,stroke:#3B6D11,color:#173404
  classDef rerank  fill:#EEEDFE,stroke:#534AB7,color:#26215C
  classDef io      fill:#FAEEDA,stroke:#BA7517,color:#412402

  class A,B,C,D setup
  class E,F,G,H,I retrieve
  class J,K,L rerank
  class E,M io
```

---

## Colour Reference

| Phase | Colour | Represents |
|-------|--------|-----------|
| Phase 1 — Setup & Index | Blue (`#E6F1FB` / `#378ADD`) | Infrastructure & configuration |
| Phase 2 — Hybrid Retrieval | Green (`#EAF3DE` / `#3B6D11`) | Dual retrieval + fusion |
| Phase 3 — Rerank & Generate | Purple (`#EEEDFE` / `#534AB7`) | Reranking + LLM generation |
| Input / Output nodes | Amber (`#FAEEDA` / `#BA7517`) | User query + final answer |

---

## Key Design Decisions

- **Parallel branches in Phase 2** — BM25 and semantic search run simultaneously from the same user query, both feeding into Weaviate's RRF fusion step
- **Phase 1 feeds Phase 2 via `D → H`** — `WeaviateV4HybridRetriever` (`alpha=0.5`) is the bridge between setup and retrieval
- **Reranker wraps the retriever** — `ContextualCompressionRetriever` sits between Cohere `rerank-v3.5` and Qwen3-8B, acting as a quality filter before generation
- **Saved demo scores reorder chunks** — for *“What is Abstractive Question Answering?”* the notebook’s executed Cohere rerank returned 0.6641, 0.3853, and 0.0860
- **Oval nodes** = external I/O (user query, final answer); **rectangle nodes** = internal processing steps

---

*Made with ❤️ by Mayank Chugh | GitHub: mayankchugh-learning | @itaienthusiast*
