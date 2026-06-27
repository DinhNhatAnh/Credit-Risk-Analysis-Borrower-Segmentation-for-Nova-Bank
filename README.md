# Credit-Risk-Analysis-Borrower-Segmentation-for-Nova-Bank
## Project Overview
This project analyzes credit risk for **Nova Bank**, a financial institution providing **personal, medical, education, and business loans** across the **USA, UK, and Canada**.

The objective is to identify **which borrower segments are more likely to default**, understand the **main drivers of default**, and develop a **risk segmentation framework** to support better lending decisions.

This project combines:
- Exploratory Data Analysis (EDA)
- Credit Risk Analytics
- Business Intelligence Thinking
- Risk Segmentation
- Executive Reporting (McKinsey-style)

---

# Business Context

Nova Bank faces a fundamental lending challenge:

> How can the bank maximize loan growth while minimizing credit losses?

Approving too many high-risk borrowers increases:
- Loan defaults
- Credit losses
- Provision expenses
- Portfolio deterioration

However, overly strict approval policies may:
- Reduce revenue
- Lower loan growth
- Reject potentially profitable borrowers

Therefore, understanding borrower risk profiles is critical for improving underwriting and portfolio quality.

---

# Business Questions

This analysis aims to answer the following questions:

1. Which types of borrowers are more likely to default?
2. Do certain loan purposes carry higher risk?
3. How do loan-to-income and debt-to-income ratios affect repayment?
4. Does employment type or home ownership matter?
5. How do past defaults and credit history affect risk?
6. Are there differences between borrowers in the USA, UK, and Canada?
7. Which loan grades or terms are safer?
8. Can borrowers be segmented into safe vs risky groups?

---

# Dataset Overview

### Dataset Size
- **Rows:** 32,574 borrowers
- **Features:** 30+ variables

### Target Variable
`loan_status`
- 0 = Non-default
- 1 = Default

### Feature Categories

#### Borrower Demographics
- person_age
- gender
- marital_status
- education_level
- country
- state
- city

#### Financial Capacity
- person_income
- other_debt
- debt_to_income_ratio
- loan_to_income_ratio

#### Credit History
- cb_person_default_on_file
- cb_person_cred_hist_length
- past_delinquencies
- open_accounts
- credit_utilization_ratio

#### Loan Information
- loan_amnt
- loan_intent
- loan_grade
- loan_int_rate
- loan_term_months

#### Stability Indicators
- employment_type
- person_emp_length
- person_home_ownership

---

# Tech Stack

- **Python**
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook
- Power BI
---

# Analysis Framework

Data Cleaning → Univariate Overview → Bivariate → Multivariable Cross-tab → Risk Scoring → Insights & Recommendations

---

# Key Business Insights

## Safe Borrowers
Characteristics:
- High income
- Low DTI
- Grade A/B
- No prior default
- Own home / mortgage

Default rate:
**3.27%**

---

## High-Risk Borrowers
Characteristics:
- Low income
- DTI > 42%
- Grade D–G
- Previous default
- Rent
- Multiple delinquencies

Default rate:
**39.91%**

---

# Recommendations

Nova Bank should adopt risk-based lending policies.

## 1. Auto-Approve Safe Borrowers
Criteria:
- Grade A–B
- Low DTI
- Strong income

Benefits:
- Faster approval
- Better customer experience

---

## 2. Manual Review for Moderate Borrowers
Require:
- Additional income verification
- Debt assessment

---

## 3. Tighten Approval for High-Risk Borrowers
Red flags:
- Low income
- DTI > 42%
- Grade D–G

Actions:
- Reduce loan amount
- Increase pricing
- Require collateral

---

## 4. Build Early Warning System
Monitor:
- Rising DTI
- Delinquencies
- Credit utilization spikes

Purpose:
- Detect default risk earlier

---

# Dashboard Preview

([Add Power BI screenshots here](https://github.com/DinhNhatAnh/Credit-Risk-Analysis-Borrower-Segmentation-for-Nova-Bank/blob/main/Dashboard%20Credit%20Risk%20Analysis.pdf))

---

# Executive Summary

This project demonstrates that credit default is not driven by a single variable.

The strongest default risk occurs when multiple risk factors accumulate:

* Weak repayment capacity
* High leverage
* Poor credit history
* Weak loan quality

Final conclusion:

> Credit default is primarily driven by the accumulation of financial stress, poor credit behavior, and risky loan characteristics.

This analysis provides a practical framework for improving underwriting decisions and reducing portfolio losses.

---

# Repository Structure

```bash
credit-risk-analysis/
│
├── notebooks
├── dashboard
├── reports (pdf)
├── file final_report
├── README.md
```

