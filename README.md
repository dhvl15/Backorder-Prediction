# Backorder Prediction in R

In supply chain systems, backorders can negatively impact effectiveness at service levels. Identifying parts with the highest chances of shortage prior its occurrence can present a high opportunity to improve an overall company’s performance.

## What is backorder?
A backorder is a purchase order for a good or service that cannot be fulfilled right away owing to a shortage of stock. Although the product might not be in the company's current inventory, it might still be in production, or the company might need to continue producing more of the item. Backorders are a sign that a company's product is in higher demand than it can meet. The company's backlog is another name for them.

<!--1.2 Backorder Graphical Visualisation:-->

## What causes backorders?
Backorders occur for a variety of reasons — some of which are preventable and others that are simply out of your control. 
* Unusual demand
* Low safety stock
* Manufacturer or supplier problem
* Human error
* Inventory and warehouse management discrepancies
* Long lead time 

## Dataset
Source of Data: The data comes from Kaggle’s dataset:  “Predict Product Backorders”.
https://www.kaggle.com/competitions/untadta/data
The dataset contains 1,048,576 rows (data points) and 23 columns (features). The target variable (or response) is the went_on_backorder variable. Each row represents an individual product and each column represents a feature such as:

## Data Preparation

There are 7 factor variables and 16 continuous variables present in the dataset.
The Correlation matrix shows a positive linear correlation between most of the continuous variables. 
It is observed that sales, forecast, min_bank, national_inv and lead_time have a strong positive correlation and can be used for prediction.








<!-- Some EDA on primary data-set:
1 -  Visualization of Sales V/s Forecasted Sales for X months







2-Forecasted Sales v/s Minimum recommended amount in stock of X Months


3 – Gross Sales of Various product with lead time range. -->

## Data Cleaning
Data Cleaning is the process to transform raw data into consistent data that can be easily analysed. It is aimed at filtering the content of statistical statements based on the data as well as their reliability. Moreover, it influences the statistical statements based on the data and improves your data quality and overall productivity.
Check with respect to the outcome variable for mislabelled entries.
Delete Rows and Columns containing all NA values.
Remove/Drop all the unused levels from Discrete variables(factors).
Imputation - Replace the missing data with the average of the feature in which the data is missing. Find features with missing values. It is observed that “lead_time” has a lot of missing values. We use the mean of this distribution to replace all the missing values.
Outlier Detection - Check all the continuous variables for any outliers which are negatively affecting the model. When an outlier is negatively impacting your model assumptions or results, you may want to replace it with a less extreme maximum value. In Winsorizing, values outside a predetermined percentile of the data are identified and set to said percentile. The following is an example of 95% Winsorization with our dataset.

Outlier detection and removal using winsorization
Converting all categorical data to numeric - Encoding Categorical data simply means we are transforming data that fall into categories into numeric data. We have 7 features with categorical data. All these variables only have 2 levels, “yes” and “no”, so it can be easily mapped to 1 and 0 respectively.
Sampling - Imbalanced datasets are those where there is a severe skew in the class distribution, such as 1:100 or 1:1000 examples in the minority class to the majority class. It is clearly seen in our dataset that with respect to the target variable “went_on_backorder”, the dataset is highly imbalanced.
This bias in the training dataset can influence many machines learning algorithms, leading some to ignore the minority class entirely. This is a problem as it is typically the minority class on which predictions are most important.
A modest amount of oversampling can be applied to the minority class to improve the bias towards these examples, whilst also applying a modest amount of undersampling to the majority class to reduce the bias on that class. This can result in improved overall performance compared to performing one or the other techniques in isolation.


Before and after sampling the data to remove the imbalance

## Modelling  
Logistic Regression
Supervised learning is demonstrated using logistic regression. It is used in computing or forecasting the likelihood of a binary event i.e., a true or false event occurring. An example of logistic regression would be using machine learning to assess whether or not a product should be placed on backorder. Logistic Regression fits a single line to divide the space exactly into two.  As shown in the figure below.
 
After cleaning and transformation of the dataset, and sampling it according to the dependent variable, we have used logistic regression with the following parameters. 
For the 1st model we used the following parameters lead_time ,sales_1_month,  national_inv  , sales_3_month , forecast_9_month.
For the 2nd model we  created a 2 parameter model with the following parameters lead_time , national_inv.
Using the Exploratory Data Analysis we had found out the direct relations of these variables to the dependent variable (went on backorder),we also estimated the influence of one or more covariates while controlling for any confounding variables. The variables national inventory and lead times were discovered to be the most important determinants in determining whether a product should be placed on backorder. 

Decision Tree Model 
A decision tree is a sequence of inquiries or tests that are repeated adaptively, such that the outcomes of previous tests may influence the next test. Decision Trees divide the area into increasingly smaller regions.

The project includes implementation of two decision tree models for the purpose of predicting backorders, that is whether a product should be ordered beforehand or not. This prediction is dependent on a number of parameters. The following independent variables are used for creating a decision tree model for the same.
The First Model used all the Variables in the dataset except the variable SKU as it had multiple different values and no relationship with the dependent Variable.
The Second model was built using 5 of the most important variables for decision tree algorithms which are as follows: lead time, 1st month sales, national inventory,  3rd month Sales and forecasted sales for 9th month.

## Results & Evaluation 
Logistic Regression can occasionally be limited by a single linear boundary. In this case, where the two classes are split by a definitely non-linear boundary, trees can better capture the separation, resulting in greater classification performance. When classes are not well-separated, however, trees are prone to overfitting the training data, hence Logistic Regression's basic linear boundary generalises better. In the project we have compared the results of various models using a confusion matrix which determines the performance of a classification problem.

Variable importance of logistic regression model

Coefficients and results of the Logistic model
The above table shows the results of a 5 variable logistic regression model which was to predict the item that should be placed on backorders. We also compared the results of each model by comparing the accuracies of the created model. The parameters national inventory and lead time had the highest significance as they had very low p values and higher importance according to the table above. The 5 parameter logistic regression provided an accuracy of  71.3% and the model with 2 parameters provided an accuracy of 65.1% which was not sufficient enough to run the models on test data. Therefore the 5 variable model was used on test data which gave the following confusion matrix. 

Confusion Matrix for Logistic Regression model


Results and Variable Importance for Decision tree model

The above figure represents the importance of each variable in the decision tree model. The two decision tree models discussed above had the following model accuracy, 82.91% for all variable model and 82.95% for the 5 parameter model. Therefore the 5 parameter model was implemented on the test data set which gave us the confusion matrix seen below

Confusion Matrix for Decision Tree model

A confusion matrix visualises and summarises a classification algorithm's performance. After comparing the Confusion matrix of the better fit models it was clearly seen that the decision tree model performs way better than the logistic regression model.  After calculating the accuracies from the confusion matrix on the test data set it was seen that logistic regression provided with 54.46% of correct predictions for backorder and decision tree produced an accuracy of 82.27%. Thus we conclude that the decision tree model is better suited for our dataset with a higher level of correct predictions if a product should be sent on backorder or not.
