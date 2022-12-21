# Comaprison-of-MSE-and-R2_score-for-different-models-on-UCI-Air-quality-dataset

## Abstract
The dataset contains 9358 instances of hourly averaged responses from an array of 5 metal oxide chemical sensors embedded in an Air Quality Chemical Multisensor Device. The device was located on the field in a significantly polluted area, at road level,within an Italian city.
Data was recorded from March 2004 to February 2005 (one year) representing the longest freely available recordings of on field deployed air quality chemical sensor devices responses.
Ground Truth hourly averaged concentrations for CO, Non Metanic Hydrocarbons, Benzene, Total Nitrogen Oxides (NOx) and Nitrogen Dioxide (NO2) and were provided by a co-located reference certified analyzer.
We have implemented multiple regression models and compared their accuracy before and after Principal Component Analysis.

## Introduction 
Urban atmospheric pollutants are considered responsible for the increased incidence of respiratory illness in citizens, and some of them (e.g. benzene) are known to induce cancers in case of prolonged exposure. Precise estimation of pollutants distribution is hence relevant for traffic management in the municipalities and more generally for the definition of integrated mobility plans designed to face these problems.


Nowadays, urban air pollution monitoring is primarily carried out by means of networks of spatially distributed fixed stations. These equipments, mostly based on industrial spectrometers, can selectively and precisely estimate the concentrations of many atmospheric pollutants, but their costs and sizes seriously hamper the deployment of adequately dense measurement networks. Unfortunately, pollutants diffusion is heavily affected by atmosphere dynamics and the availability of a limited number of measurement nodes may lead to the misevaluation of the real distribution of gases and particles concentrations in a complex and turbulent environment such as a city 

## Implementation 

The Dataset has date and time columns, so, we have extracted month and hour.
There is missing data which is represented by NaN and -200. First, we dropped NaN values and then replaced -200 by the mean of features using SimpleImputer. <br>
We have scaled the data using MinMaxScaler in the range (0,1) and plotted the correlation matrix.
Observing the correlation matrix we dropped RH, AH, T, Month, Hour and PT08.S3(NOx) which is NOx targeted tungsten oxdie as they have very low correlation. Having low correlated variables in the training set affects the R2_score of the model. We will also drop NMHC as a lot of the values are close to zero. 
We choose PT08.S5(O3) as our target variable. The data is split as 30% test set and rest as training set.

Principal component analysis, or PCA, is a dimensionality-reduction method that is often used to reduce the dimensionality of large data sets, by transforming a large set of variables into a smaller one that still contains most of the information in the large set. Reducing the number of variables of a data set naturally comes at the expense of accuracy, but the trick in dimensionality reduction is to trade a little accuracy for simplicity.

The explained variance ratio is the percentage of variance that is attributed by each of the selected components. Ideally, you would choose the number of components to include in your model by adding the explained variance ratio of each component until you reach a total of around 0.8 or 80% to avoid overfitting.

Principal Component Analysis using 2 principal components is done on X_train and total explained variance ratio is obtained as [0.76580657, 0.1961985 , 0.03799493].

LinearRegression, Lasso, Ridge, Logistic, SVD and OLS is done on original data and normalized data.

## Observations 

## Conclusion
From the observations of R2_score and MSE, we can see that R2_score for Linear Regression without normalization is 87.2 but the MSE is 141, but R2_score and MLE after normalization of data is 83.82 and 0.0689, which means the accuracy is reduced but the error is almost 0.
Lasso gave a negative R_2 score which means the chosen model fits worse than a horizontal line. R2 compares the fit of the chosen model with that of a horizontal straight line (the null hypothesis).
Logistic Regression failed to converge as the maximum likelihood estimates can be infinite and the algorithm fails to converge.
The best accuracy and MSE was achieved by Ordinary Least Squares using statsmodels.
