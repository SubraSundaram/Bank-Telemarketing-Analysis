# Bank-Telemarketing-Analysis
Analysis of Bank Telemarketing data to effectively target Customers
# Using Data to predict the success of bank telemarketing

__Jupyter Notebook with code, experimentation, further insights, and deployment strategies:__ [click here](https://github.com/SubraSundaram/Bank-Telemarketing-Analysis/blob/main/prompt_III.ipynb)

__Reference credit: Insights and the project demonstrated during office hours over the last six modules.__

## Business Goal
The Business objective of the task is to help the Portugese bank optimize their marketing efforts by predicting which customers will subscribe to a term deposit and which ones won't do so.

This can be accomplished by creating a model that predicts which customers will subscribe to the term deposit based on other existing data about the Customer.


## Data Analysis
The dataset contains 20 baseline variables, eleven of which are numeric and the remaining categorical. The target column is “y” and has the information on whether the customer signed up for the Term deposit ('y'=1) or not ('y'=0). The distribution of the target variable after the removal the duplicates is shown below. As evidenced by the counts of the target Y variables, the dataset is skewed.

![Alt text](M17_target_distrib_pic_0.png?raw=true "Target Distribution")

### Ordinal vs Onehotencoding
Some of the columns like education, day_of_Week are amenable to Ordinal encoding. But for simplicity we will onehotencode all categorical variables. Dropping day_of_week would be required if the number of columns are found to be too high and takes a long time to analyze after onehotencoding.

### Collinearity
A check for collinearity reveals that three Columns -- nr.employed, euribor3m, and emp.var.rate -- are highly correlated. Two of them could be dropped in the subsequent analyses.
![Alt text](M17_corr_matrix_pic1.PNG?raw=true "Correlation Matrix")

### Other columns
Column pdays is filled with the value 999 in 96.3% of the rows. So that column could also be dropped in the next analyses.


## Modeling and performance
### Model Comparison
As per requirements, we employed four modeling techniques -- Logistic Regression, KNearest Neighbors, Decision Tree, and Support Vector Machines. First each model was trained and evaluated using a train/test split, using the default parameters. 

### Improving The Model
This was followed by cross-validation and hyperparameter tuning using GridSearchCV to optimize performance.

Among these, The decision tree classifier, with the parameters criterion = ‘gini’ and max_depth = 5, had the best f1-score for predicting customers who will sign up for the term deposit. The model also better predicted which customers wouldn’t sign up for the campaign. This can help inform the bank’s marketing team about who not to approach or spend marketing dollars with.
![Alt text](M17_Best_DTC_Model_pic4.PNG?raw=true "Best Decision Tree Model")

The decision tree can be seen in the Jupyter notebook added to this project.

## Conclusions
The decision tree classifier was the fastest and the SVM classifier was the slowest. 
The model was run with all the columns. Four or five columns identified (‘contact’, ‘nr.employed’, ‘euribor3m’, ‘pdays’, ‘duration’) could be dropped in the next round to see if that improves the performance of the model and also the time it takes to fit the model.

The logistic regression model identified the following columns as having a significant impact on the model – High positive impact: month (Mar and Aug – last contact months), and cons.price.idx. High negative impact: emp.var.rate, poutcome (failure), month (May – last contact month).
![Alt text](M17_LGR_High_Impact_Features_pic_5.PNG?raw=true "LGR Model High Impact Params")

The KNearest Neighbor model relies on ‘nr.employed’, duration (which was suggested to be removed, and should be done in the next run), pdays (which should also be removed in the next run as the data in this field is highly skewed), and euribor3m. Here are top five important features highlighted by Permutation Importance Analysis on the best KNN model.
![Alt text](M17_KNN_High_Impact_Features_pic_6.PNG?raw=true "LGR Model High Impact Params")


## Future improvements for the analysis and other comments:
1.	More analyses such as Permutation Importance analysis should be carried out on other models.
2.	Dropping some columns that show collinearity, and those have highly skewed data, would be beneficial for the analysis.
3.	Ordinal encoding of the two columns identified (day of week, and Education) would be worth a try, to see if it improves model accuracy.

