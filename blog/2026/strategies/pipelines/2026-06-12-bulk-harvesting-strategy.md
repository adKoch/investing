# Discussion: One-Month Bulk Harvesting & Database Strategy

- **Date**: 2026-06-12
- **Participants**: User, Antigravity (Gemini)

## Summary of Discussion

We discussed a highly practical cost-optimization strategy for obtaining historical fundamental data: **the One-Month Bulk Harvesting Strategy**.

Rather than paying for expensive monthly recurring API subscriptions, we will:
1. **Harvest (Month 1)**: Subscribe to a comprehensive data API (like EODHD) for a single month, bulk-download all 10-20 year historical statement data for GPW and European companies, and store it locally inside a **SQLite database** or compressed **Parquet files**.
2. **Free Updates (Ongoing)**: Cancel the subscription, and update our database for free by scraping the latest quarterly earnings reports from GPW/eKRS or manually updating our final concentrated watchlists once a quarter.

## Decisions Made
- Updated [gpw_data_sources.md](file:///c:/projects/investing/docs/markets/gpw_data_sources.md) to detail this harvesting pipeline.
- Agreed to build our local backtesting database using this model, which minimizes recurring operational costs to near zero.

## Links to Updated Documents
- [GPW & European Data Sources](file:///c:/projects/investing/docs/markets/gpw_data_sources.md)
- [Active Roadmap](file:///c:/projects/investing/scope/active_goals.md)
