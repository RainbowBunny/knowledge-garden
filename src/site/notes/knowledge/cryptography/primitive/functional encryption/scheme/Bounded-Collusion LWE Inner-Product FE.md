---
{"dg-publish":true,"permalink":"/knowledge/cryptography/primitive/functional-encryption/scheme/bounded-collusion-lwe-inner-product-fe/","dg-note-properties":{"aliases":["ABPSY17 LWE IPFE"]}}
---

Reference:
- `[ABPSY17]` — S. Agrawal, S. Bhattacherjee, D. H. Phan, D. Stehlé, S. Yamada, _Efficient Public Trace and Revoke from Standard Assumptions_, ACM CCS 2017. Numbers refer to the full version, ePrint 2017/650, §2.2 (the random-key bounded-collusion model), §4.2 (the scheme, Theorem 18, Lemmas 4–7, 19, 20): https://eprint.iacr.org/2017/650.pdf
- `[ALS16]` — S. Agrawal, B. Libert, D. Stehlé, _Fully Secure Functional Encryption for Inner Products, from Standard Assumptions_, CRYPTO 2016, LNCS 9816, pp. 333–362 — the scheme this one modifies (`[ABPSY17]`'s reference [4]); not opened.

## Scheme

Reference Name: $\mathsf{FE}_\mathsf{LWE}$
Instantiates:: [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption\|Inner-Product Functional Encryption]]

### Setting

> [!scheme] Setting
> - $\mathbb Z_q$ with $q = p^k$ and $k \geq 2$: the plaintext modulus $p$ divides the ciphertext modulus, and a message $\mu \in \mathbb Z_p$ is encoded as $p^{k-1} \mu \in \mathbb Z_q$.
> - Discrete Gaussians $\mathcal D_{\mathbb Z, \sigma}$ and $\mathcal D_{p\mathbb Z + x, \sigma}$ (over the coset $p\mathbb Z + x$), entrywise on vectors and matrices ([[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution\|Discrete Gaussian Distribution]]).

### Parameters

> [!definition] Parameters
> - [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption\|Inner-Product Functional Encryption]]: Import $(\lambda, p)$; the vectors have length $2\ell$.
> - $L$: the bound on the number of key queries (the collusion bound).
> - $n, m$: the LWE dimension and the number of samples. $k \geq 2$, $q = p^k$.
> - $\alpha \in (0, 1)$: the encryption noise rate. $\sigma_0$: the width of the master key. $\sigma_1, \sigma_2$: the widths of the key lifts on the two halves.
> - $\alpha'$: the noise rate of the LWE assumption in the proof. $\kappa$: the statistical parameter of Lemma 19.
> - Conditions `[ABPSY17 §4.2]`:
>     - $p^{k-1}/4 > \sigma_0 (\sigma_1 + \sigma_2)\, \alpha q \sqrt{\ell m} \cdot \omega(\log^{3/2} \lambda)$ — correctness;
>     - $\sigma_1, \sigma_2 \geq p \cdot \Omega(\sqrt\lambda)$;
>     - $\alpha / \alpha' \geq \Omega(\sigma_0 \sqrt m)$;
>     - $\sigma_0, \alpha' q \geq \Omega(\sqrt \lambda)$;
>     - $\kappa \geq \Omega(\lambda + L \log \lambda)$;
>     - $\sigma_0 \geq \Omega(p \kappa \ell \sigma_2)$;
>     - $q^{n+1} / p^m \leq 2^{-\Omega(\kappa)}$.

### Algorithms

