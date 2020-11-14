---
layout: single
title: "Adaptive data analysis and transfer theorem"
categories: blog
date: 2020-11-11T15:08:02-04:00
---

Many data analysis pipelines are adaptive: the choice of which analysis to run next depends on the outcome of previous analyses. For example, hyper-parameter optimization in large-scale machine learning problems. In this case, common practice involves repeatedly evaluating a series of models on the same dataset.

The study of adaptive data analysis was initiated by Dwork et al.: rather than computing and reporting exact sample quantities, perturb these quantities with noise. This line of work established a powerful transfer theorem, that informally says that any analysis that is simultaneously differentially private and accurate in-sample will also be accurate out-of-sample.

Let $\mathcal{X}$ be an abstract data domain, and let $\mathcal{P}$ be an arbitrary distribution over $\mathcal{X}$. $S$ be a dataset sampled i.i.d from $\mathcal{P}^n$. A linear query is a function q that takes the empirical average form when acting on the dataset $S$. We will be interested in estimating the expectations of linear queries over $\mathcal{D} = \mathcal{P}^n$. Given a family of queries $Q$, a statistical estimator is a (possibly stateful) randomized algorithm $M: \mathcal{X}^n \times Q \rightarrow \mathbb{R}$ parameterized by a dataset $S$ that interactively takes as input a stream of queries $q_i \in Q$ and provides answers $a_i \in \mathbb{R}$. An analyst is an arbitrary randomized algorithm $\mathcal{A}: \mathbb{R} \rightarrow Q$ that generates a stream of queries and receives a stream of answers (which can inform the next queries it generates). When an analyst interacts with a statistical estimator, they generate a transcript of their interaction $\pi \in \Pi$ where $\Pi = (Q \times \mathbb{R})$ is the space of all transcripts.
