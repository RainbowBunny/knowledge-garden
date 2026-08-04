---
{"dg-publish":true,"permalink":"/knowledge/math/probability/statistical-distance/","dg-note-properties":{}}
---

## Definition

> [!definition] Statistical Distance (Total Variation Distance)
> Let $P_0$ and $P_1$ be probability distributions on a finite set $\mathcal R$. The **statistical distance** between $P_0$ and $P_1$ is
> $$\Delta[P_0, P_1] = \frac{1}{2} \sum_{r \in \mathcal R} |P_0(r) - P_1(r)|.$$

## Property

> [!theorem] Event Characterization
> $$\max_{\mathcal R' \subseteq \mathcal R} |P_0[\mathcal R'] - P_1[\mathcal R']| = \Delta[P_0, P_1].$$
> That is, the statistical distance is exactly the largest advantage any (even unbounded) test can achieve in telling $P_0$ from $P_1$.

> [!theorem] Data-Processing Inequality
> If $f: \mathcal S \rightarrow \mathcal T$ is a function and $X, Y$ are random variables on $\mathcal S$, then
> $$\Delta[f(X), f(Y)] \leq \Delta[X, Y].$$

## Application

- [[knowledge/cryptography/foundations/Indistinguishability\|Indistinguishability]] — for every adversary $\mathcal A$: $\text{Distadv}[\mathcal A, P_0, P_1] \leq \Delta[P_0, P_1]$; negligible $\Delta$ gives **statistical indistinguishability**, which implies computational indistinguishability.
- [[knowledge/cryptography/primitive/key establishment/Key Derivation Problem\|Key Derivation Problem]] — bounding guessing advantage after key derivation.
