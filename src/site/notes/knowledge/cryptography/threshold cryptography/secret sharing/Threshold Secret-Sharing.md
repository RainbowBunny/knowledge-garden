---
{"dg-publish":true,"permalink":"/knowledge/cryptography/threshold-cryptography/secret-sharing/threshold-secret-sharing/","dg-note-properties":{}}
---

Reference:
- `[Sha79]` — A. Shamir, _How to Share a Secret_, Communications of the ACM 22(11), November 1979: https://cs.tau.ac.il/~bchor/Shamir.html
- `[BS §22.1]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, §22.1 _Shamir's secret sharing scheme_ (§22.1.2 security): https://toc.cryptobook.us/ — not read here.
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Syntax

> [!definition] Parameters
> - $n$: the number of users, numbered $1, \dots, n$. $t$: the threshold (`[Sha79]` writes $k$).
> - $\mathcal M$: the message space; $m \in \mathcal M$ is the secret (`[Sha79]`: $D$). $s_i$: the share of user $i$ (`[Sha79]`: $D_i$).
> - $U \subseteq \{1, \dots, n\}$: a set of users; $\{s_i : i \in U\}$: their shares.

> [!definition] Threshold Secret Sharing Scheme
> A **$t$-out-of-$n$ threshold secret-sharing scheme** $\mathrm{TSS} = (\mathsf{Share}, \mathsf{Reconstruct})$ is a pair of efficient algorithms:
> - $(s_1, \dots, s_n) \leftarrow \mathsf{Share}(m)$:
> 	- **Input**: a message $m \in \mathcal M$.
> 	- **Output**: shares $s_1, \dots, s_n$. Randomized.
> - $m \leftarrow \mathsf{Reconstruct}(\{s_i : i \in U\})$:
> 	- **Input**: the shares of a set $U$ with $|U| \geq t$.
> 	- **Output**: a message. Deterministic.

> [!definition] Authorized Set
> $U$ is **authorized** if $|U| \geq t$ and **unauthorized** otherwise. Shamir's two requirements for a $(k, n)$ threshold scheme: knowledge of any $k$ or more pieces makes $D$ easily computable; knowledge of any $k - 1$ or fewer pieces leaves $D$ completely undetermined, in the sense that all its possible values are equally likely. `[Sha79]`

## Property

### Correctness

> [!definition] Correctness
> For every $m \in \mathcal M$, every output $(s_1, \dots, s_n)$ of $\mathsf{Share}(m)$ and every authorized $U$:
> $$\mathsf{Reconstruct}(\{s_i : i \in U\}) = m.$$
> This is Shamir's first requirement. `[Sha79]`

## Security

### Privacy

> [!definition] Privacy
> ### Scope
> A $t$-out-of-$n$ scheme and an adversary $\mathcal A$, computationally unbounded.
>
> ---
> ### Condition
> - **Access** — $\mathcal A$ receives the shares of the set it chose, nothing else.
> - **Promise** — $U$ is unauthorized, $|U| < t$.
> - **Quantifier** — $\forall \mathcal A$.
> - **Adaptivity** — $\mathcal A$ fixes $m_0, m_1$ and $U$ before seeing any share.
>
> ---
> ### Experiment
> A distinguishing game: the branches differ in the shared message only.
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | | $\xleftarrow{\ m_0,\, m_1,\, U\ }$ | chooses $m_0, m_1 \in \mathcal M$ and an unauthorized $U$ |
> | 2 | **Game 0**: $(s_1, \dots, s_n) \leftarrow \mathsf{Share}(m_0)$<br>**Game 1**: $(s_1, \dots, s_n) \leftarrow \mathsf{Share}(m_1)$ | $\xrightarrow{\ \{s_i \,:\, i \in U\}\ }$ | |
> | 3 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\mathsf{Adv}^\mathsf{priv}_\mathrm{TSS}(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$$
> - The scheme is **perfectly private** if $\mathsf{Adv}^\mathsf{priv}_\mathrm{TSS}(\mathcal A) = 0$ for every $\mathcal A$: the shares of an unauthorized set have the same distribution whatever the secret — Shamir's second requirement, "all its possible values are equally likely" `[Sha79]`.
>
> It is a *distinguishing* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Source of the game
> `⚠️ CLAUDE – verify:` the game form follows `[BS §22.1.2]`, which was not read here; `[Sha79]` states the property in words, as in the Authorized Set definition above.

## Related

### Instantiations
- [[knowledge/cryptography/threshold cryptography/secret sharing/scheme/Shamir Secret Sharing\|Shamir Secret Sharing]] — a random polynomial of degree $t - 1$ with constant term $m$, shares $s_i = (i, f(i) \bmod p)$ for a prime $p$ larger than the secret and than $n$ `[Sha79]`
- [[knowledge/cryptography/threshold cryptography/secret sharing/scheme/Simple n-out-of-n Scheme\|Simple n-out-of-n Scheme]]

### Prerequisites
- [[knowledge/cryptography/foundations/Security Game\|Security Game]]
