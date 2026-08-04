---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/argument/argument-systems/","dg-note-properties":{}}
---

## Syntax

> [!definition] Argument System
> An **argument system** for a function $f$ is an [[knowledge/cryptography/verifiable computing/proof/Interactive Proof Systems#Syntax\|Interactive Proof]] for $f$ in which the [[knowledge/cryptography/verifiable computing/proof/Interactive Proof Systems#Soundness\|Soundness]] condition is only required to hold against prover strategies that run in polynomial time.

> [!remark]
> Argument systems are sometimes referred to as **computationally sound proofs**.

## Property

### Completeness

- See interactive proof system [[knowledge/cryptography/verifiable computing/proof/Interactive Proof Systems#Completeness\|Completeness]].

### Succinct

> [!definition] Succinct
> We say that an argument system for circuit satisfiability is succinct if the total communication is sublinear in the size of the witness $|w|$.

> [!remark]
> Succinctness is important because:
> - Shorter proofs are always better.
> - Witness are naturally large.
> - Efficient transformations from computer programs to circuit satisfiability often produce circuits with very large witnesses.

> [!remark] Succinct in Verification
> Argument systems that achieve verifier time that is better than the time to decide the relation are considered *succinct in verification*, which is sublinear in the verification time.
> 
> This is extreme important in the case that the language has no witness.

> [!remark] Sublinear
> Sublinear means less that linear, but ideally poly-logarithmic.

## Security

### Knowledge Soundness

> [!remark]
> Knowledge soundness means that not only a witness $w$ exists, but the prover also knows $w$.

### Zero Knowledge

- See interactive proof system [[knowledge/cryptography/verifiable computing/proof/Interactive Proof Systems#Zero Knowledge\|Zero Knowledge]].

