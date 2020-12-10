# Final Project Math/Stat3340 
**Written by:** 
- Chris Freund _B00796285_
- Jacob Miller _B00795932_
- Seoyeon Cali Park _B00768397_

## Abstract 
Body Mass Index (BMI) is a screening tool to determine the status of an individual's weight. One can calculate BMI by taking their weight in kilograms and dividing it by the squared height in meters. [1] This project attempts to perform a full regression analysis using the tools learned in Math/Stat3340 and determine if there exists a relationship between the percentage of adults aged 18 years and older who have obesity and percentage of less than one fruit/vegetable consumed daily. We have extracted our data from https://lionbridge.ai/datasets/10-open-datasets-for-linear-regression/ _CDC data: Nutrition, Physical Activity, Obesity_ [3] , and will be using a subset of the data points from this document. The interaction model of fruit and vegetable consumption had highest R-squared value. Our results suggest that there exists a relationship between fruit consumptions and obesity rates as well as vegetable rates and obesity rates. 

## Introduction
This data analysis project uses techniques of regression analysis to determine if there exists a type of relationship between obesity rates, daily fruit and vegetable consumption, and income. According to the Center for Disease Control and Prevention (CDC), being obese is categorized as having a BMI value of 30.0 and above. [1] Note that although BMI correlates with amount of body fat, the actual amount of body fat may differ for two individuals of the same weight due to other factors such as daily exercise. Eating fruits and vegetables from different groups also lower the risk of being obese. Fruits and vegetables can contribute to having a lower caloric intake which helps reducing the risk of weight gain. [4] This suggests that daily fruit and vegetable consumption is somehow related to an individual’s BMI level. 

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

## Data Description
Our original data published by the CDC is composed of different types of aggregated data relating to weight, diet, and exercise in the United States in 2011 to 1016. Data is given as a percentage of the sampled population that fit in the asked question. The following questions are answered throughout the dataset [3]:<br/>
•	Percent of adults aged 18 years and older who have obesity <br/>
•	Percent of adults aged 18 years and older who have an overweight classification <br/>
•	Percent of adults who report consuming fruit less than one time daily <br/>
•	Percent of adults who report consuming vegetables less than one time daily <br/>
•	Percent of adults who achieve at least 150 minutes a week of moderate-intensity aerobic physical activity or 75 minutes a week of vigorous-intensity aerobic activity (or an     equivalent combination) <br/>
•	Percent of adults who achieve at least 150 minutes a week of moderate-intensity aerobic physical activity or 75 minutes a week of vigorous-intensity aerobic physical activity   and engage in muscle-strengthening activities on 2 or more days a week <br/>
•	Percent of adults who achieve at least 300 minutes a week of moderate-intensity aerobic physical activity or 150 minutes a week of vigorous-intensity aerobic activity (or an     equivalent combination) <br/>
•	Percent of adults who engage in muscle-strengthening activities on 2 or more days a week <br/>
•	Percent of adults who engage in no leisure-time physical activity <br/>

The data is also presented in several different ways for every group sampled. It is grouped by gender, education, age, income, and race. There are also several columns of irrelevant identifications which are removed later on. 

We decided to work with the percentage of those who eat fruits less than once a day and the percentage of those who eat vegetables less than once a day as our predictor variables. Our response variable is the rate of obesity. To make sure there is no overlapping data, we took the income grouping from every section as our data of choice. It had six different ranges, allowing us to get a higher volume of data entries.

A new data entry was added to differentiate our dataset from other groups using the same one. First, it is important to note that there is always a gap in the total sample size for the income grouping due to people not answering questions about their income. In the 2012 Alabama data (for one particular city), there is a 1255 gap in sample size total compared to the sample size of those who answered about income. There is also no Asian demographic in this particular sample. We introduced our new data point by taking the 1255 gap and introducing the same amount of Asian people into the area. We pooled them into the $50,000 - $74,999 income range for simplicity.

To get the dataset to the optimal format for analysis, we began by removing any columns unrelated to our research. This including the aforementioned identification entries, and columns of the other groupings (age and gender for example). Then, every row with data irrelevant to our research question was removed (e.g., exercise data). Then, in Excel, we created two new rows for fruits and vegetables and matched the data for every sample size. This resulted in every row having a data value for obesity, fruit consumption, and vegetable consumption. Now, the data can be used to perform regression analysis. _3340_PrimeDataSetup.Rmd_ shows the steps on how we set our data upto this point. 

Figures 1.1a and 1.2a show scatterplots of our end result data. X axis for 1.1a is the percentage of individuals who consumed less than one fruit a day. The X axis for 1.2a is the percentage of individuals who consumed less than one vegetable per day. The Y axis for both represent the rates of obesity for each observation. The two scatterplots were added to visualize how our data is presented. However, the two sets of data will be combined for most of our analysis. 

#### Figure 1.1a: Less than one fruit per day VS Rate of obesity (n = 918) <br/>
![Less than one fruit VS obesity ](https://user-images.githubusercontent.com/74206318/101719054-ed7fe300-3a78-11eb-977b-a96ad0253088.png)

#### Figure 1.2a: Less than one vegetable per day VS Rate of obesity (n = 918) <br/>
![Less than one veggie VS obesity](https://user-images.githubusercontent.com/74206318/101719062-f07ad380-3a78-11eb-825c-9f6179616bbe.png)

## Methods
_Note that terminology and equations in this section are from the textbook [5]_ <br/>
We will be defining the consumption of fruit and vegetables as our two main predictor variables, x<sub>1</sub> and x<sub>2</sub> respectively (i.e. they will be our independent variables). The percentage of adults aged 18 years and older who have obesity will thus be our response variable (i.e. our dependent variable). This project strives to perform a full regression analysis, to determine if a relationship exists between our predictor variables and the response. Before we fit the model, we begin by normalizing the predictor variables, to allow easier interpretation and to reduce variability. The normalization is achieved by taking the mean, and subsequently subtracting it from each point. 

To begin, we started off with the `lm` command which will produce two simple linear models between obesity rates (y), and the number of people who consume less than one fruit per day (x<sub>1</sub>) and less than on vegetable a day (x<sub>2</sub>).  Simple linear regression fits a straight line to our data, which we can use to determine the relationship between our predictor and response variable. The model is in the form y=B<sub>0</sub>  + B<sub>1</sub>x + error, where the e ~ N(0,σ<sup>2</sup>). In our case, we will be looking at two simple linear models; _y~x<sub>1</sub>_ and _y~x<sub>2</sub>_. Calculating the intercept and the slope (β<sub>0</sub> and β<sub>1</sub>) uses calculus to take the partial derivative of S with respect to β<sub>0</sub> and β<sub>1</sub> and can be solved for both by setting the partial derivatives equal to 0.  The intercept is the value of y when x=0, and the slope is the change in y as x increases by 1 unit. The `lm` command will provide the model’s coefficient for us, and we can obtain an in-depth statistical summary using `summary(lm)`. 

Next, we examine multiple linear regression using our dataset. Again, we will use R’s `lm` command, but this time, we will set our syntax to y~x<sub>1</sub>+x<sub>2</sub>. The basic form of multiple linear regression is y=β<sub>0</sub>+β<sub>1</sub>x<sub>1</sub>+β<sub>2</sub>x<sub>2</sub>+…+β<sub>n</sub>x<sub>n</sub>. Similar to simple linear regression, we can look at the statistical summary using the `summary` command, and draw conclusions. The least squares estimate for this model was also tested with a y-hat matrix by transforming our data into matrices. Since we have multiple variables in the equation, we can also see if there is any interaction between these variables by multiplying two or more of them together. This will add a third variable called the interaction (x<sub>1</sub>x<sub>2</sub>) for instance. The change in the multiple _R<sup>2</sup>_ value is very small using this model, so the gerneal multiple linear model is used instead.

To draw conclusions on the data, it is important that we perform hypothesis testing. Questions like “Is there an interaction between these two variables?” “Does this model best fit the data?” can be answered by performing hypothesis testing. Here are the steps to perform hypothesis testing: <br/>
1.	State the null and alternative hypotheses of interest <br/>
2.	Assuming the null hypothesis is true, the next step is to calculate the test statistic (t, z or F depending on how many degrees of freedom there are). <br/>
3.	Determine the p-value <br/>
4.	State conclusion (reject or support the null hypothesis) <br/>
Typically, in regression, we test the significance of the intercept and the slope to determine if there exists a relationship. This is done by setting H<sub>0</sub>=β<sub>i</sub> = 0 and H<sub>a</sub>= β<sub>i</sub> ≠ 0, at α = 0.95

It is also important that we check the model’s adequacy by detecting outliers within the data. This is accomplished by plotting the residuals in R and scatterplots and see the deviation between the data and line of best fit. We can then also measure the variability in the response variables. We have the following residual plots in our obesity data: <br/>
1.	The Normal Probability Plot <br/>
2.	Residuals vs leverage <br/>
3.	Residuals vs fitted values <br/>

This will all help us interpret a line of best fit, and see how far off the data is deviated from the line of best fit. <br/>

In some cases, if the variability becomes too high, and there does not appear to be a linear relationship, we can use a method called variance stabilizing. We essentially transform the model into a different relationship of the data. The most common types are ln(y), and √y. We do not need to do this in our case because if you observe figures 1.1a and 1.2a, the data follows a linear pattern (with only a couple outliers, however, not sufficient to raise concerns) and there is no need to transform the data. 

In combination with the residual techniques, we can use the hat matrix (H) to help us identify any observations that are influential. Larger residuals that exist among the data are most likely going to be influential. We can identify these through the diagonals of the hat matrix (H). Now we must test for any signs of multicollinearity by calculating the variance inflation factor. This is accomplished through R’s built-in `car` library. This enables us to use the `VIF` command to compute the variance inflation factor. Large variance inflation factors ≥ 10 raises concerns of multicollinearity. Fortunately for us, our VIF value was 1.436569 so there is no evidence of multicollinearity in our data.


## Results
We begin with scatterplots to get a general visualization of the data we are working with. 

#### Figure 1.1b: Less than one fruit per day VS Rate of obesity (Normalized) 
![Less than one fruit VS obesity (normalized)](https://user-images.githubusercontent.com/74206318/101662054-65212400-3a1f-11eb-95ae-ffc1606bf1cb.png) <br/>
**_y_ = 0.4582x<sub>1</sub> - 1.109E-15**  

#### Figure 1.2b: Less than one vegetable per day VS Rate of obesity (Normalized) 
![Less than one veggie VS obesity (normalized)](https://user-images.githubusercontent.com/74206318/101662056-65b9ba80-3a1f-11eb-99a6-7d45f7dbe864.png) <br/>
**_y_ = 0.3904x<sub>2</sub> - 4.421E-17**  

Using the linear models, we estimate that a 1% increase in the rate of those who eat less than one fruit a day in a sample population leads to a 0.4582% increase in the rate of obesity. Similarly, we can estimate that a 1% increase in the rate of those who eat less than one vegetable a day leads to a 0.3904% increase in the rate of obesity.

For finding the actual estimated obesity rate, simply take _y_ and add the mean, 30.08.

From the scatterplots, we see that there appears to be a relationship between eating fruits or vegetables and obesity. Both models have a p-value less than 10<sup>-15</sup>. If we were to test an alternate hypothesis that β<sub>i</sub> ≠ 0, at α = 0.95 we can reject a null hypothesis that β<sub>i</sub> = 0 and conclude that fruit and vegetable consumption are (independently and separately) closely related to obesity. However, we will perform a more in-depth analysis to better understand the relationships.

When performing multiple linear regression, we get the model _y_ = 0.318x<sub>1</sub> + 0.2311x<sub>2</sub> - 6.783E-16. This also produced a multiple _R<sup>2</sup>_ value of 0.4983, the strongest correlation yet. Similar to the simple linear regressions, if we test an alternate hypothesis that not all β<sub>i</sub> = 0, we can reject the null hypothesis of β<sub>1</sub> = β<sub>2</sub> = 0 at α = 0.95 because our p-value is near zero as determined from the linear regression. 

Considering that our multiple linear model is the most important for further analysis, and has the largest _R<sup>2</sup>_, we double checked the model by transforming our data into matricies and performing least squares estimations, which resulted in the following matrix:

#### Table 1.2 - Least Squares Estimation Matrix
| Coefficient | Value |
|---|---|
| β<sub>0</sub> | ~ 0 |
| β<sub>1</sub> | 0.3180 |
| β<sub>2</sub> | 0.2311 |

We verify that we can achieve the same values when calculating the linear model.

Another important question to ask is, does the multiple linear model predict new data accurately? We tested this idea using prediction intervals by looking at a potential sample where no individuals in the sample get their daily intake of fruits and vegetables. Because we are fitting a linear model, we must make a few assumptions. [5] <br/>
1. The relationship between the predictors and the response is linear. <br/>
2. The error term has zero mean and constant variance. <br/>
3. The error term has constant variance. (No signs of homoskedasticity) <br/>
4. Errors are independent, uncorrelated, and normally distributed. <br/> 

We demonstrate that these assumptions are met using residual analysis. This also plays a key role in determine the strength of our model. We have plotted the residuals using the type "R-Student Residuals". Studentized residuals are computed by deleting each observation one at a time, and each time refitting the model on the observations that are left. (n-1) The standardized format of the comparison between the observed and fitted values based on the model with n-1 observations will produce studentized residuals. <br/>
 
#### Figure 1.3: Residuals vs Fitted Plot 
![Residuals VS Fitted mlr](https://user-images.githubusercontent.com/74206318/101710271-84dc3a80-3a67-11eb-9a1c-775dae92ee8a.png)

#### Figure 1.4: Normal Q-Q Plot 
![Normal Q-Q mlr](https://user-images.githubusercontent.com/74206318/101710277-860d6780-3a67-11eb-8373-d11434163b02.png)

#### Figure 1.5: Residuals vs Leverage Plot 
![Residuals VS Leverage mlr](https://user-images.githubusercontent.com/74206318/101710280-873e9480-3a67-11eb-8dd1-5a6d7c20903e.png)

#### Figure 1.6: Scale-Location Plot 
![Scale-Location mlr](https://user-images.githubusercontent.com/74206318/101710283-886fc180-3a67-11eb-8255-d30f137a7e11.png)

Looking at figure 1.3, the plot suggests a slight evidence of a non-linear relationship. Next, looking at figure 1.4, all the residuals seem to follow a straight line well. There are 3 data points that are outliers which are 162, 202, and 205 but they seem to follow the general trend well enough to be disregarded. When looking at the figure 1.5, the residuals seem to be randomly spread apart. Again there are the same outliers but they still follow the general trend well enough to be disregarded. The last plot to analyze is shown in figure 1.6. Many data points appear to follow the cook's distance lines, however, some do not, such as observations 197, 269 and 700. Removing entries 162, 202, 205 or 197, 269, 700 (or both sets) only affect _R<sup>2</sup>_ up to 0.01, giving an _R<sup>2</sup>_ value of 0.5082. 

#### Table 1.5 Variance Inflation Factor Output (Multiple Linear Regression) <br/>
`predict(lm1.2)` output <br/>
|| Test stat | Pr> \|Test stat\| |
|--------|-------|------|
| x<sub>1</sub> | -0.4044 |  0.6860444 |
| x<sub>2</sub> | -1.1900 | 0.2343431 |
| Tukey test | -3.5719 | 0.0003545 |

| x<sub>1</sub> | x<sub>2</sub> |
|--------|-------|
| 1.436569 | 1.436569 |

To determine if multicollinearity is present in our data, we used the car library to find our variance inflation factors (VIF). This is important since a high VIF value means that there is evidence of multicollinearity in our data. Fortunately for our dataset, our VIF value is 1.436569, which shows weak evidence of multicollinearity between the predictor variables in this case. That is, it appears that hardly any variance inflation exists in our data. 

Since we have assesed the model and determined that the residuals follow the model assumptions, we do not need to perform transformations and weighting to correct model inadequacies. We verify that our coefficients are stable, and its signs and magnitudes are also reasonable. There is no concernes of multicollinearity, and the predicted responses are within the range of those observed. This all concludes that we had a good experimental design, since our regression coefficients are almost uncorrelated, and the regressor variables are not being missed and are within the appropriate range. We can ignore the few observations that are outliers since they seem to have an insignificant effect in our data. 

Now that we have made sure that these conditions are met, we can now make a prediction. The `predict` command in R was used to get: <br/>
#### Table 1.3 - 95% Prediction Interval
|| fit | lwr | upr |
|-----|-----|-----|-----|
| 1 | 36.4907 | 29.20862 | 43.77278 |

Using the best fit shows that this population would be 36.4907% above the mean obesity, so an estimated 66.57% of all individuals in this sample would be obese. The upper bound of this interval was 73.85%. Comparing this interval back to our original data, it appears to predict the sample well. However, in the real life setting, it may be difficult to find a sample where all the individuals would not eat their fruits and vegetables.  No prediction goes over 100%.

To ensure the prediction interval stays within a realistic range, we also tested for a sample population where everyone has at least a fruit and vegetable daily.
#### Table 1.4 - 95% Prediction Interval
|| fit | lwr | upr |
|-----|-----|-----|-----|
| 1 | -18.41853 | -25.41487 | -11.4222 |

Using the obesity mean 30.08%, we determine that this healthy population is no more than 18.66% obese but no less than 4.67%. Therefore, by testing prediciton interval bounds, we can say our multiple linear regression model is accurate and realistic.

Lastly, we performed another regression technique called robust statistical analysis on all the variables (fruits, vegetables, and the interaction of the two) to also test if there are any major outliers or unequal variance in the data. If you look at the coefficients of the slope in both the original linear model and the robust linear model, they are essentially the same value. The intercepts appear to be off but that is a result of normalizing the data by subtracting the mean from their values. Based on the results of the robust statistics, it is fair to say that there are no significant outliers in our dataset that could cause false observations. However, the β coefficients do increase when using a Robust lienar model, so one could assume that there are some more obesity samples that are minorly influencing the data, hence the slight increase in slope.

#### Table 1.6 - Linear and Robust Coefficients
| Model | Intercept | x<sub>1</sub> | x<sub>2</sub> |
|-----|-----|-----|-----|
| y ~ x<sub>1</sub> lm | ~ 0 | 0.4582 | |
| y ~ x<sub>1</sub> rlm | -0.0057 | 0.4852 | |
| y ~ x<sub>2</sub> lm | ~ 0 | | 0.3904 |
| y ~ x<sub>2</sub> rlm | 0.0412 | | 0.4021 |
| y ~ x<sub>1</sub> + x<sub>2</sub> lm | ~0 | 0.3180 | 0.2311 |
| y ~ x<sub>1</sub> + x<sub>2</sub> rlm | 0.0878 | 0.3195 | 0.2381 |


## Conclusion (must contain a concise discussion of what has been learned from the analysis)

## Appendix
***ALL FILES ARE FOUND AT TOP OF GITHUB PAGE*** </br>
3340_PrimeDataSetup.Rmd - R code used to format the original dataset </br>
3340_analysis.html - HTML copy of our alaysis Rmd </br>
3340_analysis.rmd - R code used for results </br>
README.md - Primary document containing details about our project </br>
data_prime.csv - Dataset formatted using PrimeDataSetup and some Excel work </br>

## Rerefences
[1] Center for Disease Control and Prevention. (2020, September 17).  About Adult BMI. _cdc.gov_ https://www.cdc.gov/healthyweight/assessing/bmi/adult_bmi/index.html  <br/>
[2] Center for Disease Control and Prevention. (2020, October 29).  Healthy Food Environments. _cdc.gov_ https://www.cdc.gov/nutrition/healthy-food-environments/index.html  <br/>
[3] Suzanne. (2018, March 23). CDC Data: Nutrition, Physical Activity, & Obesity. _kaggle.com_ https://www.kaggle.com/spittman1248/cdc-data-nutrition-physical-activity-obesity  <br/>
[4] U.S. Department of Health and Human Services and U.S. Department of Agriculture. (December 2015). 2015–2020 Dietary Guidelines for Americans _8th Edition_. https://health.gov/our-work/food-nutrition/2015-2020-dietary-guidelines/guidelines/ <br/>
[5] Montgomery, D., Peck, E., &amp; Vining, G. (2012). Introduction to Linear Regression Analysis, 5th Edition. John Wiley & Sons.



https://github.com/github/hub/issues/new?assignees=&labels=bug&template=bug_report.md&title=
https://web.stanford.edu/~kjytay/courses/stats32-aut2019/Session%208/Markdown%20Cheatsheet.pdf


