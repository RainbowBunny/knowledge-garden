---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/linear-algebra/operators/","dg-note-properties":{}}
---

Reference:
- `[Ax]` — S. Axler, _Linear Algebra Done Right_, 4th ed. (2024, open access): https://linear.axler.net/ — §5A–5B, Chapter 7: Operators on Inner Product Spaces (§7A Self-Adjoint and Normal Operators, §7B Spectral Theorem, §7C Positive Operators), Chapter 8: Operators on Complex Vector Spaces (§8A Generalized Eigenvectors and Nilpotent Operators, §8B Generalized Eigenspace Decomposition, §8C Consequences of Generalized Eigenspace Decomposition). Numbers checked in the chapter PDFs at https://link.springer.com/book/10.1007/978-3-031-41026-0 (readable up to 7.39 and 8.45).
- `[Ax2]` — S. Axler, _Linear Algebra Done Right_, 2nd ed. (1997), Chapters 7–8. Not opened; the note follows its order, and the key marks results whose 4th-edition number I could not check.
- `[LNS16]` — I. Lankham, B. Nachtergaele, A. Schilling, _Linear Algebra As an Introduction to Abstract Mathematics_ (2016), §11.6 Polar decomposition, §11.7 Singular-value decomposition, LibreTexts edition: https://math.libretexts.org/Bookshelves/Linear_Algebra/Book%3A_Linear_Algebra_(Schilling_Nachtergaele_and_Lankham)

## Definition

> [!definition] Parameters
> - $V$: a finite-dimensional [[knowledge/math/algebra/linear algebra/Vector Spaces\|vector space]] over $\mathbb F$ ($\mathbb R$ or $\mathbb C$).

> [!definition] Operator
> An **operator** on $V$ is a linear map from $V$ to itself; the operators on $V$ form $\mathcal L(V)$ ([[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]]). `[Ax 5.1]`

### Self-Adjoint and Normal Operators

> [!definition] Parameters
> - $V$: a finite-dimensional [[knowledge/math/algebra/linear algebra/Inner-Product Spaces\|inner-product space]] over $\mathbb F$.
> - $T \in \mathcal L(V)$: an operator.
> - $T^*$: its adjoint.

> [!definition] Self-Adjoint
> An operator $T \in \mathcal L(V)$ is called **self-adjoint** if $T = T^*$. `[Ax 7.10]`

> [!proposition] Eigenvalues of self-adjoint operators are real
> Every eigenvalue of a self-adjoint operator is real. `[Ax 7.12]`

> [!proposition] Over $\mathbb C$, $\langle Tv, v \rangle = 0$ for all $v$ forces $T = 0$
> If $V$ is a complex inner-product space and $T$ is an operator on $V$ such that $$\langle T(v), v \rangle = 0$$ for all $v \in V$, then $T = 0$. `[Ax 7.13]`

> [!corollary] Over $\mathbb C$, $T$ is self-adjoint iff $\langle Tv, v \rangle$ is real for every $v$
> Let $V$ be a complex inner-product space and let $T \in \mathcal L(V)$. Then $T$ is self-adjoint if and only if $$\langle T(v), v \rangle \in \mathbb R$$ for every $v \in V$. `[Ax 7.14]`

> [!proposition] Self-adjoint with $\langle Tv, v \rangle = 0$ for all $v$ forces $T = 0$
> If $T$ is a self-adjoint operator on $V$ such that $$\langle T(v), v \rangle = 0$$ for all $v \in V$, then $T = 0$. `[Ax 7.16]`

> [!remark]
> Let $S, T$ be self-adjoint, then:
> - $(S + T)^* = S^* + T^* = S + T$
> - $(aT)^* = \overline{a}T^* = \overline{a}T$
>
> The set of self-adjoint operators on a real inner-product space $V$ is a subspace of $\mathcal L(V)$.
>
> The set of self-adjoint operators on a complex inner-product space $V \neq \{0\}$ is not a subspace of $\mathcal L(V)$: for self-adjoint $T \neq 0$, $(iT)^* = -iT \neq iT$. It is closed under addition and under real scalars only. `[Ax 7.5]`

