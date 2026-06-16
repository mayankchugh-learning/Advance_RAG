# Advanced RAG Ep 02 — Pipeline Architecture
### by Mayank Chugh | IT AI Enthusiast | @itaienthusiast

**Render at:** [mermaid.live](https://mermaid.live) | Notion | GitHub | Medium

---

```mermaid
flowchart TD
  subgraph P1["🔧 Phase 1 — Setup & Index"]
    direction TB
    A([Weaviate Cloud Cluster]) --> B[HF Token + API Keys]
    B --> C["Schema: RAG class\ntext2vec-huggingface\n(MiniLM-L6-v2)"]
    C --> D[WeaviateHybridSearch\nRetriever — alpha=0.5]
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
    J[Cohere Rerank API\nCohereRerank] --> K[ContextualCompression\nRetriever]
    K --> L["Zephyr 7B Beta\n(NF4 4-bit quant)"]
    L --> M([Final Answer\nrelevance score 0.99])
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
- **Phase 1 feeds Phase 2 via `D → H`** — the WeaviateHybridSearchRetriever is the bridge between setup and retrieval
- **Reranker wraps the retriever** — `ContextualCompressionRetriever` sits between Cohere and Zephyr, acting as a quality filter before generation
- **Oval nodes** = external I/O (user query, final answer); **rectangle nodes** = internal processing steps

---

*Made with ❤️ by Mayank Chugh | GitHub: mayankchugh-learning | @itaienthusiast*
