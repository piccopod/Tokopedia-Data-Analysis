# Promo Efficiency & User Retention at Tokopedia
### Beyond Discounts: Reliable Delivery as the Key to User Loyalty


**Author:** Bunga Safhira  
**Date:** November 2026  
**Data Period:** January 2023 – December 2024  
**Target Stakeholders:** Tokopedia Management, Growth & Marketing, Operations, Data Engineering

---

## Executive Summary

> **Core Answer:** Fulfillment issues are strongly associated with lost repeat revenue, and promotional incentives do not offset the damage. Fixing voucher rules and delivery promises unlocks immediate cost savings while protecting long-term user retention.

An analysis of **268,076 cleaned transactions** and a **60-day cohort of 39,363 users** reveals two major value leaks at Tokopedia:

1. **Inefficient Promo Spend (Cost Leak):** Tokopedia spends **Rp6.39 billion/year** on promotions, yet **59% (Rp3.77 billion)** goes to orders where the promo exceeds the basket value (just 4.4% of orders). Promos show **zero statistically significant lift** in 60-day repeat rate (**74.74%** with promo vs. **74.70%** without promo, $p = 0.888$) or 365-day user GMV.
2. **Delivery Delays Eroding Loyalty (Revenue Leak):** **34.9%** of deliveries arrive late, slashing 60-day repeat rates from **79.2%** (on-time) to **66.2%** (late)—a consistent $\approx 13$ percentage point (pp) drop across all 29 customer segments. This puts **Rp5.03 billion in annual GMV at risk**.
3. **Controllable Root Causes:** **81.5%** of late deliveries miss their SLA by only **1–2 days**, and campaign delay spikes are heavily concentrated in **GoTo Logistics** on outer-island SLA tiers (**67.7%** late vs. **39.5%** for other couriers).

| Metric | Key Figure | Business Implication |
| :--- | :--- | :--- |
| **Annual Promo Spend** | Rp6.39B / year | 80.3% absorbed by large vouchers (Rp400k–Rp1M) with no retention lift |
| **Promo > Basket Value** | 59% of budget | Rp3.77B spent to generate Rp1.44B in GMV (4.4% of orders) |
| **Late Delivery Rate** | 34.9% | 81.5% miss SLA by only 1–2 days |
| **60-Day Repeat Rate** | 74.7% overall | 79.2% (on-time) vs. 66.2% (late) across 39,363 cohort users |
| **Annual GMV at Risk** | Rp5.03B / year | Driven by ~7,423 users/year experiencing a late first order |
| **Immediate Savings Potential** | Rp2.33B / year | ~37% promo budget reduction via promo cap & minimum spend rules |

---

## Business Context & Problem Statement

While Tokopedia holds a **34% market share** of Indonesia's e-commerce GMV (2024) in a market where **51%** of online shoppers are discount seekers, parent group GoTo has shifted focus toward sustainable profitability (cutting Rp2.8T in incentives and marketing in Q4 2022, $-34\%$ YoY). Internally, Growth & Marketing flagged an eroding **CLV:CAC ratio ($\le 3:1$)** alongside rising post-purchase delivery and customer service complaints reported by Operations.

### Primary Business Question
> *"Do fulfillment issues cause Tokopedia to lose repeat revenue opportunities despite allocating promotional incentives?"*

### Project Goals
1. **Promo Budget Optimization:** Ensure promotional spend drives long-term Customer Lifetime Value (CLV) rather than one-off subsidized transactions.
2. **User Retention Improvement:** Identify actionable, low-cost levers to increase sustainable repeat purchases.

---

## Key Findings

### 1. High Promo Spend Without Retention or GMV Lift
* **No Retention Impact:** First-order promo usage does not improve 60-day retention (**74.74%** promo vs. **74.70%** non-promo, $p = 0.888$). This holds across all four acquisition channels (Organic, Ads, Referral, Affiliate).
* **No Long-Term Value Lift:** 365-day GMV per user is virtually identical across **No Promo (Rp4.16M)**, **Normal Promo (Rp4.12M)**, and **Large Voucher (Rp4.14M)** users.
* **Budget Leakage via Large Vouchers:** Vouchers of **Rp400k–Rp1M** account for only **10%** of promo orders but consume **80.3% (Rp5.13B/year)** of the total promo budget. They account for **96.4%** of transactions where `promo_amount > total_amount` (median voucher Rp748,716 vs. median basket Rp354,161; correlation $r = -0.01$).
* **Rule Flaw, Not Fraud:** Concentration tests show large vouchers are distributed randomly across users, sellers, and dates (matching random expectation almost identically). The leak is caused by missing minimum-spend and cap rules, not coordinated abuse.

