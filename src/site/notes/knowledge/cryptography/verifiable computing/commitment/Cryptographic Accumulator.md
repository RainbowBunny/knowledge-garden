---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/cryptographic-accumulator/","dg-note-properties":{"aliases":["Accumulator"]}}
---

Reference:
- `[TNLPS26]` — N. Tran, K. Nguyen, D. Liu, J. Pieprzyk, W. Susilo, _Compact Lattice-Based NIZK Arguments for Set Membership and Ring Signatures without RO_, ePrint 2026/1885: §2.2 (syntax, Definition 3), §4.1 (Definition 7, Lemma 1, Theorem 1): https://eprint.iacr.org/2026/1885
- `[LNWX18]` — S. Ling, K. Nguyen, H. Wang, Y. Xu, _Lattice-Based Group Signatures: Achieving Full Dynamicity (and Deniability) with Ease_, extended version of an ACNS 2017 paper, arXiv 1801.08737: §3.1 (syntax, Definition 4), Definition 5 and Lemma 1 (the Merkle-tree accumulator of Libert, Ling, Nguyen and Wang): https://arxiv.org/pdf/1801.08737
- `[BCF+21]` — D. Benarroch, M. Campanelli, D. Fiore, K. Gurkan, D. Kolonelos, _Zero-Knowledge Proofs for Set Membership: Efficient, Succinct, Modular_, Financial Cryptography 2021; ePrint 2019/1255, §1 (RSA and pairing accumulators): https://eprint.iacr.org/2019/1255.pdf

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter. $\mathrm{pp}$: public parameters, an implicit input of the other algorithms.
> - $R = \{d_0, \dots, d_{N-1}\}$: a set of $N = \mathrm{poly}(\lambda)$ values. $u$: an accumulator value. $d$: a value. $w$: a membership witness.
>
> `[TNLPS26 §2.2]`

> [!definition] Cryptographic Accumulator
> A (deterministic) **accumulator** is a tuple of PPT algorithms $(\mathsf{Setup}, \mathsf{Acc}, \mathsf{Witness}, \mathsf{Verify})$:
> - $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$: (Randomized) Setup algorithm.
>     - **Input**: the security parameter $1^\lambda$.
>     - **Output**: public parameters $\mathrm{pp}$.
> - $u \leftarrow \mathsf{Acc}(R)$: (Deterministic) Accumulation algorithm.
>     - **Input**: a set $R$ of $N$ values.
>     - **Output**: the accumulator value $u$.
> - $w \leftarrow \mathsf{Witness}(R, d)$: (Deterministic) Witness algorithm.
>     - **Input**: a set $R$ and a value $d$.
>     - **Output**: a witness $w$ that $d$ is accumulated in $\mathsf{Acc}(R)$, or $\perp$ if $d \notin R$.
> - $b \leftarrow \mathsf{Verify}(u, d, w)$: (Deterministic) Verification algorithm.
>     - **Input**: an accumulator value, a value and a witness.
>     - **Output**: $1$ if $(d, w)$ is valid for $u$, and $0$ otherwise.
>
> `[TNLPS26 §2.2]` `[LNWX18 §3.1]`

> [!remark] Notation in the literature
> | source | algorithms | differences |
> | --- | --- | --- |
> | `[TNLPS26 §2.2]` | $(\mathsf{TSetup}, \mathsf{TAcc}, \mathsf{TWitness}, \mathsf{TVerify})$ | $\mathrm{pp}$ implicit |
> | `[LNWX18 §3.1]` | $\mathsf{TSetup}(\lambda)$, $\mathsf{TAcc}_\mathrm{pp}$, $\mathsf{TWitness}_\mathrm{pp}$, $\mathsf{TVerify}_\mathrm{pp}$ | $\mathrm{pp}$ as a subscript |

## Property

### Correctness

> [!definition] Correctness
> For all $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$, all sets $R$ and all $d \in R$,
> $$\mathsf{Verify}\big(\mathsf{Acc}(R), d, \mathsf{Witness}(R, d)\big) = 1.$$
> `[TNLPS26 §2.2]` `[LNWX18 §3.1]`

## Security

### Security against false witnesses

> [!definition] Parameters
> - The accumulator's $\lambda, \mathrm{pp}$ from Syntax. $\mathcal A$: a PPT [[knowledge/cryptography/foundations/Adversary\|Adversary]].

