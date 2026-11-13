# FlashRank reranking

Episode 6. A fast first-stage search returns a shortlist; FlashRank rescores it on CPU with ONNX Runtime, with no GPU required for the reranker itself.

**Notebook:** [`FlashRank_RAG_Clean_run.ipynb`](FlashRank_RAG_Clean_run.ipynb)

Part 1 times four FlashRank models on a fixed set of passages. Part 2 drops `FlashrankRerank` into a LangChain pipeline: FAISS retrieval, compression retriever, then an LLM.

| Option | Model | Size on disk in the notebook’s reference run |
|--------|--------|-----------------------------------------------|
| Nano | `ms-marco-TinyBERT-L-2-v2` | 4.5 MB. FlashRank’s default in the library README. |
| Small | `ms-marco-MiniLM-L-12-v2` | 34.0 MB. The English cross-encoder to pin for this corpus. |
| Medium | `rank-T5-flan` | 110.7 MB |
| Large | `ms-marco-MultiBERT-L-12` | 168.2 MB. Multilingual. `FlashrankRerank()` with no arguments loads this model; the notebook’s takeaway is to pin an English model instead. |

| Piece | Choice |
|-------|--------|
| Embeddings | `BAAI/bge-small-en-v1.5`, CPU, normalised |
| Vector store | FAISS (`faiss-cpu`), in memory |
| Corpus | 2022 State of the Union address, downloaded by the notebook (`state_of_the_union.txt`, 96 chunks at 500 characters with 100 overlap in the reference run) |
| LLM | Local `Qwen/Qwen3-4B-Instruct-2507` (4-bit) → Anthropic → OpenAI |

**Runtime:** Colab T4 so the local LLM can load. Embeddings, FAISS, and FlashRank stay on CPU.

Scores are not comparable across the four ONNX models, so a `score_threshold` has to be chosen per model. The reference numbers printed in the notebook’s opening cell (15 Sep 2026, CPU sandbox) are the ones to compare against your own run; Colab timings will differ.

Series index: [../README.md](../README.md). The from-scratch comparison of BM25, a cross-encoder, and Cohere is in [`../Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/`](../Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/).
