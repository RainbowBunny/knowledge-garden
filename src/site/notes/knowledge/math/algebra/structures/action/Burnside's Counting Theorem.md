---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/action/burnside-s-counting-theorem/","dg-note-properties":{"aliases":["Burnside's Lemma","Orbit-Counting Theorem","Cauchy–Frobenius Lemma"]}}
---

Reference:
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_, HTML edition, §14.3: Lemma 14.3.2, Theorem 14.3.3, the colouring example: https://judsonbooks.org/aata-files/aata-html/actions-section-burnsides-counting-theorem.html (result numbers as there).

## Definition

> [!theorem] Burnside's Counting Theorem — the number of orbits is the average number of fixed points
> ### Scope
> - $G$: a finite [[knowledge/math/algebra/structures/group/Group\|Group]] acting on a finite set $X$ ([[knowledge/math/algebra/structures/action/Group Action\|Group Action]]).
> - $X_g = \{x \in X \mid gx = x\}$: the points fixed by $g \in G$.
> - $k$: the number of [[knowledge/math/algebra/structures/action/Orbit\|orbits]] of $X$.
>
> ---
> ### Condition
> - $G$ and $X$ finite.
>
> ---
> ### Property
> $$k = \frac{1}{|G|} \sum_{g \in G} |X_g|.$$
>
> `[Jud Thm 14.3.3]`

## Property

> [!proof] Why — count the pairs $(g, x)$ with $gx = x$ twice
> Counting by $g$ and by $x$,
> $$\sum_{g \in G} |X_g| = \sum_{x \in X} |G_x|.$$
> Points of one orbit have isomorphic [[knowledge/math/algebra/structures/action/Stabilizer\|stabilizers]] `[Jud Lemma 14.3.2]`, and an orbit $O$ has $|O| = |G| / |G_x|$ points ([[knowledge/math/algebra/structures/action/Stabilizer#Property\|Stabilizer#Property]]). So each orbit contributes $|O| \cdot |G| / |O| = |G|$, and the sum is $k |G|$ `[Jud Thm 14.3.3]`.

## Example

> [!example] Colouring the vertices of a square `[Jud §14.3]`
> Colour the four vertices of a square black or white, up to the symmetries of the square, the [[knowledge/math/algebra/structures/group/example/Dihedral Group\|Dihedral Group]] $D_4$. The fixed colourings are $2^4$ for the identity, $2$ for each of the two quarter turns, $2^2$ for the half turn and for the two reflections through edge midpoints, and $2^3$ for the two reflections through vertices:
> $$\frac{1}{8}\left(2^4 + 2 + 2 + 2^2 + 2^2 + 2^2 + 2^3 + 2^3\right) = 6.$$
> There are 6 colourings up to symmetry.

## Related

### Siblings
- [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]] — the orbit decomposition of the conjugation action

### Prerequisites
- [[knowledge/math/algebra/structures/action/Group Action\|Group Action]], [[knowledge/math/algebra/structures/action/Orbit\|Orbit]], [[knowledge/math/algebra/structures/action/Stabilizer\|Stabilizer]]
