# Pharma-Portfolio-Predictive-Analysis

## Overview:

This repository contains my work on the Pharma Sales Data's Forecast and Analysis. This project is being upgraded.

## Languages & Tools:

- `Python`

- `Machine Learning` (on both Python and Azure)

- `Azure Machine Learning Studio`

- `SQL`

## Analysis:

### On which day of the week is the second drug (M01AE) most often sold?

@Google Colab `Python`
```
df = df[['M01AE', 'Weekday Name']]
result = df.groupby(['Weekday Name'], as_index=False).sum().sort_values('M01AE', ascending=False)
```

@AzureML `Python`
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import re
import calendar
from datetime import datetime

# The entry point function can contain up to two input arguments:
#   Param<dataframe1>: a pandas.DataFrame
#   Param<dataframe2>: a pandas.DataFrame
def azureml_main(dataframe1 = None, dataframe2 = None):

    # Execution logic goes here
    print('Input pandas.DataFrame #1:\r\n\r\n{0}'.format(dataframe1))

    # If a zip file is connected to the third input port is connected,
    # it is unzipped under ".\Script Bundle". This directory is added
    # to sys.path. Therefore, if your zip file contains a Python file
    # mymodule.py you can import it using:
    # import mymodule
    df = dataframe1[['M01AE', 'Weekday Name']]
    result = df.groupby(['Weekday Name'], as_index=False).sum().sort_values('M01AE', ascending=False)
    # Return value must be of a sequence of pandas.DataFrame
    return result
```    
![Python Queries - M01AE](https://user-images.githubusercontent.com/70437668/161901354-b6b8ac79-750d-4cd0-96fd-82e5573ca466.jpg)

@AzureML `SQL`

t1 represents my chosen dataset input into the file node.
```
SELECT Weekday_Name, sum(M01AE) AS sum_M01AE
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_M01AE ASC
```
![SQL Queries - M01AE](https://user-images.githubusercontent.com/70437668/161901382-40f830c5-a41c-4a82-a94b-5daee87a3b14.jpg)

The drug, M01AE, was most often sold on Sunday with the volume of 1384.94.

```
SELECT Weekday_Name, sum(M01AB) AS sum_M01AB
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_M01AB ASC
```

```
SELECT Weekday_Name, sum(M01AE) AS sum_M01AE
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_M01AE ASC
```

```
SELECT Weekday_Name, sum(N02BA) AS sum_N02BA
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_N02BA ASC
```

```
SELECT Weekday_Name, sum(N02BE) AS sum_N02BE
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_N02BE ASC
```

```
SELECT Weekday_Name, sum(N05B) AS sum_N05B
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_N05B ASC
```

```
SELECT Weekday_Name, sum(N05C) AS sum_N05C
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_N05C ASC
```

```
SELECT Weekday_Name, sum(R03) AS sum_R03
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_R03 ASC
```

```
SELECT Weekday_Name, sum(R06) AS sum_R06
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_R06 ASC
```

### Total value by each day

```
SELECT Weekday_Name, M01AB + M01AE + N02BA + N02BE + N05B + N05C + R03 + R06 AS Total
FROM t1
GROUP BY Weekday_Name
```

### Total value by 2015

```
SELECT LEFT(datum, 4) as Year, sum(M01AB) AS sum_M01AB, sum(M01AE) AS sum_M01AE, sum(N02BA) AS sum_N02BA, sum(N02BE) AS sum_N02BE, sum(N05B) AS sum_N05B, sum(N05C) AS sum_N05C, sum(R03) AS sum_R03, sum(R06) AS sum_R06
FROM t1
WHERE LEFT(datum, 4) == 2015
```

### Total value by 2016

```
SELECT LEFT(datum, 4) as Year, sum(M01AB) AS sum_M01AB, sum(M01AE) AS sum_M01AE, sum(N02BA) AS sum_N02BA, sum(N02BE) AS sum_N02BE, sum(N05B) AS sum_N05B, sum(N05C) AS sum_N05C, sum(R03) AS sum_R03, sum(R06) AS sum_R06
FROM t1
WHERE LEFT(datum, 4) == 2016
```

### Total value by 2017

```
SELECT LEFT(datum, 4) as Year, sum(M01AB) AS sum_M01AB, sum(M01AE) AS sum_M01AE, sum(N02BA) AS sum_N02BA, sum(N02BE) AS sum_N02BE, sum(N05B) AS sum_N05B, sum(N05C) AS sum_N05C, sum(R03) AS sum_R03, sum(R06) AS sum_R06
FROM t1
WHERE LEFT(datum, 4) == 2017
```

## Time Series Analysis

### Seasonality Analysis 

![download (3)](https://user-images.githubusercontent.com/70437668/166632744-1342e832-748c-408f-872a-9ba72c9ecb89.png)

![download (4)](https://user-images.githubusercontent.com/70437668/166632749-34128e92-31de-460f-af12-66e2a2dc31ee.png)

![download (5)](https://user-images.githubusercontent.com/70437668/166632760-8ed7b18c-1991-43d5-84c2-5dc8dd085e6c.png)

![download (6)](https://user-images.githubusercontent.com/70437668/166632771-cef0bad9-c7e8-4c5c-b2e2-ace8703ba0a5.png)

![download (7)](https://user-images.githubusercontent.com/70437668/166632792-c003a168-cfd0-4107-8da3-1636ff1fd134.png)

```
M01AB RESMEAN:5.26715996284115, OBSMEAN:35.59490833332001, PERC:14.797509558159527%

