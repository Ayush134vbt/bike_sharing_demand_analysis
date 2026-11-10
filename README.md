# Bike Sharing Demand Analysis

## Project Overview

This project investigates factors associated with hourly bicycle rental demand using the UCI Bike Sharing Dataset, which contains records from the Capital Bikeshare system in Washington, DC, during 2011–2012.

The project aims to identify patterns in bicycle rental demand, explore relationships with environmental and temporal factors, and evaluate statistical models for predicting hourly rental counts.

## Research Questions

1. How does bicycle rental demand vary throughout the day?
2. How is temperature associated with hourly bicycle rental demand?
3. How is season associated with bicycle rental demand?
4. How accurately can statistical models predict hourly bicycle rental counts?

## Dataset

**Source:** [UCI Bike Sharing Dataset](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset)

**Response Variable:** `cnt` — total number of bicycles rented per hour.

**Potential Predictors:**
- `temp` — Normalised temperature
- `hum` — Normalised humidity
- `windspeed` — Normalised wind speed
- `hr` — Hour of the day
- `workingday` — Working-day indicator
- `weathersit` — Weather conditions
- `season` — Season

## Methods

### Exploratory Data Analysis
- Descriptive statistics and data quality checks
- Hourly rental demand visualisation
- Working-day versus non-working-day comparisons
- Temperature and weather comparisons

### Statistical Modelling
- Multiple linear regression
- Poisson regression
- Negative binomial regression

### Model Evaluation
- Model diagnostics and assumption checking
- Chronological training and testing split
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)

## Tools

- Python
- pandas and NumPy
- Matplotlib and Seaborn
- statsmodels
- scikit-learn
- Git and GitHub




## Findings

### RQ1: Hourly Rental Patterns

Average hourly bicycle rental demand exhibits two distinct peaks, occurring around 8 AM and 5–6 PM. These patterns are consistent with commuting behaviour, particularly because the peaks are more pronounced on working days. However, the dataset does not directly identify individuals' reasons for renting bicycles.

**Key Finding:** Bicycle rental demand varies considerably throughout the day, with the highest average demand occurring during typical commuting hours.

### RQ2: Temperature and Rental Demand
...

### RQ3: Weather Conditions and Rental Demand
...

### RQ4: Predictive Model Performance
...



## Limitations

*To be completed following model evaluation.*

## Conclusion

*To be completed after interpreting the findings.*