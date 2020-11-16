---
layout: single
title: "Momentum-Based Variance Reduction"
tags: sgd optimization
author-profile: true
comments: true
---

[Ashok Cutkosky and Francesco Orabona](https://arxiv.org/abs/1905.10018) developed a variance reduction algorithm can do not require $n$-related batch size. But depends on adaptive learning rate.

The stochastic gradient descent with momentum algorithm is typically implemented as

$$
d_t = (1-a)d_{t-1} + a\nabla f(x_t, \xi_t)\\
x_{t+1} = x_t - \eta d_t
$$
