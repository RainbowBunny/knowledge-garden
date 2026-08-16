---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/lpcp/scheme/lpcp-for-r1-cs-construction/","dg-note-properties":{}}
---

Reference:
- https://eprint.iacr.org/2022/1690.pdf (LUNA, CCS' 24)

## Scheme

> [!scheme] LPCP for R1CS Construction
> ### Parameters
> - $S = \{\alpha_1, \dots, \alpha_{N_g}\} \subset \mathbb F$: Public interpolation point.
> - $A_i, B_i, C_i: \mathbb{F} \rightarrow \mathbb{F}$: Unique polynomials of degree $N_g - 1$ for $i \in \{0, \dots, N_w\}$ and for all $j \in [N_g]$:
> 	$$A_i(\alpha_j) = \mathbf{a}_{j, i}, B_i(\alpha_j) = \mathbf{b}_{j, i}, C_i(\alpha_j) = \mathbf{c}_{j, i}$$
> - $Z_S(z) = \prod_{j \in [N_g]}(z - \alpha_j): \mathbb{F} \rightarrow \mathbb{F}$: Vanishing polynomial.
> 
> ---
> ### Building Blocks
> - $\mathcal{CS} = (n, N_g, N_w, \{\mathbf{a}_i, \mathbf{b}_i, \mathbf{c}_i\}_{i \in [N_g]})$: [[knowledge/cryptography/verifiable computing/relations/r1cs/Rank-1 Constraint Statisfiability\|R1CS]] for finite field $\mathbb F$.
> 
> ---
> ### Algorithms
> - $(\mathrm{st}, \mathbf{Q}) \leftarrow \mathsf{Query}(\mathcal{CS}) \in \mathbb{F}^{3n+4} \times \mathbb{F}^{(4 + N_g + N_w - n) \times 4}$:
> 	1. Samples $\tau \leftarrow \mathcal U(\mathbb{F} \backslash S) \in \mathbb{F}$.
> 	2. Defines $\boldsymbol{\alpha} = (A_1(\tau), \dots, A_n(\tau)) \in \mathbb{F}^n$.
> 	3. Defines $\boldsymbol{\beta} = (B_1(\tau), \dots, B_n(\tau)) \in \mathbb{F}^n$.
> 	4. Defines $\boldsymbol{\gamma} = (C_1(\tau), \dots, C_n(\tau)) \in \mathbb{F}^n$.
> 	5. Defines $\mathrm{st} = (A_0(\tau), B_0(\tau), C_0(\tau), \boldsymbol{\alpha}, \boldsymbol{\beta}, \boldsymbol{\gamma}, Z_S(\tau)) \in \mathbb{F}^{3n + 4}$.
> 	6. Defines $\mathbf{Q} = \begin{bmatrix}Z_S(\tau) & 0 & 0 & A_{n + 1}(\tau) & \dots & A_{N_w}(\tau) & 0 & 0 & \dots & 0 \\ 0 & Z_S(\tau) & 0 & B_{n + 1}(\tau) & \dots & B_{N_w}(\tau) & 0 & 0 & \dots & 0 \\ 0 & 0 & Z_S(\tau) & C_{n + 1}(\tau) & \dots & C_{N_w}(\tau) & 0 & 0 & \dots & 0 \\ 0 & 0 & 0 & 0 & \dots & 0 & 1 & \tau & \dots & \tau^{N_g}\end{bmatrix}^T \in \mathbb F^{(4 + N_g + N_w - n) \times 4}$
> 	7. Returns $(\mathrm{st}, \mathbf{Q})$
> - $\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathcal{CS}, \mathbf{x} \in \mathbb{F}^n, \mathbf{w} \in \mathbb{F}^{N_w}) \in \mathbb{F}^{4 + N_g + N_w - n}$:
> 	1. Samples $\delta_1, \delta_2, \delta_3 \leftarrow \mathcal U(\mathbb F)$.
> 	2. Constructs $A(z) = \delta_1 Z_s(z) + A_0(z) + \sum_{i = 1}^{N_w} w_i A_i(z)$.
> 	3. Constructs $B(z) = \delta_1 Z_s(z) + B_0(z) + \sum_{i = 1}^{N_w} w_i B_i(z)$.
> 	4. Constructs $C(z) = \delta_1 Z_s(z) + C_0(z) + \sum_{i = 1}^{N_w} w_i C_i(z)$.
> 	5. Calculates $H(z) = (A(z) B(z) - C(z)) / Z_S(z)$.
> 	6. Defines $\mathbf{h} = (h_0, \dots, h_{N_g}) \in \mathbb F^{N_g + 1}$ be the coefficients of $H$.
> 	7. Parses $\mathbf{w}^T = [\mathbf{x}^T | \bar{\mathbf{w}}^T]$.
> 	8. Returns $\boldsymbol{\pi} = (\delta_1, \delta_2, \delta_3, \bar{\mathbf{w}}, \mathbf{h}) \in \mathbb{F}^{4 + N_g + N_w - n}$.
> - $\{0, 1\} \leftarrow \mathsf{Verify}(\mathrm{st} \in \mathbb{F}^{3n+4}, \mathbf{x} \in \mathbb{F}^n, \mathbf{a} = \{\mathbf{a}_i\}_{i \in [4]} \in \mathbb{F}^4)$:
> 	1. Parses $\mathrm{st} = (a_0, b_0, c_0, \boldsymbol{\alpha}, \boldsymbol{\beta}, \boldsymbol{\gamma}, z)$.
> 	2. Computes $a_1' = \mathbf{a}_1 + a_0 + \mathbf{x}^T \boldsymbol{\alpha}$.
> 	3. Computes $a_2' = \mathbf{a}_2 + b_0 + \mathbf{x}^T \boldsymbol{\beta}$.
> 	4. Computes $a_3' = \mathbf{a}_3 + c_0 + \mathbf{x}^T \boldsymbol{\gamma}$.
> 	5. Returns $a_1' a_2' - a_3' - \mathbf{a}_4 z = 0$.
