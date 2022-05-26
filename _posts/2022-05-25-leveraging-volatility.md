---
layout: single
title: "Leveraging Volatility in Trading"
tags: finance
author-profile: true
comments: true
published: true
---

## VIX Formula

According to [Wikipedia](https://en.wikipedia.org/wiki/VIX), The VIX is a 30-day expectation of volatility given by a weighted portfolio of out-of-the-money European options on the S&P 500:
$$
VIX = \sqrt{\frac{2\exp(r\tau)}{\tau} \Big(\int_0^F\frac{P(K)}{K^2}\mathrm{d}K + \int_F^\infty\frac{C(K)}{K^2}\mathrm{d}K\Big)}
$$
where \(\tau\) is the number of average days in a month (30 days), $r$ is  the risk-free rate, $F$ is the 30-day forward price on the S&P 500, and $P(K)$ and $C(K)$ are prices for puts and calls with strike $K$ and 30 days to maturity