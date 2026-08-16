# Week 1: Data Preparation and Exploratory Data Analysis Report

This report outlines the real-world problem, dataset selection, data cleaning methodology (including mathematical documentation of the price imputation), a structured missingness audit, and the initial exploratory data analysis.

---

## 1. Problem Formulation & Stakeholder Analysis

### Problem Statement
London's property market is highly diverse, with home values exhibiting massive spatial variation. While geographical distance to central London is a primary driver, secondary neighbourhood-level characteristics—such as crime rates, deprivation, and public transport connectivity—substantially influence both local property values and quality of life. Understanding how these factors associate with property prices is essential for identifying locations that offer "value for money."

### Stakeholders & Value Proposition
- **Homebuyers:** Gain data-driven insights to evaluate if a neighbourhood's safety, transport links, and deprivation level justify its premium, helping them find undervalued areas.
- **Property Investors:** Identify up-and-coming areas by analyzing how transport upgrades or deprivation reductions correlate with historical capital growth.
- **Urban Planners & Policy Makers:** Gain a granular view of how transport accessibility and public safety influence local economies and property values, supporting resource allocation.
- **Local Authorities (Councils):** Quantify the economic return of crime-reduction and neighborhood-beautification initiatives to justify capital expenditures.

---

## 2. Data Selection & Geoprocessing Challenges

To analyze these factors, we integrated four distinct public datasets at the highly granular **Lower Layer Super Output Area (LSOA)** level, yielding approximately 4,800 observations across London.

### Datasets Selected
1. **Median House Prices (ONS):** *HPSSA Dataset 46 - Median price paid for residential properties by LSOA*. Selected over borough averages to capture neighborhood-level variations and minimize the skew of ultra-expensive outliers.
2. **Recorded Crime Counts (MPS):** *MPS LSOA Level Crime (Historical)*. Covers all crimes recorded by the Metropolitan Police Service for the year 2022.
3. **Index of Multiple Deprivation (IMD) 2019 (MHCLG):** Provides a composite measure of relative deprivation using 7 domains (income, employment, education, health, crime, housing, and living environment).
4. **Public Transport Accessibility Levels (PTAL / PTAI) 2015 (GLA/TfL):** Measures a neighborhood's connectivity to the public transport network based on walking distance to transit access points and service frequency.

### Geoprocessing and Boundary Code Mismatch
The MPS crime dataset was published using newer **LSOA 2021** codes, whereas the other three datasets utilized **LSOA 2011** codes. 

To resolve this mismatch, we implemented a geoprocessing pipeline:
- **ONS LSOA 2021 to LSOA 2011 Best Fit Lookup** was applied.
- For cases where one LSOA 2021 mapped to multiple LSOA 2011 codes (119 occurrences), crime counts were divided equally between the corresponding 2011 LSOAs to avoid double-counting.
- For cases where multiple LSOA 2021 codes mapped to one LSOA 2011, crime counts were aggregated.
- To resolve the remaining 181 unmapped London LSOA 2021 codes, we developed an automated script querying the **ONS Postcode Directory (ONSPD)** to map each postcode to its constituent LSOA 2011 boundary, assigning the LSOA 2021 to the LSOA 2011 that contains the majority of its postcodes, minimising data loss while maximising geographical coverage.

---

## 3. Data Cleaning, Imputation & Missingness Audit

### Structured Data Audit (Before & After)

Below is the structured diagnostic audit detailing the column-by-column missingness counts and the narrative action log:

| Dataset | Target Column | Missing/Suppressed (Raw) | Narrative Action / Cleanup Log | Missing (Cleaned Dataset) |
| :--- | :--- | :---: | :--- | :---: |
| **ONS House Prices** | `Year ending Dec 2022` | 75 LSOAs | Checked historical prices (2016–2022). Excluded **22 LSOAs** with zero historical observations. Excluded **53 LSOAs** with no data since Dec 2020 (unreliable to impute). Imputed remaining missing values using linear interpolation or London-wide growth rates (see math below). | 0 (for 4,757 LSOAs) |
| **MPS Crime** | `Total Crime 2022` | 3 LSOAs | Excluded City of London LSOAs because they fall under the City of London Police rather than the Metropolitan Police Service. | 0 (for 4,757 LSOAs) |
| **IMD 2019** | `IMD Score` | 0 | Merged successfully using the common LSOA 2011 code. | 0 (for 4,757 LSOAs) |
| **GLA PTAL** | `Average PTAI 2015` | 0 | Merged successfully using the common LSOA 2011 code. | 0 (for 4,757 LSOAs) |

