---
title: Predicting Number of Shares
date: 2023-04-12 13:00:00 -0400
categories: [School Projects, Statistics for Data Science]
tags: [Data Science, Python]
pin: true
math: false
mermaid: false
---

## Introduction

For my Statistics for Data Science course, I had the opportunity to do a project using the [Online News Popularity dataset](https://archive.ics.uci.edu/dataset/332/online+news+popularity). It includes 58 predictive attributes about posts on Mashable, where the target variable is the number of shares for a post.

The goal of this project was to train and tune a linear regression model, a regression tree model, and a LASSO Model. Then we compared each models accuracy using a test set and chose the best predicting model.

## Data

During my exploratory data analysis of the variables I found that the target `shares` value was very skewed. By applying a log-transformation I was able to get a more normalized target feature, which is ideal for regression based models.

I also identified that the feature `is_weekend` is redundant. Other binary variables for which day of the week the post was made already existed. Best case scenario, including `is_weekend` would not provide any additional information, but worst case scenario it could potentially introduce unwanted noise into the model, so I removed the feature. This also helps serve to simplify the model and improve it interpretability.

I also removed the non-predictive variables, `url` and `timedelta`.

## Models

### Linear Regression

I trained the Linear Regression Model in four phases.

In the first phase I wanted a measure of baseline performance for future comparison, so I trained the model using only first order terms. This resulted in poor in-sample and out-of-sample metrics.

In the second phase I tried to improve the accuracy by scaling the first order terms. This allowed the model to train faster, but actually performed worse overall.

Third, I included all second order terms in the model. This resulted in much better in-sample metrics than the first two phases, but still had poor out-of-sample metrics.

Finally, in the fourth phase I performed a step-wise reduction on the third model. This resulted in similar in-sample metrics, but performed much better on out-of-sample data, indicating that the models were likely overfitting, at least until now.

### Regression Tree Model

For the Regression Tree Model, I set the minimum leaf sample size to 100. This means that at each node in the decision tree there must be at least 100 data points represented, after which splitting stops. This is an important parameter, as setting higher minimum leaf sample sizes can help prevent overfitting.

After training a base-line model on all of the features, I applied cost-complexity pruning to reduce the size of the tree, and again prevent overfitting. This helped improve out-of-sample performance while keeping the model complexity low. I also observed that this model trained significantly faster than the linear regression model, making it a more practical choice for large datasets. However, it is again worth noting that Decision Tree models can suffer from overfitting and may not generalize well to unseen data.

### LASSO Model

Unlike traditional linear regression, the LASSO models add a penalty term to the objective function that the algorithm tries to minimize during training. This penalty term is a combination of the sum of the absolute values of the coefficients, and a tuning parameter ($\alpha$) that controls the strength of regularization. By increasing the value of $\alpha$, we increase the regularization strength, which results in more sparse models with fewer non-zero coefficients.

To find an optimal value of $\alpha$, I used cross-validation. This involved splitting the data repeatedly into training and validating sets and testing the models performance with different values of $\alpha$. Doing this helps get a more reliable estimate of the model's out-of-sample performance. Then I just selected the $\alpha$ value with the best cross-validation score to be the regularization parameter for the LASSO model.

Using that optimal parameter, I trained the LASSO model again and selected the features with non-zero coefficients in the resulting model. These selected features are likely the most important features in determining the number of shares a news article recieves.

The LASSO model did have slighlty worse out-of-sample metrics compared to the decision tree regressor and linear regression models, but this is still likely an improvement because it performs feature selection and regularization. The LASSO model is much less prone to overfitting, and as a result can generalize better on unseen data, because it only selects the important features and regularizes the coefficients.

## Summary

I found the decision tree regressor had the best predictive power among the models tested, despite recieving slightly worse out-of-sample metric values compared to the linear regression model. The decision tree regressor was a much lighter-weight model and would be able to adapt faster to future needs.

Using the decision tree I found that average shares for each keyword was an important feature, as well as its interactions with the number of other Mashable articles referenced.
