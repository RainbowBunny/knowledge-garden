---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/linear-multi-prover-interactive-proofs/","dg-note-properties":{}}
---

Reference:
- https://web.cs.ucla.edu/~rafail/PUBLIC/79.pdf

## Syntax

> [!definition] Linear Multi-Prover Interactive Proofs
> ### Parameters
> - $(x, w)$: Element of [[knowledge/cryptography/verifiable computing/proof/Effective Relation\|Effective Relation]] of $\text{NP}$ language.
> - $n$: Proof length.
> - $\ell$: Number of provers
> - $\mathbb F$: Finite field.
> - $\pi_i: \mathbb F^n \rightarrow \mathbb F$: Proof functions.
> 
> ---
> ### Algorithms
> - Verifier $\mathcal V$ generates $q_1, \dots, q_\ell \in \mathbb F^n$ and sends $q_i$ to prover $\mathcal P_i$.
> - Prover $\mathcal P_i$ calculates $\pi_i(q_i)$ and sends back to $\mathcal V$.
> - $\mathcal V$ based on $(x, q_1, \dots, q_\ell, \pi_1, \dots, \pi_\ell)$ and returns $\text{accept}$ and $\text{reject}$.

## Property

### Completeness

> [!definition] Completeness
> For every $x \in L$ and corresponding NP witness $w$, the proofs system have $\delta_c$-completeness:
> $$\Pr[\mathcal V(x, q_1, \dots, q_\ell, \pi_1(q_1), \dots, \pi_\ell(q_\ell)) = \text{accept}] \geq 1 - \delta_c$$

## Security

### Soundness

> [!definition] Soundness
> For every $x \notin L$ and (possibly non-linear and computationally inefficient) proof functions $(\tilde \pi_1, \dots, \tilde \pi_\ell)$, we have
> $$\Pr[\mathcal V(x, q_1, \dots, q_\ell, \tilde \pi_1, \dots, \tilde \pi_\ell) = \text{accept}] \leq \delta_s$$