M01AE RESMEAN:4.319542609675869, OBSMEAN:28.00801458336, PERC:15.422523423856601%

N02BA RESMEAN:3.9228389592521657, OBSMEAN:27.083016, PERC:14.484498178682042%

N02BE RESMEAN:29.534357236963668, OBSMEAN:217.6597028336, PERC:13.569051529737028%

N05B RESMEAN:12.94840305932125, OBSMEAN:61.96614999972, PERC:20.895929566997072%

N05C RESMEAN:2.0384606385595405, OBSMEAN:3.871833333332, PERC:52.648460382081936%

R03 RESMEAN:11.722244335544508, OBSMEAN:40.06845833336, PERC:29.25554119906046%

R06 RESMEAN:4.278758416393868, OBSMEAN:19.744589999960002, PERC:21.67053565762842%
```

### Stationarity Analysis (to be continued)

### Regularity Analysis (to be continued)

### Autocorrelation Analysis (to be continued)

## Machine Learning in Python and Azure (to be continued)

- Linear Regression

- Polynomial Regression

- Simple Vector Regression (SVR)

- Voting Regressor's results

@Google Colab `Python`


@Azure-Machine-Learning-Studio

# Association Rules:

If `M01AB, N02BA, R06` is purchased, then with confidence **78.66%** `R03` will also be purchased. This rule has a lift ratio of
**1.0214**.

If `M01AB, N02BA, R06, N02BE` is purchased, then with confidence **78.66%** `R03` will also be purchased. This rule has a lift ratio of
**1.0214**.

If `N05B, M01AB, N02BA, R06` is purchased, then with confidence **78.65%** `R03` will also be purchased. This rule has a lift ratio of
**1.0212**.

If `R06, M01AB, N02BA, N05B, N02BE` is purchased, then with confidence **78.65%** `R03` will also be purchased. This rule has a lift ratio of
**1.0212**.

If `M01AE, R06, M01AB, N02BA, N05B, N02BE` is purchased, then with confidence **78.62%** `R03` will also be purchased. This rule has a lift ratio of **1.0208**.

If `M01AE, R06, M01AB, N02BA, N05B` is purchased, then with confidence **78.62%** `R03` will also be purchased. This rule has a lift ratio of
**1.0208**.

The support for the rule indicates its impact in terms of overall size: How many transactions are affected? If
only a small number of transactions are affected, the rule may be of little use (unless the consequent is very
valuable and/or the rule is very efficient in finding it).

• The lift ratio indicates how efficient the rule is in finding consequents, compared to random selection. A very
efficient rule is preferred to an inefficient rule, but we must still consider support: A very efficient rule that
has very low support may not be as desirable as a less efficient rule with much greater support.

• The confidence tells us at what rate consequents will be found and is useful in determining the business or
operational usefulness of a rule: A rule with low confidence may find consequents at too low a rate to be
worth the cost of (say) promoting the consequent in all the transactions that involve the antecedent.

## Time Series Forecasting

### M01AB 

#### Plots that enhance the different components of the time series

(a) Zoom-in to 1 year of data 

(b) Original series with overlaid quadratic trendline

![download](https://user-images.githubusercontent.com/70437668/173319464-ff180ab3-0963-4861-b707-9fa1220055dc.png)

#### Naive and Seasonal Naive Forecasts in a 3-year validation set for M01AB

![download (1)](https://user-images.githubusercontent.com/70437668/173319686-e8cc73b2-17b4-4812-8fdf-91f26877f4a9.png)

#### Predictive accuracy of naive and seasonal naive forecasts in the validation and training set for M01AB

Table below compares the accuracies of these two naive forecasts.
Because M01AB has monthly seasonality, the seasonal naive forecast is the clear winner on both training and validation and
on all popular measures. In choosing between the two models, the accuracy on the validation set is more relevant than the accuracy on the training set. Performance on the validation set is more indicative of how the models will perform in the future.

##### Validation set

```
regressionSummary(valid_ts_M01AB, naive_pred_M01AB)
```

```
Regression statistics

                      Mean Error (ME) : 0.1731
       Root Mean Squared Error (RMSE) : 2.7432
            Mean Absolute Error (MAE) : 2.2325
          Mean Percentage Error (MPE) : -70.3831
