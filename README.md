# SQL Data Analytics Project: From EDA to Advanced Business Insights

A comprehensive SQL-based analytics project built on a fictional retail data warehouse. This project walks through the full analytics workflow — from database setup and exploratory data analysis (EDA) to advanced reporting and business intelligence — using **Microsoft SQL Server**.

---

## 📁 Project Structure

```
sql-data-analytics-project/
│
├── datasets/
│   └── flat-files/
│       ├── dim_customers.csv
│       ├── dim_products.csv
│       └── fact_sales.csv
│
├── scripts/
│   ├── 00_init_database.sql          # Database and schema setup, bulk data load
│   ├── 01_database_exploration.sql   # Table and column metadata exploration
│   ├── 02_dimensions_exploration.sql # Unique values in dimension tables
│   ├── 03_date_range_exploration.sql # Temporal boundaries and customer ages
│   ├── 04_measures_exploration.sql   # Key business metrics overview
│   ├── 05_magnitude_analysis.sql     # Aggregations by country, gender, category
│   ├── 06_ranking_analysis.sql       # Top/bottom products and customers
│   ├── 07_change_over_time.sql       # Monthly/yearly sales trends
│   ├── 08_performance_analysis.sql   # Year-over-year product performance
│   ├── 09_cumulative_analysis.sql    # Running totals and moving averages
│   ├── 10_segmentation_analysis.sql  # Customer and product segmentation
│   ├── 11_part_to_whole_analysis.sql # Category contribution to total sales
│   ├── 12_customer_report.sql        # Customer KPI report (VIEW)
│   └── 13_product_report.sql         # Product KPI report (VIEW)
│
└── README.md
```

---

## 🗄️ Database Overview

**Database:** `DataWarehouseAnalytics`  
**Schema:** `gold`

### Tables

| Table | Description |
|---|---|
| `gold.dim_customers` | Customer dimension — demographics, location, birthdate |
| `gold.dim_products` | Product dimension — category, subcategory, cost, product line |
| `gold.fact_sales` | Sales fact — orders, quantities, amounts, dates |

---

## 🔍 Analytics Modules

### 1. Database & Dimension Exploration
Inspects schema metadata using `INFORMATION_SCHEMA` and lists unique values across key dimensions like country, product category, and subcategory.

### 2. Date Range & Measures Exploration
Establishes temporal boundaries (first/last order dates, customer ages) and calculates core business metrics: total sales, quantity, orders, customers, and average price — combined into a single key metrics report.

### 3. Magnitude Analysis
Groups and aggregates data across dimensions to reveal distribution patterns:
- Customers by country and gender
- Products by category
- Revenue by category and customer
- Sold items by country

### 4. Ranking Analysis
Identifies top and bottom performers using both `TOP N` and window functions (`RANK()`, `DENSE_RANK()`):
- Top 5 revenue-generating products
- Top 10 highest-value customers
- 3 customers with the fewest orders

### 5. Change Over Time Analysis
Tracks month-by-month and year-by-year trends in sales, customer counts, and quantities using `DATETRUNC()` and `FORMAT()` for flexible date grouping.

### 6. Performance Analysis (Year-over-Year)
Uses `LAG()` and `AVG() OVER()` window functions to compare each product's annual sales against:
- Its own historical average (`Above Avg` / `Below Avg`)
- The prior year's sales (`Increase` / `Decrease` / `No Change`)

### 7. Data Segmentation
Classifies customers and products into meaningful groups:
- **Product cost segments:** Below 100 / 100–500 / 500–1000 / Above 1000
- **Customer segments:** VIP / Regular / New (based on spending and tenure)

### 8. Part-to-Whole Analysis
Calculates each product category's percentage contribution to total revenue using `SUM() OVER()`.

---

## 📊 Final Reports (SQL Views)

### `gold.report_customers`
A consolidated customer-level view combining:
- Demographics (age, age group)
- Behavioral segment (VIP / Regular / New)
- KPIs: total orders, total sales, total quantity, recency, average order value, average monthly spend

### `gold.report_products`
A consolidated product-level view combining:
- Product metadata (category, subcategory, cost)
- Performance segment (High-Performer / Mid-Range / Low-Performer)
- KPIs: total orders, total sales, total customers, recency, average order revenue, average monthly revenue

---

## 🛠️ Tech Stack

- **Database:** Microsoft SQL Server
- **Language:** T-SQL
- **Features used:** CTEs, Window Functions (`LAG`, `RANK`, `AVG OVER`), `BULK INSERT`, Views, `DATEDIFF`, `DATETRUNC`, `FORMAT`

---

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/Dileep0509/SQL-Data-Analytics-Project-From-EDA-to-Advanced-Business-Insights.git
   ```

2. **Update file paths** in `00_init_database.sql` to match your local CSV file locations.

3. **Run scripts in order** (00 → 13) using SQL Server Management Studio (SSMS) or Azure Data Studio.

4. **Query the views** for ready-made business reports:
   ```sql
   SELECT * FROM gold.report_customers;
   SELECT * FROM gold.report_products;
   ```

> ⚠️ **Warning:** Script `00_init_database.sql` drops and recreates the `DataWarehouseAnalytics` database. Do not run it on a production environment.

---

## 📌 Key Concepts Demonstrated

- Exploratory Data Analysis (EDA) with SQL
- Dimensional modeling (star schema)
- Aggregation and grouping strategies
- Time-series analysis and trend detection
- Customer lifetime value segmentation
- Year-over-year performance benchmarking
- Reusable SQL views for business reporting

