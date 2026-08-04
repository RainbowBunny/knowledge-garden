---
{"dg-publish":true,"permalink":"/knowledge/cryptography/verifiable-computing/commitment/commitment-with-linear-decommitment/","dg-note-properties":{}}
---

Reference: 
- https://web.cs.ucla.edu/~rafail/PUBLIC/79.pdf

## Syntax

> [!definition] Commitment Scheme with Linear Decommitment 
> Let $\mathbb{F}$ be a finite field and $n$ a length parameter. A **commitment scheme with linear decommitment** is a pair of interactive PPT algorithms $\mathcal{C} = (\mathcal S, \mathcal R)$, run in two phases, where $S$ and $R$ use independent random inputs in each phase.
> - **Commitment phase.** $S$ is invoked on $(\mathbb{F}, d)$, where $d \in \mathbb{F}^n$ is the data to be committed, and $R$ is invoked on $(\mathbb{F}, n)$. The parties interact, at the end of which $S$ locally keeps a decommitment information string $z_S$ and $R$ keeps $z_R$: $$(z_S, z_R) \stackrel{\$}{\leftarrow} \langle S(\mathbb{F}, d),\, R(\mathbb{F}, n) \rangle .$$ 
> - **Decommitment phase.** $R$ is invoked on $(z_R, q)$, where $q \in \mathbb{F}^n$ is a decommitment query, and $S$ is invoked on $z_S$. The parties interact, at the end of which $R$ outputs a value $a \in \mathbb{F}$ or the symbol $\bot$ ("reject"): $$a \stackrel{\$}{\leftarrow} \langle S(z_S),\, R(z_R, q) \rangle .$$

## Property

> [!property] Correctness