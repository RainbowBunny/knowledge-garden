---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/relations/r1cs/split-r1-cs/","dg-note-properties":{}}
---

Reference:
- https://eprint.iacr.org/2025/373.pdf

## Definition

> [!definition] Split-R1CS
> Given a [[knowledge/cryptography/verifiable computing/relations/r1cs/Rank-1 Constraint Satisfiability\|R1CS]] $\mathcal{CS} = (n, N_g, N_v, \{\mathbf{a}_i, \mathbf{b}_i, \mathbf{c}_i\}_{i \in [N_g]})$ over $\mathbb F$, with extended witness $\mathbf{z} = (z_0, \dots, z_{N_v}), z_0 = 1$. A **split** of $\mathcal{CS}$ is a partition of the variable indices
> $$\{0, 1, \dots, N_v\} = \mathcal{Z}_{I} \sqcup \mathcal{Z}_{II}, \quad 0 \in \mathcal{Z}_{I},$$
> writing $v_1 = |\mathcal{Z}_I| - 1, v_2 = |\mathcal{Z}_{II}|$, and $\mathbf{z} = (\mathbf{z}_{I}, \mathbf{z}_{II})$ for the corresponding subvectors.

> [!remark]
> Let $\mathbf{A}, \mathbf{B}, \mathbf{C}$ be the matrix formed by the constraints.
> For $\mathbf{M} \in \{\mathbf{A}, \mathbf{B}, \mathbf{C}\}$, let $\mathbf{M}_{I}, \mathbf{M}_{II}$ be $\mathbf{M}$ restricted to columns in $\mathcal{Z}_{I}, \mathcal{Z}_{II}$, so that
> $$\mathbf{M} \mathbf{z} = \mathbf{M}_{I} \mathbf{z}_{I} + \mathbf{M}_{II} \mathbf{z}_{II}$$

### Split Form

> [!definition] Split Form
> Expanding $\mathbf{A} \mathbf{z} \circ \mathbf{B} \mathbf{z} = \mathbf{C} \mathbf{z}$ by [[knowledge/math/properties/map/Bilinearity\|Bilinearity]], we have
> $$(\mathbf{C}_{I} \mathbf{z}_{I}) + (\mathbf{C}_{II} \mathbf{z}_{II}) = (\mathbf{A}_{I} \mathbf{z}_{I}) \circ (\mathbf{B}_{I} \mathbf{z}_{I}) + (\mathbf{A}_{I} \mathbf{z}_{I}) \circ (\mathbf{B}_{II} \mathbf{z}_{II}) + (\mathbf{A}_{II} \mathbf{z}_{II}) \circ (\mathbf{B}_{I} \mathbf{z}_{I}) +  (\mathbf{A}_{II} \mathbf{z}_{II}) \circ (\mathbf{B}_{II} \mathbf{z}_{II})$$

