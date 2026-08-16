---
{"dg-publish":true,"permalink":"/knowledge/math/combinatorics/combinatorics/","dg-note-properties":{}}
---


> [!principle] Basic Counting Principle
> If two experiments are performed, one of which has $n$ possible outcomes and the other of which has $m$ possible outcomes, then there are $nm$ possible outcomes of performing both experiments.

> [!principle] Inclusion-Exclusion Principle
> For $n$ finite sets $A_1, A_2, A_3, \cdots, A_n$. We have
> $|\bigcup_{i = 1}^n A_i| = \sum_{i = 1}^n |A_i| - \sum_{i < j} |A_i \cap A_j| + \sum_{i < j < k} |A_i \cap A_j \cap A_k| - \cdots + (-1)^{n + 1} | \bigcap_{i = 1}^n A_i|.$
> 
> For $n$ events $A_1, A_2, \cdots, A_n$, we have
> $P(\bigcup_{i = 1}^n A_i) = \sum_{i = 1}^n P(A_i) - \sum_{i < j} P(A_i \cap A_j) + \sum_{i < j < k} P(A_i \cap A_j \cap A_k) - \cdots + (-1)^{n + 1} P(\bigcap_{i = 1}^n A_i).$

## Counting

> [!principle] Multiplication Principle
> Suppose that we perform $r$ experiments such that the $k$th experiment has $n_k$ possible outcomes, for $k = 1, 2, \cdots, r$. Then there are a total of $n_1 \times n_2 \times n_3 \times \cdots \times n_k$ possible outcomes for the sequence of $r$ experiments.

> [!definition] Setting For Counting Problem
> - **Sampling**: sampling from a set means choosing an element from that set. We often **draw** a sample at random from a given set in which each element of the set has equal chance of being chosen.
> - **With or without replacement**: usually we draw multiple samples from a set. If we put each object back after each draw, we call this **sampling with replacement** (repetition is allowed). On the other hand, if repetition is not allowed, we call it **sampling without replacement**.
> - **Ordered or unordered**: If ordering matters, this is called **ordered sampling**. Otherwise, it is called **unordered**.

## Permutation

> [!definition] Permutation
> Let $S$ be a set containing $n$ distinct objects. A **permutation** of $S$ is an ordered list of the objects in $S$. A permutation of the set $\{1, 2, \dots, n\}$ is simply called a **permutation of** $n$.

> [!proposition] 
> Let $S$ be a set containing $n$ distinct objects. Then there are exactly $n!$ different permutation of $S$.

> [!definition] $k$-Permutations
> A choosing of $k$ elements, ordered and no repetition is called a $k$-permutation of the elements in set $A$.
> The number of $k$-permutations of $n$ distinguishable objects is given by $$P^{n}_k = \frac{n!}{(n - k)!}, \text{for } 0 \leq k \leq n.$$

> [!definition] Sign of a Permutation
> The **sign** of a permutation $(m_1, \dots, m_n)$ is defined to be $1$ if the number of pairs of integers $(j, k)$ with $1 \leq j < k \leq n$ such that $j$ appears after $k$ in the list $(m_1, \dots, m_n)$ is even and $-1$ if the number of such pairs is odd.

> [!remark]
> We use $\text{perm } n$ to be the set of all permutations of $(1, \dots, n)$.

> [!lemma]
> Interchanging two entries in a permutation multiplies the sign of the permutation by $-1$.

## Combinations

> [!definition] Combinations
> Let $S$ be a set containing $n$ distinct objects. A **combination of** $r$ objects of $S$ is a subset consisting of exactly $r$ distinct elements of $S$, where the order of the objects in the subset does not matter.

> [!proposition]
> The number of possible combinations of $r$ objects chosen from a set of $n$ objects is equal to $$\binom{n}{r} = \frac{n!}{r!(n - r)!}$$

> [!definition] Multinomial Coefficients
> The number of ways to divide $n$ distinct objects to $r$ distinct groups of sizes $n_1, n_2, \dots, n_r$ is given by $$\binom{n}{n_1, n_2, \dots, n_r} = \frac{n!}{n_1! n_2! \dots n_r!}$$

| Properties               | Remark         | Formula                                                                                                                                                                                   |
| ------------------------ | -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The Binomial Theorem     |                | $(x + y)^n = \sum_{j = 0}^{n} \binom{n}{j} x^j y^{n - j}.$                                                                                                                                |
| Law of Pascal's Triangle |                | $\binom{n + 1}{k} = \binom{n}{k - 1} + \binom{n}{k}$                                                                                                                                      |
| Multinomial Theorem      |                | $(x_1 + x_2 + \dots + x_r)^n = \sum_{n_1 + n_2 + \cdots + n_r = n} \binom{n}{n_1, n_2, \cdots, n_r} x_1^{n_1} x_2^{n_2} \dots x_r^{n_r}$                                                  |
|                          |                | $(n + 1) \binom{\alpha}{n + 1} = (\alpha - n) \binom{\alpha}{n}$                                                                                                                          |
|                          |                | $\binom{n}{k} = \binom{n}{n - k}$                                                                                                                                                         |
|                          |                | $\sum_{k = 0}^n \binom{n}{k} = 2^n$                                                                                                                                                       |
|                          | $0 \leq k < n$ | $\binom{n + 1}{k + 1} = \binom{n}{k + 1} + \binom{n}{k}$ (Choosing $k + 1$ objects, deciding the last object)                                                                             |
| Vandermonde's identity   |                | $\binom{m + n}{k} = \sum_{i = 0}^k \binom{m}{i} \binom{n}{k - i}$ (Choosing $k$ objects from a group $m + n$)<br>$\binom{m - n}{k} = \sum_{i = 0}^k (-1)^k \binom{m}{i} \binom{n}{k - i}$ |
|                          |                |                                                                                                                                                                                           |

