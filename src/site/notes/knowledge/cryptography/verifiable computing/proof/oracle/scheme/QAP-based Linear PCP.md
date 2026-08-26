---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/oracle/scheme/qap-based-linear-pcp/","dg-note-properties":{"type":"LPCP"}}
---

Reference:
- https://eprint.iacr.org/2022/1690.pdf (LUNA, CCS' 24)

## Scheme

> [!scheme] QAP-based Linear PCP
> ### Parameters
> - $\mathbb F$: Finite field.
> 
> ---
> ### Building Blocks
> - $\mathcal{CS} = (n, N_g, N_w, \{\mathbf{a}_i, \mathbf{b}_i, \mathbf{c}_i\}_{i \in [N_g]})$: [[knowledge/cryptography/verifiable computing/relations/r1cs/Rank-1 Constraint Satisfiability\|R1CS]] over $\mathbb F$.
> - $\mathbf{Q} = (\{A_i(x)\}_{i \in [N_g]}, \{B_i(x)\}_{i \in [N_g]}, \{C_i(x)\}_{i \in [N_g]}, Z_S(x))$: [[knowledge/cryptography/verifiable computing/relations/arithmetization/R1CS to QAP Reduction\|R1CS to QAP Reduction]] of $\mathcal{CS}$
> 	- $S = \{\alpha_1, \dots, \alpha_{N_g}\} \subset \mathbb F$: Public interpolation point.
> 
> ---
> ### Algorithms
> - $(\mathrm{st}, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS}) \in \mathbb{F}^{3n+4} \times \mathbb{F}^{(4 + N_g + |\mathbf{w}|) \times 4}$:
> 	1. Samples $\tau \leftarrow \mathcal U(\mathbb{F} \backslash S) \in \mathbb{F}$.
> 	2. Defines $\mathbf{A} = (A_1(\tau), \dots, A_n(\tau)) \in \mathbb{F}^n$.
> 	3. Defines $\mathbf{B} = (B_1(\tau), \dots, B_n(\tau)) \in \mathbb{F}^n$.
> 	4. Defines $\mathbf{C} = (C_1(\tau), \dots, C_n(\tau)) \in \mathbb{F}^n$.
> 	5. Defines $\mathrm{st} = (A_0(\tau), B_0(\tau), C_0(\tau), \mathbf{A}, \mathbf{B}, \mathbf{C}, Z_S(\tau)) \in \mathbb{F}^{3n + 4}$.
> 	6. Defines $\mathbf{Q} = \begin{bmatrix}Z_S(\tau) & 0 & 0 & A_{n + 1}(\tau) & \dots & A_{N_w}(\tau) & 0 & 0 & \dots & 0 \\ 0 & Z_S(\tau) & 0 & B_{n + 1}(\tau) & \dots & B_{N_w}(\tau) & 0 & 0 & \dots & 0 \\ 0 & 0 & Z_S(\tau) & C_{n + 1}(\tau) & \dots & C_{N_w}(\tau) & 0 & 0 & \dots & 0 \\ 0 & 0 & 0 & 0 & \dots & 0 & 1 & \tau & \dots & \tau^{N_g}\end{bmatrix}^T \in \mathbb F^{(4 + N_g + |\mathbf{w}|) \times 4}$
> 	7. Returns $(\mathrm{st}, \mathbf{Q})$
> - $\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathcal{CS}, \mathbf{x} \in \mathbb{F}^n, \mathbf{w} \in \mathbb{F}^{N_v - n}) \in \mathbb{F}^{4 + N_g + N_w - n}$:
> 	1. Samples $\delta_1, \delta_2, \delta_3 \leftarrow \mathcal U(\mathbb F)$.
> 	2. Calculates $\mathbf{z} = (1 || \mathbf{x} || \mathbf{w})$ be the extended witness.
> 	3. Constructs $A(z) = \delta_1 Z_s(z) + \sum_{i = 0}^{N_v} \mathbf{z}^{(i)} A_i(z)$.
> 	4. Constructs $B(z) = \delta_2 Z_s(z) + \sum_{i = 0}^{N_v} \mathbf{z}^{(i)} B_i(z)$.
> 	5. Constructs $C(z) = \delta_3 Z_s(z) + \sum_{i = 0}^{N_v} \mathbf{z}^{(i)} C_i(z)$.
> 	6. Calculates $H(z) = (A(z) B(z) - C(z)) / Z_S(z)$.
> 	7. Defines $\mathbf{h} = (h_0, \dots, h_{N_g}) \in \mathbb F^{N_g + 1}$ be the coefficients of $H$.
> 	8. Returns $\boldsymbol{\pi} = (\delta_1, \delta_2, \delta_3, \mathbf{w}, \mathbf{h}) \in \mathbb{F}^{4 + N_g + |\mathbf{w}|}$.
> - $\{0, 1\} \leftarrow \mathsf{Verify}(\mathrm{st} \in \mathbb{F}^{3n+4}, \mathbf{x} \in \mathbb{F}^n, \mathbf{a} \in \mathbb{F}^4)$:
> 	1. Parses $\mathrm{st} = (a_0, b_0, c_0, \mathbf{A}, \mathbf{B}, \mathbf{C}, z)$.
> 	2. Computes $a_1' = \mathbf{a}^{(1)} + a_0 + \mathbf{x}^T \mathbf{A}$.
> 	3. Computes $a_2' = \mathbf{a}^{(2)} + b_0 + \mathbf{x}^T \mathbf{B}$.
> 	4. Computes $a_3' = \mathbf{a}^{(3)} + c_0 + \mathbf{x}^T \mathbf{C}$.
> 	5. Returns $a_1' a_2' - a_3' - \mathbf{a}_4 z = 0$.

