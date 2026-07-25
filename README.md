# Amazon Customer & Revenue Analytics

## Project Overview

This project analyzes five years of crowdsourced U.S. Amazon purchase histories together with user demographics to understand:

- Which demographic segments (age, income, education) drive the highest revenue.
- Which product categories dominate purchases and revenue.
- Which U.S. states contribute most to sales.
- How revenue evolves over time and across days of the week. 

## Dataset

**Open e-commerce 1.0:** Five years of U.S. Amazon purchase histories with user demographics collected via survey.   
Source: Harvard Dataverse (doi:10.7910/DVN/YGLYDY).

We combine:

- `amazon-purchases.csv` – transaction data (order date, price, quantity, product category, shipping state).   
- `survey.csv` – demographics (age group, income group, education, state, Amazon usage).   
- `category_map.csv` – mapping rules to aggregate raw product categories into higher‑level `Agg_Category` groups. 

## Business Problem

> How do demographic factors like age, income, and education constitute the highest‑value customers, and which geographic locations (states) drive customer value and regional product demand among U.S. Amazon customers? Are there regional variations in product category preferences? 

## Analysis Roadmap

The notebook follows these steps: 

1. **Data Integration**  
   - Import libraries (`pandas`, `numpy`, `matplotlib`, `seaborn`).  
   - Load purchases and survey data into DataFrames.  
   - Merge them on `Survey ResponseID` to create a master dataset. 

2. **Data Cleaning & Preprocessing**  
   - Drop non‑essential columns (substance use, health, small‑biz questions, etc.).   
   - Cast columns to appropriate types (dates, numeric, categories, boolean for `Q-demos-hispanic`).   
   - Add date components (`Order Year`, `Order Month`, `Order DayOfWeek`).   
   - Compute `Total Price = Purchase Price Per Unit * Quantity`.   
   - Build `Agg_Category` by applying string‑matching rules from `category_map.csv` to group similar categories. 

3. **Exploratory Data Analysis (EDA)**  
   - Distribution of `Total Price` (histograms, log‑scale bucket chart with annotated revenue per price band).   
   - Top product categories by purchase count (`Category`, `Agg_Category`).   
   - Revenue by income group, age group, and state.   
   - Monthly revenue trend over years, and daily revenue patterns by day of week.   
   - Boxplots and IQR/99th‑percentile analysis to identify outliers and very high‑value purchases. 

4. **Dashboard (Optional)**  
   - An interactive HTML dashboard summarising KPIs, revenue trends, category share, day‑of‑week patterns, and age‑segment revenue using `Chart.js`. 

## Visualizations

- [Exploratory charts (HTML)](charts/charts.html)

## Key Business Insights

From the EDA: 

- **Skewed revenue distribution:** Most purchases have low `Total Price`, but a small share of high‑value orders contributes disproportionately to overall revenue. High‑value customers should not be ignored.   
- **Category performance:**  
  - Raw `Category` shows `ABIS_BOOK` as a dominant category.  
  - Aggregated `Agg_Category` reveals `Groceries & Food` as the most purchased group, informing inventory and promotion priorities.   
- **Income segments:** The income band `$100,000–$149,999` generates the highest revenue, suggesting targeted campaigns for high‑income customers.   
- **Age segments:** Customers aged **25–34** contribute the most revenue, indicating a key age group for product and marketing focus.   
- **Geographic patterns:** **California** stands out as the top revenue‑generating state, with clear regional differences that matter for logistics and localized marketing.   
- **Temporal patterns:**  
  - Revenue spikes and drops over time, with a sharp decline around 2023 and peaks around late 2021.   
  - **Mondays** generate the highest total revenue across the week, suggesting optimal timing for campaigns and resource allocation. 

## How to Run (Colab)

1. Open the notebook `notebooks/amazon_customer_analytics.ipynb` in Google Colab.  
2. Download `amazon-purchases.csv`, `survey.csv`, and `category_map.csv` and upload them to your Colab environment or Google Drive.  
3. Update data paths at the top of the notebook to match your location (e.g. `/content/amazon-purchases.csv`).   
4. Run all cells to reproduce data integration, cleaning, EDA visualizations, and the final dashboard.

## Group Work and My Contribution

This was originally a **group project** for a Business Analytics course. I am showcasing it here to demonstrate:

- Data integration and cleaning across multiple CSV files.  
- Feature engineering (`Total Price`, date components, aggregated categories).  
- Exploratory data analysis with Python (pandas, matplotlib, seaborn).  
- Deriving clear business insights and building a lightweight dashboard.

## Tech stack

- Python
- pandas, NumPy
- matplotlib, seaborn
- Chart.js (HTML dashboard)
