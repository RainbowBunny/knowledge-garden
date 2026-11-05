---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/linear-algebra/inner-product-spaces/","dg-note-properties":{}}
---

Reference:
- `[Ax]` — S. Axler, _Linear Algebra Done Right_, 4th ed. (2024, open access): https://linear.axler.net/ — §7A Self-Adjoint and Normal Operators (adjoints). Numbers checked in the chapter PDF at https://link.springer.com/book/10.1007/978-3-031-41026-0; the Chapter 6 PDF (inner product spaces) could not be opened.
- `[Ax2]` — S. Axler, _Linear Algebra Done Right_, 2nd ed. (1997), Chapter 6: Inner-Product Spaces. Not opened; the note follows its order, and the key marks results whose 4th-edition number I could not check.
- `[AxD]` — S. Axler, _Duality, part 1: Dual Bases and Dual Maps_ (LADR supplement, unnumbered): https://www.linear.axler.net/DualBasesMaps.pdf
- `[LNS16]` — I. Lankham, B. Nachtergaele, A. Schilling, _Linear Algebra As an Introduction to Abstract Mathematics_ (2016), Chapter 9: Inner product spaces (§9.1–9.6), §7.5, LibreTexts edition: https://math.libretexts.org/Bookshelves/Linear_Algebra/Book%3A_Linear_Algebra_(Schilling_Nachtergaele_and_Lankham)
- `[Reg04]` — O. Regev, _Lattices in Computer Science_, Lecture 1: Introduction (Tel Aviv University, Fall 2004): https://cims.nyu.edu/~regev/teaching/lattices_fall_2004/ln/introduction.pdf

## Definition

> [!definition] Parameters
> - $\mathbb F$: $\mathbb R$ or $\mathbb C$.
> - $V$: a finite-dimensional [[knowledge/math/algebra/linear algebra/Vector Spaces\|vector space]] over $\mathbb F$.

> [!definition] Inner Product
> An **inner product** on $V$ is a function that takes each ordered pair $(u, v)$ of elements of $V$ to a number $\langle u, v \rangle \in \mathbb F$ and has the following properties:
> - **Positivity**: $\langle v, v \rangle \geq 0 \; \forall \; v \in V;$
> - **Definiteness**: $\langle v, v \rangle = 0 \Leftrightarrow v = 0;$
> - **Additivity in first slot**: $\langle u + v, w \rangle = \langle u, w \rangle + \langle v, w \rangle \; \forall \; u, v, w \in V;$
> - **Homogeneity in first slot**: $\langle av, w \rangle = a \langle v, w \rangle \; \forall \; a \in \mathbb F \; \forall \; v, w \in V;$
> - **Conjugate symmetry**: $\langle v, w \rangle = \overline {\langle w, v \rangle} \; \forall \; v, w \in V$.
>
> `[LNS16 Def 9.1.1]`

> [!definition] Inner Product Space
> Extends:: [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]].
>
> ---
> An **inner product space** is a vector space $V$ along with an inner product on $V$. `[LNS16 Def 9.1.3]`

## Structure

### Norms

> [!definition] Parameters
> - $u, v, w \in V$: vectors.

> [!definition] Norm
> For $v \in V$, we define the **norm** of $v$, denoted by $||v||$, by $$||v|| = \sqrt{\langle v, v \rangle}.$$ `[LNS16 Eq 9.2.1]`

> [!definition] Parameters
> - $U$: a vector space over $\mathbb F$.
> - $||\;||: U \rightarrow [0, \infty)$: a function.

> [!proposition] Norms from inner products — a norm comes from an inner product iff it satisfies the parallelogram equality
> A norm on a vector space $U$ is a function $||\;||: U \rightarrow [0, \infty)$  such that:
> 1. $||u|| = 0$ if and only if $u = 0$
> 2. $||\alpha u|| = |\alpha| \; ||u||$ for all $\alpha \in \mathbb F$ and all $u \in U$
> 3. $||u + v|| \leq ||u|| + ||v||$ for all $u, v \in U$.
>
> Then, a norm satisfying the parallelogram equality comes from an inner product (there is an inner product $\langle , \rangle$ on $U$ such that $||u|| = \langle u, u \rangle^{1/2}$ for all $u \in U$).
>
> `[LNS16 Def 9.2.1]` `[LNS16 §9.2]`

> [!definition] Orthogonal
> Two vectors $u, v \in V$ are said to be **orthogonal** if $\langle u, v \rangle = 0$. `[LNS16 Def 9.3.1]`

