# SQLite vs. Parquet for Financial Databases

When setting up a local database for investing backtests, the two most practical choices for retail investors are **SQLite** and **Apache Parquet**. This document compares their features and recommends a hybrid architecture.

---

## 1. Key Differences

| Feature | SQLite | Apache Parquet |
| :--- | :--- | :--- |
| **Type** | Relational Database (SQL) | Columnar Data Files |
| **Primary Use** | transactional storage & SQL queries | Fast analytical scans (Pandas / Polars) |
| **Incremental Updates** | Extremely Easy (`INSERT` or `UPDATE`) | Complex (requires rewriting files or appending) |
| **Query Engine** | Built-in SQL engine | Requires Pandas, DuckDB, or Polars |
| **Storage Structure** | Single `.db` file containing multiple tables | Individual files or directory of partition files |

---

## 2. When to Use SQLite

SQLite is a full-featured, zero-configuration SQL database engine.

*   **Easy Incremental Updates**: If you want to add a single new row for a company's latest quarterly earnings, you simply run an `INSERT` SQL command. 
*   **Complex Relations**: If you want to link different tables (e.g. joining the `CompanyInfo` table with the `BalanceSheet` table on the `Ticker` column), SQLite handles relational joins natively.
*   **Standard SQL Queries**: You can query the database directly in Python using standard SQL statements (e.g., `SELECT * FROM balance_sheet WHERE roic > 0.15`).

---

## 3. When to Use Parquet

Parquet is a read-optimized, columnar file format.

*   **Bulk Loading for Backtests**: In a backtest, you typically load the *entire* historical dataset into memory at once. Reading a Parquet directory directly into a Pandas DataFrame using `pd.read_parquet()` is significantly faster than querying SQLite.
*   **Compression**: Parquet files are highly compressed, making them much smaller on disk than an equivalent SQLite database.

---

## 4. Recomended Hybrid Architecture

To get the best of both worlds, we can combine them:

```
  ┌────────────────────────────────────────────────────────┐
  │ 1. Storage Layer (SQLite: `investing_data.db`)         │
  │    - Stores raw statements in tables.                  │
  │    - Handles easy quarterly inserts and manual updates.│
  └──────────┬─────────────────────────────────────────────┘
             ▼ (Convert/Cache)
  ┌────────────────────────────────────────────────────────┐
  │ 2. Cache Layer (Parquet: `cache/*.parquet`)            │
  │    - Python script exports SQLite tables to Parquet.   │
  │    - Optimizes data for fast analytical reading.       │
  └──────────┬─────────────────────────────────────────────┘
             ▼ (Load)
  ┌────────────────────────────────────────────────────────┐
  │ 3. Execution Layer (Pandas / Backtest Engine)          │
  │    - Loads Parquet files instantly for backtesting.    │
  └────────────────────────────────────────────────────────┘
```

1.  **Write/Update to SQLite**: Keep a single `investing_data.db` file. All scraper outputs and manual edits are inserted directly here using SQL.
2.  **Read/Export to Parquet**: When running a backtest, the Python script reads the SQLite data, converts it to a Pandas DataFrame, and caches it as a Parquet file for subsequent runs, ensuring maximum execution speed.
