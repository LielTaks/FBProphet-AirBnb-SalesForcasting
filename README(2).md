# Short-Term Rental Price Forecasting with Prophet

A Python forecasting project that models short-term rental prices using Meta Prophet and property-level features. The notebook prepares listing data, handles missing values, trains two forecasting models with additional regressors, generates future nightly-price estimates, and visualizes forecast trends and uncertainty.

## Project Overview

Nightly rental prices vary with time and property characteristics. This project explores that relationship by combining a date-based forecasting model with features describing a listing's size and capacity.

Two Prophet models are developed:

| Model | Additional regressors | Complete training rows |
| --- | --- | ---: |
| Model 1 | Beds and bathrooms | 917 |
| Model 2 | Bedrooms and guest capacity (`accommodates`) | 1,013 |

Both models forecast `price_quote_price_per_night` over a 365-day future horizon. Future regressor values are estimated from historical monthly averages and converted into whole-property values before prediction.

## Skills Demonstrated

- Data preparation and missing-value handling with pandas
- Datetime conversion and feature selection
- Time-series forecasting with Meta Prophet
- Incorporating external regressors into forecasting models
- Feature engineering from monthly historical averages
- Forecast and component visualization
- Comparing alternative model specifications

## Dataset

The notebook expects a `listings.csv` file containing short-term rental listing and price-quote information.

| Property | Description |
| --- | --- |
| Raw records | 1,492 listings |
| Forecast date | `price_quote_checkin_date` |
| Forecast target | `price_quote_price_per_night` |
| Model 1 features | `beds`, `bathrooms` |
| Model 2 features | `bedrooms`, `accommodates` |
| Other available data | Listing, host, location, availability, review, and booking attributes |

> The source CSV is not included in this repository. Use data you are authorized to access and document its source and licensing terms before publishing it.

## Methodology

1. Load the listing data with pandas.
2. Convert check-in dates to pandas datetime values.
3. Select the target and regressors for each model.
4. Remove records with missing values in the selected fields.
5. Rename the date and target columns to Prophet's required `ds` and `y` schema.
6. Fit Prophet with the selected property regressors.
7. Create a 365-day future date frame.
8. Estimate future regressors using historical averages grouped by calendar month.
9. Round the estimated property attributes to practical whole-number values.
10. Generate predictions and visualize the forecast and its components.

## Repository Structure

```text
.
├── Homework.ipynb       # Data preparation, Prophet models, and visualizations
└── README.md            # Project documentation
```

For a polished portfolio repository, rename the notebook to `rental_price_forecasting.ipynb` and update the command below accordingly.

## Technologies

- Python 3
- Jupyter Notebook or Google Colab
- pandas
- NumPy
- Prophet
- scikit-learn
- Matplotlib, through Prophet's plotting interface

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/oluwatimilehintomoloju/short-term-rental-price-forecasting.git
cd short-term-rental-price-forecasting
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows:

```powershell
.venv\Scripts\activate
```

### 3. Install the dependencies

```bash
pip install pandas numpy prophet scikit-learn notebook
```

### 4. Add the dataset

Create a `data` directory and place the CSV inside it:

```text
data/listings.csv
```

Replace the Google Colab path in the notebook:

```python
df = pd.read_csv("/content/listings.csv")
```

with the repository-relative path:

```python
df = pd.read_csv("data/listings.csv")
```

### 5. Run the analysis

```bash
jupyter notebook Homework.ipynb
```

Run the cells in order to reproduce both forecasting workflows.

## Forecast Output

Prophet produces the following core estimates:

- `yhat` — predicted nightly price
- `yhat_lower` — lower uncertainty bound
- `yhat_upper` — upper uncertainty bound
- Overall forecast plots showing historical observations and future estimates
- Component plots showing the fitted trend and seasonal patterns

The current notebook is an exploratory forecasting study. It does not yet report out-of-sample error metrics or prove that one regressor set performs better than the other.

## Limitations and Future Improvements

- Use a chronological train, validation, and test split.
- Compare the models with MAE, RMSE, and MAPE.
- Add a simple baseline, such as a historical or seasonal average.
- Evaluate the two regressor sets on the same complete-case sample.
- Avoid rounding aggregate future regressors by forecasting explicit property scenarios instead.
- Tune Prophet's changepoints, seasonality, and holiday effects.
- Add location, room type, review score, and availability features where appropriate.
- Investigate price outliers and apply a transformation when justified.
- Add a reproducible `requirements.txt` with pinned versions.
- Save portfolio-ready forecast charts in an `images` directory.
- Rename `Homework.ipynb` to a descriptive project filename.

## Portfolio Summary

> Developed two multivariate Prophet forecasting models for short-term rental prices using Python. Cleaned and transformed 1,492 listing records, incorporated property-capacity regressors, engineered future features from monthly patterns, and generated 365-day forecasts with trend and uncertainty visualizations.

## Disclaimer

This project is for educational and analytical purposes only. Forecasts are estimates based on the available data and modeling assumptions; they should not be treated as guaranteed rental income, valuation advice, or business recommendations.

## Author

**Oluwatimilehin Tomoloju**

- GitHub: [@oluwatimilehintomoloju](https://github.com/oluwatimilehintomoloju)

## License

No license has been specified. Unless a license is added, all rights are reserved by the repository owner. The underlying listing data remains subject to its provider's terms and licensing requirements.
