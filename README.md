# EcoTroph-RAG: Retrieval-Augmented Ecological Intelligence for Freshwater Fish Diet Analysis

## Repository

This repository contains the implementation of **EcoTroph-RAG**, a retrieval-augmented ecological intelligence framework for freshwater fish diet analysis.

Repository URL:

```text
https://github.com/ParthaPRay/EcoTroph-RAG/
````

The main executable notebook is:

```text
EcoTroph_RAG.ipynb
```

The dataset file included in this repository is:

```text
trophish_dataset.csv
```

The dataset was manually downloaded from the original TroPhish GitHub repository and uploaded here for reproducibility.

---

## Overview

**EcoTroph-RAG** is a lightweight retrieval-augmented generation framework designed to transform structured freshwater fish diet records into a semantically searchable ecological knowledge system.

The framework performs:

1. dataset loading and cleaning,
2. tabular row-to-ecological-text conversion,
3. embedding generation,
4. vector indexing,
5. semantic retrieval,
6. keyword baseline retrieval,
7. abstractive summarization,
8. model comparison,
9. statistical testing,
10. SHAP-based explainability.

The goal is to support ecological diet search, trophic interaction analysis, freshwater fish feeding pattern retrieval, and evidence-grounded summarization.

---

## Dataset Source

This work uses the **TroPhish** dataset created by Jacob Ridgway and Jeff Wesner.

Original dataset repository:

```text
https://github.com/jswesner/TroPhish
```

In the original repository, the dataset is located at:

```text
data/trophish_dataset.csv
```

Dataset citation:

```text
Ridgway, Jacob M. 2022. “TROPHISH: BUILDING A GLOBAL DATABASE OF FRESHWATER TROPHIC INTERACTIONS.” Honors Thesis. https://red.library.usd.edu/honors-thesis/259.
```

The TroPhish dataset contains dietary data extracted from literature reports ranging from the 1890s to the present and covers hundreds of freshwater fish species.

---

## Dataset Used in This Repository

For this repository, the dataset file is provided as:

```text
trophish_dataset.csv
```

The file contains **54,751 rows including the header row**.

That means the data contains approximately:

```text
54,750 dietary records + 1 header row
```

---

## Dataset Columns

The dataset contains the following columns:

```text
fish_species
prey_kingdom
prey_taxon
prey_class
prey_origin
prey_stage
diet_value
diet_units
diet_type
diet_percent
record_id
source_id
fish_id
start_date
end_date
sampling_interval
data_sorted_by
fish_min_length
fish_average_length
fish_max_length
fish_length_units
fish_length_measure
habitat_broad
habitat
longitude
latitude
```

These columns describe fish identity, prey identity, prey taxonomy, diet contribution, sampling information, fish length, habitat type, and geographic location.

---

## Framework Architecture

```text
trophish_dataset.csv
        ↓
Data cleaning and normalization
        ↓
Tabular row-to-ecological-text transformation
        ↓
Embedding generation using Hugging Face models
        ↓
Vector indexing using Chroma
        ↓
Ecological query input
        ↓
Top-k semantic retrieval
        ↓
Evidence-grounded summarization
        ↓
