---
{"dg-publish":true,"permalink":"/knowledge/cryptography/key-establishment/key-derivation-problem/","dg-note-properties":{}}
---

## Definition

> [!algorithm] Guessing Advantage
> Let $P$ be a probability distribution on a finite set $\mathcal S$ and let $I$ be a function on $\mathcal S$ (the adversary's *side information*). For an adversary $\mathcal A$:
> - The challenger samples $s$ from $P$ and sends $I(s)$ to $\mathcal A$.
> - The adversary outputs $\hat{s}$ and wins if $\hat{s} = s$.
>
> Denote the winning probability by $\text{Guessadv}[\mathcal A, P, I]$.

> [!definition] Key Derivation Problem
> The **key derivation problem** for $(P, I)$ is hard if $\text{Guessadv}[\mathcal A, P, I]$ is negligible for every efficient adversary $\mathcal A$.
