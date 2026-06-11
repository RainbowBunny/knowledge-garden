---
{"dg-publish":true,"permalink":"/knowledge/cryptography/threshold-cryptography/secret-sharing/schemes/combinatorial-approach-for-secret-sharing/","dg-note-properties":{}}
---

## Scheme

> [!scheme] Combinatorial Approach for Secret Sharing
> ### Parameters
> - $\mathbb G$: [[Non-Abelian Group\|Non-Abelian Group]].
> - $\mathcal M = \mathbb G$: Message space.
> - $t = 2$: Threshold.
> - $n$: Number of parties.
> - $\ell = \lceil \log_2 n \rceil$
> 
> ---
> ### Building Block
> - $\text{GetBits}(n, d)$: Write $n = n_1 \dots n_\ell$, return $n_d$.
> 
> ---
> ### Algorithms
> - $(s_1, \dots, s_n) \leftarrow \text{Share}(m)$:
> 	1. For $i = 1$ to $\ell$: Generate $m = k_{2i - 1} + k_{2i}$
> 	2. For $i = 1$ to $n$: $s_i = (k_{2j - 1 + \text{GetBits}(i, j)})_{j = \overline{1, \ell}}$
> 	3. Return $(s_1, \dots, s_n)$
> - $m \leftarrow \text{Reconstruct}(\{s_{i_1}, s_{i_2}, \dots\})$:
> 	1. Find a bit $j$ that $i_1$ and $i_2$ differs.
> 	2. Return $s_{i_1, j} + s_{i_2, j}$.
