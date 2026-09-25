---
layout: single
title: "Is RLCD Just a Regularised RLVR?"
tags: reinforcement-learning calibration
author-profile: true
comments: true
published: true
---

Reinforcement learning with verifiable rewards (RLVR) pays a model only for being right. On a single decision among $$K$$ options, that objective is linear in the policy, so its optimum puts all probability on one option. Accuracy can go up while the probabilities stop meaning anything. A policy that says $$0.99$$ on everything cannot tell software when to act and when to escalate.

TypeSafe's Jev answers typed questions with a distribution over options and claims that distribution is calibrated. It credits an unpublished method, Reinforcement Learning for Calibrated Decisions (RLCD). Anthony Maio built an open reconstruction, [`eve-rlcd`](https://github.com/anthony-maio/eve-rlcd), and [wrote it up](https://anthonymaio.substack.com/p/honest-about-uncertainty-i-tried). His RLCD differs from his RLVR control by one subtraction in the reward, and he showed that the subtracted reward follows a Brier-score gradient.

This post asks a narrower question: **is RLCD just RLVR with a regulariser, and if so, which one?** The answer is yes, and it is the only one. Among all regularisers of RLVR's objective, exactly one has the true posterior as its optimum, and it is the one RLCD's subtraction adds.

## Setup

A context $$x$$ arrives, the policy samples $$a \sim \pi_\theta(\cdot \mid x)$$ from $$K$$ options, and a verifier returns $$c_a = \mathbb{1}[a = y]$$ for a label $$y \sim p^\ast(\cdot \mid x)$$. Only the sampled option's outcome is revealed and there is no state transition, so this is a contextual bandit. Write $$\pi$$ for $$\pi_\theta(\cdot \mid x)$$, $$\Delta$$ for the probability simplex and $$e_y$$ for the one-hot label.

RLVR maximises

$$
J_0(\pi) = \mathbb{E}_{a \sim \pi}[c_a] = \pi \cdot p^\ast .
$$

This is linear in $$\pi$$, so its maximiser over $$\Delta$$ is a vertex: the one-hot policy on $$\arg\max_a p^\ast_a$$. We call $$\pi$$ *natively calibrated* at $$x$$ if $$\pi = p^\ast$$.

## The subtraction and the Brier identity

Maio's RLCD reward is

$$
r = c_a - \mathrm{sg}(\pi_a),
$$

where $$\mathrm{sg}$$ is stop-gradient. Both arms use REINFORCE with a leave-one-out baseline over $$G = 4$$ samples, which stays unbiased for any reward that receives no gradient. With the REINFORCE identity $$\pi_a \nabla \log \pi_a = \nabla \pi_a$$, the expected update for a fixed label is

$$
\mathbb{E}_{a \sim \pi}\big[(c_a - \pi_a)\nabla \log \pi_a\big]
= \sum_a (c_a - \pi_a)\nabla \pi_a
= -\tfrac12 \nabla \lVert \pi - e_y \rVert^2 .
$$

So REINFORCE on the subtracted reward follows half the gradient of the Brier score, using only the outcome of the sampled action. The Brier score is strictly proper, so its optimum is $$p^\ast$$. This identity is Maio's.

## Reading it as regularised RLVR

Expand the Brier score:

$$
-\tfrac12 \lVert \pi - e_y \rVert^2 = \underbrace{\pi_y}_{\text{RLVR}} + \underbrace{\tfrac12\big(1 - \lVert \pi \rVert^2\big)}_{W(\pi)} - \tfrac12 .
$$

Averaging over $$y$$, the expected RLCD update is the gradient of

$$
J_1(\pi) = \pi \cdot p^\ast + W(\pi) = -\tfrac12 \lVert \pi - p^\ast \rVert^2 + \text{const}.
$$