> [!definition] Normal Operator
> An operator $T \in \mathcal L(V)$ is called **normal** if it commutes with its adjoint: $$TT^* = T^* T.$$ `[Ax 7.18]`

> [!proposition] $T$ is normal iff $||Tv|| = ||T^*v||$ for all $v$
> An operator $T \in \mathcal L(V)$ is normal if and only if $$||T(v)|| = ||T^*(v)||$$ for all $v \in V$. `[Ax 7.20]`

> [!corollary] Eigenvectors of a normal $T$ are eigenvectors of $T^*$, with conjugate eigenvalue
> Suppose $T \in \mathcal L(V)$ is normal. If $v \in V$ is an eigenvector of $T$ with eigenvalue $\lambda \in \mathbb F$, then $v$ is also an eigenvector of $T^*$ with eigenvalue $\overline{\lambda}$. `[Ax 7.21]`

> [!corollary] Eigenvectors of a normal operator for distinct eigenvalues are orthogonal
> If $T \in \mathcal L(V)$ is normal, then eigenvectors of $T$ corresponding to distinct eigenvalues are orthogonal. `[Ax 7.22]`

> [!example]
> If $T \in \mathcal L(V)$ is normal, then:
> 1. $\text{range } T = \text{range } T^*.$ `[Ax 7.21]`
> 2. For every positive integer $k$:
>     - $\text{null } T^k = \text{null } T$
>     - $\text{range } T^k = \text{range } T$

> [!proposition] A normal operator on a complex space is self-adjoint iff its eigenvalues are real
> A normal operator on a complex inner-product space is self-adjoint if and only if all its eigenvalues are real. `[Ax2]`

### Positive Operators

> [!definition] Positive Operator
> An operator $T \in \mathcal L(V)$ is called **positive** if $T$ is self-adjoint and $$\langle T(v), v \rangle \geq 0$$ for all $v \in V$. `[Ax 7.34]`

> [!definition] Parameters
> - $S \in \mathcal L(V)$: an operator.

> [!definition] Square Root
> An operator $S$ is called a **square root** of an operator $T$ if $S^2 = T$. `[Ax 7.36]`

> [!theorem] Characterization of positive operators
> Let $T \in \mathcal L(V)$. Then the following are equivalent:
> 1. $T$ is positive;
> 2. $T$ is self-adjoint and all the eigenvalues of $T$ are nonnegative;
> 3. $T$ has a positive square root;
> 4. $T$ has a self-adjoint square root;
> 5. There exists an operator $S \in \mathcal L(V)$ such that $T = S^* S$.
>
> `[Ax 7.38]` (which adds: $T$ has a diagonal matrix with nonnegative entries in some orthonormal basis)

> [!proposition] Each positive operator has exactly one positive square root
> Every positive operator on $V$ has a unique positive square root. `[Ax 7.39]`

> [!remark]
> 1. Sum of any two positive operators on $V$ is positive.
> 2. If $T \in \mathcal L(V)$ is positive, then so is $T^k$ for every positive integer $k$.

> [!proposition] A positive operator is invertible iff $\langle Tv, v \rangle > 0$ for all $v \neq 0$
> Suppose that $T$ is a positive operator on $V$. Then, $T$ is invertible if and only if $$\langle Tv, v \rangle > 0$$ for every $v \in V \backslash \{0\}$. `[Ax2]`

> [!definition] Parameters
> - $S \in \mathcal L(V)$: an isometry.
> - $R \in \mathcal L(V)$: a positive operator.

> [!proposition] Uniqueness of the positive factor — $T = SR$ forces $R = \sqrt{T^* T}$
> For $T \in \mathcal L(V)$, $S \in \mathcal L(V)$ is an isometry, and $R \in \mathcal L(V)$ is a positive operator such that $T = SR$, then $$R = \sqrt{T^* T}$$ `[Ax2]`

> [!proposition] Polar decomposition with uniqueness — the isometry is unique iff $T$ is invertible
> $T \in \mathcal L(V)$ is invertible if and only if there exists a **unique isometry** $S$ such that $$T = S \sqrt{T^* T}.$$ `[Ax2]`

### Isometries

> [!definition] Isometry
> An operator $S \in \mathcal L(V)$ is called an **isometry** if $$||S(v)|| = ||v||$$ for all $v \in V$. In other words, an operator is an isometry if it preserves norms. `[Ax2]`

> [!theorem] Characterization of isometries
> Suppose $S \in \mathcal L(V)$. Then the following are equivalent:
> 1. $S$ is an isometry;
> 2. $\langle S(u), S(v) \rangle = \langle u, v \rangle$ for all $u, v \in V$;
> 3. $S^* S = I$;
> 4. $(S(e_1), \dots, S(e_n))$ is orthonormal whenever $(e_1, \dots, e_n)$ is an orthonormal list of vectors in $V$;
> 5. There exists an orthonormal basis $(e_1, \dots, e_n)$ of $V$ such that $(S(e_1), \dots, S(e_n))$ is orthonormal;
> 6. $S^*$ is an isometry;
> 7. $\langle S^*(u), S^*(v) \rangle = \langle u, v \rangle$ for all $u, v \in V$;
> 8. $S S^* = I$;
> 9. $(S^*(e_1), \dots, S^*(e_n))$ is orthonormal whenever $(e_1, \dots, e_n)$ is an orthonormal list of vectors in $V$;
> 10. There exists an orthonormal basis $(e_1, \dots, e_n)$ of $V$ such that $(S^*(e_1), \dots, S^*(e_n))$ is orthonormal.
>
> `[Ax2]`

> [!remark]
> Every isometry is normal.

> [!theorem] Complex isometries — an orthonormal eigenbasis with eigenvalues of absolute value $1$
> Suppose $V$ is a complex inner-product space and $S \in \mathcal L(V)$. Then $S$ is an isometry if and only if there is an orthonormal basis of $V$ consisting of eigenvectors of $S$ all of whose corresponding eigenvalues have absolute value $1$. `[Ax2]`

> [!theorem] Real isometries — block diagonal with $\pm 1$ and rotation blocks
> Suppose that $V$ is a real inner-product space and $S \in \mathcal L(V)$. Then $S$ is an isometry if and only if there is an orthonormal basis of $V$ with respect to which $S$ has a block diagonal matrix where each block on the diagonal is a $1$-by-$1$ matrix containing $1$ or $-1$ or a $2$-by-$2$ matrix of the form $$\begin{bmatrix}\cos \theta & -\sin \theta \\ \sin \theta & \cos \theta \end{bmatrix},$$ with $\theta \in (0, \pi)$. `[Ax2]`

> [!remark]
> The product of two isometries is an isometry.

### Generalized Eigenvectors

> [!definition] Parameters
> - $V$: a finite-dimensional vector space over $\mathbb F$.
> - $T \in \mathcal L(V)$: an operator.
> - $\lambda$: an eigenvalue of $T$.

> [!definition] Generalized Eigenvector
> Suppose $T \in \mathcal L(V)$ and $\lambda$ is an eigenvalue of $T$. A vector $v \in V$ is called a **generalized eigenvector** of $T$ corresponding to $\lambda$ if $v \neq 0$ and $$(T - \lambda I)^j v = 0$$ for some positive integer $j$. `[Ax 8.8]`

> [!definition] Parameters
> - $m$: a nonnegative integer.

