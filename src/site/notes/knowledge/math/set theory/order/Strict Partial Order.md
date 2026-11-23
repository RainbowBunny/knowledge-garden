---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/strict-partial-order/","dg-note-properties":{"aliases":["Strict Order","Strictly Partially Ordered Set","Chain","Maximal Element"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §11: strict partial order, upper bound, maximal element, the closing remark defining $\preceq$; Exercise 2.
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definition rel.22, Propositions rel.25, rel.26, Examples rel.19, rel.24: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, Definitions 2.1, 2.2, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf

## Intuition

> [!intuition] Why
> Many comparisons are partial: some pairs are simply incomparable, like $\{a\}$ and $\{b\}$ under inclusion. A strict partial order captures being strictly below without demanding comparability, and the maximality principles of set theory are cleanest in this form.

## Definition

> [!definition] Strict Partial Order
> A **strict partial order** on a set $O$ is a [[knowledge/math/set theory/relation/Relation\|Relation]] $\prec \;\subseteq O \times O$ satisfying
> - [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]];
> - [[knowledge/math/property/relation/Transitivity\|Transitivity]].
>
> `[Mun00 §11]`, `[Jec03 Def 2.1]`. `[OLP-Rel Def rel.22]` adds [[knowledge/math/property/relation/Asymmetry\|Asymmetry]], which these two already imply ([[knowledge/math/property/relation/Irreflexivity#Property\|Irreflexivity#Property]]).

> [!warning] Jech's "partial ordering" is this note
> `[Jec03 Def 2.1]` calls an irreflexive transitive relation a *partial ordering*. In this vault [[knowledge/math/set theory/order/Partial Order\|Partial Order]] is the reflexive version $\leq$; the two determine each other (below).

### Upper bounds and maximal elements

> [!definition] Upper Bound, Maximal Element, Chain
> Let $B \subseteq O$, and write $x \preceq y$ for $x \prec y \lor x = y$.
> - $c \in O$ is an **upper bound** on $B$ iff $b \preceq c$ for every $b \in B$.
> - $m \in O$ is a **maximal element** of $O$ iff there is no $a \in O$ with $m \prec a$.
> - $B$ is a **chain** (simply ordered subset) iff the restriction of $\prec$ to $B$ is a [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]].
>
> `[Mun00 §11]`; `[Jec03 Def 2.2]` defines maximal elements of any subset.

> [!remark] Maximal is not greatest
> A **greatest** element $g$ satisfies $x \preceq g$ for every $x$ `[Jec03 Def 2.2]`. A greatest element is maximal and unique; a maximal element need not be greatest, and there may be several. In $\mathcal P(\{a, b\}) \setminus \{\{a, b\}\}$ under $\subsetneq$, both $\{a\}$ and $\{b\}$ are maximal and neither is greatest. In a [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] the two notions agree.

## Property

> [!theorem] Strict and non-strict partial orders — two descriptions of one structure
> **Scope**
> - $O$: a set, $\mathrm{Id}_O = \{(x, x) : x \in O\}$.
>
> ---
> **Property**
> If $\prec$ is a strict partial order, then $\prec \cup\, \mathrm{Id}_O$ is a [[knowledge/math/set theory/order/Partial Order\|Partial Order]].
> If $\leq$ is a partial order, then $\leq \setminus\, \mathrm{Id}_O$ is a strict partial order.
> The two constructions are mutually inverse.
>
> `[Mun00 §11 Ex 2]`; `[OLP-Rel Prop rel.25, rel.26]`, which add that [[knowledge/math/set theory/order/Total Order\|total orders]] correspond to [[knowledge/math/set theory/order/Strict Total Order\|strict total orders]].

> [!proof] Why
> - $\prec \cup\, \mathrm{Id}_O$ is reflexive by construction; antisymmetric because $x \prec y$ and $y \prec x$ never both hold ([[knowledge/math/property/relation/Asymmetry\|Asymmetry]]); transitive by cases on which of the two pairs lie on the diagonal.
> - $\leq \setminus\, \mathrm{Id}_O$ is irreflexive by construction. If $x < y$ and $y < z$, then $x \leq z$; and $x = z$ would give $x \leq y \leq x$, so $x = y$ by [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]], which is excluded.
> - Removing and then adding the diagonal changes nothing, because $\prec$ contains no diagonal pair and $\leq$ contains all of them.

## Example

> [!example] Inclusion
> On any collection of sets, proper inclusion $\subsetneq$ is a strict partial order, and $\subseteq$ is the corresponding partial order `[Mun00 §11]` `[OLP-Rel Ex rel.24]`. It is not total: $\{a\}$ and $\{b\}$ are incomparable `[OLP-Rel Ex rel.19]`.

> [!example] Proper divisibility
> On $\mathbb Z_{>0}$, "$a \mid b$ and $a \neq b$" is a strict partial order. $1$ is the least element, the primes are the elements whose only predecessor is $1$, and there is no maximal element: $n$ properly divides $2n$.

## Related

### Descendants
- [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] — adds [[knowledge/math/property/relation/Comparability\|Comparability]]
- [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]] — a strict total order in which every nonempty subset has a least element

### Properties
- [[knowledge/math/set theory/choice/Zorn's Lemma\|Zorn's Lemma]] — chains bounded above force a maximal element
- [[knowledge/math/set theory/choice/Hausdorff Maximum Principle\|Hausdorff Maximum Principle]] — a maximal chain always exists

### Siblings
- [[knowledge/math/set theory/order/Partial Order\|Partial Order]] — the reflexive description $\leq$ of the same structure
