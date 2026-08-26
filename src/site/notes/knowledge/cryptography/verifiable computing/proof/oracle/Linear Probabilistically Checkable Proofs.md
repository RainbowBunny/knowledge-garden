---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/oracle/linear-probabilistically-checkable-proofs/","dg-note-properties":{}}
---

	Reference:
- https://eprint.iacr.org/2022/1690.pdf (LUNA, CCS '24)

## Syntax

> [!definition] Linear PCP
> Let $\mathbb{F}$ be a finite field and $\mathcal{CS} = (n, N_g, N_v, \{a_i, b_i, c_i\}_{i \in [N_g]})$ an [[knowledge/cryptography/verifiable computing/relations/r1cs/Rank-1 Constraint Satisfiability#Basic Definition\|R1CS]] over $\mathbb{F}$. A **$k$-query input-independent linear PCP** for $\mathcal{CS}$ with query length $m$ is a tuple of algorithms $\Pi_{\mathsf{LPCP}} = (\mathsf{Query}, \mathsf{Prove}, \mathsf{Verify})$:
> - $(\mathrm{st}, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal {CS})$: The query generation algorithms outputs a query matrix $\mathbf{Q} \in \mathbb{F}^{m \times k}$ and a verification state $\mathrm{st}$. 
> - $\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathcal{CS}, \mathbf{x}, \mathbf{w})$: On input the statement $\mathbf{x} \in \mathbb{F}^n$ and a witness $\mathbf{w} \in \mathbb{F}^{N_v - n}$, the prove algorithm outputs a proof $\boldsymbol{\pi} \in \mathbb{F}^m$.
> - $b \leftarrow \mathsf{Verify}(\mathrm{st}, \mathbf{x}, \mathbf{a})$: On input verification state $\mathrm{st}$, the statement $\mathbf{x} \in \mathbb{F}^n$, and a vector of responses $\mathbf{a} \in \mathbb{F}^k$, the verification algorithm outputs a bit $b \in \{0, 1\}$.

> [!definition] Linear Oracle
> For $\boldsymbol{\pi} \in \mathbb F^m$ and $\mathbf{Q} \in \mathbb{F}^{m \times k}$, the responses $\mathbf{a}$ is calculated as follow:
> $$\mathbf a_{\boldsymbol\pi, \mathbf Q} := \mathbf Q^T\boldsymbol\pi = \big(\langle \mathbf q_1, \boldsymbol\pi\rangle, \dots, \langle \mathbf q_k, \boldsymbol\pi\rangle\big) \in \mathbb F^k.$$
> Note that the verifier $\mathcal V$ only has access to this response, not the proof string $\boldsymbol{\pi}$.

## Property

### Completeness

> [!definition] Completeness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{find})$, we define the completeness advantage:
> $$\mathsf{Adv}_\mathsf{LPCP}^\mathsf{com}(\mathcal{A}) =  
\Pr\!\left[ 
\begin{array}{l}
\mathcal{CS}(\mathbf{x}, \mathbf{w}) = 1 \\
\mathsf{Verify}(st, \mathbf{x}, Q^T \boldsymbol{\pi}) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathrm{st}, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS}) \\
(\mathbf{x}, \mathbf{w}) \leftarrow \mathcal{A}_\mathsf{find}(\mathcal{CS}) \\
\pi \leftarrow \mathsf{Prove}(\mathcal{CS}, \mathbf{x}, \mathbf{w})
\end{array} \right]$$

## Security

### Non-Adaptive Soundness

> [!definition] Non-Adaptive Soundness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathrm{find})$, we define the soundness advantage:
> $$\mathsf{Adv}_\mathsf{LPCP}^{\mathsf{nsnd}\mbox{-}\mathsf{na}}(\mathcal{A}) =  
\Pr\!\left[ 
\begin{array}{l}
\mathbf{x} \notin \mathcal{L}_\mathcal{CS} \\
\mathsf{Verify}(st, \mathbf{x}, \mathbf{Q}^T \boldsymbol{\pi}^*) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathbf{x}, \boldsymbol{\pi}^*) \leftarrow \mathcal A_\mathrm{find}(\mathcal{CS}) \\
(st, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS})
\end{array} \right]$$

