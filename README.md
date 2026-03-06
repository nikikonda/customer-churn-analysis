# Telco Customer Churn Prediction
### Predictive Analytics & Business Strategy | Python | Logistic Regression

**Niki Konda** — Business Analytics, University of Ljubljana | March 2026

---

## Project Summary

| | |
|---|---|
| **Dataset** | IBM Telco Customer Churn — 7,032 customers, 21 variables |
| **Problem** | Predict which customers will cancel their service before they do |
| **Model** | Logistic Regression with adjusted classification threshold |
| **Recall** | 76% — model correctly identifies 3 in 4 churners |
| **Tools** | Python, Pandas, Scikit-learn, Seaborn, Matplotlib |

---

## Business Problem

A telecommunications company is losing ~26.6% of its customers annually. Acquiring a new customer costs 5–7x more than retaining an existing one. This project builds a predictive model that enables the retention team to identify at-risk customers **before** they cancel, enabling targeted intervention.

**The decision this model supports:** Which customers should the retention team contact this month, and how should limited retention budget be prioritised?

---

## Key Findings from EDA

### 1. Contract Type is the Strongest Categorical Predictor
Month-to-month customers churn at dramatically higher rates than annual or two-year contract customers. The reason is **switching friction** — month-to-month customers can cancel with zero financial penalty.

### 2. The First 3 Months Are Critical
Churn is heavily concentrated in customers with 1–10 months tenure. Customers who survive the initial period become significantly more loyal. This defines where retention investment has the highest ROI.

### 3. Fiber Optic Has a Service Quality Problem
Fiber Optic customers — the company's most expensive segment — have the highest churn rate. Nearly 1 in 2 Fiber Optic customers churned. Combined with higher monthly charges (~80 EUR median vs ~65 EUR for retained customers), this signals a value-for-money or quality problem.

---

## Model Performance

| Metric | Default Threshold (0.5) | Adjusted Threshold (0.3) |
|---|---|---|
| Recall (churners) | 0.52 | **0.76** |
| Precision (churners) | 0.62 | 0.53 |
| Accuracy | 0.79 | 0.75 |

**Why threshold was lowered to 0.3:** In churn prediction, a False Negative (missing a churner) is more costly than a False Positive (flagging a loyal customer). Lowering the threshold increases recall at the cost of precision — a deliberate, business-justified trade-off.

### Confusion Matrix (Threshold 0.3)
```
                  Predicted Stayed    Predicted Churned
Actual Stayed          776                  257  ← false positives (unnecessary offers)
Actual Churned          88  ← missed         286  ← correctly flagged
```

---

## Top Churn Drivers (Feature Importance)

**Increases churn risk (red flags):**
- `InternetService_Fiber optic` — strongest service-level risk driver
- `Contract_Month-to-month` — no exit barrier
- `OnlineSecurity_No` — lack of protective add-ons
- `TechSupport_No` — no ongoing support relationship
- `PaymentMethod_Electronic check` — less committed payment method

**Decreases churn risk (protective factors):**
- `tenure` — strongest overall protective factor
- `Contract_Two year` — high switching friction
- `InternetService_DSL` — more stable than Fiber Optic

---

## Business Recommendations

**Priority 1 — Convert month-to-month customers**
Offer 10–15% loyalty discount for upgrading to 12-month contracts. Target customers with 3–12 months tenure showing other risk signals.

**Priority 2 — Investigate Fiber Optic quality urgently**
Conduct NPS survey and service audit for Fiber Optic segment before any retention campaign. The problem may be product quality, not price.

**Priority 3 — Structured onboarding for new customers**
Welcome call at day 7, satisfaction check at day 30, personalised bundle offer at day 60. The first 3 months determine whether a customer stays long-term.

**Priority 4 — Bundle security add-ons for at-risk customers**
OnlineSecurity and TechSupport reduce churn. Offer these free or discounted to month-to-month Fiber Optic customers in their first year.

---

## Project Structure

```
telco-churn-analysis/
│
├── telco_churn_analysis.ipynb    # Full analysis notebook
├── README.md                     # This file
└── WA_Fn-UseC_-Telco-Customer-Churn.csv  # Dataset (from IBM/Kaggle)
```

---

## How to Run

```bash
# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn

# Open notebook
jupyter notebook telco_churn_analysis.ipynb
```

---

## Technical Glossary

| Term | Definition |
|---|---|
| **Churn** | Customer cancelling their service |
| **Recall** | Of all actual churners, % correctly identified by model |
| **Precision** | Of all flagged churners, % that actually churned |
| **False Negative** | Churner model missed — most costly error |
| **False Positive** | Loyal customer wrongly flagged — wasteful but recoverable |
| **Switching Friction** | How costly it is for a customer to leave |
| **CLV** | Customer Lifetime Value — total revenue expected before churn |
| **Classification Threshold** | Probability cut-off for predicting churn (set to 0.3) |

---

*Dataset source: IBM Telco Customer Churn via Kaggle*
