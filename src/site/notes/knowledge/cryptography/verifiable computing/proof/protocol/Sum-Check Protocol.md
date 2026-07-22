---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/protocol/sum-check-protocol/","dg-note-properties":{}}
---


Reference: https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf
## Scheme

> [!scheme] Sum-Check Protocol
> ### Parameters
> - $v$: Number of variable.
> - $\mathbb F$: Finite field.
> - $g$: A $v$-variate polynomial.
> - $\deg_j(g)$: Degree of $g(X_1, \dots, X_v)$ in variable $X_j$.
> 
> ---
> ### Statement
> The prover want to convince the verifier the following sum:
> $$H = \sum_{b_1 \in \{0, 1\}} \sum_{b_2 \in \{0, 1\}} \cdots \sum_{b_v \in \{0, 1\}} g(b_1, \dots, b_v).$$
> 
> ---
> ### Protocol
> 1. At the start of the protocol, the prover sends a value $C_1$ claimed to equal the value $H$.
> 2. In the first round, $\mathcal P$ sends the univariate polynomial $g_1(X_1)$ claimed to equal 
> $$\sum_{x_2, \dots, x_v} \in \{0, 1\}^{v - 1} g(X_1, x_2, \dots, x_v).$$
> $\mathcal V$ checks that 
> $$C_1 = g_1(0) + g_1(1),$$
> rejecting if not. 
> 3. $\mathcal V$ chooses a random element $r_1 \in \mathbb F$, and sends $r_1$ to $\mathcal P$.
> 4. In the $j$-th round, for $1 < j < v$, $\mathcal P$ sends to $\mathcal V$ a univariate polynomial $g_j(X_j)$ claimed to equal
> $$\sum_{(x_{j + 1}, \dots, x_v) \in \{0, 1\}^{v - j}} g(r_1, \dots, r_{j - 1}, X_j, x_{j + 1}, \dots, x_v).$$
> $\mathcal V$ checks that $g_j$ is a univariate polynomial of degree at most $\deg_j(g)$, and that $g_{j - 1}(r_{j - 1}) = g_j(0) + g_j(1)$, rejecting if not.
> 5. $\mathcal V$ chooses a random element $r_j \in \mathbb F$, and sends $r_j$ to $\mathcal P$.
> 6. In round $v$, $\mathcal P$ sends to $\mathcal V$ a univariate polynomial $g_v(X_v)$ claimed to equal
> $$g(r_1, \dots, r_{v - 1}, X_v).$$
> $\mathcal V$ checks that $g_v$ is a univariate polynomial of degree at most $\deg_v(g)$, rejecting if not, and also check that $g_v(r_v) = g(r_1, \dots, r_v)$, rejecting if not.
> 7. If $\mathcal V$ has not yet rejected, $\mathcal V$ halts and accepts.

> [!definition] Language $\mathcal L$
> For any specified $H \in \mathbb F$, let $\mathcal L$ be the language of polynomials $g$ such that
> $$H = \sum_{b_1 \in \{0, 1\}} \sum_{b_2 \in \{0, 1\}} \cdots \sum_{b_v \in \{0, 1\}} g(b_1, \dots, b_v).$$

## Property

### Completeness

> [!property] Completeness of Sum-Check Protocol
> The sum-check protocol is an [[knowledge/cryptography/verifiable computing/proof/Interactive Proof Systems#Syntax\|Interactive Proof System]] for language $\mathcal L$ with [[knowledge/cryptography/verifiable computing/proof/Interactive Proof Systems#Completeness\|Compleness Error]] $\delta_c = 0$.

### Complexity

| Communication                                | Rounds | $\mathcal V$ time                     | $\mathcal P$ time                                                                                             |
| -------------------------------------------- | ------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| $O(\sum_{i = 1}^v \deg_i(g))$ field elements | $v$    | $O(v + \sum_{i = 1}^v \deg_i(g)) + T$ | $O(\sum_{i = 1}^v \deg_i(g) \cdot 2^{v - i} \cdot T)$<br>$= O(2^v \cdot T)$ if $\deg_i(g) = O(1)$ for all $i$ |

## Security

### Soundness

> [!security] Soundness of Sum-Check Protocol
> The sum-check protocol is an [[knowledge/cryptography/verifiable computing/proof/Interactive Proof Systems#Syntax\|Interactive Proof System]] for language $\mathcal L$ with [[knowledge/cryptography/verifiable computing/proof/Interactive Proof Systems#Soundness\|Soundness Error]] $\delta_s \leq vd / \mathbb F$.
