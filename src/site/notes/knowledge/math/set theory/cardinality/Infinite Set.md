---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/cardinality/infinite-set/","dg-note-properties":{"aliases":["Infinite","Dedekind-Infinite","Dedekind-Finite","D-finite"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1: §6, Exercise 2; §7 (definition); §9, Theorem 9.1.
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 3: D-finite sets, Exercise 3.14, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/03-cardinal_numbers.pdf

## Intuition

> [!intuition] Why
> Infinite sets behave unlike finite ones: $\mathbb Z_{>0}$ is in bijection with the even numbers. Dedekind took this as the definition of infinite, and the theorem relating it to not being finite shows where the axiom of choice is needed.

## Definition

> [!definition] Infinite Set
> A set is **infinite** iff it is not [[knowledge/math/set theory/cardinality/Finite Set\|finite]] `[Mun00 §7]`.

> [!definition] Dedekind-Infinite
> A set $S$ is **Dedekind-finite** (D-finite) iff there is no one-to-one map of $S$ onto a proper subset of $S$, and **Dedekind-infinite** otherwise `[Jec03 Ch 3]`.

## Property

> [!theorem] Dedekind's Characterization — three ways to be infinite
> **Scope**
> - $A$: a set.
>
> ---
> **Property**
> The following are equivalent `[Mun00 Thm 9.1]`:
> - there is an injection $\mathbb Z_{>0} \to A$;
> - there is a bijection of $A$ with a proper subset of itself, i.e. $A$ is Dedekind-infinite;
> - $A$ is infinite.

> [!remark] Where choice enters
> - First ⇒ second: for an injection $f$, send $f(n)$ to $f(n + 1)$ and fix everything else; this is a bijection of $A$ onto $A \setminus \{f(1)\}$.
> - Second ⇒ third: a finite set has no bijection with a proper subset ([[knowledge/math/set theory/cardinality/Finite Set#Property\|Finite Set#Property]], Cor 6.3).
> - Third ⇒ first picks $a_1 \in A$, then $a_2 \in A \setminus \{a_1\}$, and so on: infinitely many choices, made with the [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]] in `[Mun00 §9]`.
>
> `[Jec03 Ch 3]` records the same split: every finite set is D-finite, and with the Axiom of Choice every infinite set is D-infinite.

> [!proposition] Countable subsets — the first condition again
> **Scope**
> - A set $S$.
>
> ---
> **Property**
> $S$ is Dedekind-infinite $\iff$ $S$ has a countably infinite subset.
>
> `[Jec03 Ex 3.14]`, where "countable" means countably infinite ([[knowledge/math/set theory/cardinality/Countable Set#Definition\|Countable Set#Definition]]).

## Example

> [!example] Bijections onto proper subsets
> - $\mathbb Z_{>0} \to \{2, 4, 6, \dots\}$, $n \mapsto 2n$.
> - $\mathbb R \to (0, \infty)$, $x \mapsto e^x$.
> - Every superset of an infinite set is infinite `[Mun00 §6 Ex 2]`.

## Related

### Siblings
- [[knowledge/math/set theory/cardinality/Finite Set\|Finite Set]] — the complement
- [[knowledge/math/set theory/cardinality/Countable Set\|Countable Set]] — with choice, every infinite set has a countably infinite subset
