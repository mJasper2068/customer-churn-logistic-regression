# Customer Churn Prediction (Logistic Regression)

## Overview

This project builds a churn prediction model using a Kaggle Customer Churn dataset (440,833 records).  
The goal is to identify customers at risk of leaving and reduce business loss through better decision-making.

Each missed churner is assumed to cost **$100**, making recall (catching churners) more important than raw accuracy.

---

## Objective

Predict whether a customer will:
- Stay (0)
- Churn (1)

And optimize model decisions based on **business cost**, not just accuracy.

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
- **C = 0.01** was selected to reduce model complexity and avoid overfitting

---

## Threshold Tuning (Key Insight)

Default threshold (0.50) is not optimal for business.

We tested different thresholds and selected:

```text
Threshold = 0.20
