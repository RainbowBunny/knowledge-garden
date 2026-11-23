---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/cardinality/finite-set/","dg-note-properties":{"aliases":["Finite","Cardinality of a Finite Set"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §6: definition, Lemma 6.1, Theorem 6.2, Corollaries 6.3–6.8, Exercise 2.
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 3: finite sets, Exercise 3.1(i), read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/03-cardinal_numbers.pdf

## Intuition

> [!intuition] Why
> Finiteness needs a definition because having $n$ elements must be shown to make sense: the pigeonhole principle is what makes the count of a set unique.

## Definition

> [!definition] Finite Set
> A set $A$ is **finite** iff it is empty or there is a [[knowledge/math/property/map/Bijection\|Bijection]] $A \to \{1, \dots, n\}$ for some $n \in \mathbb Z_{>0}$. Then $A$ has **cardinality** $n$, and $\emptyset$ has cardinality $0$ `[Mun00 §6]`.
>
> `[Jec03 Ch 3]`: $X$ is finite iff $|X| = |n|$ for some natural number $n = \{0, \dots, n - 1\}$; the same notion, counted from $0$.

## Property

> [!lemma] Removing one element — the count drops by one
> **Scope**
> - $A$ a set, $a_0 \in A$, $n \in \mathbb Z_{>0}$.
>
> ---
> **Property**
> $A \approx \{1, \dots, n + 1\} \iff A \setminus \{a_0\} \approx \{1, \dots, n\}$.
>
> `[Mun00 Lemma 6.1]`

> [!theorem] Proper subsets of a finite set — strictly fewer elements
> **Scope**
> - $A$ with a bijection $A \to \{1, \dots, n\}$; $B \subsetneq A$.
>
> ---
> **Property**
> There is no bijection $B \to \{1, \dots, n\}$.
> If $B \neq \emptyset$, there is a bijection $B \to \{1, \dots, m\}$ for some $m < n$.
>
> `[Mun00 Thm 6.2]`, by induction on $n$ with the lemma.

> [!corollary] Consequences — no finite set is equinumerous with a proper subset
> **Scope**
> - $A$ finite; $B \subseteq A$.
>
> ---
> **Property**
> - There is no bijection of $A$ with a proper subset of itself `[Mun00 Cor 6.3]`.
> - $\mathbb Z_{>0}$ is not finite `[Mun00 Cor 6.4]`: $n \mapsto n + 1$ maps it onto a proper subset.
> - The cardinality of $A$ is uniquely determined by $A$ `[Mun00 Cor 6.5]`.
> - $B$ is finite, and if $B \subsetneq A$ its cardinality is smaller `[Mun00 Cor 6.6]`, `[Jec03 Ex 3.1(i)]`.
> - Finite unions and finite cartesian products of finite sets are finite `[Mun00 Cor 6.8]`.

> [!corollary] Finite via maps — a surjection from or an injection into a section
> **Scope**
> - $B$ a nonempty set.
>
> ---
> **Property**
> The following are equivalent `[Mun00 Cor 6.7]`:
> - $B$ is finite;
> - there is a surjection from some section $\{1, \dots, n\}$ of $\mathbb Z_{>0}$ onto $B$;
> - there is an injection from $B$ into some section $\{1, \dots, n\}$ of $\mathbb Z_{>0}$.

## Example

> [!example] The boundary
> - $\{1, \dots, n\}$ and all its subsets are finite.
> - A set with an infinite subset is infinite `[Mun00 §6 Ex 2]`; this is the contrapositive of Cor 6.6.
> - $\mathbb Z_{>0}$ is in bijection with its proper subset of even numbers, so it is not finite.

## Related

### Siblings
- [[knowledge/math/set theory/cardinality/Infinite Set\|Infinite Set]] — not finite; with choice, equivalently in bijection with a proper subset of itself
- [[knowledge/math/set theory/cardinality/Countable Set\|Countable Set]] — finite or in bijection with $\mathbb Z_{>0}$

### Prerequisites
- [[knowledge/math/set theory/cardinality/Cardinality\|Cardinality]]
