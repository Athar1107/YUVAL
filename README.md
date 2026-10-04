# Logistics Strategic Planning & Data Exploration

Internship task — Week 1: strategic planning and exploratory data analysis on a supply chain logistics dataset, applying regression, classification, and clustering to evaluate whether operational telemetry can predict delay and risk outcomes.

## Project Overview

This project analyzes an hourly supply chain monitoring dataset (32,065 records, Jan 2021–Aug 2024) covering traffic, weather, port congestion, fuel consumption, driver behavior, and fatigue, alongside delivery outcomes (delay, risk classification, fulfillment status). The goal was to define logistics KPIs, explore the data, and test whether data science techniques — regression, classification, clustering — could predict delay risk from operating conditions.

## Key Findings

- **No predictive relationship found** between operational features and delay outcomes across all three modeling approaches tested (regression, classification, clustering).
- **Data leakage identified and corrected**: an initial classifier scored a perfect 1.00 F1 — traced to `disruption_likelihood_score` directly encoding the target label. Removing it dropped the model to majority-class guessing (0.75 accuracy, 0% recall on minority classes).
- **Clustering** produced four distinct operating-condition groups (driven by port congestion and fatigue), but risk composition was nearly identical across all four (~75% High Risk each).
- Full reasoning and evidence are documented in the report under `report/`.

## Repository Structure

```
logistics-analysis/
├── data/
│   └── dynamic_supply_chain_logistics_dataset.csv
├── notebooks/
│   └── 01_eda.ipynb          # full analysis: KPIs, EDA, regression, classification, clustering
├── report/
│   └── Logistics_Analysis_Report.docx
├── requirements.txt
└── README.md
```

## Setup

```bash
git clone <your-repo-url>
cd logistics-analysis
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Mac/Linux
pip install -r requirements.txt
```

Open `notebooks/01_eda.ipynb` in VS Code or Jupyter and run the cells in order.

## KPIs Tracked

| KPI | Value |
|---|---|
| Fulfillment Rate | 60.1% |
| Avg. Delivery Time Deviation | 5.18 hrs |
| Network Risk Exposure (% High Risk) | 74.7% |
| Avg. Shipping Cost | 459.37 (dataset units) |
| Avg. Supplier Reliability Score | 0.50 |

## Methodology

1. **Data cleaning** — checked for missing values (none found) and validated GPS bounds
2. **EDA** — computed KPIs; checked Pearson and Spearman correlations between operating features and delay outcomes
3. **Regression** — predicted `delivery_time_deviation` (Linear Regression)
4. **Classification** — predicted `risk_classification` (Random Forest), including a leakage check and correction
5. **Clustering** — grouped hours by operating-condition profile (K-Means, k=4 via elbow method)
6. **Evaluation** — cross-checked results across all three techniques for consistency

## Tools

Python, pandas, scikit-learn, matplotlib, seaborn

## Author

[Your name] — Internship Week 1 Task
