
# Crime Data Analysis, Hotspot Detection & Time-Series Forecasting

**Python | Machine Learning | Geospatial Analytics | ARIMA | Prophet | Power BI**

An end-to-end data analytics and machine learning project focused on analyzing crime patterns, identifying geographical hotspots, and forecasting gun violence trends across the United States.

The project combines **web scraping, public API integration, exploratory data analysis (EDA), machine learning, time-series forecasting, geospatial clustering, and interactive business intelligence dashboards** to transform crime data into meaningful insights.

It utilizes mass shooting records from the **Gun Violence Archive** and crime reports from the **Chicago Open Data Portal**.

---

## Project Highlights

- **Automated Data Collection:** Scrapes up to 5,000 mass shooting records from Gun Violence Archive.
- **API Integration:** Retrieves Chicago crime records through the City of Chicago Open Data API.
- **Crime Trend Analysis:** Explores geographical distributions, historical trends, and victim statistics.
- **Time-Series Forecasting:** Implements ARIMA and Prophet to forecast fatalities and injuries.
- **Geospatial Hotspot Detection:** Applies DBSCAN clustering to identify areas with concentrated gun-related incidents.
- **Machine Learning Classification:** Explores Logistic Regression, Decision Tree, and SVM for incident severity classification.
- **Interactive Visualizations:** Uses Plotly and Folium to visualize crime trends and geographical patterns.
- **Power BI Dashboard:** Includes a dedicated report for additional crime data analysis.

---

## Technologies Used

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Data Manipulation | Pandas, NumPy |
| Web Scraping | Requests, BeautifulSoup |
| Data Collection | Chicago Open Data API |
| Machine Learning | Scikit-learn |
| Time-Series Forecasting | ARIMA, Prophet |
| Geospatial Analysis | DBSCAN, Folium |
| Data Visualization | Matplotlib, Seaborn, Plotly |
| Business Intelligence | Microsoft Power BI |
| Development Environment | Jupyter Notebook |

---

## Datasets

### 1. Gun Violence Archive

