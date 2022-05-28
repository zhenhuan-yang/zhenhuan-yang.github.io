---
layout: single
title: "Option Pricing Basic"
tags: finance
author-profile: true
comments: true
published: false
---

The Black-Scholes model, aka the Black-Scholes-Merton (BSM) model, is a differential equation widely used to price options contracts.

## How to derive BSM

To derive the BSM PDE for a call-option on a non-dividend paying stoch with strike $K$ and maturity $T$, we assume that the stock price follows a geometirc Brownian motion so that

$$\mathrm{d} S_t = \mu S_t \mathrm{d} t + \sigma S_t \mathrm{d} W_t$$

where $W_t$ is a standard [Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion). We also assume that interest rates are constant so that 1 unit of currency invested in the cash account at time 0 will be worth $B_t = \exp(rt)$ at time $t$. We will denote by $C(S, t)$ the value of the call option at time $t$. By [Itô's lemma](https://en.wikipedia.org/wiki/It%C3%B4%27s_lemma) we know that

$$\mathrm{d} C(S, t) = \Big(\mu S_t\frac{\partial C}{\partial S} + \frac{\partial C}{\partial t} + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 C}{\partial S^2}\Big)\mathrm{d} t + \sigma S_t \frac{\partial C}{\partial S} \mathrm{d} W_t.$$

Let us now consider a self-financing trading strategy where at eatch time $t$ we hold $x_t$ units of the cash account and $y_t$ units of the stock. Then $P_t$, the time $t$ value of this strategy satisfies

$$P_t = x_t B_t + y_t S_t.$$

We will choose $x_t$ and $y_t$ in such a way that the strategy replicates the value of the option. The self-financing assumption implies that

$$\begin{align*}
\mathrm{d} P_t = & x_t \mathrm{d} B_t + y_t \mathrm{d} S_t \\
= & rx_t B_t \mathrm{d} t + y_t (\mu S_t \mathrm{d} t + \sigma S_t \mathrm{d} W_t) \\ 
= & (r x_t B_t + y_t \mu S_t) \mathrm{d} t + y_t \sigma S_t \mathrm{d} W_t. 
\end{align*}$$

Note that the above equation is consistent with our earlier definition of self-financing. In particular, any gains or losses on the portfolio are due entirely to gains or losses in the underlying securities, i.e. the cash-account and stock, and not due to changes in the holdings $x_t$ and $y_t$.

Returning to our derivation, we can equate terms in the value of the call option with the corresponding terms in the above equation to obtain

$$\begin{align*}
y_t = & \frac{\partial C}{\partial S}, \\ 
r x_t B_t = & \frac{\partial C}{\partial t} + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 C}{\partial S^2}.
\end{align*}$$

If we set $C_0 = P_0$, the initial value of our self-financing strategy, then it must be the case that $C_t = P_t$ for all $t$ since $C$ and $P$ have the same dynamics. This is true by construction after equate terms in the value of the call option with the corresponding terms in the self-financing trading strategy. Substituting we obtain

$$r S_t \frac{\partial C}{\partial S} + \frac{\partial C}{\partial t} + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 C}{\partial S^2} - rC = 0,$$

the Black-Scholes PDE.