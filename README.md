# Multi-Asset Portfolio Risk Early Warning System

> A rule-based risk scoring framework for Indian financial markets | April 2014 – March 2024

---

## What This Is

Most portfolio managers know when a crash has happened. The harder question is — when should you have reduced risk *before* it happened?

This project builds an Early Warning System (EWS) that answers that question systematically. It tracks nine macroeconomic and market indicators monthly, converts them into a single composite risk score between 0 and 10, and triggers Green / Amber / Red signals that prescribe specific portfolio reallocation actions.

The system was backtested across 119 months of Indian financial market data. The EWS portfolio outperformed a static buy-and-hold portfolio on every single metric.

---

## Results

| Metric | Static Portfolio | EWS Portfolio |
|---|---|---|
| Cumulative Return | 129% | **135%** |
| Max Monthly Drawdown | -15.32% | **-13.00%** |
| Mean Monthly Return | 0.74% | **0.76%** |
| Sharpe Ratio | 0.081 | **0.097** |
| Monte Carlo Worst Case | -8.75% | **-3.48%** |
| Monte Carlo Mean Outcome | 7.52% | **9.82%** |

---

## The Portfolio

Six assets representing a realistic Indian multi-asset mandate:

| Asset | Instrument | Base Weight |
|---|---|---|
| Equity | Nifty 50 | 35% |
| Banking | Nifty Bank | 15% |
| IT | Nifty IT | 10% |
| Gold | MCX Gold (₹/10gm) | 15% |
| Bonds | 10Y G-Sec Yield | 20% |
| Currency | USD/INR | 5% |

---

## The EWS Framework

### Nine Indicators Across Three Categories

| Category | Weight | Indicators |
|---|---|---|
| Market | 55% | India VIX, Nifty PE Ratio, Gold/Nifty Ratio |
| External | 35% | USD/INR Change, Brent Crude Change, FII Net Flows |
| Macro | 10% | GDP Growth, CPI Inflation, Repo Rate |

Market indicators carry the highest weight because they move in real time. Macro indicators are underweighted — GDP and Repo Rate change slowly and don't give actionable signals month to month.

### Composite Score Formula

```
Risk Score = (Market Score × 55%) + (External Score × 35%) + (Macro Score × 10%)
```

All indicators normalised to 0–10 scale using percentile-based capping (5th–95th percentile) to prevent extreme outliers from dominating the score.

### Signal Thresholds

| Score | Signal | Action | Months Triggered |
|---|---|---|---|
| 0.0 – 5.0 | 🟢 Green | Hold — full positions | 100 (83%) |
| 5.1 – 6.5 | 🟡 Amber | Reduce equity, increase safe havens | 15 (13%) |
| 6.5 – 10.0 | 🔴 Red | Defensive — minimum equity, maximum gold + bonds | 4 (3%) |

---

## Decision Rules — Built From Evidence

Reallocation weights were not set arbitrarily. They were derived by analysing how each asset actually performed during four historical stress events.

### Stress Events Analysed

| Event | Period |
|---|---|
| 2016 Demonetisation | Nov 2016 – Mar 2017 |
| 2018 IL&FS Crisis | Sep 2018 – Mar 2019 |
| 2020 COVID Crash | Feb 2020 – Aug 2020 |
| 2022 Rate Hike Cycle | Mar 2022 – Feb 2023 |

### Key Findings From Stress Analysis

- **Nifty Bank** was the worst performer in 3 out of 4 stress events — reduced most aggressively in Red
- **Nifty IT** showed mixed behaviour — badly hurt by rate hikes but fastest recovery in COVID — kept relatively high even in defensive mode
- **Bonds** were the most consistent safe haven across all scenarios — highest allocation in Red
- **Gold** reliable only in COVID — modest increase, not primary safe haven

### Portfolio Allocation by Signal

| Asset | 🟢 Green | 🟡 Amber | 🔴 Red |
|---|---|---|---|
| Nifty 50 | 35% | 30% | 15% |
| Nifty Bank | 15% | 12% | 3% |
| Nifty IT | 10% | 9% | 7% |
| Gold | 15% | 20% | 33% |
| Bonds | 20% | 25% | 35% |
| USD/INR | 5% | 4% | 7% |

---

