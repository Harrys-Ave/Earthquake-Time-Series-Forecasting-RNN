# Research Questions and Answers

This document provides an overview of the main research questions explored in this thesis on forecasting significant global earthquakes using Recurrent Neural Networks (RNNs) enhanced with Semivariogram Analysis, along with the answers derived from the study.

## Main Research Question (RQ)

**RQ**: To what extent can recurrent neural networks, enhanced with Semivariogram Analysis, forecast significant earthquakes within days using a global dataset?

**Answer**: The LSTM with Semivariogram Analysis was the best-performing model, achieving a Mean Absolute Error (MAE) of 19.39 days, slightly outperforming the ARIMA baseline (MAE: 19.40 days). This minor improvement suggests that Semivariogram Analysis aids in capturing spatial correlations, although the inherent randomness of seismic events limits substantial gains in accuracy. The results imply that while Semivariogram Analysis can slightly enhance predictive power, further advances may require more sophisticated methods or additional data.

## Sub-questions

### RQ1: Model Performance Comparison

**RQ1**: How does the performance of the ARIMA model and LSTM networks, including those enhanced with Semivariogram Analysis and attention mechanisms, compare in forecasting significant global earthquakes, in terms of Median Absolute Error (MAE)?

**Answer**: The LSTM with Semivariogram Analysis achieved the lowest MAE (19.39 days), closely followed by the ARIMA baseline (19.40 days). Attention mechanisms provided slight improvements in some LSTM models but did not outperform the Semivariogram-enhanced LSTM. The minimal differences in MAE highlight that, for this dataset, the added complexity of RNNs yields limited gains over simpler statistical models like ARIMA.

### RQ2: Feature Importance

**RQ2**: What is the relative importance of various features in the predictive performance of the best-performing model, as determined through the Permutation Importance method and SHAP (SHapley Additive exPlanations) method?

**Answer**: Feature importance analysis revealed that interactions between earthquake depth and global spatial statistics (e.g., global sill and range of depth) were the most critical for prediction. The categorical features of country and tectonic plate were also significant. This highlights the importance of spatial statistics and suggests that earthquake depth and its global variance are key factors in forecasting seismic events.

## Summary and Insights

1. **Best Model**: The LSTM with Semivariogram Analysis model slightly outperformed the ARIMA model, demonstrating that spatial correlation offers some predictive advantage, though modest.
2. **Impact of Attention Mechanisms**: Attention mechanisms provided limited additional value for this dataset, as they did not outperform the Semivariogram-enhanced LSTM.
3. **Key Features for Prediction**: Earthquake depth and its global variability (captured through spatial statistics) emerged as essential features, underlining the importance of spatio-temporal factors in earthquake prediction.
