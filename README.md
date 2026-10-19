# Air Quality Index Prediction for Indian Cities

Exploratory analysis and model comparison for predicting the Air Quality Index (AQI) from pollutant readings across 26 Indian cities, 2015–2020. Term project for Virginia Tech's Certificate Program in Business Analytics and AI (Alexandria cohort, 2022), delivered with a global engineering association for the aerospace and automotive industries.

![Correlation heatmap of pollutants and AQI](figures/correlation-heatmap.png)

## Data

Hourly and daily air quality readings from monitoring stations in 26 cities, at two levels of aggregation (city and station) and two time grains (day and hour), plus a station reference table. The measured fields are PM2.5, PM10, NO, NO₂, NOx, NH₃, CO, SO₂, O₃, benzene, toluene, xylene, AQI and AQI bucket.

## Approach

1. **Exploratory analysis:** descriptive statistics, pollutant distributions, city rankings by pollutant and AQI over time.
2. **Cleaning:** dropped rows with no AQI (the target), and filled other missing values with column medians.
3. **Scaling:** standardized features with `StandardScaler`.
4. **Feature selection:** kept the pollutants most correlated with AQI: PM2.5, PM10, NO, NO₂, NOx, CO, SO₂ and O₃.
5. **Modeling:** compared linear regression, logistic regression, decision tree regressor, SVM and Gaussian Naive Bayes on all four datasets at 80/20, 70/30 and 60/40 splits.

## Findings

- **AQI is seasonal.** It peaks every winter.
- **Delhi and Ahmedabad are the most polluted cities in the data.** Ahmedabad has the highest mean AQI, and Delhi the highest PM2.5.
- **CO, NO₂, SO₂ and PM2.5 track AQI most closely.** CO has the strongest correlation, at 0.81.
- **Only the regressors fit well.** Linear regression and the decision tree regressor scored above 0.99 on every dataset and split. The classifiers didn't suit a continuous target, and logistic regression failed to converge.
- **Linear regression was chosen.** It matched the decision tree's score and trained in 3–4 seconds instead of about 60.

**A caveat on the near-perfect scores:** AQI is calculated from these same pollutant concentrations, so a model that predicts it from them is expected to fit almost perfectly. The value of the project is in the data cleaning, exploratory analysis and model comparison, not the headline score.

## Documentation

The full report, with every chart and the model score tables, is in [docs/report.md](docs/report.md).

Built in Python with pandas, scikit-learn, matplotlib and seaborn. The original notebook wasn't preserved, so this repository documents the analysis and results.
