Health Insurance Claim Cost Predictor

A data mining and predictive analytics project that utilizes multiple linear regression to estimate healthcare claim amounts based on patient demographic and biometric data.

## Project Overview
This project analyzes the primary health and demographic risk factors that drive health insurance claim costs. Using R, multiple linear regression models were constructed, evaluated, and optimized to provide insurance companies with a reliable framework for risk assessment, premium pricing, and resource allocation.

## Key Insights
*   **Model Accuracy**: The optimized regression model explains **72.6% of the variance** in medical claim costs ($R^2 = 0.726$).
*   **Primary Cost Driver**: Smoking status is the single most significant predictor. Being a smoker increases the expected claim amount by an average of **$20,681**, holding all other factors constant.
*   **Significant Predictors**: BMI, blood pressure, diabetic status, number of children, and the Southeast geographic region are statistically significant contributors to the model ($p < 0.05$).
*   **Insignificant Factors**: Age and gender showed high p-values during early iterations and were removed to streamline model performance.

## Dataset Description
The analysis utilizes the **Insurance Claim Analysis: Demographic and Health** dataset (sourced from Kaggle). It contains 11 core variables:
*   `claim` (Response Variable): Total financial amount paid out for the insurance claim.
*   `bmi`: Body Mass Index of the insured individual.
*   `bloodpressure`: Blood pressure level.
*   `diabetic`: Binary indicator for diabetic status ($0 = \text{No}, 1 = \text{Yes}$).
*   `children`: Total number of dependents.
*   `smoker`: Binary indicator for smoking habits ($0 = \text{No}, 1 = \text{Yes}$).
*   `region`: Categorical geographic location, engineered into dummy variables (`southeast`, `northeast`, `southwest`).

## Project Workflow & R Script Structure
1.  **Data Cleaning & Preprocessing**: Missing values are checked via `colSums(is.na())` and dropped. Indexing columns are filtered out.
2.  **Data Partitioning**: The data is split using a deterministic seed (`set.seed(007)`) into a 70% training set and a 30% testing set.
3.  **Exploratory Data Analysis**: 
    *   Generates a Pearson correlation matrix and a visual heatmap using `corrplot`.
    *   Produces boxplots to identify data distributions, variance, and outliers across variables.
4.  **Model Iteration & Optimization**:
    *   `lm.fit`: Baseline model with all initial variables.
    *   `lm.fit1`: Refined model dropping insignificant predictors (age, gender).
    *   `lm.fit3`: Evaluates interaction terms between key biometrics (BMI $\times$ Blood Pressure).
    *   `model`: Tests non-linear log and square-root transformations.
5.  **Model Diagnostics**:
    *   Evaluates Variance Inflation Factors (`vif()`) using the `car` library to guarantee zero multicollinearity.
    *   Generates standard diagnostic plots (`Residuals vs Fitted`, `Normal Q-Q`, `Scale-Location`, `Residuals vs Leverage`) to validate linear regression assumptions.
6.  **Predictions & Export**: Maps predictions against the test data partition and exports the final matrix to a CSV file.

## Required R Packages
To run the analysis script, install and load the following libraries:
```R
install.packages(c("MASS", "dplyr", "ggplot2", "corrplot", "car"))
```

## How to Run the Analysis
1. Clone this repository to your local workspace.
2. Update the file pathway in `read.csv()` to target your local copy of the insurance dataset.
3. Execute the script in RStudio or via your terminal console:
   ```R
   source("insurance_analysis.R")
   ```

## Author
*   **Sabun Dhital**
*   Course: Data Mining for Managers (DSCI 724)
*   Instructor: Prof. Thomas Tiahrt
*   University of South Dakota
