---
layout: single
title: "How to understand the $\\epsilon$ value in differntial Privacy"
tags: probability differential-privacy
author-profile: true
comments: true
published: true
---

After reading so many papers about the application of differential privacy on machine learning, a nature question is raised in my mind:

$$
\textit{"So my algorithm is $\epsilon$-DP, but what does it mean?"}
$$

 In fact the answer to this question is not that hard if you know some basic probability theory - Bayes' rule to be more specific. 

 We imagine ourselves as an attacker tries to figure out whether someone (the target) is in $S$. Let's be the strongeest attacker we can think of: we know all the database, except the target. Our prior guess satisfies

 $$\mathbb{P}[S = S_{\text{yes}}] = 1 - \mathbb{P}[S = S_{\text{no}}].$$

Now the $\epsilon$-DP algorithm $A$ returns an output $O$, we have to compare $\mathbb{P}[S = S_{\text{yes}}]$ with the posterior $\mathbb{P}[S = S_{\text{yes}}|A(S) = O]$. By the Bayes' rule, we know

$$
\mathbb{P}[S = S_{\text{yes}}|A(S) = O] = \frac{\mathbb{P}[S = S_{\text{yes}}] \cdot \mathbb{P}[A(S) = O|S = S_{\text{yes}}]}{\mathbb{P}[A(S) = O]}.
$$

By the definition of conditional probability, we know

$$
\frac{\mathbb{P}[S = S_{\text{yes}}|A(S) = O]}{\mathbb{P}[S = S_{\text{no}}|A(S) = O]} = \frac{\mathbb{P}[S = S_{\text{yes}}]}{\mathbb{P}[S = S_{\text{no}}]} \cdot \frac{\mathbb{P}[A(S_{\text{yes}}) = O]}{\mathbb{P}[A(S_{\text{no}}) = O]}.
$$

Now by the DP constraint, we know 

$$
e^{-\epsilon}\leq \frac{\mathbb{P}[A(S_{\text{yes}}) = O]}{\mathbb{P}[A(S_{\text{no}}) = O]} \leq e^\epsilon.
$$

Plugging it into the formula above, we know

$$
e^{-\epsilon} \cdot \frac{\mathbb{P}[S = S_{\text{yes}}]}{\mathbb{P}[S = S_{\text{no}}]} \leq \frac{\mathbb{P}[S = S_{\text{yes}}|A(S) = O]}{\mathbb{P}[S = S_{\text{no}}|A(S) = O]} \leq e^\epsilon \cdot \frac{\mathbb{P}[S = S_{\text{yes}}]}{\mathbb{P}[S = S_{\text{no}}]}.
$$

Or

$$
\frac{\mathbb{P}[S = S_{\text{yes}}]}{e^\epsilon + (1 - e^\epsilon)\cdot \mathbb{P}[S = S_{\text{yes}}]} \leq \mathbb{P}[S = S_{\text{yes}}|A(S) = O] \leq \frac{e^\epsilon \cdot \mathbb{P}[S = S_{\text{yes}}]}{1 + (e^\epsilon - 1) \cdot \mathbb{P}[S = S_{\text{no}}]}.
$$

For example, if the prior is $50\%$ and $\epsilon = 1.1$, then the posterior is between $25\%$ to $75\%$.

 Reading the book by [Dwork](https://www.cis.upenn.edu/~aaroth/Papers/privacybook.pdf) will give you a deeper understanding on what does differential privacy guarantee. We will omit it here.