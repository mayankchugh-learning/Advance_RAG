---
name: notebook-self-learning-docs
description: >-
  Updates Jupyter notebook markdown and code comments for self-learning tutorials
  without changing executable code or saved outputs. Verifies metrics in markdown
  against cell outputs. Use when the user asks to improve notebook docs, comments,
  or teaching notes in .ipynb files, or to make a notebook understandable for AI
  students in this workspace.
---

# Notebook Self-Learning Documentation

## Hard constraints (never violate)

1. **Do not change executable code** — same imports, logic, variable names, function bodies, and shell commands.
2. **Do not change cell outputs** — preserve `outputs`, `execution_count`, and `metadata` on code cells.
3. **Comments only on code cells** — add, update, or remove `#` comments; never alter non-comment lines.
4. **Markdown is free to edit** — add, update, delete, or insert markdown cells.

If the user asks to fix broken code or re-run cells, that is a separate task — confirm before crossing this boundary.

## When to apply

- User mentions: notebook docs, markdown, comments, self-learning, tutorial, teaching, explain for students.
- Any `.ipynb` in this repo (RAG, hybrid search, reranking, Colab tutorials, etc.).

Reference implementation: `HybridSearch_Weaviate_Cohere_ReRanking/HybridSearch_Weaviate_Cohere_15Jun26_FINAL.ipynb`.

## Workflow

### 1. Inventory the notebook

```bash
python -c "
import json, sys
sys.stdout.reconfigure(encoding='utf-8')
nb = json.load(open(sys.argv[1], encoding='utf-8'))
for i, c in enumerate(nb['cells']):
    src = ''.join(c.get('source', []))
    out = bool(c.get('outputs'))
    print(f'{i:2} {c[\"cell_type\"]:8} out={out} len={len(src)}')
" path/to/notebook.ipynb
```

Extract **all cells with outputs** — these are the source of truth for metrics, scores, counts, and example results cited in markdown.

### 2. Verify before writing

Before stating numbers in markdown (rerank scores, page counts, retrieval counts, model names from execution):

| Check | Source |
|-------|--------|
| Scores / metrics | Saved `outputs` on the cell that prints them |
| Document counts | Output of load/index cells |
| Expected strings | Actual printed output, not comments or stale intro text |

**Fix stale markdown** when intro/summary scores disagree with saved outputs (common after re-runs).

### 3. Restructure for self-learning

Each major code section should have a **markdown cell above it** that explains *why* before *how*.

**Intro cell (first markdown after Colab badge):**

- Who the notebook is for
- What pipeline they will build (numbered steps)
- Prerequisites (runtime, secrets, data files, prior concepts)
- How to run (top-to-bottom)
- Table of contents mapping section → learning goal

**Per-section markdown:**

- Section title and number
- Concept explanation in plain language
- Tables for models, APIs, parameters (alpha, top_k, etc.)
- Warnings for breaking API changes
- “What to expect” when running the next code cell

**Closing cells:**

- Self-check takeaways (numbered lessons tied to live results)
- Pipeline summary table (component | class | model | role)
- Optional “next episode” pointer

### 4. Code comments

Add short `#` comments that help a solo learner:

- Why this cell exists (not what each line does if obvious)
- Breaking changes (e.g. Weaviate v3 → v4)
- Expected output in one line (`# Expected: 4 documents`)
- Saved execution values when helpful (`# Saved scores: 0.6641, 0.3853, 0.0860`)

Do **not** over-comment every line.

### 5. Cleanup

- Remove empty trailing code cells
- Insert markdown before orphan code blocks (install, credentials, preview cells)
- Fix broken HTML in markdown (unclosed tags)
- Consolidate duplicate credential cells with a markdown note (“step-by-step for learning; use consolidated cell when re-running”) — do not delete working code cells unless user asks

### 6. Validate

After edits:

- [ ] No executable line changed (diff code cells comment-only)
- [ ] All output-bearing cells still have identical `outputs`
- [ ] Markdown metrics match saved outputs
- [ ] Every major section has explanatory markdown above it
- [ ] JSON is valid (`python -m json.tool notebook.ipynb`)

## Markdown style (this repo)

- Clear headings: `# Section N — Title`
- Tables for comparisons (old vs new, component vs role)
- Blockquotes for warnings and security notes (API keys, GPU runtime)
- ASCII or fenced diagram for pipeline architecture
- Glossary for domain terms (hybrid search, reranking, alpha, stuff chain)
- Full URLs for external links; full paths for repo files
- Author credit at end if present in original notebook

## Safe editing approach

Prefer editing `.ipynb` JSON via a small script when many cells change:

- Update `source` on markdown cells
- Update `source` on code cells (comments only)
- Insert markdown cells at chosen indices
- Never touch `outputs` or `execution_count`

Or use `EditNotebook` for small, targeted changes.

## Anti-patterns

- Paraphrasing saved LLM outputs in markdown as if they were edited
- Changing `pip install` packages or model IDs while claiming “docs only”
- Inventing demo scores not present in outputs
- Removing outputs to “clean up” the notebook
- Rewriting working code “for clarity”

## Example request

> “Update markdown and comments so students can self-learn; don’t change results or outputs; check scores against execution.”

Apply this skill end-to-end: inventory → verify outputs → rewrite markdown → comment-only code updates → validate.
