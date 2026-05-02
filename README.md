# XAI-Enhanced Risk Modelling for Sustainable Finance
**MSc Dissertation — Leeds Beckett University, 2026**
**Student:** Abdul Rauf

## Project Overview
This project builds an Explainable AI (XAI) credit risk prediction system 
using XGBoost, SHAP, LIME, and SMOTE on the German Credit (Statlog) dataset.

## Files
- `Product.ipynb` — Complete project notebook (preprocessing, training, SHAP/LIME explainability, evaluation)

## How to Run
1. Open in Google Colab or Jupyter Notebook
2. Run all cells from top to bottom
3. All dependencies are installed within the notebook

## Key Results
- AUC-ROC: 0.812
- Brier Score: 0.143
- Top risk driver: Checking account status (SHAP = 0.3214)
