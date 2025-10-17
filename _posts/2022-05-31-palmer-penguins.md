---
title: Palmer Penguin Classification
date: 2022-05-31 13:00:00 -0400
categories: [Personal Projects, Data Science]
tags: [Python, Machine Learning, Data Science]
pin: true
math: false
mermaid: true
image:
  path: /assets/lib/2022-05-31-palmer-penguins/lter_penguins.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Palmer Penguins; <a href="https://allisonhorst.github.io/palmerpenguins/" target=”_blank”>Artwork by @allison_horst</a>
---

## Introduction

The Palmer Penguin Data Set is data for the three different species of penguins found on the Palmer Island. It is meant to help practice data science skills and is an alternative to the Iris Dataset.

This was my first data science project that I completed. I learned how to import and clean the dataset and represent the data graphically in a Jupyter Notebook. I also experimented with several different classification models and compared their accuracies.

## Data Cleaning

To clean the data I removed unnecessary columns and removed rows with `NaN`. The species column in the raw data also included a lot of extra species information, so I reduced the column to be either "Adelie", "Gentoo", or "Chinstrap".

## Data Visualization

I made histograms to see the distribution of individual features and used scatter plots to see how different features interacted with each other. I also used violin plots to show the distribution of continuous variables with respect to catagorical variables. I also looked at how each feature correlated with each other, and visualized that correlation in a heat map.

## Classification

Before classifying, I created training and testing data sets. I also chose 4 specific features to use. I used these data sets on several different classification models:

* Support Vector Machine
* Logistic Regression
* Decision Tree
* K-Nearest Neighbors

For each model I calculated its test accuracy. Additionally, for K-Nearest Neighbors, I calculated the test accuracy for several values of K.

## Results

All the models got really high test accuracies, but I suspect they also overfit. The Decision Tree model, for example, got a test accuracy of `1.0`, so I wonder if it's possible to somehow reduce the model complexity more and still get a good accuracy.

## Summary

This was a really insightful project for me. At this point I don't know much about Machine Learning and Data Science, but this has definitely shown me how excited I am to learn more about this in my degree.

You can find my full repository on GitHub at [zobiejrz/palmer-penguin-classification](https://github.com/zobiejrz/palmer-penguin-classification/).
