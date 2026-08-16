---
{"dg-publish":true,"permalink":"/knowledge/cryptography/assumptions/lattice-based/lwe/module-learning-with-error/","dg-note-properties":{}}
---

Reference: https://eprint.iacr.org/2022/1690.pdf

## Parameters

> [!definition] Parameters
> - $d$: Degree of polynomial, NTT friendly.
> - $k$: Module rank.
> - $m$: Number of equations.
> - $q$: Modulus.
> - $\chi_s$: Secret distribution.
> - $\chi_e$: Error distribution.
> - $R = \mathbb Z[X]/(X^d + 1), R_q = R / qR$: Polynomials ring.

## Distribution

> [!definition] Module Learning With Error Distribution
> ### Distribution
> Sampling Experiment: $\mathsf{MLWE}(d, k, m, q, \chi_s, \chi_e)$
> 1. $A \xleftarrow{\$} R_q^{m \times k}$
> 2. $\mathbf{s} \leftarrow \chi_s^k$
> 3. $\mathbf{e} \leftarrow \chi_e^m$
> 4. $\mathbf{b} = A \mathbf{s} + \mathbf{e} \bmod q$
> 5. Output $(A, \mathbf{b})$

## Problem

### Search Variant

> [!definition] Search Module Learning With Error Problem Advantage
> Reference Name: $\mathsf{SMLWE}(d, k, m, q, \chi_s, \chi_e)$
> 
> ---
> For any adversary $\mathcal A = (\mathcal A_\mathsf{search})$, we define the following advantage:
> $$\mathsf{Adv}_\mathsf{MLWE}^\mathsf{search}(\mathcal A) = 
> \Pr\!\left[ 
> \begin{array}{l}
> \mathbf{s} \in \chi_s^k \\
> (\mathbf{b} - A \mathbf{s} \bmod q) \in \chi_e^m
> \end{array} 
> \;\middle |\; 
> \begin{array}{l}
> (A, \mathbf{b}) \leftarrow \mathsf{MLWE}(d, k, m, q, \chi_s, \chi_e) \\
> \mathbf{s} \leftarrow \mathcal A_\mathsf{search}(A, \mathbf{b})
> \end{array} \right] 
> $$

> [!remark]
> 1. MLWE generalizes LWE (set $d = 1$, get LWE)
> 2. Also, MLWE is a special "structured" version of LWE.
> 3. No one knows any method to solve MLWE that is faster than the best algorithm known for solving LWE.


### Decision Module Learning With Error

> [!definition] Decision Learning With Error Problem Advantage
> Reference Name: $\mathsf{DMLWE}(d, k, m, q, \chi_s, \chi_e)$
> 
> ---
> For any adversary $\mathcal A = (\mathcal A_\mathsf{decide})$, we define the following advantage:
> $$\mathsf{Adv}^\mathsf{decide}_\mathsf{MLWE}(\mathcal A) = 
> \left|\; \Pr\!\left[
> \begin{array}{l}
> b' = 1
> \end{array}
> \;\middle |\; 
> \begin{array}{l}
> (A, \mathbf{b}) \leftarrow \mathsf{MLWE}(d, k, m, q, \chi_s, \chi_e) \\
> b' \leftarrow \mathcal A_\mathsf{decide}(A, \mathbf{b})
> \end{array} \right] 
> \;- 
> \Pr\!\left[
> \begin{array}{l}
> b' = 1
> \end{array}
> \;\middle |\; 
> \begin{array}{l}
> (A, \mathbf{b}) \xleftarrow{\$} R_q^{m \times k} \times R_q^{m} \\
> b' \leftarrow \mathcal A_\mathsf{decide}(A, \mathbf{b})
> \end{array} \right] 
> \right|.
> $$

