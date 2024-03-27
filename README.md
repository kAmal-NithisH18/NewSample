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
#### Output samples
[Components](https://github.com/kAmal-NithisH18/NewSample/blob/main/checkpoint1.jpeg)
[Result](https://github.com/kAmal-NithisH18/NewSample/blob/main/checkpoint1a.jpeg)
``` 
### References and Proof:
1. [Approximate Entropy](https://stats.stackexchange.com/questions/126829/how-to-determine-forecastability-of-time-series)<br>
2. [Stationarity](https://www.analyticsvidhya.com/blog/2021/10/a-comprehensive-guide-to-time-series-analysis/)<br>
3. [Metric](https://help.llama.ai/release/native/demand/demand-topics/Time_Series_Metrics.htm)<br>
4. [TimeSeries](https://medium.com/analytics-vidhya/assessment-of-accuracy-metrics-for-time-series-forecasting-bc115b655705)<br>


# Checkpoint 2: Generate Predictions

In this checkpoint, batch anomaly detection with Prophet is performed on time series data with forecastability scores greater than the optimal threshold. An expanding window algorithm with a window size of 7 periods is utilized for the batch anomaly detection.

### Anomaly : 

An anomaly in time series data refers to an observation or pattern that deviates significantly from the expected behavior of the data. In other words, it represents a point in the time series that is unexpected or abnormal compared to the rest of the data.

![Ananmoly](https://raw.githubusercontent.com/DHI/tsod/main/images/anomaly.png)

## Code Description

The provided code implements the batch anomaly detection process using the Prophet library. Here's a summary of the key functionalities implemented:

- Import necessary libraries such as FastAPI, pandas, Prophet, and more.
- Define a function `batch_anomaly_detection_optimized` to perform batch anomaly detection with optimized parameters.
- Utilize the `optimize_parameters` function to obtain optimized parameters for the Prophet model.
- Iterate through the dataset using an expanding window approach to detect anomalies.
- Calculate Mean Absolute Percentage Error (MAPE) for each prediction.
- Output the results including anomalies, MAPE values, number of batch fits, average batch fit time, and predicted values.

## Usage

To use the provided code:

1. Ensure you have the required libraries installed.
2. Load your time series dataset into the script.
3. Preprocess the dataset as required (e.g., handle missing values, rename columns).
4. Call the `batch_anomaly_detection_optimized` function with your dataset as input.
5. Print or use the output as needed.

Sample usage code:

```python
# Import necessary libraries
from prophet import Prophet
import pandas as pd
from tuning import optimize_parameters
from Forecastability_Score import Model

# Load and preprocess the dataset
df = pd.read_csv("path_to_your_dataset.csv")
df = df.ffill()
df.rename(columns={'point_timestamp':'ds', 'point_value':'y'}, inplace=True)

# Perform batch anomaly detection
result = batch_anomaly_detection_optimized(df)

# Print or use the output
print(result)

```
### Refernces
[Prophet](https://facebook.github.io/prophet/docs/installation.html#python)

# Checkpoint 3: REST API for Time Series Prediction

This checkpoint implements a simple REST API using FastAPI, allowing users to provide any time series data and obtain predictions along with details such as forecastability score, MAPE value, number of batch fits, and average time taken for each batch fit.

## Code Description

The provided code sets up a FastAPI server with two endpoints:

1. `/predict/`: Accepts time series data in the format of timestamps and values, performs batch anomaly detection with optimized parameters, calculates error metrics including MAPE, and returns the predictions along with other details.
2. `/`: A welcome message endpoint.

## Usage

To use the provided API:

1. Ensure you have FastAPI and its dependencies installed.
2. Run the FastAPI server.
3. Send a POST request to the `/predict/` endpoint with time series data in the specified format.
4. Receive the predictions and details in the response.

Here's an example of how to use the API with sample usage code:

```python
import requests
import pandas as pd

# Load sample dataset
df = pd.read_csv("path_to_your_dataset.csv")
df.drop('Unnamed: 0', axis=1, inplace=True)
df = df.ffill()
data_list = df.to_dict(orient='records')

# Construct the desired format
data = {"data": data_list}

# Send POST request to the API
response = requests.post("http://localhost:8000/predict/", json=data)

# Check the response
print(response.json())

```
### Input Sample
```python
data = {
    "data": [
        {"point_timestamp": "2018-01-01", "point_value": 0.000364},
        {"point_timestamp": "2018-02-01", "point_value": 0.000313},
        {"point_timestamp": "2018-03-01", "point_value": 0.000079},
        {"point_timestamp": "2018-04-01", "point_value": 0.000044},
        {"point_timestamp": "2018-05-01", "point_value": 0.000000},
        {"point_timestamp": "2018-06-01", "point_value": 0.000073},
        {"point_timestamp": "2018-07-01", "point_value": 0.000171},
        {"point_timestamp": "2018-08-01", "point_value": 0.000079},
        {"point_timestamp": "2018-09-01", "point_value": 0.000000},
        {"point_timestamp": "2018-10-01", "point_value": 0.000050},
        {"point_timestamp": "2018-11-01", "point_value": 0.000129},
        {"point_timestamp": "2018-12-01", "point_value": 0.000150},
        {"point_timestamp": "2019-01-01", "point_value": 0.000993},
        {"point_timestamp": "2019-02-01", "point_value": 0.000867},
        {"point_timestamp": "2019-03-01", "point_value": 0.000797},
        {"point_timestamp": "2019-04-01", "point_value": 0.000137},
        {"point_timestamp": "2019-05-01", "point_value": 0.000406},
        {"point_timestamp": "2019-06-01", "point_value": 0.000348},
        {"point_timestamp": "2019-07-01", "point_value": 0.000156},
        {"point_timestamp": "2019-08-01", "point_value": 0.000361},
        {"point_timestamp": "2019-09-01", "point_value": 0.000121},
        {"point_timestamp": "2019-10-01", "point_value": 0.000120},
        {"point_timestamp": "2019-11-01", "point_value": 0.000181},
        {"point_timestamp": "2019-12-01", "point_value": 0.000120},
        {"point_timestamp": "2020-01-01", "point_value": 0.000677}
    ]
}
```
### Output :
![Sample Output](https://github.com/kAmal-NithisH18/NewSample/blob/main/apioutput.jpeg)

## Checkpoint 4: Model Optimization

This checkpoint focuses on optimizing the model's per-fit training time to reduce the overall execution time for the entire set of batches. This optimization is achieved through parameter tuning in order to find an optimal trade-off between training time and accuracy.

### Code Description

The provided code defines a function `optimize_parameters()` that optimizes Prophet model parameters. Here's a breakdown of the key components:

- **Parameter Grid**: Defines a grid of parameter combinations to be tested for optimization.
- **Model Training**: Iterates through all parameter combinations, fitting Prophet models to the provided time series data.
- **Evaluation**: Evaluates each model based on Mean Absolute Percentage Error (MAPE) and checks for training time against a maximum allowed runtime.
- **Selection**: Identifies the best-performing model based on MAPE and ensures its runtime does not exceed the maximum allowed runtime.

### Usage

To utilize the optimization function:

1. Provide your time series data to the `optimize_parameters()` function.
2. Optionally, adjust parameters such as `window_size`, `factor`, and `max_runtime` to customize the optimization process.
3. Receive the optimal parameters for the Prophet model, which offer a balanced trade-off between training time and accuracy.

```python
import pandas as pd
from prophet import Prophet
from Your_Module import optimize_parameters

# Load your time series data into DataFrame 'df'

# Optimize model parameters
optimal_params = optimize_parameters(df)

print("Optimal Parameters:", optimal_params)

```
## Checkpoint 5: Batch Reduction Algorithm

In this checkpoint, we propose a method to dynamically determine the window size for batch processing in time series data. By using changepoint detection, we aim to reduce the number of training batches without majorly impacting accuracy.

### Code Description

The provided code includes a function `determine_window_size(df)` that dynamically calculates the window size based on changepoint detection. Here's a brief overview of the function:

- **Input**: A pandas DataFrame (`df`) containing the time series data with columns 'ds' (timestamps) and 'y' (values).
- **Output**: An integer representing the dynamically determined window size.

The function utilizes the `ruptures` library to perform changepoint detection, specifically using the l2-norm cost function. It then calculates the maximum gap between changepoints and determines the window size based on this gap.

## Usage

To use the `determine_window_size` function:

1. Pass your time series data as a pandas DataFrame to the function.
2. The function will return the dynamically determined window size based on changepoint detection.

Sample usage code:

```python
import pandas as pd
from determine_window_size import determine_window_size

# Load your time series data into a pandas DataFrame (df)
df = pd.read_csv("path_to_your_dataset.csv")

# Determine the window size dynamically
window_size = determine_window_size(df)

print("Dynamically Determined Window Size:", window_size)

```
![Output](https://github.com/kAmal-NithisH18/NewSample/blob/main/checkpoint5.jpeg)


