---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/set-operation/","dg-note-properties":{}}
---

Reference:
- `[Alu09]` — P. Aluffi, _Algebra: Chapter 0_, Graduate Studies in Mathematics 104, American Mathematical Society, 2009, Chapter I: Preliminaries: Set theory and categories, Section 1.3: Operations between sets; Section 1.4: Disjoint unions, products.
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 1, §5: indexed families, $m$-tuples, $\omega$-tuples; Exercise 1.
- `[Ros88]` — K. A. Ross, _Informal Introduction to Set Theory_, lecture notes, University of Oregon, 1988, the axiom of choice (unnumbered): https://people.iith.ac.in/rajeshkannan/ra2021/axiomofchoice.pdf

## Definition

### Cartesian Product

> [!definition] Cartesian Product
> The **Cartesian Product** of sets $A$ and $B$, written $A \times B$, is the set of **ordered** pairs
> $$A \times B = \{(x, y) \mid x \in A \text{ and } y \in B\}.$$
> The $n$-fold product $A_1 \times \cdots \times A_n$ consists of $n$-tuples; $A^n$ abbreviates the $n$-fold product of $A$ with itself.

> [!remark] Why this definition carries the vault
> Every Scope line in `property/` is written over a product: a [[knowledge/math/set theory/relation/Relation\|Relation]] is a subset of $A \times B$, a [[knowledge/math/set theory/Function\|function]] is a special relation, a [[knowledge/math/set theory/operation/Binary Operation\|Binary Operation]] is a function $S \times S \to S$. Ordered pairs are taken as primitive here; the set-theoretic construction $(x,y) := \{\{x\},\{x,y\}\}$ is a foundational detail, noted in [[knowledge/math/Foundations of Mathematics\|Foundations of Mathematics]] and used nowhere else.

### Indexed families and products

> [!definition] Indexed Family
> Given a nonempty collection $\mathcal A$ of sets, an **indexing function** is a surjection $f : J \to \mathcal A$ from an **index set** $J$. Writing $A_\alpha = f(\alpha)$, the collection with its indexing is the **indexed family** $\{A_\alpha\}_{\alpha \in J}$ `[Mun00 §5]`.

> [!definition] Product of an Indexed Family
> - An **$m$-tuple** of elements of $X$ is a function $x : \{1, \dots, m\} \to X$, written $(x_1, \dots, x_m)$; $x_i$ is its $i$-th **coordinate**. For sets $A_1, \dots, A_m$, the cartesian product $\prod_{i=1}^m A_i = A_1 \times \cdots \times A_m$ is the set of $m$-tuples with $x_i \in A_i$ for each $i$.
> - An **$\omega$-tuple** (infinite sequence) is a function $x : \mathbb Z_{>0} \to X$, written $(x_1, x_2, \dots)$. The product $\prod_{i \in \mathbb Z_{>0}} A_i$ is the set of $\omega$-tuples with $x_i \in A_i$, and $X^\omega$ is the set of all $\omega$-tuples of elements of $X$.
>
> `[Mun00 §5]`. For an arbitrary index set $J$, a **$J$-tuple** is a function $x : J \to X$, written $(x_\alpha)_{\alpha \in J}$ with $x_\alpha$ its $\alpha$-th coordinate `[Mun00 §19]`, and $\prod_{\alpha \in J} A_\alpha$ is the set of functions $x : J \to \bigcup_\alpha A_\alpha$ with $x(\alpha) \in A_\alpha$ for each $\alpha$; that it is nonempty whenever every $A_\alpha$ is, is a form of the [[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]] `[Ros88]`.

> [!remark] Order of the factors
> $A \times B$ and $B \times A$ are in bijection by $(a, b) \mapsto (b, a)$ `[Mun00 §5 Ex 1]`, though as sets of ordered pairs they differ unless $A = B$ or one of them is empty.

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

| Property            | Description                                                   |
| ------------------- | ------------------------------------------------------------- |
|                     | $A \cup A = A$, $A \cap A = A$                                |
|                     | $A \subseteq A \cup B$, $A \cap B \subseteq A$                |
|                     | $A \cup \emptyset = A$, $A \cap \emptyset = \emptyset$        |
|                     | $A \cup (A \cap B) = A$, $A \cap (A \cup B) = A$              |
|                     | $A \subseteq C$, $B \subseteq C$, then $A \cup B \subseteq C$ |
|                     | $C \subseteq A$, $C \subseteq B$, then $C \subseteq A \cap B$ |
|                     | $A \subset B$, $B \subset C$, then $A \subset C$              |
|                     | $A \subseteq B$, $B \subseteq C$, then $A \subseteq C$        |
|                     | $A \subset B$, $B \subseteq C$, then $A \subset C$            |
|                     | $A - (B \cap C) = (A - B) \cup (A - C)$                       |
|                     | $A - (B - C) = (A - B) \cup (A \cap C)$                       |
|                     | $A - (B \cup C) = (A - B) - C$                                |
| Negation Form       | $\lnot A$                                                     |
| Contrapositive Form | $\lnot B \implies \lnot A$                                    |
| Converse Form       | $B \implies A$                                                |
