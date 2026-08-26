---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/scheme/sum-check-protocol/","dg-note-properties":{}}
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
> ### Scheme
>  $$\begin{array}{llcl} 
\textbf{Round} & \textbf{Prover} & & \textbf{Verifier} \\[4pt] 
& (g(x_1, \dots, x_v), H) & & (g(x_1, \dots, x_v)) \\[6pt] 
0 & C_1 \leftarrow \sum_{b_1 \in \{0, 1\}} \cdots \sum_{b_v \in \{0, 1\}} g(b_1, \dots, b_v) & \xrightarrow{C_1} & \\[6pt] 
1 & g_1(X) \leftarrow \sum_{(x_2, \dots, x_v) \in \{0, 1\}^{v - 1}} & \xrightarrow{g_1(X)} & C_1 \stackrel{?}{=} g_1(0) + g_1(1); \deg g_1 \stackrel{?}{\leq} \deg_1(g) \\[6pt] 
& & \xleftarrow{r_1} & r_1 \in \mathbb F \\[6pt]
j & g_j(X) \leftarrow \sum_{(x_{j + 1}, \dots, x_v) \in \{0, 1\}^{v - j}} g(r_1, \dots, r_{j - 1}, X_j, x_{j + 1}, \dots, x_v) & \xrightarrow{g_j(X)} & g_{j - 1}(r_{j - 1}) \stackrel{?}{=} g_j(0) + g_j(1); \deg g_j \stackrel{?}{\leq} \deg_j(g) \\[6pt]
& & \xleftarrow{r_j} & r_j \in \mathbb F \\[6pt]
v & g_v(X_v) \leftarrow g(r_1, \dots, r_{v - 1}, X_v) & \xrightarrow{g_v(X)} & g_v(r_v) \stackrel{?}{=} g(r_1, \dots, r_v); \deg g_v \stackrel{?}{\leq} \deg_v(g)\\
\end{array}$$
> If any check fails, $\text{reject}$.

> [!definition] Language $\mathcal L$
> For any specified $H \in \mathbb F$, let $\mathcal L$ be the language of polynomials $g$ such that
> $$H = \sum_{b_1 \in \{0, 1\}} \sum_{b_2 \in \{0, 1\}} \cdots \sum_{b_v \in \{0, 1\}} g(b_1, \dots, b_v).$$

## Property

### Completeness

> [!property] Completeness of Sum-Check Protocol
> The sum-check protocol is an [[knowledge/cryptography/verifiable computing/proof/interactive/Interactive Proof Systems#Syntax\|Interactive Proof System]] for language $\mathcal L$ with [[knowledge/cryptography/verifiable computing/proof/interactive/Interactive Proof Systems#Completeness\|Compleness Error]] $\delta_c = 0$.

### Complexity

| Communication                                | Rounds | $\mathcal V$ time                     | $\mathcal P$ time                                                                                             |
| -------------------------------------------- | ------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| $O(\sum_{i = 1}^v \deg_i(g))$ field elements | $v$    | $O(v + \sum_{i = 1}^v \deg_i(g)) + T$ | $O(\sum_{i = 1}^v \deg_i(g) \cdot 2^{v - i} \cdot T)$<br>$= O(2^v \cdot T)$ if $\deg_i(g) = O(1)$ for all $i$ |

## Security

### Soundness

> [!security] Soundness of Sum-Check Protocol
> The sum-check protocol is an [[knowledge/cryptography/verifiable computing/proof/interactive/Interactive Proof Systems#Syntax\|Interactive Proof System]] for language $\mathcal L$ with [[knowledge/cryptography/verifiable computing/proof/interactive/Interactive Proof Systems#Soundness\|Soundness Error]] $\delta_s \leq vd / \mathbb F$.
