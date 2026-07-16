# Neighbourhood Characteristics and House Prices

Our goal is to explore which neighbourhood characteristics are most strongly associated with house prices in London. By analyzing data at the Lower Layer Super Output Area (LSOA) level, we have roughly 4,800 neighbourhoods to compare, allowing for robust statistical testing and multiple linear regression.

## Task 1: Identify a real-world problem
**Problem Statement:** Which neighbourhood characteristics (crime, public transport accessibility, deprivation, and school quality) are associated with house prices in London? Can we identify which areas offer the best value for money based on these metrics?

**Stakeholders:** Homebuyers, real estate developers, urban planners, and local authorities.
## Task 2: Data Selection
**Datasets Chosen & Sources:**
1. **Median House Prices (ONS):** Contains median house prices paid at the LSOA level. We chose this over borough-level averages because it prevents extreme luxury properties (outliers) from skewing the data. Timeframe: 1995 to 2023. `HPSSA Dataset 46 - Median price paid for residential properties by LSOA.xls` [https://www.ons.gov.uk/peoplepopulationandcommunity/housing/datasets/medianpricepaidbylowerlayersuperoutputareahpssadataset46](https://www.ons.gov.uk/peoplepopulationandcommunity/housing/datasets/medianpricepaidbylowerlayersuperoutputareahpssadataset46)
2. **MPS LSOA Level Crime (London Datastore):** Granular crime counts by category at the LSOA level. Allows us to test if specific crime types (e.g., burglary vs. anti-social behaviour) correlate differently with property values. Timeframe: July 2020 to June 2024. `MPS LSOA Level Crime (Historical).csv` [https://data.london.gov.uk/dataset/recorded_crime_summary](https://data.london.gov.uk/download/exy3m/vm7/MPS%20LSOA%20Level%20Crime%20(Historical).csv)
3. **Index of Multiple Deprivation (IMD 2019):** An official government measure of relative deprivation. Captures crucial socio-economic health variables (income, employment, health, education) in a single unified index. Timeframe: 2019. `File7:all ranks, deciles and scores for the indices of deprication, and population denominators` [https://www.gov.uk/government/statistics/english-indices-of-deprivation-2019](https://assets.publishing.service.gov.uk/media/5dc407b440f0b6379a7acc8d/File_7_-_All_IoD2019_Scores__Ranks__Deciles_and_Population_Denominators_3.csv)
4. **Public Transport Accessibility Levels (PTAL):** Measures public transport connectivity. Crucial for London, where transport links heavily dictate property desirability. Timeframe: 2015. `2015 PTAL LSOA 2011` [https://data.london.gov.uk/dataset/public-transport-accessibility-levels](https://data.london.gov.uk/download/24rz6/77d9b319-931e-4090-bf8e-f578938bd352/LSOA2011%20AvPTAI2015.csv)

**Justification for Approach:** 
By shifting to the Lower Layer Super Output Area (LSOA) level, we transform a basic 33-point borough analysis into a rich, complex 4,800-point dataset. This granularity allows for rigorous multiple linear regression, letting us isolate the specific impact of transport, crime, and deprivation on house prices.

**Navigating Real-World Data Limitations (Potential Issues):** 
While this dataset is incredibly rich, it comes with several real-world complexities that we expect to handle in our cleaning phase:
*   **Temporal Misalignment:** IMD is from 2019, PTAL is from 2015, and our Crime/Price data will be focused on 2022. We must assume that relative deprivation and transport infrastructure change slowly over time.
*   **Geographic Mismatches:** We will need to perform complex dataframe merges on `LSOA_Code`. It is highly likely that some datasets include areas outside of London or have missing codes that will result in missing data (`NaN`) after merging.
*   **Geographic Code Conversion** The crime dataset uses LSOA 2021 codes, while the house prices, IMD and PTAL datasets use LSOA 2011 codes. We therefore used the official ONS LSOA 2021 to LSOA 2011 Best Fit Lookup to make the geographical codes consistent across all datasets. Around 181 LSOAs (approximately 3% of London neighbourhoods) could not be matched during this conversion and were excluded from the crime dataset.

**Data Preparation**

To create a single analysis-ready dataset, the following data preparation steps were carried out:

*   **Crime Aggregation:** Monthly crime records were aggregated into annual totals for 2022 to match the selected house price data.
*   **Crime Categories:** Individual crime categories were pivoted into separate columns, and an additional total crime feature was created by summing all crime categories for each LSOA.
*   **House Price Processing:** House price suppression values (":") were converted to missing values (NaN) before being converted to numeric format.
*   **Missing Values:** Missing house prices were imputed using the most recent available rolling estimate in the following order: Dec 2022 → Sep 2022 → Jun 2022 → Mar 2022 → Dec 2021. This reduced the number of missing house prices to 111 observations (approximately 2% of the dataset).
*   **Dataset Integration:** The cleaned house prices, crime, IMD and PTAL datasets were merged using the common LSOA geographical identifier to create the final analytical dataset.

## Task 3: Exploratory Data Analysis (EDA)

Exploratory Data Analysis (EDA) was conducted to gain an initial understanding of the cleaned dataset, assess its overall quality, identify any remaining issues, and explore relationships between variables before carrying out statistical analysis and modelling.

The first step was to examine the overall structure of the dataset, including the number of observations and variables, data types, and the presence of any missing or duplicate records. The final merged dataset contains 4,835 observations (LSOAs) and 20 variables. There were 111 missing house price values (approximately 2% of the dataset) and 3 LSOAs with missing crime data. These three LSOAs all belong to the City of London, which is policed by the City of London Police rather than the Metropolitan Police Service (MPS). As a result, they are not included in the MPS crime dataset by design rather than due to a data quality issue. No duplicate records were identified, confirming that each LSOA appears only once in the final dataset.

Descriptive statistics were calculated for the key numerical variables to understand their central tendency, variability and range. House prices showed substantial variation across London, ranging from £147,500 to £6.43 million, with the mean (£618,617) considerably higher than the median (£520,000), indicating a strongly positively skewed distribution. Crime counts also varied widely (1–13,568 offences per LSOA), with a large difference between the mean (165) and median (114), suggesting that high crime levels are concentrated in a relatively small number of neighbourhoods. In contrast, the IMD score displayed a much more balanced distribution, while PTAI showed moderate positive skewness.

Boxplots and distribution plots revealed several outliers, particularly for house prices, crime and transport accessibility. The highest house prices were found mainly in Kensington and Chelsea and Westminster, while the highest crime levels were concentrated in Westminster, likely due to its busy shopping areas, tourist attractions and transport hubs. These appear to be genuine characteristics of the data rather than errors, so they were kept for the later analysis.

Correlation analysis identified a moderate negative relationship between house prices and deprivation (r = -0.34), a weak positive relationship with public transport accessibility (r = 0.18), and almost no linear relationship with total crime (r = 0.06). The unusually weak association between crime and house prices appears to be influenced by a small number of central London neighbourhoods, particularly Westminster, which combines exceptionally high house prices with very high recorded crime levels. These areas are potential influential outliers and  will be investigated further during the modelling stage.
