---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/group/special-group/p-group/","dg-note-properties":{}}
---

Reference:
- `[Alu]` — [[academic/Book Reference\|Algebra: Chapter 0]] (P. Aluffi), Chapter IV: Groups, second encounter, Section 1.1: Actions of groups on sets, reminder.
- `[Jud]` — T. W. Judson, _Abstract Algebra: Theory and Applications_: https://abstract.ups.edu/aata/ (read in the HTML edition at https://judsonbooks.org/aata-files/aata-html/; result numbers as there).
- `[ConConj]` — K. Conrad, _Conjugation in a group_, expository notes, Theorems 6.8, 6.9, Corollary 6.11: https://kconrad.math.uconn.edu/blurbs/grouptheory/conjclass.pdf
- `[ConSyl]` — K. Conrad, _The Sylow theorems_, expository notes, equation (2.1), §3: https://kconrad.math.uconn.edu/blurbs/grouptheory/sylowpf.pdf

## Definition

> [!definition] Parameters
> - $p$: a [[knowledge/math/number theory/Prime\|Prime]].
> - $G$: a [[knowledge/math/algebra/structures/group/Group\|Group]].

> [!definition] p-Group
> Extends:: [[knowledge/math/algebra/structures/group/Group\|Group]].
>
> ---
> A $p$-group is a finite [[knowledge/math/algebra/structures/group/Group\|Group]] whose order is a power of a prime integer $p$. `[Alu IV §1.1]`

> [!remark] Judson's definition
> [Jud §15.1] calls $G$ a $p$-group if every element of $G$ has as its order a power of $p$, without assuming $G$ finite. For a finite group the two definitions agree: $G$ is a $p$-group if and only if $|G| = p^n$ `[Jud Cor 15.1.2]`.

## Property

> [!proposition] Fixed points — a $p$-group acting on a finite set
> **Scope**
> - $G$: a $p$-group acting on a finite set $X$, with fixed-point set $\mathrm{Fix}(X)$.
>
> ---
> **Property**
> $$|X| \equiv |\mathrm{Fix}(X)| \pmod p.$$
> Hence if $p \nmid |X|$ the action has a fixed point, and if $p \mid |X|$ then $p \mid |\mathrm{Fix}(X)|$.
>
> `[ConSyl (2.1)]` ([[knowledge/math/algebra/structures/action/Group Action#Property\|Group Action#Property]]): every orbit that is not a fixed point has size a positive power of $p$.

> [!theorem] Nontrivial center — a nontrivial finite $p$-group has $Z(G) \neq \{e\}$
> **Scope**
> - $G$: a nontrivial finite $p$-group.
>
> ---
> **Property**
> $$Z(G) \neq \{e\}.$$
>
> `[ConConj Thm 6.8]`, from the [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]]: $|Z(G)| \equiv |G| \equiv 0 \bmod p$.

> [!theorem] Normal subgroups meet the center
> **Scope**
> - $G$: a nontrivial finite $p$-group.
> - $N \trianglelefteq G$, $N \neq \{e\}$.
>
> ---
> **Property**
> $$N \cap Z(G) \neq \{e\}.$$
>
> `[ConConj Thm 6.9]`: $G$ acts on $N$ by conjugation with fixed points $N \cap Z(G)$, and $|N \cap Z(G)| \equiv |N| \equiv 0 \bmod p$.

> [!proposition] Subgroups of every order — a chain $\{e\} = H_0 \subset \cdots \subset H_n = G$ with $|H_i| = p^i$
> **Scope**
> - $G$: a group of order $p^n$.
>
> ---
> **Property**
> $G$ contains an increasing chain of subgroups of orders $p^0, p^1, \dots, p^n$.
>
> `[ConSyl §3]` — [[knowledge/math/algebra/structures/group/subgroup/Sylow Theorems#Property\|Sylow Theorems#Property]].

> [!corollary] Order $p^2$ — abelian
> Every group of order $p^2$ is abelian `[ConConj Cor 6.11]` — [[Groups of Order p²\|Groups of Order p²]].

## Related

### Properties
- [[knowledge/math/algebra/structures/group/subgroup/Group Center\|Group Center]] — a group of order $p^n$ has a nontrivial center `[Jud Thm 14.2.4]`
- [[knowledge/math/algebra/structures/action/Group Action\|Group Action]] — for an action of a $p$-group on a finite set $A$ with fixed points $Z$, $|Z| \equiv |A| \bmod p$

### Constructions
- [[knowledge/math/algebra/structures/group/subgroup/Sylow Subgroup\|Sylow Subgroup]] — the maximal $p$-subgroups of a finite group
- [[Groups of Order p²\|Groups of Order p²]], [[Groups of Order p³\|Groups of Order p³]], [[Groups of Order p⁴\|Groups of Order p⁴]] — the small $p$-groups

### Prerequisites
- [[knowledge/math/algebra/structures/group/Group Order\|Group Order]] — the order $|G|$
- [[knowledge/math/algebra/structures/action/Class Equation\|Class Equation]]
