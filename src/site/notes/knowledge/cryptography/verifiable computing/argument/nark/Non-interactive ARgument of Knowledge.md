---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/argument/nark/non-interactive-a-rgument-of-knowledge/","dg-note-properties":{}}
---

Reference: 
- https://www.di.ens.fr/~nitulesc/files/Survey-SNARKs.pdf

## Syntax

> [!definition] Non-interactive ARgument of Knowledge
> Let $\mathcal{CS}$ be a [[knowledge/cryptography/verifiable computing/relations/r1cs/Rank-1 Constraint Statisfiability\|R1CS]] system over a finite field $\mathbb F$. A non-interactive argument of knowledge $\Pi_\mathsf{NARK} = (\mathsf{Setup}, \mathsf{Prove}, \mathsf{Verify})$ is a [[knowledge/cryptography/verifiable computing/argument/narg/Non-interactive ARGument\|NARG]] with soundness condition replaced by knowledge soundness:
> - $(\mathrm{crs}, \mathrm{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS})$: On input the security parameter $\lambda$ and $\mathcal{CS}$, the setup algorithm outputs a common reference string $\mathrm{crs}$ and verification state $\mathrm{st}$.
> - $\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathrm{crs}, \mathbf{x}, \mathbf{w})$: On input a common reference string $\mathrm{crs}$, a statement $\mathbf{x}$ and a witness $\mathbf{w}$, the prove algorithms outputs a proof $\boldsymbol{\pi}$.
> - $b \leftarrow \mathsf{Verify}(\mathrm{st}, \mathbf{x}, \boldsymbol{\pi})$: On input the verification state $\mathrm{st}$, a statement $\mathbf{x}$ and a proof $\boldsymbol{\pi}$, the verification algorithm outputs a bit $b \in \{0, 1\}$.


> [!definition] Non-Interactive Zero-Knowledge Argument of Knowledge
> For pairs $(x, w)$ of an [[knowledge/cryptography/verifiable computing/relations/Effective Relation#Basic Definition\|Effective Relation]] $R$ where $x$ is the statement and $w$ is the witness. A non-interactive zero-knowledge argument $\mathsf{NIZKAoK}$ for $R$ is a quadruple of efficient algorithms $(\mathsf{Setup}, \mathsf{Prove}, \mathsf{Verify}, \mathsf{Sim})$:
> - $(\sigma, \tau) \leftarrow \mathsf{Setup}(R)$: The setup algorithm that base on a relation $R$, returns a common reference string $\sigma$ and a simulation trapdoor $\tau$.
> - $\pi \leftarrow \mathsf{Prove}(\sigma, x, w)$: The prover algorithm that takes as input a common reference string $\sigma$ for a relation $R$ and $(x, w) \in R$ and returns an argument $\pi$.
> - $\{0, 1\} \leftarrow \mathsf{Verify}(\sigma, x, \pi)$: The verification algorithm takes as input a common reference string, a statement $u$ and an argument $\pi$ and returns 0 (rejects) or 1 (accepts).
> - $\pi \leftarrow \mathsf{Sim}(\tau, u)$: The simulator takes as input a simulation trapdoor and a statement $x$ and returns an argument $\pi$.

## Property

### Completeness

> [!definition] Completeness
> See [[knowledge/cryptography/verifiable computing/argument/narg/Non-interactive ARGument#Completeness\|NARG Completeness]]

### Succinct

> [!definition] Succinct
> See [[knowledge/cryptography/verifiable computing/argument/narg/Non-interactive ARGument#Succinct\|NARG Succinct]].

## Security

### Non-Adaptive Knowledge Soundness

> [!definition] Non-Adaptive Knowledge Soundness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{find})$ and an efficient extractor $\mathcal{E} = (\mathcal{E}_\mathsf{find})$, we define the knowledge soundness advantage:
> $$\mathsf{Adv}_\mathsf{NARK}^{\mathsf{ks}\mbox{-}\mathsf{na}}(\mathcal{A}, \mathcal{E}) = 
\Pr\!\left[ 
\begin{array}{l}
(\mathbf{x}, \mathbf{w}) \notin \mathcal{R}_\mathcal{CS} \\
\mathsf{Verify}(st, \mathbf{x}, \boldsymbol{\pi}^*) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathbf{x}, \boldsymbol{\pi}^*) \leftarrow \mathcal{A}_\mathsf{find}(\mathcal{CS}) \\
(\mathrm{crs}, \mathrm{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS}) \\
\mathbf{w} \leftarrow \mathcal{E}_\mathsf{find}(1^\lambda, \mathcal{CS}, \mathrm{crs}, \mathrm{st}, \mathbf{x})
\end{array} \right]$$

### Adaptive Knowledge Soundness

> [!definition] Adaptive Knowledge Soundness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{find})$ and an efficient extractor $\mathcal{E}_\mathsf{NARK}$, we define the non-adaptive knowledge soundness advantage:
> $$\mathsf{Adv}_\mathsf{NARK}^{\mathsf{ks}\mbox{-}\mathsf{a}}(\mathcal{A}, \mathcal{E}) = 
\Pr\!\left[ 
\begin{array}{l}
(\mathbf{x}, \mathbf{w}) \notin \mathcal{R}_\mathcal{CS} \\
\mathsf{Verify}(st, \mathbf{x}, \boldsymbol{\pi}^*) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathrm{crs}, \mathrm{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS}) \\
(\mathbf{x}, \boldsymbol{\pi}^*) \leftarrow \mathcal{A}_\mathsf{find}(\mathcal{CS}, \mathrm{crs}, \mathrm{st}) \\
\mathbf{w} \leftarrow \mathcal{E}_\mathsf{find}(1^\lambda, \mathcal{CS}, \mathrm{crs}, \mathrm{st}, \mathbf{x})
\end{array} \right]$$

### Zero-Knowledge

> [!definition] Zero-Knowledge
> See [[knowledge/cryptography/verifiable computing/argument/narg/Non-interactive ARGument#Zero-Knowledge\|NARG Zero-Knowledge]].

