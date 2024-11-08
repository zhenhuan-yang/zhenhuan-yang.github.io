---
layout: single
title: "Truncating Gradients: Motivation, Gain and Loss"
tags: sgd generalization probability statistics
author-profile: true
comments: true
published: false
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

The goal here is to robustly estimate the true mean $\nabla f(w) = \mathbb{E}_{z \sim \mathbb{P}} [\nabla F(w;z)]$ from sample $S$. A function $g(w;S,\delta)$ is a gradient estimator if for functions $\alpha$ and $\beta$, with probability at least $1 - \delta$, at any fixed $w \in \mathcal{W}$, the estimator satisfies the following inequality

$$
\|g(w;S,\delta) - \nabla f(w)\|_2 \leq \alpha(n,\delta)\|w - w_*\|_2+\beta(n,\delta).
$$

In heavy-tailed model / weak moment assumption (There are other works study $\epsilon$-contamination model but it is out of the scope of this post), a popular way to construct $g(w;S,\delta)$ is by geometric median-of-means

$$
\hat{\mu} = \arg\min_{\mu} \sum_{i=1}^b \|\mu - \hat{\mu}_i\|_2
$$

where $\hat{\mu}_i$ is the sample mean in batch $B_i$. Let $\mathbb{P}$ be the probability distribution of $z$ and $\mathbb{P}_w$ be the distribution of the gradient $\nabla F(w;z)$ on $\mathbb{R}^d$ with mean $\mu_w$ and covariance $\Sigma_w$. Minsker, 2015 proved that with probability at least $1-\delta$,

$$
\|\hat{\mu} - \mu_w\|_2 \leq 11\sqrt{\frac{tr(\Sigma_w)\log(1.4/\delta)}{n}}.
$$

Note this result requires bounded second moment. By now we see that such truncation has strong theoretical guarantee (The convergence is proved in Prasad et al., 2018). Note that other M-estimators has been proposed with nice concentration and convergence properties, for example, Holland and Ikeda, 2018. Yet solving the geometric median is a not a simple task...
