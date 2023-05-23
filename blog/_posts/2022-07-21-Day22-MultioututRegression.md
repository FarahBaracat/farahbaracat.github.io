---
layout: post
title: Day 22 - Finalizing baseline model and MultiOutput regression 
tags: [ICL Project]
include_toc: true
---

## General Progress
- Implemented changes in code to add the columns for multiple joints
- Duplicated the notebook of linear regression
  - quickly changed it to predict wrist and I-MCP joints --> got a negative R2 on wrist joint which can indicate 
    that its not a linear relationship (maybe I need to use quadratic regression? will have to look into this)
  - Briefly looking into the meaning of a negative $R^2$. $R^2$ is zero if I have a constant model predicting the 
    expected value or mean disregarding the input features (i.e 
    predicting 
    always the same value, this corresponds to a horizontal line fit). A negative value for $R^2$ then means we have 
    a model that is worse than this horizontal fit model.

  
<figure>
<img src="/blog/figures/coefficeint_determination_r2.png" alt="drawing" width="2500"/>
<figcaption align = "center"><b>Regression coefficient of determination $R^2$ formula</b></figcaption>
</figure>



## Regression for multi-output
- Multioutput regression refers to predicting more than one dependent variable. In my case, this would refer to 
  predicting wrist joint angle and finger joint angle for instance.
  - I came to know that "typically the outputs are dependent upon the input and upon each other. This means that often the outputs are not independent of each other and may require a model that predicts both outputs together or each output contingent upon the other outputs."
    [from this blog](https://machinelearningmastery.com/multi-output-regression-models-with-python/).

- There are other regression models than the one I am mostly familiar with: linear regresion. For instance:
  - **KNeighborsRegressor**: The target is predicted by local interpolation of the targets associated of the nearest 
    neighbors in the training (from scikit-learn documentation). Also referred to as Neighbors-based regression, "The label assigned to a query point is computed based on the mean of the labels of its nearest neighbors."
  - **DecisionTreeRegressor**
  - **RandomForestRegressor**

- I can simply use the same linear regression model to perform a multi-output prediction. I just need to pass the 
  target variable which would be n-dimensional in this case.





