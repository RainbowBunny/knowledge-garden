---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/linear-algebra/linear-maps/","dg-note-properties":{}}
---

Reference:
- `[Ax]` — S. Axler, _Linear Algebra Done Right_, 4th ed. (2024, open access): https://linear.axler.net/ — Chapter 3: Linear Maps (§3A, §3B), §5A (operator). Numbers checked in the chapter PDFs at https://link.springer.com/book/10.1007/978-3-031-41026-0.
- `[Ax2]` — S. Axler, _Linear Algebra Done Right_, 2nd ed. (1997). Not opened; the note follows its order, and the key marks results whose 4th-edition number I could not check.
- `[AxI]` — S. Axler, _Invertibility and Isomorphic Vector Spaces_ (LADR supplement, unnumbered): https://www.linear.axler.net/Invertibility.pdf
- `[LNS16]` — I. Lankham, B. Nachtergaele, A. Schilling, _Linear Algebra As an Introduction to Abstract Mathematics_ (2016), §6.7 Invertibility, LibreTexts edition: https://math.libretexts.org/Bookshelves/Linear_Algebra/Book%3A_Linear_Algebra_(Schilling_Nachtergaele_and_Lankham)
- `[MITo]` — MIT OpenCourseWare 18.700 _Linear Algebra_ (Fall 2013), notes "One-sided inverses": https://live.ocw.mit.edu/courses/18-700-linear-algebra-fall-2013/d1093d3f7651c8a58f860179ecb8e4ec_MIT18_700F13_one_sided.pdf

## Definition

> [!definition] Parameters
> - $\mathbb F$: a [[knowledge/math/algebra/structures/field/Field\|Field]].
> - $U, V, W$: [[knowledge/math/algebra/linear algebra/Vector Spaces\|vector spaces]] over $\mathbb F$.

> [!definition] Linear Map
> Extends:: [[knowledge/math/property/map/Homomorphism\|Homomorphism]]
>
> ---
> A **linear map** from $V$ to $W$ is a function $T: V \rightarrow W$ with the following properties:
> - Additivity: $T(u + v) = T(u) + T(v)$ for all $u, v \in V$;
> - Homogeneity: $$T(av) = a T(v)$$ for all $a \in \mathbb F$ and all $v \in V$.
>
> `[Ax 3.1]`

> [!remark]
> The set of all linear maps from $V$ to $W$ is denoted $\mathcal L(V, W)$; $\mathcal L(V) = \mathcal L(V, V)$. `[Ax 3.2]`

> [!definition] Parameters
> - $T \in \mathcal L(U, V)$, $S \in \mathcal L(V, W)$: linear maps.

> [!definition] Product of Linear Maps
> For $T \in \mathcal L(U, V)$ and $S \in \mathcal L(V, W)$, the **product** $ST \in \mathcal L(U, W)$ is defined by $$(ST)(u) = S(T(u))$$ for $u \in U$. `[Ax 3.7]`

> [!proposition] Algebraic properties of products — associative, unital, distributive
> - **Associativity Law**
> - **Identity Law**
> - **Distributive Law**
>
> `[Ax 3.8]`

> [!definition] Operator
> A linear map from a vector space to itself is called an **operator**. `[Ax 5.1]`

### Null Spaces and Ranges

