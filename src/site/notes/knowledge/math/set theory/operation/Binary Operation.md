---
{"dg-publish":true,"permalink":"/knowledge/math/set-theory/operation/binary-operation/","dg-note-properties":{}}
---

Reference:
- https://en.wikipedia.org/wiki/Binary_operation
- https://en.wikipedia.org/wiki/Semigroupoid

## Definition

> [!definition] Binary Operation
> A **binary operation** on a set $S$ is a [[knowledge/math/set theory/Function\|Function]]
> $$\star: S \times S \rightarrow S$$
> mapping every pair of elements of $S$ to an element of $S$.

> [!remark] Closure is in the type
> Totality and closure are not axioms here — $x \star y$ is defined for every $x, y \in S$ and lies in $S$ because the codomain says so. [[knowledge/math/property/operation/Closure\|Closure]] states the version that is *not* automatic: that a **subset** $A \subseteq S$ is closed under $\star$.

## Variant

Each variant relaxes one clause of the definition above. They are not siblings — many-sorted subsumes the other two.

### Partial Operation

> [!definition] Partial Operation
> Relaxes *total*. A **partial binary operation** on $S$ is a function $\star: D \rightarrow S$ defined on a subset $D \subseteq S \times S$. Axioms are then read only over tuples for which both sides are defined.

### External Operation

> [!definition] Left / Right External Operation
> Relaxes *both arguments from $S$*. Given a second set $R$, the **operator domain**:
> - a **left external operation** on $S$ over $R$ is a map $R \times S \rightarrow S$;
> - a **right external operation** on $S$ over $R$ is a map $S \times R \rightarrow S$.
> 
> The two coincide when the operator domain is commutative, which is why scalar multiplication over a [[knowledge/math/algebra/structures/field/Field\|Field]] is written one way only. Over a non-commutative ring they are genuinely different — this is the left/right module distinction.


## Property

Axioms an operation may satisfy: 
- [[knowledge/math/property/operation/Associativity\|Associativity]], [[knowledge/math/property/operation/Commutativity\|Commutativity]], [[knowledge/math/property/operation/Identity Element\|Identity Element]], [[knowledge/math/property/operation/Inverse Element\|Inverse Element]], [[knowledge/math/property/operation/Idempotence\|Idempotence]], [[knowledge/math/property/operation/Alternativity\|Alternativity]].
- [[knowledge/math/property/operation/Distributivity\|Distributivity]] for a pair of operations.
- [[knowledge/math/property/operation/Closure\|Closure]] for a subset.

## Example

- [[knowledge/math/set theory/operation/Binary Operation Examples\|Binary Operation Examples]]