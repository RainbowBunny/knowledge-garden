---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/partial-order/","dg-note-properties":{"aliases":["Poset","Partially Ordered Set","Partial Order Axioms"]}}
---

Reference:
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definition rel.15, Example rel.19, Propositions rel.25, rel.26: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §11: the closing remark defining $\preceq$ from $\prec$; Exercise 2 (the partial order axioms).

## Intuition

> [!intuition] Why
> Partial orders are the general notion of being below or equal: inclusion of sets, divisibility, one topology being finer than another. Much of mathematics compares things this way without a total ranking.

## Definition

> [!definition] Partial Order
> Extends:: [[knowledge/math/set theory/order/Preorder\|Preorder]]
> 
> ---
> A [[knowledge/math/set theory/relation/Relation\|Relation]] $\leq$ on a set $S$ is called a partial order if it is a [[knowledge/math/set theory/order/Preorder\|Preorder]] that also satisfies [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]]. The three **partial order axioms** are
> - [[knowledge/math/property/relation/Reflexivity\|Reflexivity]]: $a \leq a$;
> - [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]]: $a \leq b \land b \leq a \Rightarrow a = b$;
> - [[knowledge/math/property/relation/Transitivity\|Transitivity]]: $a \leq b \land b \leq c \Rightarrow a \leq c$.
>
> `[OLP-Rel Def rel.15]`; `[Mun00 §11 Ex 2]` names the three axioms.

## Property

> [!proposition] Strict partial orders — the same structure, written with $<$
> **Scope**
> - $\leq$ a partial order on $S$.
>
> ---
> **Property**
> $a < b \iff a \leq b \land a \neq b$ defines a [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]].
> $a \leq b \iff a < b \lor a = b$ recovers $\leq$ from it.
>
> `[Mun00 §11 Ex 2]`, `[OLP-Rel Prop rel.25, rel.26]`; the proof is in [[knowledge/math/set theory/order/Strict Partial Order#Property\|Strict Partial Order#Property]]. `[Mun00 §11]` takes the strict order as primary and defines the partial order from it.

## Example

> [!example] Inclusion
> $\subseteq$ on any collection of sets is a partial order, and in general not a total one: $\{a\}$ and $\{b\}$ are incomparable `[OLP-Rel Ex rel.19]`.

## Related

### Descendants
- [[knowledge/math/set theory/order/Total Order\|Total Order]] — adds [[knowledge/math/property/relation/Comparability\|Comparability]]

### Siblings
- [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]] — the irreflexive description $<$
