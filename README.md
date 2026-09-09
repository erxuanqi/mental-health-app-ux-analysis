# Mental Health App UX Analysis

## Project Overview

This project uses Python and NLP methods to analyse public user reviews of mental health mobile applications from the MHARD dataset.

The aim is to identify user experience patterns, common pain points, and design implications for digital health products. The project focuses on how users describe satisfaction, frustration, usability barriers, pricing concerns, technical problems, trust issues, and perceived support quality in mental health apps.

This is an applied UX, HCI, and digital health data analysis project. It is not intended as a clinical prediction or diagnostic system.

---

## Ethical Scope

This project analyses public app review data at an aggregate level.

The project does **not** attempt to:

- diagnose mental health conditions;
- predict depression, suicide risk, or clinical status;
- infer individual users' psychological conditions;
- identify users or personal information;
- provide clinical risk assessment.

The full raw dataset is not redistributed in this repository. The repository only includes notebooks, summary tables, aggregate outputs, and visualisations.

---

## Dataset

Dataset: MHARD mental health app reviews dataset

The dataset is loaded directly from the official public GitHub source inside the notebooks:

```text
https://raw.githubusercontent.com/Sensify-Lab/MHARD/main/MHARD_dataset.csv
```

Cleaned dataset summary:

| Item | Value |
|---|---:|
| Original dataset size | 200,972 reviews |
| Number of apps | 73 |
| Cleaned dataset size | 194,774 reviews |
| High-rating reviews | 141,642 |
| Low-rating reviews | 42,322 |
| Neutral-rating reviews | 10,810 |

Rating groups:

| Rating | Group |
|---|---|
| 1–2 stars | Low rating |
| 3 stars | Neutral rating |
| 4–5 stars | High rating |

---

## Research Questions

1. What are the most common UX pain points in low-rating mental health app reviews?
2. How do low-rating reviews differ from high-rating reviews?
3. Can topic modelling support the rule-based pain point categories?
4. Do transformer-predicted sentiment labels align with user-provided ratings?
5. What do rating-sentiment disagreement cases reveal about mixed user experiences?
6. Can DistilBERT classify low-rating versus high-rating reviews as a rating-derived user satisfaction task?

---

## Methods

The project is organised into five levels:

| Level | Method | Status |
|---|---|---|
| Level 1 | Data cleaning and exploratory data analysis | Completed |
| Level 2 | TF-IDF, UX pain point classification, and design implications | Completed |
| Level 3 | TF-IDF + NMF topic modelling | Completed |
| Level 4 | Transformer-assisted sentiment and zero-shot UX classification | Completed |
| Level 5 | DistilBERT rating classification | Completed |

---

## Level 1: Data Cleaning and Exploratory Analysis

Level 1 establishes the data foundation for the project.

Main steps:

- loaded the full MHARD dataset;
- inspected columns, missing values, and rating distribution;
- cleaned missing and duplicate reviews;
- created rating groups;
- calculated review length and word count;
- created a developer response indicator;
- generated exploratory visualisations.

Key findings:

- the dataset is strongly skewed toward high-rating reviews;
- low-rating reviews are fewer but still numerous enough for UX pain point analysis;
- low-rating and neutral-rating reviews tend to be longer, suggesting that dissatisfied users often describe problems in more detail.

---

## Level 2: TF-IDF, Pain Point Classification, and Design Implications

Level 2 is the main UX analysis layer of the project.

This level compares low-rating and high-rating reviews using TF-IDF keyword analysis. A refined TF-IDF analysis was added using project-specific stopwords to remove broad app-review words and improve interpretability.

The refined low-rating keywords highlighted issues related to:

- payment and subscriptions;
- free trials and premium features;
- account and login problems;
- updates and technical failures;
- cancellation and refunds;
- usability barriers.

A refined rule-based UX pain point classification was then applied to low-rating reviews.

Pain point results:

| Pain Point Category | Review Count |
|---|---:|
| Pricing / Subscription | 17,248 |
| Technical Issues | 13,633 |
| Other / Unclassified | 12,460 |
| Usability / Interface | 5,293 |
| Account / Login Issues | 4,722 |
| Content Quality / Effectiveness | 1,633 |
| Privacy / Trust | 1,277 |
| Customer Support | 975 |

Design implications were developed around:

- pricing transparency;
- technical reliability;
- account control and deletion rights;
- usability and onboarding;
- content effectiveness;
- privacy and trust.

---

## Level 3: Topic Modelling

Level 3 uses TF-IDF and NMF topic modelling to explore recurring themes in low-rating reviews.

Low-rating reviews with fewer than five words were removed to improve topic quality. The final topic modelling dataset contained 36,761 low-rating reviews.

NMF was selected because it is stable, interpretable, and suitable for short app review texts.

Refined NMF topics included:

- premium content and locked features;
- subscription cancellation and refunds;
- paywall barriers;
- free trial and credit card concerns;
- wasted money and perceived poor value;
- updates, crashes, and installation issues;
- account, login, email, and password problems;
- app malfunction and notification problems;
- uninstall and app removal problems;
- perceived mental health support quality.

The Level 3 topics broadly align with the Level 2 pain point categories. This supports the Level 2 classification and provides an additional unsupervised validation layer.

---

## Level 4: Transformer-assisted UX Review Analysis

Level 4 uses pre-trained transformer models to support sentiment analysis and UX pain point classification.

### Transformer Sentiment Analysis

Model used:

```text
distilbert-base-uncased-finetuned-sst-2-english
```

A stratified sample of 2,500 reviews was used:

| Rating Group | Sample Size |
|---|---:|
| Low rating | 1,000 |
| Neutral rating | 500 |
| High rating | 1,000 |

Sentiment results:

| Rating Group | Negative | Positive |
|---|---:|---:|
| Low rating | 90.7% | 9.3% |
| Neutral rating | 70.6% | 29.4% |
| High rating | 23.1% | 76.9% |

The results show that transformer-predicted sentiment broadly aligns with user ratings, but not perfectly.

### Rating-Sentiment Disagreement

Disagreement cases:

| Disagreement Type | Count |
|---|---:|
| Low rating but predicted Positive | 93 |
| High rating but predicted Negative | 231 |

These cases are useful for UX interpretation because users may express mixed experiences. For example, a user may like the app concept but give a low rating because of pricing, bugs, subscription barriers, or access problems.

### Zero-shot UX Pain Point Classification

Model used:

```text
facebook/bart-large-mnli
```

A sample of 300 low-rating reviews was classified using UX pain point labels.

Results:

| Label | Percentage |
|---|---:|
| unclear issue | 47.00% |
| usability or interface issue | 20.33% |
| pricing or subscription issue | 15.00% |
| content quality or effectiveness issue | 6.00% |
| account or login issue | 5.67% |
| privacy or trust issue | 3.67% |
| technical issue | 2.33% |

The high proportion of unclear classifications suggests that general-purpose zero-shot models may struggle with short, informal, or heavily cleaned app review text. Therefore, zero-shot classification is treated as a complementary method rather than a replacement for rule-based UX analysis or topic modelling.

---

## Level 5: BERT-based Rating Classification

Level 5 fine-tunes DistilBERT to classify low-rating versus high-rating reviews.

This is framed as a rating-derived user satisfaction classification task, not a clinical prediction task.

Model used:

```text
distilbert-base-uncased
```

Dataset:

| Group | Sample Size |
|---|---:|
| Low rating | 2,000 |
| High rating | 2,000 |
| Total | 4,000 |

Train/test split:

| Split | Size |
|---|---:|
| Train | 3,200 |
| Test | 800 |

Model performance:

| Metric | Value |
|---|---:|
| Accuracy | 0.9138 |
| Precision | 0.9413 |
| Recall | 0.8825 |
| F1-score | 0.9110 |

Confusion matrix:

```text
[[378, 22],
 [47, 353]]
```

The model correctly classified 731 out of 800 test reviews.

Error analysis showed that misclassified reviews often involved short text, mixed sentiment, positive language in low-rating reviews, or complaints within otherwise high-rating reviews.

---

## Repository Structure

```text
mental-health-app-ux-analysis/
├── notebooks/
│   ├── 01_main_analysis_level1_2.ipynb
│   ├── 02_topic_modelling_level3.ipynb
│   └── 03_transformer_and_bert_modelling_level4_5.ipynb
├── outputs/
│   ├── figures/
│   └── tables/
└── README.md
```

---

## Key Outputs

The repository includes notebooks, figures, and summary-level tables. Selected key outputs are listed below. Additional generated files can be found in the `outputs/figures/` and `outputs/tables/` folders.

### Notebooks

```text
notebooks/01_main_analysis_level1_2.ipynb
notebooks/02_topic_modelling_level3.ipynb
notebooks/03_transformer_and_bert_modelling_level4_5.ipynb
```

### Selected Figures

```text
outputs/figures/rating_distribution.png
outputs/figures/rating_group_distribution.png
outputs/figures/refined_pain_point_category_distribution.png
outputs/figures/level3_refined_topic_distribution.png
outputs/figures/level4_sentiment_by_rating_group.png
outputs/figures/level4_zero_shot_pain_point_distribution.png
outputs/figures/level5_confusion_matrix.png
```

### Selected Tables

```text
outputs/tables/refined_pain_point_counts.csv
outputs/tables/level3_refined_topic_summary_table.csv
outputs/tables/level3_refined_topic_keywords.csv
outputs/tables/level4_sentiment_summary.csv
outputs/tables/level4_disagreement_summary.csv
outputs/tables/level4_zero_shot_pain_point_summary.csv
outputs/tables/level4_method_comparison.csv
outputs/tables/level5_model_metrics.csv
outputs/tables/level5_classification_report.csv
outputs/tables/level5_error_analysis_summary.csv
```

---

## Files Not Included

This repository does not include:

- the full MHARD raw dataset;
- large review-level exports containing full review text;
- model checkpoints;
- trained model weights;
- `distilbert_level5_output/`;
- `model.safetensors`;
- `pytorch_model.bin`.

The repository focuses on reproducible notebooks, summary outputs, and aggregate visualisations.

---

## Limitations

This project has several limitations.

First, app reviews are subjective and may reflect multiple factors at once, including product quality, pricing, expectations, platform issues, and personal circumstances.

Second, low ratings are used as a proxy for dissatisfaction, but user experience is more complex than star ratings alone.

Third, rule-based classification is transparent and interpretable, but it depends on manually defined keywords and may miss implicit issues.

Fourth, topic modelling requires human interpretation and is sensitive to preprocessing choices.

Fifth, the transformer models used in Level 4 are general-purpose models and were not specifically trained on mental health app reviews.

Finally, the Level 5 DistilBERT model predicts rating-derived satisfaction, not clinical status.

---

## Summary

This project demonstrates how Python and NLP methods can be used to analyse large-scale mental health app reviews from a UX and digital health perspective.

The main contribution is the staged analytical design:

```text
Data cleaning
→ exploratory analysis
→ TF-IDF keyword analysis
→ rule-based UX pain point classification
→ design implications
→ NMF topic modelling validation
→ transformer sentiment analysis
→ zero-shot UX classification
→ DistilBERT rating classification
→ model evaluation and error analysis
```

The project shows how user review data can be transformed into interpretable evidence about pricing, technical reliability, usability, account control, content effectiveness, customer support, privacy, trust, and user satisfaction in digital mental health products.