> [!proposition] Binomial Formula
> For $n$ independent Bernoulli trials where each trial success probability $p$, the probability of $k$ successes is given by $$P(k) = \binom{n}{k} p^k (1 - p)^{n - k}$$

> [!proposition] Multinomial Formula
> Suppose that an experiment has $r$ possible outcomes, so the sample space is given by $$S = \{s_1, s_2, \dots, s_r\}.$$
> Also suppose that $P(s_i) = p_i$ for $i = 1, 2, \dots, r$. Then for $n = n_1 + n_2 + \dots + n_r$ independent trials of this experiment, the probability that each $s_i$ appears $n_i$ times is given by $$\binom{n}{n_1, n_2, \dots, n_r} p_1^{n_1} p_2^{n_2} \dots p_r^{n_r} = \frac{n!}{n_1! n_2! \dots n_r!} p_1^{n_1} p_2^{n_2} \dots p_r^{n_r}.$$

> [!example]
> Let $p$ be a prime number.
> 1. If $1 \leq j \leq p - 1$, then $\binom{p}{j}$ is divisible by $p$.
> 2. If $1 \leq j \leq p - 1$, then $\binom{p - 1}{j} = (-1)^j \pmod p$
> 3. $(a + b)^p \equiv a^p + b^p \pmod p$

> [!definition] Binomial of real number
> Let $\alpha$ is an arbitrary real numbers, then $$\binom{\alpha}{n} = \frac{\alpha (\alpha - 1) \cdots (\alpha - n + 1)}{n!}$$

## Unordered Sampling with Replacement

> [!lemma] 
> The total number of distinct $k$ samples from an $n$-element set such that repetition is allowed and ordering does not matter is the same as the number of distinct solutions to the equation $$x_1 + x_2 + \dots + x_n = k, \text{where } x_i \in \{0, 1, 2, 3, \dots\}.$$

> [!theorem]
> The number of distinct solutions to the equation $$x_1 + x_2 + \dots + x_n = k, \text{where } x_i \in \{0, 1, 2, 3, \dots\}.$$ is equal to $$\binom{n + k - 1}{k} = \binom{n + k - 1}{n - 1}.$$

> [!proof]
> We can represent the equation by the unary representation $x_i$ to get a sequence of $k$ character $1$ and $n - 1$ character $+$

## Catalan Number

### Binary Trees Count

> [!proposition]
> Let $b_n$ denote the number of different binary trees with $n$ nodes:
> 1. Recurrence formula: $b_0 = 1$ and for $n \geq 1$, $$b_n = \sum_{k = 0}^{n - 1} b_k b_{n - 1 - k}$$
> 2. Let $B(x)$ be the generating function $$B(x) = \sum_{n = 0}^\infty b_n x^n.$$ Then $B(x) = xB(x)^2 + 1$, and hence $B(x) = \frac{1}{2x}(1 - \sqrt{1 - 4x})$.
> 3. $b_n = \frac{1}{n + 1} \binom{2n}{n}$ is the $n$-th **Catalan number**.
> 4. $b_n = \frac{4^n}{\sqrt{\pi} n^{3/2}} (1 + O(1 / n))$.

### Number of Parenthesizations



## Miscellaneous Problem

### Matching Problem

> [!example] The Matching Problem
> $N$ guests arrive at a party. Each person is wearing a hat. We collect all the hats and then randomly redistribute the hats, giving each person one of the $N$ hats randomly. Let $X_N$ be the number of people who receive their own hats. Find the PMF of $X_N$.
> 

> [!remark] Solution
> **Inclusion-Exclusion Solution**: $P(X_n = 0) = \frac{1}{2!} - \frac{1}{3!} + \dots (-1)^N \frac{1}{N!}$
> **Derrangement Solution**: 
> - $!n = (n - 1)(!(n - 1) + !(n - 2))$ with $!0 = 1$ and $!1 = 0$.
> - $!n = \begin{cases} 1 &\text{if } n = 0, \\ n \cdot (!(n - 1)) + (-1)^n  &\text{if } n > 0.\end{cases}$
> 
> **PMF**: $P(X_N = k) = \binom{n}{k} !(n - k)$

### De Bruijn Sequence

> [!definition]
> A **de Brujin sequence** of order $n$ on a size-$k$ alphabet $A$ is a cyclic sequence in which every possible length-$n$ string on $A$ occurs exactly once as a substring. Such a sequence is denoted by $B(k, n)$ and has length $k^n$.