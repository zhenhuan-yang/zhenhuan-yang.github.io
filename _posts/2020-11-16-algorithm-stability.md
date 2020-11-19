---
layout: single
title: "Algorithmic stability of SGD"
tags: sgd generalization statistics
author-profile: true
comments: true
---

## The original idea

Starting from [Hardt et al.](https://arxiv.org/abs/1509.01240), stability has become the main tool for analyzing the generalization error of SGD-type algorithms.

For $L$-Lipschitz continuous, convex and $\beta$-smooth loss function, two key observations

* The probability of picking different examples from $S$ and $S'$ is $\frac{1}{n}$. The expansiveness in this case is $2\eta_t L$.

* Otherwise, when $\eta_t \leq \frac{2}{\beta}$, the gradient step is non-expansive. i.e.

$$
\|w_{t+1} - w'_{t+1}\| \leq \|w_t - w'_t\|
$$

Hence

$$
\|w_T - w'_ T\| \leq \sum_{t=1}^T\frac{2\eta_t L}{n}
$$

For  $L$-Lipschitz continuous, $\alpha$-strongly convex and $\beta$-smooth loss function, the additional key observation is

* When same example is picked and $\eta_t \leq \frac{1}{\beta}$, the grdient step is $(1 - \eta_t\alpha)$-contractive. Hence

$$
\|w_{t+1} - w'_{t+1}\| \leq (1 - \eta_t\alpha)\|w_t - w'_t\| + \frac{2\eta_t L}{n}
$$

If constant step size is picked, then

$$
\|w_T - w'_ T\| \leq \frac{2\eta L}{n}\sum_{t=1}^T (1-\eta \alpha)^t  \leq \frac{2L}{\alpha n}.
$$

However, strong convexity is hard to be satisfied for machine learning loss functions, unless one consider regularized problem. Alternate conditions are available: Polyak-Łojasiewicz condition, quadratic growth, error bound and weak convexity etc.

For $L$-Lipschitz continuous and $\beta$-smooth loss functions, the additional key observations Alternate

* When same example is picked, the grdient step is $(1 + \eta_t\beta)$-expansive. Also by picking $\eta = \frac{c}{t}$

$$
\|w_{t+1} - w'_{t+1}\| \leq (1 - \frac{1}{n})(1 + \eta_t\beta)\|w_t - w'_t\| + \frac{1}{n}\|w_t - w'_t\| + \frac{2\eta_t L}{n}\\
\leq (1 + (1 - \frac{1}{n})\frac{c\beta}{t})\|w_t - w'_t\| + \frac{2cL}{tn}\\
\leq \exp((1 - \frac{1}{n})\frac{c\beta}{t})\|w_t - w'_t\| + \frac{2cL}{tn}
$$

* SGD typically makes several steps before it even
encounters different example for the first time. Hence, an straight-forward lemma is

$$
\mathbb{E}[|f(w_T;z) - f(w'_ T;z)|] \leq \frac{t_ 0}{n} \sup f(w;z) + L\mathbb{E} [\ |w_ T - w'_ T\||\|w_ {t_0} - w'_ {t_0}\| = 0]
$$

Hence, by recurrence relation

$$
\mathbb{E}[|f(w_T;z) - f(w'_ T;z)|] \leq \sum_{t=t_0+1}^T \{\prod_{k=t+1}^T\exp((1 - \frac{1}{n})\frac{c\beta}{k})\}\frac{2cL}{tn}\\
\leq \sum_{t=t_0+1}^T \exp((1 - \frac{1}{n})c\beta\log(\frac{T}{t}))\}\frac{2cL}{tn}\\
= \frac{2cL}{n}T^{c\beta(1-\frac{1}{n})} \sum_{t = t_0 + 1}^T t^{-c\beta(1-\frac{1}{n}) - 1}\\
\leq \frac{1}{c\beta(1-\frac{1}{n})}\frac{2cL}{n}(\frac{T}{t_0})^{c\beta(1-\frac{1}{n})}\\
\leq \frac{2L}{\beta(n-1)}(\frac{T}{t_0})^{c\beta}
$$

Hence by the lemma and trading off on $t_0 = (2cL^2)^{\frac{1}{c\beta+1}} T^{1- \frac{1}{c\beta+1}}$

$$
\mathbb{E}[|f(w_T;z) - f(w'_ T;z)|] \lessapprox \frac{T^{1- \frac{1}{c\beta+1}}}{n}.
$$

Question: does the same property holds for pairwise learning?

## Extension to PL condition and QG condition

Yet, in order to get meaningful stability bound, step size is chosen small. This means longer training is necessary when considering optimization error at the same time, for example [Bassily et al. 2020](https://arxiv.org/abs/2006.06914). This is the question asked by [Charles and Papailiopoulos, 2017](https://arxiv.org/abs/1710.08402).

## Extension to 