> [!proposition] Once two null spaces in the chain agree, all later ones agree
> If $T \in \mathcal L(V)$ and $m$ is a nonnegative integer such that $\text{null } T^m = \text{null } T^{m + 1}$, then $$\text{null } T^0 \subset \text{null } T^1 \subset \cdots \subset \text{null } T^m = \text{null } T^{m + 1} = \text{null } T^{m + 2} = \cdots .$$ `[Ax 8.1]` `[Ax 8.2]`

> [!proposition] Null spaces stop growing at $\dim V$
> If $T \in \mathcal L(V)$, then $$\text{null } T^{\dim V} = \text{null } T^{\dim V + 1} = \text{null } T^{\dim V + 2} = \cdots.$$ `[Ax 8.3]`

> [!corollary] Generalized eigenvectors for $\lambda$ — the nonzero vectors of $\text{null }(T - \lambda I)^{\dim V}$
> Suppose $T \in \mathcal L(V)$ and $\lambda$ is an eigenvalue of $T$. Then the set of generalized eigenvectors of $T$ corresponding to $\lambda$, together with $0$, equals $\text{null }(T - \lambda I)^{\dim V}$. `[Ax 8.19]` `[Ax 8.20]`

> [!definition] Nilpotent
> An operator is called **nilpotent** if some power of it equals $0$. `[Ax 8.14]`

> [!definition] Parameters
> - $N \in \mathcal L(V)$: a nilpotent operator.

> [!corollary] A nilpotent operator raised to $\dim V$ is $0$
> Suppose $N \in \mathcal L(V)$ is nilpotent. Then $N^{\dim V} = 0$. `[Ax 8.16]`

> [!definition] Parameters
> - $S \in \mathcal L(V)$: an operator.

> [!proposition] $ST$ nilpotent implies $TS$ nilpotent
> If $ST$ is nilpotent, then $TS$ is nilpotent. `[Ax2]`

> [!proposition] Ranges stop shrinking at $\dim V$
> If $T \in \mathcal L(V)$, then $$\text{range } T^{\dim V} = \text{range } T^{\dim V + 1} = \text{range } T^{\dim V + 2} = \cdots.$$ `[Ax2]`

## Property

### The Spectral Theorem

> [!definition] Parameters
> - $V$: a finite-dimensional [[knowledge/math/algebra/linear algebra/Inner-Product Spaces\|inner-product space]] over $\mathbb F$.
> - $T \in \mathcal L(V)$: an operator.

> [!theorem] Complex spectral theorem — an orthonormal eigenbasis exists iff $T$ is normal
> Suppose that $V$ is a complex inner-product space and $T \in \mathcal L(V)$. Then $V$ has an **orthonormal basis** consisting of eigenvectors of $T$ if and only if $T$ is normal. `[Ax 7.31]`

> [!definition] Parameters
> - $\alpha, \beta \in \mathbb R$ with $\alpha^2 < 4\beta$.

> [!lemma] Invertible quadratic expressions — $T^2 + \alpha T + \beta I$ is invertible for self-adjoint $T$
> Suppose $T \in \mathcal L(V)$ is self-adjoint. If $\alpha, \beta \in \mathbb R$ are such that $\alpha^2 < 4\beta$, then $$T^2 + \alpha T + \beta I$$ is invertible. `[Ax 7.26]`

> [!lemma] Self-adjoint operators have eigenvalues
> Suppose $V \neq \{0\}$ and $T \in \mathcal L(V)$ is self-adjoint. Then $T$ has an eigenvalue. `[Ax 7.27]` `[Ax 5.27]`

> [!theorem] Real spectral theorem — an orthonormal eigenbasis exists iff $T$ is self-adjoint
> Suppose that $V$ is a real inner-product space and $T \in \mathcal L(V)$. Then $V$ has an **orthonormal basis** consisting of eigenvectors of $T$ if and only if $T$ is self-adjoint. `[Ax 7.29]`

> [!definition] Parameters
> - $\lambda \in \mathbb F$.
> - $\epsilon > 0$.

