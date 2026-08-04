---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/scheme/parallel-commitments-with-linear-decommitments/","dg-note-properties":{}}
---

Reference:
- https://web.cs.ucla.edu/~rafail/PUBLIC/79.pdf
## Scheme

> [!scheme] Parallel Commitments with Linear Decommitments
> ### Parameters
> - $n$: Dimension of finite field.
> - $\ell$: Number of sender.
> - $\mathbb F$: Finite field.
> 
> ---
> ### Building Block
> - Homomorphic Encryption Scheme $E = (\text{Gen}, \text{Enc}, \text{Dec})$.
> 
> ---
> ### Algorithms
> - **Commitment Phase**:
> $$\begin{array}{lcl} 
\mathcal R & & \mathcal S \\[4pt] 
& & (d_i \in \mathbb F^n, f_{d_i}(q) = \langle q_i, d_i \rangle) \\[6pt] 
(pk, sk) \leftarrow \text{Gen}() & & \\[6pt]
r_i \xleftarrow{\$} \mathbb F^n &  & \\[6pt] 
\text{Enc}(pk, r_i) & \xrightarrow{pk, \text{Enc}(pk, r_i)} & \\[6pt] 
s_i \leftarrow \text{Dec}(sk, e_i) & \xleftarrow{e} & e_i \leftarrow \text{Enc}(pk, f_{d_i}(r_i))\\[6pt]
\end{array}$$
> - **Decommitment Phase**:
> $$\begin{array}{lcl} 
\mathcal R & & \mathcal S \\[4pt] 
(q_i \in \mathbb F^n, r_i \in \mathbb F^n, s_i \in \mathbb F) & & (d_i \in \mathbb F^n, f_{d_i}(q) = \langle q_i, d_i \rangle) \\[6pt] 
\alpha_i \xleftarrow{\$} \mathbb F & \xrightarrow{(q, r + \alpha q)} & \\[6pt]
b_i \stackrel{?}{=} s_i + \alpha_i a_i & \xleftarrow{(a, b)} & (a_i, b_i) = (f_{d_i}(q_i), f_{d_i}(r_i + \alpha_i q_i))
\end{array}$$
> If the check success, $\text{accept}$ and returns $a_i$, else, $\text{reject}$ and returns $\perp$.
> 
> Also, $i \in [1, \ell]$, and there is a variant with multiple provers instead.

