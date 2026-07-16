# Predictive Fuel Management: Forecasting Indian Retail Petrol Prices

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1jue7cUbBisou_fT2Lobam8MyC5ng2b7c?usp=sharing)

An end-to-end time-series forecasting pipeline that predicts daily retail petrol prices in India and translates model forecasts into actionable, cost-saving inventory strategies for transportation fleets.

## 🚀 Business Impact

This forecasting framework moves transportation entities from reactive fuel procurement to proactive, strategic inventory management. By utilizing "jump risk" predictions and Just-in-Time (JIT) procurement based on model outputs, a simulated mid-sized transportation fleet (100 trucks) achieved:

* **Projected Savings:** Rs. 28.3L over a five-quarter period.
* **Profit Margin Gain:** 10.85% improvement through optimized bulk purchasing and advanced stockpiling during predicted administrative price-holds.

## 🧠 The Challenge: Policy-Driven Non-Stationarity

Indian retail petrol pricing presents a uniquely challenging econometric environment. It is a hybrid data-generating process where underlying economic trends (driven by global market fundamentals like Brent crude and exchange rates) are frequently superseded by discrete, deterministic government policy interventions, such as excise duty changes and politically motivated price freezes. 

Standard continuous-variation models fail here. This project successfully models this dual-regime environment using robust data normalization and probabilistic forecasting.

## ⚙️ Methodology & Architecture

### 1. Data Normalization
* Transformed heavily intervened, non-stationary raw price series into a stationary representation using log-returns.
* Implemented a rigorous walk-forward, one-step-ahead validation protocol to prevent data leakage.

### 2. The Production Model: LightGBM Quantile Regression
* **Why LightGBM?** Selected as the primary production model for its ability to generate highly calibrated 80% prediction intervals without the cumulative drift inherent in recursive deep learning models. 
* **Feature Engineering:** Utilized 21 lagged log-returns combined with rolling mean and standard deviation windows (7, 14, and 30 days).
* **Performance:** Achieved the narrowest Mean Prediction Interval Width (MPIW) with a Prediction Interval Coverage Probability (PICP) of 0.82, tightly aligning with the 80% target.

### 3. Deep Learning Ablation & Benchmarking
While LightGBM proved optimal for probabilistic calibration, several deep learning architectures were also implemented and benchmarked on the dataset to test the efficacy of gating mechanisms on short-range predictive signals:
* Gated Recurrent Unit (GRU)
* Long Short-Term Memory (LSTM)
* Temporal Convolutional Network (TCN)
* SimpleRNN

## 📂 Data Availability & Reproducibility

Due to data privacy and file size constraints, the raw daily pricing `.csv` dataset has been omitted from this repository. 

However, the complete data preprocessing pipeline, mathematical transformations, model training cycles, and evaluation metrics are fully reproducible in the cloud. Click the **"Open in Colab"** badge at the top of this document to view the executed Python environment.
