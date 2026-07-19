# Group3_Masters

# London House Prices and Crime Analysis

This project investigates the relationship between house prices, crime, deprivation, and public transport accessibility across London at **LSOA** level.

## Data Sources

* ONS Median House Prices
* Metropolitan Police Service Crime Data
* Index of Multiple Deprivation (IMD) 2019
* Public Transport Accessibility Levels (PTAL)

## Setup (Windows)

Open VS Code (or your preferred IDE) and open a new terminal. Then run:

```
git clone https://github.com/Olesya-drozh/Group3_CFGMasters.git
cd Group3_CFGMasters
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```
Finally, open main.ipynb, select the .venv Python interpreter if prompted, and run the notebook cells.

## Week 1

* Imported and cleaned all datasets.
* Converted crime data from LSOA 2021 to LSOA 2011.
* Aggregated monthly crime data into 2022 totals by LSOA and crime group.
* Cleaned the house price data and estimated suitable missing 2022 values using interpolation and the average quarterly growth rate.
* Merged the Crime, House Prices, IMD, and PTAL datasets into a single dataset.
* Completed exploratory data analysis (EDA).

## Week 2