Mean Absolute Percentage Error (MAPE) : 98.4098
```

```
 regressionSummary(valid_ts_M01AB, seasonal_pred_M01AB)
```

```
Regression statistics

                      Mean Error (ME) : -0.1253
       Root Mean Squared Error (RMSE) : 4.5251
            Mean Absolute Error (MAE) : 3.6464
          Mean Percentage Error (MPE) : -75.0077
Mean Absolute Percentage Error (MAPE) : 121.3996
```

##### Training set

```
# Calculate naive metrics for training set (shifted by 1 month)
regressionSummary(train_ts_M01AB[1:], train_ts_M01AB[:-1])
```

```
Regression statistics

               Mean Error (ME) : 0.0026
Root Mean Squared Error (RMSE) : 3.7529
     Mean Absolute Error (MAE) : 2.9228
```

```
 # Calculate seasonal naive metrics for training set (shifted by 12 months)
regressionSummary(train_ts_M01AB[12:], train_ts_M01AB[:-12])
```

```
Regression statistics

               Mean Error (ME) : 0.0082
Root Mean Squared Error (RMSE) : 3.7524
     Mean Absolute Error (MAE) : 2.9416
```

## Regression-Based Foreacasting

### Linear Regression

#### A linear trend fit to M01AB in the training period and forecasted in the validation period

![download (2)](https://user-images.githubusercontent.com/70437668/173328494-cd1c1417-6ea7-4fec-a8f2-088488838612.png)


#### Summary
```
OLS Regression Results
Dep. Variable:	M01AB_Sales	R-squared:	0.010
Model:	OLS	Adj. R-squared:	0.009
Method:	Least Squares	F-statistic:	20.12
Date:	Mon, 13 Jun 2022	Prob (F-statistic):	7.69e-06
Time:	09:36:11	Log-Likelihood:	-5010.8
No. Observations:	2070	AIC:	1.003e+04
Df Residuals:	2068	BIC:	1.004e+04
Df Model:	1		
Covariance Type:	nonrobust		
coef	std err	t	P>|t|	[0.025	0.975]
Intercept	4.5601	0.120	38.064	0.000	4.325	4.795
trend	0.0004	0.000	4.485	0.000	0.000	0.001
Omnibus:	137.713	Durbin-Watson:	1.899
Prob(Omnibus):	0.000	Jarque-Bera (JB):	168.796
Skew:	0.635	Prob(JB):	2.22e-37
Kurtosis:	3.586	Cond. No.	2.39e+03


