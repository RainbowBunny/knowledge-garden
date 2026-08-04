---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/argument/non-interactive-argument-of-knowledge/","dg-note-properties":{}}
---

Reference: 
- https://www.di.ens.fr/~nitulesc/files/Survey-SNARKs.pdf
- https://eprint.iacr.org/2014/718.pdf

## Syntax

> [!definition] Non-Interactive Argument of Knowledge
> For pairs $(x, w)$ of an [[knowledge/cryptography/verifiable computing/proof/Effective Relation#Basic Definition\|Effective Relation]] $R$ where $x$ is the statement and $w$ is the witness. A non-interactive argument for $R$ is a quadruple of efficient algorithms $(\text{Setup}, \text{Prove}, \text{Verify}, \text{Sim})$:
> - $(\sigma, \tau) \leftarrow \text{Setup}(R)$: The setup algorithm that base on a relation $R$, returns a common reference string $\sigma$ and a simulation trapdoor $\tau$.
> - $\pi \leftarrow \text{Prove}(\sigma, x, w)$: The prover algorithm that takes as input a common reference string $\sigma$ for a relation $R$ and $(x, w) \in R$ and returns an argument $\pi$.
> - $\{0, 1\} \leftarrow \text{Verify}(\sigma, x, \pi)$: The verification algorithm takes as input a common reference string, a statement $u$ and an argument $\pi$ and returns 0 (rejects) or 1 (accepts).
> - $\pi \leftarrow \text{Sim}(\tau, u)$: The simulator takes as input a simulation trapdoor and a statement $x$ and returns an argument $\pi$.

