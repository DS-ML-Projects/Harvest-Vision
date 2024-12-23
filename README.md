# Crop Yield Prediction

This project focuses on predicting crop yield (in tons per hectare) using a machine learning pipeline. The dataset used includes various agricultural factors such as soil type, crop type, weather conditions, and irrigation methods, providing a comprehensive framework for understanding and improving agricultural productivity.

## Dataset Overview
This dataset contains agricultural data for 1,000,000 samples aimed at predicting crop yield (in tons per hectare). It can be used for regression tasks in machine learning, especially for predicting crop productivity. The dataset includes the following features:

- **Region**: The geographical location where the data was collected.
- **Soil Type**: The type of soil (e.g., sandy, clay, loamy).
- **Crop Type**: The type of crop grown (e.g., wheat, corn, rice).
- **Rainfall (mm)**: Total rainfall in millimeters.
- **Temperature (C)**: Average temperature in degrees Celsius.
- **Fertilizer Usage (kg)**: Amount of fertilizer applied.
- **Irrigation Usage**: Whether irrigation was applied or not.
- **Weather Conditions**: Summary of weather during the growing period.
- **Days to Harvest**: The number of days between planting and harvesting.
- **Target Variable**: Crop yield in tons per hectare.

## Algorithms and Techniques Used

### 1. Decision Tree Regression
A decision tree regressor was implemented to model the relationship between the features and the target variable. The decision tree visually displays the decision-making process and is highly interpretable.

### 2. Confusion Matrix
To assess model performance (if a classification task is required in future expansions), confusion matrices could be used. For this regression task, metrics such as Mean Absolute Error (MAE) and R-squared are more relevant.

### 3. Outlier Detection
Outliers were detected and handled to ensure the dataset's integrity. Techniques such as z-scores and interquartile range (IQR) were used.

### 4. Correlations
The Pearson correlation coefficient was calculated to understand the linear relationships between features. This helped in feature selection and dimensionality reduction.

### 5. Normal Distributions
The distribution of numerical features (e.g., rainfall, temperature) was analyzed for normality. Techniques like logarithmic transformations were applied where necessary to meet the assumptions of the regression model.

## Visualization
### Decision Tree
Below is a placeholder for the decision tree visualization generated during the project. The tree helps in understanding feature importance and decision paths:

![Decision Tree](./decision-tree.png)

## Files Included
- `yield-prediction-1-0.ipynb`: Jupyter Notebook containing the full implementation of the project.
- `decision-tree.png`: Visualization of the decision tree regressor (attach actual image here).

## Future Work
- Expand the dataset with more features such as pest data and crop disease information.
- Explore advanced regression models like Random Forest and Gradient Boosting.
- Develop an API to serve predictions in real-time.

## How to Run
1. Clone this repository.
2. Open `yield-prediction-1-0.ipynb` in Jupyter Notebook.
3. Run all cells to preprocess the data, train the model, and evaluate results.

## Acknowledgments
Thanks to the agricultural researchers and data providers who made this dataset available for machine learning applications.

