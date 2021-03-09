# Time Series and Forecasting Quiz

This quiz is part of Algoritma Academy assessment process. Congratulations on completing the Time Series and Forecasting course! We will conduct an assessment quiz to test the practical forecasting model techniques that you have learned on the course. The quiz is expected to be taken in the classroom, please contact our team of instructors if you missed the chance to take it in class.

# Data Exploration

In this quiz, you will use the Chicago Crime dataset. The dataset contains real-time historical data of the various types of crime in the city of Chicago. This dataset was downloaded from [Chicago Data Portal](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2) and has been filtered for the primary type of crime "THEFT". The data is stored as a `.csv` file in this repository as `theft-ts.csv`.

Please load the data given `theft-ts.csv` and assign it to `theft` object, then investigate the data using `str()` or `glimpse()` function.

```
# your code here
```

The `theft` data consists of 6,492 observations and  2 variables. The description of each feature is explained below:

* `Date` : Date when the incident occurred (recorded daily).
* `Amount_Theft` : The total amount of theft on each date.

As a data scientist, you will develop a forecasting model that will aid security and other concerned parties in the decision-making process. Based on our data, we want to forecast the number of theft incidents (`Amount_Theft`). The purpose is to anticipate any crime activities on the given date and help security parties to allocate a proper amount of resources in the city of Chicago. 

Before we make a forecasting model, let us first inspect our data. Is our data a time series object? If not, please make a time series object using the `theft` data using `ts()` function with the frequency of this period is 365 and store it under `theft_ts`. 

___
1. Time series data has several characteristics. Based on your knowledge on time series, which of the following statement is **TRUE**?
 - [ ] Additive time series is additive because the amplitude of seasonal activity increases across the observed period.
 - [ ] Multiplicative time series is multiplicative because as the trend increases, the amplitude of seasonal activity also increases.
 - [ ] Time series data has no trend, seasonality, and error pattern.
___

To know the characteristics of our time series object we can visualize it using plot. For example, you can subset `theft_ts` to obtain the first 10 years of data using `head()` and visualize it with `autoplot()` from `forecast` package.

*Note: When you subset the ts object, you don't need to store the result into an object. You can directly visualize it.*

```
# your code here
```

# Decompose

After we make the time series object `theft_ts`, we can inspect its time series element. Try to look at the trend and seasonality pattern of the data to choose the appropriate model in forecasting `theft_ts` data. We can use `decompose()` to inspect the trend, seasonality, and error of our time series data and visualize them using `autoplot()`. Use the parameter `type = "multiplicative"` when decomposing the data to assume that the data is a multiplicative time series.

```
# your code here
```
___
2. Based on the decompose plot, how is the trend pattern of `theft_ts`?
 - [ ] there's no trend
 - [ ] the trend is increasing
 - [ ] the trend is decreasing
___

# Cross Validation

We have looked at the trend and seasonality of our `theft_ts` data. The next step is to build our time series model. However, we should split the dataset into training and test data before we make a model. In this section, please split the `theft_ts` data into `test_theft` which contains the last 365 days of our data using `tail()` function, and use the rest as `train_theft` using `head()` function.

```
# your code here
```

# Time Series Modeling

After splitting the `theft_ts` into `train_theft` and `test_theft` data, please inspect the trend and seasonality pattern of `train_theft` data.

```
# your code here
```

___
3.  Based on the decomposition plot, is it appropriate to use the Holt-Winters model? Why?
 - [ ] Yes, because the plot consists of trends and seasonality
 - [ ] No, it's more appropriate to use Holt's Exponential Smoothing
 - [ ] No, because we only focus on the trend, therefore, it is more appropriate to use Single Moving Average (SMA)
 - [ ] Yes, because the plot only consist of seasonality
___

After we analyze the decomposition result of `train_theft`, we are ready to build our model. Let's build our first model using Holt-Winters algorithm. You can use `HoltWinters()` function and store it under `model_hw` object.

```
# your code here
```

___
4. Using Holt-Winters as a model, which is the most appropriate code to model the `train_theft` data?
 - [ ] HoltWinters(train, gamma = F)
 - [ ] HoltWinters(train)
 - [ ] HoltWinters(train, beta = F)
 - [ ] HoltWinters(train, beta = F, gamma = F)
___

Let's explore another method to forecast our `train_theft` data using the ARIMA algorithm. Let's build an ARIMA model using `stlm()` function, set the method argument as `method = arima` and don't forget to set the `s.window` argument based on your time series frequency then store it as `model_arima` object.

```
# your code here
```

ARIMA is a statistical model to forecast time series object. It stands for AR(autoregressive) I (integrated) MA (moving average).

___
5. Based on the explanation above which of this following statement is **TRUE** about ARIMA(p,d,q)?
 - [ ] the time series object is being differenced q times to make it stationary
 - [ ] p is the number of orders you can use to determine the process of making an Autoregressive model
 - [ ] d shows the number of time in 1 frequency
 - [ ] p shows the amount of data for smoothing error using Moving Average
___

# Forecasting

On the previous section, we have built a forecasting model using Holt-Winters and ARIMA. Using `model_hw` and `model_arima`, try to forecast the theft frequency for the following 365 days using `forecast()` function. Store the result from `model_hw` in `hw_forecast` and `model_arima` in `arima_forecast`.

```
# your code here
```

# Model Evaluation (Error)

Now we have the forecast result of the Holt-Winters and ARIMA model. To evaluate our model, find the MAPE (mean absolute percentage error) value between our forecast result and our actual `test_theft` data. Please find each MAPE value from both model using `accuracy()` function from `forecast` package.

```
# your code here
```

## Model Evaluation Quiz

___
6. Based on the result, which of the following statement is **TRUE**?
 - [ ] using ARIMA model, the mean absolute percentage error is 11.6%
 - [ ] using Holt-Winters model, the mean absolute percentage error is around 11.6 theft event
 - [ ] The difference of mean absolute percentage error between ARIMA and Holt-Winters model is 0.53%
___

# Model Evaluation (Assumtion Checking)

There are several assumptions to check when performing time series analysis. These assumptions are used to make our model reliable to predict the real data.

___
7. What assumption should we check in the time series analysis?
 - [ ] Multicollinearity, No-Autocorrelation
 - [ ] No-Autocorrelation, Normality
 - [ ] Linearity, No-Autocorrelation
 - [ ] Heteroscedasticity, No-Autocorrelation
___

Please check the assumption of no-autocorrelation from your models using Ljung-Box Test.

```
# your code here
```

___
8. Which of this following statement is **TRUE** about the no-autocorrelation assumption of our time series model?
 - [ ] there is no autocorrelation in error, meaning that each error have no relation
 - [ ] there is autocorrelation in error, meaning that each error have a relation
 - [ ] there is autocorrelation in the prediction data, meaning that each predicted data a have relation
 - [ ] there is no autocorrelation in the prediction data, meaning that each predicted data have no relation
