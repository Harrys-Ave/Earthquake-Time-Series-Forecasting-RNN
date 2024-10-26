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

1. **Data Extraction, Transformation, and Loading (ETL)**:
   - **Data Source**: United States Geological Survey (USGS) dataset, focusing on significant earthquakes from 1900 to 2023.
   - **Data Cleaning**: Excluded data pre-1961 to mitigate the effect of earlier limited seismic technology. Outliers and countries with insufficient data were removed using Interquartile Range (IQR) analysis.
   - **Data Mapping**: Mapped earthquakes to respective countries and tectonic plates using GeoJSON files. This step required spatial processing to assign earthquakes near national borders accurately.

2. **Feature Engineering**:
   - Calculated cyclic features such as "day of the week" and introduced a target variable, "counter," to track days until the next earthquake for each country.
   - Engineered additional features, including average earthquake magnitude, magnitude difference, and earthquake count per country.

3. **Data Imputation and Temporal Structure**:
   - Filled gaps in time series to maintain regular intervals using kNN imputation, enabling the consistent temporal structure required by RNNs. For spatial features, Haversine distance was used to ensure geographic accuracy.

4. **Time Series Modeling and Experimental Setup**:
   - **ARIMA Model**: Established a statistical baseline for comparison.
   - **LSTM-Based Models**: Developed various LSTM-based models with attention mechanisms and semivariogram analysis to capture spatial and temporal correlations.

5. **Evaluation and Hyperparameter Tuning**:
   - Performance was evaluated using MAE, while hyperparameter tuning was achieved through random search to optimize neuron counts, dropout rates, and learning rates.

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
