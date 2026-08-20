# Nova Bank Credit Risk Analysis

> **Data Analyst Portfolio Project | Credit Risk & Lending Analytics**

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Analysis-013243?logo=numpy)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557c)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4c72b0)

## 1. Project Overview

Credit risk is one of the most important challenges in lending: a bank needs to approve enough loans to support portfolio growth while controlling the probability and cost of default.

This project analyzes **Nova Bank's loan portfolio** to identify the key drivers of borrower default and translate the findings into actionable lending policies.

The analysis focuses on three questions:

1. **Who is most likely to default?**
2. **Which borrower and loan characteristics drive default risk?**
3. **How can the bank use these findings to improve lending decisions?**

### Analytical Flow

```text
Raw Loan Data
      ↓
Data Cleaning & Preparation
      ↓
Exploratory Data Analysis
      ↓
Risk Driver Analysis
      ↓
Risk Segmentation
      ↓
Business Recommendations
```

> **Scope:** Analysis and visualization are performed entirely in **Jupyter Notebook** using Python. No Power BI is included in this project.

---

## 2. Business Problem

Nova Bank provides personal, medical, education, and business loans across the **USA, UK, and Canada**.

The key business challenge is to balance:

**Loan Growth ↔ Credit Risk ↔ Customer Experience**

Approving too many high-risk borrowers can increase default losses, while overly conservative approval policies can reject potentially profitable customers.

Therefore, the objective is not simply to identify whether a borrower defaults, but to identify **risk thresholds and borrower segments that can support better lending decisions**.

---

## 3. Dataset

The dataset contains **32,574 loan applications/borrowers** and more than 30 borrower and loan-related variables.

| Category | Examples |
|---|---|
| Borrower profile | Age, income, employment length |
| Financial profile | Debt-to-income ratio, loan-to-income ratio |
| Credit profile | Credit history, prior default, loan grade |
| Loan characteristics | Loan amount, interest rate, loan intent, loan term |
| Ownership | Home ownership |
| Geography | Country |
| Target | `loan_status` |

The overall observed **Default Rate is 21.8%**.

---

## 4. Analytical Approach

### 4.1 Data Preparation

- Inspect dataset dimensions and data types
- Identify missing values and duplicates
- Check categorical value consistency
- Review numerical distributions and potential outliers
- Validate the target variable
- Create derived variables required for risk analysis
- Prepare risk segments and analytical bands

### 4.2 Exploratory Data Analysis

The analysis starts with portfolio-level questions:

- What is the overall Default Rate?
- How is the loan portfolio distributed across grades and borrower segments?
- Which borrower characteristics are associated with higher default?
- How does default vary across income, employment, and loan characteristics?
- Are there meaningful differences between Default and Non-Default populations?

### 4.3 Risk Driver Analysis

Key dimensions include:

- Loan Grade
- Interest Rate
- Loan-to-Income Ratio (LTI)
- Income
- Debt-to-Income Ratio (DTI)
- Home Ownership
- Prior Default
- Geography

Both **univariate/bivariate analysis** and **interaction analysis** are used to identify risk concentration and important thresholds.

---

# 5. Key Findings

## Finding 1 — Loan Grade is the strongest risk boundary

Loan Grade is the strongest categorical risk driver in the portfolio.

Default Rate increases sharply from:

**Grade C: 20.7% → Grade D: 59.0%**

Grades **D–G reach approximately 59–98% Default Rate**.

### Business implication

Grade D+ represents a critical risk zone. Standard approval rules should therefore be replaced with significantly tighter underwriting controls for these borrowers.

---

## Finding 2 — Borrower affordability is a critical risk driver

LTI shows one of the clearest quantitative thresholds in the analysis.

Default Rate increases from:

**15.2% → 68.2% when crossing the 30% LTI threshold.**

Default Rate also shows a strong income gradient:

**Low income: 43.3% → High income: 9.1%**

However, income cannot completely compensate for poor credit quality.

For example:

> High-income borrowers with Grade D still show a **38.2% Default Rate**.

### Business implication

Income should be treated as a **risk modifier rather than a rescue variable**, while LTI >30% should be considered a key underwriting threshold.

---

## Finding 3 — Prior default and borrower characteristics enable targeted controls

Borrowers with a prior default show approximately **2.05× higher default risk**.

Interaction analysis also identifies extreme risk concentrations. In particular:

> **RENT + DTI >70% → approximately 77–100% Default Rate** in observed interaction cells.

### Business implication

The bank can use these combinations to create **targeted underwriting rules**, instead of applying blanket rejection policies across the entire portfolio.

---

## Additional Findings

### Interest Rate

Interest rates above 14% are associated with approximately **50–68% Default Rate**.

High-rate loans should therefore be reviewed to determine whether the loan grade and pricing appropriately reflect observed risk.

