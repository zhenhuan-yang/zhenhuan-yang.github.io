---
layout: single
title: "Recommendation Engine 101"
author-profile: true
comments: true
published: false
tags: application
---



## Click-Through Rate Prediction

In a nutshell, given a query $q$ issued by a user, `CTR` prediction determines how likely a listing $l$ is going to be clicked by the user under the context of $q$.

### Pipeline

Data collection, model Training, prediction

For data collection, we need to collect historical promoted listings, logs etc. And then we need to perform feature engineering such as embedding. Labelling are given by whether this listing is clicked by this user. We will give detail to this part.

For training, it is straightforward! The model is chosen as logistic regression and training algorithm is chosen as `FTRL-Proximal` algorithm.

For prediction, well, it is just prediction.

### Feature Representations

There are two types of features: historical features and contextual features.

For historical features, there are historical click through rate.

For contextual features, there are text features and image features. Text features can be embedded by hashing trick, continuous bag-of-words or skip-gram model. Image features can be embedded by transfer learning methods.

### Evaluation

There are two major ways to evaluate: online A/B test and offline evaluation.

As for offline evaluation, there are a lot of choices such as Normalized Discounted Cumulative Gain (NDCG), Mean Average Precision (MAP) etc.

## Personalization Using Embedding for Search Rank

### Pipeline

A recommendation engine is a recommendation system and a search engine. It works in three steps:

User search, candidate set retrieval, Ranking

In this post, we will focus on the ranking part, which works in three steps:

Feature engineering, training, online prediction

In this post, we will focus on the feature engineering part.

### Retrieval

There are User Collaborative Filtering (UCF) and Item Collaborative Filtering (ICF). Let us focus on ICF. First of all, we need to do embedding, which we will introduce later. After embedding, we will have vector representation of items. We need to calculate the similarity, which can be done by Jaccard similarity or cosine similarity. We can also do clustering such as K nearest neighborhood to retrieve, but again we also need embedding at the first place.

Besides collaborative filtering, we can also conduct ranking. However, usually we are dealing with big data, hence ranking here need to be efficient. This means simple model such as logistic regression and gradient boosted decision tree; and low-dimensional features. Also the model need to be pre-trained.


### Ranking

In the training phrase, let us say there are $N$ users with $M$ goods, and $K$ features associated with each good. The features are created by embedding which we will explain later.

There are many ways to create the training labels. Such as user click it, favorite it, add it to cart, or purchase it, all these can be positive label and others goods for this user will be set as negative.

Gradient Boosted Decision Trees with pairwise formulation is the ranker. I think the algorithm can be RankBoost.

After training (online), the ranking is given by the score on each good from retrieval set.

### Embedding

There are listing embedding and user embedding.

For listing embedding, the underlying method is word2vec embedding by skip-gram model. This is a very famous work in NLP [Distributed Representations of Words and Phrases and their Compositionality](https://papers.nips.cc/paper/2013/hash/9aa42b31882ec039965f3c4923ce901b-Abstract.html). But here the sequence of words is replaced by session of clicking. and the vocabulary is replaced by unique listing ids. The model looks like This



 But since the vocabulary is too large, learning this objective by SGD is infeasible, hence another important aspect is to use negative sampling approach.

 ### Evaluation


 Online A/B test with NDCG metric.
