# Explainable Predictive Maintenance and Risk-Aware Decisions (AI4I 2020)

Failure-risk classifier for machining equipment that turns predicted probabilities into maintenance decisions: **predict → explain → decide**. Built February to March 2026, extending a simpler regression version from late 2024.

## What it does

- **Data:** UCI AI4I 2020 Predictive Maintenance dataset, 10,000 records, 3.39% machine failures (`ai4i2020.csv`).
- **Features:** physically motivated features (temperature difference, torque–speed power proxy, wear–load interaction). Identifiers and failure-mode labels are excluded to prevent target leakage.
- **Evaluation:** stratified 70/15/15 train/validation/test split. Hyperparameters and decision thresholds are chosen on validation data; the test set is scored once.
- **Models:** logistic regression, tuned Random Forest, HistGradientBoosting.
- **Decisions:** validation-chosen maintenance threshold, cost-aware threshold analysis, SHAP explanations, and risk bands with inspection flags.

## Results (test set)

| Model | ROC-AUC | PR-AUC |
|---|---|---|
| HistGradientBoosting | 0.991 | 0.911 |
| Random Forest (tuned) | 0.980 | 0.903 |
| Logistic Regression | 0.937 | 0.443 |

Moving the Random Forest threshold from 0.50 to 0.557 (chosen on validation data) raised test precision from 0.746 to 0.878 and F1 from 0.800 to 0.860, with recall 0.843.

A cost-optimal threshold (missed failure = 10 × false alarm) was best on validation data but cost more on the test set than the 0.557 threshold (95 vs. 86), so thresholds tuned on few failures need checking on new data.

## Files

| File | What it is |
|---|---|
| `AI4I_Explainable_Risk_Aware_Predictive_Maintenance_Final.ipynb` | Main notebook |
| `AI4I_Predictive_Maintenance_Lightweight_Extended.ipynb` | Lighter extended version (written for Google Colab) |
| `AI4I_Explainable_Risk_Aware_Predictive_Maintenance_Report.docx` | Project report |
| `ai4i2020.csv` | Dataset |

The trained model file (`.joblib`) is not included; running the main notebook recreates it.

## Scope

This project predicts failure risk for the current machine state and does not estimate remaining useful life. Temporal degradation, RUL and calibrated uncertainty are covered in [fd004-degradation-aware-rul](https://github.com/HemanthDadi1/fd004-degradation-aware-rul).

Dataset: S. Matzka, AI4I 2020 Predictive Maintenance Dataset, UCI Machine Learning Repository (CC BY 4.0).