### Adaptive Soundness

> [!definition] Adaptive Soundness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathrm{find})$, we define the soundness advantage:
> $$\mathsf{Adv}_\mathsf{LPCP}^{\mathsf{snd}\mbox{-}\mathsf{a}}(\mathcal{A}) =  
\Pr\!\left[ 
\begin{array}{l}
\mathbf{x} \notin \mathcal{L}_\mathcal{CS} \\
\mathsf{Verify}(st, \mathbf{x}, \mathbf{Q}^T \boldsymbol{\pi}^*) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(st, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS}) \\
(\mathbf{x}, \boldsymbol{\pi}^*) \leftarrow \mathcal A_\mathrm{find}(\mathcal{CS})
\end{array} \right]$$

### Non-Adaptive Knowledge Soundness

> [!definition] Non-Adaptive Knowledge Soundness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{find})$ and an efficient extractor $\mathcal{E} = (\mathcal{E}_\mathsf{find})$, we define the knowledge soundness advantage:
> $$\mathsf{Adv}_\mathsf{LPCP}^{\mathsf{ks}\mbox{-}\mathsf{na}}(\mathcal{A}, \mathcal{E}) = 
\Pr\!\left[ 
\begin{array}{l}
(\mathbf{x}, \mathbf{w}) \notin \mathcal{R}_\mathcal{CS} \\
\mathsf{Verify}(st, \mathbf{x}, \mathbf{Q}^T \boldsymbol{\pi}^*) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathbf{x}, \boldsymbol{\pi}^*) \leftarrow \mathcal{A}_\mathsf{find}(\mathcal{CS}) \\
(\mathrm{st}, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS}) \\
\mathbf{w} \leftarrow \mathcal{E}_\mathsf{find}(\mathcal{CS}, \mathbf{x}, \boldsymbol{\pi}^*)
\end{array} \right]$$

### Adaptive Knowledge Soundness

> [!definition] Adaptive Knowledge Soundness
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{find})$ and an efficient extractor $\mathcal{E} = (\mathcal{E}_\mathsf{find})$, we define the non-adaptive knowledge soundness advantage:
> $$\mathsf{Adv}_\mathsf{LPCP}^{\mathsf{ks}\mbox{-}\mathsf{a}}(\mathcal{A}, \mathcal{E}) = 
\Pr\!\left[ 
\begin{array}{l}
(\mathbf{x}, \mathbf{w}) \notin \mathcal{R}_\mathcal{CS} \\
\mathsf{Verify}(st, \mathbf{x}, \mathbf{Q}^T \boldsymbol{\pi}^*) = 1
\end{array} 
\;\middle |\; 
\begin{array}{l}
(\mathrm{st}, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS}) \\
(\mathbf{x}, \boldsymbol{\pi}^*) \leftarrow \mathcal{A}_\mathsf{find}(\mathcal{CS}, \mathrm{st}, \mathbf{Q}) \\
\mathbf{w} \leftarrow \mathcal{E}_\mathsf{find}(\mathcal{CS}, \mathbf{x}, \boldsymbol{\pi}^*)
\end{array} \right]$$

### Honest-Verifier Zero Knowledge

