# Chemotherapy Resistance Prediction Using DNA Methylation Data

## Overview

This project focuses on predicting chemotherapy resistance using DNA methylation data and machine learning techniques.

It is developed as part of **Assignment 3** for the M.Sc. Data Science programme at **Freie Universität Berlin**, Winter Semester 2026/27.

The objective is to develop machine learning models that classify cancer cell lines as chemotherapy-sensitive or chemoresistant based on their DNA methylation measurements.

### Target Variable

| Label | Description |
|---|---|
| `0` | Chemotherapy-sensitive |
| `1` | Chemotherapy-resistant |

## Objectives

The main objectives of this project are:

1. Load and explore the DNA methylation features and chemotherapy-resistance labels.
2. Merge both datasets using the `Cell ID` column.
3. Investigate missing values in features and target labels.
4. Visualize the distribution of chemotherapy-resistance classes.
5. Apply appropriate preprocessing techniques, including missing-value handling and feature standardization.
6. Train and evaluate two machine learning classifiers using five-fold cross-validation.
7. Calculate and compare ROC-AUC scores for both classifiers.
8. Perform a statistical comparison to investigate whether one classifier significantly outperforms the other.
9. Optionally investigate techniques for handling class imbalance.

## Dataset

The project uses two CSV files:

| File | Description |
|---|---|
| `methylation.csv` | DNA methylation measurements for different CpG sites |
| `chemoresistance_labels.csv` | Chemotherapy-resistance labels for each cell line |

The two datasets are connected through the `Cell ID` column.

Place both files inside the `data/` directory.

## Project Structure

```text
chemoresistance-prediction/
│
├── data/
│   ├── methylation.csv
│   └── chemoresistance_labels.csv
│
├── notebooks/
│   └── general.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

## Methodology

The project follows these main stages:

1. **Data Loading and Inspection:** Examine the structure, dimensions, data types and identifiers of both datasets.
2. **Data Integration:** Merge the datasets using `Cell ID`.
3. **Data Quality Analysis:** Investigate missing values and justify the selected handling strategy.
4. **Exploratory Data Analysis:** Examine and visualize the target-class distribution.
5. **Data Preprocessing:** Handle missing feature values and standardize numerical features.
6. **Model Development:** Select two suitable classification algorithms.
7. **Model Evaluation:** Apply five-fold cross-validation and calculate ROC-AUC for each fold.
8. **Statistical Comparison:** Investigate whether the performance difference between the classifiers is statistically meaningful.
9. **Optional Extension:** Investigate class-imbalance handling techniques and their effect on model performance.

## Technologies

- Python
- Jupyter Notebook
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- SciPy

## Installation and Setup

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd chemoresistance-prediction
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

### 3. Activate the environment

**Windows:**

```bash
.venv\Scripts\activate
```

### 4. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 5. Start Jupyter Notebook

```bash
jupyter notebook
```

Open `notebooks/general.ipynb` to run the analysis.

## Reproducibility and Data Leakage Prevention

A key consideration in this project is preventing data leakage during model evaluation.

Preprocessing operations, including missing-value imputation and feature standardization, must be fitted using only the training data within each cross-validation fold.

Scikit-learn pipelines will be used to ensure that preprocessing is performed correctly during model evaluation.

## Deliverables

The assignment requires:

- One self-contained and documented Jupyter Notebook.
- A PDF exported from the completed notebook.

The final submission must follow the official assignment instructions regarding filenames and group-member names.

## Academic Context

**Programme:** M.Sc. Data Science  
**University:** Freie Universität Berlin  
**Course:** Introduction to Profile Areas  
**Assignment:** Assignment 3 — Predicting Chemotherapy Resistance from DNA Methylation Data  
**Semester:** Winter Semester 2026/27