**Source:** [Gun Violence Archive — Mass Shootings](https://www.gunviolencearchive.org/mass-shooting)

The project collects mass shooting incident data from multiple pages of the Gun Violence Archive website.

The scraping process is configured to retrieve up to **5,000 records**, depending on website accessibility and available data.

The dataset includes information such as:

- Incident date
- State
- City or county
- Number of victims killed
- Number of victims injured
- Incident information

**Output file:** `incident_dataset.csv`

This dataset supports exploratory analysis and time-series forecasting of shooting-related fatalities and injuries.

### 2. Chicago Crime Data

**Source:** [Chicago Open Data Portal](https://data.cityofchicago.org/)

The project retrieves crime records through Chicago's public Socrata API.

The implemented request retrieves up to **10,000 records** dated after January 1, 2023, ordered by date.

Relevant attributes include:

- Incident date
- Crime type and description
- Location information
- Latitude and longitude
- Arrest status
- District and community area

**Output file:** `chicago_crime_data.csv`

The Chicago dataset is used for geographical analysis and hotspot detection.

**Note:** The Gun Violence Archive and Chicago datasets are analyzed separately rather than combined into a single forecasting model.

---

## Project Architecture

```text
                 Crime Data Sources
                         |
          +--------------+--------------+
          |                             |
   Gun Violence Archive          Chicago Open Data
          |                             |
      Web Scraping                  REST API
          |                             |
     Data Cleaning                Data Cleaning
          |                             |
   Exploratory Analysis          Gun Crime Filtering
          |                             |
   Time-Series Analysis           DBSCAN Clustering
          |                             |
     +----+----+                  Hotspot Detection
     |         |                        |
   ARIMA     Prophet                Folium Maps
     |         |
  Fatality   Injury
  Forecast   Forecast
     |         |
     +----+----+
          |
    Plotly Visualizations

        Additional Analytics
                 |
       Classification Models
                 |
        Power BI Dashboard
```

---

## 1. Data Collection and Preprocessing

### Web Scraping

The project uses Python's `requests` and `BeautifulSoup` libraries to extract incident records from paginated Gun Violence Archive tables.

The scraping workflow includes:

1. Sending HTTP requests to the source website.
2. Parsing HTML tables.
3. Extracting relevant incident attributes.
4. Combining records from multiple pages.
5. Converting the extracted information into a Pandas DataFrame.
6. Exporting the dataset to CSV.

### Chicago Crime API Integration

Crime records are retrieved from the City of Chicago's public data API.

The collected records are processed to support geographical and crime-pattern analysis.

### Data Preprocessing

The project performs data preparation tasks including:

- Date conversion and formatting
- Missing-value inspection
- Numeric data conversion
- Incident filtering
- Time-series aggregation
- Geographic coordinate preparation

These operations prepare the datasets for forecasting, clustering, and visualization.

---

## 2. Exploratory Data Analysis (EDA)

Exploratory analysis is used to understand patterns and distributions within the crime datasets.

### Visualizations

The project includes:

- Incident distributions across states
- Temporal crime trends
- Fatality and injury statistics
- Correlation analysis
- Interactive time-series charts
- Three-dimensional comparisons

**Libraries:** Pandas, Matplotlib, Seaborn, and Plotly.

### Objectives

The analysis explores:

- How shooting incidents vary geographically
- Changes in incidents over time
- Patterns in reported fatalities and injuries
- Relationships between incident attributes
- Areas requiring further geographical investigation

---

## 3. Time-Series Forecasting

The forecasting component uses historical Gun Violence Archive incident data to estimate future fatality and injury counts.

Users can specify a city and the number of days to forecast.

### ARIMA — Fatality Forecasting

**Model:** AutoRegressive Integrated Moving Average

**Configuration:** `ARIMA(5,1,0)`

ARIMA models historical temporal patterns to generate forecasts for the number of victims killed.

The workflow includes:

1. Filtering incident data by the selected city.
2. Converting dates into a time-series index.
3. Aggregating fatality counts.
4. Fitting the ARIMA model.
5. Generating forecasts for the requested horizon.
6. Visualizing historical and predicted values.

### Prophet — Injury Forecasting

**Model:** Prophet

Prophet is used to forecast the number of victims injured.

The workflow includes:

1. Preparing date and injury-count columns.
2. Aggregating historical observations.
3. Fitting the Prophet forecasting model.
4. Creating future date periods.
5. Generating predictions.
6. Visualizing historical observations and forecasts.

### Interactive Forecasting

The notebook accepts user input for:

- **City:** A specific city or all available cities
- **Forecast Horizon:** Number of future days

Forecasts are displayed using interactive visualizations.

**Important:** These forecasts are statistical estimates based on historical observations. They should not be interpreted as reliable predictions of individual future violent incidents.

---

## 4. Geospatial Crime Hotspot Detection

The project applies **DBSCAN (Density-Based Spatial Clustering of Applications with Noise)** to identify geographical concentrations of gun-related incidents in Chicago.

### Methodology

1. Load Chicago crime records.
2. Filter crime descriptions containing `GUN`.
3. Extract valid latitude and longitude coordinates.
4. Convert geographical coordinates into radians.
5. Apply DBSCAN using haversine distance.
6. Assign cluster labels to incidents.
7. Visualize geographical clusters using Folium.

### DBSCAN

DBSCAN is an unsupervised machine learning algorithm that groups observations based on spatial density.

It is useful for geographical analysis because it:

- Does not require specifying the number of clusters in advance.
- Can identify irregularly shaped clusters.
- Distinguishes clustered observations from noise.
- Supports geographical hotspot exploration.

### Geographic Distance Configuration

The notebook uses haversine distance with an `eps` value of `0.01`.

Since haversine distance is measured in radians, this corresponds to approximately **63.7 km**, rather than 1 km.

For a 1 km neighborhood radius, the parameter should instead be calculated using:

```python
eps = 1 / 6371.0088
```

where `6371.0088` represents Earth's approximate mean radius in kilometers.

The clustering radius should be reviewed before interpreting the resulting clusters as neighborhood-scale crime hotspots.

### Folium Visualization

The detected clusters are displayed on interactive geographical maps.

These visualizations help explore the spatial distribution of gun-related crime records.

---

## 5. Machine Learning Classification

The project also explores supervised machine learning approaches for incident severity classification.

### Algorithms

- Logistic Regression
- Decision Tree Classifier
- Support Vector Machine (SVM)

These models provide an additional analytical approach alongside forecasting and geographical clustering.

Classification performance should be assessed using appropriate evaluation metrics, such as:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix

The classification experiments are separate from the ARIMA and Prophet forecasting pipelines.

---

## 6. Power BI Dashboard

The repository includes a Microsoft Power BI report:

`crime_analysis_powerbi.pbix`

The report complements the Python-based analysis by providing a business intelligence environment for exploring crime-related data.

### Power BI Integration

Power BI can be used to:

- Explore crime distributions
- Compare geographical areas
- Analyze historical trends
- Filter crime records
- Present analytical findings through interactive reports

### Opening the Dashboard

1. Install Microsoft Power BI Desktop.
2. Download `crime_analysis_powerbi.pbix`.
3. Open the file in Power BI Desktop.
4. Refresh the data source if necessary.

**Note:** The `.pbix` file must be opened in Power BI Desktop. GitHub does not render Power BI reports directly.

---

## Repository Structure

```text
Crime-Rate-Analysis/
|
|-- README.md
|-- Crime_Rate_Analysis.ipynb
|-- 5000R_MM.ipynb
|-- crime_analysis_powerbi.pbix
|
|-- incident_dataset.csv
|-- chicago_crime_data.csv
```

The CSV files are generated by the notebooks and may not be included in the repository until the data collection steps have been executed.

---

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Emaan-Munib/Crime-Rate-Analysis.git
cd Crime-Rate-Analysis
```

### 2. Install Dependencies

Ensure Python 3 is installed.

Install the required packages:

```bash
pip install pandas numpy requests beautifulsoup4 \
matplotlib seaborn plotly statsmodels prophet \
scikit-learn folium jupyter
```

### 3. Run Jupyter Notebook

```bash
jupyter notebook
```

Open the relevant notebooks:

- `5000R_MM.ipynb`
- `Crime_Rate_Analysis.ipynb`

Execute the notebook cells in the required order.

### 4. Generate Forecasts

When prompted, provide:

- City name (or leave blank for all cities)
- Forecast horizon in days

The notebook will generate the corresponding forecasts and visualizations.

### 5. Explore the Power BI Report

Open `crime_analysis_powerbi.pbix` using Microsoft Power BI Desktop.

---

## Project Outputs

| Output | Description |
|---|---|
| `incident_dataset.csv` | Scraped mass shooting incident records |
| `chicago_crime_data.csv` | Chicago crime records retrieved through the API |
| ARIMA Forecast | Predicted fatality counts |
| Prophet Forecast | Predicted injury counts |
| DBSCAN Clusters | Geographical groupings of gun-related incidents |
| Folium Maps | Interactive crime hotspot visualizations |
| Plotly Charts | Interactive crime trends and statistical visualizations |
| Power BI Report | Crime analysis dashboard |

---

## Challenges and Limitations

### Data Availability

Gun Violence Archive website accessibility and table structures may change, potentially affecting automated data collection.

### Forecasting Uncertainty

Crime data is influenced by many external factors that historical time-series models cannot fully capture.

### Data Completeness

Public datasets may contain missing, delayed, or inconsistently reported records.

### Geographical Clustering

DBSCAN results depend on the chosen distance threshold and minimum cluster size.

### Model Validation

Additional out-of-sample evaluation and time-based validation would help assess forecasting reliability.

---

## Future Improvements

Potential enhancements include:

- Automated scheduled data collection
- Improved forecasting evaluation using rolling time-series validation
- Comparison with SARIMA and other forecasting models
- Integration of additional socioeconomic and demographic indicators
- Improved geospatial clustering parameter selection
- Interactive city-level crime dashboards
- More extensive supervised classification experiments
- Automated Power BI data refresh
- Deployment of a web-based analytics dashboard

---

## Applications

This project demonstrates techniques applicable to:

- **Public Safety Analytics:** Exploring historical crime distributions.
- **Geospatial Data Science:** Identifying areas with concentrated incidents.
- **Time-Series Analysis:** Modeling temporal changes in reported violence.
- **Urban Analytics:** Supporting geographical and historical trend analysis.
- **Business Intelligence:** Presenting analytical findings through interactive dashboards.
- **Machine Learning:** Applying supervised and unsupervised algorithms to real-world datasets.

---

## Project Status

**Data Analytics & Machine Learning Development Project**

The project combines real-world data collection, exploratory analysis, forecasting, clustering, visualization, and business intelligence reporting.

The implementation provides a foundation for further development of crime analytics and forecasting applications.

---

## Data Sources & References

- [Gun Violence Archive](https://www.gunviolencearchive.org/)
- [Chicago Open Data Portal](https://data.cityofchicago.org/)
- [Scikit-learn Documentation](https://scikit-learn.org/)
- [Statsmodels Documentation](https://www.statsmodels.org/)
- [Prophet Documentation](https://facebook.github.io/prophet/)
- [Plotly Documentation](https://plotly.com/python/)
- [Folium Documentation](https://python-visualization.github.io/folium/)
- [Microsoft Power BI](https://powerbi.microsoft.com/)
