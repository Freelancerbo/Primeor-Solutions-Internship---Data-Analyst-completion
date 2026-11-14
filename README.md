# Primeor-Solutions-Internship---Data-Analyst-completion
# E-Commerce Sales Analysis: Data Analytics Internship Project

An end-to-end data analysis project completed during the **Data Analysis Internship at Primeor Solutions**. It takes a raw, messy e-commerce orders dataset through cleaning, Excel analysis, SQL analysis and an interactive Power BI dashboard, and ends with a business insights report.

![Python](https://img.shields.io/badge/Python-Pandas-3776AB?logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-SQLite-003B57?logo=sqlite&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-Pivot%20Tables-217346)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)

---

## Project Overview

| | |
|---|---|
| **Data** | E-commerce orders, January 2011 to December 2014 |
| **Size after cleaning** | 51,257 order lines, 21 columns, 25,026 orders |
| **Scope** | 7 markets, 13 regions, 3 categories, 17 sub-categories, 3 customer segments |
| **Goal** | Clean the data, find what drives sales and profit, and recommend actions |

> The dataset was provided by Primeor Solutions for the internship and is **not included** in this repository.

---

## Key Results

| Metric | Value |
|---|---|
| Total Sales | 12,632,373 |
| Total Profit | 1,467,497.61 |
| Profit Margin | 11.6% |
| Total Orders | 25,026 |
| Average Discount | 14.3% |

### Main findings
- **Sales grew every year**, from 2.26 million (2011) to 4.29 million (2014). The best month was November 2014, and about 34% of sales fall in October to December.
- **APAC is the top market** (28.4% of sales) and **Central is the top region** (22.3%). Canada is the smallest market (0.5%).
- **Technology is the most profitable category** (about 663 thousand profit). 5 of the 10 most profitable products are smartphones.
- **Discounts are the biggest profit risk.** 24.5% of order lines lose money. Loss-making lines have an average discount of 45%, against 4% for profitable lines, and no order line with 0% discount made a loss.
- **Tables** is the only sub-category with a large overall loss (about 64 thousand).
- **Standard Class** is used in about 60% of order lines.
- The **top 10 customers make up only 2.7%** of sales, so the business does not depend on a few accounts.

---

## What Was Done

### Level 1: Data Cleaning and Excel Analysis
**Cleaning (Python, Pandas, Google Colab)**

| Issue found | Action |
|---|---|
| 54 fully duplicate records | Removed |
| Sales stored as text with thousands separators | Cleaned and converted to numeric |
| Order and ship dates in two formats | Standardised to `YYYY-MM-DD` |
| Missing customer names | Labelled `Unknown` |
| 14 rows with missing profit | Removed (about 0.03% of rows) |
| Extra and repeated spaces in text | Trimmed |
| Invalid numbers (negative quantity, discount outside 0 to 1, negative shipping cost) | Checked, none found. Negative profit is a real loss and was kept |

**Excel analysis (Google Sheets, exported to .xlsx)**
- KPIs: total sales, total profit, average discount
- Top 5 products by sales and top 5 loss-making products
- Region-wise sales
- Pivot tables and 4 charts: sales by region, profit by category, segment-wise sales, monthly sales trend

### Level 2: SQL Analysis (SQLite)
10 queries covering top profitable products, top customers, region and market sales, category profit and discount, negative-profit orders, monthly trend, top sub-categories and ship mode usage. See [`sql/SQL_Queries.sql`](sql/SQL_Queries.sql).

Example:
```sql
SELECT category, AVG(discount) AS avg_discount
FROM orders
GROUP BY category
ORDER BY avg_discount DESC;
```

### Level 3: Power BI Dashboard
A 3-page interactive dashboard with slicers, KPI cards and a consistent colour theme:
1. **Executive Overview**: Total Sales, Total Profit, Total Orders, Average Discount
2. **Sales Analysis**: sales by region and market, monthly trend, category performance
3. **Product and Customer Insights**: top products, top customers, profit by sub-category, segment analysis

Core DAX measures:
```
Total Sales      = SUM(Final_Cleaned_Dataset[sales])
Total Profit     = SUM(Final_Cleaned_Dataset[profit])
Total Orders     = DISTINCTCOUNT(Final_Cleaned_Dataset[order_id])
Average Discount = AVERAGE(Final_Cleaned_Dataset[discount])
```

---

## Recommendations
1. **Cap discounts** (for example at 30%) or require approval above it.
2. **Review loss-making items**, starting with Tables and the largest-loss products.
3. **Protect and promote Technology**, the most profitable category.
4. **Test targeted campaigns** in the weakest markets before larger spending.
5. **Plan for the year-end peak** in stock, delivery capacity and promotions.
6. **Reward repeat buyers**, especially in the Corporate and Home Office segments.

---

## Repository Structure

```
.
├── README.md
├── notebooks/                  # Cleaning and SQL notebook (Colab)
├── sql/
│   └── SQL_Queries.sql         # All 10 SQL queries
├── excel/                      # Excel analysis workbook
└── reports/
    └── Business_Insights_Report.pdf
```

## How to Reproduce
1. Load the raw CSV with Pandas and apply the cleaning steps above.
2. Save the result as `Final_Cleaned_Dataset.csv`.
3. Load it into SQLite as a table named `orders`:
   ```python
   import sqlite3, pandas as pd
   df = pd.read_csv("Final_Cleaned_Dataset.csv")
   conn = sqlite3.connect("primeor.db")
   df.to_sql("orders", conn, if_exists="replace", index=False)
   ```
4. Run the queries in `sql/SQL_Queries.sql`.
5. Open the Power BI file and refresh it against the cleaned CSV.

## Tools Used
Python (Pandas), Google Colab, Google Sheets / Excel, SQLite, Power BI

---

## Author
**Your Name**
Data Analysis Intern, Primeor Solutions
LinkedIn: add your profile link here

#PrimeorSolutions #PrimeorDataAnalytics #PrimeorInternship
