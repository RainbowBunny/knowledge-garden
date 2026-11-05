---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/action/group-representation/","dg-note-properties":{}}
---

Reference:
- `[EGH+]` — P. Etingof, O. Golberg, S. Hensel, T. Liu, A. Schwendner, D. Vaintrob, E. Yudovina, _Introduction to Representation Theory_, AMS Student Mathematical Library 59 (2011); arXiv:0901.0827: https://arxiv.org/abs/0901.0827. Numbers follow the arXiv / MIT OCW 18.712 version; the printed book numbers differently.

## Definition

> [!definition] Parameters
> - $k$: a field. $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]]. $V$: a vector space over $k$, see [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]].
> - $\mathrm{GL}(V) = \mathrm{Aut}(V)$: the group of invertible linear maps $V \to V$.
>
> `[EGH+ Ex. 1.19(3)]`

> [!definition] Group Representation
> Extends:: [[knowledge/math/algebra/structures/action/Group Action\|Group Action]].
>
> ---
> A **representation** of $G$ is a vector space $V$ together with a group homomorphism $\rho: G \to \mathrm{GL}(V)$. `[EGH+ Ex. 1.19(3)]`

> [!remark] As a group action
> In the terms of [[knowledge/math/algebra/structures/action/Group Action\|Group Action]], a representation is an action of $G$ on the object $V$ of the category of $k$-vector spaces: $\mathsf{Aut}$ of $V$ there is $\mathrm{GL}(V)$, and $\sigma = \rho$.

> [!remark] As a module
> A representation of an algebra $A$ (associative, with unit), also called a left $A$-module, is a vector space $V$ with an algebra homomorphism $\rho: A \to \mathrm{End}\, V$ `[EGH+ Def 1.9]`. A representation of the [[knowledge/math/algebra/structures/ring/example/Group Algebra\|Group Algebra]] $k[G]$ is the same thing as a representation of $G$ `[EGH+ Ex. 1.19(3)]`. Compare [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]], where the ring acts on an abelian group.

### Subrepresentations

> [!definition] Subrepresentation and Irreducible Representation
> - A **subrepresentation** of $V$ is a subspace $W \subseteq V$ invariant under all the operators $\rho(a)$. `[EGH+ Def 1.11]`
> - $V \neq 0$ is **irreducible** (or simple) if its only subrepresentations are $0$ and $V$. `[EGH+ Def 1.12]`
> - A **homomorphism** (intertwining operator) $\varphi: V_1 \to V_2$ is a linear map with $\varphi(av) = a\varphi(v)$. `[EGH+ Def 1.13]`

> [!definition] Direct Sum
> $V_1 \oplus V_2$ is a representation by $a(v_1 \oplus v_2) = av_1 \oplus av_2$ `[EGH+ Def 1.14]`. A nonzero representation is **indecomposable** if it is not isomorphic to a direct sum of two nonzero representations `[EGH+ Def 1.15]`.

## Property

> [!theorem] Maschke's theorem — in good characteristic every representation splits into irreducibles
> ### Scope
> A finite group $G$ and a field $k$ whose characteristic does not divide $|G|$.
>
> ---
> ### Property
> - The algebra $k[G]$ is semisimple `[EGH+ Thm 3.1(i)]`; equivalently, every finite-dimensional representation of $G$ is completely reducible — isomorphic to a direct sum of irreducible representations `[EGH+ Prop 2.16]`.
> - The regular representation decomposes as $k[G] \cong \bigoplus_i \dim(V_i)\, V_i$ over the irreducible representations $V_i$, and $|G| = \sum_i \dim(V_i)^2$ `[EGH+ Thm 3.1(ii)]`.
> - Conversely, if $k[G]$ is semisimple, the characteristic of $k$ does not divide $|G|$ `[EGH+ Prop 3.2]`.

> [!theorem] Jordan–Hölder theorem — the irreducible pieces are unique
> ### Scope
> A finite-dimensional representation $V$ of an algebra $A$.
>
> ---
> ### Property
> $V$ has a filtration $0 = V_0 \subset V_1 \subset \cdots \subset V_n = V$ by subrepresentations whose quotients $W_i = V_i / V_{i-1}$ are irreducible `[EGH+ Lemma 2.8]`. For any two such filtrations, with quotients $W_1, \dots, W_n$ and $W'_1, \dots, W'_m$, we have $n = m$ and $W_{\sigma(i)} \cong W'_i$ for some permutation $\sigma$ `[EGH+ Thm 2.18]`. The sequence $W_1, \dots, W_n$ is a *Jordan–Hölder series* of $V$.

> [!remark] What the two theorems give together
> If $V \cong V_1 \oplus \cdots \oplus V_n$ with $V_i$ irreducible, the partial sums $V_1 \oplus \cdots \oplus V_j$ form a filtration with quotients $V_j$. So by Jordan–Hölder the summands that Maschke's theorem produces are unique up to order and isomorphism. Representation theory of a finite group over $\mathbb C$ then comes down to two problems: list the irreducible representations, and find their multiplicities in a given one.

> [!proposition] Number of irreducibles — as many as conjugacy classes
> If $|G| \neq 0$ in $k$, the number of isomorphism classes of irreducible representations of $G$ equals the number of conjugacy classes of $G$. `[EGH+ Cor 3.6]`

## Example

- The regular representation: $k[G]$ acting on itself by left multiplication, decomposed in Maschke's theorem above.
- The symmetric group $S_n$: its irreducible representations are the [[knowledge/math/algebra/structures/action/Specht Module\|Specht modules]], one per partition of $n$.

## Related

### Instantiations
- [[knowledge/math/algebra/structures/action/Specht Module\|Specht Module]] — the irreducible representations of $S_n$

### Siblings
- [[knowledge/math/algebra/structures/ring/example/Group Algebra\|Group Algebra]] — the same data as a ring: the representations of $G$ are its modules

### Used by
- [[knowledge/math/algebra/structures/ring/example/Hecke Algebra\|Hecke Algebra]] — the representation theory of $\mathrm{GL}_n$ over finite and $p$-adic fields

### Prerequisites
- [[knowledge/math/algebra/structures/action/Group Action\|Group Action]], [[knowledge/math/algebra/linear algebra/Vector Spaces\|Vector Spaces]], [[knowledge/math/algebra/structures/ring/module/R-Module\|R-Module]]
