# AAPL Advanced Python Analysis (AALP)
> Time-series analysis and feature engineering on two years of Apple Inc. (AAPL) historical stock data, built during Week 6 of the AnalystLab Africa internship.

---

## ⚙️ Project Type Flags
> *Check what applies. This helps reviewers and collaborators understand the nature of the work at a glance. Delete this block before publishing.*

- [x] Exploratory Data Analysis (EDA)
- [ ] SQL Analysis / Querying
- [x] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [x] Data Cleaning / Wrangling
- [ ] End-to-End (multiple of the above)
- [ ] Other: ___________

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Data Workflow](#5-data-workflow)
6. [Data Model & Schema](#6-data-model--schema)
7. [Analysis & Metrics](#7-analysis--metrics)
8. [Key Insights](#8-key-insights)
9. [Recommendations](#9-recommendations)
10. [Assumptions & Limitations](#10-assumptions--limitations)
11. [Future Enhancements](#11-future-enhancements)
12. [Deliverables](#12-deliverables)
13. [Author](#13-author)

---

## 1. Project Overview

**Context:** Week 6 of the AnalystLab Africa Data Analytics Internship (Batch A, May 1 – Jul 1, 2026) focused on advanced Python techniques for time-series data.

**Problem Statement:** How can Pandas-based data transformation, time-series analysis, and feature engineering be used to uncover meaningful trends and risk signals in historical stock price data?

**Approach:** Pulled two years of daily AAPL stock data via the yfinance API, cleaned and transformed it with Pandas, engineered time-series features (moving averages, monthly returns, volatility, cumulative return), and visualized the results with Matplotlib.

**Outcome:** A complete Jupyter notebook and insight report showing AAPL's ~47% cumulative gain over two years, a major single-day volatility event in April 2025, and rising short-term volatility heading into mid-2026.

---

## 2. Objectives

- **Primary Objective:** Apply advanced Pandas operations and time-series techniques to extract actionable insights from AAPL historical stock data.
- **Secondary Objective 1:** Engineer features (moving averages, % change, volatility) that support trend and momentum analysis.
- **Secondary Objective 2:** Communicate findings clearly through visualizations and a concise written summary.

> 💡 *Every analysis decision in this project traces back to one of these objectives.*

---

## 3. Project Scope & Tools

### Scope
:
Data Storage: 
Data Processing: 
Analysis: 
Visualization:
Version Control: 
Documentation:
Other:
| Dimension | Details |
|-----------|---------|
| **In Scope** | 501 trading days of AAPL daily price and volume data (Aug 8, 2024 – Aug 7, 2026). |
| **Out of Scope** | Predictive modeling or forecasting future prices — this project focuses on descriptive and exploratory time-series analysis, not prediction.|
| **Time Period** | August 8, 2024 – August 7, 2026 (approx. 2 years of daily trading data)
| **Granularity** | Daily (one row per trading day) |

### Tools & Technologies

| Category | Tool(s) Used |
|----------|-------------|
| Data Storage | None (data pulled live via yfinance API, not persisted to a database) |
| Data Processing | Python, Pandas, NumPy|
| Analysis |pandas (rolling windows, groupby/aggregation, pct_change) |
| Visualization |  Matplotlib |
| Version Control | Git / GitHub |
| Documentation | Markdown |
| Other | yfinance (data source API), Google Colab (execution environment) |

---

## 4. Repository Structure

```
├── data/         # Raw/reference data notes (data pulled live via yfinance)
├── notebooks/    # AAPL_Advanced_Python_Analysis.ipynb
├── reports/       # AAPL_Insight_Summary.docx
├── visuals/       # Exported chart images
└── docs/         # Supporting documentation
```
---

## 5. Data Workflow

```
Yahoo Finance via yfinance API]
     ↓
[yf.download() — daily OHLCV pull]
     ↓
[Missing-value/duplicate checks, datetime conversion, sorting]
     ↓
[Pandas — rolling windows, groupby, pct_change, feature engineering]
     ↓
[Matplotlib charts + written insight summary]

```

1. **Source:** Yahoo Finance, accessed via the yfinance Python library — 501 rows, daily OHLCV format, pulled live via API (no manual download).
2. **Ingestion:** yf.download("AAPL", period="2y", interval="1d") — pulled directly into a Pandas DataFrame.
3. **Cleaning:** Checked for missing values and duplicates (found zero of either); flattened a MultiIndex column structure returned by yfinance; converted Date to datetime and reset it from index to a regular column.
4. **Transformation:** Created Daily Change, Percentage Change, Year/Month/YearMonth grouping fields, 7-day and 30-day moving averages, 30-day annualized volatility, and cumulative return.
5. **Analysis:** Descriptive statistics, rolling-window time-series analysis, groupby/aggregation for monthly summaries, and filtering for high-momentum days (>3% single-day moves).
6. **Output:** 5 Matplotlib visualizations (price trend, volume trend, moving averages, monthly returns, volatility) plus a written insight summary document.

---

## 6. Data Model & Schema

### Dataset / Table: `[name]`

| Field Name | Data Type | Description | Example Value |
|------------|-----------|-------------|---------------|
| `Date` | date | Trading day | 2026-08-07 |
| `Open` | float | Opening price (USD)| 312.41 |
| `High` | float | Intraday high price (USD) | 314.20 |
| `Low` | float | Intraday low price (USD) |308.83 |
| `Close` | float| Closing price (USD)| 313.33 |
| `Adj Close` | float| Dividend/split-adjusted close (USD) | 311.48 |
| `Volume` | int | Shares traded | 47161100
Row count (approx.): |

> **Row count (approx.):** 501 rows
> **Date range:** August 8, 2024 – August 7, 2026
> **Key join / relationship:** Not applicable — single flat table, no joins
*Add additional table blocks as needed for multi-table projects.*

---

## 8. Analysis & Metrics

### Analytical Approach

This project used exploratory, descriptive time-series analysis rather than hypothesis testing or predictive modeling. The goal was to uncover patterns in price trend, momentum, and volatility using rolling-window calculations and period-over-period comparisons.
### Key Metrics Defined

| Metric | Plain-Language Definition | Why It Matters |
|--------|--------------------------|----------------|
| `7-Day / 30-Day Moving Average` | The average closing price over the last 7 or 30 trading days | Smooths daily noise to reveal short vs. medium-term trend direction and momentum shifts |
| `30-Day Annualized Volatility` | How much daily returns fluctuate, scaled to a yearly measure | Signals how risky/unstable the stock has been recently |
| `Cumulative Return %` | Total % gain or loss since the start of the dataset | Shows overall investment performance over the full period|

### Methods Used
- Methods Used (lines 164-169) — delete the unused bullets, keep these:
- Descriptive statistics — distribution, mean, min/max, standard deviation of daily prices
- Trend analysis across the 2-year period (Aug 2024 – Aug 2026)
- Rolling-window aggregation (7-day and 30-day moving averages, 30-day volatility) in Pandas
- Custom aggregation and feature engineering (daily % change, monthly returns, cumulative return) using Pandas groupby and rolling functions


---


## 9. Key Insights
**Insight 1: Strong Long-Term Uptrend**
AAPL rose from roughly $200 to over $325 across the two-year period — a cumulative gain of approximately 47%, despite short-term corrections along the way.

**Insight 2: April 2025 Volatility Event**
A single-day move of +15.33% on April 9, 2025 stands out as the most extreme price swing in the dataset, coinciding with a spike in 30-day volatility — likely tied to a major news or earnings event.

**Insight 3: Moving Average Crossovers Signal Momentum**
The 7-day moving average crossing above the 30-day moving average aligned with sustained rallies, while crossing below it preceded the April 2025 correction — a useful, simple momentum indicator.

**Insight 4: Rising Volatility Into 2026**
30-day annualized volatility climbed into the high-30%/low-40% range by mid-2026, alongside sharp monthly swings (May 2026: +11.39%, June 2026: -5.53%) — suggesting growing short-term uncertainty even as the long-term trend stayed positive.

---

## 10. Recommendations

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
| High | Use the 7-day/30-day MA crossover as a confirmation signal before acting on short-term price moves |Insight 3 | Investor/Analyst |
| Medium | Monitor 30-day volatility trend as an early warning indicator of elevated risk periods |Insight 4 |Investor/Analyst |
| Low |Extend analysis to 5-10 years of data to confirm whether the long-term uptrend holds across market cycles | Insight 1 |Future analysis |

---

## 11. Assumptions & Limitations

### Assumptions
- Treated Yahoo Finance data (via yfinance) as accurate and complete, without independently verifying against another data provider
- Assumed a standard 252-trading-day year for annualizing volatility
- Assumed no corporate actions (splits/dividends) materially distort the Close price beyond what Adjusted Close already accounts for

### Limitations
- Two years of data may not capture longer market cycles or major macroeconomic shifts
- No comparison benchmark (e.g., S&P 500) was included, so AAPL's performance isn't assessed relative to the broader market
- Analysis is descriptive only — no predictive or forecasting model was built
> *The goal here is pre-emptive Q&A. What would a thoughtful skeptic push back on? Document the answer here, before they ask.*

---

## 12. Future Enhancements

- [] Extend the analysis to a longer historical window (5–10 years).
- [] Compare AAPL against a market benchmark (e.g., S&P 500) or peer tech stocks.
- [] Add a simple predictive model (e.g., ARIMA or linear regression) for short-term price direction.

---

## 13. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| notebooks|  | full analysis notebook | AAPL_Advanced_Python_Analysis.ipynb |
| reports |  1–2 page insight summary | AAPL_Insight_Summary.docx |
| visuals | exported chart images | [`/path/to/file`] |

---

## 14. Author

**[Your Name]**
[Your role or title - current or target]

- 🔗 [LinkedIn URL]
- 💼 [Portfolio or GitHub profile URL]
- 📧 [Email - optional]

---

*Last updated: [Month YYYY]*
*If this template helped you, consider starring the repository.*
