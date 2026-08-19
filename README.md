# U.S.-Housing-Affordability-Analysis
Final Capstone Project - U.C. Berkeley Professional Certificate in Machine Learning and Artificial Intelligence

## Project Overview
Housing affordability has become an increasingly important economic and social issue in the United States. Prospective homebuyers looking to achieve the “American Dream” are faced with increasing and often out-of-reach home prices, as well as navigating household income and broader economic conditions in the area where they live.

The purpose of this project is to explore how housing affordability has changed across 100 major U.S. metropolitan areas between 2010 and 2024. Using data from Zillow and the U.S. Census Bureau, this analysis examines home values, median household income, population, and educational attainment in 2010, 2015, and 2024.

The goal is to identify which metropolitan areas have become more or less affordable over time, explore the economic factors associated with those differences, and provide prospective homebuyers with a better understanding of how affordability varies across major U.S. housing markets.

Housing affordability is measured using the **price-to-income ratio**, which compares typical home values with median household income. This provides a consistent measure for comparing affordability across metropolitan areas and examining how it has changed over time.

## Problem Statement

**How has housing affordability changed across major U.S. metropolitan areas between 2010 and 2024, and what economic and demographic factors are associated with differences in home values and affordability?**

This analysis evaluates housing affordability primarily using home values relative to median household income, while population and educational attainment are explored as additional factors that may be associated with housing-market differences. Exploratory data analysis and multiple regression models are used to examine relationships among these variables, compare housing affordability across metropolitan areas and over time, and evaluate which factors are most strongly associated with affordability deterioration.

## Data Sources
This project combines housing and demographic data from multiple sources:
Zillow Home Value Index (ZHVI): Metropolitan-area home values used to measure changes in housing prices from 2010–2024.
U.S. Census Bureau / American Community Survey (ACS): Median household income, population, and educational attainment data for 2010, 2015, and 2024.
Geographic matching: Metropolitan-area names were standardized across the Zillow and Census datasets to create a consistent set of 100 U.S. metropolitan areas for analysis.
Source Links:
Zillow Research Data: https://www.zillow.com/research/data/
U.S. Census Bureau / ACS: https://www.census.gov

## Exploratory Data Analysis
Exploratory data analysis was conducted to examine housing affordability trends across the 100 metropolitan areas and identify differences between markets over time. The analysis focused on changes in home values, median household income, population, educational attainment, and the engineered price-to-income ratio.
Between 2010 and 2024, the average price-to-income ratio across the metros examined increased from approximately 3.39 to 4.69, indicating an overall deterioration in housing affordability. However, the magnitude of this change varied considerably across metropolitan areas.
Key areas explored included:
- Metros with the highest and lowest price-to-income ratios
- Metros experiencing the greatest deterioration in affordability
- Changes in home values and household income
- Population growth and decline
- Relationships between economic and demographic variables and affordability

## Data Preparation & Feature Engineering
Data from Zillow and the U.S. Census Bureau required cleaning and standardization before the datasets could be combined. Metropolitan-area names were standardized across sources to allow Zillow housing data to be matched with Census income, population, and educational attainment data. The analysis was then limited to 100 major metropolitan areas with the necessary data available for comparison across the selected years.
Several features were engineered to measure changes between 2010 and 2024, including:
Percent change in median household income
Percent change in population
Change in college educational attainment
Percent change in home values
Price-to-income ratio, calculated by dividing typical home value by median household income
Affordability percent change, measuring the change in price-to-income ratio from 2010 to 2024
For modeling, AffordabilityPctChange was selected as the continuous target variable. Income percent change, population percent change, and change in educational attainment were used as predictor features. Home value percent change was excluded from the predictors because home values are already incorporated into the calculation of the price-to-income ratio, which could introduce target leakage.
The modeling data was divided into 80% training data and 20% test data, using a random_state of 42 for reproducibility. Cross-validation was also used during model evaluation and hyperparameter tuning.
## Machine Learning Approach
This project uses supervised machine learning for a regression problem, as the target variable, AffordabilityPctChange, is continuous and measures the percent change in the price-to-income ratio from 2010 to 2024.
Three predictor features were used to explore factors associated with changes in housing affordability:
Percent change in median household income
Percent change in population
Change in college educational attainment
Four regression models were evaluated:
Linear Regression — used as the baseline model and to examine the direction and magnitude of relationships between the predictors and affordability change.
Ridge Regression — used to determine whether regularization could improve upon the baseline Linear Regression model.
Decision Tree Regressor — used to explore potential nonlinear relationships and feature importance.
Random Forest Regressor — used to determine whether combining multiple decision trees could improve predictive performance.
GridSearchCV with 5-fold cross-validation was used to tune the Ridge, Decision Tree, and Random Forest models. Model performance was evaluated using Root Mean Squared Error (RMSE) and R², with cross-validation also used to assess how consistently the models performed across different subsets of the data.
## Model Evaluation & Results
Model performance was compared using test-set RMSE and R², along with 5-fold cross-validation RMSE to evaluate consistency across different subsets of the data.
| Model | Test RMSE | Test R² | CV RMSE |
|---|---:|---:|---:|
| Linear Regression | 21.07 | 0.34 | **24.23** |
| Ridge Regression | 21.46 | 0.31 | 24.97 |
| Decision Tree | 22.20 | 0.27 | 28.99 |
| Random Forest | **20.28** | **0.39** | 25.91 |

