---
{"dg-publish":true,"permalink":"/knowledge/math/property/map/homomorphism/","dg-note-properties":{}}
---

Reference:
- https://en.wikipedia.org/wiki/Signature_(logic)

## Intuition

A map that respects structure: do the operation then map, or map then do the operation, and you land in the same place. Every "…-morphism" in the vault is this with a particular signature filled in.

## Definition

> [!definition] Homomorphism
> ### Scope
> A [[knowledge/math/set theory/Function\|Map]] $\varphi: A \rightarrow B$.
> 
> ---
> ### Condition
> $A$ and $B$ carry structures over the **same signature** - the same operation symbols with the same arities (See [[knowledge/math/foundation/First-Order Logic\|First-Order Logic]]).
> 
> ---
> ### Property
> $\varphi$ is a **homomorphism** iff it commutes with every operation of the signature: for each $n$-ary symbol $\star$, 
> $$\varphi(\star_A(x_1, \dots, x_n)) = \star_B(\varphi(x_1), \dots, \varphi(x_n))$$ 
> for all $x_1, \dots, x_n \in A$. In particular, nullary symbols (constants such as identities) must be preserved.

> [!remark] The signature is what makes this statable
> Without a shared signature, "preserves the structure" has no referent. This is the one place the vault's [[knowledge/math/foundation/First-Order Logic\|Signature]] framing is not just organisational but load-bearing.