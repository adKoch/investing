# Discussion: Hard-to-Find Data Sources for GPW & Europe

- **Date**: 2026-06-12
- **Participants**: User, Antigravity (Gemini)

## Summary of Discussion

We researched the "hard-to-find" sources of financial and fundamental data for the Warsaw Stock Exchange (GPW) and Europe to enable robust backtesting.

We mapped out three viable approaches:
1. **Free / Scraping (DIY)**:
   - **Stooq.pl URL Loophole**: Downloads full historical price CSVs for free using plain HTTP requests (e.g. `https://stooq.pl/q/d/l/?s=dnp&i=d`).
   - **GPW Indicators Scraping**: Parsing `https://www.gpw.pl/wskazniki_spolek_full` for current fundamental metrics.
   - **eKRS/RDF Scraping (via Apify)**: Bypasses government anti-bot firewalls to extract official XML/PDF corporate financial statements.
2. **Affordable International APIs**:
   - **EOD Historical Data (EODHD)**: One of the few low-cost APIs (€20-30/mo) providing 10+ years of historical fundamental statements for GPW companies (ticker suffix `.WAR`).
3. **Local Polish Commercial APIs**:
   - **MGBI** and **Transparent Data**: High-quality, paid services offering structured JSON balance sheets directly from the Polish registry.

## Decisions Made
- Created [gpw_data_sources.md](file:///c:/projects/investing/docs/markets/gpw_data_sources.md) to document these data pipelines.
- Agreed to use Stooq.pl for free price data, and evaluate EODHD or a custom eKRS scraper if we proceed with automated GPW fundamental backtesting.

## Links to Updated Documents
- [GPW & European Data Sources](file:///c:/projects/investing/docs/markets/gpw_data_sources.md)
- [Active Roadmap](file:///c:/projects/investing/scope/active_goals.md)
