# Earthquake Forecasting Using Recurrent Neural Networks and Semivariogram Analysis
This repository contains the code and analysis for my master's thesis on forecasting significant global earthquakes (magnitude 5.5+) using Recurrent Neural Networks (RNNs) with enhancements such as Semivariogram Analysis and Attention Mechanisms.

# Project Overview
This thesis addresses the challenge of predicting the timing of major earthquakes by employing RNNs, specifically Long Short-Term Memory (LSTM) networks. The primary innovation in this research lies in integrating Semivariogram Analysis to capture spatial dependencies and using attention mechanisms to enhance predictive performance. The dataset spans from 1900 to 2023, with a focus on capturing spatio-temporal patterns to estimate the number of days until the next significant earthquake event.

# Files Overview
1) EDA_1_LSTM_baseline_model.ipynb: Contains exploratory data analysis (EDA) and the baseline LSTM model. This notebook includes all the EDA visuals and insights gained from preliminary analysis.

2) EDA_1_model_ARIMA.ipynb: Implements a simple ARIMA model as a statistical baseline to compare with the more complex deep learning approaches.

3) EDA_2_baseline_plus_semivariogram_model.ipynb: This notebook contains the best-performing model, which combines the LSTM with Semivariogram Analysis. This model achieved the lowest error in predicting the timing of earthquakes.

4) EDA_3_baseline_plus_attention_model.ipynb: Explores the use of attention mechanisms to improve prediction accuracy over the baseline LSTM model.

5) EDA_4_baseline_plus_semivariogram_attention_model.ipynb: Combines both Semivariogram Analysis and attention mechanisms in an LSTM model to assess the additive impact of these methods on prediction accuracy.

6) Mapping of earthquakes with countries.ipynb: Maps each earthquake to a specific country, utilizing a GeoJSON file for geographic boundaries. The mapped dataset was used in the subsequent models to avoid recalculating this time-intensive step for each experiment.

7) README.md: Project documentation.

# Methodology
The following models were employed in this study:

1) ARIMA Model: Used as a baseline for comparison.
2) LSTM Baseline: A simple LSTM model to capture temporal patterns in earthquake occurrences.
3) LSTM with Semivariogram Analysis: Incorporates Semivariogram Analysis to capture spatial dependencies alongside temporal patterns.
4) LSTM with Attention Mechanism: Adds an attention layer to the LSTM to improve focus on relevant parts of the sequence.
5) LSTM with Semivariogram and Attention Mechanism: Combines both Semivariogram Analysis and attention mechanisms for enhanced performance.

Each model was evaluated using the Mean Absolute Error (MAE) metric, with additional feature importance analysis performed on the best-performing model.

# Data Sources and Preprocessing
The earthquake data was sourced from the United States Geological Survey (USGS), including details on magnitude, depth, time, and location. The mapping of earthquakes to countries was done using Natural Earth GeoJSON files. For spatial correlation, Semivariogram parameters such as nugget, sill, and range were calculated and used as features in the RNN models.

# Results and Findings
The LSTM with Semivariogram Analysis achieved the best performance, with an MAE of 19.39 days, slightly outperforming the baseline ARIMA model, which had an MAE of 19.40 days. This result suggests that while the added complexity of RNNs provides some improvement, earthquake forecasting remains a challenging task due to the inherent randomness and unpredictability of seismic events.

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
