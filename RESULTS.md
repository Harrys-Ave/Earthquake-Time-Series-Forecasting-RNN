# Results

This section presents the outcomes of the data preprocessing steps, model performance comparisons, and feature importance analysis on our earthquake prediction models. It includes the effects of feature transformations, model performance, hyperparameter tuning results, error analysis, and insights from the feature importance analysis.

## Data Preprocessing and Feature Transformation

During data preprocessing, log transformations were applied to right-skewed features, and upper clipping was applied to the depth, counter, and magnitude features, followed by standardization. These transformations resulted in:

- Slight skewness reduction for the **magnitude** feature.
- Notable distribution improvements for the **depth** and **counter** features.
- More symmetric and uniform distributions for both **magnitude** and **counter** features, enhancing model performance.

Scatter plots of key features versus the target feature showed that these transformations improved the uniform distribution of data points, reduced central clustering, and better represented variance.

## Model Performance Comparison

The table below summarizes the Mean Absolute Error (MAE) for each model, representing the prediction error in days.

| Model                            | Validation (MAE) | Test (MAE) |
|----------------------------------|------------------|------------|
| ARIMA (baseline)                 | 19.53           | 19.40      |
| LSTM                             | 19.59           | 19.61      |
| LSTM with Semivariogram Analysis | 19.57           | **19.39**      |
| LSTM with Attention Mechanism    | 19.61           | 19.40      |
| LSTM with Attention and Semivariogram | 19.53     | 19.41      |

**Observations:**
- The best-performing model was the **LSTM with Semivariogram Analysis**, achieving a minimal error difference of 0.01 days compared to the baseline model.
- Introducing attention mechanisms did not significantly enhance performance, as the **minimal MAE difference** between the baseline ARIMA model and the best-performing RNN model suggests limited predictive advantage from the added complexity.

## Hyperparameter Tuning Results

The table below provides the optimal hyperparameters identified for each model during the tuning process.

| Model                           | Parameter              | Best Value |
|---------------------------------|------------------------|------------|
| **ARIMA (baseline)**            
|                                  | p (Autoregressive Term) | 0          |
|                                 | d (Differencing Term)  | 0          |
|                                 | q (Moving Average Term)| 0          |
| **LSTM**                        
|                                  | LSTM Units             | 16         |
|                                 | L2 Regularization      | 0.01       |
|                                 | Learning Rate          | 0.0001     |
|                                 | Huber Delta            | 20         |
|                                 | Batch Size             | 32         |
| **LSTM with Semivariogram Analysis** 
|                                  | LSTM Units         | 64         |
|                                 | Dense Units            | 32         |
|                                 | L2 Regularization      | 0.0001     |
|                                 | Learning Rate          | 0.0001     |
|                                 | Huber Delta            | 20         |
|                                 | Batch Size             | 16         |
| **LSTM with Attention Mechanism** 
|                                  | LSTM Units (first layer) | 16    |
|                                 | L2 Regularization      | 0.0001     |
|                                 | Dropout Rate           | 0.2        |
|                                 | Learning Rate          | 0.0001     |
|                                 | Huber Delta            | 20         |
|                                 | Batch Size             | 16         |
| **LSTM with Attention and Semivariogram** 
|                                  | LSTM Units (first layer) | 64 |
|                                 | L2 Regularization      | 0.01       |
|                                 | Dropout Rate           | 0.1        |
|                                 | Learning Rate          | 0.0001     |
|                                 | Huber Delta            | 5          |
|                                 | Batch Size             | 16         |

**Observations:**
- For the **ARIMA model**, the baseline parameters (0,0,0) indicate a simple model, focusing on basic temporal dynamics.
- The **LSTM models** generally required a low learning rate (0.0001) and varying regularization values to balance performance and generalization.
- **Dropout rates** were introduced for attention mechanisms to avoid overfitting.
- **Lower learning rates** (0.0001) were consistently optimal, underscoring the need for gradual optimization.
- **Batch sizes** were smaller (16) for complex models, allowing more frequent parameter updates and improved generalization.

## Error Analysis

Error analysis was conducted on both validation and test sets. The best model showed a right-skewed residual distribution, with most residuals ranging between 0 and 20 days, indicating a reasonable level of accuracy. Key findings:

- **Residual Analysis:** Most residuals were concentrated around zero, signifying good accuracy in seismic activity timing predictions. Negative residuals indicate instances where the model underpredicted days until the next earthquake.
- **Heteroscedasticity:** Residuals increase with actual values, suggesting error variance grows with actual values. This indicates challenges in predicting earthquakes with long intervals, which may occur more randomly.

## Feature Importance Analysis

The feature importance analysis identified key predictors that influence model accuracy:

- **Top Features:** Interaction terms of each earthquake’s depth with the global "sill" and "range" of depth for that year were the most important features.
- **Global vs. Local Features:** Global features ranked higher in importance, emphasizing the role of global seismic patterns and correlations.
- **Permutation and SHAP Results:** Both methods aligned on the top features, but SHAP found categorical features like country and tectonic plate names to be important.

## Conclusion

This study demonstrated that integrating Semivariogram Analysis into LSTM networks can improve earthquake prediction accuracy. However, the complexity of RNN models does not always translate into significantly better results compared to simpler models like ARIMA, as observed in this dataset.

The feature importance analysis suggests that considering global spatial statistics and earthquake depth variability are crucial for improving predictive capabilities in earthquake forecasting models.
