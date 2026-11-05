---
{"dg-publish":true,"permalink":"/knowledge/math/foundation/first-order-logic/","dg-note-properties":{}}
---

Reference:
- https://en.wikipedia.org/wiki/Signature_(logic)
- https://en.wikipedia.org/wiki/Lindstr%C3%B6m%27s_theorem

## Intuition

The logic of "for all elements" and "there exists an element" — quantifying over *elements of the carrier*, never over subsets, functions, or the carrier itself. Almost every Scope line in this vault is a first-order signature; almost every axiom in `property/` is a first-order sentence over one.

## Definition

> [!definition] Signature
> A **signature** is a list of constant, function, and relation symbols, each with an arity. A **structure** for a signature is a carrier set with an interpretation of every symbol. *(This is the vault's Scope slot, made official — and the many-sorted version types each symbol by sorts: see [[knowledge/math/set theory/operation/Many-Sorted Operation\|Many-Sorted Operation]].)*

> [!definition] First-Order Logic
> Formulas are built from signature symbols, connectives, and quantifiers ranging over **elements** of the carrier. A structure **models** a sentence if the sentence is true under the interpretation.

## Property

> [!theorem] Why FOL is the reference point
> - **Gödel completeness**: provable = true in every model.
> - **Compactness**: a theory is satisfiable iff every finite fragment is.
> - **Lindström's theorem**: FOL is the *strongest* logic having both compactness and downward Löwenheim–Skolem — its default status is a theorem, not a convention.

> [!remark] What is *not* first-order in this vault
> Completeness of $\mathbb R$ ("every bounded subset has a sup") quantifies over subsets — second-order. A topology is a set of subsets. [[knowledge/math/algebra/category/Category\|Category]]'s objects form a class. These are the Tier-2 cases: the template still applies, the logic behind it changes.