# Design of Structured Products: JPMorgan Chase & Co

Home assignment for *Fundamentals of Financial Mathematics* (KU Leuven, Prof. Dr. Wim Schoutens).

This project designs two structured products on JPMorgan Chase & Co. (JPM) stock that mature on 15 January 2027:

- **Partially Principal Protected Note (PPPN)**: 90% capital protection plus a premium if JPM leaves the corridor [270, 350].
- **Airbag Note**: full capital protection down to an airbag level of 80% of the spot price, with 69% participation in gains.

Each product is replicated with a zero-coupon bond and European options priced from the market quotes of 12 November 2025. Its expected performance is then estimated with a Monte Carlo simulation of the stock.

## Contents

| Path | Description |
|---|---|
| [`JPM_Structured_Products.pdf`](JPM_Structured_Products.pdf) | Final report |
| [`notebook/structured_products.ipynb`](notebook/structured_products.ipynb) | Companion notebook that reproduces every number and figure in the report |
| `data/jpm_options_2027-01-15.csv` | JPM option chain (calls and puts, maturity 15 Jan 2027), quoted 12 Nov 2025 |
| `data/jpm_prices_2020-11-12_2025-11-12.csv` | Daily JPM close and adjusted close over five years (Yahoo Finance) |
| `data/us_treasury_par_yields_2025-11-12.csv` | U.S. Treasury par yield curve on 12 Nov 2025 (treasury.gov) |
| `report/` | LaTeX source of the report (KU Leuven template); the notebook writes its figures to `report/figures/` |

## Main results

| | PPPN | Airbag Note |
|---|---|---|
| Options | long put K=270, long call K=350 | long call K=S0, short put K=A |
| Issuer margin | 0.5% | 0.5% |
| Expected payoff / investment (Monte Carlo) | 1.198 | 1.234 |

## Reproducing

```bash
pip install -r requirements.txt
cd notebook
jupyter nbconvert --to notebook --execute --inplace structured_products.ipynb
cd ../report
latexmk -pdf main.tex
```
