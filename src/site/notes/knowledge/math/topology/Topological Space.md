---
{"dg-publish":true,"permalink":"/knowledge/math/topology/topological-space/","dg-note-properties":{"aliases":["Topology","Open Set","Finer Topology","Coarser Topology","Discrete Topology","Trivial Topology","Finite Complement Topology"]}}
---

Reference:
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, pp. 2–4 (topology, examples, finer and coarser): https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf
- `[Mor]` — S. A. Morris, _Topology Without Tears_, version of October 14, 2007, Definitions 1.1.1, 1.1.6, 1.1.7, 1.3.1: https://www.maths.ed.ac.uk/~v1ranick/papers/morris.pdf
- `[Møl]` — J. M. Møller, _General Topology_, lecture notes, University of Copenhagen, Chapter 2: Definition 2.1, Example 2.2, Definition 2.3: https://www.math.ku.dk/~moller/e03/3gt/notes/gtnotes.pdf
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2, §12: topology, open set, Examples 2, 3, finer and coarser.
- `[Sut]` — A. V. Sutherland, MIT 18.785 _Number Theory I_, Lecture 8 _Complete fields and valuation rings_ and Lecture 9 _Local fields and Hensel's lemmas_: https://math.mit.edu/classes/18.785/2025/LectureNotes8.pdf, https://math.mit.edu/classes/18.785/2025/LectureNotes9.pdf

## Intuition

> [!intuition] Why
> Continuity, convergence and connectedness never use the actual distances, only which points are near which. A topology records exactly that, so these notions get one definition that works for metric spaces, ordered sets, function spaces and spaces with no natural metric.

## Definition

> [!definition] Topological Space
> A **topological space** is a set $X$ together with a collection $\mathcal O$ of subsets of $X$, called **open sets**, such that
> 1. the union of any collection of sets in $\mathcal O$ is in $\mathcal O$;
> 2. the intersection of any finite collection of sets in $\mathcal O$ is in $\mathcal O$;
> 3. both $\emptyset$ and $X$ are in $\mathcal O$.
>
> `[Hat p. 3]`. The collection $\mathcal O$ is a **topology** on $X$, and $U \subseteq X$ is **open** iff $U \in \mathcal O$ `[Mun00 §12]` `[Møl Def 2.1]`.

> [!remark] Two intersections suffice
> `[Mor Def 1.1.1]` asks only that the intersection of any two open sets be open; by induction this gives every finite intersection. Morris also requires $X$ to be nonempty; `[Hat p. 3]`, `[Mun00 §12]` and `[Møl Def 2.1]` do not.

### Finer and coarser

> [!definition] Finer, Coarser, Comparable
> Let $\mathcal T$ and $\mathcal T'$ be topologies on the same set $X$.
> - If $\mathcal T' \supseteq \mathcal T$, then $\mathcal T'$ is **finer** than $\mathcal T$, and $\mathcal T$ is **coarser** than $\mathcal T'$; **strictly** finer or coarser if the inclusion is proper.
> - $\mathcal T$ and $\mathcal T'$ are **comparable** iff one of them contains the other.
>
> `[Mun00 §12]`, `[Hat p. 4]`, `[Møl Def 2.3]`

> [!remark] An order on topologies
> "Finer" is the [[knowledge/math/set theory/order/Partial Order\|Partial Order]] $\supseteq$ on the set of topologies on $X$. The discrete topology is the finest and the trivial topology the coarsest. The order is not total: two topologies can fail [[knowledge/math/property/relation/Comparability\|Comparability]], as $\mathbb R_\ell$ and $\mathbb R_K$ do ([[knowledge/math/topology/example/Topologies on the Real Line\|Topologies on the Real Line]]).

### Metric topology

> [!definition] Topology of a Metric
> In a metric space $(X, d)$, the open balls $B_r(x) = \{y \in X : d(x, y) < r\}$, $r > 0$, form a [[knowledge/math/topology/Basis for a Topology\|basis]] for a topology on $X$: the open sets are the unions of balls. `[Hat p. 8]`

