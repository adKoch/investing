# Data Sources for GPW & European Stocks

Finding clean, historical financial data for the Warsaw Stock Exchange (GPW) and European mid/small-caps is a challenge. Large global databases either ignore them or charge institutional rates. This document details the "hard-to-find" free and low-cost data sources available for retail algorithmic trading and screening.

---

## Market Coverage Matrix

To clarify which tools cover Polish and European stocks, here is a breakdown of our data options:

| Service / Tool | US Stock Coverage | European Stock Coverage | Polish Stock (GPW) Coverage | Cost | Primary Use |
| :--- | :---: | :---: | :---: | :--- | :--- |
| **EODHD API** | ✅ Yes | ✅ Yes | ✅ Yes (`.WAR`) | Paid (~€20/mo) | Historical Backtest |
| **Stooq.pl** | ✅ Yes | ✅ Yes | ✅ Yes | Free | Price Backtest |
| **yfinance (Yahoo)**| ✅ Yes | ✅ Yes | ✅ Yes (`.WA`) | Free | Latest 4-Yr updates |
| **Apify eKRS Scraper**| ❌ No | ❌ No | ✅ Yes (XML) | Free Tier | Polish filing harvest|
| **SEC EDGAR API** | ✅ Yes | ❌ No | ❌ No | Free | US filing harvest |
| **FMP API (Free)** | ✅ Yes | ❌ No (spotty) | ❌ No | Free | US updates |
| **Koyfin / TradingView**| ✅ Yes | ✅ Yes | ✅ Yes | Free | Manual validation |

---

## 1. Free Price & Fundamental Data Sources

### A. Stooq.pl (Historical Price CSVs)
For historical stock prices, Stooq is a legendary tool in the Polish quant community. It allows free downloading of full historical price data via simple URL parameters.
*   **API URL Pattern**: `https://stooq.pl/q/d/l/?s=[ticker]&i=d`
*   **Example**: `https://stooq.pl/q/d/l/?s=dnp&i=d` downloads the entire historical price CSV for Dino Polska (`DNP`) from its IPO to today.
*   **Usage**: Extremely easy to integrate into a Python Pandas script.

### B. GPW Indicators Table Scraping
The Warsaw Stock Exchange publishes current market indicators (P/E, P/BV, Dividend Yield, etc.) for all listed stocks in a single public table.
*   **URL**: `https://www.gpw.pl/wskazniki_spolek_full`
*   **Scraping Method**: Python `requests` + `BeautifulSoup` or `pandas.read_html()`. This is ideal for generating a quick snapshot of the Polish market.

---

## 2. Unconventional / Scraping Solutions for Fundamentals

### A. eKRS / Repozytorium Dokumentów Finansowych (RDF)
All Polish companies are legally required to submit their structured XML/PDF financial statements to the government's eKRS repository.
*   **The Challenge**: The government site is protected by anti-bot web application firewalls (WAF like Incapsula/Imperva) and Captchas, blocking standard Python `requests`.
*   **The Loophole (Apify Platform)**: The Apify developer marketplace has pre-built KRS scrapers (e.g., *Poland KRS Financial Statements Scraper*). These automated bots bypass the WAF, extract the raw XML/PDF filings, and return them as structured JSON files via an API.

---

## 3. Commercial & Low-Cost APIs

For clean, backtestable data without the engineering overhead of scraping, these services offer the best cost-to-quality ratio:

### A. EOD Historical Data (EODHD)
One of the few global retail APIs that offers full historical financial statements (Income Statement, Balance Sheet, Cash Flow) for the Warsaw Stock Exchange.
*   **Ticker Suffix**: `.WAR` (e.g., `DNP.WAR` for Dino Polska).
*   **History**: Up to 10+ years of annual and quarterly statement history.
*   **Cost**: Approx. €20-€30/month (significantly cheaper than Bloomberg or Reuters).

### B. Local Data Aggregators
If you need highly accurate, audited Polish corporate data for commercial purposes, local APIs exist but require direct licensing:
*   **MGBI RDF API**: Specifically built to parse and distribute the official XML/PDF files from the Krajowy Rejestr Sądowy.
*   **Transparent Data**: Provides integrated APIs returning clean JSON balances and profit/loss statements by KRS/NIP numbers.

---

## 4. The One-Month "Bulk Harvesting" Strategy (Cost Optimization)

To build a backtester, we need 10-20 years of historical data. However, historical data is **static** (the balance sheet of a company in 2015 does not change). Therefore, we do not need a recurring subscription. We can execute a cost-effective harvest:

### Phase 1: The Harvest (Month 1)
1. **Subscribe**: Sign up for a 1-month plan with a high-coverage fundamental API (e.g., EODHD or FMP).
2. **Bulk Download**: Run a Python script to iterate through our target universe (GPW and European tickers) and download their entire historical financial statement history.
3. **Local Database**: Save the downloaded JSON/CSV files into a local **SQLite database** (`investing_data.db`) or compressed **Parquet files** on your drive.
4. **Cancel**: Cancel the subscription before the renewal date, keeping our total cost under €30.

### Phase 2: Free Incremental Updates (Ongoing)
Since we only rebalance quarterly or annually, we only need to update the database with the *latest* quarterly/annual reports. We can do this for free using the following services:

#### 1. Yahoo Finance (`yfinance` Python Library)
*   **Cost**: Free.
*   **Coverage**: Global (US, Europe, GPW with `.WA` suffix).
*   **Limits**: As an unofficial scrapper, it has no official rate limits but Yahoo blocks rapid IP requests (returns `429 Too Many Requests` errors).
*   **Best Practice**: Implement a `time.sleep(2)` delay between ticker requests, fetch data in small batches, and run it only once a month or quarter.

#### 2. SEC EDGAR API (US Stocks Only)
*   **Cost**: Free (Official SEC Database).
*   **Coverage**: All US-listed companies.
*   **Best Practice**: Use the official SEC REST API. It allows up to 10 requests per second (must declare user-agent header in Python) and is 100% reliable for getting the latest 10-K and 10-Q statements.

#### 3. Free Tiers of Commercial APIs (US & Global)
*   **Alpha Vantage**: Free tier allows **25 API calls per day** (sufficient for updating a concentrated 20-stock watchlist slowly).
*   **Financial Modeling Prep (FMP)**: Free tier allows **250 requests per day** (covers US stocks only).

#### 4. Manual Verification / Screeners (Koyfin / TradingView)
*   **Cost**: Free.
*   **Coverage**: Global.
*   **Best Practice**: For a highly concentrated portfolio (e.g. 10-20 compounders), manually checking the new numbers on Koyfin or TradingView once a quarter takes less than 15 minutes. It is 100% reliable, requires 0 maintenance, and ensures you actively review the financials of the companies you own.
