# Time Series Project: Pollution Analysis in New Delhi
# Context
The primary aim of this project was to perform a time series forecast on pollution data from a specific locality (Rohini) within New Delhi, India. This project was motivated by a personal interest in environmental data analysis and its potential implications for understanding historical pollution levels, particularly focusing on Particulate Matter 2.5 (PM2.5). PM2.5 is a critical air pollutant due to its small size, which allows deep lung penetration and significant health impacts, making its analysis and forecasting highly relevant for environmental health departments.

# Actions & Techniques Applied
Data Acquisition and Initial Inspection:

The pollution dataset (DL024-Rohini.csv) was loaded into a pandas DataFrame.

Initial data inspection involved viewing the first few rows (rohini_data.head()) and checking data types and non-null counts (rohini_data.info()) to identify initial data quality issues.

Missing values for each column were quantified using isnull().sum().

# Data Cleaning & Preprocessing:

The dataset was filtered to focus on primary pollutants, creating a new DataFrame primary_pollutants containing 'Date', 'PM2.5 (ug/m3)', 'PM10 (ug/m3)', 'NO2 (ug/m3)', 'CO (mg/m3)', and 'SO2 (ug/m3)'.

The 'Date' column was converted to datetime objects using a specified format (%d/%m/%Y).

The 'Date' column was set as the DataFrame index to facilitate time series operations.

Missing values across all primary pollutant columns were imputed using a backward fill (fillna(method='bfill')) to ensure data continuity.

Time Series Resampling:

The data was resampled to daily averages (resample('D').mean()) to smooth out high-frequency noise and reveal underlying daily patterns.

Further resampling to monthly averages (resample('M').mean()) was performed to observe longer-term trends and prepare data for stationarity testing and modeling.

# Time Series Visualization:

Daily PM2.5 Trends: A line plot of daily average PM2.5 concentrations was generated, visualizing the fluctuations and overall patterns over the project's timeframe.


Monthly PM2.5 Trends: A line plot of monthly average PM2.5 concentrations was created to show a smoother representation of the pollution trends, highlighting seasonal patterns.


Contextual Markers: Both daily and monthly plots included:

A horizontal red dashed line representing the WHO (World Health Organization) safety threshold for annual mean PM2.5 (35μg/m 
3
 ).

Vertical green dotted lines indicating specific Diwali dates to observe the impact of festival-related emissions.

Vertical red dotted lines marking COVID-19 lockdown periods to analyze the effect of reduced anthropogenic activities.

# Stationarity Analysis:

Augmented Dickey-Fuller (ADF) Test: The ADF test was performed on the monthly average PM2.5 series to formally check for stationarity. The p-value obtained (0.5928) was greater than 0.05, leading to the conclusion that the time series was likely non-stationary, requiring differencing for forecasting models.

Autocorrelation (ACF) and Partial Autocorrelation (PACF) Plots: These plots were generated for the monthly PM2.5 series to identify patterns (e.g., seasonality, trend) and determine appropriate parameters for ARIMA/SARIMA models.


# Differencing:

To address non-stationarity, first-order differencing (.diff()) was applied to the monthly average PM2.5 data, creating a PM2.5_diff column. This transformation is a common step to achieve stationarity, which is required for many time series forecasting models.

# Results
Comprehensive Data Preparation: The project successfully demonstrated robust data cleaning, handling missing values, and transforming raw pollution data into a clean, time-indexed format suitable for advanced time series analysis.

Clear Pollution Trend Identification: Visualizations effectively highlighted the temporal patterns of PM2.5 pollution in New Delhi, revealing periods of significantly elevated pollution (often exceeding WHO guidelines) and demonstrating the discernible impact of specific events like Diwali and COVID-19 lockdowns on air quality.

Confirmed Non-Stationarity: Statistical testing (ADF test) confirmed the non-stationary nature of the PM2.5 time series, underscoring the necessity for differencing or other transformations for accurate forecasting.

Foundation for Forecasting: The ACF and PACF plots, combined with differencing, laid the groundwork for selecting appropriate ARIMA or Seasonal ARIMA (SARIMA) model parameters, indicating an understanding of correlation structures and guiding future forecasting efforts.

Insights into Environmental Impact: The analysis provided valuable insights into the fluctuating pollution levels and external factors influencing air quality in New Delhi, which could inform environmental policy and public health interventions.
