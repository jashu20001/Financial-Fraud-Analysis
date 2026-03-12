# Money Leak Detection in Credit Card Operations using Power BI

### Fraud Loss Monitoring and Behavioral Risk Pattern Analysis for Credit Card Transactions

---

## The Question

If a bank is losing money due to fraud, can we find **patterns that explain why it is happening** instead of only reporting how much was lost?

Most dashboards built on fraud datasets only show fraud count or total fraud amount.  
That reports history. It does not help prevent future fraud.

This project treats fraud as a **money leak problem** and investigates whether the system could have predicted these frauds earlier by analyzing transaction behavior.

---

## The Dataset

The dataset used is the well known Credit Card Fraud Detection dataset containing:
https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud
- **284,807 transactions**
- **31 columns**
- Features: `Time`, `Amount`, `Class`
- 28 anonymized behavioral features: `V1` to `V28` generated using PCA

The `Class` column indicates whether a transaction is **Normal (0)** or **Fraud (1)**.

---

## What We Built From Scratch

To convert raw transaction data into decision-making visuals, new fields and measures were created.

### New Columns Created

- **Hour** extracted from `Time` to understand activity across the day
- **Amount Range** to group transactions into meaningful bins

### DAX Measures Created

```DAX
Total Transactions = COUNTROWS(creditcard)

Fraud Transactions =
CALCULATE(
    COUNTROWS(creditcard),
    creditcard[Class] = 1
)

Total Amount = SUM(creditcard[Amount])

Fraud Loss =
CALCULATE(
    SUM(creditcard[Amount]),
    creditcard[Class] = 1
)

Fraud % =
DIVIDE([Fraud Transactions], [Total Transactions])

PowerBI dashboard: https://app.powerbi.com/view?r=eyJrIjoiMGIyNDNhMzctY2FkNi00NTFiLTlhNTUtNGQ3MDBhN2ZhNTA3IiwidCI6Ijk2NDY0YThhLWY4ZWQtNDBiMS05OWUyLTVmNmI1MGEyMDI1MCIsImMiOjN9
