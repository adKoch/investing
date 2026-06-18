# Parquet vs. CSV: Financial Data Formats

When building a backtester or database for investing strategies, choosing the right file format for storing historical statements is critical for speed and storage efficiency. This document compares **CSV (Comma-Separated Values)** and **Apache Parquet**.

---

## 1. Key Differences at a Glance

| Feature | CSV | Apache Parquet |
| :--- | :--- | :--- |
| **Storage Paradigm** | Row-oriented | Column-oriented |
| **Format** | Plain Text (Human-readable) | Compressed Binary (Machine-readable) |
| **Data Schema** | None (Pandas must infer types) | Preserved (Data types saved in metadata) |
| **File Size** | Larger (No default compression) | Smaller (Run-length/dictionary encoding) |
| **Read Speed** | Slower (Full file parsing required) | Extremely Fast (Selective column loading) |

---

## 2. Why Columnar Storage (Parquet) Matters for Backtesting

In financial analysis, we often want to perform operations on a single metric across thousands of companies over many years (e.g., calculating the average `ROCE` column).

```
   Row-Oriented (CSV):
   [Company A, 2020, ROCE: 20%, Debt: 1x] -> [Company A, 2021, ROCE: 22%, Debt: 0.8x] -> ...
   (To get just ROCE, the computer must scan every single character in the file)

   Column-Oriented (Parquet):
   [Company A, Company B, Company C...]
   [2020, 2021, 2022...]
   [ROCE: 20%, ROCE: 22%, ROCE: 25%...]  <-- Read only this block from disk
```

*   **Selective Loading**: Parquet allows Pandas to read *only* the specific columns needed (e.g., loading only the `ROCE` and `Ticker` columns and ignoring 50 other balance sheet items). In a CSV, you must read the entire file line-by-line, wasting CPU and RAM.
*   **No Parsing Overhead**: In a CSV, everything is text. The computer must parse the string `"2026-06-12"` into a date object, and the string `"15.2"` into a float. Parquet stores these as native binary data types, eliminating parsing overhead and data-type errors.

---

## 3. Storage Efficiency (Compression)

Parquet groups identical or sequential data together within columns, allowing for highly efficient compression algorithms (like Snappy or Gzip):
*   **Dictionary Encoding**: Replaces repetitive text (e.g., the country name `"Poland"`) with a small integer key.
*   **Run-Length Encoding**: Compresses repeating sequences (e.g., the year `2020` repeating 1,000 times) into a simple descriptor: `[1000 times: 2020]`.
*   **Result**: Parquet files are typically **80% to 90% smaller** than the equivalent CSV.
