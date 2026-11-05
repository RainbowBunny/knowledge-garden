---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/example/matrix-group/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter III: Rings and modules, Section 1.2: First examples and special classes of rings.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the LibreTexts copy, item numbers as there: https://math.libretexts.org/Bookshelves/Abstract_and_Geometric_Algebra/Abstract_Algebra%3A_Theory_and_Applications_%28Judson%29), §12.1 Matrix Groups.
- `[CasG]` — W. Casselman, _Introduction to admissible representations of p-adic groups_ (notes on $\mathrm{GL}_n$): https://personal.math.ubc.ca/~cass/research/pdf/GLN.pdf
- `[CasH]` — W. Casselman, _The construction of Hecke algebras associated to a Coxeter group_: https://personal.math.ubc.ca/~cass/research/pdf/Hecke.pdf
- `[Lus]` — G. Lusztig, arXiv:1006.5004, §1: https://arxiv.org/abs/1006.5004

## Definition

> [!definition] Parameters
> - $n \geq 1$: the size of the matrices.

> [!definition] General Linear Group
> Instantiates:: [[knowledge/math/algebra/structures/group/Group\|Group]].
>
> ---
> $\mathsf{GL}_n(\mathbb{R})$: 
> - Object: Invertible $n \times n$ [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]] on $\mathbb{R}$.
> - Operation: Matrix multiplication.
>
> `[Alu III.1.2]` `[Jud §12.1]`

## Property

### Bruhat Decomposition

> [!theorem] Bruhat decomposition — $\mathrm{GL}_n(F)$ is the disjoint union of the double cosets $BwB$, one per permutation
> ### Scope
> $G = \mathrm{GL}_n(F)$ over a field $F$; $B$ the upper triangular matrices; $W = S_n$ ([[knowledge/math/algebra/structures/group/special group/Symmetric Group\|Symmetric Group]]), realised as the permutation matrices.
>
> ---
> ### Property
> $$G = \bigsqcup_{w \in W} BwB,$$
> a disjoint union of [[knowledge/math/algebra/structures/group/special group/Coset#Double Coset\|double cosets]] `[CasG §4; Lus §1]`. More precisely, every $m \in G$ factors as $m = b\,w\,n$ with $b \in B$ and $w \in W$, where $n$ lies in a subgroup $N_w$ of the upper unitriangular matrices chosen so that the factorization is unique `[CasG Thm 7.2]`.

> [!remark] Gauss elimination, and other groups
> The proof is row reduction: multiplying by upper triangular matrices on both sides reduces any invertible matrix to a permutation matrix `[CasG §4]`. The same decomposition holds for every finite reductive group $G$ with a Borel subgroup $B$ and Weyl group $W$ `[CasH §1]`; for $p$-adic groups there is an affine version, with the Iwahori subgroup in place of $B$ (see [[knowledge/math/algebra/structures/ring/example/Hecke Algebra\|Hecke Algebra]]).

> [!remark] Over any field
> The definition above is over $\mathbb R$; the Bruhat decomposition, like the definition, works over any field — in particular the finite field $\mathbb F_q$, where it underlies the [[knowledge/math/algebra/structures/ring/example/Hecke Algebra\|Hecke Algebra]].

## Related

### Prerequisites
- [[knowledge/math/algebra/linear algebra/Matrix\|Matrix]] — the elements of the group

### Siblings
- [[knowledge/math/algebra/structures/ring/example/Matrix Ring\|Matrix Ring]] — all $n \times n$ matrices, with addition as well; $\mathrm{GL}_n$ is its group of invertible elements
- [[knowledge/math/algebra/structures/group/Group#General Linear Group over the Integers Modulo n\|General linear group modulo n]] — the same construction with entries in $\mathbb Z_n$
