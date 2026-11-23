---
{"dg-publish":true,"permalink":"/knowledge/math/topology/example/topologies-on-the-real-line/","dg-note-properties":{"aliases":["Standard Topology","Lower Limit Topology","K-Topology","R_l","R_K","Sorgenfrey Line"]}}
---

Reference:
- `[Mun00]` — J. R. Munkres, _Topology_, 2nd ed., Prentice Hall, 2000, Chapter 2: §13 (standard, lower limit and $K$-topologies, Lemma 13.4); §14 (the order topology of $\mathbb R$).
- `[Møl]` — J. M. Møller, _General Topology_, lecture notes, University of Copenhagen, Chapter 2: Examples 2.9(1), 2.11, 2.15(1): https://www.math.ku.dk/~moller/e03/3gt/notes/gtnotes.pdf
- `[Hat]` — A. Hatcher, _Notes on Introductory Point-Set Topology_, p. 2 (open sets of $\mathbb R$), p. 4 and Exercise 15 on p. 15 (half-open interval topology): https://pi.math.cornell.edu/~hatcher/Top/TopNotes.pdf

## Intuition

> [!intuition] Why
> Comparing several topologies on one familiar set shows what changes when the open sets change: a set or a sequence can behave differently in each. $\mathbb R_\ell$ and $\mathbb R_K$ are Munkres's standard counterexamples in later chapters.

## Definition

> [!definition] Topologies on the Real Line
> Instantiates:: [[knowledge/math/topology/Topological Space\|Topological Space]]
>
> ---
> On the set $\mathbb R$, with $a < b$ throughout, each of the following is a [[knowledge/math/topology/Basis for a Topology\|basis]]:
> - the open intervals $(a, b)$, generating the **standard topology**;
> - the half-open intervals $[a, b)$, generating the **lower limit topology** $\mathbb R_\ell$;
> - with $K = \{1/n : n \in \mathbb Z_{>0}\}$, the open intervals $(a, b)$ together with the sets $(a, b) \setminus K$, generating the **$K$-topology** $\mathbb R_K$.
>
> `[Mun00 §13]`, `[Møl Ex 2.11]`. Møller calls $\mathbb R_\ell$ the right half-open interval topology, and `[Hat p. 15, Exercise 15]` the half-open interval topology.

## Property

> [!theorem] Comparison — both refine the standard topology, and neither refines the other
> **Scope**
> - The three topologies above.
>
> ---
> **Property**
> $\mathbb R_\ell$ is strictly finer than the standard topology.
> $\mathbb R_K$ is strictly finer than the standard topology.
> $\mathbb R_\ell$ and $\mathbb R_K$ are not comparable.
>
> `[Mun00 Lemma 13.4]`, `[Møl Ex 2.11]`

> [!proof] Why — by [[knowledge/math/topology/Basis for a Topology#Property\|local refinement]]
> - For $x \in (a, b)$, the basis element $[x, b)$ of $\mathbb R_\ell$ satisfies $x \in [x, b) \subseteq (a, b)$. No open interval containing $x$ lies inside $[x, d)$, so $[x, d)$ is open in $\mathbb R_\ell$ but not in the standard topology.
> - Every standard basis element is also one of $\mathbb R_K$. The set $(-1, 1) \setminus K$ is open in $\mathbb R_K$, but every open interval around $0$ meets $K$, so it is not open in the standard topology.
> - $(-1, 1) \setminus K$ is not open in $\mathbb R_\ell$ either, since every $[0, \varepsilon)$ meets $K$. And $[10, 11)$ is not open in $\mathbb R_K$, since every basis element of $\mathbb R_K$ containing $10$ contains points below $10$.

## Example

> [!example] Three descriptions of the standard topology
> - It is the [[knowledge/math/topology/Order Topology\|Order Topology]] of $<$ on $\mathbb R$ `[Mun00 §14]` `[Møl Ex 2.15(1)]`.
> - It is the topology of the metric $|x - y|$: a set is open iff around each of its points it contains an open interval `[Hat p. 2]` ([[knowledge/math/topology/Topological Space#Metric topology\|Topological Space#Metric topology]]).
> - The open rays $(a, \infty)$, $(-\infty, b)$ are a subbasis for it `[Møl Ex 2.9(1)]`.

> [!example] Inside $\mathbb R_\ell$
> Open intervals are open in $\mathbb R_\ell$: $(a, b) = \bigcup_{n} [a + 1/n, b)$, over the $n$ with $a + 1/n < b$. This is the finer-than half of the comparison, seen directly.

## Related

### Prerequisites
- [[knowledge/math/topology/Basis for a Topology\|Basis for a Topology]], [[knowledge/math/topology/Order Topology\|Order Topology]]
