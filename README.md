# EcoTroph-RAG: Retrieval-Augmented Ecological Intelligence for Freshwater Fish Diet Analysis

## Overview

**EcoTroph-RAG** is a lightweight retrieval-augmented ecological intelligence framework developed for semantic search, evidence retrieval, summarization, and explainable analysis of freshwater fish dietary records.

The framework uses the **TroPhish** dataset, which contains freshwater fish dietary information extracted from literature reports ranging from the 1890s to the present. The system converts structured tabular diet records into ecological text units, embeds them using Hugging Face embedding models, stores them in a vector database, retrieves relevant records for ecological queries, and summarizes the retrieved evidence using transformer-based summarization models.

## Dataset

This work uses the TroPhish dataset from the public GitHub repository:

https://github.com/jswesner/TroPhish

The dataset file is available in the original repository at:

```text
data/trophish_dataset.csv
````

Dataset citation:

> Ridgway, Jacob M. 2022. “TROPHISH: BUILDING A GLOBAL DATABASE OF FRESHWATER TROPHIC INTERACTIONS.” Honors Thesis. [https://red.library.usd.edu/honors-thesis/259](https://red.library.usd.edu/honors-thesis/259).

## Framework Pipeline

```text
TroPhish CSV
    ↓
Data cleaning and normalization
    ↓
Tabular row-to-ecological-text conversion
    ↓
Sentence embedding generation
    ↓
Vector indexing using Chroma
    ↓
Ecological query input
    ↓
Top-k semantic evidence retrieval
    ↓
Abstractive summarization
    ↓
Evaluation, statistical testing, and explainability
```

## Main Components

### 1. Data Preprocessing

The TroPhish CSV is cleaned and normalized. Important fields include:

* fish species
* prey kingdom
* prey taxon
* prey class
* prey origin
* prey stage
* diet value
* diet units
* diet type
* diet percentage
* habitat
* longitude
* latitude

Each row is converted into an ecological sentence such as:

```text
Fish species Notropis biguttatus consumed prey taxon ephemeroptera from prey kingdom Metazoa and prey class Insecta. The prey origin was aquatic. The diet value was 8.6 percent, measured as volume, with diet percent 8.6. The habitat was lotic.
```

### 2. Retrieval-Augmented Generation

The framework implements a RAG pipeline using:

* **retrieval** from TroPhish records
* **semantic vector search**
* **evidence-grounded summarization**

The generated answers are based on retrieved TroPhish records rather than unsupported model generation.

### 3. Embedding Models

The framework supports comparison of multiple retrieval methods:

* BM25 keyword retrieval
* `sentence-transformers/all-MiniLM-L6-v2`
* `BAAI/bge-m3`
* `nomic-ai/nomic-embed-text-v1.5`

### 4. Vector Database

The vector index is implemented using:

```text
Chroma
```

Chroma stores ecological text units, metadata, and embeddings for semantic search.

### 5. Summarization Models

Two abstractive summarization models are evaluated:

* `facebook/bart-large-cnn`
* `google-t5/t5-base`

The summarizers generate concise ecological interpretations from retrieved evidence.

## Evaluation Design

The framework evaluates retrieval and summarization quality using query-level ecological test cases.

### Retrieval Metrics

* Precision@10
* HitRate@10
* Mean Reciprocal Rank
* nDCG@10
* query latency

### Summarization Metrics

* ROUGE-1 F1
* ROUGE-2 F1
* ROUGE-L F1
* compression ratio
* summarization latency

### Statistical Analysis

The framework includes paired statistical testing across models:

* Shapiro normality test
* D’Agostino normality test
* paired t-test
* Wilcoxon signed-rank test
* bootstrap confidence intervals
* Cohen’s d
* Hedges’ g
* rank-biserial correlation
* Cliff’s delta
* Pearson correlation
* Spearman correlation
* win/tie/loss counts

### Explainability

SHAP-based surrogate explainability is used to analyze which factors influence:

* retrieval performance
* summarization quality

The SHAP analysis explains query-level evaluation outcomes, not the internal neural parameters of transformer models.

## Suggested Repository Structure

```text
EcoTroph-RAG/
│
├── data/
│   └── trophish_dataset.csv
│
├── notebooks/
│   └── EcoTroph_RAG_Colab.ipynb
│
├── results/
│   ├── dataset_statistics.csv
│   ├── query_validation_dataset_coverage.csv
│   ├── retrieval_summary.csv
│   ├── embedding_model_statistical_tests_publication.csv
│   ├── bart_t5_summarizer_summary_table.csv
│   └── bart_t5_summarizer_statistical_tests.csv
│
├── figures/
│   ├── figure_retrieval_performance.png
│   ├── figure_query_latency.png
│   ├── figure_rouge_scores.png
│   └── figure_shap_summary.png
│
├── README.md
└── requirements.txt
```

## Installation

```bash
pip install pandas numpy chromadb sentence-transformers transformers torch scikit-learn tqdm rank-bm25 rouge-score psutil matplotlib seaborn shap FlagEmbedding
```

## Basic Usage

```python
df = pd.read_csv("data/trophish_dataset.csv")
```

Run the notebook:

```text
notebooks/EcoTroph_RAG_Colab.ipynb
```

The notebook performs:

1. dataset loading
2. ecological text construction
3. embedding generation
4. Chroma indexing
5. semantic retrieval
6. BM25 baseline comparison
7. summarization using BART and T5
8. statistical evaluation
9. SHAP explainability
10. result export

## Research Contribution

EcoTroph-RAG contributes:

1. A row-to-text ecological representation method for freshwater diet records.
2. A retrieval-augmented framework for semantic fish diet intelligence.
3. Comparative evaluation of keyword and embedding-based retrieval models.
4. Comparative evaluation of BART and T5 summarization modules.
5. Statistical and explainable analysis of retrieval and summarization performance.

## Possible Paper Title

**EcoTroph-RAG: A Retrieval-Augmented Ecological Intelligence Framework for Freshwater Fish Diet Analysis**

## Citation

If using the TroPhish dataset, cite:

```text
Ridgway, Jacob M. 2022. “TROPHISH: BUILDING A GLOBAL DATABASE OF FRESHWATER TROPHIC INTERACTIONS.” Honors Thesis. https://red.library.usd.edu/honors-thesis/259.
```

Also acknowledge the TroPhish GitHub repository:

```text
https://github.com/jswesner/TroPhish
```

## License and Data Use

This repository uses the TroPhish dataset from its original public repository. Users should follow the licensing and citation requirements of the original TroPhish repository and thesis source.

## Acknowledgement

The dataset was created by Jacob Ridgway and Jeff Wesner. This framework builds upon their freshwater trophic interaction dataset to explore retrieval-augmented ecological intelligence, semantic search, summarization, and explainable AI for freshwater fish diet analysis.

```
```
