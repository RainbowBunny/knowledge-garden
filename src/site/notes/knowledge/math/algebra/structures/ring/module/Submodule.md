---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/module/submodule/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 5.3: Submodules and quotients.
- `[Las]` — _Modules over Rings and Algebras: Basics_, lecture notes on C. Lassueur's teaching page (RPTU Kaiserslautern-Landau; rings unital and associative): https://agag-lassueur.math.rptu.de/~lassueur/en/teaching/SumSchools/IKIU22/IKIU22/YAC21_ModAndAlgs.pdf

## Definition

> [!definition] Parameters
> - [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]]: Import $(R, M)$.
> - $N \subseteq M$: a subset.

> [!definition] Submodule
> Extends:: [[knowledge/math/algebra/structures/Substructure\|Substructure]].
> Requires:: [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]].
>
> ---
> A **submodule** $N$ of an [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]] $M$ is a [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] of $(M, +)$ preserved by the action of $R$:
> $$(\forall r \in R)(\forall n \in N): rn \in N.$$
> Thus, $N$ is itself an $R$-module, and the [[knowledge/math/set theory/function/Inclusion Function\|Inclusion Function]] $N \hookrightarrow M$ is a homomorphism of $R$-modules.
>
> `[Alu III.5.3]` `[Las Def A.2]`

## Property

> [!proposition] Submodules of $R$ — they are its left ideals
> As a [[knowledge/math/algebra/structures/ring/Ring\|Ring]], $R$ itself is a (left-)$R$-module; the submodules of $R$ are then precisely the (left-)[[knowledge/math/algebra/structures/ring/ideal/Ideal\|ideals]] of $R$.
>
> `[Alu III.5.3]`

> [!theorem] Kernel and image are submodules — of the source and of the target
> The kernel and the image of a homomorphism $\varphi: M \rightarrow M'$ of [[knowledge/math/algebra/structures/ring/module/R-Module\|$R$-modules]] are submodules (of $M, M'$, respectively).
>
> `[Alu III.5.3]` `[Las Rem A.5(e)]`

> [!proposition] Submodules from central elements and from ideals
> - If $r$ is in the [[knowledge/math/algebra/structures/ring/subring/Ring Center\|center]] of $R$ and $M$ is an $R$-module, then $rM = \{rm \mid m \in M\}$ is a submodule of $M$.
> - If $I$ is any (left-)[[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] of $R$, then $IM = \{\sum_i r_i m_i \mid r_i \in I, m_i \in M\}$ is a submodule of $M$.
>
> `[Alu III.5.3]`

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] — the group case
- [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]] — must contain $1$
- [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] — the submodules of $R$ itself

### Prerequisites
- [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]] — the ambient module
