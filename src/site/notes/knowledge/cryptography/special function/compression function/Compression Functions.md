---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/compression-function/compression-functions/","dg-note-properties":{"aliases":["Compression Function"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§8.4: the compression function of Merkle–Damgård; §8.5: building compression functions).

## Definition

> [!definition] Parameters
> - [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]: Import $(\mathcal M, \mathcal T)$.
> - $\mathcal X$: the chaining space. $\mathcal Y$: the block space.

> [!definition] Compression Function
> Extends:: [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]
>
> A **compression function** is a hash function on a fixed-length message space larger than its digest space. In the form [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle–Damgård]] iterates, $h$ is defined over $(\mathcal X \times \mathcal Y, \mathcal X)$: it takes a chaining value $x \in \mathcal X$ and a message block $y \in \mathcal Y$, and returns a new chaining value. `[BS §8.4]`

Security is [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|collision resistance]], unchanged.

## Related

### Instantiations
- [[knowledge/cryptography/special function/compression function/scheme/Two-Input Lattice Hash\|Two-Input Lattice Hash]] — two blocks of short ring vectors to one, collision resistant under Module-SIS
- [[knowledge/cryptography/special function/compression function/scheme/Syndrome Based Compression Function\|Syndrome Based Compression Function]] — $\mathbf H \mathbf x^\top$ on a low-weight $\mathbf x$, from syndrome decoding
- [[knowledge/cryptography/special function/compression function/scheme/Fast Syndrome Based Compression Function\|Fast Syndrome Based Compression Function]] — the same with a regular $\mathbf x$, one nonzero coordinate per section
- [[knowledge/cryptography/special function/compression function/scheme/Inefficient Compression Function\|Inefficient Compression Function]] — $x^a y^b \bmod p$, folded into $[1, q]$

### Constructions
- [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function\|Davies-Meyer Compression Function]] — block cipher → compression function, in the ideal cipher model
- [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle-Damgard Transform]] — compression function → hash function on long messages
