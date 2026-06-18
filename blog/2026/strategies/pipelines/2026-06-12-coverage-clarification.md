# Discussion: Market Coverage Clarification

- **Date**: 2026-06-12
- **Participants**: User, Antigravity (Gemini)

## Summary of Discussion

We clarified the market coverage of our proposed data pipelines for European and Polish (GPW) stocks. 

We established that:
1. **European/Polish stocks are supported**: Tools like **EODHD** (paid backtesting), **Stooq.pl** (free prices), **yfinance** (free last 4 years of metrics), and **Koyfin/TradingView** (manual audits) fully cover Polish and European stocks.
2. **US-Only Tools**: The SEC EDGAR API and the free tier of FMP are strictly US-only and will not cover Polish or European stocks.
3. **Polish-Specific Tools**: The eKRS database scrapers (via Apify) are designed exclusively for extracting XML financial reports from the Polish court registry.

## Decisions Made
- Added a visual **Market Coverage Matrix** directly to [gpw_data_sources.md](file:///c:/projects/investing/docs/markets/gpw_data_sources.md) to prevent future ambiguity about which tools can fetch Polish/European data.

## Links to Updated Documents
- [GPW & European Data Sources](file:///c:/projects/investing/docs/markets/gpw_data_sources.md)
- [Active Roadmap](file:///c:/projects/investing/scope/active_goals.md)
