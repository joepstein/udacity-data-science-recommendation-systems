# Recommendation System with IBM Data

## Introduction

From the Udacity Data Science Nanodegree, this project covers the section on recommendation systems, and is required to graduate. The project is a python notebook that loads in user, and article data from IBM. This code leverages different models in order to give recommendations to users, each with their own advantages/disadvantages. All work can be seen in `Recommendations_with_IBM_Project_Submission.html`.

## File Structure

* |- `Recommendations_with_IBM_Project_Submission.html`
* |- `Recommendations_with_IBM_Project_Submission.ipynb`
* |- `data/`
* | |- `articles_community.csv`
* | |- `user-item-interactions.csv`

## Project Overview

The data is initially loaded from csvs into dataframes, which are cleaned, and joined, through the exploration step.	With cleaned data, I can concisely pull the values we want in creating a user-user matrix, or simply ranking articles by views. Lastly, I explore a technique in filling in missing values with FunkSVD, when a user has not yet read an article, or given a rating to it.

### Exploratory Data Analysis

The data exploration begins with looking at the number of users in the given dataset, and a distribution of the number of articles each has viewed. The number of unique users, and unique articles are also observed. The data is then cleaned, or prepared for joining, by mapping the values of the email column to their respective user ID, for one of the dataframes, then joining on the user id.

### Rank Based Recommendations

Rank based recommendations is by far the most straight forward approach. This approach resorts to a metric that signifies value, like number of views for an article, movie's average rating, etc... and then simply recommends the content in sorted order. A technique like this has its benefits, say there is a brand new user to your website, there is no data on which articles they like, so best bet is to recommend the most popular one.

### User-User Based Collaborative Filtering

In collaborative filtering, the idea is to create a user-user matrix, or a matrix where the rows are users, and the columns are articles, and stored at the location `user_user_matrix[<user>][<article>]` is a 1 if the user interacted with the article, or a 0 otherwise. Through such a matrix, recommendations are just around the corner, just get the most similar user, and recommend an article that the current user hasn't seen. Similarity can be calculated by just taking the dot product with every other user, and looking at the user with the highest value, who has also viewed articles that the other user has not.

In future implementations of this technique, I plan to use matrix factorization, followed by a measure of similarity that is appropriate for the technique.

### Matrix Factorization

Lastly, we follow a custom implementation of SVD, by decomposing the user-user matrix into U, S, and V (transpose) matrices, in which we reduce the S value a sensible number of representative latent features, and remultiply. Sensibly, we can see that upon reducing latent features, the accuracy follows. But, maybe this is the result of a sort of "overfitting". Splitting on training and test data, and remultiplying on latent features demonstrates that more latent features began to reduce the accuracy. The most robust model should work well on both the training, and test sets. 