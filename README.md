# Advance RAG

Hands-on tutorials for retrieval-augmented generation beyond a single vector search: hybrid retrieval, reranking, compression, query rewriting, and long-context ordering.

Each folder is one self-contained notebook from the Advanced RAG series by **Mayank Chugh** ([@itaienthusiast](https://www.youtube.com/@itaienthusiast)). Open the notebook and run it from top to bottom. The markdown inside the notebook is the lesson; the files next to it (Mermaid diagrams, formula notes, slide PDFs, and sample text) are the references for that lesson.

Episode numbers follow each notebook’s own title. Directory names are the published paths, including `Hybird_Search_Ensember_Retriver`.

## Suggested path

| | Folder | Notebook | What you build |
|---|--------|----------|----------------|
| 1 | [`Hybird_Search_Ensember_Retriver`](Hybird_Search_Ensember_Retriver/) | `RAG_HybridSearch_Final.ipynb` | TF-IDF from scratch, dense search in Chroma, a BM25 + vector ensemble, then answers from Zephyr 7B (4-bit) |
| 2 | [`HybridSearch_Weaviate_Cohere_ReRanking`](HybridSearch_Weaviate_Cohere_ReRanking/) | `HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb` | Episode 02. Weaviate hybrid search (`alpha`), Cohere `rerank-v3.5`, answers from Qwen3-8B |
| 3 | [`Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG`](Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/) | `Reranking2026_Notebook.ipynb` | Same shortlist scored by BM25, a cross-encoder, and Cohere, then a 2026 model guide (Jina, Qwen3-Reranker, mxbai, Voyage) |
| 4 | [`Lost_In_the_Middle_MergerRetriever_LongContextReorder`](Lost_In_the_Middle_MergerRetriever_LongContextReorder/) | `MergerRetriever_LongContextReorder.ipynb` | Video 04. Merge two retrievers and reorder chunks so the best evidence sits at the start and end of the prompt |
| 5 | [`RAGFusion`](RAGFusion/) | `RAGFusion.ipynb` | Episode 5. Several phrasings of one question, fused with reciprocal rank fusion over Singapore travel notes |
| 6 | [`FlashRank_RAG`](FlashRank_RAG/) | `FlashRank_RAG_Clean_run.ipynb` | Episode 6. CPU ONNX rerankers (Nano through Large) on their own, then inside a FAISS RAG chain |
| 7 | [`ContextualCompression_RAG`](ContextualCompression_RAG/) | `ContextualCompression_RAG_Final.ipynb` | Four ways to trim retrieved chunks before the LLM: extract, filter, embedding threshold, and a compressor pipeline |
| 8 | [`SelfQuery_RAG`](SelfQuery_RAG/) | `SelfQuery_RAG_Clean.ipynb` | The LLM turns a plain question into a semantic query plus metadata filters on a sample air-cargo log |

## What you need

| Notebook | Runtime | Secrets and data |
|----------|---------|------------------|
| Hybrid search ensemble | Colab T4 GPU for Zephyr 7B | Upload the NeurIPS 2020 RAG paper PDF in Colab. Slide deck and formula notes are already in the folder. |
| Weaviate + Cohere | Colab T4 GPU | Colab Secrets: `WEAVIATE_URL`, `WEAVIATE_API_KEY`, `HF_TOKEN_READ`, `COHERE_API_KEY`. Corpus PDF is in the folder: `Retrieval-Augmented-Generation-for-NLP.pdf`. |
| Reranking from scratch | CPU is enough for MiniLM, BM25, and the cross-encoder | `COHERE_API_KEY` for the Cohere stage. Jina and hosted Qwen calls need their own keys; those cells are optional. Eight short passages live in the notebook. |
| Lost in the middle | Colab T4 GPU recommended | `alice-in-wonderland.pdf` is in the folder (public-domain text). `OPENAI_API_KEY` if you use `gpt-4o-mini`; the notebook can also load a local Qwen model. |
| RAG Fusion | Colab T4 GPU | Six notes in [`RAGFusion/data`](RAGFusion/data/). Local Qwen3-4B runs first. `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` are fallbacks. |
| FlashRank | Colab T4 GPU for the local LLM only | FlashRank, embeddings, and FAISS run on CPU. The notebook downloads the 2022 State of the Union text. Paid keys are fallbacks. |
| Contextual compression | Colab T4 GPU for the local LLM | Same speech file, downloaded by the notebook. Paid keys are fallbacks. |
| Self-query | Colab T4 GPU recommended | Twelve sample shipments are written in the notebook. Paid keys are fallbacks if the local model is unavailable. |

Each notebook installs its own packages in its setup cells. The stacks differ (LangChain 1.x import paths, Weaviate v4, Cohere v5, local 4-bit LLMs), so this repository does not ship one shared `requirements.txt`.

Keep API keys in Colab Secrets or a local `.env`. `.gitignore` already excludes `.env`, `.ipynb_checkpoints`, and local vector-store folders.

### Local Jupyter

```bash
git clone https://github.com/mayankchugh-learning/Advance_RAG.git
cd Advance_RAG
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate

pip install jupyter
jupyter notebook
```

Install the packages listed in the notebook you open, then run the cells in order. GPU notebooks that load Qwen or Zephyr are written for a Colab T4.

## Reference docs in the repo

| Doc | Use it for |
|-----|------------|
| [`Hybird_Search_Ensember_Retriver/RAG_Architecture_Mermaid.md`](Hybird_Search_Ensember_Retriver/RAG_Architecture_Mermaid.md) | Chalk-style index → retrieve → generate diagram, and how the ensemble notebook maps onto it |
| [`Hybird_Search_Ensember_Retriver/TFIDF_Formula_Reference.md`](Hybird_Search_Ensember_Retriver/TFIDF_Formula_Reference.md) | TF, IDF, and TF-IDF formulas plus a short Python sketch |
| [`HybridSearch_Weaviate_Cohere_ReRanking/HybridSearch_Weaviate_Cohere_Architecture_Mermaid.md`](HybridSearch_Weaviate_Cohere_ReRanking/HybridSearch_Weaviate_Cohere_Architecture_Mermaid.md) | Episode 02 phases: Weaviate index, hybrid retrieval, Cohere rerank, Qwen3-8B |
| [`Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/Reranking2026_Mermaid_Architecture.md`](Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/Reranking2026_Mermaid_Architecture.md) | Side-by-side BM25, cross-encoder, and Cohere on one bi-encoder shortlist |

Paste any Mermaid block into [mermaid.live](https://mermaid.live) if GitHub’s preview is not enough. When a diagram and a notebook disagree, follow the notebook: the notebooks were re-run after some of these diagrams were first drawn.

## Layout

```
Advance_RAG/
├── Hybird_Search_Ensember_Retriver/          # TF-IDF, BM25, Chroma ensemble, Zephyr
├── HybridSearch_Weaviate_Cohere_ReRanking/   # Weaviate hybrid search + Cohere + Qwen3
├── Reranking_From_Scratch(2026)_.../         # BM25, cross-encoder, Cohere, 2026 rerankers
├── Lost_In_the_Middle_MergerRetriever_LongContextReorder/
├── RAGFusion/                                # multi-query RRF; data/*.txt
├── FlashRank_RAG/
├── ContextualCompression_RAG/
└── SelfQuery_RAG/
```

## Author

**Mayank Chugh** — IT AI Enthusiast · [GitHub](https://github.com/mayankchugh-learning) · [YouTube @itaienthusiast](https://www.youtube.com/@itaienthusiast)

## License

MIT. See [LICENSE](LICENSE). Sample corpora are separate: the Alice PDF is a public-domain text, the Lewis et al. and Liu et al. PDFs are the papers those notebooks study, and the Singapore notes and air-cargo rows are tutorial data written for this series.
