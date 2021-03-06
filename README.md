# Ethereum price prediction with Social network and trends data

## Andrea Tognoli
### *May 2021*

Project exploring Data Collection, Visualisation and Prediction of crypto-stock price.


## Content

- [Project Outline](#project-outline)
- [The Data](#the-data)
- [Sentiment Analysis](#sentiment-analysis)
- [Machine Learning](#machine-learning)
- [Delivering Insight](#delivering-insight)
- [Next Steps](#next-steps)

## Project Outline

This project aim to explore techniques to predict prices of Ethereum using ML as well as twitter and Goolge trends data. Ethereum is the second bigger cryptocurrency in terms of market capitalisation as well as the pyoneer of the smart contract technology. As a fact, social media are influencing more and more 
people decision on a daily basis and probably our investment choices too. Does it work also viceversa? 

*QUESTION:* "Can information in the social network environment can be use as a feature to predict cryptocurrecies prices?"

In order to answer to our question we will:
- scrape Twitter using the Twint API
- Get and adapt Google data
- Use Binance API 
- ML models to make predictions

<img src="images/project_outline.jpg" width="970" height="660" />


## The Data

### Stock Historical price - timeseries
With a huge amount of data available, I explored a number of different sources that I could use to collect it. There are a number of crypto exchange statistics APIs, but many of the better ones require a paid licence key. I found the best sources for data were either Binance. Kraken or Geko. I opted for Binance which I consider easier to use and offer a function for csv download. The data I decided to scrape have a time window which goes from 17-8-2017 (ETH listed on binance for first time) to 11-5-2021.

### Tweets data
Since most of the famous twitter scraping API offer scraping only for limted amount of time or have huge liimits I opted for the less famous Twint API. Thanks to it I could scrape 113.000 tweets for from 17-8-2017 to 11-5-2021. The Tweets were cleaned using regex and some duplicates removed. 

Using Python I was able to automate the process of collecting and combining data from numerous days. I scraped a number of different tables into Pandas Dataframes and began to explore and clean the data. 

[Jupyter Notebooks can be found here.](https://github.com/Tognolia/Cryptocurrencies_price_predictor/blob/main/Notebooks/Twitter_scraping_and_sentiment_analysis_fixed.ipynb.zip)

### Google trends

Google trends data were scraped from the analysed period and  saved into a csv file. Unfortunately Google allow to scrape data only in a weekly format if the timeframe is greater than 90 days. A data linear interpolation technique of Pandas helped me to transform my weekly data into daily ones. 

[Jupyter Notebooks can be found here.](https://github.com/Tognolia/Cryptocurrencies_price_predictor/blob/main/Notebooks/Google_trends_interpolation.ipynb)

## Sentiment Analysis 

The goal of the analysis was to obtain a daily mean sentiment of the tweets scraped. In oreder to run the analysis we used the Vader library.

The first step of the process was to clean the data. Multile regex lines of code were used to remove re-tweets, websites, names, etc. from the tweets. Later also stop words and neutral parts of the tweets were removed. 

At the end of the process we got a list of compound polarity, one for each tweet. Eventually, the values of this list were grouped by dates and stored in a df in Pandas.

<img src="images/tweets_sentiment.png" width="1070" height="460" />

## Machine Learning
All the model will aim to predict the price with 25 days of advance. The method used are linear regression and tree classifier.

### First iteration
In the first iteration the model uses close time as feature to predict the target. The results:

<img src="images/it1.png" width="1070" height="460" />

[The Jupyter Notebook can be found here.](https://github.com/Tognolia/Cryptocurrencies_price_predictor/blob/main/Notebooks/Data_cleaning%20%2B%20ML.ipynb)

### Second iteration
In the second iteration the model uses close time and sentiment as feature to predict the target. The results are slightly worse than in the previous model.


<img src="images/it2.png" width="1070" height="460" />

[The Jupyter Notebook can be found here.](https://github.com/Tognolia/Cryptocurrencies_price_predictor/blob/main/Notebooks/Data_cleaning%20%2B%20ML.ipynb)

### Third iteration
In the third iteration the model uses daily close price and daily sentiment as features as well as Google trends to predict the target . The result has substantially improved as you can see from the chart. The R2 score increased by more than 30% from the previous model. 

<img src="images/it3.png" width="1070" height="460" />

[The Jupyter Notebook can be found here.](https://github.com/Tognolia/Cryptocurrencies_price_predictor/blob/main/Notebooks/Last%20Iteration.ipynb)


## Delivering Insights

- We have shown that the search volume index is highly correlated with cryptocurrency prices both when prices rise and when they fall
- Twitter Sentiment toward the analysed Cryptocurrency are mostly positive - Investors might have interest in making positive tweets regardless the price drops
- Price prediction with r2 of 95% can be obtained using the adopted model

## Next Steps
- Improve the sentiment analysis and the scraping hashtag/ volume
- Import the tweets volumes
- Make the model work for a greater number of stocks
- Neural network model to improve the accuray
- Create a authomatic updating for the scraping/ sentiment analysis/ modelling


