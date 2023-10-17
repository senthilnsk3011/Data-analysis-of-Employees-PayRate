# Introduction
People analytics, especially in Human Resource Management area, is important factors in talent Attraction, recruitment and retention. This revolutionising the way human resources departments operate, leading to higher efficiency and better results overall. Human resources has been using analytics for years. People analytics also can have used to check the current pay scale and pay slab for the current Job market. This analysis also can improve the employee experience and increase productivity by analysis the knowledge gap and taking steps to reduce it. It's also worth noting that you can get the following information using the same software: 1) Your personnel turnover rate; 2) The percentage of such turnover that results in a loss. 3) applicant satisfaction and experience during the recruitment process 4) On a scale of one to ten, which employees do you think will depart your company in the next year? Capacity analytics can also reveal whether your team has room to expand. Whether you do or not, you can utilise this information to improve your employee training and hiring tactics. This measure examines and deconstructs a number of leadership characteristics that reflect the calibre of your company's leaders. However, manual data collection, processing, and analysis have been the norm, and given the nature of human resource dynamics, this is no longer the case.  In this opportunity, we’re going to do predictive analytics and also interpreting its ML model.

# Objectives
We’re going to Investigate on what basis the employees are paid and check whether they are underpaid or overpaid. We highlight the hardworking and talented employees and their satisfaction. So the Management and Human Resource will be able to understand the sum of reason for Pay Gap between the employee’s. Reducing the Pay Gap also reduce the Churn rate, so the company needs analysis with accurate and interpretable methods.

# Result
It’s a common knowledge that the longer employee works in same company, the higher the salary. So we are doing feature Engineering by creating a column WorkingDays which have the Number Days working with company of an employee. We calculate this by subtracting Date of hire from the today is date. 

We will check whether the Pay rate is affected project Responsibility Count and the Number of Days Working with the Company. To interpret the output, we first need to determine the null and alternative hypotheses. 
 
H0 = there is no relationship between Pay Rate and project Responsibility Count and Number of Days Working with the Company 

H1 = There is a relationship between Pay Rate and project Responsibility Count and Number of Days Working with the Company.
 
We take the common alpha value of 5% (0.05) and compare it with the p-value we found. If the p-value is less than 0.05 then we can reject the null hypothesis. This is strong evidence that the null hypothesis is invalid. 
 
The hypothesis test done by using anova test as I am comparing the three numerical variables and not categorical variable. Figure 1 (a) shows the summary of the Anova test, from the summary we could see the p-value is less than the alpha value (0.05) so we can reject the null hypothesis. I am using Anova test to do the hypothesis test as I am comparing the three variable. Figure 1 (a) show the summary of the Anova test, from the summary we could see the P- value is less the alpha value (0.05) so we can reject the null hypothesis.

(a)
![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/5abb6975-9615-4744-af82-ffd943412a1c)

(b)
![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/be6d9452-da3f-4ea5-8cd8-f2f75312ee15)

Figure 1: (a) Anova test Summary of  (b) Correlation between the all numeric values

We use Visualization of a correlation matrix using ggcorr function to find the correlation between all the numeric values in the data set. From figure1 (b) we could see Pay Rate and Project Reasonability Count has highest correlation and Number of Days Working with the Company have significant correlation to the Pay Rate. From This we move further in our analysis and model building for predict the salary for employee.
We have lots have Missing Data, we can either remove the missing value or impute with some logical value about the data or Impute data set with random value. Using Aggregation plot function, we will be able to visualize number of missing values in each column. We can use either amelia or mice to impute the missing values. We have used amelia and we are only impute the numeric values. As we have already finished data wraggling  so we have given all the columns that doesn’t have missing values in idvars parameter which will avoid the columns.

![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/e964a9de-6348-4ac6-9c24-640fa328c49f)

Figure 2: Summary of Data Explore library

From Figure 2 we could see the almost all columns have zero missing values except of three columns which have 0.02% of missing values in the column. From figure 3 we can see how many of missing value are present in each column where used the Data Explore library to visualize the missing value through histogram plot of number of missing value in column.

While creating linear Model for the data set which has missing values, the observation with missing values get deleted. This is because the Regression ignores/delete the entire row if any single values is missing for the analysis. This is will affect the accuracy and may lead to biased output, hence it is necessary to impute the missing values. For imputation we use Amelia Library.  

![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/c12a0a1c-dd50-439c-9e81-3fb16e5ab6dd)

Figure 3: Aggregation plot for Missing Value

From the Figure 4 (a) we know Production department has the lowest average and median compared to other department, the median is not even a half of 4 highest payrate median. We know every department have different workload and there are always other factors that affect the salary. So we can’t directly say that there is an equality in payRate in different departments. We can get better insight if we analyse the payRate by each department. Pay Rate is plot against Project responsibility count by department wise using facet function. From this we could see clearly that IT/IS has more probability to get special project and production have lowest chase of getting Special Project.

(a)
![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/9099f7b0-7f60-44e4-9e26-a3d5ff74ba1c)

(b)
![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/8b8b1909-3bc5-4271-ab74-fb0fbf10b675)

Figure 4: (a) Aggregation Pay Rate by each department (b) Facet plot for PayRate and ProjectCount

![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/7ee18fd7-6db4-4fa8-8a0a-f2af148f7f73)

Figure 5: Box Plot for Outlie check

To Is there any extreme data or outlier among all numeric variables we box plot to check the outlier. From the figure 5 we know that age, DayAfterReview,SpecialProjectsCount and WorkingDay have some outlier.

# Data Imputation

We imputed the data set 20 times and we linear model is applied on all imputed data set. This is done by lapply function. We then extract the coefficient and standard error from each model and the extracted values should be given to mi.meld() to apply Rubins rule.

(a)
![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/c00bf1a5-de52-4159-9683-6ca5974ad74b)

(b)
![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/17da2fa4-eb9b-41fc-a083-59b4d5160814)

Table 1: (a) Coefficient of the 20 Imputations (b) Standard Error of the 20 Imputations

The pooled coefficients of SpecialProjectsCount and WorkingDay are 3.329837 and 0.00100714 respectively, which are both more than zero, as shown in Table 1 (a). This indicates that as the explanatory variables such as SpecialProjectsCount and WorkingDay grow, so does the Pay Rate for the imputations. In addition, the intercept's pooled coefficient is 25.04706. When the values of SpecialProjectsCount and WorkingDay are zero, the average value of Pay Rate is 25.04706 for the imputations.
The pooled standard errors of SpecialProjectsCount and WorkingDay are 0.1050733 and 0.000205951, respectively, as shown in Table 1 (b). The average distance between the fitted line to the datapoints of SpecialProjectsCount and WorkingDay is shown here.

After that we choose one impute data set based on the estimate and standard error of the model that has been trained on that data set. We have selected imputed data set 13 as it has low standard error and high estimate Intercept. From that we now check the low variance column and delete it. Low variance data is bad to our model because there is not much information the model can learn. Still Data set have lots of redundant information like Date of Birth and Date of Hire, we will delete those from data set.

We are doing Akaike information criterion (AIC) to compare the fit of several regression models. The AIC is intended to determine the model that explains the most variation in the data while punishing models with too many parameters. After you've fitted a few regression models, you may compare their AIC values. The the lower the AIC, better the model fit.

From the figure 6 we can see first model has the lowest AIC value and is thus the best fitting model

PayRate = β0 + β1(Count) + β2(Day) + β3(Age) 

![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/01a15b98-095f-4365-b94a-430a0627941d)

Figure 6: Summary of AIC

Now, we have to split the data into training data set and validation data set, to train and the model. We use the splitter function to slice the data set on 80% and make it as training data set. On validation data set we test our model to predict the Pay Rate.

Predicting Pay Rate using Decision Tree

Decision Tree is a Machine learning model that is used for regression and classification problems. We will use this model to predict the pay rate. We imported tidymodels library from which we use decision_tree function to build the model. The entire data set is split in 80% training data and test data set using split function. The model is trained on the training data set and testing using test data set.  The performance of the model can be predicted by calculating MSE (Mean Square Error) and RMSE (Root Mean Square Error). From the figure 7 we could see the RMSE have low standard error. We have also 

![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/1662c6f8-addb-48f7-afb3-7d8a37edc4a5)

Figure 7: Metric of Decision Tree Model


# Predicting Pay Rate with Random Forest

![image](https://github.com/senthilnsk3011/Working-with-data-MTHM501/assets/40666655/dea117bc-5419-49c1-9799-cda4b6487839)

Figure 8: Summary of Random Forest model

We use Random Forrest Regression to predict the Pay Rate using Special Project Count, Woking Days in Company, Age and Employee Satisfaction. Random forest is collection of many decision trees. Here Pay Rate is our Y and Special Project Count, Woking Days in Company, Age and Employee Satisfaction are our x1 ,x2, x3,x4. The performance of this model can be evaluated using the R-squared value, and this R-squared can be calculated using 1-SSR/SST where SSR is Sum of Squares Regression & SST is Sum of Squares Total. If the R-squared value is high, then the model is considered as a good model. From the Figure 8 we could see the R-square is 84% and number of trees that is used in the forest in 500. The model that has been trained on the training data set is used on validation data set using predict function to predict the PayRate. We can hyper tune the model to increase the accuracy of the model.


# Limitations
The data set have lots of low variance variable which will affect the accuracy and recall of the model and it have lots of reductant Information that also brings down the overall accuracy. Random forest Model can be hyper parameter tune to increase the accuracy and reduce the variance. Have lots Missing value which was handle by impute using amelia.


# Conclusions
From this analysis we can conclude that the Pay rate and Pay gap is based on the amount work they do through special project and Number of days working with company. We approached to this Conclusion by doing hypothesis testing using anova test. The Random forest model has simply over done the decision tree model which we can through the R-square of the Random Forest (0.84).
















