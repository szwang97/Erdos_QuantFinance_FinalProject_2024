# Optiver – Trading at the Close

**Authors**: Zilu Ma, Shaozong Wang

## Introduction

This project is part of the Kaggle competition hosted by Optiver, focusing on predicting US stock closing movements. We use auction data provided through an API by Optiver, analyzing time series data for 200 stocks. Each stock data point includes 13 features, such as ask/bid prices and sizes, and weighted average price (wap).

The primary objective is to predict the 60-second future movement of a stock's wap, relative to the synthetic index movement. The prediction targets are calculated as follows:

$$
Target = \left( \frac{StockWAP_{t+60}}{StockWAP_t} \right) - \left( \frac{IndexWAP_{t+60}}{IndexWAP_t} \right)
$$

Submissions are evaluated based on the Mean Absolute Error (MAE) between the predicted and observed movements.

## Approach

Our approach involves generating an extensive set of features with financial significance. These include imbalances, price differentials, statistics on prices and sizes, discrete derivatives, and rolling averages.

Due to the manageable size of features, our primary models are gradient boosting trees, utilizing robust libraries like XGBoost, CatBoost, and LightGBM. We have found that the models' sensitivity to hyperparameters like learning rates is minimal, with significant improvements in model performance after feature augmentation.

## Results

Our experiments led to various findings:

- Enhanced feature engineering significantly improved model accuracy.
- XGBoost models were faster but generally exhibited higher loss compared to CatBoost models, which performed better in noisy data conditions.
- An ensemble approach, combining CatBoost and XGBoost, yielded the best results.

### Model Performance Summary

| Model                           | # of Features | Learning Rate | Validation Loss | Submission Loss |
|---------------------------------|---------------|---------------|-----------------|-----------------|
| CatBoost                        | 106           | 0.005         | 5.89            | 5.99            |
| CatBoost                        | 106           | 0.05          | 5.86            | 6.21            |
| CatBoost                        | 128           | 0.005         | 5.89            | 5.58            |
| CatBoost                        | 138           | 0.005         | 5.89            | 5.60            |
| XGBoost                         | 128           | 0.05          | 5.986           | -               |
| XGBoost                         | 138           | 0.05          | 5.986           | -               |
| Ensemble (0.7×CatBoost+0.3×XGB) | 138           | 0.005, 0.05   | 5.90            | 5.53            |

## Acknowledgements

- Optiver for hosting the Kaggle competition and providing the dataset.
- The Kaggle community for insights and discussions.

