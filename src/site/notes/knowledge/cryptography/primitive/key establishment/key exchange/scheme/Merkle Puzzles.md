---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/key-establishment/key-exchange/scheme/merkle-puzzles/","dg-note-properties":{"aliases":["Merkle's Puzzles"]}}
---

Reference:
- `[Mer78]` — R. C. Merkle, _Secure Communications Over Insecure Channels_, Communications of the ACM 21(4), April 1978, pp. 294–299 ("The New Approach", "The Method", "Some Implications"): https://ralphmerkle.com/1974/PuzzlesAsPublished.pdf
- `[DH76]` — W. Diffie, M. E. Hellman, _New Directions in Cryptography_, IEEE Transactions on Information Theory IT-22(6), 1976, §III (on Merkle's system): http://www-ee.stanford.edu/%7Ehellman/publications/24.pdf

## Scheme

Reference Name: Merkle's puzzles
Instantiates:: [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]]

### Parties

> [!definition] Parties
> - $X$: builds and sends the puzzles. $Y$: solves one and answers.
> - A key channel between them that anyone may read; that it delivers messages unmodified is an assumption of the scheme — see [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Merkle Puzzles#Security\|#Security]] ("The New Approach").

### Parameters

> [!definition] Parameters
> - $N$: the number of puzzles, agreed by $X$ and $Y$. $C$: a constant.
> - $\mathcal K_r$: a **restricted key space** of $C \cdot N$ keys of $F$, so that a puzzle encrypted under a key from it is broken by exhaustive search in about $C \cdot N$ trials.
> - $K_1, K_2$: auxiliary keys of $X$. $\mathrm{CONSTANT}$: a random value that marks a correct decryption.
> - $\mathrm{ID}_i$, $\mathrm{key}_i$: the identifier and key hidden in puzzle $i$.

### Building Blocks

> [!definition] Building Blocks
> - $F$: a strong encryption function — "any function the reader considers powerful" — such as a [[knowledge/cryptography/primitive/symmetric encryption/Block Ciphers\|block cipher]]; `[Mer78]` suggests Lucifer. $F_K(m)$ encrypts $m$ under the key $K$.

### Algorithms

> [!scheme] Protocol `[Mer78, "The Method"]`
> | | $X$ | | $Y$ |
> | --- | --- | --- | --- |
> | 1 | picks $K_1, K_2, \mathrm{CONSTANT}$<br>for $i = 1, \dots, N$:<br>$\mathrm{ID}_i = F_{K_1}(i)$<br>$\mathrm{key}_i = F_{K_2}(\mathrm{ID}_i)$<br>$r_i \xleftarrow{\$} \mathcal K_r$<br>$\mathrm{puzzle}_i = F_{r_i}(\mathrm{key}_i, \mathrm{ID}_i, \mathrm{CONSTANT})$ | $\xrightarrow{\ \mathrm{CONSTANT},\, \mathrm{puzzle}_1, \dots, \mathrm{puzzle}_N\ }$ | |
> | 2 | | $\xleftarrow{\ \mathrm{ID}_j\ }$ | picks $j$ at random<br>tries every key of $\mathcal K_r$ on $\mathrm{puzzle}_j$ until the output contains $\mathrm{CONSTANT}$<br>reads $(\mathrm{key}_j, \mathrm{ID}_j)$ |
> | 3 | $\mathrm{key}_j = F_{K_2}(\mathrm{ID}_j)$ | | |
>
> Both use $\mathrm{key}_j$ as the session key.

## Property

### Correctness

> [!property] Merkle's Puzzles Correctness
> $X$ recomputes $\mathrm{key}_j = F_{K_2}(\mathrm{ID}_j)$ from the identifier $Y$ returned — the value $Y$ read from $\mathrm{puzzle}_j$ — so both hold the same key.

### Cost

> [!proposition] Work of the parties — linear for both
> $X$ spends $O(N)$ to build the puzzles; $Y$ spends $O(N)$ to solve one. `[Mer78]`

## Security

> [!security] A quadratic gap against an eavesdropper `[Mer78]`
> The eavesdropper sees every puzzle and $\mathrm{ID}_j$, but not which puzzle carries it; it must solve puzzles until it meets $\mathrm{ID}_j$, about $N/2$ of them on average, at $O(N)$ each:
> $$\text{eavesdropper's work} = O(N^2).$$
> The gap is a fixed polynomial, not the negligible advantage of the games in [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]].

> [!remark] Practicality `[DH76 §III]`
> The cost is "as much in transmission time as in computation": $N$ puzzles cross the channel before one key is agreed. With a one-megabit limit on that overhead the ratio is about $10{,}000$ to $1$, which Diffie and Hellman judged too small for most uses.

> [!remark] No active adversary
> The scheme assumes the key channel delivers messages unmodified, and leaves identities to a correct, non-secret codebook ("Some Implications"); `[DH76 §III]` notes that it requires $X$ and $Y$ to verify each other's identities by other means. Against a [[knowledge/cryptography/cryptanalysis/Man-in-the-Middle Attack\|man in the middle]] it offers nothing on its own.

## Related

### Siblings
- [[knowledge/cryptography/primitive/key establishment/key exchange/scheme/Diffie-Hellman Key Exchange\|Diffie-Hellman Key Exchange]] — the same goal with an exponential gap, under a number-theoretic assumption

### Prerequisites
- [[knowledge/cryptography/primitive/key establishment/key exchange/Key Exchange\|Key Exchange]], [[knowledge/cryptography/primitive/symmetric encryption/Block Ciphers\|Block Ciphers]]
