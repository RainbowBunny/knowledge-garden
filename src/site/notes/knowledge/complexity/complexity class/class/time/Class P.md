---
{"dg-publish":true,"permalink":"/knowledge/complexity/complexity-class/class/time/class-p/","dg-note-properties":{"aliases":["P","Polynomial Time"]}}
---

Reference:
- `[AB09]` — S. Arora, B. Barak, _Computational Complexity: A Modern Approach_, Cambridge University Press, 2009, Chapter 1: The computational model —and why it doesn’t matter, Section 1.6: The Class P, Definition 1.13, p. 25; Chapter 6: Boolean circuits, Section 6.2: Uniformly Generated Circuits; Section 6.2.1: Logspace-uniform Families.
- `[Sip]` — M. Sipser, _Introduction to the Theory of Computation_ (edition not recorded), Chapter 7: Time Complexity, Section 7.2: The Class P.

## Intuition

> [!intuition] Why
> P is the formal stand-in for efficiently solvable. Polynomial time is chosen because it is robust, the same for every reasonable machine model, and closed under composition, so efficient algorithms built from efficient parts stay efficient.

## Definition

> [!definition] Class P
> Requires:: [[knowledge/complexity/complexity class/generator/time/Class DTIME\|Class DTIME]]
> 
> ---
> $$\mathsf{P} = \bigcup_{c \geq 1} \mathsf{DTIME}(n^c).$$
> `[AB09 Def 1.13]`

> [!definition] Class P (Machine Form)
> $L \in \mathsf P$ iff there are a deterministic Turing machine $M$ and a polynomial $p$ such that
> - on input $x$, $M$ halts after at most $p(|x|)$ steps;
> - $M(x) = 1$ iff $x \in L$.

> [!remark] Role of Class P
> - $\mathsf{P}$ is the same for every model of computation that simulates the deterministic Turing machine, and is simulated by it, with polynomial overhead: one tape or many, any alphabet ([[knowledge/complexity/complexity class/Complexity Class#Machine model\|Complexity Class#Machine model]]).
> - $\mathsf{P}$ is taken as the class of problems that are efficiently solvable; `[AB09 §1.6]` discusses the criticisms of this reading.

## Property

> [!proposition] Closed under reductions — easy targets give easy sources
> **Scope**
> - Languages $A$, $B$ with $A \leq_p B$ ([[knowledge/complexity/complexity class/reducibility/Polynomial-time Karp Reducibility\|Polynomial-time Karp Reducibility]]).
>
> ---
> **Property**
> $B \in \mathsf P \Rightarrow A \in \mathsf P$.
>
> Compose the reduction with the algorithm for $B$; a polynomial of a polynomial is a polynomial.

> [!theorem] Uniform circuits — P is P/poly made uniform
> **Scope**
> - [[knowledge/complexity/complexity class/class/circuit/Class Ppoly\|Class Ppoly]] restricted to [[knowledge/complexity/circuit/P-Uniform Circuit Family\|P-uniform]] or [[knowledge/complexity/circuit/Log-Space Uniform Circuit Family\|log-space uniform]] circuit families.
>
> ---
> **Property**
> Either restriction gives exactly $\mathsf P$.
>
> `[AB09 §6.2]`

## Example

> [!example] Members of P
> - $\mathsf{CONNECTED} = \{\langle G \rangle : G \text{ is a connected undirected graph}\}$, and [[knowledge/complexity/problem/graph/Vertex Path\|PATH]].
> - $\mathsf{TRIANGLE} = \{\langle G \rangle : G \text{ contains a triangle}\}$.
> - [[knowledge/complexity/problem/graph/Two Coloring\|2COL]], [[knowledge/complexity/problem/number/Composite Number\|COMPOSITES]], [[knowledge/complexity/problem/number/Linear Programming\|Linear Programming]].
> - [[knowledge/math/number theory/Number Theory#Divisibility and greatest common divisors\|RELPRIME]], and every context-free language `[Sip §7.2]`.

## Related

### Siblings
- [[knowledge/complexity/complexity class/class/time/Class NP\|Class NP]] — verification instead of decision; [[knowledge/complexity/conjectures/P vs NP\|P vs NP]]
- [[knowledge/complexity/complexity class/class/time/Class EXP\|Class EXP]] — strictly larger, by the [[knowledge/complexity/theorem/Time Hierarchy Theorem\|Time Hierarchy Theorem]]