## Monte Carlo Simulation

100 simulations over 12 forward months based on historical return distributions.

| Scenario | Static Portfolio | EWS Portfolio |
|---|---|---|
| Best Case (95th Pct.) | 26.22% | 27.95% |
| Most Likely (50th Pct.) | 6.44% | 8.57% |
| Worst Case (5th Pct.) | -8.75% | -3.48% |
| Mean Outcome | 7.52% | 9.82% |
| Std Deviation | 11.5% | 10.4% |

The EWS cuts worst-case loss by 5.27 percentage points while improving expected return by 2.30 percentage points.

---

## Excel Workbook Structure

| Sheet | Contents |
|---|---|
| Indicators | 9 raw indicator values — monthly 2014–2024 |
| Assets | 6 asset prices and monthly % returns |
| Normalisation | 0–10 scaled indicators with percentile capping |
| Risk Score | Weighted composite score + category scores + signal |
| Signal Rules | Score threshold reference table |
| Portfolio Allocation | Evidence-based weights by signal |
| Stress Returns | Monthly asset returns during 4 stress events |
| Scenario Testing | EWS score and signal during stress periods |
| Backtesting | EWS vs static portfolio — monthly comparison |
| Monte Carlo (Actual) | 100 simulations — static portfolio |
| Monte Carlo (EWS) | 100 simulations — EWS portfolio |
| Summary | Complete results comparison |

---

## Data Sources

| Source | Data |
|---|---|
| NSE India | Nifty 50, Nifty Bank, Nifty IT, India VIX, PE Ratio |
| RBI DBIE | Repo Rate, CPI, 10Y G-Sec Yield, USD/INR |
| MOSPI | GDP Growth (quarterly) |
| SEBI | FII/FPI Net Flows (monthly) |
| Investing.com | Brent Crude, MCX Gold |

---
## Skills Demonstrated

### Excel Modelling
- Built 12 interconnected sheets with cross-sheet formula referencing throughout
- Percentile-based normalisation (5th–95th) to handle outliers in VIX and FII flow data
- Nested IF logic for dynamic signal-based portfolio allocation
- Cumulative return compounding using iterative row-by-row multiplication
- NORM.INV with RAND() for Monte Carlo simulation across 100 columns × 12 rows
- PERCENTILE, COUNTIF, PRODUCT array formulas for summary statistics

### Risk Framework Design
- Designed a composite scoring system from scratch — indicator selection, weighting rationale, threshold calibration
- Iteratively adjusted signal thresholds based on actual data distribution — not arbitrary cutoffs
- Evidence-based decision rules derived from stress period asset behaviour, not theoretical assumptions
- Balanced the classic risk-return tradeoff — EWS reduces risk without sacrificing returns

### Quantitative Analysis
- Normalised nine heterogeneous indicators to a common 0–10 scale
- Weighted composite scoring across three categories with documented rationale
- Backtesting framework comparing EWS vs static portfolio across 119 months
- Monte Carlo simulation to quantify forward-looking tail risk
- Sharpe Ratio calculation and interpretation for risk-adjusted performance comparison

### Financial Markets Knowledge
- Multi-asset portfolio construction across equity, fixed income, commodity and currency
- Understanding of how different assets behave during different stress regimes — credit crisis vs pandemic vs rate hike cycle
- Use of market-based indicators (VIX, PE ratio, FII flows) as leading signals vs lagging macro data
- RBI monetary policy cycles and their impact on duration-sensitive assets

### Data Collection & Management
- Sourced 10 years of monthly data across 5 independent data sources
- Converted international gold prices (USD/troy oz) to domestic format (INR/10gm)
- Handled quarterly GDP data interpolated to monthly frequency
- Structured all data for Power BI compatibility — clean headers, unpivoted tables, no merged cells

---


## Limitations

- Signal thresholds calibrated on the same dataset used for backtesting — out-of-sample testing would strengthen validity
- Linear normalisation assumes stable indicator relationships across the full period
- Monthly frequency limits intra-month signal detection
- Does not account for transaction costs of rebalancing

---

## Author

**Abhinav Saharan**  
FRM Candidate | B.Com + MA Economics  
*Risk Analyst Portfolio Project — March 2026*

---

## License

MIT License — free to use with attribution.