> [!definition] Accumulator Security
> ### Scope
> An accumulator and a PPT adversary $\mathcal A$.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ receives $\mathrm{pp}$; no oracle.
> - **Promise** — none.
> - **Quantifier** — $\forall$ PPT $\mathcal A$.
> - **Adaptivity** — $\mathcal A$ chooses the set itself, after seeing $\mathrm{pp}$.
>
> ---
> ### Experiment
> A search game with one branch. `[TNLPS26 Def 3]` `[LNWX18 Def 4]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $\mathrm{pp} \leftarrow \mathsf{Setup}(1^\lambda)$ | $\xrightarrow{\ \mathrm{pp}\ }$ | |
> | 2 | | $\xleftarrow{\ R,\, d^*,\, w^*\ }$ | outputs a set, a value and a witness |
> | 3 | $u = \mathsf{Acc}(R)$<br>$b = \mathsf{Verify}(u, d^*, w^*)$ | | |
>
> **Goal** — $\mathcal A$ wins iff all of:
> - $d^* \notin R$;
> - $b = 1$.
>
> ---
> ### Property
> The accumulator is **secure** if $\Pr[\mathcal A \text{ wins}]$ is negligible for every PPT $\mathcal A$.

## Example

### Lattice Merkle-tree accumulator

> [!definition] Parameters
> - $\mathcal R_{q_H}$: a polynomial ring modulo $q_H$. $B > 1$: a base; $\beta = B - 1$; $k_H = \lceil \log_B q_H \rceil$; $m = 2 n k_H$.
> - $\mathcal C_\beta$: ring elements with coefficients bounded by $\beta$. $\mathsf{dec}_B$: base-$B$ decomposition, with gadget matrix $\mathbf G_B$ ($\mathsf{dec}_B(\mathbf v) = \mathbf u$ means $\mathbf G_B \mathbf u = \mathbf v$).
> - $N = 2^\ell$: the number of leaves.
>
> `[TNLPS26 §4.1]`

> [!definition] Two-Input Lattice Hash
> For $\mathbf H = [\mathbf H_0 \mid \mathbf H_1] \in \mathcal R_{q_H}^{n \times m}$ with $\mathbf H_0, \mathbf H_1 \in \mathcal R_{q_H}^{n \times n k_H}$, and $\mathbf u_0, \mathbf u_1 \in \mathcal C_\beta^{n k_H}$,
> $$f_\mathbf H(\mathbf u_0, \mathbf u_1) = \mathsf{dec}_B(\mathbf H_0 \mathbf u_0 + \mathbf H_1 \mathbf u_1 \bmod q_H) \in \mathcal C_\beta^{n k_H}.$$
> Under $\mathsf{MSIS}^{(\infty)}_{n, m, \beta, q_H}$ (the module, $\ell_\infty$ form of [[knowledge/cryptography/assumptions/lattice-based/SIS/Short Integer Solution\|Short Integer Solution]]) the family is collision resistant. `[TNLPS26 Def 7, Lemma 1]`

> [!scheme] Algorithms `[TNLPS26 §4.1]`
> - $\mathsf{Setup}(1^\lambda)$: chooses $q_H, n, B$; samples $\mathbf H \xleftarrow{\$} \mathcal R_{q_H}^{n \times m}$; returns $\mathrm{pp} = (q_H, n, B, \mathbf H = [\mathbf H_0 \mid \mathbf H_1])$.
> - $\mathsf{Acc}(R)$: places $d_j$ at the leaf $\mathbf u_{j_0, \dots, j_{\ell-1}}$, where $(j_0, \dots, j_{\ell-1})$ is $j$ in binary; computes each inner node as $\mathbf u_{b_0, \dots, b_{i-1}} = f_\mathbf H(\mathbf u_{b_0, \dots, b_{i-1}, 0}, \mathbf u_{b_0, \dots, b_{i-1}, 1})$; returns the root $u = f_\mathbf H(\mathbf u_0, \mathbf u_1)$.
> - $\mathsf{Witness}(R, d)$: returns $\perp$ if $d \notin R$; otherwise, for $d = d_j$, returns the position and the siblings along the path, $w = \big((j_0, \dots, j_{\ell-1}), (\mathbf w_0, \dots, \mathbf w_{\ell-1})\big)$ with $\mathbf w_i = \mathbf u_{j_0, \dots, j_{i-1}, 1 - j_i}$.
> - $\mathsf{Verify}(u, d, w)$: sets $\mathbf v_{\ell-1} = d$; for $k = \ell - 1, \dots, 0$ computes
>     $$\mathbf v_{k-1} = \mathsf{dec}_B\big(\mathbf H_{j_k} \mathbf v_k + \mathbf H_{1 - j_k} \mathbf w_k \bmod q_H\big);$$
>     returns $1$ iff $\mathbf v_{-1} = u$.

> [!theorem] Security of the Merkle-tree accumulator `[TNLPS26 Thm 1]`
> The accumulator above is correct, and secure in the sense of Accumulator Security under $\mathsf{MSIS}^{(\infty)}_{n, m, \beta, q_H}$.

> [!remark] The binary original
> `[LNWX18 Def 5, Lemma 1]` restate the case $B = 2$ over $\mathbb Z_q$: $h_\mathbf A(\mathbf u_0, \mathbf u_1) = \mathsf{bin}(\mathbf A_0 \mathbf u_0 + \mathbf A_1 \mathbf u_1 \bmod q)$ with $\mathbf A = [\mathbf A_0 \mid \mathbf A_1] \in \mathbb Z_q^{n \times m}$, $k = \lceil \log_2 q \rceil$, $m = 2nk$, secure under $\mathrm{SIS}^\infty_{n, m, q, 1}$. The base $B$ trades hash size against the assumption `[TNLPS26 abstract]`.

### Number-theoretic accumulators

RSA accumulators — the accumulator and each witness are one element of a group of hidden order — and pairing-based accumulators, with small values but parameters of size about the set bound and a trusted setup `[BCF+21 §1]`. Neither is post-quantum.

## Related

### Siblings
- [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]] — an accumulator commits to a whole set, but deterministically: it binds without hiding
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Merkle Tree\|Merkle Tree]] — the hash tree the lattice example is

### Constructions
- [[knowledge/cryptography/verifiable computing/relation/Set Membership Relation\|Set Membership Relation]] — a zero-knowledge proof of a valid witness for a hidden value
- [[knowledge/cryptography/special function/hash function/scheme/Ajtai Hash Function\|Ajtai Hash Function]] — the one-input SIS hash behind $f_\mathbf H$
