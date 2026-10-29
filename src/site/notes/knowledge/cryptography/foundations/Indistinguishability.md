---
{"dg-publish":true,"permalink":"/knowledge/cryptography/foundations/indistinguishability/","dg-note-properties":{}}
---

Reference:
- `[DN08]` — I. Damgård, J. B. Nielsen, _Commitment Schemes and Zero-Knowledge Protocols_, lecture notes, Aarhus University, 2008: https://users-cs.au.dk/~ivan/ComZK08.pdf (§2.2, Definition 3).
- `[FV20]` — S. Fehr, S. Vaudenay, _Sublinear Bounds on the Distinguishing Advantage for Multiple Samples_, IWSEC 2020, LNCS 12231: https://ir.cwi.nl/pub/30130/30130.pdf (§1.1, §2.1, Eq. (1)).

## Definition

> [!definition] Parameters
> - $P_0, P_1$: probability distributions on a finite set $\mathcal R$.
> - $q$: the number of samples.
> - $\mathcal A$: an [[knowledge/cryptography/foundations/Adversary\|Adversary]], one stateful interactive machine ([[knowledge/cryptography/foundations/Security Game\|Security Game]]), possibly computationally unbounded.

> [!definition] $q$-Sample Distinguishing Advantage
> ### Scope
> Two distributions $P_0, P_1$ on $\mathcal R$ and any adversary $\mathcal A$ of Parameters.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ receives $q$ samples and nothing else: no oracle.
> - **Promise** — the $q$ samples are independent and all come from the same distribution.
> - **Quantifier** — $\forall \mathcal A$; the bound in Property holds even for unbounded $\mathcal A$.
> - **Adaptivity** — none: the samples are sent at once, before $\mathcal A$ speaks.
>
> ---
> ### Experiment
> A distinguishing game: two branches that differ in row 1 only, **Game 0** ($P_0$) and **Game 1** ($P_1$). `[FV20 §1.1]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | **Game 0**: $x_1, x_2, \dots, x_q \xleftarrow{\$} P_0$<br>**Game 1**: $x_1, x_2, \dots, x_q \xleftarrow{\$} P_1$ | $\xrightarrow{\ x_1,\, \dots,\, x_q\ }$ | |
> | 2 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\mathsf{Adv}^{q\mbox{-}\mathsf{Dist}}_{P_0, P_1}(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$$
> - The largest advantage over all, even unbounded, $\mathcal A$ is the [[knowledge/math/probability/Statistical Distance\|Statistical Distance]] $\Delta[P_0^{\otimes q}, P_1^{\otimes q}]$ of the product distributions `[FV20 §1.1]`.
>
> It is a *distinguishing* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Notation in the literature
> - `[FV20]` writes $n$ for the number of samples and $d(P_0, P_1) = \tfrac12 \sum_z \lvert P_0(z) - P_1(z) \rvert$ for the statistical distance.

> [!definition] Algorithms Distribution
> Consider a probabilistic algorithm $U$. We write $U_x$ as the probability distribution of $U$'s output, on input $x$. `[DN08 §2.2]`

> [!definition] Parameters
> - $U, V$: probabilistic algorithms, or families of distributions $U_x, V_x$ indexed by the input $x$.
> - $x$: an input; negligibility is measured in its length $\lvert x \rvert$. $L$: a language that $x$ may be restricted to.
> - $\mathcal D$: a [[knowledge/cryptography/foundations/PPT\|PPT]] distinguisher, in the computational case.

> [!definition] Indistinguishability
> Given two probabilistic algorithms (or families of distributions) $U, V$, we say that `[DN08 Def 3]`
> - $U, V$ are perfectly indistinguishable, written $U \sim^p V$, if $U_x = V_x$ for every $x$.
> - $U, V$ are statistically indistinguishable, written $U \sim^s V$, if the [[knowledge/math/probability/Statistical Distance\|Statistical Distance]] $\Delta[U_x, V_x]$ is [[knowledge/cryptography/foundations/Negligible Function\|Negligible Function]] in the length of $x$.
> - $U, V$ are computationally indistinguishable, written $U \sim^c V$, iff for every [[knowledge/cryptography/foundations/PPT\|PPT]] distinguisher $\mathcal D$ the advantage of the game below is negligible in the length of $x$. Equivalently, for any [[knowledge/cryptography/foundations/PPT\|PPT]] $D(U)$ that takes input $(x, U(x))$ we have $D(U) \sim^s D(V)$.
> 
> Sometimes, we do not want to consider how $U, V$ behave on arbitrary input $x$, but only when $x$ is in some language $L$. We then say, e.g. $U \sim^c V$ on input $x \in L.$

> [!definition] Computational Indistinguishability Game
> A distinguishing game for a fixed input $x$: two branches that differ in row 1 only, **Game 0** ($U$) and **Game 1** ($V$). `[DN08 Def 3]`
>
> | | challenger $\mathcal C$ | | distinguisher $\mathcal D$ |
> | --- | --- | --- | --- |
> | 1 | **Game 0**: $y \leftarrow U(x)$<br>**Game 1**: $y \leftarrow V(x)$ | $\xrightarrow{\ (x,\, y)\ }$ | |
> | 2 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal D, x)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal D, x) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal D, x) = 1]$ are, as a function of $x$.
>
> $$\mathsf{Adv}_{U, V}(\mathcal D, x) = \big|\Pr[\mathsf{Expt}_0(\mathcal D, x) = 1] - \Pr[\mathsf{Expt}_1(\mathcal D, x) = 1]\big|.$$
> - $U \sim^c V$ iff $\mathsf{Adv}_{U, V}(\mathcal D, x)$ is negligible in $\lvert x \rvert$ for every [[knowledge/cryptography/foundations/PPT\|PPT]] $\mathcal D$.
> - $U \sim^c V$ on input $x \in L$ iff the same holds with $x$ ranging over $L$ only.
>
> `[DN08 Def 3]` writes $p_{U, D}(x)$ and $p_{V, D}(x)$ for the probabilities that $D$ outputs the guess "$U$" in the two games.

## Property

> [!theorem]
> For every adversary $\mathcal A$ (even computationally unbounded): $\text{Adv}^{q\text{-Dist}}_{P_0, P_1}[\mathcal A] \leq q \cdot \Delta[P_0, P_1]$.
>
> `[FV20 Eq. (1)]`: the largest advantage is $\Delta[P_0^{\otimes q}, P_1^{\otimes q}]$, and $\Delta[P_0^{\otimes q}, P_1^{\otimes q}] \leq q \cdot \Delta[P_0, P_1]$ by subadditivity.

> [!corollary]
> Statistical indistinguishability implies computational indistinguishability. The converse fails: e.g. the output of a secure PRG is computationally, but not statistically, indistinguishable from uniform.

> [!theorem]
> If $\mathcal S$ and $\mathcal T$ are finite sets, $X$ and $Y$ are random variables taking values in $\mathcal S$, and $f: \mathcal S \rightarrow \mathcal T$ is a function, then $\Delta[f(X), f(Y)] \leq \Delta[X, Y]$

## Application

- [[knowledge/cryptography/primitive/symmetric encryption/Symmetric Key Encryption#Indistinguishability\|Symmetric Key Encryption#Indistinguishability]] and [[knowledge/cryptography/primitive/public-key encryption/Public-Key Encryption Scheme (Old)#Indistinguishability\|Public-Key Encryption Scheme (Old)#Indistinguishability]] — security definitions are distinguishing games between two ciphertext distributions.
- Hybrid arguments — chains of computationally indistinguishable distributions are indistinguishable (loss linear in the chain length).