> [!scheme] Algorithms
> - $(\mathrm{pk}, \mathrm{msk}) \leftarrow \mathsf{Setup}(1^\lambda, 1^L, 1^{2\ell})$: (Randomized) Setup algorithm.
>     - **Input**: the security parameter, the collusion bound $L$ and the vector length $2\ell$, in unary.
>     - **Output**: $\mathrm{pk} = (\mathbf A, \mathbf U)$ and $\mathrm{msk} = \mathbf Z$.
>     - **Steps**:
>         1. Sets $n, m$, $q = p^k$, $\alpha$, $\sigma_0, \sigma_1, \sigma_2$ as in Parameters.
>         2. Samples $\mathbf A \xleftarrow{\$} \mathbb Z_q^{m \times n}$.
>         3. Samples $\mathbf Z \leftarrow \mathcal D_{\mathbb Z, \sigma_0}^{2\ell \times m}$.
>         4. Sets $\mathbf U = \mathbf Z \mathbf A \bmod q \in \mathbb Z_q^{2\ell \times n}$.
>         5. Returns $\mathrm{pk} = (\mathbf A, \mathbf U)$ and $\mathrm{msk} = \mathbf Z$.
> - $\mathrm{sk}_\mathbf x \leftarrow \mathsf{KeyGen}(\mathrm{msk}, \mathbf x)$: (Randomized) Key-generation algorithm.
>     - **Input**: $\mathrm{msk} = \mathbf Z$ and a vector $\mathbf x = (x_1, \dots, x_{2\ell})^\top \in \mathbb Z_p^{2\ell}$.
>     - **Output**: $\mathrm{sk}_\mathbf x = (\bar{\mathbf x}, \mathbf z_\mathbf x) \in \mathbb Z^{2\ell} \times \mathbb Z^m$.
>     - **Steps**:
>         1. Samples $\bar x_i \leftarrow \mathcal D_{p\mathbb Z + x_i, \sigma_1}$ for $i \in [\ell]$.
>         2. Samples $\bar x_i \leftarrow \mathcal D_{p\mathbb Z + x_i, \sigma_2}$ for $i \in [\ell + 1, 2\ell]$.
>         3. Sets $\bar{\mathbf x} = (\bar x_1, \dots, \bar x_{2\ell})^\top \in \mathbb Z^{2\ell}$; so $\bar{\mathbf x} \equiv \mathbf x \pmod p$.
>         4. Sets $\mathbf z_\mathbf x^\top = \bar{\mathbf x}^\top \mathbf Z \in \mathbb Z^m$.
>         5. Returns $\mathrm{sk}_\mathbf x = (\bar{\mathbf x}, \mathbf z_\mathbf x)$.
> - $C \leftarrow \mathsf{Enc}(\mathrm{pk}, \mathbf y)$: (Randomized) Encryption algorithm.
>     - **Input**: $\mathrm{pk} = (\mathbf A, \mathbf U)$ and a message $\mathbf y \in \mathbb Z_p^{2\ell}$.
>     - **Output**: $C = (\mathbf c_0, \mathbf c_1) \in \mathbb Z_q^m \times \mathbb Z_q^{2\ell}$.
>     - **Steps**:
>         1. Samples $\mathbf s \xleftarrow{\$} \mathbb Z_q^n$.
>         2. Samples $\mathbf e_0 \leftarrow \mathcal D_{\mathbb Z, \alpha q}^m$.
>         3. Samples $\mathbf e_1 \leftarrow \mathcal D_{\mathbb Z, \alpha q}^{2\ell}$.
>         4. Computes $\mathbf c_0 = \mathbf A \mathbf s + \mathbf e_0 \in \mathbb Z_q^m$.
>         5. Computes $\mathbf c_1 = \mathbf U \mathbf s + \mathbf e_1 + p^{k-1} \cdot \mathbf y \in \mathbb Z_q^{2\ell}$.
>         6. Returns $C = (\mathbf c_0, \mathbf c_1)$.
> - $\mu \leftarrow \mathsf{Dec}(\mathrm{sk}_\mathbf x, C)$: (Deterministic) Decryption algorithm.
>     - **Input**: $\mathrm{sk}_\mathbf x = (\bar{\mathbf x}, \mathbf z_\mathbf x)$ and $C = (\mathbf c_0, \mathbf c_1)$.
>     - **Output**: $\mu \in \mathbb Z_p$, the inner product $\langle \mathbf x, \mathbf y \rangle \bmod p$.
>     - **Steps**:
>         1. Computes $\mu' = \langle \bar{\mathbf x}, \mathbf c_1 \rangle - \langle \mathbf z_\mathbf x, \mathbf c_0 \rangle \bmod q$.
>         2. Returns the $\mu \in \mathbb Z_p$ that minimizes $\lvert p^{k-1} \mu - \mu' \rvert$.
>
> `[ABPSY17 §4.2]`

