# 1 Data Exploration

In this quiz, you will be using the Chicago Crime dataset. The Crime dataset is originally a real-time historical data of various crime types in the city of Chicago. The dataset was downloaded from [Chicago Data Portal](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2) and has been filtered for the primary type of crime "THEFT". The data is stored as a csv file in this repository as `theft-ts.csv`.

Please load and investigate the data given `theft-ts.csv` and assign it to `theft` object, then investigate the data using `str()` or `glimpse()` function.

```
# your code here
```

The `theft` data consists of 6.492 observations and  2 variables. `theft` dataset is a real time historical crime type in the city of Chicago. The description of each features is explained below:

* `Date` : Date when the incident occurred.
* `Amount_Theft` : The frequent of total amount of theft each date.

As a data sciencetist you will develop a forecasting modeling that aid security or endurance parties in making decision. Aim of making this forecasting model is to anticipate if there is a crime happened and allocate security parties in many city of Chicago. Based on our data, we want to predict the number of theft incident based on `Amount_Theft` by `Date` column.

Before we make a forecasting model, let inspect our data first. Is our data is a time series object or not? If it's not please make a time series object using the `theft` data using `ts()` function with frequency of this period is 365 and store it under `theft_ts`. From `theft_ts` subset it which contain the first 10 years using `head()` and visualize it with `autoplot()` and answer the first question.

```
# your code here
```

## Data Exploration Quiz

1. Which is the statement below is true based on the time series plot above?
 - [ ] `theft_ts` is additive because the seasonality pattern is rather constant across the observed period
 - [ ] `theft_ts` is multiplicative because as the trend increase, the amplitude of seasonal activity is also increases
 - [ ] there is no seasonal pattern in `theft_ts`

# Decompose

After we make time series object for our `theft` data, we inspect our time series element of our `theft_ts` data. We want look the trend and seasonality pattern in order to choose the appropriate model for forecast `theft_ts` data. We can use `decompose()` to know the trend, seasonality, and error of our time series data and visualize them using `autoplot()`.

```
# your code here
```

## Decompose Quiz

2. Based on the decompose plot we have made above, how is the trend pattern of `theft_ts`?
 - [ ] there's no trend
 - [ ] the trend is increasing
 - [ ] the trend is decreasing

# Cross Validation

We have looked trend and seasonality of our `theft_ts` data. The next step is we will build our time series model. But before that, we should split the dataset into train and test data. In this section, please split the `theft_ts` data into `test_theft` which contains the last 365 days of our data using `tail()` function, and use the rest as `train_theft` using `head()` function.

```
# your code here
```

# Time Series Modeling

After splitting the `theft_ts` as `train` and `test` data, please inspect the trend and seasonality pattern of `train_theft` data.

## Modeling Quiz

3.  Based on the decompose plot above, is it appropriate to use the Holt-Winters model? If yes, why?
 - [ ] Yes, because the plot consists of trend and seasonality
 - [ ] No, it's more appropriate to use Holt's Exponential Smoothing
 - [ ] No, because we only focused on the trend, therefore, it is more appropriate to use Single Moving Average (SMA)
 - [ ] Yes, because the plot only consist of seasonality

After we analyze the decomposition result of `train_theft`, we are ready to build our model. Let's build our first model using Holt-Winters algorithm. You can use `HoltWinters()` function and store it under `model_hw` object.

```
# your code here
```

## Modeling Quiz

4. If your answer is yes using Holt-Winters as a model, which is the most appropriate code to model the `theft_ts` data?
 - [ ] HoltWinters(train, gamma = F)
 - [ ] HoltWinters(train)
 - [ ] HoltWinters(train, beta = F)
 - [ ] HoltWinters(train, beta = F, gamma = F)

Now let's explore another method to forecast our `train_theft` data using ARIMA algorithm. Let's build ARIMA model using `stlm()` function and set the method argument is `arima` then store it under `model_arima` object.

```
# your code here
```

## Modeling Quiz

ARIMA is a statistical model to forecast time series object. It stands for AR(autoregressive) I (integrated) MA (moving average).

5. Based on the explanation above which of this following statement is TRUE about ARIMA(p,d,q)?
 - [ ] the time series object is being differenced q times to make it stationary
 - [ ] p is the number of order you can use to determine the process of making an autoregressive model
 - [ ] d shows the number of time in 1 frequency
 - [ ] p shows how much data is needed for smoothing error using Moving Average

# Forecasting

In the section before, we have built a forecasting model using Holt-Winters and ARIMA. Using `model_hw` and `model_arima` model, try forecast the theft frequency for the following 365 days using `forecast()` function. Store the result of `model_hw` in `hw_forecast` and `model_arima` in `arima_forecast`.

# Model Evaluation (Erorr)

Now we have the forecast result of the Holt-Winters model and ARIMA model. To evaluate our model, find the MAPE (mean absolute percentage error) value between our forecast result and our `test_theft` data. Please find each MAPE value from both model using `MAPE()` function from `MLmetrics` package.

```
# your code here
```

## Model Evaluation Quiz

6. Based on the error result we have got, which of this following statement about model evaluation using error measure is TRUE?
 - [ ] using ARIMA model, the mean absolute of percentage error for each forecasting result is 11.6%
 - [ ] using Holt-Winters model, the mean absolute of percentage error for each forecasting result is around 11.6 theft event
 - [ ] the mean absolute of percentage error difference between ARIMA and Holt-Winters model by 1.1%

# Model evaluation (Assumtion Checking)

There are some assumptions we apply when we use time series analysis. These assumptions are used to make our model reliable enough to predict our real data.

## Assumption Checking Quiz

7. To make sure that our forecasting model is reliable enough, what assumption should be checked in time series analysis?
 - [ ] Multicollinearity, Autocorrelation
 - [ ] Autocorrelation, Normality
 - [ ] Linearity, Autocorrelation
 - [ ] Heteroscedasticity, Autocorrelation

8. Which of this following statement below is TRUE based on autocorrelation assumption in time series object?
 - [ ] there are no autocorrelation in error, means each error does not has relation
 - [ ] there are autocorrelation in error, means each error has relation
 - [ ] there are autocorrelation of each prediction data, means each predicted data has relation
 - [ ] there are no autocorrelation in each prediction data, means each predicted data has no relation
