# Olist E-Commerce 

An end-to-end analytics project that converts raw Brazilian marketplace transactions into decision-ready intelligence using SQL and Power BI.

This repository is designed as a production-style BI workflow:

- **Source data** is curated and quality-checked in `data/`
- **Data engineering** is implemented in `scripts/ETL.sql`
- **Business analytics** is defined in `scripts/analysis .sql`
- **Semantic views** for reporting are built in `scripts/views.sql`
- **Dashboard delivery** is managed in `dashboard/`

## 1) Executive Overview

The business objective is to help marketplace leaders answer three strategic questions:

- Where growth is accelerating or slowing (revenue, category, customer behavior)
- Where margin and service quality are leaking (freight burden, late delivery, low ratings)
- Which levers create sustainable performance (payment mix, regional focus, retention strategy)

The analytical scope covers the complete customer-order lifecycle:

- acquisition and first purchase
- product and seller mix
- logistics performance
- customer satisfaction and payment behavior

## 2) Project Architecture

`CSV raw/cleaned data -> MySQL staging tables -> ETL constraints and transformations -> semantic SQL views -> Power BI dashboard`

### Repository Layout

```text
PowerBiProject/
|- data/
|  |- README.md
|  |- olist_*.csv
|- scripts/
|  |- ETL.sql
|  |- analysis .sql
|  |- views.sql
|  |- README.md
|- dashboard/
|  |- (Power BI files: .pbix, templates, exports)
|- README.md
```

## 3) Data Foundation

Primary datasets (Olist public marketplace):

- customers, sellers, products, category translation
- orders, order items, payments, reviews
- geolocation

Data quality and preparation logic is documented in `data/README.md`, including:

- missing value handling in product attributes
- geolocation de-duplication
- order date and status consistency checks
- review text null normalization

## 4) SQL Pipeline (Engineering Layer)

The SQL stack is intentionally separated into three responsibilities:

1. `**ETL.sql**` (structure + integrity)
  - standardizes column data types
  - converts text timestamps to `DATETIME`/`DATE`
  - defines primary and foreign keys
  - creates high-impact indexes for reporting performance
  - applies safe/idempotent checks for rerun scenarios
2. `**views.sql**` (semantic layer)
  - publishes reusable analytical entities:
    - `dim_customer`
    - `dim_product`
    - `fact_orders`
    - `fact_order_items_enriched`
  - simplifies dashboard query logic and improves model consistency
3. `**analysis .sql**` (business logic layer)
  - codifies 10 executive business questions as repeatable SQL analyses

## 5) Business Questions Covered

The analysis script addresses a full management narrative:

1. Monthly revenue trend
2. Top revenue-driving categories
3. Average order value by payment type
4. Revenue concentration by state
5. Repeat purchase distribution
6. Delivery punctuality and lead time
7. Freight cost burden by category
8. Review score distribution
9. Categories with critical feedback
10. Payment method contribution

## 6) How to Run (End-to-End)

### Step A - Prepare Environment

- Install MySQL 8+ (or compatible)
- Create database:

```sql
CREATE DATABASE ecommerce;
USE ecommerce;
```

- Import CSVs from `data/` into matching staging tables

### Step B - Execute Engineering Scripts

Run scripts in this order:

1. `scripts/ETL.sql`
2. `scripts/views.sql`
3. `scripts/analysis .sql` (for validation and insight extraction)

Recommended validation after ETL:

- verify PK/FK constraints exist
- spot-check null or defaulted timestamps
- run sample aggregates from `analysis .sql` and compare with expected ranges

### Step C - Build Dashboard in Power BI

In `dashboard/`:

- connect Power BI to MySQL `ecommerce` database
- ingest semantic views first (`fact_*`, `dim_*`)
- define DAX measures for:
  - revenue
  - AOV
  - late delivery rate
  - repeat customer rate
  - low-rating share
- design pages for:
  - Executive KPI overview
  - Sales and category performance
  - Logistics and service quality
  - Customer and payment behavior

## 7) Dashboard Design Standards

To keep the report at enterprise quality:

- use a star-like model centered on fact tables
- enforce consistent business definitions across pages
- separate leading indicators (trend) from diagnostic indicators (root cause)
- include period-over-period comparisons and slicer-driven drilldowns
- annotate outliers (seasonality peaks, freight spikes, rating drops)

## 8) Links and References

- Olist Ecommerce dataset: [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data?select=olist_products_dataset.csv](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce/data?select=olist_products_dataset.csv)

