# Real Estate Price Prediction Project Report

### 1. Introduction <br>

#### 1.1 Project Overview <br>

This project focuses on predicting real estate prices in the USA using various regression models. The goal is to evaluate different models, including traditional linear models and advanced ensemble methods, to determine which provides the most accurate predictions of property prices based on a range of features.
1.2 Data Collection
The raw Real Estate data was downloaded from Kaggle (link provided in Appendices).
The dataset includes the following columns:
•	brokered by (categorically encoded agency/broker)
•	status (Housing status - a. ready for sale or b. ready to build)
•	price (Housing price, it is either the current listing price or recently sold price if the house is sold recently)
•	bed (# of beds)
•	bath (# of bathrooms)
•	acre_lot (Property / Land size in acres)
•	street (categorically encoded street address)
•	city (city name)
•	state (state name)
•	zip_code (postal code of the area)
•	house_size (house area/size/living space in square feet)
•	prev_sold_date (Previously sold date)
Additional data were sourced from various sources (links provided in Appendices) which had neighborhood data like:
•	neighborhood names
•	overall city rankings
•	population density
•	No. of hospitals
•	No. of Private schools
•	No. of Public schools
All these data (csv files) were downloaded and saved on Microsoft Azure blob storage so that every team member can excess the data.
Next step was to load all the data on a Jupyter Notebook and use various libraries in Pandas to prepare the data for evaluation.

2. Data Preparation
2.1 Data Cleaning
An EDA (Exploratory Data Analysis) was done and the dataset was cleaned to handle missing values, outliers, and inconsistent data entries. Relevant preprocessing steps included:
•	Merging additional data to the main real estate data.
•	Removing or imputing missing values and duplicate values.
•	Removing unimportant features.
•	Correcting data types
•	Conversion of units (Acre to Sq.Ft.)
2.2 Feature Engineering
•	Checking correlation between our feature of focus - price and other features. Visualize the results via a heatmap that shows the correlations between different numerical features in the dataset.
•	The heatmap didn’t show any substantial correlation between price and other features. But the ‘bed’ and ‘bath’ showed strong correlation between themselves.
•	Added a feature - Bed/bath ratio to improve correlation.
•	Visualized outliers of every feature on box plots and removed them.
•	To focus on cities with a substantial number of records, we will retain only the 20 most prominent cities within each state, based on their row count. This also makes the next step (One-hot encoding) easier and not bulky.
•	One-hot encoding for neighborhood, city and state.
•	Finally, uploaded the cleaned data in a parquet file format to Microsoft Azure Blob Storage.

3. Model Evaluation
This was done DataBricks Community Edition.
3.1 Models Tested
The following regression models were initialized:
•	Linear Regression
•	Lasso Regression
•	Ridge Regression
•	Polynomial Regression (degree 2)
•	ElasticNet Regression
•	RandomForest Regression
•	GradientBoosting Regression
3.2 Evaluation Metrics
The models were evaluated using the following metrics:
•	Mean Squared Error (MSE)
•	Root Mean Squared Error (RMSE)
•	R-squared (R²)
•	Adjusted R-squared
•	F-statistic
•	p-value
3.3 Results
The evaluation results for each model are summarized in the table below:
Model	MSE	RMSE	R²	Adjusted R²	F-statistic	p-value
Linear Regression	13273656888.73951	115211.357464	0.8004	0.796231	191.968109	0.0
Lasso Regression	13272005384.472576	115204.189961	0.800425	0.796256	191.997954	0.0
Ridge Regression	13268146426.687399	115187.440403	0.800483	0.796315	192.067719	0.0
ElasticNet Regression	25081250612.32745	158370.61158	0.622846	0.614967	79.057639	0.0
RandomForest Regression	3899928343.082592	62449.406267	0.941356	0.940131	768.439484	0.0
GradientBoosting Regression	17794182823.403629	133394.838069	0.732423	0.726834	131.037865	0.0
3.4 Model Selection
Based on the evaluation metrics, the most effective model was selected for predicting real estate prices. The RandomForest Regression model demonstrated superior performance in terms of lower error metrics and higher R² values.

4. Conclusions 
4.1 Summary
The project successfully evaluated several regression models for predicting real estate prices. The RandomForest Regression model provided the best performance in terms of prediction accuracy and robustness.
4.2 Recommendations
•	Model Deployment: Deploy the RandomForest Regression model for real-time price predictions.
•	Further Improvements: Consider integrating additional features or advanced models like XGBoost for potential performance gains.
•	Regular Updates: Periodically update the model with new data to maintain accuracy and relevance.
4.3 Future Work
Future work may involve:
•	Exploring more advanced machine learning techniques and feature engineering.
•	Performing a detailed error analysis to understand and mitigate prediction errors.
•	Adding more additional neighborhood data like crime ratio, property and resident history, important landmarks, celebrities/important personalities living nearby, etc.

5. Appendices
5.1 Code Snippets
Include key code snippets used for data preparation, model training, and evaluation.
5.2 Data Sources
Details on data sources and any preprocessing steps.
https://simplemaps.com/data/us-cities
https://simplemaps.com/data/us-neighborhoods
https://www.kaggle.com/datasets/ahmedshahriarsakib/usa-real-estate-dataset/data
https://www.kaggle.com/datasets/thedevastator/hospitals-in-the-united-states-a-comprehensive-d
https://public.opendatasoft.com/explore/dataset/us-public-schools/table/
https://public.opendatasoft.com/explore/dataset/us-private-schools/information/

5.3 Glossary
Definitions of technical terms and metrics used in the report.
https://www.kaggle.com/code/fahadrehman07/real-estate-price-prediction
https://www.kaggle.com/code/hastishahhosseini/usa-real-estate-price-regression
