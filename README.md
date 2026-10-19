# Restaurant-Finance-and-Performance-Tracke

<p align="center">
    <img alt="Excel" src="https://img.shields.io/badge/Excel-Workbook-217346?logo=microsoftexcel&logoColor=white">
    <img alt="Power Query" src="https://img.shields.io/badge/Power_Query-M-217346?logo=microsoftexcel&logoColor=white">
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
| Payroll and fixed costs | Manual tables inside the workbook | Salaries, rent accruals |
