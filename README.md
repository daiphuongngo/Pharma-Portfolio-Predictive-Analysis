# Pharma-Portfolio-Predictive-Analysis

## Overview:

This repository contains my work on the Pharma Sales Data's Forecast and Analysis. This project is underway.

## Languages & Tools:

- `Python`

- `Machine Learning`

- `Azure Machine Learning Studio`

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

`SQL`
```
SELECT Weekday_Name, sum(M01AE) AS sum_M01AE
FROM t1
GROUP BY Weekday_Name
ORDER BY sum_M01AE ASC
```
