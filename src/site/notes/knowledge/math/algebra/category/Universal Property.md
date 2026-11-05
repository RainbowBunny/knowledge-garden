---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/category/universal-property/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter I: Preliminaries: Set theory and categories, Section 5.1: Initial and final objects; Section 5.2: Universal properties.
- `[nLab-I]` — nLab, _initial object_: https://ncatlab.org/nlab/show/initial+object
- `[nLab-T]` — nLab, _terminal object_: https://ncatlab.org/nlab/show/terminal+object

## Definition

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $X$: an object of $\mathcal C$.

> [!definition] Universal Property
> Object $X$ is universal with respect to the following property: For any $Y$ such that ..., there exists a unique morphism $Y \rightarrow X$ such that... `[Alu I.5.2]`

> [!remark]
> This is the final form: the unique morphism goes into $X$. In the initial form it goes out of $X$, $X \to Y$ — the [[knowledge/math/algebra/category/Categorical Coproduct\|Categorical Coproduct]] and the quotient in [[knowledge/math/algebra/category/example/Quotient Category\|Quotient Category]] are of this kind, the [[knowledge/math/algebra/category/Categorical Product\|Categorical Product]] of the final kind.

### Initial Objects

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $I$: an object of $\mathcal C$.

> [!definition] Initial Objects
> Let $\mathcal{C}$ be a category. We say that an object $I$ of $\mathcal{C}$ is **initial** in $\mathcal{C}$ if for every object $A$ of $\mathcal{C}$ there exists exactly one morphism $I \rightarrow A$ in $\mathcal{C}$:
> $$\forall A \in \mathsf{Obj}(\mathcal{C}): \quad \mathsf{Hom}_{\mathcal{C}}(I, A) \text{ is a singleton.}$$
> `[Alu I.5.1]` `[nLab-I]`

### Final Objects

> [!definition] Parameters
> - $\mathcal C$: a [[knowledge/math/algebra/category/Category\|Category]].
> - $F$: an object of $\mathcal C$.

> [!definition] Final Objects
> Let $\mathcal{C}$ be a category. We say that an object $F$ of $\mathcal{C}$ is **final** (also called **terminal**) in $\mathcal{C}$ if for every object $A$ of $\mathcal{C}$ there exists exactly one morphism $A \rightarrow F$ in $\mathcal{C}$:
> $$\forall A \in \mathsf{Obj}(\mathcal{C}): \quad \mathsf{Hom}_{\mathcal{C}}(A, F) \text{ is a singleton}$$
> `[Alu I.5.1]` `[nLab-T]`

## Property

### Uniqueness

> [!proposition] Uniqueness of initial objects — two initial objects are isomorphic, by a unique isomorphism
> Let $\mathcal C$ be a category, If $I_1, I_2$ are both initial objects in $\mathcal C$, then $I_1 \cong I_2$, and the isomorphism $I_1 \to I_2$ is unique. `[Alu I.5.1]` `[nLab-I]`

> [!proposition] Uniqueness of final objects — two final objects are isomorphic, by a unique isomorphism
> Let $\mathcal C$ be a category, If $F_1, F_2$ are both final objects in $\mathcal C$, then $F_1 \cong F_2$, and the isomorphism $F_1 \to F_2$ is unique. `[Alu I.5.1]` `[nLab-T]`

## Example

- [[knowledge/math/algebra/structures/group/Category Group\|Category Group]] — the [[knowledge/math/algebra/structures/group/example/Trivial Group\|Trivial Group]] is both initial and final in $\mathsf{Grp}$.
- [[knowledge/math/algebra/structures/ring/Category Ring\|Category Ring]] — $\mathbb Z$ is initial in $\mathsf{Ring}$.
- [[knowledge/math/algebra/category/example/Quotient Category\|Quotient Category]] — the canonical projection $(\pi, A/{\sim})$ is initial.
- [[knowledge/math/algebra/structures/group/subgroup/Kernel of Group Homomorphism\|Kernel of Group Homomorphism]] — the inclusion $\ker \varphi \hookrightarrow G$ is final among the homomorphisms $\alpha$ with $\varphi \circ \alpha$ trivial.

## Related

### Prerequisites
- [[knowledge/math/algebra/category/Morphism\|Morphism]] — the isomorphism $\cong$ of the uniqueness statements.
