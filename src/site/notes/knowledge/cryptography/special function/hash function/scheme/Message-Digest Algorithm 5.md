---
{"dg-publish":true,"permalink":"/knowledge/cryptography/special-function/hash-function/scheme/message-digest-algorithm-5/","dg-note-properties":{"aliases":["MD5","MD5 Message-Digest Algorithm"]}}
---

Reference:
- `[RFC1321]` — R. Rivest, _The MD5 Message-Digest Algorithm_, RFC 1321, 1992: §1 (128-bit digest), §3.1–3.2 (padding, 512-bit blocks), §3.3 (initial buffer), §3.4 (the feed-forward $A = A + AA$): https://www.rfc-editor.org/rfc/rfc1321
- `[WFLY04]` — X. Wang, D. Feng, X. Lai, H. Yu, _Collisions for Hash Functions MD4, MD5, HAVAL-128 and RIPEMD_, ePrint 2004/199: https://eprint.iacr.org/2004/199
- `[SLW07]` — M. Stevens, A. Lenstra, B. de Weger, _Chosen-Prefix Collisions for MD5 and Colliding X.509 Certificates for Different Identities_, EUROCRYPT 2007; ePrint 2006/360 (abstract): https://eprint.iacr.org/2006/360
- `[Wu]` — D. J. Wu, _CS 346: Cryptography_, lecture 9, UT Austin, fall 2025: MD5 is a Merkle–Damgård hash: https://www.cs.utexas.edu/~dwu4/courses/fa25/static/lecture9.pdf
- More collisions and file formats that hide them: A. Albertini, M. Stevens, https://github.com/corkami/collisions

## Scheme

Reference Name: $\mathrm{MD5}$
Instantiates:: [[knowledge/cryptography/special function/hash function/Hash Function\|Hash Function]]

> [!definition] Parameters
> - Digest and chaining value: $128$ bits, four 32-bit words $A, B, C, D$ `[RFC1321 §1, §3.3]`.
> - Message blocks: $512$ bits. Padding: a $1$ bit, then $0$ bits up to $448 \bmod 512$, then the length in 64 bits `[RFC1321 §3.1–3.2]`.

> [!definition] Building Blocks
> - [[knowledge/cryptography/special function/hash function/Merkle-Damgard Transform\|Merkle-Damgard Transform]] — over a compression function that ends by adding the incoming chaining value to the result, word by word: $A = A + AA$, … `[RFC1321 §3.4]` `[Wu]`

## Cryptanalysis

> [!attack] Collisions `[WFLY04]`
> Wang, Feng, Lai and Yu found collisions for MD5 with its original initial value: pairs of two-block messages $M_0 \| M_1$ and $M_0' \| M_1'$. Finding $(M_0, M_0')$ took about one hour on an IBM P690, and the second blocks 15 seconds to 5 minutes. The method works for any given initial value.

> [!example] A colliding pair — the second pair of `[WFLY04]`
> Two 128-byte messages that differ in 6 bytes and have the same MD5 digest, `79054025255fb1a26e4bc422aef54eb4`:
> ```python
> block1 = bytes.fromhex("d131dd02c5e6eec4693d9a0698aff95c2fcab58712467eab4004583eb8fb7f8955ad340609f4b30283e488832571415a085125e8f7cdc99fd91dbdf280373c5bd8823e3156348f5bae6dacd436c919c6dd53e2b487da03fd02396306d248cda0e99f33420f577ee8ce54b67080a80d1ec69821bcb6a8839396f9652b6ff72a70")
> block2 = bytes.fromhex("d131dd02c5e6eec4693d9a0698aff95c2fcab50712467eab4004583eb8fb7f8955ad340609f4b30283e4888325f1415a085125e8f7cdc99fd91dbd7280373c5bd8823e3156348f5bae6dacd436c919c6dd53e23487da03fd02396306d248cda0e99f33420f577ee8ce54b67080280d1ec69821bcb6a8839396f965ab6ff72a70")
> ```
> `[WFLY04]` prints the messages as little-endian 32-bit words, starting `2dd31d1`, and the chaining value before padding, `8d5e7019 …`.

> [!attack] A common suffix keeps the collision — Merkle–Damgård
> The two messages above have the same length, a whole number of blocks, and collide in the full chaining value. Every later block then sees the same input, and the padding depends only on the length, so for every suffix $S$,
> $$\mathrm{MD5}(M \| S) = \mathrm{MD5}(M' \| S).$$
> A common *prefix* breaks this pair: after a prefix, the chaining value entering the two blocks is no longer the one the pair was found for.

> [!attack] Chosen-prefix collisions `[SLW07]`
> Given any two prefixes $m_1, m_2$, find $b_1, b_2$ with
> $$\mathrm{MD5}(m_1 \| b_1) = \mathrm{MD5}(m_2 \| b_2),$$
> at a cost of about $2^{52}$ calls to the compression function (ePrint version). With it, Stevens, Lenstra and de Weger built two MD5-based X.509 certificates with identical signatures but different public keys. The prefixes may differ — what the previous attack cannot do.

## Related

### Siblings
- [[knowledge/cryptography/special function/hash function/scheme/Secure Hash Algorithm 256\|Secure Hash Algorithm 256]] — also Merkle–Damgård, with a 256-bit digest
- [[knowledge/cryptography/cryptanalysis/Collision Algorithms\|Collision Algorithms]] — generic collision search, which these attacks beat
