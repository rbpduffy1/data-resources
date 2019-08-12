# Hackathon 3 suggested areas of analysis
Decoded have suggested the following datasets and areas of analysis related to the Finance Sector. Learners are, of course, free and encouraged to explore their own briefs and datasets.

## 1. Aggregate monthly Standard and Poor Composite stock prices from January 1871 to July 2019
This data is available from [this link.](../master/resources/SP_CPI_data.csv "S+P data")
Alternatively, it can be downloaded directly from [Kaggle.](https://www.kaggle.com/jonmissler/campbell-shiller-2001-data "S+P data")

Please note, to load the data into a Jupyter Notebook, learners should use the following:

_df = pd.read_csv('SP_CPI_data.csv', delimiter=';')_

**Suggestions for analysis:**
1. Build an appropriate time series model of the S&P index and/or Consumer Price Index.
2. Use that model to forecast their values.
3. Find a way to use forecasting for dataset slices in order to detect anomalies in recent history.
4. Find out if there is a dependence/covariance between S&P and CPI.

## 2. Explore potential relationships between bitcoin prices and Twitter activity

### Data 

##### <u>Daily Bitcoin Prices</u>
Historical _daily_ Bitcoin price data, dating back to 2013, can be accessed from [this link](../master/resources/BTC_USD_2013-10-01_2019-08-09-CoinDesk.csv "Bitcoin price data") or alternatively from [Coindesk.](https://www.coindesk.com/price/bitcoin "Bitcoin price data")

##### Hourly Bitcoing Prices
Conversely, historical _hourly_ Bitcoin prices, dating back to the the 1st of July 2019 can be accessed from [this link](../master/resources/hourly_btc_july_and_august.csv). The data was sourced from the API provided by [Crypto Compare](https://min-api.cryptocompare.com/).

##### Tweets that have 'BTC' or 'Bitcoin' in them
Twitter data on #bitcoin and #crypto can be accessed from [this link.](../master/resources/bitcoin-tweets.csv.zip "Bitcoin and Crypto tweets")


### Suggestions for Text analysis:

Build a tool that can analyse sentiment and determine activity levels on social media for the given topic. Explore potential relationships between Bitcoin prices and Twitter activity.

### Suggestions for Time-series analysis:
The Bitcoin data provided dates back to 2014. It therefore presents an interesting opportunity for doing time-series analysis. You could start by:

1. Exploring the Bitcoin prices time-series data for any trends.
2. Building an ARIMA-based forecasting model. (_Hint_: Bitcoin daily prices are very volatile! Aggregating price values over specified time periods would be a good starting point -- e..g per month or week -- to capture seasonality).
3. Evaluating your model(s). What can be done to improve results for similar future analysis?
