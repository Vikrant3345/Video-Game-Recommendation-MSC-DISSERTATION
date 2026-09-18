# Video Game Recommendation System

**MSc Data Science Dissertation**  
**University of Bristol**  
**Author: Vikrant Deshmukh**

This repository contains the implementation and evaluation of a **query-driven video game recommendation system** developed as part of an MSc Data Science dissertation.

Given a game title as a query, the system retrieves related games using multiple complementary recommendation approaches and combines their ranked outputs using **Weighted Reciprocal Rank Fusion (RRF)**.

---

## Recommendation Pipeline

The project includes the following recommendation approaches:

### 1. Popularity Baseline
A non-personalised catalogue-level baseline based on game popularity and engagement signals.

### 2. Metadata Recommender
A content-based recommender using structured game metadata including:

- genres
- tags
- gameplay modes

Metadata features are independently encoded and IDF-weighted before similarity retrieval.

### 3. Transformer Semantic Recommender
A semantic recommender based on transformer sentence embeddings generated using:

`sentence-transformers/all-mpnet-base-v2`

This component captures semantic similarity between game descriptions beyond direct lexical overlap.

### 4. Graph-Based Recommender
A weighted bipartite graph representation connecting games with:

- genres
- categories
- tags
- developers
- publishers

Graph-derived feature representations are used to retrieve structurally related games.

### 5. Hybrid Recommender
The final recommender combines ranked candidates from the Metadata, Graph and Semantic models using **Weighted Reciprocal Rank Fusion**.

| Model | Weight |
|---|---:|
| Metadata | 0.40 |
| Graph | 0.40 |
| Semantic | 0.20 |

The RRF smoothing constant is set to `60`.

---

## Repository Structure

```text
├── README.md
├── requirements.txt
├── .gitignore
│
└── notebooks/
    ├── Implementation Notebooks/
    │   ├── 01_Data_Preparation.ipynb
    │   ├── 02_popularity_and_weighted_metadata_recommender.ipynb
    │   ├── 03_transformer_semantic_recommender.ipynb
    │   ├── 04_graph_based_recommender.ipynb
    │   └── 05_Hybrid_Recommender.ipynb
    │
    └── Evaluation and Experimentation/
        ├── Evaluation_Notebook.ipynb
        ├── rich_text_tfidf_recommender_experimental.ipynb
        └── 06_Hardware_topup.ipynb
├── Outputs
```

---

## Dataset

The project uses the Steam Games Dataset 2025.

The processed dataset used by the recommendation models contains **89,618 games and 50 features**. Due to its large file size, the dataset is not stored directly in this repository.

Dataset access and reproduction instructions are available in [`data/README.md`](data/README.md).

---

## Evaluation

The Metadata, Graph, Semantic and Hybrid recommenders are evaluated using a common set of query games.

The evaluation considers recommendation relevance, ranking performance, diversity, runtime and RRF weight sensitivity.

The full evaluation workflow is available in:

`notebooks/Evaluation and Experimentation/Evaluation_Notebook.ipynb`

---

## Running the Project

Recommended execution order:

1. `01_Data_Preparation`
2. `02_popularity_and_weighted_metadata_recommender`
3. `03_transformer_semantic_recommender`
4. `04_graph_based_recommender`
5. `05_Hybrid_Recommender`
6. `Evaluation_Notebook`

The notebooks were developed primarily in Google Colab and use Google Drive for data and generated outputs.

---

## Project Files

The complete dissertation project, including larger datasets and generated outputs, is available on Google Drive:

[Google Drive Project Folder](https://drive.google.com/drive/folders/1bw8KhigGPyJNpMbJtwzZ_Sje4BL8hDvo?usp=sharing)
