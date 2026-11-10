# Bike Sharing Demand Analysis

**An exploratory data analysis and statistical modelling project using Python**

## Project Overview

This project investigates the temporal and environmental factors associated with hourly bicycle rental demand using the UCI Bike Sharing Dataset, which contains records from the Capital Bikeshare system in Washington, DC, during 2011–2012.

The objective is to identify patterns in rental behaviour, investigate factors associated with demand, and evaluate the ability of statistical regression models to predict hourly bicycle rental counts.

Three regression models—Multiple Linear Regression, Poisson Regression, and Negative Binomial Regression—were developed and evaluated against a baseline model.

## Research Questions

1. How does bicycle rental demand vary throughout the day?
2. How is temperature associated with hourly bicycle rental demand?
3. How is season associated with bicycle rental demand?
4. Can statistical models reliably predict hourly bicycle rental counts?

## Dataset

**Source:** [UCI Bike Sharing Dataset](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset)

The dataset contains approximately 17,000 hourly observations from 2011–2012.

**Response variable:** `cnt` — total number of bicycle rentals per hour.

**Predictor variables:**

| Variable | Description |
|---|---|
| `temp` | Normalised temperature |
| `hum` | Normalised humidity |
| `windspeed` | Normalised wind speed |
| `hr` | Hour of the day |
| `workingday` | Working-day indicator |
| `season` | Season |
| `weathersit` | Weather conditions (available in the dataset, not included in the final regression models) |

## Methods

### 1. Exploratory Data Analysis

Exploratory analysis was conducted using pandas, Matplotlib and Seaborn to investigate:

- Average hourly bicycle rental demand.
- Differences between working and non-working days.
- The relationship between temperature and rental counts.
- Seasonal patterns in hourly bicycle rental demand.

Descriptive statistics, grouped averages, visualisations and Pearson correlation were used to investigate the relationships.

### 2. Statistical Modelling

Three regression models were fitted using the same predictors:

- **Multiple Linear Regression (OLS):** Used as an initial regression baseline.
- **Poisson Regression:** Used to model non-negative rental counts.
- **Negative Binomial Regression:** Used to accommodate overdispersion identified in the Poisson model.

The predictors were temperature, humidity, wind speed, hour of day, working-day status and season.

Categorical predictors were represented using indicator variables.

The dataset was divided chronologically into 80% training data and 20% testing data to evaluate predictions on later observations.

### 3. Model Diagnostics and Evaluation

Model assumptions were examined using:

- Residuals-versus-fitted-values plots.
- Q-Q plots of OLS residuals.
- Autocorrelation function (ACF) plots.
- Pearson dispersion statistic for Poisson regression.
- Estimated negative binomial overdispersion parameter.

Predictive accuracy was evaluated using:

- Mean Absolute Error (MAE).
- Root Mean Squared Error (RMSE).

All regression models were compared against a baseline predicting the historical training-set mean.

## Key Findings

### RQ1: Hourly Rental Demand

Bicycle rental demand exhibited two noticeable peaks, occurring around 8 AM and 5–6 PM.

Comparisons between working and non-working days revealed that these peaks were particularly apparent on working days, while non-working days exhibited a more pronounced midday peak.

These patterns are consistent with differences between commuting and recreational cycling, although rental purposes cannot be directly established from the dataset.

### RQ2: Temperature and Rental Demand

