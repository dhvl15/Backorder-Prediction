# Backorder Prediction in R

In supply chain systems, backorders can negatively impact effectiveness at service levels. Identifying parts with the highest chances of shortage prior its occurrence can present a high opportunity to improve an overall company’s performance.

## What is backorder?
A backorder is a purchase order for a good or service that cannot be fulfilled right away owing to a shortage of stock. Although the product might not be in the company's current inventory, it might still be in production, or the company might need to continue producing more of the item. Backorders are a sign that a company's product is in higher demand than it can meet. The company's backlog is another name for them.
Backorder Key Features: 
A backorder is a purchase order for a good or service that cannot be fulfilled right away owing to a shortage of stock.
Backorders provide information about an organisation's inventory control. A small backorder with quick turnaround is advantageous, but a big backorder with protracted wait times can cause issues.
Demand is typically high for businesses with reasonable backorders, but those who can't keep up risk losing clients.
Backorders, on the other hand, enable a business to have lower levels of inventory, have a lesser risk of obsolescence and theft, and may lead to organic promotion for its in high demand goods.
Backorders may occur for popular items that are in great demand (such as new models of cell phones or gaming consoles).

<!--1.2 Backorder Graphical Visualisation:-->

## What causes backorders?
Backorders occur for a variety of reasons — some of which are preventable and others that are simply out of your control. 
* Unusual demand
* Low safety stock
* Manufacturer or supplier problem
* Human error
* Inventory and warehouse management discrepancies
* Long lead time 

Difference between Backlog and Backorder
Because of their similarity, people frequently mix up the two terms. A backorder can also be referred to as a backlog.


##How Do Backorders Operate?
Let's think about two instances in order to comprehend how backordering functions. In one, the business has the necessary inventory, whereas in the other, the products are out of stock

Situation 1: If the Good Is Currently in Stock
Customers place orders.
The corporation creates the sales order.
It locates the specific item in its inventory and compares it to the sales order.
The company delivers the order to the client

Situation 2: Backordering Scenario
The scenario is that the product is out of stock when the consumer puts the order.
The business starts the product's backorder. After that, it transforms it into a purchase order written to the supplier.
The company notifies the supplier of the purchase order.
The supplier completes the order after receiving the purchase order.
The business ships the order to the consumer after receiving it.

We can see from the examples that the backordering for one out-of-stock goods works nicely. But you can't use it as your only inventory approach. You must be able to match each purchase order with the appropriate sales order before starting the product delivery procedure. A strategy for managing your inventory that correlates to your sales and purchase orders is beneficial. This makes it easier for you to coordinate the management of both incoming and exiting sales.
When you do not have enough product on hand, backordering enables you to keep your consumers and ensure that your sales increase. Additionally, the organisation can benefit significantly by cutting costs, increasing the worth of your product, and minimising waste. You may also offer customised orders thanks to it. If you have a strong system in place to manage your inventory and provide excellent customer service, backordering can be a successful strategy for you.





## When Will a Backorder Occur?
A backorder is a particular circumstance involving a direct vendor or item. How long a backorder will take is not specified by law or business standards. While some businesses may just inform customers when their goods are available, others may publicly state when they anticipate their backorder will be addressed.

# Data Understanding & Preparation 
Source of Data: The data comes from Kaggle’s dataset:  “Predict Product Backorders”.
https://www.kaggle.com/competitions/untadta/data
The dataset contains 1,048,576 rows (data points) and 23 columns (features). The target variable (or response) is the went_on_backorder variable. Each row represents an individual product and each column represents a feature such as:




Data Preparation

There are 7 factor variables and 16 continuous variables present in the dataset.
The Correlation matrix shows a positive linear correlation between most of the continuous variables. 
It is observed that sales, forecast, min_bank, national_inv and lead_time have a strong positive correlation and can be used for prediction.

Exploratory Data Analysis
Exploratory data analysis (EDA) is used to analyse and investigate data sets and summarise their main characteristics, often employing data visualisation methods. Tools we can use for EDA - 
Clustering and dimension reduction techniques.
Univariate visualisation 
Bivariate visualisations 
Multivariate visualisations
K-means Clustering 
Predictive models







Some EDA on primary data-set:
1 -  Visualization of Sales V/s Forecasted Sales for X months







2-Forecasted Sales v/s Minimum recommended amount in stock of X Months


3 – Gross Sales of Various product with lead time range

Data Cleaning
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

3. Modelling  
A machine learning model is a data file that has been trained to recognise specific patterns. You train a model on a set of data by providing it with an algorithm that it may use to reason about and learn from that data. A model's purpose is to produce a low-dimensional overview of a dataset. Models will be used to divide data into patterns and residuals. Strong patterns will obscure finer trends, so as we investigate a dataset, we'll utilise models to help peel back layers of structure. In the project we used various machine learning models to predict whether a particular product must be put on back order or not. We have used two models with various parameters for our dataset. The two models with their following parameters are explained below. 
Logistic Regression
Supervised learning is demonstrated using logistic regression. It is used in computing or forecasting the likelihood of a binary event i.e., a true or false event occurring. An example of logistic regression would be using machine learning to assess whether or not a product should be placed on backorder. Logistic Regression fits a single line to divide the space exactly into two.  As shown in the figure below.
 
After cleaning and transformation of the dataset, and sampling it according to the dependent variable, we have used logistic regression with the following parameters. 
For the 1st model we used the following parameters lead_time ,sales_1_month,  national_inv  , sales_3_month , forecast_9_month.
For the 2nd model we  created a 2 parameter model with the following parameters lead_time , national_inv.
Using the Exploratory Data Analysis we had found out the direct relations of these variables to the dependent variable (went on backorder),we also estimated the influence of one or more covariates while controlling for any confounding variables. The variables national inventory and lead times were discovered to be the most important determinants in determining whether a product should be placed on backorder. 
Decision Tree Model 
A decision tree is a method for making decisions that uses a tree-like model of options and their potential consequences, such as chance event outcomes, resource costs, and utility. It's one way to demonstrate an algorithm using just conditional control statements. Decision trees are a prominent machine learning approach that is frequently used in operations research, particularly in decision analysis, to assist in discovering the strategy that is most likely to achieve a goal.
A decision tree is a sequence of inquiries or tests that are repeated adaptively, such that the outcomes of previous tests may influence the next test. Decision Trees divide the area into increasingly smaller regions.

The project includes implementation of two decision tree models for the purpose of predicting backorders, that is whether a product should be ordered beforehand or not. This prediction is dependent on a number of parameters. The following independent variables are used for creating a decision tree model for the same.
The First Model used all the Variables in the dataset except the variable SKU as it had multiple different values and no relationship with the dependent Variable.
The Second model was built using 5 of the most important variables for decision tree algorithms which are as follows: lead time, 1st month sales, national inventory,  3rd month Sales and forecasted sales for 9th month.
# Results & Evaluation 
Logistic Regression can occasionally be limited by a single linear boundary. In this case, where the two classes are split by a definitely non-linear boundary, trees can better capture the separation, resulting in greater classification performance. When classes are not well-separated, however, trees are prone to overfitting the training data, hence Logistic Regression's basic linear boundary generalises better. In the project we have compared the results of various models using a confusion matrix which determines the performance of a classification problem.

Variable importance of logistic regression model

Coefficients and results of the Logistic model
The above table shows the results of a 5 variable logistic regression model which was to predict the item that should be placed on backorders. We also compared the results of each model by comparing the accuracies of the created model. The parameters national inventory and lead time had the highest significance as they had very low p values and higher importance according to the table above. The 5 parameter logistic regression provided an accuracy of  71.3% and the model with 2 parameters provided an accuracy of 65.1% which was not sufficient enough to run the models on test data. Therefore the 5 variable model was used on test data which gave the following confusion matrix. 

Confusion Matrix for Logistic Regression model


Results and Variable Importance for Decision tree model

The above figure represents the importance of each variable in the decision tree model. The two decision tree models discussed above had the following model accuracy, 82.91% for all variable model and 82.95% for the 5 parameter model. Therefore the 5 parameter model was implemented on the test data set which gave us the confusion matrix seen below

Confusion Matrix for Decision Tree model

A confusion matrix visualises and summarises a classification algorithm's performance. After comparing the Confusion matrix of the better fit models it was clearly seen that the decision tree model performs way better than the logistic regression model.  After calculating the accuracies from the confusion matrix on the test data set it was seen that logistic regression provided with 54.46% of correct predictions for backorder and decision tree produced an accuracy of 82.27%. Thus we conclude that the decision tree model is better suited for our dataset with a higher level of correct predictions if a product should be sent on backorder or not.
