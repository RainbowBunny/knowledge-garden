---
{"dg-publish":true,"permalink":"/knowledge/cryptography/assumptions/lattice-based/lwe/module-learning-with-error/","dg-note-properties":{}}
---

Reference:
- `[SSE+22]` — R. Steinfeld, A. Sakzad, M. F. Esgin, V. Kuchta, M. Yassi, R. K. Zhao, _LUNA: Quasi-Optimally Succinct Designated-Verifier Zero-Knowledge Arguments from Lattices_, ePrint 2022/1690 (ACM CCS 2024): https://eprint.iacr.org/2022/1690.pdf
- `[LS15]` — A. Langlois, D. Stehlé, _Worst-Case to Average-Case Reductions for Module Lattices_, Designs, Codes and Cryptography 75(3), 2015; ePrint 2012/090: https://eprint.iacr.org/2012/090

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

> [!remark] Names in the sources
> `[SSE+22 Def 2]` writes $\mathsf{MLWE}_{n, l, d, q, \chi}$ with $A \leftarrow U(R_q^{l \times n})$ and one distribution $\chi$ for the secret and the error: the case $(k, m) = (n, l)$ and $\chi_s = \chi_e = \chi$ here. `[LS15 Def 4.6]` states the search and the decision problem for arbitrarily many samples.

## Problem

### Search Variant

> [!definition] Search Module Learning With Error Problem Advantage
> Reference Name: $\mathsf{SMLWE}(d, k, m, q, \chi_s, \chi_e)$
> 
> ---
> A search game: recover the secret of the MLWE samples. `[LS15 Def 4.6]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $A \xleftarrow{\$} R_q^{m \times k}$<br>$\mathbf{s} \leftarrow \chi_s^k$<br>$\mathbf{e} \leftarrow \chi_e^m$<br>$\mathbf{b} = A \mathbf{s} + \mathbf{e} \bmod q$ | $\xrightarrow{\ (A,\, \mathbf{b})\ }$ | |
> | 2 | | $\xleftarrow{\ \mathbf{s}'\ }$ | outputs a candidate secret $\mathbf{s}' \in R_q^k$ |
>
> **Goal** — $\mathcal A$ wins iff:
> - $\mathbf{s}' = \mathbf{s}$.
>
> $$\mathsf{Adv}_\mathsf{MLWE}^\mathsf{search}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$

> [!remark]
> 1. MLWE generalizes LWE (set $d = 1$, get LWE)
> 2. Also, MLWE is a special "structured" version of LWE.
> 3. No one knows any method to solve MLWE that is faster than the best algorithm known for solving LWE.


### Decision Module Learning With Error

> [!definition] Decision Learning With Error Problem Advantage
> Reference Name: $\mathsf{DMLWE}(d, k, m, q, \chi_s, \chi_e)$
> 
> ---
> A distinguishing game: MLWE samples against uniform ones; the two branches differ in row 1 only. `[SSE+22 Def 2]`, `[LS15 Def 4.6]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | **Game 0**: $(A, \mathbf{b}) \leftarrow \mathsf{MLWE}(d, k, m, q, \chi_s, \chi_e)$<br>**Game 1**: $(A, \mathbf{b}) \xleftarrow{\$} R_q^{m \times k} \times R_q^{m}$ | $\xrightarrow{\ (A,\, \mathbf{b})\ }$ | |
> | 2 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_i(\mathcal A)$, the bit $b'$ in Game $i$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> $$\mathsf{Adv}^\mathsf{decide}_\mathsf{MLWE}(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$$