### Mathematical Documentation of Price Imputation

For LSOAs missing the `Year ending Dec 2022` house price, we employed a hierarchical imputation model:

#### Method 1: Linear Interpolation (Preferred)
If an LSOA was missing its Dec 2022 price but had a prior price $P_{prev}$ (at quarterly index $T_{prev}$, not earlier than Dec 2017) and a subsequent price $P_{next}$ (at quarterly index $T_{next}$, i.e., March 2023), the missing price was imputed using linear interpolation:
$$P_{Dec2022} = P_{prev} + \frac{P_{next} - P_{prev}}{T_{next} - T_{prev}} \times (T_{target} - T_{prev})$$
Where $T$ represents the number of quarters.

#### Method 2: Compounding Quarterly Growth Rate
If subsequent data (March 2023) was unavailable, we estimated the missing price using the last available historical observation $P_{last}$ (at quarter $T_{last}$) and applying the average quarterly growth rate across London for the intervening periods:
$$\bar{g}_{q} = \frac{1}{M} \sum_{j=1}^M \left( \frac{P_{j} - P_{j-1}}{P_{j-1}} \right)$$
$$P_{Dec2022} = P_{last} \times (1 + \bar{g}_{q})^{T_{target} - T_{last}}$$
Where $\bar{g}_{q}$ is the London-wide average quarterly growth rate (computed as $+0.42\%$ for the Sep-Dec 2022 quarter).

---

## 4. Exploratory Data Analysis & Sensitivity Considerations

### Sensitivity Analysis: Assumptions of Static Transport Links (7-Year Window)
A key limitation of this analysis is the temporal misalignment between transport accessibility data (PTAL from **2015**) and house prices/crime data (**2022**). 
Assuming transport accessibility remains static over a 7-year window introduces analytical sensitivities:
- **Major Transport Projects:** Significant infrastructure upgrades occurred between 2015 and 2022, most notably the construction of the Elizabeth Line (Crossrail), London Overground extensions, and the Northern Line extension to Battersea Power Station.
- **Analytical Bias:** LSOAs surrounding new stations will have underestimated transport accessibility in our dataset (using 2015 scores), which might falsely inflate the residual "location premium" in our models, leading to spatial autocorrelation errors. This sensitivity must be kept in mind when interpreting transport regression coefficients.

### Exploratory Visualizations

We updated all visual assets to fix spelling errors (e.g. "Deprivation") and enhance labels for executive presentations.

#### Distribution Histograms
Descriptive statistics show that both median house prices and crime counts are heavily right-skewed, whereas deprivation score is moderately right-skewed, and PTAL is heavily skewed towards lower values.

<p align="center">
  <img src="pictures/hist.png" width="80%">
</p>

#### Boxplot Distribution (Spelling Corrected)
The boxplots identify several extreme outliers. Rather than data entry errors, these outliers represent genuine characteristics of London (e.g. extremely high property values in Kensington and Chelsea and high commercial crime counts in Westminster).

<p align="center">
  <img src="pictures/boxplots.png" width="80%">
</p>

#### Correlation Heatmap (Enhanced Readability & Significance Markers)
The correlation matrix has been updated to include statistical significance markers. 

<p align="center">
  <img src="pictures/corr_mtx.png" width="60%">
</p>

- House price exhibits a moderate negative correlation with deprivation ($r = -0.40^{***}$).
- House price has a weak positive correlation with transport accessibility ($r = 0.18^{***}$).
- Overall total crime has almost zero linear relationship with house prices ($r = -0.01\text{ (ns)}$) when looking at all London. However, this is heavily confounded by central London outliers, which we unpack in the statistical inference section.
