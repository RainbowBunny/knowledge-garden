---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/relations/r1cs/rank-1-constraint-satisfiability/","dg-note-properties":{}}
---

Reference: 
- https://eprint.iacr.org/2021/977.pdf

## Definition

> [!definition] Rank-1 Constraint Satisfiability
> A rank-1 constraint satisfiability (R1CS) system over a finite field $\mathbb F$ is specified by a tuple $\mathcal{CS} = (n, N_g, N_v, \{\mathbf{a}_i, \mathbf{b}_i, \mathbf{c}_i\}_{i \in [N_g]})$ where $n, N_g, N_v \in \mathbb N, n \leq N_v$, and $\mathbf{a}_i, \mathbf{b}_i, \mathbf{c}_i \in \mathbb F^{N_v + 1}$. The system $\mathcal{CS}$ is **satisfiable** for a statement $\mathbf{x} \in \mathbb F^n$ if there exists a witness $\mathbf{w} \in \mathbb F^{N_v - n}$ and given the extended witness $\mathbf{z} = (1 || \mathbf{x} || \mathbf{w})$ we have that
> - $\langle \mathbf{a}_i, \mathbf{z} \rangle \cdot \langle \mathbf{b}_i, \mathbf{z} \rangle = \langle \mathbf{c}_i, \mathbf{z} \rangle$ for all $i \in [N_g]$.
> 
> We denote this by writing $\mathcal{CS}(\mathbf{x}, \mathbf{w}) = 1$, and refer to $n$ as the statement size, $N_v$ as the number of variables, and $N_g$ as the number of constraints. Given an R1CS system $\mathcal{CS}$, we define the corresponding relation 
> $$\mathcal R_{\mathcal{CS}} = \{(x, w) \in \mathbb F^n \times \mathbb F^{N_v - n}: \mathcal{CS}(x, w) = 1\}.$$

> [!remark] Boolean and Arithmetic Circuit Satisfiability
> The language of R1CS capture [[knowledge/complexity/circuit/Boolean Circuit#Definition\|Boolean]] and [[knowledge/complexity/circuit/Arithmetic Circuit#Definition\|Arithmetic Circuit]] circuit satisfiability as special cases.
> - Boolean circuit satisfiability instance for a Boolean circuit $C: \{0, 1\}^n \times \{0, 1\}^h \rightarrow \{0, 1\}$ with $\alpha$ wires and $\beta$ bilinear gates yields an R1CS instance with $N_w = \alpha$ variables and $N_g = \beta + h + 1$ constraints.
> - An arithmetic circuit $C: \mathbb F^n \times \mathbb F^h \rightarrow \mathbb F^\ell$ with $\alpha$ wires and $\beta$ bilinear gates corresponds to a R1CS instance with $N_w = \alpha$ variables and $N_g = \beta + \ell$ constraints.

> [!remark] NP-completeness 
> R1CS is $\mathsf{NP}$-complete: For every [[knowledge/cryptography/verifiable computing/relations/Effective Relation\|Effective Relation]] $R \in \mathsf{NP}$ there are efficiently computable $\mathcal{CS}_R, \phi, \psi$ with $(\mathbf{x}, \mathbf{w}) \in R \Longleftrightarrow (\phi(\mathbf{x}), \psi(\mathbf{x}, \mathbf{w})) \in \mathcal{R}_{\mathcal{CS}_\mathcal{R}}$. A proof system for $\mathsf{R1CS}$ therefore yields one for any $R \in \mathsf{NP}$ - provided $\psi$ is efficiently invertible (for knowledge soundness) and $\phi$ leak nothing beyond $\mathbf{x}$ (for zero knowledge). This is arithmetization, and it is a compilation test with real cost, not an identification: R1CS is the target language rather than a normal form.
