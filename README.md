# Is the Algorithm Punishing Struggling Sellers Twice? A Marketplace Risk Study.

Diagnosing a fulfillment-to-exposure feedback loop in marketplace seller performance.

---

## Executive Summary

This project investigates whether sellers who fail to meet delivery expectations experience a compounding decline in algorithmic visibility, customer ratings, and returns. **And quantifies how much of the marketplace's revenue and refund cost is concentrated in this at-risk group**.

Using a synthetic but realistically messy marketplace dataset (sellers, products, orders, algorithmic exposure, reviews, and returns), this analysis builds a full pipeline of cleaning, metric development, statistical validation, a custom seller risk score, and an interactive Power BI dashboard. To move from a hypothesis to a defensible, quantified business finding.

**Headline results:**
- **~32%** of all orders had a fulfillment problem (delayed, cancelled, or returned)
- Struggling sellers' exposure score dropped from an average of **~60 to ~17** in the weeks following their first serious SLA breach
- SLA breach rate correlates **-0.44** with exposure score, **-0.53** with rating, and **+0.48** with return rate
- **71%** of all returns are explicitly reported by customers as due to late delivery
- Sellers flagged at-risk by a custom Health Score represent ~26% of all sellers but account for **25.7% of total marketplace revenue** and **43% of all refund costs**

---

## Business Problem

Marketplace platforms rely on algorithms to decide which sellers' products get shown to customers, and these algorithms typically factor in customer ratings as a signal of seller quality. A seller starts missing delivery deadlines, customers respond with lower ratings and reviews. And the algorithm reading those lower ratings as a quality signal, reduces that seller's visibility as a result.

But this creates a risk. If reduced visibility further starves a struggling seller of orders, it can accelerate their decline rather than give them room to recover. A feedback loop where the platform's own system makes the underlying problem worse, not better.

**The core question this project answers:** Does the data show that struggling sellers keep getting worse, how many sellers are affected, and how much revenue the business is losing because of it?
---

## Solution

The project was built in five stages:

1. **Data cleaning** — resolved inconsistent date formats, currency formatting, region naming, duplicate records, and missing values, with each fix validated against the raw data (e.g. confirming missing delivery dates were tied specifically to cancelled orders, not random gaps)
2. **Metrics development** — built weekly SLA breach rate, average rating, average exposure score, and return rate per seller, merged into a single seller-week analysis table
3. **Event-study analysis** — re-centered each struggling seller's timeline on their own individual breach onset date (rather than a shared calendar date), to test whether exposure decline follows breach onset specifically, not just correlates with it generally
4. **Seller Health Score** — a weighted composite score (35% breach rate, 30% exposure, 20% rating, 15% returns) built to flag at-risk sellers using a single, interpretable number
5. **Business impact quantification** — calculated the share of total revenue and refund cost tied to the at-risk cohort, and built a 3-page Power BI dashboard for ongoing monitoring

---

## Tech Stack

- **Python** (pandas, numpy) — data cleaning, metric development, statistical analysis
- **SQL** — alternative cleaning implementation
- **Power BI / DAX** — interactive dashboard and business-facing measures
- **Jupyter Notebook** — full analysis workflow

---

## Dashboard Screenshots

markdown
   <img width="1303" height="730" alt="Overview" src="https://github.com/user-attachments/assets/e615748c-589a-48d1-b46b-8b2b64830928" />
   <img width="1303" height="733" alt="Trend" src="https://github.com/user-attachments/assets/a28ca2ae-2383-4cef-95c2-fbba7ad7d703" />
   <img width="1306" height="737" alt="Returns" src="https://github.com/user-attachments/assets/bb59bce2-6b8f-4e77-b832-a023fd402135" />



---

## Key Findings

| Finding | Evidence |
|---|---|
| Fulfillment problems are widespread | **32% of all orders had a delivery issue** |
| Exposure declines specifically after breach onset, not randomly | Event-study alignment across 10 struggling sellers |
| The relationship is consistent across multiple signals | Breach rate correlates with rating, exposure, and return rate |
| Late delivery is the dominant driver of returns | 71% of all returns explicitly cite late delivery |
| The at-risk cohort is a disproportionate cost center | **26% of sellers, 25.7% of revenue, 43% of refund cost** |

---

## Limitations

- Same-week correlation between SLA breach rate and revenue was not statistically meaningful; a longer-lag analysis would be needed to confirm a downstream revenue effect
- Some points in the event study analysis are based on a small number of contributing sellers, which is noted directly alongside the relevant chart rather than hidden
- The dataset is synthetic, constructed to reflect realistic e-commerce marketplace dynamics rather than sourced from a live platform

---

## Recommendation

Introduce a temporary exposure floor for sellers on their first SLA breach, paired with an early-warning alert to operations before the algorithm's visibility penalty escalates , targeting sellers who cross into the "at-risk" tier of the Health Score. Given the concentration of revenue and refund cost already observed in this group, even a modest reduction in the feedback loop's severity represents a meaningful business opportunity.

---

## Repository Structure

```
marketplace-seller-risk-scoring/
├── README.md
├── data/
│   ├── raw/
│   └── clean/
├── notebooks/
│   └── analysis.ipynb
├── dashboard/
│   ├── seller_risk_dashboard.pbix
│   └── screenshots/
└── scripts/
    └── generate_dataset.py
```

---

## Author

Fannana Fahreen Aanan

