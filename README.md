# Bank-Loan-Analysis

Loan analysis of a bank dataset: exploring loan applications, funded amounts, amounts received, interest rates, and DTI to find key lending insights.

## Objective

Analyze bank loan data to track key lending KPIs (applications, funded amount, amount received, interest rate, and DTI) with Month-to-Date (MTD) and Month-over-Month (MoM) changes, compare good loans with bad loans, and understand how lending is distributed across time, states, loan terms, employment lengths, loan purposes, and home ownership.

## Dataset

The dataset contains 38,576 loan records issued between January 1 and December 12, 2021. Each record includes loan status, grade, sub-grade, term, purpose, state, home ownership, employment length, interest rate, DTI, installment, loan amount, and total payment received.

## Tools Used

* Power BI
* DAX measures (Total Loan Applications, Total Funded Amount, Total Amount Received, Average Interest Rate, Average DTI, plus MTD and MoM versions of each)
* Data modeling (fact table, Calendar table, and a measures table)

## Dashboards

* Summary: key KPIs, good vs bad loan split, and a loan status grid.
* Overview: monthly trend and breakdowns by state, term, employment length, purpose, and home ownership.
* Details: a loan-level table with filters for state, grade, and good vs bad loan.

![Summary](Images/summary.jpg)
![Overview](Images/overview.jpg)
![Details](Images/details.jpg)

## Key Insights

* Overall: 38,576 loan applications, $435.76M funded, and $473.07M received (108.6% of the funded amount). The average interest rate is 12.05% and the average DTI is 13.33%.
* Latest month (December 2021, MTD): 4,314 applications (up 6.91% MoM), $53.98M funded (up 13.04%), and $58.07M received (up 15.84%). Average interest rate is 12.36% (up 3.47%) and average DTI is 13.67% (up 2.73%).
* Trend: Monthly applications rose in every month except February, from 2,332 in January to 4,314 in December (up 85.0%).
* Good vs Bad Loans: Good loans (Fully Paid and Current) make up 86.18% of applications (33,243), with $370.22M funded and $435.79M received. Bad loans (Charged Off) make up 13.82% (5,333), with $65.53M funded and only $37.28M received. Good loans returned 117.7% of the funded amount, while bad loans returned 56.9%.
* Loan Status: 83.33% of loans are Fully Paid, 13.82% Charged Off, and 2.85% Current. Charged Off loans carry a higher average interest rate (13.88%) than Fully Paid loans (11.64%).
* Grade: Grade B has the most applications (11,674, 30.26%). The charge-off rate rises with the grade, from 5.7% in grade A to 31.3% in grade G.
* State: California (6,894, 17.87%) and New York (3,701, 9.59%) together account for 27.47% of applications.
* Term: 36-month loans make up 73.2% of applications (28,237) and 60-month loans make up 26.8% (10,339).
* Employment Length: Borrowers with 10+ years of employment submit the most applications (8,870, 22.99%).
* Purpose: Debt consolidation leads with 18,214 applications (47.2%). Together with credit card (4,998, 13.0%), it makes up 60.17%.
* Home Ownership: Renters (47.80%) and mortgage holders (44.58%) make up over 92% of applications.

## Data Limitations

The dataset covers only 2021, and its latest issue date is December 12, so December figures cover part of the month and year-over-year comparison is not possible. Good and bad loans are defined by loan status: Good is Fully Paid and Current, Bad is Charged Off. Current loans are still active, so their final outcome may change. The analysis focuses on the requested KPIs and does not include default prediction or profitability modeling. The employer title is missing for 1,438 records, but it is not used in the analysis.
