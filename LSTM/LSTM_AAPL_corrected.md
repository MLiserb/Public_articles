
```py
!pip install tensorflow -qqq
!pip install keras -qqq
!pip install yfinance -qqq
```

```py
import tensorflow as tf
import keras
import yfinance as yf
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Check TensorFlow version
print("TensorFlow Version: ", tf.__version__)
```

```py
# Fetch AAPL data
aapl_data = yf.download('AAPL', start='2020-01-01', end='2024-05-01')

# Display the first few rows of the dataframe
aapl_data.head()
```

```py
# Checking for missing values
aapl_data.isnull().sum()

# Filling missing values, if any
aapl_data.fillna(method='ffill', inplace=True)
```

