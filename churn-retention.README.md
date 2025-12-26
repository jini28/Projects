# Churn Prediction + Retention Recommendations

Predict which customers are likely to churn and generate a simple, actionable retention playbook based on churn risk and customer value.


## Project Overview

**Goal:**  
Build a binary classification model that estimates the probability a customer will churn, then convert those predictions into **risk buckets** and **retention actions** (e.g., “Call + targeted offer” vs. “Email + self-serve support”).

**Why it matters:**  
Churn is expensive. A model is only useful if it helps a team decide **who to contact** and **what to do** to reduce churn within budget.

---

## Data

This project is designed for the classic **Telco Customer Churn** dataset.

 columns include:
- Customer plan and account info (contract type, payment method, etc.)
- Usage/tenure (e.g., `tenure`)
- Charges (e.g., `MonthlyCharges`, `TotalCharges`)
- Target label: `Churn` (Yes/No)

---

## Approach

### 1) Exploratory Data Analysis (EDA)
- Check churn rate (class imbalance)
- Inspect missing values and data types
- Visualize churn patterns across:
  - contract type
  - tenure
  - monthly charges
  - add-on services

### 2) Preprocessing
- Numeric: impute missing values (median) + scale
- Categorical: impute missing values (most frequent) + one-hot encode
- Train/test split with stratification

### 3) Modeling
Baseline model:
- Logistic Regression (`class_weight="balanced"`)


### 4) Evaluation
Report:
- **ROC-AUC**
- **PR-AUC** (important for imbalanced churn)
- Confusion matrix + classification report
- Threshold discussion (0.5 vs. business-driven threshold)

### 5) Retention Recommendations (Decision Layer)
Convert churn probabilities into:
- **Risk buckets**: High / Medium / Low (based on percentiles)
- **Value proxy**: use `MonthlyCharges` (or `TotalCharges`) as a rough customer value signal
- **Recommended actions** based on risk + value

Example logic:
- High risk + high value → “Call + targeted offer”
- High risk + low value → “Email + save script”
- Medium risk → “Check-in + education”
- Low risk → “No action”

---

## Repository Structure

