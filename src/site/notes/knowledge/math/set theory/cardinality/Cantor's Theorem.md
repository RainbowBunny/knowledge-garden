---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/cardinality/cantor-s-theorem/","dg-note-properties":{"aliases":["Cantor Theorem","Diagonal Argument"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §7, Theorems 7.7, 7.8.
- `[OLP-Siz]` — Open Logic Project, _Sets, Functions, Relations_, chapter "The Size of Sets", revision 9620cc7 (2026-07-12), Theorem siz.24: https://builds.openlogicproject.org/content/sets-functions-relations/size-of-sets/size-of-sets-complete.pdf
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 3, Theorem 3.1, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/03-cardinal_numbers.pdf

## Intuition

> [!intuition] Why
> No set can list all of its subsets. The diagonal argument behind it is the same idea as Russell's paradox, the undecidability of the halting problem and the hierarchy theorems of complexity.

## Definition

> [!theorem] Cantor's Theorem — a set is strictly smaller than its power set
> ### Scope
> - $A$: a set, and $\mathcal P(A)$ its [[knowledge/math/set theory/special set/Power Set\|Power Set]].
>
> ---
> ### Condition
> - None; $A = \emptyset$ is included.
>
> ---
> ### Property
> There is no surjection $g : A \to \mathcal P(A)$.
> There is no injection $f : \mathcal P(A) \to A$.
> $|A| < |\mathcal P(A)|$.
>
> `[Mun00 Thm 7.8]` for the first two; `[OLP-Siz Thm siz.24]` and `[Jec03 Thm 3.1]` for the third.

## Property

> [!proof] Why — the diagonal set
> Given $g : A \to \mathcal P(A)$, let $B = \{a \in A : a \notin g(a)\}$. If $B = g(a_0)$, then $a_0 \in B \iff a_0 \notin g(a_0) = B$, a contradiction; so $B$ is not in the image of $g$. An injection $f : \mathcal P(A) \to A$ would give a surjection $A \to \mathcal P(A)$, sending $f(S)$ to $S$ and everything else to $\emptyset$. Finally $a \mapsto \{a\}$ is an injection, so $|A| \leq |\mathcal P(A)|$.

> [!remark] The shape of Russell's paradox
> $B$ is Russell's set $\{x : x \notin x\}$ cut down to $A$ and read through $g$. With "the set of all sets" for $A$ and $g(a) = a$, the argument becomes [[knowledge/math/set theory/Axiom of Set Theory#Russell's Paradox\|Russell's paradox]].

## Example

> [!example] Consequences
> - $\mathcal P(\mathbb Z_{>0})$ and $\{0, 1\}^\omega$ are uncountable ([[knowledge/math/set theory/cardinality/Countable Set#Uncountable sets\|Countable Set#Uncountable sets]]).
> - There is no largest cardinality: $|A| < |\mathcal P(A)| < |\mathcal P(\mathcal P(A))| < \cdots$.
> - For $A = \emptyset$: $\mathcal P(\emptyset) = \{\emptyset\}$ has one element, and $0 < 1$.

## Related

### Siblings
- [[knowledge/math/set theory/cardinality/Countable Set#Uncountable sets\|Countable Set#Uncountable sets]] — the diagonal argument for $\{0, 1\}^\omega$, which is the case $A = \mathbb Z_{>0}$

### Prerequisites
- [[knowledge/math/set theory/cardinality/Cardinality\|Cardinality]], [[knowledge/math/set theory/special set/Power Set\|Power Set]]
