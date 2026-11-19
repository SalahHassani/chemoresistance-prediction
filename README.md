
# Predicting Chemotherapy Resistance from DNA Methylation Data

## Project Overview

This project investigates whether DNA methylation measurements can be used to predict chemotherapy resistance in cancer cell lines using machine learning.

The project is part of **Assignment 3** for the course *Introduction to Profile Areas – Data Science*, Winter Semester 2026/27, at Freie Universität Berlin.

DNA methylation is an epigenetic modification that can influence gene expression without changing the underlying DNA sequence. Differences in methylation patterns may be associated with how cancer cells respond to chemotherapy.

The objective is to develop and evaluate machine learning classifiers that distinguish between chemotherapy-sensitive and chemoresistant cell lines based on their DNA methylation profiles.

## Objectives

The main objectives are:

1. Load and explore the provided DNA methylation and chemotherapy resistance datasets.
2. Merge the datasets using the common cell-line identifier.
3. Investigate missing values and assess data quality.
4. Analyse the distribution of chemotherapy resistance labels.
5. Apply appropriate preprocessing techniques.
6. Train two machine learning classification models.
7. Evaluate both models using stratified five-fold cross-validation.
8. Compare model performance using the ROC-AUC metric.
9. Investigate whether one classifier significantly outperforms the other.
10. Explore the effect of class weighting on model performance.

## Dataset Description

The project uses two provided CSV files.

### 1. Methylation Dataset

**File:** `methylation.csv`

Contains DNA methylation measurements for different CpG sites.

- 1,000 observations.
- 50 original CpG features.
- Each feature represents a methylation measurement.
- Contains missing values.

### 2. Chemotherapy Resistance Labels

**File:** `chemoresistance_labels.csv`

Contains the chemotherapy response labels corresponding to the cell lines.

The target variable is:

| Value | Meaning |
|---|---|
| 0 | Chemotherapy-sensitive |
| 1 | Chemotherapy-resistant |

The two datasets share a common cell-line identifier, stored in the `Unnamed: 0` column. This column is renamed to `Cell ID` before merging.

### Final Dataset

After merging and examining missing values:

- Total observations: 1,000.
- Original CpG features: 50.
- Excluded features: 3.
- Final CpG features: 47.
- Target variable: `Chemotherapy_Resistance`.

The three excluded features are:

- `CpG_14`
- `CpG_25`
- `CpG_33`

Each of these features contains 99% missing values.

The remaining 47 features are retained and their missing values are handled using median imputation.

**Note:** The original datasets are provided separately and are not included in this repository.

## Project Structure

```text
chemoresistance-prediction/
│
├── data/
│   ├── methylation.csv
│   └── chemoresistance_labels.csv
│
├── notebooks/
│   └── model.ipynb
│
├── .gitignore
├── README.md
└── requirements.txt
```

The `data/` directory contains the input datasets locally. The CSV files are excluded from Git tracking.

## Methodology

### 1. Data Loading and Exploration

Both CSV files are loaded using Pandas.

Initial data exploration includes:

- Inspecting dataset dimensions and column names.
- Checking data types.
- Identifying missing values.
- Checking identifier uniqueness.
- Verifying matching cell-line identifiers.

### 2. Dataset Integration

The two datasets are merged using `Cell ID`.

An inner join is used to retain observations with matching identifiers in both datasets.

### 3. Missing-Value Analysis

Missing values are examined for each CpG feature.

Three features with 99% missingness are excluded:

- `CpG_14`
- `CpG_25`
- `CpG_33`

The remaining 47 features are retained.

Median imputation is applied to handle the remaining missing measurements.

### 4. Target Distribution

The target distribution is:

| Class | Description | Observations | Percentage |
|---|---|---:|---:|
| 0 | Sensitive | 850 | 85% |
| 1 | Resistant | 150 | 15% |

The dataset is therefore imbalanced.

### 5. Data Preprocessing

The following preprocessing techniques are applied:

**Median Imputation**

Missing feature values are replaced with the median of the corresponding feature.

**Standardization**

The numerical features are standardized using `StandardScaler`.

**Prevention of Data Leakage**

Preprocessing and classification are combined in Scikit-learn pipelines.

Imputation and standardization parameters are learned only from the training portion of each cross-validation fold and then applied to its validation portion.

### 6. Machine Learning Models

Two classification algorithms are investigated:

**Logistic Regression**

A linear classification algorithm used to model the relationship between DNA methylation measurements and chemotherapy resistance.

**Random Forest**

An ensemble learning algorithm that combines multiple decision trees to perform classification.

### 7. Cross-Validation

Stratified five-fold cross-validation is used.

The dataset is divided into five folds:

- Four folds are used for training.
- One fold is used for validation.
- This process is repeated five times.

Stratification preserves approximately the same target-class proportions in each fold.

A fixed random seed is used to support reproducibility.

### 8. Model Evaluation

The primary evaluation metric is the **Area Under the Receiver Operating Characteristic Curve (ROC-AUC)**.

ROC-AUC measures how effectively a classifier distinguishes between the two target classes across different classification thresholds.

For each classifier, we calculate:

- ROC-AUC for every fold.
- Mean ROC-AUC.
- Standard deviation of ROC-AUC.

### 9. Statistical Comparison

A paired t-test is used as an exploratory statistical comparison of the fold-wise ROC-AUC scores.

The hypotheses are:

- Null hypothesis (H₀): There is no difference in mean ROC-AUC between the classifiers.
- Alternative hypothesis (H₁): There is a difference in mean ROC-AUC between the classifiers.

The significance level is set to 0.05.

The limitations of statistical testing with only five cross-validation folds are considered when interpreting the results, since the folds are not fully independent due to overlapping training sets.

### 10. Class-Imbalance Handling

The effect of class weighting is investigated using:

`class_weight="balanced"`

This option adjusts class weights according to their frequencies in the training data.

The original and class-weighted versions of both classifiers are compared using the same five-fold cross-validation strategy and ROC-AUC metric.

## Technologies and Libraries

The project uses Python and the following libraries:

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Pandas | Data loading and manipulation |
| NumPy | Numerical operations |
| Matplotlib | Data visualization |
| Seaborn | Statistical visualization |
| Scikit-learn | Preprocessing, classification and evaluation |
| SciPy | Statistical testing |
| Jupyter Notebook | Interactive analysis and experimentation |

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/salahhassani/chemoresistance-prediction.git
cd chemoresistance-prediction
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

**Windows PowerShell**

```powershell
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add the datasets

Place the two provided CSV files inside the `data/` directory:

```text
data/
├── methylation.csv
└── chemoresistance_labels.csv
```

The datasets are not included in the GitHub repository and must be obtained separately.

### 5. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
notebooks/model.ipynb
```

Run the notebook cells in their original order.

## Reproducibility

To support reproducibility:

- A fixed random seed (`42`) is used for randomized operations.
- Stratified five-fold cross-validation is used consistently.
- Scikit-learn pipelines prevent preprocessing leakage.
- The same validation folds are used when comparing model configurations.

## Assignment Deliverables

The assignment submission consists of:

1. A documented Jupyter Notebook (`.ipynb`) containing the analysis, preprocessing, model training, evaluation, and results.
2. A PDF export of the completed notebook.

Both files must follow the naming convention specified in the assignment and include all group members' names.

## Academic Context

**Course:** Introduction to Profile Areas – Data Science  
**University:** Freie Universität Berlin  
**Semester:** Winter Semester 2026/27  
**Assignment:** Assignment 3 – Predicting Chemotherapy Resistance from DNA Methylation Data

## Author

**GitHub:** [salahhassani](https://github.com/salahhassani)
