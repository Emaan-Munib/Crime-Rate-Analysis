# Mass Shooting & Chicago Crime Data Forecasting

This project scrapes mass shooting data from [Gun Violence Archive](https://www.gunviolencearchive.org/mass-shooting), retrieves crime data from Chicago's public data API, and performs time series forecasting using ARIMA and Prophet models.

## 🔍 Overview

- Scrapes up to 5000 rows of mass shooting data from multiple pages.
- Downloads recent crime data from the City of Chicago Open Data portal.
- Processes and forecasts:
  - Number of victims killed (ARIMA)
  - Number of victims injured (Prophet)
- Generates interactive time-series visualizations.
- Prompts user input for specific city and forecast horizon.

## ⚙️ Requirements

- Python 3.x
- pandas
- numpy
- requests
- BeautifulSoup4
- statsmodels
- prophet
- plotly

Install the dependencies:

```bash
pip install pandas numpy requests beautifulsoup4 statsmodels prophet plotly
```

## 🚀 Running the Project

1. Open and run the notebook: `Crime_Rate_Analysis.ipynb`
2. It will:
   - Scrape incident data from Gun Violence Archive
   - Download recent crimes from Chicago
   - Save both as `incident_dataset.csv` and `chicago_crime_data.csv`
3. You’ll be asked:
   - To enter a city name (or leave blank for all cities)
   - The number of days you want to forecast
4. The notebook will display forecasts using:
   - **ARIMA** for victims killed
   - **Prophet** for victims injured

## 📁 Output Files

- `incident_dataset.csv`: Contains mass shooting data
- `chicago_crime_data.csv`: Contains crime data for Chicago

## 📈 Forecast Models

- **ARIMA** (AutoRegressive Integrated Moving Average): For predicting fatality counts.
- **Prophet**: For predicting injury counts.

## 📌 Notes

- The scraper assumes consistent table formatting on the Gun Violence Archive site.
- Internet connection is required during execution.