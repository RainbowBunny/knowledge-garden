---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/subgroup/kernel-of-group-homomorphism/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter II: Groups, first encounter,  Section 6.2: Examples: Kernel and image.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the HTML edition at https://judsonbooks.org/aata-files/aata-html/; result numbers as there).

## Definition

> [!definition] Parameters
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]].
> - $G'$: a [[knowledge/math/algebra/structures/group/Group\|Group]].
> - $\varphi: G \rightarrow G'$: a [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]].
> - $e_{G'}$: the identity of $G'$.

> [!definition] Kernel of Group Homomorphism
> Requires:: [[knowledge/math/set theory/function/Kernel\|Kernel]], [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]].
>
> ---
> The **kernel** of $\varphi: G \rightarrow G'$ is the subset of $G$ consisting of elements mapping to the identity in $G'$:
> $$\ker \varphi = \{g \in G \; | \; \varphi(g) = e_{G'}\} = \varphi^{-1}(e_{G'}).$$
> `[Alu II §6.2]` `[Jud §11.1]`

> [!remark] Bridge to the origin
> [[knowledge/math/set theory/function/Kernel\|Kernel]] is the relation $a \sim b \iff \varphi(a) = \varphi(b)$; here the kernel is one fibre, $\varphi^{-1}(e_{G'})$. The fibre determines the relation, since $\varphi(a) = \varphi(b) \iff a^{-1}b \in \ker\varphi$: the classes of the relation are the [[knowledge/math/algebra/structures/group/special group/Coset\|cosets]] $a \ker\varphi$.

## Property

> [!proposition] Universal property of the kernel — $\ker\varphi \hookrightarrow G$ is final among homomorphisms that $\varphi$ sends to the identity
> Let $\varphi: G \rightarrow G'$ be a homomorphism. Then the [[knowledge/math/set theory/function/Inclusion Function\|Inclusion Function]] $\iota: \ker \varphi \hookrightarrow G$ is [[knowledge/math/algebra/category/Universal Property\|Final]] in the [[knowledge/math/algebra/category/Category\|Category]] of group homomorphism $\alpha: K \rightarrow G$ such that $\varphi \circ \alpha$ is the trivial homomorphism $K \rightarrow G'$, $k \mapsto e_{G'}$ (the one that factors through the [[knowledge/math/algebra/structures/group/example/Trivial Group\|Trivial Group]]). `[Alu II §6.2]`

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]] — the same subgroups: a kernel is normal `[Jud Thm 11.1.5]`, and every normal subgroup is a kernel
- [[knowledge/math/algebra/structures/ring/Ring Homomorphism#Kernel\|Ring Homomorphism#Kernel]] — the ring version, an [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]]

### Prerequisites
- [[knowledge/math/set theory/function/Kernel\|Kernel]] — the origin, as a relation
- [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]]
