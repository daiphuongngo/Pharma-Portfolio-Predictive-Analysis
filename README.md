# Pharma-Portfolio-Predictive-Analysis

## Overview:

This repository contains my work on the Pharma Sales Data's Forecast and Analysis. This project is underway.

## Languages & Tools:

- `Python`

- `Machine Learning`

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

`SQL`

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