Evaluation, statistical testing, and explainability
```

---

## Row-to-Text Transformation

Each tabular dietary record is converted into a natural-language ecological text unit.

Example:

```text
Fish species Notropis biguttatus consumed prey taxon ephemeroptera from prey kingdom Metazoa and prey class Insecta. The prey origin was aquatic and prey stage was not reported. The diet value was 8.6 percent, measured as volume, with diet percent 8.6. The habitat was lotic. The geographic location was longitude -78.00501 and latitude 43.29869.
```

This transformation allows sentence-embedding models to process structured ecological records as semantic text.

---

## Retrieval-Augmented Generation Design

EcoTroph-RAG uses a retrieval-augmented generation workflow.

In this framework:

1. each TroPhish row is converted into ecological text;
2. the text is embedded into a dense vector representation;
3. embeddings are stored in a Chroma vector database;
4. a user ecological query is embedded;
5. top-k relevant records are retrieved;
6. retrieved records are summarized using abstractive summarization models.

The generated responses are therefore grounded in actual TroPhish records.

---

## Retrieval Models Evaluated

The notebook compares multiple retrieval approaches:

| Method        | Description                                                       |
| ------------- | ----------------------------------------------------------------- |
| BM25          | Keyword-based lexical retrieval baseline                          |
| MiniLM-Chroma | Semantic retrieval using `sentence-transformers/all-MiniLM-L6-v2` |
| BGE-M3        | Dense retrieval using `BAAI/bge-m3`                               |
| Nomic-v1.5    | Retrieval using `nomic-ai/nomic-embed-text-v1.5`                  |

---

## Summarization Models Evaluated

The notebook evaluates two abstractive summarization models:

| Model                     | Use                                  |
| ------------------------- | ------------------------------------ |
| `facebook/bart-large-cnn` | BART-based abstractive summarization |
| `google-t5/t5-base`       | T5-based abstractive summarization   |

Both models summarize the same retrieved ecological evidence, allowing fair comparison.

---

## Evaluation Queries

A set of dataset-grounded ecological queries is used for evaluation.

Example queries include:

```text
Which fish species consume crustaceans in lotic habitats?
Which fish consume aquatic insect larvae?
Which fish species consume Odonata prey?
Which fish consume Ephemeroptera in lotic habitats?
Which fish consume filamentous algae in lotic habitats?
Which records describe Lepomis macrochirus consuming Odonata larvae in creeks?
```

Each query is validated against the dataset using matching terms to ensure that relevant records exist.

---

## Retrieval Evaluation Metrics

Retrieval models are evaluated using:

| Metric       | Meaning                                                |
| ------------ | ------------------------------------------------------ |
| Precision@10 | Fraction of top-10 retrieved records that are relevant |
| HitRate@10   | Whether at least one relevant record appears in top-10 |
| MRR          | Mean Reciprocal Rank of the first relevant record      |
| nDCG@10      | Ranking quality of retrieved evidence                  |
| Latency      | Query execution time                                   |

---

## Summarization Evaluation Metrics

Summarization models are evaluated using:

| Metric                | Meaning                                    |
| --------------------- | ------------------------------------------ |
| ROUGE-1 F1            | Unigram overlap                            |
| ROUGE-2 F1            | Bigram overlap                             |
| ROUGE-L F1            | Longest common subsequence overlap         |
| Compression Ratio     | Summary length relative to evidence length |
| Summarization Latency | Time required to generate summary          |

---

## Statistical Testing

The notebook performs enriched statistical testing for retrieval and summarization comparisons.

Statistical analyses include:

* Shapiro normality test
* D’Agostino normality test
* paired t-test
* Wilcoxon signed-rank test
* bootstrap confidence intervals
* Cohen’s d
* Hedges’ g
* rank-biserial correlation
* paired Cliff’s delta
* Pearson correlation
* Spearman correlation
* win/tie/loss counts

These tests help assess whether observed performance differences between models are meaningful.

---

## Explainability

SHAP-based surrogate explainability is included.

The SHAP analysis explains which factors influence:

1. retrieval performance,
2. summarization quality.

Important note:

```text
SHAP is applied to surrogate machine-learning models trained on query-level evaluation outputs. It does not explain the internal transformer parameters directly.
```

---

## Main Notebook

Run:

```text
EcoTroph_RAG.ipynb
```

The notebook includes:

1. package installation,
2. dataset loading,
3. dataset statistics,
4. ecological text generation,
5. Chroma indexing,
6. BM25 retrieval,
7. semantic retrieval,
8. embedding model comparison,
9. BART summarization,
10. T5 summarization,
11. ROUGE evaluation,
12. latency analysis,
13. statistical testing,
14. SHAP explainability,
15. export of result tables and figures.

---

## Installation

Recommended environment:

```text
Google Colab
Python 3.x
GPU runtime preferred
```

Install dependencies:

```bash
pip install pandas numpy chromadb sentence-transformers transformers torch scikit-learn tqdm rank-bm25 rouge-score psutil matplotlib seaborn shap FlagEmbedding
```

---

## How to Run

Clone the repository:

```bash
git clone https://github.com/ParthaPRay/EcoTroph-RAG.git
cd EcoTroph-RAG
```

Open the notebook:

```text
EcoTroph_RAG.ipynb
```

Run all cells sequentially.

Make sure the dataset file is available in the repository root:

```text
trophish_dataset.csv
```

---

## Expected Outputs

The notebook generates:

```text
dataset statistics
query validation table
retrieval evaluation table
retrieval summary table
embedding model statistical tests
summarization evaluation table
BART vs T5 comparison table
summarizer statistical tests
SHAP plots
publication-grade figures
CSV result files
```

---

## Suggested Repository Structure

```text
EcoTroph-RAG/
│
├── EcoTroph_RAG.ipynb
├── trophish_dataset.csv
├── README.md
│
├── results/
│   ├── dataset_statistics.csv
│   ├── query_validation_dataset_coverage.csv
│   ├── retrieval_summary.csv
│   ├── query_level_retrieval_evaluation.csv
│   ├── embedding_model_statistical_tests_publication.csv
│   ├── bart_t5_summarizer_summary_table.csv
│   └── bart_t5_summarizer_statistical_tests.csv
│
└── figures/
    ├── figure_retrieval_performance.png
    ├── figure_query_latency.png
    ├── figure_rouge_scores.png
    └── figure_shap_summary.png
