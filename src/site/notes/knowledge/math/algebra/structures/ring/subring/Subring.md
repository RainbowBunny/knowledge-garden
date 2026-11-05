---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/ring/subring/subring/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 2.3: Monomorphisms and epimorphisms.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_ (2025): https://abstract.ups.edu/aata/ — §16.1 Rings (read at the mirror https://judsonbooks.org/aata-files/aata-html/; item numbers as there).

## Definition

> [!definition] Parameters
> - $R$: a [[knowledge/math/algebra/structures/ring/Ring\|Ring]].
> - $S$: a ring whose underlying set is a subset of $R$.

> [!definition] Subring
> Extends:: [[knowledge/math/algebra/structures/Substructure\|Substructure]].
>
> ---
> A **subring** $S$ of a [[knowledge/math/algebra/structures/ring/Ring\|Ring]] $R$ is a ring where $S \subseteq R$ and [[knowledge/math/set theory/function/Inclusion Function\|Inclusion Function]] $S \hookrightarrow R$ is a [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]].
>
> `[Alu III.2.3]`

> [!remark] A subring contains $1_R$
> A ring homomorphism sends $1$ to $1$, so a subring contains $1_R$. A subset $S \subseteq R$ is then a subring iff
> - $1_R \in S$,
> - $r - s \in S$ for all $r, s \in S$,
> - $rs \in S$ for all $r, s \in S$.
>
> In `[Jud §16.1]` a subring is a subset that is a ring under the inherited operations and need not contain an identity; its criterion `[Jud Prop 16.1.10]` is the last two conditions together with $S \neq \emptyset$. So in `[Jud]` every [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] is a subring, while here a proper ideal never is.

## Example

> [!example]
> - $\mathbb Z \subset \mathbb Q \subset \mathbb R \subset \mathbb C$ is a chain of subrings. `[Jud Ex 16.1.9]`
> - $n \mathbb Z$ with $n \neq \pm 1$ is a subring of $\mathbb Z$ in `[Jud Ex 16.1.9]`, but not here, since $1 \notin n\mathbb Z$.
> - The [[knowledge/math/algebra/structures/ring/subring/Ring Center\|center]] $Z(R)$ is a subring of $R$.

## Related

### Siblings
- [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] — the same notion for groups.
- [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] — closed under multiplication by all of $R$, but a proper ideal does not contain $1$, so it is not a subring.

### Prerequisites
- [[knowledge/math/algebra/structures/ring/Ring Homomorphism\|Ring Homomorphism]], [[knowledge/math/set theory/function/Inclusion Function\|Inclusion Function]].
