---
{"dg-publish":true,"permalink":"/knowledge/cryptography/foundations/computational-indistinguishability/","dg-note-properties":{}}
---

## Definition

> [!algorithm] Distinguishing $P_0$ from $P_1$
> For probability distributions $P_0$ and $P_1$ on a finite set $\mathcal R$, and adversary $\mathcal A$, define two experiments. For $b = 0, 1$:
> **Experiment $b$:**
> - The challenger samples $x \xleftarrow{R} P_b$ and sends $x$ to the adversary.
> - The adversary outputs $\hat{b} \in \{0, 1\}$.
>
> Let $W_b$ be the event that $\mathcal A$ outputs 1 in Experiment $b$. Define $$\text{Distadv}[\mathcal A, P_0, P_1] = |P[W_0] - P[W_1]|.$$

> [!definition] Computational Indistinguishability
> $P_0$ and $P_1$ are **computationally indistinguishable** if $\text{Distadv}[\mathcal A, P_0, P_1]$ is negligible for all efficient adversaries.

> [!definition] Statistical Indistinguishability
> $P_0$ and $P_1$ are **statistically indistinguishable** if the [[knowledge/math/probability/Statistical Distance\|Statistical Distance]] $\Delta[P_0, P_1]$ is negligible.

## Property

> [!theorem]
> For every adversary $\mathcal A$ (even computationally unbounded): $\text{Distadv}[\mathcal A, P_0, P_1] \leq \Delta[P_0, P_1]$.

> [!corollary]
> Statistical indistinguishability implies computational indistinguishability. The converse fails: e.g. the output of a secure PRG is computationally, but not statistically, indistinguishable from uniform.

> [!theorem]
> If $\mathcal S$ and $\mathcal T$ are finite sets, $X$ and $Y$ are random variables taking values in $\mathcal S$, and $f: \mathcal S \rightarrow \mathcal T$ is a function, then $\Delta[f(X), f(Y)] \leq \Delta[X, Y]$

## Application

- [[knowledge/cryptography/symmetric encryption/Symmetric Key Encryption#Indistinguishability\|Symmetric Key Encryption#Indistinguishability]] and [[knowledge/cryptography/public-key encryption/Public Key Encryption#Indistinguishability\|Public Key Encryption#Indistinguishability]] — security definitions are distinguishing games between two ciphertext distributions.
- Hybrid arguments — chains of computationally indistinguishable distributions are indistinguishable (loss linear in the chain length).
