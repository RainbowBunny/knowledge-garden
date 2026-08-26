---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/proof/non-interactive/scheme/luna/","dg-note-properties":{"type":"zk-SNARG"}}
---

Reference:
- https://eprint.iacr.org/2022/1690.pdf (LUNA, CCS' 24)

### Scheme

> [!scheme] Lattice-based sUccinct Non-interactive Argument
> Reference Name: $\mathsf{LUNA}$
> 
> ---
> ### Parameters
> - $\mathbb{F} = \mathbb{F}(p^f)$: Finite field.
> - $f = \mathsf{ord}_{2d}(p)$: So that
> 	$$R_p = \mathbb Z[x] / (x^d + 1, p) \cong \mathbb{F}_{p^f}^{d / f}$$
> 	because we needs a field instead of just polynomial ring.
> 
> ---
> ### Building Blocks
> - $\mathcal{CS} = (n, N_g, N_v, \{\mathbf{a}_i, \mathbf{b}_i, \mathbf{c}_i\}_{i \in [N_g]})$: [[knowledge/cryptography/verifiable computing/relations/r1cs/Rank-1 Constraint Satisfiability\|R1CS]] over $\mathbb F$.
> - $\Pi_\mathsf{LPCP} = (\mathsf{Query}, \mathsf{Prove}, \mathsf{Verify})$: A [[knowledge/cryptography/verifiable computing/proof/oracle/Linear Probabilistically Checkable Proofs\|LPCP]] for $\mathcal{CS}$ over $\mathbb F$.
> 	- $k$: Number of query.
> 	- $m$: Query length.
> - $\mathsf{HGSW} = (\mathsf{Setup}, \mathsf{Enc}, \mathsf{Add}, \mathsf{Dec})$: [[knowledge/cryptography/primitive/linear-only vector encryption/scheme/Module HGSW\|Module HGSW]] over $\mathbb F^k$.
> 	- $p$: LPCP field characteristic.
> 	- $\ell'$: Extended plaintext length.
> 
> ---
> ### Algorithms
> - $(\mathrm{crs}, \mathrm{st}) \leftarrow \mathsf{Setup}(1^\lambda, \mathcal{CS})$:
> 	1. Runs $(\mathrm{st}_\mathsf{LPCP}, \mathbf{Q}) \leftarrow \Pi_\mathsf{LPCP}.\mathsf{Setup}(\mathcal{CS})$.
> 	2. Runs $\mathrm{sk} \leftarrow \mathsf{HGSW}.\mathsf{Setup}(1^\lambda)$.
> 	3. Computes $\mathbf{C}_i \leftarrow \mathsf{HGSW}.\mathsf{Enc}(i, \mathrm{sk}, \mathbf{q_i})$ for $i \in [m]$.
> 	4. Returns $(\mathrm{crs} = (\mathcal{CS}, \{\mathbf{C}_i\}_{i \in [m]}), \mathrm{st} = (\mathrm{st}_\mathsf{LPCP}, \mathrm{sk}.\mathbf{S}))$
> - $\boldsymbol{\pi} \leftarrow \mathsf{Prove}(\mathrm{crs}, \mathbf{x} \in \mathbb{F}^n, \mathbf{w} \in \mathbb{F}^{N_v - n})$: Returns a $\mathsf{HGSW}$ ciphertext.
> 	1. Runs $\boldsymbol{\pi}_\mathsf{LPCP} \leftarrow \Pi_\mathsf{LPCP}.\mathsf{Prove}(\mathcal{CS}, \mathbf{x}, \mathbf{w})$.
> 	2. Computes $\mathbf{c}^* \leftarrow \mathsf{HGSW}.\mathsf{Add}(\{\mathbf{C}_i\}_{i \in [m]}, \{\boldsymbol{\pi}_\mathsf{LPCP}^{(i)}\}_{i \in [m]})$.
> 	3. Returns $\boldsymbol{\pi} = \mathbf{c}^*$.
> - $b \leftarrow \mathsf{Verify}(\mathrm{st}, \boldsymbol{\pi}^*, \mathbf{x} \in \mathbb{F}^n) \in \{0, 1\}$:
> 	1. Runs $\mathbf{a} = \sum_{i = 1}^m \boldsymbol{\pi}^{(i)} \mathbf{q}_i^T \leftarrow \mathsf{HGSW}.\mathsf{Decrypt}(S, \mathbf{c}^*)$.
> 	2. If $\mathbf{a} = \perp$ 
> 		1. Returns $0$.
> 	3. Else
> 		1. Returns $\Pi_\mathsf{LPCP}.\mathsf{Verify}(\mathrm{st}_\mathsf{LPCP})$.