```

---

## Research Contribution

EcoTroph-RAG contributes:

1. a row-to-text ecological representation method for freshwater fish diet records;
2. a retrieval-augmented framework for freshwater trophic intelligence;
3. comparison of keyword, MiniLM, BGE-M3, and Nomic embedding retrieval;
4. comparison of BART and T5 summarization for ecological evidence;
5. statistical evaluation of retrieval and summarization performance;
6. SHAP-based explainability of query-level outcomes.

---

## Possible Paper Title

```text
EcoTroph-RAG: A Retrieval-Augmented Ecological Intelligence Framework for Freshwater Fish Diet Analysis
```

---

## Citation

If you use this repository, please cite the original TroPhish dataset source:

```text
Ridgway, Jacob M. 2022. “TROPHISH: BUILDING A GLOBAL DATABASE OF FRESHWATER TROPHIC INTERACTIONS.” Honors Thesis. https://red.library.usd.edu/honors-thesis/259.
```

Original TroPhish GitHub repository:

```text
https://github.com/jswesner/TroPhish
```

---

## Acknowledgement

The TroPhish dataset was developed by Jacob Ridgway and Jeff Wesner. This repository builds upon their freshwater trophic interaction dataset to explore semantic retrieval, retrieval-augmented generation, summarization, benchmarking, and explainable AI for freshwater fish diet analysis.

---

## Disclaimer

This repository does not claim ownership of the original TroPhish dataset. The dataset was obtained from the publicly available TroPhish repository and is included here only for reproducibility of the EcoTroph-RAG experiments. Users should consult the original TroPhish repository and thesis for dataset provenance, licensing, and full methodological details.

## Citation

If you use this repository, please cite:

````markdown
## Citation

If you use this repository, please cite:

```text
Ray, Partha Pratim. EcoTroph-RAG: Retrieval-Augmented Ecological Intelligence for Freshwater Fish Diet Analysis. May 23, 2026. GitHub repository. Available at: https://github.com/ParthaPRay/EcoTroph-RAG/
````

### BibTeX

```bibtex
@misc{ray2026ecotrophrag,
  author       = {Partha Pratim Ray},
  title        = {EcoTroph-RAG: Retrieval-Augmented Ecological Intelligence for Freshwater Fish Diet Analysis},
  year         = {2026},
  howpublished = {\url{https://github.com/ParthaPRay/EcoTroph-RAG/}},
  note         = {GitHub repository}
}
```


