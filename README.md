# KSE-100 ETF Creation Basket Builder

> 📺 Please watch the YouTube video — you will find it helpful in understanding the code.

I thought to use Python to assist in my work, which I currently do using MS Excel. I believe having Python do it is more reliable, fast and scalable. So, here is the brief description.

## Background

KSE-100 is Pakistan's broad market stock market equity index with 100 names. The purpose of the program is to create an **ETF Creation Unit basket** based on the KSE-100 Index on a given date.

There are three key parameters:

1. The **KSE-100 Index CSV** that has the 100 stocks and their weights in the index etc.
2. The **size of Creation Unit**
3. Any **minimum Cash (as %)** to be kept in the ETF Creation Unit

The index CSV is made from the KSE-100 tab of the *all indices* downloaded file from the following link:

https://dps.psx.com.pk/download/indhist/2025-10-08.xls

> **Note:** This is the date for which the sample CSV is uploaded on the IDE. So, when prompted for the date, you must enter `2025-10-08` to proceed and see the sample work.

The sheet has many tabs for different indices. The **KSE-100 tab** has the index constituents detail of the KSE-100 Index, with the following fields:

| Field | Description |
|---|---|
| `ISIN` | ISIN of the company |
| `SYMBOL` | Symbol of the company |
| `COMPANY` | Name of the company |
| `PRICE` | Share price of the company on the date of the Excel file (in the file name, e.g., `2026-06-10` means 10 June 2026) |
| `IDX WT %` | Weight of the company in the index in % without % sign; total should be 100 |
| `FF BASED SHARES` | Free Float number of shares of the company |
| `FF BASED MCAP` | Free Float Market Capitalization of the company |
| `ORD SHARES` | Total number of ordinary shares of the company |
| `ORD SHARES MCAP` | Total Market Capitalization of the company |
| `VOLUME` | Number of shares of the company traded on that day |

The CSV is named as `20251008_kse100.csv` and is available for processing *(uploaded on IDE as sample)*.

## Program Outputs

The program output is shown on the screen and saved in the following three CSVs as well:

1. `20251008_kse100_basket_300000.csv` — full table of creation basket
2. `20251008_kse100_summary_300000.csv` — headline numbers/summary
3. `20251008_kse100_dropped_300000.csv` — 0-share companies

Where `300000` (in Pak Rupees) is the Creation Unit size; both this and the date are selected by the user, so the output file names would change accordingly.

## Program Logic

Here is the core program logic:

1. Ask for the **date** (to locate the CSV), **basket size** (PKR), and the intended **cash %** of the basket.
2. **Equity target** = basket size × (100 − cash%) / 100
3. **Exact shares in basket** = (IDX WT % / 100) × equity target / PRICE
4. **Basket shares** = exact shares ROUNDED to nearest whole share.
5. Cash must **NEVER** be negative: if rounding pushes cash below zero, trim **ONE** share at a time from the company whose rounding **OVERSHOT** its exact target by the most rupees.
6. Report dropped companies, the summary, and the full table (all companies, sorted by index weight, with basket weight and the difference to 2 decimals).

## Scalability Note

> This program is created for the KSE-100 Index; however, it is scalable to **any equity ETF rebalancing worldwide** by providing:
> - the index data in the prescribed CSV format,
> - the size of the basket in the currency of the exchange (a whole number for a new ETF, or the value of the existing Creation Basket — pre-rebalancing — of an existing ETF), and
> - the minimum cash % that the Fund Manager wants to keep (for trading expenses etc.).

Similarly, an **investor** who wants to create a portfolio to passively mimic an index in its entirety can also use this program by providing the index in CSV format, the investable amount, and the amount of deliberate cash in the portfolio (for trading expenses etc.).

---

*Thank you for reading it all :)*
