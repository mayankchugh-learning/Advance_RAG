# Self-query retrieval

Similarity search cannot express “over 1,000 kg” or “into Hong Kong” as hard filters. A self-query retriever asks an LLM to split the question into a semantic search string and a structured metadata filter.

**Notebook:** [`SelfQuery_RAG_Clean.ipynb`](SelfQuery_RAG_Clean.ipynb)

The corpus is 12 sample air-cargo shipments through Hong Kong, written inside the notebook. Identifiers, weights, and delays are illustrative sample data for this episode.

Filter fields the retriever is shown: origin, destination, commodity, weight, delay, temperature control, and priority.

| Piece | Choice |
|-------|--------|
| Baseline | Ordinary similarity search, so you can see what metadata filters add |
| Vector store | Chroma, in memory |
| Embeddings | `sentence-transformers/all-MiniLM-L6-v2`, local |
| LLM | Local `Qwen2.5-3B-Instruct` on a T4, then Anthropic, then OpenAI, temperature 0 |
| Framework | LangChain 1.x (`langchain_classic`, `langchain_core`, `langchain_community`) |

Part D is titled “Three silent failures” and runs three questions: live animals from Sydney, on-time arrivals, and every pharma shipment. Compare the printed shipment IDs with the sample rows in the notebook before trusting a generated filter.

**Runtime:** Colab T4 GPU recommended. On CPU, put an Anthropic or OpenAI key in Colab Secrets. The notebook reads secrets with `userdata.get()`.

Series index: [../README.md](../README.md).
