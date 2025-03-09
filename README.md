# Time Series Interpolation for Missing Data

## Project Overview

This project focuses on the interpolation of missing values in time series data. We are given 1,000 incomplete time series with missing values, and the objective is to develop a machine learning algorithm capable of accurately predicting these missing values. Additionally, we have 68,000 fully observed time series that we can use as exogenous variables to help improve the model's accuracy.

## Dataset

- **Incomplete Time Series**: 1,000 series with missing values.
- **Complete Time Series**: 68,000 series that are fully observed and assumed to follow the same distribution as the incomplete series.
- **Time Interval**: 30-minute frequency.
- **Temporal Index**: Time-indexed data.

## Data Exploration

- We analyzed the correlation and autocorrelation between series to understand their relationships and identify potential patterns such as seasonality or stationarity.
- Four classes of missing data sequences were identified, which helped guide the choice of interpolation methods.

## Interpolation Models

### 1. **Low-Rank Adaptation**
- A matrix decomposition approach based on singular value decomposition (SVD) for interpolating missing values.
- Performs well for sequences with moderate lengths of missing data, but struggles with longer gaps.
- **MAE**: 179.

### 2. **Auto-Regressive Model (AR)**
- A statistical model used to predict missing values based on past values of the same time series.
- Effective for interpolating long sequences but fails on shorter gaps.
- **MAE**: 220.

### 3. **Vector Auto-Regressive Model (VAR)**
- An extension of the AR model that incorporates exogenous time series data to improve predictions.
- Reduces errors on long missing sequences but can produce extreme values for shorter sequences.
- **MAE**: 83.3 (significant improvement over previous models).

### 4. **Decision Tree Interpolation (Coming Soon)**

## Benchmark and Comparison

- We benchmarked the performance of our models against **Linear Interpolation** and **Cubic Spline Interpolation**.
- **Linear Interpolation MAE**: 107.78.
- **Cubic Spline MAE**: 29,038.16.

## Key Findings

- The VAR model, which utilizes complete time series as features, significantly outperforms the simpler models in terms of interpolation accuracy.
- The main limitation of all models is the instability of the time series, as many are non-stationary, which complicates accurate forecasting.
- A hybrid approach (combining linear interpolation for short gaps and VAR for longer gaps) did not significantly improve performance.

## Installation

To use this project locally, clone the repository and install the dependencies:

```bash
git clone https://github.com/yourusername/timeseries-interpolation.git
cd timeseries-interpolation
pip install -r requirements.txt
```

## Usage

Run the main script to start interpolation:

```bash
python interpolate.py
```

## Future Work

- Test additional machine learning models such as decision trees and neural networks for interpolation.
- Explore more sophisticated hybrid models combining statistical and machine learning techniques.
