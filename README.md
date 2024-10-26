# Earthquake Forecasting Using Recurrent Neural Networks and Semivariogram Analysis

**Author**: Harry Averkiadis
**Institution**: Tilburg University, MSc in Data Science & Society
**Date**: June 24, 2024

This repository contains the code and analysis for my master's thesis on forecasting significant global earthquakes (magnitude 5.5+) using Recurrent Neural Networks (RNNs) with enhancements such as Semivariogram Analysis and Attention Mechanisms.

# Project Overview
This thesis addresses the challenge of predicting the timing of major earthquakes by employing RNNs, specifically Long Short-Term Memory (LSTM) networks. The primary innovation in this research lies in integrating Semivariogram Analysis to capture spatial dependencies and using attention mechanisms to enhance predictive performance. The dataset spans from 1900 to 2023, with a focus on capturing spatio-temporal patterns to estimate the number of days until the next significant earthquake event.

# Files Overview
1) Tilburg_University_DSS_Masters_Thesis_Earthquake Forecasting_S2023.pdf: The complete thesis document, detailing the research problem, methodology, results, and conclusions.
2) EDA_1_LSTM_baseline_model.ipynb: Contains exploratory data analysis (EDA) and the baseline LSTM model. This notebook includes all the EDA visuals and insights gained from preliminary analysis.
3) EDA_1_model_ARIMA.ipynb: Implements a simple ARIMA model as a statistical baseline to compare with the more complex deep learning approaches.
4) EDA_2_baseline_plus_semivariogram_model.ipynb: This notebook contains the best-performing model, which combines the LSTM with Semivariogram Analysis. This model achieved the lowest error in predicting the timing of earthquakes.
5) EDA_3_baseline_plus_attention_model.ipynb: Explores the use of attention mechanisms to improve prediction accuracy over the baseline LSTM model.
6) EDA_4_baseline_plus_semivariogram_attention_model.ipynb: Combines both Semivariogram Analysis and attention mechanisms in an LSTM model to assess the additive impact of these methods on prediction accuracy.
7) Mapping of earthquakes with countries.ipynb: Maps each earthquake to a specific country, utilizing a GeoJSON file for geographic boundaries. The mapped dataset was used in the subsequent models to avoid recalculating this time-intensive step for each experiment.
8) README.md: Project documentation.

# Methodology
This project undertakes a one-step-ahead forecasting approach for predicting significant global earthquakes (magnitude 5.5+) using a combination of data science, time series analysis, and deep learning techniques. Below is a brief overview of the methodological stages:
  
1. **Data Extraction, Transformation, and Loading (ETL):**
   - **Data Source:** United States Geological Survey (USGS) dataset, focusing on significant earthquakes (magnitude 5.5+) from 1900 to 2023.
   - **Data Cleaning:** Excluded data prior to 1961 to mitigate the effect of limited seismic technology in earlier years. Outliers and countries with insufficient data were removed using Interquartile Range (IQR) analysis.
   - **Data Mapping:** Earthquakes were mapped to specific countries and tectonic plates using GeoJSON files. Earthquakes outside national boundaries were assigned to the nearest country, enabling spatial differentiation and better analysis of seismic activity patterns.
   - **Feature Engineering:**
     - Introduced a target variable, "counter," to track days until the next earthquake for each country.
     - Created cyclic features such as "day of the week" (with sine and cosine transformations) to capture temporal patterns.
     - Split the "time" feature into "year," "month," and "day" to improve model comprehension.
     - Engineered additional features, including average earthquake magnitude, magnitude difference, and earthquake count per country.
   - **Data Imputation and Consistency Maintenance:**
     - Gaps in time series were filled using kNN imputation to ensure a regular interval structure. Spatial imputation used the Haversine distance for accurate geographic adjustments.
     - Days with multiple earthquakes were handled by redistributing records within a 10-day window to maintain continuity, reducing missing data rates.
   - **Feature Transformation and Standardization:**
     - Applied log transformations and upper clipping to skewed features (e.g., depth, magnitude) to manage outliers. Standardization was applied to all features for consistent scaling during model training.
   - **Stationarity and Seasonality Checks:**
     - Confirmed time series stationarity using the Dickey-Fuller test.
     - Analyzed seasonality using additive decomposition, revealing a 91-day cyclic pattern, potentially useful for predictions.
   - **Autocorrelation Analysis:** Conducted ACF and PACF analyses to aid in configuring the ARIMA model parameters.
   - **Semivariogram Analysis:** Applied semivariogram analysis (globally, by tectonic plate, and by country) to capture spatial dependencies. Parameters like nugget, sill, and range were computed to enhance the model's understanding of spatial variability in earthquake data.

