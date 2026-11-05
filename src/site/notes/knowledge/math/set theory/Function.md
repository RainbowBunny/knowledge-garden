---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/function/","dg-note-properties":{}}
---

Reference:
- [[academic/Book Reference\|Algebra: Chapter 0]] - Chapter I: Preliminaries: Set theory and categories, Section 2.1: Definition; Section 2.3: Composition of functions; Section 2.5: Injections, surjections, bijections: Second viewpoint.

## Definition

> [!definition] Function
> A function is the subset of $A \times B$:
> $$\Gamma_f = \{(a, b) \in A \times B \; | \; b = f(a)\} \subseteq A \times B$$
> That satisfies:
> $$(\forall a \in A) (\exists! b \in B) \quad (a, b) \in \Gamma_f$$

> [!remark]
> Equivalently: a function is a [[knowledge/math/set theory/relation/Relation\|Relation]] $\Gamma_f \subseteq A \times B$ that is left-total and functional. The condition $(\forall a)(\exists! b)$ above says exactly that.

> [!theorem]
> Two function $f$ and $g$ are equal if and only if
> 1. $f$ and $g$ have the same domain, and
> 2. $f(x) = g(x)$ for every $x$ in the domain of $f$.

### Domain

> [!definition] Domain
> For a function $f$, the set of all elements $x$ that occur as the first members of pairs $(x, y)$ in $f$ is called the **domain** of $f$ denoted as $\mathsf{dom}(f)$.

### Co-Domain

> [!definition] Co-domain
> For a function $f$, the set of all possible elements $y$ is called the **co-domain** of $f$.

### Range

> [!definition] Range
> The **range** of a function is the set containing all the possible values of $f(x)$ denoted as $\mathsf{ran}(f)$.

### Image

> [!definition] Image
> If $S$ is a subset of $A$, we denote by $f(S)$ the subset of $B$ defined by
> $$f(S) = \{b \in B \; | \; (\exists a \in S) \; b = f(a)\}.$$
> That is, $f(S)$ is the subset of $B$ consisting of all elements that are images of elements of $S$ by the function $f$. $f(A)$ is the **image** of $f$, denoted $\text{im} \; f$.

## Variant

### Partial Function

### Restriction

> [!definition] Restriction
> $f_S$ denotes the 'restriction' of $f$ to the subset $S$: this is the function $S \rightarrow B$ defined by
> $$(\forall s \in S): \quad f|_S(s) = f(s).$$

### Composition

> [!definition] Composition
> Functions may be **composed**: if $f: A \rightarrow B$ and $g: B \rightarrow C$ are functions, then so is the operation $g \circ f$ defined by
> $$(\forall a \in A) \quad (g \circ f)(a) = g(f(a))$$

> [!remark] Commutative Diagram Form of Composition
> $$\begin{CD} 
> A @>f>> B \\ 
> @| @VVgV \\ 
> A @>>{g \circ f}> C 
> \end{CD}$$

> [!remark] Associativity of Composition
> Composition is associative: if $f: A \rightarrow B, g : B \rightarrow C$, and $h: C \rightarrow D$ are functions, then $h \circ (g \circ f) = (h \circ g) \circ f$.

> [!remark] Commutative Diagram Form of Composition
> $$\begin{CD} 
> A @>f>> B @>h \circ g>> D\\ 
> @| @VVgV @|\\ 
> A @>>{g \circ f}> C @>h>> D 
> \end{CD}$$

## Property

### Inverse

> [!definition] Inverse
> If $f: A \rightarrow B$ is a bijection, then we can define an inverse function:
> $$g: B \rightarrow A$$
> such that $a = g(b) \iff b = f(a)$.
> If $g \circ f = \text{id}_A$, we have a left-inverse.
> If $f \circ g = \text{id}_B$, we have a right-inverse.

> [!proposition]
> Assume $A \neq \emptyset$, and let $f: A \rightarrow B$ be a function. Then,
> 1. $f$ has a left-inverse if and only if it is injective.
> 2. $f$ has a right-inverse if and only if it is surjective.

> [!corollary]
> A function $f: A \rightarrow B$ is a bijection if and only if it has a (two-sided) inverse.


