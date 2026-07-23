# Crime Analysis and Statistical Inference Report

## Crime and House Prices Across London LSOAs (2022)

This analysis examines the relationship between recorded crime and median house prices across **4,757 London LSOAs**. To test whether the results were influenced by unusual areas, the analysis was repeated using four scenarios: All London, Excluding Westminster, Excluding Westminster & Kensington and Chelsea, Excluding the top 5% of crime and house-price values.

---

## Task 1: Exploratory Data Analysis

The distributions of both median house prices and total crime are right-skewed. Across all London LSOAs, total crime had a very weak positive correlation with median house price. However, the relationship changed when influential areas were excluded. The correlation became negative after removing Westminster and became increasingly negative after further exclusions.

![Crime and house prices across four scenarios](crime_report_figures/02_scenario_scatter.png)

These results suggest that the overall London relationship is affected by a small number of influential areas with unusual combinations of crime and property prices.

---

## Task 2: Hypothesis Testing

### Hypothesis 1: Do high-crime areas have lower house prices?

The analysis compared the top 25% and bottom 25% of LSOAs by crime level within each scenario. A one-tailed t-test was used to test whether high-crime areas had lower mean house prices.

The null hypothesis was rejected in all four scenarios (**p < 0.001**).

![House prices in high- and low-crime groups](crime_report_figures/03_h1_boxplots.png)

The results consistently show lower house prices in the high-crime group. The largest difference occurred after excluding Westminster and Kensington and Chelsea.

### Hypothesis 2: Are individual crime categories associated with house prices?

A multiple log-log regression was used to examine the ten crime categories simultaneously. The models explained between **24.9% and 29.3%** of the variation in log house prices across the four scenarios.

![Multiple log-log regression coefficients](crime_report_figures/04_h2_coefficients.png)

---

## Task 3: Correlation and Regression Analysis

The correlation analysis showed that crime categories have different relationships with house prices. **Violence Against The Person** had the strongest negative correlation with house prices.

![Correlation matrix](crime_report_figures/05_correlation_heatmap.png)

Overall, the results in the multiple regression models suggest that **the type of crime is more informative than total crime alone** when examining differences in London house prices. The results also show that the apparent relationship between total crime and house prices changes substantially when influential areas are excluded.

---

## Conclusion

The analysis found three main results:

1. **Total crime alone has a weak relationship with house prices**, and the direction of the relationship changes when influential areas are excluded.
2. **High-crime areas have significantly lower average house prices** across all four scenarios.
3. **Different crime categories have different relationships with house prices**, with violent crime showing the most consistent negative association.

The results demonstrate the importance of considering spatial outliers and crime composition when analysing the relationship between crime and property prices across London.


# Public Transport Accessibility and House Prices Across London LSOAs (2022)

This analysis investigates whether neighbourhoods with better public transport accessibility tend to have higher median house prices across London LSOAs.

## Exploratory Data Analysis

Descriptive statistics and boxplots showed that public transport accessibility (PTAI) is positively skewed, with a large number of high values identified as outliers by the boxplot. Inspection of these observations confirmed that they correspond to central London LSOAs with exceptionally good public transport accessibility and therefore represent genuine characteristics of the data rather than errors. These observations were retained for the subsequent analysis.



<p align="center">
  <img src="transport_report_figures/scatter.png" width="60%">
</p>

The scatter plot suggests a weak positive relationship between public transport accessibility and median house prices. While areas with better transport accessibility tend to have higher house prices, there is substantial variation, indicating that transport accessibility alone is not a strong predictor of house prices.

## Hypothesis Testing

### Hypothesis: Do areas with better public transport accessibility have higher house prices?

The analysis compared the top 25% and bottom 25% of LSOAs by public transport accessibility (PTAI). Since house prices were highly skewed, a one-tailed Mann–Whitney U test was used instead of a t-test to assess whether areas with higher transport accessibility have higher median house prices.

The Mann–Whitney U test indicated a statistically significant difference between the two groups (U = 561,887.5, p < 0.001).

<p align="center">
  <img src="transport_report_figures/boxplot.png" width="50%">
</p>

The results show that neighbourhoods with higher public transport accessibility have significantly higher house prices. The median house price increased from approximately £500,000 in the bottom 25% of PTAI areas to £585,000 in the top 25%.

## Correlation and Regression Analysis

### Pearson Correlation

Pearson's correlation coefficient was calculated to measure the strength and direction of the linear relationship between public transport accessibility and median house prices across London LSOAs.

A weak positive correlation was found (r = 0.181, p < 0.001) which indicates that neighbourhoods with better public transport accessibility tend to have higher house prices, although the relationship is relatively weak.

### Simple Linear Regression

A simple linear regression model was fitted to quantify the relationship between public transport accessibility and median house prices. The model estimates the expected change in median house price associated with a one-unit increase in Average PTAI.

Statistic |	Value
---------- | ---------
Coefficient	| £5,834
95% CI	| £4,933 – £6,734
R²	| 0.033
p-value	| < 0.001

The regression model was statistically significant (p < 0.001). On average, each one-point increase in Average PTAI was associated with an increase of approximately £5,834 in median house price. However, the model explained only 3.3% of the variation in house prices (R² = 0.033), indicating that public transport accessibility alone is a relatively weak predictor of property values.

## Conclusion

Overall, the correlation and regression analyses produced consistent results. Public transport accessibility was positively associated with house prices, but the relationship was relatively weak. This suggests that while transport accessibility contributes to property values, other neighbourhood characteristics such as deprivation and crime are also likely to play an important role.

Improving public transport accessibility may contribute to higher property values, but transport alone is unlikely to transform neighbourhood housing markets. Policymakers and urban planners should therefore consider transport investment alongside broader regeneration initiatives, including improvements in safety, local services and neighbourhood quality.