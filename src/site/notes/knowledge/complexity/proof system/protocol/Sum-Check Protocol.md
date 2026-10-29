---
{"dg-publish":true,"permalink":"/knowledge/complexity/proof-system/protocol/sum-check-protocol/","dg-note-properties":{}}
---

Reference: 
- https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf
- [[academic/Book Reference\|Computational Complexity: A Modern Approach]] - Chapter 8: Interactive Proofs, Section 8.3.2: Interactive protocol for $\# \mathsf{SAT}_\mathsf{D}$.

## Scheme

> [!definition] Parameters
> - $n$: Number of variable.
> - $\mathbb F$: Finite field.
> - $g$: A $n$-variate polynomial.

> [!definition] Statement
> The prover want to convince the verifier the following statement:
> $$H = \sum_{b_1 \in \{0, 1\}} \sum_{b_2 \in \{0, 1\}} \cdots \sum_{b_n \in \{0, 1\}} g(b_1, \dots, b_n).$$

> [!scheme] Sum-Check Protocol
> - $n = 1$:
> $$ \begin{array}{llcl} 
\mathcal{P} & & \mathcal{V} \\[4pt] 
&  & g(1) + g(0) \stackrel{?}{=} K
\end{array}$$
> - $n \geq 2$:
> $$\begin{array}{llcl} 
\mathcal{P} & & \mathcal{V} \\[4pt] 
h(X_1) = \sum_{b_2 \in \{0, 1\}} \cdots \sum_{b_n \in \{0, 1\}} g(X_1, b_2, \dots, b_n) & \xrightarrow{h} & h(1) + h(0) \stackrel{?}{=} K; \deg(h(X_1)) \leq deg_{X_1}(g) \\
& \xleftarrow{a} & a \in \mathbb{F}
\end{array}$$
> Recursively, use the same protocol to check that
> $$h(a) = \sum_{b_2 \in \{0, 1\}} \cdots \sum_{b_n \in \{0, 1\}} g(a, b_2, \dots, b_n)$$

## Property

### Completeness

> [!property] Completeness of Sum-Check Protocol
> The sum-check protocol is an [[knowledge/cryptography/verifiable computing/proof system/interactive/Interactive Proof Systems#Syntax\|Interactive Proof System]] for language $\mathcal L$ with [[knowledge/cryptography/verifiable computing/proof system/interactive/Interactive Proof Systems#Completeness\|Compleness Error]] $\delta_c = 0$.

### Complexity

| Communication                                | Rounds | $\mathcal V$ time                     | $\mathcal P$ time                                                                                             |
| -------------------------------------------- | ------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| $O(\sum_{i = 1}^v \deg_i(g))$ field elements | $v$    | $O(v + \sum_{i = 1}^v \deg_i(g)) + T$ | $O(\sum_{i = 1}^v \deg_i(g) \cdot 2^{v - i} \cdot T)$<br>$= O(2^v \cdot T)$ if $\deg_i(g) = O(1)$ for all $i$ |

## Security

### Soundness

> [!proposition]
> If statement is false, then $\mathcal{V}$ rejects with probability at least $(1 - \frac{d}{|\mathbb{F}|})^n$.

> [!security] Soundness of Sum-Check Protocol
> The sum-check protocol is an [[knowledge/cryptography/verifiable computing/proof system/interactive/Interactive Proof Systems#Syntax\|Interactive Proof System]] for the statement with [[knowledge/cryptography/verifiable computing/proof system/interactive/Interactive Proof Systems#Soundness\|Soundness Error]] $\delta_s \leq vd / |\mathbb{F}|$.
