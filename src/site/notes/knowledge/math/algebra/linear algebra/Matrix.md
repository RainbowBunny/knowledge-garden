---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/linear-algebra/matrix/","dg-note-properties":{}}
---

Reference:
- `[Ax]` — S. Axler, _Linear Algebra Done Right_, 4th ed. (2024, open access): https://linear.axler.net/ — §3C Matrices, §5A–5C (eigenvalues, upper-triangular matrices). Numbers checked in the chapter PDFs at https://link.springer.com/book/10.1007/978-3-031-41026-0.
- `[Ax2]` — S. Axler, _Linear Algebra Done Right_, 2nd ed. (1997). Not opened; the note follows its order, and the key marks results whose 4th-edition number I could not check.
- `[AxI]` — S. Axler, _Invertibility and Isomorphic Vector Spaces_ (LADR supplement, unnumbered): https://www.linear.axler.net/Invertibility.pdf
- `[LNS16]` — I. Lankham, B. Nachtergaele, A. Schilling, _Linear Algebra As an Introduction to Abstract Mathematics_ (2016), §7.5 Upper Triangular Matrices, LibreTexts edition: https://math.libretexts.org/Bookshelves/Linear_Algebra/Book%3A_Linear_Algebra_(Schilling_Nachtergaele_and_Lankham)
- `[MITg]` — MIT OpenCourseWare 18.700 _Linear Algebra_ (Fall 2013), notes "Gaussian elimination" (2013-10-14): https://www.ocw.mit.edu/courses/18-700-linear-algebra-fall-2013/b144082f6883d02faeec26d7f708c63e_MIT18_700F13_gauss.pdf
- `[Bee]` — R. A. Beezer, _A First Course in Linear Algebra_, Section RREF: https://linear.pugetsound.edu/html/section-RREF.html
- `[Hig22]` — N. J. Higham, _What Is a Circulant Matrix?_ (2022): https://nhigham.com/2022/09/27/what-is-a-circulant-matrix
- `[nLab]` — nLab, _monomial matrix_: https://ncatlab.org/nlab/show/monomial+matrix

## Definition

> [!definition] Parameters
> - $\mathbb F$: a [[knowledge/math/algebra/structures/field/Field\|Field]].
> - $m, n$: positive integers.

> [!definition] Matrix
> An $m$-by-$n$ **matrix** $A$ is a rectangular array of elements of $\mathbb F$ with $m$ rows and $n$ columns; $A_{j, k}$ (or $a_{j, k}$) denotes the entry in row $j$, column $k$. The set of all $m$-by-$n$ matrices with entries in $\mathbb F$ is denoted $\mathbb F^{m, n}$. `[Ax 3.29]` `[Ax 3.39]`

> [!definition] Parameters
> - $V$: a [[knowledge/math/algebra/linear algebra/Vector Spaces\|vector space]].
> - $I \in \mathcal L(V)$: the identity operator.

> [!definition] Identity Matrix
> For a vector space $V$, the identity operator $I \in \mathcal L(V)$ has a diagonal matrix $$\begin{bmatrix}1 & & 0 \\ & \ddots & \\ 0 & & 1\end{bmatrix}.$$ This matrix is called the **identity matrix** and is denoted $I$. `[Ax2]`

> [!definition] Parameters
> - $A$, $B$: square matrices with entries in $\mathbb F$, of the same size.

> [!definition] Invertible Matrix
> A square matrix $A$ (with entries in $\mathbb F$) is called **invertible** if there is a square matrix $B$ of the same size such that $AB = BA = I$, and we call $B$ an **inverse** of $A$. Because the inverse is unique, we use the notation $A^{-1}$ to denote the inverse of $A$. `[Ax2]`

### The Matrix of a Linear Map

