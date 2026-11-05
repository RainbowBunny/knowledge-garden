---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/linear-algebra/vector-spaces/","dg-note-properties":{}}
---

Reference:
- `[Ax]` — S. Axler, _Linear Algebra Done Right_, 4th ed. (2024, open access): https://linear.axler.net/ — Chapter 1: Vector Spaces (§1B Definition of Vector Space, §1C Subspaces); Chapter 2: Finite-Dimensional Vector Spaces (§2A Span and Linear Independence, §2B Bases, §2C Dimension). Numbers checked in the chapter PDFs at https://link.springer.com/book/10.1007/978-3-031-41026-0.

## Definition

> [!definition] Parameters
> - $\mathbb F$: a [[knowledge/math/algebra/structures/field/Field\|Field]], the scalars ($\mathbb R$ or $\mathbb C$ in `[Ax]`).
> - $V$: a [[knowledge/math/set theory/Set\|Set]] with an addition $V \times V \to V$, $(u, v) \mapsto u + v$, and a scalar multiplication $\mathbb F \times V \to V$, $(a, v) \mapsto av$.

> [!definition] Vector Space
> Extends:: [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]].
>
> ---
> A **vector space** over $\mathbb F$ — an [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]] whose ring is the field $\mathbb F$ — is a set $V$ along with an addition on $V$ and a scalar multiplication on $V$ such that the following properties hold:
> - **Commutativity Law** for addition: $u + v = v + u$ for all $u, v \in V$.
> - **Associativity Law** for addition and scalar multiplication, for all $u, v, w \in V$ and $a, b \in \mathbb F$:
>     - $(u + v) + w = u + (v + w)$
>     - $(ab)v = a(bv)$
> - **Identity Law** for addition and scalar multiplication:
>     - there exists $0 \in V$ such that $v + 0 = v$ for all $v \in V$;
>     - $1v = v$ for all $v \in V$, where $1$ is the identity of $\mathbb F$.
> - **Inverse Law** for addition: $\forall v \in V, \exists w \in V: v + w = 0$.
> - **Distributive Law**, for all $a, b \in \mathbb F$ and all $u, v \in V$:
>     - $a(u + v) = au + av$
>     - $(a + b)u = au + bu$
>
> `[Ax 1.20]`

## Structure

### Subspace

Specializes [[knowledge/math/algebra/structures/Substructure\|Substructure]].

> [!definition] Parameters
> - $V$: a vector space over $\mathbb F$.
> - $U \subseteq V$: a subset.

> [!definition] Subspaces
> A subset $U$ of $V$ is called a **subspace** of $V$ if $U$ is also a vector space (using the same addition and scalar multiplication as on $V$). `[Ax 1.33]`

> [!proposition] Conditions for a subspace — three checks suffice
> If $U$ is a subset of $V$, then to check that $U$ is a subspace of $V$ we need only check that $U$ satisfies the following:
> - **Additive identity**: $0 \in U$
> - **Closed under addition**: $u, v \in U$ implies $u + v \in U$;
> - **Closed under scalar multiplication**: $a \in \mathbb F$ and $u \in U$ implies $au \in U$.
>
> `[Ax 1.34]`

> [!proposition] Intersection of subspaces — always a subspace
> The intersection of any collection of subspaces of $V$ is a subspace of $V$. `[Ax Ex 1C.11]`

> [!proposition] Union of two subspaces — a subspace only when one contains the other
> The union of two subspaces of $V$ is a subspace if and only if one of the subspaces is contained in the other. `[Ax Ex 1C.12]`

### Sum and Direct Sums

> [!definition] Parameters
> - $U_1, \dots, U_m$: subspaces of $V$.

> [!definition] Sum of Subspaces
> Suppose $U_1, \dots, U_m$ are subspaces of $V$. The **sum** of $U_1, \dots, U_m$, denoted $U_1 + \cdots + U_m$, is defined to be the set of all possible sums of elements of $U_1, \dots, U_m$. More precisely, $$U_1 + \cdots + U_m = \{u_1 + \cdots + u_m : u_1 \in U_1, \dots, u_m \in U_m\}.$$ `[Ax 1.36]`

> [!definition] Direct Sum of Subspaces
> We say that $V$ is the **direct sum** of subspaces $U_1, \dots, U_m$, written $V = U_1 \oplus \cdots \oplus U_m$, if each element of $V$ can be written uniquely as a sum $u_1 + \cdots + u_m$, where each $u_j \in U_j.$ `[Ax 1.41]`

