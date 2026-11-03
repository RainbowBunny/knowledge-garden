---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/universal-hash-function-from-prefix-free-pseudorandom-function/","dg-note-properties":{"aliases":["Universal Hash Function from Prefix-Free PRF"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§7.2.2: CBC and cascade are computational UHFs).
- `⚠️ CLAUDE – verify:` — added by me, not taken from a source.

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/special function/hash function/Universal Hash Function\|Universal Hash Function]]: Import $(\mathcal K, \mathcal M, \mathcal T)$, with $\mathcal M = \mathcal X^{\leq \ell}$ and $\mathcal T = \mathcal Y$.
> - $\mathcal X$: the block set, $|\mathcal X| > 1$.
> - $\ell$: a poly-bounded length.
> - $\mathcal Y$: the output set, of super-poly size.

> [!definition] Building Blocks
> - $PF$: any [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Prefix-free PRF\|prefix-free secure PRF]] over $(\mathcal K, \mathcal X^{\leq \ell + 1}, \mathcal Y)$ that is also [[knowledge/cryptography/special function/Special Functions#Extendable\|extendable]] (universally quantified).

> [!definition] Universal Hash Function from Prefix-Free PRF
> - $t \leftarrow H(k, m)$: (Deterministic) Hash algorithm.
>     - **Input**: a key $k \in \mathcal K$ and a message $m \in \mathcal X^{\leq \ell}$.
>     - **Output**: a digest $t = PF(k, m) \in \mathcal Y$.
>
> The hash *is* the PRF, restricted to messages one block shorter than its domain. `[BS §7.2.2]`

## Security

> [!security] A computational UHF `[BS §7.2.2]`
> **Scope**
> - $PF$: extendable and prefix-free secure over $(\mathcal K, \mathcal X^{\leq \ell + 1}, \mathcal Y)$; $|\mathcal Y|$ super-poly; $|\mathcal X| > 1$.
> - $\mathcal A$: a [[knowledge/cryptography/special function/hash function/Universal Hash Function#Secure Universal Hash Function\|UHF adversary]] against $H$.
>
> ---
> **Property**
> There is a [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Secure Prefix-free PRF\|prefix-free PRF adversary]] $\mathcal B$, an elementary wrapper around $\mathcal A$ that makes two queries, with
> $$\mathsf{Adv}^{\mathsf{uhf}}_{H}(\mathcal A) \leq \mathsf{Adv}^{\mathsf{prf\text{-}pf}}_{PF}(\mathcal B) + \frac{1}{|\mathcal Y|}.$$

> [!security] A multi-query UHF `[BS §7.2.2]`
> **Scope**
> - $PF$: as above, with $|\mathcal X|$ super-poly as well.
> - $Q$: a bound with $|\mathcal X| > \ell Q$.
> - $\mathcal A$: a $Q$-query [[knowledge/cryptography/special function/hash function/Universal Hash Function#Multi-query Universal Hash Function\|multi-query UHF adversary]] against $H$.
>
> ---
> **Property**
> There is a $Q$-query prefix-free PRF adversary $\mathcal B$, an elementary wrapper around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{muhf}}_{H}(\mathcal A) \leq \mathsf{Adv}^{\mathsf{prf\text{-}pf}}_{PF}(\mathcal B) + \frac{Q^2}{2 |\mathcal Y|}.$$

## Example

### CBC and cascade

> [!corollary] CBC and cascade are computational UHFs `[BS §7.2.2]`
> **Scope**
> - $F$: a [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Secure PRF\|secure PRF]] over $(\mathcal K, \mathcal X, \mathcal Y)$; messages in $\mathcal X^{\leq \ell}$, $\ell$ poly-bounded.
> - $F_\mathrm{CBC}$: the [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#CBC Construction\|CBC construction]], with $\mathcal Y = \mathcal X$ of super-poly size.
> - $F^*$: the [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function#Cascade Construction\|cascade construction]], with $\mathcal Y = \mathcal K$.
> - $\mathcal A$: a $Q$-query multi-query UHF adversary.
>
> ---
> **Property**
> There are adversaries $\mathcal B_1, \mathcal B_2$ against $F$, elementary wrappers around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{muhf}}_{F_\mathrm{CBC}}(\mathcal A) \leq \mathsf{Adv}^{\mathsf{prf\text{-}pf}}_{F}(\mathcal B_1) + \frac{Q^2 (\ell + 1)^2 + Q^2}{2 |\mathcal Y|},$$
> $$\mathsf{Adv}^{\mathsf{muhf}}_{F^*}(\mathcal A) \leq Q (\ell + 1) \cdot \mathsf{Adv}^{\mathsf{prf\text{-}pf}}_{F}(\mathcal B_2) + \frac{Q^2}{2 |\mathcal Y|}.$$
>
> `⚠️ CLAUDE – verify:` $F$ is assumed only to be a secure PRF, and the terms $Q^2 (\ell + 1)^2$ and $Q (\ell + 1)$ look like the losses of turning a secure $F$ into a prefix-free secure $F_\mathrm{CBC}$ or $F^*$. If so, $\mathcal B_1, \mathcal B_2$ are PRF adversaries and both bounds should read $\mathsf{Adv}^{\mathsf{prf}}_{F}$. Check against the book.

## Related

### Siblings
- [[knowledge/cryptography/special function/hash function/Parallel Universal Hash Function from Pseudorandom Function\|Parallel Universal Hash Function from Pseudorandom Function]] — CBC and cascade call the PRF block after block; $F^\oplus$ calls it on all blocks at once

### Prerequisites
- [[knowledge/cryptography/special function/pseudorandom function/Pseudorandom Function\|Pseudorandom Function]], [[knowledge/cryptography/special function/hash function/Universal Hash Function\|Universal Hash Function]]