> [!remark] What changes from `[ALS16]`
> `[ABPSY17 §4.2]` presents the scheme as a modification of the LWE scheme of `[ALS16]` for the random-key bounded-collusion model: the vectors are doubled to length $2\ell$, and a key is the Gaussian lift $\bar{\mathbf x}$ of $\mathbf x$ on the coset $\mathbf x + p\mathbb Z^{2\ell}$, with width $\sigma_1$ on the first half and $\sigma_2$ on the second.

## Property

### Correctness

> [!property] $\mathsf{FE}_\mathsf{LWE}$ Correctness
> Since $\mathbf U = \mathbf Z \mathbf A$ and $\mathbf z_\mathbf x^\top = \bar{\mathbf x}^\top \mathbf Z$, the mask $\mathbf s$ cancels:
> $$\mu' = p^{k-1} \langle \bar{\mathbf x}, \mathbf y \rangle + \langle \bar{\mathbf x}, \mathbf e_1 \rangle - \langle \mathbf z_\mathbf x, \mathbf e_0 \rangle \bmod q,$$
> and $p^{k-1} \langle \bar{\mathbf x}, \mathbf y \rangle = p^{k-1} \langle \mathbf x, \mathbf y \rangle \bmod q$ because $\bar{\mathbf x} \equiv \mathbf x \pmod p$. The first condition of Parameters makes the noise $\langle \bar{\mathbf x}, \mathbf e_1 \rangle - \langle \mathbf z_\mathbf x, \mathbf e_0 \rangle$ smaller than $p^{k-1}/4$ with probability $1 - \lambda^{-\omega(1)}$, so rounding returns $\langle \mathbf x, \mathbf y \rangle \bmod p$. `[ABPSY17 §4.2]`

## Security

### $L$-IND-CPA

