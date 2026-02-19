# SQL Documentation | Olist E-Commerce Analytics

> **Purpose:** This folder contains the data preparation (ETL) and business analysis SQL scripts for the Olist Brazilian E-commerce BI project.  
> **Database:** `ecommerce` (MySQL)

---

## Table of Contents

1. [ETL Pipeline — Step-by-Step](#1-etl-pipeline--step-by-step)
2. [Business Analysis — The Story](#2-business-analysis--the-story)
3. [File Reference](#3-file-reference)

---

## 1. ETL Pipeline — Step-by-Step

The `ETL.sql` script transforms raw Olist CSV data into an analysis-ready relational database. It enforces data types, referential integrity, and query performance. **Run this script once** after loading the raw CSVs into MySQL.

### Overview

| Phase | Action | Outcome |
|-------|--------|---------|
| **Setup** | Disable FK checks | Safe re-run during development |
| **1–5** | Master tables | Products, sellers, customers, geolocation, categories |
| **6–9** | Transaction tables | Orders, order items, payments, reviews |
| **Finish** | Re-enable FK checks | Full referential integrity |

---

### Step 1: Product Category Translation

**Why first?** This is a lookup table. Products reference category names; we need this before products.

- Set column types (`VARCHAR`, `NOT NULL`)
- Add primary key on `product_category_name`
- Enables English category names for reporting

---

### Step 2: Products

**Dependencies:** `product_category_name_translation`

- Standardize columns: `product_id`, dimensions (cm, g), photo count
- Primary key: `product_id`
- Foreign key: `product_category_name` → translation table
- Index: `product_category_name` for faster category filters

---

### Step 3: Sellers

- Columns: `seller_id`, zip prefix, city, state
- Primary key: `seller_id`
- Indexes on `seller_zip_code_prefix` and `seller_state` for geo queries

---

### Step 4: Customers

- Columns: `customer_id`, `customer_unique_id`, zip, city, state
- Primary key: `customer_id`
- Indexes on `customer_unique_id` (for repeat purchase analysis), zip, and state

---

### Step 5: Geolocation

- Zip-level lat/lng and city/state
- Indexes on `geolocation_zip_code_prefix` and `geolocation_state`
- Supports geographic analysis and enrichment

---

### Step 6: Orders (Critical)

**Dependencies:** `olist_customers_dataset`

**Date conversion:** Raw dates are `d/m/YYYY H:MM` (e.g. `2/10/2017 10:56`). The script:

1. Checks if date columns are still text
2. Adds temporary `_dt` columns
3. Parses with `STR_TO_DATE(..., '%e/%c/%Y %k:%i')`
4. Replaces invalid or NULL values with `2017-01-01`
5. Drops text columns and renames `_dt` to final names

**Resulting columns:** `order_purchase_timestamp`, `order_approved_at`, `order_delivered_carrier_date`, `order_delivered_customer_date`, `order_estimated_delivery_date`

- Primary key: `order_id`
- Foreign key: `customer_id` → customers
- Indexes: `order_status`, `order_purchase_timestamp`

---

### Step 7: Order Items (Fact Table)

**Dependencies:** Orders, products, sellers

**Data cleanup:**

1. Fix invalid `shipping_limit_date` (empty, `0000-00-00`, or bad format) → set to `2017-01-01`
2. Set column types: `order_id`, `order_item_id`, `product_id`, `seller_id`, `price`, `freight_value`

- Composite primary key: `(order_id, order_item_id)`
- Foreign keys: `order_id`, `product_id`, `seller_id`

---

### Step 8: Order Payments

**Dependencies:** Orders

- Columns: `order_id`, `payment_sequential`, `payment_type`, `payment_installments`, `payment_value`
- Composite primary key: `(order_id, payment_sequential)`
- Index on `payment_type` for payment-method analysis

---

### Step 9: Order Reviews

**Dependencies:** Orders

**Date conversion:** Same pattern as orders — text dates to `DATETIME` using regex validation.

**Deduplication:** Remove duplicate `review_id` rows (keep one per review), then add PK/FK.

- Primary key: `review_id`
- Foreign key: `order_id` → orders
- Indexes: `order_id`, `review_score`

---

### Step 10: Finalization

- `SET FOREIGN_KEY_CHECKS = 1` — restore referential integrity checks

---

## 2. Business Analysis — The Story

The `analysis .sql` file answers 10 business questions that form a coherent narrative about our marketplace performance. Below is the story we tell.

---

### Act 1: Market Momentum & Financial Health

**Q1. The Pulse of the Business: Monthly Revenue Trends**

We see revenue swings follow Brazilian retail holidays (e.g. Black Friday) or shifts in confidence. To smooth things out we run off-season discounts when revenue dips, scale carrier capacity about a month before peaks, and use purchase timestamps to time maintenance and heavy ad spend.

**Q2. The Heavy Hitters: Top-Performing Product Categories**

We see a handful of categories (e.g. Health & Beauty, Watches) drive most GMV, likely thanks to stronger trust, seller variety, or pricing. We move ~20% of budget from weaker categories into the top three to lift ROI and put the top 10 in "Category Spotlights" on the homepage to help CTR.

**Q3. Purchasing Power: AOV by Payment Method**

We see credit card users spend more per order because installments lower the bar for premium buys. We offer flexible installments (e.g. up to 12x) in high-AOV categories, bundle for credit users, and give small discounts on Boleto to grow baskets and improve liquidity.

---

### Act 2: Customer DNA & Geographic Footprint

**Q4. Regional Powerhouses: Revenue by State**

We see revenue concentrated in Southeast/São Paulo, where density and infrastructure are stronger. We build micro-fulfillment in SP/RJ to support next-day delivery and run geo-targeted campaigns in MG/PR plus regional freight deals in underserved states to broaden our reach.

**Q5. The Loyalty Loop: Repeat Purchase Analysis**

We see many customers buy once and don’t return, often due to a weak first experience or little follow-up. We send win-back emails (e.g. 15% off after 60 days), run an "Olist Prime"–style program for frequent buyers, and personalize recommendations by `customer_unique_id` to improve retention.

---

### Act 3: Operational Excellence & Logistics

**Q6. Delivery Performance**

Late deliveries usually stem from weak carriers or infrastructure. Penalizing carriers with >15% late rate, updating delivery estimates from real-time performance, and sending apology vouchers as soon as an order is flagged late keeps expectations aligned and customers calmer.

**Q7. Freight Cost Impact**

We see in some categories shipping costs rival product price—often because of bulky items or remote sellers. We set minimum order values for free shipping on low-value/high-freight items, push "Fulfillment by Olist," and show freight early in checkout to help margins and reduce abandonment.

---

### Act 4: The Voice of the Customer

**Q8. Review Score Breakdown**

We see the spread of 1–5 star reviews reflects operational and quality issues. We set alerts when daily avg `review_score` drops below 3.5, use NLP to tag feedback (e.g. Broken/Late/Wrong), and run a 1-star recovery workflow within 24 hours to catch and fix problems fast.

**Q9. Categories with Critical Feedback**

Categories with lots of 1–2 star reviews often suffer from misleading descriptions or fragile items breaking in transit. Requiring real product photos in high-complaint categories, fragile-item packaging standards, and suspending sellers with `avg_score` <3.0 until they improve keeps quality in check.

---

### Act 5: Payment Ecosystem

**Q10. Payment Method Distribution**

We see payment mix reflect habits (Boleto for the unbanked) and incentives (credit for installments). We use vouchers for refunds to keep capital in our ecosystem and simplify credit checkout (e.g. 1-click) to lean into the higher AOV that comes with that method.



---

## 3. File Reference

| File | Purpose |
|------|---------|
| `ETL.sql` | Data preparation: types, keys, indexes, date conversion, deduplication |
| `analysis .sql` | Business analytics: 10 questions covering revenue, customers, operations, satisfaction, and payments |
