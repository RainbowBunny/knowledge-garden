---
{"dg-publish":true,"permalink":"/knowledge/cryptography/foundations/generic-helper/private-re-randomization-of-mlwe-samples/","dg-note-properties":{}}
---

## Algorithm

> [!scheme] Private Re-randomization of MLWE Samples
> ### Parameters
> **Ring and Modulus**:
> - $d$: Ring degree, power of 2 (NTT friendly).
> - $q = p \bar{q}$: Working modulus.
> - $p$: Plaintext modulus (LPCP field characteristic); divides $q$ so we can have $q / p$ message.
> - $\bar{q} = 2 \ell_q + 1 \bmod 4 \ell_q$: Prime cofactor; chosen for easier analysis.
> - $\ell_q \geq 2$: Number of irreducible factor of $x^d + 1 \bmod \bar{q}$, each of degree $d / \ell_q$.
> - $R = \mathbb Z[X]/(X^d + 1), R_q = R / qR, R_p = R / pR$: Polynomials ring.
> 
> **Dimensions**:
> - $\ell' = \ell + \tau$: Extended plaintext dimension.
> - $\tau$: Sparsification parameter.
> 
> ---
> ### Building Block
> - [[knowledge/math/algebra/structures/lattices/Lattice Gadget Algorithm\|Lattice Gadget Algorithm]]: 
> 	- $\beta$: Gadget base.
> 	- $m_q = \lceil \log_\beta q \rceil$: Gadget length.
> 	- $L$: Rows of re-randomization matrix.
> 	- $\rho = L / m_q$: Ciphertexts per re-randomization block;
> 	- $\mathbf{G} \in R_q^{L \times \rho}$: Gadget matrix.
> 	- $\mathbf{c} \in R_q^L$: Random vector.
> - [[knowledge/cryptography/assumptions/lattice-based/LWE/Module Learning With Error\|Module Learning With Error]]: 
> 	- $k \in \mathbb{Z}$: MLWE secret rank
> 	- $s \in \mathbb{R}$: MLWE error width.
> - [[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution\|Discrete Gaussian Distribution]]:
> 	- $\mathcal D$: Distribution
> 	- $r > 0 \in \mathbb{R}$:  Re-randomization width.
> - [[knowledge/math/algebra/structures/lattices/Lattices#$q$-ary Lattices\|q-ary Lattices]]: $\Lambda_q^\perp$
> ---
> ### Algorithms
> 1. Samples $\mathbf{A} \xleftarrow{\$} R_q^{L \times k}$
> 2. Samples $\mathbf{E} \leftarrow \mathcal D_{R, s}^{L \times \ell'}$
> 3. Samples $\overline{\mathbf{x}} \leftarrow \mathcal D_{(\Lambda_q^{\perp}(G) + c) \times R^{\ell'}, r}$
> 4. Let $\bar{\mathbf{E}} = \begin{pmatrix}\mathbf{E} \\ \mathbf{I}_\ell'\end{pmatrix} \in R^{(L + \ell') \times \ell'}$
> 5. Let $\bar{\mathbf{A}} = \begin{pmatrix}\mathbf{A} \\ \mathbf{0}_{\ell' \times n}\end{pmatrix} \in R^{(L + \ell') \times n}$
> 6. Returns $(\bar{\mathbf{x}}^T \bar{\mathbf{A}} \bmod q, \bar{\mathbf{x}}^T \bar{\mathbf{E}} \bmod q, \mathbf{A}, \mathbf{E})$

