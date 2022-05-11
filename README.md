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

## Stationarity Analysis (to be continued)

## Machine Learning in Python and Azure (to be continued)

- Linear Regression

- Polynomial Regression

- Simple Vector Regression (SVR)

- Voting Regressor's results

@Google Colab `Python`


@Azure-Machine-Learning-Studio


