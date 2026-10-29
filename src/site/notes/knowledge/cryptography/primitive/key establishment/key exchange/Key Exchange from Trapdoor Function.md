---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/key-establishment/key-exchange/key-exchange-from-trapdoor-function/","dg-note-properties":{}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023, §10.2 (the protocol and its security argument), §10.3 (RSA). Copy of Ch. 10, §10.1–10.4: https://www.cis.upenn.edu/~sga001/classes/cis331f19/resources/bs_ch10.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]]: Import $(\lambda, k, T_P)$.
> - $\mathcal X, \mathcal Y$: the domain and range of the trapdoor function. 
> - $(\mathrm{pk}, \mathrm{sk})$: its key pair. $x \in \mathcal X$: the shared key.

> [!definition] Building Blocks
> - $\mathcal T = (\mathsf{KeyGen}, F, I)$: any [[knowledge/cryptography/special function/trapdoor function/Trapdoor Functions\|trapdoor function scheme]] over $(\mathcal X, \mathcal Y)$ (universally quantified).

> [!definition] Key Exchange from Trapdoor Function
> | | Alice | | Bob |
> | --- | --- | --- | --- |
> | 1 | $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathcal T.\mathsf{KeyGen}()$ | $\xrightarrow{\ \mathrm{pk}\ }$ | |
> | 2 | | $\xleftarrow{\ y\ }$ | $x \xleftarrow{\$} \mathcal X$<br>$y \leftarrow F(\mathrm{pk}, x)$ |
> | 3 | $x \leftarrow I(\mathrm{sk}, y)$ | | |
>
> Both hold $x$, the shared key $k = x$; the transcript is $T_P = (\mathrm{pk}, y)$. `[BS §10.2]`

> [!remark] Notation in the literature
> `[BS §10.2]` writes the trapdoor function scheme as $(G, F, I)$ and the first step as $(pk, sk) \xleftarrow{R} G()$; key generation is $\mathsf{KeyGen}$ in this vault.

## Property

### Correctness

> [!property] Correctness
> For every key pair output by $\mathcal T.\mathsf{KeyGen}$ and every $x \in \mathcal X$,
> $$I(\mathrm{sk}, F(\mathrm{pk}, x)) = x,$$
> by the correctness of [[knowledge/cryptography/special function/trapdoor function/Trapdoor Functions#Definition\|the trapdoor function scheme]], so Alice recovers Bob's $x$.

## Security

> [!security] Eavesdropper security from one-wayness `[BS §10.2]`
> If $\mathcal T$ is [[knowledge/cryptography/special function/trapdoor function/Trapdoor Functions#One-way Security\|one way]], the protocol is [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange#Against an eavesdropper\|secure against an eavesdropper]]: for every eavesdropper $\mathcal A$ there is an inverter $\mathcal B$ for $\mathcal T$ with exactly the same advantage,
> $$\mathsf{Adv}^{\mathsf{ke}}_P(\mathcal A) = \mathsf{Adv}^{\mathsf{ow}}_{\mathcal T}(\mathcal B).$$

> [!proof] Reduction $\mathcal B$
> | | one-wayness challenger | | inverter $\mathcal B$ | | eavesdropper $\mathcal A$ |
> | --- | --- | --- | --- | --- | --- |
> | 1 | $(\mathrm{pk}, \mathrm{sk}) \leftarrow \mathcal T.\mathsf{KeyGen}()$<br>$x \xleftarrow{\$} \mathcal X$<br>$y \leftarrow F(\mathrm{pk}, x)$ | $\xrightarrow{\ \mathrm{pk},\, y\ }$ | $T_P = (\mathrm{pk}, y)$ | $\xrightarrow{\ T_P\ }$ | |
> | 2 | | | | $\xleftarrow{\ \hat k\ }$ | outputs a guess $\hat k$ |
> | 3 | | $\xleftarrow{\ \hat x = \hat k\ }$ | forwards the guess | | |
>
> $(\mathrm{pk}, y)$ is distributed exactly as the transcript of an honest run, and the key of that run is the $x$ the challenger chose: $\mathcal B$ inverts exactly when $\mathcal A$ guesses the key.

## Example

> [!example] RSA `[BS §10.3]`
> With the RSA trapdoor permutation, Alice sends $(n, e)$, Bob sends $y = x^e$ for a random $x \in \mathbb Z_n$, and Alice recovers $x = y^d$; under the RSA assumption it is secure against an eavesdropper — [[knowledge/cryptography/special function/trapdoor function/Trapdoor Functions#A Trapdoor Permutation Scheme Based on RSA\|Trapdoor Functions#A Trapdoor Permutation Scheme Based on RSA]]. `[BS]` calls RSA essentially the only known reasonable candidate for a one-way trapdoor permutation.

## Related

### Instantiations
- RSA key exchange, above

### Siblings
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]] — a key exchange from a group, not from a trapdoor
- [[knowledge/cryptography/primitive/key establishment/kem/Key Encapsulation Mechanism\|Key Encapsulation Mechanism]] — the same one-shot shape, with an encapsulation algorithm instead of $F$

### Prerequisites
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]], [[knowledge/cryptography/special function/trapdoor function/Trapdoor Functions\|Trapdoor Functions]]
