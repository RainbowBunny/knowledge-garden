---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/order/strict-total-order/","dg-note-properties":{"aliases":["Simple Order","Order Relation","Strict Linear Order","Simply Ordered Set","Ordered Set"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3: order relation, open interval, immediate predecessor and successor, largest and smallest element; Exercise 7. Chapter 2: §14 (intervals and rays); §16 (convex subsets).
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definition rel.23, Propositions rel.25, rel.26: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 2, Definition 2.1, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/02-ordinal_numbers.pdf
- `[Leb]` — J. Lebl, _Basic Analysis I: Introduction to Real Analysis, Volume I_, §1.1, Definition 1.1.1: https://www.jirka.org/ra/html/sec_basicpropsrn.html

## Intuition

> [!intuition] Why
> When any two distinct elements are comparable, the set can be laid out on a line. This is the order of ℤ, ℚ and ℝ, and the order from which the order topology is built.

## Definition

> [!definition] Strict Total Order
> Extends:: [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]]
>
> ---
> A **strict total order** on a set $O$ is a [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]] $<$ that also satisfies [[knowledge/math/property/relation/Comparability\|Comparability]]. Spelled out, the axioms are
> - [[knowledge/math/property/relation/Comparability\|Comparability]]: $x \neq y \Rightarrow x < y \lor y < x$;
> - [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]]: never $x < x$;
> - [[knowledge/math/property/relation/Transitivity\|Transitivity]]: $x < y \land y < z \Rightarrow x < z$.
>
> `[Mun00 §3]` lists exactly these three and calls the relation an **order relation** (simple order, linear order); `[Jec03 Def 2.1]` a *linear ordering*; `[OLP-Rel Def rel.23]` a *strict linear order*. A set with one is a **simply ordered set**.

> [!definition] Strict Total Order (Trichotomy Form)
> Equivalently, $<$ is transitive and for all $x, y \in O$ exactly one of $x < y$, $x = y$, $y < x$ holds `[Leb Def 1.1.1]` ([[knowledge/math/property/relation/Comparability#Property\|Comparability#Property]]).

### Intervals and rays

> [!definition] Interval, Immediate Predecessor, Immediate Successor
> For $a < b$ in $O$:
> - the **open interval** is $(a, b) = \{x \in O : a < x < b\}$;
> - if $(a, b) = \emptyset$, $a$ is the **immediate predecessor** of $b$, and $b$ is the **immediate successor** of $a$.
>
> `[Mun00 §3]`

> [!definition] Intervals and Rays
> For $a < b$ in $O$:
> - the **closed interval** is $[a, b] = \{x : a \leq x \leq b\}$, and the **half-open intervals** are $[a, b) = \{x : a \leq x < b\}$ and $(a, b] = \{x : a < x \leq b\}$;
> - the **open rays** are $(a, +\infty) = \{x : a < x\}$ and $(-\infty, a) = \{x : x < a\}$;
> - the **closed rays** are $[a, +\infty) = \{x : a \leq x\}$ and $(-\infty, a] = \{x : x \leq a\}$.
>
> `[Mun00 §14]`. The symbols $\pm\infty$ are notation, not elements of $O$.

> [!definition] Largest and Smallest Element
> For $A_0 \subseteq O$, $b$ is the **largest element** of $A_0$ iff $b \in A_0$ and $x \leq b$ for every $x \in A_0$, where $x \leq b$ means $x < b$ or $x = b$; the **smallest element** is defined dually `[Mun00 §3]`. Bounds and suprema are in [[knowledge/math/set theory/order/Supremum\|Supremum]].

### Convex subsets

> [!definition] Convex Subset
> $Y \subseteq O$ is **convex** in $O$ iff for every $a < b$ in $Y$, the whole interval $(a, b)$ of $O$ lies in $Y$ `[Mun00 §16]`. Intervals and rays are convex; $[0, 1) \cup \{2\}$ is not convex in $\mathbb R$.

## Property

> [!proposition] Restriction — a subset inherits the order
> **Scope**
> - $<$ a strict total order on $O$; $A \subseteq O$.
>
> ---
> **Property**
> $< \cap\, (A \times A)$ is a strict total order on $A$.
>
> `[Mun00 §3 Ex 7]`. Each axiom quantifies over elements only, so it survives [[knowledge/math/set theory/relation/Relation#Restriction\|restriction]].

> [!proposition] Converse — reversing the order gives another one
> **Scope**
> - $<$ a strict total order on $O$; $>$ its [[knowledge/math/set theory/relation/Relation#Converse\|converse]].
>
> ---
> **Property**
> $>$ is a strict total order on $O$.
>
> Each axiom stays true when every comparison is read backwards: $z < y < x$ gives $z < x$.

> [!proposition] Total orders — the reflexive description
> **Scope**
> - $<$ a strict partial order on $O$, and $\leq \;=\; < \cup\, \mathrm{Id}_O$.
>
> ---
> **Property**
> $<$ is a strict total order $\iff$ $\leq$ is a [[knowledge/math/set theory/order/Total Order\|Total Order]].
>
> `[OLP-Rel Prop rel.25, rel.26]`; the correspondence itself is in [[knowledge/math/set theory/order/Strict Partial Order#Property\|Strict Partial Order#Property]].

## Example

> [!example] Standard orders
> - $\mathbb Z_{>0}$, $\mathbb Z$, $\mathbb Q$, $\mathbb R$ with $<$.
> - In $\mathbb Z$, $n + 1$ is the immediate successor of $n$; in $\mathbb Q$ and $\mathbb R$ no element has an immediate successor.
> - $\mathbb R \times \mathbb R$ in the [[knowledge/math/set theory/order/Dictionary Order\|Dictionary Order]].

> [!example] One set, two order types
> $\mathbb Z_{>0}$ under $<$ has a smallest element; under the converse $>$ it has a largest one and no smallest. No [[knowledge/math/set theory/order/Order Isomorphism\|Order Isomorphism]] connects the two, since an isomorphism carries smallest elements to smallest elements.

## Related

### Descendants
- [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]] — every nonempty subset has a smallest element

### Properties
- [[knowledge/math/property/relation/Least Upper Bound Property\|Least Upper Bound Property]] — every nonempty bounded-above subset has a supremum; with density, a linear continuum

### Constructions
- [[knowledge/math/set theory/order/Dictionary Order\|Dictionary Order]] — orders $A \times B$ from orders on $A$ and $B$
- [[knowledge/math/topology/Order Topology\|Order Topology]] — the topology whose basis is the open intervals

### Siblings
- [[knowledge/math/set theory/order/Total Order\|Total Order]] — the reflexive description $\leq$
