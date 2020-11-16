---
layout: single
title: "Momentum-Based Variance Reduction"
tags: sgd optimization
author-profile: true
comments: true
---

[Ashok Cutkosky and Francesco Orabona](https://arxiv.org/abs/1905.10018) developed a variance reduction algorithm can do not require $n$-related batch size. But depends on adaptive learning rate.

The proposed update

$$
d_t = (1-a)d_{t-1} + a\nabla f(x_t, \xi_t) + (1 - a)(\nabla f(x_t, \xi_t) - \nabla f(x_{t-1}, \xi_t)),\\
x_{t+1} = x_t - \eta d_t.
$$

If $x_t \approx x_{t-1}$, then

$$
d_t \approx (1-a)d_{t-1} + a\nabla f(x_t, \xi_t)
$$

which recovers classical momentum.

To understand why the above updates delivers a variance reduction, consider the "error in $d_t$"

$$
\epsilon_t = d_t - \nabla F(x_t).
$$

The equivalent term in SGD would be

$$
\mathbb{E}[\|\nabla f(x_t, \xi_t) - \nabla F(x_t)\|^2] \leq \sigma^2.
$$

So if $\mathbb{E}[\|\epsilon_t\|^2]$ decreases over time, we have realized a variance reduction effect.

We can obtain a recursive expression for $\epsilon_t$ by
subtracting $\nabla F(x_t)$ from both sides:

$$
\epsilon_t = (1-a)\epsilon_{t-1} + a(\nabla f(x_t,\xi_t) - \nabla F(x_t)) + (1-a)(\nabla f(x_t,\xi_t) - \nabla f(x_{t-1},\xi_t) - (\nabla F(x_t) - \nabla F(x_{t-1}))).
$$

We can control $a(\nabla f(x_t,\xi_t) - \nabla F(x_t))$ simply by choosing small enough values a.

And from smoothness we expect $\nabla f(x_t,\xi_t) - \nabla f(x_{t-1},\xi_t) - (\nabla F(x_t) - \nabla F(x_{t-1}))$ to be of the order of $\mathcal{O}(\|x_t - x_{t-1}\|) = \mathcal{O}(\eta d_{t-1})$.

Therefore, by choosing small enough $\eta$ and $a$, we obtain $\|\epsilon_t\| = (1-a)\|\epsilon_{t-1}\| + Z$ where $Z$ is some small value. Thus, intuitively $\|\epsilon_t\|$ will decrease until it reaches $Z/a$.
