# RAG Fusion

Episode 5. A single user question is a brittle retrieval query. This notebook asks an LLM for several phrasings, retrieves each one, and merges the ranked lists with reciprocal rank fusion (RRF).

**Notebook:** [`RAGFusion.ipynb`](RAGFusion.ipynb)

The formula and the default `k=60` follow Cormack, Clarke, and Büttcher, *Reciprocal Rank Fusion Outperforms Condorcet and Individual Rank Learning Methods*, SIGIR 2009.

| Piece | Choice |
|-------|--------|
| Corpus | Six Singapore travel notes in [`data/`](data/), chunked to 33 passages in the saved run |
| Embeddings | `BAAI/bge-small-en-v1.5` |
| Vector store | Chroma |
| LLM | Local `Qwen3-4B-Instruct-2507` in 4-bit, then Anthropic, then OpenAI, via `with_fallbacks()` |
| Saved run | Executed on a Colab T4 on 7 Sep 2026. The local model answered every call in that run. |

`with_fallbacks()` switches only when a model raises. A weak but successful local answer stays local.

**Runtime:** Colab T4 GPU. `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` are used only if an earlier model errors.

## Notes in `data/`

| File | Topic |
|------|--------|
| `singapore_food.txt` | Hawker food and neighbourhood dishes |
| `singapore_attractions.txt` | Sights |
| `singapore_culture.txt` | Culture notes |
| `singapore_nightlife.txt` | Nightlife |
| `singapore_transport.txt` | Getting around |
| `universal_studios_singapore.txt` | Universal Studios Singapore |

These are tutorial notes written for the episode.

Series index: [../README.md](../README.md). The notebook’s closing note points at FlashRank as the next episode: [`../FlashRank_RAG/`](../FlashRank_RAG/).
