---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/module/r-module/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 5.1: Definition of (left-)R-module
- `[Las]` — _Modules over Rings and Algebras: Basics_, lecture notes on C. Lassueur's teaching page (RPTU Kaiserslautern-Landau; rings unital and associative): https://agag-lassueur.math.rptu.de/~lassueur/en/teaching/SumSchools/IKIU22/IKIU22/YAC21_ModAndAlgs.pdf

## Definition

> [!definition] Parameters
> - $(R, +, \cdot)$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
> - $(M, +)$: an [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]].

> [!definition] Left-R-module
> Extends:: [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]].
> Requires:: [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
>
> ---
> A left-$R$-module structure on an [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]] $(M, +)$ consists of a map $R \times M \rightarrow M$, $(r, m) \mapsto r \cdot m$,
> that satisfies [[knowledge/math/property/operation/Distributivity\|Distributivity]] for $(+, \cdot)$, [[knowledge/math/property/operation/Associativity\|Associativity]] for $\cdot$, [[knowledge/math/property/operation/Identity Element\|Identity Element]] for $\cdot$ (for the map); explicitly, for all $r, s \in R$ and $m, n \in M$:
> - $(r + s) \cdot m = r \cdot m + s \cdot m$
> - $r \cdot (m + n) = r \cdot m + r \cdot n$
> - $(rs) \cdot m = r \cdot (s \cdot m)$
> - $1_R \cdot m = m$
>
> `[Alu III.5.1]` `[Las Def A.1(a), Rem A.5(a)]`

> [!remark] Equivalent form
> The four axioms say exactly that $r \mapsto (m \mapsto r \cdot m)$ is a [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]] $R \to \mathrm{End}(M)$ into the ring of endomorphisms of the abelian group $(M, +)$. `[Las Def A.1(a)]`

## Variant

### Right R-module

> [!definition] Right-R-module
> The map is now $M \times R \rightarrow M$, $(m, r) \mapsto m \cdot r$.
>
> `[Las Def A.1(b)]`

## Example

> [!example] $\mathbb Z$-modules
> Every [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]] is a $\mathbb Z$-module, in exactly one way, and every $\mathbb Z$-module is an abelian group. `[Las Rem A.5(b)]`

> [!example] $R$ over itself
> $R$ is a left $R$-module, the action being the multiplication of $R$; its submodules are its left ideals (see [[knowledge/math/algebra/structures/ring/module/Submodule\|Submodule]]). `[Alu III.5.3]`

## Related

### Instantiations
- [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]] — the $\mathbb Z$-modules
- [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]] — $R$ a [[knowledge/math/algebra/structures/field/Field\|Field]]
- [[knowledge/math/algebra/structures/action/Specht Module\|Specht Module]] — a module over the group algebra of a [[knowledge/math/algebra/structures/group/special group/Symmetric Group\|Symmetric Group]]

### Constructions
- [[knowledge/math/algebra/structures/ring/module/Submodule\|Submodule]] — a subgroup closed under the action
- [[knowledge/math/algebra/structures/ring/module/Category R-Mod\|Category R-Mod]] — $R$-modules and $R$-linear maps

### Siblings
- [[knowledge/math/algebra/structures/ring/module/R-algebra\|R-algebra]] — adds a ring multiplication compatible with the action
- [[knowledge/math/algebra/structures/action/Group Action\|Group Action]] — a group acting on a set; here a ring acts on an abelian group
