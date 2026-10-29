---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof-system/oracle/linear-probabilistically-checkable-proofs/","dg-note-properties":{"aliases":["Linear PCP","LPCP"]}}
---

Reference:
- `[ISW21]` — Y. Ishai, H. Su, D. J. Wu, _Shorter and Faster Post-Quantum Designated-Verifier zkSNARKs from Lattices_, ACM CCS 2021; full version ePrint 2021/977: https://eprint.iacr.org/2021/977.pdf
- `[BISW17]` — D. Boneh, Y. Ishai, A. Sahai, D. J. Wu, _Lattice-Based SNARGs and Their Application to More Efficient Obfuscation_, EUROCRYPT 2017; ePrint 2017/240: https://eprint.iacr.org/2017/240.pdf
- `[BCI+13]` — N. Bitansky, A. Chiesa, Y. Ishai, R. Ostrovsky, O. Paneth, _Succinct Non-Interactive Arguments via Linear Interactive Proofs_, TCC 2013; ePrint 2012/718: https://eprint.iacr.org/2012/718.pdf
- `[LUNA]` — R. Steinfeld, A. Sakzad, M. F. Esgin, V. Kuchta, M. Yassi, R. K. Zhao, _LUNA: Quasi-Optimally Succinct Designated-Verifier Zero-Knowledge Arguments from Lattices_, ACM CCS 2024; ePrint 2022/1690: https://eprint.iacr.org/2022/1690.pdf

## Syntax

