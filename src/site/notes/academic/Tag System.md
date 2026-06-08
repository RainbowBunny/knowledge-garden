---
{"dg-publish":true,"permalink":"/academic/tag-system/","tags":["gardenEntry"],"dg-note-properties":{}}
---


# Tag System

Probability: $\Pr$

The vault uses **two layers** of semantic markup. They serve different jobs and shouldn't be collapsed into each other.

| Layer | Lives in | Answers | Cardinality |
|---|---|---|---|
| **Inline callouts** | Body of the note | "What *parts* are in here?" | Many per note |
| **YAML frontmatter `tags`** | Top of the note | "What *is* this note?" | One set per note |

Callouts give content typing (every definition, theorem, scheme is wrapped in a styled block). Frontmatter tags give note typing (queryable via Obsidian's tag pane and Dataview's `file.tags`).

---

## Layer 1 — Inline callouts (`> [!type]`)

All callout names are **lowercase**. Capitalized variants don't get styled — the CSS selectors are case-sensitive. Styles live in `.obsidian/snippets/math-blocks.css` and `pseudocode-callout.css`.

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

## Layer 2 — YAML frontmatter `tags`

Every note should ideally start with a frontmatter block. Hierarchical tags work natively (Obsidian renders `area/crypto/sig` as a nested tag in the tag pane, and Dataview can filter by prefix).

```yaml
---
tags:
  - domain/crypto
  - area/crypto/sig
  - kind/scheme
  - status/done
  - source/boneh-shoup
---
```

### Tag namespaces

**`domain/*`** — top-level subject:
`domain/crypto`, `domain/cs`, `domain/math`, `domain/security`, `domain/econ`, `domain/finance`

**`area/*`** — sub-area, hierarchical, mirrors folder layout:

- Crypto: `area/crypto/foundations`, `area/crypto/symmetric`, `area/crypto/mac`, `area/crypto/pke`, `area/crypto/sig`, `area/crypto/kex`, `area/crypto/kem`, `area/crypto/id`, `area/crypto/zk`, `area/crypto/threshold`, `area/crypto/mpc`, `area/crypto/he`, `area/crypto/ecc`, `area/crypto/pq/lattice`, `area/crypto/pq/code`, `area/crypto/assumptions/dlp`, `area/crypto/assumptions/lattice`, `area/crypto/assumptions/idealized`, `area/crypto/cryptanalysis`
- CS: `area/cs/foundations`, `area/cs/data-structures`, `area/cs/algorithms/dp`, `area/cs/algorithms/greedy`, `area/cs/graph`, `area/cs/computability`, `area/cs/complexity`, `area/cs/math`, `area/cs/problems`
- Math: `area/math/algebra`, `area/math/calculus`, `area/math/linear-algebra`, `area/math/number-theory`, `area/math/probability`

**`kind/*`** — what role the note plays:

| Tag | Meaning |
|---|---|
| `kind/moc` | MOC index file (links to others, no original content) |
| `kind/primitive` | Foundational primitive (PRF, hash, MAC) |
| `kind/scheme` | A concrete named scheme (RSA, Kyber, AES) |
| `kind/protocol` | An interactive protocol (Schnorr ID, ZK) |
| `kind/problem` | A hard problem / assumption (DLP, LWE) |
| `kind/attack` | A concrete attack (CRIME, Bleichenbacher) |
| `kind/theory` | Security definitions, models |
| `kind/notes` | Lecture-style scratch, not yet refined |

**`status/*`** — completion stage:

| Tag | Meaning |
|---|---|
| `status/stub` | Placeholder, mostly empty |
| `status/draft` | First pass, may have holes |
| `status/review` | Content present, needs second pass |
| `status/done` | Ready to reference / share |

**`source/*`** — textbook or origin:

`source/boneh-shoup`, `source/silverman`, `source/katz-lindell`, `source/clrs`, `source/sipser`, `source/own`, `source/lecture`, `source/paper`

---

## Examples

### A scheme note (e.g. `digital signatures/Dilithium.md`)

```yaml
---
tags:
  - domain/crypto
  - area/crypto/sig
  - area/crypto/pq/lattice     # cross-area: it's both a signature and PQ
  - kind/scheme
  - status/done
  - source/own
---
```

Body uses `[!definition]` for the math objects, `[!scheme]` for the key-gen/sign/verify triple, `[!theorem]` for the EUF-CMA reduction, `[!security]` for the concrete bound.

### A problem note (e.g. `assumptions/dlp/Discrete Logarithm Problem.md`)

```yaml
---
tags:
  - domain/crypto
  - area/crypto/hardproblem/dlp
  - kind/problem
  - status/done
  - source/boneh-shoup
---
```

Body uses `[!definition]` for the problem statement, `[!theorem]` for hardness results, `[!algorithm]` for solvers (BSGS, Pohlig-Hellman) if they're inlined.

### An MOC

```yaml
---
tags:
  - domain/crypto
  - kind/moc
  - status/done
---
```

---

## Querying

**Tag pane (sidebar):** click a hierarchical tag to filter notes — clicking `area/crypto` shows everything under crypto, clicking `area/crypto/sig` narrows to signatures.

**Dataview** — show every signature scheme:

````markdown
| File | Tags | Modified |
| ---- | ---- | -------- |

{ .block-language-dataview}
````

**Dataview** — show every theorem in the crypto folder:

````markdown
| Note | Theorems |
| ---- | -------- |

{ .block-language-dataview}
````

---

## Migration plan

The tagging is opt-in. You don't need to backfill every note before it's useful. A reasonable rollout:

1. Start with MOCs: add `kind/moc` + the appropriate `domain/*` and `status/done`. ~20 files.
2. As you touch any note for refactoring or expansion, add its frontmatter then.
3. After a month or two, run a `grep` audit for notes still missing `tags:` and decide whether to bulk-tag the largest folders.

The callouts are already in place across the vault — the new types (`security`, `construction`, `scheme`, `attack`, `intuition`) just need to be used going forward; existing notes are unchanged.
