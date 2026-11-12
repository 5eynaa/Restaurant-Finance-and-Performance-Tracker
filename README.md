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
| Till Z reports | Email read by Google Apps Script, published sheet read by Power Query | Daily cash takings |
| Business bank statements | Monthly CSV files dropped into a folder, combined by Power Query | Categorised expenses |
| Cash costs | Manual expenses table inside the workbook | Expenses missing from the bank statements |
| Handwritten staff timesheets | Photo transcribed with AI OCR, then checked by hand | Salaries |

## What it consists of

### Card takings

Card takings used to be downloaded as a file and copied into the workbook by hand every day. The workbook now connects straight to the card payment provider and brings the figures in by itself.
 
The connection takes care of the following items:

- Refunds are taken off the day's sales
- Repeated records are removed
- Only completed days are brought in, so a day still in progress does not appear

The figures land in their own table and feed the sales ledger by date via XLOOKUP. The automated figures and the hand-entered cash are kept apart.



### Cash takings from the till

The till does not offer an API, however, it does send an email every time a Z report (the end-of-day summary) is printed. That email holds the day's cash total, this becomes the data source.
 
A Google Apps Script runs once every evening on a timer. Each run it:
 
1. Searches the email inbox for Z report emails from the till provider, looking back over the last 14 days
2. Strips the email down to plain text and reads the report date, print time, cash total and report ID
3. Skips any report ID already recorded to prevent duplicate records or records getting overwritten
4. Flags any date that ends up with two reports
5. Adds the new rows to source Google Sheet and sorts it by date
 
The Google Sheet is published as a link. Power Query in the workbook reads that link on refresh, and pulls each day's cash by date. A day with no Z report stays blank rather than showing zero.



### Spending from bank statements

Monthly bank statement files are saved to a folder. The workbook reads every file in that folder and combines them.

On refresh, Power Query:
 
- Reads every CSV in the folder and stacks them into one table
- Sets the dates and amounts to the right data types
- Pulls the merchant/supplier name out of the bank's description text
- Matches each name to a spending category using a lookup list

Categories used: stock, supplies, utilities, equipment, subscriptions, bank fees and rent.



### Manual expenses

Some costs are paid in cash and they don't appear on a bank statement, these go into a separate manual expenses table inside the workbook with a date, description, category and amount.



### Salaries
 
Staff clock in and out is on a paper timesheet rather than an electronic system. To get those hours into the workbook without retyping every line:
 
1. A photo is taken of the timesheet
2. The columns that matter are highlighted on the photo: date, clock-in time, clock-out time and hours worked
3. The photo is passed to an AI model with OCR (Claude or Gemini), which transcribes the times under the matching headers in the salaries sheet
4. The transcribed figures are checked against the original sheet before salaries are marked as final



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

## Tools used
 
Excel, Power Query, pivot tables, OneDrive, and a connection to the card payment provider's reporting service.
