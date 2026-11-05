---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/polynomial/polynomial/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 1.3: Polynomial rings.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — §16.4, §17.1–17.3, §18.2, §21.1, §22.1, §23.3 (numbering as in the HTML edition https://judsonbooks.org/aata-files/aata-html/).
- `[Ax]` — S. Axler, _Linear Algebra Done Right_, 4th ed. (2024, open access): https://linear.axler.net/ — Chapter 4: Polynomials; §5B The Minimal Polynomial; §8B Generalized Eigenspace Decomposition.
- `[Ax2]` — S. Axler, _Linear Algebra Done Right_, 2nd ed. (1997), Chapters 8–9 (eigenpairs, operators on real vector spaces). ⚠️ CLAUDE – verify: attribution inferred from the terminology; this edition was not opened.
- `[HPS]` — J. Hoffstein, J. Pipher, J. H. Silverman, _An Introduction to Mathematical Cryptography_ (Springer). ⚠️ CLAUDE – verify: attribution inferred from the content and notation; not opened, section numbers not checked.
- `[Tha22]` — J. Thaler, _Proofs, Arguments, and Zero-Knowledge_ (2022), §2.4: https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf
- `[AK23]` — Z. Aliabadi, T. Kalaycı, _A note on the hull and linear complementary pair of cyclic codes_ (2023), §2: https://arxiv.org/abs/2304.12229
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Definition

> [!definition] Parameters
> - $R$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
> - $x$: an indeterminate.

> [!definition] Polynomial
> A **polynomial** $f(x)$ in the **indeterminate** $x$ and with **coefficients** in $R$ is a **finite** linear combination of non-negative 'powers' of $x$ with coefficients in $R$:
> $$f(x) = \sum_{i \geq 0} a_i x^i = a_0 + a_1 x + a_2 x^2 + \cdots,$$
> where $a_i$ are elements of $R$ (the coefficients) and we require $a_i = 0$ for $i \gg 0$. `[Alu III.1.3]` `[Jud §17.1]`

### Degree

> [!definition] Parameters
> - $f(x) = \sum_{i \geq 0} a_i x^i$: a nonzero polynomial over $R$.

> [!definition] Degree
> The **degree** of a nonzero polynomial $f(x) = \sum_{i \geq 0} a_i x^i$ is the largest integer $d$ for which $a_d \neq 0$. We denoted as $\deg f = d$. `[Alu III.1.3]` `[Jud §17.1]`

> [!definition] Constants
> Polynomial of degree $0$ (together with $0$) are called **constants**. `[Alu III.1.3]`

> [!remark]
> It is sometimes convenient to assign to the polynomial $0$ the degree $-\infty$. `[Jud §17.1]` makes this the definition.

> [!definition] Leading Coefficient
> The **leading coefficient** of polynomial is the coefficient of the highest power of $x$. `[Jud §17.1]`

> [!definition] Monic Polynomial
> A nonzero polynomial whose leading coefficient is equal to $1$ is called a **monic polynomial**. `[Jud §17.1]`

### Polynomial Space

> [!definition] Parameters
> - $\mathbb F$: a [[knowledge/math/algebra/structures/field/Field\|Field]] ($\mathbb R$ or $\mathbb C$ in `[Ax]`).
> - $m \geq 0$: an integer.

> [!definition] Polynomial Space
> $\mathcal P(\mathbb F)$ denotes the vector space of all polynomials with coefficients in $\mathbb F$ and $\mathcal P_m(\mathbb F)$ is the subspace of $\mathcal P(\mathbb F)$ consisting of the polynomials with coefficients in $\mathbb F$ and degree at most $m$. `[Ax]`

### Roots

> [!definition] Parameters
> - $p \in \mathcal P(\mathbb F)$: a polynomial.
> - $\lambda \in \mathbb F$.

> [!definition] Roots
> A number $\lambda \in \mathbb F$ is called a **root** of a polynomial $p \in \mathcal P(\mathbb F)$ if $$p(\lambda) = 0.$$ `[Jud §17.2]` `[Ax Ch. 4]`

### Irreducible

> [!definition] Parameters
> - $\mathbb F$: a [[knowledge/math/algebra/structures/field/Field\|Field]].
> - $p(x) \in \mathbb F[x]$: a polynomial.

> [!definition] Irreducible
> A polynomial $p(x)$ is called **irreducible** (over $\mathbb F$) if
> 1. $\deg(p) > 0$, and
> 2. $p$ can not be written as a product of two polynomials of positive degree.
>
> `[Jud §17.3]`

### Divisibility

> [!definition] Parameters
> - $p, q \in \mathcal P(\mathbb F)$: polynomials.

> [!definition] Divide
> A polynomial $p \in \mathcal P(\mathbb F)$ is said to **divide** a polynomial $q \in \mathcal P(\mathbb F)$ if there exists a polynomial $s \in \mathcal P(\mathbb F)$ such that $q = sp$. `[Jud §17.2]`

> [!definition] Parameters
> - $\mathbb F$: a [[knowledge/math/algebra/structures/field/Field\|Field]].
> - $a, b \in \mathbb F[x]$: polynomials.

> [!definition] Common Divisor
> A **common divisor** of two elements $a, b \in \mathbb F[x]$ is an element $d \in \mathbb F[x]$ that divides both $a$ and $b$. We say that $d$ is a **greatest common divisor** of $a$ and $b$ if every common divisor of $a$ and $b$ also divides $d$. `[Jud §17.2]`

> [!remark]
> `[Jud §17.2]` also requires $d$ to be monic; with that normalisation the greatest common divisor is unique (`[Jud Prop 17.2.5]`). Without it, $d$ is unique up to a nonzero constant factor.

## Property

### Roots and Factors

> [!proposition] Roots give linear factors — $\lambda$ is a root of $p$ iff $z - \lambda$ divides $p$
> Suppose $p \in \mathcal P(\mathbb F)$ is a polynomial with degree $m \geq 1$. Let $\lambda \in \mathbb F$. Then $\lambda$ is a root of $p$ if and only if there is a polynomial $q \in \mathcal P(\mathbb F)$ with degree $m - 1$ such that $$p(z) = (z - \lambda) q(z)$$ for all $z \in \mathbb F$. `[Ax Ch. 4]` `[Jud Cor 17.2.3]`

> [!corollary] Root bound — a polynomial of degree $m$ has at most $m$ roots
> Suppose $p \in \mathcal P(\mathbb F)$ is a polynomial with degree $m \geq 0$. Then $p$ has at most $m$ distinct roots in $\mathbb F$. `[Ax Ch. 4]` `[Jud Cor 17.2.4]`

> [!corollary] Over an infinite field, a polynomial that vanishes everywhere is zero
> Suppose $\mathbb F$ is infinite (e.g. $\mathbb R$ or $\mathbb C$) and $a_0, \dots, a_m \in \mathbb F$. If $$a_0 + a_1 z + a_2 z^2 + \dots + a_m z^m = 0$$ for all $z \in \mathbb F$, then $a_0 = \cdots = a_m = 0$. `[Ax Ch. 4]` `[cf. Jud Cor 17.2.4]`

> [!proposition] Degree and units in $\mathbb F[x]$ — degrees add, the units are the nonzero constants
> Let $\mathbb F$ be a field and let $a$ and $b$ be nonzero polynomial in $\mathbb F[x]$.
> 1. $\deg(a \cdot b) = \deg(a) + \deg(b)$.
> 2. $a$ has a multiplicative inverse in $\mathbb F[x]$ if and only if $a$ is a constant polynomial.
>
> `[Jud Prop 17.1.4]`

### Complex Coefficients

> [!theorem] Fundamental Theorem of Algebra — every nonconstant complex polynomial has a root
> Every nonconstant polynomial with complex coefficients has a root. `[Ax Ch. 4]` `[Jud Thm 23.3.8]`

> [!corollary] Factorization over $\mathbb C$ — a product of linear factors, uniquely
> If $p \in \mathcal P(\mathbb C)$ is a nonconstant polynomial, then $p$ has a unique factorization (except the order of the factors) of the form $$p(z) = c(z - \lambda_1)\dots(z - \lambda_m),$$ where $c, \lambda_1, \dots, \lambda_m \in \mathbb C$. `[Ax Ch. 4]` `[Jud Thm 21.1.25]`

> [!proposition] Conjugation commutes with a real polynomial
> Let $f$ be a polynomial with real coefficients, then $$\overline{f(z)} = f(\overline{z})$$ for every complex $z$. `[Ax Ch. 4]`

### Real Coefficients

> [!proposition] Nonreal roots of a real polynomial come in conjugate pairs
> Suppose $p$ is a polynomial with real coefficients. If $\lambda \in \mathbb C$ is a root of $p$, then so is $\overline \lambda$. `[Ax Ch. 4]`

> [!proposition] Factorization of a quadratic polynomial — real linear factors iff $\alpha^2 \geq 4\beta$
> Let $\alpha, \beta \in \mathbb R$. Then there is a polynomial factorization of the form $$x^2 + \alpha x + \beta = (x - \lambda_1) (x - \lambda_2),$$ with $\lambda_1, \lambda_2 \in \mathbb R$, if and only if $\alpha^2 \geq 4 \beta$. `[Ax Ch. 4]`

> [!theorem] Factorization over $\mathbb R$ — linear factors and irreducible quadratics, uniquely
> If $p \in \mathcal P(\mathbb R)$ is a nonconstant polynomial, then $p$ has a unique factorization (except for the order of the factors) of the form $$p(x) = c(x - \lambda_1) \dots (x - \lambda_m) (x^2 + \alpha_1 x + \beta_1) \dots (x^2 + \alpha_M x + \beta_M),$$ where $c, \lambda_1, \dots, \lambda_m \in \mathbb R$ and $(\alpha_1, \beta_1), \dots, (\alpha_M, \beta_M) \in \mathbb R^2$ with $\alpha_j^2 < 4 \beta_j$ for each $j$. `[Ax Ch. 4]`

### Factorization

> [!proposition] Algebraically closed fields — every polynomial splits into linear factors
> Suppose $\mathbb F$ is a field. The following conditions are equivalent:
> 1. Every polynomial of positive degree in $\mathcal P(\mathbb F)$ is a product of linear factors;
> 2. Every nonzero polynomial in $\mathcal P(\mathbb F)$ is a product of linear factors: $$p(x) = a \prod_{j = 1}^{\deg p} (x - \lambda_j) \quad (\lambda_j \in \mathbb F, 0 \neq a \in \mathbb F).$$
> 3. The irreducible polynomials in $\mathcal P(\mathbb F)$ are those of degree one.
>
> If these equivalent conditions are satisfied, we say that $\mathbb F$ is algebraically closed. `[Jud Thm 21.1.25]`

> [!proposition] Unique factorization — a monic polynomial is a product of monic irreducibles
> Any monic polynomial $p \in \mathcal P(\mathbb F)$ can be written as a product of powers of distinct monic irreducible polynomials $\{q_i \mid 1 \leq i \leq r\}$:
> $$p(x) = \prod_{i = 1}^r q_i(x)^{m_i},$$
> $$\deg p = \sum_{i = 1}^r m_i \deg q_i.$$
> Here $m_i$ and $\deg q_i$ are positive integers, so $r \leq \deg p$. This factorization of $p$ is unique up to rearranging the factors. The irreducible $q_i$ that appear are precisely the irreducible factors of $p$. `[Jud Cor 18.2.23]`

### The Euclidean Algorithm

> [!proposition] The ring $\mathbb F[x]$ is Euclidean — division with remainder by a nonzero polynomial
> Let $\mathbb F$ be a field and let $a$ and $b$ be polynomial in $\mathbb F[x]$ with $b \neq 0$. Then it is possible to write
> $$a = b \cdot k + r$$
> with $k$ and $r$ polynomials, and either
> - $r = 0$, or
> - $\deg r < \deg b$.
>
> We say that $a$ divided by $b$ has quotient $k$ and remainder $r$. `[Jud Thm 17.2.1]` `[Jud Ex 18.2.12]`

> [!proposition] The extended Euclidean algorithm for $\mathbb F[x]$ — $\gcd(a, b) = au + bv$
> Let $\mathbb F$ be a field and let $a$ and $b$ be polynomials in $\mathbb F[x]$ with $b \neq 0$. Then the greatest common divisor $d$ of $a$ and $b$ exists, and there are polynomials $u$ and $v$ in $\mathbb F[x]$ such that $$a \cdot u + b \cdot v = d.$$ `[Jud Prop 17.2.5]`

> [!definition] Parameters
> - $a(x), b(x) \in \mathbb Z[x]$: polynomials whose greatest common divisor in $\mathbb Q[x]$ is $1$.

> [!definition] Resultant
> Let $a(x)$ and $b(x)$ be polynomials with rational coefficients. If their greatest common divisor is $1$, then the extended Euclidean algorithm gives polynomials $A(x)$ and $B(x)$ satisfying $$a(x) A(x) + b(x) B(x) = 1.$$ In general, even if $a(x)$ and $b(x)$ have integer coefficients, the coefficients of $A(x)$ and $B(x)$ will be rational numbers. However, we can multiply the equation by a positive integer to clear the denominator. The smallest positive integer $R$ that can be written in the form $$a(x) A(x) + b(x) B(x) = R \quad \text{with} \; A(x), B(x) \in \mathbb Z[x]$$ is called the **resultant** of $a(x)$ and $b(x)$ and is denoted by $\text{Res}(a(x), b(x))$. `[HPS]`
> ⚠️ CLAUDE – verify: the usual resultant is the determinant of the Sylvester matrix of $a$ and $b$. It lies in $(a, b) \cap \mathbb Z$, but the smallest positive integer of that form (often called the *reduced* resultant) only divides it: for $a = x^2$ and $b = x^2 + 2$ the smallest one is $2 = b - a$, while the Sylvester determinant is $4$. Check which one the source defines.

### The Minimal Polynomial

> [!definition] Parameters
> - $q$: a prime power.
> - $m \geq 1$: an integer.
> - $\alpha \in \mathbb F_{q^m}$.

> [!definition] Minimal Polynomial
> A **minimal polynomial** of an element $\alpha \in \mathbb F_{q^m}$ with respect to $\mathbb F_q$ is a nonzero monic polynomial $f(x)$ of the least degree in $\mathbb F_q[x]$ such that $f(\alpha) = 0$. `[Jud Thm 21.1.10]`

> [!theorem] Existence and uniqueness of the minimal polynomial — it is the monic irreducible polynomial with root $\alpha$
> 1. The minimal polynomial of an element of $\mathbb F_{q^m}$ with respect to $\mathbb F_q$ exists and is unique. It is also irreducible over $\mathbb F_q$.
> 2. If a monic irreducible polynomial $M(x) \in \mathbb F_q[x]$ has $\alpha \in \mathbb F_{q^m}$ as a root, then it is the minimal polynomial of $\alpha$ with respect to $\mathbb F_q$.
>
> `[Jud Thm 21.1.10]`

> [!definition] Parameters
> - $q$: a prime power.
> - $n \geq 1$: an integer with $\gcd(n, q) = 1$.
> - $i \in \mathbb Z_n$.

> [!definition] Cyclotomic Coset
> Let $n$ be co-prime to $q$. The **cyclotomic coset** of $q$ (or **$q$-cyclotomic cosets**) modulo $n$ containing $i$ is defined by $$C_i = \{(i \cdot q^j \pmod n) \in \mathbb Z_n : j = 0, 1, \dots\}.$$
> A subset $\{i_1, \dots, i_t\}$ of $\mathbb Z_n$ is called a **complete set of representatives** of cyclotomic cosets of $q$ modulo $n$ if $C_{i_1}, \dots, C_{i_t}$ are distinct and $\bigcup_{j = 1}^t C_{i_j} = \mathbb Z_n$. `[AK23 §2.2]`

> [!remark]
> 1. It is easy to verify that two cyclotomic cosets are either equal or disjoint. Hence, the cyclotomic cosets partition $\mathbb Z_n$.
> 2. If $n = q^m - 1$ for some $m \geq 1$, each cyclotomic coset contains at most $m$ elements, as $q^m \equiv 1 \pmod{q^m - 1}$.
> 3. It is easy to see that, in the case of $n = q^m - 1$ for some $m \geq 1$, $|C_i| = m$ if $\gcd(i, q^m - 1) = 1$.

> [!theorem] Minimal polynomial of $\alpha^i$ — the product over the cyclotomic coset of $i$
> Let $\alpha$ be a primitive element of $\mathbb F_{q^m}$. Then the minimal polynomial of $\alpha^i$ with respect to $\mathbb F_q$ is $$M^{(i)}(x) := \prod_{j \in C_i} (x - \alpha^j),$$ where $C_i$ is the unique cyclotomic coset of $q$ modulo $q^m - 1$ containing $i$. `[AK23 §2.2]`

> [!remark]
> 1. The degree of the minimal polynomial of $\alpha^i$ is equal to the size of the cyclotomic coset containing $i$.
> 2. $\alpha^i$ and $\alpha^k$ has the same minimal polynomial if and only if $i, k$ are in the same cyclotomic coset.

> [!theorem] Factorization of $x^n - 1$ over $\mathbb F_q$ — one irreducible factor per cyclotomic coset
> Let $n$ be a positive integer with $\gcd(q, n) = 1$. Suppose that $m$ is a positive integer satisfying $n | (q^m - 1)$. Let $\alpha$ be a primitive element of $\mathbb F_{q^m}$ and let $M^{(j)}(x)$ be the minimal polynomial of $\alpha^j$ with respect to $\mathbb F_q$. Let $\{s_1, \dots, s_t\}$ be a complete set of representatives of cyclotomic cosets of $q$ modulo $n$. Then the polynomial $x^n - 1$ has the factorization into monic irreducible polynomials over $\mathbb F_q$:
> $$x^n - 1 = \prod_{i = 1}^t M^{((q^m - 1)s_i / n)}(x).$$
> `[AK23 eq. (1)]`, there stated for a primitive $n$-th root of unity; here that root is $\alpha^{(q^m - 1)/n}$.

> [!corollary] Number of irreducible factors of $x^n - 1$ — the number of cyclotomic cosets
> Let $n$ be a positive integer with $\gcd(q, n) = 1$. Then the number of monic irreducible factors of $x^n - 1$ over $\mathbb F_q$ is equal to the number of cyclotomic cosets of $q$ modulo $n$. `[AK23 eq. (1)]`

### Polynomial Interpolation

> [!theorem] Polynomial Interpolation — $t$ points with distinct $x$-coordinates determine a polynomial of degree $< t$
> Over a field $\mathbb F$, a polynomial of degree at most $t - 1$ is uniquely determined by $t$ points on the polynomial with distinct $x$-coordinates. `[Tha22 Lemma 2.3]` `[Jud Cor 17.2.4]`

> [!lemma] Linearity of Interpolation — $\omega(j^*)$ is a fixed linear combination of the $\omega(j)$
> Let $q$ be a prime, let $J \subseteq \mathbb Z_q$ be a set of size $t$, and let $j^* \in \mathbb Z_q$. Then there is a collection of values $\{\lambda_j\}_{j \in J}$, with each $\lambda_j \in \mathbb Z_q$, such that the following holds:
> - For every polynomial $\omega \in \mathbb Z_q[x]$ of degree at most $t - 1$, we have $$\omega(j^*) = \sum_{j \in J} \lambda_j \omega(j).$$
>
> Moreover, the values $\lambda_j$ for $j \in J$ are efficiently computable given $J$ and $j^*$. `[cf. Tha22 §2.4]`: $\lambda_j$ is the Lagrange basis polynomial of $j$ evaluated at $j^*$.

> [!corollary] Interpolation in the Exponent — $h^{\omega(j^*)}$ from the $h^{\omega(j)}$
> Let $\mathbb G$ be a group of prime order $q$. Let $J \subseteq \mathbb Z_q$ be a set of size $t$, and let $j^* \in \mathbb Z_q$. Given $J, j^*$, as well as a collection of group elements of the form $\{h^{\omega(j)}\}_{j \in J}$, where $h \in \mathbb G$ and $\omega \in \mathbb Z_q[x]$ is a polynomial of degree at most $t - 1$, we can efficiently compute the group element $h^{\omega(j^*)}$. `[cf. Tha22 §2.4]`

### Characteristic Polynomial

> [!proposition] Cyclic subspace of $v_0$ — $p$ is the minimal polynomial of $T$ on $U$
> Suppose $T \in \mathcal L(V)$, and $0 \neq v_0 \in V$. Define $$v_j = T^j v_0.$$ Let $m$ be the smallest positive integer with the property that $$v_m \in \text{span}(v_0, \dots, v_{m - 1}) = U.$$
> Then $(v_0, \dots, v_{m - 1})$ is linearly independent, so there is a unique expression $$v_m = -a_0 v_0 - \cdots - a_{m - 1} v_{m - 1}.$$ Define $$p(x) = x^m + a_{m - 1} x^{m - 1} + \cdots + a_0,$$ a monic polynomial of degree $m \geq 1$ in $\mathcal P(\mathbb F)$.
> 1. The $m$-dimensional subspace $U$ of $V$ is preserved by $T$: $TU \subset U$.
> 2. The linear transformation $$p(T) = T^m + a_{m - 1} T^{m - 1} + \cdots + a_0 I$$ acts by zero on $U$.
> 3. If $z$ is a polynomial and $z(T)$ acts by zero on $U$, then $z$ is divisible by $p$.
> 4. The eigenvalues of $T$ on $U$ are precisely the roots of $p$.
> 5. If $q$ is an irreducible polynomial and $\text{Null}(q(T))$ has a nonzero intersection with $U$, then $q$ divides $p$.
>
> `[cf. Ax §5B]`

#### Operator on Complex Vector Space

> [!theorem] Diagonal of an upper-triangular matrix — $\lambda$ appears $\dim \text{null}(T - \lambda I)^{\dim V}$ times
> Let $T \in \mathcal L(V)$ and $\lambda \in \mathbb F$. Then for every basis of $V$ with respect to which $T$ has an upper-triangular matrix, $\lambda$ appears on the diagonal of the matrix of $T$ precisely $\dim \text{null}(T - \lambda I)^{\dim V}$ times. `[Ax2]`

> [!definition] Parameters
> - $V$: a finite-dimensional vector space over $\mathbb F$.
> - $T \in \mathcal L(V)$: an operator.
> - $\lambda$: an eigenvalue of $T$.

> [!definition] Multiplicity of an Eigenvalue
> Suppose $T \in \mathcal L(V)$. The **multiplicity** of an eigenvalue $\lambda$ of $T$ is defined to be the dimension of the subspace of generalized eigenvectors corresponding to $\lambda$. `[Ax §8B]`

> [!remark]
> The multiplicity of an eigenvalue $\lambda$ of $T$ equals $\dim \text{null} (T - \lambda I)^{\dim V}$.

> [!proposition] Multiplicities add up to $\dim V$ — complex case
> If $V$ is a complex vector space and $T \in \mathcal L(V)$, then the sum of the multiplicities of all the eigenvalues of $T$ equals $\dim V$. `[Ax §8B]`

> [!definition] Parameters
> - $V$: a finite-dimensional complex vector space.
> - $T \in \mathcal L(V)$: an operator.
> - $\lambda_1, \dots, \lambda_m$: the distinct eigenvalues of $T$.
> - $d_j$: the multiplicity of $\lambda_j$.

> [!definition] Characteristic Polynomial of Operators on Complex Vector Space
> Suppose $V$ is a complex vector space and $T \in \mathcal L(V)$. Let $\lambda_1, \dots, \lambda_m$ denote the distinct eigenvalues of $T$. Let $d_j$ denote the multiplicity of $\lambda_j$ as an eigenvalue of $T$. The polynomial $$(z - \lambda_1)^{d_1} \dots (z - \lambda_m)^{d_m}$$ is called the **characteristic polynomial** of $T$. `[Ax §8B]`

> [!theorem] Cayley-Hamilton Theorem — an operator is annihilated by its characteristic polynomial (complex case)
> Suppose that $V$ is a complex vector space and $T \in \mathcal L(V)$. Let $q$ denote the characteristic polynomial of $T$. Then $q(T) = 0$. `[Ax §8B]`

#### Operator on Real Vector Space

> [!definition] Parameters
> - $a, b, c, d \in \mathbb R$: the entries of a $2$-by-$2$ matrix.

> [!definition] Characteristic Polynomial of a $2$-by-$2$ matrix
> The **characteristic polynomial** of a $2$-by-$2$ matrix $\begin{bmatrix}a & c \\ b & d\end{bmatrix}$ is $(x - a)(x - d) - bc$. `[Ax2]`

> [!proposition] Dimension two, no eigenvalues — $p(T)$ is $0$ or invertible
> Suppose $V$ is a real vector space with dimension $2$ and $T \in \mathcal L(V)$ has no eigenvalues. Let $p \in \mathcal P(\mathbb R)$ be a monic polynomial with degree $2$. Suppose $A$ is the matrix of $T$ with respect to some basis of $V$.
> 1. If $p$ equals the characteristic polynomial of $A$, then $p(T) = 0$.
> 2. If $p$ does not equal the characteristic polynomial of $A$, then $p(T)$ is invertible.
>
> `[Ax2]`

> [!theorem] Block upper-triangular form — how often each diagonal block occurs
> Suppose $V$ is a real vector space and $T \in \mathcal L(V)$. Suppose that with respect to some basis of $V$, the matrix of $T$ is $$\begin{bmatrix}A_1 & & * \\ & \ddots & \\ 0 & & A_m\end{bmatrix},$$ where each $A_j$ is a $1$-by-$1$ matrix or a $2$-by-$2$ matrix with no eigenvalues.
> 1. If $\lambda \in \mathbb R$, then precisely $\dim \text{null} (T - \lambda I)^{\dim V}$ of the matrices $A_1, \dots, A_m$ equal the $1$-by-$1$ matrix $[\lambda]$.
> 2. If $\alpha, \beta \in \mathbb R$ satisfy $\alpha^2 < 4\beta$, then precisely $$\frac{\dim \text{null} (T^2 + \alpha T + \beta I)^{\dim V}}{2}$$ of the matrices $A_1, \dots, A_m$ have characteristic polynomial equal to $x^2 + \alpha x + \beta$.
>
> `[Ax2]`

> [!definition] Parameters
> - $V$: a finite-dimensional real vector space.
> - $T \in \mathcal L(V)$: an operator.
> - $(\alpha, \beta) \in \mathbb R^2$.

> [!definition] Eigenpair
> Suppose $V$ is a real vector space and $T \in \mathcal L(V)$. An ordered pair $(\alpha, \beta)$ of real numbers is called an **eigenpair** of $T$ if $\alpha^2 < 4\beta$ and $$T^2 + \alpha T + \beta I$$ is not injective. `[Ax2]`

> [!definition] Parameters
> - $(\alpha, \beta)$: an eigenpair of $T$.

> [!definition] Multiplicity of an Eigenpair
> The **multiplicity** of an eigenpair $(\alpha, \beta)$ of $T$ to be $$\frac{\dim \text{null } (T^2 + \alpha T + \beta I)^{\dim V}}{2}.$$ `[Ax2]`

> [!proposition] Eigenvalue and eigenpair multiplicities add up to $\dim V$ — real case
> If $V$ is a real vector space and $T \in \mathcal L(V)$, then the sum of the multiplicities of all the eigenvalues of $T$ plus the sum of twice the multiplicities of all the eigenpairs of $T$ equals $\dim V$. `[Ax2]`

> [!definition] Parameters
> - $V$: a finite-dimensional real vector space.
> - $T \in \mathcal L(V)$: an operator.
> - $A_1, \dots, A_m$: the diagonal blocks of a block upper-triangular matrix of $T$.

> [!definition] Characteristic Polynomial of Operators on Real Vector Spaces
> Suppose $V$ is a real vector space and $T \in \mathcal L(V)$. With respect to some basis of $V$, $T$ has a block upper-triangular matrix of the form $$\begin{bmatrix}A_1 & & * \\ & \ddots & \\ 0 & & A_m\end{bmatrix}$$ where each $A_j$ is a $1$-by-$1$ or a $2$-by-$2$ matrix with no eigenvalues. We define the **characteristic polynomial** of $T$ to be the product of the characteristic polynomial of $A_1, \dots, A_m$. Explicitly, for each $j$, define $q_j \in \mathcal P(\mathbb R)$ by $$q_j(x) = \begin{cases}x - \lambda &\text{if } A_j = [\lambda]; \\ (x - a)(x - d) - bc &\text{if } A_j = \begin{bmatrix}a & c \\ b & d\end{bmatrix}. \end{cases}$$ Then the characteristic polynomial of $T$ is $$q_1(x) \dots q_m(x).$$ `[Ax2]`

> [!theorem] Cayley-Hamilton Theorem — an operator is annihilated by its characteristic polynomial (real case)
> Suppose $V$ is a real vector space and $T \in \mathcal L(V)$. Let $q$ denote the characteristic polynomial of $T$. Then $q(T) = 0$. `[Ax2]`

> [!theorem] Decomposition of a real operator — generalized eigenspaces and eigenpair spaces
> Suppose $V$ is a real vector space and $T \in \mathcal L(V)$. Let $\lambda_1, \dots, \lambda_m$ be the distinct eigenvalues of $T$, with $U_1, \dots, U_m$ the corresponding sets of generalized eigenvectors. Let $(\alpha_1, \beta_1), \dots, (\alpha_M, \beta_M)$ be the distinct eigenpairs of $T$ and let $V_j = \text{null}(T^2 + \alpha_j T + \beta_j I)^{\dim V}$. Then
> 1. $V = U_1 \oplus \cdots \oplus U_m \oplus V_1 \oplus \cdots \oplus V_M$;
> 2. Each $U_j$ and each $V_j$ is invariant under $T$;
> 3. Each $(T - \lambda_j I) |_{U_j}$ and each $(T^2 + \alpha_j T + \beta_j I) |_{V_j}$ is nilpotent.
>
> `[Ax2]`

### Polynomial Rings

The ring has its own note: [[knowledge/math/algebra/structures/polynomial/Polynomial Ring\|Polynomial Ring]].

> [!definition] Parameters
> - $R$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].