> [!theorem] Pythagorean theorem — $||u + v||^2 = ||u||^2 + ||v||^2$ for orthogonal $u, v$
> If $u, v$ are orthogonal vectors in $V$, then $$||u + v||^2 = ||u||^2 + ||v||^2.$$ `[LNS16 Thm 9.3.2]`

> [!definition] Parameters
> - $v, w \in V \subset \mathbb R^m$: vectors.
> - $\theta$: the angle between them.

> [!proposition] Angle, Cauchy–Schwarz, triangle inequality and parallelogram equality
> Let $v, w \in V \subset \mathbb R^m.$
> 1. Let $\theta$ be the angle between the vectors $v$ and $w$, where we place the starting points of $v$ and $w$ at the origin $0$. Then $$v \cdot w = ||v|| \; ||w|| \cos(\theta),$$
> 2. (**Cauchy–Schwarz Inequality**) $$|v \cdot w| \leq ||v|| \; ||w||.$$
> 3. (**Triangle Inequality**) $$||u + v|| \leq ||u|| + ||v||.$$
> 4. (**Parallelogram Equality**) $$||u + v||^2 + ||u - v||^2 = 2(||u||^2 + ||v||^2).$$
>
> `[LNS16 Thm 9.3.3]` `[LNS16 Thm 9.3.4]` `[LNS16 Thm 9.3.6]`

### Orthogonal Bases

> [!definition] Parameters
> - $(e_1, \dots, e_m)$: a list of vectors in $V$.
> - $a_1, \dots, a_m \in \mathbb F$: scalars.

> [!definition] Orthonormal
> A list of vectors is called **orthonormal** if the vectors in it are pairwise orthogonal and each vector has norm 1. `[LNS16 Def 9.4.1]`

> [!proposition] Norm of an orthonormal linear combination
> If $(e_1, \dots, e_m)$ is an orthonormal list of vectors in $V$, then $$||a_1 e_1 + \cdots + a_m e_m||^2 = |a_1|^2 + \cdots + |a_m|^2$$ for all $a_1, \dots, a_m \in \mathbb F$. `[LNS16 Prop 9.4.2]`

> [!corollary] Orthogonal lists of nonzero vectors are linearly independent
> Every orthogonal list of nonzero vectors is linearly independent. `[LNS16 Prop 9.4.2]`

> [!definition] Parameters
> - $v_1, \dots, v_n$: a basis of $V$.

> [!definition] Orthogonal Basis
> An **orthogonal basis** for a vector space $V$ is a basis $v_1, \dots, v_n$ with the property that $$v_i \cdot v_j = 0 \quad \forall i \neq j.$$ The basis is **orthonormal** if in addition, $||v_i|| = 1 \; \forall i$. `[LNS16 Def 9.4.3]`

> [!theorem] Expansion in an orthonormal basis — coefficients are inner products
> Suppose $(e_1, \dots, e_n)$ is an orthonormal basis of $V$. Then $$v = \langle v, e_1 \rangle e_1 + \cdots + \langle v, e_n \rangle e_n$$ and $$||v||^2 = |\langle v, e_1 \rangle|^2 + \cdots + |\langle v, e_n \rangle|^2$$ for every $v \in V$. `[LNS16 Thm 9.4.6]`

> [!definition] Parameters
> - $(f_1, \dots, f_m)$: an orthogonal basis of $V$.

> [!theorem] Expansion in an orthogonal basis
> Suppose $(f_1, \dots, f_m)$ is an orthogonal basis of $V$. Then $$v = \sum_{i = 1}^m \frac{\langle v, f_i \rangle}{\langle f_i, f_i \rangle} f_i$$ and $$||v||^2 = \sum_{i = 1}^m \frac{|\langle v, f_i \rangle|^2}{\langle f_i, f_i \rangle}$$ for every $v \in V$. `[LNS16 Thm 9.4.6]` applied to $e_i = f_i / ||f_i||$

> [!definition] Parameters
> - $n$: a positive integer.
> - $C[-\pi, \pi]$: the real vector space of continuous functions $[-\pi, \pi] \to \mathbb R$.

> [!proposition] The trigonometric system is orthonormal in $C[-\pi, \pi]$
> Suppose $n$ is a positive integer then $$(\frac{1}{\sqrt{2\pi}}, \frac{\sin x}{\sqrt{\pi}}, \frac{\sin 2x}{\sqrt{\pi}}, \dots, \frac{\sin nx}{\sqrt{\pi}}, \frac{\cos x}{\sqrt{\pi}}, \frac{\cos 2x}{\sqrt{\pi}}, \dots, \frac{\cos nx}{\sqrt{\pi}})$$ is an orthonormal list of vectors in $C[-\pi, \pi]$, the vector space of continuous real-valued functions on $[-\pi, \pi]$ with inner product $$\langle f, g \rangle = \int_{-\pi}^{\pi} f(x) g(x) dx.$$ `[Ax2]`

