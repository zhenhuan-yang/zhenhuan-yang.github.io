---
layout: single
title: "Leveraging Volatility in Trading"
tags: finance
author-profile: true
comments: true
published: false
---

VIX is a volatility index that measures the volatility of S&P500 Index returns expected in the next 30 days and priced (implied) in S&P500 options.

## VIX Formula

According to the [white paper](https://cdn.cboe.com/resources/vix/vixwhite.pdf), VIX is calculated as follow

$$\sigma^2 = \frac{2}{T} \sum_{i}\frac{\Delta K_i}{K_i^2} e^{RT}Q(K_i) - \frac{1}{T}\Big(\frac{F}{K_0}-1\Big)^2$$

where $\sigma = VIX/100$, $T$ is the time to expiration, $F$ is the forward index level derived from index option prices, $K_0$ is the first strike below the forward index level $F$, $K_i$ is the strike price of $i$th out-of-the-money option; a call if $K_i > K_0$ and a put if $K_i < K_0$; both put and call if $K_i=K_0$, $\Delta K_i$ is the interval between strike prices -  half the difference between the strike on either side of $K_i$: $\Delta K_i = \frac{K_{i+1} - K_{i-1}}{2}$, $R$ is the risk-free interest rate to expiration and $Q(K_i)$ is the midpoint of the bid-ask spread for each option with strike $K_i$.
