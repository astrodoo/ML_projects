# West Nile Virus Prediction Modeling

![chicago](datasets/images/chiskyline.png)

<!--
## Data is obtained from Kaggle competition: 
[West Nile Virus Competition](https://www.kaggle.com/competitions/predict-west-nile-virus/overview)

## Project Description:
-->

## Problem Identification Overview

How can the City of Chicago predict an outbreak of West Nile Virus, which is known to be spread through infected mosquitos, using weather conditions, and thus mitigate its spread next year effectively by controlling the number of mosquitos with spray?


### Context

West Nile virus (WNV) is widely spread to humans through infected mosquitos and its symptoms are

## Recommendation

Given the weather information, we build a model that predicts the presence of WNV accurately. We


## Data Analysis

### Data
Data is obtained from [Kaggle competition for West Nile Virus prediction](https://www.kaggle.com/competitions/predict-west-nile-virus/overview)

- Main Data
	- WNV test results and the number of trapped mosquitos that were measured in Chicago between
- Spray Data
	- Date and location for spray efforts to kill mosquitos
- Weather Data
	- Dataset from NOAA of the weather condition from 2007 to 2014

	
### Spread of mosquitos and WNV presence along with spraying information

In 2002, the first human cases of WNV were reported in Chicago. Due to its high infection rate and fatality,


<p align="center" width=100%>
   <img src="output/figures/Map_num_mos_positive_w_spray.png" width=70%>
   <div align="center"><i>Figure 1. The cumulative number of trapped mosquitos and the presence of WNV between 2007 and 2013. The pink shade indicates the location where spraying was conducted to control the mosquitos.</i></div>
</p>

Figure 1. shows WNV outbreaks and the cumulative number of trapped mosquitos between 2007 and

In order to reduce the number of mosquitos, the City of Chicago has applied a spray across the city. The

### Species of Mosquitos

There are 6 species in the trapped mosquitos: Culex Erraticus, Culex Pipens, Culex Restuans, Culex

<p align="center" width=100%>
   <img src="output/figures/num_mos_speices.png" width=49%>
   <img src="output/figures/WNV_positive_species.png" width=49%>
   <div align="center"><i>Figure 2. The number of trapped mosquitos (left panel) and the WNV-positive cases (right panel) depending on the species of mosquitos</i></div>
</p>

### WNV-Positive Cases by date

Figure 3. shows the total number of WNV-positive cases, which were grouped by year and month. We can

<p align="center" width=100%>
   <img src="output/figures/WNV_positive_month.png" width=70%>
   <div align="center"><i>Figure 3. The stacked bar chart for WNV-positive cases, which were grouped by year and month</i></div>
</p>

### A detailed description of the Weather Dataset

In this analysis, weather conditions are measured from two stations, which were located near the City of



<p align="center" width=100%>
   <img src="output/figures/Weather_Stations.png" width=70%>
   <div align="center"><i>Figure 4. Weather conditions, which is observed from Station 1 and Station 2 between 2007 and 2015</i></div>
</p>

Figure 5. shows the average temperature between 2007 and 2014. In general, the temperature lies within 65 ~ 70

<p align="center" width=100%>
   <img src="output/figures/Tavg_year.png" width=70%>
   <div align="center"><i>Figure 5. Box plot for the average temperature between 2007 and 2014</i></div>
</p>

### Average temperature vs. Mosquitos / WNV

It is expected that the number of mosquitos and WNV cases are affected by the weather condition. Before


<p align="center" width=100%>
   <img src="output/figures/WNV_positive_Tavg.png" width=70%>
   <div align="center"><i>Figure 6. Correlation between the average temperature and the number of mosquitos
</p>

The annual presence of WNV-positive cases is affected by the average temperature. The box plots in Figure

<p align="center" width=100%>
   <img src="output/figures/Tavg_year_WNV_station1.png" width=49%>
   <img src="output/figures/Tavg_year_WNV_station2.png" width=49%>
   <div align="center"><i>Figure 7. The average temperature along with WNV presence between 2007 and 2013</i></div>
</p>


## Data Engineering

In order to prepare the dataset for building a model, we scrutinize the data in depth and select the feature of



The features that are strongly correlated to other features can make it difficult in distinguishing between
high multi-collinearity. Using this process, we remove all features that are highly correlated against the

The correlation between features in the final dataset that is ready for modeling is depicted in Figure 8. As

<p align="center" width=100%>
   <img src="output/figures/Corr_map.jpg" width=100%>
   <div align="center"><i>Figure 8. Correlation map between features after removing features that are highly correlated to the other features.</i></div>
</p>

## Modeling

Using the cleaned & reduced dataset, we build up a model with 5 different methods: Logistic regression,


<p align="center" width=100%>
   <img src="output/figures/ROC_all.jpg" width=70%>
   <div align="center"><i>Figure 9. Comparison of receiver operating characteristic curve for the different models.</i></div>
</p>

<p align="center" width=100%>
   <img src="output/figures/ROC_AUC_all.jpg" width=70%>
   <div align="center"><i>Figure 10. The comparison of best Area Under Curve scores for the different models.</i></div>
</p>

Figure 11 shows the confusion matrix for the Random Forest model, which is the best one among the

<p align="center" width=100%>
   <img src="output/figures/confusion_RandomForest.jpg" width=70%>
   <div align="center"><i>Figure 11. Confusion matrix for Random Forest Model</i></div>
</p>

## Importance of Features

In order to understand what are the main features that affect the output of our model, we make use of the


<p align="center" width=100%>
   <img src="output/figures/SHAP_bar.jpg" width=49%>
   <img src="output/figures/SHAP_violin.jpg" width=49%>
   <div align="center"><i>Figure 11. Confusion matrix for Random Forest Model</i></div>
</p>


## Further Suggestion

In this analysis, we have a caveat that the effect of spray at some locations is already considered in the


## Conclusion

In this work, given the weather information, we build a model that predicts the presence of WNV in the

- impute the missing data by checking the characteristics of features,

With the cleaned dataset, we benchmark 5 different models: Linear Regression, Random Forest, Gaussian
