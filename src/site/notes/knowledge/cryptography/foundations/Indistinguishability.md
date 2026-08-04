---
{"dg-publish":true,"permalink":"/knowledge/cryptography/foundations/indistinguishability/","dg-note-properties":{}}
---

## Basic Definition

> [!algorithm] $q$-Sample Distinguishing Advantage
> For probability distributions $P_0$ and $P_1$ on a finite set $\mathcal R$, and adversary $\mathcal A = (\mathcal A_\text{guess})$, we define the $q$-sample distinguishing advantage:
> $$\text{Adv}^{q\text{-Dist}}_{P_0, P_1}(\mathcal A) = 
> \left|\; \Pr\!\left[
> \begin{array}{l}
> b = 1
> \end{array}
> \;\middle |\; 
> \begin{array}{l}
> x_1, x_2, \dots, x_q \xleftarrow{\$} P_0 \\
> b \leftarrow \mathcal A_\text{guess}(x_1, x_2, \dots, x_q)
> \end{array} \right] 
> \;- 
> \Pr\!\left[
> \begin{array}{l}
> b = 1
> \end{array}
> \;\middle |\; 
> \begin{array}{l}
> x_1, x_2, \dots, x_q \xleftarrow{\$} P_1 \\
> b \leftarrow \mathcal A_\text{guess}(x_1, x_2, \dots, x_q)
> \end{array} \right] 
> \right|.
> $$

### Perfect

> [!definition] Perfect Indistinguishability
> $P_0$ and $P_1$ are perfect indistinguishability if their distribution is the same.

### Computational

> [!definition] Computational Indistinguishability
> $P_0$ and $P_1$ are **computationally indistinguishable** if $\text{Adv}_{P_0, P_1}^{q\text{-Dist}}(\mathcal A)$ is negligible for all efficient adversaries.

### Statistical

> [!definition] Statistical Indistinguishability
> $P_0$ and $P_1$ are **statistically indistinguishable** if the [[knowledge/math/probability/Statistical Distance\|Statistical Distance]] $\Delta[P_0, P_1]$ is negligible.

## Property

> [!theorem]
> For every adversary $\mathcal A$ (even computationally unbounded): $\text{Adv}^{q\text{-Dist}}_{P_0, P_1}[\mathcal A] \leq q \cdot \Delta[P_0, P_1]$.

> [!corollary]
> Statistical indistinguishability implies computational indistinguishability. The converse fails: e.g. the output of a secure PRG is computationally, but not statistically, indistinguishable from uniform.

> [!theorem]
> If $\mathcal S$ and $\mathcal T$ are finite sets, $X$ and $Y$ are random variables taking values in $\mathcal S$, and $f: \mathcal S \rightarrow \mathcal T$ is a function, then $\Delta[f(X), f(Y)] \leq \Delta[X, Y]$

## Application

- [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Indistinguishability\|Symmetric Key Encryption#Indistinguishability]] and [[knowledge/cryptography/primitive/public-key encryption/Public Key Encryption#Indistinguishability\|Public Key Encryption#Indistinguishability]] — security definitions are distinguishing games between two ciphertext distributions.
- Hybrid arguments — chains of computationally indistinguishable distributions are indistinguishable (loss linear in the chain length).
