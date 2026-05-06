# XAI Credit Risk Prediction System
### MSc Dissertation — Leeds Beckett University, 2026

**Student:** Abdul Rauf | **Student ID:** 77575960
**Supervisor:** Mark Dixon | **Programme:** MSc Information Technology

---

## Project Overview

This project develops an **Explainable AI (XAI) enhanced credit risk modelling framework** for sustainable financial decision-making. Using the **German Credit (Statlog) dataset** from the UCI Machine Learning Repository, it builds a transparent, audit-ready risk prediction system that addresses the core tension between model accuracy and interpretability in regulated financial environments.

The framework is fully aligned with regulatory requirements including **GDPR Article 22**, the **EU AI Act**, and the **Sustainable Finance Disclosure Regulation (SFDR)**.

---

## Key Results

| Metric | Value |
|---|---|
| AUC-ROC (test set, n=200) | **0.812** |
| Brier Score (calibration) | **0.143** |
| High-Risk Recall | **71.7%** |
| High-Risk Precision | **68.2%** |
| F1 Score (High-Risk) | **69.9%** |
| Best CV AUC-ROC (Optuna) | **0.8314** |
| Top Risk Driver (SHAP) | **Checking status (0.3214)** |

---

## Repository Contents

```
xai-risk-modelling-dissertation/
│
├── XAI_RISK_MODELING.ipynb     # Complete project notebook (all pipeline stages)
└── README.md                   # This file
```

### What the Notebook Contains (15 cells)

| Stage | Description |
|---|---|
| Data Loading | German Credit dataset loaded from UCI, class balance confirmed (70:30) |
| Imputation | Median imputation (numerical), most-frequent imputation (categorical) |
| Train/Test Split | 80/20 stratified split — preprocessor fitted on training data only |
| Preprocessing Pipeline | StandardScaler + OneHotEncoder via ColumnTransformer |
| SMOTE Resampling | Class balance corrected from 70:30 → 50:50 (k=5 neighbours) |
| Optuna Optimisation | 50 Bayesian HPO trials (TPE sampler), 5-fold stratified CV |
| XGBoost Training | Trained with best Optuna hyperparameters |
| SHAP Explainability | TreeExplainer — exact Shapley values (global + local) |
| LIME Cross-Validation | Spearman rank correlation vs. SHAP to confirm robustness |
| Fairness Evaluation | DPD and EOD metrics on protected attributes (age, personal status) |
| Dash Dashboard | Interactive XAI Credit Risk Dashboard with live ngrok tunnel |

---

## Methodology

### Dataset
- **Source:** UCI Machine Learning Repository — German Credit (Statlog)
- **Size:** 1,000 applicant records, 20 features
- **Target:** Binary — Low Risk (0) / High Risk (1)
- **Class imbalance:** 70% low-risk / 30% high-risk → corrected with SMOTE

### Preprocessing Pipeline
- Median imputation for numerical features; most-frequent for categorical
- One-Hot Encoding for nominal features
- StandardScaler normalisation
- All transformations fitted on training data only (no data leakage)
- SMOTE with k=5 neighbours → balanced 50:50 training distribution

### Model — XGBoost + Optuna
- Bayesian hyperparameter optimisation via Optuna (Tree-structured Parzen Estimator)
- 50 trials, 5-fold stratified cross-validation
- Best CV AUC-ROC: **0.8314**
- Key hyperparameters: `learning_rate=0.0842`, `max_depth=6`, `reg_lambda=3.217`

### XAI Framework — SHAP + LIME
- **SHAP TreeExplainer** — mathematically exact Shapley values (not approximations)
- **Global explanation** — beeswarm plot across all test instances
- **Local explanation** — waterfall plot for highest-risk individual applicant
- **LIME cross-validation** — Spearman rank correlation ≥ 0.70 confirms robustness
- **Fairness metrics** — Demographic Parity Difference (DPD) + Equal Opportunity Difference (EOD)

---

## SHAP Global Feature Importance (Top 5)

| Rank | Feature | Mean \|SHAP\| |
|---|---|---|
| 1 | Checking status | 0.3214 |
| 2 | Loan duration | 0.2510 |
| 3 | Credit history | 0.2120 |
| 4 | Credit amount | 0.1768 |
| 5 | Savings status | 0.1479 |

> ⚠️ **Age** (SHAP = 0.1631) is flagged as a protected attribute requiring fairness review before any live deployment.

---

## How to Run

### Option 1 — Google Colab (Recommended)
1. Open [Google Colab](https://colab.research.google.com)
2. Click **File → Upload notebook** → upload `XAI_RISK_MODELING.ipynb`
3. Run all cells from top to bottom (**Runtime → Run all**)
4. The Dash dashboard will launch with a public ngrok URL in the final cell

> **Note:** For the ngrok tunnel (final cell) to work, add your `NGROK_AUTH_TOKEN` to Colab Secrets. A free ngrok account is available at [ngrok.com](https://ngrok.com). Without a token the dashboard still runs locally on port 8050.

### Option 2 — Jupyter Notebook (Local)
```bash
# Install dependencies
pip install pandas numpy scikit-learn imbalanced-learn xgboost optuna shap lime dash dash-bootstrap-components plotly pyngrok

# Launch notebook
jupyter notebook XAI_RISK_MODELING.ipynb
```
Run all cells from top to bottom.

---

## Dependencies

| Library | Purpose |
|---|---|
| `pandas`, `numpy` | Data loading and manipulation |
| `scikit-learn` | Preprocessing, train/test split, evaluation metrics |
| `imbalanced-learn` | SMOTE resampling |
| `xgboost` | XGBoost classifier |
| `optuna` | Bayesian hyperparameter optimisation |
| `shap` | SHAP explainability (TreeExplainer) |
| `lime` | LIME local explanations |
| `dash`, `dash-bootstrap-components` | Interactive dashboard |
| `plotly` | Visualisation |
| `pyngrok` | Public tunnel for Colab dashboard |

---

## Regulatory Alignment

| Regulation | How This Framework Addresses It |
|---|---|
| GDPR Article 22 | Local SHAP waterfall plots provide individual-level explanations for automated decisions |
| EU AI Act | Post-hoc XAI ensures model transparency and auditability |
| SFDR | Fairness evaluation (DPD/EOD) supports ESG-aligned, non-discriminatory credit decisions |
| EBA Guidelines | Global SHAP beeswarm enables portfolio-wide model behaviour audit |

---

## Demo Video

📺 Full dissertation demo video available on YouTube:
**[https://youtu.be/-88bbS4TzZw](https://youtu.be/-88bbS4TzZw)**

---

## Academic Context

- **Dissertation Title:** Risk Modeling Analysis with Explainable AI for Sustainable Financial Sectors
- **Programme:** MSc Information Technology
- **Institution:** Leeds Beckett University, School of Built Environment, Engineering and Computing
- **Supervisor:** Mark Dixon
- **Submission:** May 2026