> [!definition] Honest-Verifier Zero Knowledge
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{choose}, \mathcal{A}_\mathsf{guess})$ and simulator $\mathcal{S} = (\mathcal{S}_\mathsf{query}, \mathcal{S}_\mathsf{prove})$, we define the honest-verifier zero knowledge advantage:
> $$\mathsf{Adv}_\mathsf{LPCP}^\mathsf{hvzk}(\mathcal A, \mathcal S) = 
\left|\; \Pr\!\left[
\begin{array}{l}
b = 1
\end{array}
\;\middle |\; 
\begin{array}{l}
(\mathbf{x}, \mathbf{w}) \leftarrow \mathcal{A}_\mathsf{choose}(\mathcal{CS}) \\
(\mathrm{st}, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS}) \\
\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathcal{CS}, \mathbf{x}, \mathbf{w}) \\
\mathbf{a} \leftarrow \mathbf{Q}^T \boldsymbol{\pi}\\
b \leftarrow \mathcal{A}_\mathsf{guess}(\mathrm{st}, \mathbf{Q}, \mathbf{a})
\end{array} \right] 
\;- 
\Pr\!\left[
\begin{array}{l}
b = 1
\end{array}
\;\middle |\; 
\begin{array}{l}
(\mathbf{x}, \mathbf{w}) \leftarrow \mathcal{A}_\mathsf{choose}(\mathcal{CS}) \\
(\widetilde{\mathrm{st}}, \widetilde{\mathbf{Q}}, \mathrm{st}_{\mathcal{S}}) \leftarrow \mathcal{S}_\mathsf{query}(\mathcal{CS}) \\
\widetilde{\mathbf{a}} \leftarrow \mathcal{S}_\mathsf{prove}(\mathrm{st}_\mathcal{S}, \mathbf{x}) \\
b \leftarrow \mathcal{A}_\mathsf{guess}(\mathrm{st}, \mathbf{Q}, \widetilde{\mathbf{a}})
\end{array} \right] 
\right|.$$

### Honest-Verifier Zero Knowledge with Leakage

> [!definition] Honest-Verifier Zero Knowledge with Leakage
> For any adversary $\mathcal{A} = (\mathcal{A}_\mathsf{choose}, \mathcal{A}_\mathsf{guess})$ and simulator $\mathcal{S} = (\mathcal{S}_\mathsf{query}, \mathcal{S}_\mathsf{prove})$, we define the honest-verifier zero knowledge advantage:
> $$\mathsf{Adv}_\mathsf{LPCP}^{\mathsf{hvzk}\mbox{-}\mathcal{D}}(\mathcal A, \mathcal S) = 
\left|\; \Pr\!\left[
\begin{array}{l}
b = 1
\end{array}
\;\middle |\; 
\begin{array}{l}
(\mathbf{x}, \mathbf{w}) \leftarrow \mathcal{A}_\mathsf{choose}(\mathcal{CS}) \\
(\mathrm{st}, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS}) \\
\mathbf{Z} \leftarrow \mathcal D \\
\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathcal{CS}, \mathbf{x}, \mathbf{w}) \\
b \leftarrow \mathcal{A}_\mathsf{guess}(\mathrm{st}, \mathbf{Q}, [\mathbf{Q}^T \pi]_q, \mathbf{Z}, [\mathbf{Z}^T \pi]_q)
\end{array} \right] 
\;- 
\Pr\!\left[
\begin{array}{l}
b = 1
\end{array}
\;\middle |\; 
\begin{array}{l}
(\mathbf{x}, \mathbf{w}) \leftarrow \mathcal{A}_\mathsf{choose}(\mathcal{CS}) \\
(\widetilde{\mathrm{st}}, \widetilde{\mathbf{Q}}, \widetilde{\mathbf{Z}}, \mathrm{st}_{\mathcal{S}}) \leftarrow \mathcal{S}_\mathsf{query}(\mathcal{CS}) \\
(\widetilde{\mathbf{a}}, \widetilde{\mathbf{b}}) \leftarrow \mathcal{S}_\mathsf{prove}(\mathrm{st}_\mathcal{S}, \mathbf{x}) \\
b \leftarrow \mathcal{A}_\mathsf{guess}(\mathrm{st}, \mathbf{Q}, \widetilde{\mathbf{a}}, \widetilde{\mathbf{Z}}, \widetilde{\mathbf{b}})
\end{array} \right] 
\right|.$$
> Where $R_q$ is polynomial ring mod $q$.

