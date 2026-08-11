---
{"dg-publish":true,"permalink":"/knowledge/math/probability/continuous-probability/distribution/bernoulli-distribution/","dg-note-properties":{}}
---

## Basic Definition

> [!definition] Bernoulli Random Variable
> Let $p \in [0, 1]$. A random variable $x$ is called a **Bernoulli random variable** with **parameter** $p$, written $X \sim \mathrm{Bernoulli}(p)$, if $X$ takes values in $\{0, 1\}$ and takes the value $1$ with probability $p$. It models a single trial with two outcomes — "success" $(X = 1)$ and "failure" $(X = 0)$ — such as one toss of a coin that lands heads with probability $p$.

### Probability Mass Function

> [!definition] PMF of Bernoulli Distribution
> $$P_X(x) = \begin{cases}p &\mathrm{for } x = 1 \\ 1 - p &\text{for } x = 0 \\ 0 &\text{otherwise}\end{cases}$$

## Property

### Mean

> [!property] Mean of Bernoulli Random Variable
> $$\mathbb{E}[X] = 1 \cdot p + 0 \cdot (1 - p) = p$$

### Variance

> [!property] Variance of Bernoulli Random Variable
> $$\mathrm{Var}[X] = \mathbb{E}[X^2] - \mathbb{E}[X]^2 = p(1 - p)$$
