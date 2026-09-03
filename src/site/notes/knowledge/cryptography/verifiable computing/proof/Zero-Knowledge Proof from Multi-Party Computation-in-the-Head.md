---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/zero-knowledge-proof-from-multi-party-computation-in-the-head/","dg-note-properties":{}}
---

Reference:
- https://dl.acm.org/doi/10.1145/1250790.1250794

## Syntax

> [!scheme] Zero-Knowledge Proof from Multi-Party Computation
> Let $\mathcal{R}$ be an [[knowledge/cryptography/verifiable computing/relations/Effective Relation\|Effective Relation]]. Let $f$ be the following $(n + 1)$- argument function $(n \geq 3)$, corresponding to $R$:
> $$f(x, w_1, \dots, w_n) = \mathcal{R}(x, w_1 \oplus \dots \oplus w_n)$$
> where $(w_i)_{i \in [n]}$ are bit strings. 
> We also require some primitives:
> - $\Pi_{\mathsf{MPC}}$: [[knowledge/cryptography/verifiable computing/secure computation/Multi-Party Computation-in-the-Head\|Multi-Party Computation-in-the-Head]] for the function $f$ above.
> - $\mathcal{CS} = (\mathsf{Com}, \mathsf{Verify})$: [[knowledge/cryptography/verifiable computing/commitment/Commitment Scheme\|Commitment Scheme]].
> 
> The interaction protocol works as follow:
> $$\begin{array}{lcl} 
\mathsf{Prover} & & \mathsf{Verifier} \\[4pt] 
(n, x, w) & & (n, x) \\[6pt] 
(w_1, \dots, w_{n - 1}) \xleftarrow{\$} (\{0, 1\}^m)^n & & \\ 
w_n \leftarrow w \oplus w_1 \oplus \dots \oplus w_{n - 1} & & \\
(\mathsf{View}_1, \dots, \mathsf{View}_n) \leftarrow \Pi_{\mathsf{MPC}}& & \\
\{(c_i, o_i) \leftarrow \mathsf{Com}(\mathsf{View}_i)\}_{i \in [n]} & \xrightarrow{(c_i)_{i \in [n]}} & \\
& \xleftarrow{i, j} & i \xleftarrow{\$} [n], j \xleftarrow{\$} [n] \backslash i \\
& \xrightarrow{\mathsf{View}_i, o_i, \mathsf{View}_j, o_j} &
\end{array}$$
> The verifier accepts if and only if:
> - $\mathsf{Verify}(\mathsf{View}_i, c_i, o_i) = \mathsf{Verify}(\mathsf{View}_j, c_j, o_j) = 1$ (Commitment are consistent).
> - $\mathsf{Out}_i(\mathsf{View}_i) = \mathsf{Out}_j(\mathsf{View}_j) = 1$ (Output of the function is 1).
> - The two views are consistent with each other.

## Property

### Completeness

> [!property] Completeness
> If $(x, w) \in R$ and the prover is honest (Bullet 1, 3) then, since $w_1 \oplus \dots \oplus w_n = w$ and $\Pi_f$ is perfectly correct, the views $\mathsf{View}_i$ always have output $1$ (Bullet 2).

### Soundness