> [!proposition] Condition for a direct sum — $0$ has only the trivial decomposition
> Suppose that $U_1, \dots, U_n$ are subspaces of $V$. Then $V = U_1 \oplus \cdots \oplus U_n$ if and only if both the following conditions hold:
> 1. $V = U_1 + \cdots + U_n$;
> 2. The only way to write $0$ as a sum $u_1 + \cdots + u_n$, where each $u_j \in U_j$, is by taking all the $u_j$'s equal to $0$.
>
> `[Ax 1.45]`

> [!definition] Parameters
> - $U, W$: subspaces of $V$.

> [!proposition] Direct sum of two subspaces — the intersection is $\{0\}$
> Suppose that $U$ and $W$ are subspaces of $V$. Then $V = U \oplus W$ if and only if
> - $V = U + W$, and
> - $U \cap W = \{0\}$.
>
> `[Ax 1.46]`

### Span and Linear Independence

> [!definition] Parameters
> - $\textbf{v}_1, \dots, \textbf{v}_k \in V$: vectors.
> - $\alpha_1, \dots, \alpha_k \in \mathbb F$: scalars.

> [!definition] Linear Combinations
> Let $\textbf{v}_1, \textbf{v}_2, \cdots, \textbf{v}_k \in V$. A **linear combination** of $\textbf{v}_1, \textbf{v}_2, \cdots, \textbf{v}_k \in V$ is any vector of the form $$\textbf{w} = \alpha_1 \textbf{v}_1 + \alpha_2 \textbf{v}_2 + \cdots + \alpha_k \textbf{v}_k \quad \text{with } \alpha_1, \cdots, \alpha_k \in \mathbb F.$$
> The collection of all such linear combinations, $$\{\alpha_1 \textbf{v}_1 + \cdots + \alpha_k \textbf{v}_k : \alpha_1, \dots, \alpha_k \in \mathbb F\},$$ is called the **span** of $\{\textbf{v}_1, \dots, \textbf{v}_k\}.$
>
> `[Ax 2.2]` `[Ax 2.4]`

> [!definition] Finite-Dimensional
> A vector space is called **finite dimensional** if some list of vectors in it spans the space.
> A vector space that is not finite dimensional is called **infinite dimensional**.
>
> `[Ax 2.9]`

> [!definition] Linear Independence
> A set of vectors $\textbf{v}_1, \textbf{v}_2, \cdots, \textbf{v}_k \in V$ is **(linearly) independent** if the only way to get $$\alpha_1 \textbf{v}_1 + \alpha_2 \textbf{v}_2 + \cdots + \alpha_k \textbf{v}_k = 0$$ is to have $\alpha_1 = \alpha_2 = \cdots = \alpha_k = 0$. The set is **(linearly) dependent** if there is a combination with at least one $\alpha \neq 0$. `[Ax 2.15]`

> [!definition] Parameters
> - $(v_1, \dots, v_m)$: a list of vectors in $V$.

> [!lemma] Linear dependence lemma — a dependent list has a vector in the span of the earlier ones
> If $(v_1, \dots, v_m)$ is linearly dependent in $V$ and $v_1 \neq 0$, then there exists $j \in \{2, \dots, m\}$ such that the following hold:
> 1. $v_j \in \text{span}(v_1, \dots, v_{j - 1});$
> 2. If the $j^{\text{th}}$ term is removed from $(v_1, \dots, v_m)$, the span of the remaining list equals $\text{span}(v_1, \dots, v_m)$.
>
> `[Ax 2.19]` (stated there without $v_1 \neq 0$, allowing $j = 1$ with $\operatorname{span}() = \{0\}$)

> [!theorem] Length of linearly independent list $\leq$ length of spanning list
> In a finite-dimensional vector space, the length of every linearly independent list of vectors is less than or equal to the length of every spanning list of vectors. `[Ax 2.22]`

> [!proposition] Finite-dimensional subspaces — a subspace of a finite-dimensional space is finite-dimensional
> Every subspace of a finite-dimensional vector space is finite dimensional. `[Ax 2.25]`

> [!definition] Parameters
> - $S$: a set of vectors in $V$.
> - $L(S)$: its span.

