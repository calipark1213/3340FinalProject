# Final Project Math/Stat3340 
**Written by:** 
- Chris Freund _B00796285_
- Jacob Miller _B00795932_
- Seoyeon Cali Park _B00768397_

## Abstract 
Body Mass Index (BMI) is a screening tool to determine the status of an individual's weight. One can calculate BMI by taking their weight in kilograms and dividing it by the squared height in meters. [1] This project attempts to perform a full regression analysis using the tools learned in Math/Stat3340 and determine if there exists a relationship between the percentage of adults aged 18 years and older who have obesity and percentage of less than one fruit/vegetable consumed daily. We have extracted our data from https://lionbridge.ai/datasets/10-open-datasets-for-linear-regression/ _CDC data: Nutrition, Physical Activity, Obesity_ [3] , and will be using a subset of the data points from this document. The interaction model of fruit and vegetable consumption had highest R-squared value. Our results suggest that there exists a relationship between fruit consumptions and obesity rates as well as vegetable rates and obesity rates. 

## Introduction (must contain a thorough description of the questions of interest)
This data analysis project uses techniques of regression analysis to determine if there exists a type of relationship between obesity rates, daily fruit and vegetable consumption, and income. According to the Center for Disease Control and Prevention (CDC), being obese is categorized as having a BMI value of 30.0 and above. [1] Note that although BMI correlates with amount of body fat, the actual amount of body fat may differ for two individuals of the same weight due to other factors such as daily exercise. Eating fruits and vegetables from different groups also lower the risk of being obese. Fruits and vegetables can contribute to having a lower caloric intake which helps reducing the risk of weight gain. [4] This suggests that daily fruit and vegetable consumption is somehow related to an individual’s BMI level. <br/>
Here we strive to answer the following question using regression analysis: Is there a relationship between the percentage of adults aged 18 years and older who have obesity and percentage of less than one fruit/vegetable consumed daily? Although how the original data gathered is unknown, we have filtered the data set to fit our research question. This included removing non-existent data points as well as irrelevant data columns. The data set we will be working with can be found under the _data_prime.csv_ tab. This only be looking at the proportion of people recorded in years 2011, 2013, and 2015 who eats fruits and vegetables less than once daily. We will be setting the percentage of obesity rates as our response variables, and fruit/vegetable consumption as our predictor variable. In addition, to make the analysis more proficient, the income column was categorized into 6 levels: <br/>
#### Table 1.1
| Income | Level |
|--------|-------|
| less than $15,000 | 1 |
| $15,000 -  $24,999 | 2 |
| $25,000 - $34,999 | 3 |
| $35,000 - $49,999 | 4 |
| $50,000 - $74,999 | 5 |
| $75,000 or greater per year  | 6 |  

The techniques of regression analysis in this paper includes the following _(Found in Math/Stat3340 Syllabus)_: <br/>
1. Perform least-squares estimation, hypothesis testing and interval estimation for simple linear regression models by hand and using R. <br/>
2. Perform least-squares estimation, hypothesis testing and interval estimation for multiple linear regression models using R. <br/>
3. Perform estimation by maximum likelihood and predict new observations using R. <br/>
4. Check model adequacy via residual analysis, detection and treatment of outliers and tests for lack of fit. <br/>
5. Employ transformations and weighting to correct model inadequacies. <br/>
6. Explore diagnostics for leverage and influence. <br/>
7. Understand and be able to address multicollinearity. <br/>
8. Select variables and build models using computational techniques. <br/>
9. ANOVA. <br/>
10. Modern regression approaches. <br/>
 


## Data Description (must contain data visualizations that are properly labelled and explained)

## Methods (must contain a complete description of all analysis tools used)
We will be defining the consumption of fruit and vegetables as our two main predictor variables, x<sub>1</sub> and x<sub>2</sub> respectively, and fit a linear regression model to determine if it has an affect on obesity rates. Before we fit the model, we begin by normalizing the predictor variables by taking the mean and subtracting it from each point to allow easier interpretation and to reduce variability. 

