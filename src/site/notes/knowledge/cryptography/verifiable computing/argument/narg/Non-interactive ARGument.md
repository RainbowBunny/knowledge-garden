---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/argument/narg/non-interactive-ar-gument/","dg-note-properties":{}}
---

Reference:
- https://eprint.iacr.org/2022/1690.pdf (LUNA, CCS '2024)

## Syntax

> [!definition] Non-interactive ARGument
> Let $\mathcal{CS}$ be a [[knowledge/cryptography/verifiable computing/relations/r1cs/Rank-1 Constraint Statisfiability\|R1CS]] system over a finite field $\mathbb F$. A non-interactive argument in the pre-processing model for $\mathcal{CS}$ is a tuple $\Pi_\mathsf{NARG} = (\mathsf{Setup}, \mathsf{Prove}, \mathsf{Verify})$ with the following properties:
> - $(\mathrm{crs}, \mathrm{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS})$: On input the security parameter $\lambda$ and $\mathcal{CS}$, the setup algorithm outputs a common reference string $\mathrm{crs}$ and verification state $\mathrm{st}$.
> - $\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathrm{crs}, \mathbf{x}, \mathbf{w})$: On input a common reference string $\mathrm{crs}$, a statement $\mathbf{x}$ and a witness $\mathbf{w}$, the prove algorithms outputs a proof $\boldsymbol{\pi}$.
> - $b \leftarrow \mathsf{Verify}(\mathrm{st}, \mathbf{x}, \boldsymbol{\pi})$: On input the verification state $\mathrm{st}$, a statement $\mathbf{x}$ and a proof $\boldsymbol{\pi}$, the verification algorithm outputs a bit $b \in \{0, 1\}$.

## Property

### Completeness

> [!definition] Completeness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{find})$, we define the completeness advantage (sometimes refer as completeness error $\varepsilon_c$):
>  $$\mathsf{Adv}_\mathsf{NARG}^\mathsf{com}(\mathcal{A}) = 
\Pr\!\left[ 
\begin{array}{l}
(x, w) \in R \\
\mathsf{Verify}(\sigma, x, \pi) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathrm{crs}, \mathrm{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS}) \\
(x, w) \leftarrow \mathcal{A}_\mathsf{find}(\mathrm{crs}, \mathrm{st}) \\
\pi \leftarrow \mathsf{Prove}(\mathrm{crs}, x, w)
\end{array} \right]$$

### Succinct

> [!definition] Succinct
> There exists a polynomial $p$, independent of $\mathcal{CS}$:
> - $\mathsf{Setup}$ and $\mathsf{Prove}$ runs in time $p(\lambda + |\mathcal{CS}|)$.
> - $\mathsf{Verify}$ runs in time $p(\lambda + |x| + \log|\mathcal{CS}|)$.
> - $|\pi| \leq p(\lambda + \log|\mathcal{CS}|)$.

## Security

### Non-Adaptive Soundness

> [!definition] Non-Adaptive Soundness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathrm{find})$, we define the soundness advantage:
> $$\mathsf{Adv}_\mathsf{NARG}^{\mathsf{snd}\mbox{-}\mathsf{na}}(\mathcal{A}) =  
\Pr\!\left[ 
\begin{array}{l}
\mathbf{x} \notin \mathcal{L}_\mathcal{CS} \\
\mathsf{Verify}(st, \mathbf{x}, \boldsymbol{\pi}) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathbf{x}, \boldsymbol{\pi}^*) \leftarrow \mathcal{A}_\mathrm{find}(\mathcal{CS}) \\
(\mathrm{crs}, \mathrm{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS})
\end{array} \right]$$

### Adaptive Soundness

> [!definition] Adaptive Soundness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathrm{find})$, we define the soundness advantage:
> $$\mathsf{Adv}_\mathsf{NARG}^{\mathsf{snd}\mbox{-}\mathsf{a}}(\mathcal{A}) =  
\Pr\!\left[ 
\begin{array}{l}
\mathbf{x} \notin \mathcal{L}_\mathcal{CS} \\
\mathsf{Verify}(st, \mathbf{x}, \mathbf{Q}^T \boldsymbol{\pi}^*) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathrm{crs}, \mathrm{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS}) \\
(\mathbf{x}, \boldsymbol{\pi}^*) \leftarrow \mathcal{A}_\mathrm{find}(\mathcal{CS}, \mathrm{crs}, \mathrm{st})
\end{array} \right]$$

### Zero-Knowledge

> [!definition] Zero-Knowledge
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{find}, \mathcal{A}_\mathsf{guess})$ and simulator $\mathcal{S} = (\mathcal{S}_\mathsf{setup}, \mathcal{S}_\mathsf{prove})$, we define the zero-knowledge advantage:
> $$\mathsf{Adv}_\mathsf{NARG}^\mathsf{zk}(\mathcal{A}, \mathcal{S}) = 
\left|\; \Pr\!\left[
\begin{array}{l}
b = 1
\end{array}
\;\middle |\; 
\begin{array}{l}
(\mathsf{crs}, \mathsf{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS}) \\
(\mathbf{x}, \mathbf{w}) \leftarrow \mathcal{A}_\mathsf{find}(\mathcal{CS}, \mathrm{crs}, \mathrm{st}) \\
\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathrm{crs}, \mathbf{x}, \mathbf{w}) \\
b \leftarrow \mathcal{A}_\mathsf{guess}(\boldsymbol{\pi})
\end{array} \right] 
\;- 
\Pr\!\left[
\begin{array}{l}
b = 1
\end{array}
\;\middle |\; 
\begin{array}{l}
(\widetilde{\mathrm{crs}}, \widetilde{\mathbf{st}}, \mathrm{st}_\mathcal{S}) \leftarrow \mathcal{S}_\mathsf{setup}(1^\lambda, \mathcal{CS}) \\
(\widetilde{\mathrm{st}}, \widetilde{\mathbf{Q}}, \mathrm{st}_{\mathcal{S}}) \leftarrow \mathcal{S}_\mathsf{query}(\mathcal{CS}) \\
\widetilde{\boldsymbol{\pi}} \leftarrow \mathcal{S}_\mathsf{prove}(\mathrm{st}_\mathcal{S}, \mathbf{x}) \\
b \leftarrow \mathcal{A}_\mathsf{guess}(\widetilde{\boldsymbol{\pi}})
\end{array} \right] 
\right|.$$
