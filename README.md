# CodeT5+ Algorithmic Diversity -- Cross-Language Code Clustering

> **Decoding Algorithmic Diversity Across Programming Languages using CodeT5+ with Clustering Analysis**
> IEEE CONIT 2025 -- DOI: [10.1109/CONIT65521.2025.11167866](https://doi.org/10.1109/CONIT65521.2025.11167866)

---

## Overview

This project investigates whether **transformer-based code embeddings can capture algorithmic semantics independent of programming language syntax**. Using `Salesforce/codet5p-110m-embedding`, we embed algorithm implementations in C, Java, and Python, then apply UMAP + DBSCAN/HDBSCAN clustering to study cross-language semantic structure.

**Research Question:** When the same algorithm (e.g., quicksort, binary search, BFS) is implemented in three different languages, do the embeddings cluster by *algorithm* or by *language*?

---

## Methodology

```
Algorithm Implementations (C | Java | Python)
    |
    v
[Option A] Code-only embeddings
[Option B] AST-only embeddings          <-- Abstract Syntax Tree representation
[Option C] Code + AST combined
    |
    v
CodeT5+ (codet5p-110m-embedding)        <-- 110M parameter model, Salesforce
    |
    v
UMAP dimensionality reduction           <-- n_components in {2, 3, 4, 6, 8, 10}
    |
    v
DBSCAN / HDBSCAN clustering
    |
    v
Cluster analysis and visualisation
```

---

## Experiments

| Notebook | Track | Language(s) | Embedding Type |
|---|---|---|---|
| `C_CODEONLY.ipynb` | Code-only | C | Code |
| `JAVA_CODEONLY.ipynb` | Code-only | Java | Code |
| `python_complete.ipynb` | Code-only | Python | Code |
| `java_ast_code.ipynb` | Code + AST | Java | Code + AST |
| `Python_AST_code.ipynb` | Code + AST | Python | Code + AST |
| `Combined_all.ipynb` | Cross-language | C + Java + Python | All three tracks |

Pre-computed UMAP embeddings are included as `.xlsx` files for each language x embedding type x n_components combination (25 files total).

---

## Requirements

```bash
pip install transformers torch umap-learn hdbscan scikit-learn pandas openpyxl
```

GPU recommended for re-embedding. Pre-computed embeddings allow analysis without GPU.

---

## Key Concepts

- **CodeT5+** -- encoder-decoder transformer trained on code; the 110M embedding model maps code to a dense semantic vector space
- **AST (Abstract Syntax Tree)** -- language-agnostic structural representation of code; strips syntax, preserves logic
- **UMAP** -- dimensionality reduction preserving local manifold structure (vs PCA which preserves global variance)
- **DBSCAN** -- density-based clustering; finds clusters of arbitrary shape, marks outliers as noise
- **HDBSCAN** -- hierarchical extension of DBSCAN; handles variable-density clusters better

---

## Authors

Geda Tejesh Chowdary | Paramkusam Sriharsha | Yelipe Gowtham

Amrita Vishwa Vidyapeetham, Bengaluru
