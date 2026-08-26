---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/relations/arithmetization/square-span-program/","dg-note-properties":{}}
---

Reference: 
- https://eprint.iacr.org/2014/718.pdf

## Basic Definition

> [!definition] Square Span Program
> A Square Span Program (SSP) $Q$ over the field $\mathbb F$ is a tuple consisting of 
> - $m + 1$ polynomials $v_0(x), \dots, v_m(x) \in \mathbb F[x]$ 
> - A target polynomial $t(x)$ such that $\deg (v_i(x)) \leq \deg (t(x))$ for all $i = 0, \dots, m$. 
> 
> We say that the square span program SSP has size $m$ and degree $\deg (t(x))$. 
> 
> We say that SSP accepts an input $a_1, \dots, a_\ell \in \{0, 1\}$ if and only if there exist $a_{\ell + 1}, \dots, a_m \in \{0, 1\}$ such that $t(x)$ divides $p(x)$, where:
> $$p(x) = (v_0(x) + \sum_{i = 1}^m a_i v_i(x))^2 - 1$$

> [!definition] Square Span Program verifies a Circuit
> We say that SSP $S$ verifies a [[knowledge/complexity/circuit/Boolean Circuit#Basic Definition\|Boolean Circuit]] $C : \{0, 1\}^\ell \rightarrow \{0, 1\}$ if it accepts exactly those inputs $(a_1, \dots, a_\ell) \in \{0, 1\}^\ell$, satisfying $C(a_1, \dots, a_\ell) = 1$.

### Property

### NP-Completeness

> [!remark]
> By [[knowledge/complexity/circuit/Boolean Circuit#Linearization of Gate\|Linearization of Gate]], we have:
> $$\begin{align}aV + b \in \{0, 2\}^d &\Longleftrightarrow (aV + b) \circ (aV + b - 2) = 0\\
> &\Longleftrightarrow (aV + b - 1) \circ (aV + b - 1) = 1\end{align}$$
> where $\circ$ denotes the Hadamard product.

> [!theorem]
> For any [[knowledge/complexity/circuit/Boolean Circuit#Basic Definition\|Boolean Circuit]] $C$ of $m$ wires and $n$ fan-in 2 gates and for any prime $p \geq \max(n, 8)$, there exist polynomials $v_0(x), \dots, v_m(x)$ such that, for any distinct roots $r_1, \dots, r_d \in \mathbb F$, $C$ is satisfiable if and only if:
> $$\prod_{i = 1}^d (x - r_i) \;|\; p(x) = (v_0(x) + \sum_{i = 1}^m c_i v_i(x))^2 - 1$$
> where $c_1, \dots, c_m \in \{0, 1\}$ correspond the the values on the wires in a satisfying assignment for the circuit.
> 
> Define $t(x) = \prod_{i = 1}^d (x - r_i)$, then for any circuit $C$ of $m$ wires and $n$ gates, there exists a degree $d = m + n$ Square Span Program $Q = (v_0(x), \dots, v_m(x), t(x))$ over a field $\mathbb F$ of order $p$ that verifies $C$.