> [!definition] Polynomial Rings
> If $R$ is any ring, we can form a ring of polynomials whose coefficients are taken from the ring $R$. The ring is denoted by $$R[x] = \{a_0 + a_1 x + a_2 x^2 + \cdots + a_n x^n : n \geq 0 \text{ and } a_0, a_1, \cdots, a_n \in R\}.$$ `[Jud §17.1]`

#### Quotient of Polynomial Rings

The quotient ring has its own note: [[knowledge/math/algebra/structures/polynomial/Quotient of Polynomial Ring\|Quotient of Polynomial Ring]].

> [!proposition] Polynomial Congruence Class — each class modulo $m$ has a unique representative of degree $< \deg m$
> Let $\mathbb F$ be field and let $m \in \mathbb F[x]$ be a nonzero polynomial. Then every nonzero congruence class $\overline a \in \mathbb F[x] / (m)$ has a unique representative $r$ satisfying
> - $\deg r < \deg m$,
> - $a \equiv r \pmod m$.
>
> `[Jud Thm 17.2.1]`

> [!corollary] Size of $\mathbb F_p[x] / (m)$ — exactly $p^d$ elements
> Let $\mathbb F_p$ be a finite field and let $m \in \mathbb F_p[x]$ be a nonzero polynomial of degree $d \geq 1$. Then the quotient ring $\mathbb F_p[x] / (m)$ contains exactly $p^d$ elements. `[cf. Jud Thm 17.2.1]`

