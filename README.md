## Performing multiple regression analysis to determine factors affecting price.
### Business Problem.
A real estate agency in King County aims to provide valuable advice to homeowners on how specific home features will impact the estimated value of their homes. The primary objective is to help homeowners make informed decisions about which features could potentially yield the highest return on investment in terms of increased property value.

### Data ([kc_house_data.csv](./data/kc_house_data.csv))
We have been provided with The King County House Sales dataset which contains property sales between the years 2014 - 2015 and 21,420 records of houses sold. Each record in the data set gives features such as the number of bedrooms, the size of various rooms in square feet, about the individual homes.
 #### Objectives
1. Develop a model that will assist home buyers and home sellers in identifying attributes that influence the prices of houses.

2. Develop regression models that will guide the real estate agencies on pricing.

3. Determine features that have the biggest impact on the sale price of a house and by how much.

### Methods
We explore the data and clean it up. Thereafter, we visualize to have a better understanding of the data and create linear models, with price as our dependent variable, to gain a better insight of the variables that affect house price.

### Modelling
We create various regression models, starting with a simple linear regression model as our baseline, and then proceeding to multiple linear regression models.
 ####  Model 1a : sqft_living effect on price.
  ##### Objective
  To investigate the effect  of sqft_living on the price
  ##### Method
  Simple linear regression with price and sqft_living as dependent and independent variables respectively.
  ##### Interpretation
  At an alpha of 0.05, the model is statistically significant. The model explains 45.5% of the variance in price. Both the intercept and the target variable p-values are less than alpha hence the coefficients are statistically significant. price = 6.723 + 0.8376 sqft_living. An increase of 1 sq foot in sqft_living will result in an increase in house price by 83.76%.

#### Model 2( First multiple regression model): bedrooms, bathrooms, sqft_living, sqft_lot, floors, waterfront, view, condition, grade, sqft_above, zipcode, lat, long, sqft_living15, year, Age_sold effect over price.
##### Objective
To investigate which variables affect price.
##### Method
Multiple linear regression modelling with all selected variables 

##### Interpretation
R-squared: The R-squared value is 0.772, indicating that approximately 77.2% of the variance in price can be explained by the 16 independent variables.

The model is statistically significant overall, with an F-statistic p-value well below 0.05 the intercept is -110.9581 meaning that when all other variables are zero the estimated price is -110.9581.

Statistical Significance: all the predictors are statistically significant with zero p-values. condition number: Cond. No.4.85e+08, this suggests there is high multicollinearity

 The model has a high R-squared of 0.772 showing that 77.2% of the variance in price is explained. However, there is non-normality in residuals and the condition number is high showing that there is high collinearity between the variables. Next, we do feature selection to enhance the model.
 

 #### Model 3: We remove the variables that have a low correlation with price and those that have high multicollinearity (price, view, condition, Age_sold, year, zip code, waterfront, lat, long, sqft_above, sqft_lot, sqft_lot15)
 ##### Objective
 To identify the effect of the variables that have a high correlation with price and those that lack multicollinearity on price.
 ##### Method
 Multiple linear regression modelling for bedrooms, bathrooms, sqft_living, floors, grade, sqft_living15

 ##### Interpretation
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

#### Model 4: We use categorical variables and sqft_living to predict price. We use the One-hot encoding technique to convert categorical variables into a binary to see if we get better results.
##### Objective
To identify the effect of categorical variables and sqft_living on price.
##### Method
 Multiple linear regression modelling for categorical variables (waterfront, view, grade) and sqft_living on price.
 ##### Interpretation

 The model is statistically significant overall, with an F-statistic p-value well below 0.05

R-squared: The R-squared value is 0.580, indicating that approximately 58% of the variance in price can be explained by 'sqft_living', 'waterfront', 'view_1','view_2, 'view_3', 'view_4', 'grade_4', 'grade_5', 'grade_6', 'grade_7', 'grade_8', 'grade_9'grade_10', 'grade_11', 'grade_12',grade_13'

the intercept is 11.2452 meaning that when all other variables are zero the estimated log transformed price is 11.2452 corresponding to a significant increase in price

sqft_living: For each unit increase in square footage of living space, the log-transformed price is expected to increase by 0.0002 units. Larger living spaces are associated with higher log-transformed prices.

waterfront_1: Having a waterfront view is associated with an increase of 0.3442 units in the log-transformed price, holding other variables constant.

view_1, view_2, view_3, view_4: Having better views (higher view categories) is associated with increases in log-transformed price: 0.1791, 0.2237, 0.2555, and 0.3670 units, respectively.

grade_4, grade_5, grade_6, grade_7, grade_8, grade_9, grade_10 are not statistically significant

grade_11: An increase in grade from 11 is associated with an increase of 0.7652 units in the log-transformed price, holding other variables constant. grade_12: An increase in grade from 12 is associated with an increase of 0.8580 units in the log-transformed price, holding other variables constant. grade_13: An increase in grade from 13 is associated with an increase of 0.9900 units in the log-transformed price, holding other variables constant.


we can see that our R-squared has increased to 0.580 this is a good indication of a good fit. the rmse is also lower than the previous model next we will try to look at a few features together with categorical variables to see if we can enhance our model


#### Model 5: We use both categorical and numerical variables that have high correlation with price.
 ##### Objective
 To identify the effect of categorical and numerical variables on price.
 ##### Method
 Multiple linear regression modelling for categorical variables and numerical variables on price.
  ##### Interpretation
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

 




 
 
  