> [!proposition] Approximate eigenvalue by nearby eigenvalue — a near-eigenvector gives an eigenvalue within $\epsilon$
> Suppose $T \in \mathcal L(V)$ is self-adjoint, $\lambda \in \mathbb F$, and $\epsilon > 0$. Then, if there exists $v \in V$ such that $||v|| = 1$ and $$||T(v) - \lambda v|| < \epsilon$$ then $T$ has an eigenvalue $\lambda'$ such that $|\lambda - \lambda'| < \epsilon$. `[Ax2]`

> [!definition] Parameters
> - $\lambda_1, \dots, \lambda_m$: the distinct eigenvalues of $T$.

> [!corollary] Orthogonal eigenspace decomposition
> Suppose that $T \in \mathcal L(V)$ is self-adjoint (or that $\mathbb F = \mathbb C$ and that $T \in \mathcal L(V)$ is normal). Let $\lambda_1, \dots, \lambda_m$ denote the distinct eigenvalues of $T$. Then $$V = \text{null }(T - \lambda_1 I) \oplus \cdots \oplus \text{null } (T - \lambda_m I).$$ Furthermore, each vector in each $\text{null } (T - \lambda_j I)$ is orthogonal to all vectors in the other subspaces of this decomposition. `[Ax2]`

> [!definition] Parameters
> - $U$: a finite-dimensional real vector space.
> - $T \in \mathcal L(U)$: an operator.

> [!proposition] A real operator has an eigenbasis iff some inner product makes it self-adjoint
> Suppose $U$ is a finite-dimensional real vector space and $T \in \mathcal L(U)$. Then, $U$ has a basis consisting of eigenvectors of $T$ if and only if there is an inner product on $U$ that makes $T$ into a self-adjoint operator. `[Ax2]`

> [!remark]
> We can define an inner product by choosing a basis and declare it orthonormal.

### Normal Operators on Real Inner-Product Spaces

> [!definition] Parameters
> - $V$: a real inner-product space.
> - $T \in \mathcal L(V)$: an operator.

> [!lemma] Normal but not self-adjoint in dimension $2$ — the matrix is $\begin{bmatrix}a & -b \\ b & a\end{bmatrix}$
> Suppose $V$ is a two-dimensional real inner-product space and $T \in \mathcal L(V)$. Then the following are equivalent:
> 1. $T$ is normal but not self-adjoint;
> 2. The matrix of $T$ with respect to every orthonormal basis of $V$ has the form $$\begin{bmatrix}a & -b \\ b & a\end{bmatrix},$$ with $b \neq 0$;
> 3. The matrix of $T$ with respect to some orthonormal basis of $V$ has the form $$\begin{bmatrix}a & -b \\ b & a\end{bmatrix},$$ with $b > 0$.
>
> `[Ax2]`

> [!definition] Parameters
> - $U$: a subspace of $V$ invariant under $T$.

> [!proposition] Invariant subspaces of a normal operator — $U^\perp$ is invariant and the restrictions are normal
> Suppose $T \in \mathcal L(V)$ is normal and $U$ is a subspace of $V$ that is invariant under $T$. Then
> 1. $U^{\perp}$ is invariant under $T$;
> 2. $U$ is invariant under $T^*$;
> 3. $(T|_U)^* = (T^*)|_U$;
> 4. $T|_U$ is a normal operator on $U$;
> 5. $T|_{U^\perp}$ is a normal operator on $U^\perp$.
>
> `[Ax2]`

> [!definition] Parameters
> - $A_1, \dots, A_m$: square matrices.

> [!definition] Block Diagonal Matrix
> A **block diagonal matrix** is a square matrix of the form $$\begin{bmatrix}A_1 & & 0 \\ & \ddots & \\ 0 & & A_m \end{bmatrix},$$ where $A_1, \dots, A_m$ are square matrices lying along the diagonal and all the other entries of the matrix equal $0$. `[Ax 8.35]`

