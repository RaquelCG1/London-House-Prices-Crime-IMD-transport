# Group 3 CFG Masters Report - Week 3 Assignment

## Executive Summary
This report looks at what makes London house prices go up or down. We wanted to find out if safety, poverty (deprivation), and transport links affect property values. 

To do this, we combined four different public datasets at a neighbourhood level (called LSOAs). We found that:
1. **Poverty has the biggest impact:** Areas with higher deprivation have much cheaper houses.
2. **Crime is complicated:** Just looking at "total crime" can be confusing. Central areas like Westminster have lots of crime (because of tourists and shops) but still have extremely expensive houses. However, when we remove these outliers, we see that higher crime does lead to lower house prices. Also, violent crime drops property values much more than theft.
3. **Transport adds value:** Good transport links make houses more expensive, adding about £5,800 to the price for every step up in accessibility.

This report helps homebuyers find good value, helps investors make smart choices, and helps local councils decide where to improve neighbourhoods.

---

## Introduction/Problem Formulation

### The Problem
Why are some houses in London so expensive while others are much cheaper? It is not just about the size of the house or the postcode. Other factors in the neighbourhood play a big role:
- **Poverty (Deprivation):** Do poorer neighbourhoods have cheaper houses?
- **Crime:** Does a high crime rate scare people away and lower house prices?
- **Public Transport:** Do people pay a premium to live near tube and train stations?

Our goal is to explore these questions and find neighbourhoods that offer the best "value for money."

### Who Care About This? (Stakeholders)
- **Homebuyers:** Families looking for a safe, affordable area with good transport.
- **Property Investors:** People looking to buy houses that will grow in value.
- **Local Councils:** Planners who want to make neighbourhoods safer and better connected.

---

## Data Exploration and Analysis

### Where We Got the Data (Collection)
We gathered data for approximately 4,800 small neighbourhoods in London (called LSOAs) from four main sources:
1. **House Prices (2022):** From the Office for National Statistics (ONS).
2. **Crime Counts (2022):** From the Metropolitan Police.
3. **Indices of Deprivation (2019):** From the UK Government (measuring income, health, and employment).
4. **Transport Accessibility (PTAL, 2015):** From Transport for London (TfL).

### Cleaning and Preparing the Data
Before we could compare them, we had to fix a few issues:
- **Matching Area Codes:** The crime dataset used 2021 area codes, but the others used 2011 codes. We used a special lookup table to translate and match them correctly.
- **Missing Data:** Some areas had missing house prices. We estimated these by looking at their past prices and growth rates.
- **City of London:** We removed the City of London because it has its own police force, so crime data was missing.
In the end, we had a clean dataset of **4,757 neighbourhoods**.

---

## Results and Findings

### 1. Poverty and House Prices
Neighbourhoods with lower deprivation (less poverty) have significantly higher house prices. The average house price in less-deprived areas is around **£736,000**, compared to **£499,000** in highly deprived areas. 

### 2. Transport and House Prices
Having good transport links definitely increases house prices. Our analysis showed that a one-point increase in transport accessibility (PTAI score) increases the average house price by about **£5,834**.

### 3. Crime and House Prices
This was our most interesting finding. At first glance, total crime seemed to have almost no effect on house prices. But when we looked closer, we found two reasons why:
- **The Westminster Effect:** Westminster is a massive outlier. It has the highest crime in London (due to tourists, pickpockets, and nightlife) but also has some of the most expensive homes. When we exclude Westminster and Kensington & Chelsea from our analysis, we see that higher crime is indeed linked to lower house prices.
- **Type of Crime Matters:** Violent crime (like assault) has a strong negative effect on house prices. However, theft has a positive correlation because theft happens most in wealthy, expensive shopping areas.

### Interactive Dashboard
To explore our findings visually, you can view our interactive Tableau dashboard:
[Neighbourhood Characteristics and House Prices in London](https://public.tableau.com/app/profile/raquel.cancho.gasulla/viz/NeighbourhoodCharacteristicsandHousePricesinLondon/Dashboard1)

---

## Conclusion/Recommendations

### For Homebuyers
- **Look for safety, not just total crime:** Don't be scared off by high "total crime" numbers in central areas. Look at the type of crime. Avoid areas with high violent crime, but don't worry as much about theft rates.
- **Find "border" areas:** Look for affordable neighbourhoods that are right next to areas with great transport links. You get the benefit of transport without paying the premium.

### For Investors
- **Regeneration areas:** Look for poorer areas where the council is planning new transport links. These transport improvements will drive up house prices.

### For Local Councils
- **Combine transport with safety:** Just building a new station won't transform an area. Transport investments should be paired with safety measures like streetlights and CCTV, especially in poorer neighbourhoods.

---

## References
1. ONS Median House Prices by LSOA (1995-2023): https://www.ons.gov.uk/peoplepopulationandcommunity/housing/datasets/medianpricepaidbylowerlayersuperoutputareahpssadataset46
2. Metropolitan Police Recorded Crime Dataset (2022): https://data.london.gov.uk/dataset/recorded_crime_summary
3. English Indices of Deprivation (Ministry of Housing, Communities & Local Government, 2019): https://www.gov.uk/government/statistics/english-indices-of-deprivation-2019
4. TfL Public Transport Accessibility Levels (PTAL, 2015): https://data.london.gov.uk/dataset/public-transport-accessibility-levels
5. ONS Lower Layer Super Output Areas (December 2011) Boundaries EW BFC V3 (used for Tableau mapping): https://geoportal.statistics.gov.uk/datasets/ons::lower-layer-super-output-areas-december-2011-boundaries-ew-bfc-v3/about

