---
layout: single
title: "Truncating Gradients: Motivation, Gain and Loss"
tags: sgd generalization probability statistics
author-profile: true
comments: true
---

## Low Sensitivity Matters in Differentially Private Mechanism

In the seminal work [Deep Learning with Differential Privacy](https://arxiv.org/abs/1607.00133) by Abadi et al. 2014 DP-SGD method is based on clipping the stochastic gradient.

$$
\tilde{g} = g/\max\{1, \frac{\|g\|_2}{C}\}
$$

where $g$ is the sampled gradient, $C$ is the clipping threshold and $\tilde{g}$ is the clipped gradient in $\ell_2$ norm. This guarantees the Lipschitz condition of the loss function and hence can deal with the infinity sensitivity issue. Note that this is common in DP algorithms - assumptions that loss function is Lipschitz continuous or data has bounded $\ell_2$ or $\ell_\infty$ norm are usually imposed. Yet, the theoretical study of clipped gradients is largely overlooked.

## Stochastic Optimization via Robust Gradient Estimation

In SO, the target is to solve

$$
\min_{w \in \mathcal{W}} f(w) = \mathbb{E}_ {z \sim \mathbb{P}}[F(w; z)] = \int_{\mathcal{Z}} F(w; z) \mathrm{d} \mathbb{P}(z).
$$

where $\mathcal{W}$ is a convex set and we only have access to a sample $S = (z_1, \cdots, z_n)$ drawn from the unknown $\mathbb{P}$.

### Empirical Risk Minimization lacks robustness

A classical approach to do so is via empirical risk minimization (ERM).

To be continue...

### Robust Risk Minimization lacks computational transparency (intractable)

[Empirical risk minimization for heavy-tailed losses](https://arxiv.org/abs/1406.2462) by Brownlees et al. 2016 and [Loss Minimization and Parameter Estimation with Heavy Tails](https://www.jmlr.org/papers/v17/14-273.html) by Hsu and Sabato 2016, proposed two different types of M-estimators, Catoni's mean estimator and median-of-means estimator, respectively.

To be continue...

### Robust gradient descent lacks scalability
