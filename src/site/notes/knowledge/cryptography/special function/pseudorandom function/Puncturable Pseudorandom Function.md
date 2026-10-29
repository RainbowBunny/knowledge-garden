---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/pseudorandom-function/puncturable-pseudorandom-function/","dg-note-properties":{}}
---

Reference:
- `[SW14 Def 7]` — A. Sahai, B. Waters, _How to Use Indistinguishability Obfuscation: Deniable Encryption, and More_, STOC 2014; full version ePrint 2013/454, §3 "PRF variants": https://eprint.iacr.org/2013/454.pdf
- `[BW13 Def 3.1]` — D. Boneh, B. Waters, _Constrained Pseudorandom Functions and Their Applications_, ASIACRYPT 2013; full version ePrint 2013/352, §3.2: https://eprint.iacr.org/2013/352.pdf
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Syntax

> [!definition] Parameters
> - $\lambda$: the security parameter.
> - $d = d(\lambda)$: the input length, any polynomial in $\lambda$; $\mathcal D = \{0, 1\}^{d}$: the domain.
> - $\mathcal R = \{0, 1\}^{r(\lambda)}$: the range.
> - $X$: a non-empty set of points of $\mathcal D$, of polynomial size. $k_X$: a key punctured at $X$.

> [!definition] Puncturable Pseudorandom Function
> A **puncturable pseudorandom function (PPRF)** is a triple of [[knowledge/cryptography/foundations/PPT\|PPT]] algorithms $\mathsf{PPRF} = (\mathsf{KeyGen}, \mathsf{Puncture}, \mathsf{Eval})$ over the spaces of Parameters:
> - $k \leftarrow \mathsf{KeyGen}(1^\lambda, 1^{d})$: Randomized key generation.
>     - **Input**: the security parameter $1^\lambda$ and the input length $1^{d}$.
>     - **Output**: a key $k$.
> - $k_X \leftarrow \mathsf{Puncture}(k, X)$: Puncturing.
>     - **Input**: a key $k$ and a set $\emptyset \neq X \subseteq \mathcal D$ of polynomial size.
>     - **Output**: a punctured key $k_X$.
> - $r \leftarrow \mathsf{Eval}(k, x)$: Deterministic evaluation.
>     - **Input**: a key $k$, or a punctured key $k_X$, and a point $x \in \mathcal D$.
>     - **Output**: a value $r \in \mathcal R$.

> [!remark] Notation in the literature
> `[SW14 Def 7]` writes the family as $F = (\mathsf{Key}_F, \mathsf{Puncture}_F, \mathsf{Eval}_F)$, with an input length $n(\lambda)$ and an output length $m(\lambda)$ fixed by the family, so its key generation $\mathsf{Key}_F(1^\lambda)$ takes no input length. This vault calls key generation $\mathsf{KeyGen}$ whatever the source calls it.

## Property

### Completeness of Puncturing

> [!definition] Completeness of Puncturing
> For any $d(\lambda) = \mathrm{poly}(\lambda)$, any $X \subseteq \mathcal D$, any $k$ output by $\mathsf{KeyGen}(1^\lambda, 1^{d})$, any $k_X$ output by $\mathsf{Puncture}(k, X)$ and any $x' \notin X$:
> $$\mathsf{Eval}(k, x') = \mathsf{Eval}(k_X, x').$$
> `[SW14 Def 7]` calls it *functionality preserved under puncturing*, and asks it with probability $1$ for every set $S$ output by a PPT adversary and every $x \notin S$.

## Security

### Pseudorandomness

> [!definition] Parameters
> - From Syntax: $\lambda, d, \mathcal D, \mathcal R, X, k_X$.
> - $(r_x)_{x \in X}$: one value for each punctured point, real in Game 0 and uniform in Game 1.
> - $\mathbb A$: the class of [[knowledge/cryptography/foundations/PPT\|PPT]] [[knowledge/cryptography/foundations/Adversary\|adversaries]].

> [!definition] Pseudorandomness
> ### Scope
> A puncturable PRF $\mathsf{PPRF} = (\mathsf{KeyGen}, \mathsf{Puncture}, \mathsf{Eval})$ and the adversary class $\mathbb A$ of Parameters.
>
> ---
> ### Condition
> - **Access** — the punctured key $k_X$ and one value $r_x$ for each punctured point; no oracle. With $k_X$, $\mathcal A$ evaluates every point outside $X$ by itself.
> - **Promise** — $\emptyset \neq X \subseteq \mathcal D$, of polynomial size.
> - **Quantifier** — for every polynomial $d(\lambda)$, $\forall \mathcal A \in \mathbb A$.
> - **Adaptivity** — selective: $\mathcal A$ chooses $X$ before the key is generated, so before it has seen anything.
>
> ---
> ### Experiment
> A distinguishing game: two branches that differ in row 2 only, **Game 0** (the real values at $X$) and **Game 1** (uniform values). `[SW14 Def 7]`
>
> | | challenger $\mathcal C$ | | adversary $\mathcal A$ |
> | --- | --- | --- | --- |
> | 1 | | $\xleftarrow{\ X\ }$ | chooses a set $\emptyset \neq X \subseteq \mathcal D$ of polynomial size |
> | 2 | $k \leftarrow \mathsf{KeyGen}(1^\lambda, 1^{d})$<br>$k_X \leftarrow \mathsf{Puncture}(k, X)$<br>**Game 0**: $r_x \leftarrow \mathsf{Eval}(k, x)$ for each $x \in X$<br>**Game 1**: $r_x \xleftarrow{\$} \mathcal R$ for each $x \in X$, independently | $\xrightarrow{\ k_X,\ (r_x)_{x \in X}\ }$ | |
> | 3 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |
>
> **Goal**
> - **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
> - **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.
>
> ---
> ### Property
> $$\mathsf{Adv}^{\mathsf{pprf}}_{\mathsf{PPRF}}(\mathcal A) = \big|\Pr[\mathsf{Expt}_0(\mathcal A) = 1] - \Pr[\mathsf{Expt}_1(\mathcal A) = 1]\big|.$$
> - $\mathsf{PPRF}$ is **pseudorandom at punctured points** if $\mathsf{Adv}^{\mathsf{pprf}}_{\mathsf{PPRF}}(\mathcal A)$ is negligible in $\lambda$ for every polynomial $d$ and every $\mathcal A \in \mathbb A$ `[SW14 Def 7]`.
>
> It is a *distinguishing* game, see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

