# DAX Measures

All measures live in the `_Measures` table of `Bank_Loan_Analysis.pbix`.
The data table is `financial_loan`; dates come from `Calendar_Table`.

## Calendar table

```dax
Calendar_Table =
ADDCOLUMNS(
    CALENDARAUTO(),
    "Year", YEAR([Date]),
    "Month", MONTH([Date]),
    "MONTH Name", FORMAT([Date], "MMM"),
    "Day Name", FORMAT([Date], "dddd")
)
```

`MONTH Name` is sorted by `Month` (Column tools > Sort by column) so months appear Jan to Dec.
The calendar is related to `financial_loan[issue_date]` (one-to-many).

## Calculated column

```dax
Good & Bad Loan =
IF(
    financial_loan[loan_status] = "Fully Paid" || financial_loan[loan_status] = "Current",
    "Good Loan",
    "Bad Loan"
)
```

Good Loan = Fully Paid or Current. Bad Loan = Charged Off.

## Core KPIs

```dax
Total Loan Applications = DISTINCTCOUNT(financial_loan[id])
```

```dax
Total Funded Amount = SUM(financial_loan[loan_amount])
```

```dax
Total Amount Received = SUM(financial_loan[total_payment])
```

```dax
T.Average Interest Rate = AVERAGE(financial_loan[int_rate])
```

```dax
T.Average DTI = AVERAGE(financial_loan[dti])
```

## Month-to-Date (MTD)

```dax
MTD Loan Applications = CALCULATE([Total Loan Applications], DATESMTD(financial_loan[issue_date]))
```

```dax
MTD funded Amount = CALCULATE([Total Funded Amount], DATESMTD(financial_loan[issue_date]))
```

```dax
MTD Amount Received = CALCULATE([Total Amount Received], DATESMTD(financial_loan[issue_date]))
```

```dax
MTD Interest Rate = CALCULATE([T.Average Interest Rate], DATESMTD(financial_loan[issue_date]))
```

```dax
MTD DTI = CALCULATE([T.Average DTI], DATESMTD(financial_loan[issue_date]))
```

## Previous month (SPL)

Takes the last month in scope and returns the value for the month before it.

```dax
SPL Loan Applications =
CALCULATE([Total Loan Applications], Calendar_Table[Month] = MAX(Calendar_Table[Month]) - 1)
```

```dax
SPL Funded Amount =
CALCULATE([Total Funded Amount], Calendar_Table[Month] = MAX(Calendar_Table[Month]) - 1)
```

```dax
SPL Amount Received =
CALCULATE([Total Amount Received], Calendar_Table[Month] = MAX(Calendar_Table[Month]) - 1)
```

```dax
SPL Interest Rate =
CALCULATE([T.Average Interest Rate], Calendar_Table[Month] = MAX(Calendar_Table[Month]) - 1)
```

```dax
SPL DTI =
CALCULATE([T.Average DTI], Calendar_Table[Month] = MAX(Calendar_Table[Month]) - 1)
```

## Month-over-Month (MoM)

```dax
MOM Loan Applications = DIVIDE([MTD Loan Applications] - [SPL Loan Applications], [SPL Loan Applications])
```

```dax
MoM Funded Amount = DIVIDE([MTD funded Amount] - [SPL Funded Amount], [SPL Funded Amount])
```

```dax
MOM Amount Received = DIVIDE([MTD Amount Received] - [SPL Amount Received], [SPL Amount Received])
```

```dax
MoM Interest Rate = DIVIDE([MTD Interest Rate] - [SPL Interest Rate], [SPL Interest Rate])
```

```dax
MoM DTI = DIVIDE([MTD DTI] - [SPL DTI], [SPL DTI])
```

Note: the previous-month logic subtracts 1 from the month number, so it assumes one calendar year of data (2021). Multi-year data would need a date-based version.

## Good Loan

```dax
Good Loan Applications = CALCULATE([Total Loan Applications], financial_loan[Good & Bad Loan] = "Good Loan")
```

```dax
Good Loan Application Percentage = DIVIDE([Good Loan Applications], [Total Loan Applications])
```

```dax
Good Loan Funded Amount = CALCULATE([Total Funded Amount], financial_loan[Good & Bad Loan] = "Good Loan")
```

```dax
Good Loan Total Received Amount = CALCULATE([Total Amount Received], financial_loan[Good & Bad Loan] = "Good Loan")
```

## Bad Loan

```dax
Bad Loan Applications = CALCULATE([Total Loan Applications], financial_loan[Good & Bad Loan] = "Bad Loan")
```

```dax
Bad Loan Application Percentage = DIVIDE([Bad Loan Applications], [Total Loan Applications])
```

```dax
Bad Loan Funded Amount = CALCULATE([Total Funded Amount], financial_loan[Good & Bad Loan] = "Bad Loan")
```

```dax
Bad Loan Total Received Amount = CALCULATE([Total Amount Received], financial_loan[Good & Bad Loan] = "Bad Loan")
```

## Expected results (full data, no filters)

| KPI | Value | MTD (Dec) | MoM |
|---|---|---|---|
| Total Loan Applications | 38,576 | 4,314 | +6.9% |
| Total Funded Amount | $435.8M | $54.0M | +13.0% |
| Total Amount Received | $473.1M | $58.1M | +15.8% |
| Average Interest Rate | 12.0% | 12.4% | +3.5% |
| Average DTI | 13.3% | 13.7% | +2.7% |
