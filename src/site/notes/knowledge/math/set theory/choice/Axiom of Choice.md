---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/choice/axiom-of-choice/","dg-note-properties":{"aliases":["AC","Choice Axiom","Choice Function"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1: §9: axiom of choice, Lemma 9.2, Exercise 5; §10, Exercise 5; §11, Exercises 5–7; Supplementary Exercises 6, 7 (Well-Ordering); Chapter 2, §19, Exercise 9.
- `[Dob18]` — E.-E. Doberkat, _Sets, the Axiom of Choice, and All That: A Tutorial_, 2018, §1.1, Proposition 1.17, Theorem 1.40, Theorem 1.45: https://arxiv.org/pdf/1408.6475
- `[Nor12]` — D. Normann, _The Axiom of Choice, the Well Ordering Principle and Zorn's Lemma_, note for MAT4640, University of Oslo, 2012, Theorems 4, 5, 10: https://www.uio.no/studier/emner/matnat/math/MAT4640/v14/acwozl.pdf
- `[Ros88]` — K. A. Ross, _Informal Introduction to Set Theory_, lecture notes, University of Oregon, 1988, the section on the axiom of choice and its equivalents (unnumbered): https://people.iith.ac.in/rajeshkannan/ra2021/axiomofchoice.pdf
- `[Jec03]` — T. Jech, _Set Theory_, 3rd millennium ed., Springer, 2003, Chapter 3, the remark on countable unions without choice, read in the course copy: https://fa.ewi.tudelft.nl/~hart/onderwijs/set_theory/Jech/03-cardinal_numbers.pdf

## Intuition

> [!intuition] Why
> Choosing one element from each of infinitely many sets, with no rule to do it, cannot be proved possible from the other axioms. Choice asserts that it is, and with it come a well-ordering of every set, Zorn's lemma, a basis of every vector space and maximal ideals in every ring.

## Definition

> [!definition] Axiom of Choice
> Given a collection $\mathcal A$ of disjoint nonempty sets, there is a set $C$ consisting of exactly one element from each element of $\mathcal A$:
> - $C \subseteq \bigcup \mathcal A$;
> - for each $A \in \mathcal A$, $C \cap A$ has exactly one element.
>
> `[Mun00 §9]`

> [!definition] Choice Function
> For a collection $\mathcal B$ of nonempty sets, not necessarily disjoint, a **choice function** is a function $c : \mathcal B \to \bigcup \mathcal B$ with $c(B) \in B$ for each $B \in \mathcal B$ `[Mun00 Lemma 9.2]`.

> [!remark] The same axiom in other words
> - **Choice functions exist** for every collection of nonempty sets. `[Mun00 Lemma 9.2]` derives this from the axiom; `[Dob18 §1.1]` and `[Nor12]` take it as the axiom.
> - **Products are nonempty**: $\prod_{\lambda \in \Lambda} A_\lambda \neq \emptyset$ whenever every $A_\lambda \neq \emptyset$ `[Ros88]`; `[Mun00 §19 Ex 9]` asks for the proof of this equivalence ([[knowledge/math/set theory/Set Operation#Indexed families and products\|Set Operation#Indexed families and products]]). An element of the product is exactly one choice $a_\lambda \in A_\lambda$ for each $\lambda$.

## Property

Choice is equivalent to several ordering and maximality principles, and several basic results use it without saying so.

### Equivalents

> [!theorem] Equivalents of Choice — five statements of one strength
> **Scope**
> - Set theory without choice (ZF).
>
> ---
> **Property**
> The following are equivalent:
> - the Axiom of Choice;
> - the [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]]: every set has a well-ordering;
> - [[knowledge/math/set theory/choice/Zorn's Lemma\|Zorn's Lemma]];
> - the [[knowledge/math/set theory/choice/Hausdorff Maximum Principle\|Hausdorff Maximum Principle]];
> - [[knowledge/math/set theory/choice/Zorn's Lemma#Tukey's lemma\|Tukey's lemma]].
>
> `[Dob18 Thm 1.45]` (choice, well-ordering, Zorn, Tukey); `[Ros88]` (all five); `[Nor12 Thms 4, 5, 10]` (choice, well-ordering, Zorn).

> [!remark] Munkres's route through the exercises
> | implication | where |
> | --- | --- |
> | well-ordering theorem ⇒ AC | `[Mun00 §10 Ex 5]` |
> | maximum principle ⇒ Zorn | `[Mun00 §11]`, in the text |
> | Zorn ⇒ Kuratowski ⇒ Tukey ⇒ maximum principle | `[Mun00 §11 Ex 5, 6, 7]` |
> | maximum principle ⇔ well-ordering theorem | `[Mun00 Supp Ex 6]` |
> | AC ⇔ well-ordering theorem | `[Mun00 Supp Ex 7]` |

### Where choice is used

> [!example] Uses in this vault
> - **Right inverses.** A surjection $f : A \to B$ has a right inverse $h$: choose $h(b) \in f^{-1}(b)$ `[Mun00 §9 Ex 5a]` ([[knowledge/math/set theory/Function#Inverse\|Function#Inverse]]). A left inverse of an injection needs only one element of $A$, no axiom `[Mun00 §9 Ex 5b]`.
> - **Infinite sets** contain a copy of $\mathbb Z_{>0}$ ([[knowledge/math/set theory/cardinality/Infinite Set#Property\|Infinite Set#Property]]).
> - **Countable unions** of countable sets are countable ([[knowledge/math/set theory/cardinality/Countable Set#Property\|Countable Set#Property]]); without choice this is not provable `[Jec03 Ch 3]`.
> - **Cardinals are comparable** ([[knowledge/math/set theory/cardinality/Cardinality#Comparability of cardinals\|Cardinality#Comparability of cardinals]]), through the well-ordering theorem.
> - **Maximal ideals and bases** exist, through Zorn's lemma ([[knowledge/math/Foundations of Mathematics\|Foundations of Mathematics]]).

> [!example] Where no choice is needed
> - A finite collection of nonempty sets has a choice function, by induction on its size.
> - Nonempty subsets of $\mathbb Z_{>0}$ have a canonical choice, the smallest element. In general, a well-ordering of $\bigcup \mathcal B$ gives a choice function, which is the proof that the well-ordering theorem implies choice `[Mun00 §10 Ex 5]` `[Dob18 Prop 1.17]`.

## Related

### Properties
- [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]], [[knowledge/math/set theory/choice/Zorn's Lemma\|Zorn's Lemma]], [[knowledge/math/set theory/choice/Hausdorff Maximum Principle\|Hausdorff Maximum Principle]] — its equivalents

### Siblings
- [[knowledge/math/set theory/Axiom of Set Theory\|Axiom of Set Theory]] — the ZF axioms; choice is the C of ZFC
