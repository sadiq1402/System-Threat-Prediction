# 🛡️ System Threat Forecaster - Malware Prediction

> **Capstone Project for IIT Madras Diploma in Data Science and Applications**

This project aims to predict whether a system is infected by malware using telemetry data collected from antivirus software and system properties. The dataset includes machine-specific attributes such as OS version, hardware specs, real-time protection status, and more. Machine learning models are trained to classify systems as either **malicious (1)** or **benign (0)**.

---

## 📌 Problem Statement

You're given telemetry data from multiple systems with various features like:
- Installed antivirus products
- Operating system details
- Hardware specifications
- Real-time protection state
- And more

The goal is to **predict whether each system is infected by malware** using these features.

---

## 📁 Dataset Overview

### Files Included:

| File | Description |
|------|-------------|
| `train.csv` | Training data with 100,000 rows and 76 columns including the target variable |
| `test.csv` | Test data with 10,000 rows and 75 columns (no target) |

### Key Columns:

| Column Name | Description |
|------------|-------------|
| `MachineID` | Unique identifier for each machine |
| `ProductName`, `EngineVersion`, etc. | Antivirus-related info |
| `RealTimeProtectionState`, `IsPassiveModeEnabled` | Security settings |
| `OSBuildNumber`, `TotalPhysicalRAMMB`, etc. | OS & hardware properties |
| `DateAS`, `DateOS` | Timestamps for AV signature and OS install |
| `target` | Binary label: 1 if infected, 0 otherwise |

---

## 🧪 Exploratory Data Analysis (EDA)

- **Target Distribution**: Nearly balanced — ~50.5% class 1 (infected), ~49.5% class 0.
- **Missing Values**: Present in both numerical and categorical features.
- **Skewness & Outliers**: Many numerical features showed skewness and outliers, handled via median imputation and scaling.
- **Feature Correlation**: Point-biserial correlation identified several moderately predictive features.
- **Chi-Square Tests**: Identified significant relationships between categorical features and the target.

---

## 🔧 Feature Engineering

- Dropped `MachineID` as it was not informative.
- Extracted year/month/day from `DateAS` and `DateOS`.
- Imputed missing values in numerical features using median.
- Encoded categorical variables using:
  - One-Hot Encoding for low-cardinality features
  - Target Encoding for high-cardinality features
- Removed constant and low-importance features through statistical analysis.

---

## 🤖 Models Implemented

Several models were trained and evaluated:

| Model | Accuracy |
|------|----------|
| Logistic Regression | 0.62705 |
| Random Forest | 0.62615 |
| XGBoost (Baseline) | 0.6352 |
| ✅ **Tuned XGBoost** | **0.64195** |

### Tuned XGBoost Parameters:
```python
{
    'learning_rate': 0.1,
    'max_depth': 6,
    'n_estimators': 200,
    'subsample': 0.8
}
```

### Classification Report (Tuned XGBoost):
```
              precision    recall  f1-score   support

           0       0.65      0.60      0.62      9895
           1       0.64      0.69      0.66     10105

    accuracy                           0.64     20000
   macro avg       0.64      0.64      0.64     20000
weighted avg       0.64      0.64      0.64     20000
```

---

## 📈 Key Insights

Top Predictive Features:
- `SignatureVersion`
- `RealTimeProtectionState`
- `OSBuildNumber`
- `TotalPhysicalRAMMB`
- `AntivirusConfigID`

These insights suggest that **up-to-date antivirus signatures**, **real-time protection**, and **system configuration** play critical roles in preventing malware infections.

---

## 📈 Future Work

- Incorporate **temporal patterns** using time-series features
- Use **deep learning** for feature extraction from raw telemetry
- Build an **ensemble model** combining XGBoost, LightGBM, and others
- Add **model explainability** using SHAP or LIME
- Deploy the model as an API for real-time inference

---

## 👥 Contributors

- **Md Sadiq Hasan Ansari** – *Data Science Student*
- **IIT Madras Data Science Program** – *Academic Support*
