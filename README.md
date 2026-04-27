This project uses the Kaggle dataset "Customer Churn Dataset" with a total of 440,833 entries and applies Logistic Regression as the model. It uses 10 features with Churn as the target to identify customers who are at risk of leaving the company.

The goal of the model is to predict whether a customer will churn or stay, as for this project, each lost customer is assumed to represent an estimated cost of $100.

The approach involved identifying features and target, handling missing values, and encoding categorical data for model training.

Logistic Regression was used as the base model, and hyperparameter tuning was applied to select the optimal C value. Out of the tested values, all produced similar test performance, so C = 0.01 was selected to reduce model complexity and minimize overfitting risk.

Threshold tuning was performed to optimize business outcomes. A threshold of 0.20 was selected because it significantly reduced total cost. Although false positives increased, the reduction in missed churners (FN) justified the trade-off and remained within an acceptable range.

The final model, using a threshold of 0.20, achieved a total cost of $348,815, compared to $590,370 at the baseline threshold of 0.40. This shows that reducing missed churners leads to greater overall savings despite an increase in false positives.

This project demonstrates that model decisions should be guided by business cost, not accuracy alone.