Warnings:
[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
[2] The condition number is large, 2.39e+03. This might indicate that there are
strong multicollinearity or other numerical problems.
```

### Exponential Regression

![download (3)](https://user-images.githubusercontent.com/70437668/173328669-4f66a2cc-6343-4ccf-83eb-1b67fefab10a.png)


### Polynomial Regression

#### Quadratic trend model used to forecast M01AB. Plots of fitted, forecasted, and actual values (a) and forecast errors (b)

![download (4)](https://user-images.githubusercontent.com/70437668/173328690-031d653b-dc7d-4e2e-b0c3-71998334cf28.png)

#### Summary of Polynomial Regression with Quadratic Trend

```
OLS Regression Results
Dep. Variable:	M01AB_Sales	R-squared:	0.022
Model:	OLS	Adj. R-squared:	0.021
Method:	Least Squares	F-statistic:	23.60
Date:	Mon, 13 Jun 2022	Prob (F-statistic):	7.36e-11
Time:	09:49:36	Log-Likelihood:	-4997.4
No. Observations:	2070	AIC:	1.000e+04
Df Residuals:	2067	BIC:	1.002e+04
Df Model:	2		
Covariance Type:	nonrobust		
coef	std err	t	P>|t|	[0.025	0.975]
Intercept	3.8699	0.179	21.656	0.000	3.519	4.220
trend	0.0024	0.000	6.143	0.000	0.002	0.003
np.square(trend)	-9.651e-07	1.86e-07	-5.180	0.000	-1.33e-06	-6e-07
Omnibus:	136.147	Durbin-Watson:	1.923
Prob(Omnibus):	0.000	Jarque-Bera (JB):	167.470
Skew:	0.626	Prob(JB):	4.31e-37
Kurtosis:	3.610	Cond. No.	5.76e+06


Warnings:
[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
[2] The condition number is large, 5.76e+06. This might indicate that there are
strong multicollinearity or other numerical problems.
```

#### Summary of output from fitting additive seasonality to the M01AB data in the training period

```
OLS Regression Results
Dep. Variable:	M01AB_Sales	R-squared:	0.005
Model:	OLS	Adj. R-squared:	-0.001
Method:	Least Squares	F-statistic:	0.8905
Date:	Mon, 13 Jun 2022	Prob (F-statistic):	0.549
Time:	09:39:19	Log-Likelihood:	-5015.9
No. Observations:	2070	AIC:	1.006e+04
Df Residuals:	2058	BIC:	1.012e+04
Df Model:	11		
Covariance Type:	nonrobust		
coef	std err	t	P>|t|	[0.025	0.975]
Intercept	5.0223	0.201	24.952	0.000	4.628	5.417
C(Month)[T.2]	-0.0228	0.291	-0.078	0.938	-0.594	0.548
C(Month)[T.3]	-0.1102	0.284	-0.388	0.698	-0.668	0.447
C(Month)[T.4]	0.0956	0.287	0.334	0.739	-0.466	0.658
C(Month)[T.5]	-0.1762	0.284	-0.620	0.536	-0.734	0.381
C(Month)[T.6]	-0.3076	0.287	-1.073	0.283	-0.870	0.255
C(Month)[T.7]	0.1856	0.284	0.653	0.514	-0.372	0.743
C(Month)[T.8]	0.4060	0.284	1.428	0.153	-0.151	0.963
C(Month)[T.9]	-0.1069	0.300	-0.357	0.721	-0.695	0.481
C(Month)[T.10]	-0.0797	0.298	-0.267	0.789	-0.664	0.505
C(Month)[T.11]	0.2033	0.301	0.676	0.499	-0.387	0.793
C(Month)[T.12]	-0.0649	0.298	-0.218	0.828	-0.650	0.520
Omnibus:	142.033	Durbin-Watson:	1.889
Prob(Omnibus):	0.000	Jarque-Bera (JB):	175.275
Skew:	0.646	Prob(JB):	8.70e-39
Kurtosis:	3.603	Cond. No.	12.5


Warnings:
[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
```

#### Regression model with seasonality applied to the M01AB (a) and its forecast errors (b)

![download (5)](https://user-images.githubusercontent.com/70437668/173329014-9f2833e6-6e66-42f9-a04a-12cd036098eb.png)

#### Regression model with trend and seasonality applied to M01AB (a) and its forecast errors (b)

![download (6)](https://user-images.githubusercontent.com/70437668/173329152-14a94ab8-3ec6-477b-a8e2-ea65d415cfbf.png)

#### Summary of output from fitting trend and seasonality to M01AB in the training period

```
OLS Regression Results
Dep. Variable:	M01AB_Sales	R-squared:	0.027
Model:	OLS	Adj. R-squared:	0.021
Method:	Least Squares	F-statistic:	4.433
Date:	Mon, 13 Jun 2022	Prob (F-statistic):	1.80e-07
Time:	09:44:24	Log-Likelihood:	-4992.2
No. Observations:	2070	AIC:	1.001e+04
Df Residuals:	2056	BIC:	1.009e+04
Df Model:	13		
Covariance Type:	nonrobust		
coef	std err	t	P>|t|	[0.025	0.975]
Intercept	3.9320	0.254	15.459	0.000	3.433	4.431
C(Month)[T.2]	-0.0370	0.288	-0.129	0.898	-0.602	0.528
C(Month)[T.3]	-0.1398	0.281	-0.497	0.619	-0.691	0.412
C(Month)[T.4]	0.0505	0.284	0.178	0.859	-0.506	0.607
C(Month)[T.5]	-0.2348	0.281	-0.835	0.404	-0.787	0.317
C(Month)[T.6]	-0.3780	0.284	-1.332	0.183	-0.935	0.179
C(Month)[T.7]	0.1053	0.282	0.374	0.709	-0.447	0.658
C(Month)[T.8]	0.3175	0.282	1.126	0.260	-0.235	0.870
C(Month)[T.9]	-0.2555	0.297	-0.859	0.390	-0.839	0.328
C(Month)[T.10]	-0.2480	0.296	-0.838	0.402	-0.828	0.333
C(Month)[T.11]	0.0214	0.299	0.072	0.943	-0.564	0.607
C(Month)[T.12]	-0.2585	0.296	-0.873	0.383	-0.839	0.322
trend	0.0025	0.000	6.235	0.000	0.002	0.003
np.square(trend)	-1.005e-06	1.89e-07	-5.309	0.000	-1.38e-06	-6.34e-07
Omnibus:	135.228	Durbin-Watson:	1.934
Prob(Omnibus):	0.000	Jarque-Bera (JB):	166.110
Skew:	0.624	Prob(JB):	8.50e-37
Kurtosis:	3.607	Cond. No.	2.31e+07


Warnings:
[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
[2] The condition number is large, 2.31e+07. This might indicate that there are
strong multicollinearity or other numerical problems.
```

# Reference:

Pharma sales data analysis and forecasting by MILAN ZDRAVKOVIĆ: https://www.kaggle.com/code/milanzdravkovic/pharma-sales-data-analysis-and-forecasting
