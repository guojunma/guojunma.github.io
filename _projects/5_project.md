---
jupyter:
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.9.12
  nbformat: 4
  nbformat_minor: 5
  papermill:
    default_parameters: {}
    duration: 212.249929
    end_time: "2023-01-31T12:56:57.092165"
    environment_variables: {}
    input_path: \_\_notebook\_\_.ipynb
    output_path: \_\_notebook\_\_.ipynb
    parameters: {}
    start_time: "2023-01-31T12:53:24.842236"
    version: 2.3.4
---

::: {#1a5343f8 .cell .markdown papermill="{\"duration\":1.3433e-2,\"end_time\":\"2023-01-31T12:53:33.338639\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:33.325206\",\"status\":\"completed\"}" tags="[]"}
# Data Project - Stock Market Analysis

![techAnalysis-1000x500.jpg](vertopal_a579fb8fa69546c39551d8bfbeb13562/techAnalysis-1000x500.jpg)
:::

::: {#680b164c .cell .markdown papermill="{\"duration\":1.1525e-2,\"end_time\":\"2023-01-31T12:53:33.362147\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:33.350622\",\"status\":\"completed\"}" tags="[]"}
In this project, we explore financial data from the stock market,
particularly technology stocks. Financial data is an example of time
series data, which is one of the most prevalent data types characterized
by a series of data points indexed in time order. We will get the stock
data from the Yahoo finance website, which is a rich resource for
financial market data. By analyzing these data, we aim to answer the
following questions:

    1.) What was the average change in prices of the stock over time?
    2.) What was the correlation between different stocks?
    3.) How much value do we put at risk by investing in a particular stock?
    4.) How can we predict the future stock behavior? (For example, predicting the closing price stock price of APPLE inc.)

------------------------------------------------------------------------

## Getting the Data

