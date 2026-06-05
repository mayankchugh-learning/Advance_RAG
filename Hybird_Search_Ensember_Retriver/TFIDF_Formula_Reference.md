# TF-IDF Formula Reference
### by Mayank Chugh | IT AI Enthusiast | @itaienthusiast

---

## Term Frequency (TF)

$$
TF(t, \text{text}) = \frac{\text{Number of times term } t \text{ appears in text}}{\text{Total number of terms in the text}}
$$

---

## Inverse Document Frequency (IDF)

$$
IDF(t, \text{corpus}) = \log \left( \frac{\text{Total number of texts in corpus}}{\text{Number of texts containing term } t} \right)
$$

---

## TF-IDF

$$
\text{TF-IDF}(t, \text{text, corpus}) = TF(t, \text{text}) \times IDF(t, \text{corpus})
$$

---

## Plain Text Version (for code comments / notebooks)

```
TF(t, text)  =  count(t in text) / total_terms_in_text

IDF(t, corpus)  =  log( total_docs_in_corpus / docs_containing_t )

TF-IDF(t, text, corpus)  =  TF(t, text) × IDF(t, corpus)
```

---

## Python Implementation

```python
import math
from collections import Counter

def tf(term, document):
    """Term Frequency: how often term appears in this document."""
    words = document.lower().split()
    return words.count(term.lower()) / len(words)

def idf(term, corpus):
    """Inverse Document Frequency: how rare the term is across all docs."""
    docs_containing = sum(1 for doc in corpus if term.lower() in doc.lower())
    return math.log(len(corpus) / (docs_containing + 1))  # +1 avoids division by zero

def tfidf(term, document, corpus):
    """TF-IDF: combines term frequency with corpus-wide rarity."""
    return tf(term, document) * idf(term, corpus)

# ── Example ──────────────────────────────────────────────────────────────────
corpus = [
    "Keywords are important for keyword-based search.",
    "Document analysis involves extracting keywords.",
    "Keyword-based search relies on sparse embeddings.",
    "This document contains sample text only."
]

term = "keyword"
for i, doc in enumerate(corpus):
    score = tfidf(term, doc, corpus)
    print(f"Doc {i}: TF-IDF('{term}') = {score:.4f}  |  {doc[:50]}")
```

---

## Intuition Table

| Scenario | TF | IDF | TF-IDF | Meaning |
|----------|----|-----|--------|---------|
| Term appears often, rare in corpus | High | High | **Very High** | Strong signal — key term |
| Term appears often, common in corpus | High | Low | Low | Stop word (e.g. "the") |
| Term appears rarely, rare in corpus | Low | High | Medium | Specific but not prominent |
| Term appears rarely, common in corpus | Low | Low | **Very Low** | Noise |

---

## Key Insight

> A word that appears **frequently in one document** but **rarely across the corpus**
> gets the highest TF-IDF score — it is the most *distinctive* word for that document.
>
> This is why "keyword" scores high against our sample corpus but "the" scores near zero.

---

*Made with ❤️ by Mayank Chugh | Like, Share & Subscribe on YouTube @itaienthusiast*