$$W$$ is the sparse Tsallis entropy of [Lee et al.](https://arxiv.org/abs/1709.06293), half the Tsallis entropy of index 2. RLVR regularised by $$\alpha W$$ has the known optimum $$\mathrm{sparsemax}(p^\ast/\alpha)$$, the Euclidean projection of $$p^\ast/\alpha$$ onto the simplex. RLCD is the case $$\alpha = 1$$, and since $$p^\ast$$ already lies in the simplex, its projection is $$p^\ast$$ itself.

The algebra is a one-line rewrite of Maio's identity, and the ingredients are known: the Brier score's generalised entropy is quadratic ([Gneiting and Raftery](https://doi.org/10.1198/016214506000001437)), and quadratic regularisation yields sparsemax ([Martins and Astudillo](https://arxiv.org/abs/1602.02068)). The reading still gives two facts that the gradient form hides:

- **The subtraction is a biased baseline.** $$\mathbb{E}_{a\sim\pi}[\pi_a \nabla\log\pi_a] = \tfrac12\nabla\lVert\pi\rVert^2 \neq 0$$. An action-dependent baseline is unbiased only with a correction term ([Tucker et al.](https://arxiv.org/abs/1802.10031)). RLCD omits it, and the bias it introduces is exactly $$\nabla W$$. The subtraction adds a regulariser rather than reducing variance.
- **The stop-gradient matters.** Maximising $$\mathbb{E}_{a\sim\pi}[c_a - \pi_a] = \pi\cdot p^\ast - \lVert\pi\rVert^2$$ directly is $$\alpha = 2$$. Its optimum, $$(p^\ast + \mathbf{1}/K)/2$$ in the interior, is underconfident.

## Only one regulariser works

Maio left open whether a KL term, an entropy bonus or a temperature could rescue RLVR. The regularised reading turns this into a clean question. Write $$\Delta^\circ$$ for the interior of the simplex.

**Theorem 1 (uniqueness of the regulariser).** Let $$R$$ be continuous on $$\Delta$$ and differentiable on $$\Delta^\circ$$. Then $$p^\ast$$ maximises $$\pi\cdot p^\ast + R(\pi)$$ over $$\Delta$$ for every $$p^\ast \in \Delta^\circ$$ if and only if $$R = W + \text{const}$$.

*Proof.* If $$R = W + \text{const}$$, the objective is $$-\tfrac12\lVert\pi - p^\ast\rVert^2$$ plus a constant, maximised uniquely at $$p^\ast$$. Conversely, let $$\Phi = R - W$$. At an interior maximiser $$p^\ast$$, the derivative along every tangent direction $$v$$ (with $$\mathbf{1}\cdot v = 0$$) vanishes: $$v\cdot p^\ast + D_v R(p^\ast) = 0$$. Since $$D_v W(\pi) = -v\cdot\pi$$, this says $$D_v\Phi(p^\ast) = 0$$. As $$p^\ast$$ ranges over the convex set $$\Delta^\circ$$, $$\Phi$$ has zero tangential derivative everywhere there, so it is constant, and continuity extends this to $$\Delta$$. $$\square$$

The hypotheses are weak. $$R$$ need not be concave, and calibration is required only at interior posteriors. The one real restriction is that $$R$$ must not depend on $$p^\ast$$, which is what makes it a regulariser. In scoring-rule language: a score of the form $$\pi_y + R(\pi)$$ is proper only if it is the Brier score, which also follows from [Savage's representation](https://doi.org/10.1080/01621459.1971.10482346) of proper scores.

Theorem 1 is about objectives. RLCD is specified as a reward, so the same question can be asked at that level.

**Theorem 2 (uniqueness of the reward correction).** Let the learner use $$r = c_a + v_a(\mathrm{sg}(\pi))$$ with the leave-one-out estimator, under a softmax policy with free logits. The expected update vanishes at $$\pi = p^\ast$$ for every $$p^\ast\in\Delta^\circ$$ if and only if $$v(\pi) = -\pi + \lambda(\pi)\mathbf{1}$$.

*Proof.* The expected update is $$\sum_a g_a \nabla\pi_a$$ with $$g = p^\ast + v(\pi)$$. With logits $$z$$, $$\nabla_z \pi_a = \pi_a(e_a - \pi)$$, so the update is $$\pi \odot (g - (\pi\cdot g)\mathbf{1})$$. At an interior point this is zero exactly when $$g$$ is constant across actions. Setting $$\pi = p^\ast$$ gives $$p^\ast + v(p^\ast) = \lambda(p^\ast)\mathbf{1}$$. $$\square$$

The $$\lambda(\pi)\mathbf{1}$$ term is an action-independent baseline and does not change the update. **Among corrections that add a policy-dependent term to the outcome, RLCD's subtraction is the only one that calibrates.**

### How the standard regularisers fail

For RLVR $$+\ \alpha W$$ with full-support $$p^\ast$$, the interior optimum is

$$
\pi^\ast_{\alpha,a} = \frac{p^\ast_a - (1-\alpha)/K}{\alpha}.
$$

For $$\alpha > 1$$ it shrinks towards uniform. For $$\alpha < 1$$ it zeroes out low-posterior options, and as $$\alpha \to 0$$ it becomes RLVR's one-hot policy. With $$K = 2$$ and $$p^\ast = (0.9, 0.1)$$:

| $$\alpha$$ | reported $$\pi_1$$ | |
|---|---|---|
| 0.5 | 1.0 (clipped) | overconfident |
| **1** | **0.9** | calibrated |
| 2 | 0.7 | underconfident |

**Shannon entropy and KL.** RLVR $$-\ \beta\,\mathrm{KL}(\pi \,\Vert\, \pi_{\mathrm{ref}})$$ has optimum $$\pi \propto \pi_{\mathrm{ref}} \exp(p^\ast/\beta)$$. An exponential cannot be the identity map. Concretely, with $$K = 2$$, calibration at $$(0.5, 0.5)$$ forces a uniform reference, calibration at $$(0.9, 0.1)$$ forces $$\beta = 0.8/\ln 9 \approx 0.364$$, and that $$\beta$$ sends $$(0.6, 0.4)$$ to $$0.634$$.

**KL to the previous iterate.** Proximal updates use $$\pi_{t+1} \propto \pi_t \exp(p^\ast/\beta)$$, so $$\pi_t \propto \pi_0 \exp(t\,p^\ast/\beta)$$, which still converges to one-hot. A trust region slows the collapse but does not change where it ends.

**The coefficient is not a hyperparameter.** If the verifier pays $$\kappa c_a$$, the unique calibrating regulariser is $$\kappa W$$. The value $$\alpha = 1$$ is fixed by the units of the reward.

**Reweighting is a different escape.** Theorem 2 covers additive corrections. Multiplying the outcome by $$1/\mathrm{sg}(\pi_a)$$ also calibrates, because it estimates the log-score gradient, but the weight is unbounded as $$\pi_y \to 0$$. The Brier score is the one proper score that REINFORCE can follow from outcomes without a policy-dependent weight.

**Temperature.** A training-time temperature just reparameterises the logits, and the temperature of a regularised optimum is the Shannon case above. Post-hoc temperature scaling fits one scalar on labelled data, which falls outside the outcome-only protocol and outside these results.

## What the equivalence means

**It equates expectations, not estimators.** The RLCD arm and REINFORCE on RLVR $$+\ W$$ have the same expected gradient, the same stationary points, and the same stationary points as supervised Brier training. Their variance and finite-step trajectories can differ.

**$$W$$ is the other half of the Brier score.** RLVR's expected reward is the outcome-dependent part of the Brier score, and $$W$$ is the part that depends on $$\pi$$ alone, half the Brier score's generalised entropy. RLVR is the Brier score with its entropy removed, and RLCD puts it back. Shannon entropy is the generalised entropy of the *log* score, whose outcome-dependent part is $$\log \pi_y$$, not $$\pi_y$$. RLVR plus Shannon entropy pairs half of one scoring rule with half of another, which is why no coefficient works.

**Nothing here is sparse, and nothing is exploration.** In sparse MDPs, $$W$$ comes with an exploration coefficient and sparsemax produces small-support policies. At $$\alpha = 1$$, $$\mathrm{sparsemax}(p^\ast) = p^\ast$$ keeps every option with positive posterior. Sparsity appears only for $$\alpha < 1$$, where it is overconfidence.

**The regulariser can be computed exactly.** Because $$\pi$$ is known on all $$K$$ options, one can run the plain RLVR estimator and add $$\nabla_\theta W(\pi_\theta)$$ analytically. The result is an unbiased estimate of the RLCD update. Whether its variance is lower is open, since in the RLCD estimator the noise of the two terms is correlated.

## What `eve-rlcd`'s experiments show

These numbers are from the repository's `docs/results.md` at commit `adb9a04`. I did not rerun them. The model is Qwen3-0.6B, and the test set has 8,000 rows at temperature 1 with 15-bin ECE.

| Arm | Accuracy | ECE | Brier | Mean confidence |
|---|---|---|---|---|
| Warmup (SFT) | 0.748 | 0.022 | 0.339 | 0.763 |
| RLCD ($$\alpha = 1$$) | **0.808** | **0.023** | **0.267** | 0.830 |
| RLVR ($$\alpha = 0$$), low learning rate | 0.778 | 0.213 | 0.432 | 0.991 |
| Oracle (NLL on labels) | 0.819 | 0.059 | 0.256 | 0.878 |

On tickets where the true posterior is $$0.5$$ on each of two departments, RLVR puts $$0.990$$ on one of them. RLCD moves the warmup's $$0.798$$ down to $$0.593$$. Both results are what the $$\alpha \to 0$$ and $$\alpha = 1$$ optima predict.

Two caveats matter:

- **RLCD maintains calibration but does not improve it.** The ECE change against the warmup is within noise on all three seeds.
- **The comparison confounds reward with learning rate.** RLCD ran at a learning rate five times higher than the three-seed RLVR arm.

## What this says about Jev

Nothing here identifies TypeSafe's method. It does constrain it. If Jev's native probabilities are calibrated and it is trained by RL from outcomes, its reward cannot be the outcome alone. Entropy or KL regularisation will not fix that. It needs either RLCD's subtraction or a policy-dependent reweighting of the outcome. If Jev's data is synthetic and therefore labelled, supervised training with a proper score is enough, and no RL is needed at all.

## Open questions

- **Matched control.** Replace the oracle's NLL with the exact Brier gradient, to separate the cost of outcome-only feedback from the choice of scoring rule.
- **GRPO.** Dividing by the group standard deviation biases the update direction ([Bereket and Leskovec](https://arxiv.org/abs/2508.11800) link it to overconfidence). How far does it move the fixed point?
- **Chains of thought.** When an action is a reasoning chain $$\tau$$ followed by an answer, $$\pi(\tau) \approx 0$$, so $$c - \mathrm{sg}(\pi(\tau)) \approx c$$ and the update degenerates to plain RLVR. The regulariser has to act on the answer marginal instead. Does a leave-one-out group frequency give an unbiased $$W$$-gradient for that marginal? That is the route to calibrated RLVR on reasoning benchmarks.