> [!theorem] Real normal operators — block diagonal with $1 \times 1$ blocks and $\begin{bmatrix}a & -b \\ b & a\end{bmatrix}$ blocks
> Suppose that $V$ is a real inner-product space and $T \in \mathcal L(V)$. Then $T$ is normal if and only if there is an orthonormal basis of $V$ with respect to which $T$ has a block diagonal matrix where each block is a $1$-by-$1$ matrix or a $2$-by-$2$ matrix of the form $$\begin{bmatrix}a & -b \\ b & a\end{bmatrix},$$ with $b > 0$. `[Ax2]`

### Polar and Singular-Value Decompositions

> [!remark]
> Analogy between $\mathbb C$ and $\mathcal L(V)$: If $T$ corresponds to $z$ then $T^*$ corresponds to $\overline{z}$.

> [!definition] Parameters
> - $V$: a finite-dimensional inner-product space.
> - $T \in \mathcal L(V)$: an operator.

> [!theorem] Polar decomposition — $T = S\sqrt{T^* T}$ with $S$ an isometry
> If $T \in \mathcal L(V)$, then there exists an isometry $S \in \mathcal L(V)$ such that $$T = S\sqrt{T^* T}.$$ `[LNS16 Thm 11.6.1]` (complex $V$, $S$ unitary) `[Ax2]`

> [!definition] Singular Values
> Suppose $T \in \mathcal L(V)$. The **singular values** of $T$ are the eigenvalues of $\sqrt{T^* T}$, with each eigenvalue $\lambda$ repeated $\dim \text{null }(\sqrt{T^* T} - \lambda I)$ times. `[Ax2]`

> [!definition] Parameters
> - $s_1, \dots, s_n$: the singular values of $T$.

> [!theorem] Singular-value decomposition — $T(v) = \sum_i s_i \langle v, e_i \rangle f_i$
> Suppose $T \in \mathcal L(V)$ has singular values $s_1, \dots, s_n$. Then there exist orthonormal bases $(e_1, \dots, e_n)$ and $(f_1, \dots, f_n)$ of $V$ such that $$T(v) = \sum_{i = 1}^n s_i \langle v, e_i \rangle f_i$$ for every $v \in V$. `[LNS16 Thm 11.7.1]`

> [!corollary] Adjoint and inverse from the singular-value decomposition
> Suppose $T \in \mathcal L(V)$ has singular-value decomposition given by $$T(v) = \sum_{i = 1}^n s_i \langle v, e_i \rangle f_i$$ for every $v \in V$, where $s_1, \dots, s_n$ are the singular values of $T$ and $(e_1, \dots, e_n)$ and $(f_1, \dots, f_n)$ are orthonormal bases of $V$.
> 1. $T^*(v) = \sum_{i = 1}^n s_i \langle v, f_i \rangle e_i$ for every $v \in V$.
> 2. If $T$ is invertible, then $$T^{-1}(v) = \sum_{i = 1}^n \frac{\langle v, f_i \rangle e_i}{s_i}$$
>
> `[Ax2]`

> [!proposition] Invertibility, rank and isometry read off the singular values
> Suppose $T \in \mathcal L(V)$. Then,
> 1. $T$ is invertible if and only if $0$ is not a singular value of $T$.
> 2. $\dim \text{range } T$ equals the number of nonzero singular values of $T$.
> 3. $T$ is isometry if and only if all the singular values of $T$ equal $1$.
>
> `[Ax2]`

> [!definition] Parameters
> - $T_1, T_2 \in \mathcal L(V)$: operators.

> [!proposition] Same singular values iff $T_1 = S_1 T_2 S_2$ for isometries $S_1, S_2$
> Suppose $T_1, T_2 \in \mathcal L(V)$. Then, $T_1$ and $T_2$ have the same singular values if and only if there exist isometries $S_1, S_2 \in \mathcal L(V)$ such that $T_1 = S_1 T_2 S_2$. `[Ax2]`

> [!definition] Parameters
> - $\hat s$, $s$: the smallest and the largest singular value of $T$.

