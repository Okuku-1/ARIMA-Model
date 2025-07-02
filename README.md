# ARIMA-Model
# 📊 Time Series Analysis: Forecasting Kenya’s Bean Production Using ARIMA

This project involves modeling and forecasting bean production in Kenya using time series analysis techniques in **R**. My main objective was to develop an ARIMA model that can help in understanding and predicting future trends in bean production.

---

## 🎯 Objectives

### Main Objective
- To model bean production in Kenya using time series analysis.

### Specific Objectives
- To develop an ARIMA model.
- To estimate the model parameters.
- To forecast future bean production in Kenya.

---

## 📁 Step-by-Step Process

### 1. Data Cleaning
I began by cleaning the dataset to retain only the relevant columns: **Year** and **Value** (representing bean production). I also checked for missing values and confirmed the structure of the dataset.

### 2. Data Visualization
I visualized the time series data to understand any trends or seasonal patterns. The plot showed a visible upward and fluctuating trend, suggesting that the data was non-stationary.

### 3. Stationarity Check
To confirm whether the series was stationary, I used the **Augmented Dickey-Fuller (ADF) test**.

- The first test showed a **p-value > 0.05**, indicating that the series was not stationary.
- I then applied **first-order differencing** to the data to remove the trend.
- A second ADF test on the differenced series gave a **p-value < 0.05**, confirming that the series became stationary.

### 4. ACF and PACF Analysis
I plotted the **Autocorrelation Function (ACF)** and **Partial Autocorrelation Function (PACF)**:

- The **ACF** showed a gradual decline, reinforcing the need for differencing.
- The **PACF** cut off after lag 1, suggesting an **AR(1)** component might be appropriate.

These plots helped in the manual identification of potential ARIMA parameters.

### 5. ARIMA Model Selection
I used the `auto.arima()` function in R to automatically select the best model based on the lowest AIC value.

- Initially, auto.arima (without forcing differencing) selected **ARIMA(1,0,1)**.
- However, I had already confirmed non-stationarity and applied differencing.
- So, I ran `auto.arima()` with `d = 1`, and it selected the best model as **ARIMA(0,1,1)** with a **non-zero drift**.

The selected model had the following characteristics:
- MA(1) coefficient = -0.3754
- AIC = 719.23
- Residual variance = 6074

### 6. Residual Diagnostics

I conducted diagnostic checks to validate the model:

- **Ljung-Box Test**:
  - Null hypothesis: residuals are independently distributed.
  - p-value = 0.4429 → I failed to reject the null hypothesis.
  - Interpretation: residuals are not significantly autocorrelated.

- **Shapiro-Wilk Test**:
  - Null hypothesis: residuals are normally distributed.
  - p-value = 0.001655 → I rejected the null hypothesis.
  - Interpretation: residuals deviate from normality (common in large time series models, and often tolerable).

I also plotted the residuals to visually confirm white noise behavior, which looked satisfactory.

### 7. Forecasting

I used the fitted **ARIMA(0,1,1)** model to forecast the next **12 years** of bean production (`h = 12`).

- The forecast plot displayed expected production levels along with **80%** and **95% confidence intervals**.
- I observed an increasing trend in the point forecasts, though uncertainty increases with time.

---

## 📈 Key Takeaways

- The original time series was **non-stationary** and required **first-order differencing**.
- The **ARIMA(0,1,1)** model was selected as the best model based on AIC.
- Residual diagnostics confirmed **independence** but **slight deviation from normality**.
- The 12-step forecast provides valuable insight into expected future trends in bean production in Kenya.

---

## 🛠️ Tools Used

- **Language**: R
- **Libraries**: `forecast`, `tseries`, `ggplot2`, `readxl`, `tidyverse`, `pander`

---

## 👤 Author

This analysis was carried out by **Eddy Okuku** as part of a time series modeling exercise using R.

