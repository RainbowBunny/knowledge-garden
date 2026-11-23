---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/relation/relation/","dg-note-properties":{}}
---

Reference:
- `[OLP-Rel]` — Open Logic Project, _Sets, Functions, Relations_, chapter "Relations", revision 9620cc7 (2026-07-12), Definitions rel.1, rel.38: https://builds.openlogicproject.org/content/sets-functions-relations/relations/relations-complete.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §3: relation on a set; Exercises 2, 7, 14.

## Definition

> [!definition] Relation
> A **(binary) relation** from a [[knowledge/math/set theory/Set\|Set]] $A$ to a set $B$ is a subset
> $$R \subseteq A \times B$$
> of the [[knowledge/math/set theory/Set Operation#Cartesian Product\|cartesian product]].
> When $(a, b) \in R$ we say that $a$ and $b$ are 'related by $R$' and write
> $$a \; R \; b.$$
>
> `[OLP-Rel Def rel.1]` and `[Mun00 §3]` state the case $A = B$ below.

> [!definition] Homogeneous Relation
> A relation on a single set $S$ is the case $A = B = S$, i.e. $R \subseteq S \times S$ `[Mun00 §3]` `[OLP-Rel Def rel.1]`. These are the relations the [[knowledge/math/property/Math Properties MOC\|Relation Axioms]] apply to — [[knowledge/math/property/relation/Reflexivity\|Reflexivity]], [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]], [[knowledge/math/property/relation/Symmetry\|Symmetry]], [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]], [[knowledge/math/property/relation/Asymmetry\|Asymmetry]], [[knowledge/math/property/relation/Transitivity\|Transitivity]], [[knowledge/math/property/relation/Comparability\|Comparability]], [[knowledge/math/property/relation/Connexity\|Connexity]] all compare two elements of the *same* set.

> [!remark]
> As the relation $R$ is subset, they also import the [[knowledge/math/set theory/Set Operation\|Set Operation]].

### Associated Sets

> [!definition] Domain
> $$\mathsf{dom}(R) = \{a \in A \mid \exists b: a \; R \; b\}$$

> [!definition] Range
> $$\mathsf{ran}(R) = \{b \in B \mid \exists a: a \; R \; b\}$$

## Variant

New relations made from old ones.

### Converse

> [!definition] Converse Relation
> $R^{-1} \subseteq B \times A$ is defined by $b \; R^{-1} a \iff a \; R \; b$ `[OLP-Rel Def rel.38]`. `[Mun00 §3 Ex 14]` calls it the reverse relation.

### Restriction

> [!definition] Restriction of a Relation
> For $R \subseteq A \times A$ and $A_0 \subseteq A$, the **restriction** of $R$ to $A_0$ is
> $$R \cap (A_0 \times A_0).$$
> `[Mun00 §3 Ex 2]`; `[OLP-Rel Def rel.38]` writes $R \restriction A_0$.

> [!remark] Universal axioms survive restriction
> Each of [[knowledge/math/property/relation/Reflexivity\|Reflexivity]], [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]], [[knowledge/math/property/relation/Symmetry\|Symmetry]], [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]], [[knowledge/math/property/relation/Transitivity\|Transitivity]], [[knowledge/math/property/relation/Comparability\|Comparability]] says "for all elements …", so it still holds on $A_0$. Hence restrictions of [[knowledge/math/set theory/relation/Equivalence Relation\|equivalence relations]] and of [[knowledge/math/set theory/order/Strict Total Order\|order relations]] are again such relations `[Mun00 §3 Ex 2, Ex 7]`. A property with an existential clause, such as the [[knowledge/math/property/relation/Least Upper Bound Property\|Least Upper Bound Property]], need not survive: $\mathbb Q \subseteq \mathbb R$.

### Composition

> [!definition] Composition of Relations
> For relation $R \subseteq A \times B$ and $S \subseteq B \times C$:
> $$S \circ R = \{(a, c) \mid \exists b \in B: a \; R \; b \text{ and } b \; S \; c\} \subseteq A \times C.$$

> [!remark]
> Composition of [[knowledge/math/set theory/Function\|functions]] is this operation restricted to functional relations. It is [[knowledge/math/property/operation/Associativity\|associative]], and the identity relation $\{(a,a)\}$ is its [[knowledge/math/property/operation/Identity Element\|identity]] — so relations on $S$ form a [[knowledge/math/algebra/structures/Monoid\|Monoid]] under $\circ$.

## Property

### Left Total

> [!definition] Left Total
> A relation $R$ is **left total** if every $a \in A$ is related to at least one $b \in B$ that $a \; R \; b$.

### Right Total

> [!definition] Right Total
> A relation $R$ is **right total** if every $b \in B$ is related to at least one $a \in A$ that $a \; R \; b$.

### Functional

> [!definition] Functional
> A relation $R$ is **functional** (right-unique, single valued) if each $a$ is related to at most one $b$. 

## Specialisation

| add | get |
| --- | --- |
| [[knowledge/math/property/relation/Reflexivity\|Reflexivity]] + [[knowledge/math/property/relation/Transitivity\|Transitivity]] | [[knowledge/math/set theory/order/Preorder\|Preorder]] |
| + [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]] | [[knowledge/math/set theory/order/Partial Order\|Partial Order]] |
| + [[knowledge/math/property/relation/Comparability\|Comparability]] (equivalently [[knowledge/math/property/relation/Connexity\|Connexity]]) | [[knowledge/math/set theory/order/Total Order\|Total Order]] |
| [[knowledge/math/property/relation/Irreflexivity\|Irreflexivity]] + [[knowledge/math/property/relation/Transitivity\|Transitivity]] | [[knowledge/math/set theory/order/Strict Partial Order\|Strict Partial Order]] |
| + [[knowledge/math/property/relation/Comparability\|Comparability]] | [[knowledge/math/set theory/order/Strict Total Order\|Strict Total Order]] |
| + every nonempty subset has a least element | [[knowledge/math/set theory/order/Well-Ordered Set\|Well-Ordered Set]] |
| [[knowledge/math/property/relation/Reflexivity\|Reflexivity]] + [[knowledge/math/property/relation/Symmetry\|Symmetry]] + [[knowledge/math/property/relation/Transitivity\|Transitivity]] | [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] |
| left-total + functional | [[knowledge/math/set theory/Function\|Function]] |
