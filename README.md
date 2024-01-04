# Performing multiple regression analysis to determine factors affecting price.
**Authors** Immaculate Mwendwa, Shalom Irungu, Stephen Kariuki, Stella Ndegwa, Muhsin Ahmed, Joan Wambu


## Column descriptions for King County Data Set

1. id - unique identified for a house
2. dateDate - house was sold
3. pricePrice - is prediction target
4. bedroomsNumber - of Bedrooms/House
5. bathroomsNumber - of bathrooms/bedrooms
6. sqft_livingsquare - footage of the home
7. sqft_lotsquare - footage of the lot
8. floorsTotal - floors (levels) in house
9. waterfront - House which has a view to a waterfront
10. view - Has been viewed
11. condition - How good the condition is ( Overall )
12. grade - overall grade given to the housing unit, based on King County grading system
13. sqft_above - square footage of house apart from basement
14. sqft_basement - square footage of the basement
15. yr_renovated - Year when house was renovated
16. zipcode - zip
17. yr_built - Built Year
18. lat - Latitude coordinate
19. long - Longitude coordinate
20. sqft_living15 - The square footage of interior housing living space for the nearest 15 neighbors
21. sqft_lot15 - The square footage of the land lots of the nearest 15 neighbors

## Business Problem.
A real estate agency in King County aims to provide valuable advice to homeowners on how specific home features will impact the estimated value of their homes. The primary objective is to help homeowners make informed decisions about which features could potentially yield the highest return on investment in terms of increased property value.

## Data ([kc_house_data.csv](./data/kc_house_data.csv))
We have been provided with The King County House Sales dataset which contains property sales between the years 2014 - 2015 and 21,420 records of houses sold. Each record in the data set gives features such as the number of bedrooms, the size of various rooms in square feet, about the individual homes.
 ### Objectives
1. Develop a model that will assist home buyers and home sellers in identifying attributes that influence the prices of houses.

2. Develop regression models that will guide the real estate agencies on pricing.

3. Determine features that have the biggest impact on the sale price of a house and by how much.

## Methods
We explore the data and clean it up. Thereafter, we visualize to have a better understanding of the data and create linear models, with price as our dependent variable, to gain a better insight of the variables that affect house price.

## Data Visualization to understand how various variables correlate with price.