> [!proposition] Units of $\mathbb F[x] / (m)$ — $\overline a$ is a unit iff $\gcd(a, m) = 1$
> Let $\mathbb F$ be a field and let $a, m \in \mathbb F[x]$ be polynomials with $m \neq 0$. Then $\overline a$ is a unit in the quotient ring $\mathbb F[x] / (m)$ if and only if $$\gcd(a, m) = 1.$$ `[cf. Jud Prop 17.2.5]`

> [!corollary] Irreducible modulus gives a field
> Let $\mathbb F$ be a field and let $m \in \mathbb F[x]$ be an irreducible polynomial. Then the quotient ring $\mathbb F[x] / (m)$ is a field, i.e., every nonzero element of $\mathbb F[x] / (m)$ has a multiplicative inverse. `[Jud Thm 17.3.12]` `[Jud Thm 16.4.1]`

> [!corollary] A field with $p^d$ elements — $\mathbb F_p[x] / (m)$ for $m$ irreducible of degree $d$
> Let $\mathbb F_p$ be a finite field and let $m \in \mathbb F_p[x]$ be an irreducible polynomial of degree $d \geq 1$. Then $\mathbb F_p[x] / (m)$ is a field with $p^d$ elements. `[Jud Thm 17.3.12]` `[Jud Thm 22.1.6]`

