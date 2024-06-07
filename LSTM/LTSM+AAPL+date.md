# LTSM+AAPL+date

```py
!pip install tensorflow -qqq
!pip install keras -qqq
!pip install yfinance -qqq
```

```py
import tensorflow as tf
print(tf.__version__)
```
2.15.0
```py
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.preprocessing import MinMaxScaler
from tensorflow.keras.models import Sequential
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
from tensorflow.keras.layers import LSTM, Dense
import yfinance as yf
from tqdm import tqdm
import seaborn as sns

SYMBOLS = ['AAPL']
START_DATE = '2022-01-01'
END_DATE = '2024-01-01'
LOOK_BACK = 3
EPOCHS = 100

# Fetching stock price data from Yahoo Finance
def fetch_stock_data(symbol, start_date, end_date):
    data = yf.download(symbol, start=start_date, end=end_date)
    return data

# Step 1: Data Preparation
def prepare_data(data):
    # Selecting Adjusted Close prices
    adj_close = data['Adj Close'].values.reshape(-1,1)

    # Normalizing the data
    scaler = MinMaxScaler(feature_range=(0, 1))
    adj_close_normalized = scaler.fit_transform(adj_close)

    # Splitting data into train and test sets
    train_size = int(len(adj_close_normalized) * 0.80)
    test_size = len(adj_close_normalized) - train_size
    train_data, test_data = adj_close_normalized[0:train_size,:], adj_close_normalized[train_size:len(adj_close_normalized),:]

    return train_data, test_data, scaler

# Creating dataset with look-back
def create_dataset(dataset, look_back=1):
    X, Y = [], []
    for i in range(len(dataset)-look_back-1):
        a = dataset[i:(i+look_back), 0]
        X.append(a)
        Y.append(dataset[i + look_back, 0])
    return np.array(X), np.array(Y)

# Step 2: Model Training
def train_lstm(train_data, look_back=1, epochs=100):
    X_train, Y_train = create_dataset(train_data, look_back)
    
    # Reshape input data to match LSTM input shape
    X_train = np.reshape(X_train, (X_train.shape[0], X_train.shape[1], 1))

    # Building LSTM model
    model = Sequential()
    model.add(LSTM(4, input_shape=(look_back, 1)))
    model.add(Dense(1))
    model.compile(loss='mean_squared_error', optimizer='adam')
    
    # Training the model
    epoch_range = tqdm(range(epochs), desc="Epochs")
    for epoch in epoch_range:
        model.fit(X_train, Y_train, epochs=1, batch_size=1, verbose=0)
        epoch_range.set_postfix({'loss': model.history.history['loss'][0]})
    
    return model

# Step 3: Result Visualization
def visualize_results(data, scaler, model, stock_symbol, look_back=1):
    # Making predictions for train data
    train_predict = model.predict(data.reshape(-1, 1, 1))
    train_predict = scaler.inverse_transform(train_predict)
    
    # Converting the index to datetime format
    dates = pd.date_range(start=START_DATE, end=END_DATE, periods=len(data))

    # Setting seaborn style
    sns.set_style("whitegrid")
    
    # Plotting results with stock symbol in legend
    plt.figure(figsize=(14, 8))
    plt.plot(dates, scaler.inverse_transform(data), label=f'Actual ({stock_symbol})', color='blue', alpha=0.6, linewidth=2)
    plt.plot(dates, train_predict, label=f'Predicted ({stock_symbol})', color='orange', alpha=0.8, linewidth=2)
    plt.title(f'Predicted vs Actual Stock Prices ({stock_symbol})', fontsize=16)
    plt.xlabel('Date', fontsize=14)
    plt.ylabel('Stock Price', fontsize=14)
    plt.legend(fontsize=12)
    plt.xticks(rotation=45, fontsize=10)
    plt.yticks(fontsize=12)
    plt.show()

def evaluate_performance(model, test_data, scaler, look_back=1):
    X_test, Y_test = create_dataset(test_data, look_back)
    
    # Reshape input data to match LSTM input shape
    X_test = np.reshape(X_test, (X_test.shape[0], X_test.shape[1], 1))
    
    # Making predictions
    test_predict = model.predict(X_test)
    test_predict = scaler.inverse_transform(test_predict)
    
    # Reshape Y_test to match the shape of test_predict
    Y_test = Y_test.reshape(test_predict.shape)
    
    # Calculating performance metrics
    rmse = np.sqrt(mean_squared_error(Y_test, test_predict))
    mae = mean_absolute_error(Y_test, test_predict)
    mape = np.mean(np.abs((Y_test - test_predict) / Y_test)) * 100
    r2 = r2_score(Y_test, test_predict)
    
    print(f"RMSE: {rmse}")
    print(f"MAE: {mae}")
    print(f"MAPE: {mape}")
    print(f"R-squared: {r2}")

def main():
    for symbol in SYMBOLS:
        # Fetching and preparing data
        data = fetch_stock_data(symbol, START_DATE, END_DATE)
        train_data, test_data, scaler = prepare_data(data)
        
        # Training LSTM model
        lstm_model = train_lstm(train_data, LOOK_BACK, EPOCHS)
        
        # Evaluating performance
        evaluate_performance(lstm_model, test_data, scaler, LOOK_BACK)
        
        # Visualizing results with stock symbol
        visualize_results(train_data, scaler, lstm_model, symbol, LOOK_BACK)

if __name__ == "__main__":
    main()
```
![Predicted vs Actual Stock Prices-100epoch_date](https://github.com/MLiserb/Articles/assets/144083324/7a422325-71a0-4aab-b2b3-a2ebc72722d1)

