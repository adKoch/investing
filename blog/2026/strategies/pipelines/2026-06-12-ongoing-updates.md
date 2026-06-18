# Discussion: Ongoing Data Updates & Free Services

- **Date**: 2026-06-12
- **Participants**: User, Antigravity (Gemini)

## Summary of Discussion

We discussed how to keep our local database updated with the latest quarterly and annual earnings reports *after* completing our initial one-month bulk download.

We identified four primary free/cheap methods to achieve this:
1. **Yahoo Finance (`yfinance`)**: Free, global coverage (including GPW), but requires throttled requests (delays of 2-5 seconds) to avoid Yahoo's anti-scraping blocks.
2. **SEC EDGAR REST API**: Free, official, highly reliable for US stocks, allows 10 requests per second.
3. **Free Tiers of Commercial APIs**: Alpha Vantage (25 requests/day, global) and Financial Modeling Prep (250 requests/day, US only).
4. **Manual Watchlist Audits (Recommended)**: For a concentrated portfolio of 20-30 stocks, manually updating the database using free screeners like Koyfin or TradingView once a quarter takes 15 minutes, eliminates code maintenance, and ensures direct investor oversight.

## Decisions Made
- Updated [gpw_data_sources.md](file:///c:/projects/investing/docs/markets/gpw_data_sources.md) to document these ongoing update options.
- Agreed to use a throttled `yfinance` script for automated monitoring, backed by manual audits for our core holdings.

## Links to Updated Documents
- [GPW & European Data Sources](file:///c:/projects/investing/docs/markets/gpw_data_sources.md)
- [Active Roadmap](file:///c:/projects/investing/scope/active_goals.md)
