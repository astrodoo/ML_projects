# Web Traffic Time Series Forecasting

![chicago](notebook/images/map_webtraffic.png)

<!--
## Data is obtained from Kaggle competition: 
[Web Traffic Time Series](https://www.kaggle.com/competitions/web-traffic-time-series-forecasting/) -->

## Problem Identification Overview

How can the internet servers, such as Google, Facebook, and Yahoo, improve their capability in

### Context

Web traffic can be defined as the number of visits to a website, including requests sent and received by web

## Recommendation

Given the time series data that contains 145k Wikipedia pages, we have built and evaluated three different

## Data Analysis
Data is obtained from [Kaggle competition for Web Traffic Time Series](https://www.kaggle.com/competitions/web-traffic-time-series-forecasting/)

- train.csv
	- 145k rows each of which represents a different Wikipedia page
	- 804 columns: article title + daily traffic on the particular Wikipedia page from 2015-07-01 to
	- The first column contains information about the page which includes the information of language, access, and agent.

In this time series dataset, there are two kinds of missing values. The first type is the case where the data
is actually missing, and the second type is the case where the page is not created at the specific time and
the page has the valid counts of visits only after the page is created. For the former case, we make use of
linear interpolation to the neighbor data, and for the latter case, we simply fill in the zero value. In Figure
1, the *52_Hz_I_Love_You_zh.wikipedia.org_all-access_spider* page is created in 2016 April, so we fill
zero value before it is created, which is shown as the red line.

<p align="center">
   <img src="output/figures/imputed_data.png" width=70%>
   <div align="center"> <i> Figure 1. Imputed Data for '52_Hz_I_Love_You_zh.wikipedia.org_all-access_spider' Wikipedia page. The blue line represents the normal data, and the red line represents the imputed data.</i> 
   </div>
</p>

### Number of Articles

The dataset consists of 145k Wiki pages with different languages. As seen in Figure 2, the number of

<p align="center" width=100%>
   <img src="output/figures/n_articles_language.png" width=70%>
   <!-- <figcaption> <i> Figure 2. Number of articles per language.</i> </figcaption> -->
   <div align="center"><i> Figure 2. Number of articles per language.</i></div>
</p>

In the left panel of Figure 3, we can infer the total number of agents for the wiki pages, which non-spider

<p align="center" width=100%>
   <img width=49% src="output/figures/n_articles_agent.png">
   <img width=49% src="output/figures/n_articles_access.png">
   <div align="center"> <i> Figure 3. The number of articles per agent (left panel) and per access (right panel).</i>
   </div>
</p>

### Daily Traffic

It is interesting to note that even though the number of articles for mobile-web access is slightly larger than

<p align="center" width=100%>
   <img src="output/figures/Daily_Traffic_access.png" width=70%>
   <div align="center"><i> Figure 4. Total daily traffic per access as a function of time</i></div>
</p>

<p align="center" width=100%>
   <img width=49% src="output/figures/Daily_Traffic_language.png">
   <img width=49% src="output/figures/Daily_Traffic_language_log.png">
   <div align="center"> <i> Figure 5. Total daily traffic per language in real scale (left panel) and in logarithmic scale (right panel).</i>
   </div>
</p>

As seen in Figure 2, the wiki pages in the dataset are written in 7 languages: Chinese, French, English,
large spike in August 2016. Otherwise, while the number of articles for the Spanish pages is the smallest,

### Average Visits

To get a deeper insight into the daily traffic, we explore the average visits of the wiki pages by several

<p align="center" width=100%>
   <img width=49% src="output/figures/mean_views_month.png">
   <img width=49% src="output/figures/mean_views_weekday.png"> </br>
   <img width=49% src="output/figures/mean_views_year.png">
   <img width=49% src="output/figures/mean_views_weekend.png">
   <div align="center"> <i> Figure 6. The averaged view of the total Wiki pages by month (upper left), weekdays (upper right), year (bottom left), and between weekday and weekend (bottom right).</i>
   </div>
</p>

## Feature Engineering

The original time series dataset is in a wide format, where the columns are the sequence of time and the




## Modeling

Using the cleaned & reduced dataset, we build up a model with 3 different methods:

### Seasonal AutoRegressive Integrated Moving Average (SARIMA)

AutoRegressive Integrated Moving Average (ARIMA) is one of the most widely used forecasting methods
seasonal component of the series is called SARIMA. We build our first model with SARIMA and check

<p align="center" width=100%>
   <img src="output/figures/decomposed.png" width=70%>
   <div align="center"><i> Figure 7. The decomposed components of the averaged daily traffic time series dataset.</i></div>
</p>

Figure 7 shows the decomposed components of the averaged daily traffic time series data, which include


<p align="center" width=100%>
   <img src="output/figures/acf_pacf.png" width=70%>
   <div align="center"><i>Figure 8. Autocorrelation and Partial Autocorrelation function plots from the average daily traffic time series data.</i></div>
</p>

Stationarity means that the time series does not have a trend, has a constant variance, a constant

<p align="center" width=100%>
   <img width=49% src="output/figures/sarima_log_diff_predict.png">
   <img width=49% src="output/figures/sarima_log_diff_zoom_predict.png"> </br>
   <img width=49% src="output/figures/sarima_predict.png">
   <img width=49% src="output/figures/sarima_zoom_predict.png">
   <div align="center"> <i>Figure 9. The prediction of the average daily view, or visits. The predicted value is green line, and the actual values are blue (train) and orange (test) lines. Upper panels show the time series data for which logarithmic transformation and differencing are applied. Down panels show the recovered time series back to actual values. Left panels show the entire time range and right panels show the zoomed time range where we can compare the predicted value with the actual one in detail.</i>
   </div>
</p>



### Prophet by Facebook

[Prophet](https://facebook.github.io/prophet/) is an open-source software for forecasting time series data, which was developed and maintained


<p align="center" width=100%>
   <img src="output/figures/prophet_plot.png" width=70%>
   <div align="center"><i>Figure 10. Prediction of the average daily view from Prophet model. The blue solid line represents
</p>


### Long Short-Term Memory (LSTM)

LSTM is an artificial neural network, which has feedback connections by a recurrent neural network (RNN)


<p align="center" width=100%>
   <img width=49% src="output/figures/lstm_predict.png">
   <img width=49% src="output/figures/lstm_zoom_predict.png">
   <div align="center"> <i>Figure 11. Prediction of the average daily view from LSTM model. The blue and orange line represent the actual data, which split into train and test, respectively. The green line represents the predicted value. The left panel shows the result in the entire time period, and the right panel shows the result in zoomed period, where we can check the predicted value in detail.</i>
   </div>
</p>


### Comparison of the predictions from the different models

In Figure 12, we can compare the predictions from the different models for the last 60 days in the time

<p align="center" width=100%>
   <img src="output/figures/all_zoom_predict.png" width=70%>
   <div align="center"><i>Figure 12. The predicted average daily view for 3 different models: orange, green, red lines
</p>

In order to quantify the model performance, we measure symmetric Mean Absolute Percentage Error

<p align="center" width=100%>
   <img src="output/figures/all_smape.png" width=70%>
   <div align="center"><i>Figure 13. sMAPE scores for 3 models.</i></div>
</p>

## Further Suggestion

In this analysis, we reduced the time series data for 145k wiki pages to the total daily average view.

## Conclusion

In this work, given the time series data that contains 145k Wikipedia pages, we build and evaluate three