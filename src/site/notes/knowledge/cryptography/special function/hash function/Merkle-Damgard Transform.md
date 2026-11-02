---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/merkle-damgard-transform/","dg-note-properties":{"aliases":["Merkle-Damgård Transform","Merkle-Damgard Paradigm","Merkle-Damgård Construction","MD Transform"]}}
---

Reference:
- `[BS]` — D. Boneh, V. Shoup, _A Graduate Course in Applied Cryptography_, v0.6, 2023: https://toc.cryptobook.us/ (§8.4: the Merkle–Damgård paradigm; §8.4.1: Joux's attack).
- `[Wu]` — D. J. Wu, _CS 346: Cryptography_, lecture 9, UT Austin, fall 2025: the padding encodes the message length; the proof walks back along the chain: https://www.cs.utexas.edu/~dwu4/courses/fa25/static/lecture9.pdf

## Syntax

> [!definition] Parameters
> - [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]: Import $(\mathcal M, \mathcal T)$, with $\mathcal M = \{0, 1\}^{\leq L}$ and $\mathcal T = \mathcal X$.
> - $\mathcal X$: the chaining space. $\mathcal Y = \{0, 1\}^\ell$: the block space. $L$: a poly-bounded bound on the message length.
> - $IV \in \mathcal X$: the **initial value**, a fixed public constant.
> - $PB$: the **padding block**, appended so that the padded length is a multiple of $\ell$; it contains an encoding of the length of the message `[Wu]`.
> - $m_1, \dots, m_s \in \mathcal Y$: the **message blocks**. $t_0, \dots, t_s \in \mathcal X$: the **chaining variables**.

> [!definition] Building Blocks
> - $h$: any [[knowledge/cryptography/special function/compression function/Compression Functions\|compression function]] $h : \mathcal X \times \mathcal Y \to \mathcal X$, a [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]] over $(\mathcal X \times \mathcal Y, \mathcal X)$ (universally quantified).

> [!definition] Merkle-Damgard Transform
> - $t \leftarrow H_\mathrm{MD}(M)$: (Deterministic) Hash algorithm.
>     - **Input**: a message $M \in \{0, 1\}^{\leq L}$.
>     - **Output**: a digest $t \in \mathcal X$.
>     - **Steps**:
>         1. $\hat M \leftarrow M \| PB$.
>         2. Split $\hat M = m_1 \| m_2 \| \dots \| m_s$ into $\ell$-bit blocks.
>         3. $t_0 \leftarrow IV$.
>         4. For $i = 1, \dots, s$: $t_i \leftarrow h(t_{i-1}, m_i)$.
>         5. Return $t_s$.
>
> `[BS §8.4]`

## Security

> [!security] Collision resistance is preserved `[BS §8.4]`
> **Scope**
> - $L$: poly-bounded.
> - $h$: a [[knowledge/cryptography/special function/hash function/Hash Function#Collision Resistance\|collision resistant]] hash function over $(\mathcal X \times \mathcal Y, \mathcal X)$.
> - $\mathcal A$: a collision finder against $H_\mathrm{MD}$ over $(\{0, 1\}^{\leq L}, \mathcal X)$.
>
> ---
> **Property**
> There is a collision finder $\mathcal B$ against $h$, an elementary wrapper around $\mathcal A$, with
> $$\mathsf{Adv}^{\mathsf{cr}}_{H_\mathrm{MD}}(\mathcal A) = \mathsf{Adv}^{\mathsf{cr}}_{h}(\mathcal B).$$

> [!proof] Why `[Wu]`
> Take a collision $M \neq M'$ for $H_\mathrm{MD}$. The two chains end in the same value; walk back along them, block by block, until the inputs to $h$ differ. That pair of inputs is a collision for $h$. The length in $PB$ is what guarantees such a pair: if $|M| \neq |M'|$, the last blocks already differ.

## Related

### Constructions
- [[knowledge/cryptography/special function/hash function/scheme/SHA-256\|SHA-256]] — over the [[knowledge/cryptography/special function/compression function/Davies-Meyer Compression Function\|Davies–Meyer]] compression function on SHACAL-2
- [[knowledge/cryptography/special function/hash function/scheme/MD5\|MD5]] — over its own compression function

### Siblings
- [[knowledge/cryptography/special function/hash function/Sponge Construction\|Sponge Construction]] — the other way to hash long messages: iterate a permutation over a state with a hidden capacity, rather than a compression function
- [[knowledge/cryptography/verifiable computing/commitment/scheme/Merkle Tree\|Merkle Tree]] — hashes a list as a tree rather than a chain

### Prerequisites
- [[knowledge/cryptography/special function/compression function/Compression Functions\|Compression Functions]], [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]
