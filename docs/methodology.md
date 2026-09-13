# Methodology

## Project context

This repository documents a group project completed for the Business Analytics course at Universität Trier in 2026.

The project uses the Open e-commerce 1.0 dataset, which links crowdsourced U.S. Amazon purchase histories with survey-based customer characteristics.

## Analytical scope

The raw data contained a small number of observations after 2022. Because later coverage was incomplete, the primary descriptive and predictive analyses used complete observations from 1 January 2018 through 31 December 2022.

## Part A: Descriptive analytics

Part A analyses purchase-record value, product categories, customer demographics, geographic patterns, and time patterns.

Purchase-record value is calculated as:

$$
\text{Purchase-record value} =
\text{Purchase Price Per Unit} \times
\text{Quantity}
$$

The project uses “purchase-record value” rather than “average order value” because the data do not provide a reliable basket-level checkout identifier.

## Part B: Predictive analytics

Part B predicts whether a customer becomes a high-value future spender.

| Component | Definition |
|---|---|
| Feature period | 1 January 2018–31 December 2020 |
| Outcome period | 1 January 2021–31 December 2022 |
| Unit of analysis | One customer identified by Survey ResponseID |
| High-value target | Top 25% of future spenders |
| High-value threshold | Future spending ≥ $5,908.16 |

Historical purchase features include Recency, Frequency, Monetary value, category diversity, purchasing intensity, active purchase months, purchase regularity, and customer tenure.

## Machine-learning procedure

1. Aggregate historical purchase records to one customer-level row.
2. Create a future high-value target using 2021–2022 spending.
3. Split customers into 80% training and 20% testing data using stratified sampling.
4. Impute numerical variables with medians and categorical variables with the most frequent category.
5. Standardise numerical features and one-hot encode categorical features inside a scikit-learn pipeline.
6. Compare Dummy Baseline, Logistic Regression, Decision Tree, Random Forest, and Gradient Boosting.
7. Tune Gradient Boosting using GridSearchCV and stratified cross-validation on training data only.
8. Evaluate the final model once on the untouched test set.