> [!definition] Parameters
> - $q$: a prime power.
> - $h(x) = \sum_{i = 0}^k a_i x^i \in \mathbb F_q[x]$: a polynomial of degree $k$.

> [!definition] Reciprocal Polynomial
> Let $h(x) = \sum_{i = 0}^k a_i x^i$ be a polynomial of degree $k (a_k \neq 0)$ over $\mathbb F_q$. Define the **reciprocal polynomial** $h_R(x)$ of $h(x)$ by $$h_R(x) = x^k h(1 / x) = \sum_{i = 0}^k a_{k - i} x^i$$ `[cf. AK23 §2.1]`, where it is further divided by $h(0)$ to make it monic.

> [!remark]
> If $h(x)$ is a divisor of $x^n - 1$, then so is $h_R(x)$. `[AK23, proof of Thm 2]`

### Analogies between $\mathbb Z$ and $F[x]$

| $\mathbb Z$                                               | $F[x]$                                                                                     |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| The integer ring $\mathbb Z$                              | The polynomial ring $F[x]$                                                                 |
| An integer $m$                                            | A polynomial $f(x)$                                                                        |
| A prime number $p$                                        | An irreducible polynomial $p(x)$                                                           |
| $\mathbb Z_m = \{0, 1, \dots, m - 1\}$                    | $F[x]/(f(x)) := \{\sum_{i = 0}^{n - 1} a_i x^i : a_i \in F\}$, where $n = \deg f(x) \geq 1$ |
| $a \oplus b := (a + b \pmod m)$                           | $g(x) \oplus h(x) := (g(x) + h(x) \pmod {f(x)})$                                           |
| $a \odot b := (ab \pmod m)$                               | $g(x) \odot h(x) := (g(x)h(x) \pmod {f(x)})$                                               |
| $\mathbb Z_m$ is a ring                                   | $F[x] / (f(x))$ is a ring                                                                  |
| $\mathbb Z_m$ is a field $\Leftrightarrow$ $m$ is a prime | $F[x] / (f(x))$ is a field $\Leftrightarrow$ $f(x)$ is irreducible                         |

## Variant

### Rational Functions

> [!definition] Parameters
> - $X$: an indeterminate.
> - $a_0, \dots, a_n, b_0, \dots, b_n \in \mathbb C$: the coefficients.

> [!definition] Rational Function
> A **rational function** is a ratio of polynomials $$f(X) = \frac{a_0 + a_1 X + a_2 X^2 + \cdots + a_n X^n}{b_0 + b_1 X + b_2 X^2 + \cdots + b_n X^n}$$
> Any polynomial can be factored completely if we allow complex numbers: $$f(X) = \frac{a(X - \alpha_1)^{e_1} (X - \alpha_2)^{e_2} \cdots (X - \alpha_r)^{e_r}}{b(X - \beta_1)^{d_1} (X - \beta_2)^{d_2} \cdots (X - \beta_s)^{d_s}}$$
> Where $\alpha_1, \cdots, \alpha_r, \beta_1, \cdots, \beta_s$ are distinct numbers. `[HPS]`

> [!definition] Parameters
> - $f(X)$: a rational function, written in the factored form above.

> [!definition] Zeros, Poles, Multiplicities and Divisor
> $\alpha_1, \alpha_2, \cdots, \alpha_r$ are called the **zeros** of $f(X)$.
> $\beta_1, \beta_2, \cdots, \beta_s$ are called the **poles** of $f(X)$.
> The **exponents** $e_1, \cdots, e_r, d_1, \cdots, d_s$ are the associated **multiplicities**.
> The **divisor** of $f(X)$ can be define by the formal sum $$\text{div}(f(X)) = e_1 [\alpha_1] + e_2 [\alpha_2] + \cdots + e_r [\alpha_r] - d_1 [\beta_1] - d_2 [\beta_2] - \cdots - d_s [\beta_s].$$ `[HPS]`

> [!proposition] The divisor turns products into sums
> Let $R(x)$ and $S(x)$ be rational functions:
> $$\text{div}(R(x) S(x)) = \text{div}(R(x)) + \text{div}(S(x)).$$ `[HPS]`

## Example

### Convolution Polynomial Rings

> [!definition] Parameters
> - $N$: a positive integer (the rank).
> - $q$: a positive integer (the modulus).

> [!definition] Ring of Convolution Polynomial
> Fix a positive integer $N$. The **ring of convolution polynomials** (of rank $N$) is the quotient ring $$R = \frac{\mathbb Z [x]}{(x^N - 1)}.$$ Similarly, the ring of convolution polynomials (modulo $q$) is the quotient ring $$R_q = \frac{(\mathbb Z / q \mathbb Z)[x]}{(x^N - 1)}$$ `[HPS]`

> [!proposition] Convolution product — the coefficients of $a \star b$ collect $a_i b_j$ with $i + j \equiv k \pmod N$
> The product of two polynomials $a(x), b(x) \in R$ is given by the formula $$a(x) \star b(x) = c(x) \quad \text{with} \quad c_k = \sum_{i + j \equiv k \pmod N} a_i b_{k - i},$$ where the sum defining $c_k$ is over all $i$ and $j$ between $0$ and $N - 1$ satisfying the condition $i + j \equiv k \pmod N$. The product of two polynomials $a(x), b(x) \in R_q$ is given by the same formula, except that the value of $c_k$ is reduced modulo $q$. `[HPS]`

