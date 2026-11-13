# Contextual compression

A vector retriever returns whole chunks. A `ContextualCompressionRetriever` sits in front of the LLM and either shortens those chunks or drops them.

**Notebook:** [`ContextualCompression_RAG_Final.ipynb`](ContextualCompression_RAG_Final.ipynb)

The notebook runs the same three questions through a plain FAISS retriever and through four compressors:

| Compressor | What it does |
|------------|----------------|
| `LLMChainExtractor` | Keeps the sentences the LLM judges relevant |
| `LLMChainFilter` | Keeps or drops each document as a whole |
| `EmbeddingsFilter` | Drops chunks under a cosine threshold. The notebook sets the threshold from printed scores; the library default keeps every document. |
| `DocumentCompressorPipeline` | Splits, removes near-duplicates with `EmbeddingsRedundantFilter`, then filters |

| Piece | Choice |
|-------|--------|
| Corpus | 2022 State of the Union address, downloaded by the notebook. The saved write-up uses 95 chunks at 500 characters with 100 overlap. |
| Embeddings | `BAAI/bge-small-en-v1.5` |
| Vector store | FAISS |
| LLM | Local `Qwen/Qwen2.5-3B-Instruct`, then Anthropic, then OpenAI |
| Imports | `langchain_classic.chains` and `langchain_classic.retrievers` (these moved out of the top-level `langchain` package in 1.x) |

**Runtime:** Colab T4 GPU for the local LLM. Without a GPU the notebook uses Anthropic, then OpenAI, when those keys are in Colab Secrets.

The opening cell records one CPU test run (character counts and compression ratios). Treat those figures as that run’s measurements and re-check them after a T4 execution; fp16 similarity scores move slightly.

Series index: [../README.md](../README.md).
