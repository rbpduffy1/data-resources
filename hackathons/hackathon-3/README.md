# Sprint 3 Hackathon

It's time for the third hackathon! You've now had three sprints of learning new techniques and skills; now you've got a full day of independent data analysis to push yourself further and really hone your skills. You'll start the day with nothing but a dataset, and end it with a working data product.

You will be provided with several datasets from different sources that cover a range of topics. Some data might be specific to your cohort/company, while other data will be completely unfamiliar. You are also welcome to bring your own data that you would like to analyse if your organisation's data sharing rules permit that.

In the time provided, use your data skills to explore, examine, or model a dataset. You are free to choose the dataset, aspect, and method that most interest you; you can even combine multiple datasets if you wish.

## Guidelines

- It's a good idea to explore the data available early on; having a strong understanding of a dataset's structure and contents will be invaluable for modelling
- All the datasets will need some level of data cleaning before modelling can begin. Some will be much cleaner than others
- It's best to work in pairs/small groups
- A hackathon isn't about creating a finished, polished product; it's about learning, exploring, and collaborating together

## Resources

|Python | R |
|---|---|
| [Python docs](https://docs.python.org/3/)|[R docs](https://www.r-project.org/other-docs.html) |
| [Data cleaning with Pandas & Numpy](https://realpython.com/python-data-cleaning-numpy-pandas/) |[An Introduction to data cleaning with R](https://cran.r-project.org/doc/contrib/de_Jonge+van_der_Loo-Introduction_to_data_cleaning_with_R.pdf) |
| [Pandas docs](https://pandas.pydata.org/pandas-docs/stable/)| [Tidy Text Mining](https://www.tidytextmining.com/) |
|[The ultimate guide to text data analysis in Python](https://www.analyticsvidhya.com/blog/2018/02/the-different-methods-deal-text-data-predictive-python/)|[Time Series in R](https://www.statmethods.net/advstats/timeseries.html)|

## Datasets

We have carefully chosen datasets that allow you to practice the skills covered in Sprint 3. While the data used in the hackathons might not always be directly relevant to your day-to-day work, the skills, experience, and ideas you garner from working with them will have wider applications. You can find links to these datasets below:

## 1. Stock prices

Aggregate monthly Standard and Poor Composite stock prices from January 1871 to July 2019 can be downloaded from [Kaggle](https://www.kaggle.com/jonmissler/campbell-shiller-2001-data).

**Suggested analysis:**

  - Build an appropriate time series model of the S&P index and/or Consumer Price Index.
  - Find a way to use forecasting for dataset slices in order to detect anomalies in recent history.
  - Find out if there is a dependency/covariance between S&P and CPI.

## 2. Bitcoin prices

Historical data on Bitcoin prices (both hourly and daily) can be accessed from [this link](https://github.com/DecodedCo/data-resources/tree/master/hackathons/hackathon-3), or sourced directly by using the [Crypto Compare](https://min-api.cryptocompare.com/) API.

**Suggested analysis:**

  - Explore the Bitcoin prices time-series data for any trends.

  - Build an ARIMA-based forecasting model. (Hint: Bitcoin daily prices are very volatile! Aggregating price values over specified time periods would be a good starting point -- e..g per month or week -- to capture seasonality).

## 3. Bitcoin tweets

Tweets for the hashtags #bitcoin or #crypto can be accessed from [this link](https://github.com/DecodedCo/data-resources/tree/master/hackathons/hackathon-3).

**Suggested analysis:**

  - Explore potential relationships between Bitcoin prices and Twitter activity.
  
## 4. Datascience tweets

A dataset of roughly 200,000 tweets to [#datascience](https://github.com/DecodedCo/data-resources/raw/master/hackathons/hackathon-3/datascience_tweets.zip)

## 5. Tweets from the Financial Times API
**Suggested analysis:**
Apply text analysis techniques against a [dataset](https://github.com/DecodedCo/data-resources/tree/master/hackathons/hackathon-3) summarising 4,000 Financial Times articles with the term ‘banks’ present.

Please speak to your facilitators if you would like to pull similar FT article data based on a different term.

## 6. Your own idea

As always, you are free to explore your own areas of interest, further develop your projects, or explore any internal data you may have access to.
