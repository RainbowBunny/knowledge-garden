---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/choice/zorn-s-lemma/","dg-note-properties":{"aliases":["Zorn Lemma","Kuratowski's Lemma","Tukey's Lemma","Finite Type","Finite Character"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §11: Zorn's lemma, upper bound, maximal element, the proof from the maximum principle; Exercises 5, 6, 7.
- `[Dob18]` — E.-E. Doberkat, _Sets, the Axiom of Choice, and All That: A Tutorial_, 2018, §1.5 (finite character), Theorem 1.45 (ZL, MP): https://arxiv.org/pdf/1408.6475
- `[Ros88]` — K. A. Ross, _Informal Introduction to Set Theory_, lecture notes, University of Oregon, 1988, Zorn's lemma and Tukey's lemma (unnumbered): https://people.iith.ac.in/rajeshkannan/ra2021/axiomofchoice.pdf
- `[Nor12]` — D. Normann, _The Axiom of Choice, the Well Ordering Principle and Zorn's Lemma_, note for MAT4640, University of Oslo, 2012, ZORN, Theorems 4, 5: https://www.uio.no/studier/emner/matnat/math/MAT4640/v14/acwozl.pdf

## Intuition

> [!intuition] Why
> Zorn's lemma is the form of choice used in practice. To obtain a maximal object, such as a basis or a maximal ideal, it is enough to check that every chain of such objects has an upper bound.

## Definition

> [!theorem] Zorn's Lemma — chains bounded above force a maximal element
> ### Scope
> - $(A, \prec)$: a set with a [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]].
>
> ---
> ### Condition
> - Every chain (simply ordered subset) of $A$ has an upper bound in $A$ ([[knowledge/math/set theory/order/Strict Partial Order#Upper bounds and maximal elements\|Strict Partial Order#Upper bounds and maximal elements]]).
>
> ---
> ### Property
> $A$ has a maximal element: some $m \in A$ with no $a \in A$ satisfying $m \prec a$.
>
> `[Mun00 §11]`. `[Dob18 Thm 1.45 (ZL)]` states it for non-strict orders and `[Nor12]` for strict ones, with the same content. It is equivalent to the [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]].

> [!remark] The empty chain
> The empty set is a chain, so the condition already forces $A \neq \emptyset$. `[Ros88]` instead assumes $A \neq \emptyset$ and asks for upper bounds of nonempty chains only.

## Property

> [!proof] From the maximum principle `[Mun00 §11]`
> By the [[knowledge/math/set theory/choice/Hausdorff Maximum Principle\|Hausdorff Maximum Principle]] there is a maximal chain $B$; let $c$ be an upper bound of $B$. If $c \prec d$ for some $d$, then $d \notin B$, since every element of $B$ is $\preceq c \prec d$, and $B \cup \{d\}$ is a chain properly containing $B$, against maximality. So $c$ is maximal.

### Kuratowski's lemma

> [!corollary] Kuratowski's Lemma — union-closed families have maximal members
> **Scope**
> - $\mathcal A$: a collection of sets such that for every subcollection $\mathcal B \subseteq \mathcal A$ simply ordered by proper inclusion, $\bigcup \mathcal B \in \mathcal A$.
>
> ---
> **Property**
> $\mathcal A$ has an element properly contained in no other element of $\mathcal A$.
>
> `[Mun00 §11 Ex 5]`: apply Zorn's lemma to $(\mathcal A, \subsetneq)$, where $\bigcup \mathcal B$ is an upper bound of the chain $\mathcal B$.

### Tukey's lemma

> [!corollary] Tukey's Lemma — families of finite type have maximal members
> **Scope**
> - $X$: a set.
> - $\mathcal A$: a nonempty collection of subsets of $X$ **of finite type** (finite character): $B \subseteq X$ belongs to $\mathcal A$ iff every finite subset of $B$ belongs to $\mathcal A$.
>
> ---
> **Property**
> $\mathcal A$ has an element properly contained in no other element of $\mathcal A$.
>
> `[Mun00 §11 Ex 6]`, `[Ros88]`; `[Dob18 Thm 1.45]` calls it Tukey's maximality principle (MP) and defines finite character in §1.5. Munkres derives it from Kuratowski's lemma: a finite subset of the union of a chain in $\mathcal A$ lies in one member of the chain, so the union is in $\mathcal A$.

> [!warning] Nonempty is needed
> The empty collection is of finite type: no $B$ belongs to it, and no $B$ has all its finite subsets in it, since $\emptyset$ is not. It has no element at all, so the conclusion fails. `[Ros88]` assumes $\mathcal A \neq \emptyset$; the statement in `[Mun00 §11 Ex 6]` omits it. A nonempty collection of finite type contains $\emptyset$, and then the empty chain has its union in $\mathcal A$.

## Example

> [!example] Typical applications
> - **Bases.** The linearly independent subsets of a vector space form a nonempty family of finite type, because independence is a condition on finite subsets. A maximal member, given by Tukey's lemma, is a basis.
> - **Maximal chains.** The chains of a strictly partially ordered set form a family of finite type, which gives the [[knowledge/math/set theory/choice/Hausdorff Maximum Principle\|Hausdorff Maximum Principle]] `[Mun00 §11 Ex 7]`.

> [!example] When a chain is unbounded
> $(\mathbb Z_{>0}, <)$ has no maximal element, and the chain $\mathbb Z_{>0}$ has no upper bound: the condition is what fails.

## Related

### Siblings
- [[knowledge/math/set theory/choice/Hausdorff Maximum Principle\|Hausdorff Maximum Principle]] — a maximal chain rather than a maximal element
- [[knowledge/math/set theory/choice/Well-Ordering Theorem\|Well-Ordering Theorem]], [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]]