> [!theorem] Unique representation — $S$ spans each vector of $L(S)$ uniquely iff it spans $0$ uniquely
> A set $S$ spans every vector in $L(S)$ uniquely if and only if $S$ spans the zero vector uniquely. `[Ax §2A, after 2.15]`

> [!definition] Parameters
> - $V_n$: the vector space $\mathbb R^n$.
> - $S = \{A_1, \dots, A_k\}$: a set of vectors in $V_n$.

> [!theorem] $k + 1$ vectors in the span of $k$ independent vectors are dependent
> Let $S = \{A_1, \dots, A_k\}$ be a linearly independent set of $k$ vectors in $V_n$, and let $L(S)$ be the linear span of $S$. Then, every set of $k + 1$ vectors in $L(S)$ is linearly dependent. `[Ax 2.22]`

### Bases

> [!definition] Parameters
> - $\textbf{v}_1, \dots, \textbf{v}_n \in V$: vectors.

> [!definition] Bases
> A **basis** for $V$ is a set of linearly independent vectors $\textbf{v}_1, \dots, \textbf{v}_n$ that span $V$. This is equivalent to saying that every vector $\textbf{w} \in V$ can be written in the form $$\textbf{w} = \alpha_1 \textbf{v}_1 + \alpha_2 \textbf{v}_2 + \cdots + \alpha_n \textbf{v}_n$$ for a **unique** choice of $\alpha_1, \dots, \alpha_n \in \mathbb F$.
>
> `[Ax 2.26]` `[Ax 2.28]`

> [!theorem] Every spanning list contains a basis
> Every spanning list in a vector space can be reduced to a basis of the vector space. `[Ax 2.30]`

> [!corollary] Existence of bases — every finite-dimensional vector space has a basis
> Every finite-dimensional vector space has a basis. `[Ax 2.31]`

> [!theorem] Every linearly independent list extends to a basis
> Every linearly independent list of vectors in a finite-dimensional vector space can be extended to a basis of the vector space. `[Ax 2.32]`

> [!proposition] Every subspace has a complement — $V = U \oplus W$
> Suppose $V$ is finite dimensional and $U$ is a subspace of $V$. Then there is a subspace $W$ of $V$ such that $V = U \oplus W$. `[Ax 2.33]`

> [!definition] Parameters
> - $V \subset \mathbb R^m$: a vector space.
> - $\textbf{v}_1, \dots, \textbf{v}_n$: a basis of $V$.
> - $\textbf{w}_1, \dots, \textbf{w}_n \in V$: vectors.
> - $\alpha_{ij} \in \mathbb R$: the coefficients of $\textbf{w}_i$ in the basis $\textbf{v}_1, \dots, \textbf{v}_n$.

> [!proposition] Bases of a subspace of $\mathbb R^m$ — existence, common size, and the determinant test for a new basis
> Let $V \subset \mathbb R^m$ be a vector space.
> 1. There exists a basis for $V$.
> 2. Any two bases for $V$ have the same number of elements. The number of elements in a basis for $V$ is called the dimension of $V$.
> 3. Let $\textbf{v}_1, \dots, \textbf{v}_n$ be a basis for $V$ and let $\textbf{w}_1, \dots, \textbf{w}_n$ be another set of $n$ vectors in $V$. Write each $\textbf{w}_j$ as a linear combination of the $\textbf{v}_i$, $$
> \begin{aligned}
> \mathbf{w}_1 &= \alpha_{11} \textbf{v}_1 + \alpha_{12} \textbf{v}_2 + \cdots + \alpha_{1n} \textbf{v}_n, \\
> \mathbf{w}_2 &= \alpha_{21} \textbf{v}_1 + \alpha_{22} \textbf{v}_2 + \cdots + \alpha_{2n} \textbf{v}_n, \\
> &\ \vdots \\
> \mathbf{w}_n &= \alpha_{n1} \textbf{v}_1 + \alpha_{n2} \textbf{v}_2 + \cdots + \alpha_{nn} \textbf{v}_n. \\
> \end{aligned}
> $$ Then $\textbf{w}_1, \dots, \textbf{w}_n$ is also a basis for $V$ if and only if the determinant of the matrix $$\begin{pmatrix}
> \alpha_{11} & \alpha_{12} & \cdots & \alpha_{1n} \\
> \alpha_{21} & \alpha_{22} & \cdots & \alpha_{2n} \\
> \vdots & \vdots & \ddots & \vdots \\
> \alpha_{n1} & \alpha_{n2} & \cdots & \alpha_{nn}
> \end{pmatrix}$$ is not equal to $0$.
>
> `[Ax 2.31]` `[Ax 2.34]` (items 1–2)

