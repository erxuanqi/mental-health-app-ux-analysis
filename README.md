# Mental Health App UX Analysis

## Project Overview

This project uses Python to analyse public user review data from mental health mobile applications. The aim is to identify user experience patterns, common pain points, and design implications for digital health products.

The project combines data analysis, digital health, and user experience research. It focuses on how users describe their experiences with mental health apps, including satisfaction, usability problems, subscription concerns, trust, personalisation, and emotional support needs.

## Research Questions

1. What are the most common user concerns in mental health app reviews?
2. How do negative reviews differ from positive reviews?
3. Can user reviews be grouped into meaningful experience-based segments?
4. Which textual features are associated with low user ratings?
5. What design implications can be drawn for future digital mental health products?

## Dataset

This project uses a public mental health app review dataset. The analysis focuses on publicly available user feedback rather than private clinical records or sensitive patient-level data.

The full raw dataset is not redistributed in this repository. Instead, the project provides analysis notebooks, summary visualisations, and derived aggregate outputs.

## Methods

The project includes:

- Data cleaning
- Exploratory data analysis
- Rating distribution analysis
- App-level comparison
- Review length analysis
- Text preprocessing
- TF-IDF keyword analysis
- High-rating versus low-rating review comparison
- Rule-based user pain point classification
- Topic modelling
- Design implications for digital health products

## Tools

- Python
- pandas
- numpy
- matplotlib
- scikit-learn
- Jupyter Notebook / Google Colab

## Expected Outputs

The project will produce:

- Python analysis notebooks
- Visualisations
- User pain point summary tables
- Topic modelling outputs
- Design implications report
- Dataset source reference rather than redistributed full raw data

## Analysis Roadmap

This project is designed as a staged analysis, starting from core Python-based user review analysis and leaving space for more advanced NLP and machine learning extensions.

### Level 1: Data Cleaning and Exploratory Analysis

Status: Completed

This level loaded the full MHARD dataset, inspected the dataset structure, cleaned missing and duplicate reviews, created rating groups, and generated exploratory visualisations.

Key outputs include rating distribution, rating group distribution, review volume by app, average rating by app, and review length comparison across rating groups.

### Level 2: TF-IDF, Pain Point Classification, and Design Implications

Status: Completed

This level compares high-rating and low-rating reviews, extracts keywords using TF-IDF, identifies recurring UX pain points, and translates findings into design implications for digital mental health products.

A refined rule-based pain point classification was applied to low-rating reviews to identify recurring UX issues, including pricing and subscription problems, technical issues, usability barriers, account or login problems, content effectiveness concerns, privacy and trust concerns, and customer support issues.

### Level 3: Topic Modelling
Status: Completed

This level uses TF-IDF and NMF topic modelling to explore recurring themes in low-rating mental health app reviews. A refined NMF model with project-specific stopwords was added to improve topic interpretability. The automatically discovered topics broadly align with the Level 2 pain-point categories, including pricing, technical issues, account/login problems, usability barriers, and perceived service effectiveness.

### Level 4: Transformer-assisted Sentiment and Classification Analysis

Status: Planned

This optional level uses pre-trained transformer models to support sentiment analysis and pain-point classification.

The aim is to explore whether transformer-assisted analysis can support large-scale UX review analysis while keeping the interpretation focused on user experience rather than clinical diagnosis.

### Level 5: BERT Fine-tuning for Rating Classification

Status: Future work

This optional level explores whether review text can be used to predict low-rating versus high-rating reviews.

This level is treated as a future extension rather than the core contribution of the project.

## Ethical Considerations

This project uses a publicly available mental health app review dataset for educational and portfolio purposes. The analysis focuses on aggregated UX patterns rather than individual users.

Full raw review data is not redistributed in this repository. Only analysis notebooks, summary figures, and derived aggregate tables are included.

The project does not attempt to diagnose users, infer individual mental health conditions, identify personal information, or assess clinical risk. Advanced NLP methods are used only to support user experience analysis and digital health design interpretation.

## Project Status

Levels 1–3 have been completed. Level 4 and Level 5 are planned as optional advanced extensions.
