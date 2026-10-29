---
{"dg-publish":true,"permalink":"/knowledge/cryptography/assumptions/decisional-diffie-hellman-assumption/","dg-note-properties":{"aliases":["DDH Assumption","DDH"]}}
---

Reference:
- `[Gal12]` — S. D. Galbraith, _Mathematics of Public Key Cryptography_ (CUP 2012): Ch. 20, Definitions 20.2.3 and 20.2.4, Lemma 20.2.5: https://www.math.auckland.ac.nz/~sgal018/crypto-book/ch20.pdf · Ch. 26, §26.5.2: https://www.math.auckland.ac.nz/~sgal018/crypto-book/ch26.pdf
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, §10.5 (DH-triples). `⚠️ CLAUDE – verify:` §10.5 lies past every copy of the book I could read; the remark on DH-triples is kept as it was transcribed.

## Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|Discrete-Logarithm Assumption]]: Import $(\mathbb G, q, g, \mathcal A)$.
> - [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|Computational Diffie-Hellman Assumption]]: Import the sampling experiment $\mathrm{CDH}(\mathbb G, g)$.

## Distribution

> [!definition] DDH Distribution
> Sampling experiment $\mathrm{DDH}_b(\mathbb G, g)$, for $b \in \{0, 1\}$:
> 1. $\alpha \xleftarrow{\$} \mathbb Z_q$.
> 2. $\beta \xleftarrow{\$} \mathbb Z_q$.
> 3. $\gamma \xleftarrow{\$} \mathbb Z_q$.
> 4. Returns $(g^\alpha, g^\beta, g^{\alpha\beta})$ if $b = 0$, and $(g^\alpha, g^\beta, g^\gamma)$ if $b = 1$.
>
> `[Gal12 Def 20.2.4]`

> [!remark] DH-triples
> $(g^\alpha, g^\beta, g^\gamma)$ is a **DH-triple** if $\gamma = \alpha\beta$, and a **non-DH-triple** otherwise. DDH says that random DH-triples cannot be told apart from random triples. `[BS §10.5]`

## Problem

### Decision Variant

> [!definition] Decisional Diffie-Hellman Problem
> Given $(g, g^a, g^b, g^c) \in \langle g \rangle^4$, decide whether $g^c = g^{ab}$. `[Gal12 Def 20.2.3]`

> [!definition] Decision DDH
> A distinguishing game: the branches differ in the third group element.
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | **Game 0**: $(u, v, w) \leftarrow \mathrm{DDH}_0(\mathbb G, g)$<br>**Game 1**: $(u, v, w) \leftarrow \mathrm{DDH}_1(\mathbb G, g)$ | $\xrightarrow{\ \mathbb G,\, u,\, v,\, w\ }$ | |
> | 2 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> $$\mathsf{Adv}^{\mathsf{ddh}}_{\mathbb G}(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$$

> [!remark] The source's form
> `[Gal12 Def 20.2.4]` defines the advantage of a DDH algorithm on a family of groups $G_n$ of order $r_n$ as the same difference of probabilities, with $g$ also sampled from $G_n$ and the algorithm answering "yes" or "no".

## Claim

> [!definition] Decisional Diffie-Hellman Assumption
> The **DDH assumption** holds for $\mathbb G$ if $\mathsf{Adv}^{\mathsf{ddh}}_{\mathbb G}(\mathcal A)$ is negligible for every efficient $\mathcal A$ `[Gal12 §20.2]`. It is the strongest of the three: $\mathrm{DDH} \leq_R \mathrm{CDH} \leq_R \mathrm{DLP}$ `[Gal12 Lemma 20.2.5]`.

> [!remark] Where it fails
> On supersingular elliptic curves a distortion map turns a pairing into a DDH test, so DDH can be easy there while CDH is believed hard `[Gal12 §26.5.2]` ([[knowledge/math/algebra/structures/elliptic curve/Bilinear Pairings\|Bilinear Pairings]]).

## Related

### Constructions
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]] — its key is indistinguishable from random to an eavesdropper under DDH
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Sign-and-MAC Key Exchange\|SIGMA]] — SK-secure under DDH

### Siblings
- [[knowledge/cryptography/assumptions/Discrete-Logarithm Assumption\|Discrete-Logarithm Assumption]], [[knowledge/cryptography/assumptions/Computational Diffie-Hellman Assumption\|Computational Diffie-Hellman Assumption]]

### Prerequisites
- [[knowledge/complexity/problem/group/Discrete Logarithm Problem#Diffie-Hellman Decision Problem\|Discrete Logarithm Problem#Diffie-Hellman Decision Problem]] — the problem form
