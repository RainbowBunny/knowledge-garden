---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/subgroup/group-center/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter IV: Groups, second encounter, Section 1.2: Center, centralizer, conjugacy classes.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the HTML edition at https://judsonbooks.org/aata-files/aata-html/; result numbers as there).

## Definition

> [!definition] Parameters
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]].
> - $\sigma: G \rightarrow \mathsf{Aut}_\mathsf{Grp}(G)$: the action of $G$ on itself by conjugation, $\sigma(g)(a) = gag^{-1}$ (see [[knowledge/math/algebra/structures/action/example/Group Action on Group\|Group Action on Group]]).

> [!definition] Group Center
> Extends:: [[knowledge/math/algebra/structures/Center\|Center]].
>
> ---
> The **center** of $G$, denote $Z(G)$, is the [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] $\mathrm{ker} \; \sigma$ of $G$.
> Concretely, the **center** of $G$ is
> $$Z(G) = \{g \in G \mid (\forall a \in G): ag = ga\}$$
> `[Alu IV §1.2]` `[Jud §14.2]`

## Property

> [!proposition] The center is an abelian normal subgroup
> $Z(G)$ is an [[knowledge/math/algebra/structures/group/special group/Abelian Group\|abelian]] [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]] of $G$. `[Jud Thm 11.1.5]`
>
> ---
> Normal: $Z(G) = \ker \sigma$, and the kernel of a homomorphism is a normal subgroup `[Jud Thm 11.1.5]`. Abelian: its elements commute with every element of $G$, in particular with each other.

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/subgroup/Centralizer\|Centralizer]] — $Z(G) = C_G(G)$
- [[knowledge/math/algebra/structures/ring/subring/Ring Center\|Ring Center]] — the center of $(R, \cdot)$; a [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]]

### Properties
- [[knowledge/math/algebra/structures/group/special group/p-Group\|p-Group]] — a group of order $p^n$ has a nontrivial center `[Jud Thm 14.2.4]`

### Constructions
- [[knowledge/math/algebra/structures/group/homomorphism/Inner Automorphism\|Inner Automorphism]] — $\mathrm{Inn}(G) \cong G / Z(G)$
- [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]] — $|G| = |Z(G)| + \sum_i [G : C_G(g_i)]$

### Prerequisites
- [[knowledge/math/algebra/structures/action/example/Group Action on Group\|Group Action on Group]] — the conjugation action $\sigma$