### 2. Late Deliveries Severely Erode Repeat Purchases
* **Universal ~13 pp Drop:** Late first orders reduce 60-day repeat rates by **10.2 to 21.5 pp** across all 29 analyzed segments. Promos do **not** cushion this impact (difference of $+1.1$ pp, $p = 0.27$).
* **Severe Delays Destroy Loyalty:** Users delayed by **$> 5$ days** have only a **22.6%** repeat rate. Around **2,540 severe cases/year** (delayed $> 5$ days, failed first delivery, or filed a delay complaint) average just **25.0%** repeat rate.
* **Critical 30-Day Window:** The retention gap opens within the first **30 days** ($11.5$ pp) and remains permanently locked through day 150 ($13.5$ pp).
* **How to Recover Users:** Faster CS ticket resolution alone does **not** restore retention ($+0.5$ pp after controlling for case severity, $p = 0.84$). Recovery happens when the **next order arrives on time**, bringing repeat rates to the 3rd order back to **78.8%** (nearly matching the **79.7%** baseline for consistently on-time users).

### 3. Operational Root Causes Are Controllable
* **Thin SLA Misses:** **81.5%** of late deliveries are only **1–2 days** past the promised SLA. Simulating a **+1 day ETA buffer** drops the late delivery rate from **34.9% to 12.2%**. Meanwhile, the heavy tail of **8–18 day delays (5.9%)** requires early detection and escalation.
* **Campaign Bottleneck at GoTo Logistics:** During campaign periods (e.g., WIB), daily volume rises $\approx 3.7\times$. On outer-island SLA tiers, **GoTo Logistics** handles **37.5%** of volume with a **67.7%** late rate compared to **$\approx 39.5\%$** for other couriers.
* **Misleading Shipping Zone Labels:** The `shipping_zone` field reflects **SLA tiers, not actual geography**—matching true seller-to-destination routes only **30.4%** of the time (equivalent to random). Decisions regarding regional warehousing cannot rely on this column.

---

## Strategic Recommendations

| Priority | Recommendation | Expected Impact (Annualized) | Effort (1–5) | Confidence | Proposed Owner |
| :---: | :--- | :--- | :---: | :---: | :--- |
| **1** | **Cap promo $\le$ basket value & enforce minimum spend** for vouchers $\ge$ Rp400k | Save **Rp2.33B/year** ($\approx 37\%$ of promo budget; promo/GMV drops from 4.45% to $\approx 2.8\%$) | 1 | High | Growth & Marketing |
| **2** | **A/B Pilot: Realistic ETA (SLA + 1 day), proactive notifications, & recovery vouchers** for severe cases | Late rate **34.9% $\to$ 12.2%**; +10 pp retention lift on severe cases = **+Rp1.31B GMV** (voucher cost: Rp15.4M) | 1–2 | Medium | Operations & Growth/Marketing |
| **3** | **Reallocate outer-island campaign volume** from GoTo Logistics to JNE, SiCepat, or AnterAja | **$\approx 669$ fewer late deliveries/year** ($\approx$ Rp100M first-order retention GMV/year) | 2 | High | Operations |
| **4** | **Resolve data quality gaps** (`total_amount`/`promo_amount` definitions, `shipping_zone`, add `origin_warehouse_city`) | Enables accurate margin & geographic logistics decisions | — | High | Data Engineering |

### Target & Pilot Validation
* **Goal 2 Target:** Closing **25%** of the late-delivery retention gap preserves an estimated **Rp1.26 billion in annual GMV** ($\approx 424$ additional repeat customers in the analyzed cohort).
* **A/B Testing Design:** Validate retention levers via 50:50 user-level randomization (hashed `user_id`; 1,000$\times$ A/A test verified 5.0% false positive rate). Measuring a +10 pp lift on severe cases requires 277 users per group.
* **Deferred Initiatives:** Regional warehousing outside Java ($\approx$ Rp190M retention GMV), blanket campaign cargo expansion ($\approx$ Rp59M), blanket late-delivery vouchers, and CS ticket priority queues alone are deferred due to low ROI or weak data backing.

---

## Data Architecture & Pipeline

