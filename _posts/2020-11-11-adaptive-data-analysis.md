---
layout: single
title: "Adaptive data analysis and transfer theorem"
author-profile: true
comments: true
---

## Introduction

Many data analysis pipelines are adaptive: the choice of which analysis to run next depends on the outcome of previous analyses. For example, hyper-parameter optimization in large-scale machine learning problems. In this case, common practice involves repeatedly evaluating a series of models on the same dataset.

The study of adaptive data analysis was initiated by [Dwork et al.](https://arxiv.org/abs/1411.2664): rather than computing and reporting exact sample quantities, perturb these quantities with noise. This line of work established a powerful transfer theorem, that informally says that any analysis that is simultaneously differentially private and accurate in-sample will also be accurate out-of-sample.

### Problem setup

Let $\mathcal{X}$ be an abstract data domain, and let $\mathcal{P}$ be an arbitrary distribution over $\mathcal{X}$. $S$ be a dataset sampled i.i.d from $\mathcal{P}^n$.

A linear query is a function q that takes the empirical average form when acting on the dataset $S$. We will be interested in estimating the expectations of linear queries over $\mathcal{D} = \mathcal{P}^n$.

Given a family of queries $Q$, a statistical estimator is a (possibly stateful) randomized algorithm $M: \mathcal{X}^n \times Q \rightarrow \mathbb{R}$ parameterized by a dataset $S$ that interactively takes as input a stream of queries $q_i \in Q$ and provides answers $a_i \in \mathbb{R}$.

An analyst is an arbitrary randomized algorithm $\mathcal{A}: \mathbb{R} \rightarrow Q$ that generates a stream of queries and receives a stream of answers (which can inform the next queries it generates).

When an analyst interacts with a statistical estimator, they generate a transcript of their interaction $\pi \in \Pi$ where $\Pi = (Q \times \mathbb{R})$ is the space of all transcripts.

The interaction is summarized in Algorithm 1, and we write $Interact(M; \mathcal{A} ; S)$ or $I(S)$ to refer to it.

```
input M, A and S
for t = 1 to T do
    q_t = A(a_1, ... , a_t-1)
    a_t = M(S; q_t)
endfor
return \Pi = ((q_1, a_1), ... ,(q_T, a_T))
```

Given a transcript $\pi$ write $\mathcal{Q}_ \pi$ to denote the posterior distribution on datasets conditional on $\Pi = \pi$: $\mathcal{Q} _\pi = \mathcal{P} ^n |I(S) =  \pi$.

Note that $\mathcal{Q} _\pi$ will no longer generally be a product distribution.

We will be interested in evaluating uniform accuracy bounds, which control the worst-case error over all queries:

M satisfies $(\alpha, \beta)$-sample accuracy if for every data analyst $\mathcal{A}$ and every data distribution $\mathcal{P}$,

$$
\mathbb{P} _{S\sim \mathcal{P}^n, \Pi \sim I(M,\mathcal{A};S)} [\max_j |q_j(S) - a_j| \geq \alpha] \leq \beta
$$

M satisfies $(\alpha, \beta)$-distributional accuracy if for every data analyst $\mathcal{A}$ and every data distribution $\mathcal{P}$,

$$
\mathbb{P} _{S\sim \mathcal{P}^n, \Pi \sim I(M,\mathcal{A};S)} [\max_j |q_j(\mathcal{P}^n) - a_j| \geq \alpha] \leq \beta
$$

An interaction $Interact(M;  ; )$ satises $(\epsilon, \delta)$-differential privacy if for all data analysts $\mathcal{A}$, pairs of neighboring datasets $S, S' \in \mathcal{X}^n$, and for all events $E \subseteq \Pi$:

$$
\mathbb{P}[I(M,\mathcal{A};S) \in E] \leq e^\epsilon \mathbb{P}[I(M,\mathcal{A};S') \in E] + \delta
$$

An interaction $I(M,\mathcal{A};S)$ is called $(\epsilon, \delta)$-posterior sensitive if for every data distribution $\mathcal{P}^n$

$$
\mathbb{P} _{S\sim \mathcal{P}^n, \Pi \sim I(M,\mathcal{A};S)} [\max_j |q_j(\mathcal{P}^n) - q_j(\mathcal{Q} _\pi)| \geq \epsilon] \leq \delta
$$