## Results (all figures should be properly labelled and discussed)
We begin with scatterplots to get a general visualization of the data we are working with. 

#### Figure 1.1: Less than one fruit per day VS Rate of obesity (Normalized) <br/>
![Less than one fruit VS obesity (normalized)](https://user-images.githubusercontent.com/74206318/101662054-65212400-3a1f-11eb-95ae-ffc1606bf1cb.png) <br/>
**_y_ = 0.4582x<sub>1</sub> - 1.109E-15**  

#### Figure 1.2: Less than one vegetable per day VS Rate of obesity (Normalized) <br/>
![Less than one veggie VS obesity (normalized)](https://user-images.githubusercontent.com/74206318/101662056-65b9ba80-3a1f-11eb-99a6-7d45f7dbe864.png) <br/>
**_y_ = 0.3904x<sub>2</sub> - 4.421E-17**  

Using the linear models, we estimate that a 1% increase in the rate of those who eat less than one fruit a day in a sample population leads to a 0.4582% increase in the rate of obesity. Similarly, we can estimate that a 1% increase in the rate of those who eat less than one vegetable a day in a sample population leads to a 0.3904% increase in the rate of obesity.

For finding the actual estimated obesity rate, simply take _y_ and add the mean, 30.08.

From the scatterplots, we see that there appears to be a relationship between eating fruits or vegetables and obesity. Both models have a p-value less than 10<sup>-15</sup>. If we were to test an alternate hypothesis that β<sub>i</sub> ≠ 0, at α = 0.95 we can reject a null hypothesis that β<sub>i</sub> = 0 and conclude that fruit and vegetable consumption are (independently and separately) closely related to obesity. However, we will perform a more in-depth analysis to better understand the relationships.

When performing multiple linear regression, we get the model _y_ = 0.318x<sub>1</sub> + 0.2311x<sub>2</sub> - 6.783E-16. This also produced a multiple _R<sup>2</sup>_ value of 0.4983, the strongest correlation yet. Similar to the simple linear regressions, if we test an alternate hypothesis that not all β<sub>i</sub> = 0, we can reject the null hypothesis of β<sub>1</sub> = β<sub>2</sub> = 0 at α = 0.95 because our p-value is near zero as determined from the linear regression. 

Another important question to ask is, does the multiple linear model predict new data accurately? We tested this idea using prediction intervals by looking at a potential sample where no individuals in the sample get their daily intake of fruits and vegetables. The `predict` command in R was used to get: <br/>
#### Table 1.2 - 95% Prediction Interval
|| fit | lwr | upr |
|-----|-----|-----|-----|
| 1 | 36.4907 | 29.20862 | 43.77278 |

Calculating the least squares estimate showed that this population would be 36.4907% above the mean obesity, so an estimated 66.57% of all individuals in this sample would be obese. The upper bound of this interval was 73.85%. Comparing this interval back to our original data, it appears to predict the sample well. However, in the real life setting, it may be difficult to find a sample where all the individuals would not eat their fruits and vegetables.  No prediction goes over 100%.

To ensure the prediction interval stays within a realistic range, we also tested for a sample population where everyone has at least a fruit and vegetable daily.
#### Table 1.3 - 95% Prediction Interval
|| fit | lwr | upr |
|-----|-----|-----|-----|
| 1 | -18.41853 | -25.41487 | -11.4222 |

Using the obesity mean 30.08%, we determine that this healthy population is no more than 18.66% obese but no less than 4.67%. Therefore, by testing prediciton interval bounds, we can say our multiple linear regression model is accurate and realistic.

Residual analysis also plays a key role in determine the strength of our model.
#### Figure 1.3: Residuals vs Fitted Plot <br/>
![Residuals vs Fitted Plot](https://user-images.githubusercontent.com/74836346/101684987-99a3d880-3a3d-11eb-8b4c-c6b187f08365.png) <br/>

#### Figure 1.4: Normal Q-Q Plot <br/>
![Normal Q-Q Plot](https://user-images.githubusercontent.com/74836346/101686427-6cf0c080-3a3f-11eb-9a7b-90e821b9db3e.png) <br/>

#### Figure 1.5: Residuals vs Leverage Plot <br/>
![Residuals vs Leverage Plot](https://user-images.githubusercontent.com/74836346/101686830-f7392480-3a3f-11eb-9878-c4ecabf3d61d.png) <br/>



Looking at the residuals VS fitted plot of lm(1.2), there is a slight evidence of a non-linear relationship. Next, looking at the normal Q-Q plot, all the residuals seem to follow a straight line well. There are 3 data points that are outliers which are 162, 202, and 205 but they seem to follow the general trend well enough to be disregarded. When looking at the Scale-Location plot, the residuals seem to be randomly spread apart. Again there are the same outliers but they still follow the general trend well enough to be disregarded. The last plot to analyze is the Residuals vs Leverage plot. Many data points appear to follow the cook's distance lines, however, some do not, such as observations 197, 269 and 700. Removing entries 162, 202, 205 or 197, 269, 700 only affect _R<sup>2</sup>_ up to 0.01.



We performed a robust statistical analysis on all the variables (fruits, vegetables, and the interaction of the two) to also test if there are any major outliers or unequal variance in the data. If you look at the coefficients of the slope in both the original linear model and the robust linear model, they are essentially the same value. The intercepts appear to be off but that is a result of normalizing the data by subtracting the mean from their values. Based on the results of the robust statistics, it is fair to say that there are no significant outliers in our dataset that could cause false observations.
#### Table 1.x - Linear and Robust Coefficients
| Model | Intercept | x<sub>1</sub> | x<sub>2</sub> |
|-----|-----|-----|-----|-----|
| y ~ x<sub>1</sub> lm| ~0 | 0.6412 ||
| y ~ x<sub>1</sub> rlm | -0.0012 | 0.6789 ||
| y ~ x<sub>2</sub> lm | ~0 || 0.6013 |
| y ~ x<sub>2</sub> rlm | -0.0083 || 0.6194 |
| y ~ x<sub>1</sub> + x<sub>2</sub> lm | ~0 | 0.4449 | 0.3560 |
| y ~ x<sub>1</sub> + x<sub>2</sub> rlm | 0.0178 | 0.4471 | 0.3667 |


## Conclusion (must contain a concise discussion of what has been learned from the analysis)
## Appendix (must include all data and R Markdown files for reproducibility)
We have filtered the CDC data set to better fit our research question. This included removing non-existent data points as well as irrelavant data columns. The remaining 6 columns can be found in the _data_prime.csv tab_.
After using the library dplyr on R to filter our irrelevant data points, we then exported the file to a csv and formatted our final _data_prime.csv_. To have better data to read visually, we have created columns for fruit/vegetable consumption and moved the corresponding cell value to the new columns. In addition, we have made  **???????**


## Rerefences
[1] Center for Disease Control and Prevention. (2020, September 17).  About Adult BMI. _cdc.gov_ https://www.cdc.gov/healthyweight/assessing/bmi/adult_bmi/index.html  <br/>
[2] Center for Disease Control and Prevention. (2020, October 29).  Healthy Food Environments. _cdc.gov_ https://www.cdc.gov/nutrition/healthy-food-environments/index.html  <br/>
[3] Suzanne. (2018, March 23). CDC Data: Nutrition, Physical Activity, & Obesity. _kaggle.com_ https://www.kaggle.com/spittman1248/cdc-data-nutrition-physical-activity-obesity  <br/>
[4] U.S. Department of Health and Human Services and U.S. Department of Agriculture. (December 2015). 2015–2020 Dietary Guidelines for Americans _8th Edition_. https://health.gov/our-work/food-nutrition/2015-2020-dietary-guidelines/guidelines/ <br/>

 


https://github.com/github/hub/issues/new?assignees=&labels=bug&template=bug_report.md&title=
https://web.stanford.edu/~kjytay/courses/stats32-aut2019/Session%208/Markdown%20Cheatsheet.pdf
**Bold** and _Italic_ and `Code` text