> [!remark] Notation in the literature
> `[SW14 Def 7]` splits the adversary into $(\mathcal A_1, \mathcal A_2)$: $\mathcal A_1(1^\lambda)$ outputs the set $S$ and a state $\sigma$, and the advantage is
> $$\big|\Pr[\mathcal A_2(\sigma, K_S, S, \mathsf{Eval}_F(K, S)) = 1] - \Pr[\mathcal A_2(\sigma, K_S, S, U_{m(\lambda) \cdot |S|}) = 1]\big|,$$
> where $\mathsf{Eval}_F(K, S)$ concatenates the values at the points of $S$ in lexicographic order and $U_{m(\lambda) \cdot |S|}$ is a uniform string of the same length. Here $\mathcal A$ is one stateful machine, so no $\sigma$ is passed and $S$ (here $X$) is not sent back to it — see [[knowledge/cryptography/foundations/Security Game\|Security Game]].

## Variant

### Adaptive security

A constrained key in `[BW13 Def 3.1]` evaluates the function on a set $S$; a key punctured at $X$ is the constrained key for $S = \mathcal D \setminus X$ (BW13 does not use the word *puncturable*). Its game is adaptive: $\mathcal A$ asks for values and punctured keys in any order and picks the challenge points as it goes. Two branches that differ in the challenge answer only. `[BW13 Def 3.1]`

| | challenger $\mathcal C$ | | adversary $\mathcal A$ |
| --- | --- | --- | --- |
| 1 | $k \leftarrow \mathsf{KeyGen}(1^\lambda, 1^{d})$<br>$C \leftarrow \emptyset$<br>$V \leftarrow \emptyset$ | | |
| 2 | | $\xleftarrow{\ x\ }$ | **Evaluation queries** (repeated, adaptive): sends $x \in \mathcal D$ |
| | $y \leftarrow \mathsf{Eval}(k, x)$ if $x \notin C$, and $y \leftarrow \perp$ otherwise<br>$V \leftarrow V \cup \{x\}$ | $\xrightarrow{\ y\ }$ | |
| 3 | | $\xleftarrow{\ X\ }$ | **Puncture queries** (repeated, adaptive): sends a set $X \subseteq \mathcal D$ |
| | $k_X \leftarrow \mathsf{Puncture}(k, X)$ if $C \subseteq X$, and $k_X \leftarrow \perp$ otherwise<br>$V \leftarrow V \cup (\mathcal D \setminus X)$ | $\xrightarrow{\ k_X\ }$ | |
| 4 | | $\xleftarrow{\ x^*\ }$ | **Challenge queries** (repeated, adaptive): sends $x^* \in \mathcal D$ with $x^* \notin V$ |
| | **Game 0**: $y^* \leftarrow \mathsf{Eval}(k, x^*)$<br>**Game 1**: $y^* \xleftarrow{\$} \mathcal R$, the same value as before if $x^*$ was already challenged<br>$C \leftarrow C \cup \{x^*\}$ | $\xrightarrow{\ y^*\ }$ | |
| 5 | | $\xleftarrow{\ b'\ }$ | outputs a bit $b'$ |

**Goal**
- **Output** — $\mathsf{Expt}_b(\mathcal A)$, the bit $b'$ in Game $b$.
- **Measure** — how far apart $\Pr[\mathsf{Expt}_0(\mathcal A) = 1]$ and $\Pr[\mathsf{Expt}_1(\mathcal A) = 1]$ are.

The advantage is the difference of the two probabilities, $\mathrm{Adv}^{\mathrm{PRF}}_{\mathcal A, F}(\lambda) = |\Pr[W_0] - \Pr[W_1]|$ in BW13's notation, with $W_b$ the event that $b' = 1$ in Game $b$:
- the PRF is a **secure constrained PRF** if this is negligible for every PPT $\mathcal A$ `[BW13 Def 3.1]`;
- BW13 remarks that allowing a single challenge query gives an equivalent definition, by a hybrid argument.

The set $V$ holds every point $\mathcal A$ can evaluate by itself, so a challenge is never trivial; the set $C$ keeps later queries from revealing a challenged point.

## Related

### Prerequisites
- [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|Pseudorandom Function]], [[knowledge/cryptography/foundations/Security Game\|Security Game]], [[knowledge/cryptography/foundations/Adversary\|Adversary]]
