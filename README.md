# Nova Bank Credit Risk Analysis & Machine Learning

> **Data Analyst Portfolio Project | Credit Risk, Exploratory Analysis & Predictive Modeling**

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4c72b0)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Machine%20Learning-F7931E?logo=scikit-learn)
![XGBoost](https://img.shields.io/badge/XGBoost-Machine%20Learning-EC6B3A)

## 1. Project Overview

Nova Bank needs to balance **loan growth with credit risk**. This project analyzes a personal-loan portfolio to understand the drivers of default and then moves from descriptive risk analysis to **Machine Learning prediction of `loan_status`**.

The project answers three questions:

1. **Which borrower and loan characteristics are associated with higher default risk?**
2. **Where are the clearest risk thresholds and high-risk combinations?**
3. **Can Machine Learning improve default prediction beyond a hand-crafted risk scorecard?**

### Analytical Flow

```text
Business Problem
      ↓
Data Cleaning & EDA
      ↓
Risk Driver & Interaction Analysis
      ↓
Heuristic Risk Scorecard
      ↓
Machine Learning Classification
      ↓
Model Evaluation & Comparison
      ↓
Risk-Based Lending Recommendations
```

> **Scope:** Analysis, visualization, and Machine Learning are performed entirely in **Jupyter Notebook using Python**. No Power BI is included.

---

## 2. Business Context

Nova Bank serves borrowers across the **USA, UK, and Canada** through multiple lending products. The business objective is to balance:

**Loan Growth ↔ Credit Risk ↔ Customer Experience**

The portfolio contains **32,581 records and 29 variables** before cleaning, with an observed default rate of approximately **21.8%**.

The analysis focuses on identifying high-risk borrower segments, understanding the main drivers of default, and developing a predictive framework to support more risk-aware lending decisions.

---

## 3. Data Preparation

The notebook performs data-quality checks and preprocessing before analysis and modeling:

- Remove logically impossible age and employment-length records
- Remove redundant `loan_percent_income` because it duplicates `loan_to_income_ratio`
- Impute missing `loan_int_rate` using the median within `loan_grade`
- Fill missing employment length with `0`
- Encode the target as default / non-default
- Standardize numeric features for Logistic Regression
- Encode categorical variables using `OrdinalEncoder`

After cleaning, the dataset contains **32,574 observations with no remaining missing values**.

---

## 4. Exploratory Risk Analysis

The EDA evaluates default risk across:

- Loan Grade
- Interest Rate
- Loan-to-Income Ratio (LTI)
- Income
- Debt-to-Income Ratio (DTI)
- Home Ownership
- Prior Default
- Loan Intent
- Geography

Both univariate/bivariate analysis and interaction analysis are used to identify **risk concentration and actionable thresholds**.

---

# 5. Key Business Findings

## 5.1 Loan Grade is the strongest risk boundary

Default Rate increases sharply from **20.7% for Grade C to 59.0% for Grade D**, while Grades D–G reach approximately **59–98% Default Rate**.

**Business implication:** Grade D+ represents a critical risk zone and should trigger materially tighter underwriting controls.

## 5.2 Affordability is a critical risk driver

Default Rate rises sharply when **LTI crosses 30%**, increasing from **15.2% to 68.2%**. Income also shows a strong gradient, from **43.3% Default Rate for Low income to 9.1% for High income**.

However, income cannot fully offset poor credit quality; high-income borrowers with Grade D still show materially elevated default risk.

**Business implication:** affordability should be treated as a major risk modifier, with LTI >30% as a practical underwriting threshold.

## 5.3 Prior default and borrower combinations identify concentrated risk

Borrowers with prior default show approximately **2.05× higher default risk**. Interaction analysis also identifies extreme combinations such as **RENT + DTI >70%**, where observed Default Rate reaches approximately **77–100%** across interaction cells.

**Business implication:** targeted risk rules are preferable to applying blanket rejection policies across the entire portfolio.

---

# 6. From Risk Analysis to Machine Learning

The EDA explains **what drives default risk**. The next stage asks whether those patterns can be used to predict default at the **individual-loan level**.

The modeling dataset uses eight business-relevant features:

```text
loan_grade
loan_int_rate
loan_to_income_ratio
debt_to_income_ratio
person_income
person_home_ownership
cb_person_default_on_file
loan_intent
```

A **stratified 80/20 train-test split** is used so that both sets preserve the approximately **21.8% default rate**.

The project evaluates three ML approaches against the existing hand-crafted risk scorecard:

- Logistic Regression — interpretable baseline
- Random Forest — non-linear ensemble
- XGBoost — main predictive model

Because the target is imbalanced, XGBoost uses `scale_pos_weight` (approximately **3.58**) to give greater weight to the default class.

---

# 7. Machine Learning Results

| Model | AUC | Gini | Role |
|---|---:|---:|---|
| **Heuristic Scorecard** | 0.843 | 0.686 | Hand-crafted baseline |
| **Logistic Regression** | 0.841 | 0.682 | Interpretable baseline |
| **Random Forest** | 0.886 | 0.772 | Non-linear ensemble |
| **XGBoost** | **0.940** | **0.879** | Best predictive performance |

### XGBoost Classification Performance

| Class | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Non-default | 0.94 | 0.93 | 0.94 |
| **Default** | **0.77** | **0.78** | **0.78** |

Overall accuracy is approximately **90%**.

### Key ML Insights

**1. XGBoost delivers the strongest predictive performance**  
XGBoost achieves **AUC 0.940 / Gini 0.879**, outperforming Logistic Regression (0.841) and Random Forest (0.886).

**2. Machine Learning substantially improves default detection**  
At the notebook's 0.5 classification threshold, XGBoost captures **78% of actual defaults**, compared with **45% for Logistic Regression**. AUC is the preferred comparison for overall discrimination because it evaluates performance across thresholds.

**3. Non-linear modeling adds value beyond the heuristic scorecard**  
XGBoost improves AUC from **0.843** for the hand-crafted scorecard to **0.940**, indicating that the portfolio contains non-linear patterns that simple rule-based scoring does not fully capture.

**4. Random Forest performs below XGBoost in this setup**  
Random Forest reaches **0.886 AUC**, below XGBoost's **0.940**, under the notebook's selected hyperparameters (`max_features=2`, `max_depth=4`). This comparison supports XGBoost as the preferred model in the current experiment, while further tuning and validation would be appropriate before production use.

---

# 8. Business Interpretation

The Machine Learning stage adds a predictive layer to the earlier risk analysis:

```text
EDA
 ↓
Identify Risk Drivers
 ↓
Define Risk Thresholds
 ↓
Build Risk Scorecard
 ↓
Train Predictive Models
 ↓
XGBoost
 ↓
Individual Default Risk Prediction
```

The key shift is from:

> **“Which characteristics are associated with default?”**

to:

> **“How likely is this individual borrower to default?”**

This creates a stronger foundation for risk-based lending decisions.

---

# 9. Recommendations

## 3 Key Insights

### 1. Credit quality matters most
Loan Grade D+ represents the clearest risk boundary.

### 2. Affordability drives additional risk
LTI >30%, lower income, and high DTI are associated with substantially higher default risk.

### 3. Risk can be targeted rather than treated uniformly
Prior default and high-risk borrower combinations allow the bank to focus underwriting controls where risk is most concentrated.

## 4 Immediate Actions

| Rule | Condition | Recommended Action |
|---|---|---|
| **R1** | Grade D–G **AND** LTI ≥30% | Auto-decline / highest level of underwriting review |
| **R2** | RENT **AND** DTI >70% | Auto-decline |
| **R3** | Prior default = Yes | Mandatory manual review |
| **R4** | Interest rate >17% | Re-validate loan grade |

These rules are intended to focus underwriting resources on the highest-concentration risk zones while avoiding blanket rejection across the portfolio.

---

# 10. Long-Term Strategy — Risk-Based Lending

Move from one-size-fits-all lending toward a **Risk-Based Lending System** that combines model-predicted risk with differentiated approval and risk controls.

| Risk Tier | Lending Strategy |
|---|---|
| 🟢 **Safe** | Fast-track approval + preferred pricing |
| 🔵 **Moderate** | Standard approval + standard pricing |
| 🟠 **Risky** | Enhanced verification + tighter lending limits |
| 🔴 **High Risky** | Manual review + collateral / co-signer |

The preferred approach is **tiered intervention rather than blanket rejection**.

---

# 11. Tools & Libraries

- **Python**
- **Jupyter Notebook**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Scikit-learn**
- **XGBoost**

---

# 12. Project Structure

```text
nova-bank-credit-risk/
│
├── data/
│   └── loan_data.xlsx
│
├── notebooks/
│   └── Nova_Bank_Credit_Risk_Analysis.ipynb
│
├── images/
│   ├── eda/
│   ├── risk_analysis/
│   └── ml/
│
└── README.md
```

---

# 13. Final Takeaway

This project demonstrates an end-to-end approach to credit risk analytics:

> **Clean the data → Understand risk drivers → Identify thresholds → Build a risk score → Train predictive models → Evaluate performance → Translate results into lending decisions**

The strongest predictive result comes from **XGBoost (AUC 0.940, Gini 0.879)**, while the earlier EDA provides the business context needed to understand and act on the risk patterns.

### Final Recommendation

> **Use predictive modeling to complement—not replace—business-driven credit risk rules, combining individual default probabilities with risk-based underwriting policies.**

---

## Author

**Nhat Anh Dinh**  
Data Analyst Portfolio Project  
Finance & Banking → Data Analytics

**Focus:** Credit Risk Analysis · Python · Machine Learning · Business Analytics
