# Results Summary

This file provides a summary of the results, including Mean Absolute Error (MAE) scores for each model and the optimal hyperparameters selected during tuning.

## 1. Model Performance Comparison (MAE Scores)

| Model                               | MAE (Validation) | MAE (Test) |
|-------------------------------------|------------------|------------|
| ARIMA Baseline                      | 19.53 days      | 19.40 days |
| LSTM Baseline                       | 19.59 days      | 19.61 days |
| LSTM with Semivariogram Analysis    | 19.57 days      | **19.39 days** |
| LSTM with Attention Mechanism       | 19.61 days      | 19.40 days |
| LSTM with Semivariogram + Attention | 19.53 days      | 19.41 days |

*Note: The best-performing model is the LSTM with Semivariogram Analysis, which achieved the lowest MAE on the test set.*

## 2. Hyperparameter Tuning Results

The table below summarizes the optimal hyperparameters identified during tuning for each model.

| Model                               | LSTM Units | Dense Units | Learning Rate | Dropout Rate | Batch Size | Huber Delta | Regularization |
|-------------------------------------|------------|-------------|---------------|--------------|------------|-------------|----------------|
| LSTM Baseline                       | 16         | -           | 0.0001        | -            | 32         | 20          | 0.01           |
| LSTM with Semivariogram             | 64         | 32          | 0.0001        | -            | 16         | 20          | 0.0001         |
| LSTM with Attention                 | 16         | -           | 0.0001        | 0.2          | 16         | 20          | 0.0001         |
| LSTM with Semivariogram + Attention | 64         | -           | 0.0001        | 0.1          | 16         | 5           | 0.01           |

## 3. Insights and Observations

- **Best Model**: The LSTM with Semivariogram Analysis performed slightly better than the ARIMA model, highlighting the added value of spatial correlation.
- **Impact of Attention Mechanisms**: While attention mechanisms showed a slight improvement over the baseline LSTM, they did not outperform the Semivariogram-enhanced model significantly.
- **Optimal Hyperparameters**: The tuning process highlighted the importance of lower learning rates and smaller batch sizes for models incorporating Semivariogram Analysis and attention.
