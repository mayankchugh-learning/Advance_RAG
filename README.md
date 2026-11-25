# Advance RAG

Hands-on tutorials for retrieval-augmented generation beyond a single vector search: hybrid retrieval, reranking, compression, parent-document retrieval, query rewriting, and long-context ordering.

Each folder is one self-contained notebook from the Advanced RAG series by **Mayank Chugh** ([@itaienthusiast](https://www.youtube.com/@itaienthusiast)), plus a short README for that folder. Open the notebook and run it from top to bottom. The markdown inside the notebook is the lesson; the files next to it (Mermaid diagrams, formula notes, slide PDFs, and sample text) are the references for that lesson. The notebooks are written for a Colab T4. Watch and Open-in-Colab links are in [Notebooks and videos](#notebooks-and-videos).

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
| 7 | [`ParentDocument_RAG`](ParentDocument_RAG/) | `ParentDocument_RAG.ipynb` | Episode 07. Search 300-character child chunks, hand the LLM the parent (the whole document, or 1,200-character chunks), then answer with Qwen3-4B |
| 8 | [`ContextualCompression_RAG`](ContextualCompression_RAG/) | `ContextualCompression_RAG_Final.ipynb` | Four ways to trim retrieved chunks before the LLM: extract, filter, embedding threshold, and a compressor pipeline |
| 9 | [`SelfQuery_RAG`](SelfQuery_RAG/) | `SelfQuery_RAG_Clean.ipynb` | The LLM turns a plain question into a semantic query plus metadata filters on a sample air-cargo log |

## Notebooks and videos

Public watch links for the Advanced RAG notebooks in this repository. Episode order matches the path above.

| Notebook | YouTube | Open in Colab |
|----------|---------|----------------|
| [`RAG_HybridSearch_Final.ipynb`](Hybird_Search_Ensember_Retriver/RAG_HybridSearch_Final.ipynb) | [Hybrid Search RAG Pipeline From Scratch \| Advanced RAG \| LangChain + BM25 + ChromaDB](https://www.youtube.com/watch?v=eNzsuWaOCEI) | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/Hybird_Search_Ensember_Retriver/RAG_HybridSearch_Final.ipynb) |
| [`HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb`](HybridSearch_Weaviate_Cohere_ReRanking/HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb) | [Hybrid Search + Cohere Reranking in RAG \| Weaviate + Qwen3-8B \| Advanced RAG Tutorial](https://www.youtube.com/watch?v=iFT_MniMblk) | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/HybridSearch_Weaviate_Cohere_ReRanking/HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb) |
| [`Reranking2026_Notebook.ipynb`](Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/Reranking2026_Notebook.ipynb) | [Reranking in RAG From Scratch (2026) \| BM25 + CrossEncoder + Cohere + Qwen3 + Jina AI \| Advanced RAG](https://www.youtube.com/watch?v=XVZOQ6Fwz2c) | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/Reranking_From_Scratch%282026%29_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/Reranking2026_Notebook.ipynb) |
| [`MergerRetriever_LongContextReorder.ipynb`](Lost_In_the_Middle_MergerRetriever_LongContextReorder/MergerRetriever_LongContextReorder.ipynb) | [Advanced RAG: Fix “Lost in the Middle” with MergerRetriever & LongContextReorder \| LangChain 2026](https://www.youtube.com/watch?v=w5cHGeLV-ro) | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/Lost_In_the_Middle_MergerRetriever_LongContextReorder/MergerRetriever_LongContextReorder.ipynb) |
| [`RAGFusion.ipynb`](RAGFusion/RAGFusion.ipynb) | [RAG Fusion Explained: Reciprocal Rank Fusion (RRF) With Real Code](https://www.youtube.com/watch?v=BwgBU0CekFk) | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/RAGFusion/RAGFusion.ipynb) |
| [`FlashRank_RAG_Clean_run.ipynb`](FlashRank_RAG/FlashRank_RAG_Clean_run.ipynb) | [FlashRank Reranking for RAG: 11ms on CPU, No GPU \| Advanced RAG Ep 6](https://www.youtube.com/watch?v=31Qwp8xvY_s) | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/FlashRank_RAG/FlashRank_RAG_Clean_run.ipynb) |
| [`ParentDocument_RAG.ipynb`](ParentDocument_RAG/ParentDocument_RAG.ipynb) | — | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/ParentDocument_RAG/ParentDocument_RAG.ipynb) |
| [`ContextualCompression_RAG_Final.ipynb`](ContextualCompression_RAG/ContextualCompression_RAG_Final.ipynb) | [My RAG Compressor Deleted the Answer \| LangChain Contextual Compression (Ep 6)](https://www.youtube.com/watch?v=Emvui2Haykc) | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/ContextualCompression_RAG/ContextualCompression_RAG_Final.ipynb) |
| [`SelfQuery_RAG_Clean.ipynb`](SelfQuery_RAG/SelfQuery_RAG_Clean.ipynb) | [Self-Query Retrieval in LangChain \| LLM Metadata Filters (Ep 6)](https://www.youtube.com/watch?v=Diw3eKOLEzg) | [Colab](https://colab.research.google.com/github/mayankchugh-learning/Advance_RAG/blob/main/SelfQuery_RAG/SelfQuery_RAG_Clean.ipynb) |

`ParentDocument_RAG.ipynb` is Episode 07 in this repo. None of the titles in the channel export match that notebook, so that row has no video yet.

YouTube titles call the FlashRank, contextual compression, and self-query videos “Ep 6”. In the notebooks, only FlashRank is headed Episode 6. Contextual compression and self-query do not use an episode number. Where a video title and a notebook heading disagree, follow the notebook.

The Open in Colab badge inside `RAGFusion.ipynb` still points at `Generative-AI-Indepth-Basic-to-Advance`. Use the Colab link in this table, which opens the copy in this repository.

## What you need

| Notebook | Runtime | Secrets and data |
|----------|---------|------------------|
| Hybrid search ensemble | Colab T4 GPU for Zephyr 7B | No API key. The loader expects `/content/NeurIPS-2020-retrieval-augmented-generation-for-knowledge-intensive-nlp-tasks-Paper.pdf`. The same Lewis et al. paper is in the Weaviate folder under a different name, `Retrieval-Augmented-Generation-for-NLP.pdf`. Slide deck: [`HybridSearch_Advance_RAG.pdf`](Hybird_Search_Ensember_Retriver/HybridSearch_Advance_RAG.pdf). Formula notes are in the folder. |
| Weaviate + Cohere | Colab T4 GPU | Colab Secrets: `WEAVIATE_URL`, `WEAVIATE_API_KEY`, `HF_TOKEN_READ`, `COHERE_API_KEY`. Upload [`Retrieval-Augmented-Generation-for-NLP.pdf`](HybridSearch_Weaviate_Cohere_ReRanking/Retrieval-Augmented-Generation-for-NLP.pdf) to `/content/` before the indexing cells. |
| Reranking from scratch | CPU is enough for MiniLM, BM25, and the cross-encoder | `COHERE_API_KEY` for the Cohere stage (Colab Secrets, or the environment variable of the same name outside Colab). The Jina and Voyage snippets are comments: a bearer token written as `JINA_KEY`, and `VOYAGE_API_KEY` for `voyageai.Client()`. Qwen3-Reranker is a local vLLM note. Eight short passages live in the notebook. |
| Lost in the middle | Colab T4 GPU recommended | [`alice-in-wonderland.pdf`](Lost_In_the_Middle_MergerRetriever_LongContextReorder/alice-in-wonderland.pdf) (public domain) and the Liu et al. paper [`2307.03172v3.pdf`](Lost_In_the_Middle_MergerRetriever_LongContextReorder/2307.03172v3.pdf) are in the folder. `OPENAI_API_KEY` for `gpt-4o-mini`. The same section can load local Qwen2.5-7B. Set `ALICE_PDF` to point the loader at another file. |
| RAG Fusion | Colab T4 GPU | Six notes in [`RAGFusion/data`](RAGFusion/data/). Local Qwen3-4B runs first. `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` are used only if an earlier model errors. |
| FlashRank | Colab T4 GPU for the local LLM only | FlashRank, embeddings, and FAISS run on CPU. The notebook downloads the 2022 State of the Union text. `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` are used only if local Qwen3-4B errors. |
| Parent document | Colab T4 GPU for Qwen3-4B | Four sample maintenance and cargo documents are written by the notebook. Embeddings use the GPU when the runtime has one. `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` if you generate without a GPU. `HF_TOKEN` is optional. |
| Contextual compression | Colab T4 GPU for the local LLM | Same speech file, downloaded by the notebook. Local Qwen2.5-3B runs first. `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` when there is no GPU. |
| Self-query | Colab T4 GPU recommended | Twelve sample shipments are written in the notebook. Local Qwen2.5-3B on a T4. `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` when the local model is unavailable. |

Each notebook installs its own packages in its setup cells. The stacks differ (LangChain 1.x import paths, Weaviate v4, Cohere v5, local 4-bit LLMs), so this repository does not ship one shared `requirements.txt`.

Notebooks read keys from Colab Secrets with `userdata.get()`. Outside Colab, set those same names in the environment before the cells that need them. The notebooks do not load a `.env` file on their own. `.gitignore` excludes `.env`, `.ipynb_checkpoints`, and local vector-store folders.

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
| [`Hybird_Search_Ensember_Retriver/HybridSearch_Advance_RAG.pdf`](Hybird_Search_Ensember_Retriver/HybridSearch_Advance_RAG.pdf) | Nine-page slide deck for the ensemble notebook |
| [`Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/Reranking2026_Architecture_Diagrams.pdf`](Reranking_From_Scratch(2026)_BM25_Cross-Encoder_Cohere_Qwen3_Jina_AI_Advanced_RAG/Reranking2026_Architecture_Diagrams.pdf) | Slide diagrams for the reranking notebook. The folder also has the exported `.png` and `.svg` |
| [`Lost_In_the_Middle_MergerRetriever_LongContextReorder/2307.03172v3.pdf`](Lost_In_the_Middle_MergerRetriever_LongContextReorder/2307.03172v3.pdf) | Liu et al. 2023, the lost-in-the-middle paper the notebook cites |
| Folder `README.md` in each directory | Stack, secrets, corpus, and saved-run notes for that notebook |

Paste any Mermaid block into [mermaid.live](https://mermaid.live) if GitHub’s preview is not enough. When a diagram and a notebook disagree, follow the notebook: the notebooks were re-run after some of these diagrams were first drawn.

## Layout

```
Advance_RAG/
├── Hybird_Search_Ensember_Retriver/          # notebook, Mermaid, TF-IDF notes, slide PDF
├── HybridSearch_Weaviate_Cohere_ReRanking/   # notebook, Mermaid, Lewis et al. PDF
├── Reranking_From_Scratch(2026)_.../         # notebook, Mermaid, slide PDF
├── Lost_In_the_Middle_MergerRetriever_LongContextReorder/  # Alice PDF, arXiv:2307.03172 PDF
├── RAGFusion/                                # notebook; data/*.txt (six Singapore notes)
├── FlashRank_RAG/
├── ParentDocument_RAG/                      # child search, parent context, Qwen3-4B
├── ContextualCompression_RAG/
└── SelfQuery_RAG/
```

## Author

**Mayank Chugh** — IT AI Enthusiast · [GitHub](https://github.com/mayankchugh-learning) · [YouTube @itaienthusiast](https://www.youtube.com/@itaienthusiast) · [Medium](https://medium.com/@mayankchugh.jobathk) · [mayankchugh-learning.github.io](https://mayankchugh-learning.github.io)

## License

MIT. See [LICENSE](LICENSE). Sample corpora are separate: the Alice PDF is a public-domain text, the Lewis et al. and Liu et al. PDFs are the papers those notebooks study, and the Singapore notes, air-cargo rows, and aircraft-maintenance documents are tutorial data written for this series.
