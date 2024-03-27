# CheckPoint 1 : Forecastability Score

📈 This project aims to develop a model capable of providing a forecastability score for time series data within the range of 0 to 10, where 10 denotes highly forecastable data and 0 indicates data close to white noise. The model utilizes various techniques, including time series feature extraction and statistical analysis, to determine the forecastability score.

## Code Description

🔍 The provided code is a Python script that implements the functionalities required for calculating the forecastability score. Here's a brief overview of the key features implemented:

1. **Time Series Frequency Detection:** Detects the frequency of the time series data (hourly, daily, weekly, or monthly).
2. **Outlier Detection:** Identifies outliers in the data using the Z-score method.
3. **Null Values Handling:** Counts and handles null values in the dataset, adjusting the score accordingly based on different frequencies.
4. **Stationarity Testing:** Performs the Augmented Dickey-Fuller (ADF) test to evaluate the stationarity of the time series data.
5. **Trend Analysis:** Assesses the presence of trends in the data and calculates the number of differentiations needed to detrend the time series.
6. **Seasonality Detection:** Applies seasonal decomposition to detect trends, seasonality, and autocorrelation in the data.
7. **Approximate Entropy Analysis:** Calculates approximate entropy to assess the complexity of the time series data.
8. **Demand Pattern Analysis:** Analyzes demand patterns based on Average Demand Interval (ADI) and variation in quantity and time intervals.

## Usage

🛠️ To use the provided code:

1. Make sure you have Python installed on your system.
2. Install the required dependencies listed in the code.
3. Load your time series dataset into the script.
4. Initialize the `Model` object and calculate the forecastability score using the `calculate_forecastability_score()` method.
5. Print the forecastability score to evaluate the results.

```
# Sample usage of the Model class with a provided dataset
import pandas as pd

# Load sample dataset
df = pd.read_csv("path_to_your_dataset.csv")

# Initialize Model object
model = Model()

# Calculate forecastability score
model.calculate_forecastability_score(df)

# Print forecastability score
print("Forecastability Score:", model.forecastability_score) 

``` 
# References and Proof:
1. [Approximate Entropy](https://stats.stackexchange.com/questions/126829/how-to-determine-forecastability-of-time-series)<br>
2. [Stationarity](https://www.analyticsvidhya.com/blog/2021/10/a-comprehensive-guide-to-time-series-analysis/)<br>
3. [Metric](https://help.llama.ai/release/native/demand/demand-topics/Time_Series_Metrics.htm)<br>
4. [TimeSeries](https://medium.com/analytics-vidhya/assessment-of-accuracy-metrics-for-time-series-forecasting-bc115b655705)<br>


