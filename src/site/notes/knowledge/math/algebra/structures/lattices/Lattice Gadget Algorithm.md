---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/lattices/lattice-gadget-algorithm/","dg-note-properties":{}}
---

## Definition

> [!algorithm] The $g^{-1}_{\mathsf{rand}}$ Algorithm
> ### Parameters
> - $d$: Degree of polynomial, NTT friendly.
> - $\beta \geq 2 \in \mathbb Z$: Decomposition base.
> - $q$: Modulus.
> - $m_q = \lceil \log_\beta q \rceil$: Number of base-$\beta$ digits needed for $\mathbb Z_q$.
> - $R = \mathbb Z[X]/(X^d + 1), R_q = R / qR$: Polynomials ring.
> - $L$: Total width; must satisfy $m_q \; | \; L$.
> - $\rho = L / m_q \in \mathbb Z$: Number of blocks.
> - $r > 0 \in \mathbb R$: Gaussian width.
> 
> ---
> ### Algorithms
> - Scalar Version $g_{\mathsf{rand}}^{-1}(a): R_q \rightarrow R^m_q$
> 	1. $\mathbf{g}^T = (1, \beta, \dots, \beta^{m_q - 1}) \in R_q^{1 \times m_q}$ (Gadget Vector).
> 	2. Generates $\mathbf{c} \in R^m_q$ is a fixed vector satisfying $\mathbf{c}^T \mathbf{g} = a \bmod q$ (Gadget Matrix).
> 	3. Samples $\mathbf{x} \leftarrow \mathcal D_{\Lambda_q^\perp(\mathbf{g}) + \mathbf{c}, r}$ ([[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution#Definition\|Discrete Gaussian]] of [[knowledge/math/algebra/structures/lattices/Lattices#$q$-ary Lattices\|q-ary Lattices]]).
> 	4. Outputs $\mathbf{x}^T$ which satisfies $\mathbf{x}^T \mathbf{g} = a \bmod q$ with $\mathbf{x}$ sub-gaussian of parameter $r$.
> - Vector Version: $g_{\mathsf{rand}}^{-1}(\mathbf{a}): R_q^\rho \rightarrow R^{1 \times L}$
> 	1. $\mathbf{g}^T = (1, \beta, \dots, \beta^{m_q - 1}) \in R_q^{1 \times m_q}$ (Gadget Vector).
> 	2. $\mathbf{G} = I_\rho \otimes \mathbf{g} \in R_q^{L \times \rho}$ (Kronecker Product)
> 	3. Generates $\mathbf{c} \in R^L$ is a fixed vector satisfying $\mathbf{c}^T \mathbf{G} = \mathbf{a} \bmod q$ (Gadget Matrix).
> 	4. Samples $\mathbf{x} \leftarrow \mathcal D_{\Lambda_q^\perp(G) + \mathbf{c}, r}$ ([[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution#Definition\|Discrete Gaussian]] of [[knowledge/math/algebra/structures/lattices/Lattices#$q$-ary Lattices\|q-ary Lattices]]).
> 	5. Outputs $\mathbf{x}^T$ which satisfies $\mathbf{x}^T \mathbf{G} = \mathbf{a} \bmod q$ with $\mathbf{x}$ sub-gaussian of parameter $r$.


