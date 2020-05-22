---
title: "Lessons from the DengAI competition"
date: 2020-05-21
tags:
  - machine learning
  - statistics
  - competition
classes: wide
---

Thoughts on my team's approach to the competition.
{: .text-justify}

#### problem description

This competition is hosted on 
[Driven Data](https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/). 
We are given weekly climactic data such a precipitation and temperature spread for two cities, 
San Juan (Puerto Rico) and Iquitos (Peru), as well as the number of dengue fever cases. 
The goal is to predict the number cases for each city several weeks into the future.
Future climactic data is also given, a reasonably realistic setup since reliable short-term
climactic forecasts are readily available.
{: .text-justify}

<figure align="middle">
	<img src="assets/posts/denguai/historical_cases.png">
</figure>
**Figure 1**: historical outbreak data
{: .text-center}

First, the outbreaks clearly follow a seasonal pattern, though that it not the entire 
story as the size of the peak varies wildly year on year. The difficulty of the 
problem is thus to both capture the seasonal aspects and exponential growth in 
the major outbreak years.
{: .text-justify}

#### more informative features > expressive functional forms

This is , but having "growing up" on Kaggle you start to thing that any 
problem on structured data can be solved reasonably well by throwing stacked
XGBoost and hyperparamter optimization at it


#### avoid treating models as a black box

Before getting the idea of using time lagged features, I found some discussions suggesting that Facebook's Prophet forecasting 
model would give good results on this problem.
The model, assuming multiplicative seasonality and additonal regressors $$x(t)$$ is given by
{: .text-justify}

$$y(t) = g(t) \cdot s(t) \cdot \beta x(t) + h(t) + \varepsilon$$

Where $$g(t)$$ is the trend component and $$s(t)$$ the seasonal component. The holiday 
component $$h(t)$$ was set to 0 as there didn't seem to be any such effect in the historical data.
{: .text-justify}

