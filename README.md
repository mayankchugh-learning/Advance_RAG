# Advance RAG

Advanced Retrieval-Augmented Generation (RAG) experiments and reference materials, with a focus on **hybrid search** and **ensemble retrievers**.

## Contents

| Path | Description |
|------|-------------|
| [`Hybird_Search_Ensember_Retriver/`](Hybird_Search_Ensember_Retriver/) | Hybrid search & ensemble retriever notebooks and docs |
| `RAG_HybridSearch_Final_Notebook-final.ipynb` | End-to-end hybrid search RAG notebook |
| `RAG_Architecture_Mermaid.md` | RAG pipeline architecture diagram (Mermaid) |
| `TFIDF_Formula_Reference.md` | TF-IDF formula reference for sparse retrieval |

## Hybrid Search Overview

Hybrid RAG combines multiple retrieval strategies—typically **dense** (embedding / vector) search and **sparse** (TF-IDF / BM25) search—then fuses or re-ranks results for better recall and precision.

```
Documents → Chunking → Embedding + TF-IDF → Vector DB + Sparse Index
                                                              ↓
User Query → Embedding + TF-IDF → Similarity Search → Ranked Results → LLM → Answer
```

See [`RAG_Architecture_Mermaid.md`](Hybird_Search_Ensember_Retriver/RAG_Architecture_Mermaid.md) for the full pipeline diagram.

## Getting Started

### Prerequisites

- Python 3.10+
- [Jupyter Notebook](https://jupyter.org/) or [JupyterLab](https://jupyterlab.readthedocs.io/)

### Setup

```bash
git clone https://github.com/mayankchugh-learning/Advance_RAG.git
cd Advance_RAG
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate

pip install -r requirements.txt   # when available
jupyter notebook
```

Open `Hybird_Search_Ensember_Retriver/RAG_HybridSearch_Final_Notebook-final.ipynb` to run the hybrid search workflow.

## Author

**Mayank Chugh** — IT AI Enthusiast · [@itaienthusiast](https://github.com/mayankchugh-learning)

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
