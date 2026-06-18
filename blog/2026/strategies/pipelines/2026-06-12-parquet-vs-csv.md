# Discussion: Parquet vs. CSV & SQLite Database Architecture

- **Date**: 2026-06-12
- **Participants**: User, Antigravity (Gemini)

## Summary of Discussion

We discussed the technical differences between data storage formats for our fundamental backtesting database.

We contrasted **CSV** and **Parquet**:
1. **Row vs. Column Layout**: CSV is row-oriented (slow to search columns); Parquet is column-oriented (lightning-fast to query specific metrics like ROCE).
2. **Text vs. Binary**: CSV is plain text (no schema, large size); Parquet is compressed binary (preserves data types, 80-90% smaller).
3. **Database Architecture**: We compared **SQLite** (easy SQL queries and incremental updates) with **Parquet** (fastest bulk loading for backtests).

## Decisions Made
- Created [parquet_vs_csv.md](file:///c:/projects/investing/docs/data/parquet_vs_csv.md) and [sqlite_vs_parquet.md](file:///c:/projects/investing/docs/data/sqlite_vs_parquet.md).
- Selected a **Hybrid Database Architecture**: We will store our harvested data in a local **SQLite** database for easy updates, and convert it to **Parquet** cache files for high-speed backtest simulations in Python.

## Links to Updated Documents
- [Parquet vs. CSV Guide](file:///c:/projects/investing/docs/data/parquet_vs_csv.md)
- [SQLite vs. Parquet Guide](file:///c:/projects/investing/docs/data/sqlite_vs_parquet.md)
- [Active Roadmap](file:///c:/projects/investing/scope/active_goals.md)
