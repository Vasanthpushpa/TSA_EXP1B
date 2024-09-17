## Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA
## DEVELOPED BY: VASANTH P
## REG NO: 212222240113

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Electricity production  data
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
%matplotlib inline
train = pd.read_csv('Electric_Production.csv')
train['DATE'] = pd.to_datetime(train['DATE'], format='%d/%m/%Y')
train.head()
```
## REGULAR DIFFERENCING:
```
from statsmodels.tsa.stattools import adfuller
def adf_test(timeseries):
    print ('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic','p-value','#Lags Used'
               ,'Number of Observations Used'])
    for key,value in dftest[4].items():
       dfoutput['Critical Value (%s)'%key] = value
    print (dfoutput)
adf_test(train['IPG2211A2N'])
train['DATE'] = pd.to_datetime(train['DATE'], format='%d/%m/%Y')
train['Year'] = train['DATE'].dt.year
```
## SEASONAL ADJUSTMENT:
```
data=train
data['SeasonalAdjustment'] = data.iloc[:,1] - data.iloc[:,1].shift(12)
data['SeasonalAdjustment'].dropna()
x=data['Year']
y=data["SeasonalAdjustment"]
plt.plot(x,y,color='black')
plt.title("ElectroGraph")
plt.xlabel("<-----Year---->",color='blue')
plt.ylabel("<-----Usage---->",color='red')
plt.show()
```
## LOG TRANSFORMATION:
```
data1=train
data1['log']=np.log(data1['IPG2211A2N_diff']).dropna()
data1=data1.dropna()
x=data1['Year']
y=data1['log']
plt.xlabel('Year',color='blue')
plt.ylabel('Log Values',color='red')
```
### OUTPUT:


## REGULAR DIFFERENCING:

![322770412-f6f9e31b-3614-45b7-9a2c-2028d0cf8c40](https://github.com/LokeshRajamani/TSA_EXP1B/assets/120544804/96209b98-08fd-4ed8-b8db-d8524494880e)



## SEASONAL ADJUSTMENT:

![322770454-79a8cff9-9953-4a61-94d7-9cc660c9163c](https://github.com/LokeshRajamani/TSA_EXP1B/assets/120544804/cbea5819-7a2c-4db6-86c8-80c1ee5fabe3)



## LOG TRANSFORMATION:

![322770497-e42b45c4-90fc-4fc8-a71a-19c7f4330779](https://github.com/LokeshRajamani/TSA_EXP1B/assets/120544804/cd49c673-1119-44f9-9f31-2d28c7b01051)




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data.
