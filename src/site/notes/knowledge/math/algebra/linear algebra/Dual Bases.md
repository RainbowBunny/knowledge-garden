---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/linear-algebra/dual-bases/","dg-note-properties":{}}
---

Reference:
- `[AxD]` — S. Axler, _Duality, part 1: Dual Bases and Dual Maps_ (supplement to _Linear Algebra Done Right_, unnumbered): https://www.linear.axler.net/DualBasesMaps.pdf

## Definition

> [!definition] Parameters
> - $\mathbb F$: a [[knowledge/math/algebra/structures/field/Field\|Field]].
> - $V$: a [[knowledge/math/algebra/linear algebra/Vector Spaces\|vector space]] over $\mathbb F$.

> [!definition] Dual Space
> Requires:: [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]].
>
> ---
> A **linear functional** on $V$ is a linear map from $V$ to $\mathbb F$. The **dual space** of $V$, denoted $V'$, is the vector space of all linear functionals on $V$, that is, $V' = \mathcal L(V, \mathbb F)$. `[AxD]`

> [!definition] Parameters
> - $v_1, \dots, v_n$: a basis of $V$.

> [!definition] Dual Basis
> If $v_1, \dots, v_n$ is a basis of $V$, then the **dual basis** of $v_1, \dots, v_n$ is the list $\varphi_1, \dots, \varphi_n$ of elements of $V'$, where each $\varphi_j$ is the linear functional on $V$ such that
> - $\varphi_j(v_k) = 1$ if $k = j$,
> - $\varphi_j(v_k) = 0$ if $k \neq j$.
>
> `[AxD]`

## Property

> [!proposition] The dual basis is a basis of the dual space — so $\dim V' = \dim V$
> Suppose $V$ is finite-dimensional. Then the dual basis of a basis of $V$ is a basis of $V'$; in particular $\dim V' = \dim V$. `[AxD]`

## Related

### Siblings
- [[knowledge/math/algebra/linear algebra/Inner-Product Spaces\|Inner-Product Spaces]] — on an inner-product space the Riesz representation writes every functional as $u \mapsto \langle u, v \rangle$, and the dual basis of an orthonormal basis is $\varphi_j = \langle \cdot, e_j \rangle$

### Prerequisites
- [[knowledge/math/algebra/linear algebra/Linear Maps\|Linear Maps]] — $V' = \mathcal L(V, \mathbb F)$
- [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]] — bases and dimension
