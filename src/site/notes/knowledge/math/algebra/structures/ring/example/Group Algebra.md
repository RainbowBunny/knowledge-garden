---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/example/group-algebra/","dg-note-properties":{}}
---

Reference:
- `[EGH+]` — P. Etingof, O. Golberg, S. Hensel, T. Liu, A. Schwendner, D. Vaintrob, E. Yudovina, _Introduction to Representation Theory_, AMS Student Mathematical Library 59 (2011); arXiv:0901.0827: https://arxiv.org/abs/0901.0827. Numbers follow the arXiv / MIT OCW 18.712 version; the printed book numbers differently.
- [[academic/Book Reference\|Algebra: Chapter 0]] - Chapter III: Rings and modules, Section 1.4: Monoid rings.
- `[Bum]` — D. Bump, _Hecke Algebras_, lecture notes (2018): http://sporadic.stanford.edu/hecke.pdf

## Definition

> [!definition] Parameters
> - $k$: a field. $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]].

> [!definition] Group Algebra
> Extends:: [[knowledge/math/algebra/structures/ring/example/Monoid Ring\|Monoid Ring]].
>
> ---
> The **group algebra** $k[G]$ has basis $\{a_g : g \in G\}$ and multiplication $a_g a_h = a_{gh}$, extended bilinearly. `[EGH+ Ex. 1.6(5)]`

> [!remark] It is a monoid ring
> Writing $\sum_g c_g a_g$ as $\sum_g c_g\, g$, this is the [[knowledge/math/algebra/structures/ring/example/Monoid Ring\|Monoid Ring]] $k[G]$ with $M = G$ and $R = k$: the coefficient of $g$ in a product is $\sum_{g_1 g_2 = g} a_{g_1} b_{g_2}$, and the identity is $a_e$.

> [!remark] As functions with convolution
> For finite $G$, identify $f: G \to k$ with $\sum_g f(g)\, a_g$. The coefficient of $a_x$ in a product is $\sum_{g_1 g_2 = x} f(g_1) h(g_2)$; putting $g_1 = y$ gives
> $$(f * h)(x) = \sum_{y \in G} f(y)\, h(y^{-1} x),$$
> so $k[G]$ is the space of functions on $G$ under convolution. `[Bum §2]` normalises the convolution by $\frac{1}{|G|}$ when it defines Hecke algebras of bi-invariant functions; this algebra is the case of the trivial subgroup.

## Property

> [!proposition] Its modules are the representations of $G$
> A representation of $k[G]$ is the same thing as a [[knowledge/math/algebra/structures/action/Group Representation\|representation]] of $G$. `[EGH+ Ex. 1.19(3)]`

> [!proposition] Semisimple exactly in good characteristic
> For finite $G$, $k[G]$ is semisimple iff the characteristic of $k$ does not divide $|G|$ ([[knowledge/math/algebra/structures/action/Group Representation#Property\|Maschke's theorem]] and its converse) `[EGH+ Thm 3.1, Prop 3.2]`. Then, as a representation of itself, $k[G] \cong \bigoplus_i \dim(V_i)\, V_i$ and $|G| = \sum_i \dim(V_i)^2$ `[EGH+ Thm 3.1(ii)]`.

## Related

### Siblings
- [[knowledge/math/algebra/structures/ring/example/Hecke Algebra\|Hecke Algebra]] — a deformation of $\mathbb C[W]$ for a Coxeter group $W$; at $q = 1$ it is this algebra

### Prerequisites
- [[knowledge/math/algebra/structures/ring/example/Monoid Ring\|Monoid Ring]], [[knowledge/math/algebra/structures/ring/module/R-algebra\|R-algebra]], [[knowledge/math/algebra/structures/group/Group\|Group]]
