# Temporal-Integrated Geographically Weighted Regression for Modeling Spatial Heterogeneity and Temporal Variation: A Case Study of PM10 Concentration in DKI Jakarta, 2023

This repository contains an implementation of a Geographically Weighted Regression (GWR) model that incorporates a temporal variable as an independent predictor. The goal is to model the concentration of Particulate Matter 10 (PM10) in DKI Jakarta throughout the year 2023 while addressing spatial heterogeneity and considering temporal effects.


## Project Overview

In spatial analysis, GWR is widely used to model spatial heterogeneity by estimating local regression coefficients for each observation location. However, many real-world datasets also include temporal dimensions that influence the dependent variable. This project extends the standard GWR by integrating a temporal variable to improve the model's explanatory power. 

### Key Features:
- Implementation of GWR with the ability to include temporal variables, with time-related feature engineering using the sin/cos method.
- Optimization of bandwidth for spatial weighting using Cross Validation (CV).
- Analysis of PM10 concentration across five regions in DKI Jakarta using meteorological variables.
- Evaluation of model fit and performance metrics using Mean Absolute Error (MAE), Mean Absolute Percentage Error (MAPE), and Root Mean Squared Error (RMSE).


## Difference Between This Model and GTWR

- This Model (GWR with Temporal Variable): Estimates regression coefficients for each location (city), incorporating a temporal variable as an additional independent predictor. Coefficients are spatially varying.
- GTWR (Geographically and Temporally Weighted Regression): Estimates regression coefficients for each location (city) in each time unit, allowing coefficients to vary across both space and time. As a result, GTWR links parameters to specific locations and times, significantly increasing the number of estimated parameters.


## Dataset

The dataset used in this project includes spatial and temporal observations for DKI Jakarta from January 1, 2023, to December 31, 2023. The primary variables include:
- **Dependent variable:** PM10 concentration (Particulate Matter 10).
- **Independent variables:**
  - **Rainfall:** Measured in inches.
  - **Wind speed:** Measured in miles per hour.
  - **Humidity:** Measured as a percentage.
  - **Temperature:** Measured in degrees Fahrenheit.
- **Spatial variables:** Latitude and Longitude of observation locations.
- **Temporal variable:** Time (Date).


## Methodology

1. **Data Preparation:**
   - **Data Cleaning:** Imputation of missing values.
   - **Data Scaling:** Zero mean normalization.
   - **Time Related Feature Engineering:** sin/cos method.
   - **Data Splitting:**
     - 60% of the data is used for training.
     - 20% of the data is used for validation.
     - 20% of the data is used for testing.

2. **Model Development:**
   - Standard GWR implementation to handle spatial heterogeneity.
   - Integration of a temporal variable as an additional independent predictor.

3. **Model Optimization:**
   - Bandwidth selection using Cross-Validation.
   - Evaluation of model fit and performance metrics.


## Results
- The best kernel was selected based on AIC and R-squared values among fixed and adaptive kernels, with each kernel using Gaussian, Exponential, and Bisquare functions. The best kernel found was fixed exponential with an AIC of 2085.17 and an R-squared of 64.91%.
- Based on the seasonal components chart of PM10 data for each city, it was revealed that PM10 follows a "weekly" seasonal pattern. As a result, the "weekly" temporal feature was used as an additional variable and processed using the sin/cos method.
- A GWR model was developed for each city. Significant parameters for each location were determined through partial parameter tests in GWR.
- The model passed residual normality tests (p=0.215 > 0.05) and local multicollinearity tests (local VIF < 10), confirming its validity for modeling PM10 concentration in DKI Jakarta.
The model achieved the following performance metrics on test data: MAE = 15.21, MAPE = 9.00, and RMSE = 11.61.


## References
- Mahajan, T., Singh, G., Bruns, G., Bruns, G., Mahajan, T., & Singh, G. (2021, March). An experimental assessment of treatments for cyclical data. In Proceedings of the 2021 Computer Science Conference for CSU Undergraduates, Virtual (Vol. 6, p. 22).
- Oshan, T. M., Li, Z., Kang, W., Wolf, L. J., & Fotheringham, A. S. (2019). mgwr: A Python implementation of multiscale geographically weighted regression for investigating process spatial heterogeneity and scale. ISPRS International Journal of Geo-Information, 8(6), 269.

