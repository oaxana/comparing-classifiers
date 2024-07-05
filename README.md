# Comparing Classifiers

## About the Dataset

Our dataset comes from the UCI Machine Learning repository [link](https://archive.ics.uci.edu/ml/datasets/bank+marketing).  The data is from a Portugese banking institution and is a collection of the results of 17 marketing campaigns marketing campaigns conducted between May 2008 and November 2010, totaling 79,354 contacts.  We will make use of the article accompanying the dataset [here](CRISP-DM-BANK.pdf) for more information on the data and features.

## Business Problem

The Portuguese bank seeks to enhance the effectiveness of its direct marketing campaigns for bank products conducted over the telephone. The primary objective is to develop a predictive model that can classify whether a client will subscribe to a long-term deposit product. This classification task will involve comparing the performance of different classification algorithms (k-nearest neighbors, logistic regression, decision trees, and support vector machines) to determine which model best predicts client subscription. Additionally, the project aims to identify the most predictive features influencing the classification outcome.

## Business Problem Redefined as an ML Data Problem:

- Classification: Develop and evaluate multiple classifier models to predict whether a client will subscribe to the long-term deposit product.
- Model Comparison: Compare the performance of k-nearest neighbors, logistic regression, decision trees, and support vector machines to identify the most accurate and reliable model.
- Feature Importance: Analyze and identify the top features that significantly contribute to the prediction of a client's likelihood to subscribe to the deposit product.

## Key Findings:

In this project, we compared the performance of various machine learning models, including Logistic Regression, K-Nearest Neighbors (KNN), Decision Tree, and Support Vector Machine (SVM). The models were evaluated based on training time, training accuracy, and test accuracy. 

In order to obtain these results, hyperparameter tuning using GridSearchCV was performed on all models. 
Note that Logistic Regression coefficients did not converge.

The results are summarized in the table below:


| Model              | Train Time (s) | Train accuracy | Test Accuracy | Best Params |
| -------------------| :-------------:| :-------------:|:-------------:| --------------------------------------------------------------------|
| Logistic Regression| 0.022495       | 0.874046       | 0.870899      | {'C': 100, 'penalty': 'l1', 'solver': 'liblinear', 'max_iter': 1000}|
| KNN                | 0.002848       | 0.876671       | 0.842520      | {'n_neighbors': 3}                                                  |
| Decision Tree      | 0.022439       | 0.875728       | 0.870899      | {'criterion': 'entropy', 'max_depth': 7}                            |
| SVM                | 31.239822      | 0.882700       | 0.867618      | {'C': 10, 'gamma': 1, 'kernel': 'rbf'}                              |


### Summary of Model Performance Findings 

- Logistic Regression: Although Logistic Regression showed good performance, it faced convergence issues. Test Accuracy: 87.09% 
- KNN: Quick to train but slightly lower test accuracy compared to Logistic Regression and Decision Tree. Test Accuracy: 84.25%
- Decision Tree: Performed similarly well as Logistic Regressioncy. Despite the SVM model achieving slightly higher accuracy, the Decision Tree's interpretability makes it valuable for understanding feature importance. Test Accuracy: 87.09%
- SVM: Highest training accuracy but also extremely long training time, indicating it can handle complex decision boundaries well, however the minimal improvement in performance is generally not worth the extra compute time. Test Accuracy: 86.76%

### Most Important Features from Decision Tree model:

- Age: The most significant feature with an importance of 0.518197. Older clients are more likely to respond positively to marketing campaigns.
- Job (Student): With an importance of 0.171793, being a student significantly impacts the likelihood of a positive response.
- Education (University Degree): Higher education levels, such as holding a university degree, have a notable impact on the response, with an importance of 0.101527.
- Other Important Features:
-- Basic Education (4 years): 0.035626
-- Job (Blue-collar): 0.030376
-- Job (Unemployed): 0.025646

### Recommendations

Targeted Marketing Strategies and Personalized communication:

- Age: Given the high importance of age, marketing campaigns should be tailored to different age groups. Older clients, in particular, should be targeted with campaigns that address their specific needs and preferences.
- Students and Educated Clients: Special attention should be given to students and clients with higher education levels, such as university graduates. These groups show significant predictive importance and should be targeted with customized marketing messages.

Feature Engineering and Further Model Tuning:

- Job and Education Levels: Further feature engineering could uncover additional valuable predictors. For example, exploring interactions between job types and education levels may provide deeper insights into client behaviors.
- Handling Convergence Issues: For Logistic Regression, increasing the max_iter parameter or using a different solver like 'saga' could help achieve convergence.
- Decision Tree: Given its high accuracy and interpretability, further tuning of the Decision Tree model's parameters, such as max_depth and criterion, could yield even better results.
- Adjusting Performance Metrics: Precision, Recall, and F1 Score could be explored as additional metrics, especially since there is a class imbalance, to better capture the model's performance.

By implementing these recommendations, the bank can optimize its marketing strategies to better target potential clients and improve the overall effectiveness of its campaigns. Future work could involve refining these models and exploring additional features to further enhance predictive performance.