2. **Data Imputation and Temporal Structure**:
   - Filled gaps in time series to maintain regular intervals using kNN imputation, enabling the consistent temporal structure required by RNNs. For spatial features, Haversine distance was used to ensure geographic accuracy.

3. **Data Splitting**
   - Train-Validation-Test Split: Given the time series nature of the data, a temporal split was implemented to ensure that the model's training, validation, and testing phases reflect the most current conditions and trends in seismic activity.
   - The **most recent 20%** of the data was allocated as the test set.
   - The remaining **80%** of the data was split further, with **25%** used as the validation set and **60%** as the training set.
   - This split preserved the temporal structure, allowing for a realistic evaluation of model performance on unseen data.

4. **Time Series Modeling and Experimental Setup**:
   - **ARIMA Model**: Established a statistical baseline for comparison.
   - **LSTM-Based Models**: Developed various LSTM-based models with attention mechanisms and semivariogram analysis to capture spatial and temporal correlations.

5. **Evaluation and Hyperparameter Tuning**:
   - Performance was evaluated using MAE, while hyperparameter tuning was achieved through random search to optimize neuron counts, dropout rates, and learning rates.

6. **Error Analysis:**
   - To assess model reliability and generalization, we implemented two methods:
     - **Residual Distribution Analysis:** This technique checks for normal distribution and constant variance in residuals. Deviations from these properties indicate potential issues, such as non-linearity or the presence of outliers, providing insights into model weaknesses.
     - **Residuals vs Actual Values Scatter Plot:** This scatter plot examines the relationship between residuals and actual values, helping to identify patterns in prediction errors. It is especially useful for detecting heteroscedasticity, where residual variance increases with actual values, revealing areas where the model might struggle to maintain prediction accuracy.

7. **Feature Importance Analysis:**
   - We applied two methods to identify the most influential features in the model:
     - **SHAP (SHapley Additive exPlanations):** Based on cooperative game theory, SHAP values provide a robust measure of feature importance by calculating each feature’s contribution to model predictions. This approach is valuable for understanding feature interactions and contributions across complex datasets.
     - **Permutation Importance:** This method assesses the impact of each feature by randomly shuffling its values and observing the change in model accuracy, offering an intuitive measure of feature significance.
   - **Performance Degradation Curves:** To validate feature importance results, we used performance degradation curves. This approach sequentially neutralizes the top features (top 9 in our case) identified by each method and measures the cumulative impact on prediction error. We applied the Totally Random Time Series (TRTS) approach for neutralization, replacing each feature with random values to break any internal structure in the data. This technique allows for a comprehensive assessment of the extent to which the model relies on specific features' internal structure.

# Data Sources and Preprocessing
The earthquake data was sourced from the United States Geological Survey (USGS), including details on magnitude, depth, time, and location. The mapping of earthquakes to countries was done using Natural Earth GeoJSON files. For spatial correlation, Semivariogram parameters such as nugget, sill, and range were calculated and used as features in the RNN models.

# Results and Findings
The LSTM with Semivariogram Analysis achieved the best performance, with an MAE of 19.39 days, slightly outperforming the baseline ARIMA model, which had an MAE of 19.40 days. This result suggests that while the added complexity of RNNs provides some improvement, earthquake forecasting remains a challenging task due to the inherent randomness and unpredictability of seismic events.

# Full Thesis
For a detailed description of the research process, methodology, and analysis, refer to the full thesis in the PDF file: Tilburg_University_DSS_Masters_Thesis_Earthquake Forecasting_S2023.pdf.

# Dependencies
Python 3.11
TensorFlow 2.16.1
Keras 3.3.3
Keras Tuner 1.4.7
numpy 1.26.4
pandas 1.5.3
matplotlib 3.7.1
sklearn 1.3.0
shap 0.42.1
Please refer to the individual notebooks for further details on model architecture, tuning, and evaluation.