> [!definition] Parameters
> - $a(x) \in R_q$: a convolution polynomial modulo $q$.

> [!definition] Centered Lift
> Let $a(x) \in R_q$. The **centered lift** of $a(x)$ to $R$ is the unique polynomial $a'(x) \in R$ satisfying $$a'(x) \mod q = a(x)$$ whose coefficients are chosen in the interval $$-\frac{q}{2} < a_i' \leq \frac{q}{2}.$$ `[HPS]`

> [!proposition] Inverses in $R_q$ — $a(x)$ is invertible iff $\gcd(a(x), x^N - 1) = 1$ modulo $q$
> Let $q$ be prime. Then $a(x) \in R_q$ has a multiplicative inverse if and only if $$\gcd(a(x), x^N - 1) = 1 \quad \text{in} \; (\mathbb Z / q \mathbb Z)[x].$$ Also, the inverse $a(x)^{-1} \in R_q$ can computed using the extended Euclidean algorithm to find polynomials $u(x), v(x) \in (\mathbb Z / q \mathbb Z)[x]$ satisfying $$a(x) u(x) + (x^N - 1) v(x) = 1.$$ Then $a(x)^{-1} = u(x)$ in $R_q$. `[HPS]` `[cf. Jud Prop 17.2.5]`

> [!definition] Parameters
> - $f \in R$: a convolution polynomial of rank $N$.
> - $k \geq 0$: an integer.

