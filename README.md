# Risk-Early-Warning-Model
Rule-based Early Warning System that scores portfolio risk across 9 macro and market indicators - backtested across 10 years of Indian financial market data with Monte Carlo simulation.
Most portfolio managers know when a crash has happened. The harder question is — when should you have reduced risk before it happened?
This project builds an Early Warning System (EWS) that answers that question systematically. It tracks nine macroeconomic and market indicators monthly, converts them into a single composite risk score between 0 and 10, and triggers Green / Amber / Red signals that prescribe specific portfolio reallocation actions.
The system was backtested across 119 months of Indian financial market data. The EWS portfolio outperformed a static buy-and-hold portfolio on every single metric.

Results
MetricStatic PortfolioEWS PortfolioCumulative Return129%135%Max Monthly Drawdown-15.32%-13.00%Mean Monthly Return0.74%0.76%Sharpe Ratio0.0810.097Monte Carlo Worst Case-8.75%-3.48%Monte Carlo Mean Outcome7.52%9.82%

The Portfolio
Six assets representing a realistic Indian multi-asset mandate:
AssetInstrumentBase WeightEquityNifty 5035%BankingNifty Bank15%ITNifty IT10%GoldMCX Gold (₹/10gm)15%Bonds10Y G-Sec Yield20%CurrencyUSD/INR5%

The EWS Framework
Nine Indicators Across Three Categories
CategoryWeightIndicatorsMarket55%India VIX, Nifty PE Ratio, Gold/Nifty RatioExternal35%USD/INR Change, Brent Crude Change, FII Net FlowsMacro10%GDP Growth, CPI Inflation, Repo Rate
Market indicators carry the highest weight because they move in real time. Macro indicators are underweighted — GDP and Repo Rate change slowly and don't give actionable signals month to month.
Composite Score Formula
Risk Score = (Market Score × 55%) + (External Score × 35%) + (Macro Score × 10%)
All indicators normalised to 0–10 scale using percentile-based capping (5th–95th percentile) to prevent extreme outliers from dominating the score.
Signal Thresholds
ScoreSignalActionMonths Triggered0.0 – 5.0🟢 GreenHold — full positions100 (83%)5.1 – 6.5🟡 AmberReduce equity, increase safe havens15 (13%)6.5 – 10.0🔴 RedDefensive — minimum equity, maximum gold + bonds4 (3%)

Decision Rules — Built From Evidence
Reallocation weights were not set arbitrarily. They were derived by analysing how each asset actually performed during four historical stress events.
Stress Events Analysed
EventPeriod2016 DemonetisationNov 2016 – Mar 20172018 IL&FS CrisisSep 2018 – Mar 20192020 COVID CrashFeb 2020 – Aug 20202022 Rate Hike CycleMar 2022 – Feb 2023
Key Findings From Stress Analysis

Nifty Bank was the worst performer in 3 out of 4 stress events — reduced most aggressively in Red
Nifty IT showed mixed behaviour — badly hurt by rate hikes but fastest recovery in COVID — kept relatively high even in defensive mode
Bonds were the most consistent safe haven across all scenarios — highest allocation in Red
Gold reliable only in COVID — modest increase, not primary safe haven

Portfolio Allocation by Signal
Asset🟢 Green🟡 Amber🔴 RedNifty 5035%30%15%Nifty Bank15%12%3%Nifty IT10%9%7%Gold15%20%33%Bonds20%25%35%USD/INR5%4%7%

Monte Carlo Simulation
100 simulations over 12 forward months based on historical return distributions.
ScenarioStatic PortfolioEWS PortfolioBest Case (95th Pct.)26.22%27.95%Most Likely (50th Pct.)6.44%8.57%Worst Case (5th Pct.)-8.75%-3.48%Mean Outcome7.52%9.82%Std Deviation11.5%10.4%
The EWS cuts worst-case loss by 5.27 percentage points while improving expected return by 2.30 percentage points.

Excel Workbook Structure
SheetContentsIndicators9 raw indicator values — monthly 2014–2024Assets6 asset prices and monthly % returnsNormalisation0–10 scaled indicators with percentile cappingRisk ScoreWeighted composite score + category scores + signalSignal RulesScore threshold reference tablePortfolio AllocationEvidence-based weights by signalStress ReturnsMonthly asset returns during 4 stress eventsScenario TestingEWS score and signal during stress periodsBacktestingEWS vs static portfolio — monthly comparisonMonte Carlo (Actual)100 simulations — static portfolioMonte Carlo (EWS)100 simulations — EWS portfolioSummaryComplete results comparison

Data Sources
SourceDataNSE IndiaNifty 50, Nifty Bank, Nifty IT, India VIX, PE RatioRBI DBIERepo Rate, CPI, 10Y G-Sec Yield, USD/INRMOSPIGDP Growth (quarterly)SEBIFII/FPI Net Flows (monthly)Investing.comBrent Crude, MCX Gold

Limitations

Signal thresholds calibrated on the same dataset used for backtesting — out-of-sample testing would strengthen validity
Linear normalisation assumes stable indicator relationships across the full period
Monthly frequency limits intra-month signal detection
Does not account for transaction costs of rebalancing


Author
Abhinav Saharan
FRM Candidate | B.Com + MA Economics
Risk Analyst Portfolio Project — March 2026

License
MIT License — free to use with attribution.
