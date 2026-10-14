# Stock Price Forecasting: Model Comparison Across Volatility Conditions

**Machine Learning Final Project · Fall 2026 · Wright State University**  
**Current stage:** Initial dataset review and project planning. Model implementation has not yet begun.

## What are we investigating?

Our goal is to **predict the next trading day's closing price** and compare whether different forecasting approaches perform consistently across assets with different historical volatility. We want to understand when more complex models help, when simpler models are competitive, and whether improved accuracy justifies additional complexity.

Volatility is **a characteristic we will analyze**, not the primary value we are trying to predict.

## Our initial datasets

| Asset | Ticker | Annualized historical volatility* |
| --- | --- | ---: |
| SPDR S&P 500 ETF Trust (S&P 500-tracking ETF) | `SPY` | 18.01% |
| Amazon | `AMZN` | 33.17% |
| Tesla | `TSLA` | 59.59% |

We selected these instruments because they show relatively lower, moderate, and higher volatility **within our initial sample**. This does not mean that higher-volatility stocks are necessarily harder to predict or automatically require more complex models—that is part of what we want to investigate.

The first historical quote exports, obtained from Nasdaq, contain **2,512 daily observations per asset**, covering **October 13, 2016–October 12, 2026**. Fields are `Date`, `Close/Last`, `Volume`, `Open`, `High`, and `Low`.

Our preliminary review involved converting text-formatted prices to numbers, sorting trading dates chronologically, and checking for missing/duplicate records. We found **no duplicate dates** and **one missing SPY Volume entry (April 20, 2026)**. That trading date was excluded from all three preliminary cleaned files, leaving **2,511 rows per asset**.

*Volatility was estimated from the original closing-price series using daily simple percentage returns. We calculated the sample standard deviation of daily returns and multiplied by √252 to annualize it. Historical price-adjustment conventions still need verification.*

**Data access note:** The original downloads came from [Nasdaq](https://www.nasdaq.com). We have not established permission to redistribute these files or use them for ML model development, so **the CSVs are not being published in this public repository**. We will resolve the data permissions or use an appropriately licensed source before training; any changes to the data will be documented.

## Planned models and team responsibilities

| Team member | Starting dataset | Model |
| --- | --- | --- |
| Sanathan | SPY | **ARIMA** — statistical time-series model |
| Vivek | AMZN | **LSTM** — recurrent neural network |
| Sampan | TSLA | **GRU** — recurrent neural network |

Each member will first develop their assigned model. Then **each model will be trained and evaluated separately on all three assets** for a fair comparison. The initial assignments do not imply that one model is best for a particular stock.

We **may** explore an **ARIMA–LSTM hybrid** that uses a neural network to correct statistical forecasting errors. A **volatility-aware hybrid adjustment** is another possible extension. Both depend on time, implementation difficulty, early results, and professor feedback; neither is a required deliverable at this stage.

## How we plan to evaluate the models

- **Target:** Next-day closing price, with daily returns used only for secondary analysis.
- **Proposed chronological split:** 70% training, 10% validation, 20% final test; no shuffling.
- **Metrics:** MAE and RMSE, alongside a **previous-day-close baseline**.
- **Additional questions:** How do errors change with volatility, and does model complexity provide a meaningful benefit?

To avoid data leakage, the final test period will remain untouched during model selection, and learned preprocessing parameters will be fitted using training data only.

## Project progress

- [x] Define the initial forecasting question and select three contrasting assets.
- [x] Perform preliminary data cleaning and calculate volatility estimates.
- [ ] Resolve data permissions, verify price adjustments, and finalize the data source.
- [ ] Agree on common splits and evaluation procedures.
- [ ] Implement and compare ARIMA, LSTM, and GRU across all three assets.
- [ ] Analyze results; explore hybrid extensions if feasible.
- [ ] Document findings and finalize the report.

## Repository structure (to be built as needed)

```text
├── README.md       # Overview and progress (this file)
├── data/           # Data source/access notes; licensed data only
├── notebooks/      # EDA and individual model experiments
├── src/            # Reusable scripts and model implementations
├── experiments/    # Experiment settings and results
├── results/        # Figures and comparison tables
└── docs/           # Detailed methods and decisions, when needed
```

This README will evolve as the project progresses. **Proposed methods are not completed results**, and our scope may change with research findings or faculty feedback.

*Educational research project; not financial or investment advice.*
