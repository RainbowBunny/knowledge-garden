---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/relations/arithmetization/quadratic-span-program/","dg-note-properties":{}}
---

Reference: https://eprint.iacr.org/2014/718.pdf

## Basic Definition

> [!definition] Quadratic Span Program
> A quadratic span program over a field $\mathbb F$ contains: 
> - Two sets of polynomial $\mathcal V = \{v_0'(x), \dots v_m(x)\}$ and $\mathcal W = \{w_0'(x), \dots, w_m(x)\}$ 
> - A target polynomial $t(x)$. 
> - A partition of the indices $\mathcal I = \{1, \dots, m\}$ into $\mathcal I = \mathcal I_\text{labeled} \cup \mathcal I_\text{free}$ and a further partition $\mathcal I_\text{labeled} = \cup_{i = 1, j = 0}^{\ell, 1} \mathcal I_{i, j}$.
> 
> We say the size of quadratic span program is $m$ and the degree is $\deg (t(x))$.
> 
> For input $y \in \{0, 1\}^\ell$, let $\mathcal I_y = \mathcal I_\text{free} \cup_{i = 1}^\ell \mathcal I_{i, y_i}$, be the set of indices that "belong" to $y$. The quadratic span program accepts an input $y \in \{0, 1\}^\ell$ if and only if there exists $a_i, b_i \in \mathbb F$ such that
> $$t(x) \;|\; (v'_0(x) + \sum_{i \in \mathcal I_y} a_i v_i(x)) \cdot (w_0'(x) + \sum_{i \in \mathcal I_y} b_i w_i(x))$$

> [!definition] Quadratic Span Program verifies a Circuit
> We say the quadratic span program verifies a boolean function $f: \{0, 1\}^\ell \rightarrow \{0, 1\}$ if it accepts exactly those inputs $y$ where $f(y) = 1$. 
> 


