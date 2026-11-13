# Reranking from scratch (2026)

One bi-encoder shortlist, then three rerankers that score it independently, then a guide to the rerankers that showed up after the classic MS MARCO cross-encoder.

**Notebook:** [`Reranking2026_Notebook.ipynb`](Reranking2026_Notebook.ipynb)

| Stage | What runs |
|-------|-----------|
| Dense retrieval | `sentence-transformers/all-MiniLM-L6-v2` (384-dimensional). The notebook also names `BAAI/bge-m3` for multilingual work. |
| Lexical rerank | `BM25Okapi` from `rank_bm25`, then the same idea with `bm25s` |
| Neural rerank | `cross-encoder/ms-marco-MiniLM-L-6-v2` via `CrossEncoder.rank` |
| API rerank | Cohere `cohere.ClientV2()` with `rerank-v3.5` (also documents `rerank-v4.0-pro` and `rerank-v4.0-fast`) |
| 2026 frontier | Notes and optional calls for `jina-reranker-v3`, Qwen3-Reranker, mxbai-rerank, and Voyage. The decision-guide cell at the end is the place to pick among them. |

Compare rank order. BM25 is an unbounded keyword score, the cross-encoder emits logits, and Cohere returns a normalised relevance score.

**Runtime:** CPU is enough for MiniLM, BM25, and the cross-encoder. **Secret:** `COHERE_API_KEY` for the Cohere stage. Jina and any hosted Qwen rerank call need their own credentials; skip those cells if you only want the local comparison.

The corpus is eight short passages inside the notebook, not a separate data file.

## Files in this folder

| File | Role |
|------|------|
| `Reranking2026_Notebook.ipynb` | The tutorial. Run top to bottom. |
| [`Reranking2026_Mermaid_Architecture.md`](Reranking2026_Mermaid_Architecture.md) | Diagram of the shared shortlist and the three comparison rerankers |
| `Reranking2026_Architecture_Diagrams.pdf` | Slide diagrams for the episode |
| `diagram-1782791225632.png`, `diagram-1782791227738.svg` | Exported figures used with the slides |

Series index: [../README.md](../README.md). Episode 6 ([`FlashRank_RAG`](../FlashRank_RAG/)) is the lightweight ONNX version of this second stage.
