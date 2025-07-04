# House Price Prediction Using PySpark

## Project Overview
This project aims to build a predictive model for house prices using the Pakistan House 2023 dataset. Leveraging PySpark's machine learning pipeline, the workflow demonstrates how to clean, process, and model real estate data efficiently at scale. With growing urban development and investment in real estate, accurate price prediction models offer value to buyers, sellers, and investors in making informed decisions. This project also serves as a practical example of applying linear regression in a big data context using distributed computing.

## Dataset Overview
- Source: Kaggle House Prices 2023 (Pakistan)
- Total Records: 99,499 rows
- Features: 8 columns (1 target variable and 7 independent features)

| Column         | Description                     | Type        |
|----------------|---------------------------------|-------------|
| price          | House sale price                | Continuous  |
| bedrooms       | Number of bedrooms              | Integer     |
| bath           | Number of bathrooms             | Integer     |
| area_in_marla  | Size of the house               | Continuous  |
| city           | City where the house is located | Categorical |
| purpose        | Purpose of listing (sale/rent)  | Categorical |
| property_type  | Type of property (e.g., house, plot) | Categorical |
| location       | Location (removed due to high cardinality) | Categorical |

## Executive Summary
The dataset underwent a thorough preprocessing pipeline, including type conversions, missing value handling, outlier detection, encoding categorical variables, and feature standardization. A linear regression model was built using PySpark ML. Although the model achieved consistent performance across training and testing sets, high error values suggest limitations in the model's ability to generalize with limited and broad features. The outcome provides a solid baseline while pointing to avenues for further optimization.

## Project Workflow
### Data Import and Spark Initialization
- Initialized SparkContext and configured local Spark session for distributed computation
- Imported essential libraries: pyspark, numpy, matplotlib

### Data Reading and Inspection
- Loaded the dataset containing 99,499 rows and 8 columns
- All columns were initially read as strings
- Converted numeric fields (price, bath, bedrooms, area_in_marla) into appropriate integer/float types

### Data Cleaning
- Removed quotation marks and unwanted characters using regexp_replace
- Dropped the location Column due to high cardinality and sparse distribution

### Missing Value and Consistency Checks
- Dropped rows with missing values in the bath and bedrooms columns
- Verified label consistency in property_type, city, and purpose
- Removed rows where price <= 0

### Feature Encoding
- Applied StringIndexer and OneHotEncoder to categorical columns:
  - property_type
  - city
  - purpose
- Created binary vector representations for each encoded categorical feature

### Feature Visualization and Outlier Handling
- Plotted histograms for price, area_in_marla, bath, and bedrooms to understand distributions
- Detected and removed outliers using the Interquartile Range (IQR) method
- Reduced dataset size to 85,344 rows after outlier removal

<p align="center">
  <img src="https://github.com/user-attachments/assets/1bd5568d-cc9d-4187-ab8e-708b5bf7d2bc" width="800"/>
</p>

### Feature Engineering
- Assembled all numerical and encoded features into a single vector using VectorAssembler
- Standardized the assembled feature vector using StandardScaler

### Train-Test Spli
- Split the dataset into 70% training and 30% testing using PySpark’s randomSplit() function

### Model Building and Evaluation
- Built a Linear Regression model using pyspark.ml.regression.LinearRegression
- Evaluated model performance using:
  - Mean Absolute Error (MAE)
  - Root Mean Squared Error (RMSE)
  - Mean Squared Error (MSE)
- Visualized predicted vs. actual house prices using scatter plots for both training and test sets
  
## Model Performance Summary

<p align="center">
  <img src="https://github.com/user-attachments/assets/649f79da-61a4-4f4e-ae8f-f909c4282c72" width="800"/>
</p>

## Highlights

- PySpark’s Linear Regression model captured a clear linear relationship between actual and predicted house prices

- Mean Absolute Error (MAE) was consistent across datasets  
  Train MAE: 3,684,701.95  
  Test MAE: 3,674,413.53

- Root Mean Squared Error (RMSE) showed nearly identical values  
  Train RMSE: 4,773,656.36  
  Test RMSE: 4,758,605.25

- Mean Squared Error (MSE) remained high for both sets  
  Train MSE: 22.81 trillion  
  Test MSE: 22.64 trillion

- Scatter plots of predicted vs. actual values displayed a clear positive linear trend, showing the model successfully captured general pricing behavior


## Key Takeaways
- Trend Detection Over Precision
The model performs well in identifying pricing directionality, but its relatively high error metrics reveal limitations in making precise individual predictions, especially for high value properties.

- Feature Scope Constrains Accuracy
Excluding influential variables such as location (due to high cardinality) limited the model’s ability to capture spatial and market-level variation, critical drivers in real estate pricing.

- IQR-Based Outlier Removal Boosted Stability
Eliminating extreme values in price and area_in_marla improved overall model stability, reducing noise and enabling better generalization to unseen data.

- Standardization Supported Balanced Learning
Applying StandardScaler ensured that all numeric features contributed proportionally to the regression, enhancing model convergence and interpretability.

- No Overfitting Observed
The minimal gap between training and testing performance suggests strong generalization, a key strength for deploying this model in real-world scenarios.

## Contact
For any questions or inquiries, please contact evitanegara@gmail.com

