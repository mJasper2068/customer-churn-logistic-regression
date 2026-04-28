# Customer Churn Prediction (Logistic Regression)

## Overview

This project builds a churn prediction model using a Kaggle Customer Churn dataset (440,833 records).  
The goal is to identify customers at risk of leaving and reduce business loss through better decision-making.

Each missed churner is assumed to cost $100, making recall (catching churners) more important than raw accuracy.

---

## Objective

Predict whether a customer will:
- Stay (0)
- Churn (1)

and optimize model decisions based on **business cost**, not just accuracy.

---

## Approach

- Selected 10 relevant features
- Handled missing values
- Encoded categorical variables
- Split data into train/test sets
- Trained Logistic Regression model
- Tuned hyperparameter `C`
- Evaluated using confusion matrix
- Applied threshold tuning for cost optimization

---

## Model

Logistic Regression was used as the baseline model.

Multiple `C` values were tested:
- All produced similar test performance
- **C = 0.01** was selected to keep the model simple and reduce overfitting risk

---

## Threshold Tuning (Key Insight)

The default threshold of 0.50 is not optimal for business.

Different probability thresholds were evaluated using a cost function:
- False Negative (missed churner) = $100
- False Positive (false alarm) = $5

**Selected Threshold: 0.20**

### Cost Breakdown by Threshold

| Threshold | FN | FP | FN Cost ($100) | FP Cost ($5) | Total Cost |
|-----------:|------:|------:|---------------:|-------------:|-----------:|
| 0.40 | 5,560 | 6,874 | 556,000 | 34,370 | 590,370 |
| 0.35 | 4,786 | 8,289 | 478,600 | 41,940 | 520,540 |
| 0.30 | 4,099 | 9,973 | 409,900 | 49,865 | 459,765 |
| 0.25 | 3,416 | 12,043 | 341,600 | 60,215 | 401,815 |
| 0.20 | 2,751 | 14,743 | 275,100 | 73,715 | 348,815 |
| 0.15 | 2,081 | 18,473 | 208,100 | 92,365 | 300,465 |
| 0.10 | 1,322 | 23,544 | 132,200 | 117,720 | 249,920 |
| 0.05 | 567 | 31,765 | 56,700 | 158,825 | 215,525 |

Although 0.05 produces the lowest total cost, it results in a very high number of false positives (31,765), which may not be operationally practical.  
Therefore, 0.20 was selected as the optimal balance between cost reduction and actionable workload.

---

## Business Application

This model is designed to support retention decisions.

Instead of using predictions for reporting, the model is used to **drive action**:

- Customers with predicted churn probability ≥ 0.20 are flagged
- Retention strategies (discounts, outreach) are applied to these customers

This ensures that resources are focused on high-risk customers while controlling operational cost.

---

## Decision Rule

> Customers with predicted churn probability ≥ 0.20 are targeted for retention action

---

## Sample Output

| Customer ID | Churn Probability | Decision |
|------------|------------------|----------|
| 10231      | 0.78             | Act      |
| 20455      | 0.65             | Act      |
| 30912      | 0.18             | Ignore   |
