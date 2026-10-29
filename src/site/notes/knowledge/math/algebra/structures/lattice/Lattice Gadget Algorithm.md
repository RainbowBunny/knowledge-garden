---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/lattice/lattice-gadget-algorithm/","dg-note-properties":{}}
---

Reference:
- `[SSEKYZ22]` — R. Steinfeld, A. Sakzad, M. F. Esgin, V. Kuchta, M. Yassi, R. K. Zhao, _LUNA: Quasi-Optimally Succinct Designated-Verifier Zero-Knowledge Arguments from Lattices_ (2022), Preliminaries, Def 4 (randomized gadget decomposition): https://eprint.iacr.org/2022/1690
- `[MP12]` — D. Micciancio, C. Peikert, _Trapdoors for Lattices: Simpler, Tighter, Faster, Smaller_ (EUROCRYPT 2012), §2.4 (subgaussian), Lemma 2.8, §4 and §4.1 (the gadget $\mathbf g$, $\mathbf G = I_n \otimes \mathbf g^t$): https://web.eecs.umich.edu/~cpeikert/pubs/efftrap.pdf

## Definition

> [!definition] Parameters
> - $d$: Degree of polynomial, NTT friendly.
> - $\beta \geq 2 \in \mathbb Z$: Decomposition base.
> - $q$: Modulus.
> - $m_q = \lceil \log_\beta q \rceil$: Number of base-$\beta$ digits needed for $\mathbb Z_q$.
> - $R = \mathbb Z[X]/(X^d + 1)$: Polynomial ring.
> - $R_q = R / qR$: Polynomial ring modulo $q$.
> - $L$: Total width; must satisfy $m_q \; | \; L$.
> - $\rho = L / m_q \in \mathbb Z$: Number of blocks.
> - $r > 0 \in \mathbb R$: Gaussian width.

> [!definition] Gadget Vector and Gadget Matrix
> - $\mathbf{g}^T = (1, \beta, \dots, \beta^{m_q - 1}) \in R_q^{1 \times m_q}$ (Gadget Vector).
> - $\mathbf{G} = I_\rho \otimes \mathbf{g} \in R_q^{L \times \rho}$ ([[knowledge/math/algebra/linear algebra/Kronecker Product\|Kronecker Product]]) (Gadget Matrix).
>
> `[SSEKYZ22 Def 4]` `[MP12 §4]`

> [!remark] Notation in the literature
> [MP12 §4.1] takes base $2$, $\mathbf g^t = (1, 2, 4, \dots, 2^{k-1}) \in \mathbb Z_q^{1 \times k}$ with $k = \lceil \log_2 q \rceil$, notes that everything generalizes to any base $b \geq 2$, and writes $\mathbf G = I_n \otimes \mathbf g^t \in \mathbb Z_q^{n \times nk}$, the transpose of the form above. [SSEKYZ22 Def 4] writes $\mathbf G = \mathbf g \otimes I_\rho$; the two orders differ by a permutation of the $L$ rows.

> [!algorithm] The $g^{-1}_{\mathsf{rand}}$ Algorithm
> - $\mathbf{x}^T \leftarrow g_{\mathsf{rand}}^{-1}(a)$: Randomized gadget decomposition, scalar version, $R_q \rightarrow R^{1 \times m_q}$.
>     - **Input**: $a \in R_q$.
>     - **Output**: $\mathbf{x}^T \in R^{1 \times m_q}$ which satisfies $\mathbf{x}^T \mathbf{g} = a \bmod q$.
>     - **Steps**:
>         1. Fix any vector $\mathbf{c} \in R^{m_q}$ satisfying $\mathbf{c}^T \mathbf{g} = a \bmod q$; it fixes the coset $\Lambda_q^\perp(\mathbf{g}) + \mathbf{c}$.
>         2. Sample $\mathbf{x} \leftarrow \mathcal D_{\Lambda_q^\perp(\mathbf{g}) + \mathbf{c}, r}$ ([[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution#Definition\|Discrete Gaussian]] of [[knowledge/math/algebra/structures/lattice/Lattices#$q$-ary Lattices\|q-ary Lattices]]).
>         3. Output $\mathbf{x}^T$.
> - $\mathbf{x}^T \leftarrow g_{\mathsf{rand}}^{-1}(\mathbf{a})$: Randomized gadget decomposition, vector version, $R_q^\rho \rightarrow R^{1 \times L}$.
>     - **Input**: $\mathbf{a} \in R_q^\rho$.
>     - **Output**: $\mathbf{x}^T \in R^{1 \times L}$ which satisfies $\mathbf{x}^T \mathbf{G} = \mathbf{a} \bmod q$.
>     - **Steps**:
>         1. Fix any vector $\mathbf{c} \in R^L$ satisfying $\mathbf{c}^T \mathbf{G} = \mathbf{a} \bmod q$.
>         2. Sample $\mathbf{x} \leftarrow \mathcal D_{\Lambda_q^\perp(\mathbf G) + \mathbf{c}, r}$ ([[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution#Definition\|Discrete Gaussian]] of [[knowledge/math/algebra/structures/lattice/Lattices#$q$-ary Lattices\|q-ary Lattices]]).
>         3. Output $\mathbf{x}^T$.
>
> `[SSEKYZ22 Def 4]`

## Property

> [!proposition] Subgaussian output — above the smoothing parameter, $\mathbf x$ is subgaussian with parameter $r$
> If $r \geq \eta_\epsilon(\Lambda_q^\perp(\mathbf g))$ (vector version: $\eta_\epsilon(\Lambda_q^\perp(\mathbf G))$) for some $0 < \epsilon < 1$ ([[knowledge/math/algebra/structures/lattice/Lattices#Smoothing Parameter\|Lattices#Smoothing Parameter]]), then the output $\mathbf{x}$ is $\ln\frac{1 + \epsilon}{1 - \epsilon}$-subgaussian with parameter $r$.
>
> `[MP12 Lem 2.8]`

## Related

### Prerequisites
- [[knowledge/math/algebra/structures/lattice/Lattices#$q$-ary Lattices\|q-ary Lattices]] — the lattice $\Lambda_q^\perp(\mathbf g)$ whose cosets are sampled
- [[knowledge/math/algebra/structures/lattice/Lattices#Smoothing Parameter\|Lattices#Smoothing Parameter]] — the condition on $r$ for the subgaussian bound
- [[knowledge/math/algebra/linear algebra/Kronecker Product\|Kronecker Product]] — $\mathbf G = I_\rho \otimes \mathbf g$
- [[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution\|Discrete Gaussian Distribution]] — the sampled distribution
