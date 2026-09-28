# GENOMIQ AI

## Intelligent Genomic Variant & Pathogenicity Intelligence Platform

GENOMIQ AI is an end-to-end research and education platform for exploring genomic variant data with machine learning, explainable AI, dimensionality reduction, clustering, and anomaly detection.

The application is designed as a portfolio-grade demonstration of how data science and machine learning can be applied to genomic feature analysis.

> **Important:** The included dataset is synthetic and the generated predictions are for research, learning, and demonstration purposes only. This project is not a clinical diagnostic system and must not be used to make medical decisions.

---

## Project Overview

GENOMIQ AI provides a workflow for analyzing variant-level genomic features such as:

- PrimateAI-3D
- SpliceAI
- PhyloP

The platform performs data validation, preprocessing, feature engineering, supervised learning, prediction, explainability, clustering, and anomaly detection through a browser-based Gradio interface.

---

## Key Features

### 1. Dataset Management

- Upload CSV or TSV genomic datasets.
- Preview uploaded data.
- Inspect data types.
- Calculate missing values and missing percentages.
- Count unique values.
- Detect duplicate rows.
- Generate descriptive statistics.

### 2. Feature Engineering

The platform creates additional analytical features from the core genomic predictors:

- `AI_Combined_Score`
- `Conservation_Risk`
- `Splicing_Risk`

Missing numeric values are handled using median imputation during model processing.

### 3. Machine Learning Model Comparison

GENOMIQ AI trains and compares multiple classification algorithms:

- Logistic Regression
- Random Forest
- XGBoost
- Support Vector Machine

The models are evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC

The model with the highest ROC-AUC on the held-out test set is selected for the interactive prediction workflow.

### 4. Variant Prediction

Users can enter individual variant feature values and obtain:

- Predicted class
- Pathogenicity probability
- Risk category
- Model used for the prediction

### 5. Bulk Prediction

The platform can process the loaded dataset and generate:

- Prediction
- Pathogenicity probability
- Risk category
- Model used

The resulting table can be downloaded as a CSV file.

### 6. PCA and K-Means Clustering

The platform applies:

- Standardization
- Principal Component Analysis (PCA)
- K-Means clustering

This provides a two-dimensional visualization of variant groups based on selected genomic features.

### 7. Anomaly Detection

Isolation Forest is used to identify unusual combinations of genomic feature values.

The output includes:

- Normal or anomalous classification
- Anomaly score

### 8. Explainable AI

The project includes SHAP-based model explainability for supported models and a feature-importance fallback where appropriate.

The explainability workflow helps investigate which input features contribute most strongly to model behavior.

---

## System Workflow

```text
Genomic Dataset
       |
       v
Data Validation
       |
       v
Missing Value Handling
       |
       v
Feature Engineering
       |
       v
Model Training
       |
       v
Model Comparison
       |
       v
Prediction and Probability
       |
       +--------------------+
       |                    |
       v                    v
SHAP Explainability   PCA + K-Means
       |
       v
Feature Interpretation
       |
       v
Isolation Forest
       |
       v
Anomaly Analysis
       |
       v
Interactive Gradio Interface
```

---

## Technology Stack

| Category | Technologies |
|---|---|
| Programming | Python |
| Data Processing | Pandas, NumPy |
| Machine Learning | Scikit-learn, XGBoost |
| Explainability | SHAP |
| Dimensionality Reduction | PCA |
| Clustering | K-Means |
| Anomaly Detection | Isolation Forest |
| Visualization | Plotly, Matplotlib |
| Interface | Gradio |
| Environment | Google Colab |

---

## Input Data

The demo dataset contains fields such as:

```text
Chromosome
Position
Gene
REF
ALT
HGVSP
PrimateAI-3D
SpliceAI
PhyloP
Target
```

For a real dataset, the core numerical features expected by the current pipeline are:

```text
PrimateAI-3D
SpliceAI
PhyloP
```

If a recognized target column is not present, the demo pipeline can construct a learning target from the available feature values. For real research use, a validated target definition should be supplied instead of relying on an automatically generated target.

---

## Project Structure