### Data Source & Volume
Raw data was extracted from Google BigQuery (`datalake_tokped`), cleaned and transformed in Python, and loaded into `datawarehouse_tokped` alongside an audit table (`audit_removed_records`). Less than **0.7%** of records were removed; anomalies were corrected or quarantined with full traceability.

| Table | Raw Rows | Clean Rows | Removed | Role in `order_master` |
| :--- | :---: | :---: | :---: | :--- |
| `users` | 52,847 | 52,847 | 0 (0.00%) | User dimension (many-to-one) |
| `sellers` | 1,238 | 1,238 | 0 (0.00%) | Seller dimension (many-to-one) |
| `transactions` | 269,953 | 268,076 | $-1,877$ (0.70%) | Primary fact table (PK: `order_id`) |
| `deliveries` | 261,525 | 260,208 | $-1,317$ (0.50%) | Delivery fact (one-to-one) |
| `customer_service_tickets` | 31,553 | 31,428 | $-125$ (0.40%) | Aggregated to `ticket_count` per order |
| **`order_master`** | — | **268,076 $\times$ 50 cols** | — | **Unified order-level analytical table** |

### Key Cleaning & Feature Engineering Steps
* **Standardization:** Consolidated `payment_method` (27 $\to$ 16 labels), standardized Jakarta city names (2,397 users; 19,316 deliveries), and corrected 952 mismatched city-province pairs.
* **Anomaly Handling:** Corrected 792 erroneous 1970/2030 `order_date` values from `order_id`, quarantined 390 `total_amount` $\le 0$ records and 531 deliveries predating `order_date`, removed 1,071 exact duplicates and 384 extreme outliers ($\ge$ Rp200M).
* **Engineered Features:** `delivery_duration_days`, `late_delivery`, `days_over_sla`, `voucher_besar` ($\ge$ Rp400k), `first_order`, and 60-day / 90-day full follow-up cohorts.

---

## Tech Stack & Statistical Methodology

* **Data Warehouse:** Google BigQuery (`datalake_tokped` $\to$ `datawarehouse_tokped`)
* **Analysis & Wrangling:** Python (Google Colab) — `pandas`, `NumPy`, `SciPy`, `pandas-gbq`
* **Visualization & BI:** `matplotlib`, `seaborn`, Looker Studio (Interactive Dashboard)
* **Statistical Rigor:**
  * Two-proportion z-tests with 95% Wilson Confidence Intervals
  * Chi-square tests, Mann-Whitney U tests, Holm-Bonferroni correction
  * Permutation tests & bootstrapping
  * Mantel-Haenszel stratification across 29 segments (prioritizing auditable, interpretable statistics over black-box ML)

---

## Limitations & Data Quality Caveats

1. **Observational Design:** Findings represent strong statistical associations rather than guaranteed causal effects; retention levers should be validated via A/B pilots before full rollout.
2. **Margin Proxy:** GMV is used as a proxy for value; net profit margins and the platform vs. seller promo funding split are unavailable in the dataset.
3. **Cohort Boundary:** "First order" refers to the first observed order starting January 2023. The declining repeat trend noted in the initial business brief was not reflected in this dataset (90-day repeat remained stable at 75–78% per quarter).
4. **Geographic Blind Spot:** `shipping_zone` does not map to physical geography, and `origin_warehouse_city` is currently missing.

---

## Suggested Repository Structure

```text
├── README.md                                  # Project overview and executive summary
├── presentation/
│   └── Tokopedia_Promo_Retensi_Deck_Final.pptx # Full executive slide deck
├── notebooks/
│   ├── 01_data_extraction_and_cleaning.ipynb  # BigQuery ETL, wrangling & audit log
│   ├── 02_exploratory_and_promo_analysis.ipynb# Promo efficiency & voucher leak analysis
│   └── 03_fulfillment_and_retention_stats.ipynb# SLA delays, stratification & A/B sizing
└── sql/
    └── build_order_master.sql                 # BigQuery table merge & validation queries
```

---

## Links & Contact

* **Author:** Bunga Safhira
* **LinkedIn:** [[Bunga Safhira]((https://www.linkedin.com/in/bungaswirata/#)))](#)[](https://www.linkedin.com/in/bungaswirata/)](#)
* **Interactive Dashboard:** [[Looker Studio — Promo & Retensi](https://datastudio.google.com/u/0/reporting/b736bc66-36f4-4385-ab61-a6973965d87d/page/VpxDG)](#)
