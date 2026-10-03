# Bank Loan Analysis: SQL, Excel and Power BI

An end-to-end analysis of a bank's loan portfolio. **MySQL** is used for the KPI queries, **Excel** for validating the results, and **Power BI** (with DAX) for interactive dashboards.


---

## Problem Statement

A bank wants to monitor its loan portfolio: how many loans are applied for, how much is funded and recovered, what interest rates apply, and which loans perform well or badly.

## Dataset

`1. Data/financial_loan.csv` has **38,576 loan records** with 24 columns, including loan amount, interest rate, DTI, loan status, purpose, term, state, employment length and home ownership. Column details are in `0.2 Data Dictionary.xlsx`.

## Key Terms

| Term | Meaning |
|---|---|
| Funded amount | Money the bank lent |
| Amount received | Money repaid by borrowers so far |
| DTI | Debt-to-income ratio: share of income already going to debt payments |
| Good loan | Loan status *Fully Paid* or *Current* |
| Bad loan | Loan status *Charged Off* |
| MTD / MoM | Month-to-date / month-over-month change |

## Tech Stack

MySQL | Excel | Power BI | DAX

## Project Structure

```
1. Data/                          Raw dataset (CSV)
2. SQL_Scripts/                   Preprocessing and KPI queries for each dashboard
3. SQL_query_results/             Query outputs (CSV) used to validate Power BI
4. PowerBI_Dashboard/             .pbix file and PDF export
5. Testing_and_validation_report/ MySQL-to-Power BI connection guide, validation report
Project Images and video/         Dashboard screenshots
0.x documents                     Loan process guide, data dictionary, measures list
```

## Workflow

1. Load `financial_loan.csv` into MySQL and run `2.0 Data Preprocessing.sql` to convert text dates to `DATE`.
2. Run `2.1 Dashboard_1_Summary.sql` and `2.2 Dashboard_2_Overview.sql` to generate the KPI results.
3. Validate the Power BI numbers against the query results.
4. Open `4.1 Bank Loan Reports.pbix` in Power BI Desktop.

## KPIs

- Total loan applications, funded amount and amount received (with MTD and MoM change)
- Average interest rate and average DTI
- Good vs. bad loans: applications, percentage, funded amount, amount received

## Dashboards

| Summary | Overview | Details |
|---|---|---|
| ![Summary](Project%20Images%20and%20video/Dashboard_1_SUMMARY.png) | ![Overview](Project%20Images%20and%20video/Dashboard_2_OVERVIEW.png) | ![Details](Project%20Images%20and%20video/Dashboard_3_DETAILS.png) |

- **Summary:** headline KPIs with MTD and MoM, good vs. bad loan comparison, loan status grid
- **Overview:** monthly trend, state-wise map, loan term, employment length, loan purpose, home ownership
- **Details:** full loan-level grid

## SQL Concepts Used

- Aggregations with `GROUP BY`
- CTEs for monthly summaries
- Window function `LAG()` for month-over-month change
- Date handling with `STR_TO_DATE` and `EXTRACT`
- Subqueries to find the latest month for MTD figures

## Key Findings

Calculated from `financial_loan.csv` (loans issued in 2021):

- **38,576** loan applications, with **$435.8M** funded and **$473.1M** received.
- Average interest rate is **12.05%** and average DTI is **13.33%**.
- **86.2%** of loans are good (Fully Paid or Current) and **13.8%** are bad (Charged Off).
- Bad loans were funded **$65.5M** but have returned only **$37.3M** so far, about 57% of the amount lent.
- **Debt consolidation** is the most common loan purpose (18,214 applications).
- Most loans are **36-month** (28,237) rather than 60-month (10,339).
- **California** has the most applications (6,894), followed by New York and Florida.
- Charge-off rates are highest for **small business** loans (about 25.6%).

## Limitations

- Public dataset in a US-style loan format, not data from an Indian bank
- Descriptive analysis only, with no prediction model
- A fixed snapshot, not updated in real time

## License

MIT License. 