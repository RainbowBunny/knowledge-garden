---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/extension/group-extension/","dg-note-properties":{"aliases":["Extension of Groups","Central Extension","Factor Set","Factor System"]}}
---

Reference:
- `[McG25]` — _Lecture 2-10: H² and group extensions_, University of Washington Math 505 lecture notes, 10 February 2025, Theorem 36; the notes follow a textbook cited by pages (pp. 824–831): https://sites.math.washington.edu/~mcgovern/505%20pdf%202025/505.2-10.pdf
- `[ConSpl]` — K. Conrad, _Splitting of short exact sequences for groups_, expository notes, Theorem 3.3: https://kconrad.math.uconn.edu/blurbs/grouptheory/splittinggp.pdf

## Definition

> [!definition] Parameters
> - $A$: an [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]], written additively.
> - $Q$: a [[knowledge/math/algebra/structures/group/Group\|Group]].

> [!definition] Group Extension
> An **extension** of $Q$ by $A$ is a [[knowledge/math/algebra/structures/group/extension/Short Exact Sequence of Groups\|short exact sequence]]
> $$1 \to A \to E \to Q \to 1.$$
> Two extensions $E$, $E'$ are **equivalent** if there is an isomorphism $\beta : E \to E'$ that is the identity on $A$ and induces the identity on $Q$.
>
> `[McG25]`, which writes $G$ for the quotient. Equivalence asks more than $E \cong E'$.

> [!remark] The action on $A$
> Since $A$ is abelian, conjugation in $E$ by a lift of $q \in Q$ gives an automorphism of $A$ that depends only on $q$: an action of $Q$ on $A$, written $q \cdot a$. The extension is **central** when this action is trivial, that is, when $A$ lies in the [[knowledge/math/algebra/structures/group/subgroup/Group Center\|center]] of $E$.

### Factor set

> [!definition] Factor Set
> Choose for each $q \in Q$ a lift $\mu(q) \in E$, with $\mu(1) = 1$. Then
> $$\mu(g)\,\mu(h) = f(g, h)\,\mu(gh)$$
> defines $f : Q \times Q \to A$, the **factor set** of $\mu$. It satisfies the cocycle identity
> $$f(g, h) + f(gh, k) = g \cdot f(h, k) + f(g, hk),$$
> and the normalization $f(1, g) = f(g, 1) = 0$.
>
> `[McG25]`

## Property

> [!proposition] Changing the lifts changes $f$ by a coboundary
> **Scope**
> - $\mu' = c \cdot \mu$ another choice of lifts, $c : Q \to A$.
>
> ---
> **Property**
> The factor sets of $\mu$ and $\mu'$ differ by a coboundary, so the class of $f$ in $H^2(Q, A)$ depends only on the extension.
>
> `[McG25]`

> [!theorem] Classification — extensions with a given action correspond to $H^2(Q, A)$
> **Scope**
> - $A$: an abelian group with a fixed action of $Q$.
>
> ---
> **Property**
> There is a one-to-one correspondence between equivalence classes of extensions of $Q$ by $A$ inducing this action and the elements of $H^2(Q, A)$. The zero class corresponds to the split extensions, the [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|semidirect products]] $A \rtimes Q$.
>
> `[McG25 Thm 36]`, with `[ConSpl Thm 3.3]` for split = semidirect.

## Example

> [!example] Extensions of $C_2$ by $C_2$
> The action is trivial, since $\mathrm{Aut}(C_2) = 1$. There are two classes: the split $C_2 \times C_2$ and the non-split $C_4$ ([[knowledge/math/algebra/structures/group/extension/Short Exact Sequence of Groups#Example\|Short Exact Sequence of Groups#Example]]).

> [!example] Groups of order 16 as central extensions
> A nonabelian group of order 16 has a central subgroup $A \cong C_2$ ([[knowledge/math/algebra/structures/group/special group/p-Group#Property\|p-Group#Property]]), so it is a central extension of a group of order 8 by $C_2$. In practice it is easier to extend a normal subgroup of order 8 by $C_2$ — [[knowledge/math/algebra/structures/group/extension/Cyclic Extension\|Cyclic Extension]], [[knowledge/math/algebra/structures/group/classification/Groups of Order 16\|Groups of Order 16]].

## Related

### Descendants
- [[knowledge/math/algebra/structures/group/extension/Cyclic Extension\|Cyclic Extension]] — the quotient $Q$ is cyclic; then an extension is described by an automorphism and one element

### Constructions
- [[knowledge/math/algebra/structures/group/extension/Schur-Zassenhaus Theorem\|Schur-Zassenhaus Theorem]] — when $|A|$ and $|Q|$ are coprime, every extension splits

### Prerequisites
- [[knowledge/math/algebra/structures/group/extension/Short Exact Sequence of Groups\|Short Exact Sequence of Groups]], [[knowledge/math/algebra/structures/group/extension/Semidirect Product\|Semidirect Product]], [[knowledge/math/algebra/structures/group/special group/Abelian Group\|Abelian Group]]
