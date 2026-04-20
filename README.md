# Customer Segmentation System - Credit Card Behavioral Analysis

Production-oriented customer segmentation system that transforms raw credit card behavior data into actionable customer cohorts for marketing, personalization, and product decisioning.

## Overview

This project implements an end-to-end unsupervised learning pipeline for credit card customer analytics.
It is designed as a segmentation system, not only a clustering experiment, with emphasis on data quality, feature transformation, model selection, and business-facing outputs.

Project context:
- Timeline: Feb 2024 - Feb 2024
- Affiliation: SHAI For AI | شاي للذكاء الاصطناعي
- Role: Built the full pipeline from preprocessing through cluster interpretation

Primary goals:
- Convert raw behavioral features into stable clustering-ready representations
- Identify distinct customer segments from spending and usage patterns
- Produce segment outputs suitable for downstream targeting workflows

Representative use cases:
- Campaign targeting by spending behavior and payment habits
- Product bundling decisions for high-value vs. low-engagement segments
- Retention strategy design for customers with risky repayment behavior

## Architecture

The system follows a modular analytics pipeline:

[Raw Dataset] -> [Data Quality Layer] -> [Feature Transformation Layer] -> [Segmentation Layer] -> [Evaluation Layer] -> [Business Interpretation Layer]

Architecture layers:
- Input Layer: Credit card behavioral dataset ingestion
- Data Quality Layer: Missing-value handling and schema cleanup
- Feature Transformation Layer: Distribution correction, scaling, and dimensionality reduction
- Segmentation Layer: K-Means (primary) with DBSCAN and hierarchical clustering as comparative baselines
- Evaluation Layer: Elbow analysis, silhouette scoring, and visual cluster diagnostics
- Output Layer: Segment assignments, cluster sizes, and behavioral profiles for business action

Design decisions:
- Mode imputation for sparse fields such as CREDIT_LIMIT and MINIMUM_PAYMENTS to preserve record count
- Non-linear transforms (cube root and log1p) for skew reduction before clustering
- PCA used to reduce noise and improve cluster separability
- Multiple clustering families explored to validate segmentation robustness

### Architecture Diagram

![Modular Analytics Pipeline Architecture](./assets/Modular%20Analytics%20Pipeline%20Architecture.png)

This diagram visualizes the end-to-end segmentation workflow from ingestion to business activation.

## Features

- End-to-end segmentation workflow from raw data to interpretable customer cohorts
- Data preprocessing with explicit treatment of missing and skewed financial variables
- Multi-algorithm clustering workflow (K-Means, DBSCAN, hierarchical clustering)
- Cluster validation with quantitative and visual diagnostics
- Segment distribution reporting for operational planning
- Notebook-based analysis artifacts for transparent experimentation

## Technical Highlights

- Engineered a pipeline that separates data quality, feature engineering, modeling, and interpretation concerns
- Implemented skew-aware transformations (cbrt/log1p) to improve model stability on heavy-tailed monetary features
- Used PCA as an intermediate representation to reduce dimensionality before clustering
- Compared algorithmic behavior across centroid-based, density-based, and hierarchical methods
- Balanced metric-optimal configurations with business interpretability in final segment definition

## Model Details

- Primary model: K-Means clustering on PCA-transformed features
- Comparative models: DBSCAN and Ward-linkage hierarchical clustering
- Selection strategy: Elbow analysis for inertia trend inspection
- Selection strategy: Silhouette score sweep across cluster counts
- Selection strategy: Visual silhouette diagnostics (Yellowbrick)
- Practical selection note: The notebooks show strong 2-cluster silhouette results and also a 4-cluster operational segmentation view for richer business actionability.

## Tech Stack

- Language: Python
- Core libraries: NumPy, pandas
- Modeling: scikit-learn (K-Means, DBSCAN, PCA, silhouette metrics)
- Visualization: Matplotlib, Seaborn, Yellowbrick
- Workflow: Jupyter Notebook
- Data source: Kaggle Credit Card Dataset (CC GENERAL.csv)

## Getting Started

### Prerequisites

- Python 3.9+
- Jupyter Notebook or JupyterLab

### Installation

```bash
git clone https://github.com/<your-username>/Credit-Card-Customer-Segmentation.git
cd Credit-Card-Customer-Segmentation
pip install numpy pandas matplotlib seaborn scikit-learn yellowbrick jupyter
```

### Run

```bash
jupyter notebook
```

Open one of the project notebooks and execute cells sequentially:
- Credit Card Customer Segmentation.ipynb
- credit-card-customer-segmentation-78-score.ipynb

Data location:
- Ensure CC GENERAL.csv is available in data/ and update notebook file paths if needed.

## Results

Observed outputs from the notebooks include:
- Best silhouette score (main notebook): 0.46 for 2 clusters
- Example production-style segmentation view: 4-cluster K-Means output with segment counts [4516, 2244, 1276, 914]
- Alternative notebook variant reports stronger 2-cluster silhouette performance (0.66), highlighting sensitivity to preprocessing and experiment setup

Business interpretation outcome:
- Segments can be used to distinguish broad behavioral groups (for example, high-activity vs. low-activity users, revolving-balance dominant users, and cash-advance-heavy profiles), enabling differentiated engagement strategies.

## Project Assets

- Dataset: https://www.kaggle.com/datasets/arjunbhasin2013/ccdata
- Kaggle notebook reference: https://www.kaggle.com/kershrita/credit-card-customer-segmentation-78-score
