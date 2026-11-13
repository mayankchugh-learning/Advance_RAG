# MergerRetriever and LongContextReorder

Video 04. Language models use the start and end of a long prompt more reliably than the middle (Liu et al., 2023, arXiv:2307.03172). This notebook retrieves from two collections, merges the lists, and reorders the chunks so the strongest evidence is placed at both ends.

**Notebook:** [`MergerRetriever_LongContextReorder.ipynb`](MergerRetriever_LongContextReorder.ipynb)

| Piece | Choice |
|-------|--------|
| Corpus | [`alice-in-wonderland.pdf`](alice-in-wonderland.pdf) — *Alice’s Adventures in Wonderland* (Lewis Carroll, 1865, public domain), split into two thematic Chroma collections |
| Embeddings | `BAAI/bge-m3` |
| Retrieval | One MMR retriever per collection, combined with `MergerRetriever` |
| Ordering | `LongContextReorder` after a dedupe step |
| LLM | `gpt-4o-mini`, or a local Qwen2.5-7B path in the same section |
| Paper | [`2307.03172v3.pdf`](2307.03172v3.pdf) is included so you can read the U-shaped accuracy result next to the code |

**Runtime:** Google Colab with a T4 GPU is the recommended runtime. Set `OPENAI_API_KEY` in Colab Secrets when you take the `gpt-4o-mini` path. To point the loader at another PDF, set the `ALICE_PDF` environment variable to that file’s path before the load cell; the notebook shows the one-line example.

Series index: [../README.md](../README.md).