> [!proposition] Equality in Bessel's inequality — exactly for vectors in the span
> Suppose $(e_1, \dots, e_m)$ is an orthonormal list of vectors in $V$. Let $v \in V$, then $$||v||^2 = \sum_{i = 1}^m |\langle v, e_i \rangle|^2$$ if and only if $v \in \text{span}(e_1, \dots, e_m)$. `[Ax2]`

### Gram-Schmidt Algorithm

> [!algorithm] Gram–Schmidt Orthogonalization Algorithm
> **Input:**
> A basis $(v_1, v_2, \ldots, v_n)$ of a vector space $V \subset \mathbb{R}^m$
>
> **Output:**
> An orthogonal basis $(v_1^{*}, v_2^{*}, \ldots, v_n^{*})$ of $V$
>
> ---
>
> 1. Set:
>    $$v_1^{*} \gets v_1.$$
>
> 2. For $i = 2, 3, \ldots, n$, do:
>
>    2.1. For each $j = 1, 2, \ldots, i-1$, compute:
>    $$\mu_{ij} \gets \frac{\langle v_i, v_j^{*} \rangle}{\langle v_j^{*}, v_j^{*} \rangle}.$$
>
>    2.2. Set:
>    $$v_i^{*} \gets v_i - \sum_{j=1}^{i-1} \mu_{ij} v_j^{*}.$$
>
> 3. Return the orthogonal basis $(v_1^{*}, v_2^{*}, \ldots, v_n^{*})$.
>
> `[Reg04 Def 6]`; normalized form, $e_k = v_k^* / ||v_k^*||$, in `[LNS16 Thm 9.5.1]`

> [!definition] Parameters
> - $L$: a lattice ([[knowledge/math/algebra/structures/lattice/Lattices\|Lattices]]) with basis $\mathcal B = \{v_1, \dots, v_n\}$.
> - $\mathcal B^* = \{v_1^*, \dots, v_n^*\}$: its Gram–Schmidt orthogonal basis.

> [!proposition] Lattice determinant from Gram–Schmidt — $\det(L) = \prod_i ||v_i^*||$
> Let $\mathcal B = \{v_1, v_2, \dots, v_n\}$ be a basis for a lattice $L$ and $\mathcal B^* = \{v_1^*, v_2^*, \dots, v_n^*\}$ be the associated Gram-Schmidt orthogonal basis. Then $$\det(L) = \prod_{i = 1}^n ||v_i^*||$$ `[Reg04 §1, after Eq. 1]`

> [!corollary] Existence of orthonormal bases
> Every finite-dimensional inner-product space has an orthonormal basis. `[LNS16 Cor 9.5.3]`

> [!corollary] Every orthonormal list extends to an orthonormal basis
> Every orthonormal list of vectors in $V$ can be extended to an orthonormal basis of $V$. `[LNS16 Cor 9.5.4]`

> [!definition] Parameters
> - $T \in \mathcal L(V)$: an operator ([[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]]).

> [!corollary] Upper-triangular with respect to some orthonormal basis
> Suppose $T \in \mathcal L(V)$. If $T$ has an upper-triangular matrix with respect to some basis of $V$, then $T$ has an upper-triangular matrix with respect to some orthonormal basis of $V$. `[LNS16 Cor 9.5.5]`

> [!theorem] Schur's theorem — every complex operator is upper-triangular in some orthonormal basis
> Suppose $V$ is a complex vector space and $T \in \mathcal L(V)$. Then $T$ has an upper-triangular matrix with respect to some orthonormal basis of $V$. `[LNS16 Thm 7.5.3]` + `[LNS16 Cor 9.5.5]`

### Orthogonal Projections and Minimization Problems

> [!definition] Parameters
> - $W, U$: subspaces of $V$.

> [!definition] Orthogonal Complement
> Let $V$ be a vector space and let $W \subset V$ be a vector subspace of $V$. The **orthogonal complement** of $W$ (in $V$) is $$W^{\perp} = \{v \in V: \langle v, w \rangle = 0 \; \forall \; w \in W\}.$$ `[LNS16 Def 9.6.1]`

> [!theorem] $V = U \oplus U^{\perp}$
> If $U$ is a subspace of the finite-dimensional inner-product space $V$, then $$V = U \oplus U^{\perp}.$$ `[LNS16 Thm 9.6.2]`

