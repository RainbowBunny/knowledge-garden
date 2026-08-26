---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/interactive/multi-prover-interactive-proofs/","dg-note-properties":{}}
---

Reference: https://people.cs.georgetown.edu/jthaler/ProofsArgsAndZK.pdf
## Syntax

> [!definition] Multi-Prover Interactive Proofs
> A $k$-prover [[knowledge/cryptography/verifiable computing/proof/interactive/Interactive Proof Systems#Syntax\|Interactive Proof Protocol]] for a [[knowledge/cs/foundations/Languages\|Language]] $\mathcal L \subseteq \{0, 1\}^*$ involves $k + 1$ parties:
> - The $k + 1$ parties include a probabilistic polynomial time verifier and $k$ provers.
> - The verifier exchanges a sequence of messages with each prover; each prover's message is a function of the input and the messages from $\mathcal V$ that it has seen so far.
> - The interaction produces a transcript $t = (\mathcal V(r), \mathcal P_1, \dots, \mathcal P_k)(x)$, where $r$ denotes $\mathcal V$'s internal randomness.
> - After the transcript $t$ is produces, $\mathcal V$ decides whether to output accept or reject based on $r, t$ and $x$.
> - Denote by $\text{out}(\mathcal V, x, r, \mathcal P_1, \dots, \mathcal P_k)$ the output of verifier $\mathcal V$ on input $x$ given prover strategies $(\mathcal P_1, \dots, \mathcal P_k)$ and that $\mathcal V$'s internal randomness is equal to $r$.

## Property

### Completeness

> [!definition] Completeness Error
> A multi-prover interactive proof system $(\mathcal P_1, \dots, \mathcal P_k)$ is said to have **completeness error** $\delta_c$ if:
> - For every $x \in \mathcal L$,
> $$\Pr_r[\text{out}(\mathcal V, x, r, \mathcal P_1, \dots, \mathcal P_k) = \text{accept}] \geq 1 - \delta_c.$$
 
## Security

### Soundness

> [!definition] Soundness Error
> A multi-prover interactive proof system $(\mathcal P_1, \dots, \mathcal P_k)$ is said to have **soundness error** $\delta_s$ if:
> - For every $x \in \mathcal L$ and every tuple of prover strategies $(\mathcal P_1', \dots, \mathcal P_k')$.
> $$\Pr_r[\text{out}(\mathcal V, x, r, \mathcal P_1, \dots, \mathcal P_k) = \text{accept}] \leq \delta_s.$$
