# Core Thinking Framework & Automation Plan

To build a sustainable investing strategy, we must establish a rigorous, objective thinking framework. This framework validates our assumptions and defines a highly automated, low-maintenance operational workflow.

---

## 1. Core Assumption Validation Checklist

Before adopting any strategy or analyzing a company, we must run it through this validation filter to verify our assumptions:

```
                  ┌─────────────────────────────────┐
                  │      INVESTMENT CANDIDATE       │
                  └────────────────┬────────────────┘
                                   │
                     Is it within our Circle?
                    ┌──────────────┴──────────────┐
                    ▼ Yes                         ▼ No
     ┌─────────────────────────────┐       ┌──────────────┐
     │  Is ROCE > 15% (10-Yr Avg)?  │       │  "Too Hard"  │
     └──────────────┬──────────────┘       └──────────────┘
                    ▼ Yes
     ┌─────────────────────────────┐
     │  Is Moat durable/expanding? │
     └──────────────┬──────────────┘
                    ▼ Yes
     ┌─────────────────────────────┐
     │ Is Net Debt / EBITDA < 2.5x?│
     └──────────────┬──────────────┘
                    ▼ Yes
     ┌─────────────────────────────┐
     │  Is Valuation Fair (Yield)? │
     └──────────────┬──────────────┘
                    ▼ Yes
            [ BUY & HOLD ]
```

1. **Circle of Competence**: Do we actually understand how this company makes money, who its customers are, and what could kill it? If not, it goes to the *"Too Hard"* pile.
2. **Quality (ROCE)**: Is the high return on capital driven by high margins and asset turnover, or is it artificially inflated by debt? (Assumption: Operational strength > financial leverage).
3. **Moat Durability**: Can competitors copy this business model within 5 years? If yes, it does not qualify as a long-term compounder.
4. **Capital Allocation**: Does management reinvest cash or waste it on bad acquisitions? (Assumption: High reinvestment runway is superior to high dividend payouts).
5. **Valuation (FCF Yield)**: Are we buying at a price that yields an acceptable return even if the business growth slows down?

---

## 2. The Low-Maintenance Workflow ("Do Nothing")

Consistent with Terry Smith's "Do nothing" mantra, this strategy is designed to require very little manual intervention.

*   **Infrequent Reviews (Quarterly)**: We only review financial performance when quarterly earnings reports (10-Q/10-K) are published.
*   **Low Portfolio Turnover**: We aim to hold companies for 3 to 10+ years. We only sell if:
    1. The core investment thesis is broken (e.g., the moat is eroding).
    2. The business becomes absurdly overvalued (FCF yield drops to near 0%).
    3. We find a far superior business at a better price.
*   **Automated Screens**: Instead of manual searching, we automate the discovery phase to run in the background.

---

## 3. Automation Architecture

To minimize manual effort, we will design a simple three-tier automation pipeline:

```
  ┌──────────────────────┐
  │ 1. DATA GATHERING    │  --> Queries financial APIs (e.g., Financial Modeling Prep,
  └──────────┬───────────┘      Yahoo Finance, or SEC EDGAR) in Python.
             ▼
  ┌──────────────────────┐
  │ 2. FILTERING ENGINE  │  --> Screens stocks based on our ROCE, Margin, Debt, and
  └──────────┬───────────┘      Market Cap filters automatically.
             ▼
  ┌──────────────────────┐
  │ 3. ALERTS & REPORTS  │  --> Updates a central spreadsheet or sends a notification
  └──────────────────────┘      only when a candidate enters our valuation "Buy Zone".
```

*   **Trigger Interval**: The script runs once a week or once a quarter after earnings season.
*   **Action Required**: The investor only acts when the system flags a candidate that passes both the quantitative screener and enters the target valuation range.