> [!definition] Parameters
> - $V$, $W$: vector spaces over $\mathbb F$.
> - $(v_1, \dots, v_n)$: a basis of $V$.
> - $(w_1, \dots, w_m)$: a basis of $W$.
> - $T \in \mathcal L(V, W)$: a [[knowledge/math/algebra/linear algebra/Linear Maps\|linear map]].

> [!definition] Matrix of a Map
> Define $T: \mathbb F^n \rightarrow \mathbb F^m$ by $$T(x_1, \dots, x_n) = (\sum_{k = 1}^n a_{1, k} x_k, \dots, \sum_{k = 1}^n a_{m, k} x_k).$$ The $m$-by-$n$ matrix
> $$\begin{bmatrix}a_{1, 1} & \dots & a_{1, n} \\ \vdots & & \vdots \\ a_{m, 1} & \dots & a_{m, n} \end{bmatrix}$$ is the matrix of $T$ with respect to the bases $(v_1, \dots, v_n)$ and $(w_1, \dots, w_m)$ if $$T(v_k) = \sum_{i = 1}^m a_{i, k} w_i.$$ This matrix is denoted by $\mathcal M(T, (v_1, \dots, v_n), (w_1, \dots, w_m))$.
>
> `[Ax 3.31]`

> [!proposition] Linear maps act like matrix multiplication — $\mathcal M(T(v)) = \mathcal M(T) \mathcal M(v)$
> Suppose $T \in \mathcal L(V, W)$ and $(v_1, \dots, v_n)$ is a basis of $V$ and $(w_1, \dots, w_m)$ is a basis of $W$. Then $$\mathcal M(T(v)) = \mathcal M(T) \mathcal M(v)$$ for every $v \in V$. `[AxI]`

### Null and Range of Matrix

> [!definition] Parameters
> - $A$: an $m \times n$ matrix with columns $c_1, \dots, c_n \in \mathbb F^m$ and rows $r_1, \dots, r_m \in \mathbb F^n$.

> [!definition] Null Space, Range, Column Space, Row Space, Ranks
> The **null space** of an $m \times n$ matrix $A$ is $$\text{Null}(A) = \{v \in \mathbb F^n | Av = 0\}.$$
> The **range** of $A$ is $$\text{Range}(A) = \{Av \in \mathbb F^m | v \in \mathbb F^n\}.$$
> Let $c_j \in \mathbb F^m$ is the $j$-column of $A$, then the **column space** of $A$ is $$\text{Col}(A) = \text{span}(c_1, \dots, c_n) = \text{Range}(A) \subset \mathbb F^m.$$
> The **column rank** of $A$, $c\text{-rank}(A)$, is the dimension of the column space: $$c\text{-rank}(A) = \dim \text{Col}(A) = \dim \text{Range}(A).$$
> Similarly, let $r_i \in \mathbb F^n$ to be the $i$-row of $A$, we can define the **row space** of $A$ is $$\text{Row}(A) = \text{span}(r_1, \dots, r_m) \subset \mathbb F^n$$ and the **row rank**: $$r\text{-rank}(A) = \dim \text{Row}(A).$$
>
> `[MITg §2]`

> [!proposition] Row rank equals column rank; rank–nullity for matrices
> Suppose $A$ is an $m \times n$ matrix.
> 1. The row rank and column rank of $A$ are equal, and equal to the dimension of the range of $A$: $$r\text{-rank}(A) = c\text{-rank}(A) = \dim \text{Range}(A).$$ Their common value is called the rank of $A$, and written $\text{rank}(A)$.
> 2. The dimension of the null space of $A$ plus the rank of $A$ is equal to $n$.
>
> `[MITg Prop 2.7]`

> [!remark]
> $\dim (\text{null}(A^T)) + \text{rank}(A) = m$

> [!definition] Parameters
> - $B$: a $p \times m$ matrix with entries $b_{i, j}$.

