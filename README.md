# Time Series Prediction for individual household power
Individual household power prediction
Dateset: https://archive.ics.uci.edu/ml/datasets/individual+household+electric+power+consumption

The electric power consumption in an individual household with a one-minute sampling rate over a period between Dec 2006
and Nov 2010 (47 months) were measured. Different electrical quantities and some sub-metering values are recorded. 
Our goal is to predict the Global active power at least 1 hour into the future.

<> There are some data points of Dec 2010, which is not consistent with the data description.

Six independentvariables and a numerical dependent variable Global active power with 2,075,259 observations are available. 
Approximately 1.25% missing values are represented as “?” in the raw dataset. There are several methods to impute the missing
values as the column mean, median or using KNN based approaches. However, missing values are dropped for simplicity.
Furthermore, we find that not all observations are ordered by the date time. Therefore we analyze the data with explicit time 
stamp as an index. In the preprocessing step, we perform a bucket-average of the raw data to reduce the noise from the one-
minute sampling rate. For simplicity, we only focus on the last 18000 rows of raw dataset (the most recent data in Nov 2010).

### A list of pythons files:
+ **Gpower_Arima_Main.py** :  The executable python program of a univariate ARIMA model.
+ myArima.py : implements a class with some callable methods used for the Arima model.
+ **Gpower_Xgb_Main.py** : The executable python program of a tree based model (xgboost).
+ myXgb.py : implements some functions used for the xgboost model.
+ **lstm_Main.py** : The executable python program of a LSTM model.
+ lstm.py : implements a class of a time series model using an LSTMCell. The credit should go to  https://github.com/hzy46/TensorFlow-Time-Series-Examples/blob/master/train_lstm.py
+ util.py: implements various functions for data preprocessing.
+ Exploratory_analysis.py: exploratory analysis and plots of data.

### Here, I used 3 different approaches to model the pattern of power consumption.
1. Univariate time series ARIMA
![onestep](https://user-images.githubusercontent.com/25689659/34470019-001ea4e0-eef7-11e7-822a-5a5132e8ca75.png)
![dynamic](https://user-images.githubusercontent.com/25689659/34470018-0011600a-eef7-11e7-89df-79372c49a791.png)
![forecast](https://user-images.githubusercontent.com/25689659/34470017-0004e848-eef7-11e7-9148-abfb62f95dcc.png)
2. Regression tree-based xgboost 
![xgbManual](https://user-images.githubusercontent.com/25689659/34470022-00463b90-eef7-11e7-8a3c-d80df291f7d6.png)
3. Recurrent neural network LSTM (long short-term memoery) model
![lstmprediction](https://user-images.githubusercontent.com/25689659/34470011-ffaa7232-eef6-11e7-9ded-5c7714952d06.png)

### Possible approaches to do in the future work:
#### (i) Dynamic regression time series model
Given the strong correlations between Sub metering 1, Sub metering 2 and Sub metering 3 and our target variable, 
these variables could be included into the dynamic regression model or regression time series model.

#### (ii) Dynamic xgboost model
Include the timestep-shifted Global active power columns as features. The target variable will be current Global active power. 
Recent history of Global active power up to this time stamp (say, from 100 timesteps before) should be included
as extra features.

#### (iii) Multivariate LSTM

