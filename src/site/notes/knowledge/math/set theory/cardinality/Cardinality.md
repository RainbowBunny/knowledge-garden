---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/cardinality/cardinality/","dg-note-properties":{"aliases":["Equinumerous","Equinumerosity","Same Cardinality","Schröder–Bernstein Theorem","Continuum Hypothesis"]}}
---

Reference:
- `[OLP-Siz]` — Open Logic Project, _Sets, Functions, Relations_, chapter "The Size of Sets", revision 9620cc7 (2026-07-12), Definitions siz.19, siz.22, siz.23, Proposition siz.20, Theorem siz.25: https://builds.openlogicproject.org/content/sets-functions-relations/size-of-sets/size-of-sets-complete.pdf
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 3: (3.1), (3.2), Theorem 3.2, cardinality of a well-ordered set, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/03-cardinal_numbers.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1: §6 (cardinality of a finite set); §9, Exercise 8; §10, Exercises 10, 11.

## Intuition

> [!intuition] Why
> Cardinality compares the sizes of sets by matching their elements instead of counting them. It works for infinite sets, and shows that infinite sets come in different sizes.

## Definition

> [!definition] Cardinality
> Two sets $A$ and $B$ **have the same cardinality** (are **equinumerous**), written $|A| = |B|$ or $A \approx B$, iff there is a [[knowledge/math/property/map/Bijection\|Bijection]] $A \to B$ `[OLP-Siz Def siz.19]` `[Jec03 (3.1)]`.

> [!definition] Cardinal Comparison
> - $|A| \leq |B|$, also written $A \preceq B$, iff there is an [[knowledge/math/property/map/Injection\|Injection]] $A \to B$ `[OLP-Siz Def siz.22]` `[Jec03 (3.2)]`.
> - $|A| < |B|$, also written $A \prec B$, iff $|A| \leq |B|$ and $|A| \neq |B|$ `[OLP-Siz Def siz.23]`.

> [!remark] What $|A|$ is
> The definitions compare sets without saying what $|A|$ is as an object. For a [[knowledge/math/set theory/cardinality/Finite Set\|Finite Set]] it is the number $n$ of elements `[Mun00 §6]`, and a countably infinite set has cardinality $\aleph_0$ `[Jec03 Ch 3]`. For a well-ordered set $W$, `[Jec03 Ch 3]` takes $|W|$ to be the least ordinal equinumerous with $W$; by the [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]] this covers every set once the [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]] is assumed.

> [!remark] Specializations
> | where | what the structure adds |
> | --- | --- |
> | [[knowledge/math/algebra/structures/group/Group Order\|Group Order]] | the order of a group is $\lvert G \rvert$; for a finite group, Lagrange's theorem makes it a multiple of every subgroup order |

## Property

> [!proposition] Equinumerosity — an equivalence
> **Scope**
> - Sets $A$, $B$, $C$.
>
> ---
> **Property**
> $|A| = |A|$.
> $|A| = |B| \Rightarrow |B| = |A|$.
> $|A| = |B| \land |B| = |C| \Rightarrow |A| = |C|$.
>
> `[OLP-Siz Prop siz.20]`: identities, inverses and composites of bijections are bijections.

> [!theorem] Schröder–Bernstein — injections both ways give a bijection
> **Scope**
> - Sets $A$, $B$.
>
> ---
> **Property**
> $|A| \leq |B| \land |B| \leq |A| \Rightarrow |A| = |B|$.
>
> `[OLP-Siz Thm siz.25]`; `[Jec03 Thm 3.2]` calls it the Cantor–Bernstein theorem.

> [!theorem] Cantor — no set is as large as its power set
> **Scope**
> - A set $A$.
>
> ---
> **Property**
> $|A| < |\mathcal P(A)|$.
>
> See [[knowledge/math/set theory/cardinality/Cantor's Theorem\|Cantor's Theorem]].

### Comparability of cardinals

> [!theorem] Comparability of Cardinals — any two sets are comparable in size
> **Scope**
> - Sets $A$, $B$.
>
> ---
> **Property**
> $|A| \leq |B|$ or $|B| \leq |A|$.
> With Schröder–Bernstein: exactly one of $|A| < |B|$, $|A| = |B|$, $|B| < |A|$ holds.
>
> `[Mun00 §10 Ex 11]`, using the [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]].

> [!proof] Why `[Mun00 §10 Ex 10, 11]`
> Assume $B \neq \emptyset$ and well-order $A$ and $B$. If there is a surjection $A \to B$, sending each $b$ to the least element of its preimage is an injection $B \to A$. If there is none, then no section of $A$ maps onto $B$ either, and the [[knowledge/math/set theory/order/Principle of Recursive Definition#Example\|recursion]] $h(x) = \text{smallest}\,[B \setminus h(S_x)]$ defines an injection $h : A \to B$.

### The continuum

> [!proposition] $\mathcal P(\mathbb Z_{>0})$ and $\mathbb R$ — the same cardinality
> **Scope**
> - $\mathcal P(\mathbb Z_{>0})$ and $\mathbb R$.
>
> ---
> **Property**
> $|\mathcal P(\mathbb Z_{>0})| = |\mathbb R|$.
>
> `[Mun00 §9 Ex 8]`, using decimal expansions, which are unique once those ending in an infinite string of 9s are excluded.

> [!remark] Continuum hypothesis
> The **continuum hypothesis** asserts that no set has cardinality strictly between $|\mathbb Z_{>0}|$ and $|\mathbb R|$. The **generalized continuum hypothesis** asserts that for every infinite $A$, no set has cardinality strictly between $|A|$ and $|\mathcal P(A)|$. Both are independent of the usual axioms of set theory `[Mun00 §9 Ex 8]`.

## Example

> [!example] Same cardinality, different shapes
> - $|\mathbb Z_{>0}| = |\mathbb Z_{>0} \times \mathbb Z_{>0}| = |\mathbb Q|$ ([[knowledge/math/set theory/cardinality/Countable Set\|Countable Set]]).
> - $|(-1, 1)| = |\mathbb R|$, via $x \mapsto x / (1 - x^2)$ ([[knowledge/math/set theory/order/Order Isomorphism#Example\|Order Isomorphism#Example]]).
> - $|\mathbb Z_{>0}| < |\{0, 1\}^\omega| = |\mathcal P(\mathbb Z_{>0})| = |\mathbb R|$ ([[knowledge/math/set theory/cardinality/Countable Set#Uncountable sets\|Countable Set#Uncountable sets]]).

## Related

### Properties
- [[knowledge/math/set theory/cardinality/Finite Set\|Finite Set]], [[knowledge/math/set theory/cardinality/Infinite Set\|Infinite Set]], [[knowledge/math/set theory/cardinality/Countable Set\|Countable Set]] — the first size classes
- [[knowledge/math/set theory/cardinality/Cantor's Theorem\|Cantor's Theorem]] — there is no largest size

### Siblings
- [[knowledge/math/algebra/structures/group/Group Order\|Group Order]] — group theory's name for $\lvert G \rvert$