> [!security] $L$-IND-CPA under LWE `[ABPSY17 Thm 18]`
> Under the conditions of Parameters, $\mathsf{FE}_\mathsf{LWE}$ is $L$-IND-CPA secure — the [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption#Random-key bounded collusion\|random-key bounded-collusion game]] with at most $L$ key queries and vectors in $\mathbb Z_p^{2\ell}$ — under the [[knowledge/cryptography/assumptions/lattice-based/LWE/Learning With Error#Decision Variant\|$\mathrm{LWE}_{n, m, q, \alpha'}$ assumption]].

> [!lemma] Lemmas used in the proof
> - **Lemma 4** (Gaussian modulo a sublattice) — for full-rank lattices $\Lambda' \subseteq \Lambda$ of the same dimension and $\varepsilon \in (0, 1/2)$, if $s_m(\Sigma) \geq \eta_\varepsilon(\Lambda')$, then $\mathcal D_{\Lambda, \Sigma, \mathbf c} \bmod \Lambda'$ is within statistical distance $2\varepsilon$ of uniform over $\Lambda / \Lambda'$. ([[knowledge/math/algebra/structures/lattice/Lattice Smoothing\|Lattice Smoothing]])
> - **Lemma 5** ($\mathsf{ReRand}$) — for $r \geq \Omega(\sqrt\lambda)$, $\mathbf x \leftarrow \mathcal D_{\mathbb Z^m, r}$ and $\mathbf V \in \mathbb Z^{\ell \times m}$ with $r' > s_1(\mathbf V)$, the algorithm $\mathsf{ReRand}(\mathbf V, \mathbf b + \mathbf x, r, r')$ outputs $\mathbf V \mathbf b + \mathbf x'$ with $\mathbf x'$ within statistical distance $2^{-\Omega(\lambda)}$ of $\mathcal D_{\mathbb Z^\ell, 2 r r'}$.
> - **Lemma 7** (singular values of a Gaussian matrix) — for $m \geq 2n$, $\sigma \geq K \eta_\varepsilon(\mathbb Z)$ and $\mathbf X \leftarrow \mathcal D_{\mathbb Z, \sigma}^{n \times m}$, the extreme singular values lie in $(\sigma \sqrt{2\pi m / K}, \sigma K \sqrt{2\pi m})$ except with probability $4 m \varepsilon + O(e^{-m/K})$.
>
> `[ABPSY17 Lemmas 4, 5, 7]`

> [!proof] Games of the proof of Theorem 18 `[ABPSY17 §4.2]`
> Game 0 is the $L$-IND-CPA game: the challenger shows random vectors $\mathbf x_1, \mathbf x_2, \ldots \xleftarrow{\$} \mathbb Z_p^{2\ell}$, $\mathcal A$ asks for keys of at most $L$ of them, gets $C^* \leftarrow \mathsf{Enc}(\mathrm{pk}, \mathbf y_\beta)$ for its admissible pair $\mathbf y_0, \mathbf y_1$, and makes no further key query. The games change how the challenger runs two algorithms; each table has one column per game, "same" where a line is unchanged, and the justification of the hop from the previous game in its last row.
>
> **The random vectors and their keys** (one run per vector shown to $\mathcal A$; the key is handed over only if $\mathcal A$ asks for it):
>
> | # | Game 0 | Game 1 – 4 |
> | --- | --- | --- |
> | 1 | samples $\mathbf x \xleftarrow{\$} \mathbb Z_p^{2\ell}$ | samples $\bar x_i \leftarrow \mathcal D_{\mathbb Z, \sigma_1}$ for $i \in [\ell]$ |
> | 2 | samples $\bar x_i \leftarrow \mathcal D_{p\mathbb Z + x_i, \sigma_1}$ for $i \in [\ell]$ | samples $\bar x_i \leftarrow \mathcal D_{\mathbb Z, \sigma_2}$ for $i \in [\ell + 1, 2\ell]$ |
> | 3 | samples $\bar x_i \leftarrow \mathcal D_{p\mathbb Z + x_i, \sigma_2}$ for $i \in [\ell + 1, 2\ell]$ | sets $\bar{\mathbf x} = (\bar x_1, \dots, \bar x_{2\ell})^\top$ |
> | 4 | sets $\bar{\mathbf x} = (\bar x_1, \dots, \bar x_{2\ell})^\top$ | sets $\mathbf x = \bar{\mathbf x} \bmod p$ |
> | 5 | sets $\mathbf z_\mathbf x^\top = \bar{\mathbf x}^\top \mathbf Z$ | same |
> | 6 | returns $\mathrm{sk}_\mathbf x = (\bar{\mathbf x}, \mathbf z_\mathbf x)$ | same |
> | hop | — | Game 0 → 1: statistical, Lemma 4, since $\sigma_1, \sigma_2 \geq p \cdot \Omega(\sqrt\lambda)$; change $\leq 2^{-\Omega(\lambda)}$ |
>
> **Challenge encryption** of $\mathbf y_\beta$:
>
> | # | Game 0 – 1 | Game 2 | Game 3 | Game 4 |
> | --- | --- | --- | --- | --- |
> | 1 | samples $\mathbf s \xleftarrow{\$} \mathbb Z_q^n$ | same | samples $\mathbf u \xleftarrow{\$} \mathbb Z_q^m$ | samples $\mathbf u \xleftarrow{\$} \mathbb Z_q^m$ |
> | 2 | samples $\mathbf e_0 \leftarrow \mathcal D_{\mathbb Z, \alpha q}^m$<br>samples $\mathbf e_1 \leftarrow \mathcal D_{\mathbb Z, \alpha q}^{2\ell}$ | samples $\mathbf e \leftarrow \mathcal D_{\mathbb Z, \alpha' q}^m$ | same as Game 2 | samples $\mathbf e_0 \leftarrow \mathcal D_{\mathbb Z, \alpha q}^m$<br>samples $\mathbf e_1 \leftarrow \mathcal D_{\mathbb Z, \alpha q}^{2\ell}$ |
> | 3 | — | sets $\mathbf b = \mathbf A \mathbf s + \mathbf e$ | sets $\mathbf b = \mathbf u + \mathbf e$ | — |
> | 4 | — | sets $\mathbf V = \begin{pmatrix} \mathbf I_m \\ \mathbf Z \end{pmatrix}$ | same | — |
> | 5 | $\mathbf c_0 = \mathbf A \mathbf s + \mathbf e_0$<br>$\mathbf c_1 = \mathbf U \mathbf s + \mathbf e_1 + p^{k-1} \mathbf y_\beta$ | $(\mathbf c_0 \Vert \mathbf c_1) = \mathsf{ReRand}(\mathbf V, \mathbf b, \alpha' q, \alpha / (2\alpha'))$<br>$\phantom{(\mathbf c_0 \Vert \mathbf c_1) =} + p^{k-1} (\mathbf 0^m \Vert \mathbf y_\beta)$ | same | $\mathbf c_0 = \mathbf u + \mathbf e_0$<br>$\mathbf c_1 = \mathbf Z \mathbf u + \mathbf e_1 + p^{k-1} \mathbf y_\beta$ |
> | 6 | returns $C^* = (\mathbf c_0, \mathbf c_1)$ | same | same | same |
> | hop | — | statistical: Lemma 7 bounds $s_1(\mathbf V) \leq O(\sigma_0 \sqrt m)$, then Lemma 5 applies since $\alpha / \alpha' \geq \Omega(\sigma_0 \sqrt m)$; change $\leq 2^{-\Omega(\lambda)}$ | computational: $\mathrm{LWE}_{n, m, q, \alpha'}$ | statistical, Lemma 5; change $\leq 2^{-\Omega(\lambda)}$ |
>
> **Game 4 is close to a fair coin.** Every queried $\mathbf x$ satisfies $\langle \mathbf x, \mathbf y_1 - \mathbf y_0 \rangle = 0 \bmod p$. Lemma 19 shows that the tuple $(\mathbf A, \mathbf u, \mathbf Z \mathbf A, \mathbf X_\mathrm{top}, \mathbf X_\mathrm{top} \mathbf Z, \mathbf X_\mathrm{bot} \mathbf Z \mathbf u)$ — $\mathbf X_\mathrm{top}$ built from the queried keys, $\mathbf X_\mathrm{bot}$ completing it — is within statistical distance $2^{-\Omega(\kappa)}$ of the same tuple with $\mathbf X_\mathrm{bot} \mathbf Z \mathbf u$ replaced by a uniform vector; Lemma 20 turns an adversary with advantage $\varepsilon$ in Game 4 into a distinguisher for Lemma 19 with advantage $\varepsilon / Q^L$, by guessing which of the $Q$ random vectors will be queried. Hence
> $$\varepsilon \leq Q^L \cdot 2^{-\Omega(\kappa)} \leq 2^{-\Omega(\lambda)},$$
> using $\kappa = \Theta(\lambda + L \log \lambda)$.
>
> **Goal** of every game
> - **Output** — the bit $b'$ of $\mathcal A$; $W_\beta$ is the event $b' = 1$ when $\mathbf y_\beta$ is encrypted.
> - **Measure** — how far apart $\Pr[W_0]$ and $\Pr[W_1]$ are; it moves by the amounts in the hop rows, and is $2^{-\Omega(\lambda)}$ in Game 4.

> [!remark] Two letters for the query bound
> `[ABPSY17 §2.2]` calls the notion $Q$-IND-CPA with $Q$ key queries; §4.2 uses $L$ for the number of key queries and $Q$ for the number of random vectors shown. This note follows §4.2.

## Related

### Constructions
- [[knowledge/cryptography/primitive/public-key encryption/Trace-and-Revoke from Inner-Product FE\|Trace-and-Revoke from Inner-Product FE]] — with $(t + r)$-IND-CPA security, this gives a publicly traceable trace-and-revoke scheme from LWE

### Prerequisites
- [[knowledge/cryptography/primitive/functional encryption/Inner-Product Functional Encryption\|Inner-Product Functional Encryption]], [[knowledge/cryptography/assumptions/lattice-based/LWE/Learning With Error\|Learning With Error]], [[knowledge/math/probability/discrete probability/distribution/Discrete Gaussian Distribution\|Discrete Gaussian Distribution]], [[knowledge/math/algebra/structures/lattice/Lattice Smoothing\|Lattice Smoothing]]
