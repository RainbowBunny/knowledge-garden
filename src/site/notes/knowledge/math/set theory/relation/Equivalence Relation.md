---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/relation/equivalence-relation/","dg-note-properties":{}}
---

Reference:
- `[Alu09]` — P. Aluffi, _Algebra: Chapter 0_, Graduate Studies in Mathematics 104, American Mathematical Society, 2009, Chapter I: Preliminaries: Set theory and categories, Section 1.5: Equivalence relations, partitions, quotients.
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3: equivalence relation, equivalence class, Lemma 3.1, partitions; Exercises 2, 3, 5(b).
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definitions rel.10, rel.11, Proposition rel.12: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf

## Intuition

> [!intuition] Why
> Equivalence relations formalize being the same for the purpose at hand: congruence mod $n$, isomorphism, having the same image under a map. Passing to classes is how quotients such as $\mathbb Z/n\mathbb Z$ are built.

## Definition

> [!definition] Equivalence Relation
> A [[knowledge/math/set theory/relation/Relation#Definition\|Relation]] $\sim$ on a set $S$ is an equivalence relation iff it satisfies
> - [[knowledge/math/property/relation/Reflexivity\|Reflexivity]];
> - [[knowledge/math/property/relation/Symmetry\|Symmetry]];
> - [[knowledge/math/property/relation/Transitivity\|Transitivity]].
>
> `[Mun00 §3]`, `[OLP-Rel Def rel.10]`

### Equivalence Class 

> [!definition] Equivalence Class
> For every element $a \in S$, the **equivalence class** of $a$ (w.r.t. $\sim$) is the subset of $S$ defined by
> $$[a]_\sim = \{b \in S \; | \; b \sim a\}$$
> `[Mun00 §3]`, `[OLP-Rel Def rel.11]`. The set of classes is the [[knowledge/math/set theory/relation/Quotient Relation\|quotient]] $S/{\sim}$.

## Property

> [!proposition] Same class iff related
> **Scope**
> - $\sim$ an equivalence relation on $S$; $a, b \in S$.
>
> ---
> **Property**
> $a \sim b \iff [a]_\sim = [b]_\sim$.
>
> `[OLP-Rel Prop rel.12]`

> [!lemma] Disjoint or equal — two classes never partly overlap
> **Scope**
> - $E$, $E'$ equivalence classes of $\sim$.
>
> ---
> **Property**
> $E \cap E' = \emptyset$ or $E = E'$.
>
> `[Mun00 Lemma 3.1]`. If $c \in E \cap E'$ with $E = [a]$ and $E' = [a']$, then $c \sim a$ and $c \sim a'$, so $a \sim a'$ and $E = E'$ by the proposition above.

> [!theorem] Partitions — the same data as equivalence relations
> **Scope**
> - $S$: a set.
>
> ---
> **Property**
> The equivalence classes of an equivalence relation on $S$ form a [[knowledge/math/set theory/Set Operation#Partition\|partition]] of $S$.
> Every partition $\mathcal D$ of $S$ is the set of classes of exactly one equivalence relation: $a \sim b$ iff $a$ and $b$ lie in the same member of $\mathcal D$.
>
> `[Mun00 §3]`; Aluffi, Chapter I, Section 1.5.

> [!proposition] Restriction and intersection
> **Scope**
> - $\sim$ and $\sim_i$ ($i \in I$, $I \neq \emptyset$) equivalence relations on $S$; $S_0 \subseteq S$.
>
> ---
> **Property**
> The [[knowledge/math/set theory/relation/Relation#Restriction\|restriction]] $\sim \cap\, (S_0 \times S_0)$ is an equivalence relation on $S_0$ `[Mun00 §3 Ex 2]`.
> $\bigcap_{i \in I} \sim_i$ is an equivalence relation on $S$ `[Mun00 §3 Ex 5b]`.

## Example

> [!example] Symmetric and transitive is not enough
> If $\sim$ is symmetric and transitive and $a \sim b$ for some $b$, then $b \sim a$, so $a \sim a$. Reflexivity can still fail at an element related to nothing: the empty relation on a nonempty set is symmetric and transitive but not reflexive. This is the gap in the "proof" that `[Mun00 §3 Ex 3]` asks the reader to find.

> [!example] Fibres of a map
> For $f : S \to T$, $a \sim b \iff f(a) = f(b)$ is an equivalence relation, and its classes are the nonempty fibres $f^{-1}(t)$ ([[knowledge/math/set theory/function/Kernel\|Kernel]]).

## Related

### Constructions
- [[knowledge/math/set theory/relation/Quotient Relation\|Quotient Relation]] — the set of classes

### Siblings
- [[knowledge/math/set theory/order/Partial Order\|Partial Order]] — [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]] in place of [[knowledge/math/property/relation/Symmetry\|Symmetry]]
