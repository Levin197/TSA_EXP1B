# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:

To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data

### ALGORITHM:

1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
6. 
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
data = pd.read_csv('AirPassengers.csv')
data.head()
data['Month'] = pd.to_datetime(data['Month']) # data=pd.read_csv("/content/AirPassengers.csv",parse_dates=
data.set_index('Month', inplace=True)
data['passengers_diff'] = data['#Passengers'] - data['#Passengers'].shift(1)
result = seasonal_decompose(data['#Passengers'], model='additive', period=12)
data['passengers_sea_diff'] = result.resid
data['passengers_log'] = np.log(data['#Passengers'])
data['passengers_log_diff'] = data['passengers_log'] - data['passengers_log'].shift(1)
result = seasonal_decompose(data['passengers_log_diff'].dropna(), model='additive', period=12)
plt.plot(data['passengers_diff'], label='Differencing')
plt.legend(loc='best')
plt.title('Differencing')
plt.xlabel('Year')
plt.ylabel('Seasonally djusted No of passengers')
plt.subplot(6, 1, 3)
plt.plot(data['passengers_sea_diff'], label='Seasonal Difference ')
plt.legend(loc='best')
plt.title('Seasonal Difference')
plt.xlabel('Year')
plt.ylabel('No of passengers')
plt.subplot(6, 1, 4)
plt.plot(data['passengers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(No of passengers)')
plt.subplot(6, 1, 5)
plt.plot(data['passengers_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(No of passengers))')
data['passengers_log_seasonal_diff'] = data['passengers_log_diff'] - data['passengers_log_diff'].shift(12)
plt.subplot(6, 1, 6)
plt.plot(data['passengers_log_seasonal_diff'], label='Log Transformation and regular Differencing and S')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(No of passengers)))')
plt.tight_layout()
plt.show()+
data.plot(kind='line')
```
### OUTPUT:
REGULAR DIFFERENCING:
![Screenshot 2025-03-22 162144](https://github.com/user-attachments/assets/2f76a623-4e34-4199-87cc-5f22d9a2ecda)

SEASONAL ADJUSTMENT:
![exp1b seasonal ](https://github.com/user-attachments/assets/0fead85b-3e1e-4126-926b-bb356de60688)

LOG TRANSFORMATION:
![exp1b-log transformation](https://github.com/user-attachments/assets/0918b320-56a8-439a-ae04-9bf48d85363c)

LOG TRANSFORMATION AND REGULAR DIFFERENCING:
![exp1b-log trans+regular diff](https://github.com/user-attachments/assets/089abd6d-1605-4087-8998-57e8df7493af)

LOG TRANSFORMATION AND REGULAR DIFFERENCING AND SEASONAL DIFFERENCING:
![log+regular+seasonal](https://github.com/user-attachments/assets/29b69bdd-4d6b-430a-8418-933706f8014c)

OVERALL GRAPH:
![table](https://github.com/user-attachments/assets/907c0675-9c89-40bb-9a2b-761f136205fb)

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
