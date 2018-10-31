# Analyzing Outlandish Headlines to Determine Whether They're Satirical or Not

Satirical news articles have served as an important counter to the generally negative headlines of real news since inception of *The Onion* in 1988. It allows us to have a chuckle at the dredges of daily life. However, with the advent of social media, and the 24-hour news cycle, we've become increasingly exposed to news, which on first glance appears to be satirical, however, it's actually real. Popular social news aggregation site Reddit even has a subreddit dedicated to this type of news, called *r/NotTheOnion*. Often times, on first glance, people will misinterpret this news as fake or satirical. Hilariously enough, the opposite will also happen, wherein a satirical Onion headline will be interpreted as an [actual event](https://www.reddit.com/r/AteTheOnion/). This presents an interesting problem for those who perhaps lack the critical thinking skills necessary to differentiate joke from reality. What news is satire, and what outlandish headline is actually real? 

To help tackle this issue, I've developed a machine learning model which takes satirical headlines from The Onion, along with outlandish headlines that may appear to be satirical, and determines whether or not the headline is either a joke or reality. 

*Beyond this point, I will term the headlines as Satirical and Sensational, or Onion and non-Onion.*

## Executive Summary of Findings (Model Overview)

**NOTE: Before running any models, note that each model fitting cell is comprised of 3 grid searches!. You may wish to separate these cells for your own mental stability.**

In conducting this research, I built three different models through grid searching of hyperparameters. Each of the three models were tested on three different datasets, which were constructed as follows:

- TFIDF Vectorized | ngram range of (1,1) | SVD
- TFIDF Vectorized | ngram range of (1,1)
- TFIDF Vectorized | ngram range of (1,2)

The models I grid searched on were:

- K-Nearest Neighbors (KNN)
- Logistic Regression
- Random Forest

I had initially thought that the ensemble model, the `Random Forest` would provide the best results in model testing. However, it turns out that the highest scoring & least overfit model was created via Logistic Regression. A more thurough explanation of my motivations for selecting each model to be run can be found in the `03_modeling` notebook.

Below, you'll find a summary of scores for each model tested on:

|Dataset | Model Used |Accuracy Score (Train/Test)|
|----|---|----|
|SVD| KNN | 0.74 / 0.64| 
| SVD| Logistic Regression| 0.87 / 0.80|
| SVD |Random Forest | 0.996 / 0.76 |
| Full Dataset TFIDF 1| KNN | 0.74 / 0.63|
| Full Dataset TFIDF 1 | Logistic Regression| 0.91 / 0.81
|Full Dataset TFIDF 1 | Random Forest| 0.90 / 0.78
| Full Dataset TFIDF 2| KNN |0.74 / 0.63|
|**Full Dataset TFIDF 2** | **Logistic Regression**| **0.94 / 0.82**|
|Full Dataset TFIDF 2| Random Forest| 0.90 / 0.79

The **Full Dataset TFIDF 2 - Logistic Regression** model is the one which I considered both *best scoring* and *least overfit*, therefore is the model which I've pushed to production.

## Organization

This project is divided into 4 separate folders, while a `requirements.txt` can be found in the root directory, names and descriptions of folders below:

- data: contains the datasets scrapped from the pushshift API in the form of .json files 
- images: contains images generated within my notebooks and utilized in the presentation file
- notebooks - contains the actual project documents
  - 01_gathering_data: Querying Pushshift API for Subreddit data, and then saving it for EDA and preprocessing
  - 02_preprocessing: Loading in subreddit post data, conducting some general Exploratory Data Analysis (EDA), and readying the data for fitting models.
  - 03_modeling: Creating, fitting, and scoring 3 types of classification models. The highest and best fit model will be moved unto predicting on new, real-world data
  - 04_model_test: Using the production logarithmic model to predict on unseen headlines.
- pickle - contains python variables used in my modeling

## Presentation

The presentation is designed to be referenced alongside the notebooks, and can be found at the following link: [HERE](https://docs.google.com/presentation/d/1nEYjhchUErCDQR8fqr9AunZtu1Rai8-R14BtKmHf9_Q/edit?usp=sharing)