```text
GENOMIQ-AI/
│
├── data/
│   └── demo_variants.csv
│
├── outputs/
│   ├── model_comparison.csv
│   ├── genomiq_predictions.csv
│   ├── shap_summary.png
│   └── feature_importance.html
│
├── app.py
├── README.md
└── requirements.txt
```

The Google Colab one-cell version can also create the project directories automatically under:

```text
/content/GENOMIQ-AI
```

---

## Installation

### Google Colab

Open a new Google Colab notebook and run the complete one-cell project code.

The notebook installs the required packages automatically.

### Local Python Environment

Create a virtual environment and install dependencies:

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

Activate it on Linux or macOS:

```bash
source .venv/bin/activate
```

Install packages:

```bash
pip install -r requirements.txt
```

---

## Running the Application

### Google Colab

Run the full notebook cell. Gradio will create a public temporary URL.

### Local

Run:

```bash
python app.py
```

Then open the local URL shown by Gradio.

---

## Using the Dashboard

### Dataset

1. Upload a CSV or TSV file.
2. Click **Load Dataset**.
3. Review the preview, audit, statistics, and summary.

### Model Training

1. Open **Model Training**.
2. Click **Train and Compare Models**.
3. Review the evaluation metrics.
4. The best available model is stored for subsequent prediction tasks.

### Variant Analysis

Enter values for:

```text
PrimateAI-3D
SpliceAI
PhyloP
```

Then run the variant analysis workflow.

### Bulk Predictions

Generate predictions for the complete loaded dataset and download the generated CSV.

### PCA and K-Means

Run the clustering workflow to visualize variants in a two-dimensional PCA space and inspect cluster assignments.

### Anomaly Detection

Run Isolation Forest to identify unusual feature combinations.

### Explainable AI

Generate a SHAP or feature-importance output to investigate model behavior.

---

## Model Evaluation

The project uses a held-out test set for model comparison. The primary selection metric in the current implementation is ROC-AUC.

Example evaluation table:

```text
Model                  Accuracy   Precision   Recall   F1   ROC-AUC
Logistic Regression    ...        ...         ...      ...  ...
Random Forest          ...        ...         ...      ...  ...
XGBoost                ...        ...         ...      ...  ...
Support Vector Machine ...        ...         ...      ...  ...
```

Actual values depend on the dataset and random split used during execution.

---

## Limitations

This project is a demonstration platform and has several limitations that should be considered before using it for research beyond exploration:

1. The bundled dataset is synthetic.
2. Synthetic labels do not represent validated clinical annotations.
3. The current pipeline uses a limited feature set.
4. The default train/test split is not a substitute for external validation.
5. Model probabilities should not be interpreted as calibrated clinical probabilities.
6. The project does not implement full ACMG/AMP clinical variant classification.
7. Population bias, dataset shift, feature leakage, and annotation quality require dedicated investigation with real datasets.
8. Clinical interpretation requires validated databases, domain expertise, and appropriate review processes.

---

## Future Improvements

Potential extensions include:

- Integration with ClinVar annotations.
- ACMG/AMP rule-aware evidence processing.
- Additional genomic predictors.
- Cross-validation and nested cross-validation.
- Probability calibration.
- External validation datasets.
- Patient-level multi-variant analysis.
- Interactive SHAP dependence and force plots.
- FastAPI backend integration.
- PostgreSQL storage.
- Authentication and user management.
- Docker-based deployment.
- Cloud deployment on Google Cloud.
- Model versioning and experiment tracking.
- Data and model monitoring.

---

## Research Use

GENOMIQ AI is intended to demonstrate the intersection of:

```text
Bioinformatics
      +
Machine Learning
      +
Explainable AI
      +
Data Visualization
      +
Unsupervised Learning
      +
Anomaly Detection
```

It can be used as a portfolio project, educational prototype, or starting point for further genomic data science research.

---

## Author

**Khushi Kumari**

Interests: Bioinformatics, Machine Learning, Data Science, Computational Biology, Explainable AI

---

## License

This project is intended for educational and research demonstration purposes. Add an appropriate open-source license if you plan to distribute or publish the project publicly.
