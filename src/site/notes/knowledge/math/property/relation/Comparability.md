---
{"dg-publish":true,"permalink":"/knowledge/math/property/relation/comparability/","dg-note-properties":{"aliases":["Connected Relation","Connectedness (Relation)"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3 (order relation, "comparability").
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definition rel.7 ("connected"), Example rel.19: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, Definition 2.1(iii), read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf
- `[Leb]` — J. Lebl, _Basic Analysis I: Introduction to Real Analysis, Volume I_, §1.1, Definition 1.1.1: https://www.jirka.org/ra/html/sec_basicpropsrn.html

## Definition

> [!definition] Comparability
> ### Scope
> A relation $R \subseteq O \times O$.
>
> ---
> ### Property
> $R$ is **comparable** iff
> $$\forall x, y \in O: x \neq y \Rightarrow (x \;R\; y) \lor (y \;R\; x)$$
>
> `[Mun00 §3]` ("comparability"); `[OLP-Rel Def rel.7]` calls it **connected**; `[Jec03 Def 2.1(iii)]` writes it as $x \,R\, y \lor x = y \lor y \,R\, x$.

## Property

> [!proposition] Connexity — comparability plus reflexivity
> **Scope**
> - $R \subseteq O \times O$.
>
> ---
> **Property**
> $R$ satisfies [[knowledge/math/property/relation/Connexity\|Connexity]] $\iff$ $R$ satisfies Comparability and [[knowledge/math/property/relation/Reflexivity\|Reflexivity]].
>
> Connexity at $y = x$ is reflexivity; at $y \neq x$ it is comparability.

> [!proposition] Trichotomy — comparability plus asymmetry
> **Scope**
> - $R \subseteq O \times O$ satisfying [[knowledge/math/property/relation/Asymmetry\|Asymmetry]].
>
> ---
> **Property**
> $R$ is comparable $\iff$ for all $x, y \in O$ exactly one of $x \,R\, y$, $x = y$, $y \,R\, x$ holds.
>
> At most one holds because $R$ is asymmetric, hence irreflexive; at least one holds by comparability. `[Leb Def 1.1.1]` takes trichotomy and transitivity as the definition of an ordered set.

## Example

> [!example] Where it holds and where it fails
> - $<$ and $\leq$ on $\mathbb R$ are comparable.
> - $\subseteq$ on $\mathcal P(\{a, b\})$ is not: $\{a\}$ and $\{b\}$ are incomparable `[OLP-Rel Ex rel.19]`. Neither is $\subsetneq$.

## Related

### Descendants
- [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] — strict partial order + comparability
- [[knowledge/math/set theory/order/Total Order\|Total Order]] — partial order + comparability

### Siblings
- [[knowledge/math/property/relation/Connexity\|Connexity]] — also demands $x \,R\, x$, so it contradicts [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]]: a strict order can be comparable but never connex