> [!proposition] Rows of $BA$ are combinations of rows of $A$
> Suppose $A$ is an $m \times n$ matrix, with rows $r_1, \dots, r_m \in \mathbb F^n$. Suppose $B$ is a $p \times m$ matrix.
> 1. Each row of $BA$ is a linear combination of the rows of $A$. More precisely, the $i$-row of $BA$ is the linear combinations with coefficients given by the $i$-th row of $B$: $$\sum_{j = 1}^m b_{i, j} r_j.$$
> 2. The row space of $BA$ is a subspace of the row space of $A$: $$\text{Row}(BA) \subset \text{Row}(A) \subset \mathbb F^n.$$
> 3. Each $1 \times n$ row vector $r_j$ may be regarded as a linear map $r_j : \mathbb F^n \rightarrow \mathbb F$, $r_j(v) = r_jv$, from column vectors to $\mathbb F$, by matrix multiplication. With this notation, $$Av = \begin{pmatrix}r_1(v) \\ r_2(v) \\ \vdots \\ r_m(v)\end{pmatrix} \in \mathbb F^m.$$
> 4. The null space of $A$ is $$\text{Null}(A) = \{v \in \mathbb F^n | r_j(v) = 0 \quad (j = 1, \dots, m)\} =\{v \in \mathbb F^n | r(v) = 0 \quad (r \in \text{Row}(A))\}.$$
>
> `[MITg Prop 2.9]`

### Row-Echelon Form

> [!definition] Row-Echelon Form
> An $m \times n$ matrix $A$ is said to be in **row-echelon form** if the nonzero entries are restricted to an inverted staircase shape:
> 1. The first nonzero entry in each row is strictly to the **right** of the first nonzero entry in each earlier row; and
> 2. Any rows consisting entirely of zeros must follow any nonzero rows.
>
> `[MITg Def 2.10]`

> [!definition] Parameters
> - $r \leq m$: the number of nonzero rows of a row-echelon matrix $A$.

> [!definition] Pivots
> The **pivots** of a row-echelon matrix are the (finite) positions $(i, j(i))$ of the first nonzero entries of the nonzero row $i = 1, \cdots, r,$ with $r \leq m$ the number of nonzero rows. `[MITg §2]`

> [!definition] Reduced Row-Echelon Form
> The row-echelon matrix $A$ is said to be in **reduced row-echelon form** if in addition
> 1. Each pivot entry is equal to $1$, and
> 2. All the other entries in the column of a pivot are equal to zero.
>
> `[MITg §2]` `[Bee Def RREF]`

> [!definition] Parameters
> - $b \in \mathbb F^m$: a right-hand side.
> - $(f_1, \dots, f_m)$, $(e_1, \dots, e_n)$: the standard bases of $\mathbb F^m$, $\mathbb F^n$.

> [!proposition] Reading off range, row space, null space and solutions from a reduced row-echelon matrix
> Suppose that $A$ is in reduced row-echelon form, with $r$ pivots in the entries $\{(i, j(i)) | 1 \leq i \leq r\}$.
> 1. The first $r$ standard basis vectors $(f_1, \dots, f_r)$ of $\mathbb F^m$ are a basis of $\text{Range}(A)$. This is the column space of $A$, so $c\text{-rank}(A) = r$.
> 2. The (first) $r$ nonzero rows are a basis of the row space of $A$, so $r\text{-rank}(A) = r$.
> 3. For each free variable $x_j$, there is a vector in the null space $$n_j = e_j - \sum_{i = 1}^r a_{i, j} e_{j(i)};$$ the $n - r$ vectors $n_j$, with $x_j$ a free variable, are a basis of $\text{Null}(A)$.
> 4. The equation $Ax = b$ has a solution if and only if $b_i = 0$ for all $i > r$. In that case, one solution is
>     - $x_{j(i)} = b_i$ for $1 \leq i \leq r$,
>     - $x_j = 0$ for $x_j$ a free variable.
> 5. Still assuming that $b_i = 0$ for all $i > r$, the most general solution of $Ax = b$ has arbitrary values $x_j$ for the $n - r$ free variables, and $$x_{j(i)} = b_i - \sum_{j \text{ free}} a_{i, j} x_j \quad (1 \leq i \leq r).$$
>
> `[MITg Prop 2.11]`

