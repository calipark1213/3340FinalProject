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

The techniques of regression analysis in this paper includes the following: 
1.	Least-squares estimation, hypothesis testing, and interval estimation for simple and multiple linear regression
2.	Maximum likelihood estimation and prediction of new observations
3.	Checking for model adequacy using residual analysis, detection and treatment of outliers, and tests for lack of fit
4.	Applying transformation to correct inadequate models
5.	Leverage and influence diagnostics
6.	Discussing potential multicollinearity
7.	Variable selection and Analysis of Variance 
8.	Robust Regression
 


## Data Description (must contain data visualizations that are properly labelled and explained)

## Methods (must contain a complete description of all analysis tools used)
We will be defining the consumption of fruit and vegetables as our two main predictor variables, x<sub>1</sub> and x<sub>2</sub> respectively, and fit a linear regression model to determine if it has an affect on obesity rates. Before we fit the model, we begin by normalizing the predictor variables by taking the mean and subtracting it from each point to allow easier interpretation and to reduce variability. 

## Results (all figures should be properly labelled and discussed)
We begin with scatterplots to get a general visualization of the data we are working with. 

#### Figure 1.1: Less than one fruit per day VS Rate of obesity (Normalized) <br/>
![Less than one fruit VS obesity (normalized)](https://user-images.githubusercontent.com/74206318/101521587-6dfcf180-395c-11eb-9a8d-54b98ff294a6.png) <br/>
**_y_ = 0.4582x<sub>1</sub> - 1.109E-15**  

#### Figure 1.2: Less than one vegetable per day VS Rate of obesity (Normalized) <br/>
![Less than one veggie VS obesity (normalized)](https://user-images.githubusercontent.com/74206318/101521588-6e958800-395c-11eb-92a4-12560392ba44.png) <br/>
**_y_ = 0.3904x<sub>2</sub> - 4.421E-17**  

Using the linear models, we estimate that a 1% increase in the rate of those who eat less than one fruit a day in a sample population leads to a 0.4582% increase in the rate of obesity.
Similarly, we can estimate that a 1% increase in the rate of those who eat less than one vegetale a day in a sample population leads to a 0.3904% increase in the rate of obesity.

From the scatterplots, we see that there appears to be a relationship between eating fruits or vegetables and obesity. Both models have a p-value less than 10<sup>-15</sup>. If we were to test an alternate hypothesis that β<sub>i</sub> ≠ 0, at α = 0.95 we can condlude that fruits and vegetables are (independently) closely related.  However, we will perform a more in depth analysis to better understand the relationships. 

When using a multiple lienar regression, we get the model _y_ = 0.318x<sub>1</sub> + 0.2311x<sub>2</sub>

## Conclusion (must contain a concise discussion of what has been learned from the analysis)
## Appendix (must include all data and R Markdown files for reproducibility)
We have filtered the CDC data set to better fit our research question. This included removing non-existent data points as well as irrelavant data columns. The remaining 6 columns can be found in the _data_prime.csv tab_.
After using the library dplyr on R to filter our irrelevant data points, we then exported the file to a csv and formatted our final _data_prime.csv_. To have better data to read visually, we have created columns for fruit/vegetable consumption and moved the corresponding cell value to the new columns. In addition, we have made  


## Rerefences
[1] Center for Disease Control and Prevention. (2020, September 17).  About Adult BMI. _cdc.gov_ https://www.cdc.gov/healthyweight/assessing/bmi/adult_bmi/index.html  <br/>
[2] Center for Disease Control and Prevention. (2020, October 29).  Healthy Food Environments. _cdc.gov_ https://www.cdc.gov/nutrition/healthy-food-environments/index.html
[3] Suzanne. (2018, March 23). CDC Data: Nutrition, Physical Activity, & Obesity. _kaggle.com_ https://www.kaggle.com/spittman1248/cdc-data-nutrition-physical-activity-obesity
[4] U.S. Department of Health and Human Services and U.S. Department of Agriculture. (December 2015). 2015–2020 Dietary Guidelines for Americans _8th Edition_. https://health.gov/our-work/food-nutrition/2015-2020-dietary-guidelines/guidelines/ <br/>

1.Perform least-squares estimation, hypothesis testing and interval estimation for simple linear regression models by hand and using R.
2.Perform least-squares estimation, hypothesis testing and interval estimation for multiple linear regression models using R.
3.Perform estimation by maximum likelihood and predict new observations using R.
4.Check model adequacy via residual analysis, detection and treatment of outliers and tests for lack of fit.
5.Employ transformations and weighting to correct model inadequacies. 
6.Explore diagnostics for leverage and influence.
7.Understand and be able to address multicollinearity.
8.Select variables and build models using computational techniques.
9.ANOVA.
10.Modern regression approaches. 


https://github.com/github/hub/issues/new?assignees=&labels=bug&template=bug_report.md&title=
https://web.stanford.edu/~kjytay/courses/stats32-aut2019/Session%208/Markdown%20Cheatsheet.pdf
**Bold** and _Italic_ and `Code` text


