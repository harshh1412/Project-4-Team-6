# DME Real Estate Price Prediction Project

## 1. Introduction

### 1.1 Project Overview

This project focuses on predicting real estate prices in the USA using various regression models. The goal is to evaluate different models, including traditional linear models and advanced ensemble methods, to determine which provides the most accurate predictions of property prices based on a range of features.

### 1.2 Data Collection

The raw real estate data was downloaded from Kaggle (link provided in [Appendices](#appendices)). The dataset includes the following columns:

- `brokered_by`: Categorically encoded agency/broker
- `status`: Housing status - either *ready for sale* or *ready to build*
- `price`: Housing price, either the current listing price or recently sold price if the house was sold recently
- `bed`: Number of bedrooms
- `bath`: Number of bathrooms
- `acre_lot`: Property/Land size in acres
- `street`: Categorically encoded street address
- `city`: City name
- `state`: State name
- `zip_code`: Postal code of the area
- `house_size`: House area/size/living space in square feet
- `prev_sold_date`: Previously sold date

Additional data were sourced from various sources (links provided in [Appendices](#appendices)) and included neighborhood data like:

- Neighborhood names
- Overall city rankings
- Population density
- Number of hospitals
- Number of private schools
- Number of public schools

All these data files were downloaded and saved on Microsoft Azure Blob Storage so that every team member could access them. The next step was to load all the data into a Jupyter Notebook and use various libraries in Pandas to prepare the data for evaluation.

## 2. Data Preparation

### 2.1 Data Cleaning

An Exploratory Data Analysis (EDA) was conducted, and the dataset was cleaned to handle missing values, outliers, and inconsistent data entries. Relevant preprocessing steps included:

- Merging additional data with the main real estate data
- Removing or imputing missing values and duplicate entries
- Removing unimportant features
- Correcting data types
- Converting units (Acre to Sq.Ft.)

### 2.2 Feature Engineering

- Checked the correlation between our feature of focus—price—and other features. The results were visualized via a heatmap showing correlations between different numerical features in the dataset.
- The heatmap didn’t show any substantial correlation between price and other features, but the `bed` and `bath` features showed a strong correlation between themselves.
- Added a new feature: Bed/Bath ratio to improve correlation.
- Visualized outliers of every feature on box plots and removed them.
- To focus on cities with a substantial number of records, retained only the 20 most prominent cities within each state, based on their row count. This also made the next step (One-hot encoding) easier and less bulky.
- Applied One-hot encoding for neighborhood, city, and state.
- Finally, uploaded the cleaned data in a parquet file format to Microsoft Azure Blob Storage.

## 3. Model Evaluation

This was done using Databricks Community Edition.

### 3.1 Models Tested

The following regression models were evaluated:

- Linear Regression
- Lasso Regression
- Ridge Regression
- Polynomial Regression (degree 2)
- ElasticNet Regression
- RandomForest Regression
- GradientBoosting Regression

### 3.2 Evaluation Metrics

The models were evaluated using the following metrics:

- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R-squared (R²)
- Adjusted R-squared
- F-statistic
- p-value

### 3.3 Results

The evaluation results for each model are summarized in the table below:

| Model                    | MSE           | RMSE         | R²       | Adjusted R² | F-statistic | p-value |
|--------------------------|---------------|--------------|----------|-------------|-------------|---------|
| Linear Regression         | 13,273,656,888.739 | 115,211.357 | 0.8004   | 0.796231    | 191.968109  | 0.0     |
| Lasso Regression          | 13,272,005,384.473 | 115,204.190 | 0.800425 | 0.796256    | 191.997954  | 0.0     |
| Ridge Regression          | 13,268,146,426.687 | 115,187.440 | 0.800483 | 0.796315    | 192.067719  | 0.0     |
| ElasticNet Regression     | 25,081,250,612.327 | 158,370.612 | 0.622846 | 0.614967    | 79.057639   | 0.0     |
| RandomForest Regression   | 3,899,928,343.083  | 62,449.406  | 0.941356 | 0.940131    | 768.439484  | 0.0     |
| GradientBoosting Regression| 17,794,182,823.404 | 133,394.838 | 0.732423 | 0.726834    | 131.037865  | 0.0     |

### 3.4 Model Selection

Based on the evaluation metrics, the most effective model was selected for predicting real estate prices. The RandomForest Regression model demonstrated superior performance in terms of lower error metrics and higher R² values.

## 4. Conclusions

### 4.1 Summary

The project successfully evaluated several regression models for predicting real estate prices. The RandomForest Regression model provided the best performance in terms of prediction accuracy and robustness.

### 4.2 Recommendations

- **Model Deployment**: Deploy the RandomForest Regression model for real-time price predictions.
- **Further Improvements**: Consider integrating additional features or advanced models like XGBoost for potential performance gains.
- **Regular Updates**: Periodically update the model with new data to maintain accuracy and relevance.

### 4.3 Future Work

Future work may involve:

- Exploring more advanced machine learning techniques and feature engineering.
- Performing detailed error analysis to understand and mitigate prediction errors.
- Adding more neighborhood data like crime ratio, property and resident history, important landmarks, celebrities/important personalities living nearby, etc.

## 5. Appendices

### 5.1 Code Snippets

Include key code snippets used for data preparation, model training, and evaluation.

### 5.2 Data Sources

Details on data sources and any preprocessing steps:

- [US Cities Data](https://simplemaps.com/data/us-cities)
- [US Neighborhoods Data](https://simplemaps.com/data/us-neighborhoods)
- [USA Real Estate Dataset](https://www.kaggle.com/datasets/ahmedshahriarsakib/usa-real-estate-dataset/data)
- [Hospitals in the United States](https://www.kaggle.com/datasets/thedevastator/hospitals-in-the-united-states-a-comprehensive-d)
- [US Public Schools](https://public.opendatasoft.com/explore/dataset/us-public-schools/table/)
- [US Private Schools](https://public.opendatasoft.com/explore/dataset/us-private-schools/information/)

### 5.3 Glossary

Definitions of technical terms and metrics used in the report:

- [Real Estate Price Prediction](https://www.kaggle.com/code/fahadrehman07/real-estate-price-prediction)
- [USA Real Estate Price Regression](https://www.kaggle.com/code/hastishahhosseini/usa-real-estate-price-regression)
