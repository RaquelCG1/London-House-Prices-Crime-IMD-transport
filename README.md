# London House Prices and Neighbourhood Characteristics Analysis

This repository investigates the relationship between house prices, crime, deprivation, and public transport accessibility across London at the Lower Layer Super Output Area (LSOA) level (~4,800 neighbourhoods).

We merge and analyse four public datasets (ONS House Prices, MPS Crime, IMD 2019, and GLA PTAL 2015) to evaluate property values against neighbourhood indicators and assist stakeholders like homebuyers, investors, and local authorities.

---

## Repository Structure

```
.
├── main.ipynb                              # Full consolidated analysis notebook
├── week1_data_preparation_eda_report.md   # Week 1 report
├── week2_statistical_inference_report.md  # Week 2 report
├── week3_executive_summary_report.md      # Week 3 report
├── pictures/                              # All generated figures (15 plots)
├── data/                                  # Raw and integrated datasets
│   └── final_dataset.csv                  # Merged analysis-ready dataset
├── Neighbourhood Characteristics and House Prices in London.twb  # Tableau workbook
├── requirements.txt
└── .gitignore
```

### Key Files

- **[main.ipynb](main.ipynb)** — The single consolidated Jupyter notebook containing the entire project workflow:
  1. Data loading and ONS postcode directory boundary mapping (LSOA 2021 → LSOA 2011).
  2. Data cleaning, linear interpolation, and compounding quarterly growth rate price imputation.
  3. Exploratory Data Analysis (EDA) of numerical variables.
  4. Public Transport Accessibility Levels (PTAL) analysis — quintiles, Mann-Whitney U test, OLS regression.
  5. Index of Multiple Deprivation (IMD) analysis — quintiles, Welch's t-test.
  6. Crime scenario analyses — Welch's t-tests, multiple log-log regression, VIF multicollinearity checks, residual diagnostics.
  7. All visualisations saved to `pictures/`.

- **[pictures/](pictures/)** — Unified folder for all 15 generated plots (EDA, hypothesis testing, regression diagnostics).
- **[data/](data/)** — Raw source files and the merged `final_dataset.csv`.
- **Tableau**: `Neighbourhood Characteristics and House Prices in London.twb` is tracked in Git. The packaged `.twbx` is excluded via `.gitignore` due to its large size (~10 MB) — generate it locally from the `.twb` file using Tableau Desktop.

---

## Setup & Running (Windows)

```powershell
# Create and activate virtual environment
python -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Launch the notebook
jupyter notebook main.ipynb
```
