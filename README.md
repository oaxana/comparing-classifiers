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

Model Comparison
In this project, we compared the performance of various machine learning models, including Logistic Regression, K-Nearest Neighbors (KNN), Decision Tree, and Support Vector Machine (SVM). The models were evaluated based on training time, training accuracy, and test accuracy. The results are summarized in the table below:


| Model              |Train Time    |Train accuracy| Test Accuracy|
| -------------------|:-------------:| :-------------:|:--------------:|
| Logistic Regression| 0.023750      |0.874046        | 0.870899      |
| KNN                | 0.005072      |0.876630        | 0.860072      |
| Decision Tree      | 0.042662      |0.901772        | 0.850230      |
| SVM                | 11.340689     |0.874046        | 0.870899      |



   Model                Train Time  Train Accuracy  Test Accuracy
0  Logistic Regression    0.023750        0.874046       0.870899
1                  KNN    0.005072        0.876630       0.860072
2        Decision Tree    0.042662        0.901772       0.850230
3                  SVM   11.340689        0.874046       0.870899


Model	Train Time	Train Accuracy	Test Accuracy
KNN	0.002761	0.876671	0.842520
Decision Tree	0.020937	0.875728	0.870899
SVM	31.265578	0.882700	0.867618
The Decision Tree model performed well with a training accuracy of 87.57% and a test accuracy of 87.09%. Despite the SVM model achieving slightly higher accuracy, the Decision Tree's interpretability makes it valuable for understanding feature importance.



1) 3 linear models were created: Linear Regression, Ridge Regression and Lasso Regression.  Two non-linear models were created: Random Forest and XGBoost. 
2) All 3 linear models performed similarly and were only 63% accurate, based on the R² score of 0.63. Test RMSE for all 3 models was 8845.
3) GridSearchCV was attempted for the linear models.  This required a very long compute time, and only the Ridge model parameter of Alpha = 10 was obtained. Attempts to get other best parameters did not work as GidSearchCV did not converge with the allotted compute power after several iteration increases.
4) Decision Tree model performed much better than the Linear Models, capturing non-linear relationships in the data, with 82% accuracy based on the R² score of 0.82. Test RMSE was also slightly better = 6188
5) Random Forest model performed the best by reducing overfitting and averaging multiple trees with 89% accuracy.  Test RMSE was also slightly better than Decision Tree, and almost half the value of the RMSE error of the Linear Models. Test RMSE = 4863.
6) XGBoost performed similarly to Decision Tree with R² score of 0.82 and Test RMSE = 6224

## Notable Findings from Analysis of Linear Models Coefficients:
Based on the coefficients from the Linear Regression model, we can derive insights into how each feature influences the price of a used car. Since the coefficients from the Ridge and Lasso Regression models are similar, we'll focus on the Linear Regression model for this analysis.

### Year (3431)
- For each additional year (newer model year), the price of a car increases by approximately $3431. This makes sense as newer cars are typically more valuable.

### Manufacturer
- Ferrari (1303): Being a luxury brand, Ferrari significantly increases the car price by about $1303 compared to other manufacturers.
- Tesla (796): Tesla cars also command a higher price, increasing the value by approximately $796.
- Porsche (726): Similar to Ferrari and Tesla, Porsche increases the car's price by around $726.
- Other Brands: Brands like GMC, Lexus, and others also show positive coefficients, indicating their positive impact on car prices. On the other hand, manufacturers like Nissan (-931), Kia (-806), and Chrysler (-568) decrease the price, indicating lower market valuation.

### Type of Vehicle
- Pickup (927): Pickup trucks increase the car's price by approximately $926.57, showing their high demand and value.
- Truck (818): Trucks increase the price by $818.49, similar to pickups.
- Coupe (689): Coupes add about $689.05 to the car's price.
- Other Types: Types like sedan (-763) and hatchback (-623) have negative coefficients, indicating they might be valued lower compared to other types.

### Condition of the Car
- Good Condition (450): Cars in good condition are valued $450 higher than those in other conditions.
- New Condition (340): New cars add $340 to the price, reflecting their higher market value.
- Fair Condition (-281): Cars in fair condition decrease the price by $281.

### Odometer (-6913)
- For every additional unit on the odometer, the car's price decreases by $6913. This significant decrease highlights the impact of mileage on car depreciation.

