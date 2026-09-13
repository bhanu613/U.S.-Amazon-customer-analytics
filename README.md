# U.S. Amazon Customer Value Analytics

End-to-end descriptive and predictive analytics project using Amazon purchase histories linked to customer survey characteristics.

> **Academic group project** completed for the Business Analytics course at Universität Trier, 2026.

## Open in Google Colab

The complete notebooks can be viewed and run directly in Google Colab:

- [Part A – Descriptive Analysis and Exploratory Data Analysis](https://colab.research.google.com/drive/1YXCUxXSQ_W71Vx3GyPSXyuCuENs0r_BR?usp=sharing)
- [Part B – Predictive High-Value Customer Classification](https://colab.research.google.com/drive/1JjahOhfyc0C_Xqs6W6Zg2eIOHqIGBqjD?usp=sharing)

> The Part A notebook contains the complete descriptive analysis, including data cleaning, transaction-value distribution analysis, customer-segment analysis, geographic patterns, temporal patterns, and the interactive dashboard.  
>
> The Part B notebook contains the customer-level predictive modelling pipeline, model comparison, Gradient Boosting tuning, test-set evaluation, probability-decile analysis, and business recommendations.

## Business Objective

The project addresses two connected business questions:

1. **Descriptive analytics:** How do product categories, customer demographics, geography, and time relate to observed purchase-record value?
2. **Predictive analytics:** Can historical purchase behaviour and selected customer characteristics identify customers likely to become high-value future spenders?

## Dataset

This project uses the published **Open e-commerce 1.0** dataset, containing crowdsourced U.S. Amazon purchase histories linked to survey-based customer characteristics.

- Dataset: [Harvard Dataverse – Open e-commerce 1.0](https://doi.org/10.7910/DVN/YGLYDY)
- Source paper: Berke et al. (2024), *Open e-commerce 1.0: Five years of crowdsourced U.S. Amazon purchase histories with user demographics*, Scientific Data.

The raw data are not included in this repository. Please download the official dataset from Harvard Dataverse before running the notebooks.

## Analytical Scope

The raw file contains a small number of records after 2022, but later coverage is incomplete. Therefore, the primary analysis uses complete observations from:

**1 January 2018 to 31 December 2022**

## Part A: Descriptive Analytics

Part A examines transaction-level and customer-segment patterns, including:

- Purchase-record value distribution and outlier analysis
- Product-category revenue and purchase volume
- Aggregated category analysis
- Income-group and age-group revenue patterns
- Geographic revenue patterns
- Monthly and weekday purchasing trends
- Interactive business dashboard

### Key descriptive findings

- Purchase-record value is strongly right-skewed: mean value is higher than the median because a small number of expensive purchases increase the average.
- Books are the highest-revenue original product category in the analysed sample.
- Groceries & Food is the most frequently purchased interpretable aggregated category.
- The $100,000–$149,999 income group and customers aged 25–34 contribute the highest observed aggregate purchase-record value.
- California has the highest observed shipping-address revenue in the analysed sample.
- Monthly purchase-record value varies over time, with a visible increase around late 2021.

## Part B: Predictive High-Value Customer Classification

Part B converts the descriptive analysis into a customer-level prediction problem.

### Temporal design

| Component | Definition |
|---|---|
| Feature window | 1 January 2018–31 December 2020 |
| Outcome window | 1 January 2021–31 December 2022 |
| Unit of analysis | One customer (`Survey ResponseID`) |
| Target | Top 25% of future spenders |
| High-value threshold | Future spending ≥ $5,908.16 |

Customer-level features include recency, frequency, monetary value, purchase activity, category diversity, purchase regularity, tenure, and selected demographic/contextual variables.

### Models evaluated

- Dummy baseline
- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting

### Final model results

Gradient Boosting was selected as the strongest model after comparison and tuning.

| Metric | Tuned Gradient Boosting |
|---|---:|
| Accuracy | 0.874 |
| Precision | 0.764 |
| Recall | 0.717 |
| F1-score | 0.740 |
| ROC-AUC | 0.920 |

The highest predicted-probability decile had a 94.90% observed high-value rate on the held-out test set, compared with 24.97% overall, representing 3.80× lift.

## Business Implications

- Prioritise retention activity for customers with high historical monetary value.
- Use category diversity as a signal for cross-selling opportunities.
- Use predicted probabilities to fill campaign audiences based on available budget and capacity.
- Apply lower-cost re-engagement actions to customers with long recency or low stated platform use.
- Monitor fairness, campaign costs, model performance, and data drift before operational deployment.

## Repository Structure

```text
notebooks/
  01_descriptive_eda.ipynb
  02_predictive_customer_value.ipynb

charts/
  part_a/
  part_b/

data/
  README.md

docs/
  methodology.md
  results_summary.md
```

## Reproducibility

1. Download `amazon-purchases.csv` and `survey.csv` from the official Harvard Dataverse dataset page.
2. Place the files in a local `data/raw/` directory.
3. Update the local data path in the notebooks if necessary.
4. Run `01_descriptive_eda.ipynb`.
5. Run `02_predictive_customer_value.ipynb`.

## Limitations

- The dataset is a volunteer, crowdsourced sample and does not represent all Amazon customers.
- Findings are sample-level descriptive associations, not causal claims.
- Purchase-record value is not equivalent to basket-level checkout order value.
- The predictive model estimates future high-value status during a defined outcome period; it does not calculate full customer lifetime value.
- Model thresholds should be selected according to campaign economics, not treated as fixed universal rules.

## Project Context and Contribution

This repository documents a group project completed for the Business Analytics course at Universität Trier in 2026.

The project was completed by Group 19. My individual contribution focused on Exploratory Data Analysis and descriptive business interpretation, including transaction-value distribution analysis, category and demographic analysis, geographic and temporal patterns, chart development, dashboard support, and documentation of findings.

I also contributed to the final predictive-analysis review, including model-evaluation interpretation and the translation of results into business implications.

## Technologies

`Python` · `pandas` · `NumPy` · `Matplotlib` · `Seaborn` · `scikit-learn` · `Google Colab`

## License and Attribution

The raw data are provided by the Open e-commerce 1.0 dataset under its applicable terms. This repository contains project code, derived analysis, and documentation. Please cite the original dataset and publication if using or adapting this work.
