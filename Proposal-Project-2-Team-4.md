# Project 2 Proposal
**Andrea Ovelar, Christian Stracke, Emmy Kuo & Weiqing Wang**

The objective of this project will be to use unsupervised learning techniques to cluster stocks in the S&P 500, build predictive models on each cluster of stocks and then optimize investment strategies. 


1. [Data](#Data)
1. [Phase 1 - Cluster the Stocks](#Phase-1)
1. [Phase 2 - Predict some Prices](#Phase-2)
1. [Phase 3 - Make some Money](#Phase-3)
1. [Reach Goals](#Reach-Goals)


## **Data**

We will be using stock data for the S&P 500 starting from as early as 1990 (subject to availability constraints).

>Sources

* Capital IQ 
* Bloomberg


## **Phase 1**

We will use fundamental and technical analysis methods to find clusters of stocks within the S&P 500. The underlying assumption is that the clusters that form will share some trait which will make analysis more efficient/effective. 

We will look at the results of using only fundamental analysis, only technical analysis and using both.

**Fundamental Analysis**

 Data, as far back as 1990, will be obtained from Capital IQ. We will look at the following list of indicators:

 - P/E Ratio
 - Book Value

 >## **>>PLEASE ADD MORE<<**

**Technical Analysis**

We will calculate technical indicators from stock prices dating as far back as 1990. We will then run unsupervised clustering algorithms on our calculated technical indicators. The goal is find stocks that have similar 
behavior.

We willuse the following indicators:

- Bollinger Boundaries (1-std, 2-std)
- Simple moving averages (maybe weekly, quarterly, monthly, yearly)
- Increasing/Decreasing price (1st derivative)
- Increasing/Decreasing returns (2nd derivative)

 >## **>>PLEASE ADD MORE<<**

## **Phase 2**

Based on the results of the clustering algorithms, we will test several stocks in each cluster to determine which method is best able to predict stock prices in the next month/quarter. 

We will look at the following techniques and perform backtests based on strategy:

- Linear Regression
- ARIMA 
- Gradient Boost Regression
- LSTM

 >## **>>PLEASE ADD MORE<<**

Looking at the results, we would like to identify which technical indicators are useful in trading.

## **Phase 3**

Recommend and backtest trading strategies based on clustering and predictive tests. 

 >## **>>PLEASE ADD MORE<<**

## Reach Goals

- exploring different cost functions (MAPE)

- building a pipeline for stock data to autogenerate insights

 >## **>>PLEASE ADD MORE<<**