### Geography

Geography contributes very little discriminatory value:

- USA: **21.86%**
- UK: **21.73%**
- Canada: **21.86%**

The spread is only **0.13 percentage points**.

**Business implication:** No country-specific underwriting policy is warranted based on the observed portfolio.

---

# 6. 3 Key Insights → 4 Immediate Actions → 1 Long-Term Strategy

## 3 Key Insights

### 1. Credit quality matters most
Loan Grade D+ marks the clearest risk boundary, with Default Rate increasing sharply from Grade C to Grade D.

### 2. Affordability drives additional risk
LTI >30%, low income, and high DTI identify borrowers with materially higher default risk.

### 3. Risk can be targeted rather than treated uniformly
Prior default and combinations such as RENT + DTI >70% allow the bank to identify concentrated risk zones and apply differentiated controls.

---

## 4 Immediate Actions

| Rule | Condition | Recommended Action | Rationale |
|---|---|---|---|
| **R1** | Grade D–G **AND** LTI ≥30% | **Auto-decline** | Observed DR reaches approximately 66–100% in the identified high-risk zone |
| **R2** | RENT **AND** DTI >70% | **Auto-decline** | Observed DR reaches approximately 77–100% across interaction cells |
| **R3** | Prior default = Yes | **Mandatory manual review** | Approximately 2.05× higher default risk |
| **R4** | Interest rate >17% | **Re-validate loan grade** | High-rate loans show approximately 50–68% DR |

These rules focus underwriting resources on the **highest-concentration risk zones** while avoiding blanket rejection of the entire portfolio.

---

# 7. Long-Term Strategy — Build a Risk-Based Lending System

The long-term objective is to evolve from static rule-based approval toward a **Risk-Based Lending System** that differentiates approval, pricing, and risk controls according to borrower risk.

| Risk Tier | Lending Strategy |
|---|---|
| 🟢 **Safe** | Fast-track approval + preferred pricing |
| 🔵 **Moderate** | Standard approval + standard pricing |
| 🟠 **Risky** | Enhanced verification + LTI cap at 25% + income documentation |
| 🔴 **High Risky** | Manual review + collateral / co-signer |

Importantly, **High Risky borrowers should not automatically be rejected**. Approximately **60% of High Risky borrowers do not default**, so blanket rejection could eliminate potentially good customers.

The recommended approach is therefore:

> **Tiered intervention rather than blanket rejection.**

### Long-Term Roadmap

```text
Risk Scorecard
      ↓
Portfolio Monitoring
      ↓
Quarterly Recalibration
      ↓
Explainable Predictive Model
      ↓
Behavioral Risk Signals
```

---

# 8. Analytical Outputs

### Portfolio Overview
- Overall Default Rate
- Portfolio composition
- Default Rate by Risk Segment
- Default Rate by Loan Grade

### Risk Driver Analysis
- Default Rate by income band
- Default Rate by LTI / DTI
- Default Rate by home ownership
- Default Rate by employment length
- Default Rate by interest rate band
- Default Rate by prior default status
- Geographic comparison

### Interaction Analysis
- Income × Loan Grade
- Home Ownership × DTI
- Other borrower/loan risk combinations

### Decision Support
- Risk segmentation
- High-risk threshold identification
- Risk-based lending recommendations
- Immediate underwriting rules

---

# 9. Tools & Libraries

| Tool | Purpose |
|---|---|
| **Python** | Main analysis language |
| **Jupyter Notebook** | Analysis, documentation, and visualization |
| **Pandas** | Data cleaning and manipulation |
| **NumPy** | Numerical analysis |
| **Matplotlib** | Data visualization |
| **Seaborn** | Statistical visualization |

> This project intentionally uses **Jupyter Notebook as the single analytical and visualization environment**.

---

# 10. Key Takeaway

The analysis shows that credit risk is **not evenly distributed across the portfolio**.

The strongest risk concentrations are associated with:

> **Poor Loan Grade + High Leverage + Adverse Credit History**

Rather than applying a single approval policy to all borrowers, Nova Bank can improve risk management by adopting a **risk-based lending approach**:

```text
Data
  ↓
Identify Risk Drivers
  ↓
Define Risk Thresholds
  ↓
Segment Borrowers
  ↓
Apply Tiered Lending Controls
  ↓
Monitor Portfolio Outcomes
  ↓
Continuously Improve
```

### Final Recommendation

> **Move from one-size-fits-all lending toward a Risk-Based Lending System that accelerates low-risk approvals while applying progressively stronger controls to high-risk borrowers.**

---

## Author

**Nhat Anh Dinh**  
Data Analyst Portfolio Project  
Finance & Banking → Data Analytics

**Focus:** Credit Risk Analysis · Python · Data Visualization · Business Analytics
