---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/module/r-algebra/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 5.2: The category R-Mod.
- `[Las]` — _Modules over Rings and Algebras: Basics_, lecture notes on C. Lassueur's teaching page (RPTU Kaiserslautern-Landau; rings unital and associative): https://agag-lassueur.math.rptu.de/~lassueur/en/teaching/SumSchools/IKIU22/IKIU22/YAC21_ModAndAlgs.pdf

## Definition

> [!definition] Parameters
> - $R$: a [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]].
> - $S$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
> - $\alpha: R \rightarrow S$: a [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]].

> [!definition] R-algebra
> Extends:: [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]].
> Requires:: [[knowledge/math/algebra/structures/ring/subring/Ring Center\|Ring Center]].
>
> ---
> Let $R$ be a [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]]. An $R \mbox{-} \mathsf{algebra}$ is a [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]] $\alpha: R \rightarrow S$ such that $\alpha(R)$ is contained in the [[knowledge/math/algebra/structures/ring/subring/Ring Center\|center]] of $S$.
>
> `[Alu III.5.2]`

> [!remark] Equivalent form — a ring that is an $R$-module
> `[Las Def F.1(a)]` defines an $R$-algebra as a ring $S$ with a left [[knowledge/math/algebra/structures/ring/module/R-Module\|$R$-module]] structure on $(S, +)$ compatible with the multiplication:
> $$\forall r \in R,\ \forall a, b \in S: r \cdot (ab) = (r \cdot a) b = a (r \cdot b).$$
> The two forms correspond by
> - from $\alpha$: $r \cdot s = \alpha(r) s$;
> - back: $\alpha(r) = r \cdot 1_S$.

## Related

### Instantiations
- [[knowledge/math/algebra/structures/polynomial/Polynomial Ring\|Polynomial Ring]] — $R \to R[x]$, $r \mapsto$ the constant polynomial $r$
- [[knowledge/math/algebra/structures/ring/example/Matrix Ring\|Matrix Ring]] — $r \mapsto r I_n$
- [[knowledge/math/algebra/structures/ring/example/Group Algebra\|Group Algebra]] — $R[G]$

### Constructions
- [[knowledge/math/algebra/structures/ring/module/Category R-Alg\|Category R-Alg]] — $R$-algebras and their homomorphisms

### Siblings
- [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]] — an $R$-algebra is an $R$-module with a compatible multiplication
- [[knowledge/math/algebra/structures/Algebra Structure\|Algebra Structure]] — division algebras over $\mathbb R$; the octonions there are not associative, so they are not $\mathbb R$-algebras in this sense

### Prerequisites
- [[knowledge/math/algebra/structures/ring/special ring/Commutative Ring\|Commutative Ring]] — the base ring $R$
- [[knowledge/math/algebra/structures/ring/subring/Ring Center\|Ring Center]] — where $\alpha(R)$ must land
