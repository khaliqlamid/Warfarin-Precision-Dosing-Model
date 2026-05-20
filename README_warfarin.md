# Warfarin Precision Dosing Model

A machine learning project that predicts personalised Warfarin doses from patient data, built with clinical interpretability as a core requirement alongside predictive accuracy.

**Author:** Khaliq Lamid

---

## What this project does

Warfarin prevents blood clots, but the margin between a safe dose and a harmful one is narrow. Too much and the patient bleeds; too little and clotting goes unchecked. The right dose differs considerably between patients depending on their age, weight, genetics, existing conditions, and other medications, which makes a one-size-fits-all approach inadequate.

Right now, finding the correct dose takes weeks of trial and error. During that period, patients carry real risk. This project builds a model that predicts each patient's stable maintenance dose from their clinical and genomic profile, with the goal of giving clinicians a better starting point.

But a prediction alone isn't enough. If a clinician can't follow the reasoning behind a dose recommendation, they won't act on it. So the project pairs the model with per-prediction explanations using LIME, and wraps it in a Gradio interface that shows what clinical use would actually look like.

## What's in this repo

- `Warfarin_Precision_Dosing_Model.ipynb` — the full notebook, with explanations for every decision made
- `data/` — five source CSV files covering patient demographics, outcomes, lifestyle, clinical data, and genomics
- `README.md` — this file

## How it works

1. **Data wrangling** — merging five separate clinical and genomic files on patient ID into a single table
2. **Exploratory analysis** — checking missing values, summary statistics, and categorical distributions across all sources
3. **Feature engineering** — calculating BMI from height and weight, grouping age into clinical bands (under 30, 30-50, 50-70, 70+), and log-transforming the therapeutic range variable to reduce skew
4. **Modelling** — training and comparing three regression models: Linear Regression, Random Forest, and XGBoost
5. **Evaluation** — MAE, RMSE, and R² across all three models
6. **Experiment tracking** — MLflow logs every run so model versions stay comparable and results are reproducible
7. **Interpretability** — LIME generates an explanation for each individual prediction, showing which features drove that specific dose recommendation
8. **Deployment prototype** — a Gradio interface simulates how the model would sit inside a clinical workflow

## Tools used

- Python 3
- pandas, NumPy
- scikit-learn (LinearRegression, RandomForestRegressor, train_test_split, metrics)
- XGBoost
- MLflow
- LIME
- Gradio

## Why interpretability matters here

Most ML projects treat explainability as optional. In a clinical setting it isn't. A clinician won't act on a dose recommendation they can't verify, regardless of how well the model scores on MAE or R². LIME makes each prediction transparent; the clinician can see which features the model weighted and why, not just what number it produced.

## Limitations

- The dataset is synthetic rather than from a real clinical trial, so the results carry no clinical validation
- Both Random Forest and XGBoost ran on default hyperparameters; tuning either could shift the performance comparison
- The Gradio prototype is a demonstration only; actual clinical deployment needs regulatory approval, EHR integration, and validation at a scale this project doesn't attempt

## Reflection

The clearest takeaway from this project is that accuracy isn't the finish line in healthcare data science. A model a clinician can't interpret won't get used, no matter how well it performs on a test set. LIME and the Gradio prototype were both built with that in mind.
