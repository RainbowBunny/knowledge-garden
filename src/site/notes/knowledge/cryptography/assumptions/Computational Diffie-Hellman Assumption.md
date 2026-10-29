---
{"dg-publish":true,"permalink":"/knowledge/cryptography/assumptions/computational-diffie-hellman-assumption/","dg-note-properties":{"aliases":["CDH Assumption","CDH"]}}
---

Reference:
- `[Gal12]` — S. D. Galbraith, _Mathematics of Public Key Cryptography_ (CUP 2012), Ch. 20: Definition 20.2.1, Lemma 20.2.5: https://www.math.auckland.ac.nz/~sgal018/crypto-book/ch20.pdf

## Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|Discrete-Logarithm Assumption]]: Import $(\mathbb G, q, g, \mathcal A)$.

## Distribution

> [!definition] CDH Distribution
> Sampling experiment $\mathrm{CDH}(\mathbb G, g)$:
> 1. $\alpha \xleftarrow{\$} \mathbb Z_q$.
> 2. $\beta \xleftarrow{\$} \mathbb Z_q$.
> 3. Returns the instance $(u, v) = (g^\alpha, g^\beta)$ and the solution $w = g^{\alpha\beta}$.

## Problem

### Search Variant

> [!definition] Computational Diffie-Hellman Problem
> Given $(g, g^a, g^b) \in \mathbb G^3$, compute $g^{ab}$. `[Gal12 Def 20.2.1]`

> [!definition] Search CDH
> A search game: one branch; the challenger checks the answer in the last row.
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $((u, v), w) \leftarrow \mathrm{CDH}(\mathbb G, g)$ | $\xrightarrow{\ \mathbb G,\, u,\, v\ }$ | |
> | 2 | | $\xleftarrow{\ \hat w\ }$ | outputs some $\hat w \in \mathbb G$ |
> | 3 | checks whether $\hat w = w$ | | |
>
> **Goal** — $\mathcal A$ wins iff:
> - $\hat w = w$.
>
> $$\mathsf{Adv}^{\mathsf{cdh}}_{\mathbb G}(\mathcal A) = \Pr[\mathcal A \text{ wins}].$$

> [!remark] Fixed or variable base
> `[Gal12 Def 20.2.1]` notes two versions, with $g$ fixed or part of the instance; the game above fixes $g$ in the description of $\mathbb G$.

## Claim

> [!definition] Computational Diffie-Hellman Assumption
> The **CDH assumption** holds for $\mathbb G$ if $\mathsf{Adv}^{\mathsf{cdh}}_{\mathbb G}(\mathcal A)$ is negligible for every efficient $\mathcal A$.

> [!theorem] Reductions between DDH, CDH and DL — each problem is no harder than the next
> **Scope**
> - $\mathbb G$: a cyclic group of prime order.
>
> ---
> **Property**
> $$\mathrm{DDH} \leq_R \mathrm{CDH},$$
> $$\mathrm{CDH} \leq_R \mathrm{DLP}.$$
> So the [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|DDH assumption]] implies the CDH assumption, which implies the [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|DL assumption]]. `[Gal12 Lemma 20.2.5]`

## Related

### Constructions
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]] — CDH is exactly the eavesdropper's problem: compute $g^{\alpha\beta}$ from the transcript $(g^\alpha, g^\beta)$
- [[knowledge/cryptography/primitive/public-key encryption/scheme/Massey-Omura Three-Pass Cryptosystem\|Massey-Omura Three-Pass Cryptosystem]]

### Siblings
- [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|Discrete-Logarithm Assumption]], [[knowledge/cryptography/assumptions/Decisional Diffie-Hellman Assumption\|Decisional Diffie-Hellman Assumption]]
