# Bank Loan Analysis | Power BI Dashboard

## Objective

Build a Power BI report that helps a bank monitor its lending portfolio: how many loans were issued, how much was funded and collected, and how good loans compare with bad loans. The report follows a client brief with three dashboards: **Summary**, **Overview** and **Details**.

## Dataset

- File: `Data/financial_loan.csv`
- 38,576 loan applications issued during 2021
- Main fields: loan status, loan amount, total payment, interest rate, DTI, term, grade, purpose, home ownership, employment length, state, issue date

**Good vs Bad Loan:** a loan is *Good* if its status is Fully Paid or Current, and *Bad* if it is Charged Off.

## Tools Used

- Power BI Desktop (data model, DAX, visuals)
- DAX (KPIs, MTD, previous month, MoM, good vs bad loan)
- Python / pandas, used only to double-check the numbers

## Dashboard Pages

| Page | What it shows |
|---|---|
| Summary | 5 KPI cards with MTD and MoM, Good vs Bad Loan KPIs, Loan Status grid |
| Overview | Monthly trend, map by state, term donut, employment length, purpose, home ownership. A *Select Measure* slicer switches the charts between Applications, Funded Amount and Amount Received |
| Details | Full loan-level table |

Screenshots are in the `Screenshots` folder.

## Key Performance Indicators

| KPI | Value | MTD (Dec) | MoM |
|---|---|---|---|
| Total Loan Applications | 38.6K | 4.3K | +6.9% |
| Total Funded Amount | $435.8M | $54.0M | +13.0% |
| Total Amount Received | $473.1M | $58.1M | +15.8% |
| Average Interest Rate | 12.0% | 12.4% | +3.5% |
| Average DTI | 13.3% | 13.7% | +2.7% |

| | Applications | Funded Amount | Received Amount | Share |
|---|---|---|---|---|
| Good Loan | 33.2K | $370.2M | $435.8M | 86.2% |
| Bad Loan | 5.3K | $65.5M | $37.3M | 13.8% |

All measures are documented in [DAX_Measures.md](DAX_Measures.md).

## Key Insights

1. **Lending grew steadily through the year.** Monthly applications rose from about 2.3K in January to 4.3K in December (+85%), and funded amount from $25.0M to $54.0M (+116%).
2. **Lending is concentrated.** California alone has 6,894 applications, and the top five states (CA, NY, FL, TX, NJ) make up about 46% of all applications.
3. **Debt consolidation dominates.** It is the stated purpose of 47% of applications, far ahead of credit card (13%).
4. **Most loans are 36-month loans** (73%), but 60-month loans are riskier: 22.3% of them were charged off, against 10.7% for 36-month loans.
5. **Risk rises sharply as grade drops.** The charged-off rate goes from 5.7% for grade A to about 31% for grades F and G, while the average interest rate rises from 7.4% to 21.4%.
6. **Small-business loans are the riskiest purpose** in the data, with a 25.6% charged-off rate.
7. **Borrowers are mostly renters or mortgage holders** (48% and 45%), and the largest employment group is 10+ years (23%).
8. **Interest rate, DTI and MoM:** the average interest rate rose 3.5% month over month in December, and average DTI rose 2.7%.

## Data Limitations

- The data covers one year only (2021), so seasonality cannot be confirmed.
- "Current" loans are counted as Good Loans, even though they have not finished repaying. This may understate the real bad-loan share.
- Month-over-month logic uses the month number, so it assumes a single calendar year.
- The dataset has no information on recoveries after charge-off, so profitability is not analysed.

## Repository Structure

```
Bank-Loan-Analysis/
├── README.md
├── DAX_Measures.md
├── Bank_Loan_Analysis.pbix
├── Data/
│   └── financial_loan.csv
├── Screenshots/
└── Docs/
    └── Problem_Statement_Bank_loan_analysis.pdf
```
