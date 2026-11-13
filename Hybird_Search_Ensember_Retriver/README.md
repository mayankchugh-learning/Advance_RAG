# Hybrid search and ensemble retrieval

Keyword search and vector search answer different failures. This notebook builds both, then mixes them with LangChain’s ensemble retriever before a local LLM writes the answer.

**Notebook:** [`RAG_HybridSearch_Final.ipynb`](RAG_HybridSearch_Final.ipynb)

| Section | What it covers |
|---------|----------------|
| TF-IDF from scratch | Term frequency, inverse document frequency, and cosine ranking on a four-document toy corpus |
| Dense search | `BAAI/bge-base-en-v1.5` embeddings in Chroma |
| Ensemble | BM25 (`rank_bm25`) plus the vector retriever, with an alpha weight between them |
| Generation | Zephyr 7B loaded in 4-bit, then a naive-vs-hybrid comparison on the NeurIPS 2020 RAG paper |

**Runtime:** Google Colab with a T4 GPU (the quantized LLM). The notebook installs `langchain`, `chromadb`, `rank_bm25`, `sentence-transformers`, and `bitsandbytes` itself.

**Corpus:** upload `NeurIPS-2020-retrieval-augmented-generation-for-knowledge-intensive-nlp-tasks-Paper.pdf` to `/content/` in Colab, as the notebook’s loader cell expects. A copy of that paper is also stored next door as [`../HybridSearch_Weaviate_Cohere_ReRanking/Retrieval-Augmented-Generation-for-NLP.pdf`](../HybridSearch_Weaviate_Cohere_ReRanking/Retrieval-Augmented-Generation-for-NLP.pdf).

## Files in this folder

| File | Role |
|------|------|
| `RAG_HybridSearch_Final.ipynb` | The tutorial. Run top to bottom. |
| [`RAG_Architecture_Mermaid.md`](RAG_Architecture_Mermaid.md) | Index → embed → retrieve → generate diagram, plus how the ensemble step sits on that diagram |
| [`TFIDF_Formula_Reference.md`](TFIDF_Formula_Reference.md) | TF, IDF, and TF-IDF formulas and a short Python implementation |
| `HybridSearch_Advance_RAG.pdf` | Nine-page slide deck for this episode |

Series index: [../README.md](../README.md). The next notebook in the series puts the same idea on Weaviate and adds Cohere reranking.