> [!proposition] Singular values bound the stretching — $\hat{s} ||v|| \leq ||T(v)|| \leq s ||v||$
> Suppose $T \in \mathcal L(V)$. Let $\hat{s}$ denote the smallest singular value of $T$, and let $s$ denote the largest singular value of $T$. Then, $$\hat{s} ||v|| \leq ||T(v)|| \leq s ||v||$$ for every $v \in V$. `[Ax2]`

> [!definition] Parameters
> - $T', T'' \in \mathcal L(V)$: operators.
> - $s'$, $s''$, $s$: the largest singular values of $T'$, $T''$, $T' + T''$.

> [!proposition] Largest singular value is subadditive — $s \leq s' + s''$
> Suppose $T', T'' \in \mathcal L(V)$. Let $s'$ denote the largest singular value of $T'$, let $s''$ denote the largest singular value of $T''$, and let $s$ denote the largest singular value of $T' + T''$. Then, $s \leq s' + s''$. `[Ax2]`

### Decomposition of an Operator

> [!definition] Parameters
> - $V$: a finite-dimensional vector space over $\mathbb F$.
> - $T \in \mathcal L(V)$: an operator.
> - $p \in \mathcal P(\mathbb F)$: a [[knowledge/math/algebra/structures/polynomial/Polynomial\|Polynomial]].

> [!proposition] $\text{null } p(T)$ is invariant under $T$
> If $T \in \mathcal L(V)$ and $p \in \mathcal P(\mathbb F)$, then $\text{null } p(T)$ is invariant under $T$. `[Ax 5.18]`

> [!definition] Parameters
> - $V$: a complex vector space.
> - $\lambda_1, \dots, \lambda_m$: the distinct eigenvalues of $T$.
> - $U_1, \dots, U_m$: the corresponding subspaces of generalized eigenvectors (with $0$).

> [!theorem] Generalized eigenspace decomposition — $V = U_1 \oplus \cdots \oplus U_m$
> Suppose $V$ is a complex vector space and $T \in \mathcal L(V)$. Let $\lambda_1, \dots, \lambda_m$ be the distinct eigenvalues of $T$, and let $U_1, \dots, U_m$ be the corresponding subspaces of generalized eigenvectors. Then
> 1. $V = U_1 \oplus \cdots \oplus U_m$;
> 2. Each $U_j$ is invariant under $T$;
> 3. Each $(T - \lambda_j I)|_{U_j}$ is nilpotent.
>
> `[Ax 8.22]`

> [!corollary] Basis of generalized eigenvectors
> Suppose $V$ is a complex vector space and $T \in \mathcal L(V)$. Then there is a basis of $V$ consisting of generalized eigenvectors of $T$. `[Ax 8.9]`

> [!lemma] Matrix of a nilpotent operator — strictly upper triangular in some basis
> Suppose $N$ is nilpotent operator on $V$. Then there is a basis of $V$ with respect to which the matrix of $N$ has the form $$\begin{bmatrix}0 & & * \\ & \ddots & \\ 0 & & 0 \end{bmatrix}$$ here all entries on and below the diagonal are $0$'s. `[Ax 8.18]`

> [!theorem] Block diagonal matrix with upper-triangular blocks, one eigenvalue per block
> Suppose $V$ is a complex vector space and $T \in \mathcal L(V)$. Let $\lambda_1, \dots, \lambda_m$ be distinct eigenvalues of $T$. Then there is a basis of $V$ with respect to which $T$ has a block diagonal matrix of the form $$\begin{bmatrix} A_1 & & 0 \\ & \ddots & \\ 0 & & A_m\end{bmatrix},$$ where each $A_j$ is an upper-triangular matrix of the form $$\begin{bmatrix}\lambda_j & & * \\ & \ddots & \\ 0 & & \lambda_j \end{bmatrix}.$$ `[Ax 8.37]`

### Square Roots