### Compactness and connectedness

> [!definition] Compact, Locally Compact
> - $X$ is **compact** if every collection of open sets whose union is $X$ has a finite subcollection whose union is $X$. `[Hat p. 27]`
> - $X$ is **locally compact** if every point has a compact neighbourhood. `[Sut, Lecture 9, after Def 9.1]`

> [!definition] Connected, Totally Disconnected
> - $X$ is **connected** if it is not the union of two disjoint nonempty open sets. `[Hat p. 16]`
> - The maximal connected subsets are the **connected components**; $X$ is **totally disconnected** if its connected components are points. `[Hat p. 22]`

## Example

> [!example] Topologies on any set
> - **Discrete**: every subset is open, $\mathcal O = \mathcal P(X)$ `[Mun00 §12 Ex 2]` `[Hat p. 4]` `[Mor Def 1.1.6]`.
> - **Trivial**, also called indiscrete: only $\emptyset$ and $X$ are open `[Mun00 §12 Ex 2]` `[Hat p. 4]` `[Mor Def 1.1.7]`.
> - **Finite complement**: $\emptyset$ and every $U$ with $X \setminus U$ finite `[Mun00 §12 Ex 3]` `[Møl Ex 2.2(4)]`; `[Mor Def 1.3.1]` calls it the finite-closed topology.
> - **Particular point**: $\emptyset$ and every set containing a fixed point $p$ `[Møl Ex 2.2(3)]`.

> [!example] Why only finite intersections
> In the finite complement topology on $\mathbb Z$, each $\mathbb Z \setminus \{n\}$ is open, but $\bigcap_{n \neq 0} (\mathbb Z \setminus \{n\}) = \{0\}$ is not: its complement is infinite. The axioms allow arbitrary unions and only finite intersections, and this topology satisfies exactly that.

- $\mathbb R$ with its metric is locally compact and connected.
- [[knowledge/math/number theory/p-adic Number#Topology\|$\mathbb Q_p$]]: locally compact and totally disconnected; $\mathbb Z_p$ is compact and open.

## Related

### Descendants
- [[knowledge/math/topology/Hausdorff Space\|Hausdorff Space]] — distinct points have disjoint neighborhoods

### Properties
- [[knowledge/math/property/topology/T1 Axiom\|T1 Axiom]], [[knowledge/math/property/topology/Hausdorff Axiom\|Hausdorff Axiom]] — the first separation axioms

### Instantiations
- [[knowledge/math/geometry/algebraic geometry/Zariski Topology\|Zariski Topology]] — from algebraic geometry
- [[knowledge/math/topology/example/Topologies on the Real Line\|Topologies on the Real Line]] — standard, lower limit, $K$-topology

### Constructions
- [[knowledge/math/topology/Basis for a Topology\|Basis for a Topology]] — a topology from a basis or a subbasis
- [[knowledge/math/topology/Closed Set\|Closed Set]], [[knowledge/math/topology/Closure and Interior\|Closure and Interior]], [[knowledge/math/topology/Limit Point\|Limit Point]], [[knowledge/math/topology/Convergent Sequence\|Convergent Sequence]] — the vocabulary of §17
- [[knowledge/math/topology/Subspace Topology\|Subspace Topology]], [[knowledge/math/topology/Product Topology\|Product Topology]], [[knowledge/math/topology/Order Topology\|Order Topology]] — new spaces from old ones, and from orders

### Used by
- [[knowledge/math/measure theory/Sigma Algebra#Borel Sigma Algebra\|Sigma Algebra#Borel Sigma Algebra]] — generated by the open sets
- [[knowledge/math/number theory/p-adic Number\|p-adic Number]]

### Prerequisites
- [[knowledge/math/set theory/Set\|Set]], [[knowledge/math/set theory/special set/Power Set\|Power Set]], [[knowledge/math/calculus/Metric Space\|Metric Space]]