### Elementary Row Operation

> [!definition] Parameters
> - $Ax = b$: a system of $m$ equations in $n$ unknowns.
> - $\lambda \neq 0$, $\mu$: scalars.
> - $1 \leq i, j \leq m$: row indices.

> [!definition] Elementary Row Operation
> Suppose $Ax = b$ is a system of $m$ equations in $n$ unknowns. An **elementary row operation** is one of the four procedures below:
> 1. **Multiply** the $i$-th equation by a nonzero scalar $\lambda$ ($M(i; \lambda)$):
>     - $(a_{i1}, \dots, a_{in}) \rightsquigarrow (\lambda a_{i1}, \dots, \lambda a_{in})$
>     - $b_i \rightsquigarrow \lambda b_i$
> 2. **Add** a multiple $\mu$ of the $j$-th equation to a **later** equation $i$, with $1 \leq j < i \leq m$ ($L(i, j; \mu)$):
>     - $(a_{i1}, \dots, a_{in}) \rightsquigarrow (a_{i1} + \mu a_{j1}, \dots, a_{in} + \mu a_{jn})$
>     - $b_i \rightsquigarrow b_i + \mu b_j$
> 3. **Add** a multiple $\mu$ of the $j$-th equation to an **earlier** equation $i$, with $1 \leq i < j \leq m$ ($U(i, j; \mu)$):
>     - $(a_{i1}, \dots, a_{in}) \rightsquigarrow (a_{i1} + \mu a_{j1}, \dots, a_{in} + \mu a_{jn})$
>     - $b_i \rightsquigarrow b_i + \mu b_j$
> 4. **Exchange** equations $i$ and $j$ ($E(i, j)$):
>     - $(a_{j1}, \dots, a_{jn}) \rightsquigarrow (a_{i1}, \dots, a_{in})$
>     - $b_j \rightsquigarrow b_i$
>     - $(a_{i1}, \dots, a_{in}) \rightsquigarrow (a_{j1}, \dots, a_{jn})$
>     - $b_i \rightsquigarrow b_j$
>
> `[MITg Def 3.2]`

> [!definition] The Matrix of Elementary Row Operation
> Each elementary row operation has an associate an $m \times m$ elementary row matrix:
> $$M(i; \lambda) =
> \begin{pmatrix}
> 1 & 0 &        & \cdots  &        & 0\\
> 0 & 1 &        & \cdots  &        & 0\\
>   &   & \ddots &         &        &  \\
> 0 & 0 & \cdots & \lambda & \cdots & 0\\
>   &   &        &         & \ddots &  \\
> 0 & 0 &        &         & \cdots & 1
> \end{pmatrix}$$
> with $\lambda$ appearing in the $(i, i)$ place;
> $$L(i, j; \mu) =
> \begin{pmatrix}
> 1 & 0      &     & \cdots &   &        & 0 \\
> 0 & 1      &     & \cdots &   &        & 0 \\
>   &        &     & \ddots &   &        &   \\
> 0 & \cdots & \mu & \cdots & 1 & \cdots & 0 \\
>   &        &     &        &   & \ddots &   \\
> 0 & 0      &     & \cdots &   &        & 1
> \end{pmatrix}
> $$
> with $\mu$ appearing in the $(i, j)$ position $(i > j)$;
> $$U(i, j; \mu) =
> \begin{pmatrix}
> 1 & 0 &        &   & \cdots &        &        & 0 \\
> 0 & 1 &        &   & \cdots &        &        & 0 \\
>   &   & \ddots &   &        &        &        &   \\
> 0 & 0 & \cdots & 1 & \cdots & \mu    & \cdots & 0 \\
>   &   &        &   &        & \ddots &        &   \\
> 0 & 0 &        &   & \cdots &        &        & 1
> \end{pmatrix}
> $$
> with $\mu$ appearing in the $(i, j)$ position $(i < j)$;
> $$E(i, j) =
> \begin{pmatrix}
> 1 & 0 &        &   & \cdots &   &        & 0\\
> 0 & 1 &        &   & \cdots &   &        & 0\\
>   &   & \ddots &   &        &   &        &  \\
> 0 & 0 & \cdots & 0 & \cdots & 1 & \cdots & 0\\
>   &   &        &   & \ddots &   &\\
> 0 & 0 & \cdots & 1 & \cdots & 0 & \cdots & 0\\
>   &   &        &   &        &   & \ddots &  \\
> 0 & 0 &        &   & \cdots &   &        & 1
> \end{pmatrix}$$
> with the off-diagonal ones appearing in positions $(i, j)$ and $(j, i)\;(i < j)$.
>
> `[MITg §3]`

