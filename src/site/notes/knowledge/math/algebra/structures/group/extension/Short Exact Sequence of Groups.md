---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/extension/short-exact-sequence-of-groups/","dg-note-properties":{"aliases":["Exact Sequence of Groups","Split Exact Sequence","Splitting Lemma for Groups"]}}
---

Reference:
- `[ConSpl]` — K. Conrad, _Splitting of short exact sequences for groups_, expository notes, §1, (1.1), Theorems 3.2, 3.3, Definition 3.4: https://kconrad.math.uconn.edu/blurbs/grouptheory/splittinggp.pdf

## Definition

> [!definition] Parameters
> - $H \xrightarrow{\alpha} G \xrightarrow{\beta} K$: [[knowledge/math/algebra/structures/group/Group\|groups]] and [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|group homomorphisms]].

> [!definition] Exact Sequence
> The sequence is **exact at $G$** if
> $$\operatorname{im} \alpha = \ker \beta.$$
> A longer sequence is exact if it is exact at every inner term.
>
> `[ConSpl §1]`

> [!definition] Short Exact Sequence of Groups
> A **short exact sequence** is a sequence
> $$1 \to H \xrightarrow{\alpha} G \xrightarrow{\beta} K \to 1$$
> exact at $H$, $G$ and $K$: $\alpha$ is injective, $\beta$ is surjective, and $\operatorname{im} \alpha = \ker \beta$.
>
> `[ConSpl (1.1)]`

> [!remark] Every one comes from a normal subgroup
> $\alpha(H) = \ker \beta$ is a [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]] of $G$, and $K \cong G / \alpha(H)$ by the [[knowledge/math/set theory/function/Canonical Decomposition\|first isomorphism theorem]]. Conversely, $N \trianglelefteq G$ gives $1 \to N \hookrightarrow G \twoheadrightarrow G/N \to 1$.

### Splitting

> [!definition] Split Short Exact Sequence
> The sequence **splits** (on the right) if there is a homomorphism $\beta_0 : K \to G$ with
> $$\beta \circ \beta_0 = \mathrm{id}_K.$$
>
> `[ConSpl Thm 3.3(1), Def 3.4]`

## Property

> [!theorem] Right splitting — iff $G$ is a semidirect product
> **Scope**
> - $1 \to H \xrightarrow{\alpha} G \xrightarrow{\beta} K \to 1$: a short exact sequence.
>
> ---
> **Property**
> The following are equivalent:
> - there is a homomorphism $\beta_0 : K \to G$ with $\beta \circ \beta_0 = \mathrm{id}_K$;
> - there are an action $\varphi : K \to \mathrm{Aut}(H)$ and an isomorphism $\theta : G \to H \rtimes_\varphi K$ compatible with $\alpha$ and $\beta$ ([[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]]).
>
> `[ConSpl Thm 3.3]`

> [!theorem] Left splitting — iff $G$ is a direct product
> **Scope**
> - $1 \to H \xrightarrow{\alpha} G \xrightarrow{\beta} K \to 1$: a short exact sequence.
>
> ---
> **Property**
> The following are equivalent:
> - there is a homomorphism $\alpha_0 : G \to H$ with $\alpha_0 \circ \alpha = \mathrm{id}_H$;
> - there is an isomorphism $\theta : G \to H \times K$ compatible with $\alpha$ and $\beta$.
>
> `[ConSpl Thm 3.2]`. Left splitting is the stronger condition: a semidirect product need not be a direct product.

## Example

> [!example] Split and non-split
> - $1 \to C_3 \to S_3 \to C_2 \to 1$ splits on the right, by $C_2 \cong \langle (1\,2) \rangle$, but not on the left: $S_3$ is not $C_3 \times C_2$.
> - $1 \to C_2 \to C_4 \to C_2 \to 1$ does not split: the only element of order 2 in $C_4$ lies in the kernel, so no homomorphism $C_2 \to C_4$ lifts the generator.

## Related

### Constructions
- [[knowledge/math/algebra/structures/group/extension/Group Extension\|Group Extension]] — $G$ in the middle of a short exact sequence is an extension of $K$ by $H$
- [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]] — the split case

### Prerequisites
- [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]], [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]], [[knowledge/math/algebra/structures/group/special group/Quotient Group\|Quotient Group]]
