# ORB Breakout Analysis — NQ & ES Futures

Statistical analysis of Opening Range Breakout (ORB) setups on NQ and ES futures. Evaluates whether the first 30 minutes of price action provides a tradeable edge using a two-boundary approach.

## How It Works

For each trading day:
1. **Opening Range (OR)** is defined as the high/low of the first 30 minutes (9:30-10:00 ET)
2. **Entry** is triggered on a breakout above OR high (long) or below OR low (short)
3. **Stop** is placed at the opposite OR boundary
4. **Targets** are evaluated at 0.5R, 1R, 1.5R, 2R, and 3R multiples of risk

The analysis tracks which boundary gets hit first (stop or target) and computes expected value at each R:R level.

## Features

- Per-symbol point-based OR size filters (NQ: 30-500pts, ES: 5-60pts)
- R:R analysis across multiple target levels
- Univariate statistical testing (Mann-Whitney U, Cohen's d, Bonferroni correction)
- ML feature importance (Random Forest, Gradient Boosting, permutation importance)
- Regime analysis (VIX level, day-of-week, OR size quintiles)
- Daily indicator features (ATR, RSI, SMA trend, gap size)

## Data Sources

### yfinance (free, limited)

```bash
python orb_local_pipeline.py
```

Limited to 60 days of 5-minute data. Good for testing but insufficient for statistical significance.

### Schwab API (recommended)

```bash
# Set credentials
set SCHWAB_API_KEY=your_key
set SCHWAB_APP_SECRET=your_secret

# Download up to 2 years of 5-min bars
python schwab_fetch.py

# Run analysis on downloaded data
python orb_local_pipeline.py --csv
```

Requires a [Schwab developer app](https://developer.schwab.com). First run opens a browser for OAuth authentication.

## Install

```bash
pip install numpy pandas yfinance scikit-learn scipy schwab-py
```

## Requirements

- Python 3.10+
- Schwab developer account (for historical data beyond 60 days)
