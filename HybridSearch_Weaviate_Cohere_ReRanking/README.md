# Hybrid search on Weaviate, then Cohere reranking

Episode 02 of the Advanced RAG series. A PDF is indexed in Weaviate Cloud, retrieved with hybrid search (BM25 and vectors together), rescored with Cohere, and answered by a quantised local LLM.

**Notebook:** [`HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb`](HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb)

June 2026 stack, as executed in the notebook:

| Piece | Choice |
|-------|--------|
| Vector database | Weaviate Cloud, v4 client, collection `RAG` |
| Embeddings | `BAAI/bge-base-en-v1.5` through `text2vec-huggingface` |
| Retriever | Custom `WeaviateV4HybridRetriever`, `alpha=0.5` (0 is BM25 only, 1 is vector only) |
| Reranker | `CohereRerank` with `model='rerank-v3.5'`, wrapped in `ContextualCompressionRetriever` |
| LLM | `Qwen/Qwen3-8B`, NF4 4-bit, on a T4 GPU |
| Corpus | [`Retrieval-Augmented-Generation-for-NLP.pdf`](Retrieval-Augmented-Generation-for-NLP.pdf) (Lewis et al., NeurIPS 2020). The notebook loads it from `/content/` in Colab, so upload this file there before the indexing cells. |

**Colab Secrets:** `WEAVIATE_URL`, `WEAVIATE_API_KEY`, `HF_TOKEN_READ`, `COHERE_API_KEY`. The notebook reads them with `userdata.get()` and does not expect keys pasted into cells.

**Runtime:** Google Colab, T4 GPU.

The notebook’s saved run for *“What is Abstractive Question Answering?”* reranks three chunks at **0.6641**, **0.3853**, and **0.0860**. Those numbers are relevance scores from that run, not probabilities.

## Files in this folder

| File | Role |
|------|------|
| `HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb` | The tutorial. Run top to bottom. |
| [`HybridSearch_Weaviate_Cohere_Architecture_Mermaid.md`](HybridSearch_Weaviate_Cohere_Architecture_Mermaid.md) | Three-phase diagram: setup, hybrid retrieval, rerank and generate |

Series index: [../README.md](../README.md).
