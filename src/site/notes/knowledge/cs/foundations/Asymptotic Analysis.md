---
{"dg-publish":true,"permalink":"/knowledge/cs/foundations/asymptotic-analysis/","dg-note-properties":{}}
---

## Asymptotic Analysis

> [!definition] Worst-case Analysis
> In **worst-case analysis**, we consider the longest running time of all inputs of a particular length.

> [!definition] Average-case Analysis
> In **average-case analysis**, we consider the average of all the running times of inputs of a particular length.

> [!definition] Asymptotic Dominance
> Let $f(n)$ and $g(n)$ be functions from $\mathbb{N}$ to $\mathbb{R}_{\ge 0}$.
> We say that **$g$ asymptotically dominates $f$** if there exist constants
> $c > 0$ and $n_0$ such that
> $$f(n) \le c \, g(n) \quad \text{for all } n \ge n_0.$$

### Asymptotic Upper Bound

> [!definition] Big-O (Asymptotic Upper Bound)
> Let $f(n)$ and $g(n)$ be functions from $\mathbb{N}$ to $\mathbb{R}_{\ge 0}$.
> We say that
> $$f(n) = O(g(n))$$
> if there exist constants $c > 0$ and $n_0$ such that
> $$f(n) \le c \, g(n) \quad \text{for all } n \ge n_0.$$

> [!definition] Little-o (Strict Asymptotic Upper Bound)
> Let $f(n)$ and $g(n)$ be functions from $\mathbb{N}$ to $\mathbb{R}_{\ge 0}$.
> We say that
> $$f(n) = o(g(n))$$
> if for every constant $c > 0$ there exists $n_0$ such that
> $$f(n) < c \, g(n) \quad \text{for all } n \ge n_0.$$
>
> Equivalently,
> $$\lim_{n \to \infty} \frac{f(n)}{g(n)} = 0.$$

> [!theorem] Algebra of $o$-Symbols
> As $x \rightarrow a$, we have the following:
> 1. $o(g(x)) \pm o(g(x)) = o(g(x))$.
> 2. $o(cg(x)) = o(g(x))$ if $c \neq 0$.
> 3. $f(x) \cdot o(g(x)) = o(f(x)g(x))$.
> 4. $o(o(g(x))) = o(g(x)).$
> 5. $\frac{1}{1 + g(x)} = 1 - g(x) + o(g(x))$ if $g(x) \rightarrow 0$ as $x \rightarrow a$.


### Asymptotic Lower Bound

> [!definition] Big-$\Omega$ (Asymptotic Lower Bound)
> Let $f(n)$ and $g(n)$ be functions from $\mathbb{N}$ to $\mathbb{R}_{\ge 0}$.
> We say that
> $$f(n) = \Omega(g(n))$$
> if there exist constants $c > 0$ and $n_0$ such that
> $$f(n) \ge c \, g(n) \quad \text{for all } n \ge n_0.$$

> [!definition] Little-$\omega$ (Strict Asymptotic Lower Bound)
> Let $f(n)$ and $g(n)$ be functions from $\mathbb{N}$ to $\mathbb{R}_{\ge 0}$.
> We say that
> $$f(n) = \omega(g(n))$$
> if for every constant $c > 0$ there exists $n_0$ such that
> $$f(n) > c \, g(n) \quad \text{for all } n \ge n_0.$$
>
> Equivalently,
> $$\lim_{n \to \infty} \frac{f(n)}{g(n)} = \infty.$$

### Asymptotic Tight Bound

> [!definition] Big-$\Theta$ (Asymptotically Tight Bound)
> Let $f(n)$ and $g(n)$ be functions from $\mathbb{N}$ to $\mathbb{R}_{\ge 0}$.
> We say that
> $$f(n) = \Theta(g(n))$$
> if there exist positive constants $c_1, c_2$ and an integer $n_0$ such that
> $$c_1 g(n) \le f(n) \le c_2 g(n)
> \quad \text{for all } n \ge n_0.$$

## Analysis of Functions

### Negligible Function

> [!definition] Negligible Function
> A function $f: \mathbb Z_{\geq 1} \rightarrow \mathbb R$ is called **negligible** if for all $c \in \mathbb R_{> 0}$ there exists $n_0 \in \mathbb Z_{\geq 1}$ such that for all integers $n \geq n_0$, we have $|f(n)| < 1/n^c$.

> [!theorem]
> A function $f: \mathbb Z_{\geq} \rightarrow \mathbb R$ is negligible if and only if for all $c > 0$, we have $$\lim_{n \rightarrow \infty} f(n) n^c = 0.$$

### Super-poly Function

> [!definition] Super-poly Function
> A function $f: \mathbb Z_{\geq 1} \rightarrow \mathbb R$ is called **super-poly** if $1/f$ is negligible.

### Poly-bounded Function

> [!definition] Poly-bounded Function
> A function $f: \mathbb Z_{\geq 1} \rightarrow \mathbb R$ is called **poly-bounded**, if there exists $c, d \in \mathbb R_{> 0}$ such that for all integers $n \geq 0$, we have $|f(n)| \leq n^c + d$.

