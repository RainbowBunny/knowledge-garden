---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/special-group/coset/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter II: Groups, first encounter, Section 7.3: Cosets; Section 7.4: Quotient by normal subgroups.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the HTML edition at https://judsonbooks.org/aata-files/aata-html/; result numbers as there).
- `[CasG]` — W. Casselman, _Introduction to admissible representations of p-adic groups_ (notes on $\mathrm{GL}_n$): https://personal.math.ubc.ca/~cass/research/pdf/GLN.pdf
- `[Bum]` — D. Bump, _Hecke Algebras_, lecture notes (2018): http://sporadic.stanford.edu/hecke.pdf

## Definition

> [!definition] Parameters
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]].
> - $H \leq G$: a [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]].
> - $a \in G$: an element.

> [!definition] Coset
> Requires:: [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]].
>
> ---
> - The **left-cosets** of a [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] $H$ in a group $G$ are the sets $aH = \{ah : h \in H\}$, $a \in G$.
> - The **right-cosets** of $H$ are the sets $Ha = \{ha : h \in H\}$, $a \in G$.
>
> `[Alu II §7.3]` `[Jud §6.1]`

### Double Coset

> [!definition] Double Coset
> For subgroups $H, K \leq G$ and $g \in G$, the **double coset** of $g$ is $HgK = \{hgk : h \in H,\ k \in K\}$; the set of double cosets is written $H \backslash G / K$. The case $H = K$, $HgH$, is the one used for Hecke algebras `[Bum Thm 5]`, and $B \backslash \mathrm{GL}_n / B$ is the decomposition of [[knowledge/math/algebra/structures/group/example/Matrix Group#Bruhat Decomposition\|Bruhat]] `[CasG §4]`.

> [!proposition] Double cosets partition $G$
> $g \in HgK$; and if $hgk = h'g'k'$, then $g' = h'^{-1}h\, g\, k k'^{-1} \in HgK$, so $Hg'K \subseteq HgK$, and by symmetry $Hg'K = HgK$. Two double cosets are therefore equal or disjoint.

## Property

> [!proposition] Cosets and compatible relations — subgroups of $G$ correspond to equivalence relations compatible with multiplication on one side
> There is a one-to-one correspondence between
> - Subgroups of $G$ and [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] on $G$ satisfying
> $$(\forall g \in G): a \sim b \implies ga \sim gb.$$
> for the relation $\sim_L$ corresponding to a subgroup $H$, $G/_{\sim_L}$ may be described as the set of left-cosets $aH$ of $H$.
> - Subgroups of $G$ and [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] on $G$ satisfying
> $$(\forall g \in G): a \sim b \implies ag \sim bg.$$
> for the relation $\sim_R$ corresponding to a subgroup $H$, $G/_{\sim_R}$ may be described as the set of right-cosets $Ha$ of $H$.
>
> Here:
> - $a \sim_L b \iff a^{-1}b \in H \iff aH = bH$ `[Jud Lemma 6.1.3]`;
> - $a \sim_R b \iff ab^{-1} \in H \iff Ha = Hb$.
>
> `[Alu II §7.3]`

> [!proposition] Left and right cosets agree exactly for normal subgroups
> The relations $\sim_L, \sim_R$ corresponding to a [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] $H$ coincide if and only if $H$ is a [[knowledge/math/algebra/structures/group/subgroup/Normal Subgroup\|Normal Subgroup]]. `[Alu II §7.4]`
>
> Judson takes this as the definition of normality: $gH = Hg$ for all $g \in G$ `[Jud §10.1]`.

## Related

### Constructions
- [[knowledge/math/algebra/structures/group/special group/Quotient Group\|Quotient Group]] — the cosets of a normal subgroup form the group $G/H$; their number is the index $[G:H]$
- [[knowledge/math/algebra/structures/ring/special ring/Quotient Ring\|Quotient Ring]] — the cosets of an [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]]
- [[knowledge/math/algebra/structures/ring/example/Hecke Algebra\|Hecke Algebra]] — built on the double cosets $HgH$

### Siblings
- [[knowledge/math/algebra/structures/action/Orbit\|Orbit]] — the left coset $aH$ is the orbit of $a$ under right multiplication by $H$

### Prerequisites
- [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]]
- [[knowledge/math/set theory/relation/Equivalence Relation\|Equivalence Relation]] — $\sim_L$, $\sim_R$
