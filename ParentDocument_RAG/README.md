# Parent document retriever

Episode 07. Vector search matches small child chunks. The larger parent those chunks came from is what the LLM reads.

**Notebook:** [`ParentDocument_RAG.ipynb`](ParentDocument_RAG.ipynb)

The corpus is four sample aircraft-maintenance and air-cargo documents, written by the notebook into `mro_dataset.py` when you run it. Document numbers, part numbers, torque values, and limits are illustrative. Do not use them for real maintenance or cargo work.

| Piece | Choice |
|-------|--------|
| Embeddings | `BAAI/bge-small-en-v1.5`, 384-dimensional, normalised |
| Child store | Chroma, in memory, one collection per retriever |
| Parent store | `InMemoryStore` |
| Splitters | Child chunks of 300 characters with overlap 30. Parent chunks of 1,200 characters with overlap 0. Mode 1 leaves out the parent splitter, so each parent is the whole document. Mode 2 sets `id_key="parent_id"` so the retriever does not overwrite your `doc_id`. |
| Retriever | `ParentDocumentRetriever` from `langchain_classic`, `k=4` |
| Guard | `similarity_score_threshold` of 0.5 |
| LLM | Local `Qwen/Qwen3-4B-Instruct-2507` in NF4 4-bit, then `claude-sonnet-5`, then `gpt-5.6-sol`, via `with_fallbacks()` |
| Framework | LangChain 1.x (`langchain-classic` for the retriever) |

The seeded failure is an aft cargo-door manual whose hinge-bolt sentence and its **38 Nm** value sit in different paragraphs, next to a near-duplicate forward-door manual that says **42 Nm**. One question (main-landing-gear tyre pressure) has no answer in the corpus.

Saved run recorded 7 November 2026. The notebook outputs show `device: cuda`, real `bge-small` embeddings (size 384), and a completed load of local Qwen3-4B, with Claude and OpenAI loaded behind it as fallbacks. The answer text below is what those cells printed.

| Check | Result |
|-------|--------|
| Split | 38 child chunks (avg 172 characters) and 7 parent chunks (avg 924 characters) |
| Small-chunk baseline, k=1 | Returns `SAMPLE-AMM-52-32` (42 Nm), the forward manual |
| Split parents | k=1 and k=2 miss the 38 Nm parent. k=4 returns it, last of the four parents |
| Relevance | 0.738 on the aft-torque question, 0.42 on the tyre-pressure question. Threshold 0.5 returns 4 parents for the first and 0 for the second |
| Titled children | The forward manual is still the nearest child (distance 0.2904). The parent that contains 38 Nm is second among the parents returned |
| Context length | 375 characters for one child, 2,979 characters for the titled parents |
| Child-chain answer | 42 Nm (31 lbf-ft), cited `SAMPLE-AMM-52-32` |
| Parent-chain answer | 38 Nm (28 lbf-ft), cited `SAMPLE-AMM-52-31` |
| Tyre-pressure question | `Not found in the provided documents.` |

**Runtime:** Colab T4 GPU so the local Qwen model can load. Embeddings use the GPU when the runtime has one. Without a GPU, put `ANTHROPIC_API_KEY` or `OPENAI_API_KEY` in Colab Secrets. `HF_TOKEN` is optional. The notebook reads secrets with `userdata.get()`.

**Secrets:** `ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, `HF_TOKEN`.

Series index: [../README.md](../README.md).
