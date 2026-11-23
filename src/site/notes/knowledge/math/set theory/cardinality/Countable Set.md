---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/cardinality/countable-set/","dg-note-properties":{"aliases":["Countable","Countably Infinite","Uncountable Set","Uncountable","Enumerable Set"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §7: definitions, Theorem 7.1, Lemma 7.2, Corollaries 7.3, 7.4, Theorems 7.5–7.7; Exercises 1, 3, 4, 8.
- `[OLP-Siz]` — Open Logic Project, _Sets, Functions, Relations_, chapter "The Size of Sets", revision 9620cc7 (2026-07-12), Definitions siz.3, siz.4, Corollary siz.9, Proposition siz.12 and §siz.4 (pairing function), Theorems siz.17, siz.18, Problems siz.3, siz.14: https://builds.openlogicproject.org/content/sets-functions-relations/size-of-sets/size-of-sets-complete.pdf
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 3: countable sets, Exercise 3.3, the remark on countable unions without choice, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/03-cardinal_numbers.pdf

## Intuition

> [!intuition] Why
> Countable sets are the infinite sets that can be listed one element at a time. They mark the edge of what algorithms can enumerate: there are countably many programs, but uncountably many sets of integers.

## Definition

> [!definition] Countable Set
> A set $A$ is **countably infinite** iff there is a [[knowledge/math/property/map/Bijection\|Bijection]] $A \to \mathbb Z_{>0}$, and **countable** iff it is [[knowledge/math/set theory/cardinality/Finite Set\|finite]] or countably infinite. A set that is not countable is **uncountable**. `[Mun00 §7]`

> [!remark] Three conventions
> | source | word | finite sets included? |
> | --- | --- | --- |
> | `[Mun00 §7]` | countable | yes |
> | `[OLP-Siz Def siz.4]` | enumerable: empty, or the image of a surjection $\mathbb Z_{>0} \to A$ (an *enumeration*, Def siz.3) | yes |
> | `[Jec03 Ch 3]` | countable: of cardinality $\aleph_0$ | no: it means countably infinite |

## Property

> [!theorem] Countable via maps — a surjection from or an injection into $\mathbb Z_{>0}$
> **Scope**
> - $B$ a nonempty set.
>
> ---
> **Property**
> The following are equivalent:
> - $B$ is countable;
> - there is a surjection $\mathbb Z_{>0} \to B$;
> - there is an injection $B \to \mathbb Z_{>0}$.
>
> `[Mun00 Thm 7.1]`; `[OLP-Siz Cor siz.9]` for the surjection form.

> [!lemma] Infinite subsets of $\mathbb Z_{>0}$ — countably infinite
> **Scope**
> - $C \subseteq \mathbb Z_{>0}$ infinite.
>
> ---
> **Property**
> $C$ is countably infinite.
>
> `[Mun00 Lemma 7.2]`: list $C$ in increasing order with the recursion of [[knowledge/math/set theory/order/Principle of Recursive Definition#Example\|Principle of Recursive Definition#Example]].

> [!corollary] Subsets and pairs
> **Scope**
> - $A$ countable, $B \subseteq A$.
>
> ---
> **Property**
> $B$ is countable `[Mun00 Cor 7.3]` `[OLP-Siz Problem siz.3]`.
> $\mathbb Z_{>0} \times \mathbb Z_{>0}$ is countably infinite `[Mun00 Cor 7.4]`.
>
> Explicit bijections $\mathbb N \times \mathbb N \to \mathbb N$, with $0 \in \mathbb N$: Cantor's pairing function $g(n, m) = \tfrac{(n + m + 1)(n + m)}{2} + n$ `[OLP-Siz Prop siz.12, §siz.4]`, and $(m, n) \mapsto 2^m (2n + 1) - 1$ `[Jec03 Ex 3.3]`.

> [!theorem] Countable unions — countable, with choice
> **Scope**
> - $A_n$ ($n \in \mathbb Z_{>0}$) countable sets.
>
> ---
> **Property**
> $\bigcup_{n} A_n$ is countable.
>
> `[Mun00 Thm 7.5]`, `[OLP-Siz Problem siz.14]`. The proof fixes a surjection $\mathbb Z_{>0} \to A_n$ for every $n$ at once, which is a countable use of the [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]]. Without choice it is not even provable that $\omega_1$ is not a countable union of countable sets `[Jec03 Ch 3]`.

> [!theorem] Finite products — countable
> **Scope**
> - $A_1, \dots, A_n$ countable sets.
>
> ---
> **Property**
> $A_1 \times \cdots \times A_n$ is countable.
>
> `[Mun00 Thm 7.6]`

### Uncountable sets

> [!theorem] Binary sequences — uncountable
> **Scope**
> - $X = \{0, 1\}$, and $X^\omega$ the set of sequences $(x_1, x_2, \dots)$ in $X$ ([[knowledge/math/set theory/Set Operation#Indexed families and products\|Set Operation#Indexed families and products]]).
>
> ---
> **Property**
> $X^\omega$ is uncountable.
>
> `[Mun00 Thm 7.7]`, `[OLP-Siz Thm siz.17]`. For any $g : \mathbb Z_{>0} \to X^\omega$, the sequence whose $n$-th term is $1 - g(n)_n$ differs from every $g(n)$ in place $n$; this is Cantor's **diagonal argument**, and it shows that no $g$ is surjective.

> [!corollary] Power set of $\mathbb Z_{>0}$
> **Scope**
> - $\mathcal P(\mathbb Z_{>0})$.
>
> ---
> **Property**
> $\mathcal P(\mathbb Z_{>0})$ is in bijection with $\{0, 1\}^\omega$, by indicator sequences `[Mun00 §7 Ex 3]`.
> $\mathcal P(\mathbb Z_{>0})$ is uncountable `[OLP-Siz Thm siz.18]`.
>
> [[knowledge/math/set theory/cardinality/Cantor's Theorem\|Cantor's Theorem]] does the same for every set.

## Example

> [!example] Countable and uncountable sets of numbers
> - $\mathbb Z$ and $\mathbb Q$ are countably infinite `[Mun00 §7 Ex 1]`.
> - The real algebraic numbers are countable: there are countably many polynomials with rational coefficients, each with finitely many roots `[Mun00 §7 Ex 4a]`.
> - $\mathbb R$ is uncountable, since $|\mathbb R| = |\mathcal P(\mathbb Z_{>0})|$ ([[knowledge/math/set theory/cardinality/Cardinality#The continuum\|Cardinality#The continuum]]); so the transcendental numbers are uncountable `[Mun00 §7 Ex 4b]`.
> - The set of countable subsets of $\{0, 1\}^\omega$ has the same cardinality as $\{0, 1\}^\omega$ `[Mun00 §7 Ex 8]`.

## Related

### Properties
- [[knowledge/math/set theory/cardinality/Cantor's Theorem\|Cantor's Theorem]] — no set maps onto its power set

### Siblings
- [[knowledge/math/set theory/cardinality/Finite Set\|Finite Set]], [[knowledge/math/set theory/cardinality/Infinite Set\|Infinite Set]]

### Prerequisites
- [[knowledge/math/set theory/cardinality/Cardinality\|Cardinality]]