### Size
- Full-Size (545): Full-size cars increase the price by $545, reflecting their higher market value.
- Mid-Size (290): Mid-size cars add $290 to the price.
- Sub-Compact (-31): Sub-compact cars decrease the price by $31.
 

## Notable Findings from Random Forest Feature Importances

### Year (0.403395)
- The year of the car is the most important feature in predicting its price, contributing to ~40% of the decision making process in the model. This indicates that newer cars are generally valued higher. The high importance suggests that the age of the car significantly influences its market value, as newer models typically have better features, less wear and tear, and more up-to-date technology.

### Odometer (0.138815)
- The odometer reading is the 2nd most important feature, contributing to ~14% of the decision making process in the model. Higher mileage usually correlates with more wear and tear, reducing the car's value. The importance of this feature highlights how critical mileage is in determining the price of a used car.

### Drive Type (drive_fwd - 0.083800)
- The drive type, particularly front-wheel drive (FWD), is an important factor. This might be because FWD vehicles are generally more fuel-efficient and offer better traction in various driving conditions, making them more desirable in certain markets.

### Cylinders (cylinders_8 cylinders - 0.027287, cylinders_4 cylinders - 0.015718)
- The number of cylinders in the engine also plays a role. Eight-cylinder cars typically have higher power and performance, which can be appealing to certain buyers, while four-cylinder engines are often more fuel-efficient and cost-effective.

### Vehicle Type (type_truck - 0.012777)
- Trucks have a significant impact on the price, suggesting that they are valued differently compared to other types of vehicles, likely due to their utility, durability, and market demand.

### Manufacturer (ferrari - 0.011035)
- The manufacturer, specifically Ferrari in this case, is an important determinant of car price. Luxury brands like Ferrari generally command higher prices due to their brand value, performance, and exclusivity.

## Summary Of Model Performances

### Linear Regression:
- Mean CV RMSE: 8934.51
- Test RMSE: 8845.07
- R²: 0.63

### Ridge Regression:
- Mean CV RMSE: 8934.51
- Test RMSE: 8845.07
- R²: 0.63

### Lasso Regression:
- Mean CV RMSE: 8934.51
- Test RMSE: 8845.08
- R²: 0.63

### Decision Tree:
- Mean CV RMSE: 6422.88
- Test RMSE: 6187.57
- R²: 0.82

### Random Forest:
- Mean CV RMSE: 4975.25
- Test RMSE: 4863.73
- R²: 0.89

### XGBoost:
- Mean CV RMSE: 6317.70
- Test RMSE: 6223.63
- R²: 0.82

### Actionable Insights Recommendations:

## Modeling Recommendations
- Non-Linear Models: Given the superior performance of non-linear models like Random Forest and XGBoost, prioritize these models for future analysis. They capture complex relationships in the data more effectively than linear models. Keep in mind that Random Forest requires a much longer compute time compared to XGBoost. 
- Hyperparameter Tuning: Continuously refine hyperparameters for non-linear models to further enhance performance. Utilize techniques like GridSearchCV or RandomizedSearchCV but with optimized parameters to balance accuracy and computational efficiency.
- Additional Features: Explore creating new features or interactions between existing ones. For instance, combining year and odometer to form an age feature might provide additional insights.
- Handling Missing Values: Experiment with different imputation methods for missing values to ensure the model utilizes the complete dataset effectively.

## Business Recommendations
- Pricing Strategy: Focus on the year and odometer readings of cars. Newer cars with lower mileage should be priced higher due to their higher market value. Pay attention to high-demand manufacturers like Ferrari, Tesla, and Porsche, as well as vehicle types like pickups and trucks. These tend to sell for higher prices and should be prioritized in inventory.
- Inventory Management: Consider the importance of drive type and fuel efficiency in your inventory decisions. Vehicles with FWD and fuel-efficient options like 4-cylinder engines are more desirable and should be prioritized. Ensure cars in good or new condition are well-represented in your inventory. These cars tend to have higher market values and can contribute to increased profitability.
- Consumer Preferences: Align your inventory with consumer preferences highlighted by the model. For example, if the model indicates a higher preference for certain manufacturers or types, adjust your acquisition strategy accordingly.
- Marketing and Sales: Highlight Key Features in marketing materials and sales pitches that add value, such as low mileage, recent model years, and popular manufacturers. Use the insights to create targeted promotions for high-value cars, leveraging the model's findings to attract more customers and close more sales.
