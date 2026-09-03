---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/encoding-scheme/scheme/pairing-based-encoding-scheme/","dg-note-properties":{}}
---

## Scheme

> [!scheme] Pairing-based Encoding Scheme
> ### Parameters
> - $p$: Prime.
> - $\mathbb G$: Source [[knowledge/math/algebra/structures/groups/special groups/Cyclic Group#Definition\|Cyclic Group]] of order $p$.
> - $\mathbb G_T$: Target [[knowledge/math/algebra/structures/groups/special groups/Cyclic Group#Definition\|Cyclic Group]] of order $p$.
> - $g$: A fixed generator of $\mathbb G$.
> - $e: \mathbb G \times \mathbb G \rightarrow \mathbb G_T$: The [[knowledge/math/properties/map/Bilinearity#Definition\|Bilinear]] map that satisfies:
> 	1. $\forall a, b \in \mathbb Z_p: e(g^a, g^b) = e(g, g)^{ab}$
> 	2. $\langle g \rangle = \mathbb G \implies \langle e(g, g) \rangle = \mathbb G_T$.
> 
> ---
> ### Algorithms
> - $(pk, sk) \leftarrow \text{Gen}()$:
> 	1. Return $(pk = (p, \mathbb G, \mathbb G_T, e), sk = \perp)$
> - $z \leftarrow \text{Enc}(a)$:
> 	1. Return $z \leftarrow g^a$.

## Property

### Additive Homomorphic

> [!property] Additive Homomorphic
> $$\text{Enc}(a_1) + \text{Enc}(a_2) = g^{a_1} \cdot g^{a_2} = g^{a_1 + a_2} = \text{Enc}(a_1 + a_2)$$

### Quadratic Root Detection

> [!property] Quadratic Root Detection
> Given a quadratic polynomial $pp \in \mathbb F[x_0, \dots, x_t]$, if $pp(a_1, \dots, a_t) = 0$, then, we have:
> $$\begin{align}
> e(g, g)^{pp(a_1, \dots, a_t)} &= e(g, g)^{\sum_{i, j} c_{i, j} x_i x_j} \\
> &= \sum_{i, j} e(g^{x_i}, g^{x_j})^{c_{i, j}} \\ 
> &= \sum_{i, j} e(\text{Enc}(x_i), \text{Enc}(x_j))^{c_{i, j}} \\
> &\stackrel{?}{=} e(g, g)^0
> \end{align}$$


