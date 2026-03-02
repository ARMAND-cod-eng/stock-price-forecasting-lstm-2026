# **Data**

This project uses **no static dataset files**.
Data is downloaded automatically from Yahoo Finance
via the `yfinance` API every time the notebook runs.
This guarantees fresh, split-adjusted market data
without maintaining outdated CSV files.

---

## Source

| Field | Details |
|-------|---------|
| Provider | Yahoo Finance |
| API | yfinance 0.2.66 |
| Access | Free, no API key required |
| Adjustment | Auto-adjusted for splits and dividends |

---

## Stocks

| Ticker | Company | Sector | Why Included |
|--------|---------|--------|-------------|
| TSLA | Tesla Inc. | Automotive / Energy | Highest volatility — stress test |
| AAPL | Apple Inc. | Technology | Most stable large cap — baseline |
| AMZN | Amazon.com Inc. | E-commerce / Cloud | Different revenue cycle |
| GOOGL | Alphabet Inc. | Technology / Ads | Macro-sensitive revenue |
| MSFT | Microsoft Corp. | Technology / Cloud | Steady grower — AI premium |

---

## Period

| Field | Value |
|-------|-------|
| Start | January 2, 2020 |
| End | December 31, 2024 |
| Trading days | 1,258 per stock |
| Total rows | 6,290 across all stocks |
| Missing values | 0 |

---

## Raw Features

| Column | Description |
|--------|-------------|
| Open | Opening price (adjusted) |
| High | Daily high price (adjusted) |
| Low | Daily low price (adjusted) |
| Close | Closing price (adjusted) |
| Volume | Number of shares traded |

---

## Engineered Features (Block 3)

| Feature | Description |
|---------|-------------|
| MA7_ratio | Close / 7-day moving average |
| MA21_ratio | Close / 21-day moving average |
| RSI | Relative Strength Index (14-day) |
| MACD | 12/26-day EMA difference |
| MACD_signal | 9-day EMA of MACD |
| MACD_hist | MACD − Signal line |
| Volatility_7 | 7-day rolling return std |
| Volatility_21 | 21-day rolling return std |
| Lag_1 to Lag_5 | Lagged daily returns (1–5 days) |
| Volume_ratio | Volume / 21-day average volume |
| Return_raw | Daily percentage return |

---

## Train / Test Split

| Set | Period | Rows | Purpose |
|-----|--------|------|---------|
| Train | 2020-03-13 → 2024-01-12 | 966 | Model training |
| Test | 2024-01-16 → 2024-12-30 | 242 | Honest evaluation |
| Split ratio | 80 / 20 | — | Temporal — no shuffling |

---

## How to Download the Data

The notebook handles everything automatically.
To download manually, run this in Python:
```python
import yfinance as yf

tickers = ['TSLA', 'AAPL', 'AMZN', 'GOOGL', 'MSFT']

for ticker in tickers:
    df = yf.download(
        ticker,
        start       = '2020-01-01',
        end         = '2025-01-01',
        auto_adjust = True
    )
    df.to_csv(f'{ticker}_2020_2025.csv')
    print(f'{ticker}: {len(df)} rows saved')
```

---

## External Links

| Resource | Link |
|----------|------|
| Yahoo Finance | [finance.yahoo.com](https://finance.yahoo.com) |
| yfinance docs | [github.com/ranaroussi/yfinance](https://github.com/ranaroussi/yfinance) |
| TSLA quote | [finance.yahoo.com/quote/TSLA](https://finance.yahoo.com/quote/TSLA) |
| AAPL quote | [finance.yahoo.com/quote/AAPL](https://finance.yahoo.com/quote/AAPL) |
| AMZN quote | [finance.yahoo.com/quote/AMZN](https://finance.yahoo.com/quote/AMZN) |
| GOOGL quote | [finance.yahoo.com/quote/GOOGL](https://finance.yahoo.com/quote/GOOGL) |
| MSFT quote | [finance.yahoo.com/quote/MSFT](https://finance.yahoo.com/quote/MSFT) |

---

*All data is publicly available and free.
No registration or API key required.*
