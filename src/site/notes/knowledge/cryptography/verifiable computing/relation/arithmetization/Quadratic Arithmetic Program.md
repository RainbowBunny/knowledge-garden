---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/relation/arithmetization/quadratic-arithmetic-program/","dg-note-properties":{}}
---

Reference:
- https://www.di.ens.fr/~nitulesc/files/Survey-SNARKs.pdf

## Definition

> [!definition] Parameters
> - $\mathbb{F}$: Finite field.
> - $n$: The number of public variables.
> - $n'$: The number of private variables.
> - $N_v = n + n'$: The number of variables.
> - $N_g$: The number of constraints (degree of the divider).

> [!definition] Quadratic Arithmetic Program
> A **Quadratic Arithmetic Program** $\mathbf{Q}$ includes:
> - $\mathbf{A}(x) = \{A_i(x)\}, \mathbf{B}(x) = \{B_i(x)\}, \mathbf{C}(x) = \{C_i(x)\}$ for $i \in \{0, 1, \dots, N_v\}$: Three sets of $N_v + 1$ polynomials degree $\leq N_g - 1$.
> - $t(x)$: Target polynomial degree $N_g$.
> 
> $\mathbf{Q}$ accepts input $\mathbf{x} \in \mathbb{F}^n$ if $\exists \mathbf{w} \in \mathbb{F}^{N_v - n}$:
> - Write $\mathbf{z} = (1 || \mathbf{x} || \mathbf{w})$ then:
> $$t(x) \mid p(x) = \langle \mathbf{A}(x), \mathbf{z} \rangle \cdot \langle \mathbf{B}(x), \mathbf{z} \rangle - \langle \mathbf{C}(x), \mathbf{z} \rangle.$$