Temperature exhibited a moderate positive correlation with hourly bicycle rental demand (Pearson's r = 0.40).

Higher temperatures were generally associated with higher rental counts, although substantial variation remained.

This association does not establish causation, as other factors may influence both temperature patterns and rental demand.

### RQ3: Seasonal Variation

Hourly rental patterns were broadly consistent across seasons, with morning and evening demand peaks appearing throughout the year.

However, rental volumes differed by season. Autumn generally exhibited the highest average demand, while spring exhibited the lowest.

These differences suggest that seasonal factors may be relevant to bicycle rental demand beyond the observed relationship with temperature alone.

### RQ4: Predictive Modelling

All three regression models outperformed the baseline when evaluated using the held-out chronological testing dataset.

| Model | MAE | RMSE |
|---|---:|---:|
| Baseline | 174.98 | 232.61 |
| Multiple Linear Regression | 109.97 | 158.95 |
| Poisson Regression | **106.20** | 158.41 |
| Negative Binomial Regression | 107.27 | **157.32** |

Poisson regression achieved the lowest MAE, reducing prediction error by approximately **39.3%** relative to the baseline.

Negative binomial regression achieved the lowest RMSE, indicating slightly better performance when larger prediction errors are penalised more heavily.

However, differences between the three regression models were relatively small.

## Model Diagnostics

### Multiple Linear Regression

The OLS model achieved an R-squared of 0.633 on the training dataset.

Residual diagnostics identified:

- Heteroscedasticity, with residual variability increasing across fitted values.
- Departures from normality, particularly in the upper tail.
- Substantial positive residual autocorrelation.
- Negative fitted values, which are not meaningful for rental counts.

These findings indicate limitations in the assumptions and suitability of ordinary least squares for this dataset.

### Poisson Regression

Poisson regression exhibited substantial overdispersion, with a Pearson dispersion statistic of approximately 41.

This suggests that the variability in observed rental counts substantially exceeded that permitted by the fitted Poisson mean–variance relationship.

Despite this limitation, Poisson regression achieved the lowest test MAE.

### Negative Binomial Regression

Negative binomial regression estimated an overdispersion parameter of α = 0.3304 and achieved a substantially better training likelihood fit than Poisson regression.

However, Pearson residuals exhibited strong temporal autocorrelation, including pronounced correlations at approximately 1-hour and 24-hour lags.

This indicates that important time-dependent patterns remained unexplained.

## Limitations

Several limitations should be considered when interpreting the results.

1. **Temporal dependence:** Strong residual autocorrelation suggests that the regression models did not fully capture the time-dependent structure of rental demand.

2. **Distributional assumptions:** OLS exhibited heteroscedasticity and departures from normality, while Poisson regression showed substantial overdispersion.

3. **Historical dataset:** The data represent bicycle rentals in the Washington, DC area during 2011–2012, which limits generalisability to other periods and locations.

4. **Unobserved factors:** Events, changes in cycling infrastructure, and other unmeasured conditions may influence rental demand.

5. **Model evaluation:** Predictive performance was assessed using a single chronological testing period. Results may differ across other time periods.

6. **Forecasting assumptions:** Predictions use observed weather and calendar variables. Operational forecasting would require future values or forecasts of the relevant predictors.

## Conclusion

This project demonstrates that temporal and environmental factors provide useful information for predicting hourly bicycle rental demand.

All three statistical regression models substantially outperformed the historical-mean baseline, suggesting that modelling the relationship between rental demand and relevant predictors can improve predictive accuracy.

However, model diagnostics demonstrated that stronger predictive performance does not necessarily imply that a model adequately represents the statistical properties of the data.

Although negative binomial regression accommodated overdispersion more flexibly than Poisson regression, substantial temporal dependence remained.

Future work could explore interaction effects, lagged rental demand, and time-series modelling approaches to improve the representation of hourly demand patterns.

## Technologies Used

- **Python** — Data analysis and statistical modelling
- **pandas and NumPy** — Data processing and manipulation
- **Matplotlib and Seaborn** — Data visualisation
- **statsmodels** — Statistical regression and diagnostics
- **scikit-learn** — Predictive performance evaluation
- **Jupyter Notebook** — Interactive analysis
- **Git and GitHub** — Version control and project documentation

## Project Structure

`bike_sharing_demand_analysis/
│
├── data/
│   └── hour.csv
│
├── notebooks/
│   ├── 01_exploratory_analysis.ipynb
│   └── 02_regression_modelling.ipynb
│
├── figures/
│   ├── hourly_demand.png
│   ├── temperature_demand.png
│   └── model_comparison.png
│
├── README.md
├── requirements.txt
└── .gitignore

## Reproducing the Analysis

Clone the repository and navigate to the project folder.

Create a Python virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the required libraries:

```bash
pip install -r requirements.txt
```

Open the notebooks in VS Code or Jupyter and execute the cells in order:

1. `01_exploratory_analysis.ipynb` — Exploratory analysis and visualisations.
2. `02_regression_modelling.ipynb` — Statistical modelling, diagnostics and evaluation.

The UCI Bike Sharing Dataset must be available at `data/hour.csv`.

## Dataset Attribution

Fanaee-T, H., & Gama, J. (2014). *Event labeling combining ensemble detectors and background knowledge*. Progress in Artificial Intelligence, 2, 113–127.

Dataset available through the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset).