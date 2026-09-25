# Comparison of OPTICS and HDBSCAN in the BERTopic Algorithm for Sentiment-Based Topic Modeling of X Users Regarding Police Performance

**Final Project (Tugas Akhir) — SS234862**
Bachelor Program of Statistics, Institut Teknologi Sepuluh Nopember (ITS) Surabaya, 2026

---

## Overview

This study analyzes public opinion on Indonesian National Police (Polri) performance during the national leadership transition from President Joko Widodo to President Prabowo Subianto. Using 4,618 posts collected from social media platform X (formerly Twitter) via the keyword *"kinerja polisi"* over the period July 2023–December 2025, the study applies sentiment classification and topic modeling to map public discourse systematically.

---

## Research Questions

1. What are the characteristics of posts collected from platform X regarding police performance during the government transition era?
2. How does the IndoBERTweet model perform in classifying positive and negative sentiment?
3. How do BERTopic-based topic models using OPTICS and HDBSCAN compare in terms of topic quality and representativeness?

---

## Methodology

### Pipeline Overview

```
Data Crawling (X/Twitter)
    ↓
Text Pre-processing
    (Character Normalization → Text Normalization → Stopwords Removal → Tokenization)
    ↓
Sentiment Labeling (InSet Lexicon)
    ↓
Sentiment Classification (IndoBERTweet)
    ↓
Topic Modeling (BERTopic)
    ├── HDBSCAN clustering
    └── OPTICS clustering
    ↓
Evaluation & Comparison
```

### Sentiment Classification

- **Model:** IndoBERTweet (Koto et al., 2021) — a Transformer-based language model pretrained on Indonesian Twitter data
- **Classes:** Positive, Negative (neutral excluded)
- **Optimizer:** Adam
- **Loss:** Binary Cross-Entropy

### Topic Modeling

- **Framework:** BERTopic (Grootendorst, 2022)
- **Embedding:** Sentence embeddings from IndoBERTweet
- **Dimensionality Reduction:** UMAP
- **Clustering algorithms compared:**
  - **HDBSCAN** — Hierarchical Density-Based Spatial Clustering of Applications with Noise
  - **OPTICS** — Ordering Points To Identify the Clustering Structure
- **Topic representation:** Class-based TF-IDF (c-TF-IDF)
- **Evaluation metrics:**
  - Topic Coherence (Cv)
  - Topic Diversity (TD)
  - Outlier proportion

---

## Key Results

### Sentiment Classification

| Metric | Score |
|---|---|
| Accuracy | 93.40% |
| Macro F1-Score | 91.03% |
| Negative documents | 3,480 |
| Positive documents | 1,138 |

### Topic Modeling Comparison

| Metric | HDBSCAN (Positive) | OPTICS (Positive) | HDBSCAN (Negative) | OPTICS (Negative) |
|---|---|---|---|---|
| Outlier (%) | 28.73% | 85.94% | 62.36% | 85.63% |
| Coherence (Cv) | 0.54 | — | 0.48 | — |
| Topic Diversity | 0.97 | — | 0.90 | — |
| Topics extracted | 7 | — | 8 | — |

HDBSCAN outperforms OPTICS in this corpus due to substantially lower outlier rates. OPTICS discarded over 85% of documents as noise in both sentiment groups, making it unrepresentative for this dataset.

### Topic Highlights

**Positive topics (HDBSCAN):** Appreciation for operational performance, public service quality, anti-narcotics operations, food security contributions.

**Negative topics (HDBSCAN):** Demands for institutional reform, erosion of public trust, budget criticism, virality-driven case handling, skepticism toward satisfaction surveys, excessive force in protests (August 2025).

**Temporal shift:** Early period discourse centered on comparisons with foreign law enforcement institutions; later period shifted toward budget issues, specific incidents, and accountability demands.

---

## Dataset

- **Source:** Social media platform X (Twitter)
- **Keyword:** `kinerja polisi`
- **Language filter:** `lang:id` (Indonesian, ISO 639-1)
- **Period:** July 2023 – December 2025
- **Total documents:** 4,618
- **Collection tool:** [tweet-harvest](https://github.com/helmisatria/tweet-harvest)

---

## Tech Stack

| Component | Tool / Library |
|---|---|
| Data collection | tweet-harvest |
| Text preprocessing | Python (custom pipeline) |
| Sentiment labeling | InSet Lexicon |
| Sentiment model | IndoBERTweet (HuggingFace Transformers) |
| Topic modeling | BERTopic |
| Dimensionality reduction | UMAP |
| Clustering | HDBSCAN, OPTICS (scikit-learn) |
| Hyperparameter tuning | Grid search (custom) |
| Evaluation | Gensim (Cv), custom diversity scorer |

## Documentation

[see the documentation here!](https://drive.google.com/drive/folders/1oasfKG9457_ZC8lHykkfqt6g1D4n96VC?usp=drive_link)

## Author

**Akbar Razan**
NRP 5003221150
Department of Statistics, Faculty of Science and Data Analytics
Institut Teknologi Sepuluh Nopember (ITS) Surabaya

Contact: akbarrazan35@gmail.com

**Advisor:** Tintrim Dwi Ary Widhianingsih, S.Si., M.Stat., Ph.D.

---

## References

Key references cited in this study:

- Grootendorst, M. (2022). BERTopic: Neural topic modeling with a class-based TF-IDF procedure. *arXiv preprint arXiv:2203.05794*.
- Koto, F., Rahimi, A., Lau, J. H., & Baldwin, T. (2021). IndoBERTweet: A pretrained language model for Indonesian Twitter with effective domain-specific vocabulary initialization. *EMNLP 2021*.
- Yakymovych, A., & Singh, P. (2024). Semantic and topic analysis on threatening emails using BERTopic with OPTICS vs HDBSCAN.
- Tamzila et al. (2025). Topic modeling of traffic complaints on social media: BERTopic vs LDA.
- Jefri et al. (2025). Sentiment analysis and topic modeling of TikTok comments on maternal mental health apps using IndoBERT and BERTopic.