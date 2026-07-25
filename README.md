# Amazon Customer & Revenue Analytics

## Project Overview

This project analyzes five years of crowdsourced U.S. Amazon purchase histories together with user demographics to understand:

- Which demographic segments (age, income, education) drive the highest revenue.
- Which product categories dominate purchases and revenue.
- Which U.S. states contribute most to sales.
- How revenue evolves over time and across days of the week.[file:88]

## Dataset

**Open e-commerce 1.0:** Five years of U.S. Amazon purchase histories with user demographics collected via survey.[file:88]  
Source: Harvard Dataverse (doi:10.7910/DVN/YGLYDY).

We combine:

- `amazon-purchases.csv` – transaction data (order date, price, quantity, product category, shipping state).[file:88]  
- `survey.csv` – demographics (age group, income group, education, state, Amazon usage).[file:88]  
- `category_map.csv` – mapping rules to aggregate raw product categories into higher‑level `Agg_Category` groups.[file:88]

## Business Problem

> How do demographic factors like age, income, and education constitute the highest‑value customers, and which geographic locations (states) drive customer value and regional product demand among U.S. Amazon customers? Are there regional variations in product category preferences?[file:88]

## Analysis Roadmap

The notebook follows these steps:[file:88]

1. **Data Integration**  
   - Import libraries (`pandas`, `numpy`, `matplotlib`, `seaborn`).  
   - Load purchases and survey data into DataFrames.  
   - Merge them on `Survey ResponseID` to create a master dataset.[file:88]

2. **Data Cleaning & Preprocessing**  
   - Drop non‑essential columns (substance use, health, small‑biz questions, etc.).[file:88]  
   - Cast columns to appropriate types (dates, numeric, categories, boolean for `Q-demos-hispanic`).[file:88]  
   - Add date components (`Order Year`, `Order Month`, `Order DayOfWeek`).[file:88]  
   - Compute `Total Price = Purchase Price Per Unit * Quantity`.[file:88]  
   - Build `Agg_Category` by applying string‑matching rules from `category_map.csv` to group similar categories.[file:88]

3. **Exploratory Data Analysis (EDA)**  
   - Distribution of `Total Price` (histograms, log‑scale bucket chart with annotated revenue per price band).[file:88]  
   - Top product categories by purchase count (`Category`, `Agg_Category`).[file:88]  
   - Revenue by income group, age group, and state.[file:88]  
   - Monthly revenue trend over years, and daily revenue patterns by day of week.[file:88]  
   - Boxplots and IQR/99th‑percentile analysis to identify outliers and very high‑value purchases.[file:88]

4. **Dashboard (Optional)**  
   - An interactive HTML dashboard summarising KPIs, revenue trends, category share, day‑of‑week patterns, and age‑segment revenue using `Chart.js`.[file:88]

## Key Business Insights

From the EDA:[file:88]

- **Skewed revenue distribution:** Most purchases have low `Total Price`, but a small share of high‑value orders contributes disproportionately to overall revenue. High‑value customers should not be ignored.[file:88]  
- **Category performance:**  
  - Raw `Category` shows `ABIS_BOOK` as a dominant category.  
  - Aggregated `Agg_Category` reveals `Groceries & Food` as the most purchased group, informing inventory and promotion priorities.[file:88]  
- **Income segments:** The income band `$100,000–$149,999` generates the highest revenue, suggesting targeted campaigns for high‑income customers.[file:88]  
- **Age segments:** Customers aged **25–34** contribute the most revenue, indicating a key age group for product and marketing focus.[file:88]  
- **Geographic patterns:** **California** stands out as the top revenue‑generating state, with clear regional differences that matter for logistics and localized marketing.[file:88]  
- **Temporal patterns:**  
  - Revenue spikes and drops over time, with a sharp decline around 2023 and peaks around late 2021.[file:88]  
  - **Mondays** generate the highest total revenue across the week, suggesting optimal timing for campaigns and resource allocation.[file:88]

## How to Run (Colab)

1. Open the notebook `notebooks/amazon_customer_analytics.ipynb` in Google Colab.  
2. Download `amazon-purchases.csv`, `survey.csv`, and `category_map.csv` and upload them to your Colab environment or Google Drive.  
3. Update data paths at the top of the notebook to match your location (e.g. `/content/amazon-purchases.csv`).[file:88]  
4. Run all cells to reproduce data integration, cleaning, EDA visualizations, and the final dashboard.

## Group Work and My Contribution

This was originally a **group project** for a Business Analytics course. I am showcasing it here to demonstrate:

- Data integration and cleaning across multiple CSV files.  
- Feature engineering (`Total Price`, date components, aggregated categories).  
- Exploratory data analysis with Python (pandas, matplotlib, seaborn).  
- Deriving clear business insights and building a lightweight dashboard.[file:88][file:89]