> [!remark]
> Also known as:
> - 4-query LPCP for R1CS.
> - GGPR linear PCP.

## Property

### Correctness

> [!property] Correctness of QAP-based LPCP
> **Step 1**: Divisibility
> - With $\mathbf{z} = (1, \mathbf{w}_1, \dots, \mathbf{w}_{N_w})$ and $\mathbf{A}(z) = A_0(z) + \sum_{i = 1}^{N_w} w_i A_i(z)$ (similarly $\mathbf{B}, \mathbf{C}$), we have:
> 	$$\begin{align}
> 	\mathbf{A}(\alpha_i) \mathbf{B}(\alpha_i) - \mathbf{C}(\alpha_i) &= \mathbf{z}^T \mathbf{a_i} \cdot \mathbf{z}^T \mathbf{b_i} - \mathbf{z}^T \mathbf{c_i} \\ 
> 	&= 0.
> 	\end{align}$$
> 	As this is the $i$-th constraints of $\mathcal{CS}$.
> - Thus, we have $Z_S \; | \; \mathbf{A} \mathbf{B} - \mathbf{C}$.
> 
> **Step 2**: Blinding
> - As $A = \delta_1 Z_S + \mathbf{A}$ (similar to $B, C$), and let $\mathbf{A} \mathbf{B} - \mathbf{C} = H_0 Z_S$, we have:
> 	$$H = (AB - C) / Z_S = H_0 + \delta_2 A + \delta_1 B + \delta_1 \delta_2 Z_S - \delta_3$$
> 	Has degree $N_g$ (because only $Z_S$ has degree $N_g$) and returns as $\mathbf{h}$.
> 
> **Step 3**: Reconstruction
> - Based on the query, we calculated the secret half: 
> 	$$\begin{align}
> 	\mathbf{a}^{(1)} &= \langle \mathbf{q}_1, \boldsymbol{\pi} \rangle \\
> 	&= \delta_1 Z_S(\tau) + \sum_{i = n + 1}^{N_w} \mathbf{z}^{(i)} A_i(\tau)
> 	\end{align}$$
> - Recovered the blinded polynomials at point $\tau$:
> 	$$\begin{align}
> 	a_1' &= \mathbf{a}^{(1)} + a_0 + \mathbf{x}^T \alpha \\
> 	     &= \mathbf{A}(\tau)
> 	\end{align}$$
> 	Similarly, we have $a_2' = \mathbf{B}(\tau)$ and $a_3' = \mathbf{C}(\tau)$.
> - Also the last query give the evaluation of $H$:
> 	$$\begin{align}
> 	\mathbf{a}_4 &= \langle \mathbf{q}_4, \boldsymbol{\pi} \rangle \\
> 		&= \langle (1, \tau, \dots, \tau^{N_g}), \mathbf{h}\rangle \\ 
> 	    &= H(\tau)
> 	\end{align}$$
> 
> **Step 4**: Checking
> - We now check that
> 	$$a_1' a_2' - a_3' - \mathbf{a}_4 z = 0 \Longleftrightarrow A(\tau) B(\tau) - C(\tau) - H(\tau) Z_S(\tau) = 0$$
> 	Which is true as $H = (AB - C) / Z_S$