> [!theorem] Bases of $V_n$ — size $n$, extension, and $n$ independent vectors form a basis
> In a given vector space $V_n$, bases have the following properties:
> 1. Every basis contains exactly $n$ vectors.
> 2. Any set of linearly independent vectors is a subset of some basis.
> 3. Any set of $n$ linearly independent vectors is a basis.
>
> `[Ax 2.34]` `[Ax 2.32]` `[Ax 2.38]`

### Dimension

> [!theorem] Basis length does not depend on the basis
> Any two bases of a finite-dimensional vector space have the same length. `[Ax 2.34]`

> [!definition] Dimension
> The **dimension** of a finite-dimensional vector space is defined to be the length of any basis of the vector space. `[Ax 2.35]`

> [!definition] Parameters
> - $V$: a finite-dimensional vector space.
> - $U$: a subspace of $V$.

> [!proposition] Dimension of a subspace, and lists of the right length
> - If $V$ is finite dimensional and $U$ is a subspace of $V$, then $\dim U \leq \dim V$.
> - If $V$ is finite dimensional, then every spanning list of vectors in $V$ with length $\dim V$ is a basis of $V$.
> - If $V$ is finite dimensional, then every linearly independent list of vectors in $V$ with length $\dim V$ is a basis of $V$.
>
> `[Ax 2.37]` `[Ax 2.42]` `[Ax 2.38]`

> [!definition] Parameters
> - $U_1, U_2$: subspaces of a finite-dimensional vector space.

> [!theorem] Dimension of a sum — $\dim(U_1 + U_2) = \dim U_1 + \dim U_2 - \dim(U_1 \cap U_2)$
> If $U_1$ and $U_2$ are subspaces of a finite-dimensional vector space, then $$\dim(U_1 + U_2) = \dim U_1 + \dim U_2 - \dim(U_1 \cap U_2)$$ `[Ax 2.43]`

> [!definition] Parameters
> - $U_1, \dots, U_m$: subspaces of a finite-dimensional vector space $V$.

> [!proposition] Dimensions that add up give a direct sum
> Suppose $V$ is finite dimensional and $U_1, \dots, U_m$ are subspaces of $V$ such that $$V = U_1 + \cdots + U_m$$ and $$\dim V = \dim U_1 + \cdots + \dim U_m.$$ Then $V = U_1 \oplus \cdots \oplus U_m$. `[Ax Ex 2C.17]`

> [!proposition] Dimension of a sum is at most the sum of dimensions
> If $V$ is finite dimensional and $U_1, \dots, U_m$ are subspaces of $V$, then $$\dim(U_1 + \cdots + U_m) \leq \dim U_1 + \cdots + \dim U_m.$$ `[Ax Ex 2C.17]`

## Related

### Descendants
- [[knowledge/math/algebra/linear algebra/Inner-Product Spaces\|Inner-Product Spaces]] — adds an inner product, hence norms, angles and orthogonality
- [[knowledge/math/algebra/linear algebra/Vector Spaces Over Finite Fields\|Vector Spaces Over Finite Fields]] — $\mathbb F = \mathbb F_q$: finitely many vectors, and the "inner product" is a nondegenerate bilinear form without positivity

### Constructions
- [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]] — the structure-preserving maps; $\mathcal L(V, W)$ is again a vector space
- [[knowledge/math/algebra/linear algebra/Dual Bases\|Dual Bases]] — the dual space $V' = \mathcal L(V, \mathbb F)$
- [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]] — coordinates of vectors and linear maps once bases are chosen

### Siblings
- [[knowledge/math/algebra/structures/lattice/Lattices\|Lattices]] — integer combinations of a basis of $\mathbb R^n$ instead of $\mathbb F$-combinations: a discrete subgroup, not a subspace

### Prerequisites
- [[knowledge/math/algebra/structures/field/Field\|Field]] — the scalars
- [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]] — a vector space is a module over a field
- [[knowledge/math/algebra/structures/Substructure\|Substructure]] — the origin of [[knowledge/math/algebra/linear algebra/Vector Spaces#Subspace\|subspace]]
