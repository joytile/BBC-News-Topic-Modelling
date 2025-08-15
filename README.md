# BBC News NLP Pipeline

## Overview
This repository contains an NLP workflow for analysing and sub-categorising a BBC-style news dataset.  
The project combines **text preprocessing**, **topic modelling** with BERTopic, and **manual sub-category labelling** to explore themes within each news category.

The primary goal is to take a large, labelled corpus (e.g., BBC news articles grouped by main category) and:
- Automatically discover **sub-topics** within each main category
- Assign **human-readable sub-category labels**
- Handle and label **outlier documents** that don’t fit neatly into any cluster

---

## Features

### 1. Data Loading
- Reads a BBC-style dataset from a folder structure
- Stores articles in a Pandas DataFrame with `id`, `category`, and `text`.

### 2. Text Preprocessing
- Lemmatization using **spaCy** (`en_core_web_sm`)
- Custom stopword removal (loaded from `bbc/stopwords.txt`)
- Regex cleanup of non-alphanumeric characters
- Token count feature for basic text statistics

### 3. Topic Modelling & Sub-Categorisation
- Sentence embeddings via **SentenceTransformer** (`all-MiniLM-L6-v2`)
- **MiniBatchKMeans** clustering with an automatically estimated number of clusters
- **Cosine distance** outlier detection (top 5% marked as topic `-1`)
- BERTopic modelling **without UMAP**, using KMeans as the clustering step
- Interactive topic and document visualisations
- Manual labelling of discovered topics into **meaningful sub-categories**
- Keyword-based backfill for outlier sub-categories

---

## Requirements
## Requirements
Install all dependencies from the provided requirements file:
```bash
pip install -r requirements/requirements.txt
```

Folder Structure
.
├── BBC_NLP_Task.ipynb       # Main Jupyter Notebook
├── requirements.text
├── bbc/                     # Dataset root (subfolders per category)
│   ├── business/
│   ├── entertainment/
│   ├── politics/
│   ├── sport/
│   └── tech/
├── bbc/stopwords.txt        # Custom stopword list
└── README.md

