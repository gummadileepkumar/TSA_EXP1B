# Developed By: Gumma Dileep Kumar

# Register No: 212222240032

# Date: 

# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA


### AIM:
To perform regular differncing,seasonal adjustment and log transformation on infy_stock dataset

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
#### IMPORTING PACKAGES:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
```

#### Preprocessing:
```python
train = pd.read_csv('infy_stock-Copy1.csv')
train['Date'] = pd.to_datetime(train['Date'], format='%Y-%m-%d')
train.index=train.Date
train.head()
print(train.columns)
train.columns = train.columns.str.strip()
train['Turnover'].plot()
```

#### REGULAR DIFFERENCING:
```python
from statsmodels.tsa.stattools import adfuller
def adf_test(timeseries):
    print("Results of Dickey-Fuller Test:")
    dftest = adfuller(timeseries, autolag="AIC")
    dfoutput = pd.Series(dftest[0:4], index=["Test Statistic", "p-value", "#Lags Used", "Number of Observations Used"])
    for key, value in dftest[4].items():
        dfoutput["Critical Value (%s)" % key] = value
    print(dfoutput)
adf_test(train['Turnover'])
train['Turnover_diff']=train['Turnover']-train['Turnover'].shift(1)
train['Turnover_diff'].dropna().plot()
plt.title('Regualr Differencing')
```

#### SEASONAL DIFFERENCING:
```python
n=7
train['Turnover_diff']=train['Turnover']-train['Turnover'].shift(n)
train['Turnover_diff'].dropna().plot()
plt.title('Seasona Differencing')

```

#### LOG TRANSFORMATION:
```python
train['Turnover_log']=np.log(train['Turnover'])
train['Turnover_log_diff']=train['Turnover_log']-train['Turnover_log'].shift(1)
train['Turnover_log_diff'].dropna().plot()
plt.title('Log Transformation')
```


### OUTPUT:


##### REGULAR DIFFERENCING:

![Re_1 2_1](https://github.com/user-attachments/assets/b2112a16-5849-4ac6-afdb-b4f83761b795)



##### SEASONAL ADJUSTMENT:

![re_1 2_2](https://github.com/user-attachments/assets/3b00aaa7-9d5c-421f-9c12-c58644a2bd1d)



##### LOG TRANSFORMATION:

![Re_1 2_3](https://github.com/user-attachments/assets/31755f97-a66a-4494-92be-8882c2856516)



### RESULT:

Thus we have successfully created the python code for the conversion of non stationary to stationary data of infy stock data.
