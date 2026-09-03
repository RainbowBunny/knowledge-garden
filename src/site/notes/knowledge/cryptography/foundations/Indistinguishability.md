---
{"dg-publish":true,"permalink":"/knowledge/cryptography/foundations/indistinguishability/","dg-note-properties":{}}
---

## Definition

> [!algorithm] $q$-Sample Distinguishing Advantage
> For probability distributions $P_0$ and $P_1$ on a finite set $\mathcal R$, and adversary $\mathcal A = (\mathcal A_\mathsf{guess})$, we define the $q$-sample distinguishing advantage:
> $$\mathsf{Adv}^{q\mbox{-}\mathsf{Dist}}_{P_0, P_1}(\mathcal A) = 
> \left|\; \Pr\!\left[
> \begin{array}{l}
> b = 1
> \end{array}
> \;\middle |\; 
> \begin{array}{l}
> x_1, x_2, \dots, x_q \xleftarrow{\$} P_0 \\
> b \leftarrow \mathcal A_\mathsf{guess}(x_1, x_2, \dots, x_q)
> \end{array} \right] 
> \;- 
> \Pr\!\left[
> \begin{array}{l}
> b = 1
> \end{array}
> \;\middle |\; 
> \begin{array}{l}
> x_1, x_2, \dots, x_q \xleftarrow{\$} P_1 \\
> b \leftarrow \mathcal A_\mathsf{guess}(x_1, x_2, \dots, x_q)
> \end{array} \right] 
> \right|.
> $$

> [!definition] Algorithms Distribution
> Consider a probabilistic algorithm $U$. We write $U_x$ as the probability distribution of $U$'s output, on input $x$. 

> [!definition] Indistinguishability
> Given two probabilistic algorithms (or families of distributions) $U, V$, we say that
> - $U, V$ are perfectly indistinguishable, written $U \sim^p V$, if $U_x = V_x$ for every $x$.
> - $U, V$ are statistically indistinguishable, written $U \sim^s V$, if the [[knowledge/math/probability/Statistical Distance\|Statistical Distance]] $\Delta[U_x, V_x]$ is [[knowledge/cryptography/foundations/Negligible Function\|Negligible Function]] in the length of $x$.
> - $U, V$ are computationally indistinguishable, written $U \sim^c V$ iff for any [[knowledge/cryptography/foundations/PPT\|PPT]] $D(U)$ that takes input $(x, U(x))$ we have $D(U) \sim^s D(V)$.
> 
> Sometimes, we do not want to consider how $U, V$ behave on arbitrary input $x$, but only when $x$ is in some language $L$. We then say, e.g. $U \sim^c V$ on input $x \in L.$

## Property

> [!theorem]
> For every adversary $\mathcal A$ (even computationally unbounded): $\text{Adv}^{q\text{-Dist}}_{P_0, P_1}[\mathcal A] \leq q \cdot \Delta[P_0, P_1]$.

> [!corollary]
> Statistical indistinguishability implies computational indistinguishability. The converse fails: e.g. the output of a secure PRG is computationally, but not statistically, indistinguishable from uniform.

> [!theorem]
> If $\mathcal S$ and $\mathcal T$ are finite sets, $X$ and $Y$ are random variables taking values in $\mathcal S$, and $f: \mathcal S \rightarrow \mathcal T$ is a function, then $\Delta[f(X), f(Y)] \leq \Delta[X, Y]$

## Application

- [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Indistinguishability\|Symmetric Key Encryption#Indistinguishability]] and [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption#Indistinguishability\|Public-Key Encryption#Indistinguishability]] — security definitions are distinguishing games between two ciphertext distributions.
- Hybrid arguments — chains of computationally indistinguishable distributions are indistinguishable (loss linear in the chain length).
