+++
title = "NVIDIA Stock Analysis"
description = ""
type = ["posts","post"]
tags = [
    "Equity Markets",
    "ARIMA model",
    "Data Analysis",
]
date = "2022-05-01"
categories = [
    "Data Analysis",
    "Equity Markets",
]
+++

[THIS IS AN ONGOING PROJECT](https://github.com/rachelsohzc/Nvidia-stock-analysis)

I’ve been interested in investing in the stock market lately. I started this projects to help me learn more about valuing companies and deciding what stocks to invest in. This is a short project where I analyse Nvidia stocks using past information, and the project answers some important questions like:

* What was the change in price of stock over time?
* What is the daily and monthly return of the stock?
* What is the stock’s moving average?
* How much risk do we take by investing in this stock?
* Can we predict stock behavior with statistical models?

The last question bears the most interest to me. I used an ARIMA model as I wanted to compare its performance between a statistical model and an AI model (in my other project).

### The ARIMA model

ARIMA models only work with stationary time-series data. So it’s important to check for that first. If the data isn’t stationary, multiple iterations of differencing might be needed:

```
{{ result = adfuller(nvidia_data.Close) }}
```

Once we’re sure that our data is suitable for the model, we can build the model using the following:

```
{{ for time_point in range(N_test_obs):
model = sm.tsa.arima.ARIMA(history, order = (4,1,0))
model_fit = model.fit()
out = model_fit.forecast()
y_pred = out[0]
model_preds.append(y_pred)
y_orig = test_data[time_point]
history.append(y_orig) }}
```

View the full project repository **[here](https://github.com/rachelsohzc/Nvidia-stock-analysis)**