> [!definition] Parameters
> - $C$: a $p \times m$ matrix.

> [!proposition] Elementary row operations are left multiplications by invertible matrices and keep the solutions
> Suppose that we are give a system of $m$ simultaneous linear equations is $n$ unknowns $Ax = b$.
> 1. Performing an elementary row operation is the same as multiplying $A$ and $b$ on the left by the corresponding elementary matrix.
> 2. Multiplying $A$ and $b$ on the left by any $p \times m$ matrix $C$ can only enlarge the set of solutions. That is, any solution $x$ of $Ax = b$ is also solution of $(CA)x = Cb$.
> 3. The elementary row matrices are all invertible:
>     - $M(i; \lambda)^{-1} = M(i; \lambda^{-1})$
>     - $L(i, j; \mu)^{-1} = L(i, j; -\mu)$
>     - $U(i, j; \mu)^{-1} = U(i, j; -\mu)$
>     - $E(i, j)^{-1} = E(i, j)$
> 4. Elementary row operations do not change the solutions of $Ax = b$.
>
> Consequently any finite sequence of elementary row operations amounts to left multiplication of $A$ and $b$ by an invertible $m \times m$ matrix $L$, and does not change the set of solutions.
>
> `[MITg Prop 3.4]`

> [!proposition] Elementary row operations keep the null space, the row space and the column rank
> Suppose $A$ is an $m \times n$ matrix.
> 1. Elementary row operations do not change the null space $\text{Null}(A) \subset \mathbb F^n$. In particular, they do not change the nullity $\dim \text{Null}(A)$.
> 2. Elementary row operations do not change the row space $\text{Row}(A) \subset \mathbb F^n$. In particular, they do not change the row rank $r\text{-rank}(A)$.
> 3. Applying a sequence of elementary row operations is equivalent to left multiplication of $A$ by an invertible $m \times m$ matrix $L$. The effect of this is to apply $L$ to $\text{Range}(A) \subset \mathbb F^m$: $$\text{Range}(LA) = \text{Col}(LA) = L(\text{Col}(A)) = L(\text{Range}(A)).$$
> 4. Elementary row operations do not change the column rank $c\text{-rank}(A)$.
>
> `[MITg Prop 5.1]`

> [!definition] Parameters
> - $r$: a nonnegative integer.
> - $U \subset \mathbb F^n$: an $r$-dimensional subspace.

> [!theorem] Subspaces of $\mathbb F^n$ correspond to reduced row-echelon matrices
> Suppose $n$ and $r$ are nonnegative integers. There is a one-to-one correspondence between $r$-dimensional subspaces $U \subset \mathbb F^n$, and $r \times n$ matrices $A$ in reduced row-echelon form, with one pivot in each row. `[MITg Thm 5.2]`

### Eigenvalues of Square Matrices

> [!definition] Parameters
> - $A$: an $n$-by-$n$ matrix with entries in $\mathbb F$.

