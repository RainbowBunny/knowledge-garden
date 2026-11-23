---
{"dg-publish":true,"permalink":"/knowledge/math/topology/product-topology/","dg-note-properties":{"aliases":["Product Topology on X × Y","Product Space","Box Topology","Infinite Product"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2: §15 (the product topology on $X \times Y$, projections, Theorems 15.1, 15.2); §16, Theorem 16.3; §19 (box and product topologies on arbitrary products, Theorems 19.1–19.6, Example 2, Exercises 6, 9, 10).
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 12–13, 35–36: https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf
- `[Møl]` — J. M. Møller, _General Topology_, lecture notes, University of Copenhagen, Chapter 2: Definition 2.16, Lemma 2.17, Corollary 2.18, Theorem 2.25: https://www.math.ku.dk/~moller/e03/3gt/notes/gtnotes.pdf

## Intuition

> [!intuition] Why
> Functions of several variables and spaces like the plane need a topology on $X \times Y$ built from those of $X$ and $Y$. The product topology is the natural choice: the projections are continuous, and it is the coarsest topology for which they are. For infinitely many factors there are two candidates, the box and the product topology; the product topology is the one for which a map into the product is continuous exactly when its coordinates are.

## Definition

> [!definition] Parameters
> - $X$, $Y$: [[knowledge/math/topology/Topological Space\|topological spaces]].

> [!definition] Product Topology
> The **product topology** on the [[knowledge/math/set theory/Set Operation#Cartesian Product\|cartesian product]] $X \times Y$ is the topology having as [[knowledge/math/topology/Basis for a Topology\|basis]] the collection of all sets $U \times V$, with $U$ open in $X$ and $V$ open in $Y$.
>
> `[Mun00 §15]`, `[Hat p. 12]`. It is a basis: $X \times Y$ is one of its members, and $(U_1 \times V_1) \cap (U_2 \times V_2) = (U_1 \cap U_2) \times (V_1 \cap V_2)$ is another.

> [!remark] Open sets are unions of products, not products
> The basis elements $U \times V$ are open, but most open sets are not of that form: $(0, 1)^2 \cup (2, 3)^2 \subseteq \mathbb R \times \mathbb R$ is open and is not a product $U \times V$.

### Arbitrary products

> [!definition] Box Topology and Product Topology
> Let $\{X_\alpha\}_{\alpha \in J}$ be an indexed family of topological spaces, $\prod_{\alpha \in J} X_\alpha$ the set of $J$-tuples $(x_\alpha)_{\alpha \in J}$ with $x_\alpha \in X_\alpha$ ([[knowledge/math/set theory/Set Operation#Indexed families and products\|Set Operation#Indexed families and products]]), and $\pi_\beta : \prod_\alpha X_\alpha \to X_\beta$ the projection $(x_\alpha)_\alpha \mapsto x_\beta$.
> - The **box topology** has as basis all sets $\prod_\alpha U_\alpha$ with each $U_\alpha$ open in $X_\alpha$.
> - The **product topology** has as [[knowledge/math/topology/Basis for a Topology#Subbasis\|subbasis]] the sets $\pi_\beta^{-1}(U_\beta)$ with $\beta \in J$ and $U_\beta$ open in $X_\beta$.
>
> `[Mun00 §19]`, `[Hat pp. 35–36]`. For two factors both are the topology defined above.

## Property

> [!theorem] Products of bases — a basis of the product
> **Scope**
> - $\mathcal B$ a basis for $X$, $\mathcal C$ a basis for $Y$.
>
> ---
> **Property**
> $\mathcal D = \{B \times C : B \in \mathcal B, C \in \mathcal C\}$ is a basis for the product topology on $X \times Y$.
>
> `[Mun00 Thm 15.1]`, `[Møl Cor 2.18]`. For $W$ open and $(x, y) \in W$, choose $(x, y) \in U \times V \subseteq W$, then $x \in B \subseteq U$ and $y \in C \subseteq V$, and apply [[knowledge/math/topology/Basis for a Topology#Property\|Lemma 13.2]].

> [!theorem] Projections — preimages of open sets form a subbasis
> **Scope**
> - $\pi_1 : X \times Y \to X$ and $\pi_2 : X \times Y \to Y$, the [[knowledge/math/set theory/function/Natural Projection\|projections]] $\pi_1(x, y) = x$, $\pi_2(x, y) = y$.
>
> ---
> **Property**
> $\mathcal S = \{\pi_1^{-1}(U) : U \text{ open in } X\} \cup \{\pi_2^{-1}(V) : V \text{ open in } Y\}$ is a [[knowledge/math/topology/Basis for a Topology#Subbasis\|subbasis]] for the product topology on $X \times Y$.
>
> `[Mun00 Thm 15.2]`: $\pi_1^{-1}(U) = U \times Y$, $\pi_2^{-1}(V) = X \times V$, and $U \times V = \pi_1^{-1}(U) \cap \pi_2^{-1}(V)$.

> [!remark] The coarsest topology with continuous projections
> A map is continuous when preimages of open sets are open. `[Møl Def 2.16]` defines the product topology as the coarsest topology making the projections continuous, and recovers the basis $U \times V$ for finite products `[Møl Lemma 2.17]`; `[Hat p. 13]` checks that the projections are continuous. The subbasis theorem above is the same fact: $\mathcal S$ is exactly what must be open for $\pi_1$ and $\pi_2$ to be continuous.

> [!theorem] Subspaces of a product — the product of the subspaces
> **Scope**
> - $A \subseteq X$ and $B \subseteq Y$, with their [[knowledge/math/topology/Subspace Topology\|subspace topologies]].
>
> ---
> **Property**
> The product topology on $A \times B$ equals the subspace topology that $A \times B$ inherits from $X \times Y$.
>
> `[Mun00 Thm 16.3]`, `[Møl Thm 2.25]`. $(A \times B) \cap (U \times V) = (A \cap U) \times (B \cap V)$, so the two topologies have the same basis.

### Box versus product

> [!theorem] Comparison of the box and product topologies — finitely many restricted factors
> **Scope**
> - An indexed family $\{X_\alpha\}_{\alpha \in J}$ of spaces.
>
> ---
> **Property**
> The box topology has as basis all $\prod_\alpha U_\alpha$ with $U_\alpha$ open in $X_\alpha$.
> The product topology has as basis all $\prod_\alpha U_\alpha$ with $U_\alpha$ open in $X_\alpha$ and $U_\alpha = X_\alpha$ for all but finitely many $\alpha$.
> So the box topology is finer, and the two agree when $J$ is finite.
>
> `[Mun00 Thm 19.1]`. With bases $\mathcal B_\alpha$ of the factors, the same holds with $U_\alpha$ replaced by basis elements $B_\alpha \in \mathcal B_\alpha$ `[Mun00 Thm 19.2]`.

> [!theorem] Properties shared by both topologies
> **Scope**
> - An indexed family $\{X_\alpha\}$, all products with the box topology or all with the product topology; $A_\alpha \subseteq X_\alpha$.
>
> ---
> **Property**
> $\prod A_\alpha$ with the subspace topology is the product of the subspaces $A_\alpha$ `[Mun00 Thm 19.3]`.
> If every $X_\alpha$ is [[knowledge/math/topology/Hausdorff Space\|Hausdorff]], so is $\prod X_\alpha$ `[Mun00 Thm 19.4]`.
> $\prod \overline{A_\alpha} = \overline{\prod A_\alpha}$ ([[knowledge/math/topology/Closure and Interior\|Closure and Interior]]) `[Mun00 Thm 19.5]`.

> [!theorem] Maps into a product — only the product topology sees coordinates
> **Scope**
> - $f : A \to \prod_\alpha X_\alpha$, $f(a) = (f_\alpha(a))_\alpha$, with the product topology.
>
> ---
> **Property**
> $f$ is [[knowledge/math/property/map/Continuity\|continuous]] $\iff$ every $f_\alpha : A \to X_\alpha$ is continuous.
>
> `[Mun00 Thm 19.6]`, `[Hat p. 36]`. Every $f_\alpha = \pi_\alpha \circ f$, and $f^{-1}(\pi_\beta^{-1}(U_\beta)) = f_\beta^{-1}(U_\beta)$, so it suffices to check the subbasis.

> [!remark] Exercises of §19 worth knowing
> - A sequence in $\prod X_\alpha$ with the product topology converges to $x$ iff each coordinate sequence $\pi_\alpha(x_n)$ converges to $\pi_\alpha(x)$; Munkres asks whether this survives in the box topology `[Mun00 §19 Ex 6]`.
> - The axiom of choice is equivalent to: every product of a nonempty indexed family of nonempty sets is nonempty `[Mun00 §19 Ex 9]` ([[knowledge/math/set theory/choice/Axiom of Choice\|Axiom of Choice]]).
> - Given maps $f_\alpha : A \to X_\alpha$ from a set, there is a unique coarsest topology on $A$ making all of them continuous, with subbasis $\{f_\alpha^{-1}(U_\alpha)\}$; a map $g$ into $A$ is continuous for it iff every $f_\alpha \circ g$ is `[Mun00 §19 Ex 10]`. The product topology is the case $A = \prod X_\alpha$, $f_\alpha = \pi_\alpha$.

## Example

> [!example] The plane
> - $\mathbb R \times \mathbb R$, both factors standard: the open rectangles $(a, b) \times (c, d)$ form a basis, by Theorem 15.1 `[Mun00 §15]`.
> - $\mathbb R_\ell \times \mathbb R_\ell$: the half-open squares $[a, b) \times [c, d)$ form a basis ([[knowledge/math/topology/example/Topologies on the Real Line\|Topologies on the Real Line]]).
> - The [[knowledge/math/topology/Order Topology\|dictionary order topology]] on $\mathbb R \times \mathbb R$ is strictly finer than the product topology: a vertical line $\{a\} \times \mathbb R$ is open in it, while every $U \times V$ containing a point of the line contains points off it.

> [!example] The diagonal map into $\mathbb R^\omega$ — continuous for the product, not for the box
> $f : \mathbb R \to \mathbb R^\omega$, $f(t) = (t, t, t, \dots)$, has continuous coordinates, so it is continuous in the product topology. In the box topology $B = (-1, 1) \times (-\tfrac12, \tfrac12) \times (-\tfrac13, \tfrac13) \times \cdots$ is open, but $f^{-1}(B) = \{0\}$ is not `[Mun00 §19]` `[Hat p. 36]`.

## Related

### Siblings
- [[knowledge/math/topology/Subspace Topology\|Subspace Topology]] — the other basic construction; the two commute
- [[knowledge/math/topology/Order Topology\|Order Topology]] — a different topology on $\mathbb R \times \mathbb R$

### Prerequisites
- [[knowledge/math/topology/Basis for a Topology\|Basis for a Topology]], [[knowledge/math/set theory/function/Natural Projection\|Natural Projection]], [[knowledge/math/set theory/Set Operation#Cartesian Product\|Set Operation#Cartesian Product]]