> [!corollary] $U = (U^{\perp})^{\perp}$
> If $U$ is a subspace of the finite-dimensional inner-product space $V$, then $$U = (U^{\perp})^{\perp}$$ `[LNS16 Thm 9.6.4]`

> [!definition] Orthogonal Projection
> Suppose $U$ is a subspace of $V$, because of the decomposition $V = U \oplus U^{\perp}$ so each vector $v \in V$ can be written uniquely in the form $$v = u + w,$$ where $u \in U$ and $w \in U^{\perp}$. Then, we can define operator $P_U$ on $V$, called the **orthogonal projection** of $V$ onto $U$ by: $P_U(v) = u$. `[LNS16 Def 9.6.5]`

> [!proposition] Properties of projection — range $U$, null space $U^\perp$, idempotent, norm-decreasing
> 1. $\text{range } P_U = U$;
> 2. $\text{null } P_U = U^{\perp}$;
> 3. $v - P_U v \in U^{\perp} \; \forall \; v \in V$;
> 4. $P_U^2 = P_U$;
> 5. $||P_U(v)|| \leq ||v|| \; \forall \; v \in V$.
>
> `[LNS16 §9.6]` (items 1, 2, 4) `[Ax2]`

> [!proposition] Minimizing the distance to a subspace — $P_U(v)$ is the closest point of $U$
> Suppose $U$ is a subspace of $V$ and $v \in V$. Then $$||v - P_U(v)|| \leq ||v - u||$$ for every $u \in U$. Furthermore, if $u \in U$ and the inequality above is an equality, then $u = P_U(v)$. `[LNS16 Prop 9.6.6]`

### Linear Functionals and Adjoints

> [!definition] Linear Functional
> A **linear functional** on $V$ is a linear map from $V$ to the scalars $\mathbb F$. `[AxD]`

> [!definition] Parameters
> - $\varphi$: a linear functional on $V$.

> [!theorem] Riesz representation theorem — every linear functional is an inner product with a fixed vector
> Suppose $\varphi$ is a linear functional on $V$. Then there is a unique vector $v \in V$ such that $$\varphi(u) = \langle u, v \rangle$$ for every $u \in V$. `[Ax2]`

> [!remark]
> Let $(e_1, \dots, e_n)$ be an orthonormal basis of $V$. Then, $$\varphi(u) = \langle u, \sum_{i = 1}^n \overline{\varphi(e_i)} e_i \rangle$$

> [!definition] Parameters
> - $W$: a finite-dimensional inner-product space over $\mathbb F$.
> - $T \in \mathcal L(V, W)$: a linear map.

> [!definition] Adjoint
> Let $T \in \mathcal L(V, W)$. The **adjoint** of $T$, denoted $T^* \in \mathcal L(W, V)$ such that $$\langle T(v), w \rangle = \langle v, T^*(w) \rangle$$ for all $v \in V$ and $w \in W$. `[Ax 7.1]` `[Ax 7.4]`

> [!definition] Adjoint Riesz representation
> Let $T \in \mathcal L(V, W)$. The **adjoint** of $T$, denoted $T^*$, is the function from $W$ to $V$ defined as follow. Fix $w \in W$. Consider the linear functional on $V$ that maps $v \in V$ to $\langle T(v), w \rangle$. Let $T^*(w)$ be the unique vector in $V$ such that this linear functional is given by taking inner products with $T^*(w)$. In other words, $T^*(w)$ is the unique vector in $V$ such that $$\langle T(v), w \rangle = \langle v, T^*(w) \rangle$$ for all $v \in V$. `[Ax 7.1]`

> [!definition] Parameters
> - $U$: a finite-dimensional inner-product space over $\mathbb F$.
> - $S \in \mathcal L(W, U)$.
> - $a \in \mathbb F$: a scalar.

> [!proposition] Properties of the adjoint — additive, conjugate homogeneous, involutive, reverses products
> The function $T \rightarrow T^*$ has the following properties:
> - **Additivity**: $(S + T)^* = S^* + T^*$ for all $S, T \in \mathcal L(V, W);$
> - **Conjugate Homogeneity**: $(aT)^* = \overline{a} T^*$ for all $a \in \mathbb F$ and $T \in \mathcal L(V, W)$;
> - **Adjoint of adjoint**: $(T^*)^* = T$ for all $T \in \mathcal L(V, W)$;
> - **Identity**: $I^* = I$, where $I$ is the identity operator in $V$;
> - **Products**: $(ST)^* = T^* S^*$ for all $T \in \mathcal L(V, W)$ and $S \in \mathcal L(W, U)$.
>
> `[Ax 7.5]`

