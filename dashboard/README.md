# Power BI Dashboard Documentation

## Brazilian E-Commerce Performance (Olist)

This document summarizes **valuable insights**, **actionable ideas**, and **industry context** from the Olist Power BI dashboards. It is written for leadership and analysts who need numeric accuracy and clear storytelling for decision-making.

---

## Dashboard 1 — Executive Overview | Brazilian E-Commerce Performance

**Question answered:** *What is the overall business health, and where are the biggest opportunities and risks?*



### The story in numbers


| KPI                           | Value  | Industry context                                                       |
| ----------------------------- | ------ | ---------------------------------------------------------------------- |
| **Total revenue**             | 15.42M | Strong base; benchmark against market share goals.                     |
| **Orders delivered**          | 96K    | Volume confirms scale; compare to canceled/unavailable to see leakage. |
| **Average order value (AOV)** | 159.83 | Healthy; e‑commerce often targets 100–200 for generalist marketplaces. |
| **Average review score**      | 4.09   | Positive; NPS/satisfaction typically correlates with scores >4.0.      |
| **On-time delivery rate**     | 91.89% | Good; best-in-class often >95%; clear improvement headroom.            |


### 1. Revenue momentum and seasonality

- **Observation:** Monthly revenue falls **~59%** from a peak of **1.70M (May)** to **~0.70M (September)** in the Monthly Revenue Trend.
- **Implication:** Strong H1 (e.g. May 1.70M, August 1.63M) and a clear Q3/Q4 trough point to seasonality and/or demand slowdown.
- **Actions:**
  - Run **targeted campaigns and promotions** in slower months (Q3/Q4) to smooth demand.
  - Use **seasonal demand forecasts** for inventory (avoid overstock in slow periods, stockouts in peaks).
  - Use **loyalty and re-engagement** in low-demand periods to keep purchase frequency up.

### 2. Order process: where we lose orders

- **Delivered:** **96.47K** orders (aligns with main KPIs).
- **Main loss points:** **Canceled (~0.63K)** and **Unavailable (~0.61K)** — direct revenue leakage; Executive Insights panel estimates **~200K+ revenue opportunity**.
- **Actions:**
  - **Stock accuracy:** Real-time inventory and regular audits to cut “unavailable” cancellations.
  - **Seller SLA:** Tighten fulfillment and communication SLAs; focus first on top states and categories.

---

## Dashboard 2 — Customer & Retention Intelligence

**Question answered:** *Who are our customers, how often do they buy, and how much do we retain them?*

### The story: strong acquisition, weak retention (“leaky bucket”)


| Metric                              | Value                      | Implication                                   |
| ----------------------------------- | -------------------------- | --------------------------------------------- |
| **Customers with 1 order**          | **96.88%**                 | Almost all customers are one-time buyers.     |
| **Customers with 2 orders**         | **2.86%**                  | Very low second-purchase conversion.          |
| **Customers with 3+ orders**        | **0.26%**                  | Loyalty segment is tiny.                      |
| **Returning revenue share %**       | Peak **2.66%** (2018 Q2)   | Revenue is overwhelmingly from new customers. |
| **New customers (quarterly)**       | Up to **~20.3K** (2018 Q1) | Acquisition engine works.                     |
| **Returning customers (quarterly)** | **~0–400**                 | Retention engine is underperforming.          |


In practice: **CAC is not converting into CLTV**; growth is dependent on continuous acquisition, which is costly and unstable.

### 1. Purchase frequency — fix the leaky bucket

- **Actions:**
  - **Win-back campaigns:** After 30–60 days with no second purchase, send personalized offers (e.g. discount, free shipping, recommendations). Target: move **1–2 pp** of 1-order customers to 2 orders in the next quarter.
  - **Post-purchase experience:** Surveys and reviews after first order; use feedback to improve onboarding and support; track CSAT/NPS and repeat rate for survey completers.
  - **Loyalty program:** Tiered program (points, exclusives) from first purchase; track enrollment and repeat rate by tier.

### 2. Cohort retention matrix (State × Revenue per customer)


