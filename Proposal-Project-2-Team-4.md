# Project 2 Proposal
**Andrea Ovelar, Christian Stracke, Emmy Kuo & Weiqing Wang**

The objective of this project will be to use unsupervised learning techniques to cluster stocks in the S&P 500, build predictive models on each cluster of stocks and then optimize investment strategies. 


1. [Data](#Data)
1. [Phase 1 - Cluster the Stocks](#Phase-1)
1. [Phase 2 - Predict some Prices](#Phase-2)
1. [Phase 3 - Make some Money](#Phase-3)



## **Data**

We will be using stock data for the S&P 500 starting from as early as 1990 (subject to availability constraints).

>Sources

* Capital IQ 
* Bloomberg

## **Phase 1 ** 

We will use fundamental indicators to find clusters of stocks within the S&P 500. The underlying assumption is that the clusters that form will share some trait which will make analysis more efficient/effective. 

We will use a one day/many period snapshot to run K-means clustering from the `sklearn` library. Below are the indicators we will use:

 - P/E ratio
 - Price to book 
 - ROE
 - ROA
 - Debt to equity ratio (debt to capital)
 - Net Income Margin

Tests
- Beta

We will also look into how our clusters compare to common industry indices and build indicies based on 


## **Phase 2**

We will build LSTM models for each stock using the `tensorflow` library. We will first conduct hyperparameter tuning using the indices to find the optimal parameters to use on each model. 

## **Phase 3**

We will use gradient boosing approach as well as random forest with fundamental and technical data (feature set) in order to predict stocks outperformers and underperformers compared to the indices we had produced using clustering. That way we will build a tradable strategy and display the results using an equity curve. It is our hope to impress the investment committee. :)



