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
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("/kaggle/input/exercise-1b-dataset/ecommerce_sales_data (2).csv")
data.head()

data['Order Date'] = pd.to_datetime(data['Order Date'])

data = data.groupby('Order Date')['Sales'].sum().reset_index()

data.set_index('Order Date', inplace=True)

data['sales_diff'] = data['Sales'] - data['Sales'].shift(1)

result = seasonal_decompose(data['Sales'], model='additive', period=12)
data['sales_sea_diff'] = result.resid

data['sales_log'] = np.log(data['Sales'])
data['sales_log_diff'] = data['sales_log'] - data['sales_log'].shift(1)

result = seasonal_decompose(data['sales_log_diff'].dropna(),
                             model='additive', period=12)
data['sales_log_seasonal_diff'] = result.resid


plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Sales'], label='Original')
plt.legend(loc='best')
plt.title('Original Sales Data')
plt.xlabel('Date')
plt.ylabel('Sales')

plt.subplot(6, 1, 2)
plt.plot(data['sales_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Date')
plt.ylabel('Differenced Sales')

plt.subplot(6, 1, 3)
plt.plot(data['sales_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Date')
plt.ylabel('Seasonally Adjusted Sales')

plt.subplot(6, 1, 4)
plt.plot(data['sales_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Date')
plt.ylabel('Log(Sales)')

plt.subplot(6, 1, 5)
plt.plot(data['sales_log_diff'], label='Log + Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Date')
plt.ylabel('RDiff(Log(Sales))')

plt.subplot(6, 1, 6)
plt.plot(data['sales_log_seasonal_diff'], label='Log + Regular + Seasonal')
plt.legend(loc='best')
plt.title('Log + Regular + Seasonal Differencing')
plt.xlabel('Date')
plt.ylabel('Final Stationary Series')

plt.tight_layout()
plt.show()

data.plot(kind='line', figsize=(12,6))
plt.show()

```

### OUTPUT:

<img width="1140" height="183" alt="image" src="https://github.com/user-attachments/assets/a7bd8bd8-dc40-4a43-b93c-46de476b4331" />
<img width="1144" height="191" alt="image" src="https://github.com/user-attachments/assets/0a170779-edc3-4331-a13f-f07cb3f20302" />
<img width="1145" height="204" alt="image" src="https://github.com/user-attachments/assets/362da3f0-f2f3-47db-9e96-7b6db377b528" />
<img width="1095" height="189" alt="image" src="https://github.com/user-attachments/assets/b57de69d-0ed9-48a6-bd19-a3ef72a81b4a" />
<img width="1092" height="179" alt="image" src="https://github.com/user-attachments/assets/ac3dec6e-f4a6-4cae-9a78-55f8bf7f40b1" />




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
