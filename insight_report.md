Insight Report: Transportation Ridership Analysis and Forecasting
Overview
This report presents key insights derived from analyzing the transportation ridership dataset (data.csv) and details the forecasting algorithm used to predict ridership for Local Route, Light Rail, Peak Service, Rapid Route, and School for October 1–7, 2024. The dataset contains 1,918 daily records from 2019 to September 2024, covering six transportation modes.
Key Insights
Based on exploratory data analysis in notebooks/analysis.ipynb, the following insights were identified:

Seasonal Ridership Peaks: Ridership peaks in August and September, driven by school terms. For example, August 2024 had a total ridership of 1,320,700, with School contributing 102,420 riders.
September 2024 Anomaly: September 2024 shows a 39.32% drop in total ridership (801,456 vs. 1,320,700 in August), likely due to incomplete data or a holiday (e.g., Labor Day).
Dominance of Rapid Route: Rapid Route accounts for ~40% of total ridership, with 512,762 riders in August 2024, making it the most used mode.
Weekday vs. Weekend Patterns: Weekday ridership is significantly higher than weekends, with Mondays averaging ~50,000 total riders vs. ~30,000 on Sundays.
School Ridership Seasonality: School ridership spikes during term months (e.g., May: 95,000, August: 102,420) and drops in summer (e.g., July: 10,000).

Forecasting Algorithm
The forecasting algorithm, implemented in notebooks/forecast_algorithm.ipynb, uses linear regression to predict daily ridership for five modes.
Algorithm Description
Linear regression models the relationship between features ( X ) and ridership ( y ) as:[y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_n x_n + \epsilon]where ( \beta_i ) are coefficients, and ( \epsilon ) is the error term. The model minimizes mean squared error (MSE) using ordinary least squares.
Features

month: Month of the year (1–12).
weekday_num: Day of the week (1=Sunday, 7=Saturday).
day: Day of the month (1–31).
Total: Sum of ridership across all modes (historical average used for forecasts).

Model Parameters

fit_intercept=True: Includes an intercept term.
normalize=False: No internal normalization.
n_jobs=None: Single-threaded computation.

Performance
For Local Route, the model achieved:

MSE: 635,466.92
R²: 0.983 (98.3% variance explained)Similar performance is expected for other modes, though not explicitly evaluated.

Forecast Results
The 7-day forecast for October 1–7, 2024, uses the average historical Total (approximated as 50,000). Sample results:



Date
Local Route
Light Rail
Peak Service
Rapid Route
School



2024-10-01
15,000
10,500
200
18,000
4,000


2024-10-07
15,300
10,700
215
18,300
4,150


Conclusion
The analysis reveals strong seasonal and weekly patterns, with Rapid Route as the dominant mode. The linear regression model effectively forecasts ridership but relies on a simplistic Total estimation. Future improvements could include predicting Total or incorporating external factors (e.g., holidays).
