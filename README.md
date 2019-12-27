# Project-2

Machine learning for stock selection 

[Presentation](https://docs.google.com/presentation/d/1rcN4wPGv6Vl9rp_mUo7UpZSgeDe4XKk_56kthZHw2Rs/edit#slide=id.g6cbedc9ced_0_209)

**Andrea Ovelar, Christian Stracke, Emmy Kuo & Weiqing Wang**

## Contents

1. [Our Motivation](#Motivation-&-Summary) 
1. [Our Approach](#Our-Approach)
1. [Data](#Data)
1. [Methods & Technology](#Methods-&-Technology)
1. [Model Evaluation](#Model-Evaluation)
1. [Discussion](#Discussion)

## Motivation & Summary

We are looking to use machine learning model to create a stock portfolio that would outperform the S&P500 benchmark. Our hypothesis is that by combining fundamental and technical indicators we could have a portfolio of stocks that outperforms consistently the S&P 500 and rebalances on a monthly basis. This strategy can be easily replicated on different countries. 

Additionally, we applied clustering techniques to the stocks currently in the S&P 500, and then ran our machine learning model on the clusters to further optimize returns. We also explored using recurrent neural networks to predict the trend of individual stocks and the S&P500.



## Our Approach

### General Stock Selector

Since the goal of the project was to find outperformers on a monthly basis, we selected a supervised learning approach where we would try to classify the constituents of the S&P500 as either outperformers underperformers. We looked at both fundamental indicators and calculated technical indicators for all the constituents dating back to 1995. Stocks that had an average aggregate performance in the top third were determined to be outperformers, and stocks in the bottom third were determined to be underperformers. 

For each month of predictions, we evaluated 12 months of prior data.  The technical indicators, by design, have many redundant/slow changing entries (maximums over a quarter, a year and five years). So despite having a large volume of features, we do not expect for there to be many prevailing rules governing the data. Due to the size and nature of the data, we decided on a random forest approach as it is easy to control overfitting. We decided to use a forest of 20 trees, each with maximum tree depth of 3. Using a Gradient Boosting approach, we tested out 6 different learning rates. By keeping the forest small, and the trees shallow, we can quickly run and refresh the model as well as prevent overfitting. 

### Incorporating Clusters

Since the premise of finding outperformers relies on the relative performance of other stocks, we decided to cluster the constituents of the S&P500 based on a snapshot of fundamental indicators and then to apply our stock selection model. We did not want to go based off of traditional sectors, but instead to find clusters based on each constituents fundamental data. Therefore, we used K-means clustering, an unsupervised learning model.

We selected the optimal number of clusters to run based on the elbow curve technique where we find the point at which the reduction in inertia plateaus. We also used silhouette analysis to determine how well differentiated each cluster would have been based on the number of clusters. 

### Predicting the Market

We also sought to add an additional layer of validation by individually predicting each stock's trajectory using LSTM's. We decided on a complex model to model individual stock behavior due to the underlying assumption that the forces that drive stock price are inherently complex. This should ideally reduce the bias in modelling this system. 

We trained the system using daily closing prices of the stock. Also, to maximize the usefulness of the model, we decided to increase the number of features from only stock price to also a variety of technical and fundamental indicators and to directly train the model on target data offset by 21 days, which is 1 month worth of trading days.

## Data

We obtained financial data on fundamental indicators for all the stocks currently in the S&P 500 using the Bloomberg Terminal and Capital IQ. We calculated technical indicators based on the daily closing prices of the S&P 500 and resampled the data on a monthly interval. 


![table](https://github.com/ekuo651/Project-2/blob/master/bbg_logo.PNG "bbg_logo")

![table](https://github.com/ekuo651/Project-2/blob/master/capiq_logo.PNG "capiq_logo")

## Methods & Technology

### Stock Selector by Gradient Boosting
We had 19 features among fundamental and technicals factors. Each of which we sample every month end in order to build our feature set. We use a rolling approach in order to train and test our hypothesis. We use a lookback period of 12 month as a training set in order to predict the next forward return. Given that we had prior knowledge on the amount of noise financial data has we decided to run our models simply by using a classification approach. That way our main goal is to find stocks on a recurent basis that can outperform the SP500. 

The way we are updating our models is that we are always discarding most stale month and incorporating most recent month on the training set. In orther words we are using the past 12 months of data to train and we test our models in on the new month. Please find below ilustrative schema ilustrating how we are rolling our models over time to capture most recent information incorporated to the markets. 


![table](https://github.com/ekuo651/Project-2/blob/master/rolling.PNG "ROLLING")

We normalize the feature set by scaling all the feature values from 0 to 1 in order to have all the features contributing the same way to the model and not bias our selection on the features.  We constructed our prediction label as binary classification selecting top 30% of the stocks over that month and similarly flagging bottom 30% of underperformers. That way we dont use the stocks that are not moving much in terms of returns and therefore we are training our model with samples that trully provide valuabla information. 

After running our predictions we build an equity curve showing top 20 holdings by the model. and contrast the performance with the SP500. 

#Discuss any problems that arose with preparing the data or training the model that you didn't anticipate.
#Discuss the overall training process and highlight anything of interest with the training process: Cloud resources used, training time #required, issues with training.

### LSTM Stock Price Predictor

To prepare data for the LSTM stock predictor, individual csv's for each ticker had to be made. Each fundamental feature had to be concatenated and then technical indicators calculated. The primary challenge was that the fundamental data was reported and updated quarterly, whereas prices are reported daily. We originally planned on using a forward fill to fill in the empty boxes, but the format the data came in did not easily support this. Had we had more time, each fundmental dataframe would have been joined on a list of dates, forward filled and then concatenated with price data. Additionally, the fundamental data was incomplete/inconsistent for some of the tickers. This required careful handling when dropping null values and rows. 

Since 505 CSV's were created, we created a separate file of CSV paths to make loading separate dataframes convenient. Functions were written to load in the data either by ticker or by index number. Currently, the fundamental data is corrupted, so only the technical indicators are loaded. 

After each dataframe was prepared, the data had to be formatted to feed into a LSTM model. A function was written to scale and split the data into a customizable number of lookback days and offset days. 

![](Presentation_Resources/LSTM_Diagram.png)


## Model Evaluation

To evaluate the model performance across various iterations we used Compounded annual growth rate metrics. That way we saw the effects on the PnL directly instead of looking at the accuracy or other ML measures. We selected the top 20 results from the general classification model and calculated returns based on equal weighting of the selected stocks. 

For clustering, we used silhouette analysis to evaluate the differentiation of the clusters. We prioritized maximizing differentiation among the large clusters as opposed to the best average score. 

For the LSTM model, we evaluated the model based on the mean average percentage error as well as the maximum deviation from the true value. 


## Discussion

Gradient boosting was sufficient for the predictive task. We found several models that outperformed the SP500 benchmark. The best one is display below. Profit and loss curve in logarithmic scale. 

![table](https://github.com/ekuo651/Project-2/blob/master/pnl.PNG "pnl")

Clustering on top of gradient boosting also produced better results for one of the clusters than just gradient boosting alone. 

We were only able to get prelimary results from the LSTM using Google stock. Due to limited time, the model only ran for 100 epochs, took 12 days of prior data to predict 21 days into the future. The results showed a MAPE of ~7%, which is not optimal. However, the fundamental data was corrupted and the parameter tuning was not performed. We expect that with a larger lookback window, increased batch size and some tuning, we can improve the results.  


## Postmortem

With clustering, we were not able to get clusters that were as "clean" as the model data we used in class. Also, the elbow curve did not exhibit a large drop like we had seen in previous datasets. To decide on the clustering parameters, we decided to use silhouette analysis for maximum differentiation among the large clusters. With additional time, we could look into trimming the features used for clustering based on the more important features found from gradient boosting. 

To improve the gradient boosting accuracy score, we could try other classifiers such as SGBoost and EasyBoost with the existing dataset. We could also explore using a larger number of trees with the current classifier. 

For the LSTM piece, writing a function to prepare the cleaned dataframes for the LSTM was quite challenging. We encountered scaling difficulties, datashape and datatype errors. The amount of time required to train the LSTM was also a major roadblock. With additional time, we would train the model on at least 2 months of back data and also increase the batch size to 2 or 3. This would increase the training time by 10X or 15X. To speed up computation time, we could also explore limiting the input features based on the important features highlighted by gradient boosting. 




