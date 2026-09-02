# EconLens: UK Economic Time-Series Forecasting

I built EconLens to compare several forecasting methods across eight Bank of England time series. The data covers interest rates, mortgage rates, exchange rates, money supply and consumer credit.

The companion [UK Economic Data Pipeline](https://github.com/jsholoye/uk-economic-data-pipeline) project is about getting the data clean and usable. This project starts from the same extracts and focuses on forecasting them.

![Selected models and holdout results](images/model_comparison.png)

## What the notebook does

- Loads and checks eight Bank of England CSV files.
- Keeps monthly and business-daily series at their own frequencies.
- Holds back the final 12 months or 30 business days for comparison.
- Runs an ADF test on the training data to guide differencing.
- Compares naïve, seasonal-naïve and drift benchmarks with Holt, seasonal ETS and a small SARIMA grid.
- Ranks the candidates by RMSE, followed by MAE and sMAPE.
- Refits the selected model on the full series and produces forecasts and intervals.
- Saves the comparison tables, forecasts and residual checks as CSV files.

## Data

| Code | Indicator | Frequency used | Forecast horizon |
|---|---|---|---|
| LPMAUYN | M4 / monetary aggregate | Monthly | 12 months |
| IUDBEDR | Official Bank Rate | Business daily | 30 business days |
| IUDSOIA | SONIA | Business daily | 30 business days |
| IUMBV34 | 2-year fixed mortgage rate | Monthly | 12 months |
| IUMBV42 | 5-year fixed mortgage rate | Monthly | 12 months |
| LPMVZRI | Consumer credit | Monthly | 12 months |
| XUDLUSS | GBP/USD | Business daily | 30 business days |
| XUDLERS | GBP/EUR | Business daily | 30 business days |

The saved run selected a mix of SARIMA, Holt and seasonal ETS models, so no single method performed best for every series. The Bank Rate result needs context: its holdout error is zero because the rate did not change during that period, not because policy decisions are easy to predict.

## Repository structure

```text
data/raw/    Bank of England CSV inputs
images/      Four selected project visuals
notebooks/   Main forecasting notebook
outputs/     Model comparisons, diagnostics and forecasts
```

## Run in Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jsholoye/econlens-uk-forecasting/blob/main/notebooks/econlens_forecasting.ipynb)

Open the notebook, connect to a runtime and run this once in a temporary cell:

```python
!git clone https://github.com/jsholoye/econlens-uk-forecasting.git
```

You can then use **Runtime → Run all**. The notebook will find the cloned project folder and use the included data files.

## Run locally

```bash
git clone https://github.com/jsholoye/econlens-uk-forecasting.git
cd econlens-uk-forecasting
pip install -r requirements.txt
jupyter lab
```

Open `notebooks/econlens_forecasting.ipynb` and run it from top to bottom.

## Limitations

- The same chronological holdout is used to select a model and report its comparison metrics. A separate test period or rolling-origin evaluation would give a stronger assessment.
- SARIMA intervals come from the fitted model; intervals for the other model families are approximate residual-based bands.
- Some monthly series have fairly short histories.
- The business-day index does not account for every UK market or bank holiday.
- These are statistical forecasts, so they do not account for policy announcements or unexpected economic shocks.
