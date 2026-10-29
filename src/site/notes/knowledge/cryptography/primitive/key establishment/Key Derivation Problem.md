---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/key-establishment/key-derivation-problem/","dg-note-properties":{}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (Ch. 8, key derivation). `⚠️ CLAUDE – verify:` WebFetch returns only the first ~17 pages of the book, so this game could not be read in the source; the table redraws the wording this note already had. Check it, and its attack-game number, against Ch. 8.
- `⚠️ CLAUDE – verify:` — a point I could not check against the source.

## Definition

> [!definition] Guessing Advantage
> Let $P$ be a probability distribution on a finite set $\mathcal S$ and let $I$ be a function on $\mathcal S$ (the adversary's *side information*).
>
> A search game: one branch. `[BS Ch. 8]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | $s \leftarrow P$ | $\xrightarrow{\ I(s)\ }$ | |
> | 2 | | $\xleftarrow{\ \hat s\ }$ | outputs a guess $\hat s \in \mathcal S$ |
>
> **Goal** — $\mathcal A$ wins iff:
> - $\hat s = s$.
>
> Denote the winning probability by $\text{Guessadv}[\mathcal A, P, I]$.

> [!definition] Key Derivation Problem
> The **key derivation problem** for $(P, I)$ is hard if $\text{Guessadv}[\mathcal A, P, I]$ is negligible for every efficient adversary $\mathcal A$.
