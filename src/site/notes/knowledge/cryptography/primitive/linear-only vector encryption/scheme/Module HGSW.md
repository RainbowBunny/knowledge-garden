---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/linear-only-vector-encryption/scheme/module-hgsw/","dg-note-properties":{}}
---

Reference: 
- https://eprint.iacr.org/2022/1690.pdf (LUNA; CCS '24)

## Scheme

> [!scheme] Module Half-Gentry-Sahai-Waters
> Reference Name: $\mathsf{HGSW}$
> 
> ---
>  ### Parameters
> **Ring and Modulus**:
> - $d$: Ring degree, power of 2 (NTT friendly).
> - $q = p \bar{q}$: Working modulus.
> - $p$: Plaintext modulus; divides $q$ so we can have $q / p$ message.
> - $\bar{q} = 2 \ell_q + 1 \bmod 4 \ell_q$: Prime cofactor; chosen for easier analysis.
> - $\ell_q \geq 2$: Number of irreducible factor of $x^d + 1 \bmod \bar{q}$, each of degree $d / \ell_q$.
> - $R = \mathbb Z[X]/(X^d + 1), R_q = R / qR, R_p = R / pR$: Polynomials ring.
> 
> **Dimensions**:
> - $\ell' = \ell + \tau$: Extended plaintext dimension.
> - $\tau$: Sparsification parameter.
> 
> **Messages**:
> - $m$: The number of vector messages.
> - $\boldsymbol{\mu}_i \in R_p^\ell$ for $i \in [m]$.
> 
> ---
> ### Building Block
> - $g_{\mathsf{rand}}^{-1}(a): R_q \rightarrow R^{1 \times m_q}$ ([[knowledge/math/algebra/structures/lattices/Lattice Gadget Algorithm\|Lattice Gadget Algorithm]]):
> 	- $\beta$: Gadget base.
> 	- $m_q = \lceil \log_\beta q \rceil$: Gadget length.
> 	- $L$: Rows of re-randomization matrix.
> 	- $\rho = L / m_q$: Ciphertexts per re-randomization block.
> 	- $\mathbf{g}^T = (1, \beta, \dots, \beta^{m_q - 1}) \in R_q^{1 \times m_q}$: Gadget vector.
> 	- $\mathbf{G} \in R_q^{L \times \rho}$: Gadget matrix.
> 	- $\mathbf{c} \in R_q^L$: Random vector.
> - [[knowledge/cryptography/assumptions/lattice-based/LWE/Module Learning With Error\|Module Learning With Error]]: 
> 	- $k \in \mathbb{Z}$: MLWE secret rank.
> 	- $s \in \mathbb{R}$: MLWE error width.
> - [[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution\|Discrete Gaussian Distribution]]:
> 	- $\mathcal D$: Distribution
> 	- $r > 0 \in \mathbb{R}$:  Re-randomization width.
> - [[knowledge/math/algebra/structures/lattices/Lattices#$q$-ary Lattices\|q-ary Lattices]]: $\Lambda_q^\perp$
> 
> ---
> ### Algorithms
> - $\mathrm{sk} \leftarrow \mathsf{Setup}(1^\lambda, 1^\ell) \in (R^{k \times \ell'}, R_p^{\tau \times \ell}, R_q^{m m_q \times k}, R^{m m_q \times \ell'})$:
> 	1. Samples $\mathbf{S} \leftarrow \mathcal D_{R, s}^{k \times \ell'}$.
> 	2. Samples $\mathbf{A} \leftarrow \mathcal U(R_q^{m m_q \times k}) = (\mathbf{A}_1, \dots, \mathbf{A}_m)^T$ with $\mathbf{A}_i \in R_q^{m_q \times k}$.
> 	3. Samples $\mathbf{E} \leftarrow \mathcal D_{R, s}^{m m_q \times \ell'} = (\mathbf{E}_1, \dots, \mathbf{E}_m)^T$ with $\mathbf{E}_i \in R^{m_q \times \ell'}$.
> 	4. Samples $\mathbf{T} \leftarrow \mathcal U(R_p^{\tau \times \ell})$ (Transformation matrix).
> 	5. Returns $\mathrm{sk} = (\mathbf{S}, \mathbf{T}, \mathbf{A}, \mathbf{E})$.
> - $\mathbf{C}_i \leftarrow \mathsf{Enc}(i, \mathrm{sk}, \boldsymbol{\mu}) \in R_q^{m_q \times (k + \ell')}$: Given the message index $i$, secret key $\mathrm{sk}$ and a message vector $\boldsymbol{\mu}_i^T = (\mu_{i, 1}, \dots, \mu_{i, \ell}) \in R_p^\ell$, computes the ciphertext.
> 	1. Computes $\bar{\mu_i}^T = \begin{bmatrix}\mu_i^T & (T \mu_i)^T\end{bmatrix} \in R_p^{\ell'} = (\bar{\mu}_{i, 1}, \dots, \bar{\mu}_{i, \ell'})$.
> 	2. Computes $\mathbf{H}_i = \begin{bmatrix}\mathbf{0}^{m_q \times k} & \bar{\mu}_{i, 1} \mathbf{g} & \cdots & \bar{\mu}_{i, \ell'} \mathbf{g}\end{bmatrix} \in R_q^{m_q \times (k + \ell')}$.
> 	3. Returns $\mathbf{C}_i = \begin{bmatrix}A_i & A_i S + E_i\end{bmatrix} + \frac{q}{p} \cdot \mathbf{H}_i \in R_q^{m_q \times (k + \ell')}$.
> - $c^{*} \leftarrow \mathsf{Add}(\{\mathbf{C}_i\}_{i \in [m]}, \{a_i \in R_q\}_{i \in [m]}) \in R_q^{1 \times (k + \ell')}$:
> 	1. Generates $\tilde{a}_i^T = g_\mathsf{rand}^{-1}(a_i)$.
> 	2. Computes $\tilde{\mathbf{C}}_i = \tilde{a}_i^T \mathbf{C}_i \in R_q^{1 \times (k + \ell')}$ the re-randomized scaled ciphertext.
> 	3. Samples $\tilde{y}_j \leftarrow \mathcal D_r^{\ell'}$ for $j \in [0, m / \rho - 1]$.
> 	4. Returns $\mathbf{c}^* = \sum_{j = 0}^{m / v - 1} (\sum_{i = 1}^\rho \tilde{\mathbf{C}}_{j \rho + 1} + [\mathbf{0}^k, \mathbf{y}_j^T])$.
> - $\mathsf{Dec}(\mathbf{S} \in R^{k \times \ell'}, \mathbf{c}^* \in R_q^{1 \times (k + \ell')})$:
> 	1. Computes $\bar{\mathbf{S}}^T = \begin{bmatrix}-\mathbf{S}^T & \mathbf{I}_{\ell'}^T\end{bmatrix}$.
> 	2. Computes $\bar{\mathbf{H}} = \langle \mathbf{c}^*, \bar{\mathbf{S}}\rangle$.
> 	3. Computes $\bar{\boldsymbol{\mu}} = \lceil (p / q') \cdot \bar{H} \rfloor \in R_p^{\ell'}$.
> 	4. Parses $\bar{\boldsymbol{\mu}} = [\bar{\boldsymbol{\mu}}_1, \bar{\boldsymbol{\mu}}_2]$, where $\bar{\boldsymbol{\mu}_1} = \bar{\boldsymbol{\mu}} \in R_p^\ell$ and $\bar{\boldsymbol{\mu}}_2 \in R_p^\tau$.
> 	5. If $\bar{\boldsymbol{\mu}}_2 \neq T \bar{\boldsymbol{\mu}}_1$ then return $\perp$, else return $\bar{\mu}_1 \in R_p^\ell$.
