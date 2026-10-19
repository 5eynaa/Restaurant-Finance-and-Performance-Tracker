# Restaurant Finance and Performance Tracker

<p align="center">
    <img alt="Power Query" src="https://img.shields.io/badge/Power_Query-Excel-217346?logo=microsoftexcel&logoColor=white">
    <img alt="Pivot Tables" src="https://img.shields.io/badge/Pivot_Tables-Excel-217346?logo=microsoftexcel&logoColor=white">
    <img alt="REST API" src="https://img.shields.io/badge/REST_API-Dojo-0B6EFD?logo=json&logoColor=white">
</p>

An Excel-based reporting system for an independent café in London, built to replace manual data entry with automated daily reporting on sales, costs and profitability. This was built against and for a live business with real trading data rather than a sample dataset

## What it does
 
The system pulls data from three sources into one workbook and reports on it daily:
 
| Source | Method | Output |
|---|---|---|
| Dojo card terminal | REST API via Power Query | Daily card takings |
| Business bank statements | Monthly CSV files via Power Query | Categorised expenses |
| Payroll and fixed costs | Manual tables inside the workbook | Salaries, manual expenses |

## What it consists of

Card takings used to be downloaded as a file and copied into the workbook by hand every day. The workbook now connects straight to the card payment provider and brings the figures in by itself.
 
The connection takes care of the following items:

- Refunds are taken off the day's sales
- Repeated records are removed
- Only completed days are brought in, so a day still in progress does not appear

The figures land in their own table and feed the sales ledger by date via XLOOKUP. The automated figures and the hand-entered cash are kept apart.

### Spending from bank statements

Monthly bank statement files are saved to a folder. The workbook reads every file in that folder and combines them.

- The merchant/supplier name is pulled out of the bank's description text
- A lookup list matches each name to a spending category
- Anything the list does not recognise is labelled rather than dropped, so it stays visible and can be looked into

Categories used: stock, supplies, utilities, equipment, subscriptions, bank fees and rent.

### Dashboard

A date selector drives every figure on the dashboard, with a choice of a single month or a custom range.
 
The dashboard shows:
 
- Gross Revenue
- Total Expenses
- Salaries
- Net Margin
- Net Profit
- Sales Trend
- KPI details of selected time period

<img width="1833" height="1104" alt="Cafe_finance_tracker_dashboard" src="https://github.com/user-attachments/assets/7273a519-b3c1-4d9c-bf5a-99eea8947c29" />

---

## How it is set up

Automated figures and hand-entered figures sit in separate tables, so an update only touches the automated side.
 
Spending that does not match the lookup list is labelled rather than removed, so it still appears in the totals.
 
Stock costs and running costs are recorded under separate categories and reported separately.
 
The steps that clean and combine the data are held in Power Query rather than in cell formulas, so they run again each time the workbook is updated.

---

## Tools used
 
Excel, Power Query, pivot tables, OneDrive, and a connection to the card payment provider's reporting service.
