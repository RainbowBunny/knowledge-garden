---
{"dg-publish":true,"permalink":"/knowledge/math/property/map/continuity/","dg-note-properties":{"aliases":["Continuous Function","Continuous Map","Continuous","Pasting Lemma","Continuous at a Point"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §18: continuous functions, Theorems 18.1–18.4; §19, Theorem 19.6.
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 11, 13, 15 (Exercise 14): https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf

## Intuition

> [!intuition] Why
> A continuous map is one that does not tear: points that are near each other in $X$ land near each other in $Y$. Stated with open sets, this needs no distances, so one definition covers the $\varepsilon$–$\delta$ continuity of calculus, maps between ordered sets, and maps between spaces with no metric. It is the structure-preserving map of topology, as homomorphisms are for algebra and monotone maps for orders.

## Definition

> [!definition] Continuity
> ### Scope
> A map $f : X \to Y$ between [[knowledge/math/topology/Topological Space\|topological spaces]].
>
> ---
> ### Property
> $f$ is **continuous** iff for every open $V \subseteq Y$, the preimage $f^{-1}(V)$ is open in $X$.
>
> `[Mun00 §18]`, `[Hat p. 11]`. $f$ is **continuous at the point** $x$ iff for each neighborhood $V$ of $f(x)$ there is a neighborhood $U$ of $x$ with $f(U) \subseteq V$ `[Mun00 §18]`.

## Property

> [!theorem] Equivalent forms — four ways to say continuous
> **Scope**
> - $f : X \to Y$, with $X$, $Y$ topological spaces.
>
> ---
> **Property**
> The following are equivalent `[Mun00 Thm 18.1]`:
> - $f$ is continuous;
> - $f(\overline A) \subseteq \overline{f(A)}$ for every $A \subseteq X$ ([[knowledge/math/topology/Closure and Interior\|Closure and Interior]]);
> - $f^{-1}(B)$ is [[knowledge/math/topology/Closed Set\|closed]] in $X$ for every closed $B \subseteq Y$;
> - $f$ is continuous at every point of $X$.
>
> `[Hat p. 11]` proves the closed-set form. If the topology of $Y$ is given by a [[knowledge/math/topology/Basis for a Topology\|basis]], it suffices that preimages of basis elements are open `[Hat p. 11]`.

> [!theorem] Rules for constructing continuous functions
> **Scope**
> - Topological spaces $X$, $Y$, $Z$; $A$ a [[knowledge/math/topology/Subspace Topology\|subspace]] of $X$.
>
> ---
> **Property**
> - Constant maps are continuous.
> - The inclusion $j : A \to X$ is continuous.
> - If $f : X \to Y$ and $g : Y \to Z$ are continuous, so is $g \circ f$.
> - If $f : X \to Y$ is continuous, so is its restriction $f|_A : A \to Y$.
> - Restricting or expanding the range: if $f : X \to Y$ is continuous, so is $f$ viewed as a map into a subspace $Z \subseteq Y$ containing $f(X)$, or into a space $Z$ having $Y$ as a subspace.
> - Local formulation: $f : X \to Y$ is continuous if $X = \bigcup_\alpha U_\alpha$ with each $U_\alpha$ open and each $f|_{U_\alpha}$ continuous.
>
> `[Mun00 Thm 18.2]`; `[Hat p. 11]` for composites and restrictions, `[Hat p. 15, Ex 14]` for the local formulation.

> [!theorem] Pasting Lemma — continuous pieces on closed sets glue
> **Scope**
> - $X = A \cup B$ with $A$, $B$ closed in $X$.
> - $f : A \to Y$ and $g : B \to Y$ continuous, with $f(x) = g(x)$ for every $x \in A \cap B$.
>
> ---
> **Property**
> $h : X \to Y$, $h(x) = f(x)$ for $x \in A$ and $h(x) = g(x)$ for $x \in B$, is continuous.
>
> `[Mun00 Thm 18.3]`. For closed $C \subseteq Y$, $h^{-1}(C) = f^{-1}(C) \cup g^{-1}(C)$ is a union of two sets closed in $A$ and in $B$, hence closed in $X$ ([[knowledge/math/topology/Closed Set#Property\|Closed Set#Property]]).

> [!theorem] Maps into products — continuous iff the coordinates are
> **Scope**
> - $f : A \to X \times Y$, $f(a) = (f_1(a), f_2(a))$, with the [[knowledge/math/topology/Product Topology\|Product Topology]].
>
> ---
> **Property**
> $f$ is continuous $\iff$ its **coordinate functions** $f_1 : A \to X$ and $f_2 : A \to Y$ are continuous.
>
> `[Mun00 Thm 18.4]`, `[Hat p. 13]`. For an arbitrary product with the product topology the same holds coordinatewise `[Mun00 Thm 19.6]`; with the box topology it fails ([[knowledge/math/topology/Product Topology#Arbitrary products\|Product Topology#Arbitrary products]]).

## Example

> [!example] Continuous and not
> - Every map out of a discrete space, and every map into a trivial space, is continuous.
> - The identity $\mathbb R \to \mathbb R_\ell$ is not continuous: $[0, 1)$ is open in $\mathbb R_\ell$, and its preimage is not open in $\mathbb R$. The identity $\mathbb R_\ell \to \mathbb R$ is continuous, because $\mathbb R_\ell$ is finer ([[knowledge/math/topology/example/Topologies on the Real Line\|Topologies on the Real Line]]).
> - For maps $\mathbb R \to \mathbb R$ with the standard topology, this is the $\varepsilon$–$\delta$ continuity of [[knowledge/math/calculus/Continouity\|calculus]].
> - The pasting lemma fails without closedness: on $\mathbb R = (-\infty, 0) \cup [0, \infty)$, the function that is $0$ on the first piece and $1$ on the second is continuous on each piece but not on $\mathbb R$.

## Related

### Descendants
- [[knowledge/math/topology/Homeomorphism\|Homeomorphism]] — bijective, with continuous inverse

### Siblings
- [[knowledge/math/property/map/Homomorphism\|Homomorphism]], [[knowledge/math/property/map/Monotonicity\|Monotonicity]] — the structure-preserving maps of algebra and of orders
- [[knowledge/math/property/map/Lipschitz Map\|Lipschitz Map]] — a quantitative strengthening for metric spaces
