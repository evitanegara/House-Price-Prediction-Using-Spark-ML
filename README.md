# House Price Prediction Using PySpark

## Project Overview
This project aims to build a predictive model for house prices using the Pakistan House 2023 dataset. Leveraging PySpark's machine learning pipeline, the workflow demonstrates how to clean, process, and model real estate data efficiently at scale. With growing urban development and investment in real estate, accurate price prediction models offer value to buyers, sellers, and investors in making informed decisions. This project also serves as a practical example of applying linear regression in a big data context using distributed computing.

## Dataset Overview
- Source: [Kaggle - House Prices 2023 (Pakistan)](https://www.kaggle.com/datasets)
- Total Records: 99,499 rows
- Features: 8 columns (1 target variable and 7 independent features)

### Column Descriptions

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

### 1. Data Import and Spark Initialization
- Initialized `SparkContext` and configured local Spark session for distributed computation
- Imported essential libraries: `pyspark`, `numpy`, `matplotlib`

### 2. Data Reading and Inspection
- Loaded the dataset containing 99,499 rows and 8 columns
- All columns were initially read as strings
- Converted numeric fields (`price`, `bath`, `bedrooms`, `area_in_marla`) into appropriate integer/float types

### 3. Data Cleaning
- Removed quotation marks and unwanted characters using `regexp_replace`
- Dropped the `location` column due to high cardinality and sparse distribution

### 4. Missing Value and Consistency Checks
- Dropped rows with missing values in the `bath` and `bedrooms` columns
- Verified label consistency in `property_type`, `city`, and `purpose`
- Removed rows where `price <= 0`

### 5. Feature Encoding
- Applied `StringIndexer` and `OneHotEncoder` to categorical columns:
  - `property_type`
  - `city`
  - `purpose`
- Created binary vector representations for each encoded categorical feature

### 6. Feature Visualization and Outlier Handling
- Plotted histograms for `price`, `area_in_marla`, `bath`, and `bedrooms` to understand distributions
- Detected and removed outliers using the Interquartile Range (IQR) method
- Reduced dataset size to 85,344 rows after outlier removal

### 7. Feature Engineering
- Assembled all numerical and encoded features into a single vector using `VectorAssembler`
- Standardized the assembled feature vector using `StandardScaler`

### 8. Train-Test Split
- Split the dataset into 70% training and 30% testing using PySpark’s `randomSplit()` function

### 9. Model Building and Evaluation
- Built a Linear Regression model using `pyspark.ml.regression.LinearRegression`
- Evaluated model performance using:
  - Mean Absolute Error (MAE)
  - Root Mean Squared Error (RMSE)
  - Mean Squared Error (MSE)
- Visualized predicted vs. actual house prices using scatter plots for both training and test sets






In the rapidly growing real estate market, accurate house price predictions are crucial. The real estate industry faces the critical task of determining appropriate pricing for houses by analyzing factors such as location, size, amenities, and market trends. Effective price predictions provide valuable insights to investors, buyers, and real estate professionals, enabling informed decision-making and improved investment strategies

# Porject Objective
- The goal of this project is to predict house prices using the Pakistan House 2023.
- The dataset contains eight columns, with house price as the dependent variable and seven other features as independent variables. [Access the Dataset here](https://www.kaggle.com/datasets/manjitbaishya001/house-prices-2023)


- A linear regression model was implemented using PySpark's machine learning library to predict house prices.
- Evaluation metrics, such as MAE, RMSE, and MSE, were used to assess the model's performance on both the training and test datasets.
  
# Project Overview : 
This project involved several key steps to predict house prices using the Pakistan House 2023 dataset:
- **Data Import and Initialization**: Set up Spark for local execution and imported necessary libraries such as NumPy, Matplotlib, and PySpark.
- **Data Pre-Processing**
  - **Data Cleaning**:  Removed unnecessary characters and converted string columns into appropriate integer types.
  - **Handling Missing and Inconsistent Data**: Applied the dropna method to remove rows with missing values and ensured consistent data across relevant columns.
  - **Feature Encoding**: Transformed categorical variables (e.g., property type, city, and purpose) into numerical form using StringIndexer and OneHotEncoder.
- **Handling Outlier**: Applied the Interquartile Range (IQR) method to detect and remove outliers in continuous variables.
- **Standard Scaller**: Scaled the feature set using StandardScaler to normalize features, ensuring that each feature contributes equally to model training.
- **Train-Test Split**: Divided the dataset into 70% for training and 30% for testing to evaluate model performance on unseen data.
- **Building Model and Evaluation**
  - Building a linear regression model using PySpark.
  - Evaluated performance using metrics such as MAE, RMSE, and MSE for both training and test data.
  - Visualized predicted vs. actual prices, showing a linear relationship with some prediction errors.

# Project Result
- The linear regression model exhibited a positive correlation between actual and predicted house prices for both training and test datasets.
- Evaluation metrics (MAE, RMSE, and MSE) showed similar error values for both training and test sets, reflecting consistent model performance, though the error magnitudes indicate significant deviations from actual prices.
- Although the model demonstrated a linear relationship between actual and predicted prices, the relatively high error values highlight potential limitations, possibly due to feature insufficiency or model complexity.

# Conclusion
The project successfully applied PySpark to predict house prices. Despite a clear linear relationship, high error values suggest further improvements are needed, such as refining feature selection and model complexity for better accuracy in future predictions.
![image](https://github.com/user-attachments/assets/870c5007-7456-48e4-b860-257e42d0c612)

![image](https://github.com/user-attachments/assets/cd6a81f4-72e0-4d11-ad6f-5fabf55698cb)