![2024-01-04 (14)](https://github.com/shalomirungu/Group16_project_work/assets/149403427/550089b4-9be4-4160-97c5-68836651bfd4)
![2024-01-04 (4)](https://github.com/shalomirungu/Group16_project_work/assets/149403427/5f201944-e3d7-4c0f-a7d8-2017523d091c)
![2024-01-04 (5)](https://github.com/shalomirungu/Group16_project_work/assets/149403427/bbeca770-8634-4de6-801a-e2b1a46ada84)
![2024-01-04 (8)](https://github.com/shalomirungu/Group16_project_work/assets/149403427/9dd566ae-f3d8-4e1c-ab5d-5d47f745c1d7)
![2024-01-04 (9)](https://github.com/shalomirungu/Group16_project_work/assets/149403427/96278e95-c4d3-4ef8-b9bc-253f3f81e5f6)
![2024-01-04 (10)](https://github.com/shalomirungu/Group16_project_work/assets/149403427/5a526e6d-d30c-46af-b8e8-748daa0b16cc)
![2024-01-04 (11)](https://github.com/shalomirungu/Group16_project_work/assets/149403427/a6ae76ba-1f22-45c3-a3db-b35620f3c9b7)
![2024-01-04 (13)](https://github.com/shalomirungu/Group16_project_work/assets/149403427/bbc7ec61-85a2-49e0-82b0-d422d4a52435)

## Modelling
We create various regression models, starting with a simple linear regression model as our baseline, and then proceeding to multiple linear regression models.
 ###  Model 1a : sqft_living effect on price.
  #### Objective
  To investigate the effect  of sqft_living on the price
  #### Method
  Simple linear regression with price and sqft_living as dependent and independent variables respectively.
  #### Interpretation
 R-squared: The R-squared value is 0.493, indicating that approximately 49.3% of the variance in price can be explained by the sqft_living.

The model is statistically significant overall, with an F-statistic p-value well below 0.05 .The intercept is USD -4.399e+04 meaning that when all other variables are zero the estimated price is USD -4.399e+04 The coefficient is 280 meaning that for every unit increase in sqaure footage of sqft_living,the price increases by USD 280.8

The model violates the normality assumptions of linear regression and homoscedasticity.

 ### Model 1b: log transformation of the model above.
  #### Interpretation
The R-squared has slightly reduced but the the the normality and Homoscedasticity has improved as well.

### Model 2( First multiple regression model): bedrooms, bathrooms, sqft_living, sqft_lot, floors, waterfront, view, condition, grade, sqft_above, zipcode, lat, long, sqft_living15, year, Age_sold effect over price.
#### Objective
To investigate which variables affect price.
#### Method
Multiple linear regression modelling with all selected variables 

#### Interpretation
R-squared: The R-squared value is 0.772, indicating that approximately 77.2% of the variance in price can be explained by the 16 independent variables.

The model is statistically significant overall, with an F-statistic p-value well below 0.05 the intercept is -110.9581 meaning that when all other variables are zero the estimated price is -110.9581.

Statistical Significance: all the predictors are statistically significant with zero p-values. condition number: Cond. No.4.85e+08, this suggests there is high multicollinearity

 The model has a high R-squared of 0.772 showing that 77.2% of the variance in price is explained. However, there is non-normality in residuals and the condition number is high showing that there is high collinearity between the variables. Next, we do feature selection to enhance the model.
 

 ### Model 3: We remove the variables that have a low correlation with price and those that have high multicollinearity (price, view, condition, Age_sold, year, zip code, waterfront, lat, long, sqft_above, sqft_lot, sqft_lot15)
 #### Objective
 To identify the effect of the variables that have a high correlation with price and those that lack multicollinearity on price.
 #### Method
 Multiple linear regression modelling for bedrooms, bathrooms, sqft_living, floors, grade, sqft_living15

 #### Interpretation
 The model is statistically significant overall, with an F-statistic p-value well below 0.05

R-squared: The R-squared value is 0.560, indicating that approximately 56.0% of the variance in price can be explained by 'Bedrooms', 'Sqft_living', 'bathrooms',' floors', 'grade', 'sqft_living15'.

the intercept is 11.2452 meaning that when all other variables are zero the estimated log transformed price is 11.2452.

Bedrooms: For each unit increase in bedrooms, the log-transformed price is expected to decrease by 0.0185 units, holding other variables constant. More bedrooms are associated with a lower log-transformed price, all else being equal.

Bathrooms: The coefficient is not statistically significant.

sqft_living: For each unit increase in square footage of living space, the log-transformed price is expected to increase by 0.0002 units. This means Larger living spaces are associated with higher log-transformed prices.

Floors: The coefficient is not statistically significant.

Grade: For each additional grade point, the log-transformed price is expected to increase by 0.1722 units.

Sqft_living15: For each additional unit increase in square footage of living space in 2015, the log-transformed price is expected to increase by 0.00007114 units.

the R-squared of model2 has dropped compared to the previous model from 77% to 54.6%. However, the cond.no has reduced and the model has better linearity and normality after dealing with the multicollinearity

### Model 4: We use categorical variables and sqft_living to predict price. We use the One-hot encoding technique to convert categorical variables into a binary to see if we get better results.
#### Objective
To identify the effect of categorical variables and sqft_living on price.
#### Method
 Multiple linear regression modelling for categorical variables (waterfront, view, grade) and sqft_living on price.
 #### Interpretation

 The model is statistically significant overall, with an F-statistic p-value well below 0.05

R-squared: The R-squared value is 0.580, indicating that approximately 58% of the variance in price can be explained by 'sqft_living', 'waterfront', 'view_1','view_2, 'view_3', 'view_4', 'grade_4', 'grade_5', 'grade_6', 'grade_7', 'grade_8', 'grade_9'grade_10', 'grade_11', 'grade_12',grade_13'

the intercept is 11.2452 meaning that when all other variables are zero the estimated log transformed price is 11.2452 corresponding to a significant increase in price

sqft_living: For each unit increase in square footage of living space, the log-transformed price is expected to increase by 0.0002 units. Larger living spaces are associated with higher log-transformed prices.

waterfront_1: Having a waterfront view is associated with an increase of 0.3442 units in the log-transformed price, holding other variables constant.

view_1, view_2, view_3, view_4: Having better views (higher view categories) is associated with increases in log-transformed price: 0.1791, 0.2237, 0.2555, and 0.3670 units, respectively.

grade_4, grade_5, grade_6, grade_7, grade_8, grade_9, grade_10 are not statistically significant

grade_11: An increase in grade from 11 is associated with an increase of 0.7652 units in the log-transformed price, holding other variables constant. grade_12: An increase in grade from 12 is associated with an increase of 0.8580 units in the log-transformed price, holding other variables constant. grade_13: An increase in grade from 13 is associated with an increase of 0.9900 units in the log-transformed price, holding other variables constant.


we can see that our R-squared has increased to 0.580 this is a good indication of a good fit. the rmse is also lower than the previous model next we will try to look at a few features together with categorical variables to see if we can enhance our model


### Model 5: We use both categorical and numerical variables that have high correlation with price.
 #### Objective
 To identify the effect of categorical and numerical variables on price.
 #### Method
 Multiple linear regression modelling for categorical variables and numerical variables on price.
  #### Interpretation
 The model is statistically significant overall, with an F-statistic p-value well below 0.05

R-squared: The R-squared value is 0.590, indicating that approximately 59% of the variance in price can be explained by bedrooms,bathrooms,sqft_livn,view,condition,grade

The intercept is USD 10.8598, indicating that when all other variables are zero, the estimated log-transformed price is USD 10.8598.

bedrooms:

For each unit increase in the number of bedrooms, the log-transformed price is expected to decrease by USD 0.0163 units, holding other variables constant. More bedrooms are associated with a lower log-transformed price, all else being equal.

bathrooms:The coefficient is not statistically significant (p-value = 0.243).

sqft_living:For each unit increase in square footage of living space, the log-transformed price is expected to increase by USD 0.0002 units. Larger living spaces are associated with higher log-transformed prices. view:

For each unit increase in the view category, the log-transformed price is expected to increase by USD 0.1066 units. condition:

For each unit increase in the condition rating, the log-transformed price is expected to increase by USD 0.0954 units. grade:

For each unit increase in the grade rating, the log-transformed price is expected to increase by USD 0.1916 units.

## SUMMARY OF THE MODELS
Model 1a. with 1 predictor (sqft_living) R-squared:0.493

Model 1b. with 1 predictor (transformed price):R-squared:0.483

Model 2. with all predictors (all_features):R-squared:0.499

Model 3 with 6 predictors (handled multicollinearity and low correlation):R-squared: 0.560 * Adj. R-squared: 0.559*

Model 4 with 16 predictors (baseline and categorical variables):R-squared: 0.580 * Adj. R-squared: 0.580*

Model 5 with 6 predictors (more features and categorical data and features low p-values):R-squared: 0.590 and * Adj. R-squared: 0.589*

Model 1a (1 predictor - sqft_living): R-squared of 0.493 indicates that around 49.3% of the variance in the dependent variable is explained by sqft_living alone.

Model 1b (1 predictor - transformed price): R-squared of 0.483 indicates that around 48.3% of the variance in the log-transformed price is explained by the predictor.

Model 2 (all features): R-squared of 0.499 suggests that including all available predictors improves the explanation of variance compared to Model 1, but it's still relatively modest.

Model 3 (6 predictors - handled multicollinearity and low correlation): R-squared of 0.560 and Adj. R-squared of 0.559 indicate an improvement in explaining variance, and addressing multicollinearity and low correlation has positively impacted the model.

Model 4 (16 predictors - baseline and categorical variables): R-squared of 0.580 and Adj. R-squared of 0.580 indicate further improvement, especially with the inclusion of categorical variables.

Model 5 (6 predictors - more features, categorical data, and low p-values): R-squared of 0.590 and Adj. R-squared of 0.589 suggest the highest explanatory power among the mentioned models. The inclusion of more features, categorical data, and low p-values has contributed to the improved performance.

BEST MODEL Model 5, which includes more features, categorical data, and low p-values, is chosen as the best model due to its higher R-squared value (0.590) and adjusted R-squared value (0.589). This model strikes a balance between explanatory power and complexity.The RMSE of approximately 0.3374 suggests that, on average, the model's predictions deviate from the actual values by around 0.3374 log-transformed units. This gives an indication of the typical error in the model's predictions.

## Recommendations:
based on findings from our model5:

Consider the importance of bedrooms, sqft_living, view, condition, and grade when estimating or predicting housing prices.

Focus on upgrading property features to improve the overall grade. Communicate the potential financial returns associated with higher-grade properties.

Investigate the inconsistency in the impact of bathrooms on pricing. Collect additional data or refine the variable to better capture its significance.

Consider promoting properties with fewer bedrooms for buyers who prioritize cost-effectiveness. Highlight the advantages of smaller bedroom counts in terms of affordability.

Capitalize on properties with better views, incorporating visuals and descriptions that showcase the scenic surroundings to attract potential buyers.

Continuous efforts to improve the model can be made by exploring additional relevant features and refining existing ones.

## Conclusions:
Model Validity:

The model provides a substantial explanation of housing price variance. However, the impact of bathrooms needs further investigation to enhance the model's validity.

Property Features Influence Pricing:

Bedrooms, sqft_living, view, condition, and grade significantly influence housing prices. These features are essential considerations for buyers and sellers.

There are limitations to the model and we used log transformation to meet assupmtions of linearity

## NEXT STEPS:
gathering additional data on the homes as there may be key features missing.

methods other than regression could be used to meet assumptions


 




 
 
  
