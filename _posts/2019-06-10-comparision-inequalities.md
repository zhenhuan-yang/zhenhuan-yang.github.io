---
layout: single
title: "From Gaussian comparison inequalities"
tags: probability
author-profile: true
comments: true
published: false
---

I have heard and used concentration inequalities in my life, but I have not heard or used comparison inequalities. I recently came across some of them during my research on RSC/RSS conditions. They came in handy when you trying to reduce "complicated" random variables to "simple" ones.

[Non-convex finite-sum optimization via scsg methods](https://arxiv.org/abs/1706.09156) by Lei et al., 2017 proposed a lemma about the variance of the sample mean(without replacement).

Consider vectors $x_i$ satisfying $\sum_{i=1}^n x_i = 0$. Let $\mathcal{B}$ be a uniform random subset of $[n]$ with size $m$, we have
\[\mathbb{E}\Big\|\frac{1}{m}\sum_{i \in \mathcal{B}} x_i \Big\|_2^2 \leq \frac{\mathbb{I}[|\mathcal{B} < n|]}{mn} \sum_{i=1}^n \|x_i\|_2^2.\]