> [!proposition] Null space and range of $T^*$
> Suppose $T \in \mathcal L(V, W)$. Then
> 1. $\text{null } T^* = (\text{range } T)^\perp$;
> 2. $\text{range } T^* = (\text{null } T)^\perp$;
> 3. $\text{null } T = (\text{range } T^*)^\perp$;
> 4. $\text{range } T = (\text{null } T^*)^\perp$.
>
> `[Ax 7.6]`

> [!definition] Conjugate Transpose
> The **conjugate transpose** of an $m$-by-$n$ matrix is the $n$-by-$m$ matrix obtained by interchanging the rows and columns and then taking the complex conjugate of each entry. `[Ax 7.7]`

> [!definition] Parameters
> - $(e_1, \dots, e_n)$: an orthonormal basis of $V$.
> - $(f_1, \dots, f_m)$: an orthonormal basis of $W$.

> [!proposition] The matrix of $T^*$ is the conjugate transpose — for orthonormal bases
> Suppose $T \in \mathcal L(V, W)$. If $(e_1, \dots, e_n)$ is an orthonormal basis of $V$ and $(f_1, \dots, f_m)$ is an orthonormal basis of $W$, then $$\mathcal M(T^*, (f_1, \dots, f_m), (e_1, \dots, e_n))$$ is the conjugate transpose of $$\mathcal M(T, (e_1, \dots, e_n), (f_1, \dots, f_m)).$$ `[Ax 7.9]`

> [!remark]
> Let $\lambda$ is an eigenvalue of $T$ then $\overline{\lambda}$ is an eigenvalue of $T^*$.

## Example

### Hermitian Inner Product

> [!example] Euclidean Inner Product
> The **Euclidean inner product** on $\mathbb F^n$ is defined by $$\langle (w_1, \dots, w_n), (z_1, \dots, z_n) \rangle = w_1 \overline{z_1} + \cdots + w_n \overline{z_n}.$$
> For $\mathbb F = \mathbb R$ it is the dot product below. `[LNS16 Ex 9.1.4]`

> [!definition] Parameters
> - $\textbf{v} = (x_1, \dots, x_m) \in V \subset \mathbb R^m$: a vector.
> - $\textbf{w} = (y_1, \dots, y_m) \in V \subset \mathbb R^m$: a vector.

> [!definition] Dot Product
> Let $\textbf{v}, \textbf{w} \in V \subset \mathbb R^{m}$ and write $\textbf{v}$ and $\textbf{w}$ using coordinates as
> - $\textbf{v} = (x_1, x_2, \dots, x_m)$
> - $\textbf{w} = (y_1, y_2, \dots, y_m)$
>
> The **dot product** of $\textbf{v}$ and $\textbf{w}$ is the quantity $$\textbf{v} \cdot \textbf{w} = x_1 y_1 + x_2 y_2 + \dots + x_m y_m.$$
>
> `[LNS16 Ex 9.1.4]`

> [!example] Euclidean Norm
> The **length**, or **Euclidean norm**, of $\textbf{v}$ is the quantity $$||(x_1, \dots, x_m)|| = \sqrt{x_1^2 + x_2^2 + \cdots + x_m^2}.$$ `[LNS16 Eq 9.2.2]`

## Related

### Constructions
- [[knowledge/math/algebra/linear algebra/Operators\|Operators]] — self-adjoint, normal and positive operators, isometries, the spectral theorems and the singular-value decomposition
- [[knowledge/math/algebra/structures/lattice/Lattices\|Lattices]] — Gram–Schmidt and $\det(L) = \prod ||v_i^*||$
- [[knowledge/math/algebra/structures/lattice/LLL Lattice Reduction Algorithm\|LLL Lattice Reduction Algorithm]] — runs on the Gram–Schmidt coefficients $\mu_{ij}$

### Siblings
- [[knowledge/math/algebra/linear algebra/Vector Spaces Over Finite Fields\|Vector Spaces Over Finite Fields]] — the "inner product" on $\mathbb F_q^n$ is bilinear and nondegenerate but has no positivity, so $v \cdot v = 0$ is possible for $v \neq 0$
- [[knowledge/math/calculus/Metric Space\|Metric Space]] — an inner product gives a norm and hence the metric $d(u, v) = ||u - v||$

### Prerequisites
- [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]] — the underlying space
- [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]] — adjoints, orthogonal projections
- [[knowledge/math/algebra/linear algebra/Dual Bases\|Dual Bases]] — linear functionals; the Riesz representation identifies $V'$ with $V$
