# Advanced RAG Ep 03 & 04 — Reranking Pipeline Architecture
### by Mayank Chugh | IT AI Enthusiast | @itaienthusiast

**Render at:** [mermaid.live](https://mermaid.live) | Notion | GitHub | Medium

---

```mermaid
flowchart TD
  subgraph P1["Phase 1 — Corpus and Embedding"]
    direction TB
    A([8 Sample Documents]) --> B["Sentence Transformer\nall-MiniLM-L6-v2\n768-dim embeddings"]
    B --> C["Cosine Similarity\nquery vs all docs"]
    C --> D["Ranked Top-4\nCandidates"]
  end

  subgraph P2a["Phase 2a — BM25 Lexical Reranking"]
    direction TB
    E["Tokenize\ndoc.split()"] --> F["BM25Okapi\n(rank_bm25)"]
    F --> G["BM25 Scores\nkeyword overlap"]
  end

  subgraph P2b["Phase 2b — Cross-Encoder Neural Reranking"]
    direction TB
    H["Sentence Pairs\n query + doc"] --> I["CrossEncoder\nms-marco-MiniLM-L-6-v2"]
    I --> J["Raw Logit Scores\nunbounded float"]
  end

  subgraph P2c["Phase 2c — Cohere Rerank API"]
    direction TB
    K["cohere.Client\nrerank-english-v3.0"] --> L["Relevance Scores\nnormalised 0 to 1"]
  end

  subgraph P3["Phase 3 — Compare and Select"]
    direction TB
    M["BM25 Result\nRank 1: Efficient KE"] --> N["Consensus\nTop Result"]
    O["CrossEncoder Result\nRank 1: Efficient KE"] --> N
    P["Cohere Result\nRank 1: Efficient KE"] --> N
    N --> Q([Pass Top-2 to LLM])
  end

  QQ([User Query]) --> C
  QQ --> E
  QQ --> H
  QQ --> K

  D --> E
  D --> H
  D --> K

  G --> M
  J --> O
  L --> P

  classDef embed   fill:#E6F1FB,stroke:#378ADD,color:#042C53
  classDef bm25    fill:#FFF8E1,stroke:#F9A825,color:#3E2800
  classDef ce      fill:#EDE7F6,stroke:#5E35B1,color:#1A0050
  classDef cohere  fill:#E8F5E9,stroke:#2E7D32,color:#0A2E0C
  classDef compare fill:#FCE4EC,stroke:#C62828,color:#3B0000
  classDef io      fill:#FAEEDA,stroke:#BA7517,color:#412402

  class A,B,C,D embed
  class E,F,G bm25
  class H,I,J ce
  class K,L cohere
  class M,O,P,N,Q compare
  class QQ io
```

---

## Colour Reference

| Phase | Colour | Represents |
|---|---|---|
| Phase 1 — Corpus and Embedding | Blue (`#E6F1FB` / `#378ADD`) | Bi-encoder retrieval and top-4 selection |
| Phase 2a — BM25 Lexical | Amber (`#FFF8E1` / `#F9A825`) | Keyword-based lexical reranking |
| Phase 2b — Cross-Encoder Neural | Purple (`#EDE7F6` / `#5E35B1`) | Neural pairwise reranking |
| Phase 2c — Cohere API | Green (`#E8F5E9` / `#2E7D32`) | API-based normalised reranking |
| Phase 3 — Compare and Select | Red (`#FCE4EC` / `#C62828`) | Consensus selection and LLM input |
| Input / Output nodes | Amber (`#FAEEDA` / `#BA7517`) | User query and final answer to LLM |

---

## Key Design Decisions

- **Single query, four parallel paths** — the user query drives the bi-encoder retrieval AND all three rerankers simultaneously, making the comparison fair (identical input, identical top-4 candidate set)
- **Top-4 gate** — Phase 1 bi-encoder selects the top-4 candidates from 8 documents; all rerankers in Phase 2 operate on this same filtered set, not the full corpus
- **Three independent rerankers in parallel** — BM25 (lexical, keyword tokens), Cross-Encoder (neural, pairwise), and Cohere (API, normalised score) each produce their own ranked output
- **Consensus selection in Phase 3** — rather than trusting any single reranker, the pipeline takes the document that appears at Rank-1 consistently across methods and passes only the top-2 consensus documents to the LLM
- **Score types differ by method** — BM25 gives unbounded positive floats (higher = more keyword overlap); Cross-Encoder gives raw logits (can be negative); Cohere gives normalised 0–1 scores. Do NOT compare absolute numbers across methods — only compare rankings
- **Oval nodes** = external I/O (user query, LLM input); **rectangle nodes** = internal processing steps

---

*Made with love by Mayank Chugh | GitHub: mayankchugh-learning | @itaienthusiast*
