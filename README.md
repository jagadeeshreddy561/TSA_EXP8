### Developed by: Mallu Jagadeeswar Reddy
### Reg no: 212222240059
### Date:
# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
 


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python on National Stock exchange
.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the dataset (adjust the path accordingly)
data = pd.read_csv('infy_stock.csv')

# Convert 'Date' to datetime format and set it as the index
data['Date'] = pd.to_datetime(data['Date'], format='%Y-%m-%d')
data.set_index('Date', inplace=True)

# Focus on the 'Adj Close' column
adj_close_data = data[['Trades']]

# Display the shape and the first 5 rows of the dataset
print("Shape of the dataset:", adj_close_data.shape)
print("First 5 rows of the dataset:")
print(adj_close_data.head())

# Plot Original Dataset (Adj Close Data)
plt.figure(figsize=(12, 6))
plt.plot(adj_close_data['Trades'], label='Original Adj Close Data', color='blue')
plt.title('Original Adjusted Close Prices')
plt.xlabel('Date')
plt.ylabel('Adjusted Close Price (USD)')
plt.legend()
plt.grid()
plt.show()

# Moving Average
# Perform rolling average transformation with a window size of 10
rolling_mean_10 = adj_close_data['Trades'].rolling(window=10).mean()

# Plot Moving Average
plt.figure(figsize=(12, 6))
plt.plot(adj_close_data['Trades'], label='Original Adj Close Data', color='blue')
plt.plot(rolling_mean_10, label='Moving Average (window=10)', color='orange')
plt.title('Moving Average of Trades')
plt.xlabel('Date')
plt.ylabel('Trades')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
model = ExponentialSmoothing(adj_close_data['Trades'], trend='add', seasonal=None)
model_fit = model.fit()

# Make predictions for the next 30 periods (you can adjust this)
predictions = model_fit.predict(start=len(adj_close_data), end=len(adj_close_data) + 30)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
plt.plot(adj_close_data['Trades'], label='Original Adj Close Data', color='blue')
plt.plot(predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for trades')
plt.xlabel('Date')
plt.ylabel('Trades')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
```

### OUTPUT:

![Screenshot 2024-10-16 155554](https://github.com/user-attachments/assets/12e62c7c-bea7-4d6f-8a5e-4ca41e1164ec)

#### Moving Average

![Screenshot 2024-10-16 155625](https://github.com/user-attachments/assets/d30eac76-ab1e-4765-9680-79c5024e4bec)

#### Plot Transform Dataset
![Screenshot 2024-10-16 155607](https://github.com/user-attachments/assets/f7e7778f-8359-4905-9d32-3c197569aa39)



#### Exponential Smoothing

![Screenshot 2024-10-16 155633](https://github.com/user-attachments/assets/48793708-fc6c-41e1-82fb-a042991dcdb1)


### RESULT:
Thus , successful implemention of the Moving Average Model and Exponential smoothing using python is done.
