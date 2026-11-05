---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/linear-algebra/eigenvalues-and-eigenvectors/","dg-note-properties":{}}
---

Reference:
- `[Ax]` — S. Axler, _Linear Algebra Done Right_, 4th ed. (2024, open access): https://linear.axler.net/ — Chapter 5: Eigenvalues and Eigenvectors (§5A Invariant Subspaces, §5B The Minimal Polynomial). Numbers checked in the chapter PDF at https://link.springer.com/book/10.1007/978-3-031-41026-0.
- `[Ax2]` — S. Axler, _Linear Algebra Done Right_, 2nd ed. (1997). Not opened; the note follows its order, and the key marks results whose 4th-edition number I could not check.

## Definition

> [!definition] Parameters
> - $V$: a finite-dimensional [[knowledge/math/algebra/linear algebra/Vector Spaces\|vector space]] over $\mathbb F$.
> - $T \in \mathcal L(V)$: an operator ([[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]]).
> - $\lambda \in \mathbb F$: a scalar.

> [!definition] Eigenvalue
> A scalar $\lambda \in \mathbb F$ is called an **eigenvalue** of $T \in \mathcal L(V)$ if there exists a nonzero vector $u \in V$ such that $T(u) = \lambda u$. `[Ax 5.5]`

> [!definition] Eigenvector
> Suppose $T \in \mathcal L(V)$ and $\lambda \in \mathbb F$ is an eigenvalue of $T$. A vector $u \in V$ is called an **eigenvector** of $T$ (corresponding to $\lambda$) if $u \neq 0$ and $T(u) = \lambda u$. `[Ax 5.8]`

> [!remark]
> The set of eigenvectors of $T \in \mathcal L(V)$ corresponding to $\lambda$, together with $0$, equals $\text{null } (T - \lambda I)$. `[Ax 5.8]`

### Invariant Subspaces

> [!definition] Parameters
> - $U$: a subspace of $V$.

> [!definition] Invariant Subspaces
> For $T \in \mathcal L(V)$ and $U$ is a subspace of $V$, we say that $U$ is **invariant** under $T$ if $u \in U$ implies $T(u) \in U$, and denote the restricted operator by $T|_U$. `[Ax 5.2]`

### Polynomials Applied to Operators

> [!definition] Parameters
> - $p \in \mathcal P(\mathbb F)$: a [[knowledge/math/algebra/structures/polynomial/Polynomial\|Polynomial]], $p(z) = a_0 + a_1 z + \cdots + a_m z^m$.

> [!definition] $p(T)$
> $p(T) = a_0 I + a_1 T + \cdots + a_m T^m$, the operator obtained by substituting $T$ for $z$. `[Ax 5.14]`

> [!definition] Parameters
> - $a \in \mathbb C$: a scalar.

> [!proposition] Eigenvalues of $p(T)$ — over $\mathbb C$ they are the values $p(\lambda)$
> Suppose $\mathbb F = \mathbb C$, $T \in \mathcal L(V)$, $p \in \mathcal P(\mathbb C)$, and $a \in \mathbb C$. Then, $a$ is an eigenvalue of $p(T)$ if and only if $a = p(\lambda)$ for some eigenvalue $\lambda$ of $T$.
> The result does not hold if $\mathbb F = \mathbb R$.
>
> `[Ax2]`

## Property

> [!theorem] Eigenvectors for distinct eigenvalues are linearly independent
> Let $T \in \mathcal L(V)$. Suppose $\lambda_1, \dots, \lambda_m$ are distinct eigenvalues of $T$ and $v_1, \dots, v_m$ are corresponding nonzero eigenvectors. Then $(v_1, \dots, v_m)$ is linearly independent. `[Ax 5.11]`

> [!corollary] At most $\dim V$ eigenvalues
> Each operator on $V$ has at most $\dim V$ distinct eigenvalues. `[Ax 5.12]`

> [!definition] Parameters
> - $\lambda_1, \dots, \lambda_m$: the distinct eigenvalues of $T$.
> - $n = \dim V$.

> [!proposition] Conditions equivalent to diagonalizability
> Suppose $T \in \mathcal L(V)$. Let $\lambda_1, \dots, \lambda_m$ denote the distinct eigenvalues of $T$. Then the following are equivalent:
> 1. $T$ has a diagonal matrix with respect to some basis of $V$;
> 2. $V$ has a basis consisting of eigenvectors of $T$;
> 3. There exist one-dimensional subspaces $U_1, \dots, U_n$ of $V$, each invariant under $T$, such that $$V = U_1 \oplus \cdots \oplus U_n;$$
> 4. $V = \text{null}(T - \lambda_1 I) \oplus \cdots \oplus \text{null}(T - \lambda_m I);$
> 5. $\dim V = \dim \text{null}(T - \lambda_1 I) + \cdots + \dim \text{null} (T - \lambda_m I).$
>
> If $\mathbb F = \mathbb C$, they are also equivalent to:
> 6. Every generalized eigenvector of $T$ is an eigenvector of $T$.
> 7. The minimal polynomial of $T$ has no repeated roots.
>
> Over $\mathbb R$, 6 and 7 do not imply 1: the operator $(w, z) \mapsto (-z, w)$ on $\mathbb R^2$ has no eigenvalues `[Ax 5.9]`, so it has no generalized eigenvectors and is not diagonalizable, while its minimal polynomial $z^2 + 1$ has no repeated roots.
>
> `[Ax2]` `[Ax 5.9]` `[Ax 5.27]`

> [!definition] Parameters
> - $S \in \mathcal L(V)$: an operator.

> [!proposition] $ST$ and $TS$ have the same eigenvalues
> Suppose $S, T \in \mathcal L(V)$. Then, $ST$ and $TS$ have the same eigenvalues. `[Ax2]`

### Invariant Subspaces on Real Vector Space

> [!theorem] Real operators have an invariant subspace of dimension $1$ or $2$
> Every operator on a finite-dimensional, nonzero, real vector space has an invariant subspace of dimension $1$ or $2$. `[Ax2]`

> [!remark]
> There exist real numbers $a_0, \dots, a_n$, not all $0$, such that $$0 = a_0 v + a_1 T(v) + \cdots + a_n T^n(v).$$ Thus we have $$0 = c(T - \lambda_1 I) \dots (T - \lambda_m I) (T^2 + \alpha_1 T + \beta_1 I) \dots (T^2 + \alpha_m T + \beta_m I) (v).$$

> [!theorem] Operators on odd-dimensional spaces have eigenvalues
> Every operator on an odd-dimensional real vector space has an eigenvalue. `[Ax 5.34]`

## Related

### Constructions
- [[knowledge/math/algebra/linear algebra/Operators\|Operators]] — generalized eigenvectors, the spectral theorems and the Jordan form build on eigenvalues

### Siblings
- [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]] — eigenvalues of a square matrix; they agree with those of the operator it represents
- [[knowledge/math/algebra/structures/polynomial/Polynomial\|Polynomial]] — the minimal and characteristic polynomials, whose zeros are the eigenvalues

### Prerequisites
- [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]] — operators, null spaces
- [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]] — subspaces, direct sums
