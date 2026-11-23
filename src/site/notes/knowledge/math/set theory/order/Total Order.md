---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/total-order/","dg-note-properties":{"aliases":["Totally Ordered Set","Linear Order"]}}
---

Reference:
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definition rel.16, Propositions rel.25, rel.26: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3 (order relation).

## Definition

> [!definition] Total Order
> Extends:: [[knowledge/math/set theory/order/Partial Order\|Partial Order]]
> 
> ---
> A **total order** on a set $S$ is a [[knowledge/math/set theory/order/Partial Order\|Partial Order]] $\leq$ that also satisfies [[knowledge/math/property/relation/Comparability\|Comparability]]: any two distinct elements are comparable.
>
> `[OLP-Rel Def rel.16]`, where comparability is called *connected*.

> [!remark] Connexity instead of comparability
> For a reflexive relation, [[knowledge/math/property/relation/Comparability\|Comparability]] and [[knowledge/math/property/relation/Connexity\|Connexity]] say the same thing ([[knowledge/math/property/relation/Comparability#Property\|Comparability#Property]]). So a total order is equivalently a relation satisfying [[knowledge/math/property/relation/Connexity\|Connexity]], [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]] and [[knowledge/math/property/relation/Transitivity\|Transitivity]], with reflexivity coming free ([[knowledge/math/property/Math Properties MOC\|Math Properties MOC]], *The parenthesised tick*).

## Property

> [!proposition] Strict total orders — the same structure, written with $<$
> **Scope**
> - $\leq$ a total order on $S$.
>
> ---
> **Property**
> $\leq \setminus\, \mathrm{Id}_S$ is a [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]].
> Every strict total order arises this way from exactly one total order.
>
> `[OLP-Rel Prop rel.25, rel.26]`

## Example

> [!example] Numbers
> $\leq$ on $\mathbb Z$, $\mathbb Q$, $\mathbb R$; for $\mathbb R$ it comes from the [[knowledge/math/calculus/Real Number#The Order Axiom\|order axiom]].

## Related

### Descendants
- [[knowledge/math/algebra/structures/polynomial/monomial order/Monomial Order\|Monomial Order]] — a total order on monomials compatible with multiplication

### Siblings
- [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] — the irreflexive description $<$, which `[Mun00 §3]` takes as primary