> [!definition] Eigenvalue of a Square Matrices
> Suppose $A$ is an $n$-by-$n$ matrix with entries in $\mathbb F$. A number $\lambda \in \mathbb F$ is called an **eigenvalue** of $A$ if there exists a nonzero $n$-by-$1$ matrix $x$ such that $$Ax = \lambda x.$$ `[Ax2]`

> [!proposition] An operator and its matrix have the same eigenvalues
> Suppose $T \in \mathcal L(V)$ and $A$ is the matrix of $T$ with respect to some basis of $V$. Then the eigenvalues of $T$ are the same as the eigenvalues of $A$. `[Ax2]`

## Property

### Gaussian Elimination

> [!algorithm] Gaussian Elimination via Special Entries (Row Echelon and RREF)
> **Input**
> - A matrix $A \in \mathbb{F}^{m \times n}$
>
> **Output**
> - A reduced row echelon form of $A$
>
> ---
>
> **Part I: Finding Special Entries (Pivot Selection and Clearing Columns)**
> 1. In succession, find $r$ special entries
>    $$
>    (i(1), j(1)), (i(2), j(2)), \ldots, (i(r), j(r))
>    $$
>    such that
>    $$
>    1 \le j(1) < j(2) < \cdots < j(r) \le n,
>    $$
>    $$
>    1 \le i(p) \le m \text{ and all } i(p) \text{ are distinct}.
>    $$
>
> 2. These entries will become the pivots.
>
> 3. Perform row operations of types $M$ and $L$ so that for each $p = 1, \ldots, r$:
>    - The first nonzero entry of row $i(p)$ is $1$, in column $j(p)$.
>    - All entries in column $j(p)$ above row $i(p)$ (except in rows $i(q)$ with $q < p$) are zero.
>    - All entries in column $j(p)$ below row $i(p)$ are zero.
>
> 4. Continue until all entries of $A$ outside rows
>    $$
>    i(1), i(2), \ldots, i(r)
>    $$
>    are zero.
>
> **Theoretical Fact**
> - The row operations used in Part I are of types $M$ (scaling) and $L$ (row addition).
>
> ---
>
> **Part II: Row Reordering (Row Echelon Form)**
> 1. Starting with the matrix obtained from Part I, reorder the rows so that:
>    - Row $i(1)$ becomes row $1$,
>    - Row $i(2)$ becomes row $2$,
>    - $\vdots$
>    - Row $i(r)$ becomes row $r$.
>
> 2. After reordering, the pivots are located at
>    $$
>    (1, j(1)), (2, j(2)), \ldots, (r, j(r)),
>    $$
>    with
>    $$
>    1 \le j(1) < j(2) < \cdots < j(r) \le n.
>    $$
>
> 3. The matrix now satisfies:
>    - The first entry of row $p$ is $1$, in column $j(p)$.
>    - All entries in column $j(p)$ below row $p$ are zero.
>    - All entries of $A$ below rows $1, \ldots, r$ are zero.
>
> **Theoretical Fact**
> - The row operations used in Part II are of type $E$ (row exchanges).
>
> ---
>
> **Part III: Clearing Above the Pivots (Reduced Row Echelon Form)**
> 1. Starting with the row echelon form from Part II, clear all entries above each pivot.
>
> 2. For each $p = 1, \ldots, r$:
>    - The first entry of row $p$ remains $1$, in column $j(p)$.
>    - All other entries in column $j(p)$ are zero.
>
> 3. The resulting matrix satisfies:
>    - All entries of $A$ below rows $1, \ldots, r$ are zero.
>
> **Theoretical Fact**
> - The row operations used in Part III are of type $U$ (row addition).
>
> `[MITg §4]`