> [!lemma] Identity plus nilpotent has a square root
> Suppose $N \in \mathcal L(V)$ is nilpotent. Then $I + N$ has a square root. `[Ax 8.39]`

> [!theorem] Over $\mathbb C$, invertible operators have square roots
> Suppose $V$ is a complex vector space. If $T \in \mathcal L(V)$ is invertible, then $T$ has a square root. `[Ax 8.41]`

### The Minimal Polynomial

> [!theorem] Eigenvalues are the zeros of the minimal polynomial
> Let $T \in \mathcal L(V)$. Then the roots of the minimal polynomial of $T$ are precisely the eigenvalues of $T$. `[Ax 5.27]`

> [!proposition] A normal operator has a minimal polynomial without repeated roots
> Suppose $V$ is an inner-product space. If $T \in \mathcal L(V)$ is normal, then the minimal polynomial of $T$ has no repeated root. `[Ax2]`

### Jordan Form

> [!definition] Parameters
> - $N \in \mathcal L(V)$: a nilpotent operator.

> [!definition] Function $m(v)$
> Suppose $N \in \mathcal L(V)$ is nilpotent. For each nonzero vector $v \in V$, let $m(v)$ denote the largest nonnegative integer such that $N^{m(v)}(v) \neq 0$. `[Ax2]`

> [!lemma] Basis adapted to a nilpotent operator — strings $v, Nv, \dots, N^{m(v)}v$
> If $N \in \mathcal L(V)$ is nilpotent, then there exist vectors $v_1, \dots, v_k \in V$ such that
> 1. $(v_1, N(v_1), \dots, N^{m(v_1)}(v_1), \dots, v_k, N(v_k), \dots, N^{m(v_k)}(v_k))$ is a basis of $V$;
> 2. $(N^{m(v_1)}(v_1), \dots, N^{m(v_k)}(v_k))$ is a basis of $\text{null } N$.
>
> `[Ax2]`

> [!definition] Jordan Basis
> Suppose $T \in \mathcal L(V)$. A basis of $V$ is called a **Jordan basis** for $T$ if with respect to this basis $T$ has a block diagonal matrix $$\begin{bmatrix}A_1 & & 0 \\  & \ddots & \\ 0 & & A_m\end{bmatrix},$$ where each $A_j$ is an upper-triangular matrix of the form $$A_j = \begin{bmatrix}\lambda_j & 1 & & 0 \\ & \ddots & \ddots & \\ & & \ddots & 1 \\ 0 & & & \lambda_j\end{bmatrix}$$ `[Ax 8.44]`

> [!theorem] Jordan form — every operator on a complex vector space has a Jordan basis
> Suppose $V$ is a complex vector space. If $T \in \mathcal L(V)$, then there is a basis of $V$ that is a Jordan basis for $T$. `[Ax2]` (nilpotent case: `[Ax 8.45]`)

## Related

### Siblings
- [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]] — upper-triangular, diagonal and block upper-triangular forms, stated for matrices rather than operators
- [[knowledge/math/algebra/linear algebra/Trace, Determinant, and Volume\|Trace, Determinant, and Volume]] — $|\det T| = \det \sqrt{T^* T}$ uses the polar decomposition

### Prerequisites
- [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]] — operators, null spaces, invertibility
- [[knowledge/math/algebra/linear algebra/Eigenvalues and Eigenvectors\|Eigenvalues and Eigenvectors]] — eigenvalues, invariant subspaces, $p(T)$
- [[knowledge/math/algebra/linear algebra/Inner-Product Spaces\|Inner-Product Spaces]] — adjoints, orthonormal bases, orthogonal complements
- [[knowledge/math/algebra/structures/polynomial/Polynomial\|Polynomial]] — minimal and characteristic polynomials
- [[knowledge/math/algebra/structures/ring/Nilpotent Element\|Nilpotent Element]] — nilpotent operators are the nilpotent elements of the ring $\mathcal L(V)$
