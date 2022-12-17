# Financial-Analysis-of-Stock-Market

# Discription

I would like to implement a model  Financial Analysis of Stock Market based on Data Science. I try to implement a simple model based on the Kaggle Dataset. 

The objective of this model is   to identify stocks  who are likely to change daily .The model uses historical data on stocks and tries to find some similarity with existing stock trades  If some similarity is found those stocks  are classified as potential stocks.  The project used visualization using different python packages to analyze the dataset and also uses ML to predict the future situation.ML has a good ability to understand human activities and behave like them. On starting the project it introduces with the table content and imported packages. 

Stocks prediction model in stock market Recommendation on how to set up a  model for a finance company.


# PROJECT  MONITORING  SYSTEM

![project moniter](https://user-images.githubusercontent.com/103837009/208219367-ec1a3cba-bbac-4d6c-9cf9-de85f493c54b.jpg)

# DATABASE DESIGN:
Projects database design consist of excel sheets and csv files which are known as datasets in data science. There are 2 datasets used in making of this project.


![database](https://user-images.githubusercontent.com/103837009/208219405-fc466597-01d5-4d85-821e-a40ecbbe8227.png)


# Imported Files:
import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

%matplotlib inline

import seaborn as ns

import pandas_datareader

import datetime

import warnings

warnings.filterwarnings("ignore")

plt.style.use("seaborn-whitegrid")




start = datetime.datetime(2016,1,1)
end = datetime.datetime.today()


The next step will be downloading the data.I used 'yahoo' as source since 'google finacnce' would result in "NotImplementError: data_source="google" is not Implement
shop=pandas_datareader.DataReader("SHOP","yahoo",start,end)
jd=pandas_datareader.DataReader("JD","yahoo",start,end)
alibaba=pandas_datareader.DataReader("BABA","yahoo",start,end)
Dataset of Shopify finance stock market
#shopify
shop.head()

# Dataset of jd finance stock market and Alibaba stock market

![dataset](https://user-images.githubusercontent.com/103837009/208219568-331b1344-63aa-4711-a6d8-4b629d9a9abe.png)

# graph plot for opening stocks
shop["Open"].plot(label="shopify",figsize=(16,10),title="opening Prices")
jd["Open"].plot(label="JD.com")
alibaba["Open"].plot(label="alibaba")
plt.legend()

![plot](https://user-images.githubusercontent.com/103837009/208219631-fc25da00-213f-48bf-8681-6d7152cbb3bd.png)

New let's plot the volumne of each stock that was traded every day
shop["Volume"].plot(label="shopify",figsize=(16,10),title="volumne Traded")
jd["Volume"].plot(label="JD.com")
alibaba["Volume"].plot(label="Alibaba")
plt.legend()


![To calculate the total trade](https://user-images.githubusercontent.com/103837009/208219929-8bc510b7-5083-4410-baf1-d91c3e21739e.png)
# To calculate the total trade

shop["Total Trade"] = shop["Open"] * shop["Volume"]
jd["Total Trade"] = jd["Open"] * jd["Volume"]
alibaba["Total Trade"] = alibaba["Open"] * alibaba["Volume"]

![1](https://user-images.githubusercontent.com/103837009/208220472-d452b1c7-516b-4937-ad4d-89d99a3ed86b.png)

shop["Total Trade"].plot(figsize=(16,8),label="shopify")
jd["Total Trade"].plot(figsize=(16,8),label="jd.com")
alibaba["Total Trade"].plot(figsize=(16,8),label="alibaba")
plt.legend(loc="upper left")


![To calculate the average trade](https://user-images.githubusercontent.com/103837009/208219946-87902680-6ed0-48e4-8d44-5896be500c54.png)

# To calculate the average trade 
shop["avg"]=shop[["High","Low"]].mean(axis=1)
jd["avg"]=jd[["High","Low"]].mean(axis=1)
alibaba["avg"]=alibaba[["High","Low"]].mean(axis=1)



![2](https://user-images.githubusercontent.com/103837009/208220532-a45e38f6-9780-4628-b2b0-de1450045f8f.png)

shop["average"].plot(figsize=(16,8),label="shopify")
jd["averagee"].plot(figsize=(16,8),label="jd.com")
alibaba["average"].plot(figsize=(16,8),label="alibaba")
plt.legend(loc="upper left")

![3](https://user-images.githubusercontent.com/103837009/208220820-f31557de-de92-4061-958d-321c83ff92db.png)

# Importing file of Scatter Matrix
from pandas.plotting import scatter_matrix
ret_comp=pd.concat([shop["Open"],jd["Open"],alibaba["Open"]],axis=1)
ret_comp.columns=["ShopifyOpen","JDOpen","alibaba"]

Scatter Matrix for Open stock

![graph](https://user-images.githubusercontent.com/103837009/208219513-161ffe04-36ed-4834-8c49-70ee0005ce4e.png)
# Graph for major and minor stocks in the week

For JD company
%matplotlib notebook

jd_jan19= jd.loc["2020-01"].reset_index()
jd_jan19["Dat_ax"] = jd_jan19["Date"].apply(lambda data: date2num(data))

list_of_col = ["Dat_ax","Open","High","Low","Close"]
dayFormatter = DateFormatter("%d")
shop_value = [tuple(x) for x in jd_jan19[list_of_col].values]
mondays = WeekdayLocator(MONDAY)
alldays = DateLocator()
weekFormatter = DateFormatter("%b %d") #eg jan 12
dayFormatter = DateFormatter("%d")

fig,ax = plt.subplots()
fig.subplots_adjust(bottom=0.2)
ax.xaxis.set_major_locator(mondays)
ax.xaxis.set_minor_locator(alldays)
ax.xaxis.set_major_formatter(weekFormatter)
candlestick_ohlc(ax,shop_value,width=0.6,colorup="g",colordown='r')
plt.show()


![for shopify](https://user-images.githubusercontent.com/103837009/208219978-bd5f7d1d-4176-4f9a-81b5-0be360e00a63.png)

#  For Shopify
%matplotlib notebook

shop_jan19= shop.loc["2020-01"].reset_index()
shop_jan19["Dat_ax"] = shop_jan19["Date"].apply(lambda data: date2num(data))

list_of_col = ["Dat_ax","Open","High","Low","Close"]
dayFormatter = DateFormatter("%d")
shop_value = [tuple(x) for x in shop_jan19[list_of_col].values]
mondays = WeekdayLocator(MONDAY)
alldays = DateLocator()
weekFormatter = DateFormatter("%b %d") #eg jan 12
dayFormatter = DateFormatter("%d")

fig,ax = plt.subplots()
fig.subplots_adjust(bottom=0.2)
ax.xaxis.set_major_locator(mondays)
ax.xaxis.set_minor_locator(alldays)
ax.xaxis.set_major_formatter(weekFormatter)
candlestick_ohlc(ax,shop_value,width=0.6,colorup="g",colordown='r')
plt.show()

![4](https://user-images.githubusercontent.com/103837009/208220948-11b09536-fe77-4370-8925-828b42c23e2e.png)

# Histogram for Returning stock
shop["Return"] = shop["Close"].pct_change(1)
jd["Return"] = jd["Close"].pct_change(1)
alibaba["Return"] = alibaba["Close"].pct_change(1)
shop["Return"].hist(bins=31)


# Scatter plot using Box plot
from pandas.plotting import scatter_matrix
scatter_matrix(box_df)

![Scatter plot using Box plot](https://user-images.githubusercontent.com/103837009/208220072-8953eb51-1d4e-4e7c-9389-8e6fad92adf2.png)

box_df.plot(kind="scatter",x="shopify Return",y="Alibaba Return",figsize=(10,8),alpha=0.5)


# Scatter plot of Alibaba stock company for return stock
box_df.plot(kind="scatter",x="shopify Return",y="JD return",figsize=(10,8),alpha=0.5)

![Scatter plot of Alibaba stock company for return stock](https://user-images.githubusercontent.com/103837009/208220014-b5f21c36-4518-474e-870b-6f304e7ab26f.png)


Finally we got the result of Market Trend
