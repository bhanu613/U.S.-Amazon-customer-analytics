# Results Summary

## Part A: Descriptive findings

- Purchase-record value is strongly right-skewed: most purchases are low value, while a small number of high-value purchases create a long right tail.
- ABIS_BOOK is the highest-revenue original product category in the analysed sample.
- Groceries & Food is the most frequently purchased interpretable aggregated category.
- The $100,000–$149,999 income group produces the highest aggregate purchase-record value.
- Customers aged 25–34 produce the highest aggregate age-group purchase-record value.
- California is the highest-revenue shipping state in the analysed sample.
- Monthly purchase-record value changes over time, with a visible rise around late 2021.

## Part B: Predictive findings

- The final customer-level modelling dataset contains 4,882 customers.
- The high-value target identifies 1,221 customers, representing 25.01% of the modelling population.
- The high-value spending threshold is $5,908.16 during the 2021–2022 outcome period.
- Gradient Boosting is the strongest tested model.
- Tuned Gradient Boosting achieved ROC-AUC of 0.920 on the untouched test set.
- At the default 0.50 decision threshold, the final model achieved:
  - Accuracy: 0.874
  - Precision: 0.764
  - Recall: 0.717
  - F1-score: 0.740
- The top predicted-probability decile had a 94.90% observed high-value rate, compared with 24.97% overall, representing 3.80× lift.

## Interpretation

Historical purchase behaviour provides more predictive information than demographics alone. Demographic variables add incremental value when combined with behavioural features, but should be used carefully and monitored for fairness.

## Limitations

- The dataset is a volunteer crowdsourced sample and does not represent all Amazon customers.
- Results are predictive associations, not causal claims.
- Purchase-record value is not confirmed basket-level checkout value.
- The model estimates high-value status during a defined future period; it does not estimate full customer lifetime value.
