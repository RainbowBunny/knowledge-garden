---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/extension/semidirect-product/","dg-note-properties":{"aliases":["Semi-direct Product","Internal Direct Product"]}}
---

Reference:
- `[ConSD]` — K. Conrad, _Semidirect products_, expository notes, Theorem 2.1, Definition 3.1, Theorems 3.11, 4.1, Lemma 6.2, Theorems 6.1, 6.3: https://kconrad.math.uconn.edu/blurbs/grouptheory/semidirect-product.pdf
- `[ConSpl]` — K. Conrad, _Splitting of short exact sequences for groups_, expository notes, Theorem 3.3: https://kconrad.math.uconn.edu/blurbs/grouptheory/splittinggp.pdf
- `[Dart13]` — Dartmouth College, Math 101 (Fall 2013), Homework 6 solutions, Problem 2: https://gauss.dartmouth.edu/~m101f13/hw6-solns.pdf

## Definition

> [!definition] Parameters
> - $H, K$: [[knowledge/math/algebra/structures/group/Group\|groups]].
> - $\varphi : K \to \mathrm{Aut}(H)$, $k \mapsto \varphi_k$: a [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]], an action of $K$ on $H$ by automorphisms.

> [!definition] Semidirect Product
> The **semidirect product** $H \rtimes_\varphi K$ is the set $H \times K$ with the operation
> $$(h, k)(h', k') = (h\, \varphi_k(h'),\ k k').$$
> $H$, the factor acted on, is the normal one.
>
> `[ConSD Def 3.1]`, which writes $H \rtimes_\varphi K$ as "$H \circ_\varphi K$".

### Internal semidirect product

> [!theorem] Recognition — a normal subgroup with a complement gives a semidirect product
> **Scope**
> - $G$: a group, with subgroups $H, K$.
> - $H \trianglelefteq G$, $H \cap K = \{e\}$, $G = HK$.
> - $\varphi_k(h) = khk^{-1}$: conjugation, an action of $K$ on $H$.
>
> ---
> **Property**
> $$H \rtimes_\varphi K \to G, \qquad (h, k) \mapsto hk$$
> is an isomorphism, and $G / H \cong K$.
>
> `[ConSD Thm 4.1]`. In a finite group the conditions can be checked by orders: [[knowledge/math/algebra/structures/group/subgroup/Normalizer#Products of subgroups\|Normalizer#Products of subgroups]].

> [!theorem] Internal direct product — two normal subgroups with trivial intersection
> **Scope**
> - $H, K \trianglelefteq G$ with $H \cap K = \{e\}$.
>
> ---
> **Property**
> $$H \times K \to HK, \qquad (h, k) \mapsto hk$$
> is an isomorphism; in particular $hk = kh$ for all $h \in H$, $k \in K$.
>
> `[Dart13 Problem 2]`: $hkh^{-1}k^{-1}$ lies in $H \cap K$. `[ConSD Thm 2.1]` states it with $G = HK$, $H \cap K = \{e\}$ and elementwise commuting subgroups.

## Property

> [!proposition] Normal factors — $H \times 1$ is always normal; $1 \times K$ only for the trivial action
> **Scope**
> - $H \rtimes_\varphi K$.
>
> ---
> **Property**
> - $H \times \{e\} \trianglelefteq H \rtimes_\varphi K$, with quotient $K$.
> - $\{e\} \times K \trianglelefteq H \rtimes_\varphi K$ iff $\varphi$ is trivial, and then $H \rtimes_\varphi K = H \times K$.
>
> `[ConSD Thm 3.11]`

> [!lemma] Twisting by an automorphism of $K$ — $H \rtimes_{\varphi \circ f} K \cong H \rtimes_\varphi K$
> **Scope**
> - $f \in \mathrm{Aut}(K)$.
>
> ---
> **Property**
> $$H \rtimes_{\varphi \circ f} K \cong H \rtimes_\varphi K.$$
>
> `[ConSD Lemma 6.2]`. Used to show that all nontrivial actions of $C_p$ on $C_q$ give one group — [[knowledge/math/algebra/structures/group/classification/Groups of Order pq\|Groups of Order pq]] `[ConSD Thm 6.3]`.

> [!remark] Split short exact sequences
> $G \cong H \rtimes_\varphi K$, compatibly with the inclusion of $H$ and the projection onto $K$, iff the [[knowledge/math/algebra/structures/group/extension/Short Exact Sequence of Groups\|short exact sequence]] $1 \to H \to G \to K \to 1$ splits on the right `[ConSpl Thm 3.3]`.

## Example

> [!example] Semidirect products
> - The [[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]] $D_n \cong C_n \rtimes C_2$, the reflection acting on the rotations by inversion `[ConSD]`.
> - For primes $p < q$ with $q \equiv 1 \bmod p$, the nonabelian group of order $pq$ is $C_q \rtimes C_p$ — [[knowledge/math/algebra/structures/group/classification/Groups of Order pq\|Groups of Order pq]] `[ConSD Thm 6.3]`.
> - $S_3 \cong A_3 \rtimes \langle (1\,2) \rangle \cong C_3 \rtimes C_2$.

## Related

### Siblings
- the direct product $H \times K$ — the case of the trivial action ([[knowledge/math/algebra/category/Categorical Product\|Categorical Product]])

### Constructions
- [[knowledge/math/algebra/structures/group/extension/Group Extension\|Group Extension]] — an extension that splits is a semidirect product
- [[knowledge/math/algebra/structures/group/extension/Cyclic Extension\|Cyclic Extension]] — the extension type $(N, n, \tau, e)$ gives $N \rtimes C_n$

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]], [[knowledge/math/algebra/structures/group/homomorphism/Inner Automorphism\|Inner Automorphism]], [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]]
