---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/set-operation/","dg-note-properties":{}}
---

	Reference:
- [[academic/Book Reference\|Algebra: Chapter 0]] - Chapter I: Preliminaries: Set theory and categories, Section 1.3: Operations between sets; Section 1.4: Disjoint unions, products.

## Definition

### Cartesian Product

> [!definition] Cartesian Product
> The **Cartesian Product** of sets $A$ and $B$, written $A \times B$, is the set of **ordered** pairs
> $$A \times B = \{(x, y) \mid x \in A \text{ and } y \in B\}.$$
> The $n$-fold product $A_1 \times \cdots \times A_n$ consists of $n$-tuples; $A^n$ abbreviates the $n$-fold product of $A$ with itself.

> [!remark] Why this definition carries the vault
> Every Scope line in `property/` is written over a product: a [[knowledge/math/set theory/relation/Relation\|Relation]] is a subset of $A \times B$, a [[knowledge/math/set theory/Function\|function]] is a special relation, a [[knowledge/math/set theory/operation/Binary Operation\|Binary Operation]] is a function $S \times S \to S$. Ordered pairs are taken as primitive here; the set-theoretic construction $(x,y) := \{\{x\},\{x,y\}\}$ is a foundational detail, noted in [[knowledge/math/Foundations of Mathematics\|Foundations of Mathematics]] and used nowhere else.

### Disjoint Union

> [!definition] Disjoint Union
> The **disjoint union** of set $S$ and set $T$ denoted as $S \amalg T$ is the set consisting of union for element with tag about its original set.

### Symmetric Difference

> [!definition] Symmetric Difference
> The **symmetric difference** of set $S$ and set $T$ denoted as $S \Delta T$ is the set consisting of all elements that only in $S$ or only in $T$.

### Partition

> [!definition] Partition
> A collection of nonempty sets $A_1, A_2, \cdots$ is a **partition** of a set $A$ if they are disjoint and their union is $A$.


## Notation

### Inclusion

| Symbol                | Operation          |
| --------------------- | ------------------ |
| $\in$                 | Belongs to         |
| $\subset, \subsetneq$ | Proper Subset      |
| $\subseteq$           | Subset             |
| $=$                   | Equal              |
| $\lvert s \rvert$     | Number of Elements |
| $2^S$                 | Power Set          |

### Operations

| Symbol      | Operation            |
| ----------- | -------------------- |
| $\cup$      | Union                |
| $\cap$      | Intersection         |
| $\setminus$ | Difference           |
| $\amalg$    | Disjoint Union       |
| $\Delta$    | Symmetric Difference |
| $\times$    | Cartesian Product    |
### Famous Sets

| Notation    | Meaning                     |
| ----------- | --------------------------- |
| $\emptyset$ | Empty set                   |
| $\mathbb N$ | Set of **natural numbers**  |
| $\mathbb Z$ | Set of **integers**         |
| $\mathbb Q$ | Set of **rational numbers** |
| $\mathbb R$ | Set of **real numbers**     |
| $\mathbb C$ | Set of **complex numbers**  |

### Common Law

| Property        | Description                                                                                                                                                                                                                                  |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|                 | $A \cup A = A$, $A \cap A = A$                                                                                                                                                                                                               |
|                 | $A \subseteq A \cup B$, $A \cap B \subseteq A$                                                                                                                                                                                               |
|                 | $A \cup \emptyset = A$, $A \cap \emptyset = \emptyset$                                                                                                                                                                                       |
|                 | $A \cup (A \cap B) = A$, $A \cap (A \cup B) = A$                                                                                                                                                                                             |
|                 | $A \subseteq C$, $B \subseteq C$, then $A \cup B \subseteq C$                                                                                                                                                                                |
|                 | $C \subseteq A$, $C \subseteq B$, then $C \subseteq A \cap B$                                                                                                                                                                                |
|                 | $A \subset B$, $B \subset C$, then $A \subset C$                                                                                                                                                                                             |
|                 | $A \subseteq B$, $B \subseteq C$, then $A \subseteq C$                                                                                                                                                                                       |
|                 | $A \subset B$, $B \subseteq C$, then $A \subset C$                                                                                                                                                                                           |
|                 | $A - (B \cap C) = (A - B) \cup (A - C)$                                                                                                                                                                                                      |
|                 | $A - (B - C) = (A - B) \cup (A \cap C)$                                                                                                                                                                                                      |
|                 | $A - (B \cup C) = (A - B) - C$                                                                                                                                                                                                               |
