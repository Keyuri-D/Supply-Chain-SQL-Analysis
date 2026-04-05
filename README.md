# Supply Chain SQL Analysis
**Tool:** SQLite via DB Browser  
**Domain:** Consumer Goods — Cosmetics, Haircare & Skincare  
**Queries:** 6 | **Dataset:** 100 SKUs across 5 suppliers

---

## Overview

A structured SQL analysis of a consumer goods supply chain dataset, progressing from basic aggregations to advanced risk classification using CASE statements. Built to demonstrate applied SQL skills in an operational business context — identifying revenue drivers, supplier risk, inventory health, and shipping efficiency.

This project complements the [Power BI Supply Chain Dashboard](https://github.com/Keyuri-D/Consumer-Goods-Supply-Chain-Dashboard) built on the same dataset — the SQL queries produce the same insights as the dashboard visuals, but through raw query logic rather than drag-and-drop tools.

---

## Key Findings

- **Skincare drives the most revenue** ($241K) but cosmetics commands the highest average price ($57)
- **Supplier 5 has the highest defect rate** (2.67%) — flagged as the highest quality risk across all suppliers
- **Supplier 1 is the strongest performer** — lowest defect rate (1.8%) and highest order volume (1,458 units)
- **Sea freight is the most cost-efficient** transport mode at $8.33 per unit, though Road is fastest at 4.7 days average
- **Critical margin risk identified:** Skincare from Supplier 4 has a manufacturing cost ($85.64) exceeding its revenue per unit ($80.91) — a loss-making combination
- **Highest margin opportunity:** Cosmetics from Supplier 3 generates $240.58 revenue per unit at only $17.80 manufacturing cost — but carries a 3.87% defect rate (Critical Risk)

---

## Queries

### Query 1 — Revenue & Orders by Product Type
Basic aggregation showing which product category drives the most revenue, total orders, and average price. Entry point for understanding the product portfolio.

**Skills:** `SELECT`, `GROUP BY`, `SUM`, `AVG`, `COUNT`, `ROUND`, `ORDER BY`

| Product type | Total SKUs | Total Revenue | Total Orders | Avg Price |
|---|---|---|---|---|
| Skincare | 40 | $241,628 | 2,099 | $47.26 |
| Haircare | 34 | $174,455 | 1,480 | $46.01 |
| Cosmetics | 26 | $161,521 | 1,343 | $57.36 |

---

### Query 2 — Supplier Performance Ranking
Ranks all 5 suppliers by average defect rate, combined with lead time and order volume — a multi-metric supplier scorecard.

**Skills:** Multi-column aggregation, `ORDER BY` on calculated field

| Supplier | Avg Defect Rate | Avg Lead Time | Total Orders |
|---|---|---|---|
| Supplier 5 | 2.67% | 14.7 days | 968 |
| Supplier 3 | 2.47% | 14.3 days | 632 |
| Supplier 1 | 1.80% | 16.8 days | 1,458 |

---

### Query 3 — Shipping Cost Efficiency by Transport Mode
Calculates cost per unit for each transportation mode, revealing the trade-off between speed and cost across Road, Air, Rail, and Sea.

**Skills:** Division for ratio metrics, `AVG`, `SUM`, multi-metric comparison

| Mode | Cost Per Unit | Avg Shipping Days |
|---|---|---|
| Sea | $8.33 | 7.1 |
| Air | $10.89 | 5.1 |
| Rail | $11.30 | 6.6 |
| Road | $11.58 | 4.7 |

---

### Query 4 — Stock to Sales Ratio (Overstock Risk)
Identifies SKUs with excess inventory relative to demand. Uses `NULLIF` to prevent divide-by-zero errors — a real data quality technique.

**Skills:** `CAST`, `NULLIF`, ratio calculation, divide-by-zero handling

**Key finding:** SKU74 has a stock-to-sales ratio of 41.0 — 41x more inventory than orders received. A clear overstock flag for procurement review.

---

### Query 5 — Revenue Per Unit by Product & Supplier
Groups by both product type and supplier to identify which combinations generate the most revenue per unit sold, alongside manufacturing cost — a margin analysis.

**Skills:** Multi-column `GROUP BY`, nested aggregation, margin analysis

**Key finding:** Skincare from Supplier 4 generates $80.91 revenue per unit against $85.64 manufacturing cost — a loss-making product-supplier combination requiring immediate attention.

---

### Query 6 — Defect Risk Classification (CASE Statement)
Assigns a risk tier (Critical / High / Moderate / Acceptable) to every product-supplier combination based on average defect rate thresholds. The most advanced query in the project.

**Skills:** `CASE` statement, conditional logic, risk tiering, threshold-based classification

| Product | Supplier | Defect Rate | Classification |
|---|---|---|---|
| Cosmetics | Supplier 3 | 3.87% | Critical Risk |
| Skincare | Supplier 5 | 3.47% | Critical Risk |
| Haircare | Supplier 5 | 2.77% | High Risk |
| Cosmetics | Supplier 1 | 1.56% | Moderate Risk |

---

## SQL Concepts Demonstrated

| Concept | Query |
|---|---|
| Basic aggregation (SUM, AVG, COUNT) | 1, 2, 3 |
| Multi-column GROUP BY | 2, 5 |
| Ratio / division metrics | 3, 4, 5 |
| CAST for type conversion | 4 |
| NULLIF for divide-by-zero handling | 4, 5 |
| CASE statement for classification | 6 |
| Multi-condition conditional logic | 6 |

---

## Technical Notes

- **Tool:** DB Browser for SQLite (free, no server required)
- **Column name sensitivity:** SQLite column names are case and character sensitive. Always run `PRAGMA table_info(table_name)` on a new dataset before writing queries to confirm exact column names — silent failures (returning 0 or NULL) occur when names don't match exactly.
- **Dataset source:** Supply Chain Analysis dataset (Kaggle — Statso), 100 SKUs

---

## Files

- `supply_chain_analysis.sql` — all 6 queries with comments
- `README.md` — project documentation and findings

---

## Related Projects

- [Consumer Goods Supply Chain Dashboard (Power BI)](https://github.com/Keyuri-D/Consumer-Goods-Supply-Chain-Dashboard) — same dataset visualized in Power BI with 3-page interactive report

---

## About

**Keyuri Dodia**  
Continuous Improvement Specialist | Business Analysis & Operations  
[LinkedIn](https://linkedin.com/in/keyuri-dodia) | keyuridodia117@gmail.com
