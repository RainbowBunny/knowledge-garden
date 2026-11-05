---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/relation/relation/","dg-note-properties":{}}
---

Reference:
- https://en.wikipedia.org/wiki/Binary_relation

## Definition

> [!definition] Relation
> A **(binary) relation** from a [[knowledge/math/set theory/Set\|Set]] $A$ to a set $B$ is a subset
> $$R \subseteq A \times B.$$ 
> When $(a, b) \in R$ we say that $a$ and $b$ are 'related by $R$' and write
> $$a \; R \; b.$$

> [!definition] Homogeneous Relation
> A relation on a single set $S$ is the case $A = B = S$, i.e. $R \subseteq S \times S$. These are the relations the [[knowledge/math/property/Math Properties MOC\|Relation Axioms]] apply to — [[knowledge/math/property/relation/Reflexivity\|Reflexivity]], [[knowledge/math/property/relation/Symmetry\|Symmetry]], [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]], [[knowledge/math/property/relation/Transitivity\|Transitivity]], [[knowledge/math/property/relation/Connexity\|Connexity]] all compare two elements of the *same* set.

> [!remark]
> As the relation $R$ is subset, they also import the [[knowledge/math/set theory/Set Operation\|Set Operation]].

### Associated Sets

> [!definition] Domain
> $$\mathsf{dom}(R) = \{a \in A \mid \exists b: a \; R \; b\}$$

> [!definition] Range
> $$\mathsf{ran}(R) = \{b \in B \mid \exists a: a \; R \; b\}$$

## Variant

### Converse

> [!definition] Converse Relation
> $R^{-1} \subseteq B \times A$ is defined by $b \; R^{-1} a \iff a \; R \; b$.

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
| [[knowledge/math/property/relation/Reflexivity\|Reflexivity]] + [[knowledge/math/property/relation/Transitivity\|Transitivity]] | [[knowledge/math/set theory/relation/Preorder\|Preorder]] |
| + [[knowledge/math/property/relation/Antisymmetry\|Antisymmetry]] | [[knowledge/math/set theory/relation/Partial Order\|Partial Order]] |
| + [[knowledge/math/property/relation/Connexity\|Connexity]] | [[knowledge/math/set theory/relation/Total Order\|Total Order]] |
| [[knowledge/math/property/relation/Reflexivity\|Reflexivity]] + [[knowledge/math/property/relation/Symmetry\|Symmetry]] + [[knowledge/math/property/relation/Transitivity\|Transitivity]] | [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] |
| left-total + functional | [[knowledge/math/set theory/Function\|Function]] |