| Quadrant                 | Meaning                               | Typical action                                                                |
| ------------------------ | ------------------------------------- | ----------------------------------------------------------------------------- |
| **Acquire**              | High revenue/customer, few customers  | Scale via look-alike and niche campaigns.                                     |
| **Defend & scale**       | High revenue/customer, many customers | VIP treatment, retention, near-zero churn target.                             |
| **Upsell**               | Low revenue/customer, many customers  | Increase AOV and frequency (bundles, recommendations, “buy more, save more”). |
| **Selective investment** | Low revenue/customer, few customers   | Invest only where strategic.                                                  |


- **Observation:** Many cohorts sit in **Upsell** (large customer base, lower revenue per customer) — biggest lever is to increase AOV and frequency there.
- **Actions:**
  - **Upsell cohorts:** Personalized recommendations, bundles, complementary items at checkout; track AOV and revenue per customer.
  - **Defend & scale:** VIP service, early access, exclusive offers; track churn and CLTV.
  - **Acquire:** Analyze what makes high-revenue-per-customer segments work; build look-alike audiences and replicate.

### 3. New vs returning customer trend

- **Targets (example):**
  - Increase **returning customers** by **50–100%** quarter-over-quarter.
  - Raise **returning revenue share** to **>10%** within a year.
- **Actions:**
  - **Shift budget:** Reallocate from pure acquisition to retention and re-engagement.
  - **Churn analysis:** Segment one-time buyers by category, geography, discount usage; qualitative research (surveys/interviews) with churned customers.
  - **Re-engagement:** Target 90+ days dormant with tailored offers and new product news; measure reactivation rate and revenue.
  - **Support:** First-contact resolution and proactive post-purchase outreach; link support satisfaction to repeat purchases.

---

## Dashboard 3 — Operations & Customer Experience Command Center

**Question answered:** *Are we operationally reliable, and where are we losing customer trust?*

### 1. Late orders and scaling pressure


| Period     | Late orders (approx.) | Implication                            |
| ---------- | --------------------- | -------------------------------------- |
| Late 2017  | ~0.2K/month           | Baseline.                              |
| Early 2018 | ~1.5K/month           | **~650%** increase — scaling pressure. |


- **Likely causes:** Supply chain bottlenecks, last-mile capacity or routing, or internal process breakdowns.
- **Actions:**
  - **Fulfillment deep dive:** Map delays by stage (acceptance, pick/pack, hand-off, last mile) for late 2017–early 2018.
  - **Capacity:** Align fulfillment and logistics capacity with demand forecasts; consider automation, space, or additional carriers.
  - **Proactive communication:** Automate notifications for orders with **>2-day delay risk**; dashboard suggests potential **2–3 point improvement in review mix** from managing expectations.

### 2. Low ratings in high-revenue categories

- **Observation:** Categories with **~$1.0M–$1.5M** revenue still show **11–15% low-rating share**.
- **Context:** For core categories, **>12%** low-rating share is often the threshold where negative reviews start to materially hurt trust and conversion.
- **Actions:**
  - **Quality audit:** Product quality, descriptions, packaging, and post-purchase support in these categories; benchmark vs competitors.
  - **Vendor performance:** Stricter quality controls or alternative suppliers where relevant.
  - **Feedback loop:** Category-specific surveys for low-rated purchases to drive product and ops improvements.

### 3. Review distribution over time

- **Volume:** Reviews grow from ~~0 in late 2016 to peaks of **~~7.46K** (late 2017/early 2018).
- **Mix:** Persistent share of low (1–2) and neutral (3) ratings alongside positive (4–5); goal is to shift mix toward positive and reduce low share.
- **Target (example):** **−3 pp** low-rating share in **top 5 categories/states with low-rating share >12%** within two quarters.
- **Actions:**
  - **Root cause:** For those categories/states, analyze low reviews (product, delivery, service, expectations).
  - **Improvement loop:** Feed insights into product, operations, and customer service.

### 4. Category impact–pain matrix

- **Purpose:** Plot **business impact** (e.g. revenue, volume) vs **customer pain** (e.g. low-rating share, refunds) to find “high impact, high pain” categories.
- **Next step:** Populate the matrix with current data; prioritize those quadrants for resource allocation and intervention.

---

## Dashboard 4 — Revenue & Commercial Performance

**Question answered:** *What drives revenue quality, and which commercial actions should leadership approve?*

### 1. Payment economics (numeric snapshot)


