# SIOP Forecast Reporting Dashboard

## Project Overview

This project is a Power BI dashboard developed for SIOP reporting and forecast performance analysis. The dashboard helps analyze Revenue Forecast, Non-Revenue Forecast, and CAPEX Forecast across different countries using lag-based forecast snapshots.

The main objective of this project is to compare forecast values with actual sales data and evaluate forecast performance using Forecast Accuracy % and Forecast Bias %.

## Dashboard Features

- Revenue Forecast by Country
- Non-Revenue Forecast by Country
- CAPEX Forecast by Country
- Lag Selection Filter
  - Resultant
  - Lag 0
  - Lag 1
- Period Filter
- Country Filter
- Forecast Accuracy %
- Forecast Bias %
- Total Sales Actual Quantity
- Selected Revenue Forecast

## Tools Used

- Power BI Desktop
- Power Query Editor
- DAX Measures
- GitHub

## Data Transformation Steps

1. Imported the given Excel data into Power BI.
2. Loaded the required tables:
   - Forecast
   - Actual
   - Actuals Filter Database
3. Created a Lag Name column based on AsOfPeriod:
   - 2023 P12 as Resultant
   - 2023 P11 as Lag 0
   - 2023 P10 as Lag 1
4. Filtered only Resultant, Lag 0, and Lag 1 records.
5. Unpivoted forecast columns:
   - Revenue Forecast
   - Non-Revenue Forecast
   - CAPEX Forecast
6. Created combined forecast column names.
7. Pivoted the data to create separate forecast columns for each lag.
8. Replaced null values with 0.
9. Grouped actual sales data by Item, Country, and Period.
10. Merged Forecast and Actual tables using:
    - Item
    - Country
    - Period
11. Created DAX measures for selected forecast, forecast accuracy, and forecast bias.

## DAX Measures Used

### Selected Revenue Forecast

```DAX
Selected Revenue Forecast =
VAR SelectedLag = SELECTEDVALUE('Lag Selection'[Lag], "Lag 0")
RETURN
SWITCH(
    SelectedLag,
    "Resultant", SUM('Forecast'[Resultant Revenue Forecast]),
    "Lag 0", SUM('Forecast'[Lag 0 Revenue Forecast]),
    "Lag 1", SUM('Forecast'[Lag 1 Revenue Forecast])
)