The first step is to get the data and load it to memory. We will get our
stock data from the Yahoo Finance website. Yahoo Finance is a rich
resource of financial market data and tools to find compelling
investments. To get the data from Yahoo Finance, we will be using
yfinance library which offers a threaded and Pythonic way to download
market data from Yahoo. Check this article to learn more about yfinance:
[Reliably download historical market data from with
Python](https://aroussi.com/post/python-yahoo-finance)
:::

::: {#e7bdae83 .cell .markdown papermill="{\"duration\":1.1471e-2,\"end_time\":\"2023-01-31T12:53:33.385342\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:33.373871\",\"status\":\"completed\"}" tags="[]"}
# 1. Getting the Data {#1-getting-the-data}

In this section, we load the required packages and download the
financial data. We will get our stock data from the Yahoo Finance
website, which is a rich resource of financial market data and tools. We
are using [yfinance
library](https://aroussi.com/post/python-yahoo-finance) which offers a
programatics way to download market data from Yahoo.
:::

::: {#e11e8f6e .cell .code execution_count="1" execution="{\"iopub.execute_input\":\"2023-01-31T12:53:48.911805Z\",\"iopub.status.busy\":\"2023-01-31T12:53:48.911391Z\",\"iopub.status.idle\":\"2023-01-31T12:53:53.965505Z\",\"shell.execute_reply\":\"2023-01-31T12:53:53.964183Z\"}" papermill="{\"duration\":5.070071,\"end_time\":\"2023-01-31T12:53:53.967840\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:48.897769\",\"status\":\"completed\"}" tags="[]"}
``` python
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('whitegrid')
plt.style.use("fivethirtyeight")
%matplotlib inline

# For reading stock data from yahoo
from pandas_datareader.data import DataReader
import yfinance as yf
from pandas_datareader import data as pdr

yf.pdr_override()

# For time stamps
from datetime import datetime


# The tech stocks we'll use for this analysis
tech_list = ['AAPL', 'GOOG', 'MSFT', 'AMZN']

# Set up End and Start times for data grab
tech_list = ['AAPL', 'GOOG', 'MSFT', 'AMZN']

end = datetime.now()
start = datetime(end.year - 1, end.month, end.day)

for stock in tech_list:
    globals()[stock] = yf.download(stock, start, end)
    

company_list = [AAPL, GOOG, MSFT, AMZN]
company_name = ["APPLE", "GOOGLE", "MICROSOFT", "AMAZON"]

for company, com_name in zip(company_list, company_name):
    company["company_name"] = com_name
    
df = pd.concat(company_list, axis=0)
df.tail(10)
```

::: {.output .stream .stderr}
    [*********************100%%**********************]  1 of 1 completed
    [*********************100%%**********************]  1 of 1 completed
    [*********************100%%**********************]  1 of 1 completed
    [*********************100%%**********************]  1 of 1 completed
:::

::: {.output .execute_result execution_count="1"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
      <th>company_name</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2024-02-20</th>
      <td>167.830002</td>
      <td>168.710007</td>
      <td>165.740005</td>
      <td>167.080002</td>
      <td>167.080002</td>
      <td>41980300</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-02-21</th>
      <td>168.940002</td>
      <td>170.229996</td>
      <td>167.139999</td>
      <td>168.589996</td>
      <td>168.589996</td>
      <td>44575600</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-02-22</th>
      <td>173.100006</td>
      <td>174.800003</td>
      <td>171.770004</td>
      <td>174.580002</td>
      <td>174.580002</td>
      <td>55392400</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-02-23</th>
      <td>174.279999</td>
      <td>175.750000</td>
      <td>173.699997</td>
      <td>174.990005</td>
      <td>174.990005</td>
      <td>59715200</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-02-26</th>
      <td>175.699997</td>
      <td>176.369995</td>
      <td>174.259995</td>
      <td>174.729996</td>
      <td>174.729996</td>
      <td>44368600</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-02-27</th>
      <td>174.080002</td>
      <td>174.619995</td>
      <td>172.860001</td>
      <td>173.539993</td>
      <td>173.539993</td>
      <td>31141700</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-02-28</th>
      <td>172.440002</td>
      <td>174.050003</td>
      <td>172.270004</td>
      <td>173.160004</td>
      <td>173.160004</td>
      <td>28180500</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-02-29</th>
      <td>173.009995</td>
      <td>177.220001</td>
      <td>172.850006</td>
      <td>176.759995</td>
      <td>176.759995</td>
      <td>53805400</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-03-01</th>
      <td>176.750000</td>
      <td>178.729996</td>
      <td>176.070007</td>
      <td>178.220001</td>
      <td>178.220001</td>
      <td>31956200</td>
      <td>AMAZON</td>
    </tr>
    <tr>
      <th>2024-03-04</th>
      <td>177.529999</td>
      <td>180.139999</td>
      <td>177.490005</td>
      <td>177.580002</td>
      <td>177.580002</td>
      <td>36357160</td>
      <td>AMAZON</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#2c53382f .cell .markdown papermill="{\"duration\":1.3271e-2,\"end_time\":\"2023-01-31T12:53:53.994686\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:53.981415\",\"status\":\"completed\"}" tags="[]"}
Reviewing the content of our data, we can see that the data is numeric
and the date is the index of the data. Notice also that weekends are
missing from the records.
:::

::: {#d60ba9bf .cell .markdown papermill="{\"duration\":1.261e-2,\"end_time\":\"2023-01-31T12:53:54.020497\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:54.007887\",\"status\":\"completed\"}" tags="[]"}
## Descriptive Statistics about the Data

`.describe()` generates descriptive statistics. Descriptive statistics
include those that summarize the central tendency, dispersion, and shape
of a dataset's distribution, excluding `NaN` values.

Analyzes both numeric and object series, as well as `DataFrame` column
sets of mixed data types. The output will vary depending on what is
provided. Refer to the notes below for more detail.
:::

::: {#60465e63 .cell .code execution_count="3" execution="{\"iopub.execute_input\":\"2023-01-31T12:53:54.049732Z\",\"iopub.status.busy\":\"2023-01-31T12:53:54.048892Z\",\"iopub.status.idle\":\"2023-01-31T12:53:54.079662Z\",\"shell.execute_reply\":\"2023-01-31T12:53:54.078450Z\"}" papermill="{\"duration\":4.9011e-2,\"end_time\":\"2023-01-31T12:53:54.082514\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:54.033503\",\"status\":\"completed\"}" tags="[]"}
``` python
# Summary Stats
AAPL.describe()
```

::: {.output .execute_result execution_count="3"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>251.000000</td>
      <td>251.000000</td>
      <td>251.000000</td>
      <td>251.000000</td>
      <td>251.000000</td>
      <td>2.510000e+02</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>152.117251</td>
      <td>154.227052</td>
      <td>150.098406</td>
      <td>152.240797</td>
      <td>151.861737</td>
      <td>8.545738e+07</td>
    </tr>
    <tr>
      <th>std</th>
      <td>13.239204</td>
      <td>13.124055</td>
      <td>13.268053</td>
      <td>13.255593</td>
      <td>13.057870</td>
      <td>2.257398e+07</td>
    </tr>
    <tr>
      <th>min</th>
      <td>126.010002</td>
      <td>127.769997</td>
      <td>124.169998</td>
      <td>125.019997</td>
      <td>125.019997</td>
      <td>3.519590e+07</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>142.110001</td>
      <td>143.854996</td>
      <td>139.949997</td>
      <td>142.464996</td>
      <td>142.190201</td>
      <td>7.027710e+07</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>150.089996</td>
      <td>151.990005</td>
      <td>148.199997</td>
      <td>150.649994</td>
      <td>150.400497</td>
      <td>8.100050e+07</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>163.434998</td>
      <td>165.835007</td>
      <td>160.879997</td>
      <td>163.629997</td>
      <td>163.200417</td>
      <td>9.374540e+07</td>
    </tr>
    <tr>
      <th>max</th>
      <td>178.550003</td>
      <td>179.610001</td>
      <td>176.699997</td>
      <td>178.960007</td>
      <td>178.154037</td>
      <td>1.826020e+08</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#47806cf9 .cell .markdown papermill="{\"duration\":1.2936e-2,\"end_time\":\"2023-01-31T12:53:54.109754\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:54.096818\",\"status\":\"completed\"}" tags="[]"}
We have only 255 records in one year because weekends are not included
in the data.
:::

::: {#b419c5b2 .cell .markdown papermill="{\"duration\":1.3036e-2,\"end_time\":\"2023-01-31T12:53:54.136260\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:54.123224\",\"status\":\"completed\"}" tags="[]"}
## Information About the Data

`.info()` method prints information about a DataFrame including the
index `dtype` and columns, non-null values, and memory usage.
:::

::: {#93783cc3 .cell .code execution_count="4" execution="{\"iopub.execute_input\":\"2023-01-31T12:53:54.164746Z\",\"iopub.status.busy\":\"2023-01-31T12:53:54.164367Z\",\"iopub.status.idle\":\"2023-01-31T12:53:54.181713Z\",\"shell.execute_reply\":\"2023-01-31T12:53:54.180421Z\"}" papermill="{\"duration\":3.4359e-2,\"end_time\":\"2023-01-31T12:53:54.183931\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:54.149572\",\"status\":\"completed\"}" tags="[]"}
``` python
# General info
AAPL.info()
```

::: {.output .stream .stdout}
    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 251 entries, 2022-01-31 00:00:00-05:00 to 2023-01-30 00:00:00-05:00
    Data columns (total 7 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   Open          251 non-null    float64
     1   High          251 non-null    float64
     2   Low           251 non-null    float64
     3   Close         251 non-null    float64
     4   Adj Close     251 non-null    float64
     5   Volume        251 non-null    int64  
     6   company_name  251 non-null    object 
    dtypes: float64(5), int64(1), object(1)
    memory usage: 23.8+ KB
:::
:::

::: {#faf6d2fa .cell .markdown papermill="{\"duration\":1.3371e-2,\"end_time\":\"2023-01-31T12:53:54.210787\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:54.197416\",\"status\":\"completed\"}" tags="[]"}
## Closing Price

The closing price is the last price at which the stock is traded during
the regular trading day. A stock's closing price is the standard
benchmark used by investors to track its performance over time.
:::

::: {#b13ddab8 .cell .code execution_count="2" execution="{\"iopub.execute_input\":\"2023-01-31T12:53:54.239480Z\",\"iopub.status.busy\":\"2023-01-31T12:53:54.238719Z\",\"iopub.status.idle\":\"2023-01-31T12:53:55.692901Z\",\"shell.execute_reply\":\"2023-01-31T12:53:55.691450Z\"}" papermill="{\"duration\":1.472316,\"end_time\":\"2023-01-31T12:53:55.696413\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:54.224097\",\"status\":\"completed\"}" tags="[]"}
``` python
# Let's see a historical view of the closing price
plt.figure(figsize=(15, 10))
plt.subplots_adjust(top=1.25, bottom=1.2)

for i, company in enumerate(company_list, 1):
    plt.subplot(2, 2, i)
    company['Adj Close'].plot()
    plt.ylabel('Adj Close')
    plt.xlabel(None)
    plt.title(f"Closing Price of {tech_list[i - 1]}")
    
plt.tight_layout()
```

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/68f2406c94a63e3aa8fa55faf615805cf9f5fc0f.png)
:::
:::

::: {#247963fc .cell .markdown papermill="{\"duration\":1.5215e-2,\"end_time\":\"2023-01-31T12:53:55.728097\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:55.712882\",\"status\":\"completed\"}" tags="[]"}
## Volume of Sales

Volume is the amount of an asset or security that changes hands over
some period of time, often over the course of a day. For instance, the
stock trading volume would refer to the number of shares of security
traded between its daily open and close. Trading volume, and changes to
volume over the course of time, are important inputs for technical
traders.
:::

::: {#40a52d2f .cell .code execution_count="6" execution="{\"iopub.execute_input\":\"2023-01-31T12:53:55.763022Z\",\"iopub.status.busy\":\"2023-01-31T12:53:55.762611Z\",\"iopub.status.idle\":\"2023-01-31T12:53:57.175013Z\",\"shell.execute_reply\":\"2023-01-31T12:53:57.173744Z\"}" papermill="{\"duration\":1.4345,\"end_time\":\"2023-01-31T12:53:57.178658\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:55.744158\",\"status\":\"completed\"}" tags="[]"}
``` python
# Now let's plot the total volume of stock being traded each day
plt.figure(figsize=(15, 10))
plt.subplots_adjust(top=1.25, bottom=1.2)

for i, company in enumerate(company_list, 1):
    plt.subplot(2, 2, i)
    company['Volume'].plot()
    plt.ylabel('Volume')
    plt.xlabel(None)
    plt.title(f"Sales Volume for {tech_list[i - 1]}")
    
plt.tight_layout()
```

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/a14c01c9e883b2afed95ac1f963b31594d3d7e19.png)
:::
:::

::: {#b443cd3d .cell .markdown papermill="{\"duration\":1.7594e-2,\"end_time\":\"2023-01-31T12:53:57.214684\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:57.197090\",\"status\":\"completed\"}" tags="[]"}
Now that we\'ve seen the visualizations for the closing price and the
volume traded each day, let\'s go ahead and caculate the moving average
for the stock.
:::

::: {#8f2b7c0a .cell .markdown papermill="{\"duration\":1.7533e-2,\"end_time\":\"2023-01-31T12:53:57.249955\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:57.232422\",\"status\":\"completed\"}" tags="[]"}
# 2. What was the moving average of the various stocks? {#2-what-was-the-moving-average-of-the-various-stocks}

The moving average (MA) is a simple technical analysis tool that smooths
out price data by creating a constantly updated average price. The
average is taken over a specific period of time, like 10 days, 20
minutes, 30 weeks, or any time period the trader chooses.
:::

::: {#70c00b63 .cell .code execution_count="7" execution="{\"iopub.execute_input\":\"2023-01-31T12:53:57.288379Z\",\"iopub.status.busy\":\"2023-01-31T12:53:57.287938Z\",\"iopub.status.idle\":\"2023-01-31T12:53:59.042433Z\",\"shell.execute_reply\":\"2023-01-31T12:53:59.041484Z\"}" papermill="{\"duration\":1.779798,\"end_time\":\"2023-01-31T12:53:59.047606\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:57.267808\",\"status\":\"completed\"}" tags="[]"}
``` python
ma_day = [10, 20, 50]

for ma in ma_day:
    for company in company_list:
        column_name = f"MA for {ma} days"
        company[column_name] = company['Adj Close'].rolling(ma).mean()
        

fig, axes = plt.subplots(nrows=2, ncols=2)
fig.set_figheight(10)
fig.set_figwidth(15)

AAPL[['Adj Close', 'MA for 10 days', 'MA for 20 days', 'MA for 50 days']].plot(ax=axes[0,0])
axes[0,0].set_title('APPLE')

GOOG[['Adj Close', 'MA for 10 days', 'MA for 20 days', 'MA for 50 days']].plot(ax=axes[0,1])
axes[0,1].set_title('GOOGLE')

MSFT[['Adj Close', 'MA for 10 days', 'MA for 20 days', 'MA for 50 days']].plot(ax=axes[1,0])
axes[1,0].set_title('MICROSOFT')

AMZN[['Adj Close', 'MA for 10 days', 'MA for 20 days', 'MA for 50 days']].plot(ax=axes[1,1])
axes[1,1].set_title('AMAZON')

fig.tight_layout()
```

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/70b00d56c3196deadd40a26bee6120ef86d82eb1.png)
:::
:::

::: {#deb18236 .cell .markdown papermill="{\"duration\":2.3365e-2,\"end_time\":\"2023-01-31T12:53:59.094496\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:59.071131\",\"status\":\"completed\"}" tags="[]"}
We see in the graph that the best values to measure the moving average
are 10 and 20 days because we still capture trends in the data without
noise.
:::

::: {#6aa540d2 .cell .markdown papermill="{\"duration\":2.1563e-2,\"end_time\":\"2023-01-31T12:53:59.137965\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:59.116402\",\"status\":\"completed\"}" tags="[]"}
# 3. What was the daily return of the stock on average? {#3-what-was-the-daily-return-of-the-stock-on-average}
:::

::: {#921824c7 .cell .markdown papermill="{\"duration\":2.1726e-2,\"end_time\":\"2023-01-31T12:53:59.182189\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:59.160463\",\"status\":\"completed\"}" tags="[]"}
Now that we\'ve done some baseline analysis, let\'s go ahead and dive a
little deeper. We\'re now going to analyze the risk of the stock. In
order to do so we\'ll need to take a closer look at the daily changes of
the stock, and not just its absolute value. Let\'s go ahead and use
pandas to retrieve teh daily returns for the Apple stock.
:::

::: {#b9de09fe .cell .code execution_count="8" execution="{\"iopub.execute_input\":\"2023-01-31T12:53:59.227869Z\",\"iopub.status.busy\":\"2023-01-31T12:53:59.227496Z\",\"iopub.status.idle\":\"2023-01-31T12:54:00.704908Z\",\"shell.execute_reply\":\"2023-01-31T12:54:00.703635Z\"}" papermill="{\"duration\":1.505263,\"end_time\":\"2023-01-31T12:54:00.709370\",\"exception\":false,\"start_time\":\"2023-01-31T12:53:59.204107\",\"status\":\"completed\"}" tags="[]"}
``` python
# We'll use pct_change to find the percent change for each day
for company in company_list:
    company['Daily Return'] = company['Adj Close'].pct_change()

# Then we'll plot the daily return percentage
fig, axes = plt.subplots(nrows=2, ncols=2)
fig.set_figheight(10)
fig.set_figwidth(15)

AAPL['Daily Return'].plot(ax=axes[0,0], legend=True, linestyle='--', marker='o')
axes[0,0].set_title('APPLE')

GOOG['Daily Return'].plot(ax=axes[0,1], legend=True, linestyle='--', marker='o')
axes[0,1].set_title('GOOGLE')

MSFT['Daily Return'].plot(ax=axes[1,0], legend=True, linestyle='--', marker='o')
axes[1,0].set_title('MICROSOFT')

AMZN['Daily Return'].plot(ax=axes[1,1], legend=True, linestyle='--', marker='o')
axes[1,1].set_title('AMAZON')

fig.tight_layout()
```

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/d636a18506e84e0a2ca9832ba294d9e65421aafe.png)
:::
:::

::: {#b4947a4f .cell .markdown papermill="{\"duration\":2.583e-2,\"end_time\":\"2023-01-31T12:54:00.762088\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:00.736258\",\"status\":\"completed\"}" tags="[]"}
Great, now let\'s get an overall look at the average daily return using
a histogram. We\'ll use seaborn to create both a histogram and kde plot
on the same figure.
:::

::: {#2740efe4 .cell .code execution_count="9" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:00.814667Z\",\"iopub.status.busy\":\"2023-01-31T12:54:00.814276Z\",\"iopub.status.idle\":\"2023-01-31T12:54:02.165765Z\",\"shell.execute_reply\":\"2023-01-31T12:54:02.164503Z\"}" papermill="{\"duration\":1.380741,\"end_time\":\"2023-01-31T12:54:02.168271\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:00.787530\",\"status\":\"completed\"}" tags="[]"}
``` python
plt.figure(figsize=(12, 9))

for i, company in enumerate(company_list, 1):
    plt.subplot(2, 2, i)
    company['Daily Return'].hist(bins=50)
    plt.xlabel('Daily Return')
    plt.ylabel('Counts')
    plt.title(f'{company_name[i - 1]}')
    
plt.tight_layout()
```

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/17f0ff2ffd4cb148299a8404264b7e8cefb056c8.png)
:::
:::

::: {#dea5b30a .cell .markdown papermill="{\"duration\":2.5887e-2,\"end_time\":\"2023-01-31T12:54:02.220637\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:02.194750\",\"status\":\"completed\"}" tags="[]"}
# 4. What was the correlation between different stocks closing prices? {#4-what-was-the-correlation-between-different-stocks-closing-prices}
:::

::: {#993377ef .cell .markdown papermill="{\"duration\":2.5914e-2,\"end_time\":\"2023-01-31T12:54:02.272691\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:02.246777\",\"status\":\"completed\"}" tags="[]"}
Correlation is a statistic that measures the degree to which two
variables move in relation to each other which has a value that must
fall between -1.0 and +1.0. Correlation measures association, but
doesn't show if x causes y or vice versa --- or if the association is
caused by a third factor\[1\].

Now what if we wanted to analyze the returns of all the stocks in our
list? Let\'s go ahead and build a DataFrame with all the \[\'Close\'\]
columns for each of the stocks dataframes.
:::

::: {#1841b077 .cell .code execution_count="10" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:02.327584Z\",\"iopub.status.busy\":\"2023-01-31T12:54:02.327175Z\",\"iopub.status.idle\":\"2023-01-31T12:54:02.873181Z\",\"shell.execute_reply\":\"2023-01-31T12:54:02.872046Z\"}" papermill="{\"duration\":0.576523,\"end_time\":\"2023-01-31T12:54:02.875608\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:02.299085\",\"status\":\"completed\"}" tags="[]"}
``` python
# Grab all the closing prices for the tech stock list into one DataFrame

closing_df = pdr.get_data_yahoo(tech_list, start=start, end=end)['Adj Close']

# Make a new tech returns DataFrame
tech_rets = closing_df.pct_change()
tech_rets.head()
```

::: {.output .stream .stdout}
    [*********************100%***********************]  4 of 4 completed
:::

::: {.output .execute_result execution_count="10"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>AAPL</th>
      <th>AMZN</th>
      <th>GOOG</th>
      <th>MSFT</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2022-01-31 00:00:00-05:00</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2022-02-01 00:00:00-05:00</th>
      <td>-0.000973</td>
      <td>0.010831</td>
      <td>0.016065</td>
      <td>-0.007139</td>
    </tr>
    <tr>
      <th>2022-02-02 00:00:00-05:00</th>
      <td>0.007044</td>
      <td>-0.003843</td>
      <td>0.073674</td>
      <td>0.015222</td>
    </tr>
    <tr>
      <th>2022-02-03 00:00:00-05:00</th>
      <td>-0.016720</td>
      <td>-0.078128</td>
      <td>-0.036383</td>
      <td>-0.038952</td>
    </tr>
    <tr>
      <th>2022-02-04 00:00:00-05:00</th>
      <td>-0.001679</td>
      <td>0.135359</td>
      <td>0.002562</td>
      <td>0.015568</td>
    </tr>
  </tbody>
</table>
</div>
```
:::
:::

::: {#6e16df5d .cell .markdown papermill="{\"duration\":2.6148e-2,\"end_time\":\"2023-01-31T12:54:02.928465\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:02.902317\",\"status\":\"completed\"}" tags="[]"}
Now we can compare the daily percentage return of two stocks to check
how correlated. First let\'s see a sotck compared to itself.
:::

::: {#aa4a48af .cell .code execution_count="11" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:02.983652Z\",\"iopub.status.busy\":\"2023-01-31T12:54:02.982615Z\",\"iopub.status.idle\":\"2023-01-31T12:54:03.610584Z\",\"shell.execute_reply\":\"2023-01-31T12:54:03.609703Z\"}" papermill="{\"duration\":0.657839,\"end_time\":\"2023-01-31T12:54:03.612759\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:02.954920\",\"status\":\"completed\"}" tags="[]"}
``` python
# Comparing Google to itself should show a perfectly linear relationship
sns.jointplot(x='GOOG', y='GOOG', data=tech_rets, kind='scatter', color='seagreen')
```

::: {.output .execute_result execution_count="11"}
    <seaborn.axisgrid.JointGrid at 0x7f63e33d4990>
:::

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/07e379a8fe29b77476f38199a06deb922e5a6304.png)
:::
:::

::: {#9771e36a .cell .code execution_count="12" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:03.671117Z\",\"iopub.status.busy\":\"2023-01-31T12:54:03.670077Z\",\"iopub.status.idle\":\"2023-01-31T12:54:04.290381Z\",\"shell.execute_reply\":\"2023-01-31T12:54:04.289200Z\"}" papermill="{\"duration\":0.651554,\"end_time\":\"2023-01-31T12:54:04.293282\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:03.641728\",\"status\":\"completed\"}" tags="[]"}
``` python
# We'll use joinplot to compare the daily returns of Google and Microsoft
sns.jointplot(x='GOOG', y='MSFT', data=tech_rets, kind='scatter')
```

::: {.output .execute_result execution_count="12"}
    <seaborn.axisgrid.JointGrid at 0x7f63dba49210>
:::

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/2f01d104f93f54520edcd1cdfddaf337ce654134.png)
:::
:::

::: {#adc87028 .cell .markdown papermill="{\"duration\":3.0214e-2,\"end_time\":\"2023-01-31T12:54:04.353407\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:04.323193\",\"status\":\"completed\"}" tags="[]"}
So now we can see that if two stocks are perfectly (and positivley)
correlated with each other a linear relationship bewteen its daily
return values should occur.

Seaborn and pandas make it very easy to repeat this comparison analysis
for every possible combination of stocks in our technology stock ticker
list. We can use sns.pairplot() to automatically create this plot
:::

::: {#4e87eb1a .cell .code execution_count="13" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:04.411519Z\",\"iopub.status.busy\":\"2023-01-31T12:54:04.410429Z\",\"iopub.status.idle\":\"2023-01-31T12:54:08.821289Z\",\"shell.execute_reply\":\"2023-01-31T12:54:08.820320Z\"}" papermill="{\"duration\":4.442333,\"end_time\":\"2023-01-31T12:54:08.823722\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:04.381389\",\"status\":\"completed\"}" tags="[]"}
``` python
# We can simply call pairplot on our DataFrame for an automatic visual analysis 
# of all the comparisons

sns.pairplot(tech_rets, kind='reg')
```

::: {.output .execute_result execution_count="13"}
    <seaborn.axisgrid.PairGrid at 0x7f63c3f952d0>
:::

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/851929f301ed11e0e090e136404cfc159f2dc8ab.png)
:::
:::

::: {#f7534aae .cell .markdown papermill="{\"duration\":2.998e-2,\"end_time\":\"2023-01-31T12:54:08.886979\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:08.856999\",\"status\":\"completed\"}" tags="[]"}
Above we can see all the relationships on daily returns between all the
stocks. A quick glance shows an interesting correlation between Google
and Amazon daily returns. It might be interesting to investigate that
individual comaprison.

While the simplicity of just calling `sns.pairplot()` is fantastic we
can also use `sns.PairGrid()` for full control of the figure, including
what kind of plots go in the diagonal, the upper triangle, and the lower
triangle. Below is an example of utilizing the full power of seaborn to
achieve this result.
:::

::: {#adcc1172 .cell .code execution_count="14" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:08.948902Z\",\"iopub.status.busy\":\"2023-01-31T12:54:08.947955Z\",\"iopub.status.idle\":\"2023-01-31T12:54:12.761348Z\",\"shell.execute_reply\":\"2023-01-31T12:54:12.760116Z\"}" papermill="{\"duration\":3.847924,\"end_time\":\"2023-01-31T12:54:12.764732\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:08.916808\",\"status\":\"completed\"}" tags="[]"}
``` python
# Set up our figure by naming it returns_fig, call PairPLot on the DataFrame
return_fig = sns.PairGrid(tech_rets.dropna())

# Using map_upper we can specify what the upper triangle will look like.
return_fig.map_upper(plt.scatter, color='purple')

# We can also define the lower triangle in the figure, inclufing the plot type (kde) 
# or the color map (BluePurple)
return_fig.map_lower(sns.kdeplot, cmap='cool_d')

# Finally we'll define the diagonal as a series of histogram plots of the daily return
return_fig.map_diag(plt.hist, bins=30)
```

::: {.output .execute_result execution_count="14"}
    <seaborn.axisgrid.PairGrid at 0x7f63dbee8c10>
:::

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/b61f20171c4ed238c190b51d1d12316293e67ceb.png)
:::
:::

::: {#b2c83da8 .cell .code execution_count="15" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:12.832758Z\",\"iopub.status.busy\":\"2023-01-31T12:54:12.832382Z\",\"iopub.status.idle\":\"2023-01-31T12:54:16.582659Z\",\"shell.execute_reply\":\"2023-01-31T12:54:16.581393Z\"}" papermill="{\"duration\":3.788237,\"end_time\":\"2023-01-31T12:54:16.586517\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:12.798280\",\"status\":\"completed\"}" tags="[]"}
``` python
# Set up our figure by naming it returns_fig, call PairPLot on the DataFrame
returns_fig = sns.PairGrid(closing_df)

# Using map_upper we can specify what the upper triangle will look like.
returns_fig.map_upper(plt.scatter,color='purple')

# We can also define the lower triangle in the figure, inclufing the plot type (kde) or the color map (BluePurple)
returns_fig.map_lower(sns.kdeplot,cmap='cool_d')

# Finally we'll define the diagonal as a series of histogram plots of the daily return
returns_fig.map_diag(plt.hist,bins=30)
```

::: {.output .execute_result execution_count="15"}
    <seaborn.axisgrid.PairGrid at 0x7f63bb2df7d0>
:::

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/49acfdb84be30b943bdb6e8c52d2c951dfd997b5.png)
:::
:::

::: {#e23683a3 .cell .markdown papermill="{\"duration\":3.4881e-2,\"end_time\":\"2023-01-31T12:54:16.658540\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:16.623659\",\"status\":\"completed\"}" tags="[]"}
Finally, we could also do a correlation plot, to get actual numerical
values for the correlation between the stocks\' daily return values. By
comparing the closing prices, we see an interesting relationship between
Microsoft and Apple.
:::

::: {#66e4b9db .cell .code execution_count="16" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:16.728554Z\",\"iopub.status.busy\":\"2023-01-31T12:54:16.728068Z\",\"iopub.status.idle\":\"2023-01-31T12:54:17.309151Z\",\"shell.execute_reply\":\"2023-01-31T12:54:17.307999Z\"}" papermill="{\"duration\":0.619447,\"end_time\":\"2023-01-31T12:54:17.311920\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:16.692473\",\"status\":\"completed\"}" tags="[]"}
``` python
plt.figure(figsize=(12, 10))

plt.subplot(2, 2, 1)
sns.heatmap(tech_rets.corr(), annot=True, cmap='summer')
plt.title('Correlation of stock return')

plt.subplot(2, 2, 2)
sns.heatmap(closing_df.corr(), annot=True, cmap='summer')
plt.title('Correlation of stock closing price')
```

::: {.output .execute_result execution_count="16"}
    Text(0.5, 1.0, 'Correlation of stock closing price')
:::

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/65373a4f0a2fe5493d1a577753c20aa4953c8615.png)
:::
:::

::: {#73d046e7 .cell .markdown papermill="{\"duration\":3.4175e-2,\"end_time\":\"2023-01-31T12:54:17.383241\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:17.349066\",\"status\":\"completed\"}" tags="[]"}
Just like we suspected in our `PairPlot` we see here numerically and
visually that Microsoft and Amazon had the strongest correlation of
daily stock return. It\'s also interesting to see that all the
technology comapnies are positively correlated.
:::

::: {#14ed0afd .cell .markdown papermill="{\"duration\":3.4013e-2,\"end_time\":\"2023-01-31T12:54:17.451481\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:17.417468\",\"status\":\"completed\"}" tags="[]"}
# 5. How much value do we put at risk by investing in a particular stock? {#5-how-much-value-do-we-put-at-risk-by-investing-in-a-particular-stock}
:::

::: {#d32423e8 .cell .markdown papermill="{\"duration\":3.4077e-2,\"end_time\":\"2023-01-31T12:54:17.519890\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:17.485813\",\"status\":\"completed\"}" tags="[]"}
There are many ways we can quantify risk, one of the most basic ways
using the information we\'ve gathered on daily percentage returns is by
comparing the expected return with the standard deviation of the daily
returns.
:::

::: {#e20911fb .cell .code execution_count="17" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:17.590989Z\",\"iopub.status.busy\":\"2023-01-31T12:54:17.590290Z\",\"iopub.status.idle\":\"2023-01-31T12:54:17.981489Z\",\"shell.execute_reply\":\"2023-01-31T12:54:17.980394Z\"}" papermill="{\"duration\":0.429954,\"end_time\":\"2023-01-31T12:54:17.984282\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:17.554328\",\"status\":\"completed\"}" tags="[]"}
``` python
rets = tech_rets.dropna()

area = np.pi * 20

plt.figure(figsize=(10, 8))
plt.scatter(rets.mean(), rets.std(), s=area)
plt.xlabel('Expected return')
plt.ylabel('Risk')

for label, x, y in zip(rets.columns, rets.mean(), rets.std()):
    plt.annotate(label, xy=(x, y), xytext=(50, 50), textcoords='offset points', ha='right', va='bottom', 
                 arrowprops=dict(arrowstyle='-', color='blue', connectionstyle='arc3,rad=-0.3'))
```

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/10ccc4faa97a777de17702cc2bb73f15747ae71d.png)
:::
:::

::: {#9a2f0753 .cell .markdown papermill="{\"duration\":3.4492e-2,\"end_time\":\"2023-01-31T12:54:18.054502\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:18.020010\",\"status\":\"completed\"}" tags="[]"}
# 6. Predicting the closing price stock price of APPLE inc: {#6-predicting-the-closing-price-stock-price-of-apple-inc}
:::

::: {#7589388f .cell .code execution_count="18" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:18.126741Z\",\"iopub.status.busy\":\"2023-01-31T12:54:18.126117Z\",\"iopub.status.idle\":\"2023-01-31T12:54:18.838390Z\",\"shell.execute_reply\":\"2023-01-31T12:54:18.837307Z\"}" papermill="{\"duration\":0.751269,\"end_time\":\"2023-01-31T12:54:18.840860\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:18.089591\",\"status\":\"completed\"}" tags="[]"}
``` python
# Get the stock quote
df = pdr.get_data_yahoo('AAPL', start='2012-01-01', end=datetime.now())
# Show teh data
df
```

::: {.output .stream .stdout}
    [*********************100%***********************]  1 of 1 completed
:::

::: {.output .execute_result execution_count="18"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-03 00:00:00-05:00</th>
      <td>14.621429</td>
      <td>14.732143</td>
      <td>14.607143</td>
      <td>14.686786</td>
      <td>12.519278</td>
      <td>302220800</td>
    </tr>
    <tr>
      <th>2012-01-04 00:00:00-05:00</th>
      <td>14.642857</td>
      <td>14.810000</td>
      <td>14.617143</td>
      <td>14.765714</td>
      <td>12.586559</td>
      <td>260022000</td>
    </tr>
    <tr>
      <th>2012-01-05 00:00:00-05:00</th>
      <td>14.819643</td>
      <td>14.948214</td>
      <td>14.738214</td>
      <td>14.929643</td>
      <td>12.726295</td>
      <td>271269600</td>
    </tr>
    <tr>
      <th>2012-01-06 00:00:00-05:00</th>
      <td>14.991786</td>
      <td>15.098214</td>
      <td>14.972143</td>
      <td>15.085714</td>
      <td>12.859331</td>
      <td>318292800</td>
    </tr>
    <tr>
      <th>2012-01-09 00:00:00-05:00</th>
      <td>15.196429</td>
      <td>15.276786</td>
      <td>15.048214</td>
      <td>15.061786</td>
      <td>12.838936</td>
      <td>394024400</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2023-01-24 00:00:00-05:00</th>
      <td>140.309998</td>
      <td>143.160004</td>
      <td>140.300003</td>
      <td>142.529999</td>
      <td>142.529999</td>
      <td>66435100</td>
    </tr>
    <tr>
      <th>2023-01-25 00:00:00-05:00</th>
      <td>140.889999</td>
      <td>142.429993</td>
      <td>138.809998</td>
      <td>141.860001</td>
      <td>141.860001</td>
      <td>65799300</td>
    </tr>
    <tr>
      <th>2023-01-26 00:00:00-05:00</th>
      <td>143.169998</td>
      <td>144.250000</td>
      <td>141.899994</td>
      <td>143.960007</td>
      <td>143.960007</td>
      <td>54105100</td>
    </tr>
    <tr>
      <th>2023-01-27 00:00:00-05:00</th>
      <td>143.160004</td>
      <td>147.229996</td>
      <td>143.080002</td>
      <td>145.929993</td>
      <td>145.929993</td>
      <td>70492800</td>
    </tr>
    <tr>
      <th>2023-01-30 00:00:00-05:00</th>
      <td>144.960007</td>
      <td>145.550003</td>
      <td>142.850006</td>
      <td>143.000000</td>
      <td>143.000000</td>
      <td>63947600</td>
    </tr>
  </tbody>
</table>
<p>2787 rows × 6 columns</p>
</div>
```
:::
:::

::: {#28a8a79f .cell .code execution_count="19" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:18.912834Z\",\"iopub.status.busy\":\"2023-01-31T12:54:18.912442Z\",\"iopub.status.idle\":\"2023-01-31T12:54:19.522134Z\",\"shell.execute_reply\":\"2023-01-31T12:54:19.521110Z\"}" papermill="{\"duration\":0.648574,\"end_time\":\"2023-01-31T12:54:19.524465\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:18.875891\",\"status\":\"completed\"}" tags="[]"}
``` python
plt.figure(figsize=(16,6))
plt.title('Close Price History')
plt.plot(df['Close'])
plt.xlabel('Date', fontsize=18)
plt.ylabel('Close Price USD ($)', fontsize=18)
plt.show()
```

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/9286439759d48f539304806010efa5f63e42b574.png)
:::
:::

::: {#67324004 .cell .code execution_count="20" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:19.601788Z\",\"iopub.status.busy\":\"2023-01-31T12:54:19.601381Z\",\"iopub.status.idle\":\"2023-01-31T12:54:19.610620Z\",\"shell.execute_reply\":\"2023-01-31T12:54:19.609494Z\"}" papermill="{\"duration\":4.938e-2,\"end_time\":\"2023-01-31T12:54:19.612866\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:19.563486\",\"status\":\"completed\"}" tags="[]"}
``` python
# Create a new dataframe with only the 'Close column 
data = df.filter(['Close'])
# Convert the dataframe to a numpy array
dataset = data.values
# Get the number of rows to train the model on
training_data_len = int(np.ceil( len(dataset) * .95 ))

training_data_len
```

::: {.output .execute_result execution_count="20"}
    2648
:::
:::

::: {#10f840de .cell .code execution_count="21" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:19.687315Z\",\"iopub.status.busy\":\"2023-01-31T12:54:19.686911Z\",\"iopub.status.idle\":\"2023-01-31T12:54:19.839242Z\",\"shell.execute_reply\":\"2023-01-31T12:54:19.838019Z\"}" papermill="{\"duration\":0.192669,\"end_time\":\"2023-01-31T12:54:19.841937\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:19.649268\",\"status\":\"completed\"}" tags="[]"}
``` python
# Scale the data
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler(feature_range=(0,1))
scaled_data = scaler.fit_transform(dataset)

scaled_data
```

::: {.output .execute_result execution_count="21"}
    array([[0.00439887],
           [0.00486851],
           [0.00584391],
           ...,
           [0.7735962 ],
           [0.78531794],
           [0.767884  ]])
:::
:::

::: {#56760ac2 .cell .code execution_count="22" _kg_hide-output="true" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:19.915974Z\",\"iopub.status.busy\":\"2023-01-31T12:54:19.915577Z\",\"iopub.status.idle\":\"2023-01-31T12:54:19.931894Z\",\"shell.execute_reply\":\"2023-01-31T12:54:19.930611Z\"}" papermill="{\"duration\":5.6026e-2,\"end_time\":\"2023-01-31T12:54:19.934116\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:19.878090\",\"status\":\"completed\"}" tags="[]"}
``` python
# Create the training data set 
# Create the scaled training data set
train_data = scaled_data[0:int(training_data_len), :]
# Split the data into x_train and y_train data sets
x_train = []
y_train = []

for i in range(60, len(train_data)):
    x_train.append(train_data[i-60:i, 0])
    y_train.append(train_data[i, 0])
    if i<= 61:
        print(x_train)
        print(y_train)
        print()
        
# Convert the x_train and y_train to numpy arrays 
x_train, y_train = np.array(x_train), np.array(y_train)

# Reshape the data
x_train = np.reshape(x_train, (x_train.shape[0], x_train.shape[1], 1))
# x_train.shape
```

::: {.output .stream .stdout}
    [array([0.00439887, 0.00486851, 0.00584391, 0.00677256, 0.00663019,
           0.00695107, 0.00680444, 0.00655793, 0.00622217, 0.00726133,
           0.00819848, 0.00790947, 0.0063263 , 0.00783722, 0.00634968,
           0.01192796, 0.01149658, 0.01205972, 0.01327737, 0.01401476,
           0.01395314, 0.01372576, 0.01469479, 0.01560643, 0.01663922,
           0.01830739, 0.02181161, 0.02186474, 0.02381555, 0.02527333,
           0.0227679 , 0.02373267, 0.02371354, 0.02641875, 0.02603411,
           0.026746  , 0.02802528, 0.02873719, 0.03078787, 0.03228178,
           0.03271317, 0.03286405, 0.03030973, 0.02969346, 0.02978484,
           0.03218616, 0.03286193, 0.03431335, 0.03773469, 0.04229932,
           0.04144504, 0.04144716, 0.04474738, 0.04578017, 0.04504489,
           0.04437338, 0.04367423, 0.04599691, 0.04759072, 0.04825798])]
    [0.04660893460974819]

    [array([0.00439887, 0.00486851, 0.00584391, 0.00677256, 0.00663019,
           0.00695107, 0.00680444, 0.00655793, 0.00622217, 0.00726133,
           0.00819848, 0.00790947, 0.0063263 , 0.00783722, 0.00634968,
           0.01192796, 0.01149658, 0.01205972, 0.01327737, 0.01401476,
           0.01395314, 0.01372576, 0.01469479, 0.01560643, 0.01663922,
           0.01830739, 0.02181161, 0.02186474, 0.02381555, 0.02527333,
           0.0227679 , 0.02373267, 0.02371354, 0.02641875, 0.02603411,
           0.026746  , 0.02802528, 0.02873719, 0.03078787, 0.03228178,
           0.03271317, 0.03286405, 0.03030973, 0.02969346, 0.02978484,
           0.03218616, 0.03286193, 0.03431335, 0.03773469, 0.04229932,
           0.04144504, 0.04144716, 0.04474738, 0.04578017, 0.04504489,
           0.04437338, 0.04367423, 0.04599691, 0.04759072, 0.04825798]), array([0.00486851, 0.00584391, 0.00677256, 0.00663019, 0.00695107,
           0.00680444, 0.00655793, 0.00622217, 0.00726133, 0.00819848,
           0.00790947, 0.0063263 , 0.00783722, 0.00634968, 0.01192796,
           0.01149658, 0.01205972, 0.01327737, 0.01401476, 0.01395314,
           0.01372576, 0.01469479, 0.01560643, 0.01663922, 0.01830739,
           0.02181161, 0.02186474, 0.02381555, 0.02527333, 0.0227679 ,
           0.02373267, 0.02371354, 0.02641875, 0.02603411, 0.026746  ,
           0.02802528, 0.02873719, 0.03078787, 0.03228178, 0.03271317,
           0.03286405, 0.03030973, 0.02969346, 0.02978484, 0.03218616,
           0.03286193, 0.03431335, 0.03773469, 0.04229932, 0.04144504,
           0.04144716, 0.04474738, 0.04578017, 0.04504489, 0.04437338,
           0.04367423, 0.04599691, 0.04759072, 0.04825798, 0.04660893])]
    [0.04660893460974819, 0.04441800167645807]
:::
:::

::: {#33e725d9 .cell .code execution_count="23" execution="{\"iopub.execute_input\":\"2023-01-31T12:54:20.010250Z\",\"iopub.status.busy\":\"2023-01-31T12:54:20.009134Z\",\"iopub.status.idle\":\"2023-01-31T12:56:51.152962Z\",\"shell.execute_reply\":\"2023-01-31T12:56:51.151802Z\"}" papermill="{\"duration\":151.306093,\"end_time\":\"2023-01-31T12:56:51.277008\",\"exception\":false,\"start_time\":\"2023-01-31T12:54:19.970915\",\"status\":\"completed\"}" tags="[]"}
``` python
from keras.models import Sequential
from keras.layers import Dense, LSTM

# Build the LSTM model
model = Sequential()
model.add(LSTM(128, return_sequences=True, input_shape= (x_train.shape[1], 1)))
model.add(LSTM(64, return_sequences=False))
model.add(Dense(25))
model.add(Dense(1))

# Compile the model
model.compile(optimizer='adam', loss='mean_squared_error')

# Train the model
model.fit(x_train, y_train, batch_size=1, epochs=1)
```

::: {.output .stream .stderr}
    2023-01-31 12:54:26.137995: I tensorflow/core/common_runtime/process_util.cc:146] Creating new thread pool with default inter op setting: 2. Tune using inter_op_parallelism_threads for best performance.
    2023-01-31 12:54:26.831521: I tensorflow/compiler/mlir/mlir_graph_optimization_pass.cc:185] None of the MLIR Optimization Passes are enabled (registered 2)
:::

::: {.output .stream .stdout}
    2588/2588 [==============================] - 98s 37ms/step - loss: 0.0013
:::

::: {.output .execute_result execution_count="23"}
    <keras.callbacks.History at 0x7f639802c810>
:::
:::

::: {#37b7a61a .cell .code execution_count="24" execution="{\"iopub.execute_input\":\"2023-01-31T12:56:51.530737Z\",\"iopub.status.busy\":\"2023-01-31T12:56:51.529935Z\",\"iopub.status.idle\":\"2023-01-31T12:56:52.609024Z\",\"shell.execute_reply\":\"2023-01-31T12:56:52.608119Z\"}" papermill="{\"duration\":1.213588,\"end_time\":\"2023-01-31T12:56:52.611180\",\"exception\":false,\"start_time\":\"2023-01-31T12:56:51.397592\",\"status\":\"completed\"}" tags="[]"}
``` python
# Create the testing data set
# Create a new array containing scaled values from index 1543 to 2002 
test_data = scaled_data[training_data_len - 60: , :]
# Create the data sets x_test and y_test
x_test = []
y_test = dataset[training_data_len:, :]
for i in range(60, len(test_data)):
    x_test.append(test_data[i-60:i, 0])
    
# Convert the data to a numpy array
x_test = np.array(x_test)

# Reshape the data
x_test = np.reshape(x_test, (x_test.shape[0], x_test.shape[1], 1 ))

# Get the models predicted price values 
predictions = model.predict(x_test)
predictions = scaler.inverse_transform(predictions)

# Get the root mean squared error (RMSE)
rmse = np.sqrt(np.mean(((predictions - y_test) ** 2)))
rmse
```

::: {.output .execute_result execution_count="24"}
    4.982936594544208
:::
:::

::: {#99b14ef6 .cell .code execution_count="25" execution="{\"iopub.execute_input\":\"2023-01-31T12:56:52.848658Z\",\"iopub.status.busy\":\"2023-01-31T12:56:52.847966Z\",\"iopub.status.idle\":\"2023-01-31T12:56:53.305792Z\",\"shell.execute_reply\":\"2023-01-31T12:56:53.304602Z\"}" papermill="{\"duration\":0.579655,\"end_time\":\"2023-01-31T12:56:53.307997\",\"exception\":false,\"start_time\":\"2023-01-31T12:56:52.728342\",\"status\":\"completed\"}" tags="[]"}
``` python
# Plot the data
train = data[:training_data_len]
valid = data[training_data_len:]
valid['Predictions'] = predictions
# Visualize the data
plt.figure(figsize=(16,6))
plt.title('Model')
plt.xlabel('Date', fontsize=18)
plt.ylabel('Close Price USD ($)', fontsize=18)
plt.plot(train['Close'])
plt.plot(valid[['Close', 'Predictions']])
plt.legend(['Train', 'Val', 'Predictions'], loc='lower right')
plt.show()
```

::: {.output .stream .stderr}
    /opt/conda/lib/python3.7/site-packages/ipykernel_launcher.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      after removing the cwd from sys.path.
:::

::: {.output .display_data}
![](vertopal_a579fb8fa69546c39551d8bfbeb13562/5ea7f9ff279fe698cdcbdbd01f10c1ac52efce25.png)
:::
:::

::: {#c6fc7f35 .cell .code execution_count="26" execution="{\"iopub.execute_input\":\"2023-01-31T12:56:53.550333Z\",\"iopub.status.busy\":\"2023-01-31T12:56:53.549282Z\",\"iopub.status.idle\":\"2023-01-31T12:56:53.563444Z\",\"shell.execute_reply\":\"2023-01-31T12:56:53.562334Z\"}" papermill="{\"duration\":0.136463,\"end_time\":\"2023-01-31T12:56:53.565870\",\"exception\":false,\"start_time\":\"2023-01-31T12:56:53.429407\",\"status\":\"completed\"}" tags="[]"}
``` python
# Show the valid and predicted prices
valid
```

::: {.output .execute_result execution_count="26"}
```{=html}
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
      <th>Predictions</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2022-07-13 00:00:00-04:00</th>
      <td>145.490005</td>
      <td>146.457565</td>
    </tr>
    <tr>
      <th>2022-07-14 00:00:00-04:00</th>
      <td>148.470001</td>
      <td>146.872879</td>
    </tr>
    <tr>
      <th>2022-07-15 00:00:00-04:00</th>
      <td>150.169998</td>
      <td>147.586197</td>
    </tr>
    <tr>
      <th>2022-07-18 00:00:00-04:00</th>
      <td>147.070007</td>
      <td>148.572937</td>
    </tr>
    <tr>
      <th>2022-07-19 00:00:00-04:00</th>
      <td>151.000000</td>
      <td>148.995255</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2023-01-24 00:00:00-05:00</th>
      <td>142.529999</td>
      <td>138.565536</td>
    </tr>
    <tr>
      <th>2023-01-25 00:00:00-05:00</th>
      <td>141.860001</td>
      <td>140.022110</td>
    </tr>
    <tr>
      <th>2023-01-26 00:00:00-05:00</th>
      <td>143.960007</td>
      <td>141.225128</td>
    </tr>
    <tr>
      <th>2023-01-27 00:00:00-05:00</th>
      <td>145.929993</td>
      <td>142.469315</td>
    </tr>
    <tr>
      <th>2023-01-30 00:00:00-05:00</th>
      <td>143.000000</td>
      <td>143.833130</td>
    </tr>
  </tbody>
</table>
<p>139 rows × 2 columns</p>
</div>
```
:::
:::

::: {#1b62ce94 .cell .markdown papermill="{\"duration\":0.118756,\"end_time\":\"2023-01-31T12:56:53.802735\",\"exception\":false,\"start_time\":\"2023-01-31T12:56:53.683979\",\"status\":\"completed\"}" tags="[]"}
# Summary

In this notebook, you discovered and explored stock data.

Specifically, you learned:

-   How to load stock market data from the YAHOO Finance website using
    yfinance.
-   How to explore and visualize time-series data using Pandas,
    Matplotlib, and Seaborn.
-   How to measure the correlation between stocks.
-   How to measure the risk of investing in a particular stock.

Do you have any questions? Ask your questions in the comments below and
I will do my best to answer.

References: <https://www.investopedia.com/terms/c/correlation.asp> [Jose
Portilla Udemy Course: Learning Python for Data Analysis and
Visualization](https://www.udemy.com/course/learning-python-for-data-analysis-and-visualization/)
:::

::: {#f9f128ac .cell .code papermill="{\"duration\":0.120256,\"end_time\":\"2023-01-31T12:56:54.043466\",\"exception\":false,\"start_time\":\"2023-01-31T12:56:53.923210\",\"status\":\"completed\"}" tags="[]"}
``` python
```
:::