> [!theorem] Gaussian elimination — every matrix row-reduces to a unique reduced row-echelon form, $A' = UELA$
> Suppose $A$ is an $m \times n$ matrix with entries in a field $\mathbb F$. Then we can perform a finite sequence of elementary row operations on $A$ to obtain a new $m \times n$ matrix $A'$ in reduced row-echelon form. More precisely, we perform
> 1. At most $m$ row operations of type $M$ interspersed with at most $m(m - 1)/2$ operations of type $L$.
> 2. At most $m(m - 1)/2$ operations of type $E$; then
> 3. At most $m(m - 1)/2$ operations of type $U$.
>
> Consequently, we can write
> - $A' = UELA$
> - $A = L^{-1} E^{-1} U^{-1} A'$
>
> Here $L$ and $L^{-1}$ are $m \times m$ invertible lower-triangular matrices; $E$ and $E^{-1}$ are invertible $m \times m$ permutation matrices; and $U$ and $U^{-1}$ are invertible $m \times m$ upper-triangular matrices with ones on the diagonal. The reduced row echelon matrix $A'$ is unique.
>
> `[MITg Thm 4.8]` `[Bee Thm REMEF]` `[Bee Thm RREFU]`

### Augmented Matrix

> [!definition] Parameters
> - $A$: an $m \times n$ matrix of rank $n$.
> - $I_m$: the $m \times m$ identity matrix.

