---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/relations/arithmetization/quadratic-arithmetic-program/","dg-note-properties":{}}
---

Reference: https://www.di.ens.fr/~nitulesc/files/Survey-SNARKs.pdf

## Definition

> [!definition] Quadratic Arithmetic Program
> A Quadratic Arithmetic Program $\mathbf{Q} = (\mathbf{A}, \mathbf{B}, \mathbf{C}, t)$ over the field $\mathbb F$ for an arithmetic function $f$ takes as input $n$ elements of $\mathbb{F}$ and outputs $n'$ elements, for a total of $N = n + n'$ I/O elements includes:
> - Three sets of $m + 1$ polynomials $\mathbf{A} = \{A_i(x)\}, \mathbf{B} = \{B_i(x)\}, \mathbf{C} = \{C_i(x)\}, i \in \{0, 1, \dots, m\}$
> - A target polynomial $t(x)$. 
> 
> Such that a tuple $(x_1, \dots, x_n) \in \mathbb F^N$ is a valid assignment of $f$'s inputs and outputs, if and only if there exist coefficients $(w_{n + 1}, \dots, w_N)$ (we write $\mathbf{z} = (1, x_1, \dots, x_n, w_{n + 1}, \dots, w_N)$) such that $t(x)$ divides $p(x)$, where:
> $$p(x) = \langle \mathbf{A}, \mathbf{z} \rangle \cdot \langle \mathbf{B}, \mathbf{z} \rangle - \langle \mathbf{C}, \mathbf{z} \rangle$$