Random Forest produced the strongest performance on the test set, with the lowest RMSE (20.28) and highest R² (0.39). However, Linear Regression produced the lowest cross-validation RMSE (24.23), suggesting more consistent performance across different subsets of the data.
Overall, the more complex models did not provide a substantial improvement over the simpler Linear Regression baseline. Random Forest may capture some nonlinear relationships in the data, while Linear Regression demonstrated stronger consistency during cross-validation.
Model interpretation also supported findings from the exploratory analysis. Population change emerged as the strongest feature associated with changes in affordability, followed by income change, while educational attainment showed a weaker relationship. The models explained some of the variation in affordability deterioration across the 100 metropolitan areas, but their relatively modest R² values suggest that additional economic and housing-market factors not included in this analysis also contribute to changes in affordability.

## Key Findings
Housing affordability across the top 100 U.S. metros examined has changed considerably over the last 15 years. Based on the affordability feature engineered for this project, "price-to-income ratio," which divides typical home values by median household income, we have found that on average, this ratio increased from approximately 3.39 in 2010 to 3.92 in 2015 and 4.69 in 2024. The data also showed that this increase varied widely across metros and regions. In fact, there were 2 metros, New Orleans, LA, and Baton Rouge, LA, that experienced an improvement in affordability. All other metros examined experienced a deterioration in affordability.

The top 10 metros with the greatest deterioration in affordability are spread across the country, and the percent increase in price-to-income ratio ranges from 82% to 123%. 3 of these top 10 metros are in California, 3 are in Florida, Las Vegas leads the pack, and Detroit, Boise City, and Phoenix complete this top 10 affordability deterioration list.

Our top 5 most unaffordable metros have a price-to-income ratio greater than 8. 4 of these 5 metros are in California, and the top 2 (San Francisco and Los Angeles) have a ratio greater than 10.

High home values do not necessarily equate to deterioration in affordability. For example, New York ranks 8th in highest home values, but also made the top 10 for most stable in terms of affordability, with only an 11.5% price-to-income ratio increase.

Population growth showed the strongest association with deterioration in affordability. However, this relationship was not one-to-one. Boise City was the only metro that made the top 10 in population growth as well as top 10 in affordability deterioration. All other metros that topped the list for population growth did not make the top 10 for affordability deterioration. This suggests that population growth may be an important factor, but other factors also contribute to affordability. On the flip side, the only metro with a population decline and improvement in affordability is New Orleans. These findings show association and do not establish causation.

Income was our second strongest factor associated with deterioration of affordability. Education showed a weaker relationship.

The modeling results were generally aligned with our initial EDA findings. Random Forest performed best on the test set, while Linear Regression performed better across Cross-Validation. Population, in both EDA and modeling, was shown to be the strongest predictor of change in price-to-income ratio, followed by income. Education was a less important factor in predicting the target. Overall, our models were able to explain some of the variation in housing affordability deterioration across our selected 100 metros, but the results also suggest that there are other important factors not explored in this project.
## Recommendations
For prospective homebuyers in the U.S., these findings can help to shape perspective when it comes to comparing home values across metros and/or embarking on the journey of selecting a city to plant roots. Home valuation alone, while extremely important, does not tell the whole story. It is important to explore how affordability has changed over time and understand the relationship between income and home values. Additionally, obtaining an understanding of population ebbs and flows in different metros may provide additional context when evaluating housing markets. While it is of utmost importance to choose to live in an area that is affordable, it can also be valuable to understand how affordability has changed over time. Depending on one's budget and income, high home valuations do not immediately indicate that a metro is unaffordable, just as current affordability does not necessarily indicate how affordability will change over time.

For local governments, housing organizations, developers, and community planners, the results suggest that population growth should be considered when evaluating future housing needs. Population growth showed the strongest association with deterioration in affordability in this analysis, although the relationship was not one-to-one. Rapidly growing metros may benefit from closer examination of whether housing availability is keeping pace with population growth, along with income trends and other local economic conditions.
## Limitations & Future Work

While this project explored factors most associated with housing affordability, I only explored the top 100 metropolitan areas in the U.S. based on Zillow's metro rankings. It is possible that the incorporation of additional metros would yield different results. I chose to use a select few variables from U.S. Census Bureau datasets, including Median Household Income, Population, and Educational Attainment, as these were the most interesting to me. It is possible and likely that selecting and utilizing additional or different variables would yield different results. Our analysis also only spanned the last 15 years, as 2010 was the oldest year used from the U.S. Census Bureau data. Finally, our models identified associations between variables and affordability, but did not establish causation of affordability changes. This would require a much more in-depth economic exploration.

In order to expand on this analysis and potentially improve predictions of housing affordability in the U.S., additional variables could be incorporated. Rather than gauging trends using only 2010, 2015, and 2024, a future analysis could also examine changes on a year-over-year basis. Additional variables that would be useful to explore include mortgage rates over time, employment and unemployment rates across metros, housing supply and new construction, property taxes, and local housing policies. With more detailed annual data, future modeling could also explore whether these historical trends can help predict which metros may experience greater affordability challenges in the next five years.