> [!proposition] Left inverse by row reduction of $(A \mid I_m)$
> Suppose that $A$ is a $m \times n$ matrix of $\text{rank } r = n$ (so that $m \geq n$). Form an augmented matrix $\tilde{A} = (A | I_m)$ of size $m \times (m + n)$. Perform Gaussian elimination: $$\tilde{A} = (A | I_m) \xrightarrow{Gauss} (A' | L)$$ with $$A' = \begin{pmatrix}I_n \\ 0_{(m - n) \times n}\end{pmatrix}$$ and $L$ is the $m \times m$ matrix which is the product of all the elementary row matrices used to reduce $A$. Write $B$ for the $n \times m$ matrix consisting of the first $n$ rows of $L$. Then
> - $LA = A'$
> - $BA = I_n$
>
> and thus we have found the left inverse $B$ of $A$.
>
> `[MITg Prop 6.5]`

## Variant

### Upper-Triangular Matrices

> [!definition] Parameters
> - $V$: a finite-dimensional vector space over $\mathbb F$.
> - $T \in \mathcal L(V)$: an operator.
> - $(v_1, \dots, v_n)$: a basis of $V$.

> [!theorem] Existence of eigenvalues — every operator on a nonzero finite-dimensional complex space has one
> Every operator on a finite-dimensional, nonzero, complex vector space has an eigenvalue. `[Ax 5.19]`

> [!definition] Diagonal
> The **diagonal** of a square matrix consists of the entries along the straight line from the upper left corner to the bottom right corner. (i.e. $a_{1, 1}, a_{2, 2}, \dots, a_{n, n}$) `[Ax 5.37]`

> [!definition] Upper Triangular
> A matrix is called **upper triangular** if all the entries below the diagonal equal $0$. `[Ax 5.38]`

> [!proposition] Conditions for an upper-triangular matrix — invariant initial spans
> Suppose $T \in \mathcal L(V)$ and $(v_1, \dots, v_n)$ is a basis of $V$. Then the following are equivalent:
> 1. The matrix of $T$ with respect to $(v_1, \dots, v_n)$ is upper triangular;
> 2. $T(v_k) \in \text{span}(v_1, \dots, v_k)$ for each $k = 1, \dots, n$;
> 3. $\text{span}(v_1, \dots, v_k)$ is invariant under $T$ for each $k = 1, \dots, n$.
>
> `[Ax 5.39]`

> [!theorem] Over $\mathbb C$, every operator has an upper-triangular matrix
> Suppose $V$ is a complex vector space and $T \in \mathcal L(V)$. Then $T$ has an upper-triangular matrix with respect to some basis of $V$. `[LNS16 Thm 7.5.3]`

> [!proposition] Invertible iff the diagonal of an upper-triangular matrix has no zero
> Suppose $T \in \mathcal L(V)$ has an upper-triangular matrix with respect to some basis of $V$. Then $T$ is invertible if and only if all the entries on the diagonal of that upper-triangular matrix are nonzero. `[LNS16 Prop 7.5.4]`

> [!proposition] Eigenvalues are the diagonal entries of an upper-triangular matrix
> Suppose $T \in \mathcal L(V)$ has an upper-triangular matrix with respect to some basis of $V$. Then the eigenvalues of $T$ consist precisely of the entries on the diagonal of that upper-triangular matrix. `[Ax 5.41]` `[LNS16 Prop 7.5.4]`

### Diagonal Matrices

> [!definition] Diagonal Matrix
> A **diagonal matrix** is a square matrix that is $0$ everywhere except possibly along the diagonal. `[Ax2]`

> [!proposition] Enough eigenvalues implies diagonalizable
> If $T \in \mathcal L(V)$ has $\dim V$ distinct eigenvalues, then $T$ has a diagonal matrix with respect to some basis of $V$. `[Ax2]`

### Block Upper-Triangular Matrices

> [!definition] Parameters
> - $A_1, \dots, A_m$: square matrices.

> [!definition] Block Upper-Triangular Matrix
> A **block upper-triangular matrix** is a square matrix of the form $$\begin{bmatrix}A_1 & & * \\ & \ddots & \\ 0 & & A_m\end{bmatrix},$$ where $A_1, \dots, A_m$ are square matrices lying along the diagonal. `[Ax2]`

> [!theorem] Real operators are block upper-triangular with $1 \times 1$ and eigenvalue-free $2 \times 2$ blocks
> Suppose $V$ is a real vector space and $T \in \mathcal L(V)$. Then there is a basis of $V$ with respect to which $T$ has a block upper-triangular matrix $$\begin{bmatrix}A_1 & & * \\ & \ddots & \\ 0 & & A_m\end{bmatrix}.$$ where each $A_j$ is a $1$-by-$1$ matrix or a $2$-by-$2$ matrix with no eigenvalues. `[Ax2]`

### Circulant Matrix

> [!definition] Circulant Matrix
> A square matrix where each row is a cyclic shift to the right of the previous row. `[Hig22]`

### Monomial Matrix

> [!definition] Parameters
> - $D$, $D_1$: diagonal matrices.
> - $P$: a permutation matrix.

> [!definition] Monomial Matrix
> A monomial matrix is a square matrix with exactly one nonzero entry in each row and column. A monomial matrix $M$ can be written either in the form $DP$ or the form $PD_1$, where $D$ and $D_1$ are diagonal matrices and $P$ is a permutation matrix. `[nLab]` (definition; the factorizations reflect the description of the monomial matrices as $S_n \ltimes (\mathbb F^*)^n$ there)

## Related

### Constructions
- [[knowledge/math/algebra/structures/ring/example/Matrix Ring\|Matrix Ring]] — the $n \times n$ matrices over a ring form a ring under $+$ and matrix multiplication
- [[knowledge/math/algebra/structures/group/example/Matrix Group\|Matrix Group]] — $\mathrm{GL}_n$, the invertible matrices under multiplication
- [[knowledge/math/algebra/linear algebra/Kronecker Product\|Kronecker Product]] — the block matrix $A \otimes B$ built from two matrices

### Siblings
- [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]] — a matrix is a linear map $\mathbb F^n \to \mathbb F^m$ once bases are fixed; the matrix depends on the bases, the map does not

### Prerequisites
- [[knowledge/math/algebra/structures/field/Field\|Field]] — the entries
- [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]] — $\mathbb F^n$, span, dimension
- [[knowledge/math/algebra/linear algebra/Eigenvalues and Eigenvectors\|Eigenvalues and Eigenvectors]] — the upper-triangular and diagonal forms are statements about eigenvalues
