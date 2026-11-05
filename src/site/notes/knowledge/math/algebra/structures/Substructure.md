---
{"dg-publish":true,"permalink":"/knowledge/math/algebra/structures/substructure/","dg-note-properties":{}}
---

Reference:
- `[BS81]` — S. Burris, H. P. Sankappanavar, _A Course in Universal Algebra_ (1981; Millennium Edition): https://math.uwaterloo.ca/~snburris/htdocs/ualg.html — Chapter II, Definition 1.1; Definition 2.2 and the remarks after it (read at https://people.math.sc.edu/mcnulty/alglatvar/burrissanka.pdf).

The origin note for **sub-structures**: stated once, over any signature. [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]], [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]] and [[knowledge/math/algebra/structures/ring/module/Submodule\|Submodule]] say `Extends:: [[Substructure]]` and carry only what their structure adds.

## Definition

> [!definition] Parameters
> - $F$: a signature, as in [[knowledge/math/property/map/Homomorphism\|Homomorphism]]'s Condition — a set of operation symbols, each with an arity $n \geq 0$; a symbol of arity $0$ is a constant.
> - $\mathbf A = (A, (f^{\mathbf A})_{f \in F})$: a structure of signature $F$.
> - $B \subseteq A$: a subset of its carrier.

> [!definition] Substructure
> $B$ is **closed** in $\mathbf A$ (a *subuniverse*) if it is closed under every operation of the signature: for every $f \in F$ of arity $n$ and all $b_1, \dots, b_n \in B$,
> $$f^{\mathbf A}(b_1, \dots, b_n) \in B.$$
> In particular $B$ contains every constant of the signature: this is [[knowledge/math/property/operation/Closure\|Closure]] for the whole signature.
>
> A structure $\mathbf B = (B, (f^{\mathbf B})_{f \in F})$ of the same signature is a **substructure** (subalgebra) of $\mathbf A$, written $\mathbf B \leq \mathbf A$, if $B \subseteq A$ and every operation of $\mathbf B$ is the restriction of the corresponding operation of $\mathbf A$:
> $$f^{\mathbf B} = f^{\mathbf A}|_{B^n} \quad \text{for every } f \in F \text{ of arity } n.$$
> `[BS81 II Def 2.2]`

> [!remark]
> The carrier of a substructure is a nonempty closed subset. The empty set can be closed (when $F$ has no constants), but it is not the carrier of any substructure. `[BS81 II §2]`

> [!remark] The inclusion form
> $\mathbf B \leq \mathbf A$ iff $B \subseteq A$ and the inclusion $B \hookrightarrow A$ is a [[knowledge/math/property/map/Homomorphism\|Homomorphism]] — the form [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]], [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]] and [[knowledge/math/algebra/structures/ring/module/Submodule\|Submodule]] already use. For the inclusion, the homomorphism condition reads $f^{\mathbf B}(b_1, \dots, b_n) = f^{\mathbf A}(b_1, \dots, b_n)$, which is the restriction condition above.

## Example

- [[knowledge/math/algebra/structures/ring/subring/Ring Center\|Ring Center]] — an example: always a subring.

## Related

### Descendants

| where | what the structure adds |
| --- | --- |
| [[knowledge/math/algebra/structures/group/subgroup/Subgroup\|Subgroup]] | the one-step criterion $ab^{-1} \in H$ |
| [[knowledge/math/algebra/structures/ring/subring/Subring\|Subring]] | $1$ is a constant of the signature, so a subring contains it — which is why an [[knowledge/math/algebra/structures/ring/ideal/Ideal\|Ideal]] is usually not a subring |
| [[knowledge/math/algebra/structures/ring/module/Submodule\|Submodule]] | a subgroup closed under the $R$-action |
| [[knowledge/math/algebra/linear algebra/Vector Spaces#Subspace\|Vector Spaces#Subspace]] | the linear-algebra name |