| Payment type    | Total payment value | AOV     | Takeaway                                               |
| --------------- | ------------------- | ------- | ------------------------------------------------------ |
| **Credit card** | **12.54M**          | **164** | Primary driver; optimize checkout and installments.    |
| **Boleto**      | **2.87M**           | **145** | Important in Brazil; tune conversion and speed.        |
| **Debit card**  | **0.22M**           | **143** | Similar AOV to Boleto; test incentives to lift volume. |
| **Voucher**     | **0.38M**           | **98**  | Lowest AOV and scale; possible margin drag.            |
| **not_defined** | **0.00M**           | —       | Investigate and fix categorization.                    |


- **Actions:**
  - **Credit card:** Card-first checkout, installment tuning, loyalty linked to card.
  - **Boleto/Debit:** Targeted incentives and faster processing where feasible.
  - **Voucher:** Review use (e.g. low-value only?), terms, and margin; consider retention-focused use or pruning.
  - **Data:** Resolve “not_defined” for correct reporting and payment analytics.

### 2. What matters most (strategic focus)


| Priority          | Detail                                                                                          |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| **Card payments** | Card-first checkout, installment tuning.                                                        |
| **Freight**       | High in telephony, signaling_and_security (and others); carrier, packaging, fulfillment levers. |
| **Target 1**      | Reduce freight ratio by **−1.5 to −2.0 pp** in priority categories.                             |
| **Target 2**      | Grow revenue in funded categories by **+10% to +15%**.                                          |


### 3. Total revenue and freight by category (selected)


| Category                              | Total revenue (approx.) | Revenue growth % | Freight % of product value | Priority                     |
| ------------------------------------- | ----------------------- | ---------------- | -------------------------- | ---------------------------- |
| health_beauty                         | 1.4M                    | —                | —                          | Top line; protect.           |
| watches_gifts                         | 1.3M                    | **275.57%**      | **8.42%**                  | Grow; favorable freight.     |
| bed_bath_table                        | 1.2M                    | —                | —                          | Top line; protect.           |
| sports_leisure                        | 1.1M                    | **200.28%**      | **17.11%**                 | Solid; monitor freight.      |
| telephony                             | 379K                    | **215.11%**      | **22.38%**                 | **Freight reduction.**       |
| stationery                            | 270K                    | **347.88%**      | **20.46%**                 | **Freight reduction.**       |
| signaling_and_security                | 28K                     | **642.27%**      | **30.39%**                 | **Highest freight; urgent.** |
| small_appliances_home_oven_and_coffee | 49K                     | **6087.68%**     | **5.70%**                  | Scale; replicate model.      |
| security_and_services                 | —                       | **0.00%**        | 14.55%                     | **Investigate stagnation.**  |


- **Actions:**
  - **Freight:** Focus on **signaling_and_security (30.39%)**, **telephony (22.38%)**, **stationery (20.46%)** — carrier renegotiation, packaging, fulfillment; target **−1.5 to −2.0 pp** freight ratio.
  - **Growth:** Double down on **watches_gifts** and **small_appliances_home_oven_and_coffee**; understand success factors and replicate where possible.
  - **Stagnant:** **security_and_services** at 0% growth — diagnose (lifecycle, pricing, marketing, relevance); decide re-strategy or resource reallocation.

---

## Cross-dashboard priorities (summary)


| #   | Priority                                   | Source dashboard                 | Metric / target                                                           |
| --- | ------------------------------------------ | -------------------------------- | ------------------------------------------------------------------------- |
| 1   | Retention and repeat purchases             | Executive + Customer & Retention | Lift repeat rate from ~3.12% toward 5%+; returning revenue share >10%.    |
| 2   | Reduce canceled/unavailable orders         | Executive                        | Recover ~200K+ revenue via stock accuracy and seller SLA.                 |
| 3   | Late orders and proactive communication    | Operations & CX                  | Reverse ~650% late-order spike; implement >2-day delay alerts.            |
| 4   | Freight cost reduction                     | Revenue & Commercial             | −1.5 to −2.0 pp freight in telephony, signaling_and_security, stationery. |
| 5   | Fix low ratings in high-revenue categories | Operations & CX                  | −3 pp low-rating share in top 5 categories/states with >12% low share.    |
| 6   | Payment and category strategy              | Revenue & Commercial             | Card-first and installment tuning; +10–15% revenue in funded categories.  |


---

*Document prepared for strategic use. All figures align with the Power BI dashboards as of the last refresh. Revalidate key numbers against the live reports when making decisions.*