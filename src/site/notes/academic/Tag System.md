---
{"dg-publish":true,"permalink":"/academic/tag-system/","tags":["gardenEntry"],"dg-note-properties":{}}
---



Probability: Use $\Pr$ notation.
When you use equation by double $ instead of single $, then you need the new line.
Random: use $ to sample from a distribution ($A \xleftarrow{\$} B$)
PMF: $P$; PDF: $f$.
Expected Value: $\mathbb E$
Even though \gets and \leftarrow is equivalence, pref use \leftarrow

| Type                                   | Style                |
| -------------------------------------- | -------------------- |
| Variable                               | \mathrm              |
| Algorithms, Adv, Property              | \mathsf              |
| Scalar                                 | Lowercase            |
| Vector                                 | \mathbf, \boldsymbol |
| Matrix                                 | Uppercase            |
| sets, relations, families, adversaries | \mathcal             |

Need to refactor!!! Don't be lazy
Communication:

$$\begin{array}{lcl} 
\mathsf{Prover} & & \mathsf{Verifier} \\[4pt] 
(x = \log_g h) & & \\[6pt] 
r \xleftarrow{\$} \mathbb{Z}_p & & \\ 
a \leftarrow g^r & \xrightarrow{\quad a \quad} & \\[6pt] 
& \xleftarrow{\quad e \quad} & e \xleftarrow{\$} \mathbb{Z}_p \\[6pt]
\sigma \leftarrow ex + r & \xrightarrow{\quad \sigma \quad} & g^{\sigma} \stackrel{?}{=} h^{e} a 
\end{array}$$


| Base                                | Kind                                                              |
| ----------------------------------- | ----------------------------------------------------------------- |
| $\varepsilon_\bullet$               | error probability (something fails)                               |
| $\mathsf{Adv}^{\bullet}_{\bullet}$​ | advantage (∣Pr⁡−1/2∣\vert\Pr - 1/2\vert ∣Pr−1/2∣ or a difference) |
| $\Delta(\cdot,\cdot)$               | statistical distance                                              |


| Parameter | Meaning                |
| --------- | ---------------------- |
| $\lambda$ | Computational Security |
| $\kappa$  | Statistical Security   |


|                     |     |
| ------------------- | --- |
| Knowledge Soundness | ks  |

 $$\text{Adv}_\text{MLWE}^\text{search}(\mathcal A) = 
 \Pr\!\left[ 
 \begin{array}{l}
 s \in \chi_s^k \\
 (b - As \bmod q) \in \chi_e^m
 \end{array} 
 \;\middle |\; 
 \begin{array}{l}
 (A, b) \leftarrow \text{MLWE}(d, k, m, q, \chi_s, \chi_e) \\
 s \leftarrow \mathcal A_\text{search}(A, b)
 \end{array} \right] 
 $$


### Mathematical content

> [!definition] callout-name `definition`
> A formal definition. The green border signals "this is the canonical statement."

> [!theorem] `theorem`, `lemma`, `corollary`, `proposition`
> Provable statements, in decreasing prominence. The four share a purple/blue/teal family so they read as one visual gradient.

> [!conjecture] `conjecture`, `axiom`
> Unproven assumptions or accepted starting points. Use sparingly — flag when something is *assumed* rather than proven.

> [!proof] `proof`
> Proof body. CSS automatically appends a QED `□` marker.

### Procedural content

> [!algorithm] `algorithm`
> High-level algorithm description in prose. "BSGS proceeds in two stages…"

> [!pseudocode] `pseudocode`
> Verbatim pseudocode in a monospace block. Styled in `pseudocode-callout.css`.

### Auxiliary

> [!example] `example`
> A concrete instance: "Take $p = 11, g = 2$…"

> [!remark] `remark` · [!question] `question` · [!principle] `principle`
> Sidebar commentary, open problems, guiding ideas.

### Crypto-flavoured (new)

> [!property] `property`
> A *non-adversarial* condition a scheme must satisfy. Correctness, completeness, determinism, robustness. "PKE correctness: for all $(pk, sk)$ and all $m$, $D(sk, E(pk, m)) = m$." Title in deep-sky-blue.

> [!security] `security`
> An *adversarial* condition — no PPT attacker can do X. IND-CPA, EUF-CMA, soundness of a proof system, ZK, collision resistance. "AES-GCM is IND-CCA assuming AES is a PRP and GMAC is a PRF."

> [!construction] `construction`
> A *recipe* that takes one primitive and produces another. The body is a template, not a final algorithm tuple. "Given a PRG $G$, define a PRF $F$ by…" (GGM). "Given a Σ-protocol $\Pi$, the Fiat-Shamir transform produces a signature scheme…"

> [!scheme] `scheme`
> A *named, deployable* algorithm tuple. The body is the concrete (KeyGen, …) spec. Examples: RSA-OAEP, Schnorr signature, AES-GCM, Kyber768, ECDSA-P256.

> [!attack] `attack`
> An attack or break against a scheme. CRIME, Bleichenbacher, padding oracle.

> [!intuition] `intuition`
> The informal picture before the formal definition. "Think of a hash as a one-way pipe…"

### Scheme vs. construction — choosing the right callout

The two get conflated. A **construction** applied to a concrete primitive *produces* a **scheme**. Reach for `[!construction]` when you're describing a recipe that consumes a primitive; reach for `[!scheme]` when you're writing down the final algorithm tuple for a named, deployable object.

| Object | Callout |
|---|---|
| Definition of what a PKE / PRF / signature *is* (primitive's syntax) | `[!definition]` |
| GGM (PRG → PRF), Fiat-Shamir (Σ-protocol → signature), Encrypt-then-MAC (CPA + MAC → AE), KEM-DEM (KEM + DEM → PKE), CBC mode (PRP → CPA cipher) | `[!construction]` |
| RSA-OAEP, Schnorr signature, AES-GCM, Kyber, ECDSA-P256 | `[!scheme]` |
| Correctness: $D(sk, E(pk, m)) = m$ for all $(pk, sk), m$. Σ-protocol completeness. | `[!property]` |
| Σ-protocol soundness, ZK, IND-CPA, EUF-CMA, collision resistance — *adversarial* conditions | `[!security]` |
| "If $G$ is a secure PRG, the GGM PRF is secure" (proves the construction works) | `[!theorem]` |
| "AES-GCM has IND-CCA advantage $\le \ldots$" (concrete bound for a scheme) | `[!security]` |

### Property vs. security — the line

Both say "the scheme satisfies X." Use `[!property]` when X holds *unconditionally* in the absence of an adversary (correctness, completeness, determinism). Use `[!security]` when X is a statement about what *no PPT adversary* can do (soundness, ZK, IND-*, EUF-*, collision resistance). A typical PKE-scheme note has one `[!scheme]` block for the algorithm tuple, one `[!property]` for correctness, one `[!security]` per security notion, then theorems and proofs.

### Concrete vs. asymptotic security — the $(t, \varepsilon)$ convention

Two styles coexist in crypto literature. The vault default is **concrete**: state claims in $(t, \varepsilon)$ form.

| Callout | Style | Example |
|---|---|---|
| `[!definition]` (advantage function) | Neither — just define $\text{Adv}^{xxx}_\Pi(\mathcal{A})$ as a function | $\text{Adv}^{\text{cca}}_{\text{PKE}}(\mathcal{A}) = \lvert \Pr[b = b' : \cdots] - \tfrac{1}{2} \rvert$ |
| `[!conjecture]` (hardness) | Either; concrete preferred in PQ context | "Best $(t, \varepsilon)$ MLWE-adversary satisfies $\varepsilon \le t / 2^\lambda$" |
| `[!theorem]` (reduction) | **Always concrete** | "For any $(t, \varepsilon)$-adversary against X, there exists a $(t', \varepsilon')$-adversary against Y with $t' \le t + \Delta$, $\varepsilon' \ge \varepsilon / L$" |
| `[!security]` (derived claim) | Concrete — enables bit-security statements | "Kyber-768 is $(2^{192}, 2^{-192})$-IND-CCA assuming MLWE" |

The $(t, \varepsilon)$ form is strictly more informative: pick $t = \text{poly}(\lambda)$ and demand $\varepsilon = \text{negl}(\lambda)$ to recover the asymptotic statement. The reduction's *quantitative content* (tight vs. loose) is what makes the difference between "this scheme reaches 128 bits of security" and "this scheme reaches 80 bits of security against the same assumption." Don't lose that.

### Conjecture vs. security — the proof DAG

Hardness assumptions (M-LWE is hard, factoring is hard, DDH) and derived security claims (Kyber is IND-CCA) have *the same form*: both say "no PPT adversary has non-negligible advantage in game $G$." The split between `[!conjecture]` and `[!security]` is about **where the claim sits in the proof DAG**, not its shape.

| Callout | Position | Example |
|---|---|---|
| `[!conjecture]` | **Leaf** of the DAG — believed but not derived. No reduction backs it. | M-LWE, R-LWE, plain LWE, RSA problem, DDH, factoring |
| `[!security]` | **Non-leaf node** — derived from one or more conjectures via a reduction. | Kyber IND-CCA, RSA-OAEP IND-CCA, Schnorr EUF-CMA |
| `[!theorem]` | The reduction arrow itself, with proof. | "If M-LWE is hard, Kyber is IND-CCA." |

In `assumptions/`, the headline claim of each file should be a `[!conjecture]`, paired with a `[!definition]` of the underlying game and (optionally) a `[!theorem]` for any worst-case-to-average-case reduction that gives evidence for the conjecture. In `schemes/`, the headline security claims are `[!security]` blocks, each paired with the reduction `[!theorem]` to one or more `[!conjecture]`s.

### Casing

Always lowercase. If you write `[!Definition]` or `[!Theorem]`, the styles will not apply. (A `sed` pass already normalized existing notes.)

---