Specializes [[knowledge/math/set theory/function/Kernel\|knowledge/math/set theory/function/Kernel]] (null space) and [[knowledge/math/set theory/Function#Image\|Image]] (range).

> [!definition] Parameters
> - $T \in \mathcal L(V, W)$: a linear map.

> [!definition] Null Space
> For $T \in \mathcal L(V, W)$, the **null space (or kernel)** of $T$, denoted by $\text{null } T$, is the subset of $V$ consisting of those vectors that $T$ maps to $0$: $$\text{null } T = \{v \in V: T(v) = 0\}.$$
> We have $\text{null } T$ is a subspace of $V$.
>
> `[Ax 3.11]` `[Ax 3.13]`

> [!proposition] Injectivity $\iff$ null space equals $\{0\}$
> Let $T \in \mathcal L(V, W)$. Then $T$ is injective if and only if $\text{null } T= \{0\}$. `[Ax 3.15]`

> [!definition] Range
> For $T \in \mathcal L(V, W)$, the **range** of $T$, denoted $\text{range } T$, is the subset of $W$ consisting of those vectors that are of form $T(v)$ for some $v \in V$: $$\text{range } T = \{T(v) : v \in V\}.$$ we have $\text{range } T$ is a subspace of $W$.
>
> `[Ax 3.16]` `[Ax 3.18]`

> [!theorem] Fundamental theorem of linear maps — $\dim V = \dim \text{null } T + \dim \text{range } T$
> If $V$ is finite dimensional and $T \in \mathcal L(V, W)$, then $\text{range } T$ is a finite-dimensional subspace of $W$ and $$\dim V = \dim \text{null } T + \dim \text{range } T.$$ `[Ax 3.21]`

> [!corollary] No injection into a smaller space, no surjection onto a larger one
> - If $V$ and $W$ are finite-dimensional vector spaces such that $\dim V > \dim W$, then no linear map from $V$ to $W$ is injective.
> - If $V$ and $W$ are finite-dimensional vector spaces such that $\dim V < \dim W$, then no linear map from $V$ to $W$ is surjective.
>
> `[Ax 3.22]` `[Ax 3.24]`

### Invertibility

Specializes [[knowledge/math/algebra/category/Morphism#Isomorphism\|Isomorphism]] — an invertible linear map is an isomorphism in the category of vector spaces.

> [!definition] Invertible, Inverse
> A linear map $T \in \mathcal L(V, W)$ is called **invertible** if there exists a linear map $S \in \mathcal L(W, V)$ such that $ST$ equals the identity map on $V$ and $TS$ equals the identity map on $W$. A linear map $S \in \mathcal L(W, V)$ satisfying $ST = I$ and $TS = I$ is called an **inverse** of $T$. `[LNS16 Def 6.7.1]` `[AxI]`

> [!proposition] Invertible $\iff$ injective and surjective
> A linear map is invertible if and only if it is injective and surjective. `[LNS16 Prop 6.7.2]`

> [!definition] Isomorphic
> Two vector spaces are called **isomorphic** if there is an invertible linear map from one vector space onto the other one. `[LNS16 Def 6.7.5]`

> [!theorem] Dimension decides isomorphism — finite-dimensional spaces are isomorphic iff they have the same dimension
> Two finite-dimensional vector spaces are isomorphic if and only if they have the same dimension. `[LNS16 Thm 6.7.6]`

> [!definition] Parameters
> - $(v_1, \dots, v_n)$: a basis of $V$.
> - $(w_1, \dots, w_m)$: a basis of $W$.
> - $\mathcal M$: the map sending $T \in \mathcal L(V, W)$ to its [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]] with respect to these bases.

> [!proposition] $\mathcal L(V, W)$ and $\text{Mat}(m, n, \mathbb F)$ are isomorphic
> Suppose that $(v_1, \dots, v_n)$ is a basis of $V$ and $(w_1, \dots, w_m)$ is a basis of $W$. Then $\mathcal M$ is an invertible linear map between $\mathcal L(V, W)$ and $\text{Mat}(m, n, \mathbb F)$. `[AxI]`

> [!proposition] $\dim \mathcal L(V, W) = (\dim V)(\dim W)$
> If $V$ and $W$ are finite dimensional, then $\mathcal L(V, W)$ is finite dimensional and $$\dim \mathcal L(V, W) = (\dim V)(\dim W)$$ `[AxI]`

> [!theorem] Injectivity is equivalent to surjectivity for operators in finite dimensions
> Suppose $V$ is finite dimensional. If $T \in \mathcal L(V)$, then the following are equivalent:
> 1. $T$ is invertible;
> 2. $T$ is injective;
> 3. $T$ is surjective.
>
> `[LNS16 Thm 6.7.7]` `[AxI]`

> [!definition] Parameters
> - $U$: a subspace of $V$.
> - $S \in \mathcal L(U, W)$.

> [!proposition] Extension from a subspace — every linear map on $U$ extends to $V$
> Suppose that $V$ is finite-dimensional. If $U$ is a subspace of $V$ and $S \in \mathcal L(U, W)$, then there exists $T \in \mathcal L(V, W)$ such that $T(u) = S(u)$ for all $u \in U$. `[Ax Ex 3A.13]`

> [!definition] Parameters
> - $S_1, \dots, S_n$: linear maps whose product $S_1 \dots S_n$ is defined.

> [!proposition] A product of injective maps is injective
> If $S_1, \dots, S_n$ are injective linear maps such that $S_1 \dots S_n$ makes sense,
> then $S_1 \dots S_n$ is injective. `[Ax2]`

> [!definition] Parameters
> - $S, T \in \mathcal L(V)$: operators.

> [!proposition] One-sided inverses of operators are two-sided — $ST = I \iff TS = I$
> Suppose that $V$ is finite dimensional and $S, T \in \mathcal L(V)$, then $ST = I$ if and only if $TS = I$. `[Ax2]`

> [!definition] Parameters
> - $n$: a positive integer.
> - $a_{i, j} \in \mathbb F$ for $i, j = 1, \dots, n$.
> - $c_1, \dots, c_n \in \mathbb F$.

> [!proposition] Square systems — uniqueness for the homogeneous system $\iff$ solvability for every right-hand side
> Suppose $n$ is a positive integer and $a_{i, j} \in \mathbb F$ for $i, j = 1, \dots, n$. Then, the following are equivalent:
> 1. The trivial solution $x_1 = \cdots = x_n = 0$ is the only solution to the homogeneous system of equations $$\begin{align}\sum_{k = 1}^n a_{1, k}x_k = 0 \\ \vdots \\ \sum_{k = 1}^n a_{n, k} x_k = 0 \end{align}$$
> 2. For every $c_1, \dots, c_n \in \mathbb F$, there exists a solution to the system of equations $$\begin{align}\sum_{k = 1}^n a_{1, k}x_k = c_1 \\ \vdots \\ \sum_{k = 1}^n a_{n, k} x_k = c_n \end{align}$$
>
> `[Ax2]`

### One-sided Inverse

> [!definition] Parameters
> - $T \in \mathcal L(V, W)$: a linear map.
> - $c \in W$: a right-hand side.

> [!definition] Left Inverse, Right Inverse
> Suppose $V$ and $W$ are vector spaces over a field $\mathbb F$, and $T \in \mathcal L(V, W)$. A **left inverse** for $T$ is a linear map $S \in \mathcal L(W, V)$ with the property that $ST = I_V$ (the identity map on $V$). That is, we have $$ST(v) = v \quad \forall v \in V.$$
> A **right inverse** for $T$ is a linear map $S' \in \mathcal L(W, V)$ with the property that $TS' = I_W$ (the identity map on $W$). That is, we require $$TS'(w) = w \quad \forall w \in W.$$
>
> `[MITo]`

> [!proposition] A left inverse gives the only candidate solution
> Suppose $S$ is a left inverse of $T$. Then the only possible solution of $T(x) = c$ is $x = S(c)$. `[MITo Prop 2]`

> [!proposition] A right inverse gives a solution
> Suppose $S'$ is a right inverse of $T$. Then $x = S'(c)$ is a solution of $T(x) = c$. `[MITo Prop 3]`

> [!theorem] One-sided inverses and complements — left inverses exist iff $T$ is injective, right inverses iff $T$ is surjective
> Suppose $V$ and $W$ are finite-dimensional, and that $T \in \mathcal L(V, W)$.
> 1. The operator $T$ has a left inverse if and only if $\text{Null}(T) = 0$.
> 2. If $S$ is a left inverse of $T$, then $\text{Null}(S)$ is a complement to $\text{Range}(T)$: $$W = \text{Range}(T) \oplus \text{Null}(S).$$
> 3. Assuming that $\text{Null}(T) = 0$, there is a one-to-one correspondence between left inverses of $T$ and subspaces of $W$ complementary to $\text{Range}(T)$.
> 4. The operator $T$ has a right inverse if and only if $\text{Range}(T) = W$.
> 5. If $S'$ is a right inverse of $T$, then $\text{Range}(S')$ is a complement to $\text{Null}(T)$: $$V = \text{Null}(T) \oplus \text{Range}(S').$$
> 6. Assuming that $\text{Range}(T) = W$, there is a one-to-one correspondence between right inverses of $T$ and subspaces of $V$ complementary to $\text{Null}(T)$.
> 7. If $T$ has both a left and a right inverse, then the left and right inverses are unique and equal to each other. That, is there is a unique linear map $S \in \mathcal L(W, V)$ characterized by either of the two properties $ST = I_V$ or $TS = I_W$. If it has one of these properties, then it automatically has the other.
>
> `[MITo Thm 4]`

### Projection

> [!definition] Parameters
> - $U, W$: subspaces of $V$ with $V = U \oplus W$.

> [!definition] Projection between Subspaces
> Suppose $U$ and $W$ are subspaces of $V$ with $$V = U \oplus W.$$ Each vector $v \in V$ can be written uniquely in the form $$v = u + w,$$ where $u \in U$ and $w \in W$. With this representation, define $P_{U, W} \in \mathcal L(V)$ by $$P_{U, W}(v) = u.$$ And $P_{U, W}$ is often called the **projection** onto $U$ with null space $W$. `[Ax2]`

> [!definition] Parameters
> - $P \in \mathcal L(V)$: an operator.

> [!definition] Projection of Operator
> Suppose $V$ is a vector space. A **projection** on $V$ is a linear map $P \in \mathcal L(V)$ with the property $P^2 = P$. `[Ax2]`

> [!proposition] Projections, complementary pairs and direct sums correspond
> Suppose $V$ is a vector space. The following things are in one-to-one correspondence:
> 1. Projections $P \in \mathcal L(V)$;
> 2. Pairs of linear transformations $P$ and $Q$ in $\mathcal L(V)$ such that
>     - $P + Q = I$
>     - $PQ = 0$;
> 3. Direct sum decompositions $V = U \oplus W$.
>
> `[Ax2]`

> [!example]
> Suppose $P \in \mathcal L(V)$ and $P^2 = P$. Then, $V = \text{null } P \oplus \text{range } P$.
> - $v = (v - P(v)) + P(v)$
> - $P(v - P(v)) = 0$

> [!example]
> If $P \in \mathcal L(V)$ is such that $P^2 = P$ and every vector in $\text{null } P$ is orthogonal to every vector in $\text{range } P$, then $P$ is an orthogonal projection.
> $(V = \text{null } P \oplus \text{range } P)$

> [!example]
> If $P \in \mathcal L(V)$ is such that $P^2 = P$ and $$||P(v)|| \leq ||v||$$ for every $v \in V$, then $P$ is an orthogonal projection.
> (Let $u \in \text{range } P$ and $w \in \text{null } P$, we have $P(u + tw) = u$, thus $||u|| \leq ||u + tw|| \; \forall \; t \in \mathbb R$)

> [!example]
> Suppose $P \in \mathcal L(V)$ is such that $P^2 = P$. $P$ is an orthogonal projection if and only if $P$ is self-adjoint.

## Related

### Constructions
- [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]] — $\mathcal M(T)$, the matrix of $T$ in chosen bases
- [[knowledge/math/algebra/linear algebra/Dual Bases\|Dual Bases]] — linear maps into $\mathbb F$ (linear functionals) and the dual map

### Siblings
- [[knowledge/math/algebra/structures/group/homomorphism/Group Homomorphism\|Group Homomorphism]] — preserves only the addition; a linear map must also commute with scalars
- [[knowledge/math/algebra/linear algebra/Operators\|Operators]] — the special case $W = V$, where eigenvalues and powers make sense

### Prerequisites
- [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]] — domain and codomain
- [[knowledge/math/property/map/Homomorphism\|Homomorphism]] — the origin note
- [[knowledge/math/algebra/category/Morphism\|Morphism]] — isomorphism in the categorical sense
