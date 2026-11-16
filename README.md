# 🏦 Retail Bank Transaction Analysis — Power BI Capstone Project

## 📌 Project Overview
This project transforms 8 siloed retail banking CSV datasets into a unified, 6-page interactive Power BI report. Designed from the perspective of a Business Intelligence Analyst, the solution gives bank leadership end-to-end visibility into customer demographics, branch deposits, transaction channels, loan repayment risks, and card adoption.

---

## 📂 Dataset Architecture (8 Tables)
| File Name | Role | Records | Description |
| :--- | :--- | :--- | :--- |
| **`customers.csv`** | Dimension | 500 | Demographics, segments, income, credit score, KYC status |
| **`accounts.csv`** | Dimension / Bridge | 700 | Account types, balances ($10.20M total), interest rates, overdrafts |
| **`branches.csv`** | Dimension | 40 | Branch locations, regions, and historical opening dates |
| **`cards.csv`** | Fact / Dimension | 600 | Debit & Credit card usage across card networks |
| **`loans.csv`** | Dimension / Bridge | 300 | Loan types, principal amounts ($53.44M total), status, maturity dates |
| **`loan_payments.csv`** | Fact | 2,000 | EMI repayment history and late payment delay days |
| **`transactions.csv`** | Fact | 5,000 | Channel activity (Online, Branch, Mobile, ATM, POS, Wire) & status |
| **`date_table.csv`** | Dimension | 2010–2028 | Master calendar table for time-intelligence filtering |

---

## 🛠️ Data Preparation & Modeling
1. **ETL in Power Query:**
   - Applied `Trim`, `Clean`, and proper capitalization to eliminate duplicate categories across card networks and transaction channels.
   - Replaced blank customer segments with `"Unspecified"` instead of dropping rows, preserving referential integrity across linked accounts and loans.
   - Enforced proper data types (`Text` for IDs, `Decimal` for currency, `Whole Number` for counts).
2. **Data Modeling:**
   - Built clean **one-to-many, single-direction** relationships to prevent double-counting and ambiguous filter paths.
   - Left historical branch opening dates (`1986`) and future loan maturity dates (`2053`) unlinked from the `2010–2028` Date Table so edge-case records remain intact without generating blank date buckets.
   - Verified row counts and retained all `301` cardless accounts against source CSVs.
3. **DAX Measures & Calculated Columns:**
   - Created dynamic KPI measures directly inside their respective tables using `CALCULATE` and zero-safe `DIVIDE()`.
   - Added calculated columns for **Customer Age**, **Customer Tenure**, and **Weekday Name**.

---

## 📊 Dashboard Pages & Key Insights
1. **Customer Segmentation Analysis:** 75% active customer rate (375/500), led by Student and Business segments; **71.4%** of customers still have incomplete KYC.
2. **Account Usage & Branch Activity:** $10.20M in total deposits across 700 accounts (71% active), with IRA and Certificate of Deposit accounts holding the highest balances.
3. **Transaction Patterns Analysis:** $10.98M in completed transaction value, led by Online and Branch channels—but a **32.56% transaction failure rate** signals technical friction.
4. **Loan Performance & Repayment Analysis:** **48.40% delinquency rate** (86 Defaulted, 83 In Arrears) across a $53.44M portfolio; Personal loans average 6+ days late.
5. **Card Usage & Product Engagement:** 60% Debit vs. 40% Credit split across 600 cards, leaving **43% of accounts (301/700)** without a card.
6. **Executive Summary:** High-level leadership view consolidating all 6 core KPIs with dynamic year slicing.

---

## 🚀 Business Recommendations
- **Reduce Transaction Failures:** Audit payment gateways and online channels to resolve the 32.56% failure rate.
- **Mitigate Loan Delinquency:** Implement automated EMI auto-debit mandates and stricter credit checks for Education and Business loans.
- **Drive KYC & Card Adoption:** Run targeted outreach campaigns to verify the 357 pending KYC customers and cross-sell debit/credit cards to the 301 cardless accounts.

---

## 📎 Repository Contents
- **`Retail Bank Transaction Analysis.pbix`** — Interactive Power BI Desktop report
- **`6 Dashboards-combined.pdf`** — Exported PDF of all 6 Power BI report pages
- **`Retail Bank Transaction Analysis.pdf`** — Full project presentation deck
- **`*.csv` (8 files)** — Raw banking source datasets
