# Final Project Math/Stat3340 
**Written by:** 
- Chris Freund _B00796285_
- Jacob Miller _B00795932_
- Seoyeon Cali Park _B00768397_

## Abstract
1.	Our objective is to perform a full regression analysis of using a subset of the CDC data set found on https://lionbridge.ai/datasets/10-open-datasets-for-linear-regression/ using the techniques covered in Math/Stat3340.<br/>
    i. Some of the data points in the CDC data set have been removed due to irrelevance and or insufficient size. <br/>
    ii. Data columns have been removed to better fit our research question. <br/>
    iii.  We have added a new data point to Alabama - this is to ensure that our data set is unique compared to others with the same data set. <br/>
    _Note: ii and iii will be discussed further in the Data Description section_ <br/>
2.	We would like to answer the following questions: Does the daily consumption of fruits and vegetables have an effect on the obesity rates? Is there a relationship between income and obesity?

## Introduction
This data analysis project uses techniques of regression analysis to determine what type of relationship exists between obesity rates, daily fruit and vegetable consumption, and income. We will only be looking at the proportion of people recorded in years 2011, 2013, and 2015 who eats fruits and vegetables less than once daily. Income is divided into 6 levels:

Table 1.1
| Income | Level |
|--------|-------|
| less than $15,000 | 1 |
| $15,000 -  $24,999 | 2 |
| $25,000 - $34,999 | 3 |
| $35,000 - $49,999 | 4 |
| $50,000 - $74,999 | 5 |
| $75,000 or greater per year  | 6 | 


We will be using the techniques we learned from Math/Stat3340, which includes performing simple/multiple linear regression, calculating maximum likelihood, residual analysis, analysis of variance, etc. These techniques will be discussed further in the methods section. 

## Data Description
Data years: 2011,2013,2015
Removed irrelevant columns, remaining columns include year,state,obesity percentage,fruit percentage,veg percentage,income,location,income2
year only includes 2011, 2013, 2015 since the rest of data did not have enough data points for our analysis.
Moved obesity, fruit, vegetable percentage to one column for every income level. 

## Methods
We will be defining the consumption of fruit and vegetables as our two main predictor variables and see how it affects the obesity rates.  First, we took the means of the predictor variables to normalize the data making it easier to interpret and reduce the variability.

## Results


## Conclusion
## Appendix
## Rerefences


1.Perform least-squares estimation, hypothesis testing and interval estimation for simple linear regression models by hand and using R.
2.Perform least-squares estimation, hypothesis testing and interval estimation for multiplelinear regression models using R.
3.Perform estimation by maximum likelihood and predict new observations using R.
4.Check model adequacy via residual analysis, detection and treatment of outliers and tests for lack of fit.
5.Employ transformations and weighting to correct model inadequacies. 
6.Explore diagnostics for leverage and influence.
7.Understand and be able to address multicollinearity.
8.Select variables and build models using computational techniques.
9.ANOVA.
10.Modern regression approaches. 



**Bold** and _Italic_ and `Code` text