> [!definition] Parameters
> - $\mathcal{CS} = \{\mathcal{CS}_\kappa\}_{\kappa \in \mathbb N}$: a family of [[knowledge/cryptography/verifiable computing/relation/r1cs/Rank-1 Constraint Satisfiability#Definition\|R1CS]] systems over a finite field $\mathbb F$, $\mathcal{CS}_\kappa = (n_\kappa, N_{g,\kappa}, N_{w,\kappa}, \{\mathbf a_{i,\kappa}, \mathbf b_{i,\kappa}, \mathbf c_{i,\kappa}\}_{i \in [N_{g,\kappa}]})$, of size at most $p(\kappa)$ for a polynomial $p$; $\kappa$ is the system index.
> - $\mathcal R_\mathcal{CS} = \{(\mathbf x, \mathbf w) \in \mathbb F^n \times \mathbb F^{N_w} : \mathcal{CS}(\mathbf x, \mathbf w) = 1\}$.
> - $k$: the number of queries. $\ell$: the query length. $\varepsilon$: the knowledge error.
> - $\mathbf Q \in \mathbb F^{\ell \times k}$: the query matrix; $\mathrm{st}$: the verification state.
>
> `[ISW21 Def 2.3, Def 2.5]`

> [!definition] Linear PCP
> A **$k$-query input-independent linear PCP** for $\mathcal{CS}$ with query length $\ell$ and knowledge error $\varepsilon$ is a tuple $\Pi_\mathsf{LPCP} = (\mathcal Q_\mathsf{LPCP}, \mathcal P_\mathsf{LPCP}, \mathcal V_\mathsf{LPCP})$:
> - $(\mathrm{st}, \mathbf Q) \leftarrow \mathcal Q_\mathsf{LPCP}(1^\kappa)$:
> 	- **Input**: the system index $\kappa$.
> 	- **Output**: a query matrix $\mathbf Q \in \mathbb F^{\ell \times k}$ and a verification state $\mathrm{st}$.
> - $\boldsymbol\pi \leftarrow \mathcal P_\mathsf{LPCP}(1^\kappa, \mathbf x, \mathbf w)$:
> 	- **Input**: the system index, a statement $\mathbf x \in \mathbb F^n$ and a witness $\mathbf w \in \mathbb F^{N_w}$.
> 	- **Output**: a proof $\boldsymbol\pi \in \mathbb F^\ell$.
> - $b \leftarrow \mathcal V_\mathsf{LPCP}(\mathrm{st}, \mathbf x, \mathbf a)$:
> 	- **Input**: the verification state, the statement and a vector of responses $\mathbf a \in \mathbb F^k$.
> 	- **Output**: a bit $b \in \{0, 1\}$.
>
> `[ISW21 Def 2.5]`

> [!definition] Linear Oracle
> The verifier never reads $\boldsymbol\pi$; it receives the responses
> $$\mathbf a = \mathbf Q^\top \boldsymbol\pi = \big(\langle \mathbf q_1, \boldsymbol\pi \rangle, \dots, \langle \mathbf q_k, \boldsymbol\pi \rangle\big) \in \mathbb F^k.$$
> *Input-independent*: $\mathbf Q$ is generated without seeing the statement. `[ISW21 Def 2.5; BISW17 Def 3.1]`

> [!remark] Notation in the literature
> | source | algorithms | differences |
> | --- | --- | --- |
> | `[BISW17 Def 3.1]` | $\mathcal V^{\boldsymbol\pi}_\mathsf{LPCP} = (Q_\mathsf{LPCP}, D_\mathsf{LPCP})$ | the verifier is a query algorithm and a deterministic decision algorithm; $\mathbf Q \in \mathbb F^{m \times \ell}$, so $\ell$ counts queries and $m$ is the query length — the opposite of `[ISW21]` |

## Property

### Completeness

> [!definition] Completeness
> For all $\kappa \in \mathbb N$ and all $(\mathbf x, \mathbf w)$ with $\mathcal{CS}_\kappa(\mathbf x, \mathbf w) = 1$:
> $$\Pr\big[\mathcal V_\mathsf{LPCP}(\mathrm{st}, \mathbf x, \mathbf Q^\top \boldsymbol\pi) = 1\big] = 1,$$
> where
> - $(\mathrm{st}, \mathbf Q) \leftarrow \mathcal Q_\mathsf{LPCP}(1^\kappa)$,
> - $\boldsymbol\pi \leftarrow \mathcal P_\mathsf{LPCP}(1^\kappa, \mathbf x, \mathbf w)$.
>
> `[ISW21 Def 2.5]`

## Security

### Knowledge against linear strategies

> [!definition] Knowledge
> There is an efficient extractor $\mathcal E_\mathsf{LPCP}$ such that for all $\kappa \in \mathbb N$, all $\mathbf x \in \mathbb F^n$ and all $\boldsymbol\pi^* \in \mathbb F^\ell$: if
> $$\Pr\big[\mathcal V_\mathsf{LPCP}(\mathrm{st}, \mathbf x, \mathbf Q^\top \boldsymbol\pi^*) = 1 \;\big|\; (\mathrm{st}, \mathbf Q) \leftarrow \mathcal Q_\mathsf{LPCP}(1^\kappa)\big] > \varepsilon,$$
> then
> $$\Pr\big[\mathcal{CS}_\kappa(\mathbf x, \mathbf w) = 1 \;\big|\; \mathbf w \leftarrow \mathcal E_\mathsf{LPCP}^{\langle \boldsymbol\pi^*, \cdot \rangle}(1^\kappa, \mathbf x)\big] = 1.$$
> The extractor has oracle access to the linear function $\langle \boldsymbol\pi^*, \cdot \rangle$. `[ISW21 Def 2.5]`

> [!remark] No adversary, no adaptivity
> A cheating prover here is a fixed proof vector $\boldsymbol\pi^*$ for a fixed statement $\mathbf x$, chosen before $\mathbf Q$ is drawn: it never sees the queries, so there is no interaction to draw as a game. The statement may depend on the queries only after compilation into a SNARG, where the queries are hidden by encryption — that is where adaptive soundness is defined, see [[knowledge/cryptography/verifiable computing/property/Soundness\|Soundness]]. "Linear" means the responses are exactly $\mathbf Q^\top \boldsymbol\pi^*$; ISW21 need only this, because their encryption is strictly linear-only ([[knowledge/cryptography/verifiable computing/property/Linear-Only Security\|Linear-Only Security]]) `[ISW21 Remark 3.5]`.

### Soundness against affine provers

> [!definition] Soundness Against Affine Provers
> The response is an affine function $\mathbf a = \mathbf Q^\top \boldsymbol\pi^* + \mathbf b^*$. For every $\mathbf x$ such that $(\mathbf x, \mathbf w) \notin \mathcal R$ for all $\mathbf w$, and every affine strategy $\Pi^* = (\boldsymbol\pi^*, \mathbf b^*)$, the verifier accepts with probability at most $\varepsilon$. `[BISW17 Def 3.2]`

> [!remark] Why affine
> With an encryption that is only affine-only — e.g. any public-key scheme, where the prover can add an encryption of its own vector — the compiled prover can shift the responses by $\mathbf b^*$, so the LPCP must be sound against affine strategies `[BISW17 Def 3.2; ISW21 Remark 3.5]`. Knowledge against affine strategies is the corresponding notion of `[BCI+13 Def 2.5]` for linear interactive proofs.

### Honest-verifier zero knowledge

> [!definition] Perfect Honest-Verifier Zero Knowledge
> There is an efficient simulator $\mathcal S_\mathsf{LPCP} = (\mathcal S_1, \mathcal S_2)$ such that for all $\kappa \in \mathbb N$ and all $(\mathbf x, \mathbf w)$ with $\mathcal{CS}_\kappa(\mathbf x, \mathbf w) = 1$:
> $$\{(\mathrm{st}, \mathbf Q, \mathbf Q^\top \boldsymbol\pi)\} \equiv \{(\widetilde{\mathrm{st}}, \widetilde{\mathbf Q}, \widetilde{\mathbf a})\},$$
> where
> - $(\mathrm{st}, \mathbf Q) \leftarrow \mathcal Q_\mathsf{LPCP}(1^\kappa)$ and $\boldsymbol\pi \leftarrow \mathcal P_\mathsf{LPCP}(1^\kappa, \mathbf x, \mathbf w)$;
> - $(\widetilde{\mathrm{st}}, \widetilde{\mathbf Q}, \mathrm{st}_\mathcal S) \leftarrow \mathcal S_1(1^\kappa)$ and $\widetilde{\mathbf a} \leftarrow \mathcal S_2(\mathrm{st}_\mathcal S, \mathbf x)$.
>
> The simulator is split into a statement-independent $\mathcal S_1$ and $\mathcal S_2$, for multi-theorem zero knowledge after compilation. `[ISW21 Def 2.5 and fn. 3]`

## Variant

### Honest-verifier zero knowledge with leakage
`[ISW21 Def 3.25]` asks that zero knowledge survive a leakage (the final encryption randomness revealed to the verifier when the SNARG uses no noise smudging). `[LUNA §1.1]` shows that this property does not hold in general for existing linear PCPs, and LUNA does not rely on it; the attack is in its Appendix D.

## Related

### Constructions
- [[knowledge/cryptography/verifiable computing/proof system/non-interactive/scheme/LUNA\|LUNA]], and the SNARGs of `[BISW17, ISW21]`: a linear PCP compiled through a [[knowledge/cryptography/primitive/vector encryption/Vector Encryption\|Vector Encryption]] that is [[knowledge/cryptography/verifiable computing/property/Linear-Only Security\|linear-only]] or [[knowledge/cryptography/verifiable computing/property/Strictly Linear Targeted Malleability\|linear targeted malleable]] `[ISW21 Thm 3.21]`

### Prerequisites
- [[knowledge/cryptography/verifiable computing/relation/r1cs/Rank-1 Constraint Satisfiability\|Rank-1 Constraint Satisfiability]], [[knowledge/cryptography/verifiable computing/proof system/non-interactive/Non-Interactive Proof Systems\|Non-Interactive Proof Systems]]
