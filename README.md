# 📈 SQL Data Analytics Project

A collection of SQL scripts for data exploration, analytics, and reporting. The scripts cover database exploration, key metrics, time-based trends, cumulative analysis, segmentation, and reusable reporting views. Each script focuses on one analytical theme and demonstrates clean, practical SQL.

## 📌 Executive Summary

This project turns a sales star schema (customers, products, orders) into business insight using SQL alone. It follows a clear path from exploration to decision support:

- **Explore:** understand the structure, date range, and key metrics of the data
- **Analyze:** rank products and customers, track trends, measure growth and performance
- **Segment:** group customers (VIP, Regular, New) and products (High, Mid, Low performers)
- **Report:** consolidate findings into two reusable views, `gold.report_customers` and `gold.report_products`, ready for BI tools

The result is a repeatable analytics workflow that answers core questions: what is selling, who is buying, how performance is changing, and where value is concentrated.

## 🙏 Acknowledgment

This project was built for educational purposes by following the tutorial series by Baraa Khatib Salkini (Data With Baraa).

* Tutorial videos: [SQL Exploratory Data Analysis](https://www.youtube.com/watch?v=6cJ5Ji8zSDg), [SQL Advance Analytics](https://www.youtube.com/watch?v=2jGhQpbzHes&t=4879s)
* Author's website: [datawithbaraa.com](https://www.datawithbaraa.com)

The original work is licensed under the [MIT License](https://github.com/DataWithBaraa/sql-data-analytics-project/blob/main/LICENSE). All credit for the project concept, dataset, and structure goes to the original author.

## 🎯 Purpose

- Explore and understand a relational data model quickly
- Calculate key business metrics
- Analyze trends, performance, and part-to-whole contribution
- Segment customers and products
- Build reusable reporting views for BI tools

## 🗺️ Analytics Roadmap

The scripts follow a two-stage flow: Exploratory Data Analysis (steps 1 to 6), then Advanced Analytics (steps 7 to 12).

[![Data Analytics Roadmap](docs/project_roadmap.png)](docs/project_roadmap.png)

## 🛠️ Tech Stack

- SQL Server (T-SQL)
- SQL Server Management Studio (SSMS)
- Note: `DATETRUNC()` requires SQL Server 2022 or later

## 🗄️ Data Model

Star schema in the `gold` schema of the `DataWarehouseAnalytics` database.

| Table | Type | Description |
|---|---|---|
| `gold.dim_customers` | Dimension | Customer details: name, country, gender, marital status, birthdate |
| `gold.dim_products` | Dimension | Product details: category, subcategory, cost, product line |
| `gold.fact_sales` | Fact | Order lines: dates, sales amount, quantity, price |

## 📂 Repository Structure

```
sql-exploratory-data-analysis/
├── datasets/     # CSV source files (dim_customers, dim_products, fact_sales)
├── docs/         # Project roadmap diagram
├── scripts/      # SQL scripts 00 to 13
├── LICENSE
└── README.md
```

## 📜 Scripts Overview

| # | Script | Focus | Key Techniques |
|---|---|---|---|
| 00 | `00_init_database` | Creates the database, `gold` schema, tables, and loads CSV data | `CREATE`, `BULK INSERT` |
| 01 | `01_database_exploration` | Lists tables and column metadata | `INFORMATION_SCHEMA` |
| 02 | `02_dimensions_exploration` | Unique values in dimension tables | `DISTINCT`, `ORDER BY` |
| 03 | `03_date_range_exploration` | Time boundaries of orders and customer ages | `MIN`, `MAX`, `DATEDIFF` |
| 04 | `04_measures_exploration` | Core business metrics in one report | `SUM`, `AVG`, `COUNT`, `UNION ALL` |
| 05 | `05_magnitude_analysis` | Totals grouped by dimensions | `GROUP BY`, joins |
| 06 | `06_ranking_analysis` | Top and bottom products and customers | `TOP`, `RANK()` |
| 07 | `07_change_over_time_analysis` | Monthly sales trends and seasonality | `DATETRUNC`, `FORMAT` |
| 08 | `08_cumulative_analysis` | Running totals and moving averages | `SUM() OVER`, `AVG() OVER` |
| 09 | `09_performance_analysis` | Year-over-year and vs. average comparison | `LAG()`, `CASE`, CTEs |
| 10 | `10_data_segmentation` | Cost ranges and customer segments (VIP, Regular, New) | `CASE`, CTEs |
| 11 | `11_part_to_whole_analysis` | Category contribution to total sales | Window totals, percentages |
| 12 | `12_report_customers` | Customer report view `gold.report_customers` | Views, CTEs, KPIs |
| 13 | `13_report_products` | Product report view `gold.report_products` | Views, CTEs, KPIs |

## 📊 Reporting Views

**`gold.report_customers`**
- Customer name, age, and age group
- Segment: VIP (12+ months, over 5,000 in sales), Regular (12+ months, 5,000 or less), New (under 12 months)
- Metrics: total orders, sales, quantity, products, lifespan
- KPIs: recency, average order value, average monthly spend

**`gold.report_products`**
- Product name, category, subcategory, cost
- Segment: High-Performer (over 50,000), Mid-Range (10,000 to 50,000), Low-Performer (under 10,000)
- Metrics: total orders, sales, quantity, unique customers, lifespan
- KPIs: recency, average selling price, average order revenue, average monthly revenue

## 🚀 Getting Started

1. Install SQL Server and SSMS.
2. Clone this repository.
3. Update the CSV file paths in `00_init_database.sql` to match your local folder.
4. Run `00_init_database.sql`. Warning: it drops and recreates the `DataWarehouseAnalytics` database.
5. Run the remaining scripts in numeric order (01 to 13).

## ✅ Best Practices Shown

- Header comment in every script with purpose and functions used
- CTEs for readable, step-by-step logic
- Window functions instead of self-joins
- `NULLIF` and `CASE` to avoid divide-by-zero errors
- Filtering out null order dates before time-based analysis
- Views for reusable reporting layers