> [!definition] Rotation
> For $f$ is in a ring of convolution polynomials of rank $N$, the polynomial $x^k \star f$ is called a **rotation** of $f$ because the coefficients have been cyclically rotated $k$ positions. `[HPS]`

> [!proposition] Norm of a convolution product — $\|a \star b\| \approx \|a\| \, \|b\|$ for a random $b$
> Fix a vector $a \in \mathbb R^N$, let $T > 0$, and suppose that $b \in \mathbb R^N$ is a vector whose coefficients are randomly and uniformly chosen in the interval between $-T$ and $T$. Then for most choices of $b$ we expect to have $$||a \star b|| \approx ||a|| \; ||b||$$ `[HPS]`

### Ternary Polynomials

> [!definition] Parameters
> - $d_1, d_2$: positive integers.
> - $R$: the ring of convolution polynomials of rank $N$ (above).

> [!definition] Ternary Polynomials
> For any positive integers $d_1$ and $d_2$, we let $$ \mathcal{T}(d_1,d_2) = \{\, a(x) \in R : \begin{aligned}
> & d_1 \text{ coefficients are } 1,\\
> & d_2 \text{ coefficients are } -1,\\
> & \text{others are } 0\end{aligned}\}.$$ Polynomials in $\mathcal T(d_1, d_2)$ are called **ternary (or trinary) polynomials**. `[HPS]`

## Related

### Descendants
- [[knowledge/math/algebra/structures/polynomial/Multivariate Polynomial\|Multivariate Polynomial]] — several indeterminates $x_1, \dots, x_n$
- [[knowledge/math/algebra/structures/polynomial/Vanishing Polynomial\|Vanishing Polynomial]] — $Z_S(X) = \prod_{a \in S}(X - a)$, zero exactly on a finite set $S$

### Constructions
- [[knowledge/math/algebra/structures/polynomial/Polynomial Ring\|Polynomial Ring]] — the ring $R[x]$ of all polynomials over $R$
- [[knowledge/math/algebra/structures/polynomial/Quotient of Polynomial Ring\|Quotient of Polynomial Ring]] — $R[x]/(f)$; $\mathbb F[x]/(m)$ is a field iff $m$ is irreducible
- [[knowledge/math/algebra/structures/polynomial/Lagrange Interpolation\|Lagrange Interpolation]] — the polynomial of degree $< t$ through $t$ given points

### Siblings
- [[knowledge/math/algebra/structures/ring/example/Rings of Power Series\|Rings of Power Series]] — the condition $a_i = 0$ for $i \gg 0$ is dropped

### Prerequisites
- [[knowledge/math/algebra/structures/ring/Ring\|Ring]], [[knowledge/math/algebra/structures/field/Field\|Field]] — the coefficients
- [[knowledge/math/algebra/linear algebra/Operators\|Operators]], [[knowledge/math/algebra/linear algebra/Eigenvalues and Eigenvectors\|Eigenvalues and Eigenvectors]] — for § Characteristic